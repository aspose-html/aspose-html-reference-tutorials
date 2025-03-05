---
title: Implementieren Sie internes CSS in HTML-Dokumenten mit Aspose.HTML für Java
linktitle: Implementieren Sie internes CSS in HTML-Dokumenten mit Aspose.HTML für Java
second_title: Java-HTML-Verarbeitung mit Aspose.HTML
description: Lernen Sie mit unserem einfachen Schritt-für-Schritt-Tutorial, mit Aspose.HTML für Java internes CSS in HTML-Dokumenten zu implementieren.
type: docs
weight: 16
url: /de/java/editing-html-documents/implement-internal-css-html-documents/
---
## Einführung
Beim Erstellen schöner und gut strukturierter Webseiten kommt es oft auf ein entscheidendes Element an: das Styling. In der Webentwicklung ist CSS (Cascading Style Sheets) wie das Dressing für Ihr HTML – es lässt alles ansprechend und organisiert aussehen. Heute tauchen wir ein in die Integration von internem CSS in HTML-Dokumente mit Aspose.HTML für Java. Egal, ob Sie Anfänger oder erfahrener Entwickler sind, dieses Tutorial erklärt Ihnen die Schritte auf einfache und ansprechende Weise.
## Voraussetzungen
Bevor wir direkt loslegen, stellen wir sicher, dass Sie alles haben, was Sie brauchen, um diesem Tutorial zu folgen. Hier sind die Voraussetzungen:
1.  Java Development Kit (JDK): Stellen Sie sicher, dass JDK auf Ihrem Rechner installiert ist. Sie können es von der[Oracle-Website](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html) oder[OpenJDK](https://openjdk.java.net/).
2.  Aspose.HTML für Java-Bibliothek: Sie benötigen die Aspose.HTML-Bibliothek, um HTML-Dokumente einfach verwalten und bearbeiten zu können. Sie können die Bibliothek von der[Aspose-Website](https://releases.aspose.com/html/java/).
3. Integrierte Entwicklungsumgebung (IDE): Eine gute IDE wie IntelliJ IDEA oder Eclipse kann das Codieren wesentlich reibungsloser machen.
4. Grundkenntnisse in Java: Dieses Tutorial setzt voraus, dass Sie über gewisse Kenntnisse in der Java-Programmierung verfügen.
5. Zeit und Geduld: Dieser Vorgang ist zwar unkompliziert, der Schlüssel liegt jedoch darin, ihn Schritt für Schritt durchzuführen.
## Pakete importieren
Bevor wir mit der Codierung beginnen, importieren wir die erforderlichen Pakete, um sicherzustellen, dass unser Programm Zugriff auf die von Aspose.HTML bereitgestellten Funktionen hat.
```java
import java.io.IOException;
```
Stellen Sie sicher, dass Sie diese Importanweisungen am Anfang Ihrer Java-Datei hinzufügen. Dadurch können wir die Klassen verwenden, die zum Erstellen und Bearbeiten des HTML-Dokuments und zum Rendern als PDF erforderlich sind.
Lassen Sie uns den Vorgang in einzelne Schritte unterteilen, damit Sie ihn leicht nachvollziehen können.
## Schritt 1: Erstellen Sie eine Instanz eines HTML-Dokuments
Zuerst müssen wir eine Instanz des HTML-Dokuments erstellen. So geht's:
```java
String content = "<div><p>Internal CSS</p><p>An internal CSS is used to define a style for a single HTML page</p></div>";
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument(content, ".");
```
 Hier definieren wir eine einfache HTML-Struktur mit zwei Absätzen innerhalb eines`div` . Der`HTMLDocument` Instanz initialisiert diese Struktur, bereit zur Änderung und Formatierung.
## Schritt 2: Erstellen und Hinzufügen des Stilelements
Als Nächstes erstellen wir unsere internen CSS-Stile. Hier beginnt die Magie des Stylings!
```java
com.aspose.html.dom.Element style = document.createElement("style");
style.setTextContent(".frame1 { margin-top:50px; margin-left:50px; padding:20px; width:360px; height:90px; background-color:#a52a2a; font-family:verdana; color:#FFF5EE;}" +
                      ".frame2 { margin-top:-90px; margin-left:160px; text-align:center; padding:20px; width:360px; height:100px; background-color:#ADD8E6;}");
```
 In diesem Schritt erstellen wir eine`<style>` Element und Definieren von zwei CSS-Klassen—`frame1` Und`frame2`. Jede Klasse hat spezifische Stile für Ränder, Polsterung, Hintergrundfarbe und Schrifteigenschaften. Hier nimmt unser internes CSS langsam Gestalt an.
## Schritt 3: Anhängen des Style-Elements an den Dokumentkopf
Nachdem wir nun unsere Stile erstellt haben, müssen wir sie an die Kopfzeile des Dokuments anhängen.
```java
com.aspose.html.dom.Element head = document.getElementsByTagName("head").get_Item(0);
head.appendChild(style);
```
 Dieser Codeausschnitt lokalisiert die`head` des Dokuments und fügt unsere`<style>` Element hinzufügen. Dies verbindet unsere CSS-Stile mit dem HTML-Inhalt unten.
## Schritt 4: CSS-Klassen HTML-Elementen zuweisen
Als Nächstes wenden wir unsere definierten Stile auf die Absatzelemente in unserem Dokument an.
```java
com.aspose.html.HTMLElement paragraph = (com.aspose.html.HTMLElement) document.getElementsByTagName("p").get_Item(0);
paragraph.setClassName("frame1");
HTMLElement lastParagraph = (HTMLElement) document.getElementsByTagName("p").get_Item(document.getElementsByTagName("p").getLength() - 1);
lastParagraph.setClassName("frame2");
```
 Hier holen wir uns die Absatzelemente und setzen ihre Klassennamen auf`frame1` Und`frame2`. Jetzt erben unsere Absätze die Stile, die wir gerade definiert haben!
## Schritt 5: Stileigenschaften anpassen
Lassen Sie uns die visuelle Darstellung weiter verbessern, indem Sie die Stileigenschaften unserer Absätze anpassen.
```java
paragraph.getStyle().setFontSize("250%");
paragraph.getStyle().setTextAlign("center");
lastParagraph.getStyle().setColor("#434343");
lastParagraph.getStyle().setFontSize("150%");
lastParagraph.getStyle().setFontFamily("verdana");
```
In diesem Schritt ändern wir die Schriftgröße und Ausrichtung des ersten Absatzes und passen die Farbe und Schriftart des zweiten Absatzes an. Diese Anpassung verleiht Ihrem Dokument Persönlichkeit und Klarheit.
## Schritt 6: Speichern Sie das HTML-Dokument
Nachdem wir nun unser internes CSS fertiggestellt und unsere Änderungen vorgenommen haben, ist es an der Zeit, das Dokument in einer Datei zu speichern.
```java
document.save("edit-internal-css.html");
```
 Der`save` Methode speichert unser Dokument in einer HTML-Datei namens`edit-internal-css.html`. Sie können diese Datei in jedem Webbrowser öffnen, um Ihre Änderungen in Aktion zu sehen!
## Schritt 7: Rendern Sie das HTML-Dokument in PDF
Als letzten Schritt rendern wir unser formatiertes HTML-Dokument in ein PDF-Format. Dies ist besonders nützlich, um Ihren formatierten Inhalt zu teilen oder auszudrucken.
```java
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice("edit-internal-css.pdf");
document.renderTo(device);
```
 Hier erstellen wir eine`PdfDevice` Instanz, die auf unsere gewünschte Ausgabedatei verweist. Die`renderTo` Die Methode konvertiert dann das HTML-Dokument in ein PDF. Wie cool ist das denn?
## Abschluss
Und da haben Sie es! Sie wissen jetzt, wie Sie mit Aspose.HTML für Java internes CSS in HTML-Dokumenten implementieren. In diesem Tutorial haben Sie nicht nur gelernt, wie Sie HTML formatieren, sondern auch, wie Sie es als PDF speichern und rendern. Mit diesen Tools können Sie Ihren Webseiten Stil und Professionalität verleihen. Worauf also warten? Tauchen Sie ein und probieren Sie die Formatierungsoptionen aus!

## Häufig gestellte Fragen
### Was ist der Vorteil der Verwendung von internem CSS?  
Mit internem CSS können Sie ein einzelnes HTML-Dokument formatieren, ohne andere zu beeinflussen. Dies macht es perfekt für einzigartige Designs.
### Kann Aspose.HTML externe CSS-Dateien verarbeiten?  
Ja, Aspose.HTML kann externe CSS-Dateien verarbeiten; Sie können sie ähnlich wie interne Stile verknüpfen.
### Ist Aspose.HTML Open Source?  
Nein, Aspose.HTML ist eine kommerzielle Bibliothek, aber Sie können mit einer kostenlosen Testversion beginnen, um ihre Funktionen zu erkunden.
### Wie kann ich den Support kontaktieren, wenn ich auf Probleme stoße?  
 Besuchen Sie die[Aspose-Supportforum](https://forum.aspose.com/c/html/29) um Hilfe.
### Gibt es beim Rendern von HTML in PDF Leistungsaspekte?  
Ja, das Rendern komplexer HTML-Dokumente kann länger dauern. Durch die Optimierung des Inhalts kann die Leistung verbessert werden.