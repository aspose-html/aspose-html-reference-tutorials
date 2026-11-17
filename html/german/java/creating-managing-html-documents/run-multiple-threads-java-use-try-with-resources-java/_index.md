---
category: general
date: 2026-04-09
description: Führen Sie mehrere Threads in Java effizient mit try‑with‑resources aus.
  Erfahren Sie, wie Sie ein HTML‑Dokument in Java sicher laden und Nebenläufigkeitsprobleme
  vermeiden.
draft: false
keywords:
- run multiple threads java
- use try with resources java
- load html document java
- avoid concurrency issues java
language: de
og_description: Mehrere Threads in Java mit try‑with‑resources ausführen. Dieses Tutorial
  zeigt, wie man ein HTML‑Dokument in Java sicher lädt und dabei Konkurrenzprobleme
  vermeidet.
og_title: Mehrere Threads in Java ausführen – Leitfaden zu try‑with‑resources
tags:
- java
- multithreading
- html-parsing
title: Mehrere Threads in Java ausführen – try‑with‑resources in Java verwenden
url: /de/java/creating-managing-html-documents/run-multiple-threads-java-use-try-with-resources-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mehrere Threads in Java ausführen – try‑with‑resources in Java verwenden

Haben Sie sich jemals gefragt, wie man **mehrere Threads in Java ausführen** ohne Konflikte ausführen kann? Sie sind nicht allein – die meisten Entwickler stoßen auf dasselbe Problem, wenn sie versuchen, ein veränderbares Objekt über Threads zu teilen. Die gute Nachricht? Es gibt einen sauberen, modernen Ansatz, und er beginnt mit der `try‑with‑resources`‑Anweisung.

In diesem Leitfaden gehen wir ein vollständiges, copy‑and‑paste‑fertiges Beispiel durch, das **lädt ein HTML‑Dokument in Java**, mehrere Threads startet und garantiert, dass jeder Thread mit seiner eigenen Dokument‑Instanz arbeitet. Am Ende sehen Sie außerdem, wie man **Concurrency‑Probleme in Java vermeidet**, damit Ihre Anwendung unter Last stabil bleibt.

> **Was Sie erhalten:** ein ausführbares Java‑Programm, Schritt‑für‑Schritt‑Erklärungen, Tipps für reale Projekte und einen schnellen Test, den Sie sofort ausführen können.

---

![Mehrere Threads in Java Illustration](run-multiple-threads-java.png "Diagramm, das mehrere Threads zeigt, von denen jeder eine separate HTMLDocument‑Instanz hält")

## Voraussetzungen

- Java 17 oder neuer (die `try‑with‑resources`‑Syntax funktioniert ab Java 7 gleich, aber wir verwenden neuere Sprachfeatures für Kürze).  
- Eine kleine HTML‑Parsing‑Hilfsklasse namens `HTMLDocument`. Wenn Sie keine haben, können Sie sie später wie gezeigt stubben.  
- Grundkenntnisse zu Threads (`java.lang.Thread`) und dem `Runnable`‑Interface.

Wenn Ihnen irgendeiner dieser Punkte unbekannt ist, keine Panik – jedes Konzept wird in den nachfolgenden Schritten erneut behandelt.

---

## Schritt 1: HTML‑Dokument in Java mit einer geteilten Referenz laden

Das Erste, was wir benötigen, ist eine *geteilte* Referenz, die auf die Datei zeigt, die wir parsen wollen. Denken Sie daran wie an einen Bauplan: Die URL ist für jeden Thread gleich, aber das eigentliche Dokument‑Objekt wird später pro Thread erstellt.

```java
// Step 1: Load the source HTML document (shared reference for its URL)
HTMLDocument sharedDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

### Warum eine geteilte Referenz?

Wenn Sie jedem Thread dieselbe `HTMLDocument`‑Instanz geben würden, würden sie alle auf dieselben internen Puffer lesen und schreiben. Das ist ein klassisches Rezept für Race Conditions – genau die Art von **Concurrency‑Problemen in Java**, die wir zu vermeiden versuchen. Indem nur die *URL* geteilt wird, kann jeder Thread später sicher seinen eigenen Stream öffnen.

> **Pro‑Tipp:** Speichern Sie die URL in einer `final`‑Variablen, wenn Sie sie nie ändern wollen. Der Compiler behandelt sie dann als Konstante, was versehentliche Mutationen weiter reduziert.

---

## Schritt 2: Eine thread‑sichere Aufgabe mit try‑with‑resources in Java erstellen

Jetzt definieren wir, was jeder Thread tatsächlich tut. Der Trick besteht darin, die pro‑Thread‑Erstellung von `HTMLDocument` in einen `try‑with‑resources`‑Block zu hüllen. Das garantiert, dass das Dokument automatisch geschlossen wird, selbst wenn eine Ausnahme nach oben wandert.

```java
// Step 2: Define a task that creates its own document instance per thread
Runnable task = () -> {
    // Each thread works with its own copy to avoid concurrency issues
    try (HTMLDocument threadDoc = new HTMLDocument(sharedDoc.getUrl())) {
        // Perform thread‑specific operations on threadDoc here
        System.out.println("Thread " + Thread.currentThread().getName()
                + " loaded: " + threadDoc.getTitle());
    } catch (Exception e) {
        System.err.println("Error in thread " + Thread.currentThread().getName()
                + ": " + e.getMessage());
    }
};
```

### Wie `try‑with‑resources` hilft

Die Klasse `HTMLDocument` implementiert `java.lang.AutoCloseable`. Wenn der `try`‑Block endet, ruft die JVM automatisch `threadDoc.close()` auf. Das ist weitaus sicherer als ein manuelles `finally`‑Statement und eliminiert das Risiko, native Ressourcen zu vergessen freizugeben – etwas, das leicht zu Speicherlecks in langlaufenden, multithreaded Anwendungen führen kann.

---

## Schritt 3: Threads starten und **Concurrency‑Probleme in Java** vermeiden

Mit der fertigen Aufgabe können wir so viele Threads starten, wie wir möchten. Zur Demonstration starten wir zwei, aber es gibt nichts, was Sie daran hindert, einen Thread‑Pool mit Dutzenden von Arbeitern zu starten.

```java
// Step 3: Launch multiple threads that execute the same task
Thread t1 = new Thread(task, "Worker‑1");
Thread t2 = new Thread(task, "Worker‑2");

// Start the threads
t1.start();
t2.start();

// Optional: wait for them to finish (join) if you need deterministic ordering
t1.join();
t2.join();
```

### Warum nicht `ExecutorService` verwenden?

Im Produktionscode werden Sie wahrscheinlich **will** einen `ExecutorService` einsetzen, um einen Pool von Arbeitern zu verwalten. Das einfache `Thread`‑Beispiel hält den Fokus des Tutorials auf der Kernidee – pro Thread ein separates Dokument zu erstellen und `try‑with‑resources` zu nutzen. Ersetzen Sie die `Thread`‑Aufrufe gern durch einen `FixedThreadPool`, wenn das zu Ihrer Projekt‑Architektur passt.

---

## Vollständiges, ausführbares Beispiel

Alles zusammengefügt, hier ein eigenständiges Programm, das Sie in eine Datei namens `MultiThreadHtmlDemo.java` einfügen können. Es enthält einen minimalen Stub für `HTMLDocument`, sodass Sie es sofort kompilieren und ausführen können.

```java
// MultiThreadHtmlDemo.java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;

// --- Minimal stub for demonstration purposes ---
class HTMLDocument implements AutoCloseable {
    private final String url;
    private String content;

    public HTMLDocument(String url) throws IOException {
        this.url = url;
        // Simulate loading the file (replace with real parser in production)
        this.content = Files.readString(Path.of(url));
    }

    public String getUrl() {
        return url;
    }

    public String getTitle() {
        // Very naive title extraction – just for demo
        int start = content.indexOf("<title>");
        int end = content.indexOf("</title>");
        if (start != -1 && end != -1 && end > start) {
            return content.substring(start + 7, end).trim();
        }
        return "Untitled";
    }

    @Override
    public void close() {
        // In a real library you’d release native buffers here
        content = null;
        System.out.println("Closed document for URL: " + url);
    }
}

// --- Main class that runs multiple threads java ---
public class MultiThreadHtmlDemo {
    public static void main(String[] args) throws InterruptedException, IOException {
        // Step 1: Load the source HTML document (shared reference for its URL)
        HTMLDocument sharedDoc = new HTMLDocument("sample.html");

        // Step 2: Define a task that creates its own document instance per thread
        Runnable task = () -> {
            try (HTMLDocument threadDoc = new HTMLDocument(sharedDoc.getUrl())) {
                System.out.println("Thread " + Thread.currentThread().getName()
                        + " loaded title: " + threadDoc.getTitle());
            } catch (Exception e) {
                System.err.println("Error in thread " + Thread.currentThread().getName()
                        + ": " + e.getMessage());
            }
        };

        // Step 3: Launch multiple threads that execute the same task
        Thread t1 = new Thread(task, "Worker‑1");
        Thread t2 = new Thread(task, "Worker‑2");

        t1.start();
        t2.start();

        // Wait for both threads to finish
        t1.join();
        t2.join();

        System.out.println("All threads completed.");
    }
}
```

#### Erwartete Ausgabe (angenommen, `sample.html` enthält `<title>Hello World</title>`)

```
Thread Worker-1 loaded title: Hello World
Closed document for URL: sample.html
Thread Worker-2 loaded title: Hello World
Closed document for URL: sample.html
All threads completed.
```

Beachten Sie, wie jeder Thread seinen eigenen *geladenen Titel* ausgibt und dann die `close()`‑Methode automatisch ausgeführt wird – genau das, was `try‑with‑resources` verspricht.

---

## Häufige Fragen & Edge‑Case‑Behandlung

**Was, wenn die Datei nicht gefunden wird?**  
Der Konstruktor wirft `IOException`. Im Beispiel fangen wir sie innerhalb des `Runnable` ab und protokollieren einen Fehler, sodass eine fehlende Datei die gesamte Anwendung nicht zum Absturz bringt.

**Kann ich dieselbe `HTMLDocument`‑Instanz über Threads hinweg wiederverwenden?**  
Nur wenn die Klasse ausdrücklich als thread‑sicher dokumentiert ist. Die meisten Parser behalten veränderlichen Zustand (z. B. DOM‑Bäume), sodass das Teilen einer Instanz normalerweise zu **Concurrency‑Problemen in Java** führt. Das hier gezeigte Muster – eine Instanz pro Thread – ist die sicherste Vorgabe.

**Muss ich irgendetwas synchronisieren?**  
Nein. Da jeder Thread mit seiner eigenen `HTMLDocument` arbeitet, gibt es keinen gemeinsam veränderlichen Zustand, den man schützen müsste. Das einzige geteilte Element ist der URL‑String, der unveränderlich ist.

**Wie würde das mit einem `ExecutorService` aussehen?**  

```java
ExecutorService executor = Executors.newFixedThreadPool(4);
for (int i = 0; i < 4; i++) {
    executor.submit(task);
}
executor.shutdown();
executor.awaitTermination(1, TimeUnit.MINUTES);
```

Die Kernlogik bleibt identisch; der Pool verwaltet lediglich die Lebenszyklen der Threads für Sie.

---

## Pro‑Tipps für produktionsreife Multithreading‑Anwendungen

1. **Thread‑Anzahl begrenzen** – das Erzeugen Dutzender roher `Thread`‑Objekte kann das OS überlasten. Verwenden Sie stattdessen einen begrenzten Thread‑Pool.  
2. **Unveränderliche Konfiguration bevorzugen** – halten Sie URLs, Dateipfade und Parser‑Einstellungen unveränderlich, damit Sie sie nie versehentlich von einem Worker aus mutieren.  
3. **Ressourcennutzung überwachen** – selbst mit `try‑with‑resources` kann das gleichzeitige Öffnen vieler Dateien Dateideskriptoren erschöpfen. Drosseln Sie die Anzahl gleichzeitiger Aufgaben, wenn Sie an Grenzen stoßen.  
4. **Graceful Shutdown** – schließen Sie Ihren Executor immer oder joinen Sie Ihre Threads, damit die JVM sauber beendet werden kann.

---

## Fazit

Sie haben jetzt ein solides, copy‑and‑paste‑fertiges Muster, wie man **mehrere Threads in Java ausführen** kann, während man sicher **try‑with‑resources in Java verwendet**, **HTML‑Dokument in Java lädt** und **Concurrency‑Probleme in Java vermeidet**. Die zentrale Erkenntnis ist einfach: Jeder Thread bekommt seine eigene Dokument‑Instanz, `try‑with‑resources` übernimmt das Aufräumen, und geteilte Daten bleiben unveränderlich.

Von hier aus können Sie folgendes erkunden:

- Das Muster mit `ExecutorService` und einer Work‑Queue skalieren.  
- Auf einen echten HTML‑Parser wie *jsoup* umsteigen (der ebenfalls `Closeable` implementiert).  
- Anspruchsvollere Fehlerbehandlung oder Retry‑Logik für fehleranfällige I/O hinzufügen.

Probieren Sie es aus, variieren Sie die Anzahl der Worker und beobachten Sie, wie die Konsolenausgabe ordentlich bleibt – kein

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}