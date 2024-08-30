---
title: Festlegen von PDF-Speicheroptionen für EPUB in PDF
linktitle: Festlegen von PDF-Speicheroptionen für EPUB in PDF
second_title: Java-HTML-Verarbeitung mit Aspose.HTML
description: Erfahren Sie, wie Sie mit Aspose.HTML, einer leistungsstarken HTML-Bearbeitungsbibliothek, EPUB in Java in PDF konvertieren.
type: docs
weight: 12
url: /de/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
---

## Einführung

Aspose.HTML für Java ist ein leistungsstarkes Tool zum Arbeiten mit HTML- und EPUB-Dokumenten. In dieser Schritt-für-Schritt-Anleitung führen wir Sie durch den Prozess der Konvertierung einer EPUB-Datei in PDF mit Aspose.HTML für Java. Egal, ob Sie ein erfahrener Entwickler sind oder gerade erst anfangen, dieses Tutorial vermittelt Ihnen das Wissen und die Fähigkeiten, die Sie benötigen, um diese Aufgabe effizient auszuführen.

## Voraussetzungen

Bevor wir beginnen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

- Java-Entwicklungsumgebung: Auf Ihrem System muss eine Java-Entwicklungsumgebung eingerichtet sein.

-  Aspose.HTML für Java: Laden Sie die Bibliothek Aspose.HTML für Java herunter und installieren Sie sie. Sie finden die Bibliothek und die zugehörige Dokumentation auf der[Webseite](https://releases.aspose.com/html/java/).

- EPUB-Datei: Sie benötigen eine EPUB-Datei, die Sie in PDF konvertieren möchten.

Lassen Sie uns nun in die Schritt-für-Schritt-Anleitung zur Konvertierung von EPUB in PDF mit Aspose.HTML für Java eintauchen.

## Schritt 1: Öffnen Sie die EPUB-Datei

 Öffnen Sie zunächst eine vorhandene EPUB-Datei zum Lesen. Sie können eine`FileInputStream` um dies zu erreichen. Hier ist der Code für diesen Schritt:

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Ihr Code für die nächsten Schritte wird hier eingefügt.
}
```

## Schritt 2: PDF-Speicheroptionen festlegen

 Erstellen Sie eine Instanz von`PdfSaveOptions` mit benutzerdefinierter Seitengröße und Hintergrundfarbe. Sie können das Seiten-Setup nach Ihren Anforderungen konfigurieren. So geht's:

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

## Schritt 3: EPUB in PDF konvertieren

 Rufen Sie jetzt die`ConvertEPUB` Methode zum Konvertieren der EPUB-Datei in PDF. Geben Sie den Eingabestream, die PDF-Speicheroptionen und den Ausgabeort an. So geht's:

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

Herzlichen Glückwunsch! Sie haben eine EPUB-Datei mit Aspose.HTML für Java erfolgreich in PDF konvertiert. Sie können jetzt am angegebenen Ausgabeort auf die konvertierte PDF-Datei zugreifen.

## Vollständiger Quellcode
```java
Specifying PDF Save Options for EPUB to PDF
        // Öffnen Sie eine vorhandene EPUB-Datei zum Lesen.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Erstellen Sie eine Instanz von PdfSaveOptions mit einer benutzerdefinierten Seitengröße und einer Hintergrundfarbe.
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
            // Rufen Sie die Methode ConvertEPUB auf, um EPUB in PDF zu konvertieren.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```


## Abschluss

In diesem Tutorial haben wir gelernt, wie man mit Aspose.HTML für Java EPUB-Dateien in das PDF-Format konvertiert. Diese vielseitige Bibliothek bietet Entwicklern leistungsstarke Tools zur Dokumentbearbeitung. Indem Sie die in diesem Handbuch beschriebenen Schritte befolgen, können Sie die Konvertierung von EPUB in PDF nahtlos in Ihre Java-Anwendungen integrieren.

## Häufig gestellte Fragen (FAQs)

### Ist Aspose.HTML für Java eine kostenlose Bibliothek?
 Aspose.HTML für Java ist eine kommerzielle Bibliothek, aber Sie können eine kostenlose Testversion von deren[Webseite](https://releases.aspose.com/).

### Welche EPUB-Formate werden für die Konvertierung unterstützt?
Aspose.HTML für Java unterstützt die Konvertierung verschiedener EPUB-Formate und gewährleistet Kompatibilität mit den meisten EPUB-Dokumenten.

### Kann ich die PDF-Ausgabe weiter anpassen?
 Ja, Sie können die PDF-Ausgabe anpassen, indem Sie die Seiteneinrichtung, die Hintergrundfarbe und andere Einstellungen im`PdfSaveOptions`.

### Gibt es irgendwelche Einschränkungen bei der Testversion von Aspose.HTML für Java?
Die Testversion weist möglicherweise einige Einschränkungen auf. Es wird daher empfohlen, die Dokumentation auf Einzelheiten zu prüfen.

### Wo erhalte ich Support für Aspose.HTML für Java?
Antworten auf Ihre Fragen und Unterstützung finden Sie auf der[Aspose.HTML-Forum](https://forum.aspose.com/).
