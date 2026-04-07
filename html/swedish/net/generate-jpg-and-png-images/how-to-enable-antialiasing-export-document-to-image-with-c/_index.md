---
category: general
date: 2026-04-06
description: Lär dig hur du aktiverar kantutjämning, ställer in bildens bredd och
  höjd samt sparar dokumentet som PNG i C# – en snabb guide för att exportera dokument
  till bild.
draft: false
keywords:
- how to enable antialiasing
- save document as png
- set image width
- set image height
- export document to image
language: sv
og_description: Hur du aktiverar kantutjämning när du exporterar ett dokument till
  en bild. Den här guiden visar hur du ställer in bildens bredd, bildens höjd och
  sparar dokumentet som PNG.
og_title: Hur man aktiverar kantutjämning – Exportera dokument till bild
tags:
- C#
- ImageRendering
- Antialiasing
title: Hur man aktiverar kantutjämning – Exportera dokument till bild med C#
url: /sv/net/generate-jpg-and-png-images/how-to-enable-antialiasing-export-document-to-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man aktiverar kantutjämning – Exportera dokument till bild i C#

Har du någonsin undrat **hur man aktiverar kantutjämning** när du omvandlar ett dokument till en bild? Kanske provade du ett snabbt `Save`‑anrop och resultatet såg hackigt ut, särskilt på diagonala linjer. Den goda nyheten är att du inte behöver vara en grafikexpert—bara några rader C# och rätt alternativ.

I den här handledningen går vi igenom hur man ställer in bildens bredd, bildens höjd och slutligen **sparar dokument som PNG** så att du kan **exportera dokument till bild** med mjuka kanter. I slutet har du ett färdigt kodexempel som producerar en skarp 800 × 600 PNG med kantutjämning aktiverad.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar även på .NET Framework 4.7+)
- En referens till ett renderingsbibliotek som stöder `ImageRenderingOptions` (t.ex. Aspose.Words, Syncfusion, eller något API som exponerar liknande egenskaper)
- En grundläggande förståelse för C#‑syntax  

Ingen tung installation—lägg bara till NuGet‑paketet så är du redo att köra.

## Steg 1: Installera renderingsbiblioteket

Först, hämta paketet till ditt projekt. Om du använder Aspose.Words, kör:

```bash
dotnet add package Aspose.Words
```

> **Proffstips:** Håll biblioteksversionen uppdaterad; den senaste releasen (från april 2026) innehåller prestandaförbättringar för kantutjämning.

## Steg 2: Skapa dokumentobjektet

Läs in eller skapa dokumentet du vill rendera. Här är ett minimalt exempel som bygger ett en‑sidigt dokument med ett enkelt stycke:

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Create a new blank document
Document doc = new Document();

// Add a paragraph with some text
Paragraph para = new Paragraph(doc);
Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
para.AppendChild(run);
doc.FirstSection.Body.AppendChild(para);
```

`Document`‑klassen är ingångspunkten; allt du renderar kommer från den. I riktiga projekt skulle du förmodligen läsa in ett befintligt .docx:

```csharp
// Document doc = new Document("input.docx");
```

## Steg 3: Definiera renderingsalternativ (Bredd, Höjd, Kantutjämning)

Nu svarar vi på huvudfrågan: **hur man aktiverar kantutjämning**. `ImageRenderingOptions`‑objektet låter dig slå på jämning och kontrollera dimensioner.

```csharp
// Step 3: Define rendering options (size and antialiasing)
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Set the desired output size
    Width = 800,               // set image width
    Height = 600,              // set image height

    // Turn on antialiasing for smoother edges
    UseAntialiasing = true
};
```

Lägg märke till kommentarerna: de nämner uttryckligen **set image width**, **set image height** och **UseAntialiasing**—de tre reglagen som betyder mest när du vill ha en polerad PNG.

### Varför kantutjämning är viktigt

Utan kantutjämning ser diagonala linjer och kurvor trappstegsliknande ut eftersom renderaren behandlar varje pixel som antingen på eller av. När du aktiverar den blandas kantpixelerna, vilket ger en visuell mjukning som efterliknar vad du skulle se i en fotoeditor. Nackdelen är en liten ökning av bearbetningstiden, men för de flesta UI‑orienterade exporterna är den försumbar.

## Steg 4: Spara dokument som PNG (Exportera dokument till bild)

Med alternativen klara sparar vi slutligen **dokument som PNG**. `Save`‑metoden tar filvägen och de alternativ vi just konfigurerat.

```csharp
// Step 4: Render the document to a PNG file using the configured options
doc.Save("output.png", imageOptions);
```

Klart—ditt dokument är nu en 800 × 600 PNG med kantutjämning applicerad. Om du öppnar `output.png` ser du ren text, mjuka linjer och inga hackiga artefakter.

### Verifiera resultatet

Du kan snabbt kontrollera filen i någon bildvisare. Leta efter:

- Korrekt dimension (800 × 600)
- Inga synliga trappstegskanter på texten eller någon form
- En transparent bakgrund om ditt dokument inte innehöll en bakgrundsfärg (de flesta bibliotek använder vitt som standard)

Om bilden ser hackig ut, dubbelkolla att `UseAntialiasing = true` inte blir överskriven någon annanstans.

## Steg 5: Specialfall och variationer

### Ändra utdataformatet

Vill du ha en JPEG istället för PNG? Ändra bara filändelsen och justera eventuellt komprimeringen:

```csharp
imageOptions.JpegQuality = 90; // only works for JPEG output
doc.Save("output.jpg", imageOptions);
```

### Exportera flera sidor

När källdokumentet har flera sidor skapar renderaren som standard separata bildfiler per sida. Du kan loopa igenom sidorna:

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string fileName = $"page_{i + 1}.png";
    doc.Save(fileName, imageOptions);
}
```

### Spara till en ström (t.ex. HTTP‑svar)

Om du bygger ett webb‑API kanske du vill returnera PNG‑filen direkt:

```csharp
using (MemoryStream ms = new MemoryStream())
{
    doc.Save(ms, imageOptions);
    ms.Position = 0;
    // Return ms as FileResult in ASP.NET Core
}
```

## Fullt fungerande exempel

Nedan är det kompletta, kopiera‑och‑klistra‑klara programmet som innehåller alla steg som diskuterats:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;

class Program
{
    static void Main()
    {
        // 1️⃣ Create or load a document
        Document doc = new Document();
        Paragraph para = new Paragraph(doc);
        Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
        para.AppendChild(run);
        doc.FirstSection.Body.AppendChild(para);

        // 2️⃣ Define rendering options (size and antialiasing)
        ImageRenderingOptions imageOptions = new ImageRenderingOptions
        {
            Width = 800,               // set image width
            Height = 600,              // set image height
            UseAntialiasing = true     // how to enable antialiasing
        };

        // 3️⃣ Export document to image (save document as PNG)
        doc.Save("output.png", imageOptions);

        Console.WriteLine("Image saved as output.png with antialiasing enabled.");
    }
}
```

När du kör detta program skapas `output.png` i programmets mapp. Öppna den så ser du en mjuk, 800 × 600 PNG—precis det vi ville uppnå.

## Vanliga frågor & felsökning

- **Vad händer om bilden ser suddig ut?**  
  Suddighet kan uppstå när du skalar upp en liten källsida. Håll källsidans storlek nära mål‑dimensionerna, eller öka DPI via `imageOptions.Resolution` (t.ex. `Resolution = 300`).

- **Fungerar detta på .NET Framework?**  
  Ja. samma API finns i den klassiska ramverket; bara referera till rätt DLL.

- **Kan jag styra bakgrundsfärgen?**  
  Absolut. Sätt `imageOptions.BackgroundColor = System.Drawing.Color.Transparent;` innan du sparar.

- **Är kantutjämning hårdvaruaccelererad?**  
  De flesta bibliotek utför mjukvarukantutjämning. Om du behöver GPU‑acceleration, leta efter en renderingsmotor som uttryckligen stödjer det.

## Slutsats

Vi har gått igenom **hur man aktiverar kantutjämning** när du **exporterar dokument till bild**, gått igenom **set image width** och **set image height**, och visat dig de exakta stegen för att **spara dokument som PNG**. Kodexemplet ovan är redo för produktion, och du kan nu anpassa det till JPEG, flersidiga PDF‑filer eller till och med strömma bilden direkt till en klient.

Nästa steg kan vara att utforska att lägga till vattenstämplar, justera DPI för utskriftskvalitet, eller integrera denna logik i en ASP.NET Core‑endpoint. Samma principer gäller—byt bara filvägen mot en svarström.

Lycka till med kodningen, och njut av de skarpa, kantutjämnade bilderna! 

![Renderad PNG med kantutjämning aktiverad](output.png "Renderad PNG med kantutjämning aktiverad")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}