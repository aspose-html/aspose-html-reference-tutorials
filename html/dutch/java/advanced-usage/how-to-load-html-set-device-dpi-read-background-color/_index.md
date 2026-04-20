---
category: general
date: 2026-02-16
description: Hoe HTML te laden in Java, de DPI van het apparaat in te stellen, een
  virtuele schermgrootte te definiëren en de berekende achtergrondkleur van elk element
  te lezen.
draft: false
keywords:
- how to load html
- read background color
- set device dpi
- set virtual screen size
- get computed background color
language: nl
og_description: Hoe HTML te laden in Java, de DPI van het apparaat in te stellen,
  een virtuele schermgrootte te definiëren en de berekende achtergrondkleur van elk
  element te lezen.
og_title: Hoe HTML te laden, DPI van apparaat in te stellen & achtergrondkleur te
  lezen
tags:
- Aspose.HTML
- Java
title: Hoe HTML te laden, DPI van het apparaat in te stellen en de achtergrondkleur
  te lezen
url: /nl/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe HTML te Laden, Apparaat DPI in te Stellen & Achtergrondkleur te Lezen

Heb je je ooit afgevraagd **hoe html te laden** in een Java‑app en vervolgens de stijlen van de pagina te inspecteren? Je bent niet de enige—ontwikkelaars moeten vaak een webpagina off‑screen renderen, de uiteindelijke CSS‑waarden ophalen, en deze gebruiken voor PDF‑conversie, screenshots of zelfs geautomatiseerde tests.  

In deze gids lopen we precies dat stap voor stap door: we laden een HTML‑bestand, **stellen apparaat‑DPI in**, definiëren een **virtuele schermgrootte**, en lezen uiteindelijk de **achtergrondkleur** van het `<body>`‑element. Aan het einde heb je een volledig uitvoerbaar fragment dat de **berekende achtergrondkleur** afdrukt—geen mysterie, gewoon Java.

## Wat je nodig hebt

* Java 17 of nieuwer (de code werkt met elke recente JDK).  
* Aspose.HTML for Java 23.9 of later—download de JAR van de Aspose‑site of voeg deze toe via Maven.  
* Een eenvoudig HTML‑bestand (bijv. `responsive.html`) dat een achtergrondkleur in CSS definieert.

Dat is alles—geen extra frameworks, geen browser‑drivers. Klaar? Laten we beginnen.

![Diagram dat laat zien hoe html te laden en berekende stijlen te extraheren](/images/load-html-diagram.png){alt="Diagram dat laat zien hoe html te laden en berekende stijlen te extraheren"}

## Stap 1: Hoe HTML te Laden en Rendering‑opties te Configureren

Het eerste wat je doet is een `HtmlLoadOptions`‑object aanmaken. Dit object vertelt Aspose.HTML **hoe html te laden**—inclusief de virtuele schermafmetingen en de DPI die je wilt emuleren.

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create load options and define the virtual screen size and DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        // setVirtualScreenSize – width × height in CSS pixels
        loadOptions.setScreenSize(new Size(1280, 800));
        // setDeviceDpi – typical desktop DPI (96 is the default for most monitors)
        loadOptions.setDeviceDpi(96);
```

**Waarom dit belangrijk is:**  
Het instellen van een virtuele schermgrootte zorgt ervoor dat media‑queries zoals `@media (max-width: 600px)` zich gedragen alsof de pagina op een echte monitor wordt gerenderd. De DPI beïnvloedt hoe CSS `px`‑eenheden worden gemapt naar fysieke pixels—cruciaal wanneer je later afbeeldingen of PDF’s genereert.

## Stap 2: Het HTML‑bestand Laden met de Geconfigureerde Opties

Nu laden we daadwerkelijk het bestand. Let op dat we dezelfde `loadOptions` doorgeven die we zojuist hebben geconfigureerd.

```java
        // 2️⃣ Load the HTML file with the options we just set.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);
```

Als het bestand niet wordt gevonden, gooit Aspose een duidelijke `FileNotFoundException`. In productie wil je dit misschien in een try‑catch wikkelen en terugvallen op een standaard HTML‑string.

## Stap 3: Virtuele Schermgrootte en Apparaat‑DPI Instellen (Expliciet)

Hoewel we hierboven al `setScreenSize` en `setDeviceDpi` hebben aangeroepen, is het de moeite waard te benadrukken dat **set virtual screen size** en **set device dpi** op elk moment vóór het renderen kunnen worden aangepast. Bijvoorbeeld, je zou de DPI kunnen verhogen voor high‑resolution screenshots:

```java
        // 3️⃣ Adjust DPI for a high‑resolution render (optional).
        loadOptions.setDeviceDpi(300);   // 300 DPI is common for print‑ready images
        // 4️⃣ Change screen size for a mobile layout test.
        loadOptions.setScreenSize(new Size(375, 667)); // iPhone X viewport
```

Vergeet niet het document opnieuw te laden als je deze instellingen na de eerste load wijzigt—Aspose behandelt ze als onveranderlijk zodra de `Document` is aangemaakt.

## Stap 4: Achtergrondkleur Lezen en Berekende Achtergrondkleur Ophalen

Met het document in het geheugen kun je de berekende stijl van elk element opvragen. Hier richten we ons op de `<body>`‑tag, maar dezelfde aanpak werkt voor `<div>`, `<p>` of zelfs pseudo‑elementen.

```java
        // 5️⃣ Retrieve the <body> element.
        Element bodyElement = document.getBody();

        // 6️⃣ Output the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

**Wat je zult zien:** Als `responsive.html` `body { background: #ff5722; }` bevat, print de console iets als:

```
Computed background color: rgba(255,87,34,1)
```

Dat is het resultaat van **get computed background color**—Aspose lost alle CSS‑cascade‑regels, media‑queries en zelfs `!important`‑declaraties op voordat de uiteindelijke waarde wordt geretourneerd.

## Volledig Werkend Voorbeeld

Alles bij elkaar genomen, hier is het volledige, kant‑klaar programma:

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create load options – virtual screen size + DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        loadOptions.setScreenSize(new Size(1280, 800)); // set virtual screen size
        loadOptions.setDeviceDpi(96);                  // set device DPI (default desktop)

        // Optional: tweak for high‑resolution or mobile rendering.
        // loadOptions.setDeviceDpi(300);
        // loadOptions.setScreenSize(new Size(375, 667));

        // Step 2: Load the HTML document with the options.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);

        // Step 3: Grab the <body> element.
        Element bodyElement = document.getBody();

        // Step 4: Print the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

### Verwachte Output

```
Computed background color: rgba(255,255,255,1)
```

*(De exacte RGBA‑waarden hangen af van de CSS in je HTML‑bestand.)*

## Veelvoorkomende Valkuilen & Pro‑Tips

* **Ontbrekende DPI‑instelling?** Aspose gebruikt standaard 96 DPI, wat high‑resolution screenshots kan vervagen. Stel deze altijd expliciet in als je een scherp resultaat nodig hebt.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}