---
title: Een document maken in .NET met Aspose.HTML
linktitle: Een document maken in .NET
second_title: Aspose.HTML .NET HTML-manipulatie-API
description: Ontketen de kracht van Aspose.HTML voor .NET. Leer eenvoudig HTML- en SVG-documenten maken, manipuleren en optimaliseren. Bekijk stapsgewijze voorbeelden en veelgestelde vragen.
weight: 14
url: /nl/net/html-document-manipulation/creating-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Een document maken in .NET met Aspose.HTML


In de steeds veranderende wereld van webontwikkeling is het essentieel om voorop te blijven lopen. Aspose.HTML voor .NET biedt ontwikkelaars een robuuste toolkit om met HTML-documenten te werken. Of u nu helemaal opnieuw begint, laadt vanuit een bestand, haalt uit een URL of SVG-documenten verwerkt, deze bibliotheek biedt de veelzijdigheid die u nodig hebt.

In deze stapsgewijze handleiding duiken we in de basisprincipes van het gebruik van Aspose.HTML voor .NET, zodat u goed bent toegerust om deze krachtige tool in uw webontwikkelingsprojecten te gebruiken. Voordat we in de details duiken, gaan we eerst de vereisten en de benodigde naamruimten doornemen om uw reis te beginnen.

## Vereisten

Om deze tutorial succesvol te kunnen volgen en de kracht van Aspose.HTML voor .NET te benutten, hebt u de volgende vereisten nodig:

- Een Windows-computer met .NET Framework of .NET Core geïnstalleerd.
- Een code-editor zoals Visual Studio.
- Basiskennis van C#-programmering.

Nu u aan de vereisten hebt voldaan, kunnen we beginnen.

## Naamruimten importeren

Voordat u Aspose.HTML voor .NET gaat gebruiken, moet u de benodigde naamruimten importeren. Deze naamruimten bevatten klassen en methoden die essentieel zijn voor het werken met HTML-documenten. Hieronder vindt u een lijst met naamruimten die u moet importeren:

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

Nu u deze naamruimten hebt geïmporteerd, kunt u aan de slag met de stapsgewijze voorbeelden.

## Een HTML-document vanaf nul maken

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

In dit voorbeeld beginnen we met het maken van een leeg HTML-document en voegen we er een "Hello World!"-tekst aan toe. Vervolgens slaan we het document op in een bestand.

## Een HTML-document maken van een bestand

### Stap 1: Maak een 'document.html'-bestand

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### Stap 2: Laden vanuit een 'document.html'-bestand

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Schrijf de documentinhoud naar de uitvoerstream.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Hier bereiden we een bestand voor met "Hello World!"-inhoud en laden het vervolgens als een HTML-document. We printen de inhoud van het document naar de console.

## Een HTML-document maken van een URL

### Stap 1: Laad een document van een webpagina

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    // Schrijf de documentinhoud naar de uitvoerstream.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

In dit voorbeeld laden we een HTML-document rechtstreeks vanaf een webpagina en geven we de inhoud ervan weer.

## Een HTML-document maken van een tekenreeks

### Stap 1: Maak een HTML-code

```csharp
var html_code = "<p>Hello World!</p>";
```

### Stap 2: Initialiseer het document vanuit de tekenreeksvariabele

```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Sla het document op schijf op.
    document.Save("document.html");
}
```

Hier maken we een HTML-document van een tekenreeksvariabele en slaan dit op in een bestand.

## Een HTML-document maken van een MemoryStream

### Stap 1: Een geheugenstroomobject maken

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    // Schrijf de HTML-code in het geheugenobject
    sw.Write("<p>Hello World!</p>");
    // Zet de positie op het begin
    sw.Flush();
    mem.Seek(0, System.IO.SeekOrigin.Begin);
    // Initialiseer document vanuit de geheugenstroom
    using (var document = new Aspose.Html.HTMLDocument(mem, "."))
    {
        // Sla het document op schijf op.
        document.Save("document.html");
    }
}
```

In dit voorbeeld maken we een HTML-document van een geheugenstroom en slaan dit op in een bestand.

## Werken met SVG-documenten

### Stap 1: Initialiseer het SVG-document vanuit een tekenreeks

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "."))
{
    // Schrijf de documentinhoud naar de uitvoerstream.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Hier maken en tonen we een SVG-document van een tekenreeks.

## Een HTML-document asynchroon laden

### Stap 1: Maak het exemplaar van het HTML-document

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Stap 2: Abonneer u op het evenement 'ReadyStateChange'

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    // Controleer de waarde van de eigenschap 'ReadyState'.
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### Stap 3: Navigeer asynchroon op de opgegeven URI

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introductie.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

In dit voorbeeld laden we een HTML-document asynchroon en verwerken we de gebeurtenis 'ReadyStateChange' om de inhoud weer te geven zodra het laden is voltooid.

## Het 'OnLoad'-evenement afhandelen

### Stap 1: Maak het exemplaar van het HTML-document

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Stap 2: Abonneer je op het 'OnLoad'-evenement

```csharp
document.OnLoad += (sender, @event) =>
{
    Console.WriteLine(document.DocumentElement.OuterHTML);
    Console.WriteLine("Loading is completed. Press any key to continue...");
};
```

### Stap 3: Navigeer asynchroon op de opgegeven URI

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introductie.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

Dit voorbeeld laat zien hoe een HTML-document asynchroon wordt geladen en hoe de gebeurtenis 'OnLoad' wordt verwerkt om de inhoud weer te geven zodra het laden is voltooid.

## Tot slot

In de dynamische wereld van webontwikkeling is het cruciaal om de juiste tools tot uw beschikking te hebben. Aspose.HTML voor .NET geeft u de middelen om HTML- en SVG-documenten efficiënt te maken, manipuleren en verwerken. Deze uitgebreide gids heeft u door de basis heen geleid, zodat u de kracht van Aspose.HTML voor .NET in uw projecten kunt benutten.

## Veelgestelde vragen

### V1: Wat is Aspose.HTML voor .NET?

A1: Aspose.HTML voor .NET is een krachtige .NET-bibliotheek waarmee ontwikkelaars met HTML- en SVG-documenten kunnen werken. Het biedt een breed scala aan functies, van het maken van documenten vanaf nul tot het parsen en manipuleren van bestaande HTML- en SVG-bestanden.

### V2: Kan ik Aspose.HTML voor .NET gebruiken met .NET Core?

A2: Ja, Aspose.HTML voor .NET is compatibel met zowel .NET Framework als .NET Core, waardoor het een veelzijdige keuze is voor moderne .NET-toepassingen.

### V3: Is Aspose.HTML voor .NET geschikt voor webscraping en -parsing?

A3: Absoluut! Aspose.HTML voor .NET is een uitstekende keuze voor web scraping en parsing taken, dankzij de mogelijkheid om HTML documenten te laden van URL's en strings. U kunt data extraheren, analyses uitvoeren en meer.

### V4: Hoe krijg ik toegang tot ondersteuning voor Aspose.HTML voor .NET?

 A4: Als u problemen ondervindt of vragen hebt bij het gebruik van Aspose.HTML voor .NET, kunt u de volgende website bezoeken:[Aspose-forum](https://forum.aspose.com/) voor ondersteuning en assistentie van de community en Aspose-experts.

### A5: Waar kan ik gedetailleerde documentatie en downloadopties vinden?

A5: Voor uitgebreide documentatie en toegang tot downloadopties kunt u de volgende links raadplegen:

- [Documentatie](https://reference.aspose.com/html/net/)
- [Download](https://releases.aspose.com/html/net/)
- [Kopen](https://purchase.aspose.com/buy)
- [Gratis proefperiode](https://releases.aspose.com/)
- [Tijdelijke licentie](https://purchase.aspose.com/temporary-license/)
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
