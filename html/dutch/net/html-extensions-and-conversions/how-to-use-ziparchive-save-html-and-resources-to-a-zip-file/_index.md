---
category: general
date: 2026-03-29
description: Leer hoe je ZipArchive in C# gebruikt om HTML naar ZIP te converteren,
  HTML op te slaan in ZIP en HTML‑afbeeldingen te comprimeren — allemaal in één duidelijke
  tutorial.
draft: false
keywords:
- how to use ziparchive
- convert html to zip
- save html to zip
- create zip archive c#
- compress html images
language: nl
og_description: Ontdek hoe je ZipArchive in C# kunt gebruiken om HTML naar ZIP te
  converteren, HTML op te slaan in ZIP en HTML-afbeeldingen te comprimeren met een
  volledig, uitvoerbaar voorbeeld.
og_title: Hoe ZipArchive te gebruiken – HTML en bronnen opslaan in een ZIP‑bestand
tags:
- C#
- .NET
- Aspose.Html
- ZipArchive
title: Hoe ZipArchive te gebruiken – HTML en bronnen opslaan in een ZIP‑bestand
url: /nl/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe ZipArchive te gebruiken – HTML en bronnen opslaan in een ZIP‑bestand

Heb je je ooit afgevraagd **hoe je ZipArchive** kunt gebruiken om een HTML‑pagina samen te bundelen met zijn afbeeldingen, CSS en andere assets? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze een zelf‑containende HTML‑package moeten leveren, vooral wanneer de pagina externe bronnen verwijst. Het goede nieuws? Met een paar regels C# en Aspose.HTML kun je **HTML naar ZIP converteren**, **HTML naar ZIP opslaan**, en zelfs **HTML‑afbeeldingen comprimeren** zonder je IDE te verlaten.

In deze tutorial lopen we het volledige proces door – van het maken van een eenvoudige `HTMLDocument` tot het afhandelen van elke gekoppelde bron via een aangepaste `ResourceHandler`. Aan het einde heb je een kant‑klaar ZIP‑bestand dat je in elke webserver of e‑mailbijlage kunt plaatsen. Geen externe scripts, geen handmatig kopiëren – alleen pure .NET.

## Vereisten

- **.NET 6+** (of .NET Framework 4.6+). De gebruikte API's maken deel uit van `System.IO.Compression`.
- **Aspose.HTML for .NET** geïnstalleerd (NuGet‑pakket `Aspose.Html`).
- Een basisbegrip van C#‑syntaxis.
- Een IDE zoals Visual Studio of VS Code.

Dat is alles. Geen extra tools, geen zip‑hulpmiddelen van derden. Klaar? Laten we beginnen.

## Stap 1: Het project opzetten en afhankelijkheden toevoegen

Maak een nieuw console‑project aan:

```bash
dotnet new console -n HtmlToZipDemo
cd HtmlToZipDemo
dotnet add package Aspose.Html
```

Het `Aspose.Html`‑pakket levert de `HTMLDocument`‑klasse en de `ResourceHandler`‑basisklasse die we later zullen uitbreiden. De ingebouwde `System.IO.Compression`‑namespace biedt `ZipArchive` en `ZipArchiveEntry`.

> **Pro tip:** Als je .NET 6 targett, kun je top‑level statements gebruiken om de `Main`‑methode overzichtelijk te houden. De onderstaande code gebruikt een klassieke `Program`‑klasse voor duidelijkheid.

## Stap 2: Een aangepaste Resource Handler maken

Wanneer Aspose.HTML een document opslaat, vraagt het een `ResourceHandler` om een `Stream` te leveren voor elk extern bestand (afbeeldingen, CSS, lettertypen, enz.). Door `HandleResource` te overschrijven kunnen we elke bron rechtstreeks naar een zip‑entry sturen.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Writes each HTML resource (image, CSS, etc.) directly into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(ZipArchive zipArchive) => _zipArchive = zipArchive;

    public override Stream HandleResource(string resourceName, ResourceType resourceType)
    {
        // Ensure a folder hierarchy inside the zip (optional but tidy)
        var entry = _zipArchive.CreateEntry(resourceName, CompressionLevel.Optimal);
        return entry.Open(); // Aspose streams the content into this entry.
    }
}
```

**Waarom dit belangrijk is:** In plaats van bronnen eerst naar schijf te schrijven en ze daarna te zippen, streamt de handler ze direct, wat de I/O‑overhead vermindert en garandeert dat de zip synchroon blijft met de HTML‑inhoud.

## Stap 3: Het HTML‑document bouwen

Voor demonstratie zullen we een klein HTML‑fragment insluiten dat verwijst naar een externe afbeelding genaamd `logo.png`. In een echt project laad je HTML mogelijk uit een bestand of een database.

```csharp
// Create a simple HTML document with an external image reference.
HTMLDocument htmlDocument = new HTMLDocument(
    "<html><body><h1>Welcome!</h1><img src='logo.png' alt='Demo logo'></body></html>"
);
```

Als je **HTML‑afbeeldingen wilt comprimeren**, zorg er dan voor dat het afbeeldingsbestand naast het uitvoerbare bestand staat (of embed het als resource). De `ZipResourceHandler` voegt de afbeelding automatisch toe aan het archief.

## Stap 4: Het ZIP‑bestand openen (of maken) en opslaan

Nu verbinden we alles. We openen een `FileStream` voor de output‑zip, maken een `ZipArchive` aan in *Update*‑modus, en geven onze aangepaste handler door aan `HTMLDocument.Save`.

```csharp
using (var fileStream = new FileStream("output.zip", FileMode.Create))
using (var zipArchive = new ZipArchive(fileStream, ZipArchiveMode.Update))
{
    // Initialise the handler with the open ZipArchive.
    var zipHandler = new ZipResourceHandler(zipArchive);

    // Save the HTML document; the handler writes HTML, images, CSS, etc. into the zip.
    htmlDocument.Save(zipHandler);
}
```

Wanneer de `using`‑blokken eindigen, wordt de zip automatisch afgerond en gesloten. Het resulterende `output.zip` bevat:

- `index.html` (het geserialiseerde HTML‑document)
- `logo.png` (de afbeelding die in de HTML wordt verwezen)

Je kunt de inhoud verifiëren door de zip te openen in een willekeurige bestandsverkenner.

## Stap 5: Het resultaat verifiëren (optioneel)

Het is altijd een goed idee om dubbel te controleren of de zip daadwerkelijk werkt. Hier is een kort fragment dat je kunt uitvoeren na de vorige code om de entries te tonen:

```csharp
using (var zip = ZipFile.OpenRead("output.zip"))
{
    Console.WriteLine("Contents of output.zip:");
    foreach (var entry in zip.Entries)
        Console.WriteLine($"- {entry.FullName} ({entry.Length} bytes)");
}
```

Je zou iets moeten zien zoals:

```
Contents of output.zip:
- index.html (1234 bytes)
- logo.png (45678 bytes)
```

Open `index.html` vanuit de uitgepakte map, en je ziet de afbeelding correct weergegeven – bewijs dat **HTML naar ZIP opslaan** werkt zoals bedoeld.

## Veelvoorkomende variaties & randgevallen

### 1. Een andere entry‑naam gebruiken voor het HTML‑bestand

Standaard schrijft Aspose de HTML naar `index.html`. Als je een aangepaste naam nodig hebt, kun je `htmlDocument.FileName` instellen vóór het opslaan:

```csharp
htmlDocument.FileName = "myPage.html";
htmlDocument.Save(zipHandler);
```

### 2. Handmatig extra bestanden toevoegen

Soms wil je extra bestanden bundelen (bijv. een README). Je kunt ze direct toevoegen aan de `ZipArchive` voordat je `htmlDocument.Save` aanroept:

```csharp
var readme = zipArchive.CreateEntry("README.txt", CompressionLevel.Optimal);
using (var writer = new StreamWriter(readme.Open()))
{
    writer.WriteLine("This ZIP contains an HTML page generated with Aspose.HTML.");
}
```

### 3. Grote afbeeldingen efficiënt verwerken

Als je HTML naar zeer grote afbeeldingen verwijst, overweeg ze van tevoren te verkleinen om de zip‑grootte redelijk te houden. Het `System.Drawing.Common`‑pakket kan helpen:

```csharp
// Example: Resize logo.png to a max width of 800px before zipping.
using (var img = System.Drawing.Image.FromFile("logo.png"))
{
    int maxWidth = 800;
    if (img.Width > maxWidth)
    {
        var ratio = (double)maxWidth / img.Width;
        var newHeight = (int)(img.Height * ratio);
        using var thumb = img.GetThumbnailImage(maxWidth, newHeight, () => false, IntPtr.Zero);
        thumb.Save("logo_resized.png");
    }
}
```

Verwijs vervolgens in je HTML naar `<img src='logo_resized.png'>`.

## Volledig, uitvoerbaar voorbeeld

Hieronder staat het volledige programma dat je kunt kopiëren‑plakken in `Program.cs`. Het compileert en draait direct, ervan uitgaande dat je het Aspose.HTML‑NuGet‑pakket hebt geïnstalleerd.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Custom handler that streams each resource into a zip entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;
    public ZipResourceHandler(ZipArchive zipArchive) => _zipArchive = zipArchive;

    public override Stream HandleResource(string resourceName, ResourceType resourceType)
    {
        var entry = _zipArchive.CreateEntry(resourceName, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Create an HTML document that references an external image.
        HTMLDocument htmlDocument = new HTMLDocument(
            "<html><head><title>Demo</title></head>" +
            "<body><h2>Hello, ZipArchive!</h2>" +
            "<img src='logo.png' alt='Demo logo'></body></html>"
        );

        // 2️⃣ Open (or create) the output zip file.
        using (var fileStream = new FileStream("output.zip", FileMode.Create))
        using (var zipArchive = new ZipArchive(fileStream, ZipArchiveMode.Update))
        {
            // 3️⃣ Initialise the custom handler.
            var zipHandler = new ZipResourceHandler(zipArchive);

            // 4️⃣ Save the HTML; resources get streamed into the zip.
            htmlDocument.Save(zipHandler);
        }

        Console.WriteLine("✅ HTML document and its resources have been saved to output.zip");
    }
}
```

**Verwachte output:** De console print een succesbericht, en `output.zip` verschijnt in de projectmap met `index.html` en `logo.png`.

## Veelgestelde vragen

- **Werkt dit op .NET Core?**  
  Ja. `System.IO.Compression.ZipArchive` maakt deel uit van .NET Standard, dus dezelfde code draait op .NET 5, .NET 6 en .NET 7.

- **Wat als ik **HTML‑afbeeldingen** agressiever wil comprimeren?**  
  Je kunt afbeeldingen vooraf verwerken (verkleinen, formaat wijzigen naar WebP, enz.) voordat ze aan de zip worden toegevoegd. De handler zelf streamt alleen de ontvangen data.

- **Kan ik de zip versleutelen?**  
  `ZipArchive` ondersteunt AES‑versleuteling alleen via third‑party‑bibliotheken (bijv. `SharpZipLib`). Als je versleuteling nodig hebt, maak je de zip met die bibliotheek en geef je de stream vervolgens door aan Aspose als een aangepaste `ResourceHandler`.

- **Is er een manier om de hoofdmap binnen de zip in te stellen?**  
  Ja – voeg een mapnaam toe vóór `resourceName` in `HandleResource`, bijvoorbeeld `var entry = _zipArchive.CreateEntry($"site/{resourceName}", ...)`.

## Conclusie

Je weet nu **hoe je ZipArchive** in C# kunt gebruiken om **HTML naar ZIP te converteren**, **HTML naar ZIP op te slaan**, en **HTML‑afbeeldingen te comprimeren** in één enkele, nette workflow. Door `ResourceHandler` uit te breiden vermeden we tijdelijke bestanden en hielden we het proces geheugen‑efficiënt. Het patroon schaalt goed: plaats de gegenereerde zip gewoon op een webserver, stuur hem per e‑mail, of sla hem op in cloud‑opslag.

Volgende stappen die je kunt verkennen:

- **Maak ZIP‑archieven programmatisch** voor volledige website‑mappen (`create zip archive c#`).
- **Voeg PDF‑ of DOCX‑conversies toe** vóór het zippen voor rijkere documentatie‑pakketten.
- **Integreer met ASP.NET Core** om de zip direct naar een client‑browser te streamen (`FileStreamResult`).

Heb je meer vragen over het zippen van HTML, het verwerken van lettertypen, of het optimaliseren van afbeeldingsgrootte? Laat een reactie achter of ping me op Stack Overflow. Veel plezier met coderen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}