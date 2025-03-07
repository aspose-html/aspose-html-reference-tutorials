---
title: Passen Sie die XPS-Seitengröße mit Aspose.HTML für Java an
linktitle: Anpassen der XPS-Seitengröße
second_title: Java-HTML-Verarbeitung mit Aspose.HTML
description: Erfahren Sie, wie Sie die XPS-Seitengröße mit Aspose.HTML für Java anpassen. Steuern Sie die Ausgabeabmessungen Ihrer XPS-Dokumente ganz einfach.
weight: 16
url: /de/java/advanced-usage/adjust-xps-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Passen Sie die XPS-Seitengröße mit Aspose.HTML für Java an


In diesem Tutorial führen wir Sie durch den Prozess der Anpassung der XPS-Seitengröße mit Aspose.HTML für Java. Mit dieser leistungsstarken Bibliothek können Sie HTML-Dokumente bearbeiten und in verschiedene Formate, einschließlich XPS, rendern. Das Anpassen der Seitengröße ist wichtig, wenn Sie die Ausgabeabmessungen Ihres XPS-Dokuments steuern müssen.

## Voraussetzungen

Bevor wir beginnen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

1. Java-Entwicklungsumgebung: Stellen Sie sicher, dass Java Development Kit (JDK) auf Ihrem System installiert ist.

2.  Aspose.HTML für Java-Bibliothek: Sie müssen die Aspose.HTML für Java-Bibliothek herunterladen und in Ihr Java-Projekt einbinden. Sie finden die Bibliothek[Hier](https://releases.aspose.com/html/java/).

3. HTML-Eingabedatei: Bereiten Sie eine HTML-Datei vor, die Sie rendern möchten, und passen Sie die XPS-Seitengröße dafür an. Sie können für dieses Tutorial Ihre eigene HTML-Datei verwenden.

## Pakete importieren

Zuerst müssen Sie die erforderlichen Pakete importieren, um mit Aspose.HTML für Java arbeiten zu können. Fügen Sie diese Pakete am Anfang Ihrer Java-Klasse ein:

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Schritt 1: Legen Sie den Namen der Eingabedatei fest

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

 In diesem Schritt lesen wir Ihre HTML-Eingabedatei mit einem`FileInputStream`.

## Schritt 2: Erstellen Sie ein HTML-Dokument und legen Sie Stile fest

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n";

// ...
```

 Dieser Schritt umfasst die Erstellung eines`HTMLDocument` und Stile hinzufügen.

## Schritt 3: XPS-Rendering-Optionen erstellen

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

Hier erstellen wir XPS-Rendering-Optionen, um den Rendering-Prozess zu konfigurieren.

## Schritt 4: Passen Sie die Seitengröße an

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

In diesem Schritt legen Sie die Seitengröße fest und geben an, ob diese an die breiteste Seite angepasst werden soll.

## Schritt 5: Rendern der Ausgabe

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

Im letzten Schritt rendern wir die XPS-Ausgabe mit den konfigurierten Optionen.

## Abschluss

In diesem Tutorial haben wir Ihnen gezeigt, wie Sie die XPS-Seitengröße mit Aspose.HTML für Java anpassen. Sie können die Ausgabeabmessungen Ihrer XPS-Dokumente steuern und sicherstellen, dass sie Ihren spezifischen Anforderungen entsprechen. Mit dem bereitgestellten Code und den Schritten können Sie diese Funktion problemlos in Ihre Java-Anwendungen implementieren.

 Wenn Sie Fragen haben oder weitere Hilfe benötigen, besuchen Sie bitte die[Aspose.HTML für Java-Dokumentation](https://reference.aspose.com/html/java/) oder bitten Sie um Hilfe auf der[Aspose Forum](https://forum.aspose.com/).

## Häufig gestellte Fragen

### F1: Was ist Aspose.HTML für Java?

A1: Aspose.HTML für Java ist eine Java-Bibliothek, mit der Entwickler HTML-Dokumente bearbeiten und in verschiedene Formate wie XPS, PDF und Bilder konvertieren können.

### F2: Wo kann ich Aspose.HTML für Java herunterladen?

 A2: Sie können die Aspose.HTML für Java-Bibliothek herunterladen von[dieser Link](https://releases.aspose.com/html/java/).

### F3: Gibt es eine kostenlose Testversion von Aspose.HTML für Java?

 A3: Ja, Sie können eine kostenlose Testversion von Aspose.HTML für Java erhalten von[Hier](https://releases.aspose.com/).

### F4: Wie kann ich eine temporäre Lizenz für Aspose.HTML für Java erhalten?

 A4: Um eine temporäre Lizenz für Aspose.HTML für Java zu erhalten, besuchen Sie[diese Seite](https://purchase.aspose.com/temporary-license/).

### F5: Kann ich Support für Aspose.HTML für Java erhalten?

 A5: Ja, Sie können Hilfe und Unterstützung von der Aspose-Community erhalten auf der[Aspose Forum](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
