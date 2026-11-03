---
category: general
date: 2026-03-04
description: Ismerje meg, hogyan állíthatja be a DPI-t HTML PNG-re konvertálása közben.
  Ez az útmutató a HTML PNG-ként történő exportálását, a HTML PNG-ként való mentését,
  valamint az Aspose.HTML for Java használatával történő PNG generálását is lefedi.
draft: false
keywords:
- how to set dpi
- convert html to png
- export html as png
- save html as png
- generate png from html
language: hu
og_description: Hogyan állítsuk be a DPI-t HTML‑ról PNG‑re konvertáláskor, részletesen
  elmagyarázva. Kövesse a lépésről‑lépésre útmutatót a HTML PNG‑ként exportálásához,
  a HTML PNG‑ként mentéséhez és a PNG generálásához HTML‑ből.
og_title: Hogyan állítsuk be a DPI-t HTML PNG-re konvertáláskor
tags:
- Aspose.HTML
- Java
- Image Conversion
title: Hogyan állítsuk be a DPI-t HTML-ből PNG-be konvertáláskor
url: /hu/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-html-to-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan állítsuk be a DPI-t HTML PNG-re konvertálásakor

Valaha is elgondolkodtál **hogyan állítsuk be a DPI-t** egy raszteres képnél, amelyet egy weboldalról generálsz? Lehet, hogy jelentéskészítő eszközt, bélyegkép‑szolgáltatást vagy nyomtatásra kész anyagcsővezeték‑folyamatot építesz—bármelyik forgatókönyv általában egy HTML‑dokumentummal kezdődik, amelynek magas felbontású PNG‑vé kell válnia.  

A jó hír, hogy az Aspose.HTML for Java-val **HTML‑t PNG‑vé konvertálni** gyerekjáték, és a DPI‑t egyetlen kódsorral szabályozhatod. Ebben az útmutatóban végigvezetünk a teljes folyamaton, a HTML‑fájl betöltésétől a 300 DPI‑s PNG‑ként való exportálásig, miközben érintjük a kapcsolódó feladatokat, mint a **HTML exportálása PNG‑ként**, **HTML mentése PNG‑ként**, és **PNG generálása HTML‑ből**.

## Mit fogsz megtanulni

- Hogyan konfiguráljuk a DPI‑t (dots per inch) a kimeneti képhez.
- A DPI, a felbontás és a tömörítési minőség közti különbség.
- Egy teljes, futtatható Java‑példa, amelyet egyszerűen másolhatsz‑beilleszthetsz.
- Gyakori buktatók (pl. hiányzó betűtípusok, nagy oldalak) és azok elkerülése.
- Gyors tippek a kimenet finomhangolásához, ha **HTML‑t PNG‑vé konvertálsz** különböző környezetekben.

### Előfeltételek

- Java 8 vagy újabb telepítve a gépeden.
- Aspose.HTML for Java könyvtár (a legújabb verzió 2026 márciusáig). Maven Central‑ról húzható:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

- Egy egyszerű `input.html` fájl, amelyet PNG‑képpé szeretnél alakítani.

---

## Hogyan állítsuk be a DPI-t HTML PNG konverzióhoz

![Diagram showing DPI setting in code – how to set dpi when converting HTML to PNG](https://example.com/images/dpi-setting.png)

Az **elsődleges lépés**, amely a kép élességét szabályozza, a `Resolution` tulajdonság az `ImageSaveOptions`‑ban. Az alábbiakban a folyamatot kisebb, könnyen emészthető lépésekre bontjuk.

### 1. lépés: Bemeneti és kimeneti útvonalak meghatározása (HTML PNG-re konvertálása)

Először mondd meg a konvertálónak, hol található a forrás HTML, és hová írja a PNG‑t.

```java
// Step 1 – file locations
String htmlFilePath = "YOUR_DIRECTORY/input.html";
String pngFilePath  = "YOUR_DIRECTORY/output.png";
```

> **Miért fontos ez:** A keménykódolt útvonalak rendben vannak egy demóhoz, de éles környezetben valószínűleg konfigurációból vagy parancssori argumentumokból veszed őket. Így a kód rugalmas marad bármely **HTML mentése PNG‑ként** munkafolyamatnál.

### 2. lépés: ImageSaveOptions létrehozása és DPI beállítása (hogyan állítsuk be a DPI-t)

Most példányosítjuk a `ImageSaveOptions`‑t PNG‑hez, és beállítjuk a DPI‑t 300-ra. A DPI határozza meg, hány pixel kerül egy hüvelykre, amikor a képet nyomtatják vagy natív méretben jelenítik meg.

```java
// Step 2 – configure PNG options
ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
saveOptions.setResolution(300);   // <-- This is the DPI you asked for
saveOptions.setQuality(95);       // PNG compression (0‑100); higher = larger file, better fidelity
```

> **Magyarázat:**  
> - `setResolution(300)` azt mondja az Aspose.HTML‑nek, hogy a lapot 300 dots per inch‑en renderelje.  
> - `setQuality(95)` opcionális PNG‑hez; a ZLIB tömörítési szintet szabályozza. Alacsonyabb értékkel kisebb fájlok érhetők el, ha nem kell minden pixel tökéletes legyen.

### 3. lépés: Konverzió végrehajtása (HTML PNG-re exportálása)

Az opciók készen állnak, a tényleges konverzió egyetlen sorban megoldható.

```java
// Step 3 – run the conversion
Converter.convert(htmlFilePath, pngFilePath, saveOptions);
```

> **Mi történik a háttérben?** Az Aspose.HTML beolvassa a HTML‑t, alkalmazza a CSS‑t, elrendezi a DOM‑ot, a kért DPI‑n rasterizálja a megjelenést, majd PNG‑fájlként írja ki. Ha **PNG generálása HTML‑ből** webszolgáltatásban szükséges, a fájlútvonalakat helyettesítheted stream‑ekkel.

### Teljes működő példa

Összegezve, itt egy komplett Java‑osztály, amelyet lefordíthatsz és futtathatsz.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.*;
import com.aspose.html.saving.*;

public class ConvertHtmlToPngWithDpi {
    public static void main(String[] args) throws Exception {

        // Step 1: Define the input HTML file and the output PNG file
        String htmlFilePath = "YOUR_DIRECTORY/input.html";
        String pngFilePath  = "YOUR_DIRECTORY/output.png";

        // Step 2: Create image save options for PNG and configure high‑resolution output
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        saveOptions.setResolution(300);   // Set resolution to 300 DPI (how to set dpi)
        saveOptions.setQuality(95);       // PNG compression quality (0‑100)

        // Step 3: Perform the conversion from HTML to PNG using the configured options
        Converter.convert(htmlFilePath, pngFilePath, saveOptions);

        System.out.println("Conversion complete! PNG saved at " + pngFilePath);
    }
}
```

Futtasd a programot, és egy éles 300 DPI‑s PNG‑t találsz a megadott helyen. Nyisd meg bármely képnézőben, és ellenőrizd a kép tulajdonságait— a DPI‑nek **300**‑nak kell mutatnia.

---

## Gyakori kérdések és szélhelyzetek

### Mi van, ha a DPI beállítás figyelmen kívül marad?

- **Győződj meg róla, hogy a legújabb Aspose.HTML verziót használod.** A régebbi kiadások figyelmen kívül hagyták a `Resolution`‑t PNG‑nél.
- **Ellenőrizd a forrás HTML méretét.** Egy apró HTML‑oldal 300 DPI‑n is kis képméretet eredményezhet. A DPI csak a skálázási tényezőt befolyásolja, nem a lap eredeti méretét.

### Miben különbözik a DPI a képméretektől?

A DPI egy *fizikai* mérőszám (dots per inch). A tényleges pixel‑szélesség/magasság a következőképpen számítható:

```
pixel width  = CSS width  * DPI / 96
pixel height = CSS height * DPI / 96
```

Ha a HTML‑body 800 px széles, 300 DPI‑n a kimeneti PNG körülbelül 2500 px széles lesz (800 × 300 ÷ 96).

### Használhatok más formátumokat (JPEG, BMP), miközben a DPI‑t szabályozom?

Természetesen. Csak cseréld a `SaveFormat.PNG`‑t `SaveFormat.JPEG`‑re (vagy `BMP`‑re), és tartsd meg a `setResolution`‑t. Ne feledd, a JPEG is figyelembe veszi a `Quality` beállítást, amely a tömörítési szintet határozza meg.

### Mi van a szerveren nem telepített betűtípusokkal?

Az Aspose.HTML alapértelmezett betűtípusra vált, ami megváltoztathatja a layoutot. Azonos megjelenés garantálásához ágyazz be szükséges betűtípusokat a `FontSettings` használatával:

```java
FontSettings fontSettings = new FontSettings();
fontSettings.setFontFolder("YOUR_FONT_DIRECTORY", true);
saveOptions.setFontSettings(fontSettings);
```

### Több PNG generálása kötegelt módon

Ha sok fájlhoz kell **PNG generálása HTML‑ből**, csomagold a konverziós logikát egy ciklusba, és használd újra ugyanazt az `ImageSaveOptions` példányt. Ez csökkenti a memóriahasználatot és felgyorsítja a feldolgozást.

```java
for (Path htmlPath : Files.newDirectoryStream(Paths.get("batch_html"))) {
    String outPath = htmlPath.toString().replace(".html", ".png");
    Converter.convert(htmlPath.toString(), outPath, saveOptions);
}
```

---

## Pro tippek a magas minőségű PNG exportáláshoz

1. **Használj vektor‑barát CSS‑t** (pl. `transform: scale(1)`), hogy elkerüld az anti‑aliasing hibákat magas DPI‑n.  
2. **Állíts be háttérszínt**, ha a HTML‑nek átlátszó elemei vannak, és egy egyszínű vászonra van szükséged:

   ```java
   saveOptions.setBackgroundColor(Color.WHITE);
   ```

3. **Kerüld a beágyazott base64‑képeket**, amelyek néhány MB‑nál nagyobbak, mivel ezek a konverzió során a memóriát megterhelik.  
4. **Teszteld különböző képernyő‑DPI‑ken** (pl. 72 DPI‑s monitorok vs. 300 DPI‑s nyomtatók), hogy a vizuális minőség megfeleljen az elvárásoknak.  
5. **Használd a `setPageSize()`‑t**, ha a PNG‑nek egy adott nyomtatási méretnek (A4, Letter stb.) kell megfelelnie, függetlenül a HTML eredeti méretétől.

---

## Összegzés

Áttekintettük, **hogyan állítsuk be a DPI‑t**, amikor **HTML‑t PNG‑vé konvertálunk** az Aspose.HTML for Java‑val, bemutattunk egy teljes, azonnal futtatható példát, és megvizsgáltuk a kapcsolódó feladatokat, mint a **HTML exportálása PNG‑ként**, **HTML mentése PNG‑ként**, és **PNG generálása HTML‑ből**. A `ImageSaveOptions.setResolution` finomhangolásával szabályozhatod a kimenet fizikai élességét, míg a `setQuality` segít a fájlméret és a vizuális hűség egyensúlyában.

### Következő lépések?

Próbáld ki a PNG formátum helyett a JPEG‑et, hogy lásd, hogyan hat a tömörítés a DPI‑re, vagy kísérletezz kötegelt feldolgozással, hogy **HTML‑t PNG‑vé konvertálj** nagy mennyiségben. Érdekelhet a vízjelek vagy egyedi metaadatok hozzáadása is— mindkettő támogatott az Aspose.HTML gazdag API‑jában.

Van egy nehéz eset, ami nem szerepelt? Hagyj kommentet, és együtt megoldjuk. Boldog kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}