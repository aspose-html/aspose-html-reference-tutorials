---
category: general
date: 2026-05-22
description: Stel de breedte en hoogte van de afbeelding in bij het converteren van
  een Word‑document naar PNG. Leer hoe je een docx exporteert als afbeelding met hoogwaardige
  weergave in een stapsgewijze tutorial.
draft: false
keywords:
- set image width height
- convert word to png
- save docx as png
- export docx as image
- how to render word
language: nl
og_description: Stel de breedte en hoogte van de afbeelding in bij het converteren
  van een Word‑document naar PNG. Deze tutorial laat zien hoe je een docx exporteert
  als afbeelding met instellingen voor hoge kwaliteit.
og_title: Afbeeldingsbreedte en -hoogte instellen bij het converteren van Word naar
  PNG – Complete gids
schemas:
- author: Aspose
  dateModified: '2026-05-22'
  description: Set image width height while converting a Word document to PNG. Learn
    how to export docx as image with high‑quality rendering in a step‑by‑step tutorial.
  headline: Set Image Width Height When Converting Word to PNG – Full Guide
  type: TechArticle
- description: Set image width height while converting a Word document to PNG. Learn
    how to export docx as image with high‑quality rendering in a step‑by‑step tutorial.
  name: Set Image Width Height When Converting Word to PNG – Full Guide
  steps:
  - name: 1. Preserve Transparent Backgrounds
    text: 'If your Word document contains shapes with transparent backgrounds and
      you want to keep that transparency, set the `BackgroundColor` to `Color.Transparent`:'
  - name: 2. Render Only a Specific Range
    text: Sometimes you only need a paragraph or a table, not the whole page. Use
      `DocumentVisitor` to extract the node and render it separately. That’s a more
      advanced scenario, but it shows **how to render word** content at a granular
      level.
  - name: 3. Adjust DPI Dynamically
    text: 'If you need different DPI per page (e.g., high‑resolution for the cover
      page), modify `Resolution` inside the loop:'
  - name: 4. Batch Processing
    text: When converting dozens of documents, wrap the whole flow in a method and
      reuse the same `ImageRenderingOptions` instance. Re‑using the options object
      reduces allocation overhead.
  type: HowTo
tags:
- Aspose.Words
- C#
- Image Rendering
title: Stel afbeeldingsbreedte en -hoogte in bij het converteren van Word naar PNG
  – volledige gids
url: /nl/net/generate-jpg-and-png-images/set-image-width-height-when-converting-word-to-png-full-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Stel afbeeldingsbreedte en -hoogte in bij het converteren van Word naar PNG – Complete gids

Heb je je ooit afgevraagd hoe je **afbeeldingsbreedte en -hoogte** kunt **instellen terwijl je Word naar PNG converteert**? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer de standaardexport een wazige afbeelding of de verkeerde afmetingen oplevert, en vervolgens besteden ze uren aan het zoeken naar een oplossing die echt werkt.

In deze tutorial lopen we stap voor stap door een schone, end‑to‑end oplossing die laat zien **hoe je Word‑documenten rendert** als PNG‑afbeeldingen, zodat je **docx als PNG kunt opslaan** met precieze breedte‑hoogte‑controle en hoogwaardige antialiasing. Aan het einde heb je een kant‑klaar code‑fragment, een solide begrip van de API‑opties, en een paar pro‑tips om veelvoorkomende valkuilen te vermijden.

## Wat je zult leren

- Een `.docx`‑bestand laden met Aspose.Words for .NET.  
- **Afbeeldingsbreedte en -hoogte instellen** met `ImageRenderingOptions`.  
- **Docx exporteren als afbeelding** (PNG) met ingeschakelde antialiasing.  
- Hoe je **Word naar PNG converteert** voor één pagina of het hele document.  
- Tips voor het verwerken van grote documenten, DPI‑overwegingen en bestandspad‑beheer.

Geen externe tools, geen rommelige command‑line gymnastics—alleen pure C#‑code die je in elk .NET‑project kunt plaatsen.

---

## Vereisten

Voordat we beginnen, zorg dat je het volgende hebt:

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| **.NET 6.0+** (of .NET Framework 4.7.2) | Aspose.Words ondersteunt beide, maar nieuwere runtimes geven betere prestaties. |
| **Aspose.Words for .NET** NuGet‑package (`Install-Package Aspose.Words`) | Biedt de `Document`‑klasse en renderengine. |
| Een **Word‑document** (`.docx`) dat je wilt omzetten naar een PNG. | De bron die je gaat converteren. |
| Basiskennis van C# – je begrijpt `using`‑statements en objectinitialisatie. | Houdt de leercurve zacht. |

Als je het NuGet‑package mist, voer dan het volgende uit in de Package Manager Console:

```powershell
Install-Package Aspose.Words
```

Dat is alles—zodra het package aanwezig is, kun je beginnen met coderen.

---

## Stap 1: Laad het bron‑document

Het eerste wat je moet doen is de bibliotheek wijzen naar het Word‑bestand dat je wilt transformeren.

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Load the .docx file from disk
Document doc = new Document(@"C:\MyFiles\input.docx");
```

**Waarom dit belangrijk is:** De `Document`‑klasse leest het volledige Word‑pakket in het geheugen, waardoor je toegang krijgt tot pagina's, stijlen en alles daartussen. Als het pad onjuist is, krijg je een `FileNotFoundException`, dus controleer dubbel of het bestand bestaat en of het pad escaped backslashes (`\\`) of een verbatim string (`@`) gebruikt.  

> **Pro tip:** Plaats de laad‑aanroep in een `try/catch`‑blok als je verwacht dat het bestand tijdens runtime kan ontbreken.

---

## Stap 2: Configureer Image Rendering Options (Afbeeldingsbreedte en -hoogte instellen)

Nu komt het hart van de tutorial: **hoe je afbeeldingsbreedte en -hoogte instelt** zodat de resulterende PNG niet uitgerekt of gepixeld is. De `ImageRenderingOptions`‑klasse geeft je fijne controle over afmetingen, DPI en smoothing.

```csharp
// Create rendering options and explicitly set width and height
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Desired output size in pixels
    Width = 1024,          // Set image width height: 1024px wide
    Height = 768,          // Set image width height: 768px tall

    // High‑quality antialiasing works on Windows, Linux, and macOS
    UseAntialiasing = true,

    // Optional: increase DPI for sharper output (default is 96)
    Resolution = 300
};
```

**Uitleg van de belangrijkste eigenschappen:**

- `Width` en `Height` – Dit zijn de exacte pixelafmetingen die je wilt. Door ze in te stellen, **stel je afbeeldingsbreedte en -hoogte** direct in, waardoor de standaard paginagrootte wordt overschreven.  
- `UseAntialiasing` – Schakelt hoogwaardige smoothing in voor tekst en vector‑graphics, wat cruciaal is wanneer je **word naar png converteert** en scherpe randen wilt.  
- `Resolution` – Een hogere DPI levert meer detail, vooral bij complexe lay‑outs. Houd het geheugenverbruik in de gaten; een 300 DPI‑afbeelding kan groot worden.

> **Waarom niet gewoon de standaardgrootte gebruiken?** De standaard gebruikt de fysieke afmetingen van de pagina (bijv. A4 op 96 DPI). Dat levert vaak een afbeelding van 794 × 1123 pixel op—prima voor sommige gevallen, maar niet wanneer je een specifieke UI‑thumbnail of een vaste preview‑grootte nodig hebt.

---

## Stap 3: Renderen en opslaan als PNG (Docx exporteren als afbeelding)

Met het document geladen en de opties geconfigureerd, kun je eindelijk **docx exporteren als afbeelding**. De `RenderToImage`‑methode doet het zware werk.

```csharp
// Render the first page (page index 0) to a PNG file
doc.RenderToImage(@"C:\MyFiles\output.png", imageOptions);
```

Wil je **het hele document** (alle pagina's) renderen naar afzonderlijke PNG‑bestanden, gebruik dan een lus over de paginacollectie:

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string outPath = $@"C:\MyFiles\page_{i + 1}.png";
    doc.RenderToImage(outPath, imageOptions, i);
}
```

**Wat gebeurt er onder de motorkap?** De renderer rastert elke pagina met de door jou opgegeven afmetingen, past antialiasing toe, en schrijft een PNG‑byte‑stream naar schijf. Omdat PNG lossless is, behoud je de volledige getrouwheid van de oorspronkelijke Word‑lay‑out.

**Verwachte output:** Een scherpe PNG‑file exact 1024 × 768 pixel (of welke grootte je ook hebt ingesteld). Open het in een willekeurige afbeeldingsviewer en je ziet de Word‑inhoud precies zoals in het originele document, maar nu als bitmap‑afbeelding.

---

## Geavanceerde tips & variaties

### 1. Transparante achtergronden behouden

Als je Word‑document vormen met transparante achtergronden bevat en je die transparantie wilt behouden, stel dan `BackgroundColor` in op `Color.Transparent`:

```csharp
imageOptions.BackgroundColor = System.Drawing.Color.Transparent;
```

### 2. Alleen een specifiek bereik renderen

Soms heb je alleen een alinea of een tabel nodig, niet de hele pagina. Gebruik `DocumentVisitor` om de node te extraheren en apart te renderen. Dat is een meer geavanceerd scenario, maar het laat zien **hoe je Word‑inhoud rendert** op een granulaire manier.

### 3. DPI dynamisch aanpassen

Als je per pagina een andere DPI nodig hebt (bijv. hoge resolutie voor de omslagpagina), wijzig dan `Resolution` binnen de lus:

```csharp
if (i == 0) imageOptions.Resolution = 600; // cover page
else imageOptions.Resolution = 300;
```

### 4. Batch‑verwerking

Wanneer je tientallen documenten converteert, verpak de hele flow in een methode en hergebruik dezelfde `ImageRenderingOptions`‑instantie. Het hergebruiken van het opties‑object vermindert allocatie‑overhead.

---

## Veelvoorkomende valkuilen & hoe ze te vermijden

| Symptoom | Waarschijnlijke oorzaak | Oplossing |
|----------|--------------------------|-----------|
| PNG is wazig ondanks hoge DPI | `UseAntialiasing` staat op `false` | Zet `UseAntialiasing = true`. |
| Uitvoergrootte komt niet overeen met `Width`/`Height` | DPI niet meegenomen | Vermenigvuldig gewenste grootte met `Resolution / 96` of pas `Resolution` aan. |
| Out‑of‑memory‑exception bij grote documenten | Het hele document renderen op 300 DPI | Render één pagina tegelijk, en dispose elke afbeelding na opslaan. |
| PNG toont een witte achtergrond bij transparante afbeeldingen | `BackgroundColor` niet ingesteld | Zet `imageOptions.BackgroundColor = Color.Transparent`. |

---

## Volledig werkend voorbeeld

Hieronder vind je een zelfstandig programma dat je kunt kopiëren‑plakken in een console‑app. Het demonstreert **word naar png converteren**, **docx als PNG opslaan**, en uiteraard **afbeeldingsbreedte en -hoogte instellen**.

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;
using System.Drawing; // For Color

namespace WordToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            string inputPath = @"C:\MyFiles\input.docx";
            Document doc = new Document(inputPath);

            // 2️⃣ Configure rendering options (set image width height)
            ImageRenderingOptions options = new ImageRenderingOptions
            {
                Width = 1024,          // Desired pixel width
                Height = 768,          // Desired pixel height
                UseAntialiasing = true,
                Resolution = 300,
                BackgroundColor = Color.Transparent // Keep transparency if needed
            };

            // 3️⃣ Render the first page to PNG (export docx as image)
            string outputPath = @"C:\MyFiles\output.png";
            doc.RenderToImage(outputPath, options);

            Console.WriteLine($"✅ Document rendered successfully to {outputPath}");
            // Optional: render all pages
            //RenderAllPages(doc, options);
        }

        // Helper method for batch rendering (uncomment if needed)
        static void RenderAllPages(Document doc, ImageRenderingOptions options)
        {
            for (int i = 0; i < doc.PageCount; i++)
            {
                string pagePath = $@"C:\MyFiles\page_{i + 1}.png";
                doc.RenderToImage(pagePath, options, i);
                Console.WriteLine($"Page {i + 1} saved to {pagePath}");
            }
        }
    }
}
```

**Uitvoeren:** Bouw het project, plaats een geldig `input.docx` op het opgegeven pad, en start het. Je zou een `output.png` moeten zien van exact **1024 × 768** pixel, gerenderd met vloeiende randen.


## Gerelateerde tutorials

- [How to Enable Antialiasing When Converting DOCX to PNG/JPG](/html/english/net/generate-jpg-and-png-images/how-to-enable-antialiasing-when-converting-docx-to-png-jpg/)
- [convert docx to png – create zip archive c# tutorial](/html/english/net/generate-jpg-and-png-images/convert-docx-to-png-create-zip-archive-c-tutorial/)
- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}