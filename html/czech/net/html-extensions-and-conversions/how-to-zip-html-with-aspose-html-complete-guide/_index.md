---
category: general
date: 2026-03-21
description: Naučte se, jak zkomprimovat HTML soubory s obrázky pomocí Aspose.HTML.
  Tento průvodce pokrývá vlastní manipulátor zdrojů, uložení HTML jako zip a možnosti
  uložení v Aspose HTML.
draft: false
keywords:
- how to zip html
- save html with images
- custom resource handler
- save html as zip
- aspose html save options
language: cs
og_description: Naučte se, jak zabalit HTML s obrázky do zipu pomocí Aspose.HTML.
  Tento tutoriál ukazuje vlastní správce zdrojů, uložení HTML jako zip a nejlepší
  možnosti uložení v Aspose HTML.
og_title: Jak zkomprimovat HTML pomocí Aspose.HTML – kompletní průvodce
tags:
- Aspose.HTML
- C#
- ZIP
- HTML processing
title: Jak zipovat HTML pomocí Aspose.HTML – kompletní průvodce
url: /cs/net/html-extensions-and-conversions/how-to-zip-html-with-aspose-html-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zkomprimovat HTML pomocí Aspose.HTML – Kompletní průvodce

Už jste se někdy zamýšleli **jak zkomprimovat HTML** soubory, které obsahují externí zdroje jako obrázky, CSS nebo JavaScript? Nejste v tom sami. V mnoha projektech potřebujeme dodat jeden balíček, který zachová rozvržení stránky, a komprimace HTML spolu s jeho prostředky je nejčistším řešením.  

V tomto tutoriálu vám ukážeme **jak zkomprimovat HTML** pomocí výkonné knihovny Aspose.HTML a projdeme každý krok – od vytvoření vlastního resource handleru až po nastavení `ZipArchiveSaveOptions`. Na konci budete schopni *uložit HTML s obrázky* uvnitř ZIP archivu a pochopíte vzor **custom resource handler**, který to umožňuje.

Také se dotkneme souvisejících témat, jako je **save HTML as zip**, prozkoumáme relevantní **Aspose HTML save options** a poskytneme vám tipy pro řešení okrajových případů. Žádná externí dokumentace není potřeba – vše, co potřebujete, je zde.

---

## Co budete potřebovat

- **.NET 6+** (nebo jakékoli aktuální .NET runtime, které podporuje Aspose.HTML)
- **Aspose.HTML for .NET** NuGet balíček (verze 23.9 nebo novější)
- Základní vývojové prostředí C# (Visual Studio, Rider nebo VS Code)
- Soubor obrázku (`image.png`) umístěný ve stejné složce jako zdrojový kód (nebo jakýkoli jiný externí zdroj, který chcete zabalit)

To je vše – žádné další nástroje, žádné složité kroky sestavení. Připravení? Ponořme se do toho.

---

## Krok 1: Instalace Aspose.HTML přes NuGet

Nejprve přidejte knihovnu Aspose.HTML do svého projektu. Otevřete terminál ve složce projektu a spusťte:

```bash
dotnet add package Aspose.HTML
```

*Tip:* Pokud používáte Visual Studio, můžete také kliknout pravým tlačítkem na projekt → **Manage NuGet Packages** → vyhledat **Aspose.HTML** a nainstalovat jej odtud.

---

## Krok 2: Vytvoření vlastního Resource Handleru (save html with images)

Když zavoláte `document.Save` s možnostmi ZIP, Aspose.HTML potřebuje způsob, jak zapsat každý externí zdroj (např. `image.png`) do archivu. Zde přichází **custom resource handler**. Přijímá název zdroje a vrací zapisovatelný `Stream`.

```csharp
using Aspose.Html;
using Aspose.Html.Saving;
using System.IO;

/// <summary>
/// Writes each external resource (images, CSS, etc.) to a folder on disk.
/// The folder path is supplied when the handler is instantiated.
/// </summary>
class MyResourceHandler : ResourceHandler
{
    private readonly string _outputFolder;

    public MyResourceHandler(string outputFolder) => _outputFolder = outputFolder;

    public override Stream HandleResource(string resourceName)
    {
        // Build the full path for the resource inside the output folder
        string path = Path.Combine(_outputFolder, resourceName);
        Directory.CreateDirectory(Path.GetDirectoryName(path)!);
        // Return a stream that Aspose.HTML will write the resource to
        return File.OpenWrite(path);
    }
}
```

**Proč je to důležité:** Bez handleru by se Aspose.HTML pokusil vložit zdroje přímo do ZIP, což může vést k chybějícím obrázkům, pokud jsou cesty relativní. Náš handler zaručuje, že každý odkazovaný soubor skončí tam, kde jej HTML očekává.

---

## Krok 3: Definování HTML obsahu (save html as zip)

Pro demonstraci použijeme malý HTML úryvek, který odkazuje na externí obrázek. Klidně nahraďte řetězec svým vlastním markupem.

```csharp
string html = @"<html>
<head>
    <title>Sample Page</title>
</head>
<body>
    <h1>Welcome!</h1>
    <p>This page includes an external image.</p>
    <img src='image.png' alt='Sample image'>
</body>
</html>";
```

Všimněte si atributu `alt` – je dobrý pro přístupnost a také slouží jako užitečná náhrada, pokud se obrázek nenačte.

---

## Krok 4: Načtení HTML do Aspose.HTML Document

Nyní předáme řetězec do Aspose.HTML. Knihovna parsuje markup a vytvoří DOM, který můžeme později uložit.

```csharp
HTMLDocument document = new HTMLDocument(html);
```

To je vše – žádný souborový I/O, žádné dočasné soubory. Objekt `HTMLDocument` nyní obsahuje celou strukturu stránky.

---

## Krok 5: Nastavení ZipArchiveSaveOptions (aspose html save options)

Dále nastavíme **Aspose HTML save options**, které knihovně řeknou, aby vytvořila ZIP archiv. Také připojíme dříve vytvořený custom resource handler.

```csharp
using (var zipStream = new MemoryStream())
{
    // Prepare ZIP save options
    var zipOptions = new ZipArchiveSaveOptions
    {
        // Attach the custom handler so resources are written to the folder
        ResourceHandler = new MyResourceHandler("output/Resources")
    };

    // Save the document (HTML + all referenced resources) into the ZIP stream
    document.Save(zipStream, zipOptions);

    // Optional: write the ZIP to disk for inspection
    File.WriteAllBytes("output/output.zip", zipStream.ToArray());
}
```

**Klíčové body:**
- `ZipArchiveSaveOptions` je třída, která zapouzdřuje **aspose html save options** pro výstup ZIP.
- `ResourceHandler` zajišťuje, že každý externí soubor – například `image.png` – bude uložen vedle HTML.
- `MemoryStream` nám umožňuje držet vše v paměti, dokud se nerozhodneme, kam to zapsat.

---

## Krok 6: Ověření výsledku

Po spuštění programu byste ve složce `output` měli vidět dvě věci:

1. **output.zip** – ZIP archiv obsahující `index.html` a podsložku `Resources`.
2. **Resources/image.png** – skutečný soubor obrázku, na který byl v HTML odkazováno.

Rozbalte ZIP a otevřete `index.html` v prohlížeči. Obrázek by se měl zobrazit správně, což dokazuje, že jste úspěšně pochopili **jak zkomprimovat HTML** s jeho prostředky.

---

## Časté otázky a okrajové případy

### Co když HTML odkazuje na soubory CSS nebo JavaScript?

Stejný `MyResourceHandler` zachytí jakýkoli typ zdroje – CSS, JS, fonty atd. – pokud HTML na ně ukazuje relativní URL. Handler se nezajímá o příponu souboru.

### Jak mohu řídit strukturu složek uvnitř ZIP?

Můžete upravit `resourceName` uvnitř `HandleResource`. Například přidat předponu `"assets/"`, aby se vše umístilo pod adresář `assets`:

```csharp
string path = Path.Combine(_outputFolder, "assets", resourceName);
```

### Můžu streamovat ZIP přímo do webové odpovědi?

Určitě. Místo zápisu na disk můžete vrátit `zipStream` z ASP.NET kontroleru. Jen resetujte pozici streamu:

```csharp
zipStream.Position = 0;
return File(zipStream, "application/zip", "page.zip");
```

### Co s velkými obrázky, které mohou spotřebovat hodně paměti?

Protože handler zapisuje každý zdroj přímo do souborového streamu, spotřeba paměti zůstává nízká. Pouze HTML DOM zůstává v paměti, což je obvykle nenáročné.

---

## Kompletní funkční příklad (Uložení HTML s obrázky jako ZIP)

Níže je kompletní, připravený program. Zkopírujte jej do konzolové aplikace a stiskněte **F5**.

```csharp
using Aspose.Html;
using Aspose.Html.Saving;
using System.IO;

class MyResourceHandler : ResourceHandler
{
    private readonly string _outputFolder;
    public MyResourceHandler(string outputFolder) => _outputFolder = outputFolder;

    public override Stream HandleResource(string resourceName)
    {
        string path = Path.Combine(_outputFolder, resourceName);
        Directory.CreateDirectory(Path.GetDirectoryName(path)!);
        return File.OpenWrite(path);
    }
}

class Program
{
    static void Main()
    {
        // HTML that references an external image
        string html = @"<html>
<head><title>Sample</title></head>
<body>
    <h2>How to Zip HTML Demo</h2>
    <p>Image below is loaded from an external file.</p>
    <img src='image.png' alt='Demo image'>
</body>
</html>";

        // Load HTML into Aspose.HTML document
        HTMLDocument document = new HTMLDocument(html);

        // Prepare ZIP options and attach custom handler
        using var zipStream = new MemoryStream();
        var zipOptions = new ZipArchiveSaveOptions
        {
            ResourceHandler = new MyResourceHandler("output/Resources")
        };

        // Save HTML + resources into ZIP
        document.Save(zipStream, zipOptions);

        // Write ZIP to disk (optional)
        File.WriteAllBytes("output/output.zip", zipStream.ToArray());

        System.Console.WriteLine("ZIP created successfully! Check the 'output' folder.");
    }
}
```

**Očekávaný výstup:** Konzole vypíše *„ZIP created successfully! Check the 'output' folder.“* a adresář `output` obsahuje `output.zip` a soubor `Resources/image.png`.

---

## Závěr

Nyní víte **jak zkomprimovat HTML** dokumenty, které odkazují na externí prostředky pomocí Aspose.HTML. Vytvořením **custom resource handler**, nastavením vhodných **aspose html save options** a využitím `ZipArchiveSaveOptions` můžete spolehlivě **uložit HTML s obrázky** (nebo jakýmikoli jinými prostředky) do jediného, přenosného ZIP souboru.  

Odtud můžete zkoumat:

- **Saving HTML as zip** v koncovém bodu web API pro okamžité stahování.
- Použití stejného vzoru k vložení souborů **CSS** a **JavaScript**.
- Úprava **custom resource handler** pro kompresi obrázků za běhu.

Vyzkoušejte to, upravte handler podle své struktury složek a nechte balení ZIP udělat těžkou práci. Šťastné programování!  

---  

![how to zip html example](/images/how-to-zip-html.png "Illustration showing how to zip html with Aspose.HTML")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}