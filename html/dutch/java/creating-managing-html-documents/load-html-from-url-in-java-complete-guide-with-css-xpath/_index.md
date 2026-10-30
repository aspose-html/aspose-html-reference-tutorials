---
category: general
date: 2026-07-02
description: Laad HTML van een URL met Aspose.HTML voor Java, selecteer vervolgens
  elementen met een attribuut, haal downloadlinks op en tel XPath‑knooppunten in een
  paar eenvoudige stappen.
draft: false
keywords:
- load html from url
- select elements with attribute
- extract download links
- search html with css
- count xpath nodes
language: nl
og_description: Laad HTML van een URL in Java, gebruik vervolgens CSS-selectors en
  XPath om elementen met een attribuut te selecteren, downloadlinks te extraheren
  en XPath‑knooppunten te tellen.
og_title: HTML laden vanaf URL in Java – Volledige CSS‑ en XPath‑handleiding
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Load HTML from URL using Aspose.HTML for Java, then select elements
    with attribute, extract download links, and count XPath nodes in a few easy steps.
  headline: Load HTML from URL in Java – Complete Guide with CSS & XPath
  type: TechArticle
- description: Load HTML from URL using Aspose.HTML for Java, then select elements
    with attribute, extract download links, and count XPath nodes in a few easy steps.
  name: Load HTML from URL in Java – Complete Guide with CSS & XPath
  steps:
  - name: Maven
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-html</artifactId>
      <version>23.10</version> <!-- Check for the latest version --> </dependency>
      ```'
  - name: Gradle
    text: '```gradle implementation ''com.aspose:aspose-html:23.10'' ```'
  - name: What the selector means
    text: '| Part | Meaning | |------|---------| | `a` | any `<a>` element | | `[href*=''download'']`
      | attribute `href` that **contains** the substring `download` (`*=` is the “contains”
      operator) |'
  - name: Expected console output (may vary by site)
    text: '``` Document loaded from https://example.com'
  type: HowTo
tags:
- Java
- Aspose.HTML
- Web Scraping
title: HTML laden vanaf URL in Java – Complete gids met CSS & XPath
url: /nl/java/creating-managing-html-documents/load-html-from-url-in-java-complete-guide-with-css-xpath/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML laden vanaf URL in Java – Complete gids met CSS & XPath

Heb je ooit **HTML moeten laden vanaf een URL** in een Java‑app en specifieke links moeten ophalen zonder een volledige web‑crawler te schrijven? Je bent niet de enige. Of je nu een download‑manager, een content‑aggregator bouwt, of gewoon nieuwsgierig bent naar de pagina’s die je bezoekt, het kunnen ophalen van een pagina, **HTML doorzoeken met CSS**, en vervolgens **XPath‑nodes tellen** is een handige vaardigheid.  

In deze tutorial lopen we het volledige proces door: van het ophalen van een externe pagina naar het geheugen, tot het gebruiken van een CSS‑selector om **elementen met attribuut te selecteren**, die **download‑links** te extraheren, en uiteindelijk het resultaat te verifiëren met een XPath‑query. Geen externe services, alleen pure Java en de Aspose.HTML for Java‑bibliotheek.

> **Voorvereisten** – Je hebt Java 8+ geïnstalleerd, Maven of Gradle voor afhankelijkheidsbeheer, en een basisbegrip van HTML en Java‑syntaxis nodig. Als je nieuw bent met Aspose.HTML, geen zorgen; we behandelen de installatie stap‑voor‑stap.

---

## Wat je gaat bouwen

Aan het einde van deze gids heb je een uitvoerbare Java‑klasse die:

1. **HTML laadt vanaf een URL** (bijv. `https://example.com`).
2. **Het DOM doorzoekt met een CSS‑selector** om elke `<a>`‑tag te vinden waarvan de `href` “download” bevat.
3. **Elke download‑link extraheert en afdrukt**.
4. **Een equivalente XPath‑query uitvoert** en afdrukt hoeveel nodes er zijn gevonden.

Je ziet ook een klein diagram dat de stroom visualiseert—voor het geval je een visuele leerder bent.

![Diagram dat de stroom van het laden van HTML vanaf URL, het selecteren van elementen, het extraheren van links en het tellen van XPath‑nodes weergeeft](load-html-from-url-diagram.png)

---

## Stap 1: Voeg Aspose.HTML voor Java toe aan je project

Allereerst. Aspose.HTML is een commerciële bibliotheek, maar biedt een gratis proefversie die perfect werkt voor leerdoeleinden.

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

### Gradle

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

> **Pro tip:** Als je later een `NoClassDefFoundError` krijgt, controleer dan of de `aspose-html`‑jar op je runtime‑classpath staat.

---

## Stap 2: HTML laden vanaf URL en het document initialiseren

Nu de bibliotheek beschikbaar is, kunnen we daadwerkelijk **HTML laden vanaf een URL**. De `HTMLDocument`‑klasse accepteert een string‑URL en regelt het HTTP‑verzoek, redirects en karakter‑setdetectie voor je.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;

public class HtmlDownloader {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Define the target page
        String pageUrl = "https://example.com";

        // Step 2.2: Load the page into an HTMLDocument object
        HTMLDocument document = new HTMLDocument(pageUrl);

        System.out.println("Document loaded successfully.");
        // From here on we can query the DOM.
    }
}
```

**Waarom dit werkt:** `HTMLDocument` maakt intern een `HttpWebRequest` aan, volgt redirects en bouwt een DOM‑boom die zich gedraagt als het `document` van een browser. Dat betekent dat we meteen zowel CSS‑selectors als XPath kunnen gebruiken.

---

## Stap 3: HTML doorzoeken met CSS – Elementen met attribuut selecteren

De meest leesbare manier om elementen te vinden is met een CSS‑selector. In ons geval willen we elke `<a>` waarvan het `href`‑attribuut het woord “download” bevat. De selector‑syntaxis `a[href*='download']` doet precies dat.

```java
// Step 3: Find all anchor elements whose href contains "download"
NodeList downloadLinks = document.selectElements("a[href*='download']");

// Quick sanity check – how many did we find?
System.out.println("CSS found " + downloadLinks.getLength() + " nodes.");
```

### Wat de selector betekent

| Deel | Betekenis |
|------|-----------|
| `a` | elk `<a>`‑element |
| `[href*='download']` | attribuut `href` dat **de substring** `download` bevat (`*=` is de “contains”‑operator) |

> **Randgeval:** Als de pagina relatieve URL’s gebruikt (bijv. `href="/files/download.zip"`), zal Aspose.HTML ze ongewijzigd behouden. Je moet ze later mogelijk resolven ten opzichte van de basis‑URL.

---

## Stap 4: Download‑links extraheren

Nu we een `NodeList` hebben, is het trekken van de daadwerkelijke URL’s triviaal. We casten elk node naar een `Element` en lezen het `href`‑attribuut.

```java
System.out.println("\n--- Extracted Download Links ---");
for (int i = 0; i < downloadLinks.getLength(); i++) {
    Element anchor = (Element) downloadLinks.item(i);
    String href = anchor.getAttribute("href");
    // Resolve relative URLs to absolute ones (optional but handy)
    String absoluteHref = document.getBaseUrl().resolve(href).toString();
    System.out.println(absoluteHref);
}
```

**Resultaat dat je ziet** (voorbeeldoutput):

```
CSS found 3 nodes.

--- Extracted Download Links ---
https://example.com/files/report-download.pdf
https://example.com/downloads/setup.exe
https://cdn.example.com/assets/manual-download.docx
```

Als je alleen de ruwe attribuutwaarde nodig hebt, sla dan de `resolve`‑aanroep over. De resolvestap is handig wanneer je die URL’s later in een downloader stopt.

---

## Stap 5: HTML doorzoeken met XPath – XPath‑nodes tellen

Soms geef je de voorkeur aan XPath—vooral wanneer je complexere hiërarchische queries nodig hebt. De equivalente XPath‑expressie voor onze CSS‑selector is:

```xpath
//a[contains(@href,'download')]
```

Laten we deze uitvoeren en kijken hoeveel nodes we krijgen.

```java
// Step 5: Perform the same search using XPath
NodeList xpathNodes = document.selectNodes("//a[contains(@href,'download')]");

// Output the count
System.out.println("\nXPath found " + xpathNodes.getLength() + " nodes.");
```

De output moet overeenkomen met het CSS‑aantal, wat bevestigt dat beide benaderingen equivalent zijn:

```
XPath found 3 nodes.
```

> **Waarom beide?** Het gebruik van beide selectors in dezelfde codebase geeft je flexibiliteit. CSS is beknopt voor eenvoudige attribuutcontroles, terwijl XPath uitblinkt wanneer je omhoog/omlaag door de boom moet navigeren of meerdere voorwaarden moet combineren.

---

## Stap 6: Volledig werkend voorbeeld

Alles samengevoegd, hier is de complete klasse die je kunt kopiëren‑plakken in je IDE en direct kunt uitvoeren.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;

public class QueryExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the HTML document from a web page
        String url = "https://example.com";
        HTMLDocument document = new HTMLDocument(url);
        System.out.println("Document loaded from " + url);

        // 2️⃣ Search HTML with CSS – select elements with attribute
        NodeList cssMatches = document.selectElements("a[href*='download']");
        System.out.println("\nCSS found " + cssMatches.getLength() + " nodes.");

        // 3️⃣ Extract download links
        System.out.println("\n--- Extracted Download Links ---");
        for (int i = 0; i < cssMatches.getLength(); i++) {
            Element anchor = (Element) cssMatches.item(i);
            String href = anchor.getAttribute("href");
            // Resolve relative URLs (optional)
            String absolute = document.getBaseUrl().resolve(href).toString();
            System.out.println(absolute);
        }

        // 4️⃣ Search HTML with XPath – count xpath nodes
        NodeList xpathMatches = document.selectNodes("//a[contains(@href,'download')]");
        System.out.println("\nXPath found " + xpathMatches.getLength() + " nodes.");
    }
}
```

### Verwachte console‑output (kan per site verschillen)

```
Document loaded from https://example.com

CSS found 3 nodes.

--- Extracted Download Links ---
https://example.com/files/report-download.pdf
https://example.com/downloads/setup.exe
https://cdn.example.com/assets/manual-download.docx

XPath found 3 nodes.
```

Voer het programma uit, en je ziet meteen alle links die “download” bevatten. Pas de selector of XPath‑string aan naar je eigen criteria—bijvoorbeeld `a[href$='.pdf']` voor alleen PDF’s, of `//div[@class='product']//a` voor productpagina’s.

---

## Veelvoorkomende valkuilen & hoe ze te vermijden

| Probleem | Symptoom | Oplossing |
|----------|----------|-----------|
| **HTTPS‑certificaatfouten** | `javax.net.ssl.SSLHandshakeException` | Voeg een trust‑manager toe of gebruik een URL met een geldig certificaat. Voor snelle tests kun je certificaatvalidatie uitschakelen, maar nooit in productie. |
| **Redirect‑lussen** | Programma loopt vast of geeft `Too many redirects` | Stel een redelijke redirect‑limiet in (`document.setRedirectLimit(5)`) of inspecteer de doel‑URL handmatig. |
| **Relatieve URL’s** | Geëxtraheerde links beginnen met `/` in plaats van een volledige domeinnaam | Gebruik `document.getBaseUrl().resolve(relative)` zoals in het voorbeeld. |
| **Grote pagina’s** | Hoog geheugenverbruik | Stream de respons of gebruik `HTMLDocument`‑overloads die de DOM‑grootte beperken. |
| **Ontbrekende Aspose‑licentie** | Runtime gooit `LicenseException` nadat de proefperiode verloopt | Koop een licentie of blijf de proefversie gebruiken voor niet‑commerciële experimenten. |

---

## Volgende stappen & gerelateerde onderwerpen

- **Download de bestanden** – combineer de geëxtraheerde URL’s met Java’s `HttpURLConnection` of Apache HttpClient om de resources daadwerkelijk op te halen.  
- **Parallel verwerken** – gebruik `CompletableFuture` om meerdere bestanden gelijktijdig te downloaden.  
- **Geavanceerde CSS‑selectors** – probeer `a[href$='.zip']` voor bestands‑extensies, of `div[data-id]` om elementen met aangepaste attributen te selecteren.  
- **XPath‑functies** – verken `starts-with()`, `ends-with()` en logische operatoren (`and`, `or`) voor meer gedetailleerde queries.  
- **HTML‑sanitizing** – als je de opgehaalde HTML wilt weergeven, overweeg dan een bibliotheek zoals Jsoup om deze schoon te maken.

---

## Conclusie

We hebben zojuist laten zien hoe je **HTML kunt laden vanaf een URL** in Java, vervolgens **HTML doorzoekt met CSS** om **elementen met attribuut te selecteren**, **download‑links extraheert**, en ten slotte **XPath‑nodes telt** om het resultaat te verifiëren. De aanpak is compact, maakt gebruik van één enkele bibliotheek, en werkt zowel voor eenvoudige scraping‑taken als voor meer geavanceerde DOM‑analyse.  

Voel je vrij om de selectors aan te passen


## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Load HTML Documents from Stream with Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-stream/)
- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Handle Document Load Events in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/handle-document-load-events/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}