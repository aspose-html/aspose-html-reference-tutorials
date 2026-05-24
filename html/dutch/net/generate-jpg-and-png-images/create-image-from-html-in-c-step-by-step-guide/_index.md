---
category: general
date: 2026-02-19
description: Maak snel een afbeelding van HTML met Aspose.HTML in C#. Leer hoe je
  HTML naar een afbeelding rendert, HTML naar PNG converteert, de afbeeldingsafmetingen
  instelt en een aangepaste lettergrootte instelt.
draft: false
keywords:
- create image from html
- render html to image
- convert html to png
- set image dimensions
- set custom font size
language: nl
og_description: Maak een afbeelding van HTML met Aspose.HTML. Deze gids laat zien
  hoe je HTML rendert naar een afbeelding, HTML converteert naar PNG en de afbeeldingsafmetingen
  instelt met een aangepaste lettergrootte.
og_title: Afbeelding maken van HTML in C# – Complete tutorial
tags:
- Aspose.HTML
- C#
- Image Rendering
title: Afbeelding maken van HTML in C# – Stapsgewijze handleiding
url: /nl/net/generate-jpg-and-png-images/create-image-from-html-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak afbeelding van HTML in C# – Stapsgewijze gids

Heb je ooit **een afbeelding van HTML moeten maken** maar wist je niet welke bibliotheek pixel‑perfecte resultaten zou leveren? Je bent niet de enige. In de .NET‑wereld maakt Aspose.HTML het een fluitje van een cent om **HTML naar afbeelding te renderen**, zodat je elke markup kunt omzetten naar een PNG, JPEG of zelfs een BMP met slechts een paar regels code.

In deze tutorial lopen we een compleet, uitvoerbaar voorbeeld door dat laat zien hoe je **HTML naar PNG kunt converteren**, hoe je **afbeeldingsafmetingen kunt instellen**, en hoe je **een aangepaste lettergrootte kunt instellen** voor perfecte typografische controle. Aan het einde heb je een zelfstandige applicatie die je in elk C#‑project kunt plaatsen.

## Wat je nodig hebt

- **.NET 6+** (de code werkt ook met .NET Framework 4.6+)
- **Aspose.HTML for .NET** – je kunt het ophalen via NuGet (`Install-Package Aspose.HTML`)
- Een eenvoudig HTML‑bestand (`input.html`) dat je wilt omzetten naar een afbeelding
- Een IDE of editor waar je je prettig bij voelt (Visual Studio, Rider, VS Code…)

Er zijn geen andere third‑party tools nodig. De bibliotheek bevat zijn eigen renderengine, dus je hebt geen headless browser of externe services nodig.

---

## Stap 1: Laad het HTML‑document dat je wilt renderen

Het eerste wat we doen is de bron‑HTML lezen. De `HTMLDocument`‑klasse van Aspose.HTML kan een bestand, een URL of zelfs een ruwe string laden.

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Rendering.Image;

// Load the HTML file from disk
HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/input.html");

// Verify that the document is loaded (optional sanity check)
if (htmlDoc == null)
{
    throw new InvalidOperationException("Failed to load the HTML document.");
}
```

**Waarom dit belangrijk is:** Het laden van het document geeft de renderer een DOM om mee te werken. Als je deze stap overslaat, is er niets om op het canvas te schilderen en zal de uitvoer leeg zijn.

---

## Stap 2: Definieer de lettertype‑stijl met de nieuwe `WebFontStyle`‑API

Als je een specifiek lettertype‑gewicht of -stijl nodig hebt — bijvoorbeeld **vet cursief** — kun je `WebFontStyle` gebruiken. Hier behandelen we later ook de **aangepaste lettergrootte**.

```csharp
// Create a WebFontStyle object to control weight and style
WebFontStyle webFontStyle = new WebFontStyle
{
    Weight = FontWeight.Bold,          // Makes the text bold
    Style  = FontStyleEnum.Italic      // Makes the text italic
};
```

**Pro tip:** De `WebFontStyle`‑API werkt met elk web‑safe lettertype of een lettertype dat je via `@font-face` insluit. Als je een niet‑standaard lettertype nodig hebt, verwijs er dan gewoon naar in je HTML en Aspose.HTML haalt het automatisch op.

---

## Stap 3: Stel tekst‑renderopties in (inclusief aangepaste lettergrootte)

Nu vertellen we de renderer hoe tekst moet worden getekend. Dit is het punt waar we **aangepaste lettergrootte** instellen en de stijl toepassen die we zojuist hebben gemaakt.

```csharp
// Configure text rendering options
TextOptions textRenderOptions = new TextOptions
{
    FontFamily = "Arial",          // Fallback generic font
    FontSize   = 14,               // Custom font size in points
    FontStyle  = webFontStyle      // Apply bold‑italic style
};
```

**Waarom deze stap cruciaal is:** Zonder expliciet `FontSize` in te stellen, valt de renderer terug op de grootte die in de HTML of CSS is gedefinieerd. Het overschrijven zorgt voor consistente uitvoer, ongeacht de bron‑markup.

---

## Stap 4: Configureer afbeeldings‑renderopties – grootte, formaat en tekstopmaak

Hier beantwoorden we de vraag **afbeeldingsafmetingen instellen** en bepalen we ook het uitvoerformaat (`PNG` in dit geval). De klasse `ImageRenderingOptions` koppelt alles aan elkaar.

```csharp
// Define the overall image rendering options
ImageRenderingOptions imageRenderOptions = new ImageRenderingOptions
{
    TextOptions   = textRenderOptions, // Attach the text options we built
    Width         = 800,               // Desired image width in pixels
    Height        = 600,               // Desired image height in pixels
    OutputFormat  = ImageFormat.Png    // Convert HTML to PNG
};
```

**Opmerking voor randgevallen:** Als je HTML elementen bevat die de opgegeven breedte/hoogte overschrijden, zal Aspose.HTML ze automatisch bijsnijden of schalen op basis van de CSS‑eigenschappen `Background` en `Overflow`. Je kunt ook `PreserveAspectRatio` inschakelen als je proportionele schaal wilt.

---

## Stap 5: Render het HTML‑document naar een afbeeldingsbestand

Tot slot roepen we `RenderToImage` aan. Deze ene regel doet al het zware werk — lay‑out, rasterisatie en het wegschrijven van het bestand.

```csharp
// Render the document and save it as a PNG file
htmlDoc.RenderToImage("YOUR_DIRECTORY/output.png", imageRenderOptions);

// Quick verification: open the file (optional, works on Windows)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/output.png",
    UseShellExecute = true
});
```

Na het uitvoeren van het programma zou je `output.png` moeten zien met de exacte afmetingen (800 × 600) en de tekst gerenderd in **14‑punt vet cursief Arial**. De afbeelding zal de oorspronkelijke HTML nauwkeurig weergeven, inclusief CSS‑kleuren, randen en ingesloten afbeeldingen.

---

## Volledig werkend voorbeeld (alle stappen gecombineerd)

Hieronder staat het complete, kant‑klaar‑te‑kopiëren programma. Vervang `YOUR_DIRECTORY` door het daadwerkelijke pad waar je `input.html` zich bevindt.

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Rendering.Image;

namespace HtmlToImageDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the HTML document
            HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/input.html");
            if (htmlDoc == null)
                throw new InvalidOperationException("Unable to load HTML document.");

            // 2️⃣ Define font style (bold + italic)
            WebFontStyle webFontStyle = new WebFontStyle
            {
                Weight = FontWeight.Bold,
                Style  = FontStyleEnum.Italic
            };

            // 3️⃣ Set custom font size and family
            TextOptions textRenderOptions = new TextOptions
            {
                FontFamily = "Arial",
                FontSize   = 14,
                FontStyle  = webFontStyle
            };

            // 4️⃣ Configure image size, format, and attach text options
            ImageRenderingOptions imageRenderOptions = new ImageRenderingOptions
            {
                TextOptions   = textRenderOptions,
                Width         = 800,
                Height        = 600,
                OutputFormat  = ImageFormat.Png
            };

            // 5️⃣ Render to PNG
            htmlDoc.RenderToImage("YOUR_DIRECTORY/output.png", imageRenderOptions);

            // Optional: open the generated image automatically
            System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
            {
                FileName = "YOUR_DIRECTORY/output.png",
                UseShellExecute = true
            });
        }
    }
}
```

**Verwachte uitvoer:** Een PNG‑bestand genaamd `output.png` dat exact overeenkomt met de visuele lay‑out van `input.html`, precies 800 × 600 px groot, met alle tekst weergegeven in 14‑pt vet cursief Arial.

---

## Veelgestelde vragen & randgevallen

### Wat als mijn HTML externe CSS of afbeeldingen verwijst?

Aspose.HTML volgt dezelfde regels als een browser. Zolang de paden bereikbaar zijn (absolute URL’s of correcte relatieve paden), downloadt de renderer ze automatisch. Als je de code op een machine zonder internettoegang uitvoert, zorg dan dat alle assets lokaal zijn opgeslagen.

### Kan ik renderen naar JPEG of BMP in plaats van PNG?

Zeker. Verander simpelweg `OutputFormat`:

```csharp
OutputFormat = ImageFormat.Jpeg   // For JPEG
// or
OutputFormat = ImageFormat.Bmp    // For BMP
```

Houd er rekening mee dat JPEG verlieslatend is, waardoor tekst iets wazig kan lijken — PNG is de veiligste keuze voor scherpe typografie.

### Hoe behoud ik de oorspronkelijke beeldverhouding wanneer de HTML‑breedte onbekend is?

Stel slechts één dimensie in (bijvoorbeeld `Width = 800`) en laat de andere op `0`. Aspose.HTML berekent de hoogte automatisch op basis van de gerenderde lay‑out.

```csharp
Width = 800,
Height = 0, // Auto‑calculate height
```

### Wat als ik een andere DPI (dots per inch) nodig heb?

Gebruik de eigenschap `Resolution` binnen `ImageRenderingOptions`:

```csharp
Resolution = new Resolution(300) // 300 DPI for high‑quality prints
```

Een hogere DPI levert grotere bestanden op maar een scherper resultaat — gebruik dit wanneer je de afbeelding wilt afdrukken.

---

## 🎉 Afronding

Je weet nu hoe je **een afbeelding van HTML kunt maken** met Aspose.HTML voor .NET, van het laden van de markup tot **HTML renderen naar afbeelding**, **HTML naar PNG converteren**, **afbeeldingsafmetingen instellen**, en **aangepaste lettergrootte instellen**. Het volledige code‑voorbeeld staat klaar om te draaien, en de toelichtingen geven je het “waarom” achter elke regel, zodat je de oplossing kunt aanpassen aan complexere scenario’s.

### Wat is de volgende stap?

- Experimenteer met **verschillende uitvoerformaten** (JPEG, BMP, GIF) om te zien hoe compressie de kwaliteit beïnvloedt.
- Probeer **aangepaste web‑fonts in te sluiten** via `@font-face` in je HTML en observeer hoe Aspose.HTML ze respecteert.
- Combineer deze techniek met **PDF‑generatie** om gerenderde afbeeldingen direct in rapporten in te sluiten.
- Duik in **geavanceerde renderopties** zoals anti‑aliasing, achtergrondkleuren of SVG‑ondersteuning.

Als je tegen problemen aanloopt, laat dan een reactie achter — happy coding!

---

![Voorbeeld van afbeelding maken van HTML](example-output.png "Afbeelding maken van HTML – gerenderde PNG-uitvoer")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}