---
category: general
date: 2026-06-07
description: Maak PNG van HTML in Java met Aspose.HTML. Leer HTML naar PNG te renderen,
  de user‑agent in Java in te stellen en de device‑pixel‑ratio aan te passen in slechts
  een paar stappen.
draft: false
keywords:
- create png from html
- render html to png
- set user agent java
- convert html to png
- set device pixel ratio
language: nl
og_description: Maak PNG van HTML in Java met Aspose.HTML. Deze tutorial laat zien
  hoe je HTML naar PNG rendert, de user‑agent in Java instelt en de device‑pixel‑ratio
  instelt.
og_title: PNG maken van HTML in Java – Complete gids
schemas:
- author: Aspose
  dateModified: '2026-06-07'
  description: Create PNG from HTML in Java using Aspose.HTML. Learn to render HTML
    to PNG, set user agent Java, and adjust device pixel ratio in just a few steps.
  headline: Create PNG from HTML in Java – Full Example
  type: TechArticle
- description: Create PNG from HTML in Java using Aspose.HTML. Learn to render HTML
    to PNG, set user agent Java, and adjust device pixel ratio in just a few steps.
  name: Create PNG from HTML in Java – Full Example
  steps:
  - name: Setting the Viewport Width
    text: '```java renderingSandbox.setDeviceWidth(375); // 375 px width – typical
      iPhone size ```'
  - name: Adjusting the Device Pixel Ratio
    text: '```java renderingSandbox.setDevicePixelRatio(2.0); // 2× pixel density
      for retina displays ```'
  - name: Providing a Custom User‑Agent (set user agent java)
    text: '```java renderingSandbox.setUserAgent( "Mozilla/5.0 (iPhone; CPU iPhone
      OS 14_0 like Mac OS X) " + "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0
      Mobile/15E148 Safari/604.1" ); ```'
  - name: Expected Output
    text: 'Open the PNG in any image viewer and you should see:'
  type: HowTo
tags:
- Java
- Aspose.HTML
- Image Conversion
title: Maak PNG van HTML in Java – Volledig voorbeeld
url: /nl/java/conversion-html-to-various-image-formats/create-png-from-html-in-java-full-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak PNG van HTML in Java – Volledig voorbeeld

Heb je je ooit afgevraagd hoe je **PNG van HTML kunt maken** direct binnen een Java‑applicatie? Misschien heb je een thumbnail nodig voor een e‑mailvoorbeeld, of wil je social‑media‑kaarten on‑the‑fly genereren. Hoe dan ook, **HTML naar PNG renderen** zonder een browser te openen is een handige truc die tijd en middelen bespaart.

In deze gids lopen we stap voor stap door een praktische, end‑to‑end‑oplossing die gebruikmaakt van Aspose.HTML for Java. Je ziet hoe je **set user agent Java** instelt, de **device pixel ratio** aanpast, en uiteindelijk **convert HTML to PNG** uitvoert met slechts een paar regels code. Geen externe services, geen headless Chrome—alleen pure Java‑code die je in elk project kunt gebruiken.

## Wat je leert

- Hoe je een HTML‑pagina laadt die media‑queries bevat.
- Hoe je een rendering‑sandbox maakt die een mobiel apparaat nabootst.
- Hoe je **set device pixel ratio** en een aangepaste user‑agent‑string instelt.
- Hoe je **render HTML to PNG** en het resultaat opslaat op schijf.
- Tips voor het oplossen van veelvoorkomende valkuilen (ontbrekende lettertypen, cross‑origin bronnen, enz.).

Voordat we beginnen, zorg dat je het volgende hebt:

- Java 17 of nieuwer (de API werkt met Java 8+, maar nieuwere versies bieden betere prestaties).
- Aspose.HTML for Java‑bibliotheek (je kunt deze ophalen van Maven Central).
- Een IDE of build‑tool naar keuze (IntelliJ IDEA, Maven, Gradle—wat je maar wilt).

Klaar? Laten we de handen uit de mouwen steken.

## Stap 1: Zet het project op en voeg Aspose.HTML toe

Voeg eerst de Aspose.HTML‑dependency toe aan je `pom.xml` als je Maven gebruikt:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- check for the latest version -->
</dependency>
```

Of, voor Gradle:

```gradle
implementation 'com.aspose:aspose-html:23.9'
```

Zodra de bibliotheek op het classpath staat, ben je klaar om **PNG van HTML te maken**.

## Stap 2: Laad het HTML‑document (het startpunt voor conversie)

Het eerste wat we nodig hebben is een `HTMLDocument`‑instantie die naar de bron‑HTML wijst. Dit kan een lokaal bestand zijn, een URL, of zelfs een string met ruwe markup.

```java
// Step 2: Load the HTML document that contains media queries
HTMLDocument htmlDoc = new HTMLDocument("https://YOUR_DOMAIN/responsive.html");
```

> **Waarom dit belangrijk is:** Het laden van het document via Aspose.HTML geeft ons volledige controle over de rendering‑pipeline, waardoor we later een sandbox met aangepaste apparaatinstellingen kunnen injecteren.

## Stap 3: Maak een Rendering‑Sandbox om een mobiel apparaat te simuleren

Een sandbox is in wezen een virtuele browseromgeving. Door deze te configureren kunnen we **set device pixel ratio** en andere parameters instellen die invloed hebben op hoe CSS‑media‑queries zich gedragen.

```java
// Step 3: Create a rendering sandbox that simulates a mobile device
RenderingSandbox renderingSandbox = new RenderingSandbox();
```

### Instellen van de viewport‑breedte

```java
renderingSandbox.setDeviceWidth(375); // 375 px width – typical iPhone size
```

### Aanpassen van de device pixel ratio

```java
renderingSandbox.setDevicePixelRatio(2.0); // 2× pixel density for retina displays
```

### Een aangepaste User‑Agent leveren (set user agent java)

```java
renderingSandbox.setUserAgent(
    "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
    "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0 Mobile/15E148 Safari/604.1"
);
```

> **Pro tip:** Het overeenkomen van een echte device‑user‑agent‑string zorgt ervoor dat elke JavaScript of CSS die `navigator.userAgent` controleert zich exact gedraagt als op dat apparaat.

## Stap 4: Koppel de sandbox aan het document

Nu koppelen we de sandbox aan ons HTML‑document zodat alle daaropvolgende rendering de mobiele instellingen die we zojuist hebben gedefinieerd respecteert.

```java
// Step 4: Apply the sandbox to the document so it renders with the mobile settings
htmlDoc.setSandbox(renderingSandbox);
```

Als je deze stap overslaat, wordt de standaard desktop‑viewport gebruikt, en zullen je media‑queries voor mobiel nooit afgaan—wat betekent dat de output‑PNG er niet uitziet als een telefoonscherm.

## Stap 5: Kies afbeelding‑opslaanopties (convert html to png)

Aspose.HTML ondersteunt veel afbeeldingsformaten. Voor een scherpe PNG maken we een `ImageSaveOptions`‑instantie met `SaveFormat.PNG`.

```java
// Step 5: Prepare image save options for PNG output
ImageSaveOptions imageOptions = new ImageSaveOptions(SaveFormat.PNG);
```

Je kunt ook DPI, achtergrondkleur of compressieniveau aanpassen via het `imageOptions`‑object als je een hoger‑resolutie‑bestand nodig hebt.

## Stap 6: Renderen en opslaan – de laatste **convert html to png** stap

De laatste regel doet het zware werk: de pagina renderen binnen de sandbox en de bitmap naar schijf schrijven.

```java
// Step 6: Render the page and save it as an image that reflects the mobile viewport
htmlDoc.save("YOUR_DIRECTORY/mobile-view.png", imageOptions);
```

Wanneer het programma klaar is, vind je een `mobile‑view.png`‑bestand dat er precies uitziet als de pagina op een iPhone met een breedte van 375 px en een pixel‑dichtheid van 2×.

### Verwachte output

Open de PNG in een beeldviewer en je zou moeten zien:

- Tekst op grootte volgens de mobiele CSS‑breakpoints.
- Afbeeldingen geschaald voor een high‑density scherm (dankzij de **set device pixel ratio**‑aanroep).
- Eventuele responsieve navigatie samengevouwen naar de mobiele variant.

Als de output er niet goed uitziet, controleer dan de URL, zorg dat alle externe bronnen bereikbaar zijn, en verifieer dat de sandbox‑instellingen overeenkomen met het doelapparaat.

## Veelvoorkomende valkuilen & hoe ze op te lossen

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| **Missing fonts** | De sandbox heeft geen toegang tot systeemlettertypen die door de pagina worden gebruikt. | Installeer de benodigde lettertypen op de server of embed web‑fonts via `@font-face`. |
| **Cross‑origin images blocked** | Aspose.HTML respecteert CORS‑beleid. | Host afbeeldingen op hetzelfde domein of schakel CORS‑headers in op de bronserver. |
| **JavaScript not executed** | Standaard schakelt Aspose.HTML script‑uitvoering uit om veiligheidsredenen. | Roep `renderingSandbox.setEnableJavaScript(true)` aan als je script‑gedreven lay-outwijzigingen nodig hebt (gebruik met voorzichtigheid). |
| **Output blurry on retina screens** | DPI is standaard 96. | Stel `imageOptions.setDpiX(300); imageOptions.setDpiY(300);` in voor een hogere resolutie. |

## Volledig werkend voorbeeld (Alle stappen op één plek)

Hieronder staat de volledige, kant‑klaar‑te‑runnen Java‑klasse. Vervang `YOUR_DOMAIN` en `YOUR_DIRECTORY` door echte waarden.

```java
import com.aspose.html.*;
import com.aspose.html.saving.*;
import com.aspose.html.rendering.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the HTML document that contains media queries
        HTMLDocument htmlDoc = new HTMLDocument("https://YOUR_DOMAIN/responsive.html");

        // Step 2: Create a rendering sandbox that simulates a mobile device
        RenderingSandbox renderingSandbox = new RenderingSandbox();

        // Step 3: Configure the sandbox (viewport width, pixel ratio, and user‑agent)
        renderingSandbox.setDeviceWidth(375);                     // 375 px width
        renderingSandbox.setDevicePixelRatio(2.0);               // 2× pixel density
        renderingSandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0 Mobile/15E148 Safari/604.1");

        // Step 4: Apply the sandbox to the document so it renders with the mobile settings
        htmlDoc.setSandbox(renderingSandbox);

        // Step 5: Prepare image save options for PNG output
        ImageSaveOptions imageOptions = new ImageSaveOptions(SaveFormat.PNG);

        // Step 6: Render the page and save it as an image that reflects the mobile viewport
        htmlDoc.save("YOUR_DIRECTORY/mobile-view.png", imageOptions);
    }
}
```

Voer het programma uit (`mvn exec:java` of de run‑configuratie van je IDE) en je hebt een **create PNG from HTML**‑pipeline die volledig offline werkt.

## Conclusie

We hebben zojuist alles behandeld wat je nodig hebt om **PNG van HTML te maken** in Java—het document laden, een sandbox configureren, **setting user agent java**, de **device pixel ratio** aanpassen, en uiteindelijk **render html to png**. De code is compact, de afhankelijkheden zijn minimaal, en het resultaat is een perfect formaat PNG die een echt mobiel apparaat weerspiegelt.

Wat nu? Probeer het PNG‑formaat te vervangen door JPEG als je kleinere bestanden nodig hebt, experimenteer met verschillende viewport‑breedtes om thumbnails voor tablets te genereren, of integreer deze snippet in een Spring Boot‑endpoint die de afbeelding op aanvraag retourneert. De mogelijkheden zijn eindeloos, en nu heb je een solide basis om op voort te bouwen.

Heb je vragen of ben je een vreemd randgeval tegengekomen? Laat een reactie achter hieronder, en laten we samen het probleem oplossen. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [HTML naar PNG converteren met Aspose.HTML for Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-png/)
- [HTML naar PNG converteren met Aspose.HTML Message Handlers in Java](/html/english/java/configuring-environment/use-message-handlers/)
- [svg naar png java – SVG naar afbeelding converteren met Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}