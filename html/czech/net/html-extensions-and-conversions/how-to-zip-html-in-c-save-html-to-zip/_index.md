---
category: general
date: 2025-12-29
description: Jak rychle zabalit HTML do ZIP v C# pomocí Aspose.HTML – uložit HTML
  do ZIP s vlastním ZipResourceHandler. Naučte se krok za krokem.
draft: false
keywords:
- how to zip html
- save html to zip
- create zip archive c#
- Aspose HTML zip
- C# resource handling
language: cs
og_description: Jak rychle zkomprimovat HTML v C# pomocí Aspose.HTML. Postupujte podle
  tohoto návodu, abyste uložili HTML do zipu a vytvořili zip archiv s vlastním zpracováním
  zdrojů.
og_title: Jak zabalit HTML do ZIP v C# – Uložit HTML do ZIP
tags:
- C#
- Aspose.HTML
- ZipArchive
- File I/O
title: Jak zkomprimovat HTML v C# – Uložit HTML do ZIP
url: /cs/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zabalit HTML do ZIP v C# – Uložit HTML do ZIP

Zabalení HTML do ZIP v C# je častá potřeba, když chcete balit webové stránky pro offline použití. Ať už balíte jedinou stránku s jejími obrázky nebo exportujete celý web, **ukládání HTML do zipu** udržuje vše přehledné a přenositelné. V tomto tutoriálu vás provedeme kompletním, připraveným řešením, které nejen zabalí HTML markup, ale také streamuje všechny odkazované zdroje přímo do archivu.

Dozvíte se, jak:

* Vytvořit ZIP archiv programově pomocí .NET `System.IO.Compression`.
* Připojit vlastní `ResourceHandler` do Aspose.HTML, aby zdroje proudily přímo do ZIPu.
* Ošetřit okrajové případy, jako jsou existující ZIP soubory a velké binární assety.

Žádné externí nástroje nejsou potřeba – stačí C#, Aspose.HTML a pár řádků kódu.

## Co budete potřebovat

Než se pustíme dál, ujistěte se, že máte:

* **.NET 6+** (kód funguje také na .NET Framework 4.6.2 a novějším).
* **Aspose.HTML for .NET** – můžete si stáhnout bezplatnou zkušební verzi z webu Aspose nebo použít licencovanou kopii.
* Vývojové prostředí (Visual Studio, VS Code, Rider – co vám vyhovuje).

To je vše. Žádné další NuGet balíčky kromě `System.IO.Compression` (součást .NET) a `Aspose.HTML`.

## Krok 1: Nastavení projektu a importů

Vytvořte nový konzolový projekt (nebo vložte kód do existujícího). Přidejte požadované `using` direktivy na začátek souboru:

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;
```

> **Pro tip:** Pokud používáte Visual Studio, IDE navrhne přidání chybějícího NuGet balíčku pro `Aspose.Html`. Přijměte ho a jste připraveni k práci.

## Krok 2: Implementace vlastního ZipResourceHandler

Aspose.HTML volá `ResourceHandler` vždy, když potřebuje zapsat zdroj (např. obrázek, CSS soubor nebo skript). Přepsáním `HandleResource` můžeme přesně určit, kam každý zdroj skončí. Níže uvedený handler vytváří zip položku, která odráží logickou cestu zdroje, a vrací zapisovatelný stream, který ukazuje přímo na tuto položku.

```csharp
/// <summary>
/// Streams each HTML resource straight into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;

    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // Ensure the entry's directory structure exists inside the zip.
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        // The returned stream writes directly into the zip entry.
        return entry.Open();
    }
}
```

**Proč je to důležité:**  
Místo zápisu zdrojů do dočasné složky a následného zabalení složky, tento handler streamuje data za běhu, čímž šetří diskové I/O a udržuje nízkou spotřebu paměti. Navíc zaručuje, že vnitřní hierarchie složek v ZIPu odpovídá relativním cestám HTML, což prohlížeče očekávají při rozbalení a otevření stránky.

## Krok 3: Příprava ZIP archivu

Nyní otevřeme (nebo vytvoříme) cílový ZIP soubor. Příznak `FileMode.Create` přepíše jakýkoli existující soubor – ideální pro opakovatelné sestavení. Pokud chcete zachovat existující archiv, přepněte na `FileMode.OpenOrCreate` a podle toho řešte duplicitní položky.

```csharp
string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");

// Ensure the directory exists (useful if you run the code from a nested folder)
Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);

using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);
```

> **Okrajový případ:** Pokud proces spadne před tím, než `using` blok uvolní archiv, můžete skončit s poškozeným ZIPem. Spuštění kódu uvnitř `try/catch` a smazání částečně vytvořeného souboru při selhání je jednoduchá ochrana.

## Krok 4: Vytvoření HTML dokumentu s vloženým zdrojem

Pro demonstraci vytvoříme malou HTML stránku, která odkazuje na obrázek `image.png`. Ve skutečném scénáři byste načítali HTML ze souboru nebo řetězce z databáze.

```csharp
// Sample HTML containing an <img> tag.
// Aspose.HTML will ask the ResourceHandler for "image.png".
string htmlContent = @"
<html>
<head><title>Sample Zip</title></head>
<body>
    <h1>Hello, zipped world!</h1>
    <img src='image.png' alt='Demo image'>
</body>
</html>";

// Create the document from the string.
var html = new HTMLDocument(htmlContent);
```

Pokud máte skutečné soubory obrázků na disku, můžete je před uložením HTML přidat do ZIPu ručně, nebo nechat Aspose.HTML načíst je přes handler (např. z URL). Náš handler funguje jak pro lokální cesty, tak pro vzdálené URL.

## Krok 5: Konfigurace možností uložení pro použití ZipResourceHandler

Nyní řekneme Aspose.HTML, aby používal náš vlastní handler při zápisu zdrojů. Třída `HTMLSaveOptions` také umožňuje určit název výstupního souboru uvnitř ZIPu (ve výchozím nastavení je to `index.html`).

```csharp
var saveOptions = new HTMLSaveOptions
{
    // The HTML file itself will be saved as "index.html" inside the zip.
    OutputFileName = "index.html",
    // Plug in our handler so resources go straight into the archive.
    OutputStorage = new ZipResourceHandler(zip)
};
```

## Krok 6: Uložení dokumentu – vše streamuje do ZIPu

Nakonec zavoláme `Save`. Aspose.HTML parsuje markup, najde `<img>` tag, zavolá `HandleResource` pro `image.png` a zapíše jak HTML soubor, tak obrázek do stejného ZIP archivu.

```csharp
html.Save(saveOptions);
Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
```

Po opuštění `using` bloků `ZipArchive` finalizuje soubor a připraví jej k distribuci.

### Kompletní funkční příklad

Níže je celý program poskládaný dohromady. Zkopírujte jej do `Program.cs` a spusťte – žádné další úpravy nejsou potřeba.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;
    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare the zip file.
        string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");
        Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);
        using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
        using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);

        // 2️⃣ Build a simple HTML document with an image reference.
        string htmlContent = @"
        <html>
        <head><title>Sample Zip</title></head>
        <body>
            <h1>Hello, zipped world!</h1>
            <img src='image.png' alt='Demo image'>
        </body>
        </html>";
        var html = new HTMLDocument(htmlContent);

        // 3️⃣ Set save options to stream resources into the zip.
        var saveOptions = new HTMLSaveOptions
        {
            OutputFileName = "index.html",
            OutputStorage = new ZipResourceHandler(zip)
        };

        // 4️⃣ Save – everything ends up in output.zip.
        html.Save(saveOptions);
        Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
    }
}
```

**Očekávaný výsledek:** Po spuštění `output.zip` obsahuje dvě položky:

```
index.html
image.png
```

Pokud rozbalíte soubor a otevřete `index.html` v prohlížeči, obrázek se zobrazí správně, protože relativní cesta je zachována.

## Často kladené otázky

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}