---
category: general
date: 2026-02-10
description: Tanulja meg, hogyan használjon Java fix szálkészletet a HTML-fájlokban
  lévő képek számolásához, hogyan futtasson feladatokat párhuzamosan Java-ban, és
  hogyan állítsa le megfelelően az Executor Service‑t.
draft: false
keywords:
- java fixed thread pool
- how to count images
- shutdown executor service
- java parallel file processing
- run tasks concurrently java
language: hu
og_description: Mesteri szintű Java fix szálkészlet használat a képek számlálásához,
  fájlok párhuzamos feldolgozásához, és az executor szolgáltatás biztonságos leállításához.
og_title: 'java fix szálkészlet: Képek számlálása párhuzamos fájlokban'
tags:
- Java
- Concurrency
- Aspose.HTML
title: 'Java rögzített szálkészlet: Képek számlálása párhuzamos fájlokban'
url: /hu/java/data-handling-stream-management/java-fixed-thread-pool-count-images-in-parallel-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java fixed thread pool – Párhuzamos képek számlálása útmutató

Gondolkodtál már azon, hogyan **java fixed thread pool**-ot használva vághatsz át tucatnyi HTML fájlon, és szerezhetsz gyors képszámlálást? Lehet, hogy egy könyvtárra bámultál, és azt gondoltad: „Tudnom kell, hány `<img>` címke van minden fájlban”, majd rájöttél, hogy egy egy‑szálas ciklus örökké tartana.

A jó hír, hogy nem kell saját szálkezelőt írnod vagy alacsony szintű `Thread` objektumokkal vesződni. Ebben az útmutatóban pontosan megmutatjuk, hogyan **számoljuk meg a képeket** egy *java fixed thread pool* segítségével, run tasks concurrently java, és elegánsan **shutdown executor service**, amikor a munka befejeződött.

Áttekintjük mindent a pool beállításától, a fájllista előkészítéséig, a párhuzamos feladatok benyújtásáig, a szélhelyzetek kezeléséig, egészen a kimenet ellenőrzéséig. A végére egy kész‑a‑futtatásra programot kapsz, amely bemutatja a **java parallel file processing**-t tiszta, karbantartható módon.

## Előfeltételek

Mielőtt belevágnánk, győződj meg róla, hogy rendelkezel:

- Java 17 vagy újabb (a kód a `var` kulcsszót használja a tömörség kedvéért, de szükség esetén lejjebb is használható).
- Aspose.HTML for Java a classpath‑odban – letöltheted a Maven Central‑ról:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

- Néhány HTML fájl, amelyet elemezni szeretnél (az útmutató feltételezi, hogy a `YOUR_DIRECTORY/` könyvtárban vannak).
- Egy IDE vagy build eszköz, amivel kényelmesen dolgozol – IntelliJ IDEA, VS Code, vagy egyszerű `javac` is megfelelő.

Ennyi. Nincs extra szerver, nincs Docker, csak tiszta Java és egy apró harmadik‑fél könyvtár.

## 1. lépés: java fixed thread pool létrehozása

A *java fixed thread pool* egy korlátozott számú munkás szálat biztosít, amelyek minden benyújtott feladatnál újra felhasználják magukat. Ez megakadályozza az új szálak folyamatos létrehozásának költségét, és korlátozza a párhuzamosság szintjét, ami kulcsfontosságú, amikor lemezről olvasol fájlokat.

```java
import java.util.concurrent.*;

public class ParallelImageCounter {
    // A pool of 4 threads – adjust based on your CPU cores and I/O profile
    private static final ExecutorService executor = Executors.newFixedThreadPool(4);
}
```

**Miért 4?** Ha egy négymagos laptopod van, négy szál tartja elfoglalva minden magot anélkül, hogy túlterhelné őket. Egy többmagos szerveren növelheted a számot, de ne feledd, hogy minden szál egy fájlkezelőt nyit, így a túl sok kimerítheti az operációs rendszer korlátait.

## 2. lépés: A elemzni kívánt HTML fájlok listázása

A **java parallel file processing** következő része egyszerűen egy tömb (vagy `List`) építése a fájlútvonalakból. Egy valódi projektben rekurzívan bejárhatod a könyvtárat, szűrhetsz kiterjesztés szerint, vagy adatbázisból olvashatsz útvonalakat. Íme a legegyszerűbb megközelítés:

```java
String[] htmlFiles = {
    "YOUR_DIRECTORY/a.html",
    "YOUR_DIRECTORY/b.html",
    "YOUR_DIRECTORY/c.html",
    "YOUR_DIRECTORY/d.html"
};
```

Ha dinamikus halmazt kell kezelni, cseréld le a statikus tömböt valami hasonlira:

```java
Path dir = Paths.get("YOUR_DIRECTORY");
String[] htmlFiles = Files.list(dir)
                         .filter(p -> p.toString().endsWith(".html"))
                         .map(Path::toString)
                         .toArray(String[]::new);
```

Ez a kódrészlet bemutatja a **java parallel file processing**-t tetszőleges számú fájlra anélkül, hogy a többi kódot módosítanád.

## 3. lépés: Feladatok benyújtása a **run tasks concurrently java**-hoz

Most jön a tutorial szíve – **run tasks concurrently java**-t fogunk végrehajtani úgy, hogy minden fájlhoz egy lambda‑t nyújtunk be. Minden feladat betölti az HTML dokumentumot az Aspose.HTML segítségével, lekérdezi az összes `<img>` elemet, és kiírja a számlálót.

```java
import com.aspose.html.HTMLDocument;

public static void main(String[] args) throws InterruptedException {
    for (String filePath : htmlFiles) {
        executor.submit(() -> {
            // Load the document – Aspose.HTML does the heavy lifting
            HTMLDocument document = new HTMLDocument(filePath);
            // querySelectorAll returns a NodeList; its length is the image count
            int imageCount = document.querySelectorAll("img").length;
            System.out.println(filePath + " contains " + imageCount + " images.");
        });
    }

    // Step 4 is next – gracefully shut down the pool
    shutdownAndAwaitTermination();
}
```

**Miért lambda?** A lambda rövid kódot eredményez, és elkerüli egy külön `Runnable` osztály létrehozását. A lambda automatikusan befogja a `filePath` változót, így minden feladat a saját fájlján dolgozik.

### Hogyan **képek számlálása** hatékonyan

Az Aspose.HTML egyszer olvassa be a fájlt, felépíti a DOM-ot, majd a `querySelectorAll("img")` O(n) időben fut, ahol *n* a csomópontok száma. A legtöbb HTML oldal esetén ez elhanyagolható. Ha gyorsabb, csak streaming megközelítést igényelnél (pl. gigabájt méretű fájlok esetén), áttérhetnél egy SAX parserre, de ez feláldozná az egyszerűséget, amit keresünk.

## 4. lépés: Helyes **shutdown executor service**

Soha ne felejtsd el leállítani a pool‑t, különben a JVM örökké futni fog. Az alábbi minta a javasolt módja a **shutdown executor service**-nek, miközben vársz, hogy az összes feladat befejeződjön:

```java
private static void shutdownAndAwaitTermination() {
    executor.shutdown(); // Disable new tasks from being submitted
    try {
        // Wait a while for existing tasks to terminate
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            executor.shutdownNow(); // Cancel currently executing tasks
            // Wait a second for tasks to respond to being cancelled
            if (!executor.awaitTermination(30, TimeUnit.SECONDS))
                System.err.println("Pool did not terminate");
        }
    } catch (InterruptedException ie) {
        // (Re-)Cancel if current thread also interrupted
        executor.shutdownNow();
        // Preserve interrupt status
        Thread.currentThread().interrupt();
    }
}
```

**Mi van, ha egy feladat elakad?** A `shutdownNow()` hívás megpróbálja megszakítani a futó szálakat. Ha a képszámláló logikád tiszteletben tartja a megszakítást (amit az Aspose.HTML nem blokkol I/O‑n), a pool tisztán leáll. Ez a minta az aranyszabvány minden **java fixed thread pool** használatához.

## 5. lépés: A kimenet ellenőrzése

Futtasd a programot az IDE‑dből vagy a parancssorból:

```bash
javac -cp "path/to/aspose-html.jar" ParallelImageCounter.java
java -cp ".:path/to/aspose-html.jar" ParallelImageCounter
```

A tipikus kimenet így néz ki:

```
YOUR_DIRECTORY/a.html contains 5 images.
YOUR_DIRECTORY/b.html contains 0 images.
YOUR_DIRECTORY/c.html contains 12 images.
YOUR_DIRECTORY/d.html contains 3 images.
```

Ha a számlálók bármilyen sorrendben jelennek meg, az várható – a szálak különböző időpontokban fejeződnek be. A lényeg, hogy minden fájl szerepel, és a program tisztán kilép a leállítási szekvencia után.

## Teljes működő példa (másolás‑beillesztés kész)

```java
import com.aspose.html.HTMLDocument;
import java.util.concurrent.*;

public class ParallelImageCounter {
    // 1️⃣ Fixed thread pool – change size based on your hardware
    private static final ExecutorService executor = Executors.newFixedThreadPool(4);

    public static void main(String[] args) throws InterruptedException {
        // 2️⃣ List of HTML files – replace with your own directory
        String[] htmlFiles = {
            "YOUR_DIRECTORY/a.html",
            "YOUR_DIRECTORY/b.html",
            "YOUR_DIRECTORY/c.html",
            "YOUR_DIRECTORY/d.html"
        };

        // 3️⃣ Submit a counting task for each file
        for (String filePath : htmlFiles) {
            executor.submit(() -> {
                HTMLDocument document = new HTMLDocument(filePath);
                int imageCount = document.querySelectorAll("img").length;
                System.out.println(filePath + " contains " + imageCount + " images.");
            });
        }

        // 4️⃣ Gracefully shut down the pool
        shutdownAndAwaitTermination();
    }

    // 5️⃣ Helper method to cleanly stop the executor
    private static void shutdownAndAwaitTermination() {
        executor.shutdown(); // Disable new tasks
        try {
            if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
                executor.shutdownNow(); // Cancel currently executing tasks
                if (!executor.awaitTermination(30, TimeUnit.SECONDS))
                    System.err.println("Pool did not terminate");
            }
        } catch (InterruptedException ie) {
            executor.shutdownNow();
            Thread.currentThread().interrupt();
        }
    }
}
```

### Várható eredmény

A kódrészlet futtatása kiírja minden fájl útvonalát, majd a benne lévő `<img>` címkék számát, ezután a JVM kilép. Nincs maradandó szál, nincs memória szivárgás.

## Gyakori buktatók és profi tippek

- **Pitfall:** `newCachedThreadPool()` használata egy *fixed* pool helyett. Ez korlátlan számú szálat hoz létre, ami nagy adatmennyiségnél kimerítheti a fájlleírókat. Maradj a `newFixedThreadPool`-nál.
- **Pro tip:** Ha a HTML fájlok nagyok, fontold meg a heap növelését (`-Xmx2g`) vagy válts streaming parserre. A legtöbb marketing oldal esetén az alap heap elegendő.
- **Pitfall:** Elfelejted meghívni a `shutdown()`-ot – az alkalmazás a eredmények kiírása után lefagy. A fenti `shutdownAndAwaitTermination` metódus ezt megbízhatóan kezeli.
- **Pro tip:** Naplózd minden feladat kezdő és befejező időpontját, ha teljesítménymérő adatokat szeretnél. Egy egyszerű `System.nanoTime()` a `HTMLDocument` konstrukció előtt és után megmutatja, mennyi ideig tartott a feldolgozás.
- **Pitfall:** A szálak számának kézi beállítása. Használd a `Runtime.getRuntime().availableProcessors()`-t, hogy ésszerű alapértelmezettet válassz:

```java
int cores = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(cores);
```

## Kapcsolódó témák, amelyeket érdemes felfedezni

- **run tasks concurrently java** `CompletableFuture`-val kifejezőbb pipeline-okhoz.
- Képszámlálások adatbázisba mentése analitikai műszerfalakhoz.
- **java parallel file processing** használata a `java.nio.file.Files.walk` API-val kombinálva streamekkel.
- Egyedi `ThreadFactory` megvalósítása, hogy a szálak értelmes neveket kapjanak (segít a hibakeresésben).

## Összegzés

Most végigvettünk egy teljes, önálló példát, amely bemutatja, hogyan lehet egy **java fixed thread pool**-t felhasználni a **how to count images** több HTML fájlon keresztül, miközben megmutatja a helyes **shutdown executor service** módját. A minta szépen skálázható – cseréld le a fájl tömböt egy dinamikus listára, növeld a pool méretét, és egy robusztus megoldásod lesz bármilyen **java parallel file processing** feladatra.

Próbáld ki, állítsd be a szálak számát, és esetleg adj hozzá CSV exportot az eredményekhez. A határ csak a képzeleted, ha egy szilárd párhuzamossági alapot kombinálsz egy praktikus könyvtárral, mint az Aspose.HTML. Jó kódolást!

![java fixed thread pool diagram](image.png){alt="java fixed thread pool diagram"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}