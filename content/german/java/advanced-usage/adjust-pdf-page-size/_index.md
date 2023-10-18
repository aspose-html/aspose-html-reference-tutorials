---
title: Passen Sie die PDF-Seitengröße mit Aspose.HTML für Java an
linktitle: Anpassen der PDF-Seitengröße
second_title: Java HTML-Verarbeitung mit Aspose.HTML
description: Erfahren Sie, wie Sie die PDF-Seitengröße mit Aspose.HTML für Java anpassen. Erstellen Sie mühelos hochwertige PDFs aus HTML. Steuern Sie die Seitenabmessungen effektiv.
type: docs
weight: 15
url: /de/java/advanced-usage/adjust-pdf-page-size/
---

Im heutigen digitalen Zeitalter steigt der Bedarf an der Generierung hochwertiger PDFs aus HTML-Inhalten. Aspose.HTML für Java ist eine leistungsstarke Java-Bibliothek, mit der Sie HTML-Dokumente mühelos in das PDF-Format konvertieren können. In diesem Tutorial konzentrieren wir uns auf die Anpassung der Seitengröße beim Konvertieren von HTML in PDF mit Aspose.HTML für Java.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

- Java-Entwicklungsumgebung: Stellen Sie sicher, dass auf Ihrem System das Java Development Kit (JDK) installiert ist.
-  Aspose.HTML für Java: Sie müssen Aspose.HTML für Java von der Website herunterladen und installieren[Hier](https://releases.aspose.com/html/java/).
- HTML-Dokument: Sie sollten ein HTML-Dokument zur Konvertierung bereit haben. Wenn nicht, erstellen Sie eine oder verwenden Sie eine vorhandene HTML-Datei.

## Pakete importieren

Zunächst müssen Sie die erforderlichen Pakete importieren, um mit Aspose.HTML für Java zu arbeiten. Der folgende Codeausschnitt zeigt, wie das geht:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

Nachdem Sie nun die Voraussetzungen geschaffen und die erforderlichen Pakete importiert haben, unterteilen wir den Prozess der Anpassung der PDF-Seitengröße in mehrere Schritte:

## Schritt 1: HTML-Inhalt lesen

Zuerst müssen Sie den HTML-Inhalt lesen, den Sie in PDF konvertieren möchten. In diesem Beispiel lesen wir den HTML-Code aus einer Datei namens „FirstFile.html“.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## Schritt 2: HTML-Inhalt schreiben

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

Jetzt rendern Sie den HTML-Inhalt in eine PDF-Datei. Wir werden zwei Szenarien behandeln: eines, bei dem die Seitengröße nicht an die Breite des Inhalts angepasst wird, und ein anderes, bei dem sie angepasst wird.

### Seitengröße nicht angepasst

In diesem Szenario ist die Seitengröße auf eine feste Breite und Höhe eingestellt, wodurch der Inhalt möglicherweise abgeschnitten wird, wenn er diese Abmessungen überschreitet.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Erstellen Sie eine HTMLDocument-Instanz aus der HTML-Datei
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Legen Sie PDF-Renderingoptionen fest
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Rendern Sie die Ausgabe
pdf_renderer.render(device, html_document);
```

### Seitengröße an die Breite des Inhalts angepasst

In diesem Szenario wird die Seitengröße entsprechend der Inhaltsbreite angepasst.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Rendern Sie die Ausgabe
pdf_renderer.render(device, html_document);
```

## Abschluss

In diesem Tutorial haben wir untersucht, wie Sie die PDF-Seitengröße anpassen, wenn Sie HTML in PDF mit Aspose.HTML für Java konvertieren. Sie haben die Voraussetzungen kennengelernt, die erforderlichen Pakete importiert und eine Schritt-für-Schritt-Anleitung befolgt, um diese Aufgabe zu erfüllen. Mit Aspose.HTML für Java können Sie die Seitengröße Ihrer generierten PDFs einfach steuern und so sicherstellen, dass Ihre Inhalte wie beabsichtigt angezeigt werden.

 Experimentieren Sie ruhig mit verschiedenen Seitengrößen und -einstellungen, um Ihren spezifischen Anforderungen gerecht zu werden. Wenn Sie auf Probleme stoßen oder weitere Fragen haben, wenden Sie sich bitte an die[Aspose.HTML für Java-Dokumentation](https://reference.aspose.com/html/java/) oder der[Aspose-Supportforum](https://forum.aspose.com/).

## FAQs

### F1: Was ist Aspose.HTML für Java?

A1: Aspose.HTML für Java ist eine Java-Bibliothek, mit der Sie mit HTML-Dokumenten arbeiten, diese bearbeiten, konvertieren und in verschiedene Formate, einschließlich PDF, rendern können.

### F2: Wie kann ich die PDF-Seitengröße anpassen, wenn ich HTML mit Aspose.HTML für Java in PDF konvertiere?

 A2: Sie können die PDF-Seitengröße mithilfe von anpassen`PageSetup` Klasse und Einstellung der`AdjustToWidestPage` Eigentum zu`true` oder „false“, je nach Ihren Anforderungen.

### F3: Kann ich den Stil von HTML-Inhalten anpassen, bevor ich ihn in PDF konvertiere?

A3: Ja, Sie können den Stil anpassen, indem Sie CSS- und HTML-Elemente zu Ihrem HTML-Inhalt hinzufügen, bevor Sie ihn in PDF konvertieren, wie im Tutorial gezeigt.

### F4: Wo finde ich die Dokumentation für Aspose.HTML für Java?

 A4: Sie können sich auf die Dokumentation beziehen[Hier](https://reference.aspose.com/html/java/) Ausführliche Informationen und Beispiele finden Sie hier.

### F5: Gibt es eine kostenlose Testversion für Aspose.HTML für Java?

 A5: Ja, Sie können auf eine kostenlose Testversion von Aspose.HTML für Java zugreifen[dieser Link](https://releases.aspose.com/).