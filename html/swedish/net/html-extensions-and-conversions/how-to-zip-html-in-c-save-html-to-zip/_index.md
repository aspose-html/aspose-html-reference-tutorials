---
category: general
date: 2025-12-29
description: Hur man snabbt zippar HTML i C# med Aspose.HTML – spara HTML till zip
  med en anpassad ZipResourceHandler. Lär dig steg för steg.
draft: false
keywords:
- how to zip html
- save html to zip
- create zip archive c#
- Aspose HTML zip
- C# resource handling
language: sv
og_description: Hur man snabbt zippar HTML i C# med Aspose.HTML. Följ den här guiden
  för att spara HTML till zip och skapa ett zip‑arkiv med anpassad resurs‑hantering.
og_title: Hur man zippar HTML i C# – Spara HTML i zip
tags:
- C#
- Aspose.HTML
- ZipArchive
- File I/O
title: Hur man zippar HTML i C# – Spara HTML till zip
url: /sv/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så zippar du HTML i C# – Spara HTML till zip

Att zipa HTML i C# är ett vanligt behov när du vill paketera webbsidor för offline‑användning. Oavsett om du samlar en enskild sida med dess bilder eller exporterar en hel webbplats, **spara HTML till zip** håller allt prydligt och portabelt. I den här handledningen går vi igenom en komplett, färdig‑körbar lösning som inte bara zippar HTML‑markupen utan också strömmar varje refererad resurs direkt in i arkivet.

Du kommer att lära dig hur du:

* Skapar ett zip‑arkiv programatiskt med .NET:s `System.IO.Compression`.
* Ansluter en anpassad `ResourceHandler` till Aspose.HTML så att resurser flödar direkt in i zip‑filen.
* Hanterar kantfall som befintliga zip‑filer och stora binära tillgångar.

Inga externa verktyg behövs – bara C#, Aspose.HTML och några rader kod.

## Vad du behöver

Innan vi dyker ner, se till att du har:

* **.NET 6+** (koden fungerar även på .NET Framework 4.6.2 och senare).
* **Aspose.HTML for .NET** – du kan hämta en gratis provversion från Aspose‑webbplatsen eller använda en licensierad kopia.
* En utvecklingsmiljö (Visual Studio, VS Code, Rider – vad du föredrar).

Det är allt. Inga extra NuGet‑paket förutom `System.IO.Compression` (ingår i .NET) och `Aspose.HTML`.

## Steg 1: Ställ in projektet och importerna

Skapa ett nytt konsolprojekt (eller lägg in koden i ett befintligt). Lägg till de nödvändiga `using`‑direktiven högst upp i din fil:

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;
```

> **Proffstips:** Om du använder Visual Studio kommer IDE:n föreslå att lägga till det saknade NuGet‑paketet för `Aspose.Html`. Acceptera det, så är du redo att köra.

## Steg 2: Implementera en anpassad ZipResourceHandler

Aspose.HTML anropar en `ResourceHandler` när den behöver skriva en resurs (t.ex. en bild, CSS‑fil eller skript). Genom att överskugga `HandleResource` kan vi bestämma exakt var varje resurs hamnar. Handlaren nedan skapar ett zip‑poster som speglar resursens logiska sökväg och returnerar en skrivbar ström som pekar direkt på den posten.

```csharp
/// <summary>
/// Streams each HTML resource straight into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;

    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // Ensure the entry's directory structure exists inside the zip.
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        // The returned stream writes directly into the zip entry.
        return entry.Open();
    }
}
```

**Varför detta är viktigt:**  
Istället för att skriva resurser till en temporär mapp och sedan zippa mappen, strömmar den här handlaren data i farten, sparar disk‑I/O och håller minnesanvändningen låg. Den garanterar också att zip‑filens interna mappstruktur matchar HTML‑filens relativa sökvägar, vilket webbläsare förväntar sig när du packar upp och öppnar sidan.

## Steg 3: Förbered zip‑arkivet

Nu öppnar (eller skapar) vi mål‑zip‑filen. Flaggan `FileMode.Create` skriver över eventuell befintlig fil – perfekt för repeterbara byggen. Om du föredrar att bevara ett existerande arkiv, byt till `FileMode.OpenOrCreate` och hantera dubblettposter därefter.

```csharp
string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");

// Ensure the directory exists (useful if you run the code from a nested folder)
Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);

using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);
```

> **Kantfall:** Om processen kraschar innan `using`‑blocket disponerar arkivet kan du få en korrupt zip‑fil. Att köra koden i ett try/catch‑block och ta bort den delvis skapade filen vid fel är ett enkelt skydd.

## Steg 4: Bygg HTML‑dokumentet med en inbäddad resurs

För demonstration skapar vi en liten HTML‑sida som refererar en bild som heter `image.png`. I ett riktigt scenario laddar du HTML från en fil eller en sträng från en databas.

```csharp
// Sample HTML containing an <img> tag.
// Aspose.HTML will ask the ResourceHandler for "image.png".
string htmlContent = @"
<html>
<head><title>Sample Zip</title></head>
<body>
    <h1>Hello, zipped world!</h1>
    <img src='image.png' alt='Demo image'>
</body>
</html>";

// Create the document from the string.
var html = new HTMLDocument(htmlContent);
```

Om du har faktiska bildfiler på disk kan du lägga till dem i zip‑filen manuellt innan du sparar HTML, eller låta Aspose.HTML hämta dem via handlaren (t.ex. från en URL). Handlaren vi skrev fungerar för både lokala sökvägar och fjärr‑URL:er.

## Steg 5: Konfigurera sparalternativ för att använda ZipResourceHandler

Vi talar nu om för Aspose.HTML att använda vår anpassade handler när den skriver ut resurser. Klassen `HTMLSaveOptions` låter dig också ange filnamnet inuti zip‑filen (standard är `index.html`).

```csharp
var saveOptions = new HTMLSaveOptions
{
    // The HTML file itself will be saved as "index.html" inside the zip.
    OutputFileName = "index.html",
    // Plug in our handler so resources go straight into the archive.
    OutputStorage = new ZipResourceHandler(zip)
};
```

## Steg 6: Spara dokumentet – allt strömmar in i zip‑filen

Till sist anropar vi `Save`. Aspose.HTML analyserar markupen, hittar `<img>`‑taggen, anropar `HandleResource` för `image.png` och skriver både HTML‑filen och bilden in i samma zip‑arkiv.

```csharp
html.Save(saveOptions);
Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
```

När `using`‑blocken avslutas finaliseras `ZipArchive`‑filen och blir klar för distribution.

### Fullt fungerande exempel

Nedan är hela programmet sammansatt. Kopiera‑klistra in det i `Program.cs` och kör – inga ytterligare ändringar behövs.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;
    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare the zip file.
        string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");
        Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);
        using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
        using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);

        // 2️⃣ Build a simple HTML document with an image reference.
        string htmlContent = @"
        <html>
        <head><title>Sample Zip</title></head>
        <body>
            <h1>Hello, zipped world!</h1>
            <img src='image.png' alt='Demo image'>
        </body>
        </html>";
        var html = new HTMLDocument(htmlContent);

        // 3️⃣ Set save options to stream resources into the zip.
        var saveOptions = new HTMLSaveOptions
        {
            OutputFileName = "index.html",
            OutputStorage = new ZipResourceHandler(zip)
        };

        // 4️⃣ Save – everything ends up in output.zip.
        html.Save(saveOptions);
        Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
    }
}
```

**Förväntat resultat:** Efter körning innehåller `output.zip` två poster:

```
index.html
image.png
```

Om du packar upp filen och öppnar `index.html` i en webbläsare visas bilden korrekt eftersom den relativa sökvägen bevaras.

## Vanliga frågor

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}