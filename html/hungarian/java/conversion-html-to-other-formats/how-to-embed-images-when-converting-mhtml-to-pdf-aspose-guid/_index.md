---
category: general
date: 2026-03-29
description: Hogyan ágyazzunk be képeket MHTML PDF-re konvertálása során az Aspose
  HTML használatával. Csökkentsük a PDF fájlméretét, és sajátítsuk el az Aspose HTML
  → PDF technikákat percek alatt.
draft: false
keywords:
- how to embed images
- convert mhtml to pdf
- reduce pdf file size
- aspose html to pdf
- reduce pdf size
language: hu
og_description: Hogyan ágyazzunk be képeket az MHTML PDF-re konvertálása során az
  Aspose HTML segítségével. Tanulja meg, hogyan csökkentse a PDF fájl méretét, és
  hozza ki a legtöbbet az Aspose HTML‑ből PDF‑be konvertálásból.
og_title: Hogyan ágyazzunk be képeket MHTML PDF-re konvertálásakor – Aspose útmutató
tags:
- Aspose
- Java
- PDF
- MHTML
title: Hogyan ágyazzuk be a képeket MHTML PDF-re konvertálásakor – Aspose útmutató
url: /hu/java/conversion-html-to-other-formats/how-to-embed-images-when-converting-mhtml-to-pdf-aspose-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan ágyazzunk be képeket MHTML‑ról PDF‑re konvertáláskor – Aspose útmutató

Gondolkodtál már azon, **hogyan ágyazzunk be képeket** egy MHTML‑ról PDF‑re konvertálás során, miközben a kapott fájl karcsú marad? Nem vagy egyedül. Sok fejlesztő szembesül azzal, hogy a PDF‑jeik felrobban, mert minden erőforrás—betűkészletek, szkriptek, még a kis ikonok is—belekerül. A jó hír? Az Aspose.HTML for Java segítségével megmondhatod a konvertálónak, hogy **csak a képeket** ágyazza be, a többit külső hivatkozásként hagyja. Ez az egyetlen módosítás gyakran drámaian csökkenti a PDF méretét.

Ebben az útmutatóban végigvezetünk egy MHTML‑jelentés PDF‑re konvertálásán, a **képek beágyazásának** módjára fókuszálunk, és néhány extra tippet adunk a **PDF fájlméret csökkentéséhez**. A végére egy kész, futtatható Java osztályt kapsz, megérted, miért fontos csak a képeket beágyazni, és tudni fogod, hová fordulj, ha később betűkészleteket vagy más erőforrásokat kell beágyaznod. Nincsenek homályos „lásd a dokumentációt” rövidítések – csak egy teljes, másolás‑beillesztés megoldás.

## Amit megtanulsz

- A pontos API hívások, amelyekkel **MHTML‑t PDF‑re konvertálhatsz** az Aspose.HTML‑el.
- Hogyan konfiguráld a `PdfConversionOptions`‑t, hogy a konvertáló **csak a képeket ágyazza be**.
- Miért segít a csak képek beágyazása a **PDF méret csökkentésében**, és mikor lehet más beállítást választani.
- Egy teljes, futtatható Java példa, amelyet bármely Maven/Gradle projektbe beilleszthetsz.
- Gyakori buktatók (hiányzó erőforrások, rossz fájlutak) és gyors megoldások.

### Előfeltételek

- Java 8 vagy újabb telepítve.
- Maven vagy Gradle a függőségek kezeléséhez (a Maven példát mutatjuk).
- Aspose.HTML for Java könyvtár (letöltheted egy ingyenes próbaverziót az Aspose weboldaláról).
- Egy MHTML fájl, amelyet PDF‑re szeretnél konvertálni (a példában `report.mhtml`‑t használunk).

> **Pro tip:** Tartsd a MHTML‑t és a kimeneti PDF‑t ugyanabban a mappában a tesztelés során; a relatív útvonalak rendben tartják a dolgokat.

---

## 1. lépés – Aspose.HTML hozzáadása a projekthez

Ha Maven‑t használsz, illeszd be a következőt a `pom.xml`‑be. A megjelenített verzió a legújabb 2026. március állapotában; ellenőrizd az Aspose repóját az újabb kiadásokért.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

Gradle esetén az ekvivalens:

```groovy
implementation 'com.aspose:aspose-html:23.12'
```

Miután a függőség feloldódott, készen állsz a szükséges osztályok importálására.

## 2. lépés – Konverziós beállítások létrehozása és a beágyazási mód beállítása

A **képek beágyazásának** lényege a `PdfConversionOptions`. Alapértelmezés szerint az Aspose *minden* erőforrást beágyaz (betűkészletek, CSS, képek). Ezt átállítjuk `EMBED_IMAGES_ONLY`‑ra.

```java
// Step 2: Prepare conversion options – embed only images
PdfConversionOptions options = new PdfConversionOptions();
options.setResourceEmbeddingMode(ResourceEmbeddingMode.EMBED_IMAGES_ONLY);
```

Miért fontos ez? Képzelj el egy vállalati jelentést, amely egy hálózati megosztáson tárolt vállalati betűkészletre hivatkozik. Ennek a betűkészletnek a beágyazása több száz kilobájttal növeli a PDF‑et, még akkor is, ha a megjelenítő távolról le tudja tölteni. Ha csak a képeket ágyazzuk be, a PDF megőrzi a szükséges vizuális hűséget, miközben könnyű marad.

## 3. lépés – A konverzió végrehajtása

Most meghívjuk a `Converter.convert`‑et, megadva a forrás MHTML útvonalát, a cél PDF útvonalát és a most beállított opciókat.

```java
// Step 3: Convert MHTML to PDF using the options above
String sourcePath = "YOUR_DIRECTORY/report.mhtml";
String targetPath = "YOUR_DIRECTORY/report.pdf";

Converter.convert(sourcePath, targetPath, options);
```

Ha minden helyesen van beállítva, egy `report.pdf` fájl jelenik meg a MHTML fájl mellett. Nyisd meg – minden eredeti jelentésbeli képnek ott kell lennie, míg a betűkészletek és a CSS külső hivatkozások maradnak.

## 4. lépés – A PDF méretcsökkenés ellenőrzése

Egy gyors ellenőrzés segít megerősíteni, hogy valóban **csökkentetted a PDF méretét**. Hasonlítsd össze a fájlméretet a beágyazási mód váltása előtt és után:

```java
File before = new File("YOUR_DIRECTORY/report_full.pdf"); // generated with default settings
File after  = new File(targetPath); // our image‑only PDF

System.out.println("Full embed size: " + before.length() / 1024 + " KB");
System.out.println("Images‑only size: " + after.length() / 1024 + " KB");
```

A legtöbb esetben 30‑70 %-os csökkenést látsz, attól függően, hány betűkészlet vagy CSS fájl volt eredetileg beágyazva. Ez jelentős előny mindazoknak, akik a weben keresztül szállítanak PDF‑eket, vagy felhőbuckets‑ben tárolják őket.

## 5. lépés – Teljes, futtatható példa

Az alábbiakban a teljes Java osztályt találod, amelyet beilleszthetsz az IDE‑dbe. Cseréld le a `YOUR_DIRECTORY`‑t arra a konkrét mappára, ahol a `report.mhtml` található.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfConversionOptions;
import com.aspose.html.converters.ResourceEmbeddingMode;

import java.io.File;

public class MhtmlToPdf {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define source and destination ----------
        String sourcePath = "YOUR_DIRECTORY/report.mhtml";
        String targetPath = "YOUR_DIRECTORY/report.pdf";

        // ---------- Step 2: Set conversion options (embed only images) ----------
        PdfConversionOptions conversionOptions = new PdfConversionOptions();
        conversionOptions.setResourceEmbeddingMode(ResourceEmbeddingMode.EMBED_IMAGES_ONLY);

        // ---------- Step 3: Run the conversion ----------
        Converter.convert(sourcePath, targetPath, conversionOptions);
        System.out.println("Conversion complete! PDF saved to: " + targetPath);

        // ---------- Step 4: (Optional) Show size reduction ----------
        File outputPdf = new File(targetPath);
        System.out.println("Resulting PDF size: " + outputPdf.length() / 1024 + " KB");
    }
}
```

**Várható kimenet** (a konzolon):

```
Conversion complete! PDF saved to: YOUR_DIRECTORY/report.pdf
Resulting PDF size: 842 KB
```

Nyisd meg a `report.pdf`‑t bármely nézőben; minden eredeti képnek helyesen kell megjelenülnie. Ha hiányzó képeket észlelsz, ellenőrizd, hogy a MHTML‑ben szereplő kép‑URL‑ek abszolútak-e, vagy hogy a fájlok elérhetők‑e a konvertáló gépről.

## Gyakori kérdések és szél‑eset kezelése

### Mi van, ha *valóban* be kell ágyazni a betűkészleteket?

Állítsd a `ResourceEmbeddingMode`‑t `EMBED_ALL`‑ra vagy `EMBED_FONTS_ONLY`‑ra. Az enum négy lehetőséget kínál:

| Mód                     | Mi kerül beágyazásra |
|--------------------------|----------------------|
| `EMBED_ALL`              | Images, fonts, CSS |
| `EMBED_IMAGES_ONLY`      | Only images (our default) |
| `EMBED_FONTS_ONLY`       | Only fonts |
| `EMBED_NONE`             | Nothing (external references only) |

### A MHTML‑m külső CSS‑t tartalmaz, ami a layout‑ot befolyásolja – a PDF hibás lesz?

Mivel nem ágyazzuk be a CSS‑t, a konvertáló továbbra is letölti azt a konverzió során. Ha a CSS egy intraneten van, amelyet a konvertáló szerver nem ér el, a layout visszaeshet az alapértelmezett beállításokra. Ilyen esetben vagy ágyazzuk be a CSS‑t (`EMBED_ALL`), vagy másoljuk le a stíluslapot helyi fájlba, és módosítsuk a MHTML‑t, hogy a helyi fájlra mutasson.

### Batch‑processzálhatok egy mappát MHTML fájlokkal?

Természetesen. Csomagold a konverziós logikát egy ciklusba, amely a `File.listFiles()`‑t iterálja, és ennek megfelelően állítsd be a célfájl nevét. Ne feledd, hogy a teljesítmény érdekében egyetlen `PdfConversionOptions` példányt újrahasználj.

### Mi a helyzet a memóriakihasználással nagy dokumentumok esetén?

Az Aspose.HTML adatfolyamként dolgozik, így a memóriahasználat mérsékelt marad. Nagyon nagy képek azonban még így is memóriacsúcsokat okozhatnak. Ha `OutOfMemoryError`‑t kapsz, fontold meg a képek lecsökkentését a beágyazás előtt – az Aspose kínál `ImageConversionOptions`‑t erre, de ez egy másik útmutató témája.

## Összegzés

Most már tudod, **hogyan ágyazzunk be képeket** MHTML‑ról PDF‑re konvertáláskor az Aspose.HTML‑el, és láttad, miért csökkentheti ez a kis beállítás a **PDF fájlméretet** drámaian. A teljes, másolás‑beillesztés Java példa bemutatja a teljes folyamatot – a Maven függőség hozzáadásától a végső fájlméret kiírásáig.

Innen tovább:

- Kísérletezz a `EMBED_FONTS_ONLY`‑val, ha a PDF‑eidnek teljesen önállónak kell lenniük.
- Automatizáld a kötegelt konverziókat egy teljes jelentésmappa számára.
- Kombináld ezt a technikát az Aspose PDF optimalizációs API‑kkal a még kisebb fájlokért.

Akár jelentéskészítő szolgáltatást építesz, akár e‑mail‑PDF csővezetéket, vagy csak archivált weboldalakat tisztítasz, a beágyazott elemek szabályozása kulcsfontosságú a teljesítmény és a költségek szempontjából. Próbáld ki, finomítsd a beállításokat, és tedd a PDF‑eidet a lehető legkarcsúbbá.

*Boldog kódolást!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}