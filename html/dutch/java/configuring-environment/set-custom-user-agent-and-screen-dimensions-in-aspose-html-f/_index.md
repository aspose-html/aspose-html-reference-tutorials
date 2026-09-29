---
category: general
date: 2026-09-29
description: Stel een aangepaste user‑agent in Aspose.HTML voor Java in en leer hoe
  je de virtuele schermgrootte kunt instellen voor nauwkeurige HTML‑weergave.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom user agent
- set virtual screen size
- specify user agent
- set screen dimensions
- set screen width
language: nl
lastmod: 2026-09-29
og_description: Stel een aangepaste user‑agent in Aspose.HTML voor Java in en leer
  hoe je de virtuele schermgrootte instelt voor nauwkeurige HTML‑weergave.
og_image_alt: Diagram showing how to set custom user agent and screen dimensions in
  a Java sandbox
og_title: Stel een aangepaste user-agent en schermafmetingen in Aspose.HTML voor Java
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Set custom user agent in Aspose.HTML for Java and learn how to set
    virtual screen size for accurate HTML rendering.
  headline: Set custom user agent and screen dimensions in Aspose.HTML for Java
  type: TechArticle
tags:
- Aspose.HTML
- Java
- sandbox
- user agent
- screen size
title: Stel aangepaste user‑agent en schermafmetingen in Aspose.HTML voor Java
url: /nl/java/configuring-environment/set-custom-user-agent-and-screen-dimensions-in-aspose-html-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Stel een aangepaste user‑agent en schermafmetingen in Aspose.HTML voor Java in

Als je een **aangepaste user‑agent** wilt instellen tijdens het renderen van HTML met Aspose.HTML voor Java, laat deze gids je precies zien hoe dat moet. Door een sandbox te configureren krijg je ook de mogelijkheid om een **virtuele schermgrootte** in te stellen, zodat de lay‑out overeenkomt met een echt browser‑viewport.

Je rondt deze tutorial af met een compleet, uitvoerbaar programma dat **user‑agent specificeert**, **schermbreedte instelt** en **schermhoogte instelt**. Er zijn geen externe tools nodig—alleen Aspose.HTML voor Java en een Java 8+ runtime.

## Wat je zult leren

* Hoe je een `SandboxConfiguration` maakt om het renderen te isoleren.  
* Hoe je **een aangepaste user‑agent instelt** en waarom dat belangrijk is voor responsieve pagina’s.  
* Hoe je **virtuele schermgrootte instelt** (schermbreedte en -hoogte) voor een nauwkeurige lay‑out.  
* Hoe je een HTML‑bestand laadt in de sandbox en het verwerkte resultaat opslaat.  
* Veelvoorkomende valkuilen en best‑practice‑tips voor sandbox‑renderen.

> **Prerequisites** – Je hebt een geldige Aspose.HTML voor Java‑licentie, Java 8 of nieuwer, en een IDE (IntelliJ IDEA, Eclipse of VS Code) nodig. Het voorbeeld gebruikt een lokaal `input.html`‑bestand, maar elke bereikbare URL werkt.

![Sandbox stroomdiagram](sandbox-flow.png "voorbeeld van aangepaste user agent instellen in Java")

## Stap 1: Maak een sandbox‑configuratie (de basis)

De sandbox isoleert de renderomgeving van de host‑JVM, wat essentieel is wanneer je een **aangepaste user‑agent** wilt **instellen** of de viewport‑grootte wilt wijzigen.

```java
import com.aspose.html.sandbox.SandboxConfiguration;

// Create a fresh sandbox configuration object
SandboxConfiguration sandboxConfig = new SandboxConfiguration();
```

*Waarom deze stap?*  
`SandboxConfiguration` bevat alle renderopties, inclusief **schermafmetingen** en **user‑agent**‑strings. Door het vóór het laden van het document te configureren, garandeer je dat de HTML‑engine die instellingen vanaf het eerste verzoek respecteert.

## Stap 2: Stel schermafmetingen in om een echt apparaat na te bootsen

Responsieve sites lezen vaak `window.innerWidth` en `window.innerHeight`. Om de engine te laten denken dat hij draait op een scherm van 1024 × 768, **stel je de virtuele schermgrootte in**:

```java
// Define the virtual screen size for the sandboxed document
sandboxConfig.setScreenWidth(1024);   // set screen width
sandboxConfig.setScreenHeight(768);   // set screen height
```

*Waarom dit belangrijk is* – Als je **schermafmetingen niet instelt**, kan de renderer standaard een heel klein viewport gebruiken, waardoor CSS‑media‑queries de mobiele lay‑out kiezen. Door expliciet **schermbreedte** en **schermhoogte** in te stellen, bepaal je welke CSS‑regels worden toegepast.

## Stap 3: Specificeer een aangepaste user‑agent‑string

Sommige webpagina’s leveren verschillende inhoud op basis van de user‑agent‑header. Om **user‑agent te specificeren** stel je deze simpelweg in op de sandbox‑configuratie:

```java
// Set a custom user‑agent string that will be sent during resource loading
sandboxConfig.setUserAgent("AsposeHTML/1.0");
```

*Waarom een aangepaste user‑agent gebruiken?*  
Een aangepaste string kan botdetectie omzeilen, desktop‑only functionaliteit activeren, of testen hoe een site zich gedraagt voor een specifieke browser‑versie. De Aspose‑engine stuurt deze waarde mee met elk HTTP‑verzoek dat wordt gedaan tijdens het laden van externe bronnen (CSS, afbeeldingen, scripts).

## Stap 4: Laad het HTML‑document binnen de sandbox

Nu de sandbox volledig geconfigureerd is, laad je het HTML‑bestand. De constructor die een bestandspad en een `SandboxConfiguration` accepteert, past automatisch alle instellingen toe die we hebben gedefinieerd.

```java
import com.aspose.html.HTMLDocument;

// Load the HTML file using the previously configured sandbox
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);
```

Als je van een externe URL wilt laden, vervang je het bestandspad door de URL‑string—Aspose.HTML respecteert nog steeds de **aangepaste user‑agent** en **schermafmetingen**.

## Stap 5: Sla de verwerkte output op

Nadat het document klaar is met laden, kun je het opslaan in elk ondersteund formaat. Hier schrijven we een gesandboxte HTML‑file die eventuele DOM‑wijzigingen weerspiegelt die door de aangepaste instellingen zijn veroorzaakt.

```java
// Save the processed document to the desired output location
document.save("YOUR_DIRECTORY/sandboxed_output.html");
```

Het opgeslagen bestand bevat dezelfde markup, maar scripts die `navigator.userAgent` of `window.innerWidth` hebben opgevraagd, zien nu de waarden die jij hebt opgegeven.

## Volledig, uitvoerbaar voorbeeld

Alle stappen samengevoegd geven je een zelf‑containend programma dat je kunt kopiëren, plakken en uitvoeren.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.SandboxConfiguration;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox configuration to isolate the rendering environment
        SandboxConfiguration sandboxConfig = new SandboxConfiguration();

        // Step 2: Define the virtual screen size for the sandboxed document
        sandboxConfig.setScreenWidth(1024);   // set screen width
        sandboxConfig.setScreenHeight(768);   // set screen height

        // Step 3: Set a custom user‑agent string to be used during loading
        sandboxConfig.setUserAgent("AsposeHTML/1.0"); // set custom user agent

        // Step 4: Load the HTML document within the sandbox using the configuration
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);

        // Step 5: Save the processed document to the desired output location
        document.save("YOUR_DIRECTORY/sandboxed_output.html");
    }
}
```

### Verwachte output

Het uitvoeren van het programma maakt `sandboxed_output.html`. Als je dit bestand in een browser opent en `navigator.userAgent` inspecteert via de console, zie je **AsposeHTML/1.0**. Evenzo zal `window.innerWidth` **1024** rapporteren, wat bevestigt dat **schermafmetingen ingesteld** zijn zoals bedoeld.

## Veelgestelde vragen & edge‑case handling

| Vraag | Antwoord |
|----------|--------|
| **Wat als de pagina extra bronnen laadt van een ander domein?** | De sandbox stuurt de **aangepaste user‑agent** mee met elk verzoek, maar cross‑origin‑beleid blijft van kracht. Gebruik `sandboxConfig.setAllowCrossDomain(true)` als je die beperkingen wilt versoepelen. |
| **Kan ik de schermgrootte wijzigen nadat het document is geladen?** | Nee. Schermafmetingen worden gelezen tijdens de eerste layout‑pass. Om met een andere grootte te renderen, maak je een nieuwe `SandboxConfiguration` en laad je het document opnieuw. |
| **Moet ik `document.close()` aanroepen?** | `HTMLDocument` implementeert `AutoCloseable`. Een try‑with‑resources‑blok zorgt voor correcte opruiming, maar een expliciete `close()` is optioneel in eenvoudige scripts. |
| **Hoe verschilt dit van het instellen van een user‑agent in een HTTP‑client?** | Het instellen van de user‑agent op de sandbox beïnvloedt **alle** resource‑verzoeken die de HTML‑engine maakt, niet alleen de initiële HTML‑opvraag. Dit bootst een echte browser nauwkeuriger na. |
| **Is de sandbox veilig voor onbetrouwbare HTML?** | Ja. De sandbox isoleert bestands‑systeemtoegang en beperkt netwerk‑calls volgens de configuratie, waardoor het risico dat kwaadaardige scripts de host‑JVM beïnvloeden, wordt verminderd. |

## Pro‑tips

* **Herbruik configuraties** – Als je veel pagina’s met dezelfde viewport rendert, maak dan één `SandboxConfiguration` aan en hergebruik deze om overhead van objectcreatie te vermijden.  
* **Debug met logging** – Schakel Aspose.HTML‑logging in (`sandboxConfig.setLogLevel(LogLevel.DEBUG)`) om te zien welke bronnen met de aangepaste user‑agent zijn opgehaald.  
* **Combineer met CSS‑media‑queries** – Door **schermbreedte** aan te passen kun je testen hoe je responsieve ontwerp zich gedraagt op tablets, telefoons of grote desktops zonder een echte browser te openen.

## Conclusie

Je weet nu hoe je **een aangepaste user‑agent** en **schermafmetingen** instelt bij het renderen van HTML met Aspose.HTML voor Java. Door een sandbox te configureren, isoleer je de omgeving, beheer je de viewport, en zorg je ervoor dat externe bronnen exact de headers zien die jij opgeeft. Deze techniek is essentieel voor het testen van responsieve lay‑outs, het omzeilen van bot‑blokkades, of het reproduceren van desktop‑only functionaliteit in geautomatiseerde pipelines.

Vervolgens kun je **leren hoe je aangepaste cookies instelt** of **rendered screenshots vastlegt** met de rendering‑API van Aspose.HTML—beide concepten bouwen voort op hetzelfde sandbox‑configuratie‑patroon dat je nu beheerst.

Happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [High DPI Rendering in Java – Capture Webpage Screenshots with Custom User Agent](/html/english/java/conversion-html-to-various-image-formats/high-dpi-rendering-in-java-capture-webpage-screenshots-with/)
- [How to Load HTML, Set Device DPI & Read Background Color](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Create HTML File Java & Set Up Network Service (Aspose.HTML)](/html/english/java/configuring-environment/setup-network-service/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}