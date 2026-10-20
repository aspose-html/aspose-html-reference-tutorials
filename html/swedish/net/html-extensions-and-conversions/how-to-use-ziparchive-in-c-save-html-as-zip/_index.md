---
category: general
date: 2026-05-06
description: Hur man använder ZipArchive i C# för att spara HTML som ett ZIP‑arkiv.
  Lär dig skapa zip‑arkiv i C# från HTML‑resurser med Aspose.HTML.
draft: false
keywords:
- how to use ziparchive
- save html as zip
- create zip archive c#
- create zip from html
language: sv
og_description: Hur man använder ZipArchive i C# för att samla ett HTML‑dokument och
  dess resurser i en enda ZIP‑fil. Steg‑för‑steg‑guide med fullständig kod.
og_title: Hur man använder ZipArchive i C# – Spara HTML som ZIP
tags:
- C#
- Aspose.HTML
- ZipArchive
- File I/O
title: Hur man använder ZipArchive i C# – Spara HTML som ZIP
url: /sv/net/html-extensions-and-conversions/how-to-use-ziparchive-in-c-save-html-as-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder ZipArchive i C# – Spara HTML som ZIP

Har du någonsin undrat hur du använder ZipArchive i C# när du behöver leverera en HTML‑sida tillsammans med bilder, CSS och typsnitt? Du är inte ensam. I många web‑till‑desktop‑scenarier är det enklaste sättet att flytta en hel sida att packa allt i en ZIP‑fil.  

I den här handledningen går vi igenom **spara HTML som zip** med Aspose.HTML och en anpassad `ResourceHandler`. I slutet kommer du exakt att veta hur du skapar zip archive c# projects som automatiskt fångar varje länkad resurs, och du får ett komplett, körbart exempel som du kan lägga in i din egen kodbas.

## Vad du kommer att bygga

- Ladda en befintlig `input.html`‑fil.
- Fånga varje extern tillgång (bilder, stilmallar, typsnitt) medan dokumentet sparas.
- Skriv varje tillgång direkt in i ett `ZipArchive`‑objekt så den slutgiltiga filen blir ett prydligt `output.zip`.
- Verifiera att ZIP‑filen innehåller den förväntade mappstrukturen.

Inga ytterligare tredjeparts‑zip‑bibliotek krävs – bara den inbyggda `System.IO.Compression`‑namnrymden och Aspose.HTML.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar även på .NET Framework 4.8).
- Aspose.HTML för .NET (gratis provversion eller licensierad version). Installera via NuGet: `dotnet add package Aspose.HTML`.
- Grundläggande kunskap om C#‑fil‑I/O och strömmar.

Om du har dem, låt oss dyka ner.

![how to use ziparchive diagram](image.png "Diagram showing HTML → ZipArchive flow – how to use ziparchive")

## Steg 1: Skapa en anpassad ResourceHandler

Aspose.HTML anropar `ResourceHandler.HandleResource` för varje extern fil den behöver skriva. Genom att åsidosätta den här metoden kan vi ge renderaren en ström som pekar direkt på ett ZIP‑objekt.

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

**Varför en anpassad handler?**  
Utan den skulle Aspose.HTML skriva varje resurs till en temporär fil på disken, och du skulle behöva kopiera allt till en ZIP själv. Denna handler eliminerar det mellansteg, minskar I/O och håller koden prydlig.

## Steg 2: Ladda HTML‑dokumentet

Nu laddar vi helt enkelt källfilen. Aspose.HTML stöder både lokala sökvägar och URL:er, så du kan peka på en fjärrsida om du vill.

```csharp
// Replace with the folder where your HTML lives.
string inputPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// The HTMLDocument constructor reads the file and parses it.
var document = new HTMLDocument(inputPath);
```

**Proffstips:** Om din HTML refererar till resurser med relativa URL:er, se till att `input.html`‑filen ligger bredvid dessa tillgångar. `ResourceHandler` kommer att få de exakta sökvägar som Aspose löser upp.

## Steg 3: Anslut ZipResourceHandler och spara

Med dokumentet klart och vår handler definierad öppnar vi ett `FileStream` för utdata‑ZIP, instansierar handlern och anropar `document.Save`. Spara‑operationen triggar `HandleResource` för varje extern fil.

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

När `Save` är klar innehåller `output.zip`:

```
/index.html          (the original HTML file)
/styles/main.css
/images/logo.png
/fonts/open-sans.ttf
...
```

Du kan öppna ZIP‑filen med valfri arkivhanterare för att verifiera strukturen.

## Steg 4: Verifiera resultatet (valfritt)

En snabb kontroll sparar dig från mystiska saknade‑bild‑buggar senare.

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

Att köra detta kodstycke skriver ut varje filnamn och bekräftar att processen **create zip from html** lyckades.

## Vanliga kantfall & hur du hanterar dem

| Situation | Vad du bör hålla utkik efter | Föreslagen åtgärd |
|-----------|------------------------------|-------------------|
| **Absoluta URL:er** (t.ex. `https://example.com/img.png`) | Aspose kommer att försöka ladda ner resursen; handlern får en ström som pekar på en temporär fil. | Se till att din maskin har internetåtkomst, eller för‑ladda tillgångarna och skriv om HTML‑en för att använda lokala sökvägar. |
| **Duplicerade filnamn** (två bilder med namnet `logo.png` i olika mappar) | ZIP‑objekt måste ha unika sökvägar; annars skriver det andra objektet över det första. | Bevara mapphierarkin i objektets namn (`info.Uri.AbsolutePath.TrimStart('/')`). |
| **Stora resurser** (videor i megabyte‑storlek) | Att skriva direkt till ett zip‑objekt är okej, men du kanske vill sätta `CompressionLevel.NoCompression` för redan komprimerade media. | Justera `CreateEntry(entryName, CompressionLevel.NoCompression)` för kända mediatyper. |
| **Ej stödda format** (t.ex. SVG med externa typsnitt) | Vissa resurser kan referera till ytterligare filer som Aspose inte löser automatiskt. | Lägg till dessa filer manuellt i ZIP‑filen efter `Save`‑anropet. |

## Tips för produktionsklar kod

- **Disposera korrekt** – Både `ZipArchive` och `HTMLDocument` implementerar `IDisposable`. Wrappa dem i `using`‑block, som visas, för att frigöra inhemska resurser.
- **Trådsäkerhet** – Handlern är inte trådsäker; undvik att använda samma `ZipResourceHandler`‑instans från flera trådar.
- **Prestanda** – För massiva HTML‑paket, överväg att strömma själva HTML‑en in i ZIP (`zipArchive.CreateEntry("index.html").Open()`), och anropa sedan `document.Save(stream)` där `stream` är det objektets ström.

## Fullt fungerande exempel

Nedan är det kompletta programmet som du kan kopiera‑klistra in i en konsolapp. Det inkluderar alla `using`‑direktiv, felhantering och kommentarer.

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

Kompilera med `dotnet run` (eller din föredragna IDE) och öppna `output.zip`. Du bör se den ursprungliga HTML‑en plus varje refererad tillgång, prydligt paketerad. Det är hela arbetsflödet **create zip archive c#** i handling.

## Slutsats

Vi har just visat **hur man använder ZipArchive** för att **spara HTML som zip** och demonstrerat ett rent sätt att **create zip from html** med Aspose.HTML:s `ResourceHandler`. De viktigaste slutsatserna är:

- Åsidosätt `ResourceHandler` för att strömma resurser direkt in i ett `ZipArchive`.
- Håll ZIP‑filen öppen under hela spara‑operationen (`leaveOpen: true`).
- Verifiera resultatet och hantera kantfall som absoluta URL:er eller duplicerade namn.

Nu kan du integrera detta mönster i web‑till‑desktop‑exportörer, offline‑dokumentationsgeneratorer eller vilket scenario som helst där du behöver paketera en HTML‑sida med dess tillgångar.

Vill du gå längre? Försök komprimera flera HTML‑sidor till ett enda arkiv, eller lägg till en manifestfil som listar alla objekt. Du kan också utforska att kryptera 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}