---
category: general
date: 2026-09-10
description: Naučte se, jak používat HtmlSaveOptions v C# k řízení stylů webových
  fontů a ukládání HTML souborů pomocí Aspose.HTML. Obsahuje kompletní ukázkový kód
  a praktické tipy.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use htmlsaveoptions
- Aspose HTML library
- WebFontStyle flags
- HTMLDocument conversion
- C# save HTML
- Aspose.Html SaveOptions
language: cs
lastmod: 2026-09-10
og_description: Jak použít HtmlSaveOptions v C# k povolení tučných a kurzívních webových
  fontů při ukládání HTML pomocí Aspose.HTML. Sledujte kompletní příklad a tipy na
  osvědčené postupy.
og_image_alt: Screenshot showing how to use HtmlSaveOptions to save an HTML file in
  C#
og_title: Jak používat HtmlSaveOptions v C# s Aspose.HTML – průvodce krok za krokem
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: Learn how to use HtmlSaveOptions in C# to control web‑font styles and
    save HTML files with Aspose.HTML. Full code example and practical tips included.
  headline: How to use HtmlSaveOptions in C# with Aspose.HTML
  type: TechArticle
- description: Learn how to use HtmlSaveOptions in C# to control web‑font styles and
    save HTML files with Aspose.HTML. Full code example and practical tips included.
  name: How to use HtmlSaveOptions in C# with Aspose.HTML
  steps:
  - name: Why configure WebFontStyle?
    text: 'When you export an HTML document, Aspose.HTML can embed web fonts that
      match the original styling. By setting `WebFontStyle`, you tell the exporter
      which font variants to include. This reduces the final file size when you only
      need specific styles and guarantees that the rendered output matches the '
  - name: 5.1 Controlling CSS embedding
    text: 'You can decide whether to embed CSS inline, keep external links, or embed
      everything:'
  - name: 5.2 Saving to a specific encoding
    text: '```csharp saveOptions.Encoding = Encoding.UTF8; ```'
  - name: 5.3 Handling large documents
    text: 'For very large HTML files, consider streaming the output to avoid high
      memory consumption:'
  - name: 5.4 Error handling best practice
    text: 'Wrap the entire workflow in a try‑catch block and log the exception details.
      This ensures that any I/O or parsing errors are captured:'
  - name: Expected console output
    text: '``` HTML saved successfully to ''YOUR_DIRECTORY/output.html''. ```'
  type: HowTo
tags:
- Aspose.HTML
- C#
- HTML processing
title: Jak použít HtmlSaveOptions v C# s Aspose.HTML
url: /cs/net/working-with-html-documents/how-to-use-htmlsaveoptions-in-c-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat HtmlSaveOptions v C# s Aspose.HTML

Pokud potřebujete řídit, jak Aspose.HTML ukládá HTML dokument, **je nezbytné se naučit, jak používat HtmlSaveOptions**. Tento tutoriál vám krok za krokem ukáže, jak pomocí HtmlSaveOptions povolit tučné a kurzívní web‑fontové styly při ukládání dokumentu.

Knihovna Aspose HTML poskytuje bohaté API pro načítání, manipulaci a export HTML obsahu. Na konci tohoto průvodce budete schopni:

* Načíst existující HTML soubor do `HTMLDocument`.
* Nastavit `HtmlSaveOptions` tak, aby použil konkrétní příznaky `WebFontStyle`.
* Uložit upravený dokument na nové místo nebo do streamu.
* Rozšířit řešení o další fontové styly, vlastní CSS a zpracování chyb.

## Požadavky

Před zahájením se ujistěte, že máte:

* .NET 6.0 nebo novější nainstalovaný.
* Platnou licenci pro **Aspose.HTML for .NET** (pro tento příklad funguje i bezplatná zkušební verze).
* Visual Studio 2022 (nebo jakékoli C# IDE) pro kompilaci a spuštění kódu.

Kromě `Aspose.HTML` nejsou vyžadovány žádné další NuGet balíčky.

## Krok 1: Nastavení projektu a import jmenných prostorů

Vytvořte nový projekt **Console App** a přidejte NuGet balíček Aspose.HTML:

```bash
dotnet add package Aspose.HTML
```

Poté na začátku souboru `Program.cs` importujte požadované jmenné prostory:

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
```

Tyto jmenné prostory poskytují typy `HTMLDocument`, `HtmlSaveOptions` a `WebFontStyle`, které budete během tutoriálu používat.

## Krok 2: Načtení zdrojového HTML dokumentu

Prvním krokem je načíst HTML, které chcete zpracovat. Nahraďte `"YOUR_DIRECTORY/input.html"` skutečnou cestou k vašemu souboru.

```csharp
// Load the source HTML document from disk
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

`HTMLDocument` parsuje značkování, vytvoří strom DOM a připraví jej k manipulaci. Pokud soubor neexistuje, je vyvolána výjimka, takže pro produkční kód můžete tento volání zabalit do bloku try‑catch.

## Krok 3: Vytvoření a konfigurace HtmlSaveOptions

`HtmlSaveOptions` vám umožňuje jemně doladit proces ukládání. Pro povolení tučných a kurzívních web‑fontových stylů kombinujte odpovídající příznaky `WebFontStyle` pomocí bitového OR operátoru (`|`).

```csharp
// Create a new HtmlSaveOptions instance
HtmlSaveOptions saveOptions = new HtmlSaveOptions();

// Enable bold and italic web‑font styles (equivalent to the old FontStyle flags)
saveOptions.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

### Proč konfigurovat WebFontStyle?

Při exportu HTML dokumentu může Aspose.HTML vložit webové fonty, které odpovídají původnímu stylu. Nastavením `WebFontStyle` řeknete exportéru, které varianty fontů zahrnout. To snižuje konečnou velikost souboru, pokud potřebujete jen konkrétní styly, a zajišťuje, že vykreslený výstup odpovídá zdroji.

#### Běžné varianty

| Požadovaný styl | Corresponding `WebFontStyle` flag |
|-----------------|-----------------------------------|
| Normal (regular) | `WebFontStyle.Regular` |
| Bold | `WebFontStyle.Bold` |
| Italic | `WebFontStyle.Italic` |
| Bold + Italic | `WebFontStyle.Bold | WebFontStyle.Italic` |
| All variants | `WebFontStyle.All` |

Můžete kombinovat libovolné varianty, které vyhovují vašemu scénáři.

## Krok 4: Uložení dokumentu s nakonfigurovanými možnostmi

Nyní zapište dokument do nového souboru. Metoda `Save` přijímá cílovou cestu a připravenou instanci `HtmlSaveOptions`.

```csharp
// Save the processed HTML using the configured options
document.Save("YOUR_DIRECTORY/output.html", saveOptions);
```

Pokud potřebujete zapisovat do paměťového streamu (např. pro odeslání souboru přes HTTP), použijte přetížení, které přijímá objekt `Stream`:

```csharp
using (var stream = new MemoryStream())
{
    document.Save(stream, saveOptions);
    // Reset the position to read the content later
    stream.Position = 0;
    // Example: return the stream from a Web API endpoint
}
```

## Krok 5: Ověření výsledku

Otevřete `output.html` v prohlížeči nebo prohlédněte soubor v textovém editoru. Měli byste vidět, že blok `<style>` nyní obsahuje pravidla `@font-face` pro jak tučné, tak kurzívní varianty všech webových fontů odkazovaných v původním dokumentu.

**Očekávaný úryvek výstupu:**

```html
<link rel="stylesheet" href="fonts/Roboto-Bold.woff2" type="font/woff2">
<link rel="stylesheet" href="fonts/Roboto-Italic.woff2" type="font/woff2">
```

Pokud původní HTML odkazovalo na rodinu fontů, která měla jen regulární váhu, Aspose.HTML zahrne pouze tento soubor, respektujíc konfiguraci `WebFontStyle`.

## Pokročilé: Použití HtmlSaveOptions s dalšími funkcemi

### 5.1 Řízení vkládání CSS

Můžete rozhodnout, zda vložit CSS inline, zachovat externí odkazy, nebo vložit vše:

```csharp
saveOptions.CssSavingMode = CssSavingMode.EmbedAllCss;
```

### 5.2 Ukládání s konkrétním kódováním

```csharp
saveOptions.Encoding = Encoding.UTF8;
```

### 5.3 Zpracování velkých dokumentů

U velmi velkých HTML souborů zvažte streamování výstupu, aby se předešlo vysoké spotřebě paměti:

```csharp
using (FileStream fs = new FileStream("large_output.html", FileMode.Create, FileAccess.Write))
{
    document.Save(fs, saveOptions);
}
```

### 5.4 Nejlepší postupy pro zpracování chyb

Zabalte celý workflow do bloku try‑catch a zaznamenejte podrobnosti výjimky. Tím zajistíte, že budou zachyceny všechny I/O nebo parsingové chyby:

```csharp
try
{
    // Load, configure, and save as shown earlier
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error processing HTML: {ex.Message}");
}
```

## Pro tip: Opakované použití HtmlSaveOptions při více ukládáních

Pokud potřebujete uložit několik dokumentů se stejnou konfigurací font‑stylu, vytvořte jedinou instanci `HtmlSaveOptions` a znovu ji použijte. Tím snížíte režii alokace objektů a zajistíte konzistentní výstup.

```csharp
HtmlSaveOptions sharedOptions = new HtmlSaveOptions
{
    WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic,
    CssSavingMode = CssSavingMode.EmbedAllCss
};

foreach (var file in Directory.GetFiles("input_folder", "*.html"))
{
    HTMLDocument doc = new HTMLDocument(file);
    string outputPath = Path.Combine("output_folder", Path.GetFileName(file));
    doc.Save(outputPath, sharedOptions);
}
```

## Kompletní spustitelný příklad

Níže je celý program, který zahrnuje všechny probírané kroky. Zkopírujte jej do `Program.cs` a spusťte po úpravě cest k souborům.

```csharp
using System;
using System.IO;
using System.Text;
using Aspose.Html;
using Aspose.Html.Drawing;

class Program
{
    static void Main()
    {
        // Define input and output paths
        string inputPath = "YOUR_DIRECTORY/input.html";
        string outputPath = "YOUR_DIRECTORY/output.html";

        try
        {
            // Step 1: Load the source HTML document
            HTMLDocument document = new HTMLDocument(inputPath);

            // Step 2: Create HtmlSaveOptions and enable bold + italic web‑font styles
            HtmlSaveOptions saveOptions = new HtmlSaveOptions
            {
                WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic,
                // Optional: embed all CSS and use UTF‑8 encoding
                CssSavingMode = CssSavingMode.EmbedAllCss,
                Encoding = Encoding.UTF8
            };

            // Step 3: Save the document with the configured options
            document.Save(outputPath, saveOptions);

            Console.WriteLine($"HTML saved successfully to '{outputPath}'.");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

### Očekávaný výstup v konzoli

```
HTML saved successfully to 'YOUR_DIRECTORY/output.html'.
```

Otevřete vygenerovaný `output.html` a ověřte, že jsou přítomny tučné a kurzívní web‑fontové styly.

## Závěr

Nyní víte **jak používat HtmlSaveOptions** k řízení vkládání web‑fontů, zpracování CSS a kódování při ukládání HTML pomocí knihovny Aspose HTML v C#. Konfigurací příznaků `WebFontStyle` můžete přizpůsobit výstup tak, aby zahrnoval jen fontové varianty, které potřebujete, což zlepšuje výkon a snižuje velikost souboru.

Odtud můžete prozkoumat další vlastnosti `HtmlSaveOptions`, jako jsou `ImageSavingMode`, `JavaScriptSavingMode`, nebo kombinovat více možností pro složité konverzní pipeline. Experimentujte s ukládáním do streamů pro webová API nebo integrujte workflow do většího systému generování dokumentů.

---

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak uložit HTML pomocí Aspose.Html – Kompletní průvodce C#](/html/english/net/working-with-html-documents/how-to-save-html-with-aspose-html-complete-c-guide/)
- [Jak použít Aspose k renderování HTML do PNG v C#](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-in-c/)
- [Jak použít Aspose k renderování HTML do PNG – Krok za krokem průvodce](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}