---
category: general
date: 2026-04-03
description: Leer hoe je sandbox in Aspose.HTML Java gebruikt om de user‑agent in
  te stellen, de grootte te bepalen en direct de viewportgrootte op te halen. Volledige
  code, uitleg en tips inbegrepen.
draft: false
keywords:
- how to use sandbox
- set user agent
- get viewport size
- how to set size
- how to get viewport
language: nl
og_description: Leer hoe je sandbox in Aspose.HTML Java gebruikt om de user‑agent
  in te stellen, de grootte te bepalen en direct de viewportgrootte op te halen. Complete
  gids met code en best practices.
og_title: Hoe Sandbox te gebruiken – Stel User Agent in & verkrijg viewportgrootte
tags:
- AsposeHTML
- Java
- Sandbox
title: Hoe Sandbox te gebruiken – Stel User Agent in & verkrijg viewportgrootte
url: /nl/java/configuring-environment/how-to-use-sandbox-set-user-agent-get-viewport-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Sandbox te Gebruiken – User Agent Instellen & Viewportgrootte Ophalen

Heb je je ooit afgevraagd **hoe je sandbox kunt gebruiken** bij het renderen van HTML met Aspose.HTML voor Java? Misschien ben je tegen een muur aangelopen bij het simuleren van een specifieke schermgrootte of moet je een user‑agent‑string spoofen zodat de pagina zich gedraagt alsof hij wordt bezocht vanaf een mobiele browser.  

Het goede nieuws is dat de sandbox‑API je precies dat laat doen, en je kunt ook de berekende viewportgrootte ophalen nadat de pagina is geladen. In deze tutorial lopen we door het maken van een sandbox, het instellen van de grootte, het instellen van een aangepaste user agent, het laden van een externe pagina, en uiteindelijk het lezen van de viewport‑afmetingen. Aan het einde weet je **hoe je de grootte instelt**, **hoe je de viewport ophaalt**, en waarom deze stappen belangrijk zijn voor betrouwbare headless rendering.

> **Snelle winst:** je hebt binnen enkele seconden een uitvoerbare Java‑klasse die iets als `Viewport: 1280×800` afdrukt.

---

## Wat je nodig hebt

- **Aspose.HTML for Java** versie 24.6 of nieuwer (de API die we gebruiken werd geïntroduceerd in 24.5).  
- Een Java 17+ ontwikkelkit (elke recente JDK werkt).  
- Een IDE of een eenvoudige teksteditor—geen speciale plugins nodig.  
- Internettoegang als je een externe URL wilt laden, zoals `https://example.com`.

Dat is alles. Er is geen Maven/Gradle‑toverkunst vereist; je kunt de JAR‑bestanden handmatig op de classpath plaatsen als je dat liever doet.  

---

## Hoe Sandbox te Gebruiken – Overzicht

De sandbox isoleert de rendering‑engine van het host‑OS, waardoor je een virtueel scherm (breedte, hoogte, DPI) en een aangepaste **user agent**‑string kunt definiëren. Beschouw het als een miniatuur browservenster dat volledig in het geheugen bestaat. Wanneer je later de `HTMLDocument` vraagt om zijn standaardweergave, rapporteert de engine de **viewportgrootte** die hij heeft berekend op basis van de sandbox‑instellingen.  

Hieronder staat een overzichtelijke flow:

1. **Maak** een `DocumentSandbox` en configureer breedte, hoogte, DPI en user‑agent.  
2. **Laad** een `HTMLDocument` binnen die sandbox.  
3. **Vraag** de standaardweergave van het document op voor de viewportgrootte.  

Laten we elk stapje nader bekijken.

---

## Stap 1: Maak een Sandbox en Stel de Grootte In

Eerst starten we een sandbox en vertellen we hem hoe groot het virtuele scherm moet zijn. Dit is waar je de vraag **hoe je de grootte instelt** voor een headless render beantwoordt.

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.drawing.Size2D;

/* Step 1 – instantiate the sandbox */
DocumentSandbox sandbox = new DocumentSandbox();

/* Set the virtual screen width & height (in pixels) */
sandbox.setScreenWidth(1280);   // width in pixels
sandbox.setScreenHeight(800);   // height in pixels

/* DPI influences CSS pixel calculations – 96 is the CSS default */
sandbox.setDeviceDpi(96);

/* Optional: give the sandbox a friendly name for debugging */
sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");
```

**Pro tip:** Als je een responsive layout test, probeer dan een smalle breedte zoals `360` om een telefoon te emuleren, of een brede zoals `1920` voor een desktop. De sandbox respecteert de DPI die je instelt, dus een high‑density scherm (bijv. 144 DPI) beïnvloedt media‑queries die `device-pixel-ratio` gebruiken.

---

## Stap 2: User Agent Instellen voor de Sandbox

Waarom een aangepaste **user agent** gebruiken? Sommige sites leveren verschillende markup of scripts afhankelijk van de gemelde browser. Door `setUserAgent` aan te roepen kun je de pagina laten denken dat hij wordt bezocht vanaf Chrome, Firefox of een mobiel apparaat.

```java
/* Step 2 – customize the user‑agent string */
sandbox.setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                     "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                     "Version/15.0 Mobile/15E148 Safari/604.1");
```

Nu zal de pagina denken dat hij wordt gerenderd op een iPhone. Als je de **user agent** terug naar de standaard wilt zetten, gebruik dan gewoon de eerdere “AsposeHTML/24.6 …” string opnieuw.

---

## Stap 3: Laad een HTML‑Document in de Sandbox

Met de sandbox klaar, kunnen we elke URL of lokaal HTML‑bestand laden. De `HTMLDocument`‑constructor neemt de sandbox als tweede argument, waardoor de twee aan elkaar worden gekoppeld.

```java
import com.aspose.html.HTMLDocument;

/* Step 3 – load the page using the configured sandbox */
try (HTMLDocument doc = new HTMLDocument("https://example.com", sandbox)) {
    // The document is now rendered inside the sandbox environment.
    // Any JavaScript or CSS will see the size and user‑agent we defined.
```

Het `try‑with‑resources`‑blok zorgt ervoor dat het document correct wordt vrijgegeven, waardoor native resources die Aspose.HTML onder de motorkap toewijst, worden vrijgemaakt.

---

## Stap 4: Viewportgrootte Ophalen uit het Document

Hier is het moment waar je op hebt gewacht: het ophalen van de **viewportgrootte** die de rendering‑engine heeft berekend. Dit beantwoordt **hoe je de viewport ophaalt** nadat de pagina is opgemaakt.

```java
    /* Step 4 – fetch the viewport dimensions */
    Size2D viewport = doc.getDefaultView().getScreenSize();
    System.out.println("Viewport: " + viewport.getWidth() + "×" + viewport.getHeight());
}
```

Wanneer je het programma uitvoert, zou je iets moeten zien als:

```
Viewport: 1280×800
```

Als je de sandbox‑afmetingen in Stap 1 hebt gewijzigd, zullen de afgedrukte cijfers die nieuwe waarden weerspiegelen—perfect voor geautomatiseerde tests die responsive breakpoints verifiëren.

---

## Volledig Werkend Voorbeeld

Hieronder staat de volledige, klaar‑om‑te‑runnen klasse die alle onderdelen samenvoegt. Kopieer‑en‑plak het in een bestand genaamd `SandboxExample.java`, voeg de Aspose.HTML‑JARs toe aan je classpath, en voer `java SandboxExample` uit.

```java
import com.aspose.html.*;
import com.aspose.html.drawing.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox with a custom screen size and DPI
        DocumentSandbox sandbox = new DocumentSandbox();
        sandbox.setScreenWidth(1280);          // width in pixels
        sandbox.setScreenHeight(800);          // height in pixels
        sandbox.setDeviceDpi(96);              // screen DPI
        sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");

        // Step 2: (Optional) Override the user agent if you need a mobile profile
        sandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
            "Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 3: Load the HTML document inside the configured sandbox
        try (HTMLDocument htmlDocument = new HTMLDocument("https://example.com", sandbox)) {

            // Step 4: Retrieve and display the computed viewport size
            Size2D viewportSize = htmlDocument.getDefaultView().getScreenSize();
            System.out.println("Viewport: " + viewportSize.getWidth() + "×" + viewportSize.getHeight());
        }
    }
}
```

**Verwachte output** (ervan uitgaande dat de sandbox‑instellingen hierboven zijn):

```
Viewport: 1280×800
```

Als je een andere **breedte/hoogte** in de sandbox instelt, zal de output dienovereenkomstig veranderen—precies wat je nodig hebt bij het testen van responsive ontwerpen.

---

## Randgevallen & Veelgestelde Vragen

### Wat als de pagina `window.innerWidth` gebruikt in plaats van CSS media queries?

De virtuele schermgrootte van de sandbox beïnvloedt zowel de CSS‑lay-out als JavaScript's `window.innerWidth/innerHeight`. Dus **hoe je de viewport ophaalt** via JavaScript zal dezelfde cijfers teruggeven als je in de Java‑console ziet.

### Kan ik meerdere sandboxes parallel uitvoeren?

Ja. Elke `DocumentSandbox`‑instantie is onafhankelijk, dus je kunt een thread‑pool opzetten, elke thread zijn eigen sandbox met verschillende afmetingen geven, en tientallen pagina's gelijktijdig renderen. Vergeet alleen niet de JARs thread‑safe te houden (dat zijn ze).

### Heeft de DPI‑instelling invloed op het schalen van afbeeldingen?

Absoluut. Een hogere DPI zorgt ervoor dat één CSS‑pixel overeenkomt met meer apparaatpixels, waardoor high‑resolution afbeeldingen scherper kunnen lijken. Als je retina‑stijl assets test, probeer dan `sandbox.setDeviceDpi(144)`.

### Hoe ga ik om met HTTPS‑certificaten die zelf‑ondertekend zijn

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}