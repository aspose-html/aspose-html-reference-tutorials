---
category: general
date: 2026-05-28
description: Wie man Executor in Java mit einem festen Thread‑Pool verwendet, Text
  aus HTML extrahiert und die Verarbeitung beschleunigt – ein vollständiges Java‑Thread‑Pool‑Beispiel.
draft: false
keywords:
- how to use executor
- fixed thread pool java
- extract text from html
- java thread pool example
- create fixed thread pool
language: de
og_description: Wie man Executor in Java mit einem festen Thread‑Pool verwendet. Lernen
  Sie ein vollständiges Java‑Thread‑Pool‑Beispiel, das Text effizient aus HTML‑Dateien
  extrahiert.
og_title: Wie man Executor in Java verwendet – Leitfaden für einen festen Thread‑Pool
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: how to use executor in Java with a fixed thread pool, extract text
    from HTML and speed up processing – a complete java thread pool example.
  headline: How to Use Executor in Java – Fixed Thread Pool Guide
  type: TechArticle
tags:
- Java
- Concurrency
- HTML Parsing
title: Wie man Executor in Java verwendet – Leitfaden für einen festen Thread‑Pool
url: /de/java/advanced-usage/how-to-use-executor-in-java-fixed-thread-pool-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Executor in Java verwendet – Leitfaden für Fixed Thread Pool

Haben Sie sich jemals gefragt, **wie man Executor** verwendet, um viele Aufgaben gleichzeitig auszuführen, ohne den Speicher zu sprengen? Sie sind nicht allein. In vielen realen Anwendungen müssen Sie einen Ordner mit HTML‑Dateien durchforsten, den Body‑Text extrahieren und das schnell tun – genau das Szenario, das dieses Tutorial löst.

Wir gehen eine **fixed thread pool java** Implementierung durch, die Text aus HTML extrahiert, die Zeichenanzahl jeder Datei ausgibt und sauber herunterfährt. Am Ende haben Sie ein eigenständiges **java thread pool example**, das Sie in jedes Projekt einbinden können, plus ein paar Tipps zur Anpassung der Poolgröße und zum Umgang mit Randfällen.

> **Was Sie benötigen**  
> * Java 17 (oder ein aktuelles JDK)  
> * Eine kleine HTML‑Parsing‑Bibliothek – wir verwenden *jsoup*, weil sie erprobt und konfigurationsfrei ist.  
> * Eine Handvoll Beispiel‑*.html*-Dateien in einem Verzeichnis Ihrer Wahl.

---

## Wie man Executor mit einem Fixed Thread Pool verwendet

Das Herzstück jedes stark nebenläufigen Java‑Programms ist das `ExecutorService`. Durch das Erstellen eines **fixed thread pool** teilen wir der JVM mit, exakt N Worker‑Threads am Leben zu erhalten, was den Overhead der Thread‑Erstellung verhindert und die Ressourcennutzung begrenzt.

```java
// Step 1: Build a fixed‑size thread pool (4 workers in this case)
ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Warum das wichtig ist:*  
Wenn Sie für jede HTML‑Datei einen neuen `Thread` starten würden, müsste das Betriebssystem Dutzende von Threads auf einem bescheidenen Laptop planen, was zu einem ständigen Kontext‑Switch‑Thrashing führt. Ein fester Pool verwendet dieselben vier Threads wieder, was Ihnen eine vorhersehbare CPU‑Auslastung gibt.

---

## Definieren der zu verarbeitenden HTML‑Dateien – Fixed Thread Pool Java

Als Nächstes listen wir die Dateien auf, die wir dem Pool zuführen wollen. In einer echten Anwendung würden Sie wahrscheinlich einen Verzeichnisbaum durchlaufen; hier halten wir es einfach.

```java
// Step 2: List the HTML documents you want to parse
List<String> htmlFilePaths = List.of(
        "YOUR_DIRECTORY/a.html",
        "YOUR_DIRECTORY/b.html",
        "YOUR_DIRECTORY/c.html",
        "YOUR_DIRECTORY/d.html"
);
```

*Tipp:* `List.of` gibt eine unveränderliche Liste zurück, die sicher über Threads hinweg geteilt werden kann, ohne zusätzliche Synchronisation.

---

## Einen separaten Task für jede HTML‑Datei einreichen

Jetzt übergeben wir jedem Pfad den Executor. Das Lambda, das wir einreichen, wird **parallel** auf einem der vier Worker‑Threads ausgeführt.

```java
// Step 3: Dispatch a parsing job for every file
for (String htmlFilePath : htmlFilePaths) {
    executor.submit(() -> {
        // Each lambda runs on a thread from the pool
        try {
            // Step 4: Open the document, extract its text, and display the length
            String text = extractBodyText(htmlFilePath);
            System.out.println(htmlFilePath + " → " + text.length() + " chars");
        } catch (IOException e) {
            System.err.println("Failed to read " + htmlFilePath);
            e.printStackTrace();
        }
    });
}
```

**Warum wir die Logik in einer Methode** (`extractBodyText`) kapseln, wird im nächsten Abschnitt klar – es hält das Lambda übersichtlich und ermöglicht die Wiederverwendung des Extraktionscodes an anderer Stelle.

---

## Text aus HTML extrahieren – Die Kernlogik

Hier ist die wiederverwendbare Hilfsfunktion, die tatsächlich **Text aus HTML** mit Jsoup extrahiert. Sie öffnet die Datei, parsed das DOM und gibt den reinen Body‑Text zurück.

```java
/**
 * Reads an HTML file and returns the plain text inside the <body>.
 *
 * @param path absolute or relative path to the .html file
 * @return body text without tags
 * @throws IOException if the file cannot be read
 */
private static String extractBodyText(String path) throws IOException {
    // Jsoup parses the file into a Document object.
    org.jsoup.nodes.Document doc = org.jsoup.Jsoup.parse(new java.io.File(path), "UTF-8");
    // getBody() gives us the <body> element; text() strips all tags.
    return doc.body().text();
}
```

*Warum Jsoup?* Es ist leichtgewichtig, verarbeitet fehlerhaftes Markup elegant und benötigt keine komplette Browser‑Engine. Die Methode wirft `IOException`, sodass der Aufrufer entscheiden kann, wie er protokolliert oder sich erholt – perfekt für ein Thread‑Pool‑Szenario, bei dem Sie nicht möchten, dass eine einzige fehlerhafte Datei den gesamten Executor beendet.

---

## Den Executor sauber herunterfahren – Fixed Thread Pool erstellen

Nachdem wir alle Jobs eingereicht haben, müssen wir dem Pool mitteilen, dass er keine neuen Aufgaben mehr annimmt und das bereits Wartende abschließt.

```java
// Step 5: Initiate an orderly shutdown once all tasks are queued
executor.shutdown();
try {
    // Wait up to 30 seconds for all tasks to finish
    if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
        System.err.println("Timed out waiting for tasks; forcing shutdown.");
        executor.shutdownNow();
    }
} catch (InterruptedException ie) {
    // Preserve interrupt status and force shutdown
    Thread.currentThread().interrupt();
    executor.shutdownNow();
}
```

*Erklärung:* `shutdown()` verhindert neue Einreichungen, während `awaitTermination` blockiert, bis jeder Parsing‑Job endet (oder das Timeout abläuft). Wenn etwas hängen bleibt, versucht `shutdownNow()` laufende Tasks abzubrechen. Dieses Muster ist der empfohlene Weg, **create fixed thread pool** sicher zu erstellen.

---

## Vollständiges, ausführbares Beispiel

Wenn wir alles zusammenfügen, erhalten Sie eine einzelne Datei, die Sie kompilieren und ausführen können. Sie enthält die notwendigen Importe, die `main`‑Methode und die oben beschriebene Hilfsfunktion.

```java
import java.io.IOException;
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

/**
 * Demonstrates how to use executor with a fixed thread pool to
 * extract text from multiple HTML files concurrently.
 */
public class HtmlThreadPoolDemo {

    public static void main(String[] args) {
        // 1️⃣ Build a fixed‑size pool (adjust the size for your hardware)
        ExecutorService executor = Executors.newFixedThreadPool(4);

        // 2️⃣ Define the files we want to process
        List<String> htmlFilePaths = List.of(
                "YOUR_DIRECTORY/a.html",
                "YOUR_DIRECTORY/b.html",
                "YOUR_DIRECTORY/c.html",
                "YOUR_DIRECTORY/d.html"
        );

        // 3️⃣ Submit a parsing task for each file
        for (String htmlFilePath : htmlFilePaths) {
            executor.submit(() -> {
                try {
                    String text = extractBodyText(htmlFilePath);
                    System.out.println(htmlFilePath + " → " + text.length() + " chars");
                } catch (IOException e) {
                    System.err.println("Error processing " + htmlFilePath);
                    e.printStackTrace();
                }
            });
        }

        // 5️⃣ Shut down the pool cleanly
        executor.shutdown();
        try {
            if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("Tasks took too long; forcing shutdown.");
                executor.shutdownNow();
            }
        } catch (InterruptedException ie) {
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }

    /**
     * Reads an HTML file and returns the plain text inside the <body>.
     *
     * @param path path to the .html file
     * @return body text without markup
     * @throws IOException if file cannot be read
     */
    private static String extractBodyText(String path) throws IOException {
        Document doc = Jsoup.parse(new java.io.File(path), "UTF-8");
        return doc.body().text();
    }
}
```

**Erwartete Ausgabe** (unter der Annahme, dass jede Datei etwa 1 200 Zeichen Body‑Text enthält):

```
YOUR_DIRECTORY/a.html → 1234 chars
YOUR_DIRECTORY/b.html → 1198 chars
YOUR_DIRECTORY/c.html → 1305 chars
YOUR_DIRECTORY/d.html → 1120 chars
```

Falls eine Datei fehlt oder fehlerhaft ist, sehen Sie einen Stack‑Trace, der zu `stderr` ausgegeben wird, aber die anderen Tasks laufen unverändert weiter – genau das, was ein gut funktionierendes **java thread pool example** tun sollte.

---

## Häufige Fragen & Randfälle

| Frage | Antwort |
|----------|--------|
| *Was, wenn ich mehr als vier Dateien habe?* | Der Pool wird die zusätzlichen Tasks in die Warteschlange stellen und sie ausführen, sobald ein Thread frei wird. Kein zusätzlicher Code nötig. |
| *Sollte ich stattdessen `newCachedThreadPool` verwenden?* | `newCachedThreadPool` erstellt Threads bei Bedarf und kann unbeschränkt wachsen, was bei I/O‑intensiven Jobs riskant ist. Ein **fixed thread pool** bietet vorhersehbare Speicher‑ und CPU‑Nutzung. |
| *Wie ändere ich die Poolgröße basierend auf CPU‑Kernen?* | `int cores = Runtime.getRuntime().availableProcessors(); ExecutorService exec = Executors.newFixedThreadPool(cores);` ist ein gängiges Muster. |
| *Was, wenn das Parsen einer Datei fehlschlägt?* | Das `catch (IOException e)` im Lambda isoliert den Fehler, protokolliert ihn und lässt den Rest des Pools weiterarbeiten. |
| *Kann ich den extrahierten Text an den Aufrufer zurückgeben?* | Ja – verwenden Sie `Future<String>` anstelle von `submit(Runnable)`. Der Code würde etwa so aussehen: `Future<String> f = executor.submit(() -> extractBodyText(path));` und später `String result = f.get();`. |

---

## Fazit

Wir haben **wie man Executor** verwendet, um einen **fixed thread pool java** zu starten, der eine Sammlung von HTML‑Dateien parallel verarbeitet, deren Body‑Text extrahiert und die Zeichenanzahl ausgibt. Das vollständige **java thread pool example** demonstriert korrektes Ressourcenmanagement, Fehlerbehandlung und eine wiederverwendbare Extraktionsmethode.

Nächste Schritte? Versuchen Sie, die `extractBodyText`‑Implementierung durch einen anspruchsvolleren Scraper zu ersetzen, experimentieren Sie mit einer größeren Poolgröße oder leiten Sie die Ergebnisse in eine Datenbank weiter. Sie können auch `CompletionService` erkunden, um Ergebnisse abzurufen, sobald sie fertig sind – praktisch, wenn Dateigrößen stark variieren.

Passen Sie den Verzeichnispfad nach Belieben an, fügen Sie weitere Dateien hinzu oder integrieren Sie diesen Code‑Abschnitt in ein größeres Crawling‑Framework. Das Kernmuster – einen Pool erstellen, unabhängige Tasks einreichen und sauber herunterfahren – bleibt gleich, egal wie komplex Ihre Arbeitslast wird.

Viel Spaß beim Coden, und möge Ihre Threads immer am Leben bleiben (bis Sie sie natürlich herunterfahren)!

## Verwandte Tutorials

- [Fixed thread pool java – Parallel HTML‑Bereinigung mit ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [Wie man HTML in Java abfragt – Komplettes Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Wie man Aspose.HTML für Java verwendet – Beherrschung des HTML5‑Canvas‑Renderings](/html/english/java/html5-canvas-rendering/html5-canvas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}