---
category: general
date: 2026-05-06
description: Hoe ZipArchive in C# te gebruiken om HTML op te slaan als een ZIP‑archief.
  Leer hoe je een zip‑archief in C# maakt van HTML‑bronnen met Aspose.HTML.
draft: false
keywords:
- how to use ziparchive
- save html as zip
- create zip archive c#
- create zip from html
language: nl
og_description: Hoe ZipArchive in C# te gebruiken om een HTML‑document en de bijbehorende
  resources in één ZIP‑bestand te bundelen. Stapsgewijze handleiding met volledige
  code.
og_title: Hoe ZipArchive in C# te gebruiken – HTML opslaan als ZIP
tags:
- C#
- Aspose.HTML
- ZipArchive
- File I/O
title: Hoe ZipArchive in C# te gebruiken – HTML opslaan als ZIP
url: /nl/net/html-extensions-and-conversions/how-to-use-ziparchive-in-c-save-html-as-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe ZipArchive te gebruiken in C# – HTML opslaan als ZIP

Heb je je ooit afgevraagd hoe je ZipArchive in C# kunt gebruiken wanneer je een HTML‑pagina moet leveren samen met afbeeldingen, CSS en lettertypen? Je bent niet de enige. In veel web‑naar‑desktop‑scenario's is de eenvoudigste manier om een volledige pagina te verplaatsen alles in een ZIP‑bestand te verpakken.  

In deze tutorial lopen we stap voor stap door **HTML opslaan als zip** met behulp van Aspose.HTML en een aangepaste `ResourceHandler`. Aan het einde weet je precies hoe je zip‑archive c#‑projecten maakt die automatisch elke gekoppelde bron vastleggen, en je hebt een volledig, uitvoerbaar voorbeeld dat je in je eigen codebase kunt plaatsen.

## Wat je gaat bouwen

- Laad een bestaand `input.html`‑bestand.
- Leg elke externe bron (afbeeldingen, stylesheets, lettertypen) vast terwijl het document wordt opgeslagen.
- Schrijf elke bron direct naar een `ZipArchive`‑entry zodat het uiteindelijke bestand een net `output.zip` is.
- Controleer of de ZIP de verwachte mapstructuur bevat.

Er zijn geen extra zip‑bibliotheken van derden nodig—alleen de ingebouwde `System.IO.Compression`‑namespace en Aspose.HTML.

## Vereisten

- .NET 6.0 of later (de code werkt ook op .NET Framework 4.8).
- Aspose.HTML voor .NET (gratis proefversie of gelicentieerde versie). Installeer via NuGet: `dotnet add package Aspose.HTML`.
- Basiskennis van C# bestands‑I/O en streams.

Als je dat hebt, laten we erin duiken.

![diagram hoe ziparchive te gebruiken](image.png "Diagram dat HTML → ZipArchive stroom toont – hoe ziparchive te gebruiken")

## Stap 1: Maak een aangepaste ResourceHandler

Aspose.HTML roept `ResourceHandler.HandleResource` aan voor elk extern bestand dat het moet schrijven. Door deze methode te overschrijven kunnen we de renderer een stream geven die direct naar een ZIP‑entry wijst.

```csharp
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Rendering;

/// <summary>
/// Writes each HTML resource (image, CSS, font) into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(Stream zipStream)
    {
        // Open the archive for updating; leaveOpen keeps the underlying stream alive.
        _zipArchive = new ZipArchive(zipStream, ZipArchiveMode.Update, leaveOpen: true);
    }

    public override Stream HandleResource(ResourceInfo info)
    {
        // The URI's AbsolutePath contains the file name (e.g., "/images/logo.png").
        // Trim the leading slash so the entry appears at the root of the zip.
        var entryName = info.Uri.AbsolutePath.TrimStart('/');
        var entry = _zipArchive.CreateEntry(entryName, CompressionLevel.Optimal);

        // Return the entry's stream; Aspose will write the content straight into it.
        return entry.Open();
    }
}
```

**Waarom een aangepaste handler?**  
Zonder deze zou Aspose.HTML elke bron naar een tijdelijk bestand op schijf schrijven, waarna je alles zelf naar een ZIP zou moeten kopiëren. Deze handler elimineert de tussenstap, vermindert I/O en houdt de code overzichtelijk.

## Stap 2: Laad het HTML‑document

Nu laden we eenvoudigweg het bronbestand. Aspose.HTML ondersteunt zowel lokale paden als URL's, dus je kunt naar een externe pagina wijzen als je dat wilt.

```csharp
// Replace with the folder where your HTML lives.
string inputPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// The HTMLDocument constructor reads the file and parses it.
var document = new HTMLDocument(inputPath);
```

**Pro tip:** Als je HTML bronnen met relatieve URL's verwijst, zorg er dan voor dat het `input.html`‑bestand naast die assets staat. De `ResourceHandler` ontvangt de exacte paden die Aspose oplost.

## Stap 3: Koppel de ZipResourceHandler en sla op

Met het document klaar en onze handler gedefinieerd, openen we een `FileStream` voor de output‑ZIP, maken we de handler aan en roepen we `document.Save` aan. De opslaan‑operatie triggert `HandleResource` voor elk extern bestand.

```csharp
// The final ZIP will be placed in the same directory.
string zipPath = Path.Combine("YOUR_DIRECTORY", "output.zip");

// Open a FileStream for the zip – FileMode.Create overwrites any existing file.
using (var zipStream = new FileStream(zipPath, FileMode.Create))
{
    var zipHandler = new ZipResourceHandler(zipStream);

    // Save the HTML document; the handler captures all linked resources.
    document.Save(zipHandler);
}
```

Wanneer `Save` voltooid is, bevat `output.zip`:

```
/index.html          (the original HTML file)
/styles/main.css
/images/logo.png
/fonts/open-sans.ttf
...
```

Je kunt de ZIP openen met elke archiefbeheerder om de structuur te verifiëren.

## Stap 4: Verifieer het resultaat (optioneel)

Een snelle sanity‑check bespaart je later van mysterieuze ontbrekende‑afbeelding‑bugs.

```csharp
using (var archive = ZipFile.OpenRead(zipPath))
{
    Console.WriteLine("Entries in the ZIP:");
    foreach (var entry in archive.Entries)
    {
        Console.WriteLine($"- {entry.FullName} ({entry.Length} bytes)");
    }
}
```

Het uitvoeren van dit fragment print elke bestandsnaam, wat bevestigt dat het **create zip from html**‑proces geslaagd is.

## Veelvoorkomende randgevallen & hoe ze aan te pakken

| Situatie | Waar op te letten | Aanbevolen oplossing |
|-----------|-------------------|----------------------|
| **Absolute URL's** (bijv. `https://example.com/img.png`) | Aspose zal proberen de bron te downloaden; de handler ontvangt een stream die naar een tijdelijk bestand wijst. | Zorg ervoor dat je machine internettoegang heeft, of download de assets vooraf en herschrijf de HTML om lokale paden te gebruiken. |
| **Dubbele bestandsnamen** (twee afbeeldingen met de naam `logo.png` in verschillende mappen) | ZIP‑entries moeten unieke paden hebben; anders overschrijft de tweede entry de eerste. | Behoud de maphiërarchie in de entry‑naam (`info.Uri.AbsolutePath.TrimStart('/')`). |
| **Grote bronnen** (video's van megabyte‑grootte) | Direct naar een zip‑entry schrijven is prima, maar je wilt misschien `CompressionLevel.NoCompression` instellen voor al gecomprimeerde media. | Pas `CreateEntry(entryName, CompressionLevel.NoCompression)` aan voor bekende mediatypen. |
| **Niet‑ondersteunde formaten** (bijv. SVG met externe lettertypen) | Sommige bronnen kunnen extra bestanden refereren die Aspose niet automatisch oplost. | Voeg die bestanden handmatig toe aan de ZIP na de `Save`‑aanroep. |

## Tips voor productie‑klare code

- **Correct opruimen** – Zowel `ZipArchive` als `HTMLDocument` implementeren `IDisposable`. Omhul ze in `using`‑blokken, zoals getoond, om native resources vrij te geven.
- **Thread‑veiligheid** – De handler is niet thread‑safe; vermijd het gebruik van dezelfde `ZipResourceHandler`‑instantie vanuit meerdere threads.
- **Prestaties** – Voor enorme HTML‑bundels, overweeg om de HTML zelf te streamen naar de ZIP (`zipArchive.CreateEntry("index.html").Open()`), en roep vervolgens `document.Save(stream)` aan waarbij `stream` de stream van die entry is.

## Volledig werkend voorbeeld

Hieronder staat het volledige programma dat je kunt kopiëren‑en‑plakken in een console‑app. Het bevat alle `using`‑directieven, foutafhandeling en commentaren.

```csharp
// ------------------------------------------------------------
// How to Use ZipArchive in C# – Save HTML as ZIP (Full Demo)
// ------------------------------------------------------------
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Rendering;

class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(Stream zipStream)
    {
        _zipArchive = new ZipArchive(zipStream, ZipArchiveMode.Update, leaveOpen: true);
    }

    public override Stream HandleResource(ResourceInfo info)
    {
        var entryName = info.Uri.AbsolutePath.TrimStart('/');
        var entry = _zipArchive.CreateEntry(entryName, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Paths – adjust to your environment.
            string baseDir = Path.Combine(Environment.CurrentDirectory, "DemoFiles");
            string htmlPath = Path.Combine(baseDir, "input.html");
            string zipPath  = Path.Combine(baseDir, "output.zip");

            // 2️⃣ Load the HTML document.
            var document = new HTMLDocument(htmlPath);

            // 3️⃣ Open the ZIP stream and save.
            using (var zipStream = new FileStream(zipPath, FileMode.Create))
            {
                var zipHandler = new ZipResourceHandler(zipStream);
                document.Save(zipHandler);
            }

            // 4️⃣ Quick verification.
            Console.WriteLine($"ZIP created at: {zipPath}");
            using (var archive = ZipFile.OpenRead(zipPath))
            {
                Console.WriteLine("Contents:");
                foreach (var entry in archive.Entries)
                    Console.WriteLine($"- {entry.FullName} ({entry.Length} bytes)");
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

Compileer met `dotnet run` (of je IDE naar keuze) en open `output.zip`. Je zou de originele HTML plus elke gerefereerde asset netjes verpakt moeten zien. Dat is de volledige **create zip archive c#**‑workflow in actie.

## Conclusie

We hebben zojuist laten zien **hoe ZipArchive te gebruiken** om **HTML op te slaan als zip** en een nette manier gedemonstreerd om **zip from html** te **creëren** met behulp van Aspose.HTML’s `ResourceHandler`. De belangrijkste punten zijn:

- Overschrijf `ResourceHandler` om bronnen direct naar een `ZipArchive` te streamen.
- Houd de ZIP open gedurende de hele opslaan‑operatie (`leaveOpen: true`).
- Verifieer de output en behandel randgevallen zoals absolute URL's of dubbele namen.

Nu kun je dit patroon integreren in web‑naar‑desktop‑exporters, offline documentatie‑generatoren, of elk scenario waarbij het bundelen van een HTML‑pagina met zijn assets vereist is.  

Wil je verder gaan? Probeer meerdere HTML‑pagina's te comprimeren in één archief, of voeg een manifest‑bestand toe dat alle entries opsomt. Je zou ook kunnen onderzoeken het versleutelen van de

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}