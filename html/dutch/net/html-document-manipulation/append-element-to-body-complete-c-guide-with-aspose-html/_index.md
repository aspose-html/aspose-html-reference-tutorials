---
category: general
date: 2026-02-11
description: Voeg een element toe aan de body met Aspose.HTML in C#. Leer een paragraafelement
  te maken, de lettertypegewicht op vet te zetten, het lettertype op Arial in te stellen
  en de CSS-lettergrootte te definiëren — allemaal in één tutorial.
draft: false
keywords:
- append element to body
- create paragraph element
- set font weight bold
- set font family arial
- define css font size
language: nl
og_description: Voeg een element toe aan de body met Aspose.HTML. Deze tutorial laat
  zien hoe je een paragraafelement maakt, het lettertypegewicht op vet zet, het lettertype
  Arial instelt en de CSS-lettergrootte definieert.
og_title: Element aan body toevoegen – Complete C#‑gids
tags:
- Aspose.HTML
- C#
- DOM manipulation
title: Element aan body toevoegen – Complete C#‑gids met Aspose.HTML
url: /nl/net/html-document-manipulation/append-element-to-body-complete-c-guide-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Element aan body toevoegen – Complete C#-gids met Aspose.HTML

Heb je ooit moeten **append element to body** van een HTML‑document vanuit C# en je afgevraagd waarom de voorbeelden er altijd half‑afgewerkt uitzien? Je bent niet de enige. In veel quick‑start‑fragmenten zie je dat er een alinea wordt toegevoegd, maar de stylingdetails—zoals het **set font weight bold** maken van de tekst of het **set font family arial** gebruiken—worden weggelaten.  

In deze tutorial lopen we een real‑world‑scenario door: het maken van een `<p>`‑tag, het definiëren van de stijl (inclusief **define css font size**), en uiteindelijk **append element to body** met Aspose.HTML. Aan het einde heb je een volledig functioneel HTML‑bestand dat je in elke webpagina kunt plaatsen, en begrijp je de reden achter elke regel code.

## Wat je zult leren

- Hoe je **create paragraph element** programmeel maakt.
- De exacte stappen om **set font weight bold** en **set font family arial** te gebruiken met de `WebFontStyle`‑enum.
- Hoe je **define css font size** in points definieert voor precieze typografie.
- De meest nette manier om **append element to body** uit te voeren zonder handmatige string‑concatenatie.
- Tips, randgevallen, en een volledig uitvoerbaar voorbeeld dat je kunt copy‑paste.

Er zijn geen externe bibliotheken nodig buiten Aspose.HTML, en de code werkt met .NET 6+ (of .NET Framework 4.7.2). Laten we beginnen.

## Stap 1 – Installeer Aspose.HTML en zet het project op

Allereerst, zorg ervoor dat je het Aspose.HTML NuGet‑pakket hebt:

```bash
dotnet add package Aspose.HTML
```

> Pro tip: Gebruik de nieuwste stabiele versie (op het moment van schrijven, **23.9.0**) om te profiteren van bugfixes en nieuwe CSS‑functies.

Maak een nieuwe console‑app (of integreer in een bestaand project) en voeg de volgende `using`‑directieven toe:

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
```

## Stap 2 – Definieer CSS‑stijl: lettertypefamilie, grootte, gewicht en cursief

Waarom een stijlobject definiëren in plaats van een ruwe `style`‑attribuut‑string te schrijven? Omdat `CSSStyleDeclaration` eigenschapsnamen valideert, eenheidconversie afhandelt, en toekomstige wijzigingen moeiteloos maakt.

```csharp
// Step 2: Build a CSS style block
var paragraphStyle = new CSSStyleDeclaration();

// Set the font family to Arial – this satisfies the “set font family arial” requirement
paragraphStyle.FontFamily = "Arial";

// Define the font size in points; “define css font size” is clearer than using pixels for print‑like output
paragraphStyle.FontSize = new CSSLength(14, CSSLengthUnit.Point);

// Make the text bold – fulfills “set font weight bold”
paragraphStyle.FontWeight = WebFontStyle.Bold;

// Optional: add italic for visual flair
paragraphStyle.FontStyle = WebFontStyle.Italic;
```

> **Waarom points?** Points zijn apparaat‑onafhankelijk, waardoor dezelfde visuele grootte op scherm en bij afdrukken wordt gegarandeerd. Als je een responsief ontwerp nodig hebt, vervang dan `CSSLengthUnit.Point` door `CSSLengthUnit.Px` of `%`.

## Stap 3 – Maak een nieuw HTML‑document

Aspose.HTML biedt een schone, DOM‑achtige API die browsers nabootst. Beschouw `HTMLDocument` als het root‑object dat je zou krijgen van `document` in JavaScript.

```csharp
// Step 3: Initialize an empty HTML document
var htmlDoc = new HTMLDocument();
```

Op dit punt bevat het document de minimale `<html><head></head><body></body></html>`‑structuur, klaar voor manipulatie.

## Stap 4 – Maak het alinea‑element en pas de stijl toe

Nu maken we daadwerkelijk **create paragraph element**. De `CreateElement`‑methode retourneert een `IHTMLElement` die we kunnen verrijken met attributen en innerlijke inhoud.

```csharp
// Step 4: Build the <p> element
var paragraph = htmlDoc.CreateElement("p");

// Apply the previously built CSS style; CssText converts the declaration to a valid style string
paragraph.SetAttribute("style", paragraphStyle.CssText);

// Insert the visible text
paragraph.InnerHTML = "Styled with WebFontStyle – bold, italic, Arial, 14pt.";
```

Als je `paragraphStyle.CssText` inspecteert, zie je iets als:

```
font-family: Arial; font-size: 14pt; font-weight: bold; font-style: italic;
```

## Stap 5 – Voeg element toe aan body

Hier is het moment waar je op hebt gewacht: **append element to body**. Deze enkele regel doet het zware werk, door de `<p>` in de `<body>`‑node van het document te plaatsen.

```csharp
// Step 5: Append the styled paragraph to the document body
htmlDoc.Body.AppendChild(paragraph);
```

> **Edge case alert:** Als je `AppendChild` aanroept op een node die het element al bevat, wordt het element verplaatst—niet gedupliceerd. Dit voorkomt per ongeluk dubbele alinea's bij het itereren.

## Stap 6 – Sla het document op en controleer de output

Schrijf tenslotte de HTML naar schijf zodat je het in elke browser kunt openen:

```csharp
// Step 6: Persist the HTML file
string outputPath = Path.Combine(Environment.CurrentDirectory, "StyledParagraph.html");
htmlDoc.Save(outputPath);

// Optional: launch the file automatically (works on Windows)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo(outputPath) { UseShellExecute = true });
```

### Verwacht resultaat

Het openen van **StyledParagraph.html** moet een enkele regel tekst weergeven:

> *Gestyled met WebFontStyle – bold, italic, Arial, 14pt.*

De tekst zal **bold**, **italic**, weergegeven in **Arial**, en met een grootte van **14 pt** zijn. Als je de bron inspecteert, zie je:

```html
<!DOCTYPE html>
<html>
<head></head>
<body>
  <p style="font-family: Arial; font-size: 14pt; font-weight: bold; font-style: italic;">
    Styled with WebFontStyle – bold, italic, Arial, 14pt.
  </p>
</body>
</html>
```

## Volledig werkend voorbeeld (klaar om te copy‑pasten)

Hieronder staat het volledige programma dat je in `Program.cs` kunt plaatsen. Er zijn geen andere bestanden nodig.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Define CSS style (font family, size, weight, style)
        var paragraphStyle = new CSSStyleDeclaration
        {
            FontFamily = "Arial",                                   // set font family arial
            FontSize = new CSSLength(14, CSSLengthUnit.Point),      // define css font size
            FontWeight = WebFontStyle.Bold,                         // set font weight bold
            FontStyle = WebFontStyle.Italic                         // optional italic for demo
        };

        // 2️⃣ Create an empty HTML document
        var htmlDoc = new HTMLDocument();

        // 3️⃣ Build a <p> element and attach the style
        var paragraph = htmlDoc.CreateElement("p");
        paragraph.SetAttribute("style", paragraphStyle.CssText);
        paragraph.InnerHTML = "Styled with WebFontStyle – bold, italic, Arial, 14pt.";

        // 4️⃣ Append element to body
        htmlDoc.Body.AppendChild(paragraph);

        // 5️⃣ Save the file
        string output = Path.Combine(Environment.CurrentDirectory, "StyledParagraph.html");
        htmlDoc.Save(output);
        Console.WriteLine($"HTML saved to: {output}");

        // Open automatically (Windows only)
        System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo(output) { UseShellExecute = true });
    }
}
```

Voer `dotnet run` uit en je hebt een kant‑en‑klaar HTML‑bestand.

## Veelgestelde vragen & randgevallen

### Wat als ik meerdere alinea's moet toevoegen?

Herhaal gewoon **Stap 4** en **Stap 5** binnen een lus. Onthoud dat elke aanroep van `CreateElement("p")` een nieuw knooppunt retourneert, zodat je per ongeluk niet hetzelfde element hergebruikt.

```csharp
for (int i = 1; i <= 3; i++)
{
    var p = htmlDoc.CreateElement("p");
    p.SetAttribute("style", paragraphStyle.CssText);
    p.InnerHTML = $"Paragraph {i}";
    htmlDoc.Body.AppendChild(p);
}
```

### Kan ik externe CSS‑bestanden gebruiken in plaats van inline‑stijlen?

Absoluut. Vervang het inline `style`‑attribuut door een klassenaam en voeg een `<style>`‑blok toe of link naar een extern stylesheet. De inline‑benadering wordt hier getoond voor duidelijkheid en omdat het garandeert dat de stijl meereist met het element wanneer je **append element to body**.

### Hoe zit het met HTML5‑specifieke attributen (bijv. `data-*`)?

`SetAttribute` werkt met elke attribuutnaam, dus je kunt doen:

```csharp
paragraph.SetAttribute("data-id", "12345");
```

### Werkt dit op .NET Core op Linux?

Ja. Aspose.HTML is cross‑platform; zorg er alleen voor dat de native afhankelijkheden geïnstalleerd zijn (`libgdiplus` op sommige distributies) als je later het document naar een afbeelding wilt renderen.

## Conclusie

Je hebt nu een solide, end‑to‑end‑voorbeeld dat **append element to body** gebruikt met Aspose.HTML in C#. We hebben behandeld hoe je **create paragraph element**, **set font weight bold**, **set font family arial**, en **define css font size** kunt doen — allemaal met duidelijke uitleg waarom elke stap belangrijk is.  

Voel je vrij om te experimenteren: verwissel de lettertypefamilie, wijzig de eenheid van de grootte, of voeg meer CSS‑eigenschappen toe zoals `color` of `text-shadow`. Hetzelfde patroon werkt voor andere HTML‑elementen (tabellen, afbeeldingen, SVG's), zodat je deze basis kunt uitbreiden tot volledige documentgeneratoren.

### Volgende stappen

- Verken **Aspose.HTML rendering** om de HTML naar PDF of PNG te converteren.
- Leer hoe je **inject external JavaScript** kunt injecteren voor dynamisch gedrag.
- Combineer deze aanpak met **Razor templates** voor server‑side HTML‑generatie.

Heb je een variatie geprobeerd? Deel het in de reacties, en happy coding!  

<img src="append-element-to-body.png" alt="voorbeeld van element aan body toevoegen" width="600">

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}