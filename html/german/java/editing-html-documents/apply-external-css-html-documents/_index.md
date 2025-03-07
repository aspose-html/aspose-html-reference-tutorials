---
title: Wenden Sie externes CSS auf HTML-Dokumente in Aspose.HTML für Java an
linktitle: Wenden Sie externes CSS auf HTML-Dokumente in Aspose.HTML für Java an
second_title: Java-HTML-Verarbeitung mit Aspose.HTML
description: Entdecken Sie, wie Sie mit Aspose.HTML für Java externes CSS auf HTML-Dokumente anwenden! Folgen Sie dieser Schritt-für-Schritt-Anleitung für ein vollständiges Tutorial.
weight: 12
url: /de/java/editing-html-documents/apply-external-css-html-documents/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wenden Sie externes CSS auf HTML-Dokumente in Aspose.HTML für Java an

## Einführung
Beim Arbeiten mit HTML-Dokumenten kann die Anwendung von Stilen die Präsentation und das Benutzererlebnis entscheidend beeinflussen. Wenn Sie sich mit Java beschäftigen und lernen möchten, wie Sie mithilfe der Aspose.HTML-Bibliothek externe CSS-Stile auf Ihre HTML-Dokumente anwenden, sind Sie hier richtig! Diese Anleitung soll den Prozess Schritt für Schritt erläutern und ihn auch für diejenigen leicht machen, die mit Java oder CSS noch nicht vertraut sind.
## Voraussetzungen
Bevor Sie sich in den Code vertiefen, müssen Sie einige Dinge vorbereitet haben:
### 1. Java Development Kit (JDK)
 Stellen Sie sicher, dass JDK auf Ihrem Computer installiert ist. Sie können die neueste Version von herunterladen[Die Java-Website von Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).
### 2. Aspose.HTML für Java
Sie müssen Aspose.HTML für Java eingerichtet haben. Wenn Sie dies noch nicht getan haben, gehen Sie zu[Aspose-Downloadseite](https://releases.aspose.com/html/java/) und schnapp dir die Bibliothek.
### 3. Eine IDE oder ein Texteditor
Wählen Sie eine integrierte Entwicklungsumgebung (IDE) wie IntelliJ IDEA, Eclipse oder sogar einen einfachen Texteditor, um Ihren Java-Code zu schreiben.
### 4. Grundkenntnisse in Java
Wenn Sie mit der Java-Programmierung und den CSS-Grundlagen vertraut sind, können Sie den Anweisungen sicherlich leichter folgen.
## Pakete importieren
Sobald Sie alles eingerichtet haben, besteht der nächste Schritt darin, die erforderlichen Pakete in Ihr Java-Projekt zu importieren. Folgendes benötigen Sie:
```java
import com.aspose.html.HTMLDocument;
```
Diese Importe ermöglichen Ihnen, HTML-Dokumente zu bearbeiten und in verschiedene Formate wie PDF umzuwandeln.

Wir unterteilen unser Tutorial in überschaubare Schritte. Jeder Schritt führt Sie durch den Prozess der Anwendung externer CSS-Stile auf ein HTML-Dokument mit Aspose.HTML für Java.
## Schritt 1: Erstellen Sie ein HTML-Dokument
Zuerst müssen wir unser HTML-Dokument erstellen. Wir beginnen damit, den Inhalt mit einer einfachen HTML-Struktur zu definieren.
```java
String content = "<div><p>Internal CSS</p><p>An internal CSS is used to define a style for a single HTML page</p></div>";
HTMLDocument document = new HTMLDocument(content, ".");
```

 Hier haben wir eine grundlegende HTML-Struktur definiert, einschließlich einer`<div>` mit zwei Absätzen. Die`HTMLDocument` Klasse wird verwendet, um eine Dokumentdarstellung unseres HTML-Inhalts zu erstellen.
## Schritt 2: Erstellen Sie ein Stilelement
 Als nächstes erstellen wir eine`style` Element zum Speichern unserer CSS-Regeln.
```java
Element style = document.createElement("style");
style.setTextContent(".frame1 { margin-top:50px; margin-left:50px; padding:20px; width:360px; height:90px; background-color:#a52a2a; font-family:verdana; color:#FFF5EE;} \n" +
        ".frame2 { margin-top:-90px; margin-left:160px; text-align:center; padding:20px; width:360px; height:100px; background-color:#ADD8E6;}");
```

 Mit dem`createElement` Methode der`HTMLDocument` , wir erstellen ein neues`<style>` Element und legen Sie seinen Inhalt so fest, dass er unsere CSS-Definitionen für zwei Klassen enthält:`frame1` Und`frame2`. Diese Klassen definieren Ränder, Polsterung, Abmessungen, Hintergrundfarben, Schriftfamilien und Textfarben.
## Schritt 3: Den Stil an den Dokumentkopf anhängen
Nachdem unser CSS nun an Ort und Stelle ist, müssen wir unser Stilelement an den Kopf des Dokuments anhängen.
```java
Element head = document.getElementsByTagName("head").get_Item(0);
head.appendChild(style);
```

 Wir holen uns den Kopf des Dokuments und hängen unseren neu erstellten`style` Element. Diese Aktion integriert unser CSS effektiv in das HTML-Dokument und ermöglicht die Formatierung unseres HTML-Inhalts.
## Schritt 4: Klassen auf HTML-Elemente anwenden
Als Nächstes wenden wir die zuvor definierten CSS-Klassen auf unsere Absatzelemente an.
```java
HTMLElement paragraph = (HTMLElement) document.getElementsByTagName("p").get_Item(0);
paragraph.setClassName("frame1");
HTMLElement lastParagraph = (HTMLElement) document.getElementsByTagName("p").get_Item(document.getElementsByTagName("p").getLength() - 1);
lastParagraph.setClassName("frame2");
```

Hier greifen wir auf die ersten und letzten Absatzelemente im Dokument zu und weisen ihnen die von uns erstellten CSS-Klassen zu. Diese Zuweisung stellt sicher, dass sie den in unserem CSS definierten Stilen entsprechen.
## Schritt 5: Zusätzliche Stileigenschaften festlegen
Um das Erscheinungsbild weiter zu verbessern, legen wir zusätzliche Stileigenschaften für unsere Absätze fest.
```java
paragraph.getStyle().setFontSize("250%");
paragraph.getStyle().setTextAlign("center");
lastParagraph.getStyle().setColor("#434343");
lastParagraph.getStyle().setFontSize("150%");
lastParagraph.getStyle().setFontFamily("verdana");
```

In diesem Schritt nehmen wir die Feinabstimmung unserer Stile vor. Die Schriftgröße des ersten Absatzes wird vergrößert und zentriert, während die Farbe, Schriftgröße und Schriftfamilie des letzten Absatzes definiert werden. Diese Verfeinerung ist für die Lesbarkeit und Ästhetik von entscheidender Bedeutung.
## Schritt 6: Speichern Sie das HTML-Dokument
Nachdem wir unsere Stile angewendet haben, ist es Zeit, das HTML-Dokument zu speichern.
```java
document.save("edit-internal-css.html");
```

 Hier nutzen wir die`save` Methode der`HTMLDocument` Klasse, um den geänderten HTML-Inhalt in eine Datei zu schreiben und so unsere Stile und Änderungen beizubehalten.
## Schritt 7: Das Dokument in PDF umwandeln
Lassen Sie uns das Dokument abschließend zur Ausgabe in ein PDF-Format rendern.
```java
PdfDevice device = new PdfDevice("edit-internal-css.pdf");
document.renderTo(device);
```

 Mit dem`PdfDevice` Klasse richten wir die Darstellung unseres HTML-Dokuments in ein PDF ein. Dieser Schritt ist entscheidend, wenn Sie das gestaltete Dokument in einem allgemein zugänglichen Format freigeben möchten.
## Abschluss
Und da haben Sie es – das Anwenden von externem CSS auf HTML-Dokumente mit Aspose.HTML für Java ist sowohl unkompliziert als auch lohnend! Mit nur wenigen Codezeilen können Sie einfachen Text in optisch ansprechende und professionell gestaltete Dokumente umwandeln. Egal, ob Sie für den persönlichen Gebrauch entwerfen, Berichte erstellen oder Webinhalte entwickeln, das Verständnis der Manipulation von HTML und CSS in Java ist eine wichtige Fähigkeit, die Sie in Ihrem Toolkit haben sollten.
## Häufig gestellte Fragen
### Was ist Aspose.HTML für Java?
Aspose.HTML für Java ist eine leistungsstarke Bibliothek, die Entwicklern die Arbeit mit HTML-Dokumenten in Java-Anwendungen ermöglicht und eine breite Palette an Funktionen bietet, von der HTML-Manipulation bis zum Rendering.
### Benötige ich eine Internetverbindung, um Aspose.HTML zu verwenden?
Nein, sobald Sie die erforderlichen Bibliotheksdateien heruntergeladen haben, können Sie Aspose.HTML offline verwenden.
### Kann ich mehrere CSS-Dateien auf ein HTML-Dokument anwenden?
 Ja, Sie können mehrere erstellen`<link>` Elemente und fügen Sie sie für verschiedene CSS-Dateien an den Kopf des Dokuments an.
### Gibt es einen Unterschied zwischen internem und externem CSS?
Ja! Internes CSS wird innerhalb eines HTML-Dokuments definiert, während externes CSS in einer separaten Datei platziert und mit dem Dokument verknüpft wird.
### Wie erhalte ich Support für Aspose.HTML für Java?
 Sie erhalten Zugriff auf den Community-Support über die[Aspose-Forum](https://forum.aspose.com/c/html/29) für alle Fragen oder Probleme, die auftreten können.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
