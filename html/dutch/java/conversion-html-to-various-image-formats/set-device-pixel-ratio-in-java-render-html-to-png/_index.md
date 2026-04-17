---
category: general
date: 2026-03-14
description: Leer hoe u de device pixel ratio instelt in Java en een webpagina opslaat
  als PNG met Aspose.HTML – een volledige gids voor html‑naar‑png conversie.
draft: false
keywords:
- set device pixel ratio
- save webpage as png
- how to render png
- html to png conversion
- java html to image
language: nl
og_description: Leer hoe u de device pixel ratio in Java instelt en een webpagina
  opslaat als PNG met Aspose.HTML, met een stapsgewijze uitleg van html naar png conversie.
og_title: device pixel ratio instellen in Java – HTML renderen naar PNG
tags:
- java
- aspose-html
- image-rendering
title: device pixel ratio instellen in Java – HTML renderen naar PNG
url: /nl/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-render-html-to-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# set device pixel ratio in Java – Render HTML naar PNG

Heb je ooit **set device pixel ratio** moeten **instellen** tijdens het genereren van een screenshot van een webpagina in Java? Misschien bouw je een preview‑service voor mobiele apparaten, of wil je gewoon een scherpe thumbnail die er goed uitziet op een Retina‑scherm. Hoe dan ook, je bent op de juiste plek. In deze tutorial lopen we het volledige **html to png conversion** proces door, en zie je precies hoe je een **webpage as png** opslaat met de Aspose.HTML‑bibliotheek.

We behandelen alles, van het configureren van een sandbox die een iPhone‑viewport nabootst, tot het laden van een externe HTML‑pagina, en uiteindelijk het schrijven van het resultaat naar schijf. Aan het einde weet je **how to render png** bestanden programmatically, en heb je een herbruikbare snippet die je in elk Java‑project kunt plaatsen dat **java html to image** mogelijkheden nodig heeft.

## Wat je nodig hebt

- **Java Development Kit (JDK) 8 of nieuwer** – de bibliotheek werkt met elke recente JDK.
- **Aspose.HTML for Java** – je kunt de nieuwste JAR halen uit de Aspose Maven‑repository of de zip downloaden van de officiële site.
- Een **IDE** (IntelliJ IDEA, Eclipse, of zelfs VS Code) – alles wat je in staat stelt Java te compileren en uit te voeren.
- Een internetverbinding als je van plan bent een live URL te laden (het voorbeeld gebruikt `https://example.com/mobile.html`).

Dat is alles. Geen extra build‑tools of native binaries nodig.

## Stap 1: Configureer de Sandbox en stel device pixel ratio in

Het eerste wat je moet doen is een **Sandbox** maken die zich voordoet als een mobiel apparaat. Hier stel je daadwerkelijk **device pixel ratio** in om overeen te komen met een high‑density scherm (bijvoorbeeld de 2× retina‑display van de iPhone).

```java
import com.aspose.html.rendering.SandboxOptions;

// Create sandbox options
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixel width of iPhone 6/7/8
sandboxOptions.setScreenHeight(667);         // CSS pixel height
sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
sandboxOptions.setUserAgent(
    "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
    "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0 Mobile/15E148 Safari/604.1");

// Build the sandbox
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

**Waarom dit belangrijk is:** De `devicePixelRatio` vertelt de renderengine hoeveel fysieke pixels overeenkomen met één CSS‑pixel. Zonder deze instelling zou je uitvoerafbeelding wazig lijken op high‑DPI schermen. Door het expliciet te definiëren, zorg je ervoor dat de gegenereerde PNG de juiste hoeveelheid detail heeft.

> **Pro tip:** Als je Android‑apparaten target, kun je `3.0` gebruiken voor apparaten met 3× scaling. Pas de breedte/hoogte dienovereenkomstig aan.

## Stap 2: Laad de HTML‑pagina voor html to png conversie

Nu de sandbox klaar is, kunnen we de pagina laden die we willen vastleggen. De `HTMLDocument`‑klasse van Aspose.HTML accepteert een URL en een sandbox‑instantie, zodat de pagina precies wordt gerenderd zoals op het gesimuleerde apparaat.

```java
import com.aspose.html.HTMLDocument;

// Load the remote page inside the sandbox
HTMLDocument document = new HTMLDocument(
    "https://example.com/mobile.html", // Replace with your own URL
    mobileSandbox);
```

**Wat gebeurt er onder de motorkap?** De bibliotheek haalt de HTML op, parseert CSS, voert eventuele JavaScript uit (indien ingeschakeld), en legt de pagina uit met de viewport‑dimensies die je eerder hebt gedefinieerd. Deze stap is de kern van **java html to image** conversie omdat het je een volledig gerenderde DOM geeft die klaar is voor rasterisatie.

> **Edge case:** Als de pagina afhankelijk is van externe lettertypen, zorg er dan voor dat ze bereikbaar zijn vanaf de machine die de code uitvoert. Anders kan de tekst terugvallen op een standaardlettertype, waardoor het visuele resultaat verandert.

## Stap 3: Sla webpagina op als PNG – hoe png renderen met Aspose.HTML

Met het document gerenderd, is het laatste onderdeel om daadwerkelijk een PNG‑bestand naar schijf te schrijven. De `PngSaveOptions`‑klasse laat je compressieniveau en andere PNG‑specifieke instellingen aanpassen, maar de standaardwaarden werken perfect voor de meeste scenario's.

```java
import com.aspose.html.saving.PngSaveOptions;

// Define PNG options (optional)
PngSaveOptions pngOptions = new PngSaveOptions();
// You could adjust pngOptions.setCompressionLevel(9); for maximum compression

// Save the rendered page as a PNG image
document.save("output/mobile_view.png", pngOptions);

System.out.println("Mobile view rendered and saved as PNG.");
```

Wanneer je het programma uitvoert, krijg je `mobile_view.png` in de `output`‑map. Open het, en je zou een exacte snapshot van de externe pagina moeten zien, gerenderd op de high‑density resolutie die je hebt opgegeven via **set device pixel ratio**.

### Snelle verificatie

```text
$ java -jar MobileRenderTutorial.jar
Mobile view rendered and saved as PNG.
$ ls output
mobile_view.png
```

Open de afbeelding met een willekeurige viewer; de tekst moet scherp zijn, iconen helder, en de lay-out identiek aan wat je op een echte iPhone zou zien.

## Optioneel: Het render‑pipeline aanpassen

### DPI dynamisch aanpassen

Als je afbeeldingen moet genereren voor meerdere schermdichtheden, wikkel je de sandbox‑creatie in een methode:

```java
private static Sandbox createSandbox(double dpr) {
    SandboxOptions opts = new SandboxOptions();
    opts.setScreenWidth(375);
    opts.setScreenHeight(667);
    opts.setDevicePixelRatio(dpr); // Pass 1.0, 2.0, 3.0, etc.
    opts.setUserAgent("...");
    return new Sandbox(opts);
}
```

Roep vervolgens `createSandbox(3.0)` aan voor een 3× apparaat. Deze flexibiliteit is handig wanneer je een service bouwt die thumbnails voor iPhone, iPad en Android‑tablets in één keer retourneert.

### Renderen zonder JavaScript

Als de pagina die je vastlegt zware scripts bevat die je niet nodig hebt, kun je JavaScript uitschakelen voor een snellere **html to png conversion**:

```java
sandboxOptions.setJavaScriptEnabled(false);
```

Het uitschakelen van scripts kan de render‑tijd halveren, maar wees je ervan bewust dat sommige dynamische inhoud kan verdwijnen.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| **Vage uitvoer** | `devicePixelRatio` op standaard (1.0) gelaten | Expliciet **device pixel ratio instellen** op 2.0 of hoger |
| **Ontbrekende lettertypen** | Externe lettertypen geblokkeerd door firewall | Zorg dat de machine internettoegang heeft of embed lettertypen lokaal |
| **Out‑of‑memory fouten** | Zeer grote pagina's renderen op hoge DPI | Beperk de viewportgrootte of verlaag de `devicePixelRatio` |
| **Onjuiste URL** | Een relatief pad gebruiken zonder basis-URL | Geef een volledige absolute URL op of stel `document.setBaseUrl()` in |

## Volledig werkend voorbeeld

Hieronder staat het complete, kant‑klaar Java‑programma. Kopieer‑en‑plak het in een bestand genaamd `MobileRenderTutorial.java`, voeg de Aspose.HTML‑JAR toe aan je classpath, en voer het uit.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.Sandbox;
import com.aspose.html.rendering.SandboxOptions;
import com.aspose.html.saving.PngSaveOptions;

public class MobileRenderTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox that mimics a mobile device viewport
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS pixel width
        sandboxOptions.setScreenHeight(667);         // CSS pixel height
        sandboxOptions.setDevicePixelRatio(2.0);     // High‑density screen (set device pixel ratio)
        sandboxOptions.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0 Mobile/15E148 Safari/604.1");

        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // Step 2: Load the HTML page inside the sandbox
        HTMLDocument document = new HTMLDocument(
            "https://example.com/mobile.html", // Replace with your own URL
            mobileSandbox);

        // Step 3: Render the page to a PNG image
        PngSaveOptions pngOptions = new PngSaveOptions();
        document.save("output/mobile_view.png", pngOptions);

        System.out.println("Mobile view rendered.");
    }
}
```

> **Resultaat:** Het programma maakt `output/mobile_view.png`, een high‑resolution screenshot die de **set device pixel ratio** respecteert die je hebt gedefinieerd.

## Visuele bevestiging

<img src="output/mobile_view.png" alt="voorbeeld screenshot van set device pixel ratio" width="400"/>

De bovenstaande afbeelding (placeholder) toont de uiteindelijke PNG na het renderproces. Let op de scherpe tekst en correct geschaalde UI‑elementen—precies wat je verwacht wanneer je **set device pixel ratio** correct instelt.

## Conclusie

Je hebt nu een stevige kennis van hoe je **set device pixel ratio** in Java kunt **instellen**, een **html to png conversion** uitvoert, en **webpage as png** opslaat met Aspose.HTML. Dit dekt de essentiële “how to render png” workflow en geeft je een herbruikbaar patroon voor elke **java html to image** taak die je tegenkomt.

Klaar voor de volgende stap? Probeer de URL te vervangen door een dynamische pagina, experimenteer met verschillende `devicePixelRatio`‑waarden, of integreer deze snippet in een Spring Boot‑endpoint die PNG’s op aanvraag retourneert. De mogelijkheden zijn eindeloos, en met de basis onder de knie zul je merken dat het een fluitje van een cent is om deze oplossing uit te breiden.

Veel plezier met coderen, en voel je vrij om een reactie achter te laten

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}