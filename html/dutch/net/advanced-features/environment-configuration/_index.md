---
title: Omgevingsconfiguratie in .NET met Aspose.HTML
linktitle: Omgevingsconfiguratie in .NET
second_title: Aspose.HTML .NET HTML-manipulatie-API
description: Leer hoe u met HTML-documenten in .NET werkt met Aspose.HTML voor taken zoals scriptbeheer, aangepaste stijlen, JavaScript-uitvoeringscontrole en meer. Deze uitgebreide tutorial biedt stapsgewijze voorbeelden en FAQ's om u op weg te helpen.
type: docs
weight: 10
url: /nl/net/advanced-features/environment-configuration/
---

In de digitale wereld van vandaag is het maken en bewerken van HTML-documenten een fundamentele taak voor veel ontwikkelaars. Of u nu een webapplicatie bouwt of HTML naar andere formaten zoals PDF of afbeeldingen wilt converteren, Aspose.HTML voor .NET is een krachtige tool om in uw toolkit te hebben. In deze tutorial verkennen we verschillende aspecten van Aspose.HTML voor .NET, waaronder vereisten, het importeren van naamruimten en stapsgewijze voorbeelden met gedetailleerde uitleg.

## Vereisten

Voordat we Aspose.HTML voor .NET gaan gebruiken, moet u ervoor zorgen dat u aan de volgende vereisten voldoet:

1. Visual Studio: Zorg ervoor dat Visual Studio op uw ontwikkelmachine is geïnstalleerd. Aspose.HTML voor .NET is ontworpen om naadloos te werken met Visual Studio.

2.  Aspose.HTML voor .NET: U kunt de Aspose.HTML voor .NET-bibliotheek downloaden van de website. Gebruik de volgende link om naar de downloadpagina te gaan:[Download Aspose.HTML voor .NET](https://releases.aspose.com/html/net/).

3.  Installatie en licentie: Volg na het downloaden van de bibliotheek de installatie-instructies in de documentatie. Mogelijk hebt u ook een geldige licentie nodig om enkele van de geavanceerde functies te gebruiken. U kunt een licentie verkrijgen via de Aspose-website:[Koop Aspose.HTML-licentie](https://purchase.aspose.com/buy).

4.  Gratis proefversie: Als u Aspose.HTML wilt uitproberen voordat u een licentie aanschaft, kunt u via deze link een gratis proefversie downloaden:[Aspose.HTML gratis proefversie](https://releases.aspose.com/).

Nu u aan de vereiste vereisten voldoet, gaan we door naar de volgende sectie. Hierin importeren we de vereiste naamruimten.

## Naamruimten importeren

Om effectief met Aspose.HTML voor .NET te werken, moet u de juiste namespaces in uw project importeren. Hieronder vindt u de namespaces die u nodig hebt voor de voorbeelden die we zullen behandelen:

```csharp
using Aspose.Html;
using Aspose.Html.Configuration;
using Aspose.Html.Sandbox;
using Aspose.Html.Services;
using Aspose.Html.Saving;
using System;
using System.IO;
```

Nadat u deze naamruimten hebt geïmporteerd, hebt u toegang tot de functionaliteit van Aspose.HTML voor .NET.

## Scriptuitvoering uitschakelen

Laten we beginnen met een basisvoorbeeld van het uitschakelen van scriptuitvoering binnen een HTML-document en het converteren naar een PDF. Volg deze stappen:

1. Maak een HTML-codefragment en sla het op in een bestand met de naam 'document.html'.

```csharp
var code = "<span>Hello World!!</span> " +
           "<script>document.write('Have a nice day!');</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. Initialiseer de Aspose.HTML-configuratie en markeer 'scripts' als een niet-vertrouwde bron.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    configuration.Security |= Aspose.Html.Sandbox.Scripts;
    
    // Initialiseer een HTML-document met de opgegeven configuratie
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Converteer HTML naar PDF
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

In dit voorbeeld hebben we de uitvoering van scripts in het HTML-document voorkomen, waardoor de beveiliging tijdens het converteren naar een PDF gewaarborgd is. Laten we nu doorgaan naar het volgende voorbeeld.

## Specificeer gebruikersstijlblad

Soms wilt u misschien aangepaste stijlen toepassen op elementen in een HTML-document. Hier leest u hoe u dat kunt doen met Aspose.HTML voor .NET:

1. Maak een HTML-codefragment en sla het op in een bestand met de naam 'document.html'.

```csharp
var code = @"<span>Hello World!!!</span>";
System.IO.File.WriteAllText("document.html", code);
```

2.  Stel een aangepaste kleur in voor de`<span>` element met behulp van een gebruikers-stijlblad.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var userAgent = configuration.GetService<Aspose.Html.Services.IUserAgentService>();
    userAgent.UserStyleSheet = "span { color: green; }";
    
    // Initialiseer een HTML-document met de opgegeven configuratie
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Converteer HTML naar PDF
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

 In dit voorbeeld hebben we een aangepaste stijl toegepast op de`<span>` element, waarbij de tekstkleur op groen wordt ingesteld. Met Aspose.HTML voor .NET kunt u stijlen eenvoudig manipuleren.

## JavaScript-uitvoeringstime-out

Bij het omgaan met potentieel tijdrovende JavaScript-code is het essentieel om een time-out in te stellen om onbepaalde uitvoering te voorkomen. Dit is hoe u dat kunt doen:

1. Maak een HTML-codefragment met een eindeloze lus en sla het op in een bestand met de naam 'document.html'.

```csharp
var code = @"<script>while(true){}</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. Stel een JavaScript-uitvoeringstime-out in op 10 seconden.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var runtime = configuration.GetService<Aspose.Html.Services.IRuntimeService>();
    runtime.JavaScriptTimeout = TimeSpan.FromSeconds(10);
    
    // Initialiseer een HTML-document met de opgegeven configuratie
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Wacht tot alle scripts zijn voltooid/geannuleerd en converteer HTML naar PNG
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

In dit voorbeeld hebben we de JavaScript-uitvoeringstijd beperkt tot 10 seconden. Zo voorkomen we dat het script oneindig lang wordt uitgevoerd, wat mogelijk tot prestatieproblemen zou kunnen leiden.

## Aangepaste berichtenhandler

Soms moet u foutmeldingen of ontbrekende bronnen verwerken bij het laden van een HTML-document. Hier is een voorbeeld van hoe u een aangepaste berichthandler maakt:

1. Maak een HTML-codefragment met een ontbrekende afbeeldingsbestandsreferentie en sla het op in een bestand met de naam 'document.html'.

```csharp
var code = @"<img src='missing.jpg'>";
System.IO.File.WriteAllText("document.html", code);
```

2. Voeg een foutmeldingshandler toe aan de netwerkservice om mislukte verzoeken te registreren.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var network = configuration.GetService<Aspose.Html.Services.INetworkService>();
    network.MessageHandlers.Add(new LogMessageHandler());
    
    // Initialiseer een HTML-document met de opgegeven configuratie
    // Tijdens het laden van het document probeert de applicatie de afbeelding te laden. Het resultaat van deze bewerking ziet u in de console.
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Converteer HTML naar PNG
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

In dit voorbeeld hebben we een aangepaste berichtenbehandelaar toegevoegd (`LogMessageHandler`) om informatie over mislukte verzoeken te loggen. Dit kan met name handig zijn voor het debuggen en netjes afhandelen van ontbrekende bronnen.

## Conclusie

Aspose.HTML voor .NET is een veelzijdige bibliotheek waarmee ontwikkelaars efficiënt met HTML-documenten kunnen werken. In deze tutorial hebben we essentiële concepten behandeld en stapsgewijze voorbeelden gegeven voor veelvoorkomende taken, waaronder scriptbeheer, stylesheet-aanpassing, JavaScript-uitvoeringscontrole en aangepaste berichtverwerking.

Door de stappen in deze tutorial te volgen, kunt u de kracht van Aspose.HTML voor .NET benutten om met vertrouwen HTML-documenten in uw .NET-toepassingen te maken, bewerken en converteren.

## Veelgestelde vragen

### V1: Kan ik Aspose.HTML voor .NET gebruiken zonder een licentie aan te schaffen?

A1: Ja, u kunt Aspose.HTML voor .NET gratis uitproberen met een proefversie, maar voor sommige geavanceerde functies is mogelijk een geldige licentie vereist.

### V2: Hoe kan ik een licentie voor Aspose.HTML voor .NET verkrijgen?

 A2: U kunt een licentie kopen via de Aspose-website:[Koop Aspose.HTML-licentie](https://purchase.aspose.com/buy).

### V3: Naar welke formaten kan ik HTML-documenten converteren met Aspose.HTML voor .NET?

A3: Aspose.HTML voor .NET ondersteunt conversie naar verschillende formaten, waaronder PDF, afbeeldingen en meer.

### V4: Bestaat er een community of ondersteuningsforum voor Aspose.HTML voor .NET?

 A4: Ja, u kunt hulp en ondersteuning vinden op de Aspose-forums:[Aspose.HTML Ondersteuningsforum](https://forum.aspose.com/).

### V5: Biedt Aspose.HTML voor .NET documentatie en tutorials?

 A5: Ja, u kunt de documentatie hier vinden:[Aspose.HTML voor .NET-documentatie](https://reference.aspose.com/html/net/).