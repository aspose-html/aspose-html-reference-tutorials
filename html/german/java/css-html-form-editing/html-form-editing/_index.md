---
title: Bearbeiten und Senden von HTML-Formularen mit Aspose.HTML für Java
linktitle: Bearbeiten und Senden von HTML-Formularen mit Aspose.HTML für Java
second_title: Java-HTML-Verarbeitung mit Aspose.HTML
description: Erfahren Sie in dieser umfassenden Schritt-für-Schritt-Anleitung, wie Sie mit Aspose.HTML für Java programmgesteuert HTML-Formulare bearbeiten und übermitteln.
weight: 11
url: /de/java/css-html-form-editing/html-form-editing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bearbeiten und Senden von HTML-Formularen mit Aspose.HTML für Java

## Einführung
In der heutigen webbasierten Welt ist die Interaktion mit HTML-Formularen eine alltägliche Aufgabe für Entwickler, sei es das Ausfüllen, Senden oder Automatisieren der Dateneingabe. Aspose.HTML für Java bietet eine robuste Lösung für die programmgesteuerte Verwaltung von HTML-Formularen. Dieser Artikel führt Sie durch das Bearbeiten und Senden von HTML-Formularen mit Aspose.HTML für Java und enthält ein schrittweises Tutorial, das den Vorgang in überschaubare Teile aufteilt.
## Voraussetzungen
Bevor wir uns in die Schritt-für-Schritt-Anleitung stürzen, stellen wir sicher, dass Sie alles haben, was Sie brauchen, um den Schritten zu folgen:
1. Aspose.HTML für Java: Stellen Sie sicher, dass Sie Aspose.HTML für Java installiert haben. Sie können es von der[Download-Seite](https://releases.aspose.com/html/java/).
2. Java Development Kit (JDK): Stellen Sie sicher, dass JDK auf Ihrem System installiert ist. Aspose.HTML für Java erfordert JDK 1.6 oder höher.
3. Integrierte Entwicklungsumgebung (IDE): Verwenden Sie eine IDE wie IntelliJ IDEA, Eclipse oder eine andere Java-IDE, mit der Sie vertraut sind.
4.  Internetverbindung: Da wir mit einem Live-Webformular arbeiten, das gehostet wird bei`https://httpbin.org`, stellen Sie sicher, dass Ihr System mit dem Internet verbunden ist.
## Pakete importieren
Bevor Sie Code schreiben, müssen Sie die erforderlichen Pakete aus Aspose.HTML für Java in Ihr Projekt importieren. So können Sie das tun:
```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.forms.FormEditor;
import com.aspose.html.forms.InputElement;
import com.aspose.html.forms.TextAreaElement;
import com.aspose.html.forms.FormSubmitter;
import com.aspose.html.forms.SubmissionResult;
import com.aspose.html.dom.Document;
import java.util.Map;
import java.util.HashMap;
```
Diese Importe ermöglichen Ihnen das Erstellen und Bearbeiten von HTML-Dokumenten, das Arbeiten mit Formularen und die Abwicklung des Übermittlungsprozesses.
## Schritt-für-Schritt-Anleitung zum Bearbeiten und Senden von HTML-Formularen
In diesem Abschnitt unterteilen wir den Vorgang zum Bearbeiten und Senden von HTML-Formularen in klare, überschaubare Schritte. Jeder Schritt enthält Codeausschnitte und ausführliche Erklärungen, damit Sie ihn problemlos nachvollziehen können.
## Schritt 1: Laden Sie das HTML-Dokument
 Der erste Schritt besteht darin, das HTML-Dokument zu laden, das das zu bearbeitende Formular enthält. Wir verwenden das`HTMLDocument` Klasse, um dies zu tun.
```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("https://httpbin.org/forms/post");
```
Hier erstellen wir eine Instanz von`HTMLDocument` indem Sie die URL des HTML-Formulars übergeben. Dadurch wird das Formular in das`document` Objekt, das wir für weitere Manipulationen verwenden werden.
## Schritt 2: Erstellen Sie eine Instanz des Formular-Editors
 Sobald das Dokument geladen ist, besteht der nächste Schritt darin, eine`FormEditor` Instanz. Mit diesem Objekt können wir die Formularfelder bearbeiten.
```java
com.aspose.html.forms.FormEditor editor = com.aspose.html.forms.FormEditor.create(document, 0);
```
 Der`FormEditor.create()` Methode initialisiert den Formulareditor und verwendet das Dokument und einen Index als Parameter. Der Index`0` gibt an, dass wir mit dem ersten Formular im Dokument arbeiten.
## Schritt 3: Formularfelder ausfüllen
 Jetzt, da wir unsere`FormEditor`können wir mit dem Ausfüllen der Formularfelder beginnen. Beginnen wir mit dem Ausfüllen des Felds „custname“.
```java
com.aspose.html.forms.InputElement custname = editor.addInput("custname");
custname.setValue("John Doe");
```
 Wir verwenden die`addInput()`Methode, um das Eingabefeld anhand seines Namens („custname“) abzurufen. Dann setzen wir seinen Wert auf „John Doe“. Dieser Schritt ist wichtig, um Formularfelder vor dem Absenden vorab auszufüllen.
## Schritt 4: Textbereichsfelder bearbeiten
Formulare enthalten oft Textfelder für längere Eingaben, beispielsweise Kommentare. Füllen wir das Feld „Kommentare“ aus.
```java
com.aspose.html.forms.TextAreaElement comments = editor.getElement(com.aspose.html.forms.TextAreaElement.class, "comments");
comments.setValue("MORE CHEESE PLEASE!");
```
 Hier ermitteln wir das Textbereichselement mit dem`getElement()` Methode. Wir geben den Typ an (`TextAreaElement` ) und den Namen ("Kommentare"). Die`setValue()` Die Methode füllt dann den Textbereich mit dem gewünschten Text.
## Schritt 5: Führen Sie eine Massenoperation durch
Wenn Sie mehrere Felder ausfüllen müssen, kann es umständlich sein, dies einzeln zu tun. Sie können stattdessen eine Massenoperation ausführen.
```java
java.util.Map<String, String> dictionary = new java.util.HashMap<>();
dictionary.put("custemail", "john.doe@gmail.com");
dictionary.put("custtel", "+1202-555-0290");
```
 Wir erstellen ein Wörterbuch (ein`HashMap` in Java), um die Schlüssel-Wert-Paare zu speichern, wobei die Schlüssel die Feldnamen und die Werte die entsprechenden Daten sind. Dieser Ansatz ist effizient, wenn mehrere Felder verarbeitet werden.
## Schritt 6: Anwenden der Massendaten auf das Formular
Nachdem die Massendaten vorbereitet wurden, besteht der nächste Schritt darin, sie auf das Formular anzuwenden.
```java
for (Map.Entry<String, String> entry : dictionary.entrySet()) {
    editor.addInput(entry.getKey()).setValue(entry.getValue());
}
```
 Wir iterieren über die Einträge im Wörterbuch und verwenden`addInput()` um jedes Eingabefeld nach Namen zu finden, dann`setValue()` um es mit den entsprechenden Daten zu füllen. Diese Methode automatisiert den Formularausfüllvorgang für mehrere Felder.
## Schritt 7: Senden Sie das Formular
 Sobald alle Felder ausgefüllt sind, ist es an der Zeit, das Formular an den Server zu senden. Dies geschieht mit dem`FormSubmitter` Klasse.
```java
com.aspose.html.forms.FormSubmitter submitter = new com.aspose.html.forms.FormSubmitter(editor);
com.aspose.html.forms.SubmissionResult result = submitter.submit();
```
 Wir schaffen eine`FormSubmitter` Instanz und übergeben Sie die`editor` Einwände dagegen erheben. Die`submit()` Methode sendet die Formulardaten an den Server und gibt eine`SubmissionResult` Objekt, das die Antwort vom Server enthält.
## Schritt 8: Überprüfen Sie das Übermittlungsergebnis
Nach dem Absenden des Formulars ist es wichtig, zu überprüfen, ob die Übermittlung erfolgreich war, und die Antwort entsprechend zu verarbeiten.
```java
if (result.isSuccess()) {
    if (result.getResponseMessage().getHeaders().getContentType().getMediaType().equals("application/json")) {
        System.out.println(result.getContent().readAsString());
    } else {
        com.aspose.html.dom.Document doc = result.loadDocument();
        // Überprüfen Sie hier das HTML-Dokument.
    }
}
```
 Der`isSuccess()`Methode prüft, ob das Formular erfolgreich übermittelt wurde. Wenn die Antwort im JSON-Format vorliegt, drucken wir sie aus; andernfalls laden wir die Antwort als HTML-Dokument zur weiteren Überprüfung.
## Schritt 9: Speichern Sie das geänderte HTML-Dokument
Abschließend möchten Sie das geänderte HTML-Dokument möglicherweise lokal speichern, um später darauf zurückgreifen zu können.
```java
document.save("output/out.html");
```
 Der`save()` Methode speichert den aktuellen Zustand der`HTMLDocument` in einen angegebenen Dateipfad. Dieser Schritt stellt sicher, dass alle am Formular vorgenommenen Änderungen erhalten bleiben.
## Abschluss
Das programmgesteuerte Bearbeiten und Senden von HTML-Formularen mit Aspose.HTML für Java ist eine leistungsstarke Möglichkeit, Webinteraktionen zu automatisieren. Egal, ob Sie Formulare vorab ausfüllen, Benutzereingaben verarbeiten oder Daten an einen Server senden, Aspose.HTML für Java bietet alle Tools, die Sie benötigen, um diese Aufgaben unkompliziert und effizient zu erledigen. Wenn Sie die in diesem Tutorial beschriebenen Schritte befolgen, sollten Sie in der Lage sein, HTML-Formulare nahtlos in Ihren Java-Anwendungen zu verwalten.
## Häufig gestellte Fragen
### Was ist Aspose.HTML für Java?
Aspose.HTML für Java ist eine Bibliothek, die es Entwicklern ermöglicht, mit HTML-Dokumenten in Java-Anwendungen zu arbeiten. Sie bietet Funktionen wie das Bearbeiten von HTML, das Verwalten von Formularen und das Konvertieren zwischen verschiedenen Formaten.
### Kann ich mit Aspose.HTML für Java Formulare in einer lokalen HTML-Datei bearbeiten?
 Ja, Sie können lokale HTML-Dateien laden mit`HTMLDocument` und bearbeiten Sie dann die Formulare in diesen Dateien genau so, wie Sie es mit Online-Dokumenten tun würden.
### Wie gehe ich mit Formulareinsendungen um, die eine Authentifizierung erfordern?
 Sie können die`FormSubmitter` -Objekt, um Benutzeranmeldeinformationen einzuschließen und Sitzungen zu verwalten, sodass Sie Formulare übermitteln können, die eine Authentifizierung erfordern.
### Ist es möglich, Formulare mit Aspose.HTML für Java asynchron zu übermitteln?
Derzeit sind Formularübermittlungen synchron. Sie können jedoch asynchrone Vorgänge in Ihrer Java-Anwendung verwalten, indem Sie die Übermittlung in einem separaten Thread ausführen.
### Was passiert, wenn das Absenden des Formulars fehlschlägt?
 Wenn die Übermittlung fehlschlägt,`SubmissionResult`Objekt wird nicht als erfolgreich markiert und Sie können Fehler behandeln, indem Sie die Antwortnachricht oder die Ausnahmedetails überprüfen.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
