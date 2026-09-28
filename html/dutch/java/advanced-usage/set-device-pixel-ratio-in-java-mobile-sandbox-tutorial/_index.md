---
category: general
date: 2026-02-10
description: Stel de apparaat‑pixelverhouding in Java in met de Aspose.HTML‑sandbox.
  Leer hoe je de schermbreedte en -hoogte instelt en de paginatitel in Java opvraagt,
  met een volledig, uitvoerbaar voorbeeld.
draft: false
keywords:
- set device pixel ratio
- get page title java
- set screen width height
language: nl
og_description: Stel de apparaat‑pixelverhouding in Java met Aspose.HTML‑sandbox.
  Deze gids laat je zien hoe je de schermbreedte en -hoogte instelt en de paginatitel
  in Java opvraagt in een paar eenvoudige stappen.
og_title: Instellen van de apparaatpixelverhouding in Java – Mobile Sandbox Tutorial
tags:
- Aspose.HTML
- Java
- Mobile Emulation
title: Device‑pixelratio instellen in Java – Mobile Sandbox‑tutorial
url: /nl/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/
---

with all translations.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# device pixel ratio instellen in Java – Mobile Sandbox Tutorial

Heb je ooit moeten **device pixel ratio instellen** tijdens het testen van een responsieve site in Java? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer de pagina er perfect uitziet op desktop maar kapot gaat op high‑DPI telefoons. Het goede nieuws? Met de sandbox van Aspose.HTML kun je een iPhone X (of elk ander apparaat) emuleren rechtstreeks vanuit je Java‑code—geen browser nodig.

In deze gids lopen we stap voor stap door **hoe je screen width height instelt**, de **device pixel ratio** configureert, en uiteindelijk **get page title java** gebruikt om te verifiëren dat alles correct gerenderd is. Aan het einde heb je een zelfstandige programma dat je in elk project kunt plaatsen en direct mobiele lay-outs kunt testen.

## Vereisten

- Java 8 of nieuwer (de code compileert ook met JDK 11)  
- Aspose.HTML for Java bibliotheek (versie 23.7 of later) – je kunt deze ophalen van Maven Central  
- Een IDE of een eenvoudige `javac` commandoregel‑setup  
- Internettoegang voor de demo‑URL (`https://responsive.example.com`)

Geen extra frameworks, geen Selenium, alleen pure Java en Aspose.HTML.

---

## Stap 1: screen width height en device pixel ratio instellen

Het eerste dat we nodig hebben is een `SandboxOptions`‑object dat de sandbox vertelt welk “apparaat” we simuleren. Hier gebruiken we de iPhone X‑afmetingen (375 × 812 CSS‑pixels) en een **device pixel ratio** van 3.0, wat de high‑DPI retina‑display nabootst.

```java
// Step 1 – configure the virtual device
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixels width
sandboxOptions.setScreenHeight(812);         // CSS pixels height
sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI factor (set device pixel ratio)
```

> **Waarom dit belangrijk is:**  
> De `setDevicePixelRatio`‑aanroep schaalt alles—van afbeeldingen tot lettertype‑rendering—zodat de pagina denkt dat hij op een echte telefoon draait. Als je dit overslaat, kan de lay‑out terugvallen op desktop‑style CSS‑media‑queries, waardoor het doel van mobiel testen teniet wordt gedaan.

---

## Stap 2: De sandbox‑instantie maken

Nu zetten we die opties om in een actieve sandbox. Beschouw de sandbox als een kleine, headless browser die de afmetingen en pixelratio respecteert die we zojuist hebben gedefinieerd.

```java
// Step 2 – spin up the sandbox with the options above
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

> **Pro tip:** Je kunt hetzelfde `Sandbox`‑object hergebruiken voor meerdere paginaladingen; wijzig simpelweg de URL en de sandbox behoudt dezelfde apparaateigenschappen.

---

## Stap 3: De pagina laden in de sandbox

Met de sandbox klaar, is het laden van een pagina net zo eenvoudig als het construeren van een `HTMLDocument` en het doorgeven van de sandbox als tweede argument. Dit dwingt het document om te renderen met het virtuele apparaat dat we eerder hebben ingesteld.

```java
// Step 3 – fetch the target page using the sandbox
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("https://responsive.example.com"), mobileSandbox);
```

Als de URL onbereikbaar is of de pagina fouten bevat, zal Aspose.HTML een uitzondering gooien. Voor productiecodel zou je dit waarschijnlijk in een `try‑catch` wikkelen en de fout loggen, maar voor de tutorial houden we het eenvoudig.

---

## Stap 4: Verifiëren met get page title java

De snelste sanity‑check is het lezen van de titel van het document. Als de sandbox de **device pixel ratio** correct heeft toegepast, zal de titel identiek zijn aan wat je op een echte iPhone X zou zien.

```java
// Step 4 – retrieve and print the page title (get page title java)
System.out.println("Title under sandbox: " + htmlDoc.getTitle());
```

**Verwachte output (voorbeeld):**

```
Title under sandbox: Responsive Demo – Mobile View
```

Als je de titel ziet afgedrukt, heb je met succes **device pixel ratio ingesteld**, **screen width height ingesteld**, en **de paginatitel opgehaald** met Java.

---

## Volledig, uitvoerbaar voorbeeld

Hieronder staat het volledige programma dat je kunt kopiëren‑plakken in een bestand genaamd `SandboxDemo.java`. Zorg ervoor dat de Aspose.HTML‑JAR‑bestanden op je classpath staan (`-cp`‑vlag) voordat je compileert.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.net.URL;

/**
 * Demonstrates how to set device pixel ratio, set screen width height,
 * and get page title java using Aspose.HTML sandbox.
 */
public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define device characteristics ----------
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS pixels width
        sandboxOptions.setScreenHeight(812);         // CSS pixels height
        sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI screen factor (set device pixel ratio)

        // ---------- Step 2: Create the sandbox ----------
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // ---------- Step 3: Load a web page inside the sandbox ----------
        HTMLDocument htmlDoc = new HTMLDocument(
                new URL("https://responsive.example.com"), mobileSandbox);

        // ---------- Step 4: Verify the document loaded correctly ----------
        System.out.println("Title under sandbox: " + htmlDoc.getTitle());
    }
}
```

Compileer en voer uit:

```bash
javac -cp "aspose-html-23.7.jar" SandboxDemo.java
java -cp ".:aspose-html-23.7.jar" SandboxDemo
```

Je zou de titel in de console moeten zien verschijnen, wat bevestigt dat de pagina is gerenderd met de gewenste **device pixel ratio**.

---

## Veelgestelde vragen & randgevallen

| Vraag | Antwoord |
|----------|--------|
| **Kan ik de pixelratio tijdens runtime wijzigen?** | Ja—maak gewoon een nieuwe `SandboxOptions` met een andere `setDevicePixelRatio`‑waarde en instantiate een nieuwe `Sandbox`. Het hergebruiken van dezelfde sandbox na het wijzigen van de opties wordt niet ondersteund. |
| **Wat als ik meerdere apparaten moet testen?** | Loop over een lijst van `SandboxOptions` (bijv. iPhone 8, Pixel 4) en voer dezelfde load‑and‑title‑logica voor elk uit. |
| **Werkt dit met HTTPS‑sites die zelf‑ondertekende certificaten hebben?** | Aspose.HTML respecteert de standaard SSL‑truststore van Java. Voeg het certificaat toe aan de keystore van de JVM of schakel verificatie uit alleen voor testdoeleinden (niet aanbevolen voor productie). |
| **Hoe maak ik een screenshot in plaats van alleen de titel?** | De `HTMLDocument`‑API biedt `save`‑methoden die de gerenderde pagina kunnen exporteren naar PNG of JPEG. Gebruik `htmlDoc.save("output.png", SaveFormat.PNG);` na het laden. |
| **Is de sandbox thread‑veilig?** | Elke `Sandbox`‑instantie is geïsoleerd, maar je moet vermijden een enkele instantie te delen over meerdere threads zonder synchronisatie. |

---

## Visueel overzicht

![Diagram dat device pixel ratio instellen in mobile sandbox toont](https://example.com/images/sandbox-diagram.png "device pixel ratio diagram")

*De bovenstaande illustratie geeft de stroom weer van het configureren van `SandboxOptions` (inclusief **set screen width height** en **set device pixel ratio**) tot het laden van een URL en het extraheren van de titel.*

---

## Conclusie

Je weet nu **hoe je device pixel ratio instelt** in Java, hoe je **screen width height instelt** voor nauwkeurige mobiele emulatie, en hoe je **get page title java** gebruikt om te bevestigen dat het renderen geslaagd is. Deze compacte workflow elimineert de noodzaak voor zware browsers tijdens geautomatiseerd UI‑testen en past netjes in CI‑pipelines.

Klaar voor de volgende stap? Probeer de gerenderde pagina als afbeelding te exporteren, of experimenteer met CSS‑media‑query‑debugging door de `devicePixelRatio` tussen 1.0 en 3.0 te schakelen. Je kunt ook de PDF‑conversiefuncties van Aspose.HTML verkennen om een afdrukbare versie van de mobiele weergave vast te leggen.

Veel plezier met coderen, en moge je mobiele lay-outs altijd scherp blijven—ongeacht de pixel‑dichtheid!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}