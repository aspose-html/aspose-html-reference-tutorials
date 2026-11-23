---
category: general
date: 2026-02-22
description: Stel de device pixel ratio in Java in met de Aspose.HTML sandbox. Leer
  hoe je een aangepaste user agent instelt, de paginatitel in Java ophaalt en HTML
  naar PNG converteert in één tutorial.
draft: false
keywords:
- set device pixel ratio
- set custom user agent
- save html as image
- convert html to png
- get page title java
language: nl
og_description: Stel de device pixel ratio in Java in met de Aspose.HTML‑sandbox.
  Deze tutorial laat zien hoe je een aangepaste user‑agent instelt, de paginatitel
  in Java ophaalt en HTML naar PNG converteert.
og_title: Stel de Device Pixel Ratio in Java in – Complete gids
tags:
- Aspose.HTML
- Java
- Web Rendering
title: Device Pixel Ratio instellen in Java – Complete gids
url: /nl/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Device Pixel Ratio instellen in Java – Complete Guide

Heb je je ooit afgevraagd hoe je **device pixel ratio** kunt **instellen** bij het renderen van een webpagina vanuit Java? Je bent niet de enige. Veel ontwikkelaars moeten high‑DPI mobiele schermen emuleren zodat screenshots er scherp uitzien, vooral wanneer ze later **html als afbeelding opslaan** voor rapporten of marketingmateriaal. In deze tutorial lopen we stap voor stap door een voorbeeld dat precies dat doet – en laten we je ook zien hoe je **een aangepaste user agent instelt**, **pagina‑titel java krijgt**, en **html naar png converteert** met Aspose.HTML.

We beginnen met een kort overzicht van de sandbox‑API, duiken daarna in elke configuratiestap, en produceren uiteindelijk een PNG‑bestand dat een echte iPhone‑display nabootst. Aan het einde heb je een herbruikbare code‑snippet die je in elk Java‑project kunt gebruiken. Geen externe tools nodig, alleen plain Java en Aspose.HTML 7.x (of nieuwer).

---

## Prerequisites

- Java 17 of hoger (de code compileert ook met eerdere versies, maar 17 wordt aanbevolen).
- Aspose.HTML for Java library (download van de officiële Aspose‑site; Maven‑coördinaten: `com.aspose:aspose-html:23.10`).
- Een IDE of teksteditor naar keuze (IntelliJ IDEA, VS Code, Eclipse… alles werkt).
- Internettoegang voor de demo‑URL (`https://example.com/responsive.html`), of vervang deze door een openbare HTML‑pagina die je bezit.

> **Pro tip:** Als je achter een proxy zit, configureer dan de JVM‑system‑properties `http.proxyHost` en `http.proxyPort` voordat je de code uitvoert.

---

## Stap 1: Device Pixel Ratio en andere Sandbox‑opties instellen

Het eerste wat we nodig hebben is een **SandboxOptions**‑instantie waarin we de virtuele schermgrootte en de *device pixel ratio* (DPR) definiëren. Beschouw DPR als de factor die de browser vertelt hoeveel fysieke pixels overeenkomen met één CSS‑pixel. Op een Retina‑iPhone is de DPR doorgaans **2.0**, daarom gebruiken we die waarde.

```java
// Step 1: Create and configure SandboxOptions
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS width of an iPhone X
sandboxOptions.setScreenHeight(667);         // CSS height
sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
```

> **Waarom dit belangrijk is:** Zonder de juiste DPR zal de gerenderde afbeelding er wazig of te groot uitzien omdat de rasterizer uitgaat van een 1:1 pixel‑mapping.

---

## Stap 2: Aangepaste User Agent instellen

Websites leveren vaak verschillende markup op basis van de **User‑Agent**‑header. Om ervoor te zorgen dat onze pagina zich gedraagt alsof hij op een echte iPhone wordt bekeken, injecteren we een aangepaste string die Safari op iOS nabootst.

```java
// Step 2: Define a mobile‑specific user agent
String iphoneUA = "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                  "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                  "Version/14.0 Mobile/15E148 Safari/604.1";

sandboxOptions.setUserAgent(iphoneUA);   // <-- set custom user agent
```

> **Randgeval:** Sommige sites inspecteren ook de `Accept-Language`‑header. Als je ontbrekende vertalingen ziet, voeg dan `sandboxOptions.setAcceptLanguage("en-US,en;q=0.9");` toe.

---

## Stap 3: De pagina laden in de Sandbox en de titel ophalen

Nu starten we de sandbox met de opties die we zojuist hebben gedefinieerd. Het **Sandbox**‑object isoleert het renderproces, zodat onze DPR‑ en user‑agent‑instellingen worden gerespecteerd.

```java
// Step 3: Create the sandbox and load the HTML document
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
HTMLDocument htmlDoc = new HTMLDocument(
        "https://example.com/responsive.html", mobileSandbox);
```

Zodra de pagina geladen is, is het ophalen van de titel zo simpel als het aanroepen van `getTitle()`. Dit voldoet aan de **get page title java**‑vereiste.

```java
// Step 3b: Print the page title to the console
System.out.println("Title: " + htmlDoc.getTitle());   // <-- get page title java
```

**Verwachte console‑output**

```
Title: Responsive Demo – Mobile View
```

Als de titel leeg is, controleer dan de URL of zorg ervoor dat de pagina niet wordt geblokkeerd door CORS‑beleid.

---

## Stap 4: HTML naar PNG converteren en HTML als afbeelding opslaan

Aspose.HTML stelt je in staat om de DOM direct naar een afbeeldingsbestand te renderen. Omdat we de DPR al op 2.0 hebben gezet, krijgt de resulterende PNG een dubbele pixeldichtheid, wat een scherpe screenshot oplevert.

```java
// Step 4: Render and save as PNG (convert html to png)
htmlDoc.save("mobile_view.png");   // <-- save html as image
```

De `save`‑methode detecteert automatisch de bestandsextensie en kiest de juiste renderer. Als je een ander formaat nodig hebt (JPEG, BMP), wijzig dan simpelweg de bestandsnaam.

> **Wat als je een specifieke afbeeldingsgrootte nodig hebt?**  
> Gebruik `ImageSaveOptions` om breedte, hoogte en achtergrondkleur te bepalen:

```java
ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
pngOptions.setWidth(750);   // 375 CSS px * DPR 2
pngOptions.setHeight(1334);
htmlDoc.save("mobile_view_custom.png", pngOptions);
```

---

## Volledig werkend voorbeeld

Hieronder staat het complete, kant‑klaar programma dat alle stappen samenvoegt. Kopieer‑en‑plak het in een `SandboxDemo.java`‑bestand, voeg de Aspose.HTML‑dependency toe, en voer `java SandboxDemo` uit.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.rendering.image.ImageSaveOptions;
import com.aspose.html.rendering.image.SaveFormat;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Configure sandbox – set device pixel ratio, screen size, and user agent
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS width (iPhone)
        sandboxOptions.setScreenHeight(667);         // CSS height
        sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
        sandboxOptions.setUserAgent(
                "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                "Version/14.0 Mobile/15E148 Safari/604.1");   // <-- set custom user agent

        // 2️⃣ Create sandbox instance
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // 3️⃣ Load the target page inside the sandboxed environment
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com/responsive.html", mobileSandbox);

        // 4️⃣ Retrieve and print the page title (get page title java)
        System.out.println("Title: " + htmlDoc.getTitle());

        // 5️⃣ Render the page – convert html to png and save html as image
        // Simple save (auto‑detect PNG)
        htmlDoc.save("mobile_view.png");   // <-- save html as image

        // 6️⃣ Optional: custom size rendering
        ImageSaveOptions opts = new ImageSaveOptions(SaveFormat.PNG);
        opts.setWidth(750);   // 375 * DPR 2
        opts.setHeight(1334);
        htmlDoc.save("mobile_view_custom.png", opts); // another convert html to png example
    }
}
```

Het uitvoeren van het programma levert twee PNG‑bestanden op:

| Bestand | Beschrijving |
|------|-------------|
| `mobile_view.png` | Standaardrendering met de geconfigureerde DPR. |
| `mobile_view_custom.png` | Rendering met expliciete breedte/hoogte (handig voor assets met vaste afmetingen). |

Je kunt elk bestand openen in een beeldviewer om de high‑resolution output te verifiëren.

---

## Veelgestelde vragen & randgevallen

| Vraag | Antwoord |
|----------|--------|
| **Wat als de pagina JavaScript bevat dat het DOM na het laden wijzigt?** | Aspose.HTML voert scripts standaard uit. Als je een statisch momentopname wilt vóór script‑executie, stel `sandboxOptions.setEnableJavaScript(false)` in. |
| **Kan ik een pagina renderen die authenticatie vereist?** | Ja. Gebruik `sandboxOptions.setCredentials(new NetworkCredential("user","pass"))` of injecteer cookies via `sandboxOptions.getCookies().add(...)`. |
| **Is de DPR beperkt tot 2.0?** | Nee. Je kunt elke positieve double instellen (bijv. 3.0 voor ultra‑high‑DPI‑apparaten). Houd er wel rekening mee dat een hogere DPR grotere afbeeldingsbestanden oplevert. |
| **Hoe ga ik om met pagina's met grote assets (afbeeldingen, fonts)?** | Verhoog de geheugenlimiet van de sandbox met `sandboxOptions.setMemoryLimit(512 * 1024 * 1024)` (bytes). Dit voorkomt out‑of‑memory‑fouten bij zware pagina's. |
| **Moet ik de sandbox handmatig sluiten?** | De `Sandbox` implementeert `AutoCloseable`. Plaats het in een try‑with‑resources‑blok voor automatische opruiming. |

---

## Conclusie

We hebben laten zien hoe je **device pixel ratio** instelt in een Java‑sandbox, **een aangepaste user agent** configureert, **pagina‑titel java** ophaalt, en **html naar png** converteert (effectief **html als afbeelding opslaan**) met Aspose.HTML. Het volledige voorbeeld demonstreert een praktische workflow die je kunt aanpassen voor geautomatiseerde screenshot‑generatie, visuele regressietests, of elke situatie waarin een pixel‑perfecte weergave van een webpagina vereist is.

Voel je vrij om te experimenteren – verander de DPR naar 3.0, wissel de user‑agent naar een Android‑string, of laat de URL wijzen naar een lokaal HTML‑bestand. Hetzelfde patroon werkt voor PDF’s, SVG’s, of zelfs multi‑page rendering.

Als je deze gids nuttig vond, overweeg dan gerelateerde onderwerpen zoals **PDF‑generatie met Aspose.HTML**, **headless Chrome‑alternatieven**, of **batch‑rendering van meerdere URL’s**. Veel programmeerplezier, en moge je screenshots altijd haarscherp zijn! 

![set device pixel ratio in Java sandbox](image.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}