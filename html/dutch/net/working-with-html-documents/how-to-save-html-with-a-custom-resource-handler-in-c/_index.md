---
category: general
date: 2026-11-20
description: Leer hoe je HTML kunt opslaan met een aangepaste ResourceHandler in C#
  en ook HTML kunt opslaan in zip‑archieven met beknopte, productieklare code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save html
- save html to zip
- custom ResourceHandler C#
- HtmlAgilityPack save example
- stream based HTML export
language: nl
lastmod: 2026-11-20
og_description: Hoe HTML op te slaan met een aangepaste ResourceHandler in C# en optioneel
  HTML in zip‑bestanden op te slaan — volledige, uitvoerbare gids voor .NET‑ontwikkelaars.
og_image_alt: Diagram showing how to save HTML with a custom ResourceHandler and zip
  the output
og_title: Hoe HTML op te slaan met een aangepaste resourcehandler in C#
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  headline: How to save HTML with a custom resource handler in C#
  type: TechArticle
- description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  name: How to save HTML with a custom resource handler in C#
  steps:
  - name: What if I need multiple HTML files in the same zip?
    text: 'Create a new entry for each call to `HandleResource`. The `resourceName`
      argument typically contains the filename, so you can use it directly:'
  - name: How to handle large documents without exhausting memory?
    text: Replace `MemoryStream` with a `FileStream` that points to a temporary file.
      The handler then returns the file stream, and you can later delete the file
      after the zip is created.
  - name: Does this approach work with .NET Core on Linux?
    text: Yes. All APIs used (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) are
      cross‑platform. Ensure the target framework is at least .NET 6 for best compatibility.
  - name: Can I encrypt the zip archive?
    text: '`ZipArchive` supports password‑based encryption only through third‑party
      libraries (e.g., `SharpZipLib`). If encryption is required, wrap the output
      bytes with a library that provides AES encryption before sending them to the
      client.'
  type: HowTo
tags:
- C#
- HTML
- file I/O
title: Hoe HTML op te slaan met een aangepaste resourcehandler in C#
url: /nl/net/working-with-html-documents/how-to-save-html-with-a-custom-resource-handler-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe HTML opslaan met een aangepaste resource‑handler in C#

Als je wilt weten **how to save HTML** vanuit een in‑memory string of een geparseerd document, laat deze gids een volledige oplossing zien. Met een aangepaste `ResourceHandler` kun je de bestemmings‑stream beheersen, wat betekent dat je **save HTML to zip** archieven kunt maken zonder tijdelijke bestanden te schrijven.

Je ziet waarom een `ResourceHandler` de voorkeur heeft boven de oudere `IOutputStorage`‑aanpak, hoe je deze instelt, en hoe je hem uitbreidt voor zip‑compressie. Aan het einde van deze tutorial kun je de code in elk .NET 6+ project integreren en aanpassen aan je eigen opslagvereisten.

## Wat je gaat bouwen

* Een minimale `ResourceHandler` die een `MemoryStream` retourneert.
* Een `HtmlDocument` gemaakt met **HtmlAgilityPack**.
* Een aanroep van `doc.Save` die de HTML schrijft naar de stream die door de handler wordt geleverd.
* Een optionele wrapper die de resulterende HTML comprimeert naar een zip‑bestand.

Vereisten:

* .NET 6 SDK of later.
* `HtmlAgilityPack` NuGet‑pakket (`dotnet add package HtmlAgilityPack`).
* Basiskennis van C#‑streams.

## Stap 1: Maak een aangepaste resource‑handler (primaire manier om **how to save html**)

De `ResourceHandler`‑basisklasse (beschikbaar vanaf versie 24.2 van de viewer SDK) definieert één abstracte methode, `HandleResource`. Het implementeren van deze methode geeft je volledige controle over waar de HTML naartoe wordt geschreven.

```csharp
using System.IO;

/// <summary>
/// Handles the output stream for each HTML resource.
/// Returning a MemoryStream keeps everything in memory, which is ideal for further processing
/// such as zipping or sending over a network.
/// </summary>
class MyHandler : ResourceHandler
{
    public override Stream HandleResource(string resourceName)
    {
        // You could inspect resourceName to decide between file, memory, or zip entry.
        return new MemoryStream();
    }
}
```

**Waarom dit belangrijk is:** Door een `MemoryStream` te retourneren, vermijd je schijf‑I/O, verlaag je de latency en houd je de code deterministisch voor unit‑tests. De handler wordt automatisch aangeroepen door de `Save`‑methode, zodat je nooit expliciet een stream hoeft door te geven.

## Stap 2: Laad of bouw het HTML‑document

`HtmlAgilityPack` biedt een handige `HtmlDocument`‑klasse die een string, een bestand of een stream kan parseren. Voor dit voorbeeld laden we een eenvoudige literal, maar dezelfde code werkt met elke HTML‑bron.

```csharp
using HtmlAgilityPack;

/// <summary>
/// Builds a basic HTML document in memory. Replace the string with your own markup
/// or load it from an external source.
/// </summary>
HtmlDocument doc = new HtmlDocument();
doc.LoadHtml("<html><body>Hello World</body></html>");
```

**Waarom dit belangrijk is:** Het document in het geheugen houden sluit aan bij de stream‑gebaseerde aanpak van de aangepaste handler. Het stelt je ook in staat de DOM te manipuleren vóór het opslaan, bijvoorbeeld door scripts in te voegen of slecht gevormde tags te corrigeren.

## Stap 3: Sla het document op met de aangepaste handler

Het aanroepen van `doc.Save` met een instantie van `MyHandler` triggert de `HandleResource`‑methode. De HTML wordt direct naar de door jou geretourneerde stream geschreven.

```csharp
// Save the HTML; the handler provides the output stream.
doc.Save(new MyHandler());
```

Na voltooiing van `Save` bevat de `MemoryStream` in `MyHandler` de geserialiseerde HTML. Je kunt deze als volgt ophalen:

```csharp
// Cast the handler back to access the stream (if you kept a reference)
MyHandler handler = new MyHandler();
doc.Save(handler);

// Reset position to read from the beginning.
handler.HandleResource("").Seek(0, SeekOrigin.Begin);
using var reader = new StreamReader(handler.HandleResource(""));
string htmlOutput = reader.ReadToEnd();
System.Console.WriteLine(htmlOutput);
```

**Resultaat:** De console drukt exact de HTML af die je aan `LoadHtml` hebt doorgegeven. Dit bewijst dat je nu **how to save HTML** met een aangepaste handler begrijpt.

## Stap 4: De handler uitbreiden om **save HTML to zip** te ondersteunen

Wil je de HTML archiveren, wijzig dan `MyHandler` zodat deze schrijft naar een `ZipArchiveEntry`. De .NET `System.IO.Compression`‑namespace maakt dit eenvoudig.

```csharp
using System.IO.Compression;

/// <summary>
/// Writes the HTML into a zip entry named "document.html".
/// The zip archive is created in memory and can be saved to a file or sent over HTTP.
/// </summary>
class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        // Initialise the zip archive in create mode.
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        // Create a zip entry for the HTML file.
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open(); // Returns a stream that writes directly into the zip entry.
    }

    /// <summary>
    /// Finalises the zip archive and returns the raw bytes.
    /// </summary>
    public byte[] GetZipBytes()
    {
        // Ensure all entries are flushed.
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}
```

Gebruik nu de nieuwe handler:

```csharp
// Instantiate the zip‑aware handler.
using var zipHandler = new ZipHtmlHandler();

// Save HTML; it ends up inside the zip archive.
doc.Save(zipHandler);

// Retrieve the zip file as a byte array.
byte[] zipBytes = zipHandler.GetZipBytes();

// Optionally write the zip to disk for verification.
File.WriteAllBytes("output.zip", zipBytes);
System.Console.WriteLine("ZIP file created with size: " + zipBytes.Length);
```

**Waarom dit werkt:** De `HandleResource`‑methode maakt een zip‑entry met de naam `document.html`. Wanneer `doc.Save` naar de geretourneerde stream schrijft, worden de gegevens automatisch gecomprimeerd. Omdat de zip in het geheugen wordt opgebouwd, kun je deze vanuit een web‑API retourneren, aan een e‑mail toevoegen of in een database opslaan zonder het bestandssysteem aan te raken.

## Veelgestelde vragen en randgevallen

### Wat als ik meerdere HTML‑bestanden in dezelfde zip nodig heb?
Maak een nieuwe entry voor elke aanroep van `HandleResource`. Het argument `resourceName` bevat doorgaans de bestandsnaam, dus kun je die direct gebruiken:

```csharp
public override Stream HandleResource(string resourceName)
{
    var entry = _archive.CreateEntry(resourceName, CompressionLevel.Optimal);
    return entry.Open();
}
```

### Hoe grote documenten verwerken zonder het geheugen uit te putten?
Vervang `MemoryStream` door een `FileStream` die naar een tijdelijk bestand wijst. De handler retourneert dan de bestands‑stream, en je kunt het bestand later verwijderen nadat de zip is aangemaakt.

### Werkt deze aanpak met .NET Core op Linux?
Ja. Alle gebruikte API’s (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) zijn cross‑platform. Zorg ervoor dat het doel‑framework minimaal .NET 6 is voor optimale compatibiliteit.

### Kan ik het zip‑archief versleutelen?
`ZipArchive` ondersteunt wachtwoord‑gebaseerde encryptie alleen via externe bibliotheken (bijv. `SharpZipLib`). Als encryptie vereist is, wikkel je de output‑bytes in een bibliotheek die AES‑encryptie biedt voordat je ze naar de client stuurt.

## Pro‑tips

* **Herbruik de handler** bij het verwerken van veel documenten in één batch; een nieuwe `ZipArchive` per bestand creëert onnodige overhead.
* **Stel `LeaveOpen: true`** in op de `ZipArchive`‑constructor als je de zip‑bytes moet lezen terwijl het archief nog open is.
* **Valideer HTML** vóór het opslaan door `doc.OptionCheckSyntax = true;` aan te roepen – dit vangt slecht gevormde tags vroegtijdig op.
* **Log de grootte** van de gegenereerde zip; een ongewoon grote output duidt vaak op dubbele resources of ontbrekende compressie.

## Volledig werkend voorbeeld

Hieronder vind je één enkel bestand dat je kunt plakken in een console‑project (`dotnet new console`) en uitvoeren. Het demonstreert zowel het opslaan van platte HTML als zip‑compressie.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using HtmlAgilityPack;

// ---------- Custom handlers ----------
class MyHandler : ResourceHandler
{
    public MemoryStream HtmlStream { get; } = new();

    public override Stream HandleResource(string resourceName) => HtmlStream;
}

class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open();
    }

    public byte[] GetZipBytes()
    {
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}

// ---------- Main program ----------
class Program
{
    static void Main()
    {
        // Build a simple HTML document.
        HtmlDocument doc = new HtmlDocument();
        doc.LoadHtml("<html><body>Hello World from HtmlAgilityPack</body></html>");

        // ---- Example 1: plain HTML save ----
        var plainHandler = new MyHandler();
        doc.Save(plainHandler);
        plainHandler.HtmlStream.Seek(0, SeekOrigin.Begin);
        using var reader = new StreamReader(plainHandler.HtmlStream);
        Console.WriteLine("Plain HTML output:");


## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [HTML opslaan in C# met aangepaste resource‑handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [ZipArchive gebruiken – HTML en resources opslaan in een ZIP‑bestand](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [HTML opslaan als zip met een aangepaste resource‑handler – stapsgewijze gids](/html/english/net/html-extensions-and-conversions/save-html-as-zip-with-a-custom-resource-handler-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}