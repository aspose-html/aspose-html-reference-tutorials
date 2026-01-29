---
category: general
date: 2025-12-29
description: Maak een HTML‑document in C# en leer hoe je lettertypefamilie en lettergrootte
  instelt, en vervolgens HTML opslaat als PDF of HTML naar PDF converteert met Aspose.HTML.
draft: false
keywords:
- create html document
- set font family
- set font size
- save html as pdf
- convert html to pdf
language: nl
og_description: Maak een HTML‑document in C# en zie direct hoe je het lettertype,
  de lettergrootte instelt, en vervolgens HTML opslaat als PDF of HTML converteert
  naar PDF met Aspose.HTML.
og_title: HTML-document maken – gestylede tekst & PDF-export
tags:
- aspnet
- csharp
- pdf-generation
title: HTML-document maken met opgemaakte tekst en exporteren naar PDF – Volledige
  gids
url: /nl/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML-document maken met opgemaakte tekst en exporteren naar PDF

Heb je ooit **een HTML-document** on-the-fly moeten maken en omzetten naar een PDF zonder je C#-code te verlaten? Misschien bouw je een rapportage‑engine, een factuurgenerator, of gewoon een snelle preview voor gebruikers. Het goede nieuws is dat je dit in een paar regels kunt doen met Aspose.HTML, en je krijgt volledige controle over lettertypefamilie, lettergrootte en zelfs vet‑cursieve opmaak.

In deze tutorial lopen we het volledige proces door — van het opzetten van een in‑memory HTML-document tot het opslaan als PDF‑bestand. Aan het einde weet je precies hoe je **lettertypefamilie instelt**, **lettergrootte instelt**, en **HTML opslaat als PDF** (ook wel **HTML naar PDF converteren** genoemd) met een nette, productie‑klare code‑voorbeeld.

## Wat je nodig hebt

- .NET 6+ (de API werkt zowel met .NET Core als .NET Framework)  
- Aspose.HTML for .NET NuGet‑pakket (`Aspose.Html`) – installeer via `dotnet add package Aspose.Html`  
- Een map op schijf waar de gegenereerde PDF kan worden weggeschreven  

Geen extra HTML‑templates, geen externe converters, alleen pure C#.

![illustratie van html-document maken](/images/create-html-document.png){alt="voorbeeld van html-document maken"}

## Stap 1: Maak het HTML-document

Eerst hebben we een leeg HTML‑documentobject nodig. Beschouw het als een leeg canvas waarop je later je opgemaakte alinea schildert.

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

// Step 1 – initialize a new HTML document in memory
HTMLDocument htmlDocument = new HTMLDocument();

// Grab a reference to the <body> element for later use
HTMLBodyElement body = htmlDocument.Body;
```

**Waarom dit belangrijk is:** `HTMLDocument` geeft je een DOM‑achtige structuur die je programmatisch kunt manipuleren. Je hoeft geen ruwe strings of bestands‑I/O aan te raken tot het allerlaatste moment.

## Stap 2: Voeg een alinea toe en stel lettertypefamilie & lettergrootte in

Nu maken we een `<p>`‑element, voegen wat tekst toe, en definiëren expliciet de lettertypefamilie en -grootte. Hier komen de sleutelwoorden **set font family** en **set font size** in beeld.

```csharp
// Step 2 – create a <p> element with some sample text
HtmlElement paragraph = htmlDocument.CreateElement("p");
paragraph.InnerHtml = "Bold & Italic text";

// Define the base font style
paragraph.Style.FontFamily = "Arial";   // set font family
paragraph.Style.FontSize = "18px";      // set font size

// Attach the paragraph to the document body
body.AppendChild(paragraph);
```

**Pro‑tip:** Als je een web‑veilige fallback nodig hebt, kun je een door komma’s gescheiden lijst opgeven zoals `"Arial, Helvetica, sans-serif"`; de browser (of Aspose) kiest het eerste beschikbare lettertype.

## Stap 3: Pas vet‑ en cursieve opmaak toe met WebFontStyle‑vlaggen

Aspose.HTML biedt een handige enum `WebFontStyle` waarmee je stijlen kunt combineren met een bitwise OR. Laten we de tekst zowel vet **als** cursief maken.

```csharp
// Step 3 – apply bold and italic using WebFontStyle flags
paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

**Wat er onder de motorkap gebeurt:** De `FontStyle`‑eigenschap wordt vertaald naar CSS‑declaraties `font-weight` en `font-style`. Door de vlaggen te OR‑en vermijden we het schrijven van twee aparte CSS‑regels.

## Stap 4: Converteer de HTML naar PDF (HTML opslaan als PDF)

De laatste stap is de daadwerkelijke conversie. Met één aanroep van `Save` rendert Aspose.HTML de DOM en schrijft een PDF‑bestand naar schijf. Dit voldoet aan zowel de **save html as pdf** als **convert html to pdf** eisen.

```csharp
// Step 4 – save the HTML document as a PDF file
string outputPath = @"C:\Temp\styled.pdf";
htmlDocument.Save(outputPath, new PDFSaveOptions());

// Optional: open the PDF automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Verwacht resultaat:** Open `styled.pdf` en je ziet een enkele alinea met de tekst “Bold & Italic text” in 18‑px Arial, vet en cursief weergegeven. De PDF‑afmetingen komen overeen met een standaard A4‑pagina, en de tekst is selecteerbaar — dankzij vectorrendering.

## Volledig werkend voorbeeld

Alles bij elkaar genomen, hier is het volledige, kant‑klaar programma:

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new HTML document
        HTMLDocument htmlDocument = new HTMLDocument();
        HTMLBodyElement body = htmlDocument.Body;

        // 2️⃣ Add a styled paragraph
        HtmlElement paragraph = htmlDocument.CreateElement("p");
        paragraph.InnerHtml = "Bold & Italic text";

        // Set font family and size
        paragraph.Style.FontFamily = "Arial";
        paragraph.Style.FontSize = "18px";

        // 3️⃣ Apply bold + italic
        paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // Append to body
        body.AppendChild(paragraph);

        // 4️⃣ Save as PDF (convert HTML to PDF)
        string outputFile = @"C:\Temp\styled.pdf";
        htmlDocument.Save(outputFile, new PDFSaveOptions());

        Console.WriteLine($"PDF generated at: {outputFile}");
    }
}
```

### De code uitvoeren

1. Installeer het Aspose.HTML NuGet‑pakket:  
   ```bash
   dotnet add package Aspose.Html
   ```
2. Vervang `C:\Temp\styled.pdf` door een map waarin je schrijfrechten hebt.  
3. Bouw en voer uit: `dotnet run`.  

Je zou een console‑bericht moeten zien dat de bestandslocatie bevestigt, en de PDF zal de opgemaakte alinea bevatten.

## Veelgestelde vragen & randgevallen

- **Wat als ik een aangepast web‑lettertype nodig heb?**  
  Laad het lettertype met `HTMLFontFaceRule` of verwijs naar een externe `@font-face` CSS‑file voordat je de alinea maakt.

- **Kan ik afbeeldingen toevoegen vóór het converteren?**  
  Absoluut. Gebruik `HTMLImageElement img = (HTMLImageElement)htmlDocument.CreateElement("img");` en stel `img.Source` in op een lokaal pad of data‑URI.

- **Hoe zit het met meer‑pagina‑PDF’s?**  
  Voeg meer elementen toe (tabellen, divs, enz.) en Aspose.HTML pagineert automatisch wanneer de inhoud de paginahoogte overschrijdt.

- **Is er een manier om PDF‑metadata te beheren?**  
  Geef een `PdfSaveOptions`‑instantie door en stel eigenschappen in zoals `Author`, `Title` of `PdfAConformanceLevel`.

## Samenvatting

We hebben behandeld hoe je **een HTML-document** in C# maakt, **lettertypefamilie instelt**, **lettergrootte instelt**, vet‑cursieve stijlen toepast, en uiteindelijk **HTML opslaat als PDF** — effectief **HTML naar PDF converteert** met Aspose.HTML. De code‑snippet is kort genoeg om in elk .NET‑project te gebruiken, maar toch volledig genoeg om als solide basis te dienen voor complexere rapportagescenario’s.

## Volgende stappen

- Experimenteer met CSS‑klassen voor herbruikbare styling.  
- Combineer meerdere alinea’s, tabellen en afbeeldingen om rijkere PDF’s te maken.  
- Verken PDF/A‑conformiteit als je archief‑kwaliteit documenten nodig hebt.  

Voel je vrij om het lettertype, de grootte of kleuren aan te passen — er is geen limiet aan wat je programmatisch kunt genereren. Veel plezier met coderen, en moge je PDF’s altijd precies renderen zoals je je voorstelt!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}