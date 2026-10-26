---
category: general
date: 2026-04-09
description: Spouštějte více vláken v Javě efektivně pomocí try‑with‑resources v Javě.
  Naučte se, jak bezpečně načíst HTML dokument v Javě a vyhnout se problémům s konkurencí
  v Javě.
draft: false
keywords:
- run multiple threads java
- use try with resources java
- load html document java
- avoid concurrency issues java
language: cs
og_description: Spusťte více vláken Java s try‑with‑resources Java. Tento tutoriál
  ukazuje, jak bezpečně načíst HTML dokument Java a vyhnout se problémům s konkurencí
  Java.
og_title: Spusťte více vláken v Javě – průvodce try‑with‑resources
tags:
- java
- multithreading
- html-parsing
title: spustit více vláken v Javě – použít try‑with‑resources v Javě
url: /cs/java/creating-managing-html-documents/run-multiple-threads-java-use-try-with-resources-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# spouštění více vláken java – použití try‑with‑resources java

Už jste se někdy zamýšleli, jak **spouštět více vláken java** bez toho, aby si navzájem překážely? Nejste v tom sami – většina vývojářů narazí na stejný problém, když se snaží sdílet mutovatelný objekt mezi vlákny. Dobrá zpráva? Existuje čistý, moderní způsob, jak to udělat, a začíná to příkazem `try‑with‑resources`.

V tomto návodu projdeme kompletním, připraveným k kopírování a vložení příkladem, který **načte HTML dokument java**, spustí několik vláken a zajistí, že každé vlákno pracuje s vlastní instancí dokumentu. Na konci také uvidíte, jak **se vyhnout problémům s konkurencí java**, aby vaše aplikace zůstala stabilní i při zátěži.

> **Co získáte:** spustitelný Java program, krok‑za‑krokem vysvětlení, tipy pro reálné projekty a rychlý test, který můžete spustit hned teď.

---

![ilustrace spouštění více vláken java](run-multiple-threads-java.png "Diagram ukazující více vláken, z nichž každé drží samostatnou instanci HTMLDocument")

## Předpoklady

- Java 17 nebo novější (syntaxe `try‑with‑resources` funguje stejně už od Java 7, ale použijeme novější jazykové prvky pro stručnost).  
- Malá pomocná třída pro parsování HTML s názvem `HTMLDocument`. Pokud ji nemáte, můžete ji vytvořit podle ukázky níže.  
- Základní znalost vláken (`java.lang.Thread`) a rozhraní `Runnable`.

Pokud vám některý z těchto bodů není známý, nepanikařte – každý koncept bude v následujících krocích znovu představen.

---

## Krok 1: Načtení HTML dokumentu java se sdílenou referencí

Prvním, co potřebujeme, je *sdílená* reference, která ukazuje na soubor, který chceme parsovat. Představte si ji jako plán: URL je stejná pro každé vlákno, ale samotný objekt dokumentu bude vytvořen později v každém vlákně zvlášť.

```java
// Step 1: Load the source HTML document (shared reference for its URL)
HTMLDocument sharedDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

### Proč sdílená reference?

Kdybyste každému vláknu předali stejnou instanci `HTMLDocument`, všechna vlákna by četla a zapisovala do stejných interních bufferů. To je klasický recept na závodní podmínky – právě to, co **problémy s konkurencí java** se snažíme vyhnout. Pokud sdílíte jen *URL*, může si každé vlákno bezpečně otevřít svůj vlastní stream později.

> **Tip:** Uložte URL do proměnné `final`, pokud ji neplánujete měnit. Kompilátor ji pak bude považovat za konstantu, čímž se ještě více sníží riziko nechtěné mutace.

---

## Krok 2: Vytvoření vlákny‑bezpečného úkolu pomocí try with resources java

Nyní definujeme, co každé vlákno skutečně provede. Trik spočívá v tom, že vytvoření `HTMLDocument` pro konkrétní vlákno zabalíme do bloku `try‑with‑resources`. Tím zajistíme, že dokument bude automaticky uzavřen, i když dojde k výjimce.

```java
// Step 2: Define a task that creates its own document instance per thread
Runnable task = () -> {
    // Each thread works with its own copy to avoid concurrency issues
    try (HTMLDocument threadDoc = new HTMLDocument(sharedDoc.getUrl())) {
        // Perform thread‑specific operations on threadDoc here
        System.out.println("Thread " + Thread.currentThread().getName()
                + " loaded: " + threadDoc.getTitle());
    } catch (Exception e) {
        System.err.println("Error in thread " + Thread.currentThread().getName()
                + ": " + e.getMessage());
    }
};
```

### Jak `try‑with‑resources` pomáhá

Třída `HTMLDocument` implementuje `java.lang.AutoCloseable`. Když se blok `try` ukončí, JVM automaticky zavolá `threadDoc.close()`. To je mnohem bezpečnější než ruční `finally` a eliminuje riziko zapomenutí uvolnit nativní zdroje – něco, co může snadno vést k únikům paměti v dlouho běžících multithreaded aplikacích.

---

## Krok 3: Spuštění vláken a vyhnutí se problémům s konkurencí java

S připraveným úkolem můžeme spustit libovolný počet vláken. Pro demonstraci spustíme dvě, ale nic vám nebrání vytvořit pool s desítkami pracovníků.

```java
// Step 3: Launch multiple threads that execute the same task
Thread t1 = new Thread(task, "Worker‑1");
Thread t2 = new Thread(task, "Worker‑2");

// Start the threads
t1.start();
t2.start();

// Optional: wait for them to finish (join) if you need deterministic ordering
t1.join();
t2.join();
```

### Proč nepoužít `ExecutorService`?

V produkčním kódu pravděpodobně **budete** používat `ExecutorService` k řízení poolu pracovníků. Příklad s čistým `Thread` udržuje tutoriál zaměřený na hlavní myšlenku – vytvoření samostatného dokumentu pro každé vlákno při použití `try‑with‑resources`. Klidně si `Thread` volání vyměňte za `FixedThreadPool`, pokud to lépe odpovídá architektuře vašeho projektu.

---

## Kompletní, spustitelný příklad

Když spojíme vše dohromady, získáme samostatný program, který můžete vložit do souboru `MultiThreadHtmlDemo.java`. Obsahuje minimální stub pro `HTMLDocument`, takže jej můžete ihned zkompilovat a spustit.

```java
// MultiThreadHtmlDemo.java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;

// --- Minimal stub for demonstration purposes ---
class HTMLDocument implements AutoCloseable {
    private final String url;
    private String content;

    public HTMLDocument(String url) throws IOException {
        this.url = url;
        // Simulate loading the file (replace with real parser in production)
        this.content = Files.readString(Path.of(url));
    }

    public String getUrl() {
        return url;
    }

    public String getTitle() {
        // Very naive title extraction – just for demo
        int start = content.indexOf("<title>");
        int end = content.indexOf("</title>");
        if (start != -1 && end != -1 && end > start) {
            return content.substring(start + 7, end).trim();
        }
        return "Untitled";
    }

    @Override
    public void close() {
        // In a real library you’d release native buffers here
        content = null;
        System.out.println("Closed document for URL: " + url);
    }
}

// --- Main class that runs multiple threads java ---
public class MultiThreadHtmlDemo {
    public static void main(String[] args) throws InterruptedException, IOException {
        // Step 1: Load the source HTML document (shared reference for its URL)
        HTMLDocument sharedDoc = new HTMLDocument("sample.html");

        // Step 2: Define a task that creates its own document instance per thread
        Runnable task = () -> {
            try (HTMLDocument threadDoc = new HTMLDocument(sharedDoc.getUrl())) {
                System.out.println("Thread " + Thread.currentThread().getName()
                        + " loaded title: " + threadDoc.getTitle());
            } catch (Exception e) {
                System.err.println("Error in thread " + Thread.currentThread().getName()
                        + ": " + e.getMessage());
            }
        };

        // Step 3: Launch multiple threads that execute the same task
        Thread t1 = new Thread(task, "Worker‑1");
        Thread t2 = new Thread(task, "Worker‑2");

        t1.start();
        t2.start();

        // Wait for both threads to finish
        t1.join();
        t2.join();

        System.out.println("All threads completed.");
    }
}
```

#### Očekávaný výstup (při předpokladu, že `sample.html` obsahuje `<title>Hello World</title>`)

```
Thread Worker-1 loaded title: Hello World
Closed document for URL: sample.html
Thread Worker-2 loaded title: Hello World
Closed document for URL: sample.html
All threads completed.
```

Všimněte si, že každé vlákno vypíše svůj vlastní *načtený titulek* a poté se automaticky spustí metoda `close()` – právně to, co `try‑with‑resources` slibuje.

---

## Často kladené otázky a řešení okrajových případů

**Co když soubor není nalezen?**  
Konstruktor vyhodí `IOException`. V příkladu ji zachytíme uvnitř `Runnable` a zalogujeme chybu, takže chybějící soubor nezhavaruje celou aplikaci.

**Mohu znovu použít stejnou instanci `HTMLDocument` napříč vlákny?**  
Pouze pokud je třída explicitně dokumentována jako thread‑safe. Většina parserů udržuje mutovatelný stav (např. DOM strom), takže sdílení jedné instance obvykle vede k **problémům s konkurencí java**. Vzor zde – jedna instance na vlákno – je nejbezpečnější výchozí nastavení.

**Musím něco synchronizovat?**  
Ne. Protože každé vlákno pracuje se svou vlastní `HTMLDocument`, neexistuje žádný sdílený mutovatelný stav, který by bylo potřeba chránit. Jediný sdílený prvek je řetězec URL, který je neměnný.

**Jak by to vypadalo s `ExecutorService`?**  

```java
ExecutorService executor = Executors.newFixedThreadPool(4);
for (int i = 0; i < 4; i++) {
    executor.submit(task);
}
executor.shutdown();
executor.awaitTermination(1, TimeUnit.MINUTES);
```

Jádrová logika zůstává stejná; pool jen spravuje životní cyklus vláken za vás.

---

## Profesionální tipy pro produkční multithreading

1. **Omezte počet vláken** – vytváření desítek surových objektů `Thread` může přetížit OS. Použijte raději omezený thread pool.  
2. **Preferujte neměnnou konfiguraci** – udržujte URL, cesty k souborům a nastavení parseru jako immutable, aby se zamezilo nechtěným mutacím z pracovníků.  
3. **Monitorujte využití zdrojů** – i při `try‑with‑resources` může otevření mnoha souborů najednou vyčerpat file descriptory. Omezte počet současných úkolů, pokud narazíte na limity.  
4. **Graceful shutdown** – vždy ukončete svůj executor nebo připojte (join) vlákna, aby JVM mohl čistě skončit.

---

## Závěr

Nyní máte solidní, připravený k kopírování a vložení vzor, jak **spouštět více vláken java** a zároveň bezpečně **používat try with resources java**, **načítat html dokument java** a **vyhýbat se problémům s konkurencí java**. Hlavní myšlenka je jednoduchá: každému vláknu poskytněte vlastní instanci dokumentu, nechte konstrukci `try‑with‑resources` postarat se o úklid a udržujte sdílená data neměnná.

Odtud můžete dál:

- Škálovat vzor pomocí `ExecutorService` a fronty úkolů.  
- Přepnout na skutečný HTML parser jako *jsoup* (který také implementuje `Closeable`).  
- Přidat propracovanější zpracování chyb nebo retry logiku pro nespolehlivé I/O.

Vyzkoušejte to, upravte počet pracovníků a sledujte, jak výstup v konzoli zůstává uspořádaný – žádné

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}