---
category: general
date: 2026-03-25
description: Lär dig hur du inaktiverar kantutjämning när du konverterar HTML till
  PNG, så att du får pixelperfekt rendering. Inkluderar steg för att rendera HTML
  som bild, spara HTML som PNG och skapa PNG från HTML.
draft: false
keywords:
- how to disable antialiasing
- convert html to png
- render html as image
- save html as png
- create png from html
language: sv
og_description: Upptäck den steg‑för‑steg‑metod som inaktiverar kantutjämning när
  du konverterar HTML till PNG, så att du får pixelperfekt bildoutput varje gång.
og_title: Hur man inaktiverar kantutjämning vid konvertering av HTML till PNG
tags:
- Aspose.HTML
- C#
- Image Rendering
title: Hur man inaktiverar kantutjämning när man konverterar HTML till PNG
url: /sv/net/generate-jpg-and-png-images/how-to-disable-antialiasing-when-converting-html-to-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man inaktiverar kantutjämning vid konvertering av HTML till PNG

Har du någonsin funderat **hur man inaktiverar kantutjämning** så att din HTML‑till‑PNG‑konvertering ser exakt ut som källkoden? Kanske bygger du en miniatyrgenerator för UI‑komponenter och de suddiga kanterna förstör den visuella kvaliteten. Du är inte ensam—många utvecklare stöter på detta problem när de försöker **konvertera HTML till PNG** för pixel‑perfekta skärmdumpar.

I den här handledningen går vi igenom hela processen för **rendering av HTML som bild**, justerar renderingspipeline för att stänga av kantutjämning, och slutligen **sparar HTML som PNG** med Aspose.HTML för .NET. När du är klar har du ett färdigt kodexempel som skapar en skarp PNG från vilken HTML‑fil som helst, och du förstår varför det är viktigt att inaktivera kantutjämning i vissa designkänsliga scenarier.

## Vad du behöver

Innan vi dyker ner, se till att du har följande förutsättningar:

- **.NET 6.0** eller senare (koden fungerar även på .NET Framework 4.6+).  
- **Aspose.HTML for .NET** NuGet‑paket (`Aspose.HTML`).  
- En enkel `input.html`‑fil som du vill rasterisera.  
- Valfri IDE—Visual Studio, Rider eller till och med VS Code med C#‑tillägget.

Inga extra inhemska bibliotek eller externa verktyg krävs; Aspose.HTML hanterar allt under huven.

## Steg 1: Installera Aspose.HTML

Det första du behöver är Aspose.HTML‑biblioteket. Öppna din terminal (eller Package Manager Console) och kör:

```bash
dotnet add package Aspose.HTML
```

Eller, om du föredrar NuGet‑gränssnittet, sök efter **Aspose.HTML** och klicka på *Install*. Detta paket levereras med en kraftfull renderingsmotor som kan exportera PNG, JPEG, BMP och mer.

> **Proffstips:** Använd den senaste stabila versionen (från och med mars 2026 är det 23.12) för att dra nytta av buggfixar relaterade till bildrendering och kontroller för kantutjämning.

## Steg 2: Ladda HTML‑dokumentet

När paketet är på plats kan du ladda den HTML du vill omvandla. Klassen `HTMLDocument` abstraherar DOM och låter dig manipulera den innan rendering om så behövs.

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Image;

// Path to your source HTML file
string inputPath = Path.Combine(Environment.CurrentDirectory, "input.html");

// Create a new HTMLDocument instance
HTMLDocument htmlDoc = new HTMLDocument(inputPath);
```

> **Varför detta är viktigt:** Att ladda dokumentet först ger dig möjlighet att injicera CSS eller fixa relativa URL:er innan rasteriseringssteget. Det isolerar också renderingen från filsystemet, vilket gör koden enklare att testa.

## Steg 3: Konfigurera ImageSaveOptions och inaktivera kantutjämning

Här kommer kärnan i handledningen: att inaktivera kantutjämning. Aspose.HTML exponerar `ImageRenderingOptions` där du kan växla `UseAntialiasing`. Att sätta den till `false` tvingar motorn att rendera varje pixel exakt som definierat av vektorformerna, vilket ger en **pixel‑perfekt PNG**.

```csharp
// Create ImageSaveOptions for PNG output
ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.Png)
{
    // Attach rendering options
    ImageRenderingOptions = new ImageRenderingOptions
    {
        // Disable antialiasing for a crisp raster image
        UseAntialiasing = false
    }
};
```

### Vad kantutjämning egentligen gör

Kantutjämning mjukar upp kanterna på former genom att blanda färger från närliggande pixlar. Det ser bra ut för fotografier eller komplex grafik, men det kan sudda ut skarpa UI‑element (tänk ikoner eller text i liten storlek). Att inaktivera det säkerställer att varje linje förblir knivskarp—precis vad du behöver när du **skapar PNG från HTML** för UI‑testning eller dokumentation.

## Steg 4: Rendera och spara PNG‑filen

Nu när alternativen är satta, anropa `Save` på `HTMLDocument`. Metoden tar sökvägen för utdata och de tidigare konfigurerade `ImageSaveOptions`.

```csharp
// Destination path for the PNG file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.png");

// Render the HTML and write the PNG file
htmlDoc.Save(outputPath, saveOptions);
```

När du kör koden ovan genereras `output.png` precis bredvid din körbara fil. Öppna den i någon bildvisare—du bör se en skarp, kantutjämningsfri återgivning av `input.html`.

### Förväntat resultat

| Före (Kantutjämning på) | Efter (Kantutjämning av) |
|--------------------------|--------------------------|
| ![Kantutjämnad utskrift](antialiased.png "exempel på hur man inaktiverar kantutjämning med suddiga kanter") | ![Pixel‑perfekt utskrift](pixelperfect.png "exempel på hur man inaktiverar kantutjämning med skarpa kanter") |

*Den vänstra bilden visar standardrenderingen med kantutjämning, medan den högra bilden visar det skarpa resultatet efter att kantutjämning har inaktiverats.*

> **Obs:** Skärmbilderna ovan är platshållare; ersätt dem med dina egna filer när du publicerar.

## Steg 5: Verifiera resultatet programatiskt (valfritt)

Om du behöver säkerställa att PNG‑filen uppfyller vissa kriterier (t.ex. exakt dimension eller färgdjup) kan du inspektera den med `System.Drawing` eller `SixLabors.ImageSharp`. Här är en snabb kontroll med `ImageSharp`:

```csharp
using SixLabors.ImageSharp;
using SixLabors.ImageSharp.PixelFormats;

using (Image<Rgba32> img = Image.Load<Rgba32>(outputPath))
{
    Console.WriteLine($"Width: {img.Width}px, Height: {img.Height}px");
    // Verify that the image has no blended pixels (simple heuristic)
    // You could compare a few pixel values against expected RGBA values.
}
```

Detta extra steg är praktiskt när du automatiserar PNG‑generering i en CI‑pipeline och måste garantera konsekvens.

## Edge Cases & Vanliga frågor

### Vad händer om min HTML använder externa resurser?

Om HTML:n refererar till CSS, typsnitt eller bilder via relativa URL:er, se till att `HTMLDocument`‑bas‑URL pekar på mappen som innehåller dessa resurser:

```csharp
HTMLDocument htmlDoc = new HTMLDocument(inputPath, new Uri("file:///" + Path.GetDirectoryName(inputPath) + "/"));
```

### Kan jag ändra DPI eller bildstorlek?

Absolut. `ImageRenderingOptions` låter dig också sätta `Resolution` (dots per inch) samt `Width`/`Height`:

```csharp
saveOptions.ImageRenderingOptions.Resolution = 300; // High‑resolution PNG
saveOptions.ImageRenderingOptions.Width = 800;      // Desired pixel width
saveOptions.ImageRenderingOptions.Height = 600;     // Desired pixel height
```

Kom bara ihåg att en ökning av DPI utan att skala viewporten kan ge en större fil med samma visuella storlek.

### Påverkar inaktiverad kantutjämning läsbarheten för text?

För de flesta moderna typsnitt kan avstängd kantutjämning göra liten text hackig. Om du behöver både skarp text **och** mjuka kanter, överväg att rendera i högre upplösning och sedan nedskala med en högkvalitativ omprovningsalgoritm. Det tricket bevarar läsbarheten samtidigt som du behåller kontrollen över det slutliga pixelgittret.

### Är detta tillvägagångssätt plattformsoberoende?

Ja. Aspose.HTML är ren .NET och körs på Windows, Linux och macOS. Det enda plattforms‑specifika som kan påverka är tillgängligheten av systemtypsnitt; du kan behöva bädda in egna typsnitt i din HTML eller installera dem på målmaskinen.

## Fullt fungerande exempel

Nedan följer det kompletta, självständiga programmet som du kan kopiera och klistra in i en konsolapplikation. Det innehåller alla nödvändiga `using`‑satser, felhantering och kommentarer.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering.Image;

namespace HtmlToPngDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // -------------------------------------------------
                // 1️⃣ Define input and output paths
                // -------------------------------------------------
                string inputHtml = Path.Combine(Environment.CurrentDirectory, "input.html");
                string outputPng = Path.Combine(Environment.CurrentDirectory, "output.png");

                // -------------------------------------------------
                // 2️⃣ Load the HTML document
                // -------------------------------------------------
                // BaseUri ensures relative resources resolve correctly
                var htmlDoc = new HTMLDocument(inputHtml, new Uri("file:///" + Path.GetDirectoryName(inputHtml) + "/"));

                // -------------------------------------------------
                // 3️⃣ Configure rendering options – disable antialiasing
                // -------------------------------------------------
                var saveOptions = new ImageSaveOptions(SaveFormat.Png)
                {
                    ImageRenderingOptions = new ImageRenderingOptions
                    {
                        UseAntialiasing = false,   // 👈 The key line for pixel‑perfect output
                        // Optional: set resolution or size here
                    }
                };

                // -------------------------------------------------
                // 4️⃣ Render and save the PNG
                // -------------------------------------------------
                htmlDoc.Save(outputPng, saveOptions);
                Console.WriteLine($"✅ PNG created at: {outputPng}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
            }
        }
    }
}
```

Kör programmet så kommer **output.png** att dyka upp bredvid den körbara filen. Öppna den—inga suddiga kanter, bara en ren rasterkopia av din HTML.

## Slutsats

Vi har gått igenom **hur man inaktiverar kantutjämning** när du **konverterar HTML till PNG**, steg för steg genom varje konfigurationsinställning, och levererat ett komplett, körbart exempel som **renderar HTML som bild**, **sparar HTML som PNG**, och låter dig **skapa PNG från HTML** med pixel‑perfekt noggrannhet.  

Om du vill gå längre, experimentera med olika bildformat (JPEG, BMP), utforska vektor‑till‑raster‑skalningstricks, eller integrera detta kodexempel i en webbtjänst som genererar miniatyrer i realtid. Samma principer gäller oavsett om du bygger en dokumentationsgenerator, ett verktyg för visuell regressions‑testning eller en dynamisk diagramexportör.

Har du fler frågor om renderingsdetaljer eller Aspose.HTML‑funktioner? Lämna en kommentar nedan, och lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}