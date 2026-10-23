---
category: general
date: 2026-10-19
description: Stel device pixel ratio in Java in met behulp van Aspose.HTML sandbox.
  Leer hoe je screen width height kunt instellen en page title java kunt ophalen met
  een volledig, uitvoerbaar voorbeeld.
draft: false
keywords:
- get page title java
- device pixel ratio java
- create virtual device java
- set screen width height
lastmod: 2026-10-19
og_description: Get page title java met Aspose.HTML sandbox. Deze gids laat zien hoe
  je screen width height en device pixel ratio in Java in een paar eenvoudige stappen
  kunt instellen.
og_image_alt: 'Developer guide: set device pixel ratio in Java using Aspose.HTML sandbox'
og_title: Pagina-titel ophalen in Java – device pixel ratio instellen in Java sandbox
  tutorial
schemas:
- author: Aspose
  dateModified: '2026-10-19'
  description: set device pixel ratio in Java using Aspose.HTML sandbox. Learn how
    to set screen width height and get page title java with a complete, runnable example.
  headline: Get page title java – set device pixel ratio in Java sandbox tutorial
  type: TechArticle
- questions:
  - answer: Yes—create a new `SandboxOptions` with a different `setDevicePixelRatio`
      value and instantiate a fresh `Sandbox`. Re‑using the same sandbox after changing
      its options is not supported.
    question: Can I change the pixel ratio at runtime?
  - answer: Loop over a list of `SandboxOptions` (e.g., iPhone 8, Pixel 4) and run
      the same load‑and‑title logic for each.
    question: What if I need to test multiple devices?
  - answer: Aspose.HTML respects Java’s default SSL trust store. Add the cert to the
      JVM’s keystore or, for testing only, disable verification (not recommended for
      production).
    question: Does this work with HTTPS sites that have self‑signed certificates?
  - answer: The `HTMLDocument` API provides `save` methods that can export the rendered
      page to PNG or JPEG. Use `htmlDoc.save("output.png", SaveFormat.PNG);` after
      loading.
    question: How do I capture a screenshot instead of just the title?
  - answer: Each `Sandbox` instance is isolated, but you should avoid sharing a single
      instance across multiple threads without synchronization.
    question: Is the sandbox thread‑safe?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- mobile emulation
title: Pagina-titel ophalen in Java – device pixel ratio instellen in Java sandbox
  tutorial
url: /nl/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pagina-titel ophalen in Java – apparaat-pixelverhouding instellen in Java sandbox-tutorial

Heb je ooit moeten **set device pixel ratio** tijdens het testen van een responsieve site in Java? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer de pagina er perfect uitziet op desktop maar breekt op high‑DPI-telefoons. Het goede nieuws? Met de sandbox van Aspose.HTML kun je een iPhone X (of elk apparaat) emuleren rechtstreeks vanuit je Java-code—geen browser nodig.

In deze gids lopen we stap voor stap door **how to set screen width height**, configureren we de **device pixel ratio**, en uiteindelijk **get page title java** om te verifiëren dat alles correct gerenderd is. Aan het einde heb je een zelfstandige programma die je in elk project kunt plaatsen en direct mobiele lay-outs kunt testen.

## Snelle antwoorden
- **Hoe stel ik device pixel ratio in Java in?** Gebruik `SandboxOptions.setDevicePixelRatio(double)` voordat je de sandbox maakt.  
- **Welke methode retourneert de page title?** Roep `htmlDocument.getTitle()` aan op het geladen `HTMLDocument`.  
- **Kan ik andere apparaten emuleren?** Ja—maak een nieuwe `SandboxOptions` met de gewenste breedte, hoogte en pixelratio.  
- **Heb ik een browserdriver nodig?** Nee, de sandbox van Aspose.HTML is head‑less en draait puur in Java.  
- **Welke Aspose.HTML‑versie is vereist?** Versie 23.7 of later ondersteunt alle mobile‑emulation‑functies.

## Wat is get page title java?
`get page title java` is de bewerking om het `<title>`‑element uit een HTML‑document op te halen met Java‑code. Het stelt je in staat te bevestigen dat een pagina die in een virtuele apparaat‑context is geladen de verwachte titel heeft gerenderd. Het ophalen van de titel is een veelvoorkomende stap in geautomatiseerde validatie om te verzekeren dat de juiste pagina is geladen na het toepassen van device‑emulation‑parameters.

## Waarom Aspose.HTML sandbox gebruiken voor mobiele emulatie?
Aspose.HTML ondersteunt **30+** invoer‑ en uitvoerformaten—waaronder HTML, CSS, SVG en PDF—en kan pagina’s renderen zonder een volledige browser te starten. De sandbox verwerkt sites met honderden pagina’s terwijl het geheugengebruik onder de 200 MB blijft, waardoor het ideaal is voor CI‑pipelines.

## Vereisten

- Java 8 of nieuwer (de code compileert ook met JDK 11)  
- Aspose.HTML for Java‑bibliotheek (versie 23.7 of later) – je kunt deze ophalen van Maven Central  
- Een IDE of een eenvoudige `javac`‑commandoregel‑setup  
- Internettoegang voor de demo‑URL (`https://responsive.example.com`)

Geen extra frameworks, geen Selenium, alleen pure Java en Aspose.HTML.

## Hoe screen width height en device pixel ratio in Java instellen

De `SandboxOptions`‑klasse laat je de schermafmetingen en pixeldichtheid van het virtuele apparaat opgeven. Om een specifiek mobiel apparaat te emuleren moet je de sandbox configureren met de gewenste schermbreedte, hoogte en device pixel ratio. Door een `SandboxOptions`‑object te maken en deze eigenschappen in te stellen, zal de renderengine de pagina behandelen alsof deze op dat apparaat wordt weergegeven, waardoor CSS‑media‑queries en afbeeldingsschaling correct werken.

Maak een `SandboxOptions`‑instantie, stel de breedte in op **375**, de hoogte op **812**, en de device pixel ratio op **3.0**. Geef vervolgens die opties door aan een nieuwe `Sandbox`. Hiermee configureer je het virtuele apparaat volledig voordat een pagina wordt geladen.

De `SandboxOptions`‑klasse definieert de schermgrootte en pixeldichtheid van het virtuele apparaat. Het is het instappunt voor elke mobile‑emulation‑scenario.

```java
// Step 1 – configure the virtual device
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixels width
sandboxOptions.setScreenHeight(812);         // CSS pixels height
sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI factor (set device pixel ratio)
```

> **Waarom dit belangrijk is:**  
> De `setDevicePixelRatio`‑aanroep schaalt alles—van afbeeldingen tot lettertype‑rendering—zodat de pagina denkt dat hij op een echte telefoon draait. Als je dit overslaat, kan de lay-out terugvallen op desktop‑style CSS‑media‑queries, waardoor het doel van mobiel testen wordt ondermijnd.

## Hoe de sandbox‑instantie maken

De `Sandbox`‑klasse vertegenwoordigt een headless‑browseromgeving die HTML rendert met behulp van de eerder gedefinieerde opties. Na het configureren van `SandboxOptions`, instantiateer je een `Sandbox` met die opties om een geïsoleerde rendercontext te verkrijgen. Deze sandbox functioneert als een lichte browser, past de door jou opgegeven schermgrootte en pixeldichtheid toe, en kan worden hergebruikt voor meerdere paginaladingen terwijl de omgeving schoon blijft.

Instantiateer een `Sandbox` met de eerder geconfigureerde `SandboxOptions`. De sandbox gedraagt zich als een kleine, headless‑browser die de door jou gedefinieerde afmetingen en pixelratio respecteert.

Het `Sandbox`‑object is de geïsoleerde renderengine van Aspose.HTML die zonder UI draait. Het garandeert dat elke test in een schone omgeving wordt uitgevoerd.

```java
// Step 2 – spin up the sandbox with the options above
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

> **Pro tip:** Je kunt hetzelfde `Sandbox`‑object hergebruiken voor meerdere paginaladingen; wijzig simpelweg de URL en de sandbox behoudt dezelfde apparaatkenmerken.

## Hoe de pagina in de sandbox laden

De `HTMLDocument`‑klasse vertegenwoordigt een geparseerd HTML‑bestand in het geheugen, en biedt DOM‑toegang en rendermogelijkheden. Met de sandbox gereed, maak je een `HTMLDocument` door de doel‑URL en de sandbox‑instantie door te geven. Dit laadt en rendert de pagina met de instellingen van het virtuele apparaat, waardoor je met de DOM kunt interageren of informatie zoals de titel kunt extraheren.

Maak een `HTMLDocument` door de doel‑URL en de `Sandbox`‑instantie door te geven. Dit dwingt het document om te renderen met het virtuele apparaat dat je eerder hebt ingesteld.

De `HTMLDocument`‑klasse vertegenwoordigt een geparseerd HTML‑bestand in het geheugen en biedt methoden voor DOM‑manipulatie en het extraheren van metadata.

```java
// Step 3 – fetch the target page using the sandbox
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("https://responsive.example.com"), mobileSandbox);
```

Als de URL onbereikbaar is of de pagina fouten bevat, zal Aspose.HTML een uitzondering gooien. Voor productiecodel zou je dit in een `try‑catch` wikkelen en de fout loggen, maar de tutorial houdt het eenvoudig.

## Hoe verifiëren met get page title java

De `getTitle()`‑methode retourneert de inhoud van het `<title>`‑element van het HTML‑document als een eenvoudige string. Het lezen van de titel is de snelste sanity‑check. Na het laden van de pagina, roep je `htmlDocument.getTitle()` aan om de titeltekst op te halen. Deze eenvoudige controle bevestigt dat de pagina correct is gerenderd onder de emulatie‑apparaatinstellingen en biedt een snelle manier om navigatie‑ of inhoudsveranderingen in geautomatiseerde tests te valideren.

Roep `htmlDocument.getTitle()` aan op het geladen document en print het resultaat. Als de sandbox de **device pixel ratio** correct heeft toegepast, zal de titel overeenkomen met wat je op een echte iPhone X zou zien.

De `getTitle()`‑methode retourneert de inhoud van het `<title>`‑element als een eenvoudige string, waardoor je de rendering kunt valideren zonder visuele inspectie.

```java
// Step 4 – retrieve and print the page title (get page title java)
System.out.println("Title under sandbox: " + htmlDoc.getTitle());
```

**Verwachte output (voorbeeld):**

```
Title under sandbox: Responsive Demo – Mobile View
```

Dus als je de titel ziet afgedrukt, heb je succesvol **set device pixel ratio**, **set screen width height**, en **got the page title** met Java.

## Volledig, uitvoerbaar voorbeeld

Hieronder staat het volledige programma dat je kunt copy‑pasten in een bestand genaamd `SandboxDemo.java`. Zorg ervoor dat de Aspose.HTML‑JAR‑bestanden op je classpath staan (`-cp`‑vlag) voordat je compileert.

De `SandboxDemo`‑klasse verbindt alle voorgaande stappen tot één uitvoerbaar voorbeeld.

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

Je zou de titel in de console moeten zien afgedrukt, wat bevestigt dat de pagina is gerenderd met de gewenste **device pixel ratio**.

## Veelgestelde vragen & randgevallen

**Q: Kan ik de pixelratio tijdens runtime wijzigen?**  
A: Ja—maak een nieuwe `SandboxOptions` met een andere `setDevicePixelRatio`‑waarde en instantiateer een nieuwe `Sandbox`. Het hergebruiken van dezelfde sandbox na het wijzigen van de opties wordt niet ondersteund.

**Q: Wat als ik meerdere apparaten moet testen?**  
A: Loop over een lijst van `SandboxOptions` (bijv. iPhone 8, Pixel 4) en voer dezelfde load‑and‑title‑logica voor elk uit.

**Q: Werkt dit met HTTPS‑sites met zelf‑ondertekende certificaten?**  
A: Aspose.HTML respecteert de standaard SSL‑truststore van Java. Voeg het certificaat toe aan de keystore van de JVM of, alleen voor testen, schakel verificatie uit (niet aanbevolen voor productie).

**Q: Hoe maak ik een screenshot in plaats van alleen de titel?**  
A: De `HTMLDocument`‑API biedt `save`‑methoden die de gerenderde pagina kunnen exporteren naar PNG of JPEG. Gebruik `htmlDoc.save("output.png", SaveFormat.PNG);` na het laden.

**Q: Is de sandbox thread‑safe?**  
A: Elke `Sandbox`‑instantie is geïsoleerd, maar je moet vermijden een enkele instantie over meerdere threads te delen zonder synchronisatie.

## Visueel overzicht

![Diagram die set device pixel ratio in mobile sandbox toont](https://example.com/images/sandbox-diagram.png "set device pixel ratio diagram")

[Diagram die set device pixel ratio in mobile sandbox toont](https://example.com/images/sandbox-diagram.png "set device pixel ratio diagram")

*De illustratie hierboven toont de stroom van het configureren van `SandboxOptions` (inclusief **set screen width height** en **set device pixel ratio**) tot het laden van een URL en het extraheren van de title.*

## Conclusie

Je weet nu **how to set device pixel ratio** in Java, hoe **set screen width height** te gebruiken voor nauwkeurige mobiele emulatie, en hoe **get page title java** te gebruiken om te bevestigen dat de rendering geslaagd is. Deze compacte workflow elimineert de noodzaak van zware browsers tijdens geautomatiseerd UI‑testen en past netjes in CI‑pipelines.

Klaar voor de volgende stap? Probeer de gerenderde pagina als afbeelding te exporteren, of experimenteer met CSS‑media‑query‑debugging door de `devicePixelRatio` tussen 1.0 en 3.0 te schakelen. Je kunt ook de PDF‑conversiefuncties van Aspose.HTML verkennen om een afdrukbare versie van de mobiele weergave vast te leggen.

Veel plezier met coderen, en moge je mobiele lay-outs altijd scherp blijven—ongeacht de pixel‑dichtheid!

---

**Laatst bijgewerkt:** 2026-10-19  
**Getest met:** Aspose.HTML 23.7 for Java  
**Auteur:** Aspose

## Gerelateerde tutorials

- [HTML-titel ophalen Java – pagina renderen in sandbox met schermbreedte](/html/java/advanced-usage/get-html-title-java-render-page-in-sandbox-with-screen-width/)
- [Maak Aspose HTML Sandbox volledige Java-gids](/html/java/configuring-environment/create-aspose-html-sandbox-complete-java-guide/)
- [Device Pixel Ratio instellen in Java volledige gids](/html/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}