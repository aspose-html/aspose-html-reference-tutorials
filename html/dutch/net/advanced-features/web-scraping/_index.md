---
title: Webscraping in .NET met Aspose.HTML
linktitle: Webscraping in .NET
second_title: Aspose.HTML .NET HTML-manipulatie-API
description: Leer HTML-documenten te manipuleren in .NET met Aspose.HTML. Navigeer, filter, query en selecteer elementen effectief voor verbeterde webontwikkeling.
type: docs
weight: 13
url: /nl/net/advanced-features/web-scraping/
---

In het digitale tijdperk van vandaag is het manipuleren en extraheren van informatie uit HTML-documenten een veelvoorkomende taak voor ontwikkelaars. Aspose.HTML voor .NET is een krachtige tool die HTML-verwerking en -manipulatie in .NET-toepassingen vereenvoudigt. In deze tutorial verkennen we verschillende aspecten van Aspose.HTML voor .NET, waaronder vereisten, naamruimten en stapsgewijze voorbeelden om u te helpen het volledige potentieel ervan te benutten.

## Vereisten

Voordat u zich verdiept in de wereld van Aspose.HTML voor .NET, hebt u een aantal vereisten nodig:

1. Ontwikkelomgeving: Zorg ervoor dat u een werkende ontwikkelomgeving hebt ingesteld met Visual Studio of een andere compatibele IDE voor .NET-ontwikkeling.

2.  Aspose.HTML voor .NET: Download en installeer de Aspose.HTML voor .NET-bibliotheek van de[downloadlink](https://releases.aspose.com/html/net/)U kunt kiezen tussen de gratis proefversie of een gelicentieerde versie, afhankelijk van uw behoeften.

3. Basiskennis van HTML: Kennis van de HTML-structuur en -elementen is essentieel om Aspose.HTML voor .NET effectief te kunnen gebruiken.

## Naamruimten importeren

Om te beginnen moet u de benodigde naamruimten importeren in uw C#-project. Deze naamruimten bieden toegang tot de Aspose.HTML voor .NET-klassen en -functionaliteiten:

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.XPath;
using Aspose.Html.Css;
```

Nu de vereisten aanwezig zijn en de naamruimten zijn geïmporteerd, gaan we stap voor stap enkele belangrijke voorbeelden bespreken om te laten zien hoe u Aspose.HTML voor .NET effectief kunt gebruiken.

## Navigeren door HTML

In dit voorbeeld navigeren we door een HTML-document en openen we stap voor stap de elementen ervan.

```csharp
public static void NavigateThroughHTML()
{
    // Maak een HTML-code
    var html_code = "<span>Hello</span> <span>World!</span>";
    
    // Initialiseer een document vanuit de voorbereide code
    using (var document = new HTMLDocument(html_code, "."))
    {
        // Verkrijg de referentie naar het eerste kind (eerste SPAN) van het BODY
        var element = document.Body.FirstChild;
        Console.WriteLine(element.TextContent); // Uitvoer: Hallo

        // Verwijzing naar de witruimte tussen HTML-elementen ophalen
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Uitvoer: ' '

        // Verwijzing naar het tweede SPAN-element ophalen
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Uitvoer: Wereld!
    }
}
```

 In dit voorbeeld maken we een HTML-document, openen we het eerste kind (een`SPAN` element), de witruimte tussen elementen en de tweede`SPAN` element, dat de basisnavigatie demonstreert.

## Nodefilters gebruiken

Met knooppuntfilters kunt u specifieke elementen binnen een HTML-document selectief verwerken.

```csharp
public static void NodeFilterUsageExample()
{
    // Maak een HTML-code
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
                // Uitvoer: image1.png
                // Uitvoer: image2.png
            }
        }
    }
}
```

 Dit voorbeeld laat zien hoe u een aangepast knooppuntfilter kunt gebruiken om specifieke elementen te extraheren (in dit geval`IMG` elementen) uit het HTML-document.

## XPath-query's

Met XPath-query's kunt u op basis van specifieke criteria naar elementen in een HTML-document zoeken.

```csharp
public static void XPathQueryUsageExample()
{
    // Maak een HTML-code
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
        var result = document.Evaluate("//*[@class='happy']//span",
                                        document,
                                        null,
                                        XPathResultType.Any,
                                        null);
        
        // Herhaal de resulterende knooppunten
        for (Node node; (node = result.IterateNext()) != null;)
        {
            Console.WriteLine(node.TextContent);
            // Uitvoer: Hallo
            // Uitvoer: Wereld!
        }
    }
}
```

Dit voorbeeld laat zien hoe XPath-query's worden gebruikt om elementen in het HTML-document te vinden op basis van hun kenmerken en structuur.

## CSS-selectoren

CSS-selectors bieden een alternatieve manier om elementen in een HTML-document te selecteren, vergelijkbaar met de manier waarop CSS-stijlbladen elementen selecteren.

```csharp
public static void CSSSelectorUsageExample()
{
    // Maak een HTML-code
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
            // Uitvoer: Hallo
            // Uitvoer: Wereld!
        }
    }
}
```

Hier laten we zien hoe u CSS-selectors kunt gebruiken om specifieke elementen in het HTML-document te targeten.

Met deze voorbeelden hebt u een basiskennis gekregen over hoe u met Aspose.HTML voor .NET door elementen in HTML-documenten kunt navigeren, deze kunt filteren, opvragen en selecteren.

## Conclusie

 Aspose.HTML voor .NET is een veelzijdige bibliotheek die .NET-ontwikkelaars in staat stelt om efficiënt met HTML-documenten te werken. Met de krachtige functies voor navigatie, filteren, query's en het selecteren van elementen kunt u verschillende HTML-verwerkingstaken naadloos afhandelen. Door deze tutorial te volgen en de documentatie op[Aspose.HTML voor .NET-documentatie](https://reference.aspose.com/html/net/)kunt u het volledige potentieel van deze tool voor uw .NET-toepassingen benutten.

## Veelgestelde vragen

### V1. Is Aspose.HTML voor .NET gratis te gebruiken?

A1: Aspose.HTML voor .NET biedt een gratis proefversie, maar voor productiegebruik moet u een licentie aanschaffen. U kunt licentiedetails en -opties vinden op[Aspose.HTML Aankoop](https://purchase.aspose.com/buy).

### Vraag 2. Hoe kan ik een tijdelijke licentie voor Aspose.HTML voor .NET krijgen?

 A2: U kunt een tijdelijke licentie voor testdoeleinden verkrijgen bij[Aspose.HTML Tijdelijke licentie](https://purchase.aspose.com/temporary-license/).

### Vraag 3. Waar kan ik hulp of ondersteuning krijgen voor Aspose.HTML voor .NET?

 A3: Als u problemen ondervindt of vragen heeft, kunt u terecht op de[Aspose.HTML-forum](https://forum.aspose.com/) voor hulp en ondersteuning van de gemeenschap.

### Vraag 4. Zijn er aanvullende bronnen om Aspose.HTML voor .NET te leren?

 A4: Naast deze tutorial kunt u meer tutorials en documentatie over de[Aspose.HTML voor .NET documentatiepagina](https://reference.aspose.com/html/net/).

### V5. Is Aspose.HTML voor .NET compatibel met de nieuwste .NET-versies?

A5: Aspose.HTML voor .NET wordt regelmatig bijgewerkt om compatibiliteit met de nieuwste .NET-versies en -technologieën te garanderen.