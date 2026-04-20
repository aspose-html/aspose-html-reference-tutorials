---
category: general
date: 2026-02-22
description: Hozzon létre fix szálkészletet a HTML PDF konvertálás hatékony kötegelt
  feldolgozásához Java-ban. Ismerjen meg egy szálkészlet Java példát, amely gyorsan
  menti a HTML-t PDF-be.
draft: false
keywords:
- create fixed thread pool
- convert html to pdf
- batch html to pdf
- thread pool java example
- save html as pdf
language: hu
og_description: Hozzon létre fix szálkészletet a HTML PDF-re konvertálás kötegelt
  feldolgozásához. Ez az útmutató végigvezet egy szálkészlet Java példán, amely hatékonyan
  menti a HTML-t PDF-be.
og_title: Fix szálkészlet létrehozása kötegelt HTML‑PDF konverzióhoz
tags:
- Java
- Concurrency
- PDF Generation
title: Fix szálkészlet létrehozása kötegelt HTML‑PDF konverzióhoz
url: /hu/java/conversion-html-to-other-formats/create-fixed-thread-pool-for-batch-html-to-pdf-conversion/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Fix szálkészlet létrehozása kötegelt HTML‑PDF konverzióhoz

Gondolkodtál már azon, hogyan **hozz létre fix szálkészletet**, amely egy halom HTML‑fájlt PDF‑vé alakít anélkül, hogy leterhelné a CPU‑t? Nem vagy egyedül. Ha tucatnyi—vagy akár több száz—oldalt kell feldolgozni, egyesével futtatni őket lassú, de egy korlátlan szálkészlet indítása gyorsan kimerítheti a memóriát.  

Ebben a tutorialban megoldjuk ezt a dilemmát egy **thread pool Java példával**, amely **kötegeli a HTML‑t PDF‑vé**, elmenti az eredményt, és tisztán leáll. A végére **párhuzamosan tudsz HTML‑t PDF‑vé konvertálni**, és megérted, miért a fix szálkészlet a legoptimálisabb a legtöbb kötegelt feladathoz.

## Mit fogsz megtanulni

- Egy teljes, futtatható Java programot, amely fix szálkészletet hoz létre.
- Sor‑ról‑sorra magyarázatot minden sorra, hogy tudd, **miért** csinálunk úgy, ahogy csináljuk.
- Útmutatót a PDF‑könyvtár kiválasztásához (hogy **HTML‑t PDF‑ként menthess** anélkül, hogy kódrészleteket kellene keresgélned).
- Tippeket a hibakezeléshez, a pool méretének finomhangolásához, és a megoldás nagyobb kötegekhez való kiterjesztéséhez.

**Előfeltételek** – Java 8+ telepítve, egy alap IDE (IntelliJ, Eclipse vagy VS Code), és egy PDF‑konverziós könyvtár a classpath‑on (a példában *OpenHTMLtoPDF*-t használunk). Más keretrendszer nem szükséges.

---

## Fix szálkészlet létrehozása – Miért fontos

Amikor **fix szálkészletet hozol létre**, a JVM‑nek pontosan megmondod, hány munkás szál futhat egyszerre. Ez megakadályozza a szál‑létrehozási viharokat, kiszámíthatóvá teszi a memóriahasználatot, és lehetővé teszi az OS‑nek, hogy hatékonyan ütemezze a munkát.  

Gondolj rá úgy, mint egy pénztárra egy szupermarketben: egy meghatározott számú pénztárat nyitsz, a vásárlók sorba állnak, és a sor megszűnésekor bezárod a pénztárakat. A `FixedThreadPool` ugyanígy működik — a feladatok sorban várakoznak, de nem jönnek létre extra szálak „repülő” módon.

```java
// Step 1: Build a fixed‑size thread pool with 4 workers
ExecutorService threadPool = Executors.newFixedThreadPool(4);
```

A `4` szám jó kiindulási pont egy négymagos laptopon; a CPU‑magok és az I/O jellemzők alapján módosítható.

## Kötegelt HTML‑PDF konverzió: Minden oldal átalakítása

Most, hogy a pool létezik, fel kell töltenünk feladatokkal, amelyek **HTML‑t PDF‑vé konvertálnak**. Minden feladat:

1. Betölt egy HTML‑dokumentumot a lemezről.
2. Átadja a PDF‑könyvtárnak.
3. Visszaírja a kapott PDF‑et ugyanabba a könyvtárba.

Mivel a munka I/O‑intenzív (fájlok olvasása, PDF‑ek írása), egy kis pool gyakran jobb teljesítményt nyújt, mint egy nagyobb, amely csak a lemezre vár.

```java
// Step 2: Submit a conversion job for every HTML file you have
for (int i = 0; i < 4; i++) {
    final int pageIndex = i;               // capture loop variable for the lambda
    threadPool.submit(() -> {
        // Load the HTML file
        Path htmlPath = Paths.get("YOUR_DIRECTORY/page" + pageIndex + ".html");
        String html = Files.readString(htmlPath, StandardCharsets.UTF_8);

        // Convert and save as PDF
        Path pdfPath = Paths.get("YOUR_DIRECTORY/page" + pageIndex + ".pdf");
        convertHtmlToPdf(html, pdfPath);
    });
}
```

> **Pro tipp:** Ha több mint négy oldalad van, egyszerűen növeld a ciklus határát vagy olvasd be a fájllistát dinamikusan — `Files.list(Paths.get("YOUR_DIRECTORY")).filter(p -> p.toString().endsWith(".html"))` gond nélkül megoldja.

## Thread Pool Java példa részletesen

Vessük szét a **thread pool Java példát** soronként, hogy ne csak másolj kódot, hanem valóban megértsd a folyamatot.

| Sor | Mit csinál | Miért fontos |
|------|------------|--------------|
| `ExecutorService threadPool = Executors.newFixedThreadPool(4);` | Pontosan négy szálból álló poolt hoz létre. | Biztosítja a korlátozott számú egyidejű konverziót, elkerülve a memória‑kimerülést. |
| `for (int i = 0; i < 4; i++) { … }` | Végigiterál a feldolgozni kívánt oldalakon. | A ciklus vezérli a feladatok létrehozását; a statikus határ helyettesíthető dinamikus listával. |
| `final int pageIndex = i;` | Elkapja a ciklusindexet a lambda‑ban való használatra. | `final` (vagy effektíve final) nélkül a lambda változója változó lenne, ami hibás fájlneveket eredményez. |
| `threadPool.submit(() -> { … });` | Egy `Runnable`‑t ad át a poolnak aszinkron végrehajtásra. | A pool ütemezi a runnable‑t egy szabad munkás szálra, miközben a fő szál továbbra is feladatokat sorol be. |
| `Files.readString(htmlPath, …);` | Beolvassa a HTML‑fájlt egy `String`‑be. | Szükséges, mert a legtöbb PDF‑könyvtár HTML‑t stringként vagy stream‑ként vár. |
| `convertHtmlToPdf(html, pdfPath);` | Meghív egy segédfüggvényt, amely a tényleges konverziót végzi. | Tiszta lambda‑t biztosít, és elkülöníti a könyvtár‑specifikus kódot. |

Alább a teljes segédfüggvény, amely **OpenHTMLtoPDF**‑t használ, egy könnyű könyvtárat, amely **HTML‑t PDF‑ként ment** egyetlen hívással.

```java
import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;

private static void convertHtmlToPdf(String html, Path outputPdf) throws IOException {
    try (OutputStream os = Files.newOutputStream(outputPdf)) {
        PdfRendererBuilder builder = new PdfRendererBuilder();
        builder.withHtmlContent(html, null);     // base URI is null because we use absolute paths
        builder.toStream(os);
        builder.run();                           // blocks until PDF is written
    } catch (Exception e) {
        // Wrap any checked exception as an unchecked one so the lambda can compile
        throw new RuntimeException("Failed to convert HTML to PDF for " + outputPdf, e);
    }
}
```

> **Miért OpenHTMLtoPDF?** Tiszta Java, nincs natív függőség, és támogatja a CSS‑t, így a létrehozott PDF‑ek nagyon hasonlítanak az eredeti weboldalakra. Ha inkább iText‑et vagy Flying Saucer‑t használnál, csak cseréld ki a `convertHtmlToPdf` belsejét.

## HTML‑t PDF‑ként mentés – Könyvtár választás

Lehet, hogy felteszed: „Melyik könyvtárral **konvertáljam a HTML‑t PDF‑vé**?” Íme egy gyors összehasonlítás:

| Könyvtár | Maven koordináták | Előnyök | Hátrányok |
|---------|-------------------|--------|-----------|
| OpenHTMLtoPDF | `com.openhtmltopdf:openhtmltopdf-pdfbox:1.0.10` | Tiszta Java, jó CSS‑támogatás, könnyű | Korlátozott fejlett PDF‑funkciók (pl. titkosítás) |
| iText 7 + html2pdf | `com.itextpdf:html2pdf:3.0.6` | Gazdag funkciókészlet, kereskedelmi támogatás | Sok esetben fizetős licenc szükséges |
| Flying Saucer | `org.xhtmlrenderer:flying-saucer-pdf:9.1.22` | Érett, régebbi Java verziókkal is működik | Lassú nagy dokumentumoknál, kevésbé teljes CSS‑lefedettség |

Válaszd azt, amelyik a projekted igényeihez legjobban illeszkedik. Egy **kötegelt HTML‑PDF** feladathoz az OpenHTMLtoPDF általában a legjobb választás: gyors, egyszerű és ingyenes.

## Elegáns leállítás és hibakezelés

Ha a végrehajtót futtatva hagyod, az megakadályozhatja a JVM kilépését, és a szálakban keletkező elkapatlan kivételek nehezen észlelhetők. Az alábbi minta biztosítja a rendezett leállítást:

```java
// Step 5: Initiate an orderly shutdown after all tasks are queued
threadPool.shutdown();                     // No new tasks accepted
try {
    // Wait up to 60 seconds for existing tasks to finish
    if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
        threadPool.shutdownNow();          // Force shutdown if tasks linger
    }
} catch (InterruptedException ex) {
    threadPool.shutdownNow();              // Preserve interrupt status
    Thread.currentThread().interrupt();
}
```

- `shutdown()` jelzi a poolnak, hogy fejezze be a már folyamatban levő feladatokat, de ne fogadjon újakat.
- `awaitTermination` blokkol, amíg minden be nem fejeződik vagy a timeout lejár.
- `shutdownNow()` megpróbálja megszakítani a futó feladatokat — hasznos kényszerített leállításkor.

Ha bármely konverzió hibát okoz, a `RuntimeException` feljebb kerül az executor‑ba, amely alapértelmezés szerint a konzolra logolja. Éles környezetben érdemes egy saját `ThreadPoolExecutor`‑t csatolni, amely felülírja az `afterExecute` metódust, és a naplózást fájlba vagy monitorozó rendszerbe irányítja.

## Teljes működő példa

Mindent egy helyen, itt egy önálló Java osztály, amelyet be tudsz másolni a `src/main/java/com/example/BatchPdfConverter.java`‑ba. Győződj meg róla, hogy az OpenHTMLtoPDF függőség a classpath‑on van.

```java
package com.example;

import java.io.*;
import java.nio.charset.StandardCharsets;
import java.nio.file.*;
import java.util.concurrent.*;

import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;

/**
 * Demonstrates how to create a fixed thread pool to batch HTML to PDF conversion.
 * Adjust POOL_SIZE and DIRECTORY constants to fit your environment.
 */
public class BatchPdfConverter {

    private static final int POOL_SIZE = 4;                     // Number of parallel workers
    private static final Path DIRECTORY = Paths.get("YOUR_DIRECTORY"); // Change to your folder

    public static void main(String[] args) {
        ExecutorService threadPool = Executors.newFixedThreadPool(POOL_SIZE);

        // Discover all *.html files in the target directory
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(DIRECTORY, "*.html")) {
            for (Path htmlPath : stream) {
                threadPool.submit(() -> processFile(htmlPath));
            }
        } catch (IOException e) {
            System.err.println("Failed to list HTML files: " + e.getMessage());
        }

        // Graceful shutdown
        thread

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}