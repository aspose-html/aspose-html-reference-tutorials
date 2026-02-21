---
category: general
date: 2026-02-21
description: Jak použít ExecutorService k rychlé konverzi HTML na PNG. Naučte se hromadně
  převádět HTML soubory pomocí paralelních úloh v Javě.
draft: false
keywords:
- how to use executorservice
- convert html to png
- how to run parallel tasks
- how to convert html to png
- batch convert html files
language: cs
og_description: Jak použít ExecutorService k hromadnému převodu HTML souborů na PNG.
  Krok za krokem průvodce s kompletním Java příkladem.
og_title: Jak použít ExecutorService pro paralelní konverzi HTML na PNG
tags:
- Java
- concurrency
- Aspose.HTML
- image‑conversion
title: Jak použít ExecutorService pro paralelní hromadnou konverzi HTML na PNG
url: /cs/java/conversion-html-to-various-image-formats/how-to-use-executorservice-for-parallel-html-to-png-batch-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat ExecutorService pro paralelní hromadnou konverzi HTML‑to‑PNG

Už jste se někdy zamysleli **jak používat ExecutorService**, když máte složku plnou HTML stránek, které mají být převedeny na PNG obrázky? Nejste v tom sami — mnoho vývojářů narazí na tuto překážku, když jejich pipeline pro web‑reporting uvízne v jednovláknové smyčce konverze.  

Dobrá zpráva? S několika řádky Javy a výkonným Aspose.HTML `Converter` můžete spustit bazén pracovních vláken, předat každému HTML souboru konvertor a sledovat, jak se obrázky vytvářejí paralelně. V tomto tutoriálu se také dotkneme základů **convert html to png**, ukážeme vám, jak **run parallel tasks**, a poskytneme vám připravený **batch convert html files** skript.

## Požadavky

- Java 17 nebo novější (kód používá moderní API `java.nio.file`).  
- Knihovna Aspose.HTML pro Java ve vaší classpath. Můžete ji získat z Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

- Adresář, který obsahuje zdrojové soubory `.html`, a prázdná výstupní složka.  
- Rozumné množství RAM — každá konverze běží ve svém vlastním vlákně, takže velikost poolu by měla odpovídat počtu jader CPU, které máte.

> **Pro tip:** Pokud používáte stroj s hyper‑threadingem, `Runtime.getRuntime().availableProcessors()` obvykle vrací optimální počet jader.

## Krok 1 – Definování vstupních a výstupních cest

Nejprve musíme Jave říct, kde se HTML nachází a kam mají být PNG soubory uloženy. Použití objektů `Path` udržuje kód nezávislý na platformě.

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

> **Proč je to důležité:** Vytvoření výstupního adresáře předem zabraňuje `FileNotFoundException`, když se první pracovní vlákno pokusí zapsat soubor.

## Krok 2 – Vytvoření pevně velkého thread poolu

Jádrem **how to use ExecutorService** je vytvoření poolu, který odpovídá vašemu hardware. *Pevný* pool zaručuje, že nebudeme vytvářet více vláken, než dokážeme skutečně spustit.

```java
        // Create a thread pool sized to the number of available CPU cores
        ExecutorService pool = Executors.newFixedThreadPool(
                Runtime.getRuntime().availableProcessors());
```

> **Vysvětlení:** `ExecutorService` abstrahuje nízkoúrovňovou správu vláken. Použitím `newFixedThreadPool` umožníme JVM znovu používat vlákna, což snižuje režii spojenou s neustálým vytvářením a ničením vláken.

## Krok 3 – Odeslání jedné konverzní úlohy na každý HTML soubor

Nyní projdeme vstupní adresář, vybereme každý soubor `*.html` a předáme jej poolu. Každá úloha je malá lambda, která volá `Converter.convert`.

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

### Co se děje pod kapotou?

1. **DirectoryStream** líně čte názvy souborů, takže i při tisících souborech zůstává spotřeba paměti nízká.  
2. Lambda zachytává `htmlFile` a `outputDir` — není potřeba samostatná třída `Runnable`.  
3. `Converter.convert` je blokující volání, které načte HTML, vykreslí jej a zapíše PNG. Protože každé volání běží ve svém vlastním vlákně, zpracovává se více souborů současně — přesně to chování, které očekáváte při **run parallel tasks**.

## Krok 4 – Elegantní ukončení poolu

Po zařazení všech úloh do fronty řekneme poolu, aby nepřijímal novou práci a čekal, až vše dokončí. Pokud něco visí, časový limit po hodině přeruší operaci, což je velkorysé pro většinu hromadných úloh.

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

> **Okrajový případ:** Pokud máte výjimečně velké HTML soubory, možná budete chtít zvýšit časový limit nebo sledovat využití paměti. Přidání `pool.setRejectedExecutionHandler(new ThreadPoolExecutor.CallerRunsPolicy())` nutí vlákno volajícího spouštět přebytečné úlohy, čímž se zabrání `RejectedExecutionException`.

## Kompletní, připravený k spuštění příklad

Níže je celý program, který lze zkopírovat a vložit do jediného souboru `ParallelBatchConversion.java`.

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

### Očekávaný výstup

Spuštění programu vypíše řádek pro každou úspěšnou konverzi:

```
Converted: report1.html
Converted: dashboard.html
Converted: summary.html
All conversions completed.
```

Pokud soubor selže, uvidíte řádek s chybou a zprávou výjimky, což usnadní ladění.

## Jak rozšířit tento vzor

- **Různé formáty obrázků:** Zaměňte příponu `.png` za `.jpg` nebo `.bmp` a podle toho upravte možnosti konverze v Aspose.  
- **Dynamický počet vláken:** Pro I/O‑vázané úlohy můžete zvýšit velikost poolu (`availableProcessors() * 2`).  
- **Sledování průběhu:** Nahraďte `System.out.println` knihovnou pro vlákny‑bezpečný progress bar, jako je `jline`, nebo logujte do souboru.  
- **Zpracování chyb:** Shromažďujte neúspěšné cesty do `List<Path>` a po dokončení hlavní smyčky je zkuste znovu.

## Často kladené otázky

**Q: Funguje to na Windows i Linuxu?**  
A: Ano. `java.nio.file` abstrahuje podkladový souborový systém, takže stejný kód běží beze změny na jakémkoli OS, který podporuje Javu.

**Q: Co když mám více než 10 000 HTML souborů?**  
A: Iterátor `DirectoryStream` čte položky líně, takže paměť zůstává nízká. Jen se ujistěte, že máte na disku dostatek volného místa pro výstup PNG.

**Q: Můžu omezit paměť, kterou každá konverze používá?**  
A: Aspose.HTML vám umožňuje konfigurovat renderovací engine pomocí `HtmlLoadOptions` a `ImageSaveOptions`. Můžete nastavit maximální velikost bitmapy nebo povolit nízkou kvalitu renderování, aby byl spotřeba RAM pod kontrolou.

## Závěr

Prošli jsme **how to use ExecutorService** k **batch convert html files** do PNG obrázků, vysvětlili, proč je pevně velký pool ideální pro CPU‑vázané renderování, a poskytli vám kompletní, zkopírovatelný Java program. Dodržením výše uvedených kroků přeměníte pomalou jednovláknovou smyčku na rychlý, škálovatelný pipeline, který dokáže zpracovat tisíce souborů jedním příkazem.

Jste připraveni na další výzvu? Zkuste nahradit `Converter.convert` exportem PDF od Aspose pro **convert html to pdf**, nebo integrujte tuto logiku do microservice Spring Boot, která přijímá požadavky na nahrání‑a‑konverzi. Hlavní myšlenka — používání `ExecutorService` k **run parallel tasks** — zůstává stejná a zjistíte, že je užitečná v nesčetných scénářích hromadného zpracování.

Šťastné programování a ať vaše vlákna vždy běží! 

![jak používat executorservice diagram](placeholder.png "Diagram ilustrující workflow thread poolu pro paralelní konverzi HTML‑to‑PNG")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}