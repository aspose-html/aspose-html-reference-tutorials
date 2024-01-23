---
title: Webscrapen in .NET met Aspose.HTML
linktitle: Webscrapen in .NET
second_title: Aspose.HTML .NET HTML-manipulatie-API
description: Leer HTML-documenten manipuleren in .NET met Aspose.HTML. Navigeer, filter, bevraag en selecteer elementen effectief voor verbeterde webontwikkeling.
type: docs
weight: 13
url: /nl/net/advanced-features/web-scraping/
---

In het huidige digitale tijdperk is het manipuleren en extraheren van informatie uit HTML-documenten een veel voorkomende taak voor ontwikkelaars. Aspose.HTML voor .NET is een krachtig hulpmiddel dat HTML-verwerking en -manipulatie in .NET-toepassingen vereenvoudigt. In deze zelfstudie verkennen we verschillende aspecten van Aspose.HTML voor .NET, inclusief vereisten, naamruimten en stapsgewijze voorbeelden, zodat u het volledige potentieel ervan kunt benutten.

## Vereisten

Voordat je in de wereld van Aspose.HTML voor .NET duikt, heb je een aantal vereisten nodig:

1. Ontwikkelomgeving: Zorg ervoor dat u over een werkende ontwikkelomgeving beschikt met Visual Studio of een andere compatibele IDE voor .NET-ontwikkeling.

2.  Aspose.HTML voor .NET: Download en installeer de Aspose.HTML voor .NET-bibliotheek van de[download link](https://releases.aspose.com/html/net/). U kunt kiezen tussen de gratis proefversie of een gelicentieerde versie, afhankelijk van uw behoeften.

3. Basiskennis van HTML: Bekendheid met de HTML-structuur en -elementen is essentieel om Aspose.HTML effectief te gebruiken voor .NET.

## Naamruimten importeren

Om te beginnen moet u de benodigde naamruimten in uw C#-project importeren. Deze naamruimten bieden toegang tot de Aspose.HTML voor .NET-klassen en functionaliteiten:

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.XPath;
using Aspose.Html.Css;
```

Nu aan de vereisten is voldaan en de naamruimten zijn geïmporteerd, gaan we stap voor stap enkele belangrijke voorbeelden opsplitsen om te illustreren hoe u Aspose.HTML voor .NET effectief kunt gebruiken.

## Navigeren door HTML

In dit voorbeeld navigeren we door een HTML-document en krijgen we stap voor stap toegang tot de elementen ervan.

```csharp
public static void NavigateThroughHTML()
{
    // Bereid een HTML-code voor
    var html_code = "<span>Hello</span> <span>World!</span>";
    
    // Initialiseer een document vanuit de voorbereide code
    using (var document = new HTMLDocument(html_code, "."))
    {
        // Verkrijg de verwijzing naar het eerste kind (eerste SPAN) van het LICHAAM
        var element = document.Body.FirstChild;
        Console.WriteLine(element.TextContent); // Uitgang: Hallo

        // Haal de verwijzing naar de witruimte tussen HTML-elementen op
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Uitvoer: ''

        // Haal de verwijzing naar het tweede SPAN-element op
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Uitgang: Wereld!
    }
}
```

 In dit voorbeeld maken we een HTML-document, openen het eerste onderliggende document (a`SPAN` element), de witruimte tussen elementen, en de tweede`SPAN` element, dat de basisnavigatie demonstreert.

## Knooppuntfilters gebruiken

Met knooppuntfilters kunt u selectief specifieke elementen binnen een HTML-document verwerken.

```csharp
public static void NodeFilterUsageExample()
{
    // Bereid een HTML-code voor
    var code = @"
        <p>Hello</p>
        <img src='image1.png'>
        <img src='image2.png'>
        <p>World!</p>";
    
    // Initialiseer een document op basis van de voorbereide code
    using (var document = new HTMLDocument(code, "."))
    {
        // Maak een TreeWalker met een aangepast filter voor afbeeldingselementen
        using (var iterator = document.CreateTreeWalker(document, NodeFilter.SHOW_ALL, new OnlyImageFilter()))
        {
            while (iterator.NextNode() != null)
            {
                var image = (HTMLImageElement)iterator.CurrentNode;
                Console.WriteLine(image.Src);
                // Uitvoer: afbeelding1.png
                // Uitvoer: afbeelding2.png
            }
        }
    }
}
```

 Dit voorbeeld laat zien hoe u een aangepast knooppuntfilter gebruikt om specifieke elementen te extraheren (in dit geval:`IMG` elementen) uit het HTML-document.

## XPath-query's

Met XPath-query's kunt u op basis van specifieke criteria naar elementen in een HTML-document zoeken.

```csharp
public static void XPathQueryUsageExample()
{
    // Bereid een HTML-code voor
    var code = @"
        <div class='happy'>
            <div>
                <span>Hello!</span>
            </div>
        </div>
        <p class='happy'>
            <span>World</span>
        </p>
    ";
    
    // Initialiseer een document op basis van de voorbereide code
    using (var document = new HTMLDocument(code, "."))
    {
        // Evalueer een XPath-expressie om specifieke elementen te selecteren
        var result = document.Evaluate("//*[@class='gelukkig']//span",
                                        document,
                                        null,
                                        XPathResultType.Any,
                                        null);
        
        // Herhaal de resulterende knooppunten
        for (Node node; (node = result.IterateNext()) != null;)
        {
            Console.WriteLine(node.TextContent);
            // Uitgang: Hallo
            // Uitgang: Wereld!
        }
    }
}
```

Dit voorbeeld toont het gebruik van XPath-query's om elementen in het HTML-document te lokaliseren op basis van hun attributen en structuur.

## CSS-kiezers

CSS-selectors bieden een alternatieve manier om elementen in een HTML-document te selecteren, vergelijkbaar met de manier waarop CSS-stylesheets elementen targeten.

```csharp
public static void CSSSelectorUsageExample()
{
    // Bereid een HTML-code voor
    var code = @"
        <div class='happy'>
            <div>
                <span>Hello</span>
            </div>
        </div>
        <p class='happy'>
            <span>World!</span>
        </p>
    ";
    
    // Initialiseer een document op basis van de voorbereide code
    using (var document = new HTMLDocument(code, "."))
    {
        //Gebruik een CSS-selector om elementen te extraheren op basis van klasse en hiërarchie
        var elements = document.QuerySelectorAll(".happy span");
        
        // Herhaal de resulterende lijst met elementen
        foreach (HTMLElement element in elements)
        {
            Console.WriteLine(element.InnerHTML);
            // Uitgang: Hallo
            // Uitgang: Wereld!
        }
    }
}
```

Hier laten we zien hoe u CSS-selectors kunt gebruiken om specifieke elementen in het HTML-document te targeten.

Met deze voorbeelden heeft u een fundamenteel inzicht gekregen in hoe u met Aspose.HTML voor .NET kunt navigeren, filteren, opvragen en selecteren van elementen in HTML-documenten.

## Conclusie

 Aspose.HTML voor .NET is een veelzijdige bibliotheek waarmee .NET-ontwikkelaars efficiënt met HTML-documenten kunnen werken. Met de krachtige functies voor navigatie, filteren, opvragen en selecteren van elementen kunt u verschillende HTML-verwerkingstaken naadloos afhandelen. Door deze tutorial te volgen en de documentatie te verkennen op[Aspose.HTML voor .NET-documentatie](https://reference.aspose.com/html/net/), kunt u het volledige potentieel van deze tool voor uw .NET-applicaties benutten.

## Veelgestelde vragen

### Q1. Is Aspose.HTML voor .NET gratis te gebruiken?

A1: Aspose.HTML voor .NET biedt een gratis proefversie, maar voor productiegebruik moet u een licentie aanschaffen. Licentiegegevens en -opties vindt u op[Aspose.HTML-aankoop](https://purchase.aspose.com/buy).

### Vraag 2. Hoe kan ik een tijdelijke licentie krijgen voor Aspose.HTML voor .NET?

 A2: U kunt een tijdelijke licentie voor testdoeleinden verkrijgen bij[Aspose.HTML Tijdelijke licentie](https://purchase.aspose.com/temporary-license/).

### Q3. Waar kan ik hulp of ondersteuning zoeken voor Aspose.HTML voor .NET?

 A3: Als u problemen ondervindt of vragen heeft, kunt u terecht bij de[Aspose.HTML-forum](https://forum.aspose.com/) voor hulp en gemeenschapsondersteuning.

### Q4. Zijn er aanvullende bronnen voor het leren van Aspose.HTML voor .NET?

 A4: Naast deze zelfstudie kunt u meer zelfstudies en documentatie verkennen over de[Aspose.HTML voor .NET-documentatiepagina](https://reference.aspose.com/html/net/).

### Vraag 5. Is Aspose.HTML voor .NET compatibel met de nieuwste .NET-versies?

A5: Aspose.HTML voor .NET wordt regelmatig bijgewerkt om compatibiliteit met de nieuwste .NET-versies en -technologieën te garanderen.