---
category: general
date: 2026-02-21
description: Hoe je ExecutorService gebruikt om HTML snel naar PNG te converteren.
  Leer HTML‑bestanden in batch te converteren met parallelle taken in Java.
draft: false
keywords:
- how to use executorservice
- convert html to png
- how to run parallel tasks
- how to convert html to png
- batch convert html files
language: nl
og_description: Hoe je ExecutorService gebruikt om HTML‑bestanden batchgewijs naar
  PNG te converteren. Stapsgewijze handleiding met volledig Java‑voorbeeld.
og_title: Hoe ExecutorService te gebruiken voor parallelle HTML‑naar‑PNG-conversie
tags:
- Java
- concurrency
- Aspose.HTML
- image‑conversion
title: Hoe ExecutorService te gebruiken voor parallelle HTML‑naar‑PNG batchconversie
url: /nl/java/conversion-html-to-various-image-formats/how-to-use-executorservice-for-parallel-html-to-png-batch-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe ExecutorService te gebruiken voor parallelle HTML‑naar‑PNG batchconversie

Heb je je ooit afgevraagd **hoe je ExecutorService kunt gebruiken** wanneer je een map vol HTML‑pagina's hebt die PNG‑afbeeldingen moeten worden? Je bent niet de enige—veel ontwikkelaars lopen tegen dit probleem aan wanneer hun web‑reporting‑pipeline vastloopt in een single‑threaded conversielus.  

Het goede nieuws? Met een paar regels Java en de krachtige Aspose.HTML `Converter` kun je een pool van werkthread‑s opzetten, elk HTML‑bestand aan de converter voeren, en de afbeeldingen parallel laten verschijnen. In deze tutorial behandelen we ook de basisprincipes van **convert html to png**, laten we je zien hoe je **run parallel tasks** uitvoert, en geven we je een kant‑klaar **batch convert html files**‑script.

## Vereisten

- Java 17 of hoger (de code maakt gebruik van de moderne `java.nio.file` API).  
- Aspose.HTML for Java bibliotheek op je classpath. Je kunt deze ophalen van Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

- Een map die de bron‑`.html`‑bestanden bevat en een lege uitvoermap.  
- Een bescheiden hoeveelheid RAM—elke conversie draait in een eigen thread, dus de pool‑grootte moet overeenkomen met het aantal CPU‑kernen dat je hebt.

> **Pro tip:** Als je op een machine met hyper‑threading werkt, geeft `Runtime.getRuntime().availableProcessors()` meestal het optimale aantal kernen terug.

## Stap 1 – Definieer invoer‑ en uitvoer‑paden

Eerst moeten we Java vertellen waar de HTML zich bevindt en waar de PNG‑s naartoe moeten. Het gebruik van `Path`‑objecten houdt de code platform‑onafhankelijk.

```java
import java.nio.file.*;

public class ParallelBatchConversion {
    public static void main(String[] args) throws Exception {
        // Input folder containing .html files
        Path inputDir  = Paths.get("YOUR_DIRECTORY/input/html");
        // Output folder for the generated .png files
        Path outputDir = Paths.get("YOUR_DIRECTORY/output/png");

        // Ensure the output folder exists
        Files.createDirectories(outputDir);
```

> **Waarom dit belangrijk is:** Het vooraf aanmaken van de uitvoermap voorkomt `FileNotFoundException` wanneer de eerste werkthread probeert een bestand te schrijven.

## Stap 2 – Bouw een thread‑pool met vaste grootte

Het hart van **how to use ExecutorService** ligt in het creëren van een pool die bij je hardware past. Een *vaste* pool garandeert dat we niet meer threads starten dan we daadwerkelijk kunnen uitvoeren.

```java
        // Create a thread pool sized to the number of available CPU cores
        ExecutorService pool = Executors.newFixedThreadPool(
                Runtime.getRuntime().availableProcessors());
```

> **Uitleg:** `ExecutorService` abstraheert het beheer van low‑level threads. Door `newFixedThreadPool` te gebruiken, laten we de JVM threads hergebruiken, wat de overhead van constant creëren en vernietigen vermindert.

## Stap 3 – Dien één conversietaak per HTML‑bestand in

Nu lopen we door de invoermap, selecteren we elk `*.html`‑bestand en geven we het aan de pool door. Elke taak is een kleine lambda die `Converter.convert` aanroept.

```java
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(inputDir, "*.html")) {
            for (Path htmlFile : stream) {
                pool.submit(() -> {
                    try {
                        // Build the output filename by swapping .html for .png
                        String outputFile = outputDir.resolve(
                                htmlFile.getFileName().toString().replaceAll("\\.html$", ".png"))
                                .toString();

                        // Perform the actual conversion
                        Converter.convert(htmlFile.toString(), outputFile);
                        System.out.println("Converted: " + htmlFile.getFileName());
                    } catch (Exception e) {
                        System.err.println("Failed: " + htmlFile.getFileName()
                                           + " – " + e.getMessage());
                    }
                });
            }
        }
```

### Wat gebeurt er onder de motorkap?

1. **DirectoryStream** leest bestandsnamen lui, zodat het geheugenverbruik laag blijft, zelfs bij duizenden bestanden.  
2. De lambda vangt `htmlFile` en `outputDir` op—geen aparte `Runnable`‑klasse nodig.  
3. `Converter.convert` is een blokkerende oproep die de HTML leest, rendert en een PNG schrijft. Omdat elke oproep in een eigen thread draait, worden meerdere bestanden gelijktijdig verwerkt—precies het gedrag dat je verwacht bij het **run parallel tasks**.

## Stap 4 – Sluit de pool netjes af

Nadat alle taken in de wachtrij staan, vertellen we de pool om geen nieuw werk meer te accepteren en wachten we tot alles is voltooid. Als iets blijft hangen, wordt de timeout na een uur afgebroken, wat ruim voldoende is voor de meeste batch‑taken.

```java
        // No more tasks will be submitted
        pool.shutdown();

        // Wait up to 1 hour for all conversions to complete
        if (!pool.awaitTermination(1, TimeUnit.HOURS)) {
            System.err.println("Timeout: some files didn't finish in time.");
        }

        System.out.println("All conversions completed.");
    }
}
```

> **Randgeval:** Als je uitzonderlijk grote HTML‑bestanden hebt, wil je misschien de timeout verhogen of het geheugenverbruik monitoren. Het toevoegen van `pool.setRejectedExecutionHandler(new ThreadPoolExecutor.CallerRunsPolicy())` dwingt de aanroepende thread om overtollige taken uit te voeren, waardoor `RejectedExecutionException` wordt voorkomen.

## Volledig, kant‑klaar voorbeeld

Hieronder staat het volledige programma, klaar om te kopiëren en te plakken in een enkel `ParallelBatchConversion.java`‑bestand.

```java
import com.aspose.html.converters.Converter;
import java.nio.file.*;
import java.util.concurrent.*;

public class ParallelBatchConversion {
    public static void main(String[] args) throws Exception {
        // Step 1: Define source and destination folders
        Path inputDir  = Paths.get("YOUR_DIRECTORY/input/html");
        Path outputDir = Paths.get("YOUR_DIRECTORY/output/png");
        Files.createDirectories(outputDir);

        // Step 2: Create a thread pool sized to the available CPU cores
        ExecutorService pool = Executors.newFixedThreadPool(
                Runtime.getRuntime().availableProcessors());

        // Step 3: Submit a conversion task for each HTML file found
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(inputDir, "*.html")) {
            for (Path htmlFile : stream) {
                pool.submit(() -> {
                    try {
                        String outputFile = outputDir.resolve(
                                htmlFile.getFileName().toString().replaceAll("\\.html$", ".png"))
                                .toString();
                        Converter.convert(htmlFile.toString(), outputFile);
                        System.out.println("Converted: " + htmlFile.getFileName());
                    } catch (Exception e) {
                        System.err.println("Failed: " + htmlFile.getFileName()
                                           + " – " + e.getMessage());
                    }
                });
            }
        }

        // Step 4: Shut down the pool and wait for all conversions to finish
        pool.shutdown();
        if (!pool.awaitTermination(1, TimeUnit.HOURS)) {
            System.err.println("Timeout: some files didn't finish in time.");
        }
        System.out.println("All conversions completed.");
    }
}
```

### Verwachte output

Het uitvoeren van het programma print een regel voor elke succesvolle conversie:

```
Converted: report1.html
Converted: dashboard.html
Converted: summary.html
All conversions completed.
```

Als een bestand faalt, zie je een foutregel met het exceptiebericht, waardoor debuggen eenvoudig is.

## Hoe dit patroon uit te breiden

- **Verschillende afbeeldingsformaten:** Vervang de `.png`‑extensie door `.jpg` of `.bmp` en pas de Aspose‑conversie‑opties dienovereenkomstig aan.  
- **Dynamisch aantal threads:** Voor I/O‑gebonden workloads kun je de pool‑grootte verhogen (`availableProcessors() * 2`).  
- **Voortgangsmonitoring:** Vervang `System.out.println` door een thread‑veilige voortgangsbalkbibliotheek zoals `jline` of log naar een bestand.  
- **Foutafhandeling:** Verzamel mislukte paden in een `List<Path>` en probeer ze opnieuw nadat de hoofdloop is voltooid.

## Veelgestelde vragen

**Q: Werkt dit op Windows en Linux?**  
A: Ja. `java.nio.file` abstraheert het onderliggende bestandssysteem, dus dezelfde code draait ongewijzigd op elk OS dat Java ondersteunt.

**Q: Wat als ik meer dan 10 000 HTML‑bestanden heb?**  
A: De `DirectoryStream`‑iterator leest items lui, zodat het geheugen laag blijft. Zorg er alleen voor dat je schijf voldoende vrije ruimte heeft voor de PNG‑output.

**Q: Kan ik het geheugen beperken dat elke conversie gebruikt?**  
A: Aspose.HTML stelt je in staat de renderengine te configureren via `HtmlLoadOptions` en `ImageSaveOptions`. Je kunt een maximale bitmap‑grootte instellen of low‑quality rendering inschakelen om het RAM‑verbruik onder controle te houden.

## Conclusie

We hebben stap voor stap **how to use ExecutorService** doorlopen om **batch convert html files** naar PNG‑afbeeldingen te converteren, uitgelegd waarom een pool met vaste grootte de ideale keuze is voor CPU‑gebonden rendering, en je een compleet, kopieer‑en‑plakbaar Java‑programma gegeven. Door de bovenstaande stappen te volgen, verander je een trage, single‑threaded lus in een snelle, schaalbare pipeline die duizenden bestanden met één commando aankan.

Klaar voor de volgende uitdaging? Probeer `Converter.convert` te vervangen door de PDF‑export van Aspose om **convert html to pdf** te doen, of integreer deze logica in een Spring Boot‑microservice die upload‑en‑convert‑verzoeken accepteert. Het kernidee—het gebruik van `ExecutorService` om **run parallel tasks** uit te voeren—blijft hetzelfde, en je zult het nuttig vinden in talloze batch‑verwerkingsscenario's.

Veel plezier met coderen, en moge je threads altijd levend blijven! 

![how to use executorservice diagram](placeholder.png "Diagram illustrating the thread pool workflow for parallel HTML‑to‑PNG conversion")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}