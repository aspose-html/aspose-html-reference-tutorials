---
category: general
date: 2026-08-19
description: Uložte HTML jako ZIP v C# pomocí Aspose.HTML a vlastního správce zdrojů.
  Postupujte podle tohoto průvodce krok za krokem, abyste vložili zdroje a vytvořili
  přenosný archiv.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save HTML as ZIP
- custom resource handler
- Aspose.HTML C#
- HTML archive generation
- resource streaming C#
language: cs
lastmod: 2026-08-19
og_description: Uložte HTML jako ZIP v C# pomocí Aspose.HTML a vlastního manipulátoru
  zdrojů. Tento tutoriál ukazuje kompletní kód, vysvětluje, proč je každý krok důležitý,
  a popisuje běžné úskalí.
og_image_alt: Screenshot of C# code that saves an HTML document as a ZIP archive
og_title: Uložte HTML jako ZIP s vlastním handlerem zdrojů v C# – kompletní průvodce
schemas:
- author: Aspose
  dateModified: '2026-08-19'
  description: Save HTML as ZIP in C# using Aspose.HTML and a custom resource handler.
    Follow this step‑by‑step guide to embed resources and generate a portable archive.
  headline: Save HTML as ZIP with a custom resource handler in C#
  type: TechArticle
- description: Save HTML as ZIP in C# using Aspose.HTML and a custom resource handler.
    Follow this step‑by‑step guide to embed resources and generate a portable archive.
  name: Save HTML as ZIP with a custom resource handler in C#
  steps:
  - name: Saving to a specific folder inside the ZIP
    text: 'If you want all resources to reside under a subfolder (e.g., `assets/`),
      modify the handler to prepend the folder name to each file name:'
  - name: Streaming directly to a network location
    text: 'When the ZIP must be sent over HTTP without touching the local file system,
      use a `MemoryStream` for the final archive:'
  - name: Handling large resources
    text: 'Large images or videos can exhaust memory if you keep everything in `MemoryStream`.
      Switch to a file‑based stream inside the handler:'
  - name: Preserving original URLs
    text: 'Aspose.HTML rewrites the `src`/`href` attributes to point to the new locations
      inside the ZIP. If you need to keep the original URLs for later processing,
      capture them before saving:'
  type: HowTo
tags:
- C#
- Aspose.HTML
- ZIP archive
- resource handling
title: Uložte HTML jako ZIP s vlastním handlerem zdrojů v C#
url: /cs/net/advanced-features/save-html-as-zip-with-a-custom-resource-handler-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Uložení HTML jako ZIP s vlastním manipulátorem zdrojů v C#

Pokud potřebujete **uložit HTML jako ZIP** a zároveň mít kontrolu nad tím, jak jsou ukládány propojené zdroje, tento návod poskytuje kompletní řešení. Naučíte se vytvořit vlastní manipulátor zdrojů, nakonfigurovat možnosti uložení v Aspose.HTML a vygenerovat přenosný ZIP archiv, který obsahuje HTML soubor i jeho soubory.

Správné vložení zdrojů je důležité, když chcete distribuovat samostatnou webovou stránku, archivovat zprávu pro soulad s předpisy nebo uložit snímek pro offline použití. Níže uvedené kroky fungují s Aspose.HTML 23.10 nebo novějším a vyžadují pouze .NET vývojové prostředí.

## Co si vytvoříte

Na konci tohoto tutoriálu budete mít:

* Třídu v C#, která implementuje `ResourceHandler` a vrací proud pro každý zdroj.
* Kód, který načte existující HTML soubor z disku.
* Konfiguraci `HTMLSaveOptions` pro použití vlastního manipulátoru.
* Volání `HTMLDocument.Save`, které vytvoří `output.zip`, ZIP archiv obsahující HTML dokument a všechny odkazované zdroje.

## Předpoklady

* .NET 6.0 SDK nebo novější (příklad funguje také na .NET Framework 4.7.2).
* Visual Studio 2022 nebo jakékoli IDE podporující C# projekty.
* NuGet balíček Aspose.HTML pro .NET (`Aspose.Html`).
* HTML soubor (`example.html`) s alespoň jedním externím zdrojem (obrázek, CSS, skript), abyste mohli vidět manipulátor v akci.

## Krok 1: Vytvořte vlastní manipulátor zdrojů

**Vlastní manipulátor zdrojů** rozhoduje, kam se každý externí asset zapíše. Implementací `ResourceHandler` získáte plnou kontrolu nad výstupním proudem.

```csharp
using Aspose.Html;
using System.IO;

/// <summary>
/// Provides a stream for each resource referenced by the HTML document.
/// </summary>
class MyResourceHandler : ResourceHandler
{
    /// <summary>
    /// Returns a writable stream for the given resource.
    /// </summary>
    /// <param name="resource">Metadata about the resource being saved.</param>
    /// <returns>A stream that Aspose.HTML will write the resource to.</returns>
    public override Stream HandleResource(Resource resource)
    {
        // Create a memory stream for the resource.
        // In production you might write to a file on disk, a cloud blob, or a database.
        return new MemoryStream();
    }
}
```

**Proč je to důležité:**  
`HandleResource` je voláno pro každý externí soubor (obrázky, styly, skripty). Vrácením nového `MemoryStream` umožníte Aspose.HTML shromáždit data v paměti, která později uloží do ZIP archivu. Pokud potřebujete zdroje na disku, nahraďte `new MemoryStream()` voláním `File.Create(Path.Combine(outputFolder, resource.FileName))`.

## Krok 2: Načtěte HTML dokument

Načtěte zdrojový soubor pomocí `HTMLDocument`. Konstruktor přijímá cestu k souboru, URL nebo proud.

```csharp
using Aspose.Html;

// Adjust the path to point to your HTML file.
string htmlPath = Path.Combine("YOUR_DIRECTORY", "example.html");

// Load the document into memory.
HTMLDocument doc = new HTMLDocument(htmlPath);
```

**Proč je to důležité:**  
Načtení dokumentu nejprve zajistí, že Aspose.HTML provede analýzu DOM a objeví všechny propojené zdroje. Knihovna pak předá každý nalezený zdroj manipulátoru definovanému v předchozím kroku.

## Krok 3: Nakonfigurujte možnosti uložení s vlastním manipulátorem

`HTMLSaveOptions` umožňuje specifikovat výstupní formát a manipulátor zdrojů.

```csharp
using Aspose.Html.Saving;

// Create default save options.
HTMLSaveOptions saveOptions = new HTMLSaveOptions();

// Attach the custom resource handler.
saveOptions.ResourceHandler = new MyResourceHandler();
```

**Proč je to důležité:**  
Bez přiřazení `ResourceHandler` zapisuje Aspose.HTML zdroje do dočasné složky na disku, kterou nemůžete ovládat. Propojením vašeho `MyResourceHandler` určíte přesně, jak bude každý zdroj uložen před vytvořením ZIP archivu.

## Krok 4: Uložte dokument jako ZIP archiv

Nakonec zavolejte `HTMLDocument.Save` s `SaveFormat.Zip`. Metoda zkomprimuje HTML soubor a všechny proudy poskytnuté manipulátorem.

```csharp
// Define the output ZIP path.
string zipPath = Path.Combine("YOUR_DIRECTORY", "output.zip");

// Save the document as a ZIP archive.
doc.Save(zipPath, SaveFormat.Zip, saveOptions);
```

Po dokončení volání `output.zip` obsahuje:

* `example.html` – původní HTML soubor s aktualizovanými odkazy na zdroje.
* Všechny externí assety (obrázky, CSS, JS) uložené jako samostatné položky, každou vytvořenou vlastním manipulátorem.

## Ověření výsledku

Otevřete vygenerovaný ZIP v libovolném prohlížeči archivů. Měli byste vidět strukturu složek podobnou:

```
output.zip
│─ example.html
│─ images/
│   └─ logo.png
│─ styles/
│   └─ main.css
│─ scripts/
│   └─ app.js
```

Otevřete `example.html` z rozbalené složky v prohlížeči; stránka by se měla vykreslit přesně jako originál, což potvrzuje, že zdroje byly správně vloženy.

## Běžné varianty a okrajové případy

### Ukládání do konkrétní složky uvnitř ZIP

Pokud chcete, aby všechny zdroje byly umístěny pod podsložkou (např. `assets/`), upravte manipulátor tak, aby před každým názvem souboru přidal název složky:

```csharp
public override Stream HandleResource(Resource resource)
{
    string folder = "assets";
    string entryName = Path.Combine(folder, resource.FileName);
    // Aspose.HTML uses the entry name when packing the ZIP.
    resource.FileName = entryName;
    return new MemoryStream();
}
```

### Přímé streamování na síťové místo

Když musí být ZIP odeslán přes HTTP bez zápisu na lokální souborový systém, použijte `MemoryStream` pro finální archiv:

```csharp
using (var zipStream = new MemoryStream())
{
    doc.Save(zipStream, SaveFormat.Zip, saveOptions);
    zipStream.Position = 0; // Reset for reading.
    // Send zipStream to a web API, store in Azure Blob, etc.
}
```

### Zpracování velkých zdrojů

Velké obrázky nebo videa mohou vyčerpat paměť, pokud vše držíte v `MemoryStream`. Přepněte na soubor‑založený proud uvnitř manipulátoru:

```csharp
public override Stream HandleResource(Resource resource)
{
    string tempPath = Path.GetTempFileName();
    return new FileStream(tempPath, FileMode.Create, FileAccess.Write);
}
```

Po dokončení `doc.Save` můžete dočasné soubory smazat.

### Zachování původních URL

Aspose.HTML přepíše atributy `src`/`href`, aby ukazovaly na nová umístění uvnitř ZIP. Pokud potřebujete zachovat původní URL pro pozdější zpracování, zachyťte je před uložením:

```csharp
foreach (var img in doc.Images)
{
    Console.WriteLine($"Original src: {img.Source}");
}
```

## Profesionální tipy

* **Znovupoužití manipulátoru** – Vytvořte jedinou instanci `MyResourceHandler` a používejte ji napříč více ukládáními, abyste se vyhnuli opakovanému alokování.
* **Validace zdrojů** – V `HandleResource` můžete kontrolovat `resource.MimeType` nebo `resource.FileName` a filtrovat nechtěné soubory (např. přeskočit analytické skripty).
* **Nastavení úrovně komprese** – `HTMLSaveOptions` exponuje `CompressionLevel` (0–9). Vyšší hodnoty produkují menší ZIPy za cenu vyššího zatížení CPU.

## Kompletní, spustitelný příklad

Níže je kompletní program, který můžete zkopírovat do nového konzolového projektu (`dotnet new console`). Ukazuje každý krok od načtení HTML souboru až po vytvoření `output.zip`.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Saving;

class MyResourceHandler : ResourceHandler
{
    public override Stream HandleResource(Resource resource)
    {
        // Return a memory stream for each resource.
        // Replace with FileStream if you need disk persistence.
        return new MemoryStream();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Define paths.
        string baseDir = Path.Combine(Environment.CurrentDirectory, "YOUR_DIRECTORY");
        string htmlPath = Path.Combine(baseDir, "example.html");
        string zipPath = Path.Combine(baseDir, "output.zip");

        // 2️⃣ Load the HTML document.
        HTMLDocument doc = new HTMLDocument(htmlPath);

        // 3️⃣ Configure save options with the custom handler.
        HTMLSaveOptions saveOptions = new HTMLSaveOptions
        {
            ResourceHandler = new MyResourceHandler()
        };

        // 4️⃣ Save as a ZIP archive.
        doc.Save(zipPath, SaveFormat.Zip, saveOptions);

        Console.WriteLine($"HTML saved as ZIP at: {zipPath}");
    }
}
```

**Očekávaný výstup**

```
HTML saved as ZIP at: C:\path\to\YOUR_DIRECTORY\output.zip
```

Rozbalte ZIP a ověřte strukturu popsanou výše.

## Závěr

Nyní víte, jak **uložit HTML jako ZIP** pomocí Aspose.HTML pro .NET a využít **vlastní manipulátor zdrojů** k řízení, kam se každý asset zapíše. Tento přístup vám poskytuje plnou flexibilitu při správě zdrojů, umožňuje zpracování v paměti a snadno se integruje s cloudovými nebo on‑premise workflow.

Dále můžete:

* Rozšířit manipulátor tak, aby zapisoval zdroje do Azure Blob Storage (sekundární klíčové slovo: custom resource handler).
* Kombinovat ZIP s digitálním podpisem pro bezpečnou distribuci dokumentů.
* Použít `HTMLSaveOptions` k vygenerování jiných formátů (např. MHTML) při zachování programové správy zdrojů.

Experimentujte s různými typy proudů, úrovněmi komprese a strukturou složek, aby vyhovovaly požadavkům vašeho projektu. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným vysvětlením, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vlastních projektech.

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Custom Resource Handler in C# – Convert HTML to ZIP Tutorial](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [How to Render HTML – Complete Guide with Custom Resource Handler](/html/english/net/rendering-html-documents/how-to-render-html-complete-guide-with-custom-resource-handl/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}