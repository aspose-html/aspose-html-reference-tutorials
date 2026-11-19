---
category: general
date: 2026-02-27
description: Spara HTML som ZIP i C# med en anpassad resurs‑hanterare och skapa ZIP‑arkiv
  i C#. Följ den här steg‑för‑steg‑handledningen för att paketera HTML och dess resurser.
draft: false
keywords:
- save html as zip
- custom resource handler
- create zip archive in c#
language: sv
og_description: Spara HTML som ZIP i C# med en anpassad resurs‑hanterare. Lär dig
  hur du skapar ZIP‑arkiv i C# och enkelt bäddar in resurser.
og_title: Spara HTML som ZIP i C# – Fullständig handledning
tags:
- Aspose.HTML
- C#
- ZIP
title: Spara HTML som ZIP i C# – Komplett guide med anpassad resurshanterare
url: /sv/net/working-with-html-documents/save-html-as-zip-in-c-complete-guide-with-custom-resource-ha/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Spara HTML som ZIP i C# – Komplett guide med anpassad resurshanterare

Har du någonsin undrat hur du **sparar HTML som ZIP** i C# utan att rycka ur dig håret? Du är inte ensam—många utvecklare stöter på problem när de måste leverera en HTML‑sida tillsammans med bilder, CSS‑ eller JavaScript‑filer. Den goda nyheten? Med Aspose.HTML kan du göra det i några enkla steg, och en **custom resource handler** gör processen smärtfri.

I den här handledningen går vi igenom allt du behöver veta: från att installera biblioteket, skriva en hanterare som strömmar resurser direkt in i ett **create ZIP archive in C#**, till att verifiera det slutgiltiga paketet. I slutet har du en färdig lösning som du kan lägga till i vilket .NET‑projekt som helst.

![Save HTML as ZIP example](/images/save-html-as-zip.png "Diagram showing HTML saved as a ZIP file")

## Spara HTML som ZIP – Vad den här guiden täcker

Vi kommer att täcka hela pipeline:n:

1. **Prerequisites** – de minsta verktygen och paket du behöver.  
2. **Custom resource handler** – varför du behöver en och hur du implementerar den.  
3. **Creating a ZIP archive in C#** – med `System.IO.Compression`.  
4. **Configuring Aspose.HTML save options** för att peka på hanteraren.  
5. **Running the code** och kontrollera resultatet.  

Om du är bekväm med grundläggande C#‑syntax och har Visual Studio (eller VS Code) installerat, är du redo att dyka in. Ingen extern dokumentation behövs—allt finns här.

---

## Steg 1: Ställ in projektet och installera Aspose.HTML

Innan vi skriver någon kod, se till att ditt projekt kan referera till Aspose.HTML‑biblioteket.

```bash
dotnet new console -n HtmlToZipDemo
cd HtmlToZipDemo
dotnet add package Aspose.HTML
```

*Pro tip:* Det senaste NuGet‑paketet (från februari 2026) riktar sig mot .NET 6+, så du kan använda det moderna SDK‑stilsprojektet utan att oroa dig för äldre ramverk.

När paketet har återställts, öppna `Program.cs`. Vi kommer att ersätta standardinnehållet med hela exemplet senare, men håll filen öppen för tillfället.

## Implementera en Custom Resource Handler

### Varför en Custom Resource Handler?

När Aspose.HTML sparar ett HTML‑dokument som ett ZIP‑paket, måste det hämta varje extern resurs (bilder, typsnitt, skript) och skriva dem någonstans. Standardbeteendet skriver dem till en temporär mapp på disken. Genom att tillhandahålla en **custom resource handler** talar du om för biblioteket exakt var varje resurs ska placeras—i vårt fall, direkt i ZIP‑arkivet. Detta undviker extra I/O, håller allt organiserat och ger dig full kontroll över namngivning.

### Kod: Hanterarklassen

Skapa en ny klassfil som heter `MyHandler.cs` (eller placera den i `Program.cs` om du föredrar en enkel‑fil‑demo).

```csharp
using Aspose.Html;
using Aspose.Html.Saving;
using System.IO;
using System.IO.Compression;

/// <summary>
/// Streams each external resource straight into the supplied ZipArchive.
/// </summary>
class MyHandler : ResourceHandler
{
    // The ZipArchive is supplied via a static field for simplicity.
    // In production code you might inject it through the constructor.
    public static ZipArchive ZipArchive;

    /// <summary>
    /// Called by Aspose.HTML for every external resource.
    /// </summary>
    /// <param name="info">Metadata about the resource (URI, MIME type, etc.).</param>
    /// <returns>A writable stream that Aspose.HTML will fill with the resource data.</returns>
    public override Stream HandleResource(ResourceInfo info)
    {
        // Use the resource URI as the entry name – this mimics the folder structure
        // you would get if you saved the page manually.
        var entry = ZipArchive.CreateEntry(info.Uri);
        // Return the entry's stream so Aspose.HTML can write directly.
        return entry.Open();
    }
}
```

**Förklaring:**  
* `ResourceHandler` är en abstrakt klass från Aspose.HTML som låter dig avbryta resurshämtning.  
* Genom att returnera `Stream` som erhålls från `ZipArchiveEntry.Open()` ger vi biblioteket ett skrivbart rör direkt in i ZIP‑filen. Inga temporära filer, ingen extra städning.

## Skapa ZIP‑arkivet i C#

Nu när hanteraren är klar, behöver vi en plats för den att skriva till. .NET‑klassen `ZipArchive` sköter det tunga arbetet.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare a simple HTML document that references an external image.
        var html = "<html><body><h1>Hello, ZIP!</h1><img src='logo.png' alt='Logo'></body></html>";
        var document = new HTMLDocument(html);

        // 2️⃣ Open a FileStream that will become our .zip file.
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.zip");
        using (var zipStream = new FileStream(outputPath, FileMode.Create))
        using (var zipArchive = new ZipArchive(zipStream, ZipArchiveMode.Update))
        {
            // 3️⃣ Make the archive visible to the custom handler.
            MyHandler.ZipArchive = zipArchive;

            // 4️⃣ Configure save options to use ZIP format and plug in the handler.
            var saveOptions = new HTMLSaveOptions(SaveFormat.ZIP)
            {
                ResourceHandler = new MyHandler()
            };

            // 5️⃣ Save the document. The handler writes the image into the ZIP automatically.
            document.Save(outputPath, saveOptions);
        }

        Console.WriteLine($"✅ HTML saved as ZIP at: {outputPath}");
    }
}
```

### Vad detta gör

1. **Skapar ett HTML‑dokument i minnet** med en referens till `logo.png`.  
2. **Öppnar en `FileStream`** som kommer att bli `output.zip`.  
3. **Tilldelar `ZipArchive`** till det statiska fältet i `MyHandler`.  
4. **Ställer in `HTMLSaveOptions`** till `SaveFormat.ZIP` och bifogar vår hanterare.  
5. **Anropar `document.Save`** – Aspose.HTML analyserar HTML‑koden, hämtar `logo.png` och strömmar den in i arkivet via `MyHandler`.  

Eftersom hanteraren använder resurs‑URI:n (`logo.png`) som postnamn, innehåller den resulterande ZIP‑filen en fil med exakt det namnet, vilket bevarar den ursprungliga relativa sökvägen.

## Konfigurera sparalternativ för ZIP‑paketet

`HTMLSaveOptions`‑objektet är där du talar om för Aspose.HTML **hur** du ska paketera resultatet. Förutom `ResourceHandler` kan du justera några användbara egenskaper:

```csharp
var saveOptions = new HTMLSaveOptions(SaveFormat.ZIP)
{
    // Use a custom folder inside the ZIP if you like:
    // ResourceFolder = "assets",
    ResourceHandler = new MyHandler(),
    // Optional: compress resources (true by default)
    EnableCompression = true
};
```

*Varför bry sig om `EnableCompression`?*  
Om du hanterar stora bilder kan aktivering av komprimering minska den slutgiltiga arkivet med upp till 70 %. För redan komprimerade PNG‑filer är vinsten dock liten, så du kan stänga av den för att snabba upp sparandet.

## Kör koden och verifiera resultatet

Kompilera och kör programmet:

```bash
dotnet run
```

Du bör se ett lyckat meddelande skrivet i konsolen. Navigera till den utskrivna katalogen och öppna `output.zip`. Inuti hittar du:

- `index.html` – den sparade HTML‑filen.  
- `logo.png` – bilden som refererades i markup‑koden.

Öppna `index.html` direkt från ZIP‑filen (de flesta OS‑filutforskare låter dig förhandsgranska den) och du kommer att se rubriken och bilden renderade exakt som i den ursprungliga strängen.

**Särskilda fall att beakta**

| Situation | Vad att göra |
|-----------|--------------|
| HTML‑dokumentet refererar till en **remote URL** (t.ex. `https://example.com/style.css`) | Hanteraren kommer fortfarande att få en `ResourceInfo.Uri`. Se till att din miljö kan nå URL:en, eller för‑ladda resursen och justera HTML‑koden till en lokal sökväg. |
| Du behöver en **folder hierarchy** i ZIP‑filen (t.ex. `images/logo.png`) | Ändra `HandleResource` så att den lägger till ett mappnamn före: `var entry = ZipArchive.CreateEntry($"assets/{info.Uri}");` |
| Resursen **fails to load** (404) | Hanteraren kommer att anropas, men strömmen får noll byte. Omslut sparningsanropet i en `try/catch` och inspektera `info.Status` om du behöver anpassad felhantering. |

## Sammanfattning: Spara HTML som ZIP i ett kompakt flöde

- **Primary Goal:** Packa en HTML‑sida och alla dess externa resurser i en enda ZIP‑fil med C#.  
- **Key Tools:** Aspose.HTML (`HTMLDocument`, `HTMLSaveOptions`), `System.IO.Compression.ZipArchive`, och en **custom resource handler**.  
- **Result:** En portabel `output.zip` som kan skickas, lagras eller överföras över nätverket, och senare extraheras utan att förlora resurssökvägar.

## Vad blir nästa steg? Utöka arbetsflödet

Nu när du har bemästrat **save HTML as ZIP**, kanske du vill utforska relaterade scenarier:

- **Save HTML as PDF** – ersätt `SaveFormat.ZIP` med `SaveFormat.PDF` och justera alternativna därefter.  
- **Embed fonts** – använd `@font-face` i din HTML och låt hanteraren fånga teckensnitts‑filerna.  
- **Batch processing** – iterera över en samling HTML‑strängar, återanvänd samma `ZipArchive` för att skapa ett paket med flera dokument.  

Alla dessa bygger på samma **custom resource handler**‑mönster och **create ZIP archive in C#**‑teknik som du just lärt dig.

### Avslutande tankar

Du har just sett hur enkelt det är att **save HTML as ZIP** i C# när du låter Aspose.HTML

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}