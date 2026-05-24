---
category: general
date: 2026-02-11
description: Maak een HTML‑document in Java met Aspose.HTML. Leer hoe je JSON‑JavaScript
  kunt ophalen, een script‑element kunt toevoegen, HTML uit JSON kunt genereren en
  JSON naar pre kunt converteren.
draft: false
keywords:
- create html document
- fetch json javascript
- add script element
- generate html from json
- convert json to pre
language: nl
og_description: Maak een HTML‑document in Java met Aspose.HTML. Haal JSON‑JavaScript
  op, voeg een script‑element toe, genereer HTML uit JSON en zet JSON om naar pre—alles
  in één tutorial.
og_title: HTML-document maken in Java – volledige gids
tags:
- Aspose.HTML
- Java
- Web Automation
title: HTML-document maken met Java – JSON ophalen en inhoud genereren
url: /nl/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML-document maken – Volledige Java-tutorial

Heb je ooit **HTML-document maken** on-the-fly moeten **maken**, maar wist je niet hoe je externe gegevens erin kon halen? Je bent niet de enige. In veel projecten wil je JSON ophalen met JavaScript, het resultaat in een pagina injecteren en vervolgens de uiteindelijke markup opslaan als een statisch bestand. Deze gids laat je precies zien hoe je dat doet met Aspose.HTML voor Java.

We lopen elke stap door: van het instantieren van een leeg document, tot **fetch JSON JavaScript**, tot **add script element**, en uiteindelijk tot **generate HTML from JSON** en **convert JSON to pre** tags. Aan het einde heb je een kant‑klaar `fetchResult.html` dat de opgehaalde gegevens bevat, weergegeven als mooi opgemaakte JSON.

## Vereisten

- Java 17 of nieuwer (de code compileert ook met JDK 11+)
- Aspose.HTML for Java bibliotheek (beschikbaar via Maven Central)
- Basiskennis van HTML en async JavaScript
- Een IDE of gewone `javac`/`java` commandoregel

Er zijn geen extra frameworks nodig—alles draait lokaal.

## Stap 1: Het project opzetten en Aspose.HTML importeren

Voeg eerst de Aspose.HTML‑dependency toe aan je `pom.xml` (of download de JAR handmatig).

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- latest as of Feb 2026 -->
</dependency>
```

> **Pro tip:** Houd het versienummer up‑to‑date; nieuwere releases verhelpen bugs en verbeteren de scriptengine.

## Stap 2: **HTML-document maken** – het lege canvas

We beginnen met het aanmaken van een lege `HTMLDocument`. Beschouw het als een frisse pagina waarop we later ons script plaatsen.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();
```

Waarom hebben we een documentobject nodig? De `ScriptEngine` van Aspose.HTML werkt tegen een DOM, niet tegen een ruwe string. Door een correct document te bouwen geven we de engine een echte omgeving om onze **fetch JSON JavaScript** uit te voeren.

## Stap 3: Schrijf de JavaScript‑snippet – **Fetch JSON JavaScript** en **Convert JSON to pre**

Het hart van de tutorial bevindt zich in deze meerregelige string. Het voert een asynchrone `fetch` uit, parseert de JSON en schrijft vervolgens een `<pre>`‑element met mooi opgemaakte gegevens.

```java
        // Step 3: Define a JavaScript snippet that fetches JSON data and injects it into the page
        String fetchScript = """
            (async function() {
                const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                const data = await response.json();
                // Convert JSON to <pre> for readable formatting
                document.body.innerHTML = '<pre>' + JSON.stringify(data, null, 2) + '</pre>';
            })();
            """;
```

Let op de opmerking *Convert JSON to <pre>* – dat is precies wat de `JSON.stringify(..., null, 2)`‑aanroep doet. Het voegt inspringing toe, waardoor de output mens‑leesbaar wordt.

## Stap 4: **Script‑element toevoegen** aan het document

Nu maken we een `<script>`‑tag, plaatsen onze code erin en voegen deze toe aan de body. Dit is het **add script element**‑deel.

```java
        // Step 4: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);
```

Waarom aan de body toevoegen? In een echte browser zou het script direct na het parsen uitgevoerd worden. Door het aan de DOM toe te voegen bootsen we dat exacte gedrag na, zodat de asynchrone fetch wordt uitgevoerd wanneer we later de engine aanroepen.

## Stap 5: Script‑engine uitvoeren – Laat de async fetch voltooien

Aspose.HTML biedt een `ScriptEngine` die de DOM‑gebaseerde JavaScript kan uitvoeren. We roepen `run()` aan en wachten tot de promise‑keten is afgehandeld.

```java
        // Step 5: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();
```

De engine blokkeert tot alle lopende taken (onze fetch) zijn afgehandeld, waardoor gegarandeerd wordt dat de gegenereerde HTML de gegevens al bevat.

## Stap 6: **HTML genereren vanuit JSON** – Resultaat opslaan

Tot slot slaan we het document op schijf op. Het bestand bevat nu het `<pre>`‑blok met de JSON‑payload.

```java
        // Step 6: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

Het uitvoeren van het programma produceert `fetchResult.html`. Open het in een browser en je ziet iets als:

```html
<pre>{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}</pre>
```

Dat is het **generate HTML from JSON**‑resultaat waar je naar op zoek was.

## Volledig werkend voorbeeld

Hieronder staat het volledige, kant‑klaar te draaien bronbestand. Kopieer, plak, pas het uitvoerpad aan en voer `java JsFetchExample` uit.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();

        // Step 2: Define a JavaScript snippet that fetches JSON data and injects it into the page
        String fetchScript = """
            (async function() {
                const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                const data = await response.json();
                // Convert JSON to <pre> for readable formatting
                document.body.innerHTML = '<pre>' + JSON.stringify(data, null, 2) + '</pre>';
            })();
            """;

        // Step 3: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);

        // Step 4: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();

        // Step 5: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

## Verwachte output & verificatie

1. **Console:** Je ziet `HTML with fetched data saved.`  
2. **Bestand (`fetchResult.html`):** Bij openen wordt de JSON binnen een `<pre>`‑blok weergegeven, mooi ingesprongen.  
3. **Validatie:** Als je de paginabron bekijkt, vind je alleen een `<pre>`‑element—geen extra script‑tags meer omdat de engine ze al heeft uitgevoerd.

## Veelgestelde vragen & randgevallen

| Vraag | Antwoord |
|----------|--------|
| *Wat als de API een fout retourneert?* | Plaats de `fetch`‑aanroep in een `try…catch`‑blok en schrijf een foutmelding naar de body in plaats van de JSON. |
| *Kan ik meerdere bronnen ophalen?* | Ja—keten gewoon extra `await fetch(...)`‑aanroepen of gebruik `Promise.all`. De uiteindelijke `innerHTML` kan meerdere `<pre>`‑blokken aan elkaar plakken. |
| *Moet ik CORS‑headers instellen?* | Aangezien het script draait binnen de sandbox van Aspose.HTML, respecteert het het same‑origin‑beleid. Het openbare JSONPlaceholder‑endpoint staat al cross‑origin‑verzoeken toe. |
| *Hoe wijzig ik de uitvoermap tijdens runtime?* | Geef het pad door als command‑line‑argument (`args[0]`) en vervang de hard‑gecodeerde string in `htmlDoc.save`. |
| *Is er een manier om CSS in te sluiten voor styling?* | Zeker. Maak een `<style>`‑element, stel de `textContent` in op je CSS, en voeg het toe aan `<head>` voordat je de engine start. |

## Tips voor productiegebruik

- **Cache de JSON** als het endpoint traag is; je kunt de opgehaalde string naar een bestand schrijven en opnieuw gebruiken.
- **Sanitize de data** voordat je deze injecteert, vooral als de bron niet vertrouwd is. Gebruik `JSON.stringify` veilig of escape HTML‑entities.
- **Configureer de ScriptEngine‑timeout** (`scriptEngine.setTimeout(5000)`) om vastlopen bij niet‑responsieve services te voorkomen.

## Visuele samenvatting

![voorbeeld van html-document maken dat de gegenereerde HTML met JSON binnen een pre‑tag toont](fetchResult.png "Schermafbeelding van het gegenereerde HTML‑document")

*Alt‑tekst:* *voorbeeld van html‑document maken – gegenereerd HTML‑bestand dat opgehaalde JSON weergeeft binnen een pre‑element.*

## Conclusie

Je weet nu hoe je programmatically in Java **HTML-document** kunt **maken**, **fetch JSON JavaScript** kunt **uitvoeren**, **script‑element kunt toevoegen**, **HTML kunt genereren vanuit JSON**, en **JSON naar pre** kunt **converteren** voor leesbare output. De volledige workflow draait offline, vereist alleen Aspose.HTML, en produceert een schoon statisch bestand dat je overal kunt serveren.

Probeer vervolgens het script uit te breiden om over een array van objecten te itereren, CSS‑styling toe te voegen, of meerdere pagina's te genereren met dezelfde techniek. Je kunt ook de `fetch`‑URL vervangen door je eigen API om dynamische gegevens om te zetten in statische snapshots—perfect voor SEO‑vriendelijke pre‑rendering.

Veel plezier met coderen, en deel gerust je experimenten in de reacties!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}