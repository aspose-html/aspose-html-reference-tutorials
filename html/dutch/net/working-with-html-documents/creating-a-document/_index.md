---
title: Een HTML-document maken in .NET met Aspose.HTML
linktitle: Een HTML-document maken in .NET
second_title: Aspose.HTML .NET HTML-manipulatie-API
description: Leer hoe u HTML-documenten in .NET maakt met Aspose.HTML, vanaf nul of vanaf URL's. Een uitgebreide tutorial voor webontwikkelaars.
type: docs
weight: 10
url: /nl/net/working-with-html-documents/creating-a-document/
---

Op het gebied van webontwikkeling en datamanipulatie is een krachtige tool om HTML-documenten te maken, te wijzigen en ermee te werken onmisbaar. Aspose.HTML voor .NET is zo'n tool die uw HTML-gerelateerde taken kan vereenvoudigen. In deze uitgebreide tutorial gaan we stap voor stap bekijken hoe u HTML-documenten kunt maken met Aspose.HTML voor .NET. Voordat we in de voorbeelden duiken, bespreken we eerst enkele vereisten.

## Vereisten

Voordat u aan deze reis begint, moet u ervoor zorgen dat u aan de volgende voorwaarden voldoet:

1. Visual Studio: Zorg ervoor dat Visual Studio op uw systeem is geïnstalleerd.

2. Aspose.HTML voor .NET: Download en installeer de Aspose.HTML voor .NET-bibliotheek. U kunt de downloadlink vinden[hier](https://releases.aspose.com/html/net/).

3. Basiskennis van C#: Maak uzelf vertrouwd met de basisprincipes van de programmeertaal C#.

Nu we de vereisten onder de knie hebben, kunnen we beginnen met het maken van HTML-documenten.

## Naamruimten importeren

Ten eerste moet u de benodigde namespaces importeren om Aspose.HTML in uw C#-project te gebruiken. Voeg de volgende using-directives toe aan uw codebestand:

```csharp
using Aspose.Html.Dom.Svg;
using Aspose.Html;
```

## Een SVG-document maken

```csharp
static void CreateSVG()
{
    using (var document = new SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "about:blank"))
    {
        // Voer hier acties uit op het SVG-document...
    }
}
```

 In dit voorbeeld maken we een SVG-document door de SVG-inhoud en een basis-URL op te geven.`SVGDocument` klasse van Aspose.HTML voor .NET waarmee u moeiteloos SVG-documenten kunt bewerken.

## Een HTML-document vanaf nul maken

```csharp
static void FromScratch()
{
    using (var document = new HTMLDocument())
    {
        // Voer hier acties uit op het HTML-document...
    }
}
```

 Dit voorbeeld laat zien hoe u een HTML-document vanaf nul kunt maken.`HTMLDocument`klasse biedt een leeg canvas voor uw HTML-inhoud.

## Een HTML-document maken van een lokaal bestand

```csharp
static void FromLocalFile()
{
    string dataDir = "Your Data Directory";
    using (var document = new HTMLDocument(dataDir + "input.html"))
    {
        // Voer hier acties uit op het HTML-document...
    }
}
```

 Als u een bestaand HTML-bestand op uw lokale systeem hebt, kunt u dit laden met behulp van de`HTMLDocument` klasse, zoals in dit voorbeeld wordt getoond.

## Een HTML-document maken vanaf een externe URL

```csharp
static void FromRemoteURL()
{
    using (var document = new HTMLDocument("http://uw.site.com/"))
    {
        // Voer hier acties uit op het HTML-document...
    }
}
```

Soms moet u mogelijk werken met HTML-inhoud die op een externe server wordt gehost. Dit voorbeeld laat zien hoe u een HTML-document maakt vanaf een externe URL.

## Een HTML-document maken vanaf een externe URL (alternatief)

```csharp
static void FromRemoteURL1()
{
    using (var document = new HTMLDocument(new Url("http://uw.site.com/")))
    {
        // Voer hier acties uit op het HTML-document...
    }
}
```

Deze alternatieve aanpak laat ook zien hoe u een HTML-document kunt maken van een externe URL met behulp van een andere constructor.

## Een HTML-document maken van HTML-inhoud

```csharp
static void FromHTML()
{
    using (var document = new HTMLDocument("<p>my first paragraph</p>", "."))
    {
        // Voer hier acties uit op het HTML-document...
    }
}
```

Als u HTML-inhoud in een tekenreeksindeling hebt, kunt u er een HTML-document mee maken, zoals in dit voorbeeld wordt gedemonstreerd.

## Een HTML-document maken van een stream

```csharp
static void FromStream()
{
    using (MemoryStream mem = new MemoryStream())
    using (StreamWriter sw = new StreamWriter(mem))
    {
        sw.Write("<p>my first paragraph</p>");
        sw.Flush();
        mem.Seek(0, SeekOrigin.Begin);
        using (var document = new HTMLDocument(mem, "about:blank"))
        {
            // Voer hier acties uit op het HTML-document...
        }
    }
}
```

In dit voorbeeld laten we zien hoe u een HTML-document maakt van gegevens in een geheugenstroom. Dit kan handig zijn als u HTML-inhoud in een stroom hebt en deze wilt manipuleren.

## Conclusie

Aspose.HTML voor .NET biedt een krachtige set tools voor het maken en werken met HTML-documenten in uw .NET-toepassingen. Met de voorbeelden in deze tutorial kunt u eenvoudig aan de slag met het maken van HTML-documenten, of u nu helemaal opnieuw begint, lokale bestanden, externe URL's of bestaande HTML-inhoud gebruikt.

 Heeft u vragen of hulp nodig? Bezoek het Aspose.HTML community forum voor ondersteuning op[https://forum.aspose.com/](https://forum.aspose.com/).

## Veelgestelde vragen

### V1: Is Aspose.HTML voor .NET gratis te gebruiken?
 A1: Aspose.HTML voor .NET biedt een gratis proefversie, maar voor volledig gebruik moet u een licentie aanschaffen. Meer informatie vindt u op[https://purchase.aspose.com/buy](https://purchase.aspose.com/buy).

### V2: Hoe kan ik een tijdelijke licentie voor Aspose.HTML voor .NET krijgen?
 A2: Als u een tijdelijk rijbewijs nodig hebt, kunt u dit verkrijgen bij[https://purchase.aspose.com/temporary-license/](https://purchase.aspose.com/temporary-license/).

### V3: Waar kan ik documentatie vinden voor Aspose.HTML voor .NET?
A3: De documentatie is te vinden op[https://reference.aspose.com/html/net/](https://reference.aspose.com/html/net/).

### V4: Zijn er nog andere Aspose-bibliotheken voor .NET-ontwikkeling?
 A4: Ja, Aspose biedt een reeks bibliotheken voor verschillende bestandsformaten en documentmanipulatietaken. Bekijk hun aanbod op[https://products.aspose.com/](https://products.aspose.com/).

### V5: Kan ik Aspose.HTML voor .NET gebruiken in mijn webapplicaties?
A5: Ja, Aspose.HTML voor .NET is compatibel met webapplicaties, waardoor het een veelzijdige keuze is voor zowel desktop- als webgebaseerde projecten.
