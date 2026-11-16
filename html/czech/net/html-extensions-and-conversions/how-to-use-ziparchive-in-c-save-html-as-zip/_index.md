---
category: general
date: 2026-05-06
description: Jak použít ZipArchive v C# k uložení HTML jako ZIP archivu. Naučte se
  vytvořit ZIP archiv v C# z HTML zdrojů pomocí Aspose.HTML.
draft: false
keywords:
- how to use ziparchive
- save html as zip
- create zip archive c#
- create zip from html
language: cs
og_description: Jak použít ZipArchive v C# k zabalení HTML dokumentu a jeho zdrojů
  do jediného ZIP souboru. Podrobný návod krok za krokem s kompletním kódem.
og_title: Jak používat ZipArchive v C# – Uložit HTML jako ZIP
tags:
- C#
- Aspose.HTML
- ZipArchive
- File I/O
title: Jak používat ZipArchive v C# – Uložit HTML jako ZIP
url: /cs/net/html-extensions-and-conversions/how-to-use-ziparchive-in-c-save-html-as-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat ZipArchive v C# – Uložit HTML jako ZIP

Už jste se někdy zamýšleli, jak použít ZipArchive v C#, když potřebujete distribuovat HTML stránku spolu s obrázky, CSS a fonty? Nejste v tom sami. V mnoha scénářích web‑to‑desktop je nejjednodušší způsob, jak přesunout celou stránku, zabalit vše do ZIP souboru.  

V tomto tutoriálu vás provedeme **ukládáním HTML jako zip** pomocí Aspose.HTML a vlastního `ResourceHandler`. Na konci přesně budete vědět, jak vytvořit zip archiv c# projekty, které automaticky zachytí každý odkazovaný zdroj, a budete mít kompletní, spustitelný příklad, který můžete vložit do svého kódu.

## Co vytvoříte

- Načíst existující soubor `input.html`.
- Zachytit každý externí zdroj (obrázky, styly, fonty) během ukládání dokumentu.
- Zapsat každý zdroj přímo do položky `ZipArchive`, aby výsledný soubor byl úhledný `output.zip`.
- Ověřit, že ZIP obsahuje očekávanou strukturu složek.

Není potřeba žádná další knihovna zip třetí strany – stačí vestavěný prostor názvů `System.IO.Compression` a Aspose.HTML.

## Požadavky

- .NET 6.0 nebo novější (kód funguje také na .NET Framework 4.8).
- Aspose.HTML pro .NET (bezplatná zkušební verze nebo licencovaná verze). Nainstalujte přes NuGet: `dotnet add package Aspose.HTML`.
- Základní znalost práce se soubory a proudy v C#.

Pokud je máte, pojďme na to.

![Diagram jak použít ZipArchive](image.png "Diagram ukazující tok HTML → ZipArchive – jak použít ZipArchive")

## Krok 1: Vytvořte vlastní ResourceHandler

Aspose.HTML volá `ResourceHandler.HandleResource` pro každý externí soubor, který potřebuje zapsat. Přepsáním této metody můžeme rendereru předat proud, který ukazuje přímo na položku ZIP.

```csharp
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Rendering;

/// <summary>
/// Writes each HTML resource (image, CSS, font) into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(Stream zipStream)
    {
        // Open the archive for updating; leaveOpen keeps the underlying stream alive.
        _zipArchive = new ZipArchive(zipStream, ZipArchiveMode.Update, leaveOpen: true);
    }

    public override Stream HandleResource(ResourceInfo info)
    {
        // The URI's AbsolutePath contains the file name (e.g., "/images/logo.png").
        // Trim the leading slash so the entry appears at the root of the zip.
        var entryName = info.Uri.AbsolutePath.TrimStart('/');
        var entry = _zipArchive.CreateEntry(entryName, CompressionLevel.Optimal);

        // Return the entry's stream; Aspose will write the content straight into it.
        return entry.Open();
    }
}
```

**Proč vlastní handler?**  
Bez něj by Aspose.HTML zapisoval každý zdroj do dočasného souboru na disku a vy byste museli vše ručně zkopírovat do ZIP. Tento handler odstraňuje mezikrok, snižuje I/O a udržuje kód přehledný.

## Krok 2: Načtěte HTML dokument

Nyní jednoduše načteme zdrojový soubor. Aspose.HTML podporuje jak lokální cesty, tak URL, takže můžete odkazovat na vzdálenou stránku, pokud chcete.

```csharp
// Replace with the folder where your HTML lives.
string inputPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// The HTMLDocument constructor reads the file and parses it.
var document = new HTMLDocument(inputPath);
```

**Tip:** Pokud váš HTML odkazuje na zdroje pomocí relativních URL, ujistěte se, že soubor `input.html` leží vedle těchto aktiv. `ResourceHandler` obdrží přesné cesty, které Aspose vyřeší.

## Krok 3: Připojte ZipResourceHandler a uložte

Když je dokument připraven a náš handler definován, otevřeme `FileStream` pro výstupní ZIP, vytvoříme instanci handleru a zavoláme `document.Save`. Operace ukládání spustí `HandleResource` pro každý externí soubor.

```csharp
// The final ZIP will be placed in the same directory.
string zipPath = Path.Combine("YOUR_DIRECTORY", "output.zip");

// Open a FileStream for the zip – FileMode.Create overwrites any existing file.
using (var zipStream = new FileStream(zipPath, FileMode.Create))
{
    var zipHandler = new ZipResourceHandler(zipStream);

    // Save the HTML document; the handler captures all linked resources.
    document.Save(zipHandler);
}
```

Po dokončení `Save` obsahuje `output.zip`:

```
/index.html          (the original HTML file)
/styles/main.css
/images/logo.png
/fonts/open-sans.ttf
...
```

ZIP můžete otevřít v libovolném správci archivů a ověřit strukturu.

## Krok 4: Ověřte výsledek (volitelné)

Rychlá kontrola vám ušetří pozdější záhadné chyby chybějících obrázků.

```csharp
using (var archive = ZipFile.OpenRead(zipPath))
{
    Console.WriteLine("Entries in the ZIP:");
    foreach (var entry in archive.Entries)
    {
        Console.WriteLine($"- {entry.FullName} ({entry.Length} bytes)");
    }
}
```

Spuštěním tohoto úryvku se vypíše každé jméno souboru, což potvrzuje, že proces **create zip from html** byl úspěšný.

## Běžné okrajové případy a jak je řešit

| Situace | Na co si dát pozor | Navrhované řešení |
|-----------|-------------------|---------------|
| **Absolutní URL** (např. `https://example.com/img.png`) | Aspose se pokusí stáhnout zdroj; handler obdrží proud ukazující na dočasný soubor. | Ujistěte se, že váš počítač má přístup k internetu, nebo předem stáhněte aktiva a přepište HTML tak, aby používalo lokální cesty. |
| **Duplicitní názvy souborů** (dvě obrázky pojmenované `logo.png` v různých složkách) | Položky ZIP musí mít unikátní cesty; jinak druhá položka přepíše první. | Zachovejte hierarchii složek v názvu položky (`info.Uri.AbsolutePath.TrimStart('/')`). |
| **Velké zdroje** (videá o velikosti megabajtů) | Zapisování přímo do položky zip je v pořádku, ale můžete chtít nastavit `CompressionLevel.NoCompression` pro již komprimovaná média. | Upravte `CreateEntry(entryName, CompressionLevel.NoCompression)` pro známé typy médií. |
| **Nepodporované formáty** (např. SVG s externími fonty) | Některé zdroje mohou odkazovat na další soubory, které Aspose automaticky nevyřeší. | Manuálně přidejte tyto soubory do ZIP po volání `Save`. |

## Tipy pro produkční kód

- **Správně uvolňujte** – Jak `ZipArchive`, tak `HTMLDocument` implementují `IDisposable`. Zabalte je do bloků `using`, jak je ukázáno, aby se uvolnily nativní zdroje.
- **Bezpečnost vláken** – Handler není thread‑safe; vyhněte se použití stejné instance `ZipResourceHandler` z více vláken.
- **Výkon** – Pro obrovské HTML balíčky zvažte streamování samotného HTML do ZIP (`zipArchive.CreateEntry("index.html").Open()`), pak zavolejte `document.Save(stream)`, kde `stream` je proud této položky.

## Kompletní funkční příklad

Níže je kompletní program, který můžete zkopírovat a vložit do konzolové aplikace. Obsahuje všechny `using` direktivy, ošetření chyb a komentáře.

```csharp
// ------------------------------------------------------------
// How to Use ZipArchive in C# – Save HTML as ZIP (Full Demo)
// ------------------------------------------------------------
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Rendering;

class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(Stream zipStream)
    {
        _zipArchive = new ZipArchive(zipStream, ZipArchiveMode.Update, leaveOpen: true);
    }

    public override Stream HandleResource(ResourceInfo info)
    {
        var entryName = info.Uri.AbsolutePath.TrimStart('/');
        var entry = _zipArchive.CreateEntry(entryName, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Paths – adjust to your environment.
            string baseDir = Path.Combine(Environment.CurrentDirectory, "DemoFiles");
            string htmlPath = Path.Combine(baseDir, "input.html");
            string zipPath  = Path.Combine(baseDir, "output.zip");

            // 2️⃣ Load the HTML document.
            var document = new HTMLDocument(htmlPath);

            // 3️⃣ Open the ZIP stream and save.
            using (var zipStream = new FileStream(zipPath, FileMode.Create))
            {
                var zipHandler = new ZipResourceHandler(zipStream);
                document.Save(zipHandler);
            }

            // 4️⃣ Quick verification.
            Console.WriteLine($"ZIP created at: {zipPath}");
            using (var archive = ZipFile.OpenRead(zipPath))
            {
                Console.WriteLine("Contents:");
                foreach (var entry in archive.Entries)
                    Console.WriteLine($"- {entry.FullName} ({entry.Length} bytes)");
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

Zkompilujte pomocí `dotnet run` (nebo vašeho preferovaného IDE) a otevřete `output.zip`. Měli byste vidět původní HTML plus všechny odkazované zdroje, úhledně zabalené. To je celý **create zip archive c#** workflow v akci.

## Závěr

Právě jsme ukázali **jak používat ZipArchive** k **ukládání HTML jako zip** a předvedli čistý způsob **create zip from html** pomocí `ResourceHandler` z Aspose.HTML. Hlavní poznatky jsou:

- Přepište `ResourceHandler`, aby streamoval zdroje přímo do `ZipArchive`.
- Udržujte ZIP otevřený po celou dobu operace ukládání (`leaveOpen: true`).
- Ověřte výstup a řešte okrajové případy jako absolutní URL nebo duplicitní názvy.

Nyní můžete tento vzor integrovat do web‑to‑desktop exportérů, generátorů offline dokumentace nebo jakéhokoli scénáře, kde je potřeba zabalit HTML stránku s jejími zdroji.  

Chcete jít dál? Zkuste komprimovat více HTML stránek do jednoho archivu, nebo přidejte soubor manifestu, který vypíše všechny položky. Můžete také prozkoumat šifrování the

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}