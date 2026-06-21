---
category: general
date: 2026-03-29
description: Naučte se, jak používat ZipArchive v C# k převodu HTML do ZIP, uložení
  HTML do ZIP a kompresi obrázků v HTML – vše v jednom přehledném tutoriálu.
draft: false
keywords:
- how to use ziparchive
- convert html to zip
- save html to zip
- create zip archive c#
- compress html images
language: cs
og_description: Objevte, jak použít ZipArchive v C# k převodu HTML do ZIP, uložení
  HTML do ZIP a kompresi obrázků v HTML s kompletním, spustitelným příkladem.
og_title: Jak používat ZipArchive – Uložte HTML a zdroje do ZIP souboru
tags:
- C#
- .NET
- Aspose.Html
- ZipArchive
title: Jak používat ZipArchive – Uložit HTML a zdroje do ZIP souboru
url: /cs/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat ZipArchive – Uložit HTML a zdroje do ZIP souboru

Už jste se někdy zamýšleli **jak používat ZipArchive** k zabalení HTML stránky spolu s jejími obrázky, CSS a dalšími soubory? Nejste v tom sami. Mnoho vývojářů narazí na problém, když potřebují doručit samostatný HTML balíček, zejména pokud stránka odkazuje na externí zdroje. Dobrá zpráva? Několika řádky C# a Aspose.HTML můžete **převést HTML do ZIP**, **uložit HTML do ZIP** a dokonce **komprimovat obrázky v HTML** přímo v IDE.

V tomto tutoriálu projdeme celý proces – od vytvoření jednoduchého `HTMLDocument` až po zpracování každého propojeného zdroje pomocí vlastního `ResourceHandler`. Na konci budete mít připravený ZIP soubor, který můžete nasadit na jakýkoli webový server nebo připojit k e‑mailu. Žádné externí skripty, žádné ruční kopírování – jen čistý .NET.

## Požadavky

Než začneme, ujistěte se, že máte:

- **.NET 6+** (nebo .NET Framework 4.6+). Používaná API jsou součástí `System.IO.Compression`.
- **Aspose.HTML for .NET** nainstalovaný (NuGet balíček `Aspose.Html`).
- Základní znalost syntaxe C#.
- IDE jako Visual Studio nebo VS Code.

To je vše. Žádné další nástroje, žádné třetí strany pro zipování. Připravení? Pojďme na to.

## Krok 1: Nastavení projektu a přidání závislostí

Vytvořte nový konzolový projekt:

```bash
dotnet new console -n HtmlToZipDemo
cd HtmlToZipDemo
dotnet add package Aspose.Html
```

Balíček `Aspose.Html` nám poskytuje třídu `HTMLDocument` a základní třídu `ResourceHandler`, kterou později rozšíříme. Vestavěný prostor názvů `System.IO.Compression` poskytuje `ZipArchive` a `ZipArchiveEntry`.

> **Tip:** Pokud cílíte na .NET 6, můžete použít top‑level statements, aby metoda `Main` zůstala přehledná. Níže uvedený kód používá klasickou třídu `Program` pro větší srozumitelnost.

## Krok 2: Vytvoření vlastního Resource Handleru

Když Aspose.HTML ukládá dokument, požádá `ResourceHandler`, aby poskytl `Stream` pro každý externí soubor (obrázky, CSS, fonty atd.). Přepsáním metody `HandleResource` můžeme každý zdroj přímo nasměrovat do zip položky.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Writes each HTML resource (image, CSS, etc.) directly into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(ZipArchive zipArchive) => _zipArchive = zipArchive;

    public override Stream HandleResource(string resourceName, ResourceType resourceType)
    {
        // Ensure a folder hierarchy inside the zip (optional but tidy)
        var entry = _zipArchive.CreateEntry(resourceName, CompressionLevel.Optimal);
        return entry.Open(); // Aspose streams the content into this entry.
    }
}
```

**Proč je to důležité:** Místo toho, abychom nejprve zapisovali zdroje na disk a pak je zipovali, handler je streamuje přímo, což snižuje zátěž I/O a zaručuje, že zip bude synchronizován s obsahem HTML.

## Krok 3: Vytvoření HTML dokumentu

Pro demonstraci vložíme malý HTML úryvek, který odkazuje na externí obrázek `logo.png`. Ve skutečném projektu můžete HTML načíst ze souboru nebo databáze.

```csharp
// Create a simple HTML document with an external image reference.
HTMLDocument htmlDocument = new HTMLDocument(
    "<html><body><h1>Welcome!</h1><img src='logo.png' alt='Demo logo'></body></html>"
);
```

Pokud potřebujete **komprimovat obrázky v HTML**, stačí zajistit, aby soubor s obrázkem byl vedle spustitelného souboru (nebo jej vložit jako zdroj). `ZipResourceHandler` přidá obrázek do archivu automaticky.

## Krok 4: Otevření (nebo vytvoření) ZIP souboru a uložení

Nyní vše spojíme. Otevřeme `FileStream` pro výstupní zip, vytvoříme `ZipArchive` v režimu *Update* a předáme náš vlastní handler metodě `HTMLDocument.Save`.

```csharp
using (var fileStream = new FileStream("output.zip", FileMode.Create))
using (var zipArchive = new ZipArchive(fileStream, ZipArchiveMode.Update))
{
    // Initialise the handler with the open ZipArchive.
    var zipHandler = new ZipResourceHandler(zipArchive);

    // Save the HTML document; the handler writes HTML, images, CSS, etc. into the zip.
    htmlDocument.Save(zipHandler);
}
```

Po opuštění bloků `using` je zip automaticky dokončen a uzavřen. Výsledný `output.zip` obsahuje:

- `index.html` (serializovaný HTML dokument)
- `logo.png` (obrázek odkazovaný v HTML)

Obsah můžete ověřit otevřením zipu v libovolném správci souborů.

## Krok 5: Ověření výsledku (volitelné)

Vždy je dobré dvakrát zkontrolovat, že zip skutečně funguje. Zde je rychlý úryvek, který můžete spustit po předchozím kódu a vypíše položky:

```csharp
using (var zip = ZipFile.OpenRead("output.zip"))
{
    Console.WriteLine("Contents of output.zip:");
    foreach (var entry in zip.Entries)
        Console.WriteLine($"- {entry.FullName} ({entry.Length} bytes)");
}
```

Měli byste vidět něco jako:

```
Contents of output.zip:
- index.html (1234 bytes)
- logo.png (45678 bytes)
```

Otevřete `index.html` z rozbalené složky a uvidíte, že se obrázek zobrazí správně – důkaz, že **uložení HTML do ZIP** funguje podle očekávání.

## Běžné varianty a okrajové případy

### 1. Použití jiného názvu položky pro HTML soubor

Ve výchozím nastavení Aspose zapisuje HTML do `index.html`. Pokud potřebujete vlastní název, můžete před uložením nastavit `htmlDocument.FileName`:

```csharp
htmlDocument.FileName = "myPage.html";
htmlDocument.Save(zipHandler);
```

### 2. Přidání dalších souborů ručně

Někdy chcete přibalit další soubory (např. README). Můžete je přidat přímo do `ZipArchive` před voláním `htmlDocument.Save`:

```csharp
var readme = zipArchive.CreateEntry("README.txt", CompressionLevel.Optimal);
using (var writer = new StreamWriter(readme.Open()))
{
    writer.WriteLine("This ZIP contains an HTML page generated with Aspose.HTML.");
}
```

### 3. Efektivní zpracování velkých obrázků

Pokud HTML odkazuje na velmi velké obrázky, zvažte jejich předchozí zmenšení, aby byl zip rozumné velikosti. Pomoci může balíček `System.Drawing.Common`:

```csharp
// Example: Resize logo.png to a max width of 800px before zipping.
using (var img = System.Drawing.Image.FromFile("logo.png"))
{
    int maxWidth = 800;
    if (img.Width > maxWidth)
    {
        var ratio = (double)maxWidth / img.Width;
        var newHeight = (int)(img.Height * ratio);
        using var thumb = img.GetThumbnailImage(maxWidth, newHeight, () => false, IntPtr.Zero);
        thumb.Save("logo_resized.png");
    }
}
```

Pak v HTML změňte odkaz na `<img src='logo_resized.png'>`.

## Kompletní, spustitelný příklad

Níže je kompletní program, který můžete zkopírovat a vložit do `Program.cs`. Překládá se a spouští tak, jak je, pokud máte nainstalovaný NuGet balíček Aspose.HTML.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Custom handler that streams each resource into a zip entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;
    public ZipResourceHandler(ZipArchive zipArchive) => _zipArchive = zipArchive;

    public override Stream HandleResource(string resourceName, ResourceType resourceType)
    {
        var entry = _zipArchive.CreateEntry(resourceName, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Create an HTML document that references an external image.
        HTMLDocument htmlDocument = new HTMLDocument(
            "<html><head><title>Demo</title></head>" +
            "<body><h2>Hello, ZipArchive!</h2>" +
            "<img src='logo.png' alt='Demo logo'></body></html>"
        );

        // 2️⃣ Open (or create) the output zip file.
        using (var fileStream = new FileStream("output.zip", FileMode.Create))
        using (var zipArchive = new ZipArchive(fileStream, ZipArchiveMode.Update))
        {
            // 3️⃣ Initialise the custom handler.
            var zipHandler = new ZipResourceHandler(zipArchive);

            // 4️⃣ Save the HTML; resources get streamed into the zip.
            htmlDocument.Save(zipHandler);
        }

        Console.WriteLine("✅ HTML document and its resources have been saved to output.zip");
    }
}
```

**Očekávaný výstup:** Konzole vypíše zprávu o úspěchu a `output.zip` se objeví ve složce projektu s `index.html` a `logo.png`.

## Často kladené otázky

- **Funguje to na .NET Core?**  
  Ano. `System.IO.Compression.ZipArchive` je součástí **.NET Standard**, takže stejný kód běží na .NET 5, .NET 6 i .NET 7.

- **Co když potřebuji **komprimovat obrázky v HTML** agresivněji?**  
  Můžete před přidáním do zipu předzpracovat obrázky (zmenšit, změnit formát na WebP atd.). Handler pouze streamuje data, která obdrží.

- **Mohu zip zašifrovat?**  
  `ZipArchive` podporuje AES šifrování jen prostřednictvím knihoven třetích stran (např. `SharpZipLib`). Pokud šifrování potřebujete, vytvořte zip pomocí takové knihovny a poté jej předávejte Aspose jako vlastní `ResourceHandler`.

- **Je možné nastavit kořenovou složku uvnitř zipu?**  
  Ano – předponujte název složky k `resourceName` uvnitř `HandleResource`, např. `var entry = _zipArchive.CreateEntry($"site/{resourceName}", ...)`.

## Závěr

Nyní už víte **jak používat ZipArchive** v C# k **převodu HTML do ZIP**, **uložení HTML do ZIP** a **kompresi obrázků v HTML** v jednom čistém workflow. Rozšířením `ResourceHandler` jsme se vyhnuli dočasným souborům a zachovali proces paměťově efektivní. Tento vzor se dobře škáluje: stačí vygenerovaný zip nahrát na webový server, poslat e‑mailem nebo uložit do cloudového úložiště.

Další kroky, které můžete zkusit:

- **Programově vytvářet ZIP archivy** pro celé složky webu (`create zip archive c#`).
- **Přidat konverze PDF nebo DOCX** před zipováním pro bohatší dokumentační balíčky.
- **Integrovat s ASP.NET Core** a streamovat zip přímo do prohlížeče klienta (`FileStreamResult`).

Máte další otázky ohledně zipování HTML, práce s fonty nebo optimalizace velikosti obrázků? Napište komentář nebo mě kontaktujte na Stack Overflow. Šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}