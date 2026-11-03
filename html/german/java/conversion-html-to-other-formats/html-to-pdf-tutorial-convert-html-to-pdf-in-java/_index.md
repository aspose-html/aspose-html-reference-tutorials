---
category: general
date: 2026-06-19
description: Erfahren Sie, wie Sie PDF aus HTML mit einem einfachen Java‑Beispiel
  erzeugen. Dieses HTML‑zu‑PDF‑Tutorial zeigt Ihnen, wie Sie HTML‑Dateien mit OpenHTMLtoPDF
  in PDF konvertieren.
draft: false
keywords:
- html to pdf tutorial
- generate pdf from html
- convert html file pdf
- create pdf from html
- convert webpage to pdf
language: de
og_description: Das HTML‑zu‑PDF‑Tutorial zeigt Ihnen, wie Sie mit Java PDFs aus HTML
  generieren. Befolgen Sie die Schritte, um HTML‑Dateien schnell in PDFs zu konvertieren.
og_title: 'HTML-zu-PDF-Tutorial: Java-Konvertierungsleitfaden'
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  headline: 'html to pdf tutorial: Convert HTML to PDF in Java'
  type: TechArticle
- description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  name: 'html to pdf tutorial: Convert HTML to PDF in Java'
  steps:
  - name: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
    text: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
  - name: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
    text: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
  - name: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
    text: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
  type: HowTo
tags:
- Java
- PDF
- HTML conversion
title: 'HTML-zu-PDF-Tutorial: HTML in PDF mit Java konvertieren'
url: /de/java/conversion-html-to-other-formats/html-to-pdf-tutorial-convert-html-to-pdf-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# html to pdf tutorial – Eine HTML‑Seite mit Java in ein PDF umwandeln

Haben Sie sich jemals gefragt, wie man eine statische HTML‑Seite in ein elegantes PDF‑Dokument verwandelt, ohne die IDE zu verlassen? Sie sind nicht allein. In diesem **html to pdf tutorial** führen wir Sie durch ein komplettes, sofort ausführbares Java‑Beispiel, das **generate pdf from html** in nur wenigen Minuten erzeugt.

Wir behandeln alles, was Sie benötigen – Projekt‑Setup, das Hinzufügen der richtigen Bibliothek, das Schreiben des Konvertierungscodes und sogar einen schnellen Tipp zum Konvertieren einer Live‑Webseite in ein PDF. Am Ende können Sie **convert html file pdf** auf Ihrem eigenen Rechner ausführen und verstehen, wie man **create pdf from html** für jedes zukünftige Projekt erstellt.

## Was Sie benötigen

- Java 17 oder neuer (der Code funktioniert mit jedem aktuellen JDK)
- Maven oder Gradle (wir zeigen das Maven‑Snippet)
- Eine kleine HTML‑Datei, die Sie in ein PDF umwandeln möchten (wir erstellen sie sofort)
- Eine IDE oder ein einfacher Texteditor – Ihre Entscheidung

Das ist alles. Keine schweren Server, keine kostenpflichtigen SDKs, nur reines Java und eine kostenlose Open‑Source‑Bibliothek.

## Schritt 1: html to pdf tutorial – Ein Maven‑Projekt einrichten

Zuerst das Wichtigste. Erstellen Sie ein neues Maven‑Projekt (oder fügen Sie es zu einem bestehenden hinzu). Die einzige Abhängigkeit, die Sie wirklich benötigen, ist **OpenHTMLtoPDF**, das das schwere Heben beim Rendern von HTML und CSS in ein PDF übernimmt.

```xml
<!-- pom.xml snippet -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>html-to-pdf-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- OpenHTMLtoPDF core -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-pdfbox</artifactId>
            <version>1.0.10</version>
        </dependency>
        <!-- Optional: support for SVG, if your HTML uses it -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-svg-support</artifactId>
            <version>1.0.10</version>
        </dependency>
    </dependencies>
</project>
```

> **Pro‑Tipp:** Wenn Sie Gradle verwenden, können dieselben Abhängigkeiten unter `implementation` in `build.gradle` hinzugefügt werden.  

Warum dieser Schritt wichtig ist: Ohne die Bibliothek weiß die JVM nicht, wie HTML‑Tags in PDF‑Zeichenbefehle übersetzt werden sollen. OpenHTMLtoPDF ist leichtgewichtig, wird aktiv gepflegt und unterstützt CSS‑2.1, sodass Ihr Styling erhalten bleibt.

## Schritt 2: generate pdf from html – Eine Beispiel‑HTML‑Datei vorbereiten

Lassen Sie uns eine kleine `input.html` direkt neben unserem Java‑Quellcode erstellen. Das hält das Beispiel eigenständig und demonstriert den **create pdf from html**‑Arbeitsablauf.

```html
<!-- src/main/resources/input.html -->
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Sample Report</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        h1 { color: #2E86C1; }
        p { line-height: 1.5; }
    </style>
</head>
<body>
    <h1>Monthly Sales Report</h1>
    <p>This PDF was generated directly from an HTML file using Java.</p>
    <p>All you need is a few lines of code.</p>
</body>
</html>
```

Sie können den Inhalt durch alles ersetzen – Tabellen, Bilder, sogar JavaScript (der Renderer ignoriert jedoch Skripte). Wichtig ist, dass die Datei im Klassenpfad liegt, damit der Konverter sie finden kann.

## Schritt 3: convert html file pdf – Das Konvertierungs‑Utility schreiben

Jetzt das Herzstück des **html to pdf tutorial**: eine kleine `HtmlToPdfConverter`‑Klasse, die das HTML liest und ein PDF schreibt. Der untenstehende Code ist ein vollständiges, ausführbares Beispiel; kopieren Sie ihn nach `src/main/java/com/example/HtmlToPdfConverter.java`.

```java
package com.example;

import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardCopyOption;

/**
 * Simple utility that converts an HTML file to PDF.
 * It demonstrates the "convert html file pdf" use‑case.
 */
public class HtmlToPdfConverter {

    /**
     * Converts the given HTML file to a PDF file.
     *
     * @param htmlPath path to the source HTML file (can be absolute or classpath)
     * @param pdfPath  destination path for the generated PDF
     * @throws IOException if reading or writing fails
     */
    public static void convert(String htmlPath, String pdfPath) throws IOException {
        // Resolve the HTML file – support both absolute paths and classpath resources
        InputStream htmlStream = Files.exists(Path.of(htmlPath))
                ? Files.newInputStream(Path.of(htmlPath))
                : HtmlToPdfConverter.class.getResourceAsStream(htmlPath);

        if (htmlStream == null) {
            throw new FileNotFoundException("HTML source not found: " + htmlPath);
        }

        // Ensure the output directory exists
        Path pdfFile = Path.of(pdfPath);
        Files.createDirectories(pdfFile.getParent());

        try (OutputStream os = Files.newOutputStream(pdfFile);
             InputStream is = htmlStream) {

            // Builder does the heavy lifting – it parses HTML + CSS and writes PDF bytes
            new PdfRendererBuilder()
                    .withHtmlContent(new String(is.readAllBytes()), null) // base URI null = no external resources
                    .toStream(os)
                    .run();
        }
    }

    // Demo entry point – feel free to run this class directly
    public static void main(String[] args) {
        // Step 1: Specify the input HTML file location
        String htmlPath = "src/main/resources/input.html";

        // Step 2: Specify the desired output PDF file location
        String pdfPath = "target/output.pdf";

        // Step 3: Convert the HTML document to PDF using default conversion settings
        try {
            convert(htmlPath, pdfPath);
            System.out.println("✅ PDF successfully created at " + pdfPath);
        } catch (Exception e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Warum dieser Code funktioniert

1. **Ressourcen‑Flexibilität** – die Methode prüft zuerst, ob der angegebene Pfad auf eine echte Datei zeigt; falls nicht, greift sie auf eine Klassenpfad‑Ressource zurück. Das bedeutet, Sie können später **convert webpage to pdf** ausführen, indem Sie einen URL‑String übergeben (einfach den Aufruf `withHtmlContent` durch `withUri` ersetzen).

2. **Automatisches Erstellen von Verzeichnissen** – `Files.createDirectories` stellt sicher, dass der Ordner `target/` existiert, sodass Sie keinen „No such file or directory“-Fehler erhalten.

3. **Einzeilige Konvertierung** – `PdfRendererBuilder` verarbeitet CSS, Schriften und Seitenlayout intern. Es ist nicht nötig, PDF‑Seiten manuell zu verwalten; die Bibliothek übernimmt das für Sie und hält das Beispiel kurz und fokussiert auf das **convert html file pdf**‑Konzept.

## Schritt 4: create pdf from html – Das Programm ausführen und überprüfen

Öffnen Sie ein Terminal im Projekt‑Root und führen Sie aus:

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HtmlToPdfConverter
```

Wenn alles korrekt eingerichtet ist, sehen Sie:

```
✅ PDF successfully created at target/output.pdf
```

Öffnen Sie `target/output.pdf` mit einem beliebigen PDF‑Betrachter. Sie sollten die formatierte Überschrift „Monthly Sales Report“, den Absatztext und dieselben Ränder sehen, die Sie im HTML‑`<style>`‑Block definiert haben.

> **Was, wenn Sie das Styling nicht sehen?**  
> Stellen Sie sicher, dass das CSS inline ist oder sich im selben Ordner wie das HTML befindet. OpenHTMLtoPDF löst relative URLs basierend auf der Basis‑URI auf, die Sie `withHtmlContent` übergeben. Im obigen Snippet haben wir `null` übergeben, was für einfaches Inline‑CSS funktioniert. Für externe Stylesheets geben Sie den Verzeichnispfad als zweites Argument an.

## Schritt 5: convert webpage to pdf – Remote‑URLs verarbeiten (optional)

Manchmal müssen Sie **convert webpage to pdf** direkt aus dem Internet durchführen – denken Sie an das Archivieren einer Online‑Quittung. Die Bibliothek unterstützt dies über `withUri`. Hier ist eine schnelle Anpassung:

```java
public static void convertUrl(String url, String pdfPath) throws IOException {
    Path pdfFile = Path.of(pdfPath);
    Files.createDirectories(pdfFile.getParent());

    try (OutputStream os = Files.newOutputStream(pdfFile)) {
        new PdfRendererBuilder()
                .withUri(url)          // Load HTML from the web
                .toStream(os)
                .run();
    }
}
```

Rufen Sie es so auf:



## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man HTML nach PDF in Java konvertiert – Verwendung von Aspose.HTML für Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [HTML nach PDF in Java konvertieren – Umgebung in Aspose.HTML konfigurieren](/html/english/java/configuring-environment/)
- [HTML nach PDF in Java konvertieren – Schritt‑für‑Schritt‑Anleitung mit Seitengrößeneinstellungen](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}