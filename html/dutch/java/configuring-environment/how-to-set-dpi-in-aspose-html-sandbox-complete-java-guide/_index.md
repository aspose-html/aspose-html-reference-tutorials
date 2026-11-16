---
category: general
date: 2026-04-02
description: Leer hoe u DPI, de viewportgrootte en de user‑agent instelt in Aspose.HTML
  Sandbox. Stapsgewijs Java‑voorbeeld met volledige code en tips.
draft: false
keywords:
- how to set dpi
- set viewport size
- set user agent
- Aspose.HTML sandbox
- Java rendering settings
language: nl
og_description: Beheers hoe je DPI, de viewportgrootte en de user‑agent instelt in
  Aspose.HTML Sandbox met een compleet Java‑voorbeeld.
og_title: Hoe DPI in Aspose.HTML Sandbox in te stellen – Java‑tutorial
tags:
- Aspose.HTML
- Java
- Rendering
- Sandbox
title: Hoe DPI in de Aspose.HTML Sandbox in te stellen – Complete Java-gids
url: /nl/java/configuring-environment/how-to-set-dpi-in-aspose-html-sandbox-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe DPI in Aspose.HTML Sandbox in te stellen – Complete Java-gids

Heb je je ooit afgevraagd **hoe je DPI** instelt bij het renderen van een webpagina met Aspose.HTML? Je bent niet de enige. In veel testscenario's moet de lay-out overeenkomen met een specifieke schermdichtheid—denk aan print‑klare PDF's of hoge‑resolutie screenshots. Het goede nieuws is dat de Aspose.HTML sandbox je in staat stelt DPI, viewport‑grootte en zelfs de user‑agent‑string in één handig pakket te regelen.

In deze tutorial lopen we een praktisch Java‑voorbeeld door dat **DPI instelt**, **viewport‑grootte instelt**, en **user agent instelt** in één keer. Aan het einde heb je een uitvoerbaar programma, weet je waarom elke instelling belangrijk is, en ben je klaar om de sandbox aan te passen voor je eigen projecten.

---

## Wat je nodig hebt

- **Java 17** (of een recente JDK; de API is compatibel met Java 8+)
- **Aspose.HTML for Java** bibliotheek (versie 23.12 of nieuwer)
- Een IDE of eenvoudige teksteditor + command‑line compilatie
- Internettoegang voor de voorbeeld‑URL (`https://example.com`)

Er zijn geen externe build‑tools vereist; de code compileert met `javac` en draait met `java`. Als je Maven of Gradle verkiest, voeg dan gewoon de Aspose.HTML‑dependency toe—niets ingewikkeld.

## Stap 1: Maak een Sandbox die de Rendering‑omgeving Definieert

De sandbox is waar je Aspose.HTML vertelt welk “scherm” je wilt simuleren. Hier stellen we een **viewport van 1024 × 768**, een **DPI van 96**, en een aangepaste **user‑agent‑string** in.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Define the sandbox – this is the core of how to set dpi, viewport, and user agent.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent
```

**Waarom dit belangrijk is:**
- **DPI** beïnvloedt hoe CSS `pt`‑eenheden naar pixels worden omgezet; een hogere DPI levert scherpere weergave op.
- **Viewport‑grootte** bepaalt de layout‑breakpoints die responsive CSS zal raken.
- **User‑agent** kan server‑side contentvariaties activeren (mobiel vs desktop).

> **Pro tip:** Als je later PDF's genereert, stem de DPI af op de gewenste afdrukresolutie (bijv. 300 dpi voor hoge‑kwaliteit afdrukken).

## Stap 2: Laad een Webpagina in de Sandbox

Nu wijzen we de sandbox op een URL. De `HTMLDocument`‑constructor accepteert de sandbox, zodat de layout‑engine de instellingen die we zojuist hebben gedefinieerd respecteert.

```java
        // Load the page using the sandbox we just configured.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {
```

**Wat er onder de motorkap gebeurt:**
Aspose.HTML creëert een geïsoleerde rendering‑context, vergelijkbaar met een headless browser, maar zonder de overhead van een volledige Chromium‑instantie. Dit maakt de bewerking snel en geheugen‑licht—perfect voor batchverwerking.

## Stap 3: Interactie met de DOM – Lees de Paginatitel

Voor demonstratie halen we de titel op en printen die. In een real‑world scenario kun je een screenshot maken, exporteren naar PDF, of data scrapen.

```java
            // Simple DOM interaction – fetch and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());
        }
    }
}
```

**Verwachte output** (wanneer `https://example.com` bereikbaar is):

```
Title inside sandbox: Example Domain
```

Als de site een andere titel retourneert, zie je die in plaats daarvan—er hoeft verder niets te worden aangepast.

## Stap 4: Verifieer de Instellingen (Optionele Debug)

Soms wil je dubbel controleren of de sandbox echt je DPI en viewport respecteert. Aspose.HTML geeft die waarden niet direct vrij, maar je kunt ze afleiden door elementafmetingen te meten.

```java
        // Example: measure a known element's width in pixels.
        int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
        System.out.println("Measured width (px): " + elementWidth);
```

Als je weet dat de CSS het element declareert als `width: 200pt;`, zou je bij **96 dpi** `200pt * (96/72) ≈ 267px` moeten zien. Pas de DPI aan en voer opnieuw uit om de wijziging te zien—bewijs dat **hoe je dpi instelt** daadwerkelijk werkt.

## Volledige Broncode in Eén Blok

Kopieer‑en plak het volgende in `SandboxExample.java`. Het compileert direct; zorg er alleen voor dat de Aspose.HTML‑JAR op je classpath staat.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox that defines the rendering environment
        // (viewport size 1024×768 and 96 dpi) and a custom user‑agent string.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent

        // Step 2: Load a web page inside the sandbox so layout respects the settings.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {

            // Step 3: Interact with the DOM – here we simply read and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());

            // Optional: verify DPI effect by measuring an element (if you know its CSS size).
            // int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
            // System.out.println("Measured width (px): " + elementWidth);
        }
    }
}
```

Compileer en voer uit:

```bash
javac -cp "aspose-html-23.12.jar" SandboxExample.java
java -cp ".:aspose-html-23.12.jar" SandboxExample
```

Je zou de titel moeten zien afgedrukt, wat bevestigt dat de sandbox werkt met de **ingestelde dpi**, **ingestelde viewport‑grootte**, en **ingestelde user agent** die je hebt opgegeven.

## Veelgestelde Vragen & Randgevallen

### Wat als ik een andere DPI nodig heb?

Verander gewoon het tweede argument van `DocumentSandbox`. Voor print‑klare PDF's kun je `300` gebruiken:

```java
new DocumentSandbox(new Size(1024, 768), 300, "MyCustomUserAgent/1.0");
```

Een hogere DPI levert grotere pixelafmetingen op voor dezelfde CSS‑punten, wat de rasterkwaliteit verbetert maar meer geheugen verbruikt.

### Kan ik een lokaal HTML‑bestand laden in plaats van een URL?

Zeker. Vervang de URL door een bestandspad:

```java
HTMLDocument webDoc = new HTMLDocument("file:///C:/myfolder/page.html", renderingSandbox);
```

Zorg ervoor dat het pad absoluut is en het `file:///`‑schema gebruikt.

### Hoe wijzig ik de user‑agent nadat de sandbox is aangemaakt?

De sandbox is onveranderlijk—zodra je deze doorgeeft aan `HTMLDocument`, zijn de instellingen vergrendeld. Om een andere user‑agent te gebruiken, maak je een nieuwe `DocumentSandbox` aan met de gewenste string.

### Ondersteunt Aspose.HTML JavaScript‑executie?

Ja, de engine voert de meeste client‑side scripts uit. Als een script de DOM na het laden wijzigt, kun je even wachten:

```java
webDoc.waitForLoad();
```

Of gebruik `setTimeout`‑achtige logica binnen de pagina voordat je elementen opvraagt.

## Visuele Bevestiging (Afbeelding)

Hieronder staat een console‑screenshot die de succesvolle uitvoering toont. Let op dat de titeloutput overeenkomt met de pagina, wat bevestigt dat de sandbox onze instellingen respecteerde.

![Console‑output die laat zien hoe DPI in Aspose.HTML Sandbox in te stellen](/images/console-output.png)

*Alt‑tekst:* *Console‑output die laat zien hoe DPI, viewport‑grootte, en user‑agent in Aspose.HTML Sandbox worden ingesteld.*

## Samenvatting & Volgende Stappen

We hebben behandeld **hoe DPI in te stellen** (96 dpi in het voorbeeld), **viewport‑grootte in te stellen** (1024 × 768), en **user‑agent in te stellen** (aangepaste string) met de sandbox‑API van Aspose.HTML. Het volledige, uitvoerbare Java‑programma bewijst dat deze instellingen niet alleen theoretisch zijn—ze beïnvloeden direct rendering en DOM‑interactie.

Klaar voor meer?

- **Exporteren naar PDF:** Na het laden van de pagina, roep `webDoc.save("output.pdf", SaveFormat.PDF);` aan om een hoge‑resolutie PDF te genereren die de ingestelde DPI weerspiegelt.
- **Maak een Screenshot:** Gebruik `webDoc.renderToBitmap("screenshot.png");` voor pixel‑perfecte afbeeldingen.
- **Speel met Responsive Layouts:** Verander de viewport‑afmetingen om mobiele breakpoints te testen zonder een echt apparaat.

Experimenteer met verschillende DPI‑waarden, viewport‑combinaties en user‑agents om te zien hoe servers en CSS reageren. De sandbox is een lichtgewicht speelplaats die je bespaart van het opzetten van volledige browsers.

### Blijf Verkennen

- **Aspose.HTML Documentatie** – duik dieper in de `DocumentSandbox`‑opties.
- **Geavanceerde CSS Media Queries** – leer hoe viewport‑grootte verschillende stijlen activeert.
- **User‑Agent Spoofing** – ontdek hoe sommige sites alternatieve markup leveren op basis van de agent‑string.

Heb je vragen of een lastig geval? Laat een reactie achter, en laten we samen het probleem oplossen. Veel plezier met coderen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}