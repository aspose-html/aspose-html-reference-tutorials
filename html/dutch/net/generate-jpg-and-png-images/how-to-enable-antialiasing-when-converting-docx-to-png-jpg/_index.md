---
category: general
date: 2025-12-27
description: Leer hoe je antialiasing kunt inschakelen bij het converteren van DOCX
  naar PNG of JPG. Deze stapsgewijze handleiding behandelt ook het converteren van
  docx naar png en het converteren van docx naar jpg.
draft: false
keywords:
- how to enable antialiasing
- convert docx to png
- convert docx to jpg
- how to convert docx
- how to render docx
language: nl
og_description: Hoe antialiasing in te schakelen bij het converteren van DOCX‑bestanden
  naar PNG of JPG. Volg deze volledige gids voor een soepele, hoogwaardige output.
og_title: Hoe antialiasing in te schakelen bij het converteren van DOCX naar PNG/JPG
tags:
- C#
- Document Rendering
- Image Processing
title: Hoe antialiasing in te schakelen bij het converteren van DOCX naar PNG/JPG
url: /nl/net/generate-jpg-and-png-images/how-to-enable-antialiasing-when-converting-docx-to-png-jpg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe antialiasing in te schakelen bij het converteren van DOCX naar PNG/JPG

Heb je je ooit afgevraagd **hoe antialiasing in te schakelen** zodat je geconverteerde DOCX‑afbeeldingen er scherp uitzien in plaats van gekarteld? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze een Word‑document moeten omzetten naar een PNG of JPG en eindigen met vage randen op lijnen en tekst. Het goede nieuws? Met een paar regels C# kun je die ruwe output omzetten in pixel‑perfecte graphics—zonder dat je een externe beeldeditor nodig hebt.

In deze tutorial lopen we het volledige proces door van **convert docx to png** en **convert docx to jpg** met behulp van een moderne renderbibliotheek. Je leert niet alleen *hoe je docx converteert* maar ook *hoe je docx rendert* met antialiasing en hinting ingeschakeld, zodat elke curve en elk teken er glad uitziet. Er is geen eerdere ervaring met grafische programmeren nodig; alleen een basis C#‑omgeving en een DOCX‑bestand dat je wilt omzetten naar een afbeelding.

---

## Wat je nodig hebt

- **.NET 6+** (of .NET Framework 4.6+ als je de klassieke runtime verkiest)  
- Een **DOCX**‑bestand dat je wilt renderen (plaats het in een map genaamd `input` voor de demo)  
- Het **Aspose.Words for .NET** NuGet‑pakket (of een willekeurige bibliotheek die `Document`, `ImageRenderingOptions` en `ImageDevice` exposeert). Installeer het met:

```bash
dotnet add package Aspose.Words
```

Dat is alles—geen extra beeldverwerkingstools nodig.

## Stap 1: Laad het DOCX Document (how to convert docx)

Eerst hebben we een `Document`‑object nodig dat het bronbestand vertegenwoordigt. Beschouw het als de digitale versie van je Word‑bestand die de bibliotheek kan lezen en manipuleren.

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;
using Aspose.Words.Saving;

// Load the DOCX you want to render
Document sourceDoc = new Document("input/input.docx");
```

> **Waarom dit belangrijk is:** Het laden van het document is de basis voor *how to render docx*. Als het bestand niet gelezen kan worden, zullen geen van de latere stappen werken, dus beginnen we hier.

## Stap 2: Configureer Image Rendering Options (enable antialiasing)

Nu komt het magische deel—het inschakelen van antialiasing en hinting. Antialiasing maakt de gekartelde randen die je normaal op diagonale lijnen ziet glad, terwijl hinting de helderheid van kleine tekst verbetert.

```csharp
// Set up rendering options with antialiasing and hinting
ImageRenderingOptions renderingOptions = new ImageRenderingOptions
{
    UseAntialiasing = true,                // <‑‑ smooth graphics
    Text = { UseHinting = true }           // <‑‑ sharper text
};
```

> **Pro tip:** Als je ooit een prestatie‑boost nodig hebt bij enorme documenten, kun je `UseAntialiasing` uitschakelen, maar de visuele kwaliteit zal merkbaar dalen.

## Stap 3: Kies het uitvoerformaat – PNG of JPG (convert docx to png / convert docx to jpg)

De `ImageDevice`‑klasse bepaalt waar de gerenderde pagina’s naartoe gaan. Door de `ImageSaveOptions` te wisselen kun je ofwel PNG (verliesvrij) of JPG (gecomprimeerd) outputten. Hieronder maken we twee aparte devices zodat je beide formaten in één run kunt genereren.

```csharp
// PNG device – lossless, ideal for screenshots or further editing
ImageDevice pngDevice = new ImageDevice(renderingOptions)
{
    SaveOptions = new ImageSaveOptions(SaveFormat.Png)
    {
        OutputFileName = "output/page_{0}.png"   // {0} will be replaced by page number
    }
};

// JPG device – smaller file size, good for web thumbnails
ImageDevice jpgDevice = new ImageDevice(renderingOptions)
{
    SaveOptions = new ImageSaveOptions(SaveFormat.Jpeg)
    {
        OutputFileName = "output/page_{0}.jpg",
        JpegQuality = 90          // 0‑100, higher = better quality
    }
};
```

> **Waarom beide?** PNG behoudt elk pixel, wat perfect is wanneer je exacte getrouwheid nodig hebt (bijv. afdrukken). JPG daarentegen comprimeert de afbeelding, waardoor deze sneller laadt op een website.

## Stap 4: Render de documentpagina’s naar afbeeldingen (how to render docx)

Met de devices klaar, laten we de `Document` elke pagina renderen. De bibliotheek zal automatisch door alle pagina’s lopen en ze opslaan volgens het naamgevingspatroon dat we hebben gedefinieerd.

```csharp
// Render to PNG
sourceDoc.RenderTo(pngDevice);

// Render to JPG
sourceDoc.RenderTo(jpgDevice);
```

Na het uitvoeren van de code vind je een reeks bestanden zoals `page_0.png`, `page_1.png`, … en `page_0.jpg`, `page_1.jpg` in de `output`‑map. Elke afbeelding heeft antialiasing toegepast, zodat lijnen glad zijn en tekst kristalhelder.

## Stap 5: Verifieer het resultaat (expected output)

Open een van de gegenereerde afbeeldingen. Je zou moeten zien:

- **Gladde krommen** op vormen en diagrammen (geen traptrede‑artefacten).  
- **Scherpe, leesbare tekst** zelfs bij kleine lettergroottes, dankzij hinting.  
- **Consistente kleuren** tussen PNG en JPG (hoewel JPG lichte compressie‑artefacten kan vertonen als je de kwaliteit verlaagt).

Als je enige onscherpte opmerkt, controleer dan dubbel of `UseAntialiasing` is ingesteld op `true` en dat je bron‑DOCX geen lage‑resolutie raster‑afbeeldingen bevat.

## Veelgestelde vragen & randgevallen

### Wat als ik slechts één pagina nodig heb?

Je kunt een specifieke pagina renderen door de `PageInfo`‑overload te gebruiken:

```csharp
// Render only the first page to PNG
sourceDoc.RenderTo(pngDevice, new PageInfo(0));
```

### Kan ik de DPI (dots per inch) aanpassen voor een hogere resolutie output?

Absoluut. Pas de `Resolution`‑eigenschap aan op `ImageRenderingOptions`:

```csharp
renderingOptions.Resolution = 300; // 300 DPI for print‑quality images
```

Een hogere DPI betekent grotere bestanden, maar het antialiasing‑effect wordt nog duidelijker.

### Hoe ga ik om met grote DOCX‑bestanden zonder geheugenproblemen?

Render pagina’s één‑voor‑één en maak het device na elke iteratie vrij:

```csharp
for (int i = 0; i < sourceDoc.PageCount; i++)
{
    using var singlePageDevice = new ImageDevice(renderingOptions);
    singlePageDevice.SaveOptions = new ImageSaveOptions(SaveFormat.Png)
    {
        OutputFileName = $"output/page_{i}.png"
    };
    sourceDoc.RenderTo(singlePageDevice, new PageInfo(i));
}
```

### Is het mogelijk om te converteren naar andere formaten zoals BMP of TIFF?

Ja—vervang gewoon `SaveFormat.Png` of `SaveFormat.Jpeg` door `SaveFormat.Bmp` of `SaveFormat.Tiff`. Dezelfde antialiasing‑instellingen blijven van toepassing.

## Volledig werkend voorbeeld (Klaar om te kopiëren‑plakken)

Hieronder staat het volledige programma dat je in een nieuw console‑project kunt plaatsen. Het bevat alle using‑statements, foutafhandeling en commentaren voor duidelijkheid.

```csharp
// File: Program.cs
using System;
using System.IO;
using Aspose.Words;
using Aspose.Words.Rendering;
using Aspose.Words.Saving;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the DOCX document (how to convert docx)
        // -------------------------------------------------
        string inputPath = Path.Combine("input", "input.docx");
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❗ Input file not found: {inputPath}");
            return;
        }

        Document sourceDoc = new Document(inputPath);

        // -------------------------------------------------
        // 2️⃣ Configure rendering options (enable antialiasing)
        // -------------------------------------------------
        ImageRenderingOptions renderingOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            Text = { UseHinting = true },
            Resolution = 150 // optional – 150 DPI is a good balance
        };

        // -------------------------------------------------
        // 3️⃣ Set up PNG and JPG devices (convert docx to png / convert docx to jpg)
        // -------------------------------------------------
        string outputFolder = "output";
        Directory.CreateDirectory(outputFolder);

        // PNG (lossless)
        ImageDevice pngDevice = new ImageDevice(renderingOptions)
        {
            SaveOptions = new ImageSaveOptions(SaveFormat.Png)
            {
                OutputFileName = Path.Combine(outputFolder, "page_{0}.png")
            }
        };

        // JPG (compressed)
        ImageDevice jpgDevice = new ImageDevice(renderingOptions)
        {
            SaveOptions = new ImageSaveOptions(SaveFormat.Jpeg)
            {
                OutputFileName = Path.Combine(outputFolder, "page_{0}.jpg"),
                JpegQuality = 90
            }
        };

        // -------------------------------------------------
        // 4️⃣ Render all pages (how to render docx)
        // -------------------------------------------------
        try
        {
            sourceDoc.RenderTo(pngDevice);
            sourceDoc.RenderTo(jpgDevice);
            Console.WriteLine($"✅ Rendering complete! Check the '{outputFolder}' folder.");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ An error occurred: {ex.Message}");
        }
    }
}
```

> **Resultaat:** Na het compileren (`dotnet run`) zie je een reeks PNG‑ en JPG‑bestanden in de `output`‑directory, elk met antialiasing toegepast.

## Conclusie

We hebben behandeld **hoe antialiasing in te schakelen** wanneer je **DOCX naar PNG of JPG converteert**, we hebben de exacte stappen doorlopen om **convert docx to png**, **convert docx to jpg** te doen, en zelfs aangeraakt **how to render docx** voor aangepaste

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}