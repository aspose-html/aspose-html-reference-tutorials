---
category: general
date: 2026-04-19
description: Převádějte HTML do PDF rychle pomocí příkladu s Java ExecutorService.
  Naučte se vzor s pevnou velikostí vlákna v Javě pro generování PDF z HTML a bezpečně
  ukončete ExecutorService.
draft: false
keywords:
- convert html to pdf
- java executorservice example
- fixed thread pool java
- generate pdf from html
- shutdown executor service
language: cs
og_description: Efektivně převádějte HTML na PDF pomocí přístupu s pevnou vlákny v
  Javě. Tento průvodce ukazuje kompletní příklad java ExecutorService, jak generovat
  PDF z HTML a správné ukončení ExecutorService.
og_title: Převod HTML na PDF pomocí Java ExecutorService – krok za krokem
tags:
- Java
- Concurrency
- PDF Generation
title: Převod HTML na PDF pomocí Java ExecutorService – Kompletní průvodce
url: /cs/java/conversion-html-to-other-formats/convert-html-to-pdf-with-java-executorservice-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod HTML na PDF pomocí Java ExecutorService – Kompletní průvodce

Už jste někdy potřebovali **převést HTML na PDF**, ale obávali se rychlosti při desítkách souborů? Nejste v tom sami. V mnoha dávkových zpracovacích řetězcích se jednovláknový přístup stává úzkým místem, zejména když je knihovna pro konverzi sama o sobě I/O‑vázaná.

Dobrou zprávou je, že Java `ExecutorService` vám umožní vytvořit **pevný pool vláken** a spouštět mnoho konverzí paralelně, a to vše při zachování čistého kódu a kontroly nad zdroji. V tomto tutoriálu projdeme **java executorservice example**, který **generuje PDF z HTML**, vysvětlí, proč je pevný pool vláken ideální, a ukáže správný způsob **shutdown executor service**, jakmile je vše hotovo.

Na konci tohoto průvodce budete mít připravený program, který vezme seznam HTML souborů, každý z nich převede na PDF pomocí Aspose.HTML a ukončí se elegantně – žádná osiřelá vlákna, žádné úniky paměti.

---

## Co vytvoříte

- Java třídu pojmenovanou `ParallelBatch`, která načte pole cest k HTML souborům.  
- **Pevný pool vláken** (`Executors.newFixedThreadPool`), který zpracovává každou konverzi souběžně.  
- Čisté zacházení s životním cyklem executoru pomocí `shutdown()` a `awaitTermination`.  
- Výstup do konzole potvrzující každý vygenerovaný PDF soubor.

**Požadavky**

- Java 17 nebo novější (kód používá lambda syntaxi).  
- Knihovna Aspose.HTML pro Java ve vašem classpathu (stáhněte z [aspose.com/html/java](https://products.aspose.com/html/java/)).  
- Složka obsahující několik ukázkových `.html` souborů.

Externí nástroje pro sestavení nejsou vyžadovány; můžete kompilovat pomocí `javac` a spustit pomocí `java`. Pokud dáváte přednost Maven nebo Gradle, stačí přidat závislost Aspose.HTML.

## Krok 1: Nastavte svůj projekt a závislosti

### Proč je to důležité

Než se spustí jakýkoli kód, JVM musí najít třídy Aspose.HTML. Chybějící jar soubory způsobí `ClassNotFoundException`, což je častá překážka pro nováčky.

### Jak na to

1. **Vytvořte složku** pojmenovanou `pdf‑converter`.  
2. **Stáhněte** `aspose-html-<version>.jar` a umístěte ji do podsložky `libs`.  
3. **Uspořádejte** svůj zdrojový soubor takto:

```
pdf-converter/
├─ libs/
│  └─ aspose-html-23.10.jar
└─ src/
   └─ ParallelBatch.java
```

Můžete kompilovat pomocí:

```bash
javac -cp "libs/*" src/ParallelBatch.java -d out
```

A spustit pomocí:

```bash
java -cp "out:libs/*" ParallelBatch
```

*(Na Windows nahraďte `:` znakem `;` ve classpathu.)*

## Krok 2: Seznam HTML souborů, které chcete převést

### Úvaha

Pevné zakódování seznamu souborů je v pořádku pro ukázku, ale v produkci byste pravděpodobně prohledávali adresář. Pro jednoduchost ponecháme pole; ukazuje hlavní logiku bez rušení vás I/O kódem.

### Code

```java
// Step 2: Define the source HTML files
String[] htmlFiles = {
    "YOUR_DIRECTORY/1.html",
    "YOUR_DIRECTORY/2.html",
    "YOUR_DIRECTORY/3.html"
};
```

Nahraďte `YOUR_DIRECTORY` absolutní nebo relativní cestou, kde se nacházejí vaše HTML soubory.

## Krok 3: Vytvořte instanci pevného poolu vláken v Javě

### Proč pevný pool?

**Pevný pool vláken** (`newFixedThreadPool`) vám poskytuje předvídatelný počet pracovních vláken. Příliš mnoho vláken může vyčerpat CPU nebo paměť, zatímco příliš málo podvyužívá systém. Pro úlohy náročné na CPU je pravidlem `availableProcessors()`, ale pro I/O‑vázanou konverzi často nejlépe funguje skromný pool 3‑5 vláken.

### Code

```java
// Step 3: Initialise a fixed‑size thread pool (3 threads in this example)
ExecutorService executor = Executors.newFixedThreadPool(3);
```

Klidně upravte velikost poolu podle vašeho hardwaru a velikosti HTML souborů.

## Krok 4: Odeslat úlohu konverze pro každý HTML soubor

### Jak to funguje

Každá úloha je lambda, která:

1. Získá název PDF souboru (`replace(".html", ".pdf")`).  
2. Zavolá `Conversion.convert` z Aspose.HTML.  
3. Vytiskne řádek s potvrzením.

Použití `executor.submit` zajišťuje, že úloha běží na jednom z vláken poolu.

### Code

```java
// Step 4: Enqueue conversion jobs
for (String htmlFilePath : htmlFiles) {
    executor.submit(() -> {
        // Derive the PDF output path
        String pdfFilePath = htmlFilePath.replace(".html", ".pdf");
        // Perform the conversion
        Conversion.convert(htmlFilePath, pdfFilePath);
        // Log the result
        System.out.println(pdfFilePath + " generated.");
    });
}
```

**Tip:** Pokud konverze selže, Aspose vyhodí `Exception`. Můžete obalit tělo do try‑catch a zaznamenat chyby, aniž byste zničili celý pool.

```java
executor.submit(() -> {
    try {
        String pdfFilePath = htmlFilePath.replace(".html", ".pdf");
        Conversion.convert(htmlFilePath, pdfFilePath);
        System.out.println(pdfFilePath + " generated.");
    } catch (Exception e) {
        System.err.println("Failed to convert " + htmlFilePath + ": " + e.getMessage());
    }
});
```

## Krok 5: Elegantně ukončit Executor Service

### Proč elegantní ukončení?

Volání `shutdown()` zabraňuje přijímání nových úloh. `awaitTermination` pak blokuje, dokud všechny úlohy ve frontě nedokončí **nebo** nevyprší časový limit. Tento vzor zajišťuje, že aplikace neukončí, dokud běží pozadí vlákna, což je častý zdroj zkrácených PDF.

### Code

```java
// Step 5: Shut down the pool and wait for completion
executor.shutdown();                       // No new tasks
boolean finished = executor.awaitTermination(5, TimeUnit.MINUTES);

if (finished) {
    System.out.println("All PDFs generated successfully.");
} else {
    System.err.println("Timeout reached before all tasks finished.");
}
```

Můžete zvýšit časový limit, pokud očekáváte velmi velké dokumenty.

## Kompletní funkční příklad

Níže je kompletní, samostatný program. Zkopírujte jej do `src/ParallelBatch.java`, upravte cesty k souborům a spusťte podle popisu v Kroku 1.

```java
import com.aspose.html.Conversion;
import java.util.concurrent.*;

public class ParallelBatch {
    public static void main(String[] args) throws Exception {
        // Step 1: List the HTML files that will be converted to PDF
        String[] htmlFiles = {
            "YOUR_DIRECTORY/1.html",
            "YOUR_DIRECTORY/2.html",
            "YOUR_DIRECTORY/3.html"
        };

        // Step 2: Create a fixed‑size thread pool to run conversions in parallel
        ExecutorService executor = Executors.newFixedThreadPool(3);

        // Step 3: For each HTML file, submit a conversion task to the pool
        for (String htmlFilePath : htmlFiles) {
            executor.submit(() -> {
                try {
                    String pdfFilePath = htmlFilePath.replace(".html", ".pdf");
                    // Convert HTML to PDF using Aspose.HTML
                    Conversion.convert(htmlFilePath, pdfFilePath);
                    System.out.println(pdfFilePath + " generated.");
                } catch (Exception e) {
                    System.err.println("Error converting " + htmlFilePath + ": " + e.getMessage());
                }
            });
        }

        // Step 4: Shut down the executor and wait for all tasks to finish
        executor.shutdown(); // stop accepting new tasks
        boolean terminated = executor.awaitTermination(5, TimeUnit.MINUTES);

        if (terminated) {
            System.out.println("All conversions completed.");
        } else {
            System.err.println("Some tasks did not finish within the timeout.");
        }
    }
}
```

**Očekávaný výstup do konzole** (pořadí se může lišit kvůli paralelismu):

```
YOUR_DIRECTORY/1.pdf generated.
YOUR_DIRECTORY/2.pdf generated.
YOUR_DIRECTORY/3.pdf generated.
All conversions completed.
```

Pokud některý soubor selže, uvidíte řádek s chybou a příčinou, ale ostatní konverze budou pokračovat.

## Časté otázky a okrajové případy

### 1. *Co když mám stovky HTML souborů?*

Zvyšte velikost poolu mírně (např. `Runtime.getRuntime().availableProcessors()`) a zvažte načtení seznamu souborů z adresáře:

```java
Path dir = Paths.get("YOUR_DIRECTORY");
try (Stream<Path> stream = Files.list(dir)) {
    List<String> files = stream
        .filter(p -> p.toString().endsWith(".html"))
        .map(Path::toString)
        .collect(Collectors.toList());
    // feed `files` into the executor loop
}
```

### 2. *Mohu omezit využití paměti?*

Aspose.HTML streamuje zdrojový soubor, ale pokud zpracováváte velmi velké HTML stránky, můžete chtít nastavit vlastní `ConversionOptions` s nižším nastavením `MaxMemory`. Dokumentace API poskytuje přesné názvy vlastností.

### 3. *Co když konverze uvízne?*

Zabalte úlohu do `Future` a použijte `future.get(timeout, TimeUnit.SECONDS)`. Pokud časový limit vyprší, úlohu zrušte:

```java
Future<?> future = executor.submit(task);
try {
    future.get(2, TimeUnit.MINUTES);
} catch (TimeoutException te) {
    future.cancel(true);
    System.err.println("Conversion timed out for " + htmlFilePath);
}
```

### 4. *Funguje to na Windows i Linuxu?*

Ano—`ExecutorService` a Aspose.HTML jsou platformně nezávislé. Jen zajistěte, aby nativní knihovny (pokud existují) byly přístupné přes `java.library.path`.

## Profesionální tipy a úskalí

- **Pro tip:** Znovu použijte jedinou instanci `Conversion`, pokud knihovna podporuje; může to snížit režii vytváření objektů.  
- **Dejte si pozor na:** Pevně zakódované cesty s mezerami. Uzavřete je do uvozovek nebo použijte objekty `Path`, aby nedošlo k `FileNotFoundException`.  
- **Logování:** Nahraďte `System.out.println` vhodným logovacím frameworkem (SLF4J, Log4j) pro produkční úroveň viditelnosti.  
- **Elegantní ukončení:** Vždy zavolejte `shutdown()` *i* když nastane výjimka; blok `try‑finally` zajistí vyčištění poolu.

## Závěr

Právě jsme **převáděli HTML na PDF** pomocí **java executorservice example**, který využívá **pevný pool vláken java**. Kód ukazuje, jak **generovat PDF z HTML**, zacházet s chybami a správně **shutdown executor service** po dokončení veškeré práce.

Tento přístup se dobře škáluje – od tří souborů po tisíce – a zároveň udržuje aplikaci responzivní a šetrnou k prostředkům. Dále můžete zkoumat:

- Přidání **monitorování průběhu** pomocí `CompletionService`.  
- Použití **dynamických poolů vláken** (`newCachedThreadPool`) pro nepředvídatelné zatížení.  
- Integraci konvertoru do **REST API**, aby ostatní služby mohly na vyžádání spouštět generování PDF.

Vyzkoušejte to, upravte velikost poolu a uvidíte, jak rychlejší se vaše dávkové konverze stanou. Šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}