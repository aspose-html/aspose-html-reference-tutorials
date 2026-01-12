---
date: 2026-01-02
description: Erfahren Sie, wie Sie EPUB in Java mit Aspose.HTML in PDF konvertieren,
  wobei Sie eine benutzerdefinierte PDF‑Seitengröße und weitere PDF‑Speicheroptionen
  festlegen.
linktitle: Specifying PDF Save Options for EPUB to PDF
second_title: Java HTML Processing with Aspose.HTML
title: 'Benutzerdefinierte PDF‑Seitengröße: PDF‑Speicheroptionen für EPUB zu PDF festlegen'
url: /de/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Benutzerdefinierte PDF‑Seitengröße: Festlegen von PDF‑Speicheroptionen für EPUB zu PDF

## Einführung

Aspose.HTML for Java macht es einfach, **EPUB in PDF** zu konvertieren und gibt Ihnen die volle Kontrolle über die Ausgabe, einschließlich der Festlegung einer **benutzerdefinierten PDF‑Seitengröße**. In dieser Schritt‑für‑Schritt‑Anleitung führen wir Sie durch alles, was Sie benötigen – von der Vorbereitung Ihrer Umgebung bis zum Anpassen der `PdfSaveOptions`, sodass das erzeugte PDF exakt die von Ihnen gewünschten Seitenabmessungen hat. Egal, ob Sie eine Publishing‑Pipeline, eine E‑Learning‑Plattform aufbauen oder einfach die Dokumentenkonvertierung automatisieren möchten, Sie werden die hier vorgestellten Techniken als wertvoll empfinden.

## Schnelle Antworten
- **Was ist der Hauptzweck dieses Tutorials?** Ein EPUB‑Datei in PDF konvertieren und dabei eine benutzerdefinierte PDF‑Seitengröße anwenden.  
- **Welche Bibliothek wird verwendet?** Aspose.HTML for Java.  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion ist verfügbar; für den Produktionseinsatz ist eine kommerzielle Lizenz erforderlich.  
- **Kann ich die Hintergrundfarbe ändern?** Ja, mit `PdfSaveOptions`.  
- **Wird Java 8+ unterstützt?** Absolut – jede moderne Java‑Runtime funktioniert.

## Was ist eine benutzerdefinierte PDF‑Seitengröße?

Eine benutzerdefinierte PDF‑Seitengröße ermöglicht es Ihnen, die genaue Breite und Höhe jeder Seite im Ausgabepdf festzulegen, anstatt sich auf Standardgrößen wie A4 oder Letter zu verlassen. Dies ist besonders nützlich für E‑Books, Flyer oder jede Situation, in der das visuelle Layout einem bestimmten Design entsprechen muss.

## Warum Aspose.HTML für die EPUB‑zu‑PDF‑Konvertierung verwenden?

- **Hohe Treue:** Bewahrt komplexe Layouts, Schriftarten und Bilder.  
- **Fein abgestimmte Kontrolle:** Seitengröße, Hintergrund, Ränder und mehr über `PdfSaveOptions` anpassen.  
- **Plattformübergreifend:** Funktioniert unter Windows, Linux und macOS mit demselben Java‑Code.  
- **Leistung:** Optimierte Rendering‑Engine für schnelle Konvertierungen.

## Voraussetzungen

- **Java-Entwicklungsumgebung:** JDK 8 oder höher installiert und konfiguriert.  
- **Aspose.HTML for Java:** Laden Sie das neueste JAR von der [Website](https://releases.aspose.com/html/java/) herunter.  
- **EPUB‑Datei:** Ein `.epub`‑Dokument, das Sie konvertieren möchten.  

Jetzt, da alles bereit ist, tauchen wir in die eigentlichen Konvertierungsschritte ein.

## Schritt 1: EPUB‑Datei öffnen

Zuerst müssen wir die EPUB‑Datei mit einem `FileInputStream` öffnen. Dieser Stream wird später an den Konverter übergeben.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

## Schritt 2: PDF‑Speicheroptionen definieren

Hier legen wir die **benutzerdefinierte PDF‑Seitengröße** und die optionale Hintergrundfarbe fest. Passen Sie die Pixelwerte an, um die gewünschten Abmessungen zu erreichen.

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

### Profi‑Tipp:
- **Pixel vs. Punkte:** `Length.fromPixels` konvertiert Bildschirmpixel in PDF‑Punkte (1 Punkt = 1/72 Zoll). Wählen Sie Werte, die die endgültige Druckgröße widerspiegeln, die Sie benötigen.

## Schritt 3: EPUB nach PDF konvertieren

Mit dem Eingabestream und den benutzerdefinierten Optionen bereit, rufen Sie den Konverter auf. Das erzeugte PDF wird an dem von Ihnen angegebenen Ort gespeichert.

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

## Vollständiger Quellcode

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
| **PDF‑Seiten sind leer** | Eingabestream wurde vor der Konvertierung geschlossen | Lassen Sie den `try‑with‑resources`‑Block bis nach `convertEPUB` geöffnet. |
| **Falsche Seitenabmessungen** | Verwendung von Pixeln, die nicht zur gewünschten Druckgröße passen | Konvertieren Sie die gewünschten Zoll in Punkte (`1 inch = 72 points`) und dann in Pixel mit `Length.fromPixels`. |
| **Fehlende Schriftarten** | Schriftarten nicht im EPUB eingebettet | Stellen Sie sicher, dass die Schriftarten im EPUB enthalten sind oder installieren Sie sie auf dem Host‑Rechner. |

## Häufig gestellte Fragen (FAQs)

### Ist Aspose.HTML for Java eine kostenlose Bibliothek?
Aspose.HTML for Java ist eine kommerzielle Bibliothek, aber Sie können eine kostenlose Testversion von ihrer [Website](https://releases.aspose.com/) erhalten.

### Welche EPUB‑Formate werden für die Konvertierung unterstützt?
Aspose.HTML for Java unterstützt die Konvertierung verschiedener EPUB‑Formate und gewährleistet die Kompatibilität mit den meisten EPUB‑Dokumenten.

### Kann ich die PDF‑Ausgabe weiter anpassen?
Ja, Sie können die PDF‑Ausgabe anpassen, indem Sie die Seiteneinrichtung, Hintergrundfarbe und weitere Einstellungen in den `PdfSaveOptions` ändern.

### Gibt es Einschränkungen in der Testversion von Aspose.HTML for Java?
Die Testversion kann einige Einschränkungen haben; es wird empfohlen, die Dokumentation für Details zu prüfen.

### Wo kann ich Unterstützung für Aspose.HTML for Java erhalten?
Sie finden Antworten auf Ihre Fragen und erhalten Unterstützung im [Aspose.HTML‑Forum](https://forum.aspose.com/).

---

**Zuletzt aktualisiert:** 2026-01-02  
**Getestet mit:** Aspose.HTML for Java 24.11 (neueste zum Zeitpunkt der Erstellung)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}