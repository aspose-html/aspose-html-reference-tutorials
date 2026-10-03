---
category: general
date: 2026-10-02
description: Erstelle PDF aus HTML in Java mit einem einzigen Aufruf. Dieses Tutorial
  zeigt, wie man HTML in PDF konvertiert, Optionen konfiguriert und häufige Probleme
  behandelt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf from html
- convert html to pdf
- how to convert html to pdf
- html to pdf conversion java
- convert html file to pdf
language: de
lastmod: 2026-10-02
og_description: Erstelle PDF aus HTML in Java mit HtmlConverter. Folge diesem umfassenden
  Leitfaden, um HTML in PDF zu konvertieren, Optionen festzulegen und Fallstricke
  zu vermeiden.
og_image_alt: Diagram showing create pdf from html process in Java
og_title: PDF aus HTML in Java erstellen – schnelle, zuverlässige Konvertierung
schemas:
- author: Aspose
  dateModified: '2026-10-02'
  description: Create pdf from html in Java with a single call. This tutorial shows
    how to convert html to pdf, configure options, and handle common issues.
  headline: How to create pdf from html in Java – step‑by‑step guide
  type: TechArticle
- description: Create pdf from html in Java with a single call. This tutorial shows
    how to convert html to pdf, configure options, and handle common issues.
  name: How to create pdf from html in Java – step‑by‑step guide
  steps:
  - name: Why this approach works
    text: '* **Single responsibility** – the `convertHtmlToPdf` method isolates the
      conversion logic, making the code easy to test. * **Resource safety** – `try‑with‑resources`
      guarantees that the `PDDocument` is closed, preventing file‑handle leaks. *
      **Flexibility** – you can swap `HtmlRenderer` for another '
  - name: 1️⃣ Specify the source HTML file and the target PDF file
    text: '```java private static final String INPUT_PATH = "YOUR_DIRECTORY/input.html";
      private static final String OUTPUT_PATH = "YOUR_DIRECTORY/output.pdf"; ``` *Replace
      `YOUR_DIRECTORY` with an absolute or relative path that your Java process can
      read/write.*'
  - name: 2️⃣ Load the HTML content
    text: '```java String html = Files.readString(Path.of(INPUT_PATH)); ``` Reading
      the file as a `String` preserves the original markup and makes it easy to feed
      the converter. The method assumes UTF‑8; if your HTML uses a different charset,
      use `Files.readAllBytes` and decode accordingly.'
  - name: 3️⃣ Convert the HTML document to PDF
    text: '```java byte[] pdfBytes = convertHtmlToPdf(html); ``` `convertHtmlToPdf`
      encapsulates **how to convert html to pdf**. Inside, `HtmlRenderer` parses the
      markup, applies CSS, and draws the result onto a PDF page. This is the heart
      of the **html to pdf conversion java** process.'
  - name: 4️⃣ Write the PDF file
    text: '```java Files.write(Path.of(OUTPUT_PATH), pdfBytes, StandardOpenOption.CREATE,
      StandardOpenOption.TRUNCATE_EXISTING); ``` The `Files.write` call creates the
      output file if it does not exist, or overwrites it otherwise. The method throws
      `IOException` if the directory is missing or the process lacks '
  type: HowTo
tags:
- Java
- PDF
- HTML conversion
title: Wie man in Java aus HTML ein PDF erstellt – Schritt‑für‑Schritt‑Anleitung
url: /de/java/conversion-html-to-other-formats/how-to-create-pdf-from-html-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man pdf aus html in Java erstellt – Schritt‑für‑Schritt‑Anleitung

Wenn Sie **pdf aus html erstellen** in einer Java‑Anwendung benötigen, zeigt Ihnen dieses Handbuch eine vollständige, sofort einsatzbereite Lösung. Sie sehen, wie man **html in pdf konvertiert** mit einem einzigen Methodenaufruf, die Konvertierung konfiguriert und typische Randfälle behandelt.

Wir behandeln alles, was Sie wissen müssen: erforderliche Abhängigkeiten, eine vollständige Quelldatei und Tipps zur Fehlersuche. Am Ende können Sie **html‑Datei zuverlässig in pdf konvertieren** in jedem Java‑Projekt.

## Voraussetzungen

* JDK 17 oder neuer installiert  
* Maven 3.8+ (oder Gradle) zur Verwaltung der Abhängigkeiten  
* Grundlegende Kenntnisse von Java I/O  

Das Beispiel verwendet die Open‑Source‑Klasse **HtmlConverter** aus der *pdfbox‑layout*‑Bibliothek, die Apache PDFBox für die HTML‑Renderung einbindet. Wenn Sie eine andere Bibliothek bevorzugen, gelten dieselben Schritte – passen Sie einfach die Import‑Anweisungen an.

## Erforderliche Abhängigkeit hinzufügen

Fügen Sie die folgenden Maven‑Koordinaten zu Ihrer `pom.xml` hinzu. Dadurch werden PDFBox und das HTML‑zu‑PDF‑Hilfsmodul eingebunden.

```xml
<dependency>
    <groupId>org.apache.pdfbox</groupId>
    <artifactId>pdfbox</artifactId>
    <version>3.0.2</version>
</dependency>
<dependency>
    <groupId>com.github.jhonnymertz</groupId>
    <artifactId>pdfbox-layout</artifactId>
    <version>1.0.0</version>
</dependency>
```

Wenn Sie Gradle verwenden, ist das Äquivalent:

```gradle
implementation "org.apache.pdfbox:pdfbox:3.0.2"
implementation "com.github.jhonnymertz:pdfbox-layout:1.0.0"
```

> **Pro‑Tipp:** Halten Sie Ihre Abhängigkeiten aktuell; neuere Versionen beheben Rendering‑Fehler und fügen CSS‑Unterstützung hinzu.

## pdf aus html erstellen – Gesamt‑Ablauf

Die Konvertierung besteht aus drei logischen Schritten:

1. **Quell‑HTML‑Datei lesen** – stellen Sie sicher, dass der Pfad korrekt ist und die Datei UTF‑8 kodiert ist.  
2. **Den Konverter aufrufen** – die Bibliothek parst das HTML, wendet CSS an und erzeugt ein PDF‑Dokument.  
3. **Das PDF auf die Festplatte schreiben** – behandeln Sie I/O‑Ausnahmen und bestätigen Sie, dass die Datei erstellt wurde.  

Unten finden Sie eine vollständige, eigenständige Java‑Klasse, die diesen Ablauf implementiert.

```java
package com.example.pdfconverter;

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

import org.apache.pdfbox.pdmodel.PDDocument;
import org.apache.pdfbox.pdmodel.PDPage;
import org.apache.pdfbox.pdmodel.PDPageContentStream;
import org.apache.pdfbox.pdmodel.common.PDRectangle;
import org.apache.pdfbox.layout.Document;
import org.apache.pdfbox.layout.element.Paragraph;
import org.apache.pdfbox.layout.renderer.HtmlRenderer;

/**
 * Simple utility that demonstrates how to create pdf from html in Java.
 *
 * The class reads an HTML file, converts it to PDF, and saves the result.
 * It uses Apache PDFBox together with the pdfbox‑layout HtmlRenderer.
 *
 * Adjust INPUT_PATH and OUTPUT_PATH to match your environment.
 */
public class HtmlToPdfConverter {

    // --------------------------------------------------------------------
    // 1️⃣  Define input and output locations
    // --------------------------------------------------------------------
    private static final String INPUT_PATH  = "YOUR_DIRECTORY/input.html";
    private static final String OUTPUT_PATH = "YOUR_DIRECTORY/output.pdf";

    public static void main(String[] args) {
        try {
            // --------------------------------------------------------------
            // 2️⃣  Load the HTML content (UTF‑8 is assumed)
            // --------------------------------------------------------------
            String html = Files.readString(Path.of(INPUT_PATH));

            // --------------------------------------------------------------
            // 3️⃣  Perform the conversion
            // --------------------------------------------------------------
            byte[] pdfBytes = convertHtmlToPdf(html);

            // --------------------------------------------------------------
            // 4️⃣  Write the PDF file to disk
            // --------------------------------------------------------------
            Files.write(Path.of(OUTPUT_PATH), pdfBytes,
                    StandardOpenOption.CREATE,
                    StandardOpenOption.TRUNCATE_EXISTING);

            System.out.println("✅ PDF created successfully at " + OUTPUT_PATH);
        } catch (IOException e) {
            System.err.println("❌ Failed to convert HTML to PDF: " + e.getMessage());
            e.printStackTrace();
        }
    }

    /**
     * Core conversion logic.
     *
     * @param html the raw HTML string
     * @return a byte array containing the generated PDF
     * @throws IOException if PDF generation fails
     */
    private static byte[] convertHtmlToPdf(String html) throws IOException {
        // Create a new PDFBox document – this is the container for the output.
        try (PDDocument pdDocument = new PDDocument()) {

            // The HtmlRenderer parses the HTML and draws it onto a PDF page.
            HtmlRenderer renderer = new HtmlRenderer(pdDocument);
            renderer.renderHtml(html);

            // Save the document into a byte array so we can write it later.
            return toByteArray(pdDocument);
        }
    }

    /**
     * Helper that converts a PDDocument into a byte array.
     *
     * @param document the populated PDFBox document
     * @return PDF content as a byte array
     * @throws IOException if writing fails
     */
    private static byte[] toByteArray(PDDocument document) throws IOException {
        try (java.io.ByteArrayOutputStream out = new java.io.ByteArrayOutputStream()) {
            document.save(out);
            return out.toByteArray();
        }
    }
}
```

### Warum dieser Ansatz funktioniert

* **Single Responsibility** – die Methode `convertHtmlToPdf` isoliert die Konvertierungslogik und macht den Code leicht testbar.  
* **Ressourcensicherheit** – `try‑with‑resources` stellt sicher, dass das `PDDocument` geschlossen wird, wodurch Dateihandle‑Lecks vermieden werden.  
* **Flexibilität** – Sie können `HtmlRenderer` gegen eine andere Implementierung austauschen (z. B. *OpenHTMLtoPDF*), ohne den umgebenden I/O‑Code zu ändern, was nützlich ist, wenn Sie **html to pdf conversion java** benötigen, das erweitertes CSS unterstützt.

## Schritt‑für‑Schritt‑Erklärung

### 1️⃣ Quell‑HTML‑Datei und Ziel‑PDF‑Datei angeben
```java
private static final String INPUT_PATH  = "YOUR_DIRECTORY/input.html";
private static final String OUTPUT_PATH = "YOUR_DIRECTORY/output.pdf";
```
*Ersetzen Sie `YOUR_DIRECTORY` durch einen absoluten oder relativen Pfad, den Ihr Java‑Prozess lesen/schreiben kann.*

### 2️⃣ HTML‑Inhalt laden
```java
String html = Files.readString(Path.of(INPUT_PATH));
```

Das Einlesen der Datei als `String` bewahrt das ursprüngliche Markup und erleichtert das Übergeben an den Konverter. Die Methode geht von UTF‑8 aus; verwendet Ihr HTML ein anderes Charset, nutzen Sie `Files.readAllBytes` und dekodieren Sie entsprechend.

### 3️⃣ HTML‑Dokument in PDF konvertieren
```java
byte[] pdfBytes = convertHtmlToPdf(html);
```

`convertHtmlToPdf` kapselt **wie man html in pdf konvertiert**. Intern parst `HtmlRenderer` das Markup, wendet CSS an und zeichnet das Ergebnis auf eine PDF‑Seite. Das ist das Kernstück des **html to pdf conversion java**‑Prozesses.

### 4️⃣ PDF‑Datei schreiben
```java
Files.write(Path.of(OUTPUT_PATH), pdfBytes,
        StandardOpenOption.CREATE,
        StandardOpenOption.TRUNCATE_EXISTING);
```

Der Aufruf `Files.write` erstellt die Ausgabedatei, falls sie nicht existiert, oder überschreibt sie andernfalls. Die Methode wirft `IOException`, wenn das Verzeichnis fehlt oder der Prozess keine Schreibberechtigung hat.

## Umgang mit häufigen Fallstricken

| Problem | Symptome | Lösung |
|-------|----------|-----|
| **Fehlende Eingabedatei** | `java.nio.file.NoSuchFileException` | Überprüfen Sie, ob `INPUT_PATH` auf eine vorhandene Datei zeigt. Verwenden Sie `Files.exists(Path)` für einen Vorab‑Check. |
| **Nicht unterstütztes CSS** | Layout sieht schlicht oder fehlerhaft aus | Verwenden Sie eine funktionsreichere Engine wie *OpenHTMLtoPDF* (fügen Sie deren Maven‑Abhängigkeit hinzu und ersetzen Sie `HtmlRenderer` durch `PdfRendererBuilder`). |
| **Großes HTML verursacht Speicherbelastung** | `OutOfMemoryError` | Streamen Sie das HTML in Teilen oder erhöhen Sie den JVM‑Heap (`-Xmx2g`). |
| **Unicode‑Zeichen erscheinen als �** | Verzerrter Text im PDF | Stellen Sie sicher, dass die HTML‑Datei als UTF‑8 gespeichert ist und dass die Schrift des Renderers die benötigten Glyphen unterstützt (betten Sie eine Schrift ein via `renderer.setDefaultFont("Arial Unicode MS")`). |

## Voll funktionsfähiges Beispiel

Speichern Sie die obige Klasse als `src/main/java/com/example/pdfconverter/HtmlToPdfConverter.java`, passen Sie die Pfade an und führen Sie sie aus:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.pdfconverter.HtmlToPdfConverter"
```

Wenn alles korrekt eingerichtet ist, sehen Sie:

```
✅ PDF created successfully at YOUR_DIRECTORY/output.pdf
```

Öffnen Sie `output.pdf` mit einem beliebigen PDF‑Betrachter – Sie sollten die gerenderte HTML‑Seite exakt so sehen, wie sie im Browser erscheint.

## Fazit

Sie wissen jetzt, wie man **pdf aus html erstellt** in Java mit einem knappen, produktionsbereiten Muster. Das Tutorial behandelte:

* Hinzufügen der notwendigen Maven‑Abhängigkeiten  
* Sicheres Einlesen einer HTML‑Datei  
* Ausführen der **convert html file to pdf**‑Operation mit `HtmlRenderer`  
* Schreiben des resultierenden PDFs und Umgang mit I/O‑Fehlern  

Ab hier können Sie fortgeschrittene Themen erkunden, wie **convert html to pdf** mit benutzerdefinierten Kopf‑/Fußzeilen, Streaming großer Dokumente oder den Wechsel zu einer anderen Rendering‑Engine für umfangreichere CSS‑Unterstützung.

**Nächste Schritte**

* Probieren Sie **how to convert html to pdf** mit *OpenHTMLtoPDF* für bessere CSS3‑Unterstützung.  
* Experimentieren Sie mit dem Hinzufügen einer Titelseite oder eines Inhaltsverzeichnisses mittels PDFBox direkt.  
* Untersuchen Sie die serverseitige PDF‑Erstellung für Web‑Services, bei der Sie die PDF‑Bytes in einer HTTP‑Antwort zurückgeben.

Viel Spaß beim Coden und genießen Sie den reibungslosen Workflow, HTML in hochwertige PDFs zu verwandeln!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man HTML zu PDF in Java konvertiert – Verwendung von Aspose.HTML für Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [PDF aus HTML in Java erstellen – Vollständiger Schritt‑für‑Schritt‑Leitfaden](/html/english/java/conversion-html-to-other-formats/create-pdf-from-html-in-java-complete-step-by-step-guide/)
- [html‑to‑pdf‑Tutorial: HTML in Java mit einem Aufruf in PDF konvertieren](/html/english/java/conversion-html-to-other-formats/html-to-pdf-tutorial-convert-html-to-pdf-in-java-in-one-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}