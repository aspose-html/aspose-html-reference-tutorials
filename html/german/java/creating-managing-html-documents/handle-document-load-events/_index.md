---
date: 2026-04-23
description: Erfahren Sie in dieser Schritt‑für‑Schritt‑Anleitung, wie Sie mit Aspose.HTML
  für Java das äußere HTML erhalten und auf das Laden des Dokuments warten.
keywords:
- get outer html
- wait for document load
- java html processing
- navigate html document
- aspose html example
linktitle: Dokumenten‑Ladeereignisse in Aspose.HTML verarbeiten
second_title: Java HTML Processing with Aspose.HTML
title: Outer‑HTML abrufen und Ladeereignisse in Aspose.HTML für Java verarbeiten
url: /de/java/creating-managing-html-documents/handle-document-load-events/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Erhalte das äußere HTML & verarbeite Ladeereignisse in Aspose.HTML für Java

## Einleitung
Wenn Sie **get outer html** von einer entfernten Seite benötigen und sofort reagieren möchten, sobald das Dokument das Laden abgeschlossen hat, wird das Handling von Dokument‑Ladeereignissen unverzichtbar. In Java bietet Aspose.HTML eine klare API, um sowohl zu einer URL zu navigieren als auch das `OnLoad`‑Ereignis zu abonnieren, sodass Sie sicher auf das HTML zugreifen können, sobald es bereit ist. Dieses Tutorial führt Sie durch den gesamten Prozess – von der Einrichtung bis zum Ausgeben des äußeren HTML einer geladenen Seite – sodass Sie es in jede web‑zentrierte Java‑Anwendung integrieren können.

## Schnelle Antworten
- **Was bedeutet „get outer html“?** Es gibt das vollständige HTML‑Markup des Wurzelelements des Dokuments zurück.  
- **Welche Bibliothek verarbeitet Ladeereignisse?** Aspose.HTML für Java stellt das `OnLoad`‑Ereignis bereit.  
- **Benötige ich eine Lizenz für Tests?** Eine kostenlose Testversion ist verfügbar; für die Produktion ist eine kommerzielle Lizenz erforderlich.  
- **Wie kann ich warten, bis das Dokument geladen ist?** Verwenden Sie den `OnLoad`‑Handler oder ein einfaches Sleep‑Verfahren für Demonstrationszwecke.  
- **Ist dieser Ansatz asynchron sicher?** Ja, das Ereignis wird ausgelöst, nachdem das Dokument fertig geladen ist, sodass das HTML bereit ist.

## Was ist „get outer html“?
`document.getDocumentElement().getOuterHTML()` gibt die komplette HTML‑Zeichenkette des Wurzelelements des Dokuments zurück, einschließlich der öffnenden und schließenden Tags. Dies ist nützlich, wenn Sie das rohe Markup für weitere Verarbeitung, Speicherung oder Transformation benötigen.

## Warum Aspose.HTML für Java verwenden?
- **Robuste HTML‑Analyse** ohne einen Browser‑Engine zu benötigen.  
- **Ereignisgesteuertes Modell** ermöglicht es, genau dann zu reagieren, wenn das Dokument bereit ist.  
- **Plattformübergreifende Unterstützung** für Windows, Linux und macOS.  
- **Umfangreiche API** für Navigation, Manipulation und Konvertierung zu PDF, Bild usw.

## Voraussetzungen
Bevor wir in den Code eintauchen, stellen Sie sicher, dass Sie Folgendes haben:

1. **Java Development Kit (JDK)** – Installieren Sie es von der [Oracle's website](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html).  
2. **Aspose.HTML for Java** – Laden Sie das neueste JAR von der [Aspose releases page](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse oder ein beliebiger Editor Ihrer Wahl.  
4. **Grundlegende Java‑Kenntnisse** – Verständnis von Klassen, Methoden und Ereignisbehandlung.  
5. **Internetverbindung** – Das Beispiel lädt eine Online‑HTML‑Seite.

Sobald alles bereit ist, können Sie mit dem Codieren beginnen!

## Schritt‑für‑Schritt‑Anleitung

### Schritt 1: Initialisieren eines HTML‑Dokuments
Zuerst erstellen wir eine `HTMLDocument`‑Instanz. Zusätzlich richten wir ein `AtomicBoolean` ein, um den Ladezustand zu verfolgen.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument();
java.util.concurrent.atomic.AtomicBoolean isLoading = new java.util.concurrent.atomic.AtomicBoolean(false);
```

### Schritt 2: Abonnieren des **OnLoad**‑Ereignisses
Fügen Sie einen Handler hinzu, der das `isLoading`‑Flag umschaltet, sobald das Dokument das Laden abgeschlossen hat. Hier wissen wir, dass es sicher ist, **get outer html** aufzurufen.

```java
document.OnLoad.add(new DOMEventHandler() {
    @Override
    public void invoke(Object o, Event event) {
        isLoading.set(true);
    }
});
```

### Schritt 3: Navigieren zum Dokument (HTML von URL laden)
Geben Sie dem `HTMLDocument` an, welche Seite abgerufen werden soll. In diesem Beispiel laden wir eine öffentliche Aspose‑Dokumentationsseite.

```java
document.navigate("https://docs.aspose.com/html/net/creating-a-document/document.html");
```

### Schritt 4: Warten, bis das Dokument geladen ist
Das Laden einer entfernten Seite ist asynchron. Zum Demonstrationszweck pausieren wir den Thread für einige Sekunden; in der Produktion würden Sie das `OnLoad`‑Flag oder eine ausgefeiltere Synchronisations‑Technik nutzen.

```java
Thread.sleep(5000);
```

### Schritt 5: Zugriff auf das geladene Dokument und **Get Outer HTML**
Jetzt, wo `isLoading` true ist, rufen wir das vollständige Markup des Wurzelelements des Dokuments ab.

```java
System.out.println("outerHTML = " + document.getDocumentElement().getOuterHTML());
```

Sie sollten das komplette HTML der geladenen Seite in der Konsole ausgegeben sehen.

## Häufige Probleme und Lösungen
| Problem | Grund | Lösung |
|-------|--------|-----|
| **`isLoading` never becomes true** | Der `OnLoad`‑Handler wurde nicht vor `navigate()` angehängt | Hängen Sie den Handler **vor** dem Aufruf von `navigate()` an. |
| **`NullPointerException` on `getDocumentElement()`** | Dokument war beim Zugriff nicht vollständig geladen | Verwenden Sie einen geeigneten Warte‑Mechanismus (z. B. Schleife über `isLoading.get()` oder ein `CountDownLatch`). |
| **SSLHandshakeException when loading HTTPS URLs** | Fehlende vertrauenswürdige Zertifikate | Fügen Sie das entsprechende Zertifikat zu Ihrem Java‑Keystore hinzu oder verwenden Sie `-Djsse.enableSNIExtension=false`. |
| **Slow loading causing timeout** | Große Seite oder Netzwerkverzögerung | Erhöhen Sie die Schlafdauer oder implementieren Sie einen timeout‑bewussten Listener. |

## Häufig gestellte Fragen

**Q: Was ist Aspose.HTML für Java?**  
A: Aspose.HTML für Java ist eine Bibliothek, die Entwicklern ermöglicht, HTML‑Dokumente in Java‑Anwendungen zu erstellen, zu manipulieren und zu konvertieren.

**Q: Wie lade ich Aspose.HTML für Java herunter?**  
A: Sie können es von der [Aspose releases page](https://releases.aspose.com/html/java/) herunterladen.

**Q: Kann ich Aspose.HTML kostenlos nutzen?**  
A: Ja, Sie können Aspose.HTML kostenlos testen, indem Sie eine Testversion von der [Aspose website](https://releases.aspose.com/) herunterladen.

**Q: Gibt es Unterstützung für Aspose.HTML?**  
A: Ja, Sie finden Support und können Fragen im [Aspose forum](https://forum.aspose.com/c/html/29) stellen.

**Q: Wie erhalte ich eine temporäre Lizenz für Aspose.HTML?**  
A: Sie können eine temporäre Lizenz beantragen, indem Sie die [Aspose temporary license page](https://purchase.aspose.com/temporary-license/) besuchen.

---

**Last Updated:** 2026-04-23  
**Tested With:** Aspose.HTML for Java 24.11  
**Author:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}