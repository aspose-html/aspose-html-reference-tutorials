---
category: general
date: 2026-09-10
description: Leer hoe je HtmlSaveOptions in C# kunt gebruiken om web‑fontstijlen te
  beheren en HTML‑bestanden op te slaan met Aspose.HTML. Volledig codevoorbeeld en
  praktische tips inbegrepen.
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
language: nl
lastmod: 2026-09-10
og_description: Hoe HtmlSaveOptions in C# te gebruiken om vette en cursieve web‑fontstijlen
  in te schakelen bij het opslaan van HTML met Aspose.HTML. Volg het volledige voorbeeld
  en de best‑practice‑tips.
og_image_alt: Screenshot showing how to use HtmlSaveOptions to save an HTML file in
  C#
og_title: Hoe HtmlSaveOptions te gebruiken in C# met Aspose.HTML – stapsgewijze handleiding
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
title: Hoe HtmlSaveOptions te gebruiken in C# met Aspose.HTML
url: /nl/net/working-with-html-documents/how-to-use-htmlsaveoptions-in-c-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe HtmlSaveOptions te gebruiken in C# met Aspose.HTML

Als je de manier wilt controleren waarop Aspose.HTML een HTML‑document opslaat, **is het leren gebruiken van HtmlSaveOptions essentieel**. Deze tutorial laat je stap‑voor‑stap zien hoe je HtmlSaveOptions gebruikt om vette en cursieve web‑font‑stijlen in te schakelen tijdens het opslaan van een document.

De Aspose HTML‑bibliotheek biedt een uitgebreide API voor het laden, manipuleren en exporteren van HTML‑inhoud. Aan het einde van deze gids kun je:

* Een bestaand HTML‑bestand laden in een `HTMLDocument`.
* `HtmlSaveOptions` configureren om specifieke `WebFontStyle`‑vlaggen toe te passen.
* Het gewijzigde document opslaan naar een nieuwe locatie of een stream.
* De oplossing uitbreiden voor andere lettertype‑stijlen, aangepaste CSS en foutafhandeling.

## Vereisten

Zorg ervoor dat je het volgende hebt:

* .NET 6.0 of hoger geïnstalleerd.
* Een geldige licentie voor **Aspose.HTML for .NET** (de gratis proefversie werkt voor dit voorbeeld).
* Visual Studio 2022 (of een andere C#‑IDE) om de code te compileren en uit te voeren.

Er zijn geen extra NuGet‑pakketten vereist naast `Aspose.HTML`.

## Stap 1: Het project instellen en namespaces importeren

Maak een nieuw **Console App**‑project aan en voeg het Aspose.HTML NuGet‑pakket toe:

```bash
dotnet add package Aspose.HTML
```

Importeer vervolgens bovenaan `Program.cs` de benodigde namespaces:

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
```

Deze namespaces maken de types `HTMLDocument`, `HtmlSaveOptions` en `WebFontStyle` beschikbaar die je gedurende de tutorial zult gebruiken.

## Stap 2: Laad het bron‑HTML‑document

De eerste handeling is het lezen van de HTML die je wilt verwerken. Vervang `"YOUR_DIRECTORY/input.html"` door het daadwerkelijke pad naar je bestand.

```csharp
// Load the source HTML document from disk
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

`HTMLDocument` parseert de markup, bouwt een DOM‑boom en maakt deze klaar voor manipulatie. Als het bestand niet bestaat, wordt er een uitzondering gegooid, dus je wilt deze oproep wellicht omhullen met een try‑catch‑blok voor productiecodel.

## Stap 3: Maak en configureer HtmlSaveOptions

`HtmlSaveOptions` stelt je in staat het opslaan fijn af te stemmen. Om vette en cursieve web‑font‑stijlen in te schakelen, combineer je de bijbehorende `WebFontStyle`‑vlaggen met de bitwise OR‑operator (`|`).

```csharp
// Create a new HtmlSaveOptions instance
HtmlSaveOptions saveOptions = new HtmlSaveOptions();

// Enable bold and italic web‑font styles (equivalent to the old FontStyle flags)
saveOptions.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

### Waarom WebFontStyle configureren?

Wanneer je een HTML‑document exporteert, kan Aspose.HTML web‑fonts insluiten die overeenkomen met de oorspronkelijke opmaak. Door `WebFontStyle` in te stellen, vertel je de exporter welke font‑varianten moeten worden opgenomen. Dit verkleint de uiteindelijke bestandsgrootte wanneer je alleen specifieke stijlen nodig hebt en garandeert dat de gerenderde output overeenkomt met de bron.

#### Veelvoorkomende variaties

| Gewenste stijl | Bijbehorende `WebFontStyle`‑vlag |
|----------------|-----------------------------------|
| Normal (regular) | `WebFontStyle.Regular` |
| Bold | `WebFontStyle.Bold` |
| Italic | `WebFontStyle.Italic` |
| Bold + Italic | `WebFontStyle.Bold | WebFontStyle.Italic` |
| All variants | `WebFontStyle.All` |

Je kunt elke gewenste combinatie gebruiken die bij je scenario past.

## Stap 4: Sla het document op met de geconfigureerde opties

Schrijf nu het document naar een nieuw bestand. De `Save`‑methode accepteert het doelpad en de `HtmlSaveOptions`‑instantie die je hebt voorbereid.

```csharp
// Save the processed HTML using the configured options
document.Save("YOUR_DIRECTORY/output.html", saveOptions);
```

Als je naar een memory‑stream wilt schrijven (bijvoorbeeld om het bestand via HTTP te verzenden), gebruik dan de overload die een `Stream`‑object accepteert:

```csharp
using (var stream = new MemoryStream())
{
    document.Save(stream, saveOptions);
    // Reset the position to read the content later
    stream.Position = 0;
    // Example: return the stream from a Web API endpoint
}
```

## Stap 5: Verifieer het resultaat

Open `output.html` in een browser of inspecteer het bestand met een teksteditor. Je zou moeten zien dat het `<style>`‑blok nu `@font-face`‑regels bevat voor zowel de vette als de cursieve varianten van alle web‑fonts die in het oorspronkelijke document worden gebruikt.

**Verwacht output‑fragment:**

```html
<link rel="stylesheet" href="fonts/Roboto-Bold.woff2" type="font/woff2">
<link rel="stylesheet" href="fonts/Roboto-Italic.woff2" type="font/woff2">
```

Als de oorspronkelijke HTML een lettertype‑familie verwees die alleen een reguliere dikte had, zal Aspose.HTML alleen dat bestand opnemen, volgens de `WebFontStyle`‑configuratie.

## Geavanceerd: HtmlSaveOptions gebruiken met extra functies

### 5.1 CSS‑inbedding regelen

Je kunt bepalen of je CSS inline wilt insluiten, externe links wilt behouden, of alles wilt insluiten:

```csharp
saveOptions.CssSavingMode = CssSavingMode.EmbedAllCss;
```

### 5.2 Opslaan met een specifieke codering

```csharp
saveOptions.Encoding = Encoding.UTF8;
```

### 5.3 Grote documenten verwerken

Voor zeer grote HTML‑bestanden kun je overwegen de output te streamen om hoog geheugenverbruik te vermijden:

```csharp
using (FileStream fs = new FileStream("large_output.html", FileMode.Create, FileAccess.Write))
{
    document.Save(fs, saveOptions);
}
```

### 5.4 Beste praktijken voor foutafhandeling

Omhul de volledige workflow in een try‑catch‑blok en log de details van de uitzondering. Dit zorgt ervoor dat eventuele I/O‑ of parse‑fouten worden vastgelegd:

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

## Pro‑tip: HtmlSaveOptions hergebruiken voor meerdere opslagen

Als je meerdere documenten moet opslaan met dezelfde font‑style‑configuratie, maak dan één `HtmlSaveOptions`‑instantie aan en hergebruik deze. Dit vermindert de overhead van objectallocatie en garandeert consistente output.

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

## Volledig uitvoerbaar voorbeeld

Hieronder staat het volledige programma dat alle besproken stappen bevat. Kopieer het naar `Program.cs` en voer het uit nadat je de bestandspaden hebt aangepast.

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

### Verwachte console‑output

```
HTML saved successfully to 'YOUR_DIRECTORY/output.html'.
```

Open het gegenereerde `output.html` om te bevestigen dat vette en cursieve web‑font‑stijlen aanwezig zijn.

## Conclusie

Je weet nu **hoe je HtmlSaveOptions** kunt gebruiken om web‑font‑insluiting, CSS‑afhandeling en codering te regelen bij het opslaan van HTML met de Aspose HTML‑bibliotheek in C#. Door de `WebFontStyle`‑vlaggen te configureren kun je de output afstemmen op alleen de font‑varianten die je nodig hebt, wat de prestaties verbetert en de bestandsgrootte verkleint.

Vanaf hier kun je andere `HtmlSaveOptions`‑eigenschappen verkennen, zoals `ImageSavingMode`, `JavaScriptSavingMode`, of meerdere opties combineren voor complexe conversiepijplijnen. Experimenteer met opslaan naar streams voor web‑API’s, of integreer de workflow in een groter document‑generatiesysteem.

---


## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe HTML op te slaan met Aspose.Html – Complete C#‑gids](/html/english/net/working-with-html-documents/how-to-save-html-with-aspose-html-complete-c-guide/)
- [Hoe Aspose te gebruiken om HTML naar PNG te renderen in C#](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-in-c/)
- [Hoe Aspose te gebruiken om HTML naar PNG te renderen – Stapsgewijze gids](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}