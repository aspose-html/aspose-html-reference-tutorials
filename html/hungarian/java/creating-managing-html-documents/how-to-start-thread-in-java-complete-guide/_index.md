---
category: general
date: 2026-06-19
description: Hogyan indítsunk szálat Java-ban újrahasználható Runnable-lal, indítsunk
  több szálat, írjuk ki a szál nevét, és parse-oljunk HTML-t Java-val. Lépésről‑lépésre
  példa.
draft: false
keywords:
- how to start thread
- start multiple threads
- print thread name
- parse html with java
- how to use runnable
language: hu
og_description: Hogyan indítsunk szálat Java-ban Runnable segítségével, futtassunk
  több szálat, írjuk ki a szál nevét, és parse-oljunk HTML-t Java-val egyetlen, futtatható
  példában.
og_title: Hogyan indítsunk szálat Java-ban – Teljes útmutató
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
title: Hogyan indítsunk szálat Java-ban – Teljes útmutató
url: /hu/java/creating-managing-html-documents/how-to-start-thread-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan indítsunk szálat Java-ban – Teljes útmutató

Gondolkodtál már azon, **hogyan indítsunk szálat** Java-ban anélkül, hogy a sablonkódokba fulladnál? Nem vagy egyedül. Akár webkötőt, UI frissítőt építesz, vagy csak egy nehéz számítást kell kiszervezned, a szálak létrehozásának elsajátítása elengedhetetlen képesség minden Java fejlesztő számára.

Ebben a tutorialban egy gyakorlati példán keresztül vezetünk végig: **HTML parse-olás Java-val**, a jelenlegi szál nevét kiíratjuk, és **több szálat indítunk**, amelyek ugyanazt a logikát osztják meg. A végére megtanulod **hogyan használjuk a Runnable-t**, több munkavállalót indíthatsz, és a várt kimenetet láthatod – mindezt egy önálló példában, amit most azonnal másolhatsz‑beilleszthetsz.

## Amit megtanulsz

- A pontos lépések **hogyan indítsunk szálat** a `Thread` osztály és egy `Runnable` használatával.
- Hogy **indítsunk több szálat**, amelyek ugyanazt a feladatot hajtják végre kódduplikáció nélkül.
- A legegyszerűbb mód **a szál nevét kiírni** a feldolgozási eredmények mellett.
- Egy tiszta módszer **HTML parse-olásra Java-val** egy könnyű `HTMLDocument` segítő (vagy bármely általad preferált parser) használatával.
- Miért fontos **hogyan használjuk a runnable-t** újrahasználható, tesztelhető kódhoz.

Nincs szükség külső könyvtárakra a fő példához, de megjegyzünk, hol cserélheted le Jsoup-ra vagy más parserre, ha nagyobb teljesítményre van szükséged.

---

## 1. lépés: Újrahasználható feladat definiálása – **how to use runnable**

Az első dolog, amit tudnod kell **how to use runnable**, hogy becsomagold azt a munkát, amit minden szálnak el kell végeznie. Egy `Runnable` csak egy funkcionális interfész egyetlen `run()` metódussal, ami tökéletes a lambda‑kifejezésekhez.

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

**Miért fontos:** A logikát egy `Runnable`‑ban tartva bármennyi `Thread` objektumnak, szálkészletnek vagy később egy executor service‑nek átadhatod. Ez a kódot DRY‑nek és tesztelhetőnek tartja.

---

## 2. lépés: **How to start thread** – az első munkavállaló létrehozása

Most, hogy van egy `Runnable`‑unk, egy szál indítása olyan egyszerű, mint a `Thread` konstruktor meghívása. A **how to start thread** kérdés egyetlen sorban megválaszolva:

```java
// Start the first thread
Thread worker1 = new Thread(extractTextLength, "Worker-1");
worker1.start();   // <-- this actually starts the new thread
```

Vedd észre a második argumentumot, `"Worker-1"`. Ez a név később megjelenik, amikor **print thread name**‑t hívunk, így a hibakeresés sokkal kevésbé titokzatos lesz.

---

## 3. lépés: **Start multiple threads** – ugyanazon Runnable újrahasználata

Szeretnél egyszerre több HTML fájlt feldolgozni? Indíts egy újabb `Thread`‑t ugyanazzal a `Runnable`‑val. Ez bemutatja a **start multiple threads** lehetőségét a feladatkód másolása nélkül:

```java
// Start a second thread that runs the exact same task
Thread worker2 = new Thread(extractTextLength, "Worker-2");
worker2.start();
```

Mind a `Worker-1`, mind a `Worker-2` egyidejűleg végrehajtja az `extractTextLength`‑ben definiált blokkot. Mivel a feladat állapotmentes (csak egy fájlt olvas), nincs versenyhelyzet, ami miatt aggódni kellene.

---

## 4. lépés: **Print thread name** HTML parse-olás közben

A `Runnable`‑ban már meghívtuk a `Thread.currentThread().getName()`‑t. Ez a kanonikus mód **print thread name**‑hez. A kimenet valahogy így néz ki (feltételezve, hogy a HTML body 1 234 karaktert tartalmaz):

```
Worker-1: 1234
Worker-2: 1234
```

Ha a programot nagyobb fájlon futtatod, minden sor ugyanazt a hosszúságot mutatja, mert mindkét szál ugyanazt a fájlt olvassa. Változtasd meg az útvonalat vagy add át a fájlnevet paraméterként, hogy különböző eredményeket láss.

---

## 5. lépés: Teljes, futtatható példa – az importtól a végrehajtásig

Az alábbiakban a teljes, **self‑contained** programot találod, amelyet beilleszthetsz egy `HtmlThreadDemo.java` nevű fájlba. Tartalmaz egy apró `HTMLDocument` stub‑ot, hogy a kód leforduljon akkor is, ha nincs valós parsered. Cseréld le a stub‑ot Jsoup-ra vagy bármely könyvtárra, amit a termékben használnál.

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

### Várt kimenet

Feltételezve, hogy a `page.html` 2 567 karaktert tartalmaz a `<body>` címkében, valami ilyesmit látsz majd:

```
Worker-1: 2567
Worker-2: 2567
```

Ha a fájlt nem lehet beolvasni, a stack trace ki lesz nyomtatva – köszönhetően a `catch` blokknak.

---

## Gyakori hibák és profi tippek

| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| **File not found** | A `"YOUR_DIRECTORY/page.html"` útvonal a JVM indítási helyéhez relatív. | Használj abszolút útvonalat vagy `Paths.get("").toAbsolutePath()`‑t a hibakereséshez. |
| **Race conditions** | Ha a `Runnable` megváltoztatja a megosztott állapotot, a szálak ütközhetnek. | Tartsd a feladatot állapotmentesnek, vagy szinkronizáld a megosztott objektumok hozzáférését. |
| **Too many threads** | Tucatnyi `Thread` indítása kimerítheti az OS erőforrásait. | Válts `ExecutorService`‑re egy korlátozott pool‑al, miután elsajátítottad az alapokat. |
| **Incorrect HTML parsing** | A stub `HTMLDocument` egyszerű, komplex oldalak hibát okozhatnak. | Cseréld le Jsoup-ra: `Document doc = Jsoup.parse(new File(path), "UTF‑8");` |

---

## A példa kiterjesztése

Most, hogy tudod **how to start thread**, érdemes lehet:

- **Különböző fájlok parse-olása** a fájlnév átadásával a `Runnable`‑nak (használj konstruktort vagy egy változót befogó lambda‑kifejezést).
- **Eredmények gyűjtése** egy `ConcurrentLinkedQueue<Integer>` segítségével a csak kiírás helyett.
- **Szálkészlet használata** (`Executors.newFixedThreadPool(4)`) a jobb skálázhatóságért.
- **Parser cseréje** Jsoup-ra, HtmlUnit-ra vagy bármely könyvtárra, ami a projekted igényeinek megfelel.

Mindezek a lépések továbbra is az általunk lefektetett alapötletre épülnek: definiálj egy újrahasználható feladatot, add át egy vagy több szálnak, és figyeld meg, melyik szál végzi a munkát **print thread name**‑nel.

---

## Összegzés

Áttekintettük, **how to start thread** Java-ban, bemutattuk, **how to use runnable**‑t az újrahasználható munkához, megmutattuk, hogyan **start multiple threads**, és egyszerű módot ábrázoltunk **HTML parse-olásra Java-val**, miközben **print thread name**‑t használunk minden munkavállalóhoz. A fenti teljes kódrészlet készen áll a futtatásra, és a koncepciók skálázhatók összetettebb, termék‑szintű alkalmazásokra is.

Nyugodtan kísérletezz: változtasd meg a fájl útvonalát, növeld a munkavállalók számát, vagy csatlakoztass egy valódi HTML parser‑t. Az alapok változatlanok, és most már szilárd alapod van bármely több szálas Java projekthez.

Van kérdésed a szálbiztonságról, executor service‑ről vagy HTML parser könyvtárakról? Írj egy megjegyzést alább, és jó kódolást!

## Mit érdemes következőként tanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek az API további funkcióinak elsajátításában és alternatív megvalósítási megközelítések felfedezésében saját projektjeidben.

- [Fixed thread pool java – Parallel HTML Cleaning with ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}