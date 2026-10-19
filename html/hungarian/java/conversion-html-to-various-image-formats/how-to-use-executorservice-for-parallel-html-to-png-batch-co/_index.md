---
category: general
date: 2026-02-21
description: Hogyan használjuk az ExecutorService-t a HTML gyors PNG-re konvertálásához.
  Tanulja meg a HTML fájlok kötegelt átalakítását párhuzamos feladatokkal Java-ban.
draft: false
keywords:
- how to use executorservice
- convert html to png
- how to run parallel tasks
- how to convert html to png
- batch convert html files
language: hu
og_description: Hogyan használjuk az ExecutorService-t HTML fájlok kötegelt PNG-re
  konvertálásához. Lépésről lépésre útmutató teljes Java példával.
og_title: Hogyan használjuk az ExecutorService‑t párhuzamos HTML‑PNG konverzióhoz
tags:
- Java
- concurrency
- Aspose.HTML
- image‑conversion
title: Hogyan használjuk az ExecutorService‑t párhuzamos HTML‑to‑PNG kötegelt konverzióhoz
url: /hu/java/conversion-html-to-various-image-formats/how-to-use-executorservice-for-parallel-html-to-png-batch-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjuk az ExecutorService‑t párhuzamos HTML‑ról‑PNG kötegelt átalakításhoz

Gondolkodtál már azon, **hogyan használjuk az ExecutorService‑t**, amikor egy mappában rengeteg HTML‑oldal van, amelyeket PNG képekké kell konvertálni? Nem vagy egyedül – sok fejlesztő ütközik ebbe a problémába, amikor a web‑jelentéskészítő folyamatuk egyetlen szálas átalakítási ciklusnál akad el.  

A jó hír? Néhány Java sor és az erőteljes Aspose.HTML `Converter` segítségével fel tudsz állítani egy munkás szálakból álló medencét, minden HTML‑fájlt átadhatsz a konverternek, és párhuzamosan megjelennek a képek. Ebben az útmutatóban érintjük a **convert html to png** alapjait, megmutatjuk, **hogyan futtassunk párhuzamos feladatokat**, és adunk egy azonnal futtatható **batch convert html files** szkriptet.

## Előfeltételek

- Java 17 vagy újabb (a kód a modern `java.nio.file` API‑t használja).  
- Aspose.HTML for Java könyvtár a classpath‑on. Letöltheted a Maven Central‑ról:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

- Egy könyvtár, amely tartalmazza a forrás `.html` fájlokat, valamint egy üres kimeneti mappát.  
- Mérsékelt mennyiségű RAM – minden konverzió saját szálban fut, ezért a medence méretének meg kell egyeznie a rendelkezésre álló CPU‑magok számával.

> **Pro tipp:** Ha hyper‑threadinggel rendelkező gépen dolgozol, a `Runtime.getRuntime().availableProcessors()` általában a legoptimálisabb magszámot adja vissza.

## 1. lépés – Bemeneti és kimeneti útvonalak definiálása

Először meg kell mondanunk a Java‑nak, hol vannak a HTML‑fájlok, és hová kerüljenek a PNG‑k. A `Path` objektumok használata platform‑független kódot eredményez.

```java
import java.nio.file.*;

public class ParallelBatchConversion {
    public static void main(String[] args) throws Exception {
        // Input folder containing .html files
        Path inputDir  = Paths.get("YOUR_DIRECTORY/input/html");
        // Output folder for the generated .png files
        Path outputDir = Paths.get("YOUR_DIRECTORY/output/png");

        // Ensure the output folder exists
        Files.createDirectories(outputDir);
```

> **Miért fontos:** A kimeneti könyvtár előzetes létrehozása megakadályozza a `FileNotFoundException`‑t, amikor az első munkás szál megpróbál egy fájlt írni.

## 2. lépés – Fix méretű szálmedence építése

A **hogyan használjuk az ExecutorService‑t** lényege egy olyan medence létrehozása, amely megfelel a hardverednek. Egy *fix* medence garantálja, hogy ne indítsunk több szálat, mint amennyit ténylegesen tudunk futtatni.

```java
        // Create a thread pool sized to the number of available CPU cores
        ExecutorService pool = Executors.newFixedThreadPool(
                Runtime.getRuntime().availableProcessors());
```

> **Magyarázat:** Az `ExecutorService` elrejti az alacsony szintű szálkezelést. A `newFixedThreadPool` használatával a JVM újrahasználja a szálakat, ami csökkenti a folyamatos létrehozás és megsemmisítés terhelését.

## 3. lépés – Egy konverziós feladat benyújtása minden HTML fájlhoz

Most bejárjuk a bemeneti könyvtárat, kiválasztjuk az összes `*.html` fájlt, és átadjuk őket a medencének. Minden feladat egy apró lambda, amely meghívja a `Converter.convert`‑ot.

```java
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(inputDir, "*.html")) {
            for (Path htmlFile : stream) {
                pool.submit(() -> {
                    try {
                        // Build the output filename by swapping .html for .png
                        String outputFile = outputDir.resolve(
                                htmlFile.getFileName().toString().replaceAll("\\.html$", ".png"))
                                .toString();

                        // Perform the actual conversion
                        Converter.convert(htmlFile.toString(), outputFile);
                        System.out.println("Converted: " + htmlFile.getFileName());
                    } catch (Exception e) {
                        System.err.println("Failed: " + htmlFile.getFileName()
                                           + " – " + e.getMessage());
                    }
                });
            }
        }
```

### Mi történik a háttérben?

1. **DirectoryStream** lusta módon olvassa a fájlneveket, így a memóriahasználat alacsony marad még több ezer fájl esetén is.  
2. A lambda befogja a `htmlFile` és `outputDir` változókat – nincs szükség külön `Runnable` osztályra.  
3. A `Converter.convert` egy blokkoló hívás, amely beolvassa a HTML‑t, rendereli, és PNG‑t ír ki. Mivel minden hívás saját szálban fut, több fájl kerül egyszerre feldolgozásra – pontosan azt a viselkedést, amit **run parallel tasks** esetén elvársz.

## 4. lépés – A medence elegáns leállítása

Miután az összes feladat be lett sorolva, azt mondjuk a medencének, hogy ne fogadjon új munkát, és várjuk meg, amíg minden befejeződik. Ha valami elakad, az időkorlát egy óra után megszakad, ami a legtöbb kötegelt feladathoz bőven elegendő.

```java
        // No more tasks will be submitted
        pool.shutdown();

        // Wait up to 1 hour for all conversions to complete
        if (!pool.awaitTermination(1, TimeUnit.HOURS)) {
            System.err.println("Timeout: some files didn't finish in time.");
        }

        System.out.println("All conversions completed.");
    }
}
```

> **Szélsőséges eset:** Ha rendkívül nagy HTML‑fájljaid vannak, érdemes lehet növelni az időkorlátot vagy figyelni a memóriahasználatot. A `pool.setRejectedExecutionHandler(new ThreadPoolExecutor.CallerRunsPolicy())` hozzáadása arra kényszeríti a hívó szálat, hogy a felesleges feladatokat is végrehajtsa, így elkerülhető a `RejectedExecutionException`.

## Teljes, azonnal futtatható példa

Az alábbiakban a teljes program látható, amely egyszerűen beilleszthető egy `ParallelBatchConversion.java` fájlba.

```java
import com.aspose.html.converters.Converter;
import java.nio.file.*;
import java.util.concurrent.*;

public class ParallelBatchConversion {
    public static void main(String[] args) throws Exception {
        // Step 1: Define source and destination folders
        Path inputDir  = Paths.get("YOUR_DIRECTORY/input/html");
        Path outputDir = Paths.get("YOUR_DIRECTORY/output/png");
        Files.createDirectories(outputDir);

        // Step 2: Create a thread pool sized to the available CPU cores
        ExecutorService pool = Executors.newFixedThreadPool(
                Runtime.getRuntime().availableProcessors());

        // Step 3: Submit a conversion task for each HTML file found
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(inputDir, "*.html")) {
            for (Path htmlFile : stream) {
                pool.submit(() -> {
                    try {
                        String outputFile = outputDir.resolve(
                                htmlFile.getFileName().toString().replaceAll("\\.html$", ".png"))
                                .toString();
                        Converter.convert(htmlFile.toString(), outputFile);
                        System.out.println("Converted: " + htmlFile.getFileName());
                    } catch (Exception e) {
                        System.err.println("Failed: " + htmlFile.getFileName()
                                           + " – " + e.getMessage());
                    }
                });
            }
        }

        // Step 4: Shut down the pool and wait for all conversions to finish
        pool.shutdown();
        if (!pool.awaitTermination(1, TimeUnit.HOURS)) {
            System.err.println("Timeout: some files didn't finish in time.");
        }
        System.out.println("All conversions completed.");
    }
}
```

### Várt kimenet

A program futtatása minden sikeres konverzióhoz egy sort ír ki:

```
Converted: report1.html
Converted: dashboard.html
Converted: summary.html
All conversions completed.
```

Ha egy fájl hibát okoz, egy hibaüzenet jelenik meg a kivétel szövegével, ami megkönnyíti a hibakeresést.

## Hogyan bővítsük ezt a mintát

- **Különböző képformátumok:** Cseréld le a `.png` kiterjesztést `.jpg` vagy `.bmp`‑re, és állítsd be az Aspose konverziós opciókat ennek megfelelően.  
- **Dinamikus szál szám:** I/O‑központú terhelés esetén növelheted a medence méretét (`availableProcessors() * 2`).  
- **Folyamatfigyelés:** Cseréld le a `System.out.println`‑t egy szálbiztos progress bar könyvtárra, például `jline`‑ra, vagy logolj egy fájlba.  
- **Hibakezelés:** Gyűjtsd össze a sikertelen útvonalakat egy `List<Path>`‑be, és próbáld újra a fő ciklus befejezése után.

## Gyakran ismételt kérdések

**K: Működik ez Windows‑on és Linux‑on is?**  
V: Igen. A `java.nio.file` elrejti az alatta lévő fájlrendszert, így a kód változtatás nélkül fut minden Java‑t támogató operációs rendszeren.

**K: Mi van, ha több mint 10 000 HTML fájlom van?**  
V: A `DirectoryStream` iterátor lusta módon olvassa a bejegyzéseket, így a memóriahasználat alacsony marad. Csak győződj meg róla, hogy a lemezen elegendő szabad hely van a PNG kimenethez.

**K: Korlátozhatom a konverziók memóriahasználatát?**  
V: Az Aspose.HTML lehetővé teszi a renderelő motor konfigurálását `HtmlLoadOptions` és `ImageSaveOptions` segítségével. Beállíthatsz maximális bitmap méretet vagy alacsony minőségű renderelést a RAM‑fogyasztás kordozásához.

## Összegzés

Áttekintettük, **hogyan használjuk az ExecutorService‑t** **batch convert html files** PNG képekké, megmagyaráztuk, miért a fix méretű medence a legoptimálisabb a CPU‑központú rendereléshez, és adtunk egy teljes, beilleszthető Java programot. A fenti lépések követésével egy lassú, egy szálas ciklust gyors, skálázható csővezetékké alakíthatsz, amely egyetlen parancsra több ezer fájlt képes feldolgozni.

Készen állsz a következő kihívásra? Próbáld ki a `Converter.convert` helyett az Aspose PDF exportot, hogy **convert html to pdf**‑t valósíts meg, vagy integráld ezt a logikát egy Spring Boot mikro‑szolgáltatásba, amely feltöltés‑és‑konvertál kéréseket fogad. A lényeg – az `ExecutorService` használata **run parallel tasks**‑hez – változatlan, és számtalan kötegelt feldolgozási szituációban hasznos lesz.

Boldog kódolást, és legyenek a szálaid mindig élőek! 

![hogyan használjuk az executorservice diagram](placeholder.png "Diagram a szálmedence munkafolyamatáról párhuzamos HTML‑ról‑PNG konvertáláshoz")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}