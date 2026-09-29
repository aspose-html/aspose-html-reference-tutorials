---
category: general
date: 2026-09-29
description: Lernen Sie, wie man Elemente nach Klasse auswählt, HTML aus einer Datei
  liest und externe Links in Java findet. Diese Schritt‑für‑Schritt‑Anleitung behandelt
  das effiziente Durchlaufen einer NodeList.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- select elements by class
- read html from file
- find external links
- iterate nodelist java
- use queryselectorall java
language: de
lastmod: 2026-09-29
og_description: Wählen Sie Elemente nach Klasse in Java aus, lesen Sie HTML aus einer
  Datei und finden Sie externe Links mit querySelectorAll. Folgen Sie dem vollständigen
  Beispiel, um eine NodeList zu iterieren.
og_image_alt: Screenshot showing Java code that selects elements by class from an
  HTML file
og_title: Elemente nach Klasse in Java auswählen – vollständiger Leitfaden mit querySelectorAll
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
title: Wie man in Java Elemente per Klasse mit querySelectorAll auswählt
url: /de/java/creating-managing-html-documents/how-to-select-elements-by-class-in-java-using-queryselectora/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Elemente nach Klasse in Java mit querySelectorAll auswählt

Wenn Sie **Elemente nach Klasse** beim Verarbeiten einer HTML‑Datei in Java auswählen müssen, zeigt Ihnen diese Anleitung genau, wie das geht. Sie lernen, HTML aus einer Datei zu lesen, `querySelectorAll` zu verwenden, um externe Links zu finden, und die resultierende `NodeList` sicher zu iterieren.

Die Arbeit mit HTML in Java wirkt oft schwerfällig, aber moderne Bibliotheken bieten Ihnen eine kompakte, CSS‑Selektor‑basierte API. Das nachfolgende Beispiel verwendet **jsoup** (Version 1.17.2), weil es `querySelectorAll`‑artige Selektoren implementiert und eine `Elements`‑Sammlung zurückgibt, die sich wie eine `NodeList` verhält. Sie können dieselbe Logik bei Bedarf an andere DOM‑Implementierungen anpassen.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie folgendes haben:

* JDK 17 oder neuer installiert.
* Maven oder Gradle für das Abhängigkeitsmanagement.
* Grundlegende Kenntnisse von Java‑Streams und dem DOM‑Modell.

Fügen Sie jsoup zu Ihrem Projekt hinzu:

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

## Schritt 1: HTML aus Datei lesen

Die erste Aufgabe besteht darin, das HTML‑Dokument von der Festplatte zu laden. `Jsoup.parse(Path, Charset)` liest die Datei und erstellt einen DOM‑Baum, den Sie abfragen können.

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

*Warum das wichtig ist*: Das Laden der Datei einmal vermeidet wiederholte I/O‑Operationen, während Sie später über die Elemente iterieren. Das `Document`‑Objekt enthält das komplette DOM und ermöglicht schnelle Selektor‑Abfragen.

## Schritt 2: `querySelectorAll` verwenden, um Elemente nach Klasse auszuwählen

Jetzt, wo das Dokument im Speicher ist, können Sie **Elemente nach Klasse** mit einem CSS‑Selektor auswählen. Der Selektor `"a.external"` trifft auf `<a>`‑Tags zu, die die Klasse `external` besitzen – genau das, was Sie benötigen, um **externe Links zu finden**.

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

*Warum das wichtig ist*: Die Verwendung eines Klassenselektors ist sowohl ausdrucksstark als auch performant. Die Bibliothek übersetzt den Selektor in eine optimierte Traversierung, sodass Sie keine manuellen Schleifen über jeden Knoten schreiben müssen.

## Schritt 3: Die NodeList (Elements) in Java iterieren

`Elements` implementiert `Iterable<Element>`, was bedeutet, dass Sie eine Standard‑`for‑each`‑Schleife verwenden können, um **NodeList‑Java**‑Objekte zu **iterieren**. Die Schleife unten gibt das `href`‑Attribut jedes Links aus.

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

*Warum das wichtig ist*: Direkte Iteration hält den Code lesbar und vermeidet den Overhead, die Sammlung in einen Stream zu konvertieren, wenn Sie nur eine einfache Ausgabe benötigen.

## Vollständiges funktionierendes Beispiel

Wenn Sie die drei Schritte zusammenführen, erhalten Sie ein eigenständiges Programm, das Sie über die Befehlszeile ausführen können.

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

### Erwartete Ausgabe

Angenommen, `input.html` enthält:

```html
<a class="external" href="https://example.com">Example</a>
<a class="internal" href="/about">About</a>
<a class="external" href="https://openai.com">OpenAI</a>
```

Das Ausführen des Programms gibt aus:

```
External link: https://example.com
External link: https://openai.com
```

## Profi‑Tipps und häufige Fallstricke

* **Encoding matters** – Lesen Sie die Datei immer mit UTF‑8 (oder dem Zeichensatz, der Ihrer Quelle entspricht). Eine falsche Kodierung kann Zeichen in Attributwerten beschädigen.
* **Multiple classes** – Wenn ein Element mehrere Klassen hat (z. B. `class="btn external"`), trifft der Selektor `"a.external"` weiterhin zu, weil CSS‑Klassenselektoren das Vorhandensein des Tokens prüfen, nicht den exakten String.
* **Performance tip** – Wenn Sie nur das `href`‑Attribut benötigen, können Sie es direkt mit `doc.select("a.external[href]").eachAttr("href")` anfordern. Das vermeidet das Erzeugen vollständiger `Element`‑Objekte für jede Übereinstimmung.
* **Null safety** – `link.attr("href")` gibt einen leeren String zurück, wenn das Attribut fehlt, sodass Sie vor dem Ausgeben keine Null‑Prüfung benötigen.

## Häufig gestellte Fragen

**Q: Funktioniert das mit HTML‑Fragmenten, denen ein `<html>`‑Root fehlt?**  
A: Ja. `Jsoup.parse` behandelt die Eingabe als Fragment und fügt fehlende Root‑Elemente automatisch hinzu, sodass Selektoren im Body des Fragments funktionieren.

**Q: Kann ich `querySelectorAll` ohne jsoup verwenden?**  
A: Die standardmäßige Java‑DOM‑API (`org.w3c.dom`) enthält kein `querySelectorAll`. Bibliotheken wie **HTMLUnit** oder **jodd-lagarto** bieten ähnliche Methoden. Das hier gezeigte Muster – laden, mit CSS auswählen, iterieren – bleibt gleich.

**Q: Was ist, wenn ich die Links ändern muss, anstatt sie nur auszugeben?**  
A: Nachdem Sie jedes `Element` erhalten haben, können Sie `link.attr("href", "newUrl")` aufrufen und das Dokument anschließend mit `Files.writeString` zurück auf die Festplatte schreiben.

## Fazit

Sie wissen jetzt, wie man **Elemente nach Klasse** auswählt, **HTML aus einer Datei liest**, **externe Links findet** und **eine NodeList in Java** mit `querySelectorAll`‑artigen Selektoren iteriert. Das vollständige Beispiel zeigt einen sauberen, produktionsbereiten Workflow, den Sie in größere Scraping‑ oder Transformations‑Pipelines einbinden können.

Als Nächstes können Sie verwandte Themen erkunden, wie **dynamischen Content mit HTMLUnit parsen**, **modifiziertes HTML zurück auf die Festplatte schreiben** oder **Java‑Streams verwenden, um Link‑URLs in einer Liste zu sammeln**. Jeder dieser Punkte baut auf der hier gezeigten Kerntechnik der klassenbasierten Auswahl auf. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man HTML in Java abfragt – Elemente auswählen, nach Attribut filtern und Text erhalten](/html/english/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/)
- [NodeList in Java iterieren – HTML lesen & Bild‑src erhalten](/html/english/java/creating-managing-html-documents/iterate-nodelist-java-read-html-get-image-src/)
- [HTML‑Dokumente aus Datei in Aspose.HTML für Java laden](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}