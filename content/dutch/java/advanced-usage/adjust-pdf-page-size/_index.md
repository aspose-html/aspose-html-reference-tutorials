---
title: Pas het PDF-paginaformaat aan met Aspose.HTML voor Java
linktitle: PDF-paginaformaat aanpassen
second_title: Java HTML-verwerking met Aspose.HTML
description: Leer hoe u het paginaformaat van een PDF kunt aanpassen met Aspose.HTML voor Java. Maak moeiteloos hoogwaardige PDF's van HTML. Beheer pagina-afmetingen effectief.
type: docs
weight: 15
url: /nl/java/advanced-usage/adjust-pdf-page-size/
---

In het huidige digitale tijdperk wordt de behoefte aan het genereren van hoogwaardige PDF's uit HTML-inhoud steeds groter. Aspose.HTML voor Java is een krachtige Java-bibliotheek waarmee u HTML-documenten moeiteloos naar PDF-indeling kunt converteren. In deze zelfstudie concentreren we ons op het aanpassen van de paginagrootte bij het converteren van HTML naar PDF met Aspose.HTML voor Java.

## Vereisten

Voordat u begint, moet u ervoor zorgen dat u aan de volgende vereisten voldoet:

- Java-ontwikkelomgeving: Zorg ervoor dat Java Development Kit (JDK) op uw systeem is geïnstalleerd.
-  Aspose.HTML voor Java: u moet Aspose.HTML voor Java downloaden en installeren vanaf de website[hier](https://releases.aspose.com/html/java/).
- HTML-document: U moet een HTML-document gereed hebben voor conversie. Als dit niet het geval is, maakt u er een of gebruikt u een bestaand HTML-bestand.

## Pakketten importeren

Om te beginnen moet u de benodigde pakketten importeren om met Aspose.HTML voor Java te kunnen werken. Het volgende codefragment laat zien hoe u dit doet:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

Nu u aan de vereisten voldoet en de benodigde pakketten hebt geïmporteerd, gaan we het proces van het aanpassen van de PDF-paginagrootte in meerdere stappen opsplitsen:

## Stap 1: HTML-inhoud lezen

Eerst moet u de HTML-inhoud lezen die u naar PDF wilt converteren. In dit voorbeeld lezen we de HTML uit een bestand met de naam 'FirstFile.html'.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## Stap 2: HTML-inhoud schrijven

Vervolgens schrijft u de HTML-inhoud naar een bestand met de naam 'FirstFileOut.html'.

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Voeg hier aangepaste HTML-stijlen of inhoud toe
    String style = "<style>\n" +
                   ".st\n" +
                   "{\n" +
                   "color:\n" +
                   "green;\n" +
                   "}\n" +
                   "</style >\n" +
                   "<div id = id1 > Aspose.Html rendering Text in Black Color</div >\n" +
                   "<div id = id2 class='' st '' > Aspose.Html rendering Text in Green Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: blue;' > Aspose.Html rendering Text in Blue Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: red;' ><font face = 'Arial' > Aspose.Html rendering Text in Red\n" +
                   "Color</font ></div >\n";
    fileOutputStream.write(style.getBytes(java.nio.charset.StandardCharsets.UTF_8));
}
```

## Stap 3: HTML naar PDF renderen

Nu gaat u de HTML-inhoud naar een PDF-bestand renderen. We behandelen twee scenario's: één waarbij het paginaformaat niet wordt aangepast aan de breedte van de inhoud, en een ander waarbij het wel wordt aangepast.

### Paginaformaat niet aangepast

In dit scenario wordt het paginaformaat ingesteld op een vaste breedte en hoogte, waardoor de inhoud mogelijk wordt bijgesneden als deze deze afmetingen overschrijdt.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Maak een HTMLDocument-instantie van het HTML-bestand
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Opties voor PDF-weergave instellen
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Geef de uitvoer weer
pdf_renderer.render(device, html_document);
```

### Paginaformaat aangepast aan de breedte van de inhoud

In dit scenario wordt het paginaformaat aangepast aan de breedte van de inhoud.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Geef de uitvoer weer
pdf_renderer.render(device, html_document);
```

## Conclusie

In deze zelfstudie hebben we onderzocht hoe u de PDF-paginagrootte kunt aanpassen bij het converteren van HTML naar PDF met Aspose.HTML voor Java. U hebt de vereisten geleerd, de vereiste pakketten geïmporteerd en een stapsgewijze handleiding gevolgd om deze taak te volbrengen. Met Aspose.HTML voor Java kunt u eenvoudig de paginagrootte van uw gegenereerde PDF's bepalen, zodat uw inhoud wordt weergegeven zoals bedoeld.

 Experimenteer gerust met verschillende paginaformaten en instellingen om aan uw specifieke vereisten te voldoen. Als u problemen ondervindt of verdere vragen heeft, aarzel dan niet om hulp te vragen aan de[Aspose.HTML voor Java-documentatie](https://reference.aspose.com/html/java/) of de[Aspose-ondersteuningsforum](https://forum.aspose.com/).

## Veelgestelde vragen

### V1: Wat is Aspose.HTML voor Java?

A1: Aspose.HTML voor Java is een Java-bibliotheek waarmee u met HTML-documenten kunt werken, deze kunt manipuleren, converteren en weergeven in verschillende indelingen, waaronder PDF.

### Vraag 2: Hoe kan ik de PDF-paginagrootte aanpassen wanneer ik HTML naar PDF converteer met Aspose.HTML voor Java?

 A2: U kunt het PDF-paginaformaat aanpassen met behulp van de`PageSetup` klasse en het instellen van de`AdjustToWidestPage` eigendom aan`true` of 'false', afhankelijk van uw vereisten.

### V3: Kan ik de stijl van HTML-inhoud aanpassen voordat ik deze naar PDF converteer?

A3: Ja, u kunt de stijl aanpassen door CSS- en HTML-elementen aan uw HTML-inhoud toe te voegen voordat u deze naar PDF converteert, zoals gedemonstreerd in de zelfstudie.

### V4: Waar kan ik de documentatie voor Aspose.HTML voor Java vinden?

 A4: U kunt de documentatie raadplegen[hier](https://reference.aspose.com/html/java/) voor uitgebreide informatie en voorbeelden.

### V5: Is er een gratis proefversie beschikbaar voor Aspose.HTML voor Java?

 A5: Ja, u kunt toegang krijgen tot een gratis proefversie van Aspose.HTML voor Java vanaf[deze link](https://releases.aspose.com/).