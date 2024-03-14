---
title: Een document maken in .NET met Aspose.HTML
linktitle: Een document maken in .NET
second_title: Aspose.HTML .NET HTML-manipulatie-API
description: Ontketen de kracht van Aspose.HTML voor .NET. Leer eenvoudig HTML- en SVG-documenten maken, manipuleren en optimaliseren. Ontdek stapsgewijze voorbeelden en veelgestelde vragen.
type: docs
weight: 14
url: /nl/net/html-document-manipulation/creating-a-document/
---

In de steeds evoluerende wereld van webontwikkeling is het essentieel om voorop te blijven lopen. Aspose.HTML voor .NET biedt ontwikkelaars een robuuste toolkit om met HTML-documenten te werken. Of u nu helemaal opnieuw begint, vanuit een bestand laadt, een URL ophaalt of SVG-documenten verwerkt, deze bibliotheek biedt de veelzijdigheid die u nodig heeft.

In deze stapsgewijze handleiding gaan we dieper in op de basisbeginselen van het gebruik van Aspose.HTML voor .NET, zodat u goed toegerust bent om deze krachtige tool in uw webontwikkelingsprojecten te gebruiken. Voordat we ingaan op de details, laten we eerst de vereisten en de benodigde naamruimten doornemen om uw reis een vliegende start te geven.

## Vereisten

Om deze tutorial succesvol te volgen en de kracht van Aspose.HTML voor .NET te benutten, heb je de volgende vereisten nodig:

- Een Windows-machine waarop .NET Framework of .NET Core is geïnstalleerd.
- Een code-editor zoals Visual Studio.
- Basiskennis van programmeren in C#.

Nu u over de vereisten beschikt, gaan we aan de slag.

## Naamruimten importeren

Voordat u Aspose.HTML voor .NET gaat gebruiken, moet u de benodigde naamruimten importeren. Deze naamruimten bevatten klassen en methoden die essentieel zijn voor het werken met HTML-documenten. Hieronder vindt u een lijst met naamruimten die u moet importeren:

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

Nu deze naamruimten zijn geïmporteerd, bent u nu klaar om in de stapsgewijze voorbeelden te duiken.

## Een HTML-document maken vanuit het niets

### Stap 1: Initialiseer een leeg HTML-document

```csharp
// Initialiseer een leeg HTML-document.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Maak een tekstelement en voeg het toe aan het document
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Sla het document op schijf op.
    document.Save("document.html");
}
```

In dit voorbeeld beginnen we met het maken van een leeg HTML-document en het toevoegen van een "Hallo wereld!" tekst ernaar. Vervolgens slaan we het document op in een bestand.

## Een HTML-document maken van een bestand

### Stap 1: Bereid een 'document.html'-bestand voor

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### Stap 2: Laden vanuit een 'document.html'-bestand

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Schrijf de documentinhoud naar de uitvoerstroom.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Hier bereiden we een bestand voor met "Hallo wereld!" inhoud en laad deze vervolgens als een HTML-document. We drukken de inhoud van het document af naar de console.

## Een HTML-document maken op basis van een URL

### Stap 1: Laad een document van een webpagina

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    // Schrijf de documentinhoud naar de uitvoerstroom.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

In dit voorbeeld laden we een HTML-document rechtstreeks vanaf een webpagina en geven we de inhoud ervan weer.

## Een HTML-document maken van een string

### Stap 1: Bereid een HTML-code voor

```csharp
var html_code = "<p>Hello World!</p>";
```

### Stap 2: Initialiseer het document vanuit de stringvariabele

```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Sla het document op schijf op.
    document.Save("document.html");
}
```

Hier maken we een HTML-document van een stringvariabele en slaan dit op in een bestand.

## Een HTML-document maken vanuit een MemoryStream

### Stap 1: Maak een geheugenstroomobject

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    // Schrijf de HTML-code in het geheugenobject
    sw.Write("<p>Hello World!</p>");
    // Stel de positie in op het begin
    sw.Flush();
    mem.Seek(0, System.IO.SeekOrigin.Begin);
    // Initialiseer het document vanuit de geheugenstroom
    using (var document = new Aspose.Html.HTMLDocument(mem, "."))
    {
        // Sla het document op schijf op.
        document.Save("document.html");
    }
}
```

In dit voorbeeld maken we een HTML-document uit een geheugenstroom en slaan dit op in een bestand.

## Werken met SVG-documenten

### Stap 1: Initialiseer het SVG-document vanuit een tekenreeks

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "."))
{
    // Schrijf de documentinhoud naar de uitvoerstroom.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Hier maken en tonen we een SVG-document uit een string.

## Een HTML-document asynchroon laden

### Stap 1: Maak het exemplaar van HTML-document

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Stap 2: Abonneer u op de gebeurtenis 'ReadyStateChange'

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    //Controleer de waarde van de eigenschap 'ReadyState'.
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### Stap 3: Navigeer asynchroon naar de opgegeven Uri

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introductie.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

In dit voorbeeld laden we een HTML-document asynchroon en verwerken we de gebeurtenis 'ReadyStateChange' om de inhoud weer te geven wanneer het laden is voltooid.

## Het afhandelen van de 'OnLoad'-gebeurtenis

### Stap 1: Maak het exemplaar van HTML-document

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Stap 2: Abonneer u op het 'OnLoad'-evenement

```csharp
document.OnLoad += (sender, @event) =>
{
    Console.WriteLine(document.DocumentElement.OuterHTML);
    Console.WriteLine("Loading is completed. Press any key to continue...");
};
```

### Stap 3: Navigeer asynchroon naar de opgegeven Uri

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introductie.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

Dit voorbeeld demonstreert het asynchroon laden van een HTML-document en het afhandelen van de gebeurtenis 'OnLoad' om de inhoud na voltooiing weer te geven.

## Ten slotte

In de dynamische wereld van webontwikkeling is het van cruciaal belang dat u over de juiste tools beschikt. Aspose.HTML voor .NET geeft u de middelen om HTML- en SVG-documenten efficiënt te creëren, manipuleren en verwerken. Deze uitgebreide gids leidt u door de essentiële zaken, zodat u de kracht van Aspose.HTML voor .NET in uw projecten kunt benutten.

## Veelgestelde vragen

### V1: Wat is Aspose.HTML voor .NET?

A1: Aspose.HTML voor .NET is een krachtige .NET-bibliotheek waarmee ontwikkelaars met HTML- en SVG-documenten kunnen werken. Het biedt een breed scala aan functies, van het helemaal opnieuw maken van documenten tot het parseren en manipuleren van bestaande HTML- en SVG-bestanden.

### V2: Kan ik Aspose.HTML gebruiken voor .NET met .NET Core?

A2: Ja, Aspose.HTML voor .NET is compatibel met zowel .NET Framework als .NET Core, waardoor het een veelzijdige keuze is voor moderne .NET-toepassingen.

### V3: Is Aspose.HTML voor .NET geschikt voor webscraping en parsing?

A3: Absoluut! Aspose.HTML voor .NET is een uitstekende keuze voor webscraping- en parseringstaken, dankzij de mogelijkheid om HTML-documenten te laden vanuit URL's en tekenreeksen. U kunt gegevens extraheren, analyses uitvoeren en meer.

### V4: Hoe krijg ik toegang tot ondersteuning voor Aspose.HTML voor .NET?

 A4: Als u problemen ondervindt of vragen hebt tijdens het gebruik van Aspose.HTML voor .NET, kunt u terecht op de[Aspose-forum](https://forum.aspose.com/) voor ondersteuning en hulp van de gemeenschap en Aspose-experts.

### A5: Waar kan ik gedetailleerde documentatie en downloadopties vinden?

A5: Voor uitgebreide documentatie en toegang tot downloadopties kunt u de volgende links raadplegen:

- [Documentatie](https://reference.aspose.com/html/net/)
- [Downloaden](https://releases.aspose.com/html/net/)
- [Kopen](https://purchase.aspose.com/buy)
- [Gratis proefperiode](https://releases.aspose.com/)
- [Tijdelijke licentie](https://purchase.aspose.com/temporary-license/)