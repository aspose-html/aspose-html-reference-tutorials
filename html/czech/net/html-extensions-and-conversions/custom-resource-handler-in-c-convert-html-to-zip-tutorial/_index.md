---
category: general
date: 2026-02-10
description: Vlastní obslužná rutina zdrojů vám umožní převést HTML do ZIP v C#. Naučte
  se, jak uložit HTML jako zip a efektivně streamovat HTML zdroje.
draft: false
keywords:
- custom resource handler
- convert html to zip
- save html as zip
- create zip with html
- stream html resources
language: cs
og_description: Vlastní handler zdrojů vám umožní převést HTML do ZIP v C#. Postupujte
  podle tohoto krok‑za‑krokem návodu, abyste uložili HTML jako zip a streamovali HTML
  zdroje.
og_title: Vlastní obsluha zdrojů v C# – Převod HTML do ZIP
tags:
- Aspose.HTML
- C#
- ZIP archive
- file streaming
title: Vlastní handler zdrojů v C# – Návod na převod HTML do ZIP
url: /cs/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vlastní manipulátor zdrojů – Převod HTML do ZIP v C#

Už jste se někdy zamýšleli, jak **vlastním manipulátorem zdrojů** převést surové HTML přímo do souboru ZIP? Nejste sami. Mnoho vývojářů narazí na problém, když potřebují zabalit HTML stránku s jejími prostředky, aniž by zaplnili disk dočasnými soubory. Dobrá zpráva? S Aspose.HTML můžete vše provést v paměti a trik spočívá ve vlastním manipulátoru zdrojů.

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který vám ukáže, jak **převést HTML do ZIP**, **uložit HTML jako ZIP** a **streamovat HTML zdroje** za běhu. Na konci budete mít jedinou metodu, která přijme řetězec HTML a vytvoří připravený ke stažení `result.zip` obsahující stránku a všechny propojené zdroje.

> **Požadavky** – .NET 6+ (nebo .NET Framework 4.6+), nainstalovaný Aspose.HTML pro .NET a základní znalost streamů. Žádné externí nástroje nejsou potřeba.

---

## Vlastní manipulátor zdrojů – Základní koncept

*Manipulátor zdrojů* v Aspose.HTML je objekt, který rozhoduje **kam** se každá část dokumentu uloží – ať už na disk, do paměťového bufferu nebo, jak ukážeme, jako položka uvnitř ZIP archivu. Děděním třídy `ResourceHandler` získáte plnou kontrolu nad cílovým umístěním výstupu hlavního HTML souboru **i** všech pomocných zdrojů (CSS, obrázky, fonty atd.).

Představte si to jako dopravního policistu pro prostředky vašeho dokumentu: metoda `HandleResource` vám předá `Stream` pro hlavní HTML, zatímco událost `ResourceSaving` vám umožní zachytit každý závislý soubor těsně před jeho zápisem.

---

## Krok 1: Implementace vlastního manipulátoru zdrojů

Nejprve vytvořte třídu, která dědí z `ResourceHandler`. Přepíšeme `HandleResource`, aby Aspose získal čerstvý `MemoryStream` pro primární výstup HTML. Pro propojené prostředky se později připojíme k události `ResourceSaving`.

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using System.IO;

/// <summary>
/// Supplies a stream for every resource the HTML document needs to save.
/// </summary>
class MyHandler : ResourceHandler
{
    /// <summary>
    /// Returns a new stream for the main HTML content.
    /// </summary>
    public override Stream HandleResource(ResourceInfo info)
    {
        // In real life you might return a FileStream or a ZipEntry stream.
        // Here we just hand back a clean MemoryStream.
        return new MemoryStream();
    }
}
```

**Proč je to důležité:** Vrácení nového `MemoryStream` znamená, že HTML se nikdy nedotkne souborového systému. To je základ pro čisté, paměťové vytvoření ZIP souboru později.

---

## Krok 2: Uložení HTML do jediného MemoryStream

Nyní, když máme manipulátor, můžeme vygenerovat HTML dokument a zachytit jej kompletně v paměti. Tento krok je volitelný, pokud potřebujete jen ZIP, ale ilustruje, jak manipulátor funguje samostatně.

```csharp
using Aspose.Html;

// Sample HTML – replace with your own markup or load from a file.
string htmlContent = "<html><head><title>Demo</title></head><body>Hello world!</body></html>";

// Create the document from a string.
HTMLDocument htmlDocument = new HTMLDocument(htmlContent);

// Instantiate our custom handler.
MyHandler memoryHandler = new MyHandler();

using (MemoryStream htmlStream = new MemoryStream())
{
    // Save triggers HandleResource and writes the HTML into htmlStream.
    htmlDocument.Save(htmlStream, memoryHandler);

    // Reset position for potential reading.
    htmlStream.Position = 0;

    // For demo purposes, dump the HTML to console.
    using (StreamReader reader = new StreamReader(htmlStream))
    {
        Console.WriteLine("Generated HTML:");
        Console.WriteLine(reader.ReadToEnd());
    }
}
```

**Očekávaný výstup** (formátovaný pro čitelnost):

```
Generated HTML:
<html><head><title>Demo</title></head><body>Hello world!</body></html>
```

Po spuštění tohoto úryvku uvidíte, že HTML existuje jen v RAM – žádné dočasné soubory nejsou vytvořeny.

---

## Krok 3: Zabalení HTML a zdrojů do ZIP archivu

Nyní přichází ta šťavnatá část: zabalení HTML **a** všech odkazovaných prostředků do ZIP souboru, aniž by se kdykoli zapisovaly mezilehlé soubory na disk. Použijeme `System.IO.Compression.ZipArchive` spolu s událostí `ResourceSaving`.

```csharp
using Aspose.Html;
using System.IO;
using System.IO.Compression;

// Re‑use the same HTMLDocument from the previous step.
HTMLDocument htmlDocument = new HTMLDocument("<html><body>Hello world!</body></html>");

// Path where the final ZIP will be written.
string zipPath = Path.Combine(Environment.CurrentDirectory, "result.zip");

// Open a FileStream for the ZIP file.
using (FileStream zipFile = new FileStream(zipPath, FileMode.Create))
using (ZipArchive zipArchive = new ZipArchive(zipFile, ZipArchiveMode.Update))
{
    // Create a fresh handler for the ZIP operation.
    MyHandler zipHandler = new MyHandler();

    // Hook the ResourceSaving event – this fires for every resource.
    zipHandler.ResourceSaving += (sender, e) =>
    {
        // Ensure we don't create leading folder entries like "/css/style.css".
        string entryName = e.ResourceInfo.Path.TrimStart('/');

        // Create a new entry inside the ZIP.
        ZipArchiveEntry entry = zipArchive.CreateEntry(entryName);

        // Provide the stream that Aspose will write into.
        e.Stream = entry.Open();
    };

    // Save the document; the handler will fill the ZIP for us.
    htmlDocument.Save(zipHandler);
}

// Verify the ZIP exists.
Console.WriteLine($"ZIP created at: {zipPath}");
```

### Co se děje pod kapotou?

1. **`ResourceSaving`** se spustí pro hlavní HTML soubor i pro každý odkazovaný prostředek.  
2. Naše lambda vytvoří odpovídající položku (`CreateEntry`) v otevřeném ZIP souboru.  
3. Přiřazením `e.Stream = entry.Open()` předáme Aspose zapisovatelný stream, který zapisuje přímo do položky ZIP.  
4. Když se dokončí `htmlDocument.Save`, ZIP obsahuje kompletní HTML stránku plus veškeré CSS, obrázky nebo fonty, na které markup odkazuje.

**Výsledek:** Jeden soubor `result.zip`, který můžete servírovat prohlížečům, připojit k e‑mailům nebo uložit do blob úložiště – bez zbylých dočasných souborů.

---

## Bonus: Použití ZIP v Web API

Pokud vytváříte endpoint v ASP.NET Core, který ZIP vrací na vyžádání, platí stejná logika. Zde je kompaktní akce kontroleru:

```csharp
[ApiController]
[Route("api/[controller]")]
public class HtmlZipController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult DownloadZip()
    {
        // Build the document (could be loaded from a DB, etc.).
        var html = "<html><body><h1>Dynamic report</h1></body></html>";
        var doc = new HTMLDocument(html);
        var handler = new MyHandler();

        // Prepare an in‑memory ZIP.
        using var zipStream = new MemoryStream();
        using (var archive = new ZipArchive(zipStream, ZipArchiveMode.Create, true))
        {
            handler.ResourceSaving += (s, e) =>
            {
                var entry = archive.CreateEntry(e.ResourceInfo.Path.TrimStart('/'));
                e.Stream = entry.Open();
            };
            doc.Save(handler);
        }

        zipStream.Position = 0;
        return File(zipStream, "application/zip", "report.zip");
    }
}
```

Nyní GET požadavek na `/api/HtmlZip/download` streamuje vygenerovaný ZIP přímo klientovi – ideální pro reporty generované za běhu.

---

## Časté problémy a tipy

| Problém | Proč se vyskytuje | Řešení |
|---------|-------------------|--------|
| **Prázdné složky v ZIP** | `ResourceInfo.Path` začíná `/`, což vytváří položku jako `/` | Použijte `TrimStart('/')` podle ukázky v obsluze události. |
| **Chybějící obrázky** | Obrázky s absolutními URL se automaticky nevyžádají | Nastavte `htmlDocument.Options.ResourceLoading = ResourceLoadingMode.Stream` a poskytněte vlastní `ResourceHandler`, který stáhne vzdálené prostředky. |
| **Velké soubory zatěžují paměť** | Všechny streamy zůstávají v paměti, dokud se ZIP neuzavře | Přepněte `ZipArchiveMode.Update` na `Create` a zapisujte každou položku přímo bez bufferování, nebo streamujte z disku, pokud velikost přesahuje RAM. |
| **Výjimka “The stream does not support seeking”** | Pokus o opětovné použití ne‑seekovatelného streamu pro více zdrojů | Vždy poskytněte čerstvý `MemoryStream` nebo `entry.Open()` pro každý zdroj. |

---

## Závěr

Právě jsme ukázali, jak **vlastní manipulátor zdrojů** umožňuje **převést HTML do ZIP**, **uložit HTML jako ZIP** a **streamovat HTML zdroje** bez dotyku souborového systému. Přepsáním `HandleResource` a využitím `ResourceSaving` získáte detailní kontrolu nad každým bajtem, který opustí Aspose.HTML.

Tento vzor je škálovatelný: vyměňte paměťový `MemoryStream` za stream do cloudového blobu, přidejte nastavení komprese nebo zapojte logovací vrstvu pro audit, které prostředky jsou zabaleny. Možnosti jsou neomezené, jakmile ovládáte pipeline zdrojů.

Jste připraveni na další krok? Zkuste vložit CSS a obrázky přímo do HTML, experimentujte se vzdáleným načítáním zdrojů nebo integrujte tento tok do Azure Function, která vrací ZIP na vyžádání. Šťastné programování!

--- 

*Obrázek ilustrující tok vlastního manipulátoru zdrojů, který mění HTML na ZIP soubor.*

![custom resource handler workflow](https://example.com/placeholder-image.png "custom resource handler workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}