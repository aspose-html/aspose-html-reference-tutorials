---
title: Pas XPS-paginaformaat aan met Aspose.HTML voor Java
linktitle: XPS-paginaformaat aanpassen
second_title: Java HTML-verwerking met Aspose.HTML
description: Leer hoe u de XPS-paginagrootte aanpast met Aspose.HTML voor Java. Beheer eenvoudig de uitvoerafmetingen van uw XPS-documenten.
type: docs
weight: 16
url: /nl/java/advanced-usage/adjust-xps-page-size/
---

In deze tutorial begeleiden we u door het proces van het aanpassen van de XPS-paginagrootte met behulp van Aspose.HTML voor Java. Met deze krachtige bibliotheek kunt u HTML-documenten manipuleren en ze in verschillende formaten weergeven, waaronder XPS. Het aanpassen van de paginagrootte is essentieel wanneer u de uitvoerafmetingen van uw XPS-document wilt regelen.

## Vereisten

Voordat we beginnen, moet u ervoor zorgen dat aan de volgende voorwaarden is voldaan:

1. Java-ontwikkelomgeving: zorg ervoor dat de Java Development Kit (JDK) op uw systeem is geïnstalleerd.

2.  Aspose.HTML voor Java-bibliotheek: U moet de Aspose.HTML voor Java-bibliotheek downloaden en opnemen in uw Java-project. U kunt de bibliotheek vinden[hier](https://releases.aspose.com/html/java/).

3. Input HTML-bestand: bereid een HTML-bestand voor dat u wilt renderen en pas de XPS-paginagrootte aan. U kunt uw eigen HTML-bestand gebruiken voor deze tutorial.

## Pakketten importeren

Eerst moet u de benodigde pakketten importeren om te werken met Aspose.HTML voor Java. Neem deze pakketten op aan het begin van uw Java-klasse:

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Stap 1: Stel de invoerbestandsnaam in

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

 In deze stap lezen we uw HTML-invoerbestand met behulp van een`FileInputStream`.

## Stap 2: Maak een HTML-document en stel stijlen in

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n";

// ...
```

 Deze stap omvat het maken van een`HTMLDocument` en er stijlen aan toevoegen.

## Stap 3: XPS-renderingopties maken

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

Hier maken we XPS-renderingopties om het renderingproces te configureren.

## Stap 4: Pas de paginagrootte aan

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

In deze stap stelt u het paginaformaat in en geeft u aan of u het formaat wilt aanpassen aan de breedste pagina.

## Stap 5: De uitvoer renderen

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

In de laatste stap renderen we de XPS-uitvoer met behulp van de geconfigureerde opties.

## Conclusie

In deze tutorial hebben we je laten zien hoe je de XPS-paginagrootte aanpast met Aspose.HTML voor Java. Je kunt de uitvoerafmetingen van je XPS-documenten beheren en ervoor zorgen dat ze voldoen aan je specifieke vereisten. Met de meegeleverde code en stappen kun je deze functie eenvoudig implementeren in je Java-toepassingen.

 Als u vragen heeft of verdere hulp nodig heeft, kunt u gerust een bezoek brengen aan de[Aspose.HTML voor Java-documentatie](https://reference.aspose.com/html/java/) of vraag om hulp op de[Aspose-forum](https://forum.aspose.com/).

## Veelgestelde vragen

### V1: Wat is Aspose.HTML voor Java?

A1: Aspose.HTML voor Java is een Java-bibliotheek waarmee ontwikkelaars HTML-documenten kunnen bewerken en converteren naar verschillende formaten, zoals XPS, PDF en afbeeldingen.

### V2: Waar kan ik Aspose.HTML voor Java downloaden?

 A2: U kunt de Aspose.HTML voor Java-bibliotheek downloaden van[deze link](https://releases.aspose.com/html/java/).

### V3: Is er een gratis proefversie beschikbaar voor Aspose.HTML voor Java?

 A3: Ja, u kunt een gratis proefversie van Aspose.HTML voor Java krijgen van[hier](https://releases.aspose.com/).

### V4: Hoe kan ik een tijdelijke licentie voor Aspose.HTML voor Java verkrijgen?

 A4: Om een tijdelijke licentie voor Aspose.HTML voor Java te krijgen, bezoek[deze pagina](https://purchase.aspose.com/temporary-license/).

### V5: Kan ik ondersteuning krijgen voor Aspose.HTML voor Java?

 A5: Ja, u kunt hulp en ondersteuning zoeken bij de Aspose-community op de[Aspose-forum](https://forum.aspose.com/).