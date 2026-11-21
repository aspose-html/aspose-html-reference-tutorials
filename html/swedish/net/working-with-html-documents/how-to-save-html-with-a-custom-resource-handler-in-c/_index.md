---
category: general
date: 2026-11-20
description: Lär dig hur du sparar HTML med en anpassad ResourceHandler i C# och även
  sparar HTML till zip‑arkiv med koncis, produktionsklar kod.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save html
- save html to zip
- custom ResourceHandler C#
- HtmlAgilityPack save example
- stream based HTML export
language: sv
lastmod: 2026-11-20
og_description: Hur man sparar HTML med en anpassad ResourceHandler i C# och valfritt
  sparar HTML till zip‑filer – komplett, körbar guide för .NET‑utvecklare.
og_image_alt: Diagram showing how to save HTML with a custom ResourceHandler and zip
  the output
og_title: Hur man sparar HTML med en anpassad resurs‑hanterare i C#
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
title: Hur man sparar HTML med en anpassad resurshanterare i C#
url: /sv/net/working-with-html-documents/how-to-save-html-with-a-custom-resource-handler-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så sparar du HTML med en anpassad resurs‑hanterare i C#

Om du behöver veta **hur man sparar HTML** från en sträng i minnet eller ett parsat dokument, visar den här guiden en komplett lösning. Genom att använda en anpassad `ResourceHandler` kan du kontrollera destinationsströmmen, vilket betyder att du kan **spara HTML till zip**‑arkiv utan att skriva temporära filer.

Du kommer att se varför en `ResourceHandler` föredras framför den äldre `IOutputStorage`‑metoden, hur du konfigurerar den och hur du utökar den för zip‑komprimering. I slutet av den här tutorialen kan du bädda in koden i vilket .NET 6+‑projekt som helst och anpassa den efter dina egna lagringskrav.

## Vad du kommer att bygga

* En minimal `ResourceHandler` som returnerar en `MemoryStream`.
* Ett `HtmlDocument` skapat med **HtmlAgilityPack**.
* Ett anrop till `doc.Save` som skriver HTML till strömmen som tillhandahålls av hanteraren.
* En valfri wrapper som komprimerar den resulterande HTML‑filen till ett zip‑arkiv.

Förutsättningar:

* .NET 6 SDK eller senare.
* `HtmlAgilityPack` NuGet‑paket (`dotnet add package HtmlAgilityPack`).
* Grundläggande kunskap om C#‑strömmar.

## Steg 1: Skapa en anpassad resurs‑hanterare (primärt sätt att **how to save html**)

`ResourceHandler`‑basisklassen (tillgänglig från version 24.2 av viewer‑SDK‑et) definierar en enda abstrakt metod, `HandleResource`. Genom att implementera denna metod får du full kontroll över var HTML‑en skrivs.

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

**Varför detta är viktigt:** Genom att returnera en `MemoryStream` undviker du disk‑I/O, minskar latens och håller koden deterministisk för enhetstester. Hanteraren anropas automatiskt av `Save`‑metoden, så du behöver aldrig skicka en ström explicit.

## Steg 2: Ladda eller bygga HTML‑dokumentet

`HtmlAgilityPack` tillhandahåller en bekväm `HtmlDocument`‑klass som kan parsas från en sträng, en fil eller en ström. I det här exemplet laddar vi en enkel literal, men samma kod fungerar med vilken HTML‑källa som helst.

```csharp
using HtmlAgilityPack;

/// <summary>
/// Builds a basic HTML document in memory. Replace the string with your own markup
/// or load it from an external source.
/// </summary>
HtmlDocument doc = new HtmlDocument();
doc.LoadHtml("<html><body>Hello World</body></html>");
```

**Varför detta är viktigt:** Att hålla dokumentet i minnet stämmer överens med den ström‑baserade metoden för den anpassade hanteraren. Det låter dig också manipulera DOM‑en innan du sparar, till exempel injicera skript eller rätta till felaktiga taggar.

## Steg 3: Spara dokumentet med den anpassade hanteraren

Att anropa `doc.Save` med en instans av `MyHandler` triggar `HandleResource`‑metoden. HTML‑en skrivs direkt till den ström du returnerade.

```csharp
// Save the HTML; the handler provides the output stream.
doc.Save(new MyHandler());
```

När `Save` är klar innehåller `MemoryStream`‑en i `MyHandler` den serialiserade HTML‑en. Du kan hämta den så här:

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

**Resultat:** Konsolen skriver ut exakt den HTML du skickade till `LoadHtml`. Detta bevisar att du nu förstår **how to save HTML** med en anpassad hanterare.

## Steg 4: Utöka hanteraren för att **save HTML to zip**

Om du vill arkivera HTML‑en, ändra `MyHandler` så att den skriver till en `ZipArchiveEntry`. .NET‑namnutrymmet `System.IO.Compression` gör detta enkelt.

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

Använd nu den nya hanteraren:

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

**Varför detta fungerar:** `HandleResource`‑metoden skapar ett zip‑entry med namnet `document.html`. När `doc.Save` skriver till den returnerade strömmen komprimeras data automatiskt. Eftersom zip‑filen byggs i minnet kan du returnera den från ett web‑API, bifoga den i ett e‑mail eller lagra den i en databas utan att röra filsystemet.

## Vanliga frågor och kantfall

### Vad händer om jag behöver flera HTML‑filer i samma zip?

Skapa ett nytt entry för varje anrop till `HandleResource`. Argumentet `resourceName` innehåller vanligtvis filnamnet, så du kan använda det direkt:

```csharp
public override Stream HandleResource(string resourceName)
{
    var entry = _archive.CreateEntry(resourceName, CompressionLevel.Optimal);
    return entry.Open();
}
```

### Hur hanterar man stora dokument utan att tömma minnet?

Byt ut `MemoryStream` mot en `FileStream` som pekar på en temporär fil. Hanteraren returnerar då filströmmen, och du kan senare ta bort filen efter att zip‑filen har skapats.

### Fungerar detta tillvägagångssätt med .NET Core på Linux?

Ja. Alla använda API:er (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) är plattformsoberoende. Se till att mål‑ramverket är minst .NET 6 för bästa kompatibilitet.

### Kan jag kryptera zip‑arkivet?

`ZipArchive` stödjer lösenords‑baserad kryptering endast via tredjeparts‑bibliotek (t.ex. `SharpZipLib`). Om kryptering krävs, omslut utdata‑bytena med ett bibliotek som tillhandahåller AES‑kryptering innan du skickar dem till klienten.

## Pro‑tips

* **Återanvänd hanteraren** när du bearbetar många dokument i ett batch‑läge; att skapa ett nytt `ZipArchive` för varje fil ger onödig overhead.
* **Sätt `LeaveOpen: true`** på `ZipArchive`‑konstruktorn om du behöver läsa zip‑bytena medan arkivet fortfarande är öppet.
* **Validera HTML** innan du sparar genom att anropa `doc.OptionCheckSyntax = true;` – detta fångar felaktiga taggar tidigt.
* **Logga storleken** på den genererade zip‑filen; onormalt stora utdata indikerar ofta duplicerade resurser eller saknad komprimering.

## Fullt fungerande exempel

Nedan är en enda fil som du kan klistra in i ett konsolprojekt (`dotnet new console`) och köra. Den demonstrerar både enkel HTML‑sparning och zip‑komprimering.



## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man sparar HTML i C# med anpassad resurs‑hanterare](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [Hur man använder ZipArchive – Spara HTML och resurser till en ZIP‑fil](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [spara html som zip med en anpassad resurs‑hanterare – steg‑för‑steg‑guide](/html/english/net/html-extensions-and-conversions/save-html-as-zip-with-a-custom-resource-handler-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}