---
category: general
date: 2026-01-01
description: Naučte se, jak použít pevný pool vláken v Javě k odstranění značek script
  z HTML souborů. Tento příklad ExecutorService v Javě ukazuje efektivní načítání
  HTML dokumentů.
draft: false
keywords:
- fixed thread pool java
- remove script tags
- remove javascript html
- executorservice example java
- load html document
language: cs
og_description: Ovládněte pevný thread pool v Javě pro odstraňování značek script
  z HTML souborů. Kompletní příklad ExecutorService v Javě s kroky načtení HTML dokumentu.
og_title: Pevný pool vláken v Javě – Průvodce paralelním čištěním HTML
tags:
- Java concurrency
- HTML processing
- Aspose.HTML
title: Fixní pool vláken v Javě – Paralelní čištění HTML pomocí ExecutorService
url: /cs/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Fixní thread pool java – Paralelní čištění HTML pomocí ExecutorService

Už jste někdy potřebovali **fixed thread pool java** pro zrychlení hromadného zpracování HTML? Nejste v tom sami. Když máte desítky – nebo i stovky – HTML souborů posetých elementy `<script>`, provádění práce sekvenčně může připomínat sledování, jak schne barva.  

V tomto tutoriálu vám ukážeme, jak přesně vytvořit **fixed thread pool java**, načíst každý HTML dokument, odstranit veškerý JavaScript (`<script>` tagy) a uložit vyčištěné soubory – vše paralelně pomocí **executorservice example java**. Na konci budete mít připravený program, který efektivně odstraňuje script tagy, a pochopíte, proč je fixní thread pool často ideální pro úlohy náročné na CPU.

## Co dosáhnete

- Nastavit `ExecutorService` s pevně daným počtem vláken.  
- Načíst HTML soubory pomocí `HTMLDocument` z Aspose.HTML.  
- Použít CSS selektor k **remove script tags** (nebo jiným nechtěným elementům).  
- Uložit vyčištěný výstup s jasnou konvencí pojmenování.  
- Zpracovat vypnutí a elegantní ukončení thread poolu.  

Žádné externí nástroje pro sestavení, žádná skrytá magie – jen čistý Java 8+ a Aspose.HTML.

## Požadavky

Než se ponoříme dál, ujistěte se, že máte:

| Požadavek | Proč je důležité |
|-------------|----------------|
| **Java 8 or newer** | Potřebné pro lambda výrazy a API `ExecutorService`. |
| **Aspose.HTML for Java** (download from <https://products.aspose.com/html/java/>) | Poskytuje třídu `HTMLDocument` používanou k načtení a manipulaci s HTML. |
| **A folder with sample HTML files** | Demo zpracovává soubory jako `input1.html`, `input2.html`, atd. |
| **An IDE or command‑line build tool** (IntelliJ, Eclipse, Maven, Gradle) | Pro kompilaci a spuštění kódu. |

Pokud jste ještě nepřidali Aspose.HTML do svého projektu, vložte JAR do složky `libs` a přidejte jej do classpath, nebo deklarujte Maven závislost:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

## Krok 1: Vytvořte Fixed Thread Pool java

**fixed thread pool java** vám poskytuje předvídatelný počet pracovních vláken, která zůstávají aktivní po celou dobu úlohy. To eliminuje režii neustálého vytváření a ničení vláken, což je zvláště užitečné, když je každá úloha krátkodobá, jako načtení a vyčištění jediného HTML souboru.

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.TimeUnit;

public class ParallelProcessingDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);
        // ...
    }
}
```

> **Tip:** Zvolte velikost poolu na základě počtu CPU jader (`Runtime.getRuntime().availableProcessors()`) plus malý buffer, pokud úlohy zahrnují I/O.

## Krok 2: Vylistujte HTML soubory, které chcete zpracovat

Můžete prohledávat adresář dynamicky, ale pro přehlednost použijeme pevně zakódované pole. Nahraďte `"YOUR_DIRECTORY"` skutečnou cestou na vašem počítači.

```java
String[] htmlFiles = {
    "YOUR_DIRECTORY/input1.html",
    "YOUR_DIRECTORY/input2.html",
    "YOUR_DIRECTORY/input3.html",
    "YOUR_DIRECTORY/input4.html"
};
```

Pokud dáváte přednost dynamickému přístupu, `Files.list(Paths.get("YOUR_DIRECTORY"))` může pole naplnit automaticky.

## Krok 3: Odeslat úlohu čištění pro každý soubor

Každý soubor dostane vlastní úlohu **executorservice example java**. V lambda výrazu provádíme:

1. Otevřít soubor pomocí `HTMLDocument`.  
2. **Remove script tags** pomocí CSS selektoru (`"script"`).  
3. Uložit vyčištěnou verzi s příponou `_clean.html`.

```java
for (String htmlFile : htmlFiles) {
    executor.submit(() -> {
        // Load the document (each thread works with its own instance)
        try (HTMLDocument doc = new HTMLDocument(htmlFile)) {
            // Remove all <script> elements from the document
            doc.querySelectorAll("script")
               .forEach(node -> node.getParentNode().removeChild(node));

            // Save the cleaned document with a new name
            doc.save(htmlFile.replace(".html", "_clean.html"));
        } catch (Exception e) {
            System.err.println("Failed to process " + htmlFile + ": " + e.getMessage());
        }
    });
}
```

> **Proč to funguje:** `querySelectorAll("script")` vrací živou kolekci všech elementů `<script>`. Smyčka `forEach` pak odpojí každý uzel od jeho rodiče, čímž efektivně **remove javascript html** ze zdroje.

## Krok 4: Ukončete pool a počkejte na dokončení

Elegantní ukončení je klíčové; nechcete, aby po dokončení úlohy zůstávaly viset nechtěná vlákna.

```java
// Step 4: Shut down the pool and wait for all tasks to finish
executor.shutdown();
if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
    System.err.println("Some tasks did not finish within the timeout.");
    executor.shutdownNow(); // Force shutdown if needed
}
System.out.println("All HTML files have been cleaned.");
```

Pokud máte mnoho souborů nebo velké dokumenty, zvyšte timeout na vyšší hodnotu.

## Kompletní funkční příklad

Spojením všeho dohromady získáte kompletní program, který můžete zkopírovat do `ParallelProcessingDemo.java` a spustit.

```java
import com.aspose.html.HTMLDocument;
import java.util.concurrent.*;

public class ParallelProcessingDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);

        // 2️⃣ List the HTML files to be processed
        String[] htmlFiles = {
            "YOUR_DIRECTORY/input1.html",
            "YOUR_DIRECTORY/input2.html",
            "YOUR_DIRECTORY/input3.html",
            "YOUR_DIRECTORY/input4.html"
        };

        // 3️⃣ Submit a cleaning task for each file
        for (String htmlFile : htmlFiles) {
            executor.submit(() -> {
                try (HTMLDocument doc = new HTMLDocument(htmlFile)) {
                    // 🌟 Remove all <script> elements (remove script tags)
                    doc.querySelectorAll("script")
                       .forEach(node -> node.getParentNode().removeChild(node));

                    // Save cleaned version
                    doc.save(htmlFile.replace(".html", "_clean.html"));
                } catch (Exception e) {
                    System.err.println("Error processing " + htmlFile + ": " + e.getMessage());
                }
            });
        }

        // 4️⃣ Shut down the pool and wait for completion
        executor.shutdown();
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            System.err.println("Timeout reached before all tasks finished.");
            executor.shutdownNow();
        } else {
            System.out.println("All files cleaned successfully!");
        }
    }
}
```

### Očekávaný výstup

Když spustíte program, uvidíte zprávy v konzoli jako:

```
All files cleaned successfully!
```

A ve vašem adresáři najdete:

- `input1_clean.html`
- `input2_clean.html`
- `input3_clean.html`
- `input4_clean.html`

Každý soubor `_clean.html` bude identický s původním souborem, jen bez všech `<script>` bloků.

## Často kladené otázky (FAQ)

**Q: Mohu změnit velikost thread poolu za běhu?**  
A: Ano. Použijte `Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() + 1)` pro dynamickou velikost založenou na hostitelském stroji.

**Q: Co když moje HTML soubory obsahují inline event handlery (`onclick`, `onload`)?**  
A: Aktuální selektor odstraňuje jen `<script>` tagy. Pro odstranění inline handlerů byste museli projít všechny elementy a vymazat atributy začínající na `on`. To je dobré rozšíření pro pozdější tutoriál.

**Q: Je Aspose.HTML jediná knihovna, která podporuje `querySelectorAll`?**  
A: Ne. Knihovny jako jsoup také nabízejí CSS selektory, ale Aspose.HTML poskytuje kompletní DOM API, které napodobuje chování prohlížeče, což je užitečné pro složité úkoly čištění.

**Q: Jak zacházet s velmi velkými HTML soubory, které se nemusí vejít do paměti?**  
A: Pro obrovské soubory zvažte streamovací parsery (např. Saxon pro XML) nebo zpracování souboru po částech. Vzorec fixního thread poolu stále platí; jen nahradíte `HTMLDocument` streamovacím řešením.

## Další kroky a související témata

- **Remove JavaScript HTML with jsoup** – lehká alternativa, pokud nepotřebujete plnou podporu DOM.  
- **Dynamic thread pool sizing** – prozkoumejte `ThreadPoolExecutor` pro jemnější kontrolu.  
- **Batch processing with `CompletableFuture`** – kombinujte futures pro bohatší pipeline.  
- **HTML sanitization beyond scripts** – odstraňte styly, iframy nebo nebezpečné atributy.  

Všechny tyto stavby vycházejí ze stejného základu **executorservice example java**, který jsme zde představili.

## Závěr

Nyní máte robustní, připravený příklad pro produkci, jak použít **fixed thread pool java** k **remove script tags** z dávky HTML souborů. Využitím `ExecutorService` je každý soubor zpracován paralelně, což dramaticky zkracuje celkový čas běhu. Přístup je modulární, snadno rozšiřitelný a funguje s libovolnou Java‑kompatibilní HTML knihovnou, která nabízí možnost `load html document`.  

Vyzkoušejte to, upravte velikost poolu nebo přidejte další pravidla čištění – vaše další HTML‑zpracovatelská výzva je jen pár řádků daleko.

![Ilustrace Fixed thread pool java](https://example.com/fixed-thread-pool-java.png "Fixed thread pool java")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}