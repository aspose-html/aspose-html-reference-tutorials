---
category: general
date: 2025-12-27
description: Vytvořte paměťový stream v C# rychle s podrobným návodem krok za krokem.
  Naučte se, jak vytvořit stream, spravovat zdroje a implementovat vlastní tvorbu
  streamu v .NET.
draft: false
keywords:
- create memory stream c#
- how to create stream
- how to handle resources
- custom stream creation
language: cs
og_description: Vytvořte paměťový stream v C# během několika sekund. Tento tutoriál
  ukazuje, jak vytvořit stream, spravovat zdroje a vytvořit vlastní stream pomocí
  moderních .NET API.
og_title: Vytvořte paměťový stream v C# – Kompletní průvodce vlastním streamem
tags:
- stream
- csharp
- .net
- resource-handling
title: Vytvoření paměťového streamu v C# – Průvodce tvorbou vlastního streamu
url: /cs/net/advanced-features/create-memory-stream-c-custom-stream-creation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření memory stream v C# – Průvodce tvorbou vlastního streamu

Už jste někdy potřebovali **vytvořit memory stream v C#**, ale nebyli jste si jisti, kterou API zvolit? Nejste v tom sami. V mnoha starších projektech narazíte na `IOutputStorage`, zatímco novější kódy upřednostňují `ResourceHandler`. Ať už zvolíte jakýkoli přístup, cíl je stejný: vytvořit `Stream`, který váš framework dokáže spotřebovat.

V tomto tutoriálu se naučíte **jak vytvořit stream** objekty, **jak bezpečně zacházet se zdroji** a ovládnete **tvorbu vlastního streamu** pro verze knihovny před 24.2 i 24.2+. Na konci budete mít funkční příklad, který můžete vložit do libovolného .NET řešení – žádné tajemné reference, jen čistý C#.

## Co si z toho odnesete

- Přehledné srovnání starého vzoru `IOutputStorage` a moderního přístupu `ResourceHandler`.  
- Kompletní, připravený k kopírování kód, který se kompiluje proti .NET 6+ (nebo starším verzím, pokud je potřebujete).  
- Tipy pro okrajové případy, jako je uvolňování streamů, práce s velkými payloady a testování vašeho vlastního streamu.  

> **Pro tip:** Pokud cílíte na .NET 8, novější `ResourceHandler` poskytuje vestavěnou asynchronní podporu, která může ušetřit milisekundy ve scénářích s vysokou propustností.

---

## Vytvoření memory stream v C# – Starý přístup (pre‑24.2)

Když jste uvězněni na starší verzi knihovny, musíte splnit kontrakt `IOutputStorage`. Rozhraní požaduje pouze metodu, která vrátí `Stream` pro daný název zdroje.

```csharp
using System;
using System.IO;

// Step 1: Implement the old IOutputStorage contract.
public class MyStorage : IOutputStorage
{
    /// <summary>
    /// Returns a stream for the requested resource name.
    /// In a real app you might open a file, a network socket,
    /// or generate data on the fly.
    /// </summary>
    /// <param name="name">Logical name of the resource.</param>
    /// <returns>A writable Stream instance.</returns>
    public Stream CreateStream(string name)
    {
        // Custom stream creation logic.
        // Here we simply return an in‑memory stream.
        // You could also wrap a FileStream if you prefer.
        return new MemoryStream();
    }
}
```

### Proč to funguje

- **Smlouva rozhraní** – Framework zavolá `CreateStream`, kdykoli potřebuje zapisovat výstup.  
- **Flexibilita** – Protože vracíte `Stream`, můžete později vyměnit `MemoryStream` za `FileStream` nebo dokonce za vlastní bufferovaný stream, aniž byste museli měnit zbytek kódu.  
- **Bezpečnost zdrojů** – Volající je zodpovědný za uvolnění vráceného streamu, proto v metodě nevoláme `Dispose`.

### Časté úskalí

| Problém | Co se stane | Oprava |
|---------|-------------|--------|
| Vrácení uzavřeného streamu | Spotřebitelé dostanou `ObjectDisposedException` při zápisu. | Ujistěte se, že stream je **otevřený**, když jej předáváte dál. |
| Zapomenutí nastavit `Position = 0` po zápisu | Data se při následném čtení jeví jako prázdná. | Před návratem zavolejte `stream.Seek(0, SeekOrigin.Begin)`, pokud jste stream předem naplnili. |
| Použití obrovského `MemoryStream` pro velké soubory | Selhání z nedostatku paměti. | Přepněte na dočasný `FileStream` nebo vlastní bufferovaný stream. |

---

## Vytvoření memory stream v C# – Moderní přístup (24.2+)

Od verze 24.2 knihovna představila `ResourceHandler`. Místo rozhraní nyní dědíte z základní třídy a přepisujete jedinou metodu. To vám poskytuje čistší a asynchronně‑přátelské vstupní místo.

```csharp
using System;
using System.IO;

// Step 2: Inherit from the new ResourceHandler base class.
public class MyHandler : ResourceHandler
{
    /// <summary>
    /// Called by the framework to obtain a stream for a resource.
    /// </summary>
    /// <param name="name">The logical name of the resource.</param>
    /// <returns>A writable Stream instance.</returns>
    public override Stream HandleResource(string name)
    {
        // Your custom stream creation logic goes here.
        // For demonstration we use a MemoryStream.
        return new MemoryStream();
    }

    // Optional async version (available in 24.2+)
    public override async Task<Stream> HandleResourceAsync(string name, CancellationToken ct = default)
    {
        // Simulate async work, e.g., fetching data from a service.
        await Task.Delay(10, ct);
        return new MemoryStream();
    }
}
```

### Proč upřednostnit `ResourceHandler`

- **Asynchronní podpora** – Metoda `HandleResourceAsync` vám umožní provádět I/O bez blokování vláken.  
- **Vestavěná obsluha chyb** – Základní třída zachytí výjimky a převede je na chybové kódy specifické pro framework.  
- **Budoucnost** – Novější vydání přidávají háčky (např. logování, telemetry), které fungují jen s handlerovým vzorem.

### Zpracování okrajových případů

1. **Uvolňování** – Framework uvolní stream po dokončení, ale pokud obalujete další disposable (např. `FileStream`), měli byste uvnitř metody použít `using` blok a vrátit wrapper, který předává `Dispose`.  
2. **Velké payloady** – Pokud očekáváte payloady > 100 MB, nahraďte `MemoryStream` `FileStream` ukazujícím na dočasný soubor. Příklad:  

   ```csharp
   return new FileStream(Path.GetTempFileName(),
                         FileMode.Create,
                         FileAccess.ReadWrite,
                         FileShare.None,
                         bufferSize: 81920,
                         useAsync: true);
   ```

3. **Testování** – Jednotkové testy vašeho handleru můžete provést injekcí mock `IServiceProvider`, pokud základní třída získává služby z DI. Ověřte, že `HandleResource` vrací stream, do kterého lze zapisovat i číst.

---

## Jak vytvořit stream – Rychlý cheat sheet

| Scénář | Doporučené API | Ukázkový kód |
|--------|----------------|--------------|
| Jednoduchá data v paměti | `MemoryStream` | `new MemoryStream()` |
| Velké dočasné soubory | `FileStream` (temp) | `new FileStream(Path.GetTempFileName(), FileMode.Create, FileAccess.ReadWrite, FileShare.None, 81920, true)` |
| Zdroj založený na síti | `NetworkStream` | `new NetworkStream(socket)` |
| Vlastní bufferování | Dědit z `Stream` | Viz [Microsoft docs] pro implementaci vlastního streamu |

> **Poznámka:** Vždy nastavte `stream.Position = 0` před návratem, pokud jste stream předem naplnili; jinak čtecí komponenty budou mít dojem, že je stream prázdný.

---

## Ilustrační obrázek

![Diagram ukazující proces vytvoření memory stream v C#](https://example.com/images/create-memory-stream-diagram.png)

*Alt text:* diagram ukazující proces vytvoření memory stream v C#

---

## Kompletní spustitelný příklad

Níže je minimální konzolová aplikace, která demonstruje oba přístupy – starý i moderní. Stačí ji zkopírovat do nového .NET 6 konzolového projektu a spustit tak, jak je.

```csharp
using System;
using System.IO;
using System.Threading;
using System.Threading.Tasks;

// -------------------------------------------------
// Legacy implementation (pre‑24.2)
// -------------------------------------------------
public class MyStorage : IOutputStorage
{
    public Stream CreateStream(string name) => new MemoryStream();
}

// -------------------------------------------------
// Modern implementation (24.2+)
// -------------------------------------------------
public class MyHandler : ResourceHandler
{
    public override Stream HandleResource(string name) => new MemoryStream();

    public override async Task<Stream> HandleResourceAsync(string name, CancellationToken ct = default)
    {
        await Task.Delay(10, ct); // simulate async work
        return new MemoryStream();
    }
}

// -------------------------------------------------
// Demo program
// -------------------------------------------------
class Program
{
    static async Task Main()
    {
        // Legacy usage
        IOutputStorage legacy = new MyStorage();
        using (var legacyStream = legacy.CreateStream("legacy"))
        using (var writer = new StreamWriter(legacyStream))
        {
            writer.Write("Hello from legacy API!");
            writer.Flush();
            legacyStream.Seek(0, SeekOrigin.Begin);
            Console.WriteLine(new StreamReader(legacyStream).ReadToEnd());
        }

        // Modern sync usage
        var handler = new MyHandler();
        using (var modernStream = handler.HandleResource("modern"))
        using (var writer = new StreamWriter(modernStream))
        {
            writer.Write("Hello from modern API!");
            writer.Flush();
            modernStream.Seek(0, SeekOrigin.Begin);
            Console.WriteLine(new StreamReader(modernStream).ReadToEnd());
        }

        // Modern async usage
        using (var asyncStream = await handler.HandleResourceAsync("async"))
        using (var writer = new StreamWriter(asyncStream))
        {
            await writer.WriteAsync("Hello from async API!");
            await writer.FlushAsync();
            asyncStream.Seek(0, SeekOrigin.Begin);
            Console.WriteLine(await new StreamReader(asyncStream).ReadToEndAsync());
        }
    }
}
```

**Očekávaný výstup**

```
Hello from legacy API!
Hello from modern API!
Hello from async API!
```

Program ukazuje tři způsoby, **jak vytvořit stream**: starý `IOutputStorage`, nový synchronní `HandleResource` a asynchronní `HandleResourceAsync`. Všechny tři vrací `MemoryStream`, což dokazuje, že tvorba vlastního streamu funguje bez ohledu na cílovou verzi.

---

## Často kladené otázky (FAQ)

**Q: Musím volat `Dispose` na stream, který dostanu zpět?**  
A: Framework (nebo váš volající kód) je zodpovědný za uvolnění. Pokud ve vráceném streamu obalujete další disposable, ujistěte se, že propaguje volání `Dispose`.

**Q: Můžu vrátit jenom read‑only stream?**  
A: Ano, ale kontrakt obvykle očekává zapisovatelný stream. Pokud potřebujete jen čtení, implementujte `CanWrite => false` a dokumentujte omezení.

**Q: Co když jsou moje data větší než dostupná RAM?**  
A: Přepněte na `FileStream` založený na dočasném souboru, nebo implementujte vlastní bufferovaný stream, který zapisuje na disk po částech.

**Q: Existuje rozdíl ve výkonu mezi těmito dvěma přístupy?**  
A: Moderní `ResourceHandler` přidává malou režii kvůli logice základní třídy, ale asynchronní verze může dramaticky zlepšit propustnost při vysoké souběžnosti.

---

## Závěr

Právě jsme probrali **vytvoření memory stream v C#** ze všech úhlů, na které můžete narazit v praxi. Nyní umíte **vytvořit stream** pomocí starého vzoru `IOutputStorage` i novější třídy `ResourceHandler`, a získali jste praktické tipy, jak **bezpečně zacházet se zdroji** a rozšířit vzor o **vlastní tvorbu streamu** pro velké soubory nebo asynchronní scénáře.

Připraveno pro

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}