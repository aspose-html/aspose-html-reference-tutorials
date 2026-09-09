---
category: general
date: 2026-01-01
description: Leer hoe je HTML kunt queryen met Java, hoe je CSS selecteert, en elementen
  uit HTML kunt extraheren met praktische voorbeelden en het tellen van knooppunten.
draft: false
keywords:
- how to query html
- how to select css
- extract elements from html
- select multiple css classes
- how to count nodes
language: nl
og_description: Beheers hoe je HTML in Java kunt opvragen, leer hoe je CSS selecteert,
  elementen uit HTML extraheert en knooppunten telt met echte codevoorbeelden.
og_title: Hoe HTML in Java op te vragen – Complete tutorial
tags:
- Java
- HTML parsing
- Aspose.HTML
title: Hoe HTML in Java te queryen – Complete tutorial
url: /nl/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe HTML opvragen in Java – Complete Tutorial

Heb je je ooit afgevraagd **hoe je HTML kunt opvragen** vanuit een Java‑programma zonder je haar uit te trekken? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur wanneer ze data uit een statische catalogus moeten halen of een eenvoudige pagina moeten scrapen, en de gebruikelijke DOM‑trucs voelen omslachtig.  

Het goede nieuws? Met een paar regels code kun je een HTML‑bestand laden, XPath‑ of CSS‑selectoren uitvoeren, en zelfs de knooppunten tellen die je interesseren – allemaal in één nette stroom. In deze gids lopen we **hoe je HTML opvraagt**, **hoe je CSS selecteert**, en laten we zien hoe je **elementen uit HTML haalt**, **meerdere CSS‑klassen selecteert**, en **hoe je knooppunten telt** met Aspose.HTML for Java.

## Wat je gaat leren

- Een HTML‑document laden vanaf schijf of een URL.  
- XPath gebruiken om elementen te vinden die aan complexe voorwaarden voldoen.  
- CSS‑selectoren toepassen, inclusief queries met meerdere klassen.  
- De resultaten programmatic tellen.  
- Tips, valkuilen en variaties voor real‑world scenario’s.

*Voorwaarden*: Java 8+, Maven of Gradle, en een kopie van de Aspose.HTML for Java‑bibliotheek (de gratis trial werkt prima voor experimenten).

---

![how to query html example](https://example.com/images/query-html.png "Screenshot die laat zien hoe je HTML met Java opvraagt")

## Hoe HTML opvragen – Het document laden

Voordat je vragen kunt stellen, heb je een documentobject nodig om te onderzoeken. Aspose.HTML’s `HTMLDocument`‑klasse doet het zware werk.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.Element;
import java.util.List;

public class QueryDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document you want to query
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/catalog.html");
```

> **Waarom dit belangrijk is** – Het laden van het bestand creëert een DOM‑boom in het geheugen. Vanaf daar kun je zowel XPath‑ als CSS‑queries uitvoeren zonder je zorgen te maken over netwerklatentie of slecht gevormde markup. Als het bestand niet wordt gevonden, gooit Aspose een duidelijke `FileNotFoundException`, waardoor debuggen pijnloos is.

### Pro tip
Als je HTML van een externe site haalt, geef je simpelweg de URL‑string door aan `HTMLDocument` — Aspose haalt het op en parseert het voor je.

## Hoe CSS selecteren – Met CSS‑selectoren

Zodra de DOM klaar is, is het selecteren van knooppunten met CSS net zo simpel als één regel code. Laten we elk element pakken dat de `featured`‑ of `highlight`‑klasse heeft.

```java
        // Step 2: Locate elements marked as featured or highlighted using a CSS selector
        List<Element> featuredElements = document.selectCss(".featured, .highlight");

        // Step 3: Output the number of elements found by the CSS selector
        System.out.println("Featured elements: " + featuredElements.size());
```

> **Uitleg** – De selector `.featured, .highlight` vertelt de engine om *elk* element terug te geven waarvan het `class`‑attribuut `featured` **of** `highlight` bevat. Dit is de canonieke manier om **meerdere CSS‑klassen te selecteren** in één query.

### Randgeval
Als een element beide klassen bevat (bijv. `<div class="featured highlight">`), verschijnt het **eenmalig** in de resultaatslijst, waardoor dubbel tellen wordt voorkomen.

## Elementen uit HTML halen – XPath en CSS combineren

XPath blinkt uit wanneer je relationele logica nodig hebt, zoals “alle `<book>`‑knooppunten waarvan de prijs hoger is dan 30”. Hier is het exacte fragment uit het oorspronkelijke voorbeeld:

```java
        // Step 4: Find all <book> elements with a price greater than 30 using XPath
        List<Element> expensiveBooks = document.selectXPath("//book[price>30]");

        // Step 5: Output the number of books that match the XPath query
        System.out.println("Expensive books count: " + expensiveBooks.size());
```

> **Waarom XPath?** – XPath kan numerieke vergelijkingen (`price>30`) direct evalueren, iets wat CSS niet kan. Het laat je ook ouder‑/kind‑relaties traverseren zonder extra code.

### Variatie
Als je de *titels* van die dure boeken wilt ophalen, kun je een tweede query ketenen:

```java
        List<Element> titles = expensiveBooks.get(0).selectXPath("./title");
        System.out.println("First expensive book title: " + titles.get(0).getTextContent());
```

## Meerdere CSS‑klassen selecteren – Geavanceerde selector‑trucs

Soms wil je elementen targeten die **gelijktijdig** meerdere klassen hebben, zoals `class="product featured"`. De CSS‑syntaxis hiervoor is een aaneengeschakelde selector zonder komma’s.

```java
        // Example: select <div> elements that are both .product and .featured
        List<Element> productFeatured = document.selectCss("div.product.featured");
        System.out.println("Product‑featured divs: " + productFeatured.size());
```

> **Belangrijk punt** – Geen spatie tussen de klassennamen; een spatie zou “descendant” betekenen. Dit patroon is essentieel wanneer je **meerdere CSS‑klassen selecteert** die samen een component stylen.

## Hoe knooppunten tellen – Nauwkeurige totalen krijgen

Knooppunten tellen is vaak de laatste stap in een data‑extractiepijplijn. Je hebt al `list.size()` gezien na elke query, maar laten we het in een herbruikbare helper plaatsen.

```java
    /**
     * Returns the count of elements that match the given CSS selector.
     */
    private static int countByCss(HTMLDocument doc, String selector) {
        return doc.selectCss(selector).size();
    }

    /**
     * Returns the count of elements that match the given XPath expression.
     */
    private static int countByXPath(HTMLDocument doc, String xpath) {
        return doc.selectXPath(xpath).size();
    }

    public static void main(String[] args) throws Exception {
        HTMLDocument doc = new HTMLDocument("YOUR_DIRECTORY/catalog.html");

        System.out.println("Expensive books: " + countByXPath(doc, "//book[price>30]"));
        System.out.println("Featured items: " + countByCss(doc, ".featured, .highlight"));
        System.out.println("Product‑featured divs: " + countByCss(doc, "div.product.featured"));
    }
```

> **Waarom inpakken?** – Het centraliseren van de tel‑logica maakt je code makkelijker te testen en vermindert duplicatie. Het verduidelijkt bovendien **hoe je knooppunten telt** voor toekomstige lezers.

### Veelvoorkomende valkuilen
- **Witruimte in class‑attributen** – `"featured "` (trailing space) matcht nog steeds `.featured` omdat de selector witruimte trimt.
- **Hoofdlettergevoeligheid** – HTML‑klassennamen zijn hoofdlettergevoelig in XML‑modus; zorg ervoor dat je bron‑HTML consistente hoofdlettergebruik heeft.

## Volledig werkend voorbeeld

Alles samengevoegd, hier is een zelfstandige programma‑code die je kunt copy‑pasten in je IDE:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.Element;
import java.util.List;

public class QueryDemo {

    private static int countByCss(HTMLDocument doc, String selector) {
        return doc.selectCss(selector).size();
    }

    private static int countByXPath(HTMLDocument doc, String xpath) {
        return doc.selectXPath(xpath).size();
    }

    public static void main(String[] args) throws Exception {
        // Load the HTML file (adjust the path as needed)
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/catalog.html");

        // XPath: books priced over 30
        int expensiveBooks = countByXPath(document, "//book[price>30]");
        System.out.println("Expensive books count: " + expensiveBooks);

        // CSS: featured or highlighted elements
        int featured = countByCss(document, ".featured, .highlight");
        System.out.println("Featured elements: " + featured);

        // CSS: elements that are both .product and .featured
        int productFeatured = countByCss(document, "div.product.featured");
        System.out.println("Product‑featured divs: " + productFeatured);
    }
}
```

**Verwachte output** (ervan uitgaande dat er een typische `catalog.html` is):

```
Expensive books count: 4
Featured elements: 7
Product‑featured divs: 2
```

Als je bestand minder overeenkomende knooppunten bevat, passen de getallen zich dienovereenkomstig aan — geen verrassingen.

---

## Conclusie

We hebben **hoe je HTML kunt opvragen** met Aspose.HTML for Java behandeld, **hoe je CSS selecteert** gedemonstreerd, laten zien hoe je **elementen uit HTML haalt**, **meerdere CSS‑klassen selecteert**, en uitgelegd **hoe je knooppunten betrouwbaar telt**.  

De belangrijkste les? Het document één keer laden en vervolgens dezelfde `HTMLDocument`‑instantie hergebruiken stelt je in staat om XPath‑ en CSS‑queries te mixen zonder prestatie‑penalty’s.  

Klaar voor de volgende stap? Probeer selectors te ketenen om attribuutwaarden (`@href`, `@src`) op te halen of exporteer de resultaatsset naar JSON voor downstream verwerking. Je kunt ook paginering verkennen als je bron‑HTML zich over meerdere pagina’s uitstrekt.

Heb je een lastige selector of een randgeval dat je niet kunt oplossen? Laat een reactie achter, en laten we samen troubleshoot’en. Veel succes met query‑en!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}