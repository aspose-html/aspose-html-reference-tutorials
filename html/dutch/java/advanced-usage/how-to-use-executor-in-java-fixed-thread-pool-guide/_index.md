---
category: general
date: 2026-05-28
description: Hoe je een executor in Java gebruikt met een vaste threadpool, tekst
  uit HTML haalt en de verwerking versnelt – een compleet Java threadpool‑voorbeeld.
draft: false
keywords:
- how to use executor
- fixed thread pool java
- extract text from html
- java thread pool example
- create fixed thread pool
language: nl
og_description: Hoe gebruik je executor in Java met een vaste threadpool. Leer een
  compleet Java‑threadpoolvoorbeeld dat efficiënt tekst uit HTML‑bestanden extraheert.
og_title: Hoe gebruik je Executor in Java – Gids voor vaste threadpool
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
title: Hoe Executor in Java te gebruiken – Gids voor een vaste threadpool
url: /nl/java/advanced-usage/how-to-use-executor-in-java-fixed-thread-pool-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Executor te gebruiken in Java – Gids voor vaste threadpool

Heb je je ooit afgevraagd **how to use executor** om veel taken tegelijk uit te voeren zonder je geheugen te overbelasten? Je bent niet de enige. In veel real‑world apps moet je een map met HTML‑bestanden doorzoeken, de body‑tekst eruit halen, en dat snel doen — precies het scenario dat deze tutorial oplost.

We lopen door een **fixed thread pool java** implementatie die tekst uit HTML extraheert, het tekenaantal van elk bestand afdrukt, en netjes afsluit. Tegen het einde heb je een zelfstandige **java thread pool example** die je in elk project kunt gebruiken, plus een paar tips over het aanpassen van de poolgrootte en het afhandelen van randgevallen.

> **Wat je nodig hebt**  
> * Java 17 (of een recente JDK)  
> * Een kleine HTML‑parsing bibliotheek – we gebruiken *jsoup* omdat het beproefd is en zero‑config.  
> * Een handvol voorbeeld *.html* bestanden in een map naar keuze.

---

## Hoe Executor te gebruiken met een vaste threadpool

Het hart van elk concurrency‑zwaar Java‑programma is de `ExecutorService`. Door een **fixed thread pool** te maken, vertellen we de JVM om precies N worker‑threads actief te houden, wat thread‑creatie‑overhead voorkomt en het resource‑gebruik beperkt.

```java
// Step 1: Build a fixed‑size thread pool (4 workers in this case)
ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Waarom dit belangrijk is:*  
Als je voor elk HTML‑bestand een nieuwe `Thread` startte, zou het OS tientallen threads moeten plannen op een bescheiden laptop, wat leidt tot context‑switch thrashing. Een vaste pool hergebruikt dezelfde vier threads, waardoor je voorspelbaar CPU‑gebruik krijgt.

---

## Definieer de HTML‑bestanden om te verwerken – Fixed Thread Pool Java

Vervolgens sommen we de bestanden op die we in de pool willen stoppen. In een echte app zou je waarschijnlijk een mapboom doorlopen; hier houden we het simpel.

```java
// Step 2: List the HTML documents you want to parse
List<String> htmlFilePaths = List.of(
        "YOUR_DIRECTORY/a.html",
        "YOUR_DIRECTORY/b.html",
        "YOUR_DIRECTORY/c.html",
        "YOUR_DIRECTORY/d.html"
);
```

*Tip:* `List.of` retourneert een onveranderlijke lijst, die veilig gedeeld kan worden tussen threads zonder extra synchronisatie.

---

## Dien een aparte taak in voor elk HTML‑bestand

Nu geven we elk pad door aan de executor. De lambda die we indienen zal **parallel** draaien op een van de vier worker‑threads.

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

**Waarom we de logica in een methode wikkelen** (`extractBodyText`) wordt duidelijk in de volgende sectie — het houdt de lambda overzichtelijk en laat ons de extractiecode elders hergebruiken.

---

## Tekst extraheren uit HTML – De kernlogica

Hier is de herbruikbare helper die daadwerkelijk **extracts text from html** gebruikt met Jsoup. Het opent het bestand, parseert de DOM, en retourneert de platte body‑tekst.

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

*Waarom Jsoup?* Het is lichtgewicht, verwerkt misvormde markup gracieus, en vereist geen volledige browser‑engine. De methode gooit `IOException` zodat de aanroeper kan bepalen hoe te loggen of te herstellen — perfect voor een thread‑pool scenario waarin je niet wilt dat één slecht bestand de hele executor beëindigt.

---

## Sluit de Executor netjes af – Maak vaste threadpool

Nadat we elke taak hebben ingediend, moeten we de pool vertellen geen nieuw werk meer te accepteren en af te ronden wat al in de wachtrij staat.

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

*Uitleg:* `shutdown()` voorkomt nieuwe inzendingen, terwijl `awaitTermination` blokkeert tot elke parse‑taak eindigt (of de timeout verloopt). Als iets vastloopt, probeert `shutdownNow()` lopende taken te annuleren. Dit patroon is de aanbevolen manier om **create fixed thread pool** veilig te maken.

---

## Volledig, uitvoerbaar voorbeeld

Alles samenvoegend, hier is een enkel bestand dat je kunt compileren en uitvoeren. Het bevat de benodigde imports, de `main`‑methode, en de hierboven beschreven helper.

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

**Verwachte output** (ervan uitgaande dat elk bestand ongeveer 1 200 tekens body‑tekst bevat):

```
YOUR_DIRECTORY/a.html → 1234 chars
YOUR_DIRECTORY/b.html → 1198 chars
YOUR_DIRECTORY/c.html → 1305 chars
YOUR_DIRECTORY/d.html → 1120 chars
```

Als een bestand ontbreekt of misvormd is, zie je een stack‑trace afgedrukt naar `stderr`, maar de andere taken gaan ongestoord verder — precies wat een goed‑gedragen **java thread pool example** zou moeten doen.

---

## Veelgestelde vragen & randgevallen

| Vraag | Antwoord |
|----------|--------|
| *Wat als ik meer dan vier bestanden heb?* | De pool zal de extra taken in de wachtrij plaatsen en ze uitvoeren zodra een thread vrij is. Geen extra code nodig. |
| *Moet ik in plaats daarvan `newCachedThreadPool` gebruiken?* | `newCachedThreadPool` maakt threads op aanvraag aan en kan onbeperkt groeien, wat riskant is voor I/O‑zware taken. Een **fixed thread pool** geeft je voorspelbaar geheugen- en CPU‑gebruik. |
| *Hoe wijzig ik de poolgrootte op basis van CPU‑kernen?* | `int cores = Runtime.getRuntime().availableProcessors(); ExecutorService exec = Executors.newFixedThreadPool(cores);` is een veelvoorkomend patroon. |
| *Wat als het parseren mislukt voor één bestand?* | De `catch (IOException e)` binnen de lambda isoleert de fout, logt deze, en laat de rest van de pool blijven werken. |
| *Kan ik de geëxtraheerde tekst teruggeven aan de aanroeper?* | Ja — gebruik `Future<String>` in plaats van `submit(Runnable)`. De code zou er zo uitzien `Future<String> f = executor.submit(() -> extractBodyText(path));` en later `String result = f.get();`. |

---

## Conclusie

We hebben **how to use executor** behandeld om een **fixed thread pool java** op te zetten die een collectie HTML‑bestanden parallel verwerkt, hun body‑tekst extraheert, en het tekenaantal rapporteert. Het volledige **java thread pool example** toont correct resource‑beheer, foutafhandeling, en een herbruikbare extractiemethode.

Volgende stappen? Probeer de `extractBodyText`‑implementatie te vervangen door een meer geavanceerde scraper, experimenteer met een grotere poolgrootte, of voer de resultaten in een database in. Je kunt ook `CompletionService` verkennen om resultaten op te halen zodra ze klaar zijn, wat handig is wanneer bestandsgroottes sterk variëren.

Voel je vrij om het directory‑pad aan te passen, meer bestanden toe te voegen, of dit fragment in een groter crawling‑framework te integreren. Het kernpatroon — maak een pool, dien onafhankelijke taken in, en sluit netjes af — blijft hetzelfde, ongeacht hoe complex je workload wordt.

Veel programmeerplezier, en moge je threads altijd blijven draaien (totdat je ze afsluit, natuurlijk)!

## Gerelateerde tutorials

- [Fixed thread pool java – Parallel HTML Cleaning met ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [Hoe HTML te queryen in Java – Complete tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Hoe Aspose.HTML voor Java te gebruiken - Mastering HTML5 Canvas Rendering](/html/english/java/html5-canvas-rendering/html5-canvas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}