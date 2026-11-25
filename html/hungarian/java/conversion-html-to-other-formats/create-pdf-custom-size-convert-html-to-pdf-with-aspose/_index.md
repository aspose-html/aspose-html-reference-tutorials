---
category: general
date: 2026-03-26
description: Készíts egyedi méretű PDF-et HTML-ből az Aspose.HTML for Java segítségével.
  Tanulja meg, hogyan konvertálhat HTML-t PDF-be, és állíthatja be a PDF oldalméretét
  néhány lépésben.
draft: false
keywords:
- create pdf custom size
- convert html to pdf
- change pdf page size
- generate pdf from html
- set pdf page size
language: hu
og_description: PDF egyedi méret létrehozása HTML-ből az Aspose-szal. Ez az útmutató
  megmutatja, hogyan konvertálhat HTML-t PDF-be, hogyan változtathatja meg a PDF oldal
  méretét, és hogyan állíthatja be könnyedén a PDF oldal méretét.
og_title: PDF egyedi méret létrehozása – Gyors útmutató a HTML PDF-re konvertálásához
tags:
- aspose
- java
- pdf
- html
title: PDF egyedi méret létrehozása – HTML PDF-re konvertálása az Aspose-szal
url: /hu/java/conversion-html-to-other-formats/create-pdf-custom-size-convert-html-to-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF egyedi méret létrehozása – HTML PDF‑re konvertálása Aspose‑szal

Szükséged volt már **PDF egyedi méret** létrehozására egy HTML‑fájlból? Ebben az útmutatóban megmutatjuk, hogyan **konvertálhatod a HTML‑t PDF‑re**, és állíthatod be a PDF oldalméretét az Aspose.HTML for Java segítségével.  

Ha számlákat, jelentéseket vagy e‑könyveket készítesz, a pontos oldalméretek kulcsfontosságúak – különben a layout eltolódik vagy levágódik.  

Lépésről lépésre végigvezetünk a forrás‑HTML betöltésétől a margók finomhangolásáig, és egy használatra kész PDF‑et adunk át. Nincs homályos hivatkozás, csak egy teljes, futtatható példa, amit ma másolhatsz‑beilleszthetsz.

## Amire szükséged lesz

- **Java 17** (vagy bármely friss JDK).  
- **Aspose.HTML for Java** JAR‑ok – a legújabb verziót a Maven tárolóból vagy az Aspose weboldaláról töltheted le.  
- Egy egyszerű `input.html` fájl, amelyet egy általad irányított mappában helyezel el.  
- Egy IDE vagy szövegszerkesztő – általában IntelliJ IDEA‑t használok, de az Eclipse is tökéletesen működik.

Ezek a feltételek biztosítják, hogy ne kapj “class not found” hibát a folyamat közepén.  

Most merüljünk el a részletekben.

![Create PDF custom size example](/images/create-pdf-custom-size.png "Screenshot showing a PDF generated with custom page size and margins – create pdf custom size")

## PDF egyedi méret létrehozása – Alaplépések

Az alábbiakban a teljes Java programot láthatod, amelyet a végén kapsz. Nyugodtan másold be egy `ConvertHtmlToPdfCustomPage.java` nevű fájlba, és futtasd, miután hozzáadtad az Aspose függőségeket a projektedhez.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.PdfConversionOptions;
import com.aspose.html.saving.PageSize;
import com.aspose.html.saving.Margin;

public class ConvertHtmlToPdfCustomPage {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the source HTML document
        HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/input.html");

        // Step 2: Set up PDF conversion options
        PdfConversionOptions pdfOptions = new PdfConversionOptions();
        pdfOptions.setPageSize(PageSize.A4); // Choose page size (A4, Letter, etc.)
        pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Portrait); // Portrait or Landscape
        pdfOptions.setMargins(new Margin(20, 20, 20, 20)); // Margins: left, top, right, bottom (points)

        // Step 3: Convert the HTML document to a PDF file with the custom settings
        Converter.convertHTML(htmlDoc, "YOUR_DIRECTORY/custom_page.pdf", pdfOptions);

        // Step 4: Inform the user that the PDF has been created
        System.out.println("PDF generated with custom page size and margins.");
    }
}
```

### 1. lépés – HTML konvertálása PDF‑re: Dokumentum betöltése

Az első dolog, amit teszünk, **betölti a HTML‑t**, amelyet PDF‑vé akarunk alakítani.  
`HTMLDocument` beolvassa a fájlt, feloldja a relatív hivatkozásokat, és felépít egy DOM‑ot, amelyet az Aspose renderelni tud.  

> **Miért fontos:** Ha a HTML CSS‑t vagy képeket hivatkozik, az Aspose a fájl útvonala alapján tölti le őket. Egy abszolút útvonal (`YOUR_DIRECTORY/input.html`) használata elkerüli a “file not found” meglepetéseket.

### 2. lépés – PDF oldalméret módosítása: Opciók beállítása

Itt hozunk létre egy `PdfConversionOptions` objektumot.  
- `setPageSize(PageSize.A4)` azt mondja az Aspose‑nak, hogy a szabványos A4 méretet (210 × 297 mm) használja.  
- `setPageOrientation(...)` elforgatja az oldalt, ha tájolásra van szükség.  
- `setMargins(new Margin(20, 20, 20, 20))` minden oldalra 20 pont margót ad.

A `PageSize.A4` helyett használhatod a `PageSize.LETTER`‑t vagy akár **egyedi méretet** is, ha egy `SizeF` objektumot adsz meg, például:

```java
pdfOptions.setPageSize(new SizeF(500, 800)); // width, height in points
```

> **Pro tipp:** Egy pont 1/72 hüvelyknek felel meg. Ha milliméterben gondolkodsz, szorozd meg 2,83465‑tel a pontértékhez.

### 3. lépés – PDF generálása HTML‑ből: Konverzió futtatása

A `Converter.convertHTML` végzi a nehéz munkát. Átveszi a betöltött `HTMLDocument`‑et, a kimeneti útvonalat és a most beállított opciókat.  

Ha **dinamikusan** szeretnéd beállítani a PDF oldalméretet a tartalom alapján, a lépés előtt kiszámíthatod a szükséges méreteket, és ennek megfelelően módosíthatod a `pdfOptions`‑t.

### 4. lépés – Az eredmény ellenőrzése

A `System.out.println` sor opcionális, de gyors visszajelzést ad, ha a programot konzolból futtatod. A futtatás után nyisd meg a `custom_page.pdf`‑t – egy A4 álló PDF‑et kell látnod, egyenletes 20 pont margóval, pontosan úgy, ahogy megadtuk.

## HTML konvertálása PDF‑re – Gyakori variációk

### Fájlútvonal helyett stream használata

Előfordulhat, hogy nincs fizikai fájl; a HTML egy adatbázisból vagy API‑ból érkezik. Ebben az esetben a stringet egy `ByteArrayInputStream`‑be csomagolhatod:

```java
String htmlContent = "<html><body><h1>Hello, PDF!</h1></body></html>";
HTMLDocument htmlDoc = new HTMLDocument(
        new ByteArrayInputStream(htmlContent.getBytes(StandardCharsets.UTF_8)),
        "http://example.com/");
```

A második argumentum a relatív erőforrások feloldásához használt alap‑URL.

### Oldalorientáció módosítása

Ha a jelentésed széles, válts tájolásra:

```java
pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Landscape);
```

### Margók finomhangolása

A margók lebegőpontos értékeket is elfogadnak, így beállíthatsz 0,5 pt‑t egy szál‑vékony kerethez:

```java
pdfOptions.setMargins(new Margin(5.5, 10.2, 5.5, 10.2));
```

### Nagy HTML‑fájlok kezelése

Masszív dokumentumok esetén fontold meg a **memóriahatékony streaming** engedélyezését:

```java
pdfOptions.setUseMemoryCache(true);
```

Ez azt mondja az Aspose‑nak, hogy a köztes adatokat ideiglenes fájlokba írja, a RAM helyett.

## PDF oldalméret beállítása – Szélsőséges esetek és buktatók

- **Hiányzó betűkészletek:** Ha a HTML egy, a szerveren nem telepített egyedi betűtípust használ, a PDF egy alapértelmezett betűtípusra fog visszaesni. A betűtípust beágyazhatod a `pdfOptions.getFontEmbeddingMode().setEmbeddingMode(EmbeddingMode.Always);` segítségével.  
- **Képméret csökkentése:** A nagy felbontású képek felrobbanthatják a PDF‑et. Használd a `pdfOptions.setImageResolution(150);`‑t a felbontás csökkentéséhez, miközben megőrzöd a minőséget.  
- **CSS kompatibilitás:** Nem minden CSS‑tulajdonság támogatott teljes mértékben. Maradj a szabványos elrendezési technikáknál (a flexbox működik, de a grid‑nek lehetnek sajátosságai).  
- **Útvonal jogosultságok:** Győződj meg róla, hogy a folyamatnak írási joga van a `YOUR_DIRECTORY`‑hez. Ellenkező esetben `IOException` keletkezik.

## Várt kimenet

A program futtatása után a PDF a következőhöz hasonlóan néz ki (konceptuális ábra):

```
+---------------------------------------------------+
|                     Header                        |
|                                                   |
|   (HTML rendered content goes here)               |
|                                                   |
|                     Footer                        |
+---------------------------------------------------+
```

- Oldalméret: **A4** (210 × 297 mm).  
- Orientáció: **Álló**.  
- Margók: **20 pt** minden oldalon.  

Nyisd meg a fájlt bármely PDF‑olvasóval (Adobe Reader, Chrome, stb.) a megerősítéshez.

## Összegzés

Most már tudod, hogyan **hozhatsz létre PDF egyedi méretet** egy HTML forrásból az Aspose.HTML for Java segítségével. Az útmutató lefedte a teljes folyamatot: **HTML konvertálása PDF‑re**, **PDF oldalméret módosítása**, **PDF oldalméret beállítása**, és **PDF generálása HTML‑ből** egyedi margókkal.  

Nyugodtan kísérletezz – cseréld le a `PageSize.LETTER`‑t jogi méretre, finomítsd a margókat, vagy ágyazz be saját betűtípusokat. Következő lépésként felfedezheted a **vízjelek hozzáadását**, **PDF titkosítását**, vagy **tömeges HTML‑fájlok feldolgozását**. Mindezek a témák ugyanazokra az alapelvekre épülnek, amelyeket most megtanultál.

Van kérdésed egy konkrét szélsőséges esettel kapcsolatban? Írj egy megjegyzést alul, és segítek a hibaelhárításban. Boldog kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}