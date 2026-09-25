---
category: general
date: 2026-01-14
description: hogyan állítsuk be a DPI-t URL PNG-re konvertálásakor. Tanulja meg, hogyan
  rendereljük a HTML-t PNG-re, állítsuk be a nézetablak méretét, és mentsük a HTML-t
  PNG-ként az Aspose.HTML Java használatával.
draft: false
keywords:
- how to set dpi
- render html to png
- convert url to png
- set viewport size
- save html as png
language: hu
og_description: Hogyan állítsuk be a DPI-t URL PNG-re konvertálásakor. Lépésről lépésre
  útmutató a HTML PNG-re rendereléséhez, a nézetablak méretének szabályozásához és
  a HTML PNG-ként mentéséhez az Aspose.HTML segítségével.
og_title: hogyan állítsuk be a dpi-t – HTML renderelése PNG-be az AsposeHTML segítségével
tags:
- AsposeHTML
- Java
- image rendering
title: hogyan állítsuk be a DPI-t – HTML renderelése PNG‑be az AsposeHTML‑kel
url: /hu/java/conversion-html-to-various-image-formats/how-to-set-dpi-render-html-to-png-with-asposehtml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hogyan állítsuk be a DPI-t – HTML renderelése PNG-be az AsposeHTML segítségével

Valaha is elgondolkodtál már azon, **hogyan állítsuk be a DPI-t** egy weboldalról generált képernyőképszerű képhez? Lehet, hogy 300 DPI-s PNG-re van szükséged nyomtatáshoz, vagy egy alacsony felbontású bélyegképre mobilalkalmazáshoz. Bármelyik esetben a trükk, hogy megmondjuk a renderelő motornak, milyen logikai DPI-t szeretnénk, majd hagyjuk, hogy elvégezze a nehéz munkát.  

Ebben az útmutatóban egy élő URL-t fogunk felhasználni, rendereljük PNG fájlba, **beállítjuk a viewport méretét**, módosítjuk a DPI-t, és végül **HTML-t mentünk PNG‑ként** – mindezt az Aspose.HTML for Java segítségével. Nincs külső böngésző, nincs bonyolult parancssori eszköz – csak tiszta Java kód, amelyet bármely Maven vagy Gradle projektbe beilleszthetsz.

> **Pro tipp:** Ha csak egy gyors bélyegképre van szükséged, a DPI-t hagyhatod 96 DPI‑n (a legtöbb képernyő alapértelmezett értéke). Nyomtatásra kész anyagok esetén emeld 300 DPI‑ra vagy magasabbra.

![hogyan állítsuk be a DPI példája](https://example.com/images/how-to-set-dpi.png "hogyan állítsuk be a DPI példája")

## Amire szükséged lesz

- **Java 17** (vagy bármely friss JDK).  
- **Aspose.HTML for Java** 24.10 vagy újabb. Letöltheted a Maven Central‑ról:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.10</version>
</dependency>
```

- Internetkapcsolat a céloldal lekéréséhez (a példa a `https://example.com/sample.html` URL‑t használja).  
- Írási jogosultság a kimeneti mappához.

Ennyi – nincs Selenium, nincs headless Chrome. Az Aspose.HTML a renderelést a folyamaton belül végzi, ami azt jelenti, hogy a JVM‑en belül maradsz, és elkerülöd a böngésző indításának terheit.

## 1. lépés – HTML dokumentum betöltése URL‑ről

Először létrehozunk egy `HTMLDocument` példányt, amely a rögzíteni kívánt oldalra mutat. A konstruktor automatikusan letölti a HTML‑t, feldolgozza, és előkészíti a DOM‑ot.

```java
import com.aspose.html.HTMLDocument;
import java.nio.file.Paths;

// Load the remote page
HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");
```

*Miért fontos:* A dokumentum közvetlen betöltésével elkerülöd egy külön HTTP kliens használatát. Az Aspose.HTML tiszteletben tartja az átirányításokat, sütiket, és még az alapvető hitelesítést is, ha a URL‑ben adod meg a hitelesítő adatokat.

## 2. lépés – Sandbox létrehozása a kívánt DPI‑val és viewporttal

A **sandbox** az Aspose.HTML módja annak, hogy egy böngésző környezetet utánozzon. Itt azt mondjuk neki, mintha egy 1280 × 720 képernyő lenne, és, ami kulcsfontosságú, beállítjuk a **eszköz DPI‑t**. A DPI módosítása megváltoztatja a renderelt kép pixel sűrűségét anélkül, hogy a logikai méretet befolyásolná.

```java
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;

// Create a sandbox that simulates a 1280×720 screen at 96 DPI
SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
        .setViewportSize(1280, 720)          // width, height in pixels
        .setDeviceDpi(96)                    // logical DPI (change to 300 for print)
        .setUserAgent("AsposeHTML/24.10")    // optional custom user‑agent
        .build();

// Apply the sandbox to the document
htmlDoc.setSandbox(sandbox);
```

*Miért érdemes ezeket az értékeket módosítani:*  
- **Viewport méret** szabályozza, hogy a CSS média lekérdezések (`@media (max-width: …)`) hogyan viselkednek.  
- **Eszköz DPI** befolyásolja a kép fizikai méretét nyomtatáskor. Egy 96 DPI‑s kép jól néz ki a képernyőkön; egy 300 DPI‑s kép megőrzi a tisztaságot papíron.  

Ha négyzet alakú bélyegképre van szükséged, egyszerűen módosítsd a `setViewportSize(500, 500)` értéket, és tartsd alacsonyan a DPI‑t.

## 3. lépés – PNG kiválasztása kimeneti formátumként

Az Aspose.HTML több raszteres formátumot támogat (PNG, JPEG, BMP, GIF). A PNG veszteségmentes, ami tökéletesé teszi képernyőképekhez, ahol minden pixel megőrzése fontos.

```java
import com.aspose.html.rendering.ImageSaveOptions;

// Prepare PNG save options
ImageSaveOptions pngOptions = new ImageSaveOptions();
pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);
```

A tömörítési szintet is módosíthatod (`pngOptions.setCompressionLevel(9)`), ha a fájlméret aggaszt.

## 4. lépés – Kép renderelése és mentése

Most azt mondjuk a dokumentumnak, hogy **mentse** magát képként. A `save` metódus egy fájlútvonalat és a korábban beállított opciókat várja.

```java
// Define the output path (replace with your own directory)
String outputPath = "YOUR_DIRECTORY/sandboxed.png";

// Render the document to a PNG file
htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

System.out.println("Rendering completed.");
```

Amikor a program befejeződik, a `YOUR_DIRECTORY/sandboxed.png` helyen találsz egy PNG fájlt. Nyisd meg – ha a DPI‑t 300‑ra állítottad, a kép metaadatai ezt tükrözik, bár a pixelméretek továbbra is 1280 × 720 maradnak.

## 5. lépés – DPI ellenőrzése (opcionális, de hasznos)

Ha szeretnéd duplán ellenőrizni, hogy a DPI valóban alkalmazva lett, beolvashatod a PNG metaadatait egy könnyű könyvtárral, például a **metadata‑extractor**‑ral:

```java
import com.drew.imaging.ImageMetadataReader;
import com.drew.metadata.png.PngDirectory;

File pngFile = new File(outputPath);
var metadata = ImageMetadataReader.readMetadata(pngFile);
var pngDir = metadata.getFirstDirectoryOfType(PngDirectory.class);
int dpi = pngDir.getInt(PngDirectory.TAG_PIXELS_PER_UNIT_X);
System.out.println("DPI stored in PNG: " + dpi);
```

A konzolon a `300` (vagy amit beállítottál) értéket kell látnod. Ez a lépés nem kötelező a rendereléshez, de gyors ellenőrzés, különösen, ha nyomtatási munkafolyamatokhoz generálsz anyagokat.

## Gyakori kérdések és speciális esetek

### „Mi van, ha az oldal JavaScript‑et használ a tartalom betöltéséhez?”

Az Aspose.HTML egy **korlátozott részhalmazt** hajt végre a JavaScript‑ből. A legtöbb statikus oldalnál azonnal működik. Ha az oldal erősen támaszkodik kliens‑oldali keretrendszerekre (React, Angular, Vue), előfordulhat, hogy előre kell renderelned az oldalt, vagy helyette headless böngészőt kell használnod. A DPI beállítása azonban ugyanúgy működik, amint a DOM készen áll.

### „Renderelhetek PDF‑et PNG helyett?”

Természetesen. Cseréld le a `ImageSaveOptions`‑t `PdfSaveOptions`‑ra, és módosítsd a kimeneti kiterjesztést `.pdf`‑re. A DPI beállítás továbbra is befolyásolja a beágyazott képek raszteres megjelenését.

### „Mi a helyzet a magas felbontású képernyőképekkel a retina kijelzőkhöz?”

Egyszerűen duplázd meg a viewport méreteit, miközben a DPI‑t 96 DPI‑n tartod, vagy tartsd a viewportot, és emeld a DPI‑t 192‑re. Az eredményül kapott PNG kétszer annyi pixelt tartalmaz, így a retina hatást érheted el.

### „ Szükséges erőforrásokat felszabadítani?”

`HTMLDocument` implements `AutoCloseable`. In a production app, wrap it in a try‑with‑resources block:

```java
try (HTMLDocument doc = new HTMLDocument(url)) {
    // configure sandbox, render, etc.
}
```

Ez biztosítja, hogy a natív erőforrások gyorsan felszabaduljanak.

## Teljes működő példa (másolás‑beillesztés kész)

Az alábbiakban a teljes, futtatható program látható. Cseréld le a `YOUR_DIRECTORY`‑t egy valós mappára a gépeden.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.ImageSaveOptions;
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;
import java.nio.file.Paths;

public class RenderHtmlToPng {
    public static void main(String[] args) {
        // 1️⃣ Load the HTML document from a URL
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");

        // 2️⃣ Create a sandbox – set viewport size and DPI
        SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
                .setViewportSize(1280, 720)   // width × height in pixels
                .setDeviceDpi(96)             // change to 300 for print‑ready PNG
                .setUserAgent("AsposeHTML/24.10")
                .build();

        htmlDoc.setSandbox(sandbox); // apply sandbox to the document

        // 3️⃣ Prepare PNG save options
        ImageSaveOptions pngOptions = new ImageSaveOptions();
        pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);

        // 4️⃣ Render and save
        String outputPath = "YOUR_DIRECTORY/sandboxed.png";
        htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

        System.out.println("Rendering completed. Check: " + outputPath);
    }
}
```

Futtasd az osztályt, és kapsz egy PNG‑t, amely tiszteletben tartja a megadott **dpi beállítást**.

## Összegzés

Áttekintettük, **hogyan állítsuk be a DPI‑t**, amikor **HTML‑t renderelünk PNG‑be**, lefedtük a **viewport méret beállítása** lépést, és megmutattuk, hogyan **menthetünk HTML‑t PNG‑ként** az Aspose.HTML for Java segítségével. A fő tanulságok:

- Használj **sandbox‑ot** a DPI és a viewport vezérléséhez.  
- Válaszd a megfelelő **ImageSaveOptions**‑t a veszteségmentes kimenethez.  
- Ellenőrizd a DPI metaadatokat, ha a nyomtatási minőséget garantálni szeretnéd.

Innen tovább kísérletezhetsz különböző DPI értékekkel, nagyobb viewportokkal, vagy akár tömegesen feldolgozhatsz egy URL‑listát. Szeretnél egy egész weboldalt PNG bélyegképekké konvertálni? Csak iterálj egy URL‑tömbön, és használd újra ugyanazt a sandbox konfigurációt.

Boldog renderelést, és legyenek a képernyőképeid mindig pixel‑tökéletesek!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}