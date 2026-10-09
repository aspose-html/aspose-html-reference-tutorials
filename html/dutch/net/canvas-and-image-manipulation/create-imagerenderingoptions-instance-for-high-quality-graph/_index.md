---
category: general
date: 2026-10-09
description: Maak een imagerenderingoptions‑instantie aan om antialiasing in te schakelen
  en de kwaliteit van grafische weergave te verbeteren in .NET‑toepassingen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create imagerenderingoptions instance
- ImageRenderingOptions
- antialiasing
- SmoothingMode
- graphics rendering
language: nl
lastmod: 2026-10-09
og_description: Maak een ImageRenderingOptions‑instance aan om antialiasing in te
  schakelen en een soepelere grafische weergave in .NET te bereiken. Volg de stapsgewijze
  handleiding.
og_image_alt: Screenshot showing smooth edges after enabling antialiasing with ImageRenderingOptions
og_title: Maak een ImageRenderingOptions‑instantie – verbeter de grafische kwaliteit
  in .NET
schemas:
- author: Aspose
  dateModified: '2026-10-09'
  description: Create imagerenderingoptions instance to enable antialiasing and improve
    graphics rendering quality in .NET applications.
  headline: Create imagerenderingoptions instance for high‑quality graphics rendering
  type: TechArticle
- description: Create imagerenderingoptions instance to enable antialiasing and improve
    graphics rendering quality in .NET applications.
  name: Create imagerenderingoptions instance for high‑quality graphics rendering
  steps:
  - name: '**Forgetting to pass the options** – Rendering methods that accept `ImageRenderingOptions`
      will ignore antialiasing if you call the overload without the options parameter.
      Always use the three‑parameter `GetThumbnail` or equivalent method.'
    text: '**Forgetting to pass the options** – Rendering methods that accept `ImageRenderingOptions`
      will ignore antialiasing if you call the overload without the options parameter.
      Always use the three‑parameter `GetThumbnail` or equivalent method.'
  - name: '**Mixing SmoothingMode with ImageRenderingOptions** – Setting `Graphics.SmoothingMode`
      has no effect on Aspose.Slides rendering. Rely solely on `UseAntialiasing`.'
    text: '**Mixing SmoothingMode with ImageRenderingOptions** – Setting `Graphics.SmoothingMode`
      has no effect on Aspose.Slides rendering. Rely solely on `UseAntialiasing`.'
  - name: '**Using an outdated library version** – `ImageRenderingOptions` was introduced
      in Aspose.Slides 20.5. Ensure your NuGet package is up‑to‑date; otherwise the
      class may be missing or lack the `UseAntialiasing` property.'
    text: '**Using an outdated library version** – `ImageRenderingOptions` was introduced
      in Aspose.Slides 20.5. Ensure your NuGet package is up‑to‑date; otherwise the
      class may be missing or lack the `UseAntialiasing` property.'
  type: HowTo
tags:
- .NET
- C#
- rendering
title: Maak een ImagerenderingOptions‑instantie aan voor hoogwaardige grafische weergave
url: /nl/net/canvas-and-image-manipulation/create-imagerenderingoptions-instance-for-high-quality-graph/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak een imagerenderingoptions‑instantie voor grafische weergave van hoge kwaliteit

Als je **een imagerenderingoptions‑instantie moet maken** om vloeiendere graphics te produceren, laat deze gids je precies zien hoe. Door antialiasing te configureren elimineer je gekartelde randen en verkrijg je output van professionele kwaliteit zonder extra bibliotheken.

Je leert hoe je `ImageRenderingOptions` instantiateert, antialiasing inschakelt en de opties koppelt aan een renderengine zoals Aspose.Slides of System.Drawing. De tutorial gaat ervan uit dat je bekend bent met basis‑C#‑syntaxis en een .NET‑ontwikkelomgeving klaar hebt staan.

## Vereisten

- .NET 6.0 of later (de API is beschikbaar in .NET Standard 2.0+)
- Een referentie naar de assembly die `ImageRenderingOptions` bevat (bijv. `Aspose.Slides.NET`)
- Een IDE zoals Visual Studio 2022 of VS Code met de C#‑extensie
- Basiskennis van graphics‑rendering‑pijplijnen

## Stap 1: Maak imagerenderingoptions‑instantie

De eerste handeling is het aanmaken van een nieuw `ImageRenderingOptions`‑object. Dit object fungeert als container voor alle render‑gerelateerde vlaggen.

```csharp
using Aspose.Slides;          // Replace with the appropriate namespace
using Aspose.Slides.Export;   // Needed for ImageRenderingOptions

// Step 1: Create the ImageRenderingOptions instance
ImageRenderingOptions imgOptions = new ImageRenderingOptions();
```

Het maken van de instantie geeft je volledige controle over hoe vector‑graphics gerasterd worden. Later kun je specifieke functies zoals antialiasing, tekst‑renderingsmodus of beeldcompressie in- of uitschakelen.

## Stap 2: Schakel antialiasing in om de graphics‑rendering te verbeteren

Antialiasing maakt de overgang tussen pixelkleuren vloeiender, waardoor het traptrede‑effect op diagonale of gebogen lijnen wordt verminderd. De oudere eigenschap `SmoothingMode` is verouderd; `UseAntialiasing` is de moderne, aanbevolen aanpak.

```csharp
// Step 2: Turn on antialiasing for smoother output
imgOptions.UseAntialiasing = true;
```

`UseAntialiasing` op `true` zetten vertelt de renderengine om tijdens het rasteren een filter van hoge kwaliteit toe te passen. Deze vlag werkt zowel voor vectorvormen als tekst, waardoor consistente visuele getrouwheid over de dia heen wordt gegarandeerd.

### Waarom niet `SmoothingMode` gebruiken?

`SmoothingMode` behoort tot `System.Drawing.Graphics` en beïnvloedt alleen GDI+‑tekeningen. Wanneer je dia’s of PDF’s rendert via Aspose.Slides, is `ImageRenderingOptions.UseAntialiasing` de enige vlag die de bibliotheek respecteert. Het gebruik van de nieuwere eigenschap garandeert toekomstbestendigheid en elimineert onverwacht gedrag op niet‑Windows‑platformen.

## Stap 3: Pas de opties toe op een render‑operatie

Zodra de `ImageRenderingOptions`‑instantie is geconfigureerd, geef je deze door aan de methode die de feitelijke rendering uitvoert. Hieronder staat een volledig, uitvoerbaar voorbeeld dat een presentatie laadt, de eerste dia als PNG rendert en de afbeelding opslaat met ingeschakelde antialiasing.

```csharp
using System;
using Aspose.Slides;
using Aspose.Slides.Export;

class Program
{
    static void Main()
    {
        // Load a sample presentation
        using Presentation pres = new Presentation("sample.pptx");

        // Create and configure ImageRenderingOptions
        ImageRenderingOptions imgOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true   // Enable antialiasing
        };

        // Render the first slide to a PNG file
        Slide slide = pres.Slides[0];
        slide.GetThumbnail(2f, 2f, imgOptions)   // 2x scale for higher resolution
            .Save("slide1_antialiased.png", Export.SaveFormat.Png);

        Console.WriteLine("Slide rendered with antialiasing.");
    }
}
```

**Uitleg van belangrijke regels**

- `new Presentation("sample.pptx")` laadt het bronbestand.  
- `GetThumbnail(2f, 2f, imgOptions)` maakt een bitmap van de dia met het dubbele van de standaard DPI, terwijl de door jou geconfigureerde renderopties worden toegepast.  
- De resulterende PNG (`slide1_antialiased.png`) toont gladde curven en tekst dankzij `UseAntialiasing = true`.

### Verwachte output

Open `slide1_antialiased.png` in een willekeurige afbeeldingsviewer. Vergeleken met een rendering zonder antialiasing zul je merken dat:

- Afgeronde hoeken van vormen verschijnen zonder gekartelde stappen.  
- Tekstranden zijn scherp maar verzacht, waardoor gepixelde artefacten verdwijnen.  
- De algehele visuele kwaliteit overeenkomt met wat je in de originele PowerPoint‑weergave ziet.

## Stap 4: Optionele aanpassingen voor geavanceerde graphics‑rendering

Hoewel antialiasing de meest voorkomende vlag is, biedt `ImageRenderingOptions` extra controle:

| Eigenschap | Doel | Typische waarde |
|------------|------|-----------------|
| `UseHighQualityRendering` | Schakelt sub‑pixel rendering voor tekst in | `true` |
| `PixelFormat` | Bepaalt de kleurdiepte van de uitvoer‑bitmap | `PixelFormat.Format32bppArgb` |
| `ImageFormat` | Stelt het doel‑afbeeldingsformaat in (PNG, JPEG, enz.) | `Export.SaveFormat.Png` |

Je kunt deze instellingen combineren:

```csharp
imgOptions.UseHighQualityRendering = true;
imgOptions.PixelFormat = System.Drawing.Imaging.PixelFormat.Format32bppArgb;
```

**Pro‑tip:** Bij het genereren van grootschalige PDF’s of high‑resolution PNG’s, houd `UseAntialiasing` aan maar houd het geheugengebruik in de gaten. Antialiasing voegt extra verwerkings‑overhead toe, wat merkbaar kan zijn op low‑end machines.

## Veelvoorkomende valkuilen en hoe ze te vermijden

1. **Vergeten de opties door te geven** – Render‑methoden die `ImageRenderingOptions` accepteren negeren antialiasing als je de overload zonder de opties‑parameter aanroept. Gebruik altijd de drie‑parameter `GetThumbnail` of een equivalente methode.  
2. **`SmoothingMode` combineren met `ImageRenderingOptions`** – Het instellen van `Graphics.SmoothingMode` heeft geen effect op Aspose.Slides‑rendering. Vertrouw uitsluitend op `UseAntialiasing`.  
3. **Een verouderde bibliotheekversie gebruiken** – `ImageRenderingOptions` werd geïntroduceerd in Aspose.Slides 20.5. Zorg dat je NuGet‑pakket up‑to‑date is; anders kan de klasse ontbreken of de eigenschap `UseAntialiasing` missen.

## Conclusie

Je weet nu hoe je **een imagerenderingoptions‑instantie maakt**, antialiasing inschakelt en de opties integreert in een render‑workflow. Deze aanpak garandeert vloeiendere graphics‑rendering, vervangt de legacy‑instelling `SmoothingMode` en werkt consistent over .NET‑platformen.

Vanaf hier kun je extra render‑vlaggen verkennen, experimenteren met verschillende DPI‑schalen, of de techniek combineren met PDF‑export voor assets van afdruk‑kwaliteit. Het beheersen van `ImageRenderingOptions` is een hoeksteen van .NET‑graphics‑programmering met hoge getrouwheid.

---


## Wat moet je hierna leren?


De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Create PNG from HTML – Full C# Rendering Guide](/html/english/net/rendering-html-documents/create-png-from-html-full-c-rendering-guide/)
- [Create image from HTML in C# – Complete Step‑by‑Step Guide](/html/english/net/rendering-html-documents/create-image-from-html-in-c-complete-step-by-step-guide/)
- [Create canvas text – Full Guide to Rendering Text on Images](/html/english/net/canvas-and-image-manipulation/create-canvas-text-full-guide-to-rendering-text-on-images/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}