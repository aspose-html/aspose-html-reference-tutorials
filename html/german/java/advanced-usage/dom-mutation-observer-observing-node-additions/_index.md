---
title: DOM Mutation Observer mit Aspose.HTML für Java
linktitle: DOM Mutation Observer - Beobachten von Knotenerweiterungen
second_title: Java-HTML-Verarbeitung mit Aspose.HTML
description: Erfahren Sie in dieser Schritt-für-Schritt-Anleitung, wie Sie mit Aspose.HTML für Java einen DOM Mutation Observer implementieren. Überwachen Sie DOM-Änderungen und reagieren Sie effektiv darauf.
type: docs
weight: 11
url: /de/java/advanced-usage/dom-mutation-observer-observing-node-additions/
---

Sind Sie ein Java-Entwickler, der Änderungen im Document Object Model (DOM) eines HTML-Dokuments beobachten und darauf reagieren möchte? Aspose.HTML für Java bietet eine leistungsstarke Lösung für diese Aufgabe. In dieser Schritt-für-Schritt-Anleitung erfahren Sie, wie Sie mit Aspose.HTML für Java ein HTML-Dokument erstellen und Knotenzusätze mit einem Mutation Observer beobachten. Dieses Tutorial führt Sie durch den Prozess und unterteilt jedes Beispiel in mehrere Schritte. Am Ende können Sie DOM Mutation Observer problemlos in Ihre Java-Projekte implementieren.

## Voraussetzungen

Bevor wir uns mit der Verwendung von Aspose.HTML für Java befassen, stellen wir sicher, dass die erforderlichen Voraussetzungen erfüllt sind:

1. Java-Entwicklungsumgebung: Stellen Sie sicher, dass auf Ihrem System das Java Development Kit (JDK) installiert ist.

2.  Aspose.HTML für Java: Sie müssen Aspose.HTML für Java herunterladen und installieren. Den Download-Link finden Sie[Hier](https://releases.aspose.com/html/java/).

3. IDE (Integrated Development Environment): Verwenden Sie zum Schreiben und Ausführen von Java-Code Ihre bevorzugte Java-IDE, beispielsweise IntelliJ IDEA oder Eclipse.

## Pakete importieren

Um mit Aspose.HTML für Java zu beginnen, müssen Sie die erforderlichen Pakete in Ihren Java-Code importieren. So können Sie das tun:

```java
// Importieren Sie die erforderlichen Pakete
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.mutations.MutationObserver;
import com.aspose.html.dom.mutations.MutationCallback;
import com.aspose.html.dom.mutations.MutationRecord;
import com.aspose.html.dom.mutations.MutationObserverInit;
import com.aspose.html.dom.Element;
import com.aspose.html.dom.Text;
import com.aspose.html.generic.IGenericList;

// Erstellen Sie ein leeres HTML-Dokument
HTMLDocument document = new HTMLDocument();
```

Nachdem Sie nun die erforderlichen Pakete importiert haben, fahren wir mit der Schritt-für-Schritt-Anleitung zur Implementierung eines DOM Mutation Observers in Java fort.

## Schritt 1: Erstellen Sie eine Mutation Observer-Instanz

Zuerst müssen Sie eine Mutation Observer-Instanz erstellen. Dieser Beobachter überwacht Änderungen im DOM und führt eine Rückruffunktion aus, wenn Mutationen auftreten.

```java
MutationObserver observer = new MutationObserver(new MutationCallback() {
    @Override
    public void invoke(IGenericList<MutationRecord> mutations, MutationObserver mutationObserver) {
        mutations.forEach(mutationRecord -> {
            mutationRecord.getAddedNodes().forEach(node -> {
                synchronized (this) {
                    System.out.println("The '" + node + "' node was added to the document.");
                    notifyAll();
                }
            });
        });
    }
});
```

In diesem Schritt erstellen wir einen Beobachter mit einer Rückruffunktion, die eine Meldung ausgibt, wenn Knoten zum DOM hinzugefügt werden.

## Schritt 2: Konfigurieren Sie den Observer

Konfigurieren wir nun den Beobachter mit den gewünschten Optionen. Wir möchten Änderungen an untergeordneten Listen und Teilbäumen sowie Änderungen an Zeichendaten beobachten.

```java
MutationObserverInit config = new MutationObserverInit();
config.setChildList(true);
config.setSubtree(true);
config.setCharacterData(true);

// Übergeben Sie den zu beobachtenden Zielknoten mit der angegebenen Konfiguration
observer.observe(document.getBody(), config);
```

 Hier setzen wir die`config` Objekt, um Änderungen an untergeordneten Listen, Teilbäumen und Zeichendaten beobachten zu können. Anschließend übergeben wir den Zielknoten (in diesem Fall den des Dokuments)`<body>`) und die Konfiguration an den Beobachter.

## Schritt 3: Ändern des DOM

Jetzt nehmen wir einige Änderungen am DOM vor, um den Beobachter auszulösen. Wir erstellen ein Absatzelement und hängen es an den Hauptteil des Dokuments an.

```java
// Erstellen Sie ein Absatzelement und hängen Sie es an den Dokumenttext an.
Element p = document.createElement("p");
document.getBody().appendChild(p);

// Erstellen Sie einen Text und hängen Sie ihn an den Absatz an
Text text = document.createTextNode("Hello World");
p.appendChild(text);
```

In diesem Schritt erstellen wir ein HTML-Absatzelement und fügen es dem Textkörper des Dokuments hinzu. Anschließend erstellen wir einen Textknoten mit dem Inhalt „Hallo Welt“ und hängen ihn an den Absatz an.

## Schritt 4: Auf Beobachtungen warten (asynchron)

Da Mutationen asynchron beobachtet werden, müssen wir einen Moment warten, damit der Beobachter die Änderungen erfassen kann. Wir verwenden`synchronized` Und`wait` zu diesem Zweck, wie unten gezeigt.

```java
// Da Mutationen im asynchronen Modus arbeiten, warten Sie einige Sekunden
synchronized (this) {
    wait(5000);
}
```

Hier warten wir 5 Sekunden, um sicherzustellen, dass der Beobachter die Möglichkeit hat, alle Mutationen zu erfassen.

## Schritt 5: Beenden Sie die Beobachtung

Wenn Sie mit der Beobachtung fertig sind, müssen Sie unbedingt die Verbindung zum Beobachter trennen, um Ressourcen freizugeben.

```java
// Hör auf zu beobachten
observer.disconnect();
```

Mit diesem Schritt haben Sie die Beobachtung abgeschlossen und können Ressourcen bereinigen.

## Abschluss

In diesem Tutorial haben wir den Prozess der Verwendung von Aspose.HTML für Java zur Implementierung eines DOM-Mutations-Observers durchgegangen. Sie haben gelernt, wie Sie einen Observer erstellen, konfigurieren, Änderungen am DOM vornehmen, auf Beobachtungen warten und die Beobachtung beenden. Jetzt sind Sie in der Lage, DOM-Mutations-Observer in Ihren Java-Projekten anzuwenden, um Änderungen im DOM von HTML-Dokumenten effektiv zu überwachen und darauf zu reagieren.

Wenn Sie Fragen haben oder auf Probleme stoßen, zögern Sie nicht, Hilfe im[Aspose.HTML-Forum](https://forum.aspose.com/) . Darüber hinaus haben Sie Zugriff auf die[Dokumentation](https://reference.aspose.com/html/java/) für detaillierte Informationen zu Aspose.HTML für Java.

## Häufig gestellte Fragen

### F1: Was ist ein DOM-Mutationsbeobachter?

A1: Ein DOM Mutation Observer ist eine JavaScript-Funktion, mit der Sie auf Änderungen im Document Object Model (DOM) eines HTML-Dokuments achten können. Sie bietet eine Möglichkeit, in Echtzeit auf Hinzufügungen, Löschungen oder Änderungen von DOM-Knoten zu reagieren.

### F2: Kann ich Aspose.HTML für Java in meinen kommerziellen Projekten verwenden?

 A2: Ja, Sie können Aspose.HTML für Java in kommerziellen Projekten verwenden. Lizenzierungs- und Kaufinformationen finden Sie hier[Hier](https://purchase.aspose.com/buy).

### F3: Gibt es eine kostenlose Testversion von Aspose.HTML für Java?

 A3: Ja, Sie können eine kostenlose Testversion von Aspose.HTML für Java erhalten[Hier](https://releases.aspose.com/). So können Sie die Funktionen und Möglichkeiten erkunden, bevor Sie einen Kauf tätigen.

### F4: Welchen Vorteil bietet die Beobachtung von Charakterdatenänderungen mit dem Mutation Observer?

A4: Die Beobachtung von Zeichendatenänderungen ist in Szenarien nützlich, in denen Sie Änderungen im Textinhalt von HTML-Elementen überwachen und darauf reagieren möchten. Sie können dies beispielsweise verwenden, um Benutzereingaben in Webformularen zu verfolgen und darauf zu reagieren.

### F5: Wie verfüge ich über Ressourcen, wenn ich Aspose.HTML für Java verwende?

 A5: Es ist wichtig, Ressourcen freizugeben, wenn Sie fertig sind. In unserem Beispiel haben wir`document.dispose()` um mit dem HTML-Dokument verknüpfte Ressourcen zu bereinigen. Stellen Sie sicher, dass Sie alle erstellten Objekte und Ressourcen löschen, um Speicherlecks zu vermeiden.