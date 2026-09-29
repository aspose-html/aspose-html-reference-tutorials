---
category: general
date: 2026-09-29
description: Leer hoe je elementen selecteert op basis van klasse, HTML uit een bestand
  leest en externe links vindt in Java. Deze stapsgewijze gids behandelt het efficiënt
  itereren over een NodeList.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- select elements by class
- read html from file
- find external links
- iterate nodelist java
- use queryselectorall java
language: nl
lastmod: 2026-09-29
og_description: Selecteer elementen op basis van klasse in Java, lees HTML uit een
  bestand en vind externe links met querySelectorAll. Volg het volledige voorbeeld
  om een NodeList te itereren.
og_image_alt: Screenshot showing Java code that selects elements by class from an
  HTML file
og_title: Elementen selecteren op klasse in Java – volledige gids met querySelectorAll
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to select elements by class, read HTML from file, and find
    external links in Java. This step‑by‑step guide covers iterating a NodeList efficiently.
  headline: How to select elements by class in Java using querySelectorAll
  type: TechArticle
- questions:
  - answer: Yes. `Jsoup.parse` treats the input as a fragment and automatically adds
      missing root elements, allowing selectors to work on the fragment’s body.
    question: Does this work with HTML fragments that lack a `<html>` root?
  - answer: The standard Java DOM API (`org.w3c.dom`) does not include `querySelectorAll`.
      Libraries such as **HTMLUnit** or **jodd-lagarto** provide similar methods.
      The pattern shown here—load, select with CSS, iterate—remains the same.
    question: Can I use `querySelectorAll` without jsoup?
  - answer: 'After obtaining each `Element`, you can call `link.attr("href", "newUrl")`
      and then write the document back to disk with `Files.writeString`. ## Conclusion
      You now know how to **select elements by class**, **read HTML from file**, **find
      external links**, and **iterate a NodeList in Java** using `qu'
    question: What if I need to modify the links instead of just printing them?
  type: FAQPage
tags:
- Java
- HTML parsing
- DOM manipulation
title: Hoe elementen selecteren op basis van klasse in Java met querySelectorAll
url: /nl/java/creating-managing-html-documents/how-to-select-elements-by-class-in-java-using-queryselectora/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe selecteer je elementen op class in Java met querySelectorAll

Als je **elementen op class** moet selecteren tijdens het verwerken van een HTML‑bestand in Java, laat deze gids je precies zien hoe je dat doet. Je leert HTML uit een bestand te lezen, `querySelectorAll` te gebruiken om externe links te vinden, en de resulterende `NodeList` veilig te itereren.

Werken met HTML in Java voelt vaak zwaar, maar moderne bibliotheken bieden je een beknopte, CSS‑selector‑gebaseerde API. Het voorbeeld hieronder gebruikt **jsoup** (versie 1.17.2) omdat het `querySelectorAll`‑achtige selectors implementeert en een `Elements`‑collectie retourneert die zich gedraagt als een `NodeList`. Je kunt dezelfde logica aanpassen voor andere DOM‑implementaties indien nodig.

## Vereisten

* JDK 17 of nieuwer geïnstalleerd.
* Maven of Gradle voor afhankelijkheidsbeheer.
* Basiskennis van Java‑streams en het DOM‑model.

Voeg jsoup toe aan je project:

```xml
<!-- Maven -->
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

```gradle
// Gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

## Stap 1: HTML uit bestand lezen

De eerste taak is het HTML‑document van de schijf te laden. `Jsoup.parse(Path, Charset)` leest het bestand en bouwt een DOM‑boom die je kunt doorzoeken.

```java
import java.nio.file.Paths;
import java.nio.charset.StandardCharsets;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class HtmlLoader {
    /**
     * Loads an HTML file and returns a Jsoup Document.
     *
     * @param filePath absolute or relative path to the HTML file
     * @return parsed Document ready for DOM queries
     * @throws IOException if the file cannot be read
     */
    public static Document load(String filePath) throws IOException {
        return Jsoup.parse(Paths.get(filePath).toFile(),
                           StandardCharsets.UTF_8.name(),
                           "");
    }
}
```

*Waarom dit belangrijk is*: Het bestand één keer laden voorkomt herhaald I/O terwijl je later over elementen iterereert. Het `Document`‑object bevat de volledige DOM, waardoor snelle selector‑queries mogelijk zijn.

## Stap 2: Gebruik `querySelectorAll` om elementen op class te selecteren

Nu het document in het geheugen staat, kun je **elementen op class** selecteren met een CSS‑selector. De selector `"a.external"` komt overeen met `<a>`‑tags die de `external`‑class hebben—precies wat je nodig hebt om **externe links te vinden**.

```java
import org.jsoup.select.Elements;
import org.jsoup.nodes.Element;

/**
 * Returns all anchor elements with the CSS class "external".
 *
 * @param doc the parsed HTML document
 * @return a collection of matching Elements
 */
public static Elements findExternalLinks(Document doc) {
    // querySelectorAll is simulated by the select() method in Jsoup
    return doc.select("a.external");
}
```

*Waarom dit belangrijk is*: Het gebruik van een class‑selector is zowel expressief als performant. De bibliotheek vertaalt de selector naar een geoptimaliseerde traversie, zodat je geen handmatige lussen over elke node hoeft te schrijven.

## Stap 3: Iterate de NodeList (Elements) in Java

`Elements` implementeert `Iterable<Element>`, wat betekent dat je een standaard `for‑each`‑lus kunt gebruiken om **NodeList Java**‑objecten te itereren. De onderstaande lus print de `href`‑attribuut van elke link.

```java
/**
 * Prints the href attribute of every external link.
 *
 * @param externalLinks collection returned by findExternalLinks()
 */
public static void printExternalLinks(Elements externalLinks) {
    for (Element link : externalLinks) {
        System.out.println("External link: " + link.attr("href"));
    }
}
```

*Waarom dit belangrijk is*: Direct itereren houdt de code leesbaar en voorkomt de overhead van het omzetten van de collectie naar een stream wanneer je alleen eenvoudige output nodig hebt.

## Volledig werkend voorbeeld

Door de drie stappen te combineren krijg je een zelfstandig programma dat je vanaf de commandoregel kunt uitvoeren.

```java
import java.io.IOException;
import org.jsoup.nodes.Document;
import org.jsoup.select.Elements;

public class ExternalLinkExtractor {

    public static void main(String[] args) {
        // Validate input
        if (args.length != 1) {
            System.err.println("Usage: java ExternalLinkExtractor <input.html>");
            System.exit(1);
        }

        String inputPath = args[0];

        try {
            // Step 1: read HTML from file
            Document doc = HtmlLoader.load(inputPath);

            // Step 2: select elements by class (find external links)
            Elements externalLinks = findExternalLinks(doc);

            // Step 3: iterate NodeList Java and print hrefs
            printExternalLinks(externalLinks);
        } catch (IOException e) {
            System.err.println("Error reading file: " + e.getMessage());
        }
    }

    // Reuse methods from previous sections
    private static Elements findExternalLinks(Document doc) {
        return doc.select("a.external");
    }

    private static void printExternalLinks(Elements externalLinks) {
        for (org.jsoup.nodes.Element link : externalLinks) {
            System.out.println("External link: " + link.attr("href"));
        }
    }
}
```

### Verwachte output

Aangenomen dat `input.html` bevat:

```html
<a class="external" href="https://example.com">Example</a>
<a class="internal" href="/about">About</a>
<a class="external" href="https://openai.com">OpenAI</a>
```

Het uitvoeren van het programma print:

```
External link: https://example.com
External link: https://openai.com
```

## Pro‑tips en veelvoorkomende valkuilen

* **Encoding is belangrijk** – Lees het bestand altijd met UTF‑8 (of de charset die bij je bron past). Een onjuiste encoding kan tekens in attribuutwaarden corrupt maken.
* **Meerdere classes** – Als een element meerdere classes heeft (bijv. `class="btn external"`), komt de selector `"a.external"` nog steeds overeen omdat CSS‑class‑selectors controleren op de aanwezigheid van het token, niet op de exacte string.
* **Performance‑tip** – Als je alleen het `href`‑attribuut nodig hebt, kun je dit direct opvragen met `doc.select("a.external[href]").eachAttr("href")`. Dit voorkomt het aanmaken van volledige `Element`‑objecten voor elke match.
* **Null‑veiligheid** – `link.attr("href")` retourneert een lege string als het attribuut ontbreekt, dus je hoeft geen null‑check uit te voeren vóór het afdrukken.

## Veelgestelde vragen

**Q: Werkt dit met HTML‑fragmenten die geen `<html>`‑root hebben?**  
A: Ja. `Jsoup.parse` behandelt de invoer als een fragment en voegt automatisch ontbrekende root‑elementen toe, waardoor selectors werken op de body van het fragment.

**Q: Kan ik `querySelectorAll` gebruiken zonder jsoup?**  
A: De standaard Java DOM‑API (`org.w3c.dom`) bevat geen `querySelectorAll`. Bibliotheken zoals **HTMLUnit** of **jodd-lagarto** bieden vergelijkbare methoden. Het hier getoonde patroon—laden, selecteren met CSS, itereren—blijft hetzelfde.

**Q: Wat als ik de links moet aanpassen in plaats van ze alleen af te drukken?**  
A: Nadat je elk `Element` hebt verkregen, kun je `link.attr("href", "newUrl")` aanroepen en vervolgens het document terug naar schijf schrijven met `Files.writeString`.

## Conclusie

Je weet nu hoe je **elementen op class** kunt **lezen uit een HTML‑bestand**, **externe links kunt vinden**, en **een NodeList in Java kunt itereren** met `querySelectorAll`‑achtige selectors. Het volledige voorbeeld toont een nette, productie‑klare workflow die je kunt integreren in grotere scraping‑ of transformatie‑pijplijnen.

Vervolgens kun je gerelateerde onderwerpen verkennen, zoals **dynamische content parsen met HTMLUnit**, **gewijzigde HTML terug naar schijf schrijven**, of **Java‑streams gebruiken om link‑URL's in een lijst te verzamelen**. Elk van deze bouwt voort op de kerntechniek van class‑gebaseerde selectie die hier wordt gedemonstreerd. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe HTML in Java te queryen – Elementen selecteren, filteren op attribuut, en tekst ophalen](/html/english/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/)
- [NodeList Java itereren – HTML lezen & Image src ophalen](/html/english/java/creating-managing-html-documents/iterate-nodelist-java-read-html-get-image-src/)
- [HTML‑documenten laden vanuit bestand in Aspose.HTML voor Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}