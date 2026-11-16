---
category: general
date: 2026-04-23
description: Leer hoe je HTML‑elementen kunt extraheren in Java, meerdere CSS‑klassen
  kunt selecteren, XPath kunt gebruiken en elementen kunt tellen met praktische codevoorbeelden.
draft: false
keywords:
- extract html elements
- select multiple css classes
- java html scraping
- count elements java
- xpath query java
og_description: Beheers hoe je HTML‑elementen kunt extraheren in Java, leer hoe je
  meerdere CSS‑klassen selecteert, XPath‑query's uitvoert en knooppunten telt met
  echte codevoorbeelden.
og_title: HTML-elementen extraheren in Java – Complete tutorial
tags:
- Java
- HTML parsing
- Aspose.HTML
title: HTML-elementen extraheren in Java – Complete handleiding
url: /nl/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML-elementen extraheren in Java – Volledige tutorial

Heb je je ooit afgevraagd **hoe je html-elementen kunt extraheren** uit een Java‑programma zonder je haar uit te trekken? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze gegevens uit een statische catalogus moeten halen of een eenvoudige pagina moeten scrapen, en de gebruikelijke DOM‑trucs aanvoelen onhandig.  

Het goede nieuws? Met een paar regels code kun je een HTML‑bestand laden, XPath‑ of CSS‑selectoren uitvoeren, en zelfs de knooppunten tellen die je nodig hebt – alles in één nette stroom. In deze gids lopen we **hoe je html-elementen kunt extraheren**, **hoe je CSS selecteert**, en laten we je zien hoe je **elementen uit HTML kunt extraheren**, **meerdere CSS‑klassen selecteert**, en **hoe je knooppunten telt** met Aspose.HTML for Java.

## Snelle antwoorden
- **Welke bibliotheek verwerkt HTML‑parsing in Java?** Aspose.HTML for Java  
- **Kan ik CSS‑selectoren met meerdere klassen gebruiken?** Ja, met selectoren zoals `.class1, .class2` of `div.class1.class2`  
- **Hoe tel ik knooppunten?** Roep `.size()` aan op de lijst die wordt geretourneerd door `selectCss` of `selectXPath`  
- **Wordt XPath ondersteund?** Absoluut – perfect voor numerieke vergelijkingen en relationele queries  
- **Heb ik een licentie nodig voor productie?** Een commerciële licentie is vereist voor productiegebruik; een gratis proefversie is beschikbaar voor testen  

## Wat betekent “html-elementen extraheren”?
HTML‑elementen extraheren betekent een HTML‑document laden in een DOM (Document Object Model) en vervolgens die DOM doorzoeken om specifieke knooppunten op te halen – of het nu gaat om tag‑naam, attribuut, CSS‑klasse of XPath‑expressie. Deze techniek voedt alles van eenvoudige data‑scraping‑scripts tot complexe content‑migratie‑pijplijnen.

## Waarom Aspose.HTML voor Java gebruiken?
Aspose.HTML biedt een **enkele, goed gedocumenteerde API** die zowel CSS‑selectoren als XPath ondersteunt, werkt met slecht gevormde markup, en draait consistent op Java 8+. Het elimineert de noodzaak voor derden‑parsers en levert ingebouwde helpers voor tellen, itereren en attribuutwaarden extraheren.

## Vereisten
- Java 8 of nieuwer  
- Maven‑ of Gradle‑buildsysteem  
- Aspose.HTML for Java‑bibliotheek (proefversie of gelicentieerde versie)  

## Wat je zult leren

- Een HTML‑document laden vanaf schijf of een URL.  
- XPath gebruiken om elementen te vinden die aan complexe voorwaarden voldoen.  
- CSS‑selectoren toepassen, inclusief **meerdere css‑klassen selecteren**.  
- **Elementen java tellen** programmatically.  
- Tips, valkuilen en variaties voor real‑world scenario’s.

![how to query html example](https://example.com/images/query-html.png "Screenshot showing how to query html with Java")

## Hoe HTML te queryen – Het document laden

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
Als je HTML van een externe site haalt, geef je simpelweg de URL‑string door aan `HTMLDocument` – Aspose haalt het op en parseert het voor je.

## Hoe CSS te selecteren – CSS‑selectoren gebruiken

Zodra de DOM klaar is, is het selecteren van knooppunten met CSS net zo simpel als één regel code. Laten we elk element pakken dat de `featured`‑ of `highlight`‑klasse heeft.

```java
        // Step 2: Locate elements marked as featured or highlighted using a CSS selector
        List<Element> featuredElements = document.selectCss(".featured, .highlight");

        // Step 3: Output the number of elements found by the CSS selector
        System.out.println("Featured elements: " + featuredElements.size());
```

> **Uitleg** – De selector `.featured, .highlight` vertelt de engine om *elk* element te retourneren waarvan het `class`‑attribuut `featured` **of** `highlight` bevat. Dit is de canonieke manier om **meerdere css‑klassen te selecteren** in één query.

### Randgeval
Als een element beide klassen bevat (bijv. `<div class="featured highlight">`), verschijnt het **eenmaal** in de resultaatslijst, waardoor dubbel tellen wordt voorkomen.

## HTML-elementen extraheren – XPath en CSS combineren

XPath blinkt uit wanneer je relationele logica nodig hebt, zoals “alle `<book>`‑knooppunten waar de prijs hoger is dan 30”. Hier is het exacte fragment uit het oorspronkelijke voorbeeld:

```java
        // Step 4: Find all <book> elements with a price greater than 30 using XPath
        List<Element> expensiveBooks = document.selectXPath("//book[price>30]");

        // Step 5: Output the number of books that match the XPath query
        System.out.println("Expensive books count: " + expensiveBooks.size());
```

> **Waarom XPath?** – XPath kan numerieke vergelijkingen (`price>30`) direct evalueren, iets wat CSS niet kan. Het laat je ook ouder‑/kind‑relaties doorlopen zonder extra code.

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

> **Belangrijk punt** – Geen spatie tussen de klassennamen; een spatie zou “afstammeling” betekenen. Dit patroon is essentieel wanneer je **meerdere css‑klassen selecteert** die samenwerken om een component te stylen.

## Hoe knooppunten tellen – Nauwkeurige totalen verkrijgen

Knooppunten tellen is vaak de laatste stap in een data‑extractie‑pijplijn. Je hebt al `list.size()` gezien na elke query, maar laten we het in een herbruikbare helper verpakken.

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

> **Waarom verpakken?** – Het centraliseren van de tel‑logica maakt je code makkelijker te testen en vermindert duplicatie. Het verduidelijkt ook **hoe knooppunten te tellen** voor toekomstige lezers.

### Veelvoorkomende valkuilen
- **Witruimte in class‑attributen** – `"featured "` (spatie aan het einde) matcht nog steeds `.featured` omdat de selector witruimte trimt.  
- **Hoofdlettergevoeligheid** – HTML‑klassennamen zijn hoofdlettergevoelig in XML‑modus; zorg dat je bron‑HTML consistente hoofdlettergebruik hanteert.

## Volledig werkend voorbeeld

Alles bij elkaar, hier is een zelf‑containend programma dat je kunt kopiëren‑plakken in je IDE:

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

Als je bestand minder overeenkomende knooppunten bevat, passen de cijfers zich dienovereenkomstig aan – geen verrassingen.

## Veelvoorkomende problemen en oplossingen

- **Bestand niet gevonden** – Controleer of het pad absoluut is of relatief ten opzichte van de werkdirectory.  
- **Slecht gevormde HTML** – Aspose.HTML tolereert de meeste fouten, maar extreem gebroken markup kan voorafgaande reiniging vereisen.  
- **Prestaties bij grote bestanden** – Laad het document één keer, hergebruik dezelfde `HTMLDocument`‑instantie voor alle queries.  

## Veelgestelde vragen

**Q: Kan ik deze aanpak gebruiken voor web‑scraping over meerdere pagina’s?**  
A: Ja. Laad elke pagina met een nieuwe `HTMLDocument`‑instantie of hergebruik dezelfde instantie na het aanroepen van `document.load(url)`.

**Q: Ondersteunt Aspose.HTML HTML5‑elementen?**  
A: Absoluut. De parser is HTML5‑bewust en verwerkt moderne tags zoals `<section>`, `<article>` en `<video>`.

**Q: Hoe haal ik attribuutwaarden zoals `href` uit links?**  
A: Nadat je het element hebt geselecteerd, roep je `element.getAttribute("href")` aan op elk `Element` in de resultaatslijst.

**Q: Is er een manier om de geselecteerde knooppunten naar JSON te exporteren?**  
A: Je kunt over de lijst itereren, een JSON‑object bouwen met de gewenste eigenschappen, en elke JSON‑bibliotheek (bijv. Jackson) gebruiken om het te serialiseren.

**Q: Welke Java‑versies worden ondersteund?**  
A: De bibliotheek werkt met Java 8 en nieuwer, inclusief Java 11, 17 en latere LTS‑releases.

## Conclusie

We hebben **hoe je html-elementen kunt extraheren** met Aspose.HTML for Java behandeld, **hoe je CSS selecteert**, laten zien hoe je **elementen uit HTML kunt extraheren**, **meerdere CSS‑klassen selecteert**, en uitgelegd **hoe knooppunten te tellen** op een betrouwbare manier.  

De belangrijkste les? Het document één keer laden en vervolgens dezelfde `HTMLDocument`‑instantie hergebruiken stelt je in staat om XPath‑ en CSS‑queries te mixen zonder prestatie‑penalty’s.  

Klaar voor de volgende stap? Probeer selectors te chainen om attribuutwaarden (`@href`, `@src`) op te halen of exporteer de resultaatsset naar JSON voor downstream verwerking. Je kunt ook paginering verkennen als je bron‑HTML zich over meerdere pagina’s uitstrekt.

Heb je een lastige selector of een randgeval dat je niet kunt kraken? Laat een reactie achter hieronder, en laten we samen troubleshootten. Veel plezier met queryen!

---

**Last Updated:** 2026-04-23  
**Tested With:** Aspose.HTML for Java 24.11  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}