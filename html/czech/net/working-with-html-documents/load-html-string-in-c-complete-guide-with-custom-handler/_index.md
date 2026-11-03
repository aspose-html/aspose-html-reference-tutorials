---
category: general
date: 2026-08-03
description: Načtěte řetězec HTML v C# a vytvořte vlastní obslužný mechanismus pro
  uložení HTMLDocument. Naučte se, jak uložit HTMLDocument s vlastním zpracováním
  zdrojů.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- load html string
- create custom handler
- how to save htmldocument
- custom resource handling
language: cs
lastmod: 2026-08-03
og_description: Načtěte řetězec HTML v C# a použijte vlastní handler pro uložení HTMLDocument.
  Tento tutoriál ukazuje kompletní implementaci a osvědčené postupy.
og_image_alt: Screenshot showing load html string code with custom handler in C#
og_title: Načtení HTML řetězce v C# – krok za krokem průvodce vlastním handlerem
schemas:
- author: Aspose
  dateModified: '2026-08-03'
  description: Load html string in C# and create custom handler to save HTMLDocument.
    Learn how to save HTMLDocument with custom resource handling.
  headline: Load html string in C# – complete guide with custom handler
  type: TechArticle
- description: Load html string in C# and create custom handler to save HTMLDocument.
    Learn how to save HTMLDocument with custom resource handling.
  name: Load html string in C# – complete guide with custom handler
  steps:
  - name: Common pitfalls
    text: '| Issue | Why it happens | Fix | |-------|----------------|-----| | `htmlContent`
      is `null` | The string variable was never assigned. | Validate before creating
      the document: `if (htmlContent == null) throw new ArgumentNullException(nameof(htmlContent));`
      | | Encoding problems | The library assumes '
  - name: Extending the handler for file output
    text: 'If you prefer to write each resource to a specific folder, modify the method
      as follows:'
  - name: Verifying the result
    text: 'If you used the file‑system version of `MyHandler`, you should see an `output`
      folder with the original HTML file and any referenced assets. For the `MemoryStream`
      version, you can inspect the stream length to confirm data was written:'
  - name: Saving to a `MemoryStream` for in‑memory processing
    text: 'If you need the final HTML as a string or want to send it over HTTP without
      touching disk, replace `MyHandler` with a version that returns a shared `MemoryStream`:'
  - name: Handling large resources safely
    text: When dealing with large images or PDFs, avoid loading the entire file into
      memory. Instead, return a `FileStream` that writes directly to disk, as shown
      earlier. This prevents `OutOfMemoryException` in high‑throughput scenarios.
  - name: Thread‑safety considerations
    text: '`HTMLDocument` instances are **not** thread‑safe. If you need to process
      multiple HTML strings concurrently, create a separate `HTMLDocument` and `MyHandler`
      per thread, or synchronize access with a `lock`.'
  - name: Disposing streams
    text: Both `HTMLDocument.Save` and `ResourceHandler.HandleResource` may return
      streams that need disposal. In the examples above, the library disposes the
      streams automatically after writing. If you manage streams yourself (e.g., opening
      a `FileStream` before calling `Save`), wrap them in `using` statemen
  type: HowTo
tags:
- HTMLDocument
- C#
- resource handling
title: Načíst HTML řetězec v C# – kompletní průvodce s vlastním handlerem
url: /cs/net/working-with-html-documents/load-html-string-in-c-complete-guide-with-custom-handler/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Načtení HTML řetězce v C# – kompletní průvodce s vlastním handlerem

Pokud potřebujete **načíst html řetězec** v aplikaci C#, tento tutoriál vám přesně ukáže, jak to provést a jak **vytvořit vlastní handler** pro správu zdrojů. Také se naučíte **jak uložit htmldocument** pomocí **vlastní manipulace se zdroji**, takže každý obrázek, CSS soubor nebo skript bude zapsán přesně tam, kde chcete.

Provedeme vás celým procesem — od převodu surového HTML řetězce na objekt `HTMLDocument` až po implementaci podtřídy `ResourceHandler`, která řídí, kam se každý zdroj uloží. Na konci budete mít samostatný, připravený pro produkci příklad, který můžete vložit do libovolného .NET projektu.

## Požadavky

- .NET 6.0 nebo novější (kód také funguje na .NET Framework 4.7+)
- Reference na knihovnu, která poskytuje `HTMLDocument`, `ResourceHandler` a `ResourceInfo` (např. *HtmlRenderer* nebo podobná HTML‑to‑PDF/DOM knihovna)
- Základní znalost syntaxe C# a streamů

> **Tip:** Pokud používáte Visual Studio, povolte *nullable reference types* (`<Nullable>enable</Nullable>`), abyste včas zachytili chyby související s null.

## Jak načíst html řetězec do HTMLDocument

Prvním krokem je převést prostý HTML řetězec na objekt `HTMLDocument`, se kterým může knihovna pracovat.

```csharp
using System;
using System.IO;

// Assume the library namespace is HtmlProcessing
using HtmlProcessing;   // <-- replace with the actual namespace

// 1️⃣ Load the HTML string
string htmlContent = "<html><body><h1>Hello, World!</h1></body></html>";

// 2️⃣ Create the document instance from the string
HTMLDocument htmlDoc = new HTMLDocument(htmlContent);
```

**Proč je to důležité:**  
`HTMLDocument` parsuje značkování, vytváří strom DOM a připravuje zdroje (obrázky, styly atd.) pro pozdější uložení. Přímé předání řetězce eliminuje potřebu dočasných souborů a udržuje tok práce v paměti.

### Časté úskalí

| Problém | Proč k tomu dochází | Řešení |
|-------|----------------|-----|
| `htmlContent` je `null` | Proměnná řetězce nebyla nikdy přiřazena. | Ověřte před vytvořením dokumentu: `if (htmlContent == null) throw new ArgumentNullException(nameof(htmlContent));` |
| Problémy s kódováním | Knihovna předpokládá UTF‑8, ale zdroj používá jiné kódování. | Poskytněte explicitní přetížení `Encoding`, pokud je k dispozici, nebo zajistěte správné dekódování řetězce. |

## Vytvoření vlastního handleru pro správu zdrojů

**Vlastní handler zdrojů** vám dává plnou kontrolu nad tím, jak knihovna zapisuje externí zdroje (obrázky, CSS, fonty). Níže je minimální implementace, která zapisuje každý zdroj do `MemoryStream`. Tělo můžete nahradit logikou souborového systému, cloudovým úložištěm nebo jakýmkoli jiným cílem.

```csharp
/// <summary>
/// Custom handler that writes each resource into a memory stream.
/// </summary>
class MyHandler : ResourceHandler
{
    /// <summary>
    /// Called by HTMLDocument for every external resource.
    /// </summary>
    /// <param name="info">Metadata about the resource (e.g., URL, MIME type).</param>
    /// <returns>A writable stream where the resource data will be stored.</returns>
    public override Stream HandleResource(ResourceInfo info)
    {
        // For demonstration we use a MemoryStream.
        // In real scenarios you might open a FileStream or upload to cloud storage.
        return new MemoryStream();
    }
}
```

**Proč potřebujete vlastní handler:**  
Výchozí handler často zapisuje zdroje do dočasné složky, což může být z bezpečnostních nebo výkonnostních důvodů nežádoucí. Přepsáním `HandleResource` určíte přesně, kde a jak je každý bajt uložen.

### Rozšíření handleru pro výstup do souboru

Pokud dáváte přednost zápisu každého zdroje do konkrétní složky, upravte metodu následovně:

```csharp
public override Stream HandleResource(ResourceInfo info)
{
    string outputDir = Path.Combine(Environment.CurrentDirectory, "output");
    Directory.CreateDirectory(outputDir);

    // Generate a safe file name based on the resource URL.
    string fileName = Path.GetFileName(new Uri(info.Uri).LocalPath);
    string filePath = Path.Combine(outputDir, fileName);

    // Return a FileStream that the library will write into.
    return new FileStream(filePath, FileMode.Create, FileAccess.Write);
}
```

## Jak uložit htmldocument pomocí vlastního handleru

Nyní, když máme jak instanci `HTMLDocument`, tak implementaci `MyHandler`, můžeme dokument uložit. Metoda `Save` přijímá libovolnou podtřídu `ResourceHandler`, což vám umožní vložit vlastní logiku.

```csharp
// 3️⃣ Instantiate the custom handler
var handler = new MyHandler();

// 4️⃣ Save the document; the handler decides where resources go
htmlDoc.Save(handler);
```

Když se spustí `Save`, knihovna provede:

1. Projde strom DOM.  
2. Detekuje externí zdroje (např. `<img src="logo.png">`).  
3. Zavolá `handler.HandleResource` pro každý zdroj.  
4. Zapíše data zdroje do vráceného streamu.  
5. Dokončí hlavní HTML výstup (často jako samostatný soubor nebo stream).

### Ověření výsledku

Pokud jste použili verzi `MyHandler` pro souborový systém, měli byste vidět složku `output` s původním HTML souborem a všemi odkazovanými assety. Pro verzi `MemoryStream` můžete zkontrolovat délku streamu, abyste potvrdili, že data byla zapsána:

```csharp
using (var stream = handler.HandleResource(new ResourceInfo { Uri = "data:," }))
{
    Console.WriteLine($"Stream length after save: {stream.Length} bytes");
}
```

## Kompletní, spustitelný příklad

Níže je jeden program připravený ke zkopírování a vložení, který demonstruje celý tok. Obsahuje zpracování chyb, uvolňování streamů a komentáře vysvětlující každý krok.

```csharp
using System;
using System.IO;
using HtmlProcessing;   // Replace with the actual namespace of your HTML library

namespace HtmlStringDemo
{
    /// <summary>
    /// Custom handler that saves each resource to the local "output" directory.
    /// </summary>
    class MyHandler : ResourceHandler
    {
        private readonly string _outputDir;

        public MyHandler()
        {
            _outputDir = Path.Combine(Environment.CurrentDirectory, "output");
            Directory.CreateDirectory(_outputDir);
        }

        public override Stream HandleResource(ResourceInfo info)
        {
            // Derive a safe file name from the resource URI.
            string fileName = Path.GetFileName(new Uri(info.Uri, UriKind.RelativeOrAbsolute).LocalPath);
            if (string.IsNullOrWhiteSpace(fileName))
                fileName = Guid.NewGuid().ToString() + ".bin";

            string filePath = Path.Combine(_outputDir, fileName);
            // Return a FileStream that the library will write into.
            return new FileStream(filePath, FileMode.Create, FileAccess.Write);
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the HTML string.
            string htmlContent = "<html><body><h1>Hello, World!</h1></body></html>";
            if (string.IsNullOrWhiteSpace(htmlContent))
                throw new ArgumentException("HTML content cannot be empty.", nameof(htmlContent));

            // 2️⃣ Create the HTMLDocument from the string.
            HTMLDocument htmlDoc = new HTMLDocument(htmlContent);

            // 3️⃣ Create the custom resource handler.
            var handler = new MyHandler();

            // 4️⃣ Save the document using the custom handler.
            htmlDoc.Save(handler);

            Console.WriteLine("HTML document and resources have been saved to the \"output\" folder.");
        }
    }
}
```

**Očekávaný výstup**

```
HTML document and resources have been saved to the "output" folder.
```

Po spuštění programu adresář `output` obsahuje:

- `index.html` (hlavní dokument)
- Jakékoli další soubory vygenerované knihovnou (např. obrázky, CSS)

## Pokročilé varianty a okrajové případy

### Ukládání do `MemoryStream` pro zpracování v paměti

Pokud potřebujete finální HTML jako řetězec nebo jej chcete odeslat přes HTTP, aniž byste se dotkli disku, nahraďte `MyHandler` verzí, která vrací sdílený `MemoryStream`:

```csharp
class InMemoryHandler : ResourceHandler
{
    private readonly MemoryStream _mainStream = new MemoryStream();

    public MemoryStream MainStream => _mainStream;

    public override Stream HandleResource(ResourceInfo info)
    {
        // All resources go into the same memory buffer.
        return _mainStream;
    }
}
```

Po `htmlDoc.Save(handler)` můžete HTML přečíst:

```csharp
handler.MainStream.Position = 0;
string resultHtml = new StreamReader(handler.MainStream).ReadToEnd();
Console.WriteLine(resultHtml);
```

### Bezpečná manipulace s velkými zdroji

Při práci s velkými obrázky nebo PDF se vyhněte načítání celého souboru do paměti. Místo toho vraťte `FileStream`, který zapisuje přímo na disk, jak bylo ukázáno dříve. To zabraňuje `OutOfMemoryException` v scénářích s vysokou propustností.

### Úvahy o vláknové bezpečnosti

Instance `HTMLDocument` **nejsou** vlákny‑bezpečné. Pokud potřebujete zpracovávat více HTML řetězců současně, vytvořte pro každé vlákno samostatný `HTMLDocument` a `MyHandler`, nebo synchronizujte přístup pomocí `lock`.

### Uvolňování streamů

Jak `HTMLDocument.Save`, tak `ResourceHandler.HandleResource` mohou vracet streamy, které je třeba uvolnit. V uvedených příkladech knihovna po zápisu streamy automaticky uvolní. Pokud spravujete streamy sami (např. otevřením `FileStream` před voláním `Save`), zabalte je do `using` bloků.

## Shrnutí

Tento průvodce vám ukázal, jak **načíst html řetězec** do `HTMLDocument`, **vytvořit vlastní handler** pro určení uložení zdrojů a **jak uložit htmldocument** s **vlastní manipulací se zdroji**. Nyní máte:

1. Jasný způsob, jak převést surové HTML na DOM objekt.  
2. Znovupoužitelnou podtřídu `ResourceHandler`, která může zapisovat zdroje do paměti, na disk nebo do cloudového úložiště.  
3. Kompletní, spustitelný program, který demonstruje celý workflow.

## Další kroky

- Prozkoumejte další přepsání `ResourceHandler`, jako jsou `HandleCss` nebo `HandleFont`, pokud je vaše knihovna poskytuje.  
- Kombinujte tento přístup s krokem konverze do PDF, abyste generovali PDF z HTML při zachování plné kontroly nad vloženými assety.  
- Projděte dokumentaci knihovny pro další možnosti jako *komprese*, *caching* nebo *asynchronní* ukládání.

Neváhejte experimentovat s různými strategiemi ukládání a sdílet své poznatky v komentářích nebo ve vaší oblíbené vývojářské komunitě. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak uložit HTML v C# – Kompletní průvodce s použitím vlastního resource handleru](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Vytvoření HTML ze řetězce v C# – Průvodce vlastním resource handlerem](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Jak zipovat HTML v C# – Uložit HTML do Zip](/html/english/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}