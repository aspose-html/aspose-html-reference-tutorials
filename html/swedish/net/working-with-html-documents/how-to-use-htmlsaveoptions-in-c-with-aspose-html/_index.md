---
category: general
date: 2026-09-10
description: Lär dig hur du använder HtmlSaveOptions i C# för att kontrollera webbteckensnittsstilar
  och spara HTML‑filer med Aspose.HTML. Fullständigt kodexempel och praktiska tips
  ingår.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use htmlsaveoptions
- Aspose HTML library
- WebFontStyle flags
- HTMLDocument conversion
- C# save HTML
- Aspose.Html SaveOptions
language: sv
lastmod: 2026-09-10
og_description: Hur man använder HtmlSaveOptions i C# för att aktivera fet och kursiv
  webbteckensnittsstilar när man sparar HTML med Aspose.HTML. Följ det kompletta exemplet
  och bästa praxis‑tipsen.
og_image_alt: Screenshot showing how to use HtmlSaveOptions to save an HTML file in
  C#
og_title: Hur man använder HtmlSaveOptions i C# med Aspose.HTML – steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: Learn how to use HtmlSaveOptions in C# to control web‑font styles and
    save HTML files with Aspose.HTML. Full code example and practical tips included.
  headline: How to use HtmlSaveOptions in C# with Aspose.HTML
  type: TechArticle
- description: Learn how to use HtmlSaveOptions in C# to control web‑font styles and
    save HTML files with Aspose.HTML. Full code example and practical tips included.
  name: How to use HtmlSaveOptions in C# with Aspose.HTML
  steps:
  - name: Why configure WebFontStyle?
    text: 'When you export an HTML document, Aspose.HTML can embed web fonts that
      match the original styling. By setting `WebFontStyle`, you tell the exporter
      which font variants to include. This reduces the final file size when you only
      need specific styles and guarantees that the rendered output matches the '
  - name: 5.1 Controlling CSS embedding
    text: 'You can decide whether to embed CSS inline, keep external links, or embed
      everything:'
  - name: 5.2 Saving to a specific encoding
    text: '```csharp saveOptions.Encoding = Encoding.UTF8; ```'
  - name: 5.3 Handling large documents
    text: 'For very large HTML files, consider streaming the output to avoid high
      memory consumption:'
  - name: 5.4 Error handling best practice
    text: 'Wrap the entire workflow in a try‑catch block and log the exception details.
      This ensures that any I/O or parsing errors are captured:'
  - name: Expected console output
    text: '``` HTML saved successfully to ''YOUR_DIRECTORY/output.html''. ```'
  type: HowTo
tags:
- Aspose.HTML
- C#
- HTML processing
title: Hur man använder HtmlSaveOptions i C# med Aspose.HTML
url: /sv/net/working-with-html-documents/how-to-use-htmlsaveoptions-in-c-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så använder du HtmlSaveOptions i C# med Aspose.HTML

Om du behöver kontrollera hur Aspose.HTML sparar ett HTML‑dokument, **är det viktigt att lära sig hur man använder HtmlSaveOptions**. Denna handledning visar dig steg‑för‑steg hur du använder HtmlSaveOptions för att aktivera fetstil och kursiv web‑font‑stil när du sparar ett dokument.

Aspose HTML‑biblioteket erbjuder ett omfattande API för att ladda, manipulera och exportera HTML‑innehåll. I slutet av den här guiden kommer du att kunna:

* Ladda en befintlig HTML‑fil i ett `HTMLDocument`.
* Konfigurera `HtmlSaveOptions` för att tillämpa specifika `WebFontStyle`‑flaggor.
* Spara det modifierade dokumentet till en ny plats eller till en ström.
* Utöka lösningen för andra teckensnittsstilar, anpassad CSS och felhantering.

## Förutsättningar

Innan du börjar, se till att du har:

* .NET 6.0 eller senare installerat.
* En giltig licens för **Aspose.HTML for .NET** (gratis provversion fungerar för detta exempel).
* Visual Studio 2022 (eller någon C#‑IDE) för att kompilera och köra koden.

Inga ytterligare NuGet‑paket krävs utöver `Aspose.HTML`.

## Steg 1: Ställ in projektet och importera namnrymder

Skapa ett nytt **Console App**‑projekt och lägg till Aspose.HTML‑NuGet‑paketet:

```bash
dotnet add package Aspose.HTML
```

Sedan, högst upp i `Program.cs`, importera de nödvändiga namnrymderna:

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
```

Dessa namnrymder exponerar typerna `HTMLDocument`, `HtmlSaveOptions` och `WebFontStyle` som du kommer att använda genom hela handledningen.

## Steg 2: Ladda käll‑HTML‑dokumentet

Den första operationen är att läsa den HTML du vill bearbeta. Ersätt `"YOUR_DIRECTORY/input.html"` med den faktiska sökvägen till din fil.

```csharp
// Load the source HTML document from disk
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

`HTMLDocument` analyserar markupen, bygger ett DOM‑träd och gör det redo för manipulation. Om filen inte finns kastas ett undantag, så du kanske vill omsluta detta anrop i ett try‑catch‑block för produktionskod.

## Steg 3: Skapa och konfigurera HtmlSaveOptions

`HtmlSaveOptions` låter dig finjustera sparprocessen. För att aktivera fetstil och kursiv web‑font‑stil, kombinera motsvarande `WebFontStyle`‑flaggor med bitvis OR‑operator (`|`).

```csharp
// Create a new HtmlSaveOptions instance
HtmlSaveOptions saveOptions = new HtmlSaveOptions();

// Enable bold and italic web‑font styles (equivalent to the old FontStyle flags)
saveOptions.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

### Varför konfigurera WebFontStyle?

När du exporterar ett HTML‑dokument kan Aspose.HTML bädda in web‑fonter som matchar den ursprungliga stilen. Genom att sätta `WebFontStyle` talar du om för exportören vilka teckensnittsvarianter som ska inkluderas. Detta minskar den slutliga filstorleken när du bara behöver specifika stilar och garanterar att den renderade utskriften matchar källan.

#### Vanliga varianter

| Önskad stil | Motsvarande `WebFontStyle`‑flagga |
|-------------|-----------------------------------|
| Normal (vanlig) | `WebFontStyle.Regular` |
| Fet | `WebFontStyle.Bold` |
| Kursiv | `WebFontStyle.Italic` |
| Fet + Kursiv | `WebFontStyle.Bold | WebFontStyle.Italic` |
| Alla varianter | `WebFontStyle.All` |

Du kan kombinera valfri kombination som passar ditt scenario.

## Steg 4: Spara dokumentet med de konfigurerade alternativen

Skriv nu dokumentet till en ny fil. `Save`‑metoden accepterar mål‑sökvägen och den `HtmlSaveOptions`‑instans du förberett.

```csharp
// Save the processed HTML using the configured options
document.Save("YOUR_DIRECTORY/output.html", saveOptions);
```

Om du behöver skriva till en minnesström (t.ex. för att skicka filen via HTTP), använd den överlagrade metoden som accepterar ett `Stream`‑objekt:

```csharp
using (var stream = new MemoryStream())
{
    document.Save(stream, saveOptions);
    // Reset the position to read the content later
    stream.Position = 0;
    // Example: return the stream from a Web API endpoint
}
```

## Steg 5: Verifiera resultatet

Öppna `output.html` i en webbläsare eller inspektera filen med en textredigerare. Du bör se att `<style>`‑blocket nu innehåller `@font-face`‑regler för både fet- och kursivvarianter av alla web‑fonter som refereras i det ursprungliga dokumentet.

**Förväntat utdrag av output:**

```html
<link rel="stylesheet" href="fonts/Roboto-Bold.woff2" type="font/woff2">
<link rel="stylesheet" href="fonts/Roboto-Italic.woff2" type="font/woff2">
```

Om den ursprungliga HTML:n refererade till en teckensnittsfamilj som bara hade en normal vikt, kommer Aspose.HTML endast att inkludera den filen, i enlighet med `WebFontStyle`‑konfigurationen.

## Avancerat: Använda HtmlSaveOptions med ytterligare funktioner

### 5.1 Styrning av CSS‑inbäddning

Du kan bestämma om du vill bädda in CSS inline, behålla externa länkar eller bädda in allt:

```csharp
saveOptions.CssSavingMode = CssSavingMode.EmbedAllCss;
```

### 5.2 Spara med en specifik kodning

```csharp
saveOptions.Encoding = Encoding.UTF8;
```

### 5.3 Hantera stora dokument

För mycket stora HTML‑filer, överväg att strömma utdata för att undvika hög minnesanvändning:

```csharp
using (FileStream fs = new FileStream("large_output.html", FileMode.Create, FileAccess.Write))
{
    document.Save(fs, saveOptions);
}
```

### 5.4 Bästa praxis för felhantering

Omslut hela arbetsflödet i ett try‑catch‑block och logga undantagsdetaljerna. Detta säkerställer att eventuella I/O‑ eller parsingsfel fångas:

```csharp
try
{
    // Load, configure, and save as shown earlier
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error processing HTML: {ex.Message}");
}
```

## Pro‑tips: Återanvänd HtmlSaveOptions för flera sparningar

Om du behöver spara flera dokument med samma teckensnittsstils‑konfiguration, skapa en enda `HtmlSaveOptions`‑instans och återanvänd den. Detta minskar overhead för objektallokering och garanterar konsekvent output.

```csharp
HtmlSaveOptions sharedOptions = new HtmlSaveOptions
{
    WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic,
    CssSavingMode = CssSavingMode.EmbedAllCss
};

foreach (var file in Directory.GetFiles("input_folder", "*.html"))
{
    HTMLDocument doc = new HTMLDocument(file);
    string outputPath = Path.Combine("output_folder", Path.GetFileName(file));
    doc.Save(outputPath, sharedOptions);
}
```

## Fullt körbart exempel

Nedan är hela programmet som inkluderar alla diskuterade steg. Kopiera det till `Program.cs` och kör det efter att du justerat filsökvägarna.

```csharp
using System;
using System.IO;
using System.Text;
using Aspose.Html;
using Aspose.Html.Drawing;

class Program
{
    static void Main()
    {
        // Define input and output paths
        string inputPath = "YOUR_DIRECTORY/input.html";
        string outputPath = "YOUR_DIRECTORY/output.html";

        try
        {
            // Step 1: Load the source HTML document
            HTMLDocument document = new HTMLDocument(inputPath);

            // Step 2: Create HtmlSaveOptions and enable bold + italic web‑font styles
            HtmlSaveOptions saveOptions = new HtmlSaveOptions
            {
                WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic,
                // Optional: embed all CSS and use UTF‑8 encoding
                CssSavingMode = CssSavingMode.EmbedAllCss,
                Encoding = Encoding.UTF8
            };

            // Step 3: Save the document with the configured options
            document.Save(outputPath, saveOptions);

            Console.WriteLine($"HTML saved successfully to '{outputPath}'.");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

### Förväntad konsolutdata

```
HTML saved successfully to 'YOUR_DIRECTORY/output.html'.
```

Öppna den genererade `output.html` för att bekräfta att fet- och kursiv web‑font‑stilar finns.

## Slutsats

Du vet nu **hur du använder HtmlSaveOptions** för att kontrollera inbäddning av web‑fonter, CSS‑hantering och kodning när du sparar HTML med Aspose HTML‑biblioteket i C#. Genom att konfigurera `WebFontStyle`‑flaggorna kan du skräddarsy output så att den bara inkluderar de teckensnittsvarianter du behöver, vilket förbättrar prestanda och minskar filstorleken.

Härifrån kan du utforska andra `HtmlSaveOptions`‑egenskaper såsom `ImageSavingMode`, `JavaScriptSavingMode`, eller kombinera flera alternativ för komplexa konverteringspipelines. Experimentera med att spara till strömmar för webb‑API:er, eller integrera arbetsflödet i ett större dokumentgenereringssystem.

---

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man sparar HTML med Aspose.Html – Komplett C#‑guide](/html/english/net/working-with-html-documents/how-to-save-html-with-aspose-html-complete-c-guide/)
- [Hur man använder Aspose för att rendera HTML till PNG i C#](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-in-c/)
- [Hur man använder Aspose för att rendera HTML till PNG – Steg‑för‑steg‑guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}