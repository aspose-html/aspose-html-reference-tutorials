---
category: general
date: 2026-05-28
description: jak používat executor v Javě s pevnou velikostí thread poolu, extrahovat
  text z HTML a urychlit zpracování – kompletní příklad thread poolu v Javě.
draft: false
keywords:
- how to use executor
- fixed thread pool java
- extract text from html
- java thread pool example
- create fixed thread pool
language: cs
og_description: jak používat executor v Javě s pevnou velikostí vláken. Naučte se
  kompletní příklad thread poolu v Javě, který efektivně extrahuje text z HTML souborů.
og_title: Jak používat Executor v Javě – Průvodce fixním poolem vláken
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
title: Jak používat Executor v Javě – Průvodce fixním vláknovým poolem
url: /cs/java/advanced-usage/how-to-use-executor-in-java-fixed-thread-pool-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat Executor v Javě – Průvodce pevnou vláknovou zásobou

Už jste se někdy zamýšleli **jak používat executor** k spuštění mnoha úkolů najednou, aniž byste přetížili paměť? Nejste v tom sami. V mnoha reálných aplikacích budete potřebovat procházet složku souborů HTML, vytáhnout text těla a udělat to rychle – přesně tohle řeší tento tutoriál.

Provedeme vás implementací **fixed thread pool java**, která extrahuje text z HTML, vypíše počet znaků v každém souboru a čistě se vypne. Na konci budete mít samostatný **java thread pool example**, který můžete vložit do jakéhokoli projektu, plus několik tipů, jak přizpůsobit velikost poolu a řešit okrajové případy.

> **Co budete potřebovat**  
> * Java 17 (nebo jakýkoli aktuální JDK)  
> * Malá knihovna pro parsování HTML – použijeme *jsoup*, protože je osvědčená a nevyžaduje žádnou konfiguraci.  
> * Několik ukázkových *.html* souborů v adresáři dle vašeho výběru.

---

## Jak používat Executor s pevnou vláknovou zásobou

Srdcem každého programu v Javě, který silně využívá souběžnost, je `ExecutorService`. Vytvořením **fixed thread pool** říkáme JVM, aby udržoval právě N pracovních vláken aktivních, což zabraňuje režii při vytváření vláken a omezuje využití zdrojů.

```java
// Step 1: Build a fixed‑size thread pool (4 workers in this case)
ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Proč je to důležité:*  
Kdybyste spustili nový `Thread` pro každý HTML soubor, OS by musela plánovat desítky vláken na skromném notebooku, což by vedlo k nadměrnému přepínání kontextu. Pevný pool znovu používá stejná čtyři vlákna, což vám poskytuje předvídatelné využití CPU.

---

## Definování HTML souborů ke zpracování – Fixed Thread Pool Java

Dále uvedeme soubory, které chceme vložit do poolu. Ve skutečné aplikaci byste pravděpodobně procházeli strom adresářů; zde to zjednodušíme.

```java
// Step 2: List the HTML documents you want to parse
List<String> htmlFilePaths = List.of(
        "YOUR_DIRECTORY/a.html",
        "YOUR_DIRECTORY/b.html",
        "YOUR_DIRECTORY/c.html",
        "YOUR_DIRECTORY/d.html"
);
```

*Tip:* `List.of` vrací neměnný seznam, který je bezpečný ke sdílení mezi vlákny bez další synchronizace.

---

## Odeslání samostatného úkolu pro každý HTML soubor

Nyní předáme každou cestu executorovi. Lambda, kterou odešleme, poběží **paralelně** na jednom ze čtyř pracovních vláken.

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

**Proč zabalíme logiku do metody** (`extractBodyText`) se ukáže v další sekci – udržuje lambda přehlednou a umožňuje nám znovu použít kód pro extrakci jinde.

---

## Extrahování textu z HTML – Jádrová logika

Zde je znovupoužitelná pomocná metoda, která skutečně **extrahuje text z html** pomocí Jsoup. Otevře soubor, parsuje DOM a vrátí čistý text těla.

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

*Proč Jsoup?* Je lehký, elegantně zvládá špatně formovaný markup a nevyžaduje kompletní prohlížečový engine. Metoda vyhazuje `IOException`, takže volající může rozhodnout, jak zaznamenat nebo zotavit – ideální pro scénář s thread‑pool, kde nechcete, aby jeden špatný soubor ukončil celý executor.

---

## Elegantní ukončení Executoru – Vytvoření pevné vláknové zásoby

Po odeslání všech úkolů musíme poolu říci, aby nepřijímal novou práci a dokončil to, co je již ve frontě.

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

*Vysvětlení:* `shutdown()` zabraňuje novým odesláním, zatímco `awaitTermination` blokuje, dokud nedojde ke konci všech úkolů parsování (nebo nevyprší časový limit). Pokud se něco zasekne, `shutdownNow()` se pokusí zrušit běžící úkoly. Tento vzor je doporučený způsob, jak bezpečně **create fixed thread pool**.

---

## Kompletní, spustitelný příklad

Spojením všeho dohromady, zde je jeden soubor, který můžete zkompilovat a spustit. Obsahuje potřebné importy, metodu `main` a výše popsanou pomocnou funkci.

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

**Očekávaný výstup** (předpokládáme, že každý soubor obsahuje přibližně 1 200 znaků těla):

```
YOUR_DIRECTORY/a.html → 1234 chars
YOUR_DIRECTORY/b.html → 1198 chars
YOUR_DIRECTORY/c.html → 1305 chars
YOUR_DIRECTORY/d.html → 1120 chars
```

Pokud některý soubor chybí nebo je poškozený, uvidíte výpis stack trace na `stderr`, ale ostatní úkoly budou pokračovat bez ovlivnění – přesně to, co by měl dobře fungující **java thread pool example** dělat.

---

## Časté otázky a okrajové případy

| Question | Answer |
|----------|--------|
| *Co když mám více než čtyři soubory?* | Pool zařadí přebytečné úkoly do fronty a spustí je, jakmile se uvolní vlákno. Není potřeba žádný další kód. |
| *Mám místo toho použít `newCachedThreadPool`?* | `newCachedThreadPool` vytváří vlákna na vyžádání a může růst neomezeně, což je riskantní pro I/O‑těžké úlohy. **Fixed thread pool** vám poskytuje předvídatelné využití paměti a CPU. |
| *Jak změním velikost poolu podle počtu CPU jader?* | `int cores = Runtime.getRuntime().availableProcessors(); ExecutorService exec = Executors.newFixedThreadPool(cores);` je běžný vzor. |
| *Co když parsování selže u jednoho souboru?* | `catch (IOException e)` uvnitř lambda zachytí selhání, zaznamená ho a umožní zbytku poolu pokračovat v práci. |
| *Mohu vrátit extrahovaný text volajícímu?* | Ano—použijte `Future<String>` místo `submit(Runnable)`. Kód by vypadal takto `Future<String> f = executor.submit(() -> extractBodyText(path));` a později `String result = f.get();`. |

---

## Závěr

Probrali jsme **jak používat executor** k vytvoření **fixed thread pool java**, který zpracovává kolekci HTML souborů paralelně, extrahuje jejich text těla a hlásí počet znaků. Kompletní **java thread pool example** ukazuje správnou správu zdrojů, ošetření chyb a znovupoužitelnou metodu extrakce.

Další kroky? Zkuste vyměnit implementaci `extractBodyText` za sofistikovanější scraper, experimentujte s větší velikostí poolu nebo výstupy vložte do databáze. Můžete také prozkoumat `CompletionService` pro získání výsledků, jakmile jsou připravené, což je užitečné, když se velikosti souborů výrazně liší.

Neváhejte upravit cestu k adresáři, přidat více souborů nebo integrovat tento úryvek do většího crawling frameworku. Základní vzor – vytvořit pool, odeslat nezávislé úkoly a elegantně jej ukončit – zůstává stejný, bez ohledu na to, jak složitý je váš pracovní zátěž.

Šťastné programování a ať vaše vlákna vždy běží (dokud je samozřejmě nevypnete)!

## Související tutoriály

- [Fixed thread pool java – Parallel HTML Cleaning with ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Use Aspose.HTML for Java - Mastering HTML5 Canvas Rendering](/html/english/java/html5-canvas-rendering/html5-canvas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}