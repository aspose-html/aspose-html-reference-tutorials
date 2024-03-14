---
title: Een document opslaan in .NET met Aspose.HTML
linktitle: Een document opslaan in .NET
second_title: Aspose.HTML .NET HTML-manipulatie-API
description: Ontgrendel de kracht van Aspose.HTML voor .NET met onze stapsgewijze handleiding. Leer HTML- en SVG-documenten maken, manipuleren en converteren
type: docs
weight: 16
url: /nl/net/html-document-manipulation/saving-a-document/
---

In het huidige digitale tijdperk is het maken en manipuleren van HTML- en SVG-documenten essentieel voor veel softwareontwikkelaars en bedrijven. Aspose.HTML voor .NET is een krachtige bibliotheek die deze taken vereenvoudigt en verschillende functionaliteiten biedt om met HTML, SVG en meer te werken. In deze uitgebreide handleiding duiken we in de essentie van Aspose.HTML voor .NET, waarbij we elk voorbeeld opsplitsen in eenvoudig te volgen stappen. Of u nu een doorgewinterde ontwikkelaar bent of net begint, u zult deze handleiding van onschatbare waarde vinden als u de mogelijkheden van Aspose.HTML wilt benutten.

## Vereisten

Voordat we aan deze reis beginnen, zorgen we ervoor dat u over alles beschikt wat u nodig heeft:

- Ontwikkelomgeving: Zorg ervoor dat Visual Studio of een andere .NET-ontwikkelomgeving op uw computer is geïnstalleerd.

- Aspose.HTML voor .NET: U hebt de Aspose.HTML voor .NET-bibliotheek nodig. Je kunt het downloaden van[hier](https://releases.aspose.com/html/net/).

- Kennis van C#: Bekendheid met de programmeertaal C# is nuttig maar niet verplicht. Deze handleiding is ontworpen om beginnersvriendelijk te zijn.

## Naamruimte importeren

Om Aspose.HTML voor .NET te gaan gebruiken, moet u de benodigde naamruimten in uw project importeren. Neem in uw C#-code de volgende naamruimte op:

### Stap 1: Aspose.HTML-naamruimte importeren
```csharp
using Aspose.Html;
```

Deze naamruimte geeft u toegang tot verschillende HTML- en SVG-manipulatiemogelijkheden.

## HTML naar bestand

### Stap 1: Initialiseer een leeg HTML-document
```csharp
// Initialiseer een leeg HTML-document.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Maak een tekstelement en voeg het toe aan het document
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Sla de HTML op in het bestand op schijf.
    document.Save("document.html");
}
```

In dit voorbeeld maken we een HTML-document en voegen we een eenvoudige "Hallo wereld!" tekst ernaar. Vervolgens slaan we de HTML op in een bestand op de schijf.

## HTML zonder gekoppeld bestand

### Stap 1: bereid een eenvoudig HTML-bestand voor
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Hier maken we een eenvoudig HTML-bestand met een ankerlink naar een ander bestand.

### Stap 2: Laad 'document.html' in het geheugen
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Maak een exemplaar van Save Options
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    //Stel de maximale verwerkingsdiepte in op 0 om gekoppelde HTML-bestanden af te snijden.
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    // Bewaar het document
    document.Save(@".\html-to-file-example\document.html", options);
}
```

In dit voorbeeld laden we een HTML-document in het geheugen, stellen we de maximale verwerkingsdiepte in om gekoppelde bestanden af te snijden en slaan we het document op. 

## HTML naar MHTML

### Stap 1: bereid een eenvoudig HTML-bestand voor
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Net als in voorbeeld 2 maken we een eenvoudig HTML-bestand met een ankerlink naar een ander bestand.

### Stap 2: Laad 'document.html' in het geheugen en sla het op als MHTML
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Sla het document op als MHTML
    document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
}
```

Hier laden we het HTML-document in het geheugen en slaan het op in MHTML-indeling.

## HTML naar Markdown

### Stap 1: Bereid een HTML-code voor
```csharp
var html_code = "<H2>Hello World!</H2>";
```

 In deze stap definiëren we een HTML-codefragment met daarin een`<H2>` element.

### Stap 2: Initialiseer het document vanuit HTML-code en sla het op als Markdown
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Sla het document op als een Markdown-bestand.
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

We maken een HTML-document van het codefragment en slaan dit op als een Markdown-bestand.

## SVG naar bestand

### Stap 1: Bereid een SVG-code voor
```csharp
var code = @"
    <svg xmlns='http://www.w3.org/2000/svg' hoogte='80' breedte='300'>
        <g fill='none'>
            <path stroke='red' d='M5 20 l215 0' />
            <path stroke='black' d='M5 40 l215 0' />
            <path stroke='blue' d='M5 60 l215 0' />
        </g>
    </svg>";
```

Hier maken we een SVG-code die een eenvoudige, kleurrijke afbeelding tekent.

### Stap 2: Initialiseer een SVG-document vanuit de code en sla het op schijf op
```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument(code, "."))
{
    // Sla het SVG-bestand op de schijf op
    document.Save("document.svg");
}
```

In deze stap maken we van de code een SVG-document en slaan dit op als een SVG-bestand.

## Conclusie

Aspose.HTML voor .NET is een veelzijdige bibliotheek die de verwerking van HTML- en SVG-documenten in uw .NET-toepassingen vereenvoudigt. In deze handleiding hebben we vijf essentiële voorbeelden besproken, die we allemaal hebben opgesplitst in stapsgewijze instructies. Of u nu documenten maakt, manipuleert of converteert, Aspose.HTML staat voor u klaar. Door deze stappen te volgen, bent u goed op weg om deze krachtige tool onder de knie te krijgen.

## Veelgestelde vragen

### V1: Wat is Aspose.HTML voor .NET?

A1: Aspose.HTML voor .NET is een .NET-bibliotheek die een breed scala aan functies biedt voor het werken met HTML- en SVG-documenten, inclusief creatie, manipulatie en conversie.

### V2: Waar kan ik Aspose.HTML voor .NET downloaden?

 A2: U kunt Aspose.HTML voor .NET downloaden van[hier](https://releases.aspose.com/html/net/).

### V3: Is Aspose.HTML voor .NET geschikt voor beginners?

A3: Ja, Aspose.HTML voor .NET kan worden gebruikt door zowel beginners als ervaren ontwikkelaars. De voorbeelden in deze handleiding zijn ontworpen om beginnersvriendelijk te zijn.

### V4: Kan ik HTML naar andere formaten converteren met Aspose.HTML voor .NET?

A4: Ja, Aspose.HTML voor .NET ondersteunt conversie naar verschillende formaten, waaronder MHTML en Markdown, zoals weergegeven in de voorbeelden.

### V5: Waar kan ik ondersteuning krijgen voor Aspose.HTML voor .NET?

 A5: U kunt ondersteuning en antwoorden op uw vragen vinden op het Aspose.HTML-communityforum[hier](https://forum.aspose.com/).