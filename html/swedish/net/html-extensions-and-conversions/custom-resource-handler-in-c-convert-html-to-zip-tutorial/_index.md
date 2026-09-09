---
category: general
date: 2026-02-10
description: Anpassad resurs‑hanterare låter dig konvertera HTML till ZIP i C#. Lär
  dig hur du sparar HTML som zip och strömmar HTML‑resurser effektivt.
draft: false
keywords:
- custom resource handler
- convert html to zip
- save html as zip
- create zip with html
- stream html resources
language: sv
og_description: Anpassad resurs‑hanterare låter dig konvertera HTML till ZIP i C#.
  Följ den här steg‑för‑steg‑guiden för att spara HTML som zip och strömma HTML‑resurser.
og_title: Anpassad resurs‑hanterare i C# – Konvertera HTML till ZIP
tags:
- Aspose.HTML
- C#
- ZIP archive
- file streaming
title: Anpassad resurs‑hanterare i C# – Konvertera HTML till ZIP‑handledning
url: /sv/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Anpassad resurs‑hanterare – Konvertera HTML till ZIP i C#

Har du någonsin funderat på hur du **custom resource handler** din väg från rå HTML direkt till en ZIP‑fil? Du är inte ensam. Många utvecklare stöter på problem när de måste paketera en HTML‑sida med dess tillgångar utan att skräpa ner disken med temporära filer. Den goda nyheten? Med Aspose.HTML kan du göra allt i minnet, och tricket ligger i en anpassad resurs‑hanterare.

I den här handledningen går vi igenom ett komplett, körbart exempel som visar hur du **convert HTML to ZIP**, **save HTML as ZIP**, och **stream HTML resources** i farten. I slutet har du en enda metod som tar en sträng med HTML och spottar ut en färdig‑att‑ladda‑ner `result.zip` som innehåller sidan och alla länkade resurser.

> **Prerequisites** – .NET 6+ (eller .NET Framework 4.6+), Aspose.HTML för .NET installerat, och en grundläggande förståelse för streams. Inga externa verktyg krävs.

---

## Anpassad resurs‑hanterare – Grundkoncept

En *resource handler* i Aspose.HTML är ett objekt som bestämmer **var** varje del av ett dokument hamnar – oavsett om det är en fil på disk, en minnesbuffert eller, som vi kommer att visa, ett inlägg i ett ZIP‑arkiv. Genom att subklassa `ResourceHandler` får du full kontroll över utskriftsdestinationen för huvud‑HTML‑filen **och** alla hjälpresurser (CSS, bilder, teckensnitt, etc.).

Tänk på det som en trafikpolis för ditt dokuments tillgångar: `HandleResource`‑metoden ger dig en `Stream` för huvud‑HTML, medan `ResourceSaving`‑händelsen låter dig fånga varje beroende fil precis innan den skrivs.

## Steg 1: Implementera en anpassad resurs‑hanterare

Först, skapa en klass som ärver från `ResourceHandler`. Vi kommer att åsidosätta `HandleResource` för att ge Aspose ett nytt `MemoryStream` för den primära HTML‑utmatningen. För länkade tillgångar kommer vi senare att koppla in `ResourceSaving`.

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using System.IO;

/// <summary>
/// Supplies a stream for every resource the HTML document needs to save.
/// </summary>
class MyHandler : ResourceHandler
{
    /// <summary>
    /// Returns a new stream for the main HTML content.
    /// </summary>
    public override Stream HandleResource(ResourceInfo info)
    {
        // In real life you might return a FileStream or a ZipEntry stream.
        // Here we just hand back a clean MemoryStream.
        return new MemoryStream();
    }
}
```

**Why this matters:** Att returnera ett nytt `MemoryStream` betyder att HTML aldrig rör filsystemet. Detta är grunden för en ren, in‑memory ZIP‑skapelse senare.

## Steg 2: Spara HTML i ett enda MemoryStream

Nu när vi har en hanterare kan vi generera ett HTML‑dokument och fånga det helt i minnet. Detta steg är valfritt om du bara behöver ZIP‑filen, men det illustrerar hur hanteraren fungerar i isolering.

```csharp
using Aspose.Html;

// Sample HTML – replace with your own markup or load from a file.
string htmlContent = "<html><head><title>Demo</title></head><body>Hello world!</body></html>";

// Create the document from a string.
HTMLDocument htmlDocument = new HTMLDocument(htmlContent);

// Instantiate our custom handler.
MyHandler memoryHandler = new MyHandler();

using (MemoryStream htmlStream = new MemoryStream())
{
    // Save triggers HandleResource and writes the HTML into htmlStream.
    htmlDocument.Save(htmlStream, memoryHandler);

    // Reset position for potential reading.
    htmlStream.Position = 0;

    // For demo purposes, dump the HTML to console.
    using (StreamReader reader = new StreamReader(htmlStream))
    {
        Console.WriteLine("Generated HTML:");
        Console.WriteLine(reader.ReadToEnd());
    }
}
```

**Expected output** (formaterad för läsbarhet):

```
Generated HTML:
<html><head><title>Demo</title></head><body>Hello world!</body></html>
```

Om du kör detta kodstycke kommer du att se att HTML bara lever i RAM—inga temporära filer skapas.

## Steg 3: Paketera HTML och resurser i ett ZIP‑arkiv

Nu kommer den saftiga delen: att paketera HTML **och** varje refererad tillgång i en ZIP‑fil utan att någonsin skriva mellanfiler till disk. Vi kommer att använda `System.IO.Compression.ZipArchive` tillsammans med `ResourceSaving`‑händelsen.

```csharp
using Aspose.Html;
using System.IO;
using System.IO.Compression;

// Re‑use the same HTMLDocument from the previous step.
HTMLDocument htmlDocument = new HTMLDocument("<html><body>Hello world!</body></html>");

// Path where the final ZIP will be written.
string zipPath = Path.Combine(Environment.CurrentDirectory, "result.zip");

// Open a FileStream for the ZIP file.
using (FileStream zipFile = new FileStream(zipPath, FileMode.Create))
using (ZipArchive zipArchive = new ZipArchive(zipFile, ZipArchiveMode.Update))
{
    // Create a fresh handler for the ZIP operation.
    MyHandler zipHandler = new MyHandler();

    // Hook the ResourceSaving event – this fires for every resource.
    zipHandler.ResourceSaving += (sender, e) =>
    {
        // Ensure we don't create leading folder entries like "/css/style.css".
        string entryName = e.ResourceInfo.Path.TrimStart('/');

        // Create a new entry inside the ZIP.
        ZipArchiveEntry entry = zipArchive.CreateEntry(entryName);

        // Provide the stream that Aspose will write into.
        e.Stream = entry.Open();
    };

    // Save the document; the handler will fill the ZIP for us.
    htmlDocument.Save(zipHandler);
}

// Verify the ZIP exists.
Console.WriteLine($"ZIP created at: {zipPath}");
```

### Vad händer under huven?

1. **`ResourceSaving` avfyras** för huvud‑HTML‑filen och varje länkad tillgång.
2. Vår lambda skapar ett matchande inlägg (`CreateEntry`) i den öppna ZIP‑filen.
3. Genom att tilldela `e.Stream = entry.Open()` ger vi Aspose en skrivbar ström som skriver direkt in i ZIP‑inlägget.
4. När `htmlDocument.Save` är klar innehåller ZIP‑filen en fullständig HTML‑sida plus eventuell CSS, bilder eller teckensnitt som refereras i markupen.

**Result:** En enda `result.zip`‑fil som du kan leverera till webbläsare, bifoga i e‑post, eller lagra i blob‑lagring—inga temporära filer kvar.

## Bonus: Använda ZIP‑filen i ett Web‑API

Om du bygger en ASP.NET Core‑endpoint som returnerar ZIP‑filen på begäran gäller samma logik. Här är en kompakt controller‑action:

```csharp
[ApiController]
[Route("api/[controller]")]
public class HtmlZipController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult DownloadZip()
    {
        // Build the document (could be loaded from a DB, etc.).
        var html = "<html><body><h1>Dynamic report</h1></body></html>";
        var doc = new HTMLDocument(html);
        var handler = new MyHandler();

        // Prepare an in‑memory ZIP.
        using var zipStream = new MemoryStream();
        using (var archive = new ZipArchive(zipStream, ZipArchiveMode.Create, true))
        {
            handler.ResourceSaving += (s, e) =>
            {
                var entry = archive.CreateEntry(e.ResourceInfo.Path.TrimStart('/'));
                e.Stream = entry.Open();
            };
            doc.Save(handler);
        }

        zipStream.Position = 0;
        return File(zipStream, "application/zip", "report.zip");
    }
}
```

Nu strömmar en GET‑förfrågan till `/api/HtmlZip/download` den genererade zip‑filen direkt till klienten—perfekt för rapporter i farten.

## Vanliga fallgropar & pro‑tips

| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| **Tomma mappar i ZIP** | `ResourceInfo.Path` börjar med `/` vilket skapar ett inlägg som `/` | Använd `TrimStart('/')` som visas i händelsehanteraren. |
| **Saknade bilder** | Bilder som refereras med absoluta URL:er hämtas inte automatiskt | Ställ in `htmlDocument.Options.ResourceLoading = ResourceLoadingMode.Stream` och tillhandahåll en anpassad `ResourceHandler` som laddar ner fjärrtillgångar. |
| **Stora filer orsakar minnespress** | Alla strömmar hålls i minnet tills ZIP‑filen stängs | Byt `ZipArchiveMode.Update` till `Create` och skriv varje inlägg direkt utan buffring, eller ström från disk om storleken överstiger RAM. |
| **Undantag “The stream does not support seeking”** | Försöker återanvända en icke‑sökbar ström för flera resurser | Tillhandahåll alltid ett nytt `MemoryStream` eller `entry.Open()` för varje resurs. |

## Slutsats

Vi har just demonstrerat hur en **custom resource handler** ger dig möjlighet att **convert HTML to ZIP**, **save HTML as ZIP**, och **stream HTML resources** utan att röra filsystemet. Genom att åsidosätta `HandleResource` och utnyttja `ResourceSaving` får du fin‑granulär kontroll över varje byte som lämnar Aspose.HTML.

Mönstret skalar: byt ut den in‑memory `MemoryStream` mot en moln‑blob‑ström, lägg till komprimeringsinställningar, eller anslut ett loggningslager för att auditera vilka tillgångar som paketeras. Himlen är gränsen när du äger resurs‑pipeline:n.

Redo för nästa steg? Prova att bädda in CSS och bilder i din HTML, experimentera med fjärrresurs‑laddning, eller integrera detta flöde i en Azure Function som returnerar en ZIP på begäran. Lycka till med kodandet!

--- 

*Bild som illustrerar flödet av en custom resource handler som omvandlar HTML till en ZIP‑fil.*

![custom resource handler workflow](https://example.com/placeholder-image.png "custom resource handler workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}