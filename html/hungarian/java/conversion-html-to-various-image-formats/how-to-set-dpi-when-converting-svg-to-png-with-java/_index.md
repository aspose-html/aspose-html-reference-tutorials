---
category: general
date: 2026-02-14
description: Hogyan állítsuk be a DPI-t SVG‑ról PNG‑re konvertáláskor Java használatával.
  Exportáljunk nagy felbontású PNG‑t, tanuljuk meg az SVG‑ról PNG‑re konvertálást,
  és használjunk Java képkonvertáló könyvtárat.
draft: false
keywords:
- how to set dpi
- convert svg to png
- export high resolution png
- how to convert svg
- java image conversion library
language: hu
og_description: Hogyan állítsuk be a DPI-t az SVG → PNG konverzióhoz Java használatával.
  Ez az útmutató megmutatja, hogyan exportáljunk nagy felbontású PNG-t, és használjunk
  Java képkonvertáló könyvtárat.
og_title: Hogyan állítsuk be a DPI-t SVG-ből PNG-be Java-val történő konvertáláskor
tags:
- java
- image-conversion
- svg
- png
title: Hogyan állítsuk be a DPI-t SVG‑ról PNG‑re Java‑val konvertálva
url: /hu/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan állítsuk be a DPI-t SVG‑ról PNG‑re konvertáláskor Java‑val

Gondolkodtál már azon, **hogyan állítsuk be a DPI-t** egy SVG‑ról PNG‑re konvertáláskor, hogy az eredmény éles legyen egy nyomtatásra kész poszteren? Nem vagy egyedül. Sok projektben—gondolj marketing szórólapokra, UI makettekre vagy műszaki diagramokra—egy magas felbontású PNG előállítása SVG‑ből elengedhetetlen.

Ebben az útmutatóban lépésről‑lépésre bemutatjuk, hogyan **konvertáljunk SVG‑t PNG‑re**, **exportáljunk nagy felbontású PNG‑t**, és ami a legfontosabb, hogyan szabályozzuk a DPI‑t az Aspose.HTML for Java könyvtár segítségével. A végére egy újrahasználható kódrészletet kapsz, amelyet bármely Java alkalmazásba beilleszthetsz, legyen az asztali eszköz vagy háttérszolgáltatás.

## Amire szükséged lesz

- **Java 8+** (a kód bármely friss JDK‑val lefordítható)
- **Aspose.HTML for Java** JAR‑ok (elérhetők a Maven Central‑on vagy az Aspose weboldalán)
- Egy SVG fájl, amelyet rasterizálni szeretnél  
- Egy csipetnyi kíváncsiság—másra nincs szükség.

Ha jártas vagy a Maven‑ben, egyszerűen add hozzá a következő szekcióban látható függőséget; egyébként töltsd le a JAR‑okat manuálisan, és add hozzá az osztályúthoz.

## 1. lépés: Add the Java Image Conversion Library

Először is a projektednek szüksége van a **java image conversion library**‑ra, amely ténylegesen tudja olvasni az SVG‑t és írni a PNG‑t. Az Aspose.HTML egy jó választás, mert natívan kezeli a CSS‑t, betűtípusokat és a komplex vektorfunkciókat.

**Maven felhasználók** beilleszthetik ezt a `pom.xml`‑be:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- use the latest stable version -->
</dependency>
```

**Gradle kedvelők** hozzáadhatják:

```gradle
implementation 'com.aspose:aspose-html:23.12'
```

Ha a manuális útvonalat részesíted előnyben, töltsd le a JAR‑t az Aspose letöltési oldaláról, helyezd a `libs/` könyvtárba, majd add hozzá az IDE‑d build útvonalához.

> **Pro tipp:** Figyeld a verziószámot; az újabb kiadások gyakran javítják a DPI‑kezelést és hibákat orvosolnak.

## 2. lépés: Hozd létre a konverziós beállításokat és állítsd be a kívánt DPI‑t

Most, hogy a könyvtár már a projektben van, meg kell mondanunk, *hogyan* szeretnénk, hogy a kimeneti PNG kinézzen. Itt jön a fő kulcsszó—**hogyan állítsuk be a DPI-t**. Az `ImageConversionOptions` osztály lehetővé teszi a finomhangolást a vízszintes (`dpiX`) és függőleges (`dpiY`) felbontásra.

```java
import com.aspose.html.converters.ImageConversionOptions;

// Step 2: Build the options object and set DPI
ImageConversionOptions conversionOptions = new ImageConversionOptions();
conversionOptions.setDpiX(300); // 300 DPI horizontally
conversionOptions.setDpiY(300); // 300 DPI vertically
```

Miért 300 DPI? A legtöbb nyomtatási folyamatban a 300 dots‑per‑inch „nyomtatási minőségnek” számít. Ha csak webes anyagokról van szó, lecsökkentheted 72 vagy 96 DPI‑ra, hogy a fájlméret kisebb legyen.

> **Mi van, ha a szélesség és magasság DPI‑ja különböző?**  
> Egyszerűen állítsd be a `setDpiX`‑et és a `setDpiY`‑t külön-külön. A könyvtár támogatja a nem egyenletes értékeket, ami anamorfin képek esetén hasznos.

## 3. lépés: Végezze el az SVG‑t‑PNG konvertálást

A beállítások készen állnak, a tényleges konverzió egy statikus hívás. A `java.nio.file.Paths`‑t használjuk, hogy a kód platform‑független legyen.

```java
import com.aspose.html.converters.Converter;
import java.nio.file.Paths;

public class SvgToPng {
    public static void main(String[] args) throws Exception {
        // Paths to input SVG and output PNG
        var inputSvg  = Paths.get("YOUR_DIRECTORY/input.svg").toUri();
        var outputPng = Paths.get("YOUR_DIRECTORY/output.png").toUri();

        // Convert using the DPI settings we defined earlier
        Converter.convert(inputSvg, outputPng, conversionOptions);
    }
}
```

Ennyi—futtasd a `main` metódust, és egy éles, 300 DPI‑s PNG‑t találsz a `YOUR_DIRECTORY`‑ben. A könyvtár automatikusan skálázza a vektorgrafikát a megadott DPI‑nek megfelelően, megőrizve az arányt és a szöveg tisztaságát.

## 4. lépés: Ellenőrizd az eredményt (opcionális, de ajánlott)

Egy gyors ellenőrzés későbbi fejfájást megelőzhet. Nyisd meg a generált PNG‑t egy olyan képnézőben, amely megjeleníti a DPI metaadatokat (pl. Photoshop, GIMP vagy akár a Windows Explorer „Részletek” fülén). A **300 DPI**‑t kell látnod a vízszintes és függőleges felbontás alatt.

Ha a fájl homályos, ellenőrizd:

1. Az eredeti SVG nem alacsony felbontású (a vektorfájlok felbontás‑függetlenek, de a bennük beágyazott raszteres képek korlátozhatják a minőséget).  
2. Valóban a DPI beállítása után mentetted el a fájlt—néha az IDE‑k régi buildeket cache‑lnek.  
3. A konverziós beállításokat nem felülírtad máshol a kódban.

## Miért fontos a DPI a nagy felbontású PNG exportálásakor

Talán azt kérdezed: „Miért is kell foglalkozni a DPI‑val? A PNG csak pixelekből áll.” A valóságban a DPI egy *metaadat* címke, amely megmondja a downstream alkalmazásoknak (különösen a nyomtatásra szántaknak), hogy hány pixel felel meg egy hüvelyk fizikai térnek. Ha egy 1200 × 800 PNG‑t nyomtatónak adsz DPI metaadat nélkül, a nyomtató gyakran 72 DPI‑t feltételez, és felnagyítja a képet, ami elmosódott eredményt ad.

A DPI helyes beállítása teljesítményelőny is: elkerülöd a későbbi raster képek felskálázását, ami számításigényes és a minőséget rontja.

## Szélsőséges esetek és gyakori buktatók

| Helyzet | Mire figyelj | Hogyan javíts |
|-----------|-------------------|------------|
| **SVG beágyazott bitmap képeket tartalmaz** | A beágyazott bitmap alacsony felbontású lehet, ami a végső PNG‑t pixelessé teszi még magas DPI‑nél is. | Cseréld ki a bitmapet nagyobb felbontású változatra, vagy szerkeszd az SVG‑t, hogy külső képre hivatkozzon. |
| **Nagy DPI értékek (pl. 1200 DPI)** | Memóriaigény ugrik; `OutOfMemoryError` léphet fel. | Növeld a JVM heap méretét (`-Xmx2g`) vagy korlátozd a DPI‑t egy ésszerű maximumra a felhasználási esethez. |
| **Nem négyzetes pixelek** | Egyes kijelzők másként értelmezik a DPI‑t, így nyúlt képek keletkeznek. | Győződj meg róla, hogy a `setDpiX` egyenlő a `setDpiY`‑vel, hacsak nincs speciális okod a különböző értékekre. |
| **Hiányzó betűtípusok** | Az SVG‑ben lévő szöveg alapértelmezett betűtípusra vált, ami megváltoztatja a layoutot. | Ágyazz be betűtípusokat az SVG‑be, vagy telepítsd a szükséges betűtípusokat a futtatási gépre. |

## Gyors összefoglaló (egy mondatban)

A **hogyan állítsuk be a DPI-t** egy SVG‑ról PNG‑re konvertáláskor úgy oldhatod meg, hogy létrehozol egy `ImageConversionOptions` objektumot, beállítod a `dpiX`/`dpiY` értékeket, majd meghívod a `Converter.convert`‑et az Aspose.HTML Java könyvtárból.

## Következő lépések és kapcsolódó témák

- **Kötegelt feldolgozás:** Iterálj egy SVG‑k könyvtárán, és alkalmazd ugyanazt a DPI beállítást.  
- **Dinamikus DPI:** Olvass be egy konfigurációs fájlt vagy parancssori argumentumot, hogy futásidőben állítsd be a DPI‑t.  
- **Alternatív könyvtárak:** Ha nem tudod használni az Aspose‑t, fontold meg a **Batik**‑et (Apache) vagy a **SVG Salamander**‑t, bár ezeknél extra kódra lehet szükség a DPI kezeléshez.  
- **Export nagy felbontású PNG‑hez Android assetekhez:** Kombináld ezt a technikát az Android `drawable‑hdpi`, `xhdpi` stb. mappáival.

Nyugodtan kísérletezz—próbáld ki a 72 DPI‑t webes bélyegképekhez, a 600 DPI‑t nagyformátumú nyomtatáshoz, vagy a 150 DPI‑t köztes megoldásként. A kód változatlan marad; csak a számok változnak.

---

![hogyan állítsuk be a DPI-t](placeholder-image.png "Illusztráció a DPI beállításáról Java konverziós munkafolyamatban")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}