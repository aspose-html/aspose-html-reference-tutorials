---
category: general
date: 2026-03-29
description: Lär dig hur du använder ZipArchive i C# för att konvertera HTML till
  ZIP, spara HTML i ZIP och komprimera HTML‑bilder – allt i en tydlig handledning.
draft: false
keywords:
- how to use ziparchive
- convert html to zip
- save html to zip
- create zip archive c#
- compress html images
language: sv
og_description: Upptäck hur du använder ZipArchive i C# för att konvertera HTML till
  ZIP, spara HTML i ZIP och komprimera HTML‑bilder med ett komplett, körbart exempel.
og_title: Hur man använder ZipArchive – Spara HTML och resurser i en ZIP‑fil
tags:
- C#
- .NET
- Aspose.Html
- ZipArchive
title: Hur man använder ZipArchive – Spara HTML och resurser i en ZIP-fil
url: /sv/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder ZipArchive – Spara HTML och resurser till en ZIP‑fil

Har du någonsin funderat på **hur man använder ZipArchive** för att paketera en HTML‑sida tillsammans med dess bilder, CSS och andra tillgångar? Du är inte ensam. Många utvecklare fastnar när de måste leverera ett självständigt HTML‑paket, särskilt när sidan refererar till externa resurser. Den goda nyheten? Med några rader C# och Aspose.HTML kan du **konvertera HTML till ZIP**, **spara HTML till ZIP** och till och med **komprimera HTML‑bilder** utan att lämna din IDE.

I den här handledningen går vi igenom hela processen – från att skapa ett enkelt `HTMLDocument` till att hantera varje länkad resurs via en anpassad `ResourceHandler`. I slutet har du en färdig‑att‑använda ZIP‑fil som du kan släppa på vilken webbserver som helst eller bifoga i ett e‑postmeddelande. Inga externa skript, ingen manuell kopiering – bara ren .NET.

## Förutsättningar

Innan vi dyker ner, se till att du har:

- **.NET 6+** (eller .NET Framework 4.6+). API:erna som används är en del av `System.IO.Compression`.
- **Aspose.HTML for .NET** installerat (NuGet‑paket `Aspose.Html`).
- En grundläggande förståelse för C#‑syntax.
- En IDE som Visual Studio eller VS Code.

Det är allt. Inga extra verktyg, inga tredjeparts‑zip‑verktyg. Är du redo? Låt oss börja.

## Steg 1: Ställ in projektet och lägg till beroenden

Skapa ett nytt konsolprojekt:

```bash
dotnet new console -n HtmlToZipDemo
cd HtmlToZipDemo
dotnet add package Aspose.Html
```

`Aspose.Html`‑paketet ger oss klassen `HTMLDocument` och basklassen `ResourceHandler` som vi senare kommer att utöka. Det inbyggda `System.IO.Compression`‑namnutrymmet tillhandahåller `ZipArchive` och `ZipArchiveEntry`.

> **Pro tip:** Om du riktar in dig på .NET 6 kan du använda top‑level‑statements för att hålla `Main`‑metoden prydlig. Koden nedan använder en klassisk `Program`‑klass för tydlighet.

## Steg 2: Skapa en anpassad Resource Handler

När Aspose.HTML sparar ett dokument ber den en `ResourceHandler` att tillhandahålla en `Stream` för varje extern fil (bilder, CSS, teckensnitt osv.). Genom att åsidosätta `HandleResource` kan vi leda varje resurs direkt in i ett zip‑objekt.

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

**Varför detta är viktigt:** Istället för att först skriva resurser till disk och sedan zip‑a dem, strömmar hanteraren dem direkt, vilket minskar I/O‑belastning och garanterar att zip‑filen hålls i synk med HTML‑innehållet.

## Steg 3: Bygg HTML‑dokumentet

För demonstration embedder vi ett litet HTML‑snutt som refererar till en extern bild som heter `logo.png`. I ett riktigt projekt kan du läsa in HTML från en fil eller en databas.

```csharp
// Create a simple HTML document with an external image reference.
HTMLDocument htmlDocument = new HTMLDocument(
    "<html><body><h1>Welcome!</h1><img src='logo.png' alt='Demo logo'></body></html>"
);
```

Om du behöver **komprimera HTML‑bilder**, se bara till att bildfilen ligger bredvid den körbara filen (eller embedda den som en resurs). `ZipResourceHandler` lägger automatiskt till bilden i arkivet.

## Steg 4: Öppna (eller skapa) ZIP‑filen och spara

Nu knyter vi ihop allt. Vi öppnar ett `FileStream` för utdata‑zippet, instansierar `ZipArchive` i *Update*-läge och skickar vår anpassade hanterare till `HTMLDocument.Save`.

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

När `using`‑blocken avslutas färdigställs och stängs zip‑filen automatiskt. Den resulterande `output.zip` innehåller:

- `index.html` (det serialiserade HTML‑dokumentet)
- `logo.png` (bilden som refereras i HTML‑dokumentet)

Du kan verifiera innehållet genom att öppna zip‑filen i någon filutforskare.

## Steg 5: Verifiera resultatet (valfritt)

Det är alltid en bra idé att dubbelkolla att zip‑filen faktiskt fungerar. Här är ett snabbt kodsnutt du kan köra efter föregående kod för att lista posterna:

```csharp
using (var zip = ZipFile.OpenRead("output.zip"))
{
    Console.WriteLine("Contents of output.zip:");
    foreach (var entry in zip.Entries)
        Console.WriteLine($"- {entry.FullName} ({entry.Length} bytes)");
}
```

Du bör se något liknande:

```
Contents of output.zip:
- index.html (1234 bytes)
- logo.png (45678 bytes)
```

Öppna `index.html` från den extraherade mappen, så ser du bilden renderad korrekt – ett bevis på att **spara HTML till ZIP** fungerade som avsett.

## Vanliga varianter & kantfall

### 1. Använda ett annat namn för HTML‑filen

Som standard skriver Aspose HTML till `index.html`. Om du behöver ett eget namn kan du sätta `htmlDocument.FileName` innan du sparar:

```csharp
htmlDocument.FileName = "myPage.html";
htmlDocument.Save(zipHandler);
```

### 2. Lägg till ytterligare filer manuellt

Ibland vill du paketera extra filer (t.ex. en README). Du kan lägga till dem direkt i `ZipArchive` innan du anropar `htmlDocument.Save`:

```csharp
var readme = zipArchive.CreateEntry("README.txt", CompressionLevel.Optimal);
using (var writer = new StreamWriter(readme.Open()))
{
    writer.WriteLine("This ZIP contains an HTML page generated with Aspose.HTML.");
}
```

### 3. Hantera stora bilder effektivt

Om ditt HTML refererar till mycket stora bilder, överväg att ändra storlek på dem i förväg för att hålla zip‑storleken rimlig. `System.Drawing.Common`‑paketet kan hjälpa:

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

Peka sedan `<img src='logo_resized.png'>` i ditt HTML.

## Fullt, körbart exempel

Nedan är hela programmet som du kan kopiera‑klistra in i `Program.cs`. Det kompileras och körs som‑det‑är, förutsatt att du har installerat Aspose.HTML NuGet‑paketet.

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

**Förväntad output:** Konsolen skriver ett lyckat meddelande, och `output.zip` dyker upp i projektmappen med `index.html` och `logo.png`.

## Vanliga frågor

- **Fungerar detta på .NET Core?**  
  Ja. `System.IO.Compression.ZipArchive` är en del av .NET Standard, så samma kod körs på .NET 5, .NET 6 och .NET 7.

- **Vad händer om jag behöver **komprimera HTML‑bilder** mer aggressivt?**  
  Du kan förbehandla bilder (ändra storlek, byta format till WebP osv.) innan de läggs till i zip‑filen. Själva hanteraren strömmar bara de data den får.

- **Kan jag kryptera zip‑filen?**  
  `ZipArchive` stödjer AES‑kryptering endast via tredjepartsbibliotek (t.ex. `SharpZipLib`). Om du behöver kryptering, skapa zip‑filen med det biblioteket och mata sedan strömmen till Aspose som en anpassad `ResourceHandler`.

- **Finns det ett sätt att sätta rotmappen i zip‑filen?**  
  Ja – lägg till ett mappnamn före `resourceName` i `HandleResource`, t.ex. `var entry = _zipArchive.CreateEntry($"site/{resourceName}", ...)`.

## Slutsats

Du vet nu **hur man använder ZipArchive** i C# för att **konvertera HTML till ZIP**, **spara HTML till ZIP** och **komprimera HTML‑bilder** i ett enda, rent arbetsflöde. Genom att utöka `ResourceHandler` undvek vi temporära filer och höll processen minnes‑effektiv. Mönstret skalar bra: släpp bara den genererade zip‑filen på en webbserver, e‑posta den eller lagra den i molnlagring.

Nästa steg du kan utforska:

- **Skapa ZIP‑arkiv programatiskt** för hela webbplatsmappar (`create zip archive c#`).
- **Lägg till PDF‑ eller DOCX‑konverteringar** innan zip‑ning för rikare dokumentationspaket.
- **Integrera med ASP.NET Core** för att streama zip‑filen direkt till en klientwebbläsare (`FileStreamResult`).

Har du fler frågor om att zip‑a HTML, hantera teckensnitt eller optimera bildstorlek? Lämna en kommentar eller hör av dig på Stack Overflow. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}