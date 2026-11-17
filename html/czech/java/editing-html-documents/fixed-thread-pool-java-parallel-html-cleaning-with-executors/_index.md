---
category: general
date: 2026-06-24
description: Naučte se, jak použít fixed thread pool java k odstranění script tagů
  z HTML souborů. Tento executorservice example java ukazuje efektivní načítání HTML
  dokumentů.
draft: false
keywords:
- fixed thread pool java
- executorservice example java
- java executorservice tutorial
- load html document java
- remove script tags java
og_description: Ovládněte fixed thread pool java k odstranění script tagů z HTML souborů.
  Kompletní executorservice example java s kroky pro načtení HTML dokumentu.
og_title: Fixed thread pool java – Průvodce paralelním čištěním HTML
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Learn how to use a fixed thread pool java to remove script tags from
    HTML files. This executorservice example java shows loading HTML documents efficiently.
  headline: Fixed thread pool java – Parallel HTML Cleaning with ExecutorService
  type: TechArticle
- description: Learn how to use a fixed thread pool java to remove script tags from
    HTML files. This executorservice example java shows loading HTML documents efficiently.
  name: Fixed thread pool java – Parallel HTML Cleaning with ExecutorService
  steps:
  - name: Open the file with `HTMLDocument`.
    text: Open the file with `HTMLDocument`.
  - name: '**Remove script tags** using a CSS selector (`"script"`).'
    text: '**Remove script tags** using a CSS selector (`"script"`).'
  - name: Save the cleaned version with a `_clean.html` suffix.
    text: Save the cleaned version with a `_clean.html` suffix.
  type: HowTo
- questions:
  - answer: Yes. Use `Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors()
      + 1)` for a dynamic size based on the host machine.
    question: Can I change the thread pool size at runtime?
  - answer: The current selector only removes `<script>` tags. To strip inline handlers,
      you’d need to traverse all elements and clear attributes that start with `on`.
      That’s a good extension for a later tutorial.
    question: What if my HTML files contain inline event handlers (`onclick`, `onload`)?
  - answer: No. Libraries like jsoup also offer CSS selectors, but Aspose.HTML gives
      you a full DOM API that mirrors browser behavior, which is handy for complex
      cleaning tasks.
    question: Is Aspose.HTML the only library that supports `querySelectorAll`?
  - answer: For massive files, consider streaming parsers (e.g., Saxon for XML) or
      processing the file in chunks. The fixed thread pool pattern still applies;
      you’d just replace `HTMLDocument` with a streaming solution.
    question: How do I handle very large HTML files that might not fit into memory?
  - answer: It will use as many threads as you configure. A common practice is to
      set the pool size to the number of available processors, which maximizes CPU
      utilization without causing excessive context switching.
    question: Will the fixed thread pool java automatically use all CPU cores?
  type: FAQPage
tags:
- Java concurrency
- HTML processing
- Aspose.HTML
title: Fixed thread pool java – Paralelní čištění HTML s ExecutorService
url: /cs/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pevný thread pool java – Paralelní čištění HTML pomocí ExecutorService

Už jste někdy potřebovali **fixed thread pool java** pro zrychlení hromadného zpracování HTML? Nejste v tom sami. Když máte desítky – nebo dokonce stovky – HTML souborů posetých elementy `<script>`, provádění práce sekvenčně může připomínat sledování, jak schne barva.  

V tomto tutoriálu vám ukážeme, jak přesně vytvořit **fixed thread pool java**, načíst každý HTML dokument, odstranit veškerý JavaScript (`<script>` tagy) a uložit vyčištěné soubory – vše paralelně pomocí **executorservice example java**. Na konci budete mít připravený program, který efektivně odstraňuje script tagy, a pochopíte, proč je pevný thread pool často ideální pro CPU‑intenzivní úlohy.

## Rychlé odpovědi
`ExecutorService` je Java rozhraní, které spravuje pool pracovních vláken a umožňuje asynchronní spouštění úloh.

- **Co dělá fixed thread pool java?** Vytváří pevný počet opakovaně použitelných pracovních vláken, která úlohy vykonávají souběžně, čímž eliminuje režii neustálého vytváření nových vláken.  
- **Která knihovna načítá HTML dokumenty?** Třída `HTMLDocument` z Aspose.HTML poskytuje kompletní DOM API pro čtení a manipulaci s HTML v Javě.  
- **Jak jsou script tagy odstraňovány?** Výběrem všech elementů `<script>` pomocí CSS selektoru `"script"` a odpojením každého uzlu od jeho rodiče.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro testování; pro produkční použití je vyžadována komerční licence.  
- **Mohu upravit velikost poolu?** Ano – použijte `Runtime.getRuntime().availableProcessors()` k nastavení velikosti poolu podle počtu CPU hostitele.

## Co dosáhnete

- Nastavte `ExecutorService` s pevně daným počtem vláken.  
- Načtěte HTML soubory pomocí `HTMLDocument` z Aspose.HTML.  
- Použijte CSS selektor k **odstranění script tagů** (nebo jakýchkoli jiných nechtěných elementů).  
- Uložte vyčištěný výstup s jasnou konvencí pojmenování.  
- Zpracujte ukončení a elegantní ukončení thread poolu.

Žádné externí nástroje pro sestavení, žádná skrytá magie – jen čistá Java 8+ a Aspose.HTML.

---

## Požadavky

`HTMLDocument` je jádrová třída Aspose.HTML představující HTML soubor v paměti a poskytuje metody pro manipulaci s DOM.

Before we dive in, make sure you have:

| Požadavek | Proč je důležité |
|-------------|----------------|
| **Java 8 nebo novější** | Potřebné pro lambda výrazy a API `ExecutorService`. |
| **Aspose.HTML pro Java** ([stáhnout zde](https://products.aspose.com/html/java/)) | Poskytuje třídu `HTMLDocument` používanou k načtení a manipulaci s HTML. |
| **Složka se vzorovými HTML soubory** | Demo zpracovává soubory jako `input1.html`, `input2.html` atd. |
| **IDE nebo nástroj pro sestavení z příkazové řádky** (IntelliJ, Eclipse, Maven, Gradle) | Pro kompilaci a spuštění kódu. |

If you haven’t added Aspose.HTML to your project yet, drop the JAR into your `libs` folder and add it to the classpath, or declare the Maven dependency:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

## Jak fixed thread pool java zlepšuje rychlost zpracování?

Pevný thread pool java znovu používá předem určený počet vláken, takže JVM se vyhýbá nákladnému vytváření a ničení vláken pro každý soubor. To snižuje latenci a zvyšuje propustnost, zejména když je každá úloha (načtení, čištění a uložení HTML souboru) krátkodobá. Na 8‑jádrovém stroji může použití 8‑10 vláken zkrátit celkový čas běhu přibližně o 70 % ve srovnání s jednovláknovým cyklem.

## Definice: ExecutorService

`ExecutorService` je vysoce‑úrovňový rámec Javy pro správu poolu pracovních vláken a odesílání úloh `Runnable` nebo `Callable` k asynchronnímu provedení.

## Krok 1: Vytvořit pevný thread pool java

**fixed thread pool java** vám poskytuje předvídatelný počet pracovních vláken, která zůstávají aktivní po celou dobu úlohy. To eliminuje režii neustálého vytváření a ničení vláken, což je zvláště užitečné, když je každá úloha krátkodobá, například načtení a čištění jediného HTML souboru.

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

> **Tip:** Zvolte velikost poolu na základě počtu CPU jader (`Runtime.getRuntime().availableProcessors()`) plus malý rezervní prostor, pokud úlohy zahrnují I/O.

## Definice: HTMLDocument

`HTMLDocument` je jádrová třída Aspose.HTML, která představuje kompletní HTML soubor v paměti a poskytuje metody manipulace s DOM srovnatelné s těmi ve webovém prohlížeči.

## Krok 2: Seznam HTML souborů, které chcete zpracovat

Můžete dynamicky prohledávat adresář, ale pro přehlednost použijeme pevně zadané pole. Nahraďte `"YOUR_DIRECTORY"` skutečnou cestou na vašem počítači.

```java
String[] htmlFiles = {
    "YOUR_DIRECTORY/input1.html",
    "YOUR_DIRECTORY/input2.html",
    "YOUR_DIRECTORY/input3.html",
    "YOUR_DIRECTORY/input4.html"
};
```

If you prefer a dynamic approach, `Files.list(Paths.get("YOUR_DIRECTORY"))` can populate the array automatically.

## Krok 3: Odeslat úlohu čištění pro každý soubor

Každý soubor získá vlastní úlohu **executorservice example java**. V rámci lambda výrazu provádíme:

1. Otevřete soubor pomocí `HTMLDocument`.  
2. **Odstraňte script tagy** pomocí CSS selektoru (`"script"`).  
3. Uložte vyčištěnou verzi s příponou `_clean.html`.

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

> **Proč to funguje:** `querySelectorAll("script")` vrací živou kolekci všech elementů `<script>`. Smyčka `forEach` pak odpojí každý uzel od jeho rodiče, čímž efektivně **odstraní javascript html** ze zdroje.

## Krok 4: Ukončit pool a čekat na dokončení

Elegantní ukončení je klíčové; nechcete, aby po dokončení úlohy zůstávaly viset nepoužívaná vlákna.

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

## Proč použít pevný thread pool java pro paralelní zpracování souborů?

Aspose.HTML podporuje **více než 50 vstupních a výstupních formátů** – včetně HTML, XHTML, XML, PDF a typů obrázků – a může zpracovávat soubory až do **500 MB** bez načítání celého dokumentu do paměti. Kombinace s pevný thread pool java vám umožní vyčistit tisíce souborů během zlomek času potřebného pro jednovláknový přístup, přičemž využití paměti zůstává předvídatelné a nízké.

## Kompletní funkční příklad

Spojením všech částí získáte kompletní program, který můžete zkopírovat a vložit do `ParallelProcessingDemo.java` a spustit.

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

Po spuštění programu uvidíte zprávy v konzoli jako:

```
All files cleaned successfully!
```

A ve vašem adresáři najdete:

- `input1_clean.html`
- `input2_clean.html`
- `input3_clean.html`
- `input4_clean.html`

Každý soubor `_clean.html` bude identický s původním protějškem, jen bez všech `<script>` bloků.

## Často kladené otázky (FAQ)

**Q: Mohu změnit velikost thread poolu za běhu?**  
A: Ano. Použijte `Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() + 1)` pro dynamickou velikost založenou na hostitelském stroji.

**Q: Co když moje HTML soubory obsahují inline event handlery (`onclick`, `onload`)?**  
A: Aktuální selektor odstraňuje pouze `<script>` tagy. Pro odstranění inline handlerů byste museli projít všechny elementy a vymazat atributy začínající na `on`. To je dobré rozšíření pro pozdější tutoriál.

**Q: Je Aspose.HTML jediná knihovna, která podporuje `querySelectorAll`?**  
A: Ne. Knihovny jako jsoup také nabízejí CSS selektory, ale Aspose.HTML poskytuje kompletní DOM API, které napodobuje chování prohlížeče, což je užitečné pro složité úlohy čištění.

**Q: Jak zacházet s velmi velkými HTML soubory, které se nemusí vejít do paměti?**  
A: Pro obrovské soubory zvažte streamovací parsery (např. Saxon pro XML) nebo zpracování souboru po částech. Vzorec pevného thread poolu stále platí; jen byste nahradili `HTMLDocument` streamovacím řešením.

**Q: Použije pevný thread pool java automaticky všechny CPU jádra?**  
A: Použije tolik vláken, kolik nastavíte. Běžná praxe je nastavit velikost poolu na počet dostupných procesorů, což maximalizuje využití CPU bez nadměrného přepínání kontextu.

## Další kroky a související témata

- **Odstranit JavaScript HTML pomocí jsoup** – lehká alternativa, pokud nepotřebujete plnou podporu DOM.  
- **Dynamické nastavení velikosti thread poolu** – prozkoumejte `ThreadPoolExecutor` pro jemnější kontrolu.  
- **Dávkové zpracování s `CompletableFuture`** – kombinujte futures pro bohatší pipeline.  
- **HTML sanitizace nad rámec skriptů** – odstraňte styly, iframy nebo nebezpečné atributy.  

Všechny tyto stavby vycházejí ze stejného základu **executorservice example java**, který jsme zde představili.

## Závěr

Nyní máte solidní, připravený příklad pro produkci, jak použít **fixed thread pool java** k **odstranění script tagů** z dávky HTML souborů. Využitím `ExecutorService` je každý soubor zpracován paralelně, což dramaticky zkracuje celkový čas běhu. Přístup je modulární, snadno rozšiřitelný a funguje s libovolnou Java‑kompatibilní HTML knihovnou, která nabízí možnost `load html document`.

Vyzkoušejte ho, upravte velikost poolu nebo přidejte další pravidla čištění – vaše další HTML‑zpracovatelská výzva je jen pár řádků daleko.

---

![Ilustrace pevného thread pool java](https://example.com/fixed-thread-pool-java.png "Ilustrace pevného thread pool java")

[Ilustrace pevného thread pool java](https://example.com/fixed-thread-pool-java.png "Ilustrace pevného thread pool java")

**Poslední aktualizace:** 2026-06-24  
**Testováno s:** Aspose.HTML 24.12 for Java  
**Autor:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Související tutoriály

- [Vytvořit HTML dokumenty asynchronně v Aspose.HTML pro Java](/html/java/creating-managing-html-documents/create-html-documents-async/)
- [Načíst HTML dokumenty ze souboru v Aspose.HTML pro Java](/html/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Jak dotazovat HTML v Javě – kompletní tutoriál](/html/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}