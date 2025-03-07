---
title: Passen Sie die PDF-Seitengröße mit Aspose.HTML für Java an
linktitle: Anpassen der PDF-Seitengröße
second_title: Java-HTML-Verarbeitung mit Aspose.HTML
description: Erfahren Sie, wie Sie die PDF-Seitengröße mit Aspose.HTML für Java anpassen. Erstellen Sie mühelos hochwertige PDFs aus HTML. Kontrollieren Sie die Seitenabmessungen effektiv.
weight: 15
url: /de/java/advanced-usage/adjust-pdf-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Passen Sie die PDF-Seitengröße mit Aspose.HTML für Java an


Im heutigen digitalen Zeitalter steigt der Bedarf an der Generierung hochwertiger PDFs aus HTML-Inhalten. Aspose.HTML für Java ist eine leistungsstarke Java-Bibliothek, mit der Sie HTML-Dokumente mühelos in das PDF-Format konvertieren können. In diesem Tutorial konzentrieren wir uns auf die Anpassung der Seitengröße bei der Konvertierung von HTML in PDF mit Aspose.HTML für Java.

## Voraussetzungen

Stellen Sie zunächst sicher, dass die folgenden Voraussetzungen erfüllt sind:

- Java-Entwicklungsumgebung: Stellen Sie sicher, dass Java Development Kit (JDK) auf Ihrem System installiert ist.
-  Aspose.HTML für Java: Sie müssen Aspose.HTML für Java von der Website herunterladen und installieren[Hier](https://releases.aspose.com/html/java/).
- HTML-Dokument: Sie sollten ein HTML-Dokument zur Konvertierung bereit haben. Falls nicht, erstellen Sie eines oder verwenden Sie eine vorhandene HTML-Datei.

## Pakete importieren

Zu Beginn müssen Sie die erforderlichen Pakete importieren, um mit Aspose.HTML für Java arbeiten zu können. Der folgende Codeausschnitt zeigt, wie das geht:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

Nachdem Sie nun die Voraussetzungen geschaffen und die erforderlichen Pakete importiert haben, unterteilen wir den Vorgang zum Anpassen der PDF-Seitengröße in mehrere Schritte:

## Schritt 1: HTML-Inhalte lesen

Zuerst müssen Sie den HTML-Inhalt lesen, den Sie in PDF konvertieren möchten. In diesem Beispiel lesen wir das HTML aus einer Datei namens „FirstFile.html“.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## Schritt 2: HTML-Inhalte schreiben

Als Nächstes schreiben Sie den HTML-Inhalt in eine Datei mit dem Namen „FirstFileOut.html“.

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Fügen Sie hier benutzerdefinierte HTML-Stile oder Inhalte hinzu
    String style = "<style>\n" +
                   ".st\n" +
                   "{\n" +
                   "color:\n" +
                   "green;\n" +
                   "}\n" +
                   "</style >\n" +
                   "<div id = id1 > Aspose.Html rendering Text in Black Color</div >\n" +
                   "<div id = id2 class='' st '' > Aspose.Html rendering Text in Green Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: blue;' > Aspose.Html rendering Text in Blue Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: red;' ><font face = 'Arial' > Aspose.Html rendering Text in Red\n" +
                   "Color</font ></div >\n";
    fileOutputStream.write(style.getBytes(java.nio.charset.StandardCharsets.UTF_8));
}
```

## Schritt 3: HTML in PDF rendern

Jetzt rendern Sie den HTML-Inhalt in eine PDF-Datei. Wir werden zwei Szenarien behandeln: eines, bei dem die Seitengröße nicht an die Inhaltsbreite angepasst ist, und ein anderes, bei dem sie angepasst ist.

### Seitengröße nicht angepasst

In diesem Szenario ist die Seitengröße auf eine feste Breite und Höhe eingestellt, wodurch der Inhalt abgeschnitten werden kann, wenn er diese Abmessungen überschreitet.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Erstellen Sie eine HTMLDocument-Instanz aus der HTML-Datei
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Festlegen von PDF-Rendering-Optionen
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Rendern der Ausgabe
pdf_renderer.render(device, html_document);
```

### Seitengröße an Inhaltsbreite angepasst

In diesem Szenario wird die Seitengröße entsprechend der Inhaltsbreite angepasst.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Rendern der Ausgabe
pdf_renderer.render(device, html_document);
```

## Abschluss

In diesem Tutorial haben wir untersucht, wie Sie die PDF-Seitengröße anpassen, wenn Sie HTML mit Aspose.HTML für Java in PDF konvertieren. Sie haben die Voraussetzungen kennengelernt, die erforderlichen Pakete importiert und eine Schritt-für-Schritt-Anleitung befolgt, um diese Aufgabe zu erledigen. Mit Aspose.HTML für Java können Sie die Seitengröße Ihrer generierten PDFs problemlos steuern und sicherstellen, dass Ihr Inhalt wie beabsichtigt angezeigt wird.

 Experimentieren Sie mit verschiedenen Seitengrößen und Einstellungen, um Ihre spezifischen Anforderungen zu erfüllen. Wenn Sie auf Probleme stoßen oder weitere Fragen haben, wenden Sie sich bitte an den[Aspose.HTML für Java-Dokumentation](https://reference.aspose.com/html/java/) oder die[Aspose-Supportforum](https://forum.aspose.com/).

## Häufig gestellte Fragen

### F1: Was ist Aspose.HTML für Java?

A1: Aspose.HTML für Java ist eine Java-Bibliothek, mit der Sie mit HTML-Dokumenten arbeiten, diese bearbeiten, konvertieren und in verschiedene Formate, einschließlich PDF, rendern können.

### F2: Wie kann ich die PDF-Seitengröße anpassen, wenn ich HTML mit Aspose.HTML für Java in PDF konvertiere?

 A2: Sie können die PDF-Seitengröße anpassen, indem Sie`PageSetup` Klasse und Festlegen der`AdjustToWidestPage` Eigentum an`true` oder „false“, abhängig von Ihren Anforderungen.

### F3: Kann ich die Formatierung von HTML-Inhalten anpassen, bevor ich sie in PDF konvertiere?

A3: Ja, Sie können den Stil anpassen, indem Sie Ihrem HTML-Inhalt CSS- und HTML-Elemente hinzufügen, bevor Sie ihn in PDF konvertieren, wie im Tutorial gezeigt.

### F4: Wo finde ich die Dokumentation für Aspose.HTML für Java?

 A4: Sie können die Dokumentation zu Rate ziehen[Hier](https://reference.aspose.com/html/java/) für umfassende Informationen und Beispiele.

### F5: Gibt es eine kostenlose Testversion von Aspose.HTML für Java?

 A5: Ja, Sie können eine kostenlose Testversion von Aspose.HTML für Java von[dieser Link](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
