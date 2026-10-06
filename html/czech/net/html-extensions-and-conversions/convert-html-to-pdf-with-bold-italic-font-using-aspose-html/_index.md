---
category: general
date: 2026-10-05
description: Převést HTML na PDF pomocí Aspose.HTML a přidat tučné a kurzívní styly
  písma. Naučte se, jak uložit HTML jako PDF a přizpůsobit možnosti vykreslování.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to pdf
- save html as pdf
- add font style pdf
- set bold italic font
- aspose html pdf conversion
language: cs
lastmod: 2026-10-05
og_description: Převod HTML do PDF pomocí Aspose.HTML, přidání tučného a kurzívního
  písma. Tento návod ukazuje, jak uložit HTML jako PDF, nastavit antialiasing a zajistit
  ostré vykreslování textu.
og_image_alt: Screenshot of PDF generated from HTML using Aspose.HTML with bold‑italic
  font
og_title: Převod HTML na PDF s tučným‑kurzivním fontem pomocí Aspose.HTML
schemas:
- author: Aspose
  dateModified: '2026-10-05'
  description: Convert HTML to PDF with Aspose.HTML while adding bold and italic font
    styles. Learn how to save HTML as PDF and customize rendering options.
  headline: Convert HTML to PDF with bold‑italic font using Aspose.HTML
  type: TechArticle
- description: Convert HTML to PDF with Aspose.HTML while adding bold and italic font
    styles. Learn how to save HTML as PDF and customize rendering options.
  name: Convert HTML to PDF with bold‑italic font using Aspose.HTML
  steps:
  - name: Enable antialiasing for smoother images
    text: Antialiasing reduces jagged edges on raster graphics. Setting `UseAntialiasing`
      replaces the older `SmoothingMode` property and yields a cleaner visual result.
  - name: Enable text hinting for clearer rendering
    text: Text hinting aligns glyphs to pixel boundaries, which makes small fonts
      easier to read. The `UseHinting` flag supersedes the older `TextRenderingHint`.
  - name: Define bold and italic font style (set bold italic font)
    text: Aspose.HTML represents font styles with the `WebFontStyle` flags. By combining
      `Bold` and `Italic`, you instruct the renderer to apply both styles to any matching
      text.
  - name: Combine options and **save HTML as PDF**
    text: Now that image, text, and font options are configured, you can invoke `Document.Save`
      with the `HtmlSaveOptions` instance. The output file will be a PDF that reflects
      all of the rendering tweaks.
  - name: Full, runnable example
    text: Putting all of the pieces together gives you a self‑contained program you
      can copy, paste, and run.
  type: HowTo
tags:
- Aspose.HTML
- C#
- PDF generation
- HTML-to-PDF
title: Převod HTML do PDF s tučným‑kurzivním písmem pomocí Aspose.HTML
url: /cs/net/html-extensions-and-conversions/convert-html-to-pdf-with-bold-italic-font-using-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod HTML do PDF s tučným‑kurzivním fontem pomocí Aspose.HTML

Pokud potřebujete **convert HTML to PDF** a chcete, aby výstup zachoval tučný a kurzivní text, tento průvodce vám přesně ukáže, jak to provést pomocí Aspose.HTML. Naučíte se, jak *save HTML as PDF* při konfiguraci možností vykreslování pro hladké obrázky a čitelný text.

Tutoriál pokrývá vše od načtení zdrojového HTML souboru po definování **bold‑italic font style**, takže můžete vytvářet profesionálně vypadající PDF bez dalšího post‑processing. Žádné externí nástroje nejsou potřeba—pouze knihovna Aspose.HTML for .NET.

## Požadavky

* .NET 6.0 nebo novější nainstalováno  
* Visual Studio 2022 (nebo jakékoli C# IDE)  
* Platná licence Aspose.HTML for .NET nebo dočasný evaluační klíč  
* HTML soubor (`input.html`), který chcete převést  

Mít tyto položky připravené zajišťuje, že kód poběží bez chybějících závislostí.

## Převod HTML do PDF s vlastními možnostmi vykreslování

Prvním krokem je načíst HTML dokument a vytvořit instanci `HtmlSaveOptions`, která bude obsahovat všechna naše nastavení vykreslování. Tento objekt říká Aspose.HTML, jak zacházet s obrázky, textem a fonty během **aspose html pdf conversion**.

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Text;

// Load the HTML document you want to convert
var document = new Document("YOUR_DIRECTORY/input.html");

// Create a container for all save options
var saveOptions = new HtmlSaveOptions();
```

### Povolení antialiasingu pro hladší obrázky

Antialiasing snižuje zubaté hrany na rastrových grafikách. Nastavení `UseAntialiasing` nahrazuje starší vlastnost `SmoothingMode` a poskytuje čistší vizuální výsledek.

```csharp
var imageOptions = new ImageRenderingOptions
{
    UseAntialiasing = true   // smoother image rendering
};

saveOptions.ImageRenderingOptions = imageOptions;
```

### Povolení textového hintingu pro jasnější vykreslování

Textový hinting zarovnává glyfy k pixelovým hranicím, což usnadňuje čtení malých fontů. Příznak `UseHinting` nahrazuje starší `TextRenderingHint`.

```csharp
var textOptions = new TextOptions
{
    UseHinting = true   // clearer text rendering
};

saveOptions.TextOptions = textOptions;
```

### Definování tučného a kurzivního stylu písma (set bold italic font)

Aspose.HTML reprezentuje styly písma pomocí příznaků `WebFontStyle`. Kombinací `Bold` a `Italic` instruujete renderer, aby použil oba styly na jakýkoli odpovídající text.

```csharp
var fontStyle = new WebFontStyle
{
    Style = WebFontStyle.Bold | WebFontStyle.Italic   // set bold italic font
};

// Apply the style to the document's default font settings
document.DefaultFont = new FontSettings
{
    FontStyle = fontStyle
};
```

> **Pro tip:** Pokud váš HTML již označuje text značkami `<b>` nebo `<i>`, renderer tyto značky automaticky respektuje. Explicitní přístup `WebFontStyle` je užitečný, když chcete vynutit styl v celém dokumentu.

### Kombinace možností a **save HTML as PDF**

Nyní, když jsou nastaveny možnosti obrázků, textu a fontů, můžete zavolat `Document.Save` s instancí `HtmlSaveOptions`. Výstupní soubor bude PDF, který odráží všechny úpravy vykreslování.

```csharp
// Save the document as a PDF using the configured options
document.Save("YOUR_DIRECTORY/output.pdf", saveOptions);
```

### Kompletní, spustitelný příklad

Sestavením všech částí dohromady získáte samostatný program, který můžete zkopírovat, vložit a spustit.

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Text;
using Aspose.Html.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the HTML document you want to convert
        var document = new Document("YOUR_DIRECTORY/input.html");

        // 2️⃣ Configure image rendering (antialiasing)
        var imageOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true
        };

        // 3️⃣ Configure text rendering (hinting)
        var textOptions = new TextOptions
        {
            UseHinting = true
        };

        // 4️⃣ Define bold‑italic font style
        var fontStyle = new WebFontStyle
        {
            Style = WebFontStyle.Bold | WebFontStyle.Italic
        };
        document.DefaultFont = new FontSettings
        {
            FontStyle = fontStyle
        };

        // 5️⃣ Bundle all options into HtmlSaveOptions
        var saveOptions = new HtmlSaveOptions
        {
            ImageRenderingOptions = imageOptions,
            TextOptions = textOptions
        };

        // 6️⃣ Save the HTML as a PDF
        document.Save("YOUR_DIRECTORY/output.pdf", saveOptions);
    }
}
```

**Expected output:** Soubor pojmenovaný `output.pdf` umístěný v `YOUR_DIRECTORY`. Otevřete jej v libovolném PDF prohlížeči a uvidíte původní HTML obsah vykreslený s hladkými obrázky a **bold‑italic** textem tam, kde je to relevantní.

## Časté otázky a řešení okrajových případů

| Question | Answer |
|----------|--------|
| *Co když moje HTML používá vlastní webový font?* | Přidejte soubor fontu do stejné složky jako HTML a odkažte na něj pomocí `@font-face` v `<style>` bloku. Aspose.HTML během konverze automaticky vloží font. |
| *Způsobí velké HTML soubory problémy s pamětí?* | U velmi velkých dokumentů zvažte konverzi po stránkách pomocí `Document.Pages` a ukládání každého segmentu samostatně, poté sloučte PDF pomocí knihovny určené pro PDF. |
| *Jak změním velikost stránky PDF?* | Nastavte `saveOptions.PageSetup.PaperSize = PaperSize.A4;` před voláním `Save`. |
| *Mohu šifrovat výsledné PDF?* | Ano. Použijte `PdfSaveOptions` (namísto `HtmlSaveOptions`) a nastavte vlastnosti `Encryption`. Tento tutoriál se pro jednoduchost soustředí na `HtmlSaveOptions`. |
| *Co když výstup vypadá rozmazaně?* | Ověřte, že `UseAntialiasing` je `true`, a zvyšte DPI obrázku pomocí `imageOptions.Dpi = 300;`. Vyšší DPI poskytuje ostřejší rastrové obrázky za cenu větší velikosti souboru. |

## Tipy pro produkční použití

* **License early:** Zaregistrujte svou licenci Aspose.HTML před vytvořením objektu `Document`, abyste se vyhnuli zprávám o vodoznaku.  
  ```csharp
  var license = new Aspose.Html.License();
  license.SetLicense("Aspose.HTML.lic");
  ```
* **Path handling:** Použijte `Path.Combine` pro bezpečnou tvorbu cest k souborům napříč Windows, Linux a macOS.  
* **Logging:** Zabalte konverzi do bloku `try / catch` a zaznamenejte `HtmlConversionException` pro odstraňování problémů.  
* **Performance:** Znovu použijte jedinou instanci `HtmlSaveOptions`, pokud převádíte mnoho souborů najednou; vytvoření nové instance pro každý soubor přidává režii.

## Závěr

Nyní máte kompletní, připravené řešení pro **convert HTML to PDF**, které **přidává funkce stylu písma PDF** jako **set bold italic font**. Příklad ukazuje celý workflow **aspose html pdf conversion**: načtení HTML, konfiguraci antialiasingu a hintingu, definování tučného‑kurzivního stylu a nakonec **save html as pdf**.

Odtud můžete zkoumat další úpravy—například vkládání vlastních fontů, změnu okrajů stránky nebo aplikaci vodoznaků. Experimentujte s různými možnostmi vykreslování, které Aspose.HTML poskytuje, a doladíte své PDF pro jakýkoli scénář. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Převod HTML do PDF v Javě – Kompletní průvodce s vkládáním fontů](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-complete-guide-with-font-embeddi/)
- [Převod HTML do PDF v Javě – Nastavení velikosti stránky PDF, rozlišení a uložení HTML](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-set-pdf-page-size-resolution-and/)
- [Jak používat Aspose – Dávkový převod HTML do PDF v Javě](/html/english/java/conversion-html-to-other-formats/how-to-use-aspose-batch-convert-html-to-pdf-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}