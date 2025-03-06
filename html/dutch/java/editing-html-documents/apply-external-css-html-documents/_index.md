---
title: Externe CSS toepassen op HTML-documenten in Aspose.HTML voor Java
linktitle: Externe CSS toepassen op HTML-documenten in Aspose.HTML voor Java
second_title: Java HTML-verwerking met Aspose.HTML
description: Ontdek hoe u externe CSS toepast op HTML-documenten met Aspose.HTML voor Java! Volg deze stapsgewijze handleiding voor een complete tutorial.
weight: 12
url: /nl/java/editing-html-documents/apply-external-css-html-documents/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Externe CSS toepassen op HTML-documenten in Aspose.HTML voor Java

## Invoering
Bij het werken met HTML-documenten kan het toepassen van stijlen het verschil maken in presentatie en gebruikerservaring. Als u zich verdiept in Java en wilt leren hoe u externe CSS-stijlen kunt toepassen op uw HTML-documenten met behulp van de Aspose.HTML-bibliotheek, bent u hier aan het juiste adres! Deze gids is bedoeld om het proces stap voor stap te verduidelijken, waardoor het zelfs voor mensen die nieuw zijn in Java of CSS eenvoudig is.
## Vereisten
Voordat u de code induikt, moet u een aantal zaken regelen:
### 1. Java-ontwikkelingskit (JDK)
 Zorg ervoor dat u JDK op uw machine hebt geïnstalleerd. U kunt de nieuwste versie downloaden van[Java-website van Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).
### 2. Aspose.HTML voor Java
Je moet Aspose.HTML voor Java hebben ingesteld. Als je dit nog niet hebt gedaan, ga dan naar de[Aspose downloadpagina](https://releases.aspose.com/html/java/) en pak de bibliotheek.
### 3. Een IDE of teksteditor
Kies een Integrated Development Environment (IDE) zoals IntelliJ IDEA, Eclipse of zelfs een eenvoudige teksteditor om uw Java-code te schrijven.
### 4. Basiskennis van Java
Als u bekend bent met de basisbeginselen van Java-programmering en CSS, kunt u de cursus gemakkelijker volgen.
## Pakketten importeren
Zodra u alles hebt ingesteld, is de volgende stap het importeren van de benodigde pakketten in uw Java-project. Dit is wat u nodig hebt:
```java
import com.aspose.html.HTMLDocument;
```
Met deze imports kunt u HTML-documenten bewerken en ze in verschillende formaten weergeven, zoals PDF.

We zullen onze tutorial opsplitsen in beheersbare stappen. Elke stap zal u door het proces leiden van het toepassen van externe CSS-stijlen op een HTML-document met behulp van Aspose.HTML voor Java.
## Stap 1: Maak een HTML-document
Allereerst moeten we ons HTML-document maken. We beginnen met het definiëren van de inhoud met een eenvoudige HTML-structuur.
```java
String content = "<div><p>Internal CSS</p><p>An internal CSS is used to define a style for a single HTML page</p></div>";
HTMLDocument document = new HTMLDocument(content, ".");
```

 Hier hebben we een basis-HTML-structuur gedefinieerd, inclusief een`<div>` met twee alinea's. De`HTMLDocument` klasse wordt gebruikt om een documentweergave van onze HTML-inhoud te maken.
## Stap 2: Een stijlelement maken
 Vervolgens gaan we een`style` element om onze CSS-regels vast te leggen.
```java
Element style = document.createElement("style");
style.setTextContent(".frame1 { margin-top:50px; margin-left:50px; padding:20px; width:360px; height:90px; background-color:#a52a2a; font-family:verdana; color:#FFF5EE;} \n" +
        ".frame2 { margin-top:-90px; margin-left:160px; text-align:center; padding:20px; width:360px; height:100px; background-color:#ADD8E6;}");
```

 Met behulp van de`createElement` methode van`HTMLDocument` , we creëren een nieuwe`<style>` element en stel de inhoud in om onze CSS-definities voor twee klassen op te nemen:`frame1` En`frame2`Deze klassen definiëren marges, opvulling, afmetingen, achtergrondkleuren, lettertypefamilies en tekstkleuren.
## Stap 3: De stijl toevoegen aan de documentkoptekst
Nu we de CSS op de juiste plek hebben, moeten we het stijlelement aan de kop van het document toevoegen.
```java
Element head = document.getElementsByTagName("head").get_Item(0);
head.appendChild(style);
```

 We halen de kop van het document op en voegen onze nieuw gecreëerde`style` element. Deze actie integreert onze CSS effectief in het HTML-document, waardoor het onze HTML-inhoud kan stylen.
## Stap 4: Klassen toepassen op HTML-elementen
Vervolgens passen we de eerder gedefinieerde CSS-klassen toe op onze alinea-elementen.
```java
HTMLElement paragraph = (HTMLElement) document.getElementsByTagName("p").get_Item(0);
paragraph.setClassName("frame1");
HTMLElement lastParagraph = (HTMLElement) document.getElementsByTagName("p").get_Item(document.getElementsByTagName("p").getLength() - 1);
lastParagraph.setClassName("frame2");
```

Hier benaderen we de eerste en laatste alinea-elementen in het document en wijzen we ze de CSS-klassen toe die we hebben gemaakt. Deze toewijzing zorgt ervoor dat ze voldoen aan de stijlen die zijn gedefinieerd in onze CSS.
## Stap 5: Stel extra stijleigenschappen in
Om het uiterlijk nog verder te verbeteren, stellen we extra stijlkenmerken in voor onze alinea's.
```java
paragraph.getStyle().setFontSize("250%");
paragraph.getStyle().setTextAlign("center");
lastParagraph.getStyle().setColor("#434343");
lastParagraph.getStyle().setFontSize("150%");
lastParagraph.getStyle().setFontFamily("verdana");
```

In deze stap verfijnen we onze stijlen. De lettergrootte van de eerste alinea wordt vergroot en gecentreerd, terwijl de kleur, lettergrootte en lettertypefamilie van de laatste alinea worden gedefinieerd. Deze verfijning is cruciaal voor de leesbaarheid en esthetische aantrekkingskracht.
## Stap 6: Sla het HTML-document op
Zodra de stijlen zijn toegepast, is het tijd om het HTML-document op te slaan.
```java
document.save("edit-internal-css.html");
```

 Hier maken we gebruik van de`save` methode van de`HTMLDocument` klasse om de gewijzigde HTML-inhoud naar een bestand te schrijven, zodat onze stijlen en wijzigingen behouden blijven.
## Stap 7: Het document naar PDF renderen
Ten slotte converteren we het document naar een PDF-formaat voor uitvoer.
```java
PdfDevice device = new PdfDevice("edit-internal-css.pdf");
document.renderTo(device);
```

 Met behulp van de`PdfDevice` klasse, we stellen de rendering van ons HTML-document in een PDF in. Deze stap is essentieel als u het gestileerde document wilt delen in een universeel toegankelijk formaat.
## Conclusie
En daar heb je het: externe CSS toepassen op HTML-documenten met Aspose.HTML voor Java is zowel eenvoudig als lonend! Met slechts een paar regels code kun je platte tekst omzetten in visueel aantrekkelijke en professioneel vormgegeven documenten. Dus of je nu ontwerpt voor persoonlijk gebruik, rapporten maakt of webcontent ontwikkelt, het is een krachtige vaardigheid om HTML en CSS in Java te kunnen manipuleren.
## Veelgestelde vragen
### Wat is Aspose.HTML voor Java?
Aspose.HTML voor Java is een krachtige bibliotheek waarmee ontwikkelaars met HTML-documenten in Java-toepassingen kunnen werken. De bibliotheek biedt een breed scala aan functies, van HTML-manipulatie tot rendering.
### Heb ik een internetverbinding nodig om Aspose.HTML te gebruiken?
Nee, zodra u de benodigde bibliotheekbestanden hebt gedownload, kunt u Aspose.HTML offline gebruiken.
### Kan ik meerdere CSS-bestanden op een HTML-document toepassen?
 Ja, u kunt meerdere`<link>` elementen en voeg ze toe aan de kop van het document voor verschillende CSS-bestanden.
### Is er een verschil tussen interne en externe CSS?
Ja! Interne CSS wordt gedefinieerd in een HTML-document, terwijl externe CSS in een apart bestand wordt geplaatst en aan het document wordt gekoppeld.
### Hoe kan ik ondersteuning krijgen voor Aspose.HTML voor Java?
 U kunt toegang krijgen tot ondersteuning van de gemeenschap via de[Aspose-forum](https://forum.aspose.com/c/html/29) voor eventuele vragen of problemen die u tegenkomt.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
