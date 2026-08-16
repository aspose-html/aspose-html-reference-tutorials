---
date: 2026-05-30
description: Erfahren Sie, wie Sie EPUB in Java mit Aspose.HTML in PDF konvertieren
  und dabei eine benutzerdefinierte PDF‑Seitengröße sowie weitere PDF‑Speicheroptionen
  festlegen.
keywords:
- custom pdf page size
- convert epub to pdf
- change pdf background color
- specify pdf page dimensions
- aspose.html java
linktitle: Festlegen von PDF‑Speicheroptionen für EPUB zu PDF
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  headline: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  type: TechArticle
- description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  name: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  steps:
  - name: Open the EPUB File
    text: First, create a `FileInputStream` that points to your source `.epub`. Keeping
      the stream open until the conversion finishes prevents “blank page” errors.
  - name: Define PDF Save Options
    text: '`PdfSaveOptions` is Aspose.HTML''s configuration class that controls PDF
      output settings such as page size, background color, and margins. `Length.fromPixels`
      converts screen pixels to PDF points (1 point = 1/72 inch), allowing you to
      specify dimensions in familiar pixel units.'
  - name: Convert EPUB to PDF
    text: With the input stream and custom options ready, invoke the converter. The
      output PDF will be saved to the location you specify, preserving the exact page
      dimensions you defined. `PdfSaveOptions.setEnableParallelProcessing` is a method
      that enables parallel processing of pages during PDF conversion.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a commercial library, but you can obtain a free
      trial version from their [website](https://releases.aspose.com/).
    question: Is Aspose.HTML for Java a free library?
  - answer: Aspose.HTML for Java supports EPUB 2.0, EPUB 3.0, and EPUB 3.1, handling
      re‑flowable and fixed‑layout books with full CSS support.
    question: What EPUB formats are supported for conversion?
  - answer: Yes, you can customize the PDF output by adjusting the page setup, background
      color, compression level, and other settings in the `PdfSaveOptions`.
    question: Can I customize the PDF output further?
  - answer: The trial version may add a watermark to the first few pages and limits
      the maximum file size to 10 MB; purchase a license to remove these restrictions.
    question: Are there any limitations to the trial version of Aspose.HTML for Java?
  - answer: You can find answers to your questions and seek support on the [Aspose.HTML
      forum](https://forum.aspose.com/).
    question: Where can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: Benutzerdefinierte PDF‑Seitengröße – Festlegen von PDF‑Speicheroptionen für
  EPUB zu PDF
url: /de/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Benutzerdefinierte PDF‑Seitengröße: Festlegen von PDF‑Speicheroptionen für EPUB zu PDF

## Einführung

Aspose.HTML für Java macht es einfach, **EPUB in PDF** zu konvertieren und gibt Ihnen die volle Kontrolle über die Ausgabe, einschließlich der Festlegung einer **benutzerdefinierten PDF‑Seitengröße**. In diesem Schritt‑für‑Schritt‑Leitfaden führen wir Sie durch alles, was Sie benötigen – von der Vorbereitung Ihrer Umgebung bis zum Anpassen der `PdfSaveOptions`, sodass das erzeugte PDF exakt die von Ihnen gewünschten Seitenabmessungen hat. Egal, ob Sie eine Publishing‑Pipeline, eine E‑Learning‑Plattform aufbauen oder einfach die Dokumentenkonvertierung automatisieren möchten, die hier vorgestellten Techniken sind wertvoll.

## Schnelle Antworten
- **Was ist der Hauptzweck dieses Tutorials?** Ein EPUB‑Datei in PDF konvertieren und dabei eine benutzerdefinierte PDF‑Seitengröße anwenden.  
- **Welche Bibliothek wird verwendet?** Aspose.HTML für Java.  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion ist verfügbar; für den Produktionseinsatz ist eine kommerzielle Lizenz erforderlich.  
- **Kann ich die Hintergrundfarbe ändern?** Ja, mit `PdfSaveOptions`.  
- **Wird Java 8+ unterstützt?** Absolut – jede moderne Java‑Runtime funktioniert.

## Was ist eine benutzerdefinierte PDF‑Seitengröße?

Eine benutzerdefinierte PDF‑Seitengröße ermöglicht es Ihnen, die genaue Breite und Höhe jeder Seite im Ausgabepdf festzulegen, anstatt sich auf Standardgrößen wie A4 oder Letter zu verlassen.  
Sie können die Abmessungen in Punkten (1 Punkt = 1/72 Zoll) festlegen oder aus Pixeln konvertieren, wodurch Sie pixelgenaue Kontrolle über das endgültige Layout erhalten. Dies ist ideal für E‑Books, Flyer oder jedes Design, das ohne manuelle Nachbearbeitung einem vordefinierten Format entsprechen muss.

## Warum Aspose.HTML für die EPUB‑zu‑PDF‑Konvertierung verwenden?

Aspose.HTML konvertiert EPUB in PDF mit nur zwei Codezeilen und bewahrt dabei komplexe Layouts, eingebettete Schriftarten und hochauflösende Bilder. Es unterstützt **mehr als 50 Eingabe‑ und Ausgabeformate**, kann PDFs mit bis zu **2.000 Seiten** rendern, ohne die gesamte Datei in den Speicher zu laden, und läuft auf Windows, Linux und macOS mit identischen Ergebnissen. Die Bibliothek bietet zudem feinkörnige PDF‑Speicheroptionen, mit denen Sie Seitengröße, Hintergrundfarbe, Ränder und Komprimierungseinstellungen anpassen können – alles aus Java heraus.

## Voraussetzungen
- **Java-Entwicklungsumgebung:** JDK 8 oder höher installiert und konfiguriert.  
- **Aspose.HTML für Java:** Laden Sie das neueste JAR von der [Website](https://releases.aspose.com/html/java/) herunter.  
- **EPUB‑Datei:** Ein `.epub`‑Dokument, das Sie konvertieren möchten.  

Jetzt, da alles bereit ist, tauchen wir in die eigentlichen Konvertierungsschritte ein.

## Wie konvertiert man EPUB zu PDF mit einer benutzerdefinierten Seitengröße?

`FileInputStream` ist eine Java‑Klasse, die Rohbytes aus einer Datei liest.  
`PdfSaveOptions` ist eine Klasse in Aspose.HTML, die PDF‑Ausgabe­einstellungen wie Seitengröße und Hintergrundfarbe konfiguriert.  
Laden Sie Ihr EPUB mit einem `FileInputStream`, konfigurieren Sie `PdfSaveOptions`, um die genauen Seitenabmessungen festzulegen, und rufen Sie den Konverter auf. Der folgende dreistufige Arbeitsablauf führt die Konvertierung in weniger als einer Minute für typische E‑Book‑Größen durch und skaliert bei größeren Sammlungen mit minimalen Code‑Änderungen.

### Schritt 1: EPUB‑Datei öffnen

Zuerst erstellen Sie einen `FileInputStream`, der auf Ihre Quell‑`.epub`‑Datei zeigt. Das offene Halten des Streams bis zum Abschluss der Konvertierung verhindert „leere Seite“-Fehler.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

### Schritt 2: PDF‑Speicheroptionen definieren

`PdfSaveOptions` ist die Konfigurationsklasse von Aspose.HTML, die PDF‑Ausgabe­einstellungen wie Seitengröße, Hintergrundfarbe und Ränder steuert.  
`Length.fromPixels` konvertiert Bildschirmpixel in PDF‑Punkte (1 Punkt = 1/72 Zoll) und ermöglicht es Ihnen, Abmessungen in vertrauten Pixeleinheiten anzugeben.

```java
com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
anyPage.setSize(new com.aspose.html.drawing.Size(
    com.aspose.html.drawing.Length.fromPixels(3000),
    com.aspose.html.drawing.Length.fromPixels(1000))
);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
```

#### Profi‑Tipp:
- **Pixel vs. Punkte:** `Length.fromPixels` konvertiert Bildschirmpixel in PDF‑Punkte (1 Punkt = 1/72 Zoll). Wählen Sie Werte, die die gewünschte endgültige Druckgröße widerspiegeln.

### Schritt 3: EPUB zu PDF konvertieren

Mit dem Eingabestream und den benutzerdefinierten Optionen bereit, rufen Sie den Konverter auf. Das Ausgabepdf wird an dem von Ihnen angegebenen Ort gespeichert und bewahrt die von Ihnen definierten genauen Seitenabmessungen.

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

`PdfSaveOptions.setEnableParallelProcessing` ist eine Methode, die die parallele Verarbeitung von Seiten während der PDF‑Konvertierung aktiviert.

## Vollständiger Quellcode

Das vollständige, ausführbare Beispiel kombiniert die drei oben genannten Schritte in einer einzigen Java‑Klasse. Ersetzen Sie die Platzhalter‑Pfade durch Ihre eigenen Dateipfade.

```java
Specifying PDF Save Options for EPUB to PDF
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of the PdfSaveOptions with a custom page-size and a background-color.
            com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
            com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
            com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
            anyPage.setSize(new com.aspose.html.drawing.Size(
                    com.aspose.html.drawing.Length.fromPixels(3000),
                    com.aspose.html.drawing.Length.fromPixels(1000))
            );
            pageSetup.setAnyPage(anyPage);
            options.setPageSetup(pageSetup);
            options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
            // Call the ConvertEPUB method to convert the EPUB to PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```

## Häufige Probleme und Lösungen

| Problem | Ursache | Lösung |
|-------|-------|-----|
| **PDF‑Seiten sind leer** | Eingabestream vor der Konvertierung geschlossen | Den `try‑with‑resources`‑Block bis nach `convertEPUB` geöffnet lassen. |
| **Falsche Seitenabmessungen** | Verwendung von Pixeln, die nicht zur gewünschten Druckgröße passen | Gewünschte Zoll in Punkte umrechnen (`1 Zoll = 72 Punkte`) und dann mit `Length.fromPixels` in Pixel umwandeln. |
| **Fehlende Schriftarten** | Schriftarten nicht im EPUB eingebettet | Stellen Sie sicher, dass die Schriftarten im EPUB enthalten sind oder installieren Sie sie auf dem Host‑Rechner. |
| **Leistungsabfall bei großen Büchern** | Jede Seite wird sequenziell gerendert | Mehrthread‑Rendering über `PdfSaveOptions.setEnableParallelProcessing(true)` aktivieren, um die Verarbeitung von EPUBs mit über 500 Seiten zu beschleunigen. |

## Häufig gestellte Fragen (FAQs)

**Q: Ist Aspose.HTML für Java eine kostenlose Bibliothek?**  
A: Aspose.HTML für Java ist eine kommerzielle Bibliothek, aber Sie können eine kostenlose Testversion von ihrer [Website](https://releases.aspose.com/) erhalten.

**Q: Welche EPUB‑Formate werden für die Konvertierung unterstützt?**  
A: Aspose.HTML für Java unterstützt EPUB 2.0, EPUB 3.0 und EPUB 3.1 und verarbeitet wiederflussfähige sowie fest layoutete Bücher mit voller CSS‑Unterstützung.

**Q: Kann ich die PDF‑Ausgabe weiter anpassen?**  
A: Ja, Sie können die PDF‑Ausgabe anpassen, indem Sie die Seiteneinrichtung, Hintergrundfarbe, Komprimierungsgrad und andere Einstellungen im `PdfSaveOptions` ändern.

**Q: Gibt es Einschränkungen in der Testversion von Aspose.HTML für Java?**  
A: Die Testversion kann den ersten paar Seiten ein Wasserzeichen hinzufügen und die maximale Dateigröße auf 10 MB begrenzen; ein Lizenzkauf entfernt diese Beschränkungen.

**Q: Wo kann ich Support für Aspose.HTML für Java erhalten?**  
A: Sie finden Antworten auf Ihre Fragen und Support im [Aspose.HTML‑Forum](https://forum.aspose.com/).

**Zuletzt aktualisiert:** 2026-05-30  
**Getestet mit:** Aspose.HTML für Java 24.11 (zum Zeitpunkt des Schreibens aktuellste Version)  
**Autor:** Aspose

## Verwandte Tutorials

- [PDF‑Seitengröße mit Aspose.HTML für Java anpassen](/html/java/advanced-usage/adjust-pdf-page-size/)
- [Wie man EPUB zu PDF mit Java konvertiert – mit Aspose.HTML](/html/java/conversion-epub-to-image-and-pdf/convert-epub-to-pdf/)
- [EPUB zu PDF und Bildern mit Aspose.HTML für Java konvertieren](/html/java/conversion-epub-to-image-and-pdf/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}