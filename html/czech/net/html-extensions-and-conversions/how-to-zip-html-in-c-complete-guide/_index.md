---
category: general
date: 2026-03-18
description: Jak rychle zipovat HTML soubory v C# pomocí Aspose.Html a vlastního resource
  handleru – naučte se komprimovat HTML dokument a vytvářet zip archivy.
draft: false
keywords:
- how to zip html
- compress html document
- custom resource handler
- c# zip file example
- how to create zip
language: cs
og_description: Jak rychle zkomprimovat HTML soubory v C# pomocí Aspose.Html a vlastního
  manipulátoru zdrojů. Ovládněte techniky komprese HTML dokumentů a vytvářejte zip
  archivy.
og_title: Jak zipovat HTML v C# – Kompletní průvodce
tags:
- C#
- Aspose.Html
- ZIP
- File Compression
title: Jak zipovat HTML v C# – Kompletní průvodce
url: /cs/net/html-extensions-and-conversions/how-to-zip-html-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zkomprimovat HTML v C# – Kompletní průvodce

Už jste se někdy zamýšleli **jak zkomprimovat html** soubory přímo z vaší .NET aplikace, aniž byste je nejprve ukládali na disk? Možná jste vytvořili nástroj pro webové reportování, který generuje spoustu HTML stránek, CSS a obrázků, a potřebujete úhledný balíček k odeslání klientovi. Dobrou zprávou je, že to můžete udělat v několika řádcích C# kódu a nemusíte se uchylovat k externím nástrojům příkazové řádky.

V tomto tutoriálu projdeme praktickým **c# zip file example**, který používá `ResourceHandler` z Aspose.Html k **compress html document** zdrojům za běhu. Na konci budete mít znovupoužitelný vlastní handler zdrojů, připravený úryvek k okamžitému spuštění a jasnou představu o **how to create zip** archivech pro jakoukoli sadu webových aktiv. Nepotřebujete žádné další NuGet balíčky kromě Aspose.Html a přístup funguje s .NET 6+ i s klasickým .NET Framework.

---

## Co budete potřebovat

- **Aspose.Html for .NET** (jakákoli recentní verze; ukázané API funguje s 23.x a novějšími).  
- Vývojové prostředí .NET (Visual Studio, Rider nebo `dotnet` CLI).  
- Základní znalost C# tříd a streamů.  

To je vše. Pokud už máte projekt, který generuje HTML pomocí Aspose.Html, můžete kód vložit a okamžitě začít komprimovat.

---

## Jak zkomprimovat HTML pomocí vlastního Resource Handleru

Základní myšlenka je jednoduchá: když Aspose.Html ukládá dokument, požádá `ResourceHandler` o `Stream` pro každý zdroj (HTML soubor, CSS, obrázek atd.). Poskytnutím handleru, který zapisuje tyto streamy do `ZipArchive`, získáme workflow **compress html document**, který se nikdy nedotýká souborového systému.

### Krok 1: Vytvořte třídu ZipHandler

Nejprve definujeme třídu, která dědí z `ResourceHandler`. Její úkolem je otevřít nový záznam v ZIP pro každý příchozí název zdroje.

```csharp
using Aspose.Html;
using Aspose.Html.Saving;
using System.IO.Compression;

/// <summary>
/// Writes each HTML resource (HTML, CSS, images, etc.) into a ZipArchive entry.
/// </summary>
class ZipHandler : ResourceHandler
{
    private readonly ZipArchive _archive;

    public ZipHandler(ZipArchive archive) => _archive = archive;

    public override Stream HandleResource(string name, string mimeType)
    {
        // The entry name mirrors the resource path (e.g., "index.html" or "css/style.css").
        var entry = _archive.CreateEntry(name, CompressionLevel.Fastest);
        return entry.Open(); // The stream the Aspose.Html saver will write into.
    }
}
```

> **Proč je to důležité:** Vrácením streamu spojeného se záznamem ZIP se vyhneme dočasným souborům a vše držíme v paměti (nebo přímo na disku, pokud je použit `FileStream`). To je jádro vzoru **custom resource handler**.

### Krok 2: Nastavte ZIP archiv

Dále otevřeme `FileStream` pro finální zip soubor a zabalíme jej do `ZipArchive`. Příznak `leaveOpen: true` nám umožní udržet stream otevřený, dokud Aspose.Html nedokončí zápis.

```csharp
using var zipStream = new FileStream("output.zip", FileMode.Create);
using var archive = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: true);
```

> **Tip:** Pokud dáváte přednost uchovávat zip v paměti (např. pro odpověď API), nahraďte `FileStream` za `MemoryStream` a později zavolejte `ToArray()`.

### Krok 3: Vytvořte ukázkový HTML dokument

Pro demonstraci vytvoříme malou HTML stránku, která odkazuje na CSS soubor a obrázek. Aspose.Html nám umožňuje programově vytvořit DOM.

```csharp
var htmlDoc = new HtmlDocument();

// Add a simple stylesheet entry (Aspose.Html will ask the handler for "styles/style.css").
var style = htmlDoc.CreateElement("style");
style.InnerHtml = "body { font-family: Arial; background:#f9f9f9; }";
htmlDoc.Head.AppendChild(style);

// Add an image element (the handler will request "images/logo.png").
var img = htmlDoc.CreateElement("img");
img.SetAttribute("src", "images/logo.png");
img.SetAttribute("alt", "Demo Logo");

// Assemble the body.
htmlDoc.Body.AppendChild(htmlDoc.CreateElement("h1")).InnerHtml = "ZIP Demo";
htmlDoc.Body.AppendChild(img);
```

> **Poznámka k okrajovým případům:** Pokud váš HTML odkazuje na externí URL, handler bude stále volán s těmito URL jako názvy. Můžete je filtrovat nebo zdroje stáhnout na požádání – něco, co můžete chtít pro produkční **compress html document** utilitu.

### Krok 4: Připojte handler k metodě Saver

Nyní připojíme náš `ZipHandler` k metodě `HtmlDocument.Save`. Objekt `SavingOptions` může zůstat výchozí; v případě potřeby můžete upravit `Encoding` nebo `PrettyPrint`.

```csharp
var zipHandler = new ZipHandler(archive);
htmlDoc.Save(zipHandler, new SavingOptions());
```

When `Save` runs, Aspose.Html will:

1. Zavolá `HandleResource("index.html", "text/html")` → vytvoří záznam `index.html`.  
2. Zavolá `HandleResource("styles/style.css", "text/css")` → vytvoří záznam CSS.  
3. Zavolá `HandleResource("images/logo.png", "image/png")` → vytvoří záznam obrázku.  

Všechny streamy jsou zapisovány přímo do `output.zip`.

### Krok 5: Ověřte výsledek

Po uvolnění `using` bloků je zip soubor připraven. Otevřete jej v libovolném prohlížeči archivů a měli byste vidět strukturu podobnou:

```
output.zip
│─ index.html
│─ styles/style.css
└─ images/logo.png
```

Pokud rozbalíte `index.html` a otevřete jej v prohlížeči, stránka se vykreslí s vloženým stylem a obrázkem – přesně to, co jsme zamýšleli při **how to create zip** archivech pro HTML obsah.

---

## Komprimace HTML dokumentu – kompletní funkční příklad

Níže je kompletní, připravený k zkopírování program, který spojuje výše uvedené kroky do jedné konzolové aplikace. Klidně jej vložte do nového .NET projektu a spusťte.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class ZipHandler : ResourceHandler
{
    private readonly ZipArchive _archive;
    public ZipHandler(ZipArchive archive) => _archive = archive;

    public override Stream HandleResource(string name, string mimeType)
    {
        var entry = _archive.CreateEntry(name, CompressionLevel.Fastest);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // Step 1: Prepare the zip container.
        using var zipStream = new FileStream("output.zip", FileMode.Create);
        using var archive = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: true);

        // Step 2: Build an HTML document in memory.
        var htmlDoc = new HtmlDocument();

        // Inline CSS (will be saved as "styles/style.css").
        var style = htmlDoc.CreateElement("style");
        style.InnerHtml = "body { font-family: Arial; background:#f9f9f9; }";
        htmlDoc.Head.AppendChild(style);

        // Image element (will be saved as "images/logo.png").
        var img = htmlDoc.CreateElement("img");
        img.SetAttribute("src", "images/logo.png");
        img.SetAttribute("alt", "Demo Logo");
        // For demo purposes we embed a tiny placeholder image.
        // In a real scenario you would copy an existing image file into the zip.
        var placeholder = new byte[] {
            0x89,0x50,0x4E,0x47,0x0D,0x0A,0x1A,0x0A, // PNG header
            // ... (binary data omitted for brevity)
        };
        // Write placeholder image directly to the zip entry.
        var imgEntry = archive.CreateEntry("images/logo.png", CompressionLevel.Fastest);
        using (var imgStream = imgEntry.Open())
        {
            imgStream.Write(placeholder, 0, placeholder.Length);
        }

        // Assemble body content.
        htmlDoc.Body.AppendChild(htmlDoc.CreateElement("h1")).InnerHtml = "ZIP Demo";
        htmlDoc.Body.AppendChild(img);

        // Step 3: Save using the custom handler.
        var zipHandler = new ZipHandler(archive);
        htmlDoc.Save(zipHandler, new SavingOptions());

        Console.WriteLine("HTML and resources have been zipped to output.zip");
    }
}
```

**Očekávaný výstup:** Spuštění programu vypíše *„HTML and resources have been zipped to output.zip“* a vytvoří `output.zip` obsahující `index.html`, `styles/style.css` a `images/logo.png`. Otevření `index.html` po rozbalení zobrazí nadpis „ZIP Demo“ s placeholder obrázkem.

---

## Časté otázky a úskalí

- **Potřebuji přidat reference na System.IO.Compression?**  
  Ano—ujistěte se, že váš projekt odkazuje na `System.IO.Compression` a `System.IO.Compression.FileSystem` (poslední pro `ZipArchive` na .NET Framework).

- **Co když můj HTML odkazuje na vzdálené URL?**  
  Handler získá URL jako název zdroje. Můžete tyto zdroje buď přeskočit (vrátit `Stream.Null`) nebo je nejprve stáhnout a pak zapsat do zipu. Tato flexibilita je důvod, proč je **custom resource handler** tak výkonný.

- **Mohu ovládat úroveň komprese?**  
  Rozhodně—`CompressionLevel.Fastest`, `Optimal` nebo `NoCompression` jsou akceptovány metodou `CreateEntry`. Pro velké dávky HTML často `Optimal` poskytuje nejlepší poměr velikosti a rychlosti.

- **Je tento přístup thread‑safe?**  
  Instance `ZipArchive` není thread‑safe, takže všechny zápisy provádějte v jednom vlákně nebo archiv chraňte zámkem, pokud paralelizujete generování dokumentů.

---

## Rozšíření příkladu – reálné scénáře

1. **Dávkové zpracování více reportů:** Procházejte kolekci objektů `HtmlDocument`, znovu použijte stejný `ZipArchive` a uložte každý report do vlastní složky v zipu.

2. **Poskytnutí ZIP přes HTTP:** Nahraďte `FileStream` za `MemoryStream` a poté zapište `memoryStream.ToArray()` do ASP.NET Core `FileResult` s typem obsahu `application/zip`.

3. **Přidání souboru manifestu:** Před uzavřením archivu vytvořte

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}