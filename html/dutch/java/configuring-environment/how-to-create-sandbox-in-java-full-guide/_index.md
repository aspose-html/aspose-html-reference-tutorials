---
category: general
date: 2026-03-15
description: 'Hoe een sandbox in Java te maken: leer de schermgrootte in te stellen,
  netwerktoegang uit te schakelen en een HTML‑document veilig te laden.'
draft: false
keywords:
- how to create sandbox
- set screen size
- disable network access
- load html document
- how to render html
language: nl
og_description: Hoe maak je een sandbox in Java en render je HTML veilig. Stapsgewijze
  gids over schermgrootte, netwerkrestricties en het laden van documenten.
og_title: Hoe een sandbox in Java te maken – Complete tutorial
tags:
- Java
- Aspose.HTML
- Security
title: Hoe maak je een sandbox in Java – volledige gids
url: /nl/java/configuring-environment/how-to-create-sandbox-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een Sandbox in Java te Maken – Volledige Gids

Heb je je ooit afgevraagd **hoe je een sandbox** kunt maken voor het renderen van onbetrouwbare webinhoud in Java? Je bent niet de enige. Veel ontwikkelaars hebben een veilige omgeving nodig waar HTML kan worden gerenderd zonder het hostsysteem in gevaar te brengen, en de Aspose.HTML Sandbox maakt dat een eitje. In deze tutorial lopen we door het instellen van de schermgrootte, het uitschakelen van netwerktoegang, het laden van een HTML‑document en uiteindelijk het renderen – allemaal binnen een gesandboxte omgeving.

> **Wat je krijgt:** een compleet, uitvoerbaar code‑voorbeeld, uitleg van elke regel, en praktische tips die je behoeden voor veelvoorkomende valkuilen. Geen externe documentatie nodig; alles wat je nodig hebt staat hier.

## Wat Je Nodig Hebt

- **Java 8+** (de code gebruikt standaard Java‑syntaxis, niets exotisch)
- **Aspose.HTML for Java**‑bibliotheek (versie 23.10 of nieuwer)
- Een IDE of eenvoudige teksteditor – Visual Studio Code werkt prima
- Internettoegang *alleen* voor het downloaden van de bibliotheek; de sandbox zelf werkt offline

Zodra je dat hebt, kun je meteen beginnen.

![How to create sandbox diagram](sandbox-diagram.png){alt="Hoe een sandbox in Java maken diagram"}

## Hoe een Sandbox te Maken – Overzicht

De sandbox is in wezen een container die beperkt wat de HTML‑engine mag doen. Beschouw het als een mini‑browser die in een gesandboxte kamer leeft: jij bepaalt hoe groot het venster is (`set screen size`), of het toegang heeft tot het web (`disable network access`), en welk HTML‑bestand het moet openen (`load html document`). Aan het einde van deze gids zie je precies hoe al deze onderdelen in elkaar passen.

## Stap 1: Schermgrootte Instellen

Wanneer je `SandboxConfiguration` instantiateert, kun je de renderengine vertellen welke viewport hij moet emuleren. Dit is handig als je later screenshots of PDF‑conversie wilt maken met een specifieke lay‑out.

```java
// Step 1: Define sandbox constraints – screen size
SandboxConfiguration sandboxConfig = new SandboxConfiguration();
sandboxConfig.setScreenWidth(1024);   // width in pixels
sandboxConfig.setScreenHeight(768);   // height in pixels
```

Het instellen van een realistische schermgrootte zorgt ervoor dat CSS‑media‑queries zich gedragen zoals verwacht. Als je deze stap overslaat, valt de engine terug op een kleine 800×600‑viewport, wat responsieve ontwerpen kan breken.

**Waarom het belangrijk is:** Veel moderne sites verbergen of herschikken content op basis van de viewport‑afmetingen. Door expliciet `set screen size` aan te roepen, garandeer je consistente weergave bij elke uitvoering.

## Stap 2: Netwerktoegang Uitschakelen

Security‑first ontwikkelaars willen elke uitgaande traffic blokkeren. Met de sandbox kun je dat met één enkele vlag doen.

```java
// Step 2: Turn off network calls – disable network access
sandboxConfig.setEnableNetworkAccess(false);
```

Wanneer `disable network access` true is, wordt elke `<script src="...">`, afbeelding‑URL of CSS‑import die naar een externe host wijst simpelweg genegeerd. Dit voorkomt dat kwaadaardige payloads contact opnemen met een command‑and‑control server.

> **Pro tip:** Als je later een enkel vertrouwd resource moet ophalen, kun je tijdelijk netwerktoegang inschakelen voor die specifieke oproep en daarna weer uitschakelen.

## Stap 3: HTML‑Document Laden Binnen de Sandbox

Nu de sandbox geconfigureerd is, maken we de sandbox‑instantie aan en voeren we een HTML‑bestand in. In dit voorbeeld wijzen we naar `https://example.com`, maar je kunt net zo goed een lokaal bestand laden met `new HTMLDocument("file:///path/to/file.html", sandbox)`.

```java
// Step 3: Create the sandbox and load the HTML document
Sandbox sandbox = new Sandbox(sandboxConfig);

try (HTMLDocument htmlDoc = new HTMLDocument("https://example.com", sandbox)) {
    // Step 4 will happen inside this block
    System.out.println("Document title: " + htmlDoc.getTitle());
}
```

Let op het **try‑with‑resources**‑blok – dit garandeert dat het document correct wordt vrijgegeven, waardoor native resources worden vrijgemaakt. Het aanroepen van `load html document` gebeurt automatisch wanneer je `HTMLDocument` construeert met het sandbox‑argument.

**Wat je zult zien:** Als je het programma uitvoert, print de console de titel van de pagina, bijvoorbeeld `Document title: Example Domain`. Dat bevestigt dat de HTML succesvol is geparseerd binnen de sandbox.

## Stap 4: HTML Renderen en Output Verifiëren

Renderen kan veel betekenen: tekenen naar een bitmap, een PDF genereren, of simpelweg de DOM extraheren. Voor deze tutorial blijven we bij de eenvoudigste verificatie – het printen van de titel. Als je een visuele render nodig hebt, biedt Aspose.HTML `HTMLRenderer`:

```java
// Optional: render to an image (demonstrates how to render html)
HTMLRenderer renderer = new HTMLRenderer(htmlDoc);
renderer.renderToFile("output.png", ImageFormat.PNG);
System.out.println("Rendered image saved as output.png");
```

Het volledige programma uitvoeren geeft nu twee bewijzen dat de sandbox werkt:

1. **Console‑output** met de paginatitel (bewijst dat `load html document` geslaagd is).
2. **output.png**‑bestand (bewijst dat `how to render html` daadwerkelijk iets tekent).

## Compleet, Uitvoerbaar Voorbeeld

Hieronder staat het volledige programma dat je kunt kopiëren‑plakken in een bestand met de naam `SandboxDemo.java`. Het bevat alle imports, de configuratiestappen en het optionele render‑blok.

```java
import com.aspose.html.sandbox.*;
import com.aspose.html.*;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Define sandbox constraints – set screen size
        SandboxConfiguration sandboxConfig = new SandboxConfiguration();
        sandboxConfig.setScreenWidth(1024);
        sandboxConfig.setScreenHeight(768);
        // Step 2: Disable network access for security
        sandboxConfig.setEnableNetworkAccess(false);

        // Step 3: Create the sandbox instance using the configuration
        Sandbox sandbox = new Sandbox(sandboxConfig);

        // Step 4: Load an HTML document inside the sandboxed environment
        try (HTMLDocument htmlDoc = new HTMLDocument("https://example.com", sandbox)) {
            // Verify that the document loaded – print its title
            System.out.println("Document title: " + htmlDoc.getTitle());

            // Optional: render the page to an image (demonstrates how to render html)
            HTMLRenderer renderer = new HTMLRenderer(htmlDoc);
            renderer.renderToFile("output.png", ImageFormat.PNG);
            System.out.println("Rendered image saved as output.png");
        }
    }
}
```

**Verwachte output (console):**

```
Document title: Example Domain
Rendered image saved as output.png
```

En je vindt `output.png` in je projectmap, een snapshot van `example.com` gerenderd op 1024×768 pixels.

## Veelvoorkomende Valkuilen en Pro Tips

| Probleem | Waarom het gebeurt | Hoe op te lossen |
|----------|--------------------|------------------|
| **Ontbrekende `sandboxConfig.setEnableNetworkAccess(false)`** | De engine haalt stilletjes externe assets op, waardoor het sandbox‑doel wordt ondermijnd. | Stel deze vlag altijd in, zelfs als je denkt dat de pagina zelf‑voorzienend is. |
| **Een externe URL gebruiken zonder netwerktoegang** | Het document kan niet geladen worden omdat de sandbox het verzoek blokkeert. | Schakel netwerktoegang tijdelijk in voor die oproep of download de HTML eerst en laad deze vanaf schijf. |
| **Viewport komt niet overeen met CSS‑media‑queries** | Layout ziet er kapot uit omdat de standaardgrootte te klein is. | Gebruik `setScreenWidth` en `setScreenHeight` om overeen te komen met je doelapparaat. |
| **Vergeten `HTMLDocument` te sluiten** | Native geheugenlekken kunnen zich opstapelen in langdurige services. | Gebruik try‑with‑resources zoals getoond, of roep handmatig `htmlDoc.dispose()` aan. |

## De Sandbox Uitbreiden: Praktijkvoorbeelden

- **PDF‑generatie:** Vervang `HTMLRenderer` door `HTMLToPDFConverter` om de geladen pagina om te zetten naar een PDF, terwijl de sandbox‑limieten behouden blijven.
- **Batchverwerking:** Loop over een lijst met URL’s en hergebruik dezelfde `Sandbox`‑instantie om de overhead van telkens een nieuwe sandbox te creëren te vermijden.
- **Aangepaste Resource Handlers:** Implementeer `IResourceHandler` om afbeeldingen of stylesheets in‑memory te leveren, waardoor je fijnmazige controle krijgt over wat de sandbox mag zien.

## Samenvatting

We hebben behandeld **hoe je een sandbox** in Java vanaf nul maakt, **set screen size** gedemonstreerd, laten zien hoe je **network access uitschakelt**, doorlopen hoe je **load html document** uitvoert, en een korte blik geworpen op **how to render html** naar een afbeelding. Het volledige voorbeeld werkt direct, en de toelichtingen beantwoorden het “waarom” achter elke configuratie‑vlag.

Klaar voor de volgende stap? Vervang de URL door een lokaal HTML‑bestand dat een klein script bevat, en schakel `disable network access` in om te zien hoe het script stilletjes wordt genegeerd. Of experimenteer met verschillende viewport‑groottes om responsieve lay‑outs te laten verschuiven.

Heb je vragen, edge‑case scenario’s, of wil je je eigen sandbox‑trucs delen? Laat een reactie achter – laten we het gesprek gaande houden. Veel plezier met sandboxen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}