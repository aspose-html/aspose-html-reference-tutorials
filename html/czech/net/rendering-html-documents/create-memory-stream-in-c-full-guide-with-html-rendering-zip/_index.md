---
category: general
date: 2026-03-31
description: Vytvořte paměťový stream v C# a naučte se převádět HTML na PNG, použít
  vlastní handler zdrojů, uložit HTML do ZIP a nastavit styl písma programově – vše
  v jednom tutoriálu.
draft: false
keywords:
- create memory stream
- render html to png
- custom resource handler
- save html to zip
- set font style programmatically
language: cs
og_description: Vytvořte paměťový stream v C# a okamžitě renderujte HTML do PNG, použijte
  vlastní manipulátory zdrojů, uložte HTML do ZIP a nastavte styl písma programově.
og_title: Vytvořte paměťový stream v C# – kompletní programovací průvodce
tags:
- C#
- HTML rendering
- Streams
- ZIP archives
- Image processing
title: Vytvoření Memory Stream v C# – Kompletní průvodce s renderováním HTML a exportem
  ZIP
url: /cs/net/rendering-html-documents/create-memory-stream-in-c-full-guide-with-html-rendering-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření Memory Stream v C# – Kompletní průvodce s renderováním HTML a exportem ZIP

Už jste se někdy zamysleli, jak **vytvořit memory stream** v C# a poté převést HTML dokument na PNG obrázek, ZIP soubor nebo dokonce během běhu změnit styl písma? Nejste v tom sami. Mnoho vývojářů narazí na problém, když potřebují in‑memory reprezentaci dokumentu, ale nechtějí zasahovat do souborového systému.  

V tomto tutoriálu projdeme kompletní, end‑to‑end řešení: vytvoříme vlastní resource handler, pošleme HTML do `MemoryStream`, zabalíme stejný dokument do ZIP a nakonec jej vykreslíme jako obrázek s antialiasingem. Na konci budete schopni **renderovat HTML do PNG**, **uložit HTML do ZIP** a **nastavit styl písma programově** bez jakéhokoli zápisu dočasných souborů na disk.

## Požadavky

- .NET 6.0 nebo novější (rozhraní API je stabilní napříč posledními verzemi).  
- Odkaz na knihovnu HTML‑to‑image, která poskytuje `HTMLDocument`, `ImageRenderer` a související typy – například **HtmlRenderer.Core** (nahraďte skutečným balíčkem, který používáte).  
- Základní znalost streamů, `using` bloků a objektově orientovaných vzorů v C#.

> **Pro tip:** Pokud používáte Visual Studio, povolte **nullable reference types** (`<Nullable>enable</Nullable>`), abyste včas zachytili jemné chyby.

## Krok 1: Vytvoření Memory Stream s vlastním Resource Handlerem

První věc, kterou potřebujeme, je handler, který řekne HTML engine *kam* zapisovat každý zdroj (obrázky, CSS atd.). Děděním z `ResourceHandler` můžeme nasměrovat každý výstup do jediného `MemoryStream`.

```csharp
using System;
using System.IO;

// Step 1: Define a handler that writes resources to an in‑memory stream
class MemoryResourceHandler : ResourceHandler
{
    // The stream lives for the whole lifetime of the handler
    public MemoryStream OutputStream = new MemoryStream();

    // The engine calls this for every resource it needs to write
    public override Stream HandleResource(ResourceInfo info) => OutputStream;
}
```

**Proč je to důležité:**  
`MemoryStream` existuje výhradně v RAM, což znamená žádný diskový I/O – ideální pro vysoce výkonné scénáře jako webové služby nebo unit testy. Handler také udržuje API spokojené, protože engine očekává `Stream` pro každý zdroj.

## Krok 2: Načtení HTML dokumentu a uložení do Memory Stream

Nyní načteme existující HTML soubor (nebo řetězec) a řekneme mu, aby použil náš `MemoryResourceHandler`. Po volání `Save` obsahuje `OutputStream` kompletní HTML payload.

```csharp
using System.IO;

// Assume the HTML file lives under YOUR_DIRECTORY
HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");

// Instantiate the memory handler
MemoryResourceHandler memoryHandler = new MemoryResourceHandler();

// Save the document – all resources flow into the same MemoryStream
htmlDoc.Save(memoryHandler);
```

V tomto okamžiku je pozice streamu na konci, takže ji musíme přetočit zpět, než budeme moci obsah číst.

```csharp
// Reset the stream position to the beginning
memoryHandler.OutputStream.Position = 0;

// Quick verification (optional)
// string htmlContent = new StreamReader(memoryHandler.OutputStream).ReadToEnd();
// Console.WriteLine(htmlContent);
```

> **Poznámka:** Řádek `ReadToEnd` výše je zakomentovaný, protože v produkčním scénáři pravděpodobně předáte stream jiné komponentě místo jeho výpisu.

## Krok 3: Zabalit stejný HTML do ZIP pomocí vlastního ZIP Resource Handleru

Někdy potřebujete odeslat HTML spolu s jeho prostředky. Druhý vlastní handler může za běhu vytvořit ZIP položku pro každý zdroj.

```csharp
using System.IO.Compression;

// Step 4: Define a handler that writes each resource into a ZIP archive
class ZipResourceHandler : ResourceHandler, IDisposable
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(string zipPath)
    {
        // Open (or create) the archive in write mode
        _zipArchive = ZipFile.Open(zipPath, ZipArchiveMode.Create);
    }

    // The engine calls this for each resource; we create a ZIP entry with the same name
    public override Stream HandleResource(ResourceInfo info) =>
        _zipArchive.CreateEntry(info.Name).Open();

    // Proper disposal of the underlying ZipArchive
    protected override void Dispose(bool disposing)
    {
        if (disposing) _zipArchive.Dispose();
        base.Dispose(disposing);
    }

    public void Dispose() => Dispose(true);
}
```

Nyní znovu použijeme stejnou instanci `htmlDoc` a zapíšeme ji do ZIP souboru.

```csharp
// Step 5: Save the HTML document into a ZIP file
using (var zipHandler = new ZipResourceHandler("YOUR_DIRECTORY/output.zip"))
{
    htmlDoc.Save(zipHandler);
}
```

**Tip pro okrajové případy:** Pokud HTML odkazuje na stejný obrázek vícekrát, ZIP handler vytvoří duplicitní položky. Abyste tomu předešli, můžete udržovat `HashSet<string>` již přidaných názvů a vracet stream existující položky místo nového.

## Krok 4: Programové nastavení stylu písma v Default Stylesheetu

Změna vzhledu dokumentu bez úpravy zdrojového HTML je často užitečná – například při generování PDF náhledu s tučným nadpisem. Knihovna poskytuje `DefaultViewStyleSheet`, který můžete upravit.

```csharp
// Step 6: Apply bold and italic styling to the default view stylesheet
htmlDoc.DefaultViewStyleSheet.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

Můžete kombinovat libovolné příznaky definované v `WebFontStyle`. Změna je okamžitá a ovlivní následné rendery nebo uložení.

## Krok 5: Renderování HTML dokumentu do PNG obrázku

Nakonec převádíme HTML na rastrový obrázek. Povolením antialiasingu a hintingu získáme ostrý text a hladké hrany.

```csharp
using System.Drawing; // For ImageRenderingOptions if needed

// Step 7: Render the document to an image with antialiasing and hinting
var renderingOptions = new ImageRenderingOptions
{
    UseAntialiasing = true,
    UseHinting = true
};

new ImageRenderer(renderingOptions).Render(htmlDoc, "YOUR_DIRECTORY/out.png");
```

**Co uvidíte:** PNG soubor pojmenovaný `out.png` ve složce `YOUR_DIRECTORY`, který vypadá přesně jako prohlížeč by vykreslil HTML, ale s tučně‑kurzívním stylem, který jsme nastavili dříve.

![Snímek obrazovky výstupu vytvoření memory stream](placeholder-image.png "příklad vytvoření memory stream")

*Alt text obrázku obsahuje primární klíčové slovo pro SEO.*

## Časté otázky a úskalí

| Otázka | Odpověď |
|----------|--------|
| **Mohu znovu použít stejný `HTMLDocument` po uložení do ZIP?** | Ano. Objekt dokumentu zůstává v paměti; můžete volat `Save` opakovaně s různými handlery. |
| **Co když HTML obsahuje velké binární zdroje?** | `MemoryStream` poroste úměrně. Pro velmi velké soubory zvažte streamování přímo do souboru nebo použití `BufferedStream`. |
| **Musím volat `Dispose` na `MemoryResourceHandler`?** | Není to naprosto nutné, protože drží jen `MemoryStream`, který je uvolněn při garbage‑collection handleru. Přesto je volání `Dispose` dobrým zvykem. |
| **Jak změním formát obrázku (např. JPEG místo PNG)?** | Předáte jinou příponu souboru metodě `ImageRenderer.Render`, nebo použijete `ImageRenderer.RenderToBitmap` a následně uložíte pomocí `bitmap.Save("out.jpg", ImageFormat.Jpeg)`. |
| **Je ZIP handler thread‑safe?** | Ne. `ZipArchive` není thread‑safe, takže přístup serializujte nebo vytvořte samostatný handler pro každý vlákno. |

## Kompletní funkční příklad

Níže je jednorázový program připravený ke zkopírování a vložení, který demonstruje každý krok. Nahraďte `YOUR_DIRECTORY` skutečnou cestou na vašem počítači.

```csharp
// FullExample.cs
using System;
using System.IO;
using System.IO.Compression;

// Assume these types come from your HTML rendering library
using HtmlRendering; // placeholder namespace

class MemoryResourceHandler : ResourceHandler
{
    public MemoryStream OutputStream = new MemoryStream();
    public override Stream HandleResource(ResourceInfo info) => OutputStream;
}

class ZipResourceHandler : ResourceHandler, IDisposable
{
    private readonly ZipArchive _zipArchive;
    public ZipResourceHandler(string zipPath) =>
        _zipArchive = ZipFile.Open(zipPath, ZipArchiveMode.Create);

    public override Stream HandleResource(ResourceInfo info) =>
        _zipArchive.CreateEntry(info.Name).Open();

    protected override void Dispose(bool disposing)
    {
        if (disposing) _zipArchive.Dispose();
        base.Dispose(disposing);
    }

    public void Dispose() => Dispose(true);
}

class Program
{
    static void Main()
    {
        // 1️⃣ Load HTML
        var htmlDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");

        // 2️⃣ Write to a memory stream
        var memHandler = new MemoryResourceHandler();
        htmlDoc.Save(memHandler);
        memHandler.OutputStream.Position = 0;
        // Optional: verify content
        // Console.WriteLine(new StreamReader(memHandler.OutputStream).ReadToEnd());

        // 3️⃣ Zip the same document
        using (var zipHandler = new ZipResourceHandler("YOUR_DIRECTORY/output.zip"))
        {
            htmlDoc.Save(zipHandler);
        }

        // 4️⃣ Change font style programmatically
        htmlDoc.DefaultViewStyleSheet.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // 5️⃣ Render to PNG with antialiasing & hinting
        var renderOpts = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            UseHinting = true
        };
        new ImageRenderer(renderOpts).Render(htmlDoc, "YOUR_DIRECTORY/out.png");

        Console.WriteLine("All operations completed successfully.");
    }
}
```

Po spuštění tohoto programu získáte tři artefakty:

1. **In‑memory HTML** uložené v `memHandler.OutputStream`.  
2. **`output.zip`** obsahující HTML a všechny propojené zdroje.  
3. **`out.png`** – vykreslený obrázek, který respektuje tučně‑kurzívní styl.

## Závěr

Ukázali jsme, jak **vytvořit memory stream** v C# a bez problémů jej integrovat s renderováním HTML, archivací ZIP a generováním obrázků. Hlavní myšlenkou je, že jediný `HTMLDocument` může být uložen různými způsoby – do `MemoryStream`, ZIP archivu nebo PNG souboru – jednoduše výměnou `ResourceHandler`.  

Pokud jste připraveni posunout to dál, zkuste:

- **Renderovat do PDF** pomocí PDF rendereru, který přijímá `Stream`.  
- **Komprimovat memory stream** před odesláním po síti (např. `GZipStream`).  
- **Sloučit více HTML stránek** do jednoho ZIP pro hromadný export.

Neváhejte experimentovat a pokud narazíte na problém, zanechte komentář. Šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}