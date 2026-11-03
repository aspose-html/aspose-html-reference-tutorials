---
category: general
date: 2026-04-05
description: Java több szálas oktatóanyag, amely bemutatja, hogyan futtathatók párhuzamosan
  feladatok egy fix szálkészlettel, és hogyan állítható le biztonságosan az ExecutorService.
draft: false
keywords:
- java multithreading tutorial
- fixed thread pool java
- shutdown executorservice
- print thread name
- run tasks parallel
language: hu
og_description: Java több szálas oktatóanyag, amely végigvezet a feladatok párhuzamos
  futtatásán, egy fix szálkészlet létrehozásán Java-ban, a szál nevének kiírásán,
  és az ExecutorService tiszta leállításán.
og_title: Java több szálú programozási útmutató – Párhuzamos végrehajtás fix szálkészlettel
tags:
- Java
- Concurrency
- ExecutorService
title: 'Java több szálas oktatóanyag: Feladatok párhuzamos futtatása rögzített szálkészlettel'
url: /hu/java/advanced-usage/java-multithreading-tutorial-run-tasks-parallel-with-fixed-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java multithreading tutorial – Parallel Execution Made Simple

Gondolkodtál már azon, hogyan **run tasks parallel** Java-ban anélkül, hogy az alacsony szintű szálkezelésben fulladnál? Ebben a **java multithreading tutorial**-ban pontosan ezt mutatjuk be: egy **fixed thread pool java** használatával, minden szál nevének kiírásával, és a munka befejezésekor a **shutdown executorservice** tiszta végrehajtásával.  

Ha már írtál valaha egy ciklust, amely a hálózati I/O-n blokkol, vagy egyszerre több weboldalt kell lekérned, az alább bemutatott minta időt és fejfájást takarít meg.  

Mindent lefedünk, amire szükséged van – nincs külső dokumentáció, csak tiszta Java kód, amit másolhatsz‑beilleszthetsz, futtathatsz, és láthatod az eredményt. A végére megérted, miért a fixed thread pool gyakran a legjobb választás a korlátozott párhuzamossághoz, hogyan lehet biztonságosan leállítani, és hogyan teheted olvashatóbbá a naplókat a szál nevének kiírásával.  

> **Prerequisites**: Java 8+ (a `java.util.concurrent` csomag évek óta stabil), egy IDE vagy egyszerű `javac`/`java` parancssor, valamint az OOP alapvető ismerete. Nem szükséges további könyvtár a már meglévő Aspose HTML for Java jar-hoz.

---

![java multithreading tutorial diagram showing a thread pool feeding tasks](https://example.com/images/java-multithreading-tutorial.png "java multithreading tutorial diagram")

## java multithreading tutorial – Fixed Thread Pool beállítása

A **fixed thread pool** korlátozza a párhuzamosan futó szálak számát, megakadályozva, hogy az alkalmazás túl sok OS szálat hozzon létre és kimerítse az erőforrásokat. Itt egy négy munkásos pool-t hozunk létre:

```java
import java.util.concurrent.*;

public class ParallelProcessingTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Miért négy?* Ez megegyezik a lekérdezendő URL-ek számával, de a számot a CPU magok, I/O intenzitás vagy memória korlátok alapján is beállíthatod. Az `Executors` gyár megvédi a low‑level `Thread` konstruktor használatától, és egy tiszta `ExecutorService` referenciát ad, amelyet később **shutdown executorservice**-rel állíthatsz le.

## URL-ek előkészítése és párhuzamos feladatok meghatározása

Ezután felsoroljuk a feldolgozni kívánt oldalakat. Egy valódi scraper esetén valószínűleg fájlból vagy adatbázisból olvasnád be őket, de egy statikus tömb önmagában tartja a példát:

```java
        // Step 2: List the web pages to process
        String[] pageUrls = {
            "https://example.com/a.html",
            "https://example.com/b.html",
            "https://example.com/c.html",
            "https://example.com/d.html"
        };
```

Most következik a **run tasks parallel** rész. Minden URL-hez egy lambda-t adunk át, amely betölti a dokumentumot és kiírja a címét. Figyeld meg a `Thread.currentThread().getName()` használatát – ez a **print thread name** trükkünk, amely sokkal egyszerűbbé teszi a hibakeresést:

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

> **Pro tipp**: A `HTMLDocument` try‑with‑resources blokkba ágyazása garantálja, hogy az alatta lévő stream lezárásra kerül, még ha az oldal betöltése sikertelen is.

## Gracefully Shutdown the ExecutorService

A szálpool életben hagyása a munka befejezése után a JVM-et függőben tarthatja. A helyes módja a **shutdown executorservice**, majd a befejezésre várás:

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

*Miért van időkorlát?* Ez megvédi egy olyan szabadgyalog feladattól, amely soha nem tér vissza (pl. egy lefagyott hálózati hívás). Ha a pool egy perc alatt nem fejeződik be, meghívjuk a `shutdownNow()`-t, hogy megszakítsuk a maradék szálakat.

### Expected Output

A program futtatása hasonló kimenetet ad:

```
pool-1-thread-1 – Example A
pool-1-thread-3 – Example C
pool-1-thread-2 – Example B
pool-1-thread-4 – Example D
```

A pontos sorrend változhat – végül is a feladatok valóban párhuzamosak. Ami állandó, az a **print thread name** előtag, amely pontosan megmutatja, melyik munkás kezelte az egyes URL-eket.

---

## Common Variations & Edge Cases

| Helyzet | Mit kell módosítani | Ok |
|-----------|----------------|--------|
| **Több URL, mint szál** | Tartsd meg a pool méretét; a felesleges feladatok automatikusan sorba kerülnek. | A fixed pool kezeli helyetted a back‑pressure‑t. |
| **CPU‑bound work** | Állítsd be a pool méretét `Runtime.getRuntime().availableProcessors()` értékre a keményen kódolt 4 helyett. | Maximális CPU kihasználás anélkül, hogy túlterhelnéd a rendszert. |
| **Need to cancel a specific task** | Tarts egy `Future<?>` referenciát az `executor.submit()`-ból, és hívd a `future.cancel(true)`-t. | Finomhangolt vezérlést biztosít az egyes feladatok felett. |
| **Processing large files** | Növeld a pool méretét mérsékelten *vagy* válts `newCachedThreadPool()`-ra, ha csúcsokra számítasz. | A cached pool igény szerint hoz létre szálakat, de vigyázz a korlátlan növekedésre. |

---

## Conclusion

Most már van egy alapos **java multithreading tutorial**, amely bemutatja, hogyan **run tasks parallel** egy **fixed thread pool java** használatával, **print thread name** a tiszta naplózáshoz, és **shutdown executorservice** tisztán. A teljes, futtatható kód egyetlen osztályban található, így bármelyik projektbe beillesztheted, és azonnal skálázhatod az I/O‑bound munkádat.

Mi a következő? Próbáld megcserélni a `HTMLDocument`-ot a saját HTTP kliensedre, kísérletezz különböző pool méretekkel, vagy integrálj egy `CompletionService`-t, hogy a befejeződő eredményeket összegyűjtsd. Továbbá felfedezheted a `java.util.concurrent.Flow`-t a reaktív stream-ekhez, ha egyszerű soron túlmutató back‑pressure kezelést igényelsz.

Boldog kódolást, és ne feledd: a megfelelő thread‑pool stratégia mellett a párhuzamosság *gyerekjáték*, nem hibaforrás. Ha kérdésed van, nyugodtan hagyj megjegyzést – mindig szívesen beszélgetek a Java concurrency‑ról!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}