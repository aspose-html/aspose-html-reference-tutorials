---
category: general
date: 2026-10-15
description: Kombinera teckensnittsstilar i C# genom att ange teckensnittsfamilj och
  storlek med Aspose.HTML Font‑konstruktorn. Lär dig att snabbt skapa fet kursiv text.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- combine font styles
- set font family
- set font size c#
- c# font constructor
- create bold italic text
language: sv
lastmod: 2026-10-15
og_description: Kombinera teckensnittsstilar i C# med Aspose.HTML Font‑konstruktorn.
  Denna handledning visar hur du anger teckensnittsfamilj, ställer in teckenstorlek
  i C# och skapar fet kursiv text.
og_image_alt: Screenshot of C# code that combines font styles with Aspose.HTML
og_title: Kombinera typsnittsstilar i C# – snabbguide med Aspose.HTML
schemas:
- author: Aspose
  dateModified: '2026-10-15'
  description: Combine font styles in C# by setting font family and size using the
    Aspose.HTML Font constructor. Learn to create bold italic text quickly.
  headline: How to combine font styles in C# with Aspose.HTML
  type: TechArticle
- description: Combine font styles in C# by setting font family and size using the
    Aspose.HTML Font constructor. Learn to create bold italic text quickly.
  name: How to combine font styles in C# with Aspose.HTML
  steps:
  - name: Explanation
    text: '- `"Arial"` – **set font family** to Arial, a widely supported sans‑serif
      typeface. - `12` – **set font size c#** to 12 points, which is a comfortable
      default for body text. - `WebFontStyle.Bold | WebFontStyle.Italic` – this expression
      **combines font styles**. The `|` operator merges the `Bold` and'
  - name: Why this works
    text: '- `paragraph.Style.FontFamily` uses the **set font family** value from
      the `Font` instance. - `paragraph.Style.FontSize` uses the **set font size c#**
      you defined. - The explicit `FontWeight` and `FontStyle` assignments mirror
      the **combine font styles** flags, ensuring the rendered output matches t'
  - name: Pro tip on performance
    text: 'Creating many `Font` objects inside a tight loop can degrade performance.
      Cache commonly used fonts in a dictionary and reuse them:'
  type: HowTo
tags:
- C#
- Aspose.HTML
- Font styling
title: Hur man kombinerar teckensnittsstilar i C# med Aspose.HTML
url: /sv/net/html-document-manipulation/how-to-combine-font-styles-in-c-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man kombinerar teckensnittsstilar i C# med Aspose.HTML

Om du behöver **kombinera teckensnittsstilar** i en C#‑applikation visar den här guiden ett koncist sätt att göra det med Aspose.HTML. Du får lära dig hur du anger teckensnittsfamilj, anger teckensnittsstorlek c#, och använder **c#‑teckensnittskonstruktorn** för att skapa fet kursiv text på bara några rader kod.

Utvecklare undrar ofta om de måste bygga separata `Font`‑objekt för varje stil eller om en enda konstruktor kan hantera flera attribut. Svaret är att du kan kombinera stilar direkt när du instansierar teckensnittet. Denna handledning går igenom hela processen, från att importera rätt namnrymd till att rendera stylad text i ett HTML‑dokument.

## Förutsättningar

Innan du börjar, se till att du har:

- Aspose.HTML för .NET installerat (NuGet‑paketet `Aspose.HTML` version 23.9 eller senare).
- .NET 6.0+ eller .NET Framework 4.7.2+.
- Grundläggande kunskap om C#‑syntax och objekt‑orienterad programmering.

Inga ytterligare tredjepartsbibliotek krävs.

## Steg 1: Importera drawing‑namnrymden

Det första du måste göra är att **importera Aspose.Html.Drawing‑namnrymden** så att du kan komma åt `Font`‑klassen och relaterade ritverktyg.

```csharp
using Aspose.Html.Drawing;
```

> **Varför?** `Font`‑klassen finns i `Aspose.Html.Drawing`. Genom att importera denna namnrymd blir typen tillgänglig utan att du måste ange hela namnet varje gång, vilket håller koden ren och läsbar.

## Steg 2: Använd c#‑teckensnittskonstruktorn för att ange familj, storlek och kombinera stilar

Den **c#‑teckensnittskonstruktorn** accepterar tre parametrar: teckensnittsfamiljens namn, punktstorleken och en bitvis kombination av `WebFontStyle`‑flaggor. Genom att använda den bitvisa OR‑operatorn (`|`) kan du **kombinera teckensnittsstilar** såsom fet och kursiv.

```csharp
// Create a Font instance that is both bold and italic
var font = new Font("Arial", 12, WebFontStyle.Bold | WebFontStyle.Italic);
```

### Förklaring

- `"Arial"` – **ange teckensnittsfamilj** till Arial, ett brett stödjande sans‑serif‑typsnitt.
- `12` – **ange teckensnittsstorlek c#** till 12 pt, vilket är en bekväm standard för brödtext.
- `WebFontStyle.Bold | WebFontStyle.Italic` – detta uttryck **kombinerar teckensnittsstilar**. `|`‑operatorn sammanslår `Bold`‑ och `Italic`‑flaggorna till ett enda värde, så att konstruktorn kan skapa ett teckensnitt som samtidigt är fet *och* kursiv.

> **Proffstips:** Om du behöver lägga till understrykning eller genomstrykning, inkludera `WebFontStyle.Underline` eller `WebFontStyle.Strikethrough` i samma uttryck.

## Steg 3: Applicera teckensnittet på ett HTML‑element

Nu när du har ett `Font`‑objekt kan du applicera det på vilket HTML‑element som helst som stödjer styling. Nedan skapar vi ett enkelt HTML‑dokument, lägger till ett stycke och tilldelar den kombinerade stilen.

```csharp
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

// Create a new HTML document
var document = new HTMLDocument();

// Add a paragraph element
var paragraph = document.CreateElement("p");
paragraph.InnerHtml = "This text is bold and italic using combined font styles.";
document.Body.AppendChild(paragraph);

// Apply the Font object to the paragraph's style
paragraph.Style.FontFamily = font.Family;
paragraph.Style.FontSize = $"{font.Size}pt";
paragraph.Style.FontWeight = "bold";
paragraph.Style.FontStyle = "italic";

// Render the document to an image (optional verification step)
using (var renderer = new ImageRenderer())
{
    renderer.Render(document, "output.png");
}
```

### Varför detta fungerar

- `paragraph.Style.FontFamily` använder **ange teckensnittsfamilj**‑värdet från `Font`‑instansen.
- `paragraph.Style.FontSize` använder **ange teckensnittsstorlek c#** som du definierade.
- De explicita `FontWeight`‑ och `FontStyle`‑tilldelningarna speglar **kombinera teckensnittsstilar**‑flaggorna, vilket säkerställer att den renderade utdata matchar den avsedda fet‑kursiva utseendet.

> **Edge case:** Om den valda teckensnittsfamiljen inte stödjer kursiva eller feta varianter kan webbläsaren simulera stilen, vilket kan påverka den visuella återgivningen. Testa alltid med det faktiska teckensnitt du planerar att distribuera.

## Steg 4: Verifiera resultatet

Kör programmet och öppna `output.png`. Du bör se meningen renderad i Arial, 12 pt, med både fet och kursiv stil. Detta bekräftar att **c#‑teckensnittskonstruktorn** korrekt kombinerade stilarna.

Om du föredrar att visa HTML‑koden direkt kan du hoppa över renderingssteget och spara dokumentet:

```csharp
document.Save("styled.html");
```

Öppna `styled.html` i någon modern webbläsare för att se samma stylade stycke.

## Vanliga variationer och tips

| Mål | Kodsnutt | Kommentar |
|------|--------------|-------|
| **Endast fet** | `new Font("Arial", 12, WebFontStyle.Bold)` | Använd en enda flagga när du inte behöver kursiv. |
| **Fet, kursiv, understruken** | `new Font("Arial", 12, WebFontStyle.Bold \| WebFontStyle.Italic \| WebFontStyle.Underline)` | Kombinera så många stilar du behöver. |
| **Dynamisk storlek** | `var size = 14; var font = new Font("Times New Roman", size, WebFontStyle.Italic);` | Du kan beräkna storleken vid körning. |
| **Anpassad teckensnittsfamilj** | `new Font("MyCustomFont", 10, WebFontStyle.Bold)` | Säkerställ att det anpassade teckensnittet är tillgängligt för renderingsmotorn (t.ex. via `@font-face`). |

### Proffstips om prestanda

Att skapa många `Font`‑objekt i en tight loop kan försämra prestandan. Cacha ofta använda teckensnitt i en dictionary och återanvänd dem:

```csharp
var fontCache = new Dictionary<string, Font>();
string key = "Arial_12_BoldItalic";

if (!fontCache.TryGetValue(key, out var cachedFont))
{
    cachedFont = new Font("Arial", 12, WebFontStyle.Bold | WebFontStyle.Italic);
    fontCache[key] = cachedFont;
}
```

## Fullt körbart exempel

Nedan är ett självständigt program som du kan kopiera, klistra in och köra. Det demonstrerar hela flödet från att importera namnrymden till att rendera den stylade texten.

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Rendering.Image;

class Program
{
    static void Main()
    {
        // Step 1: Import Aspose.Html.Drawing (already done via using statements)

        // Step 2: Create a Font that combines bold and italic
        var font = new Font("Arial", 12, WebFontStyle.Bold | WebFontStyle.Italic);

        // Step 3: Build a simple HTML document
        var document = new HTMLDocument();
        var paragraph = document.CreateElement("p");
        paragraph.InnerHtml = "This text is bold and italic using combined font styles.";
        document.Body.AppendChild(paragraph);

        // Apply font settings
        paragraph.Style.FontFamily = font.Family;
        paragraph.Style.FontSize = $"{font.Size}pt";
        paragraph.Style.FontWeight = "bold";
        paragraph.Style.FontStyle = "italic";

        // Optional: Render to PNG for visual verification
        using (var renderer = new ImageRenderer())
        {
            renderer.Render(document, "output.png");
        }

        // Save HTML for manual inspection
        document.Save("styled.html");

        Console.WriteLine("Styled document generated: styled.html and output.png");
    }
}
```

**Förväntad utdata**

- `styled.html` visar ett stycke med Arial 12 pt, fet och kursiv.
- `output.png` innehåller en bild av samma stylade stycke.

## Slutsats

Du vet nu hur du **kombinerar teckensnittsstilar** i C# med Aspose.HTML **c#‑teckensnittskonstruktor**. Genom att **ange teckensnittsfamilj**, **ange teckensnittsstorlek c#**, och skicka en bitvis‑OR av `WebFontStyle`‑flaggor kan du **skapa fet kursiv text** (eller vilken kombination som helst) med minimal kod. Använd samma mönster för andra element, cacha teckensnitt för prestanda och utöka metoden med understrykning eller genomstrykning vid behov.

Redo att utforska mer? Prova:

- Använd `WebFontStyle.Underline` för att **ange teckensnitt understrykning**.
- Ladda anpassade webbteckensnitt med `@font-face` och applicera dem via samma konstruktor.
- Rendera PDF‑filer istället för bilder genom att byta `ImageRenderer` mot `PdfRenderer`.

Lycka till med kodandet, och njut av flexibiliteten att programatiskt styla text i C#!

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringssätt i dina egna projekt.

- [Create HTML Document C# – Bold Italic Text with Custom Font](/html/english/net/html-document-manipulation/create-html-document-c-bold-italic-text-with-custom-font/)
- [Create HTML document C# – Render to PNG with Bold Italic Font](/html/english/net/rendering-html-documents/create-html-document-c-render-to-png-with-bold-italic-font/)
- [Simpan HTML sebagai PDF di C# – Panduan Lengkap dengan Font](/html/indonesian/net/html-extensions-and-conversions/save-html-as-pdf-in-c-complete-guide-with-fonts/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}