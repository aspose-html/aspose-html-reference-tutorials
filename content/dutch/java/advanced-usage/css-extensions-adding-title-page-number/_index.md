---
title: Pas HTML-paginamarges aan met Aspose.HTML
linktitle: CSS-extensies - Titel en paginanummer toevoegen
second_title: Java HTML-verwerking met Aspose.HTML
description: Leer hoe u paginamarges kunt aanpassen, paginanummers en titels aan HTML-documenten kunt toevoegen met Aspose.HTML voor Java.
type: docs
weight: 10
url: /nl/java/advanced-usage/css-extensions-adding-title-page-number/
---
Aspose.HTML voor Java is een krachtige bibliotheek voor het verwerken van HTML-documenten in Java-toepassingen. In deze zelfstudie onderzoeken we hoe u aangepaste paginamarges kunt maken en paginanummers en titels aan uw HTML-documenten kunt toevoegen met behulp van Aspose.HTML voor Java. Deze stapsgewijze handleiding verdeelt het proces in beheersbare stappen, zodat u deze functies eenvoudig in uw HTML-documenten kunt integreren.

## Vereisten

Voordat we beginnen, zorg ervoor dat u aan de volgende vereisten voldoet:

1. Java-ontwikkelomgeving: Zorg ervoor dat er een Java-ontwikkelomgeving op uw computer is geïnstalleerd.

2.  Aspose.HTML voor Java: Download en installeer de Aspose.HTML voor Java-bibliotheek van[hier](https://releases.aspose.com/html/java/).

## Pakketten importeren

Om aan de slag te gaan, moet u de benodigde pakketten importeren uit Aspose.HTML voor Java. Voeg de volgende importinstructies toe aan uw Java-code:

```java
// Importeer Aspose.HTML-pakketten
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

Laten we nu het proces van het toevoegen van aangepaste paginamarges, paginanummers en titels in beheersbare stappen opsplitsen:

## Stap 1: Initialiseer de configuratie en paginamarges

```java
// Initialiseer het configuratieobject en stel de paginamarges voor het document in
Configuration configuration = new Configuration();
try {
    // Haal de User Agent-service op
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Stel de stijl van aangepaste marges in en maak er markeringen op
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

In deze stap initialiseren we het configuratieobject en stellen we aangepaste paginamarges in, inclusief de positie van de paginateller en de paginatitel.

## Stap 2: Initialiseer een HTML-document

```java
// Initialiseer een HTML-document
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Hier maken we een HTML-document met een voorbeeldinhoud (in dit geval een 'Hallo wereld'-bericht) en passen we de configuratie uit stap 1 toe.

## Stap 3: Initialiseer een uitvoerapparaat en render het document

```java
// Initialiseer een uitvoerapparaat
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    //Verzend het document naar het uitvoerapparaat
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

In deze stap stellen we een uitvoerapparaat in en renderen we het HTML-document. Het document wordt verwerkt en opgeslagen als een XPS-bestand met de opgegeven paginamarges, paginanummers en titel.

## Conclusie

Gefeliciteerd! U hebt met succes geleerd hoe u aangepaste paginamarges kunt maken en paginanummers en titels aan uw HTML-documenten kunt toevoegen met Aspose.HTML voor Java. Met deze aanpassing kunt u professionelere en visueel aantrekkelijkere documenten maken.

 Als u vragen heeft of problemen ondervindt, kunt u terecht bij de[Aspose.HTML voor Java-documentatie](https://reference.aspose.com/html/java/) of zoek hulp op de[Aspose-ondersteuningsforum](https://forum.aspose.com/).

## Veelgestelde vragen

### V1: Wat is Aspose.HTML voor Java?

A1: Aspose.HTML voor Java is een Java-bibliotheek die krachtige hulpmiddelen biedt voor het werken met HTML-documenten in Java-toepassingen.

### Vraag 2: Kan ik de paginamarges verder aanpassen?

A2: Ja, u kunt de CSS-stijlen in stap 1 wijzigen om de paginamarges aan uw vereisten aan te passen.

### Vraag 3: Hoe kan ik meer inhoud aan het HTML-document toevoegen?

A3: U kunt de HTML-inhoud in stap 2 wijzigen door de voorbeeldinhoud te vervangen door uw eigen inhoud.

### V4: Is Aspose.HTML voor Java compatibel met andere documentformaten?

A4: Ja, Aspose.HTML voor Java kan worden gebruikt om HTML-documenten naar verschillende formaten te converteren, waaronder PDF, XPS en afbeeldingen.

### V5: Heb ik een licentie nodig voor het gebruik van Aspose.HTML voor Java?

 A5: Ja, u kunt een licentie of een gratis proefversie verkrijgen van[hier](https://purchase.aspose.com/buy) of[hier](https://releases.aspose.com/).