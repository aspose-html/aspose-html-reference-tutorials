---
title: DOM Mutation Observer mit Aspose.HTML für Java
linktitle: DOM Mutation Observer – Knotenhinzufügungen beobachten
second_title: Java HTML-Verarbeitung mit Aspose.HTML
description: Erfahren Sie in dieser Schritt-für-Schritt-Anleitung, wie Sie Aspose.HTML für Java verwenden, um einen DOM Mutation Observer zu implementieren. Überwachen Sie DOM-Änderungen und reagieren Sie effektiv darauf.
type: docs
weight: 11
url: /de/java/advanced-usage/dom-mutation-observer-observing-node-additions/
---

Sind Sie ein Java-Entwickler und möchten Änderungen im Document Object Model (DOM) eines HTML-Dokuments beobachten und darauf reagieren? Aspose.HTML für Java bietet eine leistungsstarke Lösung für diese Aufgabe. In dieser Schritt-für-Schritt-Anleitung erfahren Sie, wie Sie mit Aspose.HTML für Java ein HTML-Dokument erstellen und Knotenhinzufügungen mit einem Mutation Observer beobachten. Dieses Tutorial führt Sie durch den Prozess und unterteilt jedes Beispiel in mehrere Schritte. Am Ende können Sie DOM Mutation Observers problemlos in Ihre Java-Projekte implementieren.

## Voraussetzungen

Bevor wir uns mit der Verwendung von Aspose.HTML für Java befassen, stellen wir sicher, dass Sie über die erforderlichen Voraussetzungen verfügen:

1. Java-Entwicklungsumgebung: Stellen Sie sicher, dass auf Ihrem System das Java Development Kit (JDK) installiert ist.

2.  Aspose.HTML für Java: Sie müssen Aspose.HTML für Java herunterladen und installieren. Den Download-Link finden Sie hier[Hier](https://releases.aspose.com/html/java/).

3. IDE (Integrated Development Environment): Verwenden Sie Ihre bevorzugte Java-IDE, wie IntelliJ IDEA oder Eclipse, zum Schreiben und Ausführen von Java-Code.

## Pakete importieren

Um mit Aspose.HTML für Java zu beginnen, müssen Sie die erforderlichen Pakete in Ihren Java-Code importieren. So können Sie es machen:

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

Nachdem Sie nun die erforderlichen Pakete importiert haben, fahren wir mit der Schritt-für-Schritt-Anleitung zur Implementierung eines DOM Mutation Observer in Java fort.

## Schritt 1: Erstellen Sie eine Mutation Observer-Instanz

Zuerst müssen Sie eine Mutation Observer-Instanz erstellen. Dieser Beobachter überwacht das DOM auf Änderungen und führt eine Rückruffunktion aus, wenn Mutationen auftreten.

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

In diesem Schritt erstellen wir einen Beobachter mit einer Rückruffunktion, der eine Nachricht ausgibt, wenn Knoten zum DOM hinzugefügt werden.

## Schritt 2: Konfigurieren Sie den Observer

Nun konfigurieren wir den Beobachter mit den gewünschten Optionen. Wir möchten Änderungen an untergeordneten Listen und Teilbäumen sowie Änderungen an Zeichendaten beobachten.

```java
MutationObserverInit config = new MutationObserverInit();
config.setChildList(true);
config.setSubtree(true);
config.setCharacterData(true);

// Übergeben Sie den zu beobachtenden Zielknoten mit der angegebenen Konfiguration
observer.observe(document.getBody(), config);
```

 Hier legen wir fest`config` Objekt, um die Beobachtung von Änderungen an untergeordneten Listen, Teilbäumen und Zeichendaten zu ermöglichen. Anschließend übergeben wir den Zielknoten (in diesem Fall den des Dokuments).`<body>`) und die Konfiguration für den Beobachter.

## Schritt 3: Ändern Sie das DOM

Jetzt nehmen wir einige Änderungen am DOM vor, um den Beobachter auszulösen. Wir erstellen ein Absatzelement und hängen es an den Hauptteil des Dokuments an.

```java
// Erstellen Sie ein Absatzelement und hängen Sie es an den Dokumenttext an
Element p = document.createElement("p");
document.getBody().appendChild(p);

// Erstellen Sie einen Text und hängen Sie ihn an den Absatz an
Text text = document.createTextNode("Hello World");
p.appendChild(text);
```

In diesem Schritt erstellen wir ein HTML-Absatzelement und fügen es dem Hauptteil des Dokuments hinzu. Anschließend erstellen wir einen Textknoten mit dem Inhalt „Hello World“ und hängen ihn an den Absatz an.

## Schritt 4: Auf Beobachtungen warten (asynchron)

Da Mutationen asynchron beobachtet werden, müssen wir einen Moment warten, damit der Beobachter die Änderungen erfassen kann. Wir werden verwenden`synchronized` Und`wait` zu diesem Zweck, wie unten gezeigt.

```java
// Da Mutationen im asynchronen Modus arbeiten, warten Sie einige Sekunden
synchronized (this) {
    wait(5000);
}
```

Hier warten wir 5 Sekunden, um sicherzustellen, dass der Beobachter die Möglichkeit hat, etwaige Mutationen zu erfassen.

## Schritt 5: Hören Sie auf zu beobachten

Wenn Sie mit der Beobachtung fertig sind, ist es schließlich wichtig, die Verbindung zum Beobachter zu trennen, um Ressourcen freizugeben.

```java
// Hören Sie auf zu beobachten
observer.disconnect();
```

Mit diesem Schritt haben Sie die Beobachtung abgeschlossen und können Ressourcen bereinigen.

## Abschluss

In diesem Tutorial haben wir den Prozess der Verwendung von Aspose.HTML für Java zur Implementierung eines DOM Mutation Observers durchlaufen. Sie haben gelernt, wie Sie einen Beobachter erstellen, ihn konfigurieren, Änderungen am DOM vornehmen, auf Beobachtungen warten und die Beobachtung beenden. Jetzt verfügen Sie über die Fähigkeiten, DOM Mutation Observer in Ihren Java-Projekten einzusetzen, um Änderungen im DOM von HTML-Dokumenten effektiv zu überwachen und darauf zu reagieren.

Wenn Sie Fragen haben oder auf Probleme stoßen, zögern Sie nicht, Hilfe im zu suchen[Aspose.HTML-Forum](https://forum.aspose.com/) . Darüber hinaus können Sie auf die zugreifen[Dokumentation](https://reference.aspose.com/html/java/) Ausführliche Informationen zu Aspose.HTML für Java finden Sie hier.

## FAQs

### F1: Was ist ein DOM Mutation Observer?

A1: Ein DOM Mutation Observer ist eine JavaScript-Funktion, mit der Sie auf Änderungen im Document Object Model (DOM) eines HTML-Dokuments achten können. Es bietet eine Möglichkeit, in Echtzeit auf Hinzufügungen, Löschungen oder Änderungen von DOM-Knoten zu reagieren.

### F2: Kann ich Aspose.HTML für Java in meinen kommerziellen Projekten verwenden?

 A2: Ja, Sie können Aspose.HTML für Java in kommerziellen Projekten verwenden. Hier finden Sie Lizenzierungs- und Kaufinformationen[Hier](https://purchase.aspose.com/buy).

### F3: Gibt es eine kostenlose Testversion für Aspose.HTML für Java?

 A3: Ja, Sie können eine kostenlose Testversion von Aspose.HTML für Java erhalten[Hier](https://releases.aspose.com/). Auf diese Weise können Sie die Funktionen und Möglichkeiten erkunden, bevor Sie einen Kauf tätigen.

### F4: Welchen Vorteil bietet die Beobachtung von Charakterdatenänderungen mit dem Mutation Observer?

A4: Das Beobachten von Zeichendatenänderungen ist nützlich für Szenarien, in denen Sie Änderungen im Textinhalt von HTML-Elementen überwachen und darauf reagieren möchten. Sie können damit beispielsweise Benutzereingaben in Webformularen verfolgen und darauf reagieren.

### F5: Wie entsorge ich Ressourcen, wenn ich Aspose.HTML für Java verwende?

 A5: Es ist wichtig, Ressourcen freizugeben, wenn Sie fertig sind. In unserem Beispiel haben wir verwendet`document.dispose()` um mit dem HTML-Dokument verknüpfte Ressourcen zu bereinigen. Stellen Sie sicher, dass Sie alle von Ihnen erstellten Objekte und Ressourcen entsorgen, um Speicherverluste zu vermeiden.