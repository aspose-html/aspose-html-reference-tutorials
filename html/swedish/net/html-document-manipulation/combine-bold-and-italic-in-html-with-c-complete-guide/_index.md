---
category: general
date: 2026-04-01
description: Kombinera fetstil och kursiv i HTML med C#. Lär dig hur du ändrar HTML‑teckensnittsstil,
  sparar den modifierade HTML‑koden och ändrar teckensnittsstil med C# i några enkla
  steg.
draft: false
keywords:
- combine bold and italic
- save modified html
- modify html font style
- change font style c#
language: sv
og_description: Kombinera fetstil och kursiv i HTML med C#. Den här guiden visar hur
  du ändrar HTML‑fontstil, sparar den modifierade HTML:n och snabbt ändrar fontstil
  i C#.
og_title: Kombinera fetstil och kursiv i HTML med C# – Steg för steg
tags:
- C#
- Aspose.Html
- HTML manipulation
title: Kombinera fetstil och kursiv i HTML med C# – Komplett guide
url: /sv/net/html-document-manipulation/combine-bold-and-italic-in-html-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kombinera fet och kursiv i HTML med C# – Komplett guide

Har du någonsin behövt **kombinera fet och kursiv** i ett HTML‑fragment men varit osäker på hur man gör det programatiskt? Du är inte ensam—många utvecklare stöter på detta problem när de genererar dynamiska e‑postmeddelanden eller rapporter. Den goda nyheten är att med några rader C# och Aspose.HTML‑biblioteket kan du applicera en kombinerad fet‑och‑kursiv teckensnittsstil på vilket dokument som helst och sedan **spara modifierad HTML** för senare bruk.

I den här handledningen går vi igenom hela processen: laddar ett litet HTML‑fragment, **modifierar HTML‑teckensnittsstil**, applicerar **kombinera fet och kursiv**‑effekten och slutligen **sparar den modifierade HTML** till disk. När du är klar vet du exakt hur du **ändrar teckensnittsstil i C#** utan att gräva i oklara dokument.

## Vad du behöver

- .NET 6 eller senare (koden fungerar även på .NET Core)  
- Aspose.HTML för .NET – du kan hämta det från NuGet (`Install-Package Aspose.HTML`)  
- En textredigerare eller IDE (Visual Studio, VS Code, Rider—vad du än föredrar)  

Inga andra beroenden. Om du redan har ett projekt, lägg bara till NuGet‑paketet så är du klar.

![Skärmbild som visar kombinerad fet och kursiv text i en webbläsare – kombinera fet och kursiv](https://example.com/combine-bold-italic.png)

*Bildtext: kombinera fet och kursiv*

## Steg 1: Ladda HTML‑fragmentet och skapa ett dokument

Först behöver vi ett `Aspose.Html.Document`‑objekt som representerar den HTML vi vill arbeta med. Koden nedan laddar ett litet fragment som innehåller `<b>`‑ och `<i>`‑taggar.

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;

// The raw HTML we’ll transform
string htmlContent = "<html><body><b>Bold</b> <i>Italic</i></body></html>";

// Create a Document instance from the string
Document document = new Document(htmlContent);
```

**Varför detta är viktigt:**  
Att skapa ett `Document` ger dig en full DOM‑liknande modell, så att du kan manipulera stilar exakt som en webbläsare skulle. Det förbereder också objektet för senare sparning, vilket är avgörande när du vill **spara modifierad HTML**.

## Steg 2: Kombinera fet och kursiv teckensnittsstil

Nu kommer kärnan i handledningen—att applicera en stil som är både fet **och** kursiv samtidigt. Aspose.HTML exponerar `WebFontStyle`‑enumerationen, och medlemmen `BoldItalic` är en förkortning för `FontStyle.Bold | FontStyle.Italic`.

```csharp
// Retrieve the default viewport style (covers the whole document)
var defaultStyle = document.DefaultViewPort.Style;

// Apply the combined bold‑and‑italic style
defaultStyle.FontStyle = WebFontStyle.BoldItalic; // same as FontStyle.Bold | FontStyle.Italic
```

**Förklaring:**  
`DefaultViewPort.Style` är den globala CSS‑regeln som påverkar varje element om den inte åsidosätts. Genom att sätta `FontStyle` till `BoldItalic` säkerställer vi att **modifiera HTML‑teckensnittsstil** tillämpas enhetligt, vilket eliminerar behovet av att ändra varje `<b>`‑ eller `<i>`‑tagg individuellt.

> *Proffstips:* Om du bara vill att vissa element ska vara fet‑och‑kursiv, hämta dem med `document.QuerySelectorAll("p.special")` och sätt stilen på varje nod istället för på den globala viewporten.

## Steg 3: Verifiera förändringen (valfritt men hjälpsamt)

Innan vi skriver något till disk är det en bra idé att titta på den resulterande markupen. Du kan skriva ut HTML till konsolen eller ett debug‑fönster:

```csharp
// Output the transformed HTML for quick verification
string transformedHtml = document.ToString();
Console.WriteLine(transformedHtml);
```

Du bör se ett `<style>`‑block injicerat i `<head>` som tvingar hela kroppen att renderas med `font-weight: bold; font-style: italic;`. Detta bekräftar att **kombinera fet och kursiv**‑operationen lyckades.

## Steg 4: Spara modifierad HTML

Till sist sparar vi det uppdaterade dokumentet. `Save`‑metoden skriver automatiskt en välformad HTML‑fil och bevarar eventuella externa resurser du kan ha lagt till.

```csharp
// Choose an output path that makes sense for your project
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.html");

// Save the document – this is the “save modified html” step
document.Save(outputPath);
Console.WriteLine($"Modified HTML saved to: {outputPath}");
```

**Vad du får:**  
En `output.html`‑fil som, när den öppnas i någon webbläsare, visar den ursprungliga texten **både fet och kursiv**. Detta är det konkreta resultatet av att **ändra teckensnittsstil i C#** med Aspose.HTML.

## Steg 5: Vanliga variationer och kantfall

### a) Rikta in endast specifika element

Om du behöver **modifiera HTML‑teckensnittsstil** för bara en delmängd—t.ex. alla stycken med klassen `highlight`—använd en selector:

```csharp
var highlights = document.QuerySelectorAll("p.highlight");
foreach (var node in highlights)
{
    node.Style.FontStyle = WebFontStyle.BoldItalic;
}
```

### b) Behålla original‑`<b>` / `<i>`‑taggar

Ibland vill du bevara de ursprungliga taggarna för semantik men ändå applicera den kombinerade stilen. I så fall lägger du till en CSS‑klass istället för att åsidosätta den globala stilen:

```csharp
// Add a CSS class to the head
var style = document.CreateElement("style");
style.InnerHtml = ".bold-italic { font-weight: bold; font-style: italic; }";
document.Head.AppendChild(style);

// Apply the class to the body (or any element you like)
document.Body.ClassName = "bold-italic";
```

### c) Spara med annan kodning

Aspose.HTML använder UTF‑8 som standard, men du kan ange en annan kodning om ditt efterföljande system kräver det:

```csharp
var saveOptions = new HtmlSaveOptions()
{
    Encoding = System.Text.Encoding.ASCII // or any other Encoding
};
document.Save("output-ascii.html", saveOptions);
```

## Fullt fungerande exempel

Genom att sätta ihop allt får du ett självständigt program som du kan kopiera och klistra in i en konsolapp:

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the HTML snippet
        string htmlContent = "<html><body><b>Bold</b> <i>Italic</i></body></html>";
        Document document = new Document(htmlContent);

        // 2️⃣ Apply combined bold‑and‑italic style
        var defaultStyle = document.DefaultViewPort.Style;
        defaultStyle.FontStyle = WebFontStyle.BoldItalic; // combine bold and italic

        // 3️⃣ (Optional) Verify by printing to console
        Console.WriteLine("Transformed HTML:");
        Console.WriteLine(document.ToString());

        // 4️⃣ Save the modified HTML
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.html");
        document.Save(outputPath);
        Console.WriteLine($"✅ Modified HTML saved to: {outputPath}");
    }
}
```

**Förväntad output:**  
När du öppnar `output.html` i en webbläsare ser du orden “Bold Italic” renderade **både fet och kursiv**. Konsolen kommer också att visa den genererade HTML‑koden, med ett `<style>`‑tagg som upprätthåller den kombinerade stilen.

## Slutsats

Du vet nu hur du **kombinerar fet och kursiv** i ett HTML‑dokument med C#. Genom att ladda HTML i ett `Aspose.Html.Document`, sätta `WebFontStyle.BoldItalic` på standard‑viewporten och sedan **spara den modifierade HTML**, har du en ren, återanvändbar lösning för alla automatiseringsuppgifter. Oavsett om du behöver **modifiera HTML‑teckensnittsstil** globalt, rikta in specifika noder, eller **ändra teckensnittsstil i C#** för en webb‑mail‑mall, gäller samma principer.

Vad blir nästa steg? Prova att experimentera med andra `WebFontStyle`‑värden—`Underline`, `StrikeThrough` eller egna CSS‑klasser—för att utöka ditt stilverktyg. Du kan också utforska Aspose.HTML:s bildhantering eller PDF‑konverteringsfunktioner för att omvandla samma stylade dokument till en PDF i farten.

Har du frågor eller ett knepigt kantfall? Lägg en kommentar nedan, och lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}