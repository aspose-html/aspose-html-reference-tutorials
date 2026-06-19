---
category: general
date: 2026-06-19
description: Jak spustit vlákno v Javě s opakovaně použitelným Runnable, spustit více
  vláken, vypsat název vlákna a parsovat HTML v Javě. Příklad krok za krokem.
draft: false
keywords:
- how to start thread
- start multiple threads
- print thread name
- parse html with java
- how to use runnable
language: cs
og_description: Jak spustit vlákno v Javě pomocí Runnable, spustit více vláken, vypsat
  název vlákna a parsovat HTML v Javě v jednom spustitelném příkladu.
og_title: Jak spustit vlákno v Javě – Kompletní průvodce
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to start thread in Java with a reusable Runnable, start multiple
    threads, print thread name, and parse HTML with Java. Step‑by‑step example.
  headline: How to start thread in Java – Complete Guide
  type: TechArticle
tags:
- java
- multithreading
- html-parsing
- runnable
title: Jak spustit vlákno v Javě – kompletní průvodce
url: /cs/java/creating-managing-html-documents/how-to-start-thread-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak spustit vlákno v Javě – Kompletní průvodce

Už jste se někdy zamýšleli **jak spustit vlákno** v Javě, aniž byste se topili v boilerplate kódu? Nejste v tom sami. Ať už stavíte webový crawler, aktualizátor UI, nebo jen potřebujete odlehčit těžký výpočet, ovládnutí vytváření vláken je nezbytná dovednost pro každého Java vývojáře.

V tomto tutoriálu projdeme praktickým scénářem: **parsování HTML v Javě**, výpis názvu aktuálního vlákna a **spuštění více vláken**, která sdílejí stejnou logiku. Na konci budete vědět **jak používat Runnable**, vytvoříte několik pracovních vláken a uvidíte očekávaný výstup — vše v **samostatném** příkladu, který můžete okamžitě zkopírovat a vložit.

## Co se naučíte

- Přesné kroky **jak spustit vlákno** pomocí třídy `Thread` a `Runnable`.
- Jak **spustit více vláken**, která vykonávají stejný úkol bez duplikace kódu.
- Nejednodušší způsob, jak **vytisknout název vlákna** vedle výsledků zpracování.
- Čistá metoda pro **parsování HTML v Javě** pomocí lehkého pomocníka `HTMLDocument` (nebo libovolného parseru, který preferujete).
- Proč **jak používat runnable** má význam pro znovupoužitelný, testovatelný kód.

Pro základní příklad nejsou vyžadovány žádné externí knihovny, ale uvedeme, kde můžete nahradit Jsoup nebo jiný parser, pokud budete potřebovat větší výkon.

---

## Krok 1: Definujte znovupoužitelný úkol – **jak používat runnable**

První věc, kterou musíte vědět **jak používat runnable**, je zabalit práci, kterou má každé vlákno vykonat. `Runnable` je jen funkční rozhraní s jedinou metodou `run()`, což ho činí ideálním pro lambda výrazy.

```java
// Define the reusable task
Runnable extractTextLength = () -> {
    // Open the HTML file inside a try‑with‑resources block
    try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
        // Get the length of the body text
        int textLength = doc.getBody().getTextContent().length();

        // Print the thread name and the length
        System.out.println(Thread.currentThread().getName() + ": " + textLength);
    } catch (Exception e) {
        e.printStackTrace();
    }
};
```

**Proč je to důležité:** Když udržíte logiku uvnitř `Runnable`, můžete ji předat libovolnému počtu objektů `Thread`, thread poolu nebo dokonce executor service později. To udržuje váš kód DRY a testovatelný.

---

## Krok 2: **Jak spustit vlákno** – vytvořte první pracovníka

Nyní, když máme `Runnable`, spuštění vlákna je tak jednoduché jako zavolat konstruktor `Thread`. Otázka **jak spustit vlákno** je zodpovězena jedním řádkem:

```java
// Start the first thread
Thread worker1 = new Thread(extractTextLength, "Worker-1");
worker1.start();   // <-- this actually starts the new thread
```

Všimněte si druhého argumentu, `"Worker-1"`. Tento název se objeví, když později **vytiskneme název vlákna**, což usnadní ladění.

---

## Krok 3: **Spustit více vláken** – znovu použít stejný Runnable

Chcete zpracovat několik HTML souborů najednou? Stačí vytvořit další `Thread` se stejným `Runnable`. Toto ukazuje **spuštění více vláken** bez kopírování kódu úkolu:

```java
// Start a second thread that runs the exact same task
Thread worker2 = new Thread(extractTextLength, "Worker-2");
worker2.start();
```

Oba `Worker-1` i `Worker-2` budou současně vykonávat blok definovaný v `extractTextLength`. Protože úkol je bezstavový (pouze čte soubor), není třeba se obávat podmínek závodu.

---

## Krok 4: **Vytisknout název vlákna** při parsování HTML

Uvnitř `Runnable` už voláme `Thread.currentThread().getName()`. To je kanonický způsob, jak **vytisknout název vlákna**. Výstup bude vypadat zhruba takto (předpokládáme, že tělo HTML obsahuje 1 234 znaků):

```
Worker-1: 1234
Worker-2: 1234
```

Pokud spustíte program na větším souboru, každý řádek zobrazí stejnou délku, protože oba vlákna čtou stejný soubor. Změňte cestu nebo předávejte název souboru jako parametr, abyste viděli různé výsledky.

---

## Krok 5: Kompletní, spustitelný příklad – od importu po spuštění

Níže je kompletní, **samostatný** program, který můžete vložit do souboru pojmenovaného `HtmlThreadDemo.java`. Obsahuje malý stub `HTMLDocument`, aby se kód přeložil i bez skutečného parseru. Nahraďte stub Jsoup nebo libovolnou knihovnou, kterou preferujete pro produkční použití.

```java
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Minimal HTMLDocument helper.
 * In a real project you would use Jsoup or another robust parser.
 */
class HTMLDocument implements AutoCloseable {
    private final String content;

    private HTMLDocument(String html) {
        this.content = html;
    }

    public static HTMLDocument load(String path) throws IOException {
        String html = new String(Files.readAllBytes(Paths.get(path)));
        return new HTMLDocument(html);
    }

    public Body getBody() {
        // Very naive extraction of <body>...</body>
        int start = content.indexOf("<body");
        if (start == -1) return new Body("");
        start = content.indexOf('>', start) + 1;
        int end = content.indexOf("</body>", start);
        if (end == -1) end = content.length();
        return new Body(content.substring(start, end));
    }

    @Override
    public void close() {
        // No resources to free in this stub
    }

    /** Simple wrapper for body text */
    static class Body {
        private final String text;
        Body(String text) { this.text = text; }
        public String getTextContent() { return text; }
    }
}

public class HtmlThreadDemo {

    public static void main(String[] args) {
        // Step 1: Define a reusable task (how to use runnable)
        Runnable extractTextLength = () -> {
            try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
                int textLength = doc.getBody().getTextContent().length();
                // Step 4: Print thread name and length
                System.out.println(Thread.currentThread().getName() + ": " + textLength);
            } catch (Exception e) {
                e.printStackTrace();
            }
        };

        // Step 2 & 3: How to start thread and start multiple threads
        new Thread(extractTextLength, "Worker-1").start();
        new Thread(extractTextLength, "Worker-2").start();
    }
}
```

### Očekávaný výstup

Předpokládejme, že `page.html` obsahuje 2 567 znaků uvnitř tagu `<body>`, uvidíte něco jako:

```
Worker-1: 2567
Worker-2: 2567
```

Pokud soubor nelze přečíst, bude vytištěna stack trace — díky `catch` bloku.

---

## Časté úskalí a profesionální tipy

| Problém | Proč k tomu dochází | Řešení |
|-------|----------------|-----|
| **Soubor nenalezen** | Cesta `"YOUR_DIRECTORY/page.html"` je relativní k místu, odkud spouštíte JVM. | Použijte absolutní cestu nebo `Paths.get("").toAbsolutePath()` pro ladění. |
| **Závodní podmínky** | Pokud `Runnable` mění sdílený stav, vlákna mohou kolidovat. | Udržujte úkol bezstavový, nebo synchronizujte přístup ke sdíleným objektům. |
| **Příliš mnoho vláken** | Vytváření desítek `Thread`s může vyčerpat zdroje OS. | Přepněte na `ExecutorService` s omezeným poolem poté, co zvládnete základy. |
| **Nesprávné parsování HTML** | Stub `HTMLDocument` je zjednodušený; složité stránky selžou. | Nahraďte jej Jsoup: `Document doc = Jsoup.parse(new File(path), "UTF‑8");` |

---

## Rozšíření příkladu

Nyní, když víte **jak spustit vlákno**, můžete chtít:

- **Parsovat různé soubory** předáním názvu souboru do `Runnable` (použijte konstruktor nebo lambda, která zachytí proměnnou).
- **Shromažďovat výsledky** pomocí `ConcurrentLinkedQueue<Integer>` místo pouhého výpisu.
- **Využít thread pool** (`Executors.newFixedThreadPool(4)`) pro lepší škálovatelnost.
- **Vyměnit parser** za Jsoup, HtmlUnit nebo libovolnou knihovnu, která vyhovuje potřebám vašeho projektu.

Všechny tyto kroky stále vycházejí ze základní myšlenky, kterou jsme probrali: definujte znovupoužitelný úkol, předáte jej jednomu nebo více vláknům a sledujte, které vlákno práci vykonává, pomocí **vytisknutí názvu vlákna**.

---

## Závěr

Probrali jsme **jak spustit vlákno** v Javě, ukázali **jak používat runnable** pro znovupoužitelnou práci, ukázali jsme, jak **spustit více vláken**, a představili jednoduchý způsob, jak **parsovat HTML v Javě** a **vytisknout název vlákna** pro každého pracovníka. Kompletní úryvek kódu výše je připraven k spuštění a koncepty lze rozšířit na složitější, produkční aplikace.

Neváhejte experimentovat: změňte cestu k souboru, zvyšte počet pracovníků nebo připojte skutečný HTML parser. Základy zůstávají stejné a nyní máte pevný základ pro jakýkoli multithreaded Java projekt.

Máte otázky ohledně bezpečnosti vláken, executor služeb nebo knihoven pro parsování HTML? Zanechte komentář níže a šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Fixed thread pool java – Paralelní čištění HTML pomocí ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [Jak upravit HTML pomocí Aspose.HTML pro Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Jak převést HTML do PDF v Javě – pomocí Aspose.HTML pro Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}