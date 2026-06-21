---
category: general
date: 2026-04-05
description: Java tutoriál o multithreadingu, který ukazuje, jak spouštět úlohy paralelně
  pomocí pevného thread poolu v Javě a bezpečně ukončit ExecutorService.
draft: false
keywords:
- java multithreading tutorial
- fixed thread pool java
- shutdown executorservice
- print thread name
- run tasks parallel
language: cs
og_description: Java tutoriál o vícevláknovém programování, který vás provede paralelním
  spouštěním úloh, vytvořením pevného thread poolu v Javě, výpisem názvu vlákna a
  čistým ukončením ExecutorService.
og_title: java multithreading tutorial – Paralelní provádění s pevným poolem vláken
tags:
- Java
- Concurrency
- ExecutorService
title: 'Java multithreading tutoriál: Paralelní spouštění úloh s fixním poolem vláken'
url: /cs/java/advanced-usage/java-multithreading-tutorial-run-tasks-parallel-with-fixed-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java multithreading tutorial – Jednoduché paralelní provádění

Už jste se někdy zamysleli, jak **run tasks parallel** v Javě provést, aniž byste se topili v nízkoúrovňové správě vláken? V tomto **java multithreading tutorial** vás provedeme přesně tímto: použitím **fixed thread pool java**, výpisem jména každého vlákna a čistým **shutdown executorservice**, když je práce hotová.  

Pokud jste někdy napsali smyčku, která blokuje síťové I/O, nebo potřebujete najednou stáhnout několik webových stránek, vzor, který níže popisujeme, vám ušetří čas i starosti.  

Provedeme vše, co potřebujete – žádná externí dokumentace, jen čistý Java kód, který můžete zkopírovat, spustit a vidět výsledky. Na konci pochopíte, proč je **fixed thread pool** často ideální volbou pro omezenou paralelnost, jak jej bezpečně ukončit a jak učinit své logy čitelnějšími výpisem jména vlákna.  

> **Prerequisites**: Java 8+ (balíček `java.util.concurrent` je stabilní už roky), IDE nebo jednoduchý příkazový řádek `javac`/`java` a základní pochopení OOP. Žádné další knihovny nejsou potřeba kromě Aspose HTML for Java jar, který již máte.

---

![diagram java multithreading tutorial ukazující napájení úloh thread poolem](https://example.com/images/java-multithreading-tutorial.png "diagram java multithreading tutorial")

## java multithreading tutorial – Nastavení Fixed Thread Pool

**fixed thread pool** omezuje počet současně běžících vláken, čímž zabraňuje vaší aplikaci vytvářet příliš mnoho OS vláken a vyčerpávat zdroje. Zde vytvoříme pool se čtyřmi pracovníky:

```java
import java.util.concurrent.*;

public class ParallelProcessingTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Proč čtyři?* Odpovídá počtu URL, které budeme načítat, ale můžete toto číslo ladit podle počtu CPU jader, intenzity I/O nebo limitů paměti. Továrna `Executors` vás chrání před nízkoúrovňovým konstruktorem `Thread` a poskytuje čistý odkaz na `ExecutorService`, který později **shutdown executorservice**.

## Připravte URL a definujte paralelní úlohy

Dále uvedeme stránky, které chceme zpracovat. Ve skutečném scraperu byste je pravděpodobně načítali ze souboru nebo databáze, ale statické pole udržuje příklad samostatný:

```java
        // Step 2: List the web pages to process
        String[] pageUrls = {
            "https://example.com/a.html",
            "https://example.com/b.html",
            "https://example.com/c.html",
            "https://example.com/d.html"
        };
```

Nyní přichází část **run tasks parallel**. Pro každou URL odešleme lambda výraz, který načte dokument a vytiskne jeho titulek. Všimněte si použití `Thread.currentThread().getName()` – to je náš trik **print thread name**, který značně usnadňuje ladění:

```java
        // Step 3: Submit a task for each URL that loads the document and prints its title
        for (String url : pageUrls) {
            executor.submit(() -> {
                try (HTMLDocument doc = new HTMLDocument(url)) {
                    String title = doc.getTitle();
                    // Print the thread name alongside the title
                    System.out.println(Thread.currentThread().getName() + " – " + title);
                } catch (Exception e) {
                    System.err.println(Thread.currentThread().getName() + " failed: " + e.getMessage());
                }
            });
        }
```

> **Pro tip**: Zabalení `HTMLDocument` do bloku try‑with‑resources zaručuje, že podkladový stream bude uzavřen, i když se stránka nepodaří načíst.

## Elegantní ukončení ExecutorService

Nechat thread pool běžet po dokončení práce může způsobit, že se JVM zasekne. Správný způsob je **shutdown executorservice**, a poté čekat na ukončení:

```java
        // Step 4: Shut down the pool and wait for all tasks to finish
        executor.shutdown();                         // No new tasks will be accepted
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            // Force shutdown if tasks exceed the timeout
            executor.shutdownNow();
        }
    }
}
```

*Proč timeout?* Chrání vás před úlohou, která se nikdy nevrátí (např. síťové volání, které se zasekne). Pokud pool nedokončí práci během jedné minuty, zavoláme `shutdownNow()`, aby přerušil všechny přetrvávající vlákna.

### Očekávaný výstup

Spuštění programu vytiskne něco podobného:

```
pool-1-thread-1 – Example A
pool-1-thread-3 – Example C
pool-1-thread-2 – Example B
pool-1-thread-4 – Example D
```

Přesné pořadí se může lišit – úlohy jsou přece skutečně paralelní. To, co zůstává konstantní, je předpona **print thread name**, která vám přesně říká, který pracovník zpracoval kterou URL.

---

## Běžné varianty a okrajové případy

| Situation | What to Change | Reason |
|-----------|----------------|--------|
| **Více URL než vláken** | Zachovejte stejnou velikost poolu; přebytečné úlohy se automaticky zařadí do fronty. | Fixed pool pro vás řeší zpětný tlak. |
| **CPU‑vázaná práce** | Nastavte velikost poolu na `Runtime.getRuntime().availableProcessors()` místo pevně zadaných 4. | Maximalizuje využití CPU bez přetížení. |
| **Potřeba zrušit konkrétní úlohu** | Uchovejte referenci `Future<?>` z `executor.submit()` a zavolejte `future.cancel(true)`. | Poskytuje jemnozrnné řízení jednotlivých úloh. |
| **Zpracování velkých souborů** | Zvyšte velikost poolu mírně *nebo* přepněte na `newCachedThreadPool()`, pokud očekáváte výkyvy. | Cacheované pooly vytvářejí vlákna na požádání, ale pozor na neomezený růst. |

---

## Závěr

Nyní máte solidní **java multithreading tutorial**, který ukazuje, jak **run tasks parallel** pomocí **fixed thread pool java**, **print thread name** pro přehledné logování a **shutdown executorservice** čistě ukončit. Kompletní spustitelný kód je v jedné třídě, takže jej můžete vložit do libovolného projektu a okamžitě začít škálovat svou I/O‑vázanou práci.

Co dál? Zkuste nahradit `HTMLDocument` vlastním HTTP klientem, experimentujte s různými velikostmi poolu nebo integrujte `CompletionService` pro sběr výsledků, jakmile jsou hotové. Můžete také prozkoumat `java.util.concurrent.Flow` pro reaktivní proudy, pokud potřebujete řízení zpětného tlaku nad rámec jednoduché fronty.

Šťastné programování a pamatujte: se správnou strategií thread‑poolu se souběžnost stane *piece of cake*, nikoli zdrojem chyb. Pokud máte otázky, neváhejte zanechat komentář – vždy rád povídám o Java concurrency!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}