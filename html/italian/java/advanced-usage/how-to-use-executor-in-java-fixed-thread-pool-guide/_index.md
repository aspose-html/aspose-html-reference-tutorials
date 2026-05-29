---
category: general
date: 2026-05-28
description: come usare executor in Java con un pool di thread fisso, estrarre testo
  da HTML e velocizzare l'elaborazione – un esempio completo di pool di thread Java.
draft: false
keywords:
- how to use executor
- fixed thread pool java
- extract text from html
- java thread pool example
- create fixed thread pool
language: it
og_description: come usare executor in Java con un pool di thread fisso. Scopri un
  esempio completo di pool di thread Java che estrae testo dai file HTML in modo efficiente.
og_title: Come utilizzare Executor in Java – Guida al pool di thread fisso
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
title: Come usare Executor in Java – Guida al pool di thread fisso
url: /it/java/advanced-usage/how-to-use-executor-in-java-fixed-thread-pool-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare Executor in Java – Guida al pool di thread fisso

Ti sei mai chiesto **come usare executor** per eseguire molti compiti contemporaneamente senza far esplodere la memoria? Non sei solo. In molte applicazioni reali dovrai scansionare una cartella di file HTML, estrarre il testo del body e farlo rapidamente—esattamente lo scenario che questo tutorial risolve.

Passeremo in rassegna un'implementazione **fixed thread pool java** che estrae testo da HTML, stampa il conteggio dei caratteri di ogni file e si chiude correttamente. Alla fine avrai un **java thread pool example** autonomo che potrai inserire in qualsiasi progetto, oltre a qualche consiglio su come personalizzare la dimensione del pool e gestire i casi limite.

> **Cosa ti servirà**  
> * Java 17 (o qualsiasi JDK recente)  
> * Una piccola libreria di parsing HTML – useremo *jsoup* perché è collaudata e zero‑config.  
> * Una manciata di file *.html* di esempio in una directory a tua scelta.

---

## Come usare Executor con un pool di thread fisso

Il cuore di qualsiasi programma Java pesante di concorrenza è il `ExecutorService`. Creando un **fixed thread pool** diciamo alla JVM di mantenere esattamente N thread worker attivi, il che previene l'overhead di creazione dei thread e limita l'uso delle risorse.

```java
// Step 1: Build a fixed‑size thread pool (4 workers in this case)
ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Perché è importante:*  
Se avessi lanciato un nuovo `Thread` per ogni file HTML, il sistema operativo avrebbe dovuto schedulare decine di thread su un laptop modesto, portando a un eccessivo thrashing di context‑switch. Un pool fisso riutilizza gli stessi quattro thread, garantendoti un utilizzo della CPU prevedibile.

---

## Definire i file HTML da elaborare – Fixed Thread Pool Java

Successivamente elenchiamo i file che vogliamo passare al pool. In un'app reale probabilmente percorreresti un albero di directory; qui lo manteniamo semplice.

```java
// Step 2: List the HTML documents you want to parse
List<String> htmlFilePaths = List.of(
        "YOUR_DIRECTORY/a.html",
        "YOUR_DIRECTORY/b.html",
        "YOUR_DIRECTORY/c.html",
        "YOUR_DIRECTORY/d.html"
);
```

*Suggerimento:* `List.of` restituisce una lista immutabile, che è sicura da condividere tra thread senza sincronizzazione aggiuntiva.

---

## Inviare un compito separato per ogni file HTML

Ora passiamo ogni percorso all'executor. La lambda che inviamo verrà eseguita **in parallelo** su uno dei quattro thread worker.

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

**Perché avvolgiamo la logica in un metodo** (`extractBodyText`) diventerà chiaro nella sezione successiva—mantiene la lambda ordinata e ci permette di riutilizzare il codice di estrazione altrove.

---

## Estrarre testo da HTML – La logica centrale

Ecco l'helper riutilizzabile che effettivamente **estrae testo da html** usando Jsoup. Apre il file, analizza il DOM e restituisce il testo plain del body.

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

*Perché Jsoup?* È leggero, gestisce markup malformato in modo elegante e non richiede un motore browser completo. Il metodo lancia `IOException` così il chiamante può decidere come loggare o recuperare—perfetto per uno scenario di pool di thread dove non vuoi che un singolo file difettoso termini l'intero executor.

---

## Chiudere l'Executor in modo corretto – Create Fixed Thread Pool

Dopo aver inviato tutti i job, dobbiamo dire al pool di non accettare più lavoro e di terminare ciò che è già in coda.

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

*Spiegazione:* `shutdown()` impedisce nuove sottomissioni, mentre `awaitTermination` blocca fino al completamento di ogni job di parsing (o fino alla scadenza del timeout). Se qualcosa si blocca, `shutdownNow()` tenta di annullare i task in esecuzione. Questo pattern è il modo consigliato per **create fixed thread pool** in sicurezza.

---

## Esempio completo, eseguibile

Mettendo tutto insieme, ecco un singolo file che puoi compilare ed eseguire. Include le import necessarie, il metodo `main` e l'helper descritto sopra.

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

**Output previsto** (supponendo che ogni file contenga circa 1 200 caratteri di testo nel body):

```
YOUR_DIRECTORY/a.html → 1234 chars
YOUR_DIRECTORY/b.html → 1198 chars
YOUR_DIRECTORY/c.html → 1305 chars
YOUR_DIRECTORY/d.html → 1120 chars
```

Se qualche file è mancante o malformato, vedrai una stack trace stampata su `stderr`, ma gli altri task continueranno indisturbati—esattamente ciò che dovrebbe fare un **java thread pool example** ben comportato.

---

## Domande comuni & casi limite

| Domanda | Risposta |
|----------|--------|
| *E se ho più di quattro file?* | Il pool accoderà i task extra e li eseguirà non appena un thread sarà libero. Nessun codice aggiuntivo necessario. |
| *Dovrei usare `newCachedThreadPool` invece?* | `newCachedThreadPool` crea thread su richiesta e può crescere indefinitamente, il che è rischioso per job I/O‑heavy. Un **fixed thread pool** ti offre un utilizzo prevedibile di memoria e CPU. |
| *Come cambio la dimensione del pool in base ai core CPU?* | `int cores = Runtime.getRuntime().availableProcessors(); ExecutorService exec = Executors.newFixedThreadPool(cores);` è un pattern comune. |
| *E se il parsing fallisce per un file?* | Il `catch (IOException e)` all'interno della lambda isola il fallimento, lo logga e permette al resto del pool di continuare a lavorare. |
| *Posso restituire il testo estratto al chiamante?* | Sì—usa `Future<String>` invece di `submit(Runnable)`. Il codice sarebbe così: `Future<String> f = executor.submit(() -> extractBodyText(path));` e più tardi `String result = f.get();`. |

---

## Conclusione

Abbiamo coperto **come usare executor** per avviare un **fixed thread pool java** che elabora in parallelo una collezione di file HTML, ne estrae il testo del body e ne riporta il conteggio dei caratteri. L'**java thread pool example** completo dimostra una corretta gestione delle risorse, gestione degli errori e un metodo di estrazione riutilizzabile.

Passi successivi? Prova a sostituire l'implementazione di `extractBodyText` con uno scraper più sofisticato, sperimenta con un pool più grande, o invia i risultati a un database. Potresti anche esplorare `CompletionService` per recuperare i risultati non appena sono pronti, utile quando le dimensioni dei file variano molto.

Sentiti libero di modificare il percorso della directory, aggiungere più file o integrare questo snippet in un framework di crawling più ampio. Il pattern di base—creare un pool, sottomettere task indipendenti e chiudere in modo corretto—rimane lo stesso, indipendentemente dalla complessità del carico di lavoro.

Buon coding, e che i tuoi thread rimangano sempre vivi (finché non li spegni, ovviamente)!

## Tutorial correlati

- [Fixed thread pool java – Parallel HTML Cleaning with ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Use Aspose.HTML for Java - Mastering HTML5 Canvas Rendering](/html/english/java/html5-canvas-rendering/html5-canvas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}