---
title: Een document opslaan in .NET met Aspose.HTML
linktitle: Een document opslaan in .NET
second_title: Aspose.HTML .NET HTML-manipulatie-API
description: Ontgrendel de kracht van Aspose.HTML voor .NET met onze stapsgewijze handleiding. Leer HTML- en SVG-documenten te maken, te bewerken en te converteren.
type: docs
weight: 16
url: /nl/net/html-document-manipulation/saving-a-document/
---

In het digitale tijdperk van vandaag is het maken en bewerken van HTML- en SVG-documenten essentieel voor veel softwareontwikkelaars en bedrijven. Aspose.HTML voor .NET is een krachtige bibliotheek die deze taken vereenvoudigt en verschillende functionaliteiten biedt om met HTML, SVG en meer te werken. In deze uitgebreide gids duiken we in de basisprincipes van Aspose.HTML voor .NET, waarbij we elk voorbeeld opsplitsen in eenvoudig te volgen stappen. Of u nu een doorgewinterde ontwikkelaar bent of net begint, u zult deze gids van onschatbare waarde vinden voor het benutten van de mogelijkheden van Aspose.HTML.

## Vereisten

Voordat we aan deze reis beginnen, willen we er zeker van zijn dat u alles heeft wat u nodig hebt:

- Ontwikkelomgeving: Zorg ervoor dat Visual Studio of een andere .NET-ontwikkelomgeving op uw computer is geïnstalleerd.

- Aspose.HTML voor .NET: U moet de Aspose.HTML voor .NET-bibliotheek verkrijgen. U kunt deze downloaden van[hier](https://releases.aspose.com/html/net/).

- Kennis van C#: Kennis van de programmeertaal C# is nuttig, maar niet verplicht. Deze gids is ontworpen om beginnersvriendelijk te zijn.

## Naamruimte importeren

Om Aspose.HTML voor .NET te gaan gebruiken, moet u de benodigde namespaces importeren in uw project. Neem de volgende namespace op in uw C#-code:

### Stap 1: Importeer Aspose.HTML-naamruimte
```csharp
using Aspose.Html;
```

Met deze naamruimte krijgt u toegang tot diverse HTML- en SVG-manipulatiemogelijkheden.

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

In dit voorbeeld maken we een HTML-document en voegen er een simpele "Hello World!"-tekst aan toe. Vervolgens slaan we de HTML op in een bestand op de schijf.

## HTML zonder gekoppeld bestand

### Stap 1: Maak een eenvoudig HTML-bestand
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Hier maken we een eenvoudig HTML-bestand met een ankerlink naar een ander bestand.

### Stap 2: Laad 'document.html' in het geheugen
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Instantie voor opties opslaan maken
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    //Stel de maximale verwerkingsdiepte in op 0 om gekoppelde HTML-bestanden af te snijden.
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    // Sla het document op
    document.Save(@".\html-to-file-example\document.html", options);
}
```

In dit voorbeeld laden we een HTML-document in het geheugen, stellen we de maximale verwerkingsdiepte in om gekoppelde bestanden af te snijden en slaan we het document op. 

## HTML naar MHTML

### Stap 1: Maak een eenvoudig HTML-bestand
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Net als in Voorbeeld 2 maken we een eenvoudig HTML-bestand met een ankerlink naar een ander bestand.

### Stap 2: Laad 'document.html' in het geheugen en sla het op als MHTML
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Sla het document op als MHTML
    document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
}
```

Hier laden we het HTML-document in het geheugen en slaan het op in MHTML-formaat.

## HTML naar Markdown

### Stap 1: Een HTML-code voorbereiden
```csharp
var html_code = "<H2>Hello World!</H2>";
```

 In deze stap definiëren we een HTML-codefragment met een`<H2>` element.

### Stap 2: Initialiseer het document vanuit HTML-code en sla het op als Markdown
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Sla het document op als een Markdown-bestand.
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

We maken een HTML-document van het codefragment en slaan het op als een Markdown-bestand.

## SVG naar bestand

### Stap 1: Een SVG-code voorbereiden
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

In deze stap maken we een SVG-document van de code en slaan dit op als SVG-bestand.

## Conclusie

Aspose.HTML voor .NET is een veelzijdige bibliotheek die HTML- en SVG-documentverwerking in uw .NET-toepassingen vereenvoudigt. In deze handleiding hebben we vijf essentiële voorbeelden behandeld, elk opgesplitst in stapsgewijze instructies. Of u nu documenten maakt, bewerkt of converteert, Aspose.HTML heeft alles wat u nodig hebt. Door deze stappen te volgen, bent u goed op weg om deze krachtige tool onder de knie te krijgen.

## Veelgestelde vragen

### V1: Wat is Aspose.HTML voor .NET?

A1: Aspose.HTML voor .NET is een .NET-bibliotheek die een breed scala aan functies biedt voor het werken met HTML- en SVG-documenten, waaronder het maken, bewerken en converteren ervan.

### V2: Waar kan ik Aspose.HTML voor .NET downloaden?

 A2: U kunt Aspose.HTML voor .NET downloaden van[hier](https://releases.aspose.com/html/net/).

### V3: Is Aspose.HTML voor .NET geschikt voor beginners?

A3: Ja, Aspose.HTML voor .NET kan worden gebruikt door zowel beginners als ervaren ontwikkelaars. De voorbeelden in deze gids zijn ontworpen om beginnersvriendelijk te zijn.

### V4: Kan ik HTML naar andere formaten converteren met Aspose.HTML voor .NET?

A4: Ja, Aspose.HTML voor .NET ondersteunt conversie naar verschillende formaten, waaronder MHTML en Markdown, zoals in de voorbeelden wordt getoond.

### V5: Waar kan ik ondersteuning krijgen voor Aspose.HTML voor .NET?

 A5: U kunt ondersteuning en antwoorden op uw vragen vinden in het Aspose.HTML communityforum[hier](https://forum.aspose.com/).