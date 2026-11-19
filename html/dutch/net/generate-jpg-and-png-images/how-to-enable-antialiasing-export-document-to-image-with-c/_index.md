---
category: general
date: 2026-04-06
description: Leer hoe je antialiasing inschakelt, de breedte en hoogte van de afbeelding
  instelt, en het document opslaat als PNG in C# – een snelle gids om een document
  naar een afbeelding te exporteren.
draft: false
keywords:
- how to enable antialiasing
- save document as png
- set image width
- set image height
- export document to image
language: nl
og_description: Hoe antialiasing in te schakelen wanneer je een document exporteert
  naar een afbeelding. Deze gids laat zien hoe je de afbeeldingsbreedte instelt, de
  afbeeldingshoogte instelt en het document opslaat als PNG.
og_title: Hoe antialiasing inschakelen – Document exporteren naar afbeelding
tags:
- C#
- ImageRendering
- Antialiasing
title: Hoe antialiasing inschakelen – Document exporteren naar afbeelding met C#
url: /nl/net/generate-jpg-and-png-images/how-to-enable-antialiasing-export-document-to-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe antialiasing in te schakelen – Document exporteren naar afbeelding in C#

Heb je je ooit afgevraagd **hoe je antialiasing kunt inschakelen** terwijl je een document naar een afbeelding omzet? Misschien heb je een snelle `Save`‑aanroep geprobeerd en zag het resultaat er gekarteld uit, vooral bij diagonale lijnen. Het goede nieuws is dat je geen grafische tovenaar nodig hebt—slechts een paar regels C# en de juiste opties.

In deze tutorial lopen we door het instellen van de afbeeldingsbreedte, het instellen van de afbeeldingshoogte, en uiteindelijk **document opslaan als PNG** zodat je **document kunt exporteren naar afbeelding** met gladde randen. Aan het einde heb je een kant‑klaar fragment dat een scherpe 800 × 600 PNG produceert met ingeschakelde antialiasing.

## Vereisten

- .NET 6.0 of later (de code werkt ook op .NET Framework 4.7+)
- Een verwijzing naar een renderingsbibliotheek die `ImageRenderingOptions` ondersteunt (bijv. Aspose.Words, Syncfusion, of elke API die vergelijkbare eigenschappen blootlegt)
- Een basisbegrip van C#‑syntaxis  

Geen uitgebreide setup—voeg gewoon het NuGet‑pakket toe en je bent klaar om te gaan.

## Stap 1: Installeer de renderingsbibliotheek

Eerst haal je het pakket in je project. Als je Aspose.Words gebruikt, voer je uit:

```bash
dotnet add package Aspose.Words
```

> **Pro tip:** Houd de bibliotheekversie up‑to‑date; de nieuwste release (vanaf april 2026) voegt prestatie‑optimalisaties toe voor antialiasing.

## Stap 2: Maak het Document‑object

Laad of maak het document dat je wilt renderen. Hier is een minimaal voorbeeld dat een één‑pagina document bouwt met een eenvoudige alinea:

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Create a new blank document
Document doc = new Document();

// Add a paragraph with some text
Paragraph para = new Paragraph(doc);
Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
para.AppendChild(run);
doc.FirstSection.Body.AppendChild(para);
```

De `Document`‑klasse is het startpunt; alles wat je rendert komt ervan. In echte projecten laad je waarschijnlijk een bestaande .docx:

```csharp
// Document doc = new Document("input.docx");
```

## Stap 3: Definieer renderopties (Breedte, Hoogte, Antialiasing)

Nu beantwoorden we de kernvraag: **hoe je antialiasing kunt inschakelen**. Het `ImageRenderingOptions`‑object laat je gladstrijken in- of uitschakelen en de afmetingen beheren.

```csharp
// Step 3: Define rendering options (size and antialiasing)
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Set the desired output size
    Width = 800,               // set image width
    Height = 600,              // set image height

    // Turn on antialiasing for smoother edges
    UseAntialiasing = true
};
```

Let op de opmerkingen: ze vermelden expliciet **set image width**, **set image height**, en **UseAntialiasing**—de drie instellingen die het meest van belang zijn wanneer je een gepolijste PNG wilt.

### Waarom antialiasing belangrijk is

Zonder antialiasing verschijnen diagonale lijnen en krommen trap­vormig omdat de renderer elke pixel als aan of uit beschouwt. Door het in te schakelen worden randpixels gemengd, wat een visuele verzachting oplevert die lijkt op wat je in een foto‑editor zou zien. Het nadeel is een kleine toename in verwerkingstijd, maar voor de meeste UI‑gerichte exports is dit verwaarloosbaar.

## Stap 4: Document opslaan als PNG (Document exporteren naar afbeelding)

Met de opties klaar, slaan we eindelijk **document op als PNG**. De `Save`‑methode neemt het bestandspad en de opties die we zojuist hebben geconfigureerd.

```csharp
// Step 4: Render the document to a PNG file using the configured options
doc.Save("output.png", imageOptions);
```

Dat is alles—je document is nu een 800 × 600 PNG met toegepaste antialiasing. Als je `output.png` opent, zie je schone tekst, gladde lijnen en geen gekartelde artefacten.

### Het resultaat verifiëren

Je kunt het bestand snel controleren in elke afbeeldingsviewer. Let op:

- Juiste afmetingen (800 × 600)  
- Geen zichtbare trap­vormige randen op de tekst of vormen  
- Een transparante achtergrond als je document geen achtergrondkleur bevatte (de meeste bibliotheken gebruiken standaard wit)

Als de afbeelding er gekarteld uitziet, controleer dan dubbel of `UseAntialiasing = true` niet ergens anders wordt overschreven.

## Stap 5: Randgevallen & Variaties

### Het uitvoerformaat wijzigen

Wil je een JPEG in plaats van PNG? Verander gewoon de bestandsextensie en pas eventueel de compressie aan:

```csharp
imageOptions.JpegQuality = 90; // only works for JPEG output
doc.Save("output.jpg", imageOptions);
```

### Meerdere pagina’s exporteren

Wanneer het bron‑document meerdere pagina’s heeft, maakt de renderer standaard afzonderlijke afbeeldingsbestanden per pagina. Je kunt door de pagina’s itereren:

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string fileName = $"page_{i + 1}.png";
    doc.Save(fileName, imageOptions);
}
```

### Opslaan naar een stream (bijv. HTTP‑respons)

Als je een web‑API bouwt, wil je de PNG misschien direct teruggeven:

```csharp
using (MemoryStream ms = new MemoryStream())
{
    doc.Save(ms, imageOptions);
    ms.Position = 0;
    // Return ms as FileResult in ASP.NET Core
}
```

## Volledig werkend voorbeeld

Hieronder staat het volledige, kant‑klaar programma dat elke besproken stap bevat:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;

class Program
{
    static void Main()
    {
        // 1️⃣ Create or load a document
        Document doc = new Document();
        Paragraph para = new Paragraph(doc);
        Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
        para.AppendChild(run);
        doc.FirstSection.Body.AppendChild(para);

        // 2️⃣ Define rendering options (size and antialiasing)
        ImageRenderingOptions imageOptions = new ImageRenderingOptions
        {
            Width = 800,               // set image width
            Height = 600,              // set image height
            UseAntialiasing = true     // how to enable antialiasing
        };

        // 3️⃣ Export document to image (save document as PNG)
        doc.Save("output.png", imageOptions);

        Console.WriteLine("Image saved as output.png with antialiasing enabled.");
    }
}
```

Het uitvoeren van dit programma genereert `output.png` in de map van het uitvoerbare bestand. Open het, en je ziet een gladde 800 × 600 PNG—precies wat we wilden bereiken.

## Veelgestelde vragen & probleemoplossing

- **Wat als de afbeelding er wazig uitziet?**  
  Vervaging kan optreden wanneer je een kleine bronpagina opschaalt. Houd de bronpaginasize dicht bij de doelafmetingen, of verhoog de DPI via `imageOptions.Resolution` (bijv. `Resolution = 300`).

- **Werkt dit op .NET Framework?**  
  Ja. dezelfde API bestaat in het klassieke framework; verwijs gewoon naar de juiste DLL.

- **Kan ik de achtergrondkleur regelen?**  
  Zeker. Stel `imageOptions.BackgroundColor = System.Drawing.Color.Transparent;` in vóór het opslaan.

- **Is antialiasing hardware‑versneld?**  
  De meeste bibliotheken voeren software‑antialiasing uit. Als je GPU‑versnelling nodig hebt, zoek dan een renderengine die dit expliciet ondersteunt.

## Conclusie

We hebben **hoe je antialiasing kunt inschakelen** wanneer je **document exporteert naar afbeelding** behandeld, doorlopen **set image width** en **set image height**, en hebben je de exacte stappen getoond om **document op te slaan als PNG**. Het fragment hierboven is klaar voor productie, en je kunt het nu aanpassen naar JPEG, multi‑page PDF’s, of zelfs de afbeelding direct naar een client streamen.

Vervolgens kun je watermerken toevoegen, DPI aanpassen voor afdruk‑kwaliteit, of deze logica integreren in een ASP.NET Core‑endpoint. Dezelfde principes gelden—vervang gewoon het bestandspad door een responsestream.

Veel plezier met coderen, en geniet van die scherpe, antialias‑afbeeldingen! 

![Gerenderde PNG met antialiasing ingeschakeld](output.png "Gerenderde PNG met antialiasing ingeschakeld")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}