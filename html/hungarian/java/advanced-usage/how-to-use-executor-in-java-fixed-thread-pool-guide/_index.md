---
category: general
date: 2026-05-28
description: hogyan használjuk az Executor-t Java-ban egy fix szálkészlettel, szöveg
  kinyerése HTML-ből és a feldolgozás felgyorsítása – egy teljes Java szálkészlet
  példája.
draft: false
keywords:
- how to use executor
- fixed thread pool java
- extract text from html
- java thread pool example
- create fixed thread pool
language: hu
og_description: Hogyan használjuk az Executor-t Java-ban fix szálkészlettel. Ismerj
  meg egy teljes Java szálkészlet példát, amely hatékonyan kinyeri a szöveget HTML-fájlokból.
og_title: Hogyan használjuk az Executor-t Java-ban – Fix szálkészlet útmutató
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
title: Hogyan használjuk az Executor-t Java-ban – Fix szálkészlet útmutató
url: /hu/java/advanced-usage/how-to-use-executor-in-java-fixed-thread-pool-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjuk az Executor-t Java-ban – Fix szálkészlet útmutató

Gondoltad már valaha, **hogyan használjuk az executor-t**, hogy egyszerre sok feladatot futtassunk anélkül, hogy a memóriát felrobbantanánk? Nem vagy egyedül. Sok valós alkalmazásban egy mappában lévő HTML fájlokat kell bejárni, kinyerni a body szöveget, és ezt gyorsan megtenni – éppen ezt a szituációt oldja meg ez a tutorial.

Át fogunk vezetni egy **fixed thread pool java** megvalósításon, amely HTML-ből kinyeri a szöveget, kiírja minden fájl karakter számát, és tisztán leáll. A végére egy önálló **java thread pool example**-t kapsz, amelyet bármely projektbe beilleszthetsz, valamint néhány tippet a pool méretének testreszabásához és a szélhelyzetek kezeléséhez.

> **Amire szükséged lesz**  
> * Java 17 (vagy bármely friss JDK)  
> * Egy kis HTML‑parsing könyvtár – a *jsoup*-ot fogjuk használni, mert kipróbált és konfiguráció nélküli.  
> * Néhány minta *.html* fájl a választott könyvtáradban.

---

## Hogyan használjuk az Executor-t fix szálkészlettel

A bármely párhuzamos Java program szíve a `ExecutorService`. Egy **fixed thread pool** létrehozásával azt mondjuk a JVM-nek, hogy pontosan N munkás szálat tartson életben, ami megakadályozza a szálak létrehozásának költségét és korlátozza az erőforrás-használatot.

```java
// Step 1: Build a fixed‑size thread pool (4 workers in this case)
ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Miért fontos ez:*  
Ha minden egyes HTML fájlhoz új `Thread`-et indítanál, az operációs rendszernek egy átlagos laptopon tucatnyi szálat kellene ütemeznie, ami kontextus‑váltási túlterhelést okoz. Egy fix pool újrahasználja ugyanazokat a négy szálat, így kiszámítható CPU‑használatot biztosít.

---

## Határozd meg a feldolgozandó HTML fájlokat – Fixed Thread Pool Java

Ezután felsoroljuk a pool-ba betáplálni kívánt fájlokat. Egy valódi alkalmazásban valószínűleg egy könyvtárfát járnál be; itt egyszerűen tartjuk.

```java
// Step 2: List the HTML documents you want to parse
List<String> htmlFilePaths = List.of(
        "YOUR_DIRECTORY/a.html",
        "YOUR_DIRECTORY/b.html",
        "YOUR_DIRECTORY/c.html",
        "YOUR_DIRECTORY/d.html"
);
```

*Tip:* `List.of` egy immutable listát ad vissza, amely biztonságosan megosztható szálak között extra szinkronizáció nélkül.

---

## Küldj külön feladatot minden HTML fájlhoz

Most minden útvonalat átadunk az executor-nak. A benyújtott lambda **párhuzamosan** fog futni a négy munkás szál egyikén.

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

**Miért csomagoljuk a logikát egy metódusba** (`extractBodyText`), az a következő szekcióban lesz egyértelmű – ez rendezi a lambdát és lehetővé teszi a kinyerési kód újrahasználatát máshol.

---

## Szöveg kinyerése HTML-ből – A fő logika

Itt van a újrahasználható segédfüggvény, amely valójában **kivonja a szöveget a html-ből** a Jsoup segítségével. Megnyitja a fájlt, elemezni a DOM-ot, és visszaadja a tiszta body szöveget.

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

*Miért Jsoup?* Könnyű, hibás markup-ot is elegánsan kezel, és nem igényel teljes böngésző motorot. A metódus `IOException`-t dob, így a hívó eldöntheti, hogyan naplózza vagy helyreállítja – tökéletes egy thread‑pool szituációban, ahol nem akarod, hogy egy rossz fájl leállítsa az egész executor-t.

---

## Az Executor elegáns leállítása – Fix szálkészlet létrehozása

Miután minden feladatot benyújtottuk, meg kell mondanunk a pool-nak, hogy ne fogadjon új munkát, és fejezze be a már sorba állítottakat.

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

*Magyarázat:* A `shutdown()` megakadályozza az új benyújtásokat, míg az `awaitTermination` blokkol, amíg minden elemző feladat be nem fejeződik (vagy a timeout lejár). Ha valami elakad, a `shutdownNow()` megpróbálja leállítani a futó feladatokat. Ez a minta a **create fixed thread pool** biztonságos ajánlott módja.

---

## Teljes, futtatható példa

Mindent összevonva, itt egy egyetlen fájl, amelyet lefordíthatsz és futtathatsz. Tartalmazza a szükséges importokat, a `main` metódust, és a fent leírt segédfüggvényt.

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

**Várható kimenet** (feltételezve, hogy minden fájl körülbelül 1 200 karakter body szöveget tartalmaz):

```
YOUR_DIRECTORY/a.html → 1234 chars
YOUR_DIRECTORY/b.html → 1198 chars
YOUR_DIRECTORY/c.html → 1305 chars
YOUR_DIRECTORY/d.html → 1120 chars
```

Ha bármelyik fájl hiányzik vagy hibás, egy stack trace-et látsz a `stderr`-re nyomtatva, de a többi feladat érintetlenül folytatódik – éppen ez a jól viselkedő **java thread pool example** elvárása.

---

## Gyakori kérdések és szélhelyzetek

| Kérdés | Válasz |
|----------|--------|
| *Mi van, ha négynél több fájlom van?* | A pool sorba állítja a többlet feladatokat, és futtatja őket, amint egy szál szabad lesz. Nem szükséges extra kód. |
| *Használjam helyette a `newCachedThreadPool`-t?* | `newCachedThreadPool` igény szerint hoz létre szálakat, és korlátlanul növekedhet, ami kockázatos I/O‑intenzív feladatoknál. Egy **fixed thread pool** kiszámítható memória- és CPU‑használatot biztosít. |
| *Hogyan változtassam meg a pool méretét a CPU magok számához igazítva?* | `int cores = Runtime.getRuntime().availableProcessors(); ExecutorService exec = Executors.newFixedThreadPool(cores);` egy gyakori minta. |
| *Mi van, ha a feldolgozás egy fájlnál hibát okoz?* | A lambda belsejében lévő `catch (IOException e)` elkülöníti a hibát, naplózza, és a pool többi része tovább működik. |
| *Visszaadhatom a kinyert szöveget a hívónak?* | Igen – használj `Future<String>`-et a `submit(Runnable)` helyett. A kód így nézne ki: `Future<String> f = executor.submit(() -> extractBodyText(path));` és később `String result = f.get();`. |

---

## Összegzés

Áttekintettük, **hogyan használjuk az executor-t**, hogy elindítsunk egy **fixed thread pool java**-t, amely párhuzamosan dolgozza fel a HTML fájlok gyűjteményét, kinyeri a body szöveget, és jelentést készít a karakterek számáról. A teljes **java thread pool example** bemutatja a megfelelő erőforrás-kezelést, hibakezelést és egy újrahasználható kinyerési metódust.

Következő lépések? Próbáld megcserélni a `extractBodyText` implementációt egy fejlettebb scraper-re, kísérletezz nagyobb pool mérettel, vagy tápláld az eredményeket egy adatbázisba. Emellett felfedezheted a `CompletionService`-t, hogy a kész eredményeket azonnal lekérd, ami hasznos, ha a fájlméretek nagyban eltérnek.

Nyugodtan módosítsd a könyvtár útvonalát, adj hozzá több fájlt, vagy integráld ezt a kódrészletet egy nagyobb crawling keretrendszerbe. A fő minta – pool létrehozása, független feladatok benyújtása, és elegáns leállítás – változatlan marad, függetlenül attól, mennyire összetett a feladat.

Boldog kódolást, és legyenek a szálaid mindig élőek (amíg le nem állítod őket, természetesen)!

## Kapcsolódó tutorialok

- [Fixed thread pool java – Párhuzamos HTML tisztítás ExecutorService-szel](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [HTML lekérdezése Java-ban – Teljes tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Aspose.HTML használata Java-hoz – HTML5 Canvas renderelés mestersége](/html/english/java/html5-canvas-rendering/html5-canvas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}