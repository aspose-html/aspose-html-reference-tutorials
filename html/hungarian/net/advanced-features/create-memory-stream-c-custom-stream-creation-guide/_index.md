---
category: general
date: 2025-12-27
description: Hozzon létre memóriafolyamot C#‑ban gyorsan egy lépésről‑lépésre útmutatóval.
  Tanulja meg, hogyan hozhat létre folyamot, kezelje az erőforrásokat, és valósítsa
  meg az egyedi folyam létrehozását a .NET‑ben.
draft: false
keywords:
- create memory stream c#
- how to create stream
- how to handle resources
- custom stream creation
language: hu
og_description: Hozzon létre memóriafolyamot C#-ban néhány másodperc alatt. Ez az
  útmutató bemutatja, hogyan hozhat létre folyamot, kezelheti az erőforrásokat, és
  építhet egyedi folyamkészítést a modern .NET API-kkal.
og_title: Memóriafolyam létrehozása C# – Teljes egyedi stream útmutató
tags:
- stream
- csharp
- .net
- resource-handling
title: Memóriastream létrehozása C# – Egyéni stream létrehozási útmutató
url: /hu/net/advanced-features/create-memory-stream-c-custom-stream-creation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Memory stream létrehozása c# – Egyéni stream létrehozás útmutatója

Valaha szükséged volt **memory stream létrehozása c#**-ra, de nem tudtad, melyik API-t válaszd? Nem vagy egyedül. Sok régi projektben megtalálod a `IOutputStorage`-t, míg az újabb kódbázisok a `ResourceHandler`-t részesítik előnyben. Bármelyik is legyen, a cél ugyanaz: egy `Stream` előállítása, amelyet a keretrendszered felhasználhat.

Ebben az útmutatóban megtanulod, hogyan **hozz létre stream** objektumokat, hogyan **kezelj biztonságosan erőforrásokat**, és elsajátítod az **egyéni stream létrehozását** a könyvtár pre‑24.2 és 24.2+ verzióihoz egyaránt. A végére egy működő példát kapsz, amelyet bármely .NET megoldásba beilleszthetsz – nincsenek rejtett hivatkozások, csak tiszta C#.

## Mit fogsz elsajátítani

- A régi `IOutputStorage` minta és a modern `ResourceHandler` megközelítés közötti világos összehasonlítás.  
- Teljes, másolásra kész kód, amely .NET 6+ (vagy régebbi, ha szükséges) verzióval fordul.  
- Tippek a szélhelyzetekhez, például a stream-ek felszabadítása, nagy adatmennyiségek kezelése és az egyéni stream tesztelése.  

> **Pro tipp:** Ha a .NET 8-ra célozol, az újabb `ResourceHandler` beépített aszinkron támogatást nyújt, amely ezredmásodperceket takaríthat meg a nagy áteresztőképességű szcenáriókban.

---

## Memory stream létrehozása c# – Örökölt megközelítés (pre‑24.2)

Amikor egy régebbi könyvtárverzióval vagy elakadva, a teljesítendő szerződés a `IOutputStorage`. Az interfész csak egy metódust kér, amely egy adott erőforrásnévhez `Stream`-et ad vissza.

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

### Miért működik ez

- **Interface contract** – A keretrendszer meghívja a `CreateStream`-et, amikor kimenetet kell írnia.  
- **Flexibility** – Mivel egy `Stream`-et adsz vissza, később kicserélheted a `MemoryStream`-et `FileStream`-re vagy akár egy egyéni pufferelt stream-re anélkül, hogy a többi kódot módosítanád.  
- **Resource safety** – A hívó felelős a visszaadott stream felszabadításáért, ezért a metódusban nem hívunk `Dispose`-t.  

### Gyakori buktatók

| Probléma | Mi történik | Megoldás |
|----------|--------------|----------|
| Lezárt stream visszaadása | A fogyasztók `ObjectDisposedException`-t kapnak íráskor. | Győződj meg róla, hogy a stream **nyitott** amikor átadod. |
| `Position = 0` beállításának elfelejtése írás után | Az adatok üresnek tűnnek későbbi olvasáskor. | Hívja a `stream.Seek(0, SeekOrigin.Begin)`-et a visszaadás előtt, ha előre feltöltöd. |
| Nagy `MemoryStream` használata nagy fájlokhoz | Memóriahiányos összeomlások. | Válts át egy ideiglenes `FileStream`-re vagy egy egyéni pufferelt stream-re. |

---

## Memory stream létrehozása c# – Modern megközelítés (24.2+)

A 24.2-es verziótól a könyvtár bevezette a `ResourceHandler`-t. Az interfész helyett most egy bázisosztályból öröklődsz, és felülírsz egyetlen metódust. Ez tisztább, aszinkron‑barát belépési pontot biztosít.

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

### Miért érdemes a `ResourceHandler`-t használni

- **Async support** – A `HandleResourceAsync` metódus lehetővé teszi I/O végrehajtását szálak blokkolása nélkül.  
- **Built‑in error handling** – A bázisosztály elkapja a kivételeket, és keretrendszer‑specifikus hibakódokká alakítja őket.  
- **Future‑proof** – Az újabb kiadások hook-okat (pl. naplózás, telemetria) adnak hozzá, amelyek csak a handler mintával működnek.  

### Szélhelyzetek kezelése

1. **Disposal** – A keretrendszer felszabadítja a stream-et, miután befejeződött, de ha egy másik felszabadítható objektumot (például `FileStream`) csomagolsz, akkor a metóduson belül egy `using` blokkot kell alkalmaznod, és egy olyan wrappert kell visszaadnod, amely továbbítja a `Dispose`-t.  
2. **Large payloads** – Ha > 100 MB méretű terhelésre számítasz, cseréld le a `MemoryStream`-et egy `FileStream`-re, amely egy ideiglenes fájlra mutat. Példa:  

   ```csharp
   return new FileStream(Path.GetTempFileName(),
                         FileMode.Create,
                         FileAccess.ReadWrite,
                         FileShare.None,
                         bufferSize: 81920,
                         useAsync: true);
   ```

3. **Testing** – Egységteszteld a handleredet úgy, hogy egy mock `IServiceProvider`-t injektálsz, ha a bázisosztály a DI-ből szolgáltatásokat kér. Ellenőrizd, hogy a `HandleResource` olyan stream-et ad vissza, amelybe lehet írni és amelyből olvasni lehet.  

## Hogyan hozz létre stream-et – Gyors segédlet

| Forgatókönyv | Ajánlott API | Minta kód |
|--------------|--------------|-----------|
| Egyszerű memóriaadat | `MemoryStream` | `new MemoryStream()` |
| Nagy ideiglenes fájlok | `FileStream` (temp) | `new FileStream(Path.GetTempFileName(), FileMode.Create, FileAccess.ReadWrite, FileShare.None, 81920, true)` |
| Hálózati forrás | `NetworkStream` | `new NetworkStream(socket)` |
| Egyéni pufferelés | Derive from `Stream` | See [Microsoft docs] for custom stream implementation |

> **Megjegyzés:** Mindig állítsd be a `stream.Position = 0`-t a visszaadás előtt, ha előre feltöltöd a stream-et; különben a downstream olvasók üresnek fogják gondolni a stream-et.

## Kép illusztráció

![Diagram showing create memory stream c# process](https://example.com/images/create-memory-stream-diagram.png)

*Alt text:* diagram a memory stream létrehozásának c# folyamatáról

## Teljes futtatható példa

Az alábbiakban egy minimális konzolalkalmazás látható, amely bemutatja mind az örökölt, mind a modern megközelítést. A kódot egyszerűen másold be egy új .NET 6 konzolprojektbe, és futtasd változtatás nélkül.

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

**Várható kimenet**

```
Hello from legacy API!
Hello from modern API!
Hello from async API!
```

A program három módot mutat be arra, hogyan **hozz létre stream**-et: a régi `IOutputStorage`, az új szinkron `HandleResource`, és az aszinkron `HandleResourceAsync`. Mindhárom `MemoryStream`-et ad vissza, bizonyítva, hogy az egyéni stream létrehozás működik, függetlenül attól, hogy melyik verziót célozod.

## Gyakran ismételt kérdések (GYIK)

**K: Kell hívnom a `Dispose`-t a visszakapott stream-en?**  
V: A keretrendszer (vagy a hívó kód) felelős a felszabadításért. Ha egy másik felszabadítható objektumot csomagolsz a visszaadott stream-be, győződj meg róla, hogy továbbítja a `Dispose` hívást.

**K: Visszaadhatok csak olvasható stream-et?**  
V: Igen, de a szerződés általában írható stream-et vár. Ha csak olvasni kell, implementáld a `CanWrite => false`-t, és dokumentáld a korlátozást.

**K: Mi van, ha az adataim nagyobbak, mint a rendelkezésre álló RAM?**  
V: Cseréld le egy ideiglenes fájlon alapuló `FileStream`-re, vagy implementálj egy egyéni pufferelt stream-et, amely darabokban ír a lemezre.

**K: Van teljesítménykülönbség a két megközelítés között?**  
V: A modern `ResourceHandler` kis extra terhet jelent a bázisosztály logikája miatt, de az aszinkron változat jelentősen javíthatja a teljesítményt magas párhuzamosság esetén.

## Összegzés

Most lefedtük a **memory stream létrehozása c#** minden szempontját, amellyel a gyakorlatban találkozhatsz. Most már tudod, hogyan **hozz létre stream**-et a régi `IOutputStorage` mintával és az új `ResourceHandler` osztállyal, valamint láttál gyakorlati tippeket arra, hogyan **kezelj erőforrásokat** felelősségteljesen, és hogyan bővítsd a mintát **egyéni stream létrehozással** nagy fájlok vagy aszinkron szcenáriók esetén.

Ready for

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}