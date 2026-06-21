---
category: general
date: 2026-03-31
description: Maak een geheugenstroom in C# en leer HTML naar PNG te renderen, gebruik
  een aangepaste resourcehandler, sla HTML op in een ZIP, en stel de lettertype‑stijl
  programmeermatig in — allemaal in één tutorial.
draft: false
keywords:
- create memory stream
- render html to png
- custom resource handler
- save html to zip
- set font style programmatically
language: nl
og_description: Maak een geheugenstroom in C# en render direct HTML naar PNG, gebruik
  aangepaste resourcehandlers, sla HTML op in een ZIP en stel de lettertype‑stijl
  via code in.
og_title: Maak een Memory Stream in C# – Complete programmeergids
tags:
- C#
- HTML rendering
- Streams
- ZIP archives
- Image processing
title: Maak een Memory Stream in C# – Volledige gids met HTML-rendering en ZIP-export
url: /nl/net/rendering-html-documents/create-memory-stream-in-c-full-guide-with-html-rendering-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak een Memory Stream in C# – Volledige Gids met HTML Rendering & ZIP Export

Heb je je ooit afgevraagd hoe je **een memory stream** in C# maakt en vervolgens een HTML‑document omzet in een PNG‑afbeelding, een ZIP‑bestand, of zelfs de lettertype‑stijl onderweg aanpast? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze een in‑memory representatie van een document nodig hebben, maar geen bestandssysteem willen aanraken.  

In deze tutorial lopen we een complete, end‑to‑end oplossing stap voor stap door: we bouwen een aangepaste resource‑handler, pompen HTML naar een `MemoryStream`, zippen hetzelfde document, en renderen het uiteindelijk naar een afbeelding met antialiasing. Aan het einde kun je **HTML naar PNG renderen**, **HTML naar ZIP opslaan**, en **lettertype‑stijl programmatisch instellen** zonder ooit tijdelijke bestanden naar schijf te schrijven.

## Voorwaarden

- .NET 6.0 of later (de API‑surface is stabiel over recente versies).  
- Een referentie naar een HTML‑naar‑afbeelding bibliotheek die `HTMLDocument`, `ImageRenderer` en gerelateerde types biedt – bijvoorbeeld **HtmlRenderer.Core** (vervang door het daadwerkelijke pakket dat je gebruikt).  
- Basiskennis van streams, `using`‑statements en C# object‑georiënteerde patronen.

> **Pro tip:** Als je Visual Studio gebruikt, schakel **nullable reference types** (`<Nullable>enable</Nullable>`) in om subtiele bugs vroegtijdig te detecteren.

## Stap 1: Maak een Memory Stream met een Aangepaste Resource Handler

Het eerste wat we nodig hebben is een handler die de HTML‑engine vertelt *waar* elke resource (afbeeldingen, CSS, enz.) moet worden weggeschreven. Door te erven van `ResourceHandler` kunnen we elke output naar één enkele `MemoryStream` leiden.

```csharp
using System;
using System.IO;

// Step 1: Define a handler that writes resources to an in‑memory stream
class MemoryResourceHandler : ResourceHandler
{
    // The stream lives for the whole lifetime of the handler
    public MemoryStream OutputStream = new MemoryStream();

    // The engine calls this for every resource it needs to write
    public override Stream HandleResource(ResourceInfo info) => OutputStream;
}
```

**Waarom dit belangrijk is:**  
Een `MemoryStream` leeft volledig in RAM, wat betekent dat er geen schijf‑I/O plaatsvindt – perfect voor high‑performance scenario’s zoals webservices of unit‑tests. De handler houdt de API ook tevreden omdat de engine een `Stream` verwacht voor elke resource.

## Stap 2: Laad het HTML‑Document en Sla het op in de Memory Stream

Nu laden we een bestaand HTML‑bestand (of een string) en vertellen we het om onze `MemoryResourceHandler` te gebruiken. Na de `Save`‑aanroep bevat `OutputStream` de volledige HTML‑payload.

```csharp
using System.IO;

// Assume the HTML file lives under YOUR_DIRECTORY
HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");

// Instantiate the memory handler
MemoryResourceHandler memoryHandler = new MemoryResourceHandler();

// Save the document – all resources flow into the same MemoryStream
htmlDoc.Save(memoryHandler);
```

Op dit moment staat de positie van de stream aan het einde, dus moeten we terugspoelen voordat we de inhoud kunnen lezen.

```csharp
// Reset the stream position to the beginning
memoryHandler.OutputStream.Position = 0;

// Quick verification (optional)
// string htmlContent = new StreamReader(memoryHandler.OutputStream).ReadToEnd();
// Console.WriteLine(htmlContent);
```

> **Opmerking:** De bovenstaande `ReadToEnd`‑regel is uitgecommentarieerd omdat je in een productie‑scenario de stream waarschijnlijk aan een andere component zou doorgeven in plaats van deze af te drukken.

## Stap 3: Zip dezelfde HTML met een Aangepaste ZIP Resource Handler

Soms moet je de HTML samen met de bijbehorende assets leveren. Een tweede aangepaste handler kan tijdens het uitvoeren een ZIP‑entry voor elke resource aanmaken.

```csharp
using System.IO.Compression;

// Step 4: Define a handler that writes each resource into a ZIP archive
class ZipResourceHandler : ResourceHandler, IDisposable
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(string zipPath)
    {
        // Open (or create) the archive in write mode
        _zipArchive = ZipFile.Open(zipPath, ZipArchiveMode.Create);
    }

    // The engine calls this for each resource; we create a ZIP entry with the same name
    public override Stream HandleResource(ResourceInfo info) =>
        _zipArchive.CreateEntry(info.Name).Open();

    // Proper disposal of the underlying ZipArchive
    protected override void Dispose(bool disposing)
    {
        if (disposing) _zipArchive.Dispose();
        base.Dispose(disposing);
    }

    public void Dispose() => Dispose(true);
}
```

Nu hergebruiken we dezelfde `htmlDoc`‑instantie en schrijven we deze naar een ZIP‑bestand.

```csharp
// Step 5: Save the HTML document into a ZIP file
using (var zipHandler = new ZipResourceHandler("YOUR_DIRECTORY/output.zip"))
{
    htmlDoc.Save(zipHandler);
}
```

**Tip voor randgevallen:** Als de HTML dezelfde afbeelding meerdere keren referereert, zal de ZIP‑handler dubbele entries aanmaken. Om dat te voorkomen kun je een `HashSet<string>` bijhouden met al toegevoegde namen en de bestaande entry‑stream teruggeven.

## Stap 4: Programmeer­matig Lettertype‑Stijl Instellen op het Standaard Stylesheet

De look van het document aanpassen zonder de bron‑HTML te wijzigen is vaak handig – bijvoorbeeld bij het genereren van een PDF‑preview met een vetkop. De bibliotheek biedt een `DefaultViewStyleSheet` die je kunt aanpassen.

```csharp
// Step 6: Apply bold and italic styling to the default view stylesheet
htmlDoc.DefaultViewStyleSheet.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

Je kunt elke vlag combineren die in `WebFontStyle` is gedefinieerd. De wijziging is direct en beïnvloedt volgende renders of opslagen.

## Stap 5: Render het HTML‑Document naar een PNG‑Afbeelding

Tot slot zetten we de HTML om in een raster‑afbeelding. Door antialiasing en hinting in te schakelen krijgen we scherpe tekst en vloeiende randen.

```csharp
using System.Drawing; // For ImageRenderingOptions if needed

// Step 7: Render the document to an image with antialiasing and hinting
var renderingOptions = new ImageRenderingOptions
{
    UseAntialiasing = true,
    UseHinting = true
};

new ImageRenderer(renderingOptions).Render(htmlDoc, "YOUR_DIRECTORY/out.png");
```

**Wat je zult zien:** Een PNG‑bestand met de naam `out.png` onder `YOUR_DIRECTORY` dat er precies uitziet zoals een browser de HTML zou renderen, maar met de vet‑cursieve stijl die we eerder hebben ingesteld.

![Screenshot of create memory stream output](placeholder-image.png "create memory stream example")

*Image alt text includes the primary keyword to satisfy SEO.*

## Veelgestelde Vragen & Valkuilen

| Vraag | Antwoord |
|----------|--------|
| **Kan ik dezelfde `HTMLDocument` opnieuw gebruiken na het opslaan naar een ZIP?** | Ja. Het documentobject blijft in het geheugen; je kunt `Save` meerdere keren aanroepen met verschillende handlers. |
| **Wat als de HTML grote binaire assets bevat?** | De `MemoryStream` groeit dan mee. Voor zeer grote bestanden kun je overwegen direct naar een bestand te streamen of een `BufferedStream` te gebruiken. |
| **Moet ik `Dispose` aanroepen op `MemoryResourceHandler`?** | Niet strikt noodzakelijk omdat het alleen een `MemoryStream` bevat, die wordt vrijgegeven wanneer de handler door de garbage collector wordt opgeruimd. Toch is het aanroepen van `Dispose` een goede gewoonte. |
| **Hoe wijzig ik het afbeeldingsformaat (bijv. JPEG in plaats van PNG)?** | Geef een andere bestandsextensie door aan `ImageRenderer.Render`, of gebruik `ImageRenderer.RenderToBitmap` en sla vervolgens op met `bitmap.Save("out.jpg", ImageFormat.Jpeg)`. |
| **Is de ZIP‑handler thread‑safe?** | Nee. `ZipArchive` is niet thread‑safe, dus serialiseer de toegang of maak een aparte handler per thread. |

## Volledig Werkend Voorbeeld

Hieronder vind je een enkel, kant‑en‑klaar programma dat elke besproken stap demonstreert. Vervang `YOUR_DIRECTORY` door een echt pad op jouw machine.

```csharp
// FullExample.cs
using System;
using System.IO;
using System.IO.Compression;

// Assume these types come from your HTML rendering library
using HtmlRendering; // placeholder namespace

class MemoryResourceHandler : ResourceHandler
{
    public MemoryStream OutputStream = new MemoryStream();
    public override Stream HandleResource(ResourceInfo info) => OutputStream;
}

class ZipResourceHandler : ResourceHandler, IDisposable
{
    private readonly ZipArchive _zipArchive;
    public ZipResourceHandler(string zipPath) =>
        _zipArchive = ZipFile.Open(zipPath, ZipArchiveMode.Create);

    public override Stream HandleResource(ResourceInfo info) =>
        _zipArchive.CreateEntry(info.Name).Open();

    protected override void Dispose(bool disposing)
    {
        if (disposing) _zipArchive.Dispose();
        base.Dispose(disposing);
    }

    public void Dispose() => Dispose(true);
}

class Program
{
    static void Main()
    {
        // 1️⃣ Load HTML
        var htmlDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");

        // 2️⃣ Write to a memory stream
        var memHandler = new MemoryResourceHandler();
        htmlDoc.Save(memHandler);
        memHandler.OutputStream.Position = 0;
        // Optional: verify content
        // Console.WriteLine(new StreamReader(memHandler.OutputStream).ReadToEnd());

        // 3️⃣ Zip the same document
        using (var zipHandler = new ZipResourceHandler("YOUR_DIRECTORY/output.zip"))
        {
            htmlDoc.Save(zipHandler);
        }

        // 4️⃣ Change font style programmatically
        htmlDoc.DefaultViewStyleSheet.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // 5️⃣ Render to PNG with antialiasing & hinting
        var renderOpts = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            UseHinting = true
        };
        new ImageRenderer(renderOpts).Render(htmlDoc, "YOUR_DIRECTORY/out.png");

        Console.WriteLine("All operations completed successfully.");
    }
}
```

Wanneer je dit programma uitvoert, krijg je drie artefacten:

1. **In‑memory HTML** opgeslagen in `memHandler.OutputStream`.  
2. **`output.zip`** met de HTML en alle gekoppelde resources.  
3. **`out.png`** – een gerenderde afbeelding die de vet‑cursieve stijl respecteert.

## Conclusie

We hebben laten zien hoe je **een memory stream** in C# maakt en deze naadloos integreert met HTML‑rendering, ZIP‑archivering en afbeelding‑generatie. De belangrijkste les is dat één enkele `HTMLDocument` op meerdere manieren kan worden opgeslagen – in een `MemoryStream`, een ZIP‑archief, of een PNG‑bestand – simpelweg door de `ResourceHandler` te wisselen.  

Als je klaar bent om verder te gaan, probeer dan:

- **Renderen naar PDF** met een PDF‑renderer die een `Stream` accepteert.  
- **De memory stream comprimeren** voordat je deze over een netwerk stuurt (bijv. `GZipStream`).  
- **Meerdere HTML‑pagina's combineren** in één ZIP voor bulk‑export.

Voel je vrij om te experimenteren, en aarzel niet om een reactie achter te laten als je ergens vastloopt. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}