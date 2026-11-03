---
category: general
date: 2026-05-22
description: Ställ in bildens bredd och höjd när du konverterar ett Word‑dokument
  till PNG. Lär dig hur du exporterar docx som bild med högkvalitativ rendering i
  en steg‑för‑steg‑handledning.
draft: false
keywords:
- set image width height
- convert word to png
- save docx as png
- export docx as image
- how to render word
language: sv
og_description: Ställ in bildens bredd och höjd när du konverterar ett Word‑dokument
  till PNG. Denna handledning visar hur du exporterar docx som bild med högkvalitativa
  inställningar.
og_title: Ställ in bildens bredd och höjd vid konvertering av Word till PNG – Komplett
  guide
schemas:
- author: Aspose
  dateModified: '2026-05-22'
  description: Set image width height while converting a Word document to PNG. Learn
    how to export docx as image with high‑quality rendering in a step‑by‑step tutorial.
  headline: Set Image Width Height When Converting Word to PNG – Full Guide
  type: TechArticle
- description: Set image width height while converting a Word document to PNG. Learn
    how to export docx as image with high‑quality rendering in a step‑by‑step tutorial.
  name: Set Image Width Height When Converting Word to PNG – Full Guide
  steps:
  - name: 1. Preserve Transparent Backgrounds
    text: 'If your Word document contains shapes with transparent backgrounds and
      you want to keep that transparency, set the `BackgroundColor` to `Color.Transparent`:'
  - name: 2. Render Only a Specific Range
    text: Sometimes you only need a paragraph or a table, not the whole page. Use
      `DocumentVisitor` to extract the node and render it separately. That’s a more
      advanced scenario, but it shows **how to render word** content at a granular
      level.
  - name: 3. Adjust DPI Dynamically
    text: 'If you need different DPI per page (e.g., high‑resolution for the cover
      page), modify `Resolution` inside the loop:'
  - name: 4. Batch Processing
    text: When converting dozens of documents, wrap the whole flow in a method and
      reuse the same `ImageRenderingOptions` instance. Re‑using the options object
      reduces allocation overhead.
  type: HowTo
tags:
- Aspose.Words
- C#
- Image Rendering
title: Ställ in bildens bredd och höjd vid konvertering från Word till PNG – Fullständig
  guide
url: /sv/net/generate-jpg-and-png-images/set-image-width-height-when-converting-word-to-png-full-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ställ in bildens bredd och höjd vid konvertering av Word till PNG – Komplett guide

Har du någonsin undrat hur du **ställer in bildens bredd och höjd** när du **konverterar Word till PNG**? Du är inte ensam. Många utvecklare stöter på problem när standardexporten ger en suddig bild eller fel dimensioner, och sedan spenderar de timmar på att leta efter en lösning som faktiskt fungerar.

I den här handledningen går vi igenom en ren, end‑to‑end‑lösning som visar **hur man renderar word**‑dokument som PNG‑bilder, så att du kan **spara docx som PNG** med exakt kontroll över bredd‑och‑höjd samt högkvalitativ kantutjämning. I slutet har du ett färdigt kodexempel, en gedigen förståelse för API‑alternativen och några pro‑tips för att undvika vanliga fallgropar.

## Vad du kommer att lära dig

- Läs in en `.docx`‑fil med Aspose.Words för .NET.
- **Ställ in bildens bredd och höjd** med `ImageRenderingOptions`.
- **Exportera docx som bild** (PNG) med antialiasing aktiverat.
- Hur man **konverterar word till png** för en enskild sida eller hela dokumentet.
- Tips för att hantera stora dokument, DPI‑aspekter och filsystemssökvägar.

Inga externa verktyg, ingen rörig kommandorads‑gymnastik—bara ren C#‑kod som du kan klistra in i vilket .NET‑projekt som helst.

---

## Förutsättningar

Innan vi dyker ner, se till att du har följande:

| Krav | Varför det är viktigt |
|------|-----------------------|
| **.NET 6.0+** (or .NET Framework 4.7.2) | Aspose.Words stöder båda, men nyare runtime‑miljöer ger bättre prestanda. |
| **Aspose.Words for .NET** NuGet package (`Install-Package Aspose.Words`) | Tillhandahåller `Document`‑klassen och renderingsmotorn. |
| A **Word document** (`.docx`) you want to turn into a PNG. | Källan du ska konvertera. |
| Basic C# knowledge – you’ll understand `using` statements and object initialization. | Håller inlärningskurvan mjuk. |

Om du saknar NuGet‑paketet, kör detta i Package Manager Console:

```powershell
Install-Package Aspose.Words
```

Det är allt—när paketet är på plats är du redo att börja koda.

---

## Steg 1: Läs in källdokumentet

Det allra första du behöver göra är att peka biblioteket på Word‑filen du vill omvandla.

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Load the .docx file from disk
Document doc = new Document(@"C:\MyFiles\input.docx");
```

**Varför detta är viktigt:** `Document`‑klassen läser in hela Word‑paketet i minnet, vilket ger dig åtkomst till sidor, stilar och allt annat. Om sökvägen är fel får du ett `FileNotFoundException`, så dubbelkolla att filen finns och att sökvägen använder escapade bakåtsnedstreck (`\\`) eller en verbatim‑sträng (`@`).  

> **Pro‑tips:** Omge laddningsanropet med ett `try/catch`‑block om du förväntar dig att filen kan saknas vid körning.

---

## Steg 2: Konfigurera Image Rendering Options (Ställ in bildens bredd och höjd)

Nu kommer kärnan i handledningen: **hur man ställer in bildens bredd och höjd** så att den resulterande PNG‑filen inte blir utdragen eller pixelerad. Klassen `ImageRenderingOptions` ger dig fin‑granulär kontroll över dimensioner, DPI och utjämning.

```csharp
// Create rendering options and explicitly set width and height
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Desired output size in pixels
    Width = 1024,          // Set image width height: 1024px wide
    Height = 768,          // Set image width height: 768px tall

    // High‑quality antialiasing works on Windows, Linux, and macOS
    UseAntialiasing = true,

    // Optional: increase DPI for sharper output (default is 96)
    Resolution = 300
};
```

**Förklaring av de viktigaste egenskaperna:**

- `Width` and `Height` – Detta är de exakta pixel‑dimensionerna du vill ha. Genom att sätta dem **ställer du in bildens bredd och höjd** direkt, och åsidosätter standard sidstorlek.
- `UseAntialiasing` – Aktiverar högkvalitativ utjämning för text och vektorgrafik, vilket är avgörande när du **konverterar word till png** och vill ha skarpa kanter.
- `Resolution` – Högre DPI ger mer detalj, särskilt för komplexa layouter. Håll ett öga på minnesanvändning; en 300 DPI‑bild kan bli stor.

> **Varför inte bara förlita sig på standardstorleken?** Standard använder sidans fysiska dimensioner (t.ex. A4 vid 96 DPI). Det ger ofta en bild på 794 × 1123 pixlar—okej för vissa fall men inte när du behöver en specifik UI‑miniatur eller en förhandsvisning med fast storlek.

---

## Steg 3: Rendera och spara som PNG (Exportera Docx som bild)

När dokumentet är läst in och alternativen konfigurerade kan du äntligen **exportera docx som bild**. Metoden `RenderToImage` gör det tunga arbetet.

```csharp
// Render the first page (page index 0) to a PNG file
doc.RenderToImage(@"C:\MyFiles\output.png", imageOptions);
```

Om du vill rendera **hela dokumentet** (alla sidor) till separata PNG‑filer, loopa över sidkollektionen:

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string outPath = $@"C:\MyFiles\page_{i + 1}.png";
    doc.RenderToImage(outPath, imageOptions, i);
}
```

**Vad händer under huven?** Renderaren rasteriserar varje sida med de dimensioner du angav, tillämpar antialiasing och skriver en PNG‑byte‑ström till disk. Eftersom PNG är förlustfri behåller du hela originallayoutens kvalitet.

**Förväntat resultat:** En skarp PNG‑fil exakt 1024 × 768 pixlar (eller vilken storlek du än har angett). Öppna den i någon bildvisare så ser du Word‑innehållet renderat exakt som det visas i originaldokumentet, men nu som en bitmap‑bild.

---

## Avancerade tips & variationer

### 1. Bevara transparenta bakgrunder

Om ditt Word‑dokument innehåller former med transparent bakgrund och du vill behålla den transparensen, sätt `BackgroundColor` till `Color.Transparent`:

```csharp
imageOptions.BackgroundColor = System.Drawing.Color.Transparent;
```

### 2. Rendera endast ett specifikt område

Ibland behöver du bara ett stycke eller en tabell, inte hela sidan. Använd `DocumentVisitor` för att extrahera noden och rendera den separat. Det är ett mer avancerat scenario, men det visar **hur man renderar word**‑innehåll på en granular nivå.

### 3. Justera DPI dynamiskt

Om du behöver olika DPI per sida (t.ex. högupplöst för framsidan), ändra `Resolution` inuti loopen:

```csharp
if (i == 0) imageOptions.Resolution = 600; // cover page
else imageOptions.Resolution = 300;
```

### 4. Batch‑bearbetning

När du konverterar dussintals dokument, paketera hela flödet i en metod och återanvänd samma `ImageRenderingOptions`‑instans. Återanvändning av options‑objektet minskar allokeringskostnaden.

---

## Vanliga fallgropar & hur man undviker dem

| Symtom | Trolig orsak | Åtgärd |
|--------|--------------|--------|
| PNG är suddig trots hög DPI | `UseAntialiasing` lämnades på false | Sätt `UseAntialiasing = true`. |
| Utdata storlek matchar inte `Width`/`Height` | DPI beaktades inte | Multiplicera önskad storlek med `Resolution / 96` eller justera `Resolution`. |
| Out‑of‑memory‑undantag på stora dokument | Renderar hela dokumentet vid 300 DPI | Rendera en sida åt gången, frigör varje bild efter sparning. |
| PNG visar vit bakgrund på transparenta bilder | `BackgroundColor` är inte satt | Sätt `imageOptions.BackgroundColor = Color.Transparent`. |

---

## Komplett fungerande exempel

Nedan är ett fristående program som du kan kopiera och klistra in i en konsolapp. Det demonstrerar **konvertera word till png**, **spara docx som png**, och naturligtvis **ställa in bildens bredd och höjd**.

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;
using System.Drawing; // For Color

namespace WordToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            string inputPath = @"C:\MyFiles\input.docx";
            Document doc = new Document(inputPath);

            // 2️⃣ Configure rendering options (set image width height)
            ImageRenderingOptions options = new ImageRenderingOptions
            {
                Width = 1024,          // Desired pixel width
                Height = 768,          // Desired pixel height
                UseAntialiasing = true,
                Resolution = 300,
                BackgroundColor = Color.Transparent // Keep transparency if needed
            };

            // 3️⃣ Render the first page to PNG (export docx as image)
            string outputPath = @"C:\MyFiles\output.png";
            doc.RenderToImage(outputPath, options);

            Console.WriteLine($"✅ Document rendered successfully to {outputPath}");
            // Optional: render all pages
            //RenderAllPages(doc, options);
        }

        // Helper method for batch rendering (uncomment if needed)
        static void RenderAllPages(Document doc, ImageRenderingOptions options)
        {
            for (int i = 0; i < doc.PageCount; i++)
            {
                string pagePath = $@"C:\MyFiles\page_{i + 1}.png";
                doc.RenderToImage(pagePath, options, i);
                Console.WriteLine($"Page {i + 1} saved to {pagePath}");
            }
        }
    }
}
```

**Kör det:** Bygg projektet, placera en giltig `input.docx` på den sökväg du angav, och kör. Du bör se en `output.png` exakt **1024 × 768** pixlar, renderad med mjuka kanter.

## Relaterade handledningar

- [Hur man aktiverar antialiasing vid konvertering av DOCX till PNG/JPG](/html/english/net/generate-jpg-and-png-images/how-to-enable-antialiasing-when-converting-docx-to-png-jpg/)
- [konvertera docx till png – skapa zip‑arkiv c#‑handledning](/html/english/net/generate-jpg-and-png-images/convert-docx-to-png-create-zip-archive-c-tutorial/)
- [Hur man använder Aspose för att rendera HTML till PNG – steg‑för‑steg‑guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}