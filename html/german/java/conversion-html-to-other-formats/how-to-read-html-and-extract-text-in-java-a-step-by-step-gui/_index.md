---
category: general
date: 2026-10-28
description: Wie man HTML in Java liest und Text aus HTML‑Dateien extrahiert. Lernen
  Sie, HTML mit Jsoup in Text zu konvertieren, einschließlich des Lesens von HTML
  aus Dateien und Java‑Techniken zur Umwandlung von HTML in Text.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to read html
- extract text from html
- convert html to text
- html to text java
- read html from file
language: de
lastmod: 2026-10-28
og_description: Wie man HTML in Java liest und Text aus HTML‑Dateien extrahiert. Dieses
  Tutorial zeigt eine vollständige Lösung zum Konvertieren von HTML zu Text mit Jsoup.
og_image_alt: Diagram showing how to read HTML and extract text in Java
og_title: Wie man HTML liest und Text in Java extrahiert – Schnellleitfaden
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
title: Wie man HTML liest und Text in Java extrahiert – eine Schritt‑für‑Schritt‑Anleitung
url: /de/java/conversion-html-to-other-formats/how-to-read-html-and-extract-text-in-java-a-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man HTML in Java liest und Text extrahiert – eine Schritt‑für‑Schritt‑Anleitung

Wenn Sie **how to read html** von einer lokalen Datei benötigen, bietet dieser Leitfaden eine vollständige Lösung. Sie lernen, ein HTML‑Dokument zu laden, den Klartext zu extrahieren und optional HTML in Text mit feinkörniger Kontrolle zu konvertieren. Am Ende des Tutorials können Sie den Beispielcode ausführen und den extrahierten Text in der Konsole ausgegeben sehen.

HTML‑Dateien zu lesen ist eine gängige Aufgabe beim Verarbeiten von Web‑Scraping‑Daten, beim Erstellen von Berichten oder beim Bereinigen von nutzergenerierten Inhalten. Die nachfolgenden Schritte decken alles ab, was Sie benötigen, vom Hinzufügen der erforderlichen Bibliothek bis zum Umgang mit Sonderfällen wie fehlerhaftem Markup oder Zeichenkodierungsproblemen.

## Was Sie benötigen

- Java 17 oder neuer (der Code lässt sich auch mit früheren Versionen kompilieren)
- Maven oder Gradle für das Abhängigkeitsmanagement, oder das Jsoup‑JAR manuell hinzugefügt
- Eine HTML‑Datei namens `input.html` im Verzeichnis `src/main/resources` des Projekts (der Pfad kann später geändert werden)

## Jsoup-Bibliothek einrichten

Jsoup ist eine leichtgewichtige, gut dokumentierte Bibliothek, die HTML in eine DOM‑ähnliche Struktur parst. Sie verarbeitet defektes HTML robust, was sie ideal für **extract text from html**‑Aufgaben macht.

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

Wenn Sie einen manuellen Download bevorzugen, legen Sie das JAR in Ihren Klassenpfad und importieren Sie `org.jsoup.*` in Ihrer Quellcodedatei.

## HTML aus einer Datei laden

Der erste programmatische Schritt besteht darin, die Datei in ein `Document`‑Objekt zu lesen. Jsoup bietet eine statische `parse`‑Methode, die ein `File` und einen Zeichensatznamen akzeptiert.

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

**Why this matters:** `Jsoup.parse(File, String)` liest die Rohbytes, dekodiert sie gemäß dem angegebenen Zeichensatz und erstellt ein sauberes DOM. Dieser Ansatz ist sicherer, als die Datei selbst in einen String zu lesen, weil Jsoup Zeilenenden normalisiert und gängige Markup‑Fehler automatisch korrigiert.

## Klartext aus dem HTML extrahieren

Sobald Sie ein `Document` haben, ist das Abrufen des sichtbaren Textes ein einziger Methodenaufruf. Die `text()`‑Methode verkettet den Textinhalt aller Elemente und verwirft Tags, Skripte und Styles.

```java
// Inside the try block from the previous snippet
String plainText = doc.body().text();
System.out.println("Extracted text:");
System.out.println(plainText);
```

Der Aufruf `body()` begrenzt die Extraktion auf das `<body>`‑Element, das typischerweise das Ziel ist, wenn Sie **read html from file** für Inhaltsanalysen verwenden. Der resultierende String enthält Leerzeichen, die auf einzelne Leerzeichen reduziert wurden, und ahmt damit nach, wie ein Browser den Text rendern würde.

### Erwartete Ausgabe

Angenommen, `input.html` enthält:

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

Das Ausführen des Programms gibt aus:

```
Extracted text:
Hello World This is a demo page.
```

## HTML in Text mit zusätzlichen Optionen konvertieren

Manchmal benötigen Sie mehr Kontrolle als `text()` bietet – z. B. das Beibehalten von Zeilenumbrüchen, das Bewahren von Listennummerierungen oder das Ignorieren bestimmter Tags. Jsoups `NodeTraversor` in Kombination mit einem benutzerdefinierten `NodeVisitor` liefert diese Flexibilität.

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

Ersetzen Sie den einfachen Aufruf `doc.body().text()` durch:

```java
String detailedText = convertHtmlToText(doc);
System.out.println("Detailed conversion:");
System.out.println(detailedText);
```

**Why this works:** Der Visitor durchläuft das DOM tiefen‑first und fügt vor jedem Block‑Level‑Element (z. B. `<p>`, `<div>`, `<h1>`) einen Zeilenumbruch ein. Das erhält die Trennung von Absätzen, was nützlich ist, wenn Sie **convert html to text** für Lesbarkeit oder nachgelagerte NLP‑Pipelines benötigen.

## Häufige Fallstricke und bewährte Vorgehensweisen

| Problem | Warum es auftritt | Empfohlene Lösung |
|---------|-------------------|-------------------|
| Falsches Charset | Dateien, die in ISO‑8859‑1 gespeichert sind, aber als UTF‑8 geparst werden, erzeugen fehlerhafte Zeichen. | Erkennen Sie das Charset aus dem Meta‑Tag der Datei (`<meta charset="...">`) oder übergeben Sie den korrekten Namen an `Jsoup.parse`. |
| Große Dateien | Das Laden einer sehr großen HTML‑Datei in den Speicher kann zu `OutOfMemoryError` führen. | Streamen Sie die Datei mit `Jsoup.parse(File, String, String baseUri)` und verarbeiten Sie Knoten inkrementell, oder erhöhen Sie die JVM‑Heap‑Größe. |
| Unerwünschter Skript-/Stil‑Text | `text()` entfernt Skript‑ und Stil‑Inhalte, aber benutzerdefinierte Besucher können diese unbeabsichtigt einbeziehen. | Überspringen Sie Knoten, deren Tag‑Name `script` oder `style` ist, innerhalb der `head`‑Methode des Besuchers. |
| Erhaltung von Leerzeichen | Das Zusammenziehen von Leerzeichen kann Formatierungen verlieren, die für die Markdown‑Konvertierung nötig sind. | Verwenden Sie `Element.wholeText()` für rohe Textknoten und bearbeiten Sie Leerzeichen anschließend manuell. |

Die Berücksichtigung dieser Punkte stellt sicher, dass Ihre **html to text java**‑Lösung zuverlässig über verschiedene Eingaben hinweg funktioniert.

## Vollständiges ausführbares Beispiel

Unten finden Sie ein eigenständiges Programm, das den gesamten Workflow demonstriert – von der Einrichtung der Abhängigkeiten bis zur Ausgabeüberprüfung. Kopieren Sie den Code in eine Datei namens `HtmlToTextDemo.java`, legen Sie eine `input.html`‑Datei daneben und führen Sie `javac && java` wie gezeigt aus.

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

### Ausführen des Programms

```bash
javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java
java -cp .:jsoup-1.17.2.jar HtmlToTextDemo
```

Die Konsole zeigt sowohl die einfache Extraktion als auch die detaillierte

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man XPath in Java verwendet – HTML lesen und Text extrahieren](/html/english/java/creating-managing-html-documents/how-to-use-xpath-in-java-read-html-and-extract-text/)
- [Wie man HTML in Java parst – Text aus HTML‑Artikeln extrahieren](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Text aus HTML mit Java extrahieren – vollständiger Schritt‑für‑Schritt‑Leitfaden](/html/english/java/creating-managing-html-documents/extract-text-from-html-with-java-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}