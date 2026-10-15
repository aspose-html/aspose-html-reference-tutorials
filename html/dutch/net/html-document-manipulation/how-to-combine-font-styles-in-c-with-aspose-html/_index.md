---
category: general
date: 2026-10-15
description: Combineer lettertype‑stijlen in C# door de lettertypefamilie en -grootte
  in te stellen met de Aspose.HTML Font‑constructor. Leer snel vetgedrukte cursieve
  tekst te maken.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- combine font styles
- set font family
- set font size c#
- c# font constructor
- create bold italic text
language: nl
lastmod: 2026-10-15
og_description: Combineer lettertype‑stijlen in C# met de Aspose.HTML Font‑constructor.
  Deze tutorial laat zien hoe je de lettertypefamilie instelt, de lettergrootte in
  C# instelt en vet‑cursieve tekst maakt.
og_image_alt: Screenshot of C# code that combines font styles with Aspose.HTML
og_title: Combineer lettertype‑stijlen in C# – snelle gids met Aspose.HTML
schemas:
- author: Aspose
  dateModified: '2026-10-15'
  description: Combine font styles in C# by setting font family and size using the
    Aspose.HTML Font constructor. Learn to create bold italic text quickly.
  headline: How to combine font styles in C# with Aspose.HTML
  type: TechArticle
- description: Combine font styles in C# by setting font family and size using the
    Aspose.HTML Font constructor. Learn to create bold italic text quickly.
  name: How to combine font styles in C# with Aspose.HTML
  steps:
  - name: Explanation
    text: '- `"Arial"` – **set font family** to Arial, a widely supported sans‑serif
      typeface. - `12` – **set font size c#** to 12 points, which is a comfortable
      default for body text. - `WebFontStyle.Bold | WebFontStyle.Italic` – this expression
      **combines font styles**. The `|` operator merges the `Bold` and'
  - name: Why this works
    text: '- `paragraph.Style.FontFamily` uses the **set font family** value from
      the `Font` instance. - `paragraph.Style.FontSize` uses the **set font size c#**
      you defined. - The explicit `FontWeight` and `FontStyle` assignments mirror
      the **combine font styles** flags, ensuring the rendered output matches t'
  - name: Pro tip on performance
    text: 'Creating many `Font` objects inside a tight loop can degrade performance.
      Cache commonly used fonts in a dictionary and reuse them:'
  type: HowTo
tags:
- C#
- Aspose.HTML
- Font styling
title: Hoe lettertype‑stijlen combineren in C# met Aspose.HTML
url: /nl/net/html-document-manipulation/how-to-combine-font-styles-in-c-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe lettertype‑stijlen combineren in C# met Aspose.HTML

Als je **lettertype‑stijlen moet combineren** in een C#‑applicatie, laat deze gids je een beknopte manier zien om dit te doen met Aspose.HTML. Je leert hoe je lettertype‑familie instelt, lettergrootte in C# instelt, en de **c# font constructor** gebruikt om vet‑cursieve tekst te maken in slechts een paar regels code.

Ontwikkelaars vragen zich vaak af of ze voor elke stijl een apart `Font`‑object moeten maken of dat één enkele constructor meerdere attributen kan verwerken. Het antwoord is dat je stijlen direct kunt combineren wanneer je het lettertype instantiateert. Deze tutorial loopt het volledige proces door, van het importeren van de juiste namespace tot het renderen van gestylede tekst in een HTML‑document.

## Vereisten

Voordat je begint, zorg dat je het volgende hebt:

- Aspose.HTML for .NET geïnstalleerd (NuGet‑pakket `Aspose.HTML` versie 23.9 of later).
- .NET 6.0+ of .NET Framework 4.7.2+.
- Basiskennis van C#‑syntaxis en object‑georiënteerd programmeren.

Er zijn geen extra externe bibliotheken nodig.

## Stap 1: Importeer de drawing‑namespace

Het eerste wat je moet doen is **de Aspose.Html.Drawing‑namespace importeren** zodat je toegang hebt tot de `Font`‑klasse en gerelateerde teken‑hulpmiddelen.

```csharp
using Aspose.Html.Drawing;
```

> **Waarom?** De `Font`‑klasse bevindt zich in `Aspose.Html.Drawing`. Door deze namespace te importeren is het type beschikbaar zonder elke keer de volledige kwalificatie te gebruiken, waardoor je code schoon en leesbaar blijft.

## Stap 2: Gebruik de C#‑font‑constructor om familie, grootte en stijlen te combineren

De **c# font constructor** accepteert drie parameters: de naam van de lettertype‑familie, de puntgrootte en een bitwise‑combinatie van `WebFontStyle`‑vlaggen. Door de bitwise‑OR‑operator (`|`) te gebruiken, kun je **lettertype‑stijlen combineren** zoals vet en cursief.

```csharp
// Create a Font instance that is both bold and italic
var font = new Font("Arial", 12, WebFontStyle.Bold | WebFontStyle.Italic);
```

### Uitleg

- `"Arial"` – **stel lettertype‑familie in** op Arial, een breed ondersteund schreefloos lettertype.
- `12` – **stel lettergrootte in C#** in op 12 punten, wat een comfortabel standaardformaat is voor body‑tekst.
- `WebFontStyle.Bold | WebFontStyle.Italic` – deze expressie **combineert lettertype‑stijlen**. De `|`‑operator voegt de `Bold`‑ en `Italic`‑vlaggen samen tot één waarde, waardoor de constructor een lettertype kan produceren dat tegelijk vet *en* cursief is.

> **Pro tip:** Als je onderstrepen of doorhalen wilt toevoegen, voeg dan `WebFontStyle.Underline` of `WebFontStyle.Strikethrough` toe in dezelfde expressie.

## Stap 3: Pas het lettertype toe op een HTML‑element

Nu je een `Font`‑object hebt, kun je het toepassen op elk HTML‑element dat styling ondersteunt. Hieronder maken we een eenvoudig HTML‑document, voegen een alinea toe en wijzen de gecombineerde stijl.

```csharp
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

// Create a new HTML document
var document = new HTMLDocument();

// Add a paragraph element
var paragraph = document.CreateElement("p");
paragraph.InnerHtml = "This text is bold and italic using combined font styles.";
document.Body.AppendChild(paragraph);

// Apply the Font object to the paragraph's style
paragraph.Style.FontFamily = font.Family;
paragraph.Style.FontSize = $"{font.Size}pt";
paragraph.Style.FontWeight = "bold";
paragraph.Style.FontStyle = "italic";

// Render the document to an image (optional verification step)
using (var renderer = new ImageRenderer())
{
    renderer.Render(document, "output.png");
}
```

### Waarom dit werkt

- `paragraph.Style.FontFamily` gebruikt de **lettertype‑familie**‑waarde van de `Font`‑instantie.
- `paragraph.Style.FontSize` gebruikt de **lettergrootte in C#** die je hebt gedefinieerd.
- De expliciete `FontWeight`‑ en `FontStyle`‑toewijzingen weerspiegelen de **combineer‑lettertype‑stijlen**‑vlaggen, zodat de gerenderde output overeenkomt met de gewenste vet‑cursieve weergave.

> **Randgeval:** Als de doel‑lettertype‑familie geen cursieve of vette varianten ondersteunt, kan de browser de stijl simuleren, wat de visuele nauwkeurigheid kan beïnvloeden. Test altijd met het daadwerkelijke lettertype dat je wilt leveren.

## Stap 4: Verifieer het resultaat

Voer het programma uit en open `output.png`. Je zou de zin moeten zien gerenderd in Arial, 12 pt, met zowel vet als cursief toegepast. Dit bevestigt dat de **c# font constructor** de stijlen correct heeft gecombineerd.

Als je de HTML liever direct bekijkt, kun je de render‑stap overslaan en het document opslaan:

```csharp
document.Save("styled.html");
```

Open `styled.html` in een moderne browser om dezelfde gestylede alinea te zien.

## Veelvoorkomende variaties en tips

| Doel | Code‑fragment | Opmerkingen |
|------|--------------|-------------|
| **Alleen vet** | `new Font("Arial", 12, WebFontStyle.Bold)` | Gebruik één vlag wanneer je geen cursief nodig hebt. |
| **Vet, cursief, onderstrepen** | `new Font("Arial", 12, WebFontStyle.Bold \| WebFontStyle.Italic \| WebFontStyle.Underline)` | Combineer zoveel stijlen als nodig. |
| **Dynamische grootte** | `var size = 14; var font = new Font("Times New Roman", size, WebFontStyle.Italic);` | Je kunt de grootte tijdens runtime berekenen. |
| **Aangepaste lettertype‑familie** | `new Font("MyCustomFont", 10, WebFontStyle.Bold)` | Zorg dat het aangepaste lettertype beschikbaar is voor de renderengine (bijv. via `@font-face`). |

### Pro tip voor prestaties

Het maken van veel `Font`‑objecten binnen een strakke lus kan de prestaties aantasten. Cache vaak gebruikte lettertypen in een dictionary en hergebruik ze:

```csharp
var fontCache = new Dictionary<string, Font>();
string key = "Arial_12_BoldItalic";

if (!fontCache.TryGetValue(key, out var cachedFont))
{
    cachedFont = new Font("Arial", 12, WebFontStyle.Bold | WebFontStyle.Italic);
    fontCache[key] = cachedFont;
}
```

## Volledig uitvoerbaar voorbeeld

Hieronder vind je een zelfstandig programma dat je kunt kopiëren, plakken en uitvoeren. Het demonstreert de volledige stroom van het importeren van de namespace tot het renderen van de gestylede tekst.

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Rendering.Image;

class Program
{
    static void Main()
    {
        // Step 1: Import Aspose.Html.Drawing (already done via using statements)

        // Step 2: Create a Font that combines bold and italic
        var font = new Font("Arial", 12, WebFontStyle.Bold | WebFontStyle.Italic);

        // Step 3: Build a simple HTML document
        var document = new HTMLDocument();
        var paragraph = document.CreateElement("p");
        paragraph.InnerHtml = "This text is bold and italic using combined font styles.";
        document.Body.AppendChild(paragraph);

        // Apply font settings
        paragraph.Style.FontFamily = font.Family;
        paragraph.Style.FontSize = $"{font.Size}pt";
        paragraph.Style.FontWeight = "bold";
        paragraph.Style.FontStyle = "italic";

        // Optional: Render to PNG for visual verification
        using (var renderer = new ImageRenderer())
        {
            renderer.Render(document, "output.png");
        }

        // Save HTML for manual inspection
        document.Save("styled.html");

        Console.WriteLine("Styled document generated: styled.html and output.png");
    }
}
```

**Verwachte output**

- `styled.html` toont een alinea met Arial 12 pt, vet en cursief.
- `output.png` bevat een afbeelding van dezelfde gestylede alinea.

## Conclusie

Je weet nu hoe je **lettertype‑stijlen kunt combineren** in C# met de Aspose.HTML **c# font constructor**. Door **lettertype‑familie in te stellen**, **lettergrootte in C# in te stellen**, en een bitwise‑OR van `WebFontStyle`‑vlaggen door te geven, kun je **vet‑cursieve tekst maken** (of elke andere combinatie) met minimale code. Pas hetzelfde patroon toe op andere elementen, cache lettertypen voor betere prestaties, en breid de aanpak uit met onderstrepen of doorhalen indien nodig.

Klaar om meer te ontdekken? Probeer:

- `WebFontStyle.Underline` te gebruiken om **lettertype‑onderstreping** in te stellen.
- Aangepaste web‑fonts te laden met `@font-face` en ze toe te passen via dezelfde constructor.
- PDF’s te renderen in plaats van afbeeldingen door `ImageRenderer` te vervangen door `PdfRenderer`.

Veel programmeerplezier, en geniet van de flexibiliteit van het programmatic stylen van tekst in C#!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Create HTML Document C# – Bold Italic Text with Custom Font](/html/english/net/html-document-manipulation/create-html-document-c-bold-italic-text-with-custom-font/)
- [Create HTML document C# – Render to PNG with Bold Italic Font](/html/english/net/rendering-html-documents/create-html-document-c-render-to-png-with-bold-italic-font/)
- [Simpan HTML sebagai PDF di C# – Panduan Lengkap dengan Font](/html/indonesian/net/html-extensions-and-conversions/save-html-as-pdf-in-c-complete-guide-with-fonts/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}