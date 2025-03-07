---
title: Passen Sie HTML-Seitenränder mit Aspose.HTML an
linktitle: CSS-Erweiterungen - Hinzufügen von Titel und Seitenzahl
second_title: Java-HTML-Verarbeitung mit Aspose.HTML
description: Erfahren Sie, wie Sie mit Aspose.HTML für Java Seitenränder anpassen und Seitenzahlen und Titel zu HTML-Dokumenten hinzufügen.
weight: 10
url: /de/java/advanced-usage/css-extensions-adding-title-page-number/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Passen Sie HTML-Seitenränder mit Aspose.HTML an

Aspose.HTML für Java ist eine leistungsstarke Bibliothek zur Verarbeitung von HTML-Dokumenten in Java-Anwendungen. In diesem Tutorial erfahren Sie, wie Sie mit Aspose.HTML für Java benutzerdefinierte Seitenränder erstellen und Seitenzahlen und Titel zu Ihren HTML-Dokumenten hinzufügen. Diese Schritt-für-Schritt-Anleitung unterteilt den Prozess in überschaubare Schritte, damit Sie diese Funktionen problemlos in Ihre HTML-Dokumente integrieren können.

## Voraussetzungen

Bevor wir beginnen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

1. Java-Entwicklungsumgebung: Stellen Sie sicher, dass auf Ihrem Computer eine Java-Entwicklungsumgebung eingerichtet ist.

2.  Aspose.HTML für Java: Laden Sie die Aspose.HTML für Java-Bibliothek herunter und installieren Sie sie von[Hier](https://releases.aspose.com/html/java/).

## Pakete importieren

Um zu beginnen, müssen Sie die erforderlichen Pakete aus Aspose.HTML für Java importieren. Fügen Sie Ihrem Java-Code die folgenden Importanweisungen hinzu:

```java
// Aspose.HTML-Pakete importieren
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

Lassen Sie uns nun den Vorgang des Hinzufügens benutzerdefinierter Seitenränder, Seitenzahlen und Titel in überschaubare Schritte aufteilen:

## Schritt 1: Konfiguration und Seitenränder initialisieren

```java
// Konfigurationsobjekt initialisieren und Seitenränder für das Dokument einrichten
Configuration configuration = new Configuration();
try {
    // Abrufen des User-Agent-Dienstes
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Legen Sie den Stil der benutzerdefinierten Ränder fest und erstellen Sie Markierungen darauf
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

In diesem Schritt initialisieren wir das Konfigurationsobjekt und richten benutzerdefinierte Seitenränder ein, einschließlich der Position des Seitenzählers und des Seitentitels.

## Schritt 2: Initialisieren eines HTML-Dokuments

```java
// Initialisieren eines HTML-Dokuments
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Hier erstellen wir ein HTML-Dokument mit einem Beispielinhalt (in diesem Fall eine „Hallo Welt“-Nachricht) und wenden die Konfiguration aus Schritt 1 an.

## Schritt 3: Initialisieren Sie ein Ausgabegerät und rendern Sie das Dokument

```java
// Initialisieren eines Ausgabegeräts
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    //Senden Sie das Dokument an das Ausgabegerät
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

In diesem Schritt richten wir ein Ausgabegerät ein und rendern das HTML-Dokument. Das Dokument wird verarbeitet und als XPS-Datei mit den angegebenen Seitenrändern, Seitenzahlen und dem Titel gespeichert.

## Abschluss

Herzlichen Glückwunsch! Sie haben erfolgreich gelernt, wie Sie mit Aspose.HTML für Java benutzerdefinierte Seitenränder erstellen und Ihren HTML-Dokumenten Seitenzahlen und Titel hinzufügen. Mit dieser Anpassung können Sie professionellere und optisch ansprechendere Dokumente erstellen.

 Wenn Sie Fragen haben oder auf Probleme stoßen, besuchen Sie bitte die[Aspose.HTML für Java-Dokumentation](https://reference.aspose.com/html/java/) oder suchen Sie Hilfe auf der[Aspose-Supportforum](https://forum.aspose.com/).

## Häufig gestellte Fragen

### F1: Was ist Aspose.HTML für Java?

A1: Aspose.HTML für Java ist eine Java-Bibliothek, die leistungsstarke Tools für die Arbeit mit HTML-Dokumenten in Java-Anwendungen bereitstellt.

### F2: Kann ich die Seitenränder weiter anpassen?

A2: Ja, Sie können die CSS-Stile in Schritt 1 ändern, um die Seitenränder Ihren Anforderungen entsprechend anzupassen.

### F3: Wie kann ich dem HTML-Dokument mehr Inhalt hinzufügen?

A3: Sie können den HTML-Inhalt in Schritt 2 ändern, indem Sie den Beispielinhalt durch Ihren eigenen ersetzen.

### F4: Ist Aspose.HTML für Java mit anderen Dokumentformaten kompatibel?

A4: Ja, Aspose.HTML für Java kann zum Konvertieren von HTML-Dokumenten in verschiedene Formate verwendet werden, darunter PDF, XPS und Bilder.

### F5: Benötige ich eine Lizenz, um Aspose.HTML für Java zu verwenden?

 A5: Ja, Sie können eine Lizenz oder eine kostenlose Testversion erhalten von[Hier](https://purchase.aspose.com/buy) oder[Hier](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
