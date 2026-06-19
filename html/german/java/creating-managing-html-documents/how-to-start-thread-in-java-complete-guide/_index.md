---
category: general
date: 2026-06-19
description: Wie man in Java einen Thread mit einem wiederverwendbaren Runnable startet,
  mehrere Threads startet, den Threadnamen ausgibt und HTML mit Java parst. Schritt‑für‑Schritt‑Beispiel.
draft: false
keywords:
- how to start thread
- start multiple threads
- print thread name
- parse html with java
- how to use runnable
language: de
og_description: Wie man in Java einen Thread mit Runnable startet, mehrere Threads
  ausführt, den Threadnamen ausgibt und HTML mit Java in einem einzigen, ausführbaren
  Beispiel parst.
og_title: Wie man einen Thread in Java startet – Vollständiger Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to start thread in Java with a reusable Runnable, start multiple
    threads, print thread name, and parse HTML with Java. Step‑by‑step example.
  headline: How to start thread in Java – Complete Guide
  type: TechArticle
tags:
- java
- multithreading
- html-parsing
- runnable
title: Wie man einen Thread in Java startet – Vollständiger Leitfaden
url: /de/java/creating-managing-html-documents/how-to-start-thread-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man einen Thread in Java startet – Vollständige Anleitung

Haben Sie sich jemals gefragt, **wie man einen Thread** in Java startet, ohne in Boiler‑Plate‑Code zu ersticken? Sie sind nicht allein. Ob Sie einen Web‑Crawler bauen, eine UI‑Aktualisierung durchführen oder einfach eine schwere Berechnung auslagern wollen – das Erstellen von Threads ist eine unverzichtbare Fähigkeit für jeden Java‑Entwickler.

In diesem Tutorial gehen wir ein praktisches Szenario durch: **HTML mit Java parsen**, den Namen des aktuellen Threads ausgeben und **mehrere Threads starten**, die dieselbe Logik teilen. Am Ende wissen Sie, **wie man Runnable verwendet**, mehrere Worker hochfährt und die erwartete Ausgabe sieht – alles in einem eigenständigen Beispiel, das Sie jetzt kopieren und einfügen können.

## Was Sie lernen werden

- Die genauen Schritte, **wie man einen Thread** mit der `Thread`‑Klasse und einem `Runnable` startet.
- Wie man **mehrere Threads startet**, die dieselbe Aufgabe ausführen, ohne Code zu duplizieren.
- Der einfachste Weg, **den Thread‑Namen auszugeben** zusammen mit Ihren Verarbeitungsergebnissen.
- Eine saubere Methode, **HTML mit Java zu parsen** mithilfe eines leichten `HTMLDocument`‑Hilfsprogramms (oder jedem anderen Parser Ihrer Wahl).
- Warum **wie man Runnable verwendet** wichtig ist für wiederverwendbaren, testbaren Code.

Für das Kernbeispiel sind keine externen Bibliotheken nötig, wir weisen jedoch darauf hin, wo Sie Jsoup oder einen anderen Parser einsetzen könnten, wenn Sie mehr Leistung benötigen.

---

## Schritt 1: Definieren einer wiederverwendbaren Aufgabe – **wie man Runnable verwendet**

Das Erste, was Sie wissen müssen, **wie man Runnable verwendet**, ist, die Arbeit zu kapseln, die jeder Thread ausführen soll. Ein `Runnable` ist nur ein funktionales Interface mit einer einzigen `run()`‑Methode, was es perfekt für Lambda‑Ausdrücke macht.

```java
// Define the reusable task
Runnable extractTextLength = () -> {
    // Open the HTML file inside a try‑with‑resources block
    try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
        // Get the length of the body text
        int textLength = doc.getBody().getTextContent().length();

        // Print the thread name and the length
        System.out.println(Thread.currentThread().getName() + ": " + textLength);
    } catch (Exception e) {
        e.printStackTrace();
    }
};
```

**Warum das wichtig ist:** Indem Sie die Logik in einem `Runnable` behalten, können Sie sie an beliebig viele `Thread`‑Objekte, einen Thread‑Pool oder später sogar an einen Executor‑Service übergeben. Das hält Ihren Code DRY und testbar.

---

## Schritt 2: **Wie man einen Thread startet** – den ersten Worker erstellen

Jetzt, wo wir ein `Runnable` haben, ist das Starten eines Threads so einfach wie der Aufruf des `Thread`‑Konstruktors. Die **wie man einen Thread startet**‑Frage wird in einer einzigen Zeile beantwortet:

```java
// Start the first thread
Thread worker1 = new Thread(extractTextLength, "Worker-1");
worker1.start();   // <-- this actually starts the new thread
```

Beachten Sie das zweite Argument, `"Worker-1"`. Dieser Name erscheint später, wenn wir **den Thread‑Namen ausgeben**, und macht das Debuggen deutlich weniger kryptisch.

---

## Schritt 3: **Mehrere Threads starten** – dasselbe Runnable wiederverwenden

Möchten Sie mehrere HTML‑Dateien gleichzeitig verarbeiten? Starten Sie einfach einen weiteren `Thread` mit demselben `Runnable`. Das demonstriert **mehrere Threads starten**, ohne den Aufgabencode zu kopieren:

```java
// Start a second thread that runs the exact same task
Thread worker2 = new Thread(extractTextLength, "Worker-2");
worker2.start();
```

Sowohl `Worker-1` als auch `Worker-2` führen den in `extractTextLength` definierten Block gleichzeitig aus. Da die Aufgabe zustandslos ist (sie liest nur eine Datei), gibt es keine Race‑Condition, um die Sie sich sorgen müssten.

---

## Schritt 4: **Thread‑Namen ausgeben** beim Parsen von HTML

Innerhalb des `Runnable` haben wir bereits `Thread.currentThread().getName()` aufgerufen. Das ist der kanonische Weg, **den Thread‑Namen auszugeben**. Die Ausgabe sieht etwa so aus (angenommen, der HTML‑Body enthält 1 234 Zeichen):

```
Worker-1: 1234
Worker-2: 1234
```

Wenn Sie das Programm mit einer größeren Datei ausführen, zeigt jede Zeile dieselbe Länge, weil beide Threads dieselbe Datei lesen. Ändern Sie den Pfad oder übergeben Sie den Dateinamen als Parameter, um unterschiedliche Ergebnisse zu sehen.

---

## Schritt 5: Vollständiges, ausführbares Beispiel – von Import bis Ausführung

Unten finden Sie das komplette, **selbst‑enthaltende** Programm, das Sie in eine Datei namens `HtmlThreadDemo.java` einfügen können. Es enthält einen kleinen `HTMLDocument`‑Stub, sodass der Code kompiliert, selbst wenn Sie keinen echten Parser zur Hand haben. Ersetzen Sie den Stub für den Produktionseinsatz durch Jsoup oder eine andere Bibliothek Ihrer Wahl.

```java
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Minimal HTMLDocument helper.
 * In a real project you would use Jsoup or another robust parser.
 */
class HTMLDocument implements AutoCloseable {
    private final String content;

    private HTMLDocument(String html) {
        this.content = html;
    }

    public static HTMLDocument load(String path) throws IOException {
        String html = new String(Files.readAllBytes(Paths.get(path)));
        return new HTMLDocument(html);
    }

    public Body getBody() {
        // Very naive extraction of <body>...</body>
        int start = content.indexOf("<body");
        if (start == -1) return new Body("");
        start = content.indexOf('>', start) + 1;
        int end = content.indexOf("</body>", start);
        if (end == -1) end = content.length();
        return new Body(content.substring(start, end));
    }

    @Override
    public void close() {
        // No resources to free in this stub
    }

    /** Simple wrapper for body text */
    static class Body {
        private final String text;
        Body(String text) { this.text = text; }
        public String getTextContent() { return text; }
    }
}

public class HtmlThreadDemo {

    public static void main(String[] args) {
        // Step 1: Define a reusable task (how to use runnable)
        Runnable extractTextLength = () -> {
            try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
                int textLength = doc.getBody().getTextContent().length();
                // Step 4: Print thread name and length
                System.out.println(Thread.currentThread().getName() + ": " + textLength);
            } catch (Exception e) {
                e.printStackTrace();
            }
        };

        // Step 2 & 3: How to start thread and start multiple threads
        new Thread(extractTextLength, "Worker-1").start();
        new Thread(extractTextLength, "Worker-2").start();
    }
}
```

### Erwartete Ausgabe

Angenommen, `page.html` enthält 2 567 Zeichen innerhalb des `<body>`‑Tags, dann sehen Sie etwa Folgendes:

```
Worker-1: 2567
Worker-2: 2567
```

Kann die Datei nicht gelesen werden, wird der Stack‑Trace ausgegeben – dank des `catch`‑Blocks.

---

## Häufige Stolperfallen & Pro‑Tipps

| Problem | Warum es passiert | Lösung |
|---------|-------------------|--------|
| **Datei nicht gefunden** | Der Pfad `"YOUR_DIRECTORY/page.html"` ist relativ zu dem Ort, an dem Sie die JVM starten. | Verwenden Sie einen absoluten Pfad oder `Paths.get("").toAbsolutePath()` zum Debuggen. |
| **Race Conditions** | Wenn das `Runnable` gemeinsam genutzten Zustand verändert, können Threads kollidieren. | Halten Sie die Aufgabe zustandslos oder synchronisieren Sie den Zugriff auf geteilte Objekte. |
| **Zu viele Threads** | Das Erzeugen Dutzender `Thread`s kann OS‑Ressourcen erschöpfen. | Wechseln Sie nach dem Grundlagen‑Erlernen zu einem `ExecutorService` mit begrenztem Pool. |
| **Fehlerhafte HTML‑Parsen** | Der Stub `HTMLDocument` ist simpel; komplexe Seiten brechen. | Ersetzen Sie ihn durch Jsoup: `Document doc = Jsoup.parse(new File(path), "UTF‑8");` |

---

## Das Beispiel erweitern

Jetzt, wo Sie **wie man einen Thread startet** kennen, könnten Sie:

- **Verschiedene Dateien parsen**, indem Sie den Dateinamen in das `Runnable` übergeben (z. B. über einen Konstruktor oder ein Lambda, das eine Variable erfasst).
- **Ergebnisse sammeln** mit einer `ConcurrentLinkedQueue<Integer>` anstatt nur zu drucken.
- **Einen Thread‑Pool nutzen** (`Executors.newFixedThreadPool(4)`) für bessere Skalierbarkeit.
- **Den Parser austauschen** gegen Jsoup, HtmlUnit oder jede Bibliothek, die zu Ihrem Projekt passt.

All diese Schritte beruhen weiterhin auf der Kernidee, die wir behandelt haben: eine wiederverwendbare Aufgabe definieren, sie einem oder mehreren Threads übergeben und beobachten, welcher Thread arbeitet, indem Sie **den Thread‑Namen ausgeben**.

---

## Fazit

Wir haben **wie man einen Thread** in Java startet, gezeigt, **wie man Runnable verwendet** für wiederverwendbare Arbeit, demonstriert, **wie man mehrere Threads startet**, und eine einfache Methode vorgestellt, **HTML mit Java zu parsen**, während wir **den Thread‑Namen ausgeben** für jeden Worker. Der komplette Code‑Snippet oben ist sofort ausführbar, und die Konzepte skalieren zu komplexeren, produktionsreifen Anwendungen.

Experimentieren Sie gern: ändern Sie den Dateipfad, erhöhen Sie die Anzahl der Worker oder binden Sie einen echten HTML‑Parser ein. Die Grundlagen bleiben gleich, und Sie haben nun ein solides Fundament für jedes multithreaded Java‑Projekt.

Haben Sie Fragen zu Thread‑Sicherheit, Executor‑Services oder HTML‑Parsing‑Bibliotheken? Hinterlassen Sie einen Kommentar unten – happy coding!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Fixed thread pool java – Parallel HTML Cleaning with ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}