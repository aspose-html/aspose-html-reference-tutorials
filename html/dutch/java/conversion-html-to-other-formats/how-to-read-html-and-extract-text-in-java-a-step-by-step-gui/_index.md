---
category: general
date: 2026-10-28
description: Hoe HTML in Java te lezen en tekst uit HTML‑bestanden te extraheren.
  Leer HTML naar tekst te converteren met Jsoup, met uitleg over het lezen van HTML
  uit een bestand en HTML‑naar‑tekst‑technieken in Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to read html
- extract text from html
- convert html to text
- html to text java
- read html from file
language: nl
lastmod: 2026-10-28
og_description: Hoe HTML te lezen in Java en tekst uit HTML‑bestanden te extraheren.
  Deze tutorial toont een volledige oplossing om HTML naar tekst te converteren met
  behulp van Jsoup.
og_image_alt: Diagram showing how to read HTML and extract text in Java
og_title: Hoe HTML te lezen en tekst te extraheren in Java – snelle gids
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  headline: How to read HTML and extract text in Java – a step‑by‑step guide
  type: TechArticle
- description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  name: How to read HTML and extract text in Java – a step‑by‑step guide
  steps:
  - name: Maven
    text: '```xml <dependency> <groupId>org.jsoup</groupId> <artifactId>jsoup</artifactId>
      <version>1.17.2</version> </dependency> ```'
  - name: Gradle
    text: '```gradle implementation ''org.jsoup:jsoup:1.17.2'' ```'
  - name: Expected output
    text: 'Assuming `input.html` contains:'
  - name: Running the program
    text: '```bash javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java java -cp .:jsoup-1.17.2.jar
      HtmlToTextDemo ```'
  type: HowTo
tags:
- Java
- HTML parsing
- Text extraction
title: Hoe HTML te lezen en tekst te extraheren in Java – een stap‑voor‑stap gids
url: /nl/java/conversion-html-to-other-formats/how-to-read-html-and-extract-text-in-java-a-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe HTML te lezen en tekst te extraheren in Java – een stapsgewijze handleiding

Als je **how to read html** van een lokaal bestand moet lezen, biedt deze gids een volledige oplossing. Je leert een HTML‑document te laden, de platte tekst te extraheren, en optioneel HTML naar tekst te converteren met fijnmazige controle. Aan het einde van de tutorial kun je de voorbeeldcode uitvoeren en de geëxtraheerde tekst op de console zien afgedrukt.

HTML‑bestanden lezen is een veelvoorkomende taak bij het verwerken van web‑gescrapte data, het genereren van rapporten of het opschonen van door gebruikers gegenereerde inhoud. De onderstaande stappen behandelen alles wat je nodig hebt, van het toevoegen van de vereiste bibliotheek tot het afhandelen van randgevallen zoals slecht gevormde markup of problemen met tekencodering.

## Wat je nodig hebt

- Java 17 of nieuwer (de code compileert ook met eerdere versies)
- Maven of Gradle voor afhankelijkheidsbeheer, of de Jsoup‑JAR handmatig toegevoegd
- Een HTML‑bestand genaamd `input.html` geplaatst in de `src/main/resources` map van het project (je kunt het pad later wijzigen)

## Stel de Jsoup‑bibliotheek in

Jsoup is een lichtgewicht, goed gedocumenteerde bibliotheek die HTML parseert naar een DOM‑achtige structuur. Het verwerkt gebroken HTML op een nette manier, waardoor het ideaal is voor **extract text from html** taken.

### Maven

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

### Gradle

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

Als je de voorkeur geeft aan een handmatige download, plaats de JAR op je classpath en importeer `org.jsoup.*` in je bronbestand.

## Laad HTML vanuit een bestand

De eerste programmeer‑stap is het lezen van het bestand in een `Document`‑object. Jsoup biedt een statische `parse`‑methode die een `File` en een tekenset‑naam accepteert.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Path to the HTML file – adjust if your file lives elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Parse the file using UTF‑8 encoding
            Document doc = Jsoup.parse(input, "UTF-8");
            // Continue with text extraction…
        } catch (IOException e) {
            System.err.println("Failed to read the HTML file: " + e.getMessage());
        }
    }
}
```

**Waarom dit belangrijk is:** `Jsoup.parse(File, String)` leest de ruwe bytes, decodeert ze volgens de opgegeven tekenset en bouwt een schone DOM. Deze aanpak is veiliger dan het zelf inlezen van het bestand naar een string, omdat Jsoup regeleinden normaliseert en veelvoorkomende markup‑fouten automatisch corrigeert.

## Extraheer platte tekst uit de HTML

Zodra je een `Document` hebt, is het ophalen van de zichtbare tekst één enkele methode‑aanroep. De `text()`‑methode concateneert de tekstuele inhoud van alle elementen terwijl tags, scripts en stijlen worden weggelaten.

```java
// Inside the try block from the previous snippet
String plainText = doc.body().text();
System.out.println("Extracted text:");
System.out.println(plainText);
```

De `body()`‑aanroep beperkt de extractie tot het `<body>`‑element, wat de typische doel is wanneer je **read html from file** voor content‑analyse. De resulterende string bevat witruimte samengevoegd tot enkele spaties, wat nabootst hoe een browser de tekst zou weergeven.

### Verwachte output

Stel dat `input.html` bevat:

```html
<!DOCTYPE html>
<html>
<head><title>Sample</title></head>
<body>
  <h1>Hello World</h1>
  <p>This is a <strong>demo</strong> page.</p>
</body>
</html>
```

Het uitvoeren van het programma print:

```
Extracted text:
Hello World This is a demo page.
```

## Converteer HTML naar tekst met extra opties

Soms heb je meer controle nodig dan `text()` biedt — bijvoorbeeld het behouden van regeleinden, het behouden van lijstnummers, of het negeren van bepaalde tags. Jsoup’s `NodeTraversor` gecombineerd met een aangepaste `NodeVisitor` geeft je die flexibiliteit.

```java
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

public class HtmlToTextDemo {

    // ... (main method unchanged)

    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();
        NodeVisitor visitor = new NodeVisitor() {
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Preserve line breaks for block elements
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }
            public void tail(Node node, int depth) {
                // No action needed on exit
            }
        };
        NodeTraversor.traverse(visitor, doc.body());
        // Collapse multiple newlines into a single one
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

Vervang de eenvoudige `doc.body().text()`‑aanroep door:

```java
String detailedText = convertHtmlToText(doc);
System.out.println("Detailed conversion:");
System.out.println(detailedText);
```

**Waarom dit werkt:** De bezoeker doorloopt de DOM diepte‑eerst en voegt een regeleinde toe vóór elk blok‑niveau element (bijv. `<p>`, `<div>`, `<h1>`). Dit behoudt de scheiding tussen alinea’s, wat nuttig is wanneer je **convert html to text** voor leesbaarheid of downstream NLP‑pijplijnen.

## Veelvoorkomende valkuilen en best practices

| Probleem | Waarom het gebeurt | Aanbevolen oplossing |
|----------|--------------------|----------------------|
| Verkeerde tekenset | Bestanden opgeslagen in ISO‑8859‑1 maar geparseerd als UTF‑8 leveren onleesbare tekens op. | Detecteer de tekenset uit de meta‑tag van het bestand (`<meta charset="...">`) of geef de juiste naam door aan `Jsoup.parse`. |
| Grote bestanden | Het laden van een zeer groot HTML‑bestand in het geheugen kan een `OutOfMemoryError` veroorzaken. | Stream het bestand met `Jsoup.parse(File, String, String baseUri)` en verwerk knooppunten incrementeel, of vergroot de JVM‑heapgrootte. |
| Ongewenste script/style‑tekst | `text()` verwijdert script‑ en style‑inhoud, maar aangepaste bezoekers kunnen deze per ongeluk includeren. | Sla knooppunten over waarvan de tagnaam `script` of `style` is binnen de `head`‑methode van de bezoeker. |
| Witruimte behouden | Spaties samenvouwen kan opmaak verliezen die nodig is voor markdown‑conversie. | Gebruik `Element.wholeText()` voor ruwe tekstknooppunten, en verwerk witruimte daarna handmatig. |

Het aanpakken van deze aandachtspunten zorgt ervoor dat jouw **html to text java**‑oplossing betrouwbaar werkt voor diverse invoer.

## Volledig uitvoerbaar voorbeeld

Hieronder staat een zelfstandige applicatie die de volledige workflow demonstreert — van het instellen van de afhankelijkheden tot het verifiëren van de output. Kopieer de code naar een bestand genaamd `HtmlToTextDemo.java`, plaats een `input.html`‑bestand ernaast, en voer `javac && java` uit zoals getoond.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Adjust the path if your HTML file is located elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Load and parse the HTML file using UTF‑8
            Document doc = Jsoup.parse(input, "UTF-8");

            // Simple extraction – suitable for most cases
            String plain = doc.body().text();
            System.out.println("=== Simple extraction ===");
            System.out.println(plain);
            System.out.println();

            // Detailed conversion – keeps line breaks for readability
            String detailed = convertHtmlToText(doc);
            System.out.println("=== Detailed conversion ===");
            System.out.println(detailed);
        } catch (IOException e) {
            System.err.println("Error reading HTML file: " + e.getMessage());
        }
    }

    /**
     * Walks the DOM and builds a text representation that preserves
     * line breaks for block‑level elements.
     *
     * @param doc the parsed HTML document
     * @return a readable plain‑text version of the HTML body
     */
    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();

        NodeVisitor visitor = new NodeVisitor() {
            @Override
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Add a newline before block elements (e.g., <p>, <div>, <h1>)
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }

            @Override
            public void tail(Node node, int depth) {
                // No operation needed when exiting a node
            }
        };

        NodeTraversor.traverse(visitor, doc.body());

        // Collapse consecutive newlines and trim leading/trailing whitespace
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

### Het programma uitvoeren

```bash
javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java
java -cp .:jsoup-1.17.2.jar HtmlToTextDemo
```

De console toont zowel de eenvoudige extractie als de gedetailleerde

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe XPath te gebruiken in Java – HTML lezen en tekst extraheren](/html/english/java/creating-managing-html-documents/how-to-use-xpath-in-java-read-html-and-extract-text/)
- [Hoe HTML te parsen in Java – Tekst extraheren uit HTML‑artikelen](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Tekst extraheren uit HTML met Java – Complete stapsgewijze gids](/html/english/java/creating-managing-html-documents/extract-text-from-html-with-java-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}