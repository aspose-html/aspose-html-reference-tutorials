---
category: general
date: 2026-05-28
description: Leer hoe je een aangepaste resourcehandler in C# maakt om een webpagina
  naar een afbeelding te renderen, een screenshot van de webpagina te maken en HTML
  op te slaan als PNG, met volledige code.
draft: false
keywords:
- custom resource handler
- render webpage to image
- capture webpage screenshot
- render html to png
- save webpage as png
language: nl
og_description: Maak een aangepaste resourcehandler in C# en render een webpagina
  naar een afbeelding. Maak een screenshot, render HTML naar PNG en sla het resultaat
  op met een volledig voorbeeld.
og_title: Aangepaste resourcehandler in C# – Webpagina renderen naar afbeelding
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to create a custom resource handler in C# to render webpage
    to image, capture webpage screenshot and save HTML as PNG with complete code.
  headline: Custom Resource Handler in C# – Render Webpage to Image
  type: TechArticle
- description: Learn how to create a custom resource handler in C# to render webpage
    to image, capture webpage screenshot and save HTML as PNG with complete code.
  name: Custom Resource Handler in C# – Render Webpage to Image
  steps:
  - name: Expected Output
    text: Running the full program should produce a PNG that looks like a faithful
      snapshot of `https://example.com`. Open it in any image viewer, and you’ll see
      the page rendered at the default viewport size (usually 1024 × 768 px). All
      linked images and styles are stored alongside, ready for reuse.
  - name: What if the target page uses relative URLs?
    text: Our handler already strips the leading slash (`info.Path.TrimStart('/')`)
      and combines it with the output folder, so relative paths resolve correctly.
      If you encounter a URL that starts with `//` (protocol‑relative), the renderer
      normalizes it before calling `HandleResource`.
  - name: How do I change the output dimensions?
    text: 'Pass a `Size` object to `RenderPage` overload:'
  - name: Can I render multiple pages in one run?
    text: Absolutely. Just loop over a list of URLs and call `RenderPage` each time.
      The same `MyResourceHandler` instance will keep populating the `output` folder,
      keeping everything tidy.
  - name: What about authentication‑protected sites?
    text: If the page requires cookies or HTTP headers, configure an `HttpClient`
      and assign it to the renderer’s `HttpClient` property (if your library exposes
      it). This keeps the **render html to png** flow seamless for internal dashboards.
  type: HowTo
tags:
- C#
- ImageRenderer
- WebAutomation
title: Aangepaste resourcehandler in C# – Webpagina renderen naar afbeelding
url: /nl/net/generate-jpg-and-png-images/custom-resource-handler-in-c-render-webpage-to-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Custom Resource Handler in C# – Render Webpage to Image

Heb je je ooit afgevraagd hoe je met een **custom resource handler** een perfecte screenshot van elke site kunt maken? Je bent niet de enige. Het programmatically vastleggen van een screenshot van een webpagina kan aanvoelen als het achtervolgen van een bewegend doelwit, vooral wanneer je de afbeeldingen en lettertypen precies wilt opslaan waar je ze nodig hebt.

In deze gids lopen we stap voor stap door het bouwen van een **custom resource handler** in C#, het configureren van renderopties, en uiteindelijk het gebruik van de ImageRenderer om **render webpage to image**. Aan het einde weet je hoe je **capture webpage screenshot**, **render html to png**, en **save webpage as png** kunt uitvoeren zonder je haar uit te trekken.

## Wat je nodig hebt

- .NET 6.0 of later (de API die we gebruiken richt zich op .NET Standard 2.0, dus elke moderne runtime werkt)
- Een NuGet‑pakket dat `ImageRenderer`, `ImageRenderingOptions` en gerelateerde types levert (bijv. *Aspose.HTML* of een vergelijkbare bibliotheek)
- Basiskennis van C#—niets exotisch, alleen een paar `using`‑statements en een `Main`‑methode
- Een output‑map waar de renderer bestanden kan plaatsen (voel je vrij om er handmatig één aan te maken of laat de code het doen)

Dat is alles. Geen extra services, geen headless browsers, alleen pure .NET‑code.

![Custom resource handler saving rendered resources](https://example.com/assets/custom-resource-handler.png "custom resource handler")

## Stap 1: Bouw een **Custom Resource Handler**

Het eerste wat je nodig hebt is een klasse die erft van `ResourceHandler`. Hier gebeurt de magie: elke afbeelding, CSS‑bestand of lettertype die de renderer aanvraagt, wordt via jouw handler geleid, en jij bepaalt waar het wordt weggeschreven.

```csharp
using System.IO;
using Aspose.Html.Rendering.Image;   // Adjust the namespace to your library

// Step 1: Create a custom resource handler to store rendered resources
class MyResourceHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info)
    {
        // Build a safe file path inside the output directory
        string filePath = Path.Combine("output", info.Path.TrimStart('/'));

        // Ensure the directory hierarchy exists
        Directory.CreateDirectory(Path.GetDirectoryName(filePath)!);

        // Return a writable stream that the renderer will fill
        return File.OpenWrite(filePath);
    }
}
```

**Waarom dit belangrijk is:** Zonder een handler kan de renderer bronnen in het geheugen houden of ze volledig weggooien. Door een `Stream` bloot te stellen, krijg je volledige controle over waar elk asset terechtkomt—perfect voor later hergebruik of debugging.

## Stap 2: Configureer Image Rendering Options

Nu we een plek hebben voor de assets, laten we de renderer vertellen hoe we de uiteindelijke afbeelding willen hebben. Antialiasing maakt randen glad, hinting verbetert de teksthelderheid, en het kiezen van een lettertype zorgt ervoor dat de output overeenkomt met je ontwerp.

```csharp
using Aspose.Html.Drawing;          // For ImageRenderingOptions, TextOptions, Font, etc.

// Step 2: Set up image rendering options (antialiasing, text hinting, font)
var imageOptions = new ImageRenderingOptions
{
    UseAntialiasing = true,
    TextOptions = new TextOptions { UseHinting = true },
    Font = new Font("Times New Roman", 14, WebFontStyle.Bold)
};
```

**Waarom deze instellingen?** Antialiasing vermindert gekartelde pixels, vooral bij krommen. Hinting vertelt de rasterizer om glyphs op pixelgrenzen uit te lijnen, wat cruciaal is wanneer je **render html to png** bij typische schermresoluties. Het vette Times New Roman‑lettertype is slechts een voorbeeld; vervang het door elk web‑safe of aangepast lettertype dat je wilt.

## Stap 3: Koppel de Handler aan de Image Renderer

Met de opties en een handler klaar, maken we de `ImageRenderer`. Door onze `MyResourceHandler` toe te wijzen aan de `ResourceHandler`‑eigenschap zorg je ervoor dat elk extern bestand op schijf terechtkomt.

```csharp
using Aspose.Html.Rendering.Image; // For ImageRenderer

// Step 3: Create the image renderer with the options and the custom handler
var renderer = new ImageRenderer(imageOptions)
{
    ResourceHandler = new MyResourceHandler()
};
```

**Pro tip:** Als je ooit elke aanvraag wilt loggen, overschrijf dan `HandleResource` en voeg een `Console.WriteLine(info.Path)` toe voordat je de stream retourneert. Deze kleine toevoeging kan uren besparen bij het oplossen van ontbrekende lettertypen of kapotte afbeeldingen.

## Stap 4: **Render Webpage to Image** en sla het op

Vertel tenslotte de renderer welke URL moet worden vastgelegd en waar de PNG moet worden opgeslagen. De onderstaande aanroep doet al het zware werk: hij haalt de pagina op, verwerkt CSS, laadt lettertypen, en schrijft de resulterende bitmap weg.

```csharp
// Step 4: Render a web page to an image file
renderer.RenderPage("https://example.com", "output/page.png");
```

Wanneer de methode voltooid is, vind je twee dingen in de `output`‑map:

1. `page.png` – de screenshot van de pagina (ons **capture webpage screenshot** resultaat)
2. Een sub‑mapstructuur die de bronnen van de pagina (CSS, afbeeldingen, lettertypen) weerspiegelt – alles opgeslagen dankzij onze **custom resource handler**

### Verwachte output

Het uitvoeren van het volledige programma moet een PNG produceren die eruitziet als een getrouwe weergave van `https://example.com`. Open het in een willekeurige afbeeldingsviewer, en je ziet de pagina gerenderd op de standaard viewport‑grootte (meestal 1024 × 768 px). Alle gekoppelde afbeeldingen en stijlen worden naast elkaar opgeslagen, klaar voor hergebruik.

## Veelgestelde vragen & randgevallen

### Wat als de doelpagina relatieve URL's gebruikt?

Onze handler verwijdert al de voorloop‑slash (`info.Path.TrimStart('/')`) en combineert deze met de output‑map, zodat relatieve paden correct worden opgelost. Als je een URL tegenkomt die begint met `//` (protocol‑relatief), normaliseert de renderer deze voordat `HandleResource` wordt aangeroepen.

### Hoe wijzig ik de output‑afmetingen?

Geef een `Size`‑object door aan de overload van `RenderPage`:

```csharp
renderer.RenderPage("https://example.com", "output/page.png", new Size(1920, 1080));
```

Zo kun je **save webpage as png** in hoge resolutie voor print‑klare assets.

### Kan ik meerdere pagina's in één run renderen?

Absoluut. Loop gewoon over een lijst met URL's en roep elke keer `RenderPage` aan. Dezelfde `MyResourceHandler`‑instantie blijft de `output`‑map vullen, waardoor alles netjes blijft.

### Hoe zit het met authenticatie‑beveiligde sites?

Als de pagina cookies of HTTP‑headers vereist, configureer dan een `HttpClient` en wijs deze toe aan de `HttpClient`‑eigenschap van de renderer (indien je bibliotheek deze exposeert). Dit houdt de **render html to png**‑stroom naadloos voor interne dashboards.

## Volledig werkend voorbeeld

Alles samenvoegend, hier is een minimale console‑app die je kunt kopiëren‑plakken in Visual Studio:

```csharp
using System;
using System.IO;
using Aspose.Html.Drawing;
using Aspose.Html.Rendering.Image;

class MyResourceHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info)
    {
        string filePath = Path.Combine("output", info.Path.TrimStart('/'));
        Directory.CreateDirectory(Path.GetDirectoryName(filePath)!);
        return File.OpenWrite(filePath);
    }
}

class Program
{
    static void Main()
    {
        var imageOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            TextOptions = new TextOptions { UseHinting = true },
            Font = new Font("Times New Roman", 14, WebFontStyle.Bold)
        };

        var renderer = new ImageRenderer(imageOptions)
        {
            ResourceHandler = new MyResourceHandler()
        };

        // Render the page and save as PNG
        renderer.RenderPage("https://example.com", "output/page.png");

        Console.WriteLine("Done! Screenshot saved to output/page.png");
    }
}
```

Compileer en voer uit (`dotnet run`), controleer vervolgens de `output`‑directory. Je hebt zojuist **rendered a webpage to image**, een screenshot vastgelegd, en de HTML opgeslagen als PNG—allemaal dankzij een nette **custom resource handler**.

## Conclusie

We hebben een **custom resource handler** gebouwd, renderopties aangepast, en een `ImageRenderer` gebruikt om **render webpage to image**. Het resultaat is een scherpe PNG plus een volledige set bronnen, waardoor je alles hebt wat je nodig hebt om **capture webpage screenshot**, **render html to png**, en **save webpage as png** te doen voor rapporten, thumbnails, of geautomatiseerd testen.

Wat nu? Probeer te experimenteren met:

- Verschillende viewport‑groottes voor mobiele versus desktop‑screenshots
- Watermerken of overlays toevoegen na het renderen
- Exporteren naar andere formaten (JPEG, BMP) door `ImageRenderingOptions` aan te passen

Voel je vrij om een reactie achter te laten als je tegen een probleem aanloopt of een slimme aanpassing ontdekt. Veel plezier met coderen, en moge je screenshots altijd pixel‑perfect zijn!

## Gerelateerde tutorials

- [Hoe HTML opslaan in C# – Complete gids met een Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [HTML maken vanuit string in C# – Gids voor Custom Resource Handler](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Hoe HTML renderen als PNG – Complete C# gids](/html/english/net/rendering-html-documents/how-to-render-html-as-png-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}