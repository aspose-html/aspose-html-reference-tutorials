---
category: general
date: 2026-03-25
description: Hogyan használjuk a sandboxot weboldal képernyőképeinek rögzítésére az
  Aspose.HTML for Java segítségével. Tanulja meg, hogyan menthet HTML-t PNG‑ként,
  HTML‑ről képre konvertálást és HTML‑ről PNG‑re konvertálást percek alatt.
draft: false
keywords:
- how to use sandbox
- capture webpage screenshot
- save html as png
- html to image conversion
- html to png conversion
language: hu
og_description: Hogyan használjuk a sandboxot weboldal képernyőképeinek rögzítésére.
  Ez az útmutató bemutatja, hogyan menthetjük el a HTML-t PNG formátumban, lefedve
  a HTML képpé konvertálását és a HTML PNG-re konvertálását az Aspose.HTML for Java
  segítségével.
og_title: Hogyan használjuk a Sandboxot a weboldal képernyőképeinek rögzítéséhez
tags:
- Aspose.HTML
- Java
- Web Automation
title: Hogyan használjuk a Sandboxot a weboldal képernyőképeinek rögzítéséhez
url: /hu/java/conversion-html-to-various-image-formats/how-to-use-sandbox-to-capture-webpage-screenshot/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjuk a Sandboxot weboldal képernyőképként való rögzítéshez

A sandbox használata weboldal képernyőképként való rögzítésére gyakori követelmény, amikor pixel‑pontos előnézetre van szükség egy reszponzív oldalról. Ebben az útmutatóban megmutatjuk, hogyan **menthetünk HTML-t PNG‑ként** az Aspose.HTML for Java segítségével, lefedve mindent a *html to image conversion*-től a *html to png conversion*-ig egyetlen, reprodukálható példában.

Képzeld el, hogy egy marketing céloldalt tesztelsz, amely telefonon, tableten és asztali gépen másként jelenik meg. A három böngésző megnyitása helyett elindíthatsz egy sandboxot, rámutathatsz a URL‑re, és azonnal kapsz egy PNG‑t, amely pontosan azt tükrözi, amit egy valódi eszköz renderelne. A tutorial végére egy teljes, futtatható Java programod lesz, amely ezt megteszi, valamint néhány gyakorlati tippet, amelyet újra felhasználhatsz a saját projektjeidben.

## Amire szükséged lesz

- **Aspose.HTML for Java** (v23.9 vagy újabb). A könyvtár elérhető a Maven Central‑on, így a függőség hozzáadása gyerekjáték.
- A gépeden telepített **JDK 11+**.
- Egy tetszőleges IDE vagy szövegszerkesztő (IntelliJ IDEA, VS Code, Eclipse… bármelyik megfelel).
- Internetkapcsolat a példában szereplő URL‑hez (`https://example.com/responsive.html`), vagy cseréld le bármelyik oldalra, amelyet le szeretnél fényképezni.

Nem szükséges további natív bináris vagy headless böngésző – a sandbox teljesen memóriában fut.

---

## Hogyan használjuk a Sandboxot – 1. lépés: A virtuális eszköz definiálása

Az első dolog, amit megteszel, hogy megmondod a sandboxnak, milyen képernyőméretet szeretnél emulálni. Itt jön képbe a fő kulcsszó: *how to use sandbox* egy adott nézetablakhoz.

```java
// Step 1: Create a DeviceInfo that describes the virtual screen
DeviceInfo sandboxDevice = new DeviceInfo();
sandboxDevice.setWidth(800);               // width in pixels
sandboxDevice.setHeight(600);              // height in pixels
sandboxDevice.setDevicePixelRatio(1.0);    // 1 × for standard displays
sandboxDevice.setUserAgent("AsposeHTML/Java Sandbox");
```

**Miért fontos ez:**  
A szélesség és magasság beállítása arra kényszeríti a layout motorját, hogy a lapot úgy kezelje, mintha egy 800×600-as monitoron jelenne meg. A `devicePixelRatio` befolyásolja, hogyan viselkednek a CSS‑alapú média lekérdezések (`@media (min‑device‑pixel‑ratio: ...)`), biztosítva, hogy a képernyőkép megfeleljen a valós élménynek.

> **Pro tipp:** Ha magas DPI‑ű képernyőképre van szükséged (gondolj a Retina kijelzőkre), állítsd a `devicePixelRatio`‑t `2.0`‑ra, és ennek megfelelően növeld a szélességet/magasságot.

---

## Weboldal képernyőkép rögzítése – 2. lépés: Az oldal betöltése a Sandboxban

Most azt kérjük az Aspose.HTML‑t, hogy töltse le a távoli HTML‑t, és renderelje a most definiált sandboxban. Ez a lépés a **capture webpage screenshot** szívét képezi.

```java
// Step 2: Load the remote HTML page using the sandboxed environment
HTMLDocument document = new HTMLDocument(
        "https://example.com/responsive.html",
        new HTMLDocumentLoadOptions(new Sandbox(sandboxDevice)));
```

**Mi történik a háttérben?**  
A `HTMLDocumentLoadOptions` megkap egy `Sandbox` példányt, amely tartalmazza a `DeviceInfo`‑t. A könyvtár ezután egy headless renderelési kontextust hoz létre, amely figyelembe veszi a nézetablakot, a user‑agent stringet, és bármilyen JavaScriptet, amelyet az oldal végrehajthat – *mind anélkül, hogy Chrome‑t vagy Firefox‑t indítana*.

Ha a céloldal hitelesítést igényel, a `HTMLDocumentLoadOptions`‑on keresztül be lehet injektálni sütiket vagy egyéni fejléceket is. Ez egy hasznos speciális eset, amikor intranet portálokkal dolgozol.

---

## HTML mentése PNG‑ként – 3. lépés: A renderelt dokumentum konvertálása képpé

Miután az oldal renderelve van, az utolsó lépés a **HTML mentése PNG‑ként**. Ez a tényleges *html to png conversion* lépés.

```java
// Step 3: Convert the rendered document to PNG and write it to disk
try (FileOutputStream out = new FileOutputStream("output/responsive_page.png")) {
    Converter.convertDocument(
            document,
            new ConversionOptions(ConversionFormat.PNG),
            out);
}
```

Amikor a `Converter` befejeződik, a `output` mappában egy `responsive_page.png` nevű fájlt találsz. Nyisd meg, és pontosan azt fogod látni, ahogy az oldal 800×600 pixelben nézett ki – nincs böngésző felület, nincs görgetősáv, csak a tiszta render.

**Gyakori buktatók:**  
- **Fájl jogosultsági hibák:** Győződj meg arról, hogy a könyvtár létezik (`output/` a példában), és a folyamatod tud beleírni.  
- **Nagy oldalak:** Nagyon magas oldalak hatalmas PNG fájlokat eredményezhetnek; korlátozhatod a magasságot a `DeviceInfo`‑ban, vagy vágás után levághatod.  
- **Dinamikus tartalom:** Ha az oldal AJAX‑on keresztül tölt be adatokat a kezdeti betöltés után, be kell vezetned egy rövid késleltetést (`Thread.sleep(2000)`) a konvertálás előtt, vagy használhatod a `HTMLDocumentLoadOptions.setWaitForResources(true)`‑t.

### html to image conversion – Haladó beállítások

Az Aspose.HTML több beállítási lehetőséget kínál, amelyekkel finomhangolhatod a **html to image conversion**-t:

| Opció | Leírás | Mikor használjuk |
|--------|-------------|-------------|
| `ConversionOptions.setQuality(int)` | Beállítja a PNG tömörítési szintet (0‑100). | Csökkenti a fájlméretet webes eszközök számára. |
| `ConversionOptions.setBackgroundColor(Color)` | Kényszeríti a háttérszín beállítását (alapértelmezett az átlátszó). | Hasznos, ha az oldal átlátszó részeket tartalmaz. |
| `ConversionOptions.setPageSize(PageSize)` | Felülírja a sandbox méretét a kimeneti képhez. | Különböző felbontású bélyegképek létrehozása. |

Az alábbi gyors kódrészlet fehér háttér és 90 % minőség beállítását mutatja:

```java
ConversionOptions pngOptions = new ConversionOptions(ConversionFormat.PNG);
pngOptions.setBackgroundColor(java.awt.Color.WHITE);
pngOptions.setQuality(90);

try (FileOutputStream out = new FileOutputStream("output/white_bg_page.png")) {
    Converter.convertDocument(document, pngOptions, out);
}
```

---

## Teljes működő példa

Mindent összevonva, itt a teljes program, amelyet beilleszthetsz egy `SandboxResponsiveExample.java` fájlba és futtathatsz:

```java
import com.aspose.html.devices.DeviceInfo;
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.ConversionOptions;
import com.aspose.html.converters.ConversionFormat;
import com.aspose.html.render.HTMLDocument;
import com.aspose.html.render.HTMLDocumentLoadOptions;
import com.aspose.html.render.Sandbox;

import java.io.FileOutputStream;

public class SandboxResponsiveExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Define a sandbox with the desired viewport (800×600) and device pixel ratio
        DeviceInfo sandboxDevice = new DeviceInfo();
        sandboxDevice.setWidth(800);
        sandboxDevice.setHeight(600);
        sandboxDevice.setDevicePixelRatio(1.0);
        sandboxDevice.setUserAgent("AsposeHTML/Java Sandbox");

        // Step 2: Load the remote HTML page inside the sandboxed environment
        HTMLDocument document = new HTMLDocument(
                "https://example.com/responsive.html",
                new HTMLDocumentLoadOptions(new Sandbox(sandboxDevice)));

        // Step 3: Convert the document to PNG – the output reflects exactly how the page looks on the defined screen size
        try (FileOutputStream out = new FileOutputStream("output/responsive_page.png")) {
            Converter.convertDocument(
                    document,
                    new ConversionOptions(ConversionFormat.PNG),
                    out);
        }

        System.out.println("Screenshot saved to output/responsive_page.png");
    }
}
```

A program futtatása kiír egy megerősítő sort, és a PNG‑t a `output` mappába helyezi. Nyisd meg a fájlt, és pontosan azt a távoli oldalt látod, amelyet a megadott méretben kértél.

---

## Gyakran ismételt kérdések

**K: Működik ez helyi HTML fájlokkal?**  
**A:** Természetesen. Cseréld le az URL‑t egy `file://` URI‑ra, vagy adj meg egy `java.io.File` útvonalat a `HTMLDocument` konstruktorának.

**K: Mi van, ha PDF‑re van szükségem PNG helyett?**  
**A:** Cseréld ki a `ConversionFormat.PNG`-t `ConversionFormat.PDF`-re. A kód többi része változatlan marad.

**K: Készíthetek teljes oldal (görgethető) képernyőképet?**  
**A:** Állítsd be a `DeviceInfo` magasságát az oldal görgetési magasságára (`document.getDocumentElement().getScrollHeight()`) a konvertálás előtt, vagy használd a `ConversionOptions.setPageSize`‑t a vászon nagyításához.

---

## Következtetés

Most már tudod, **hogyan használjuk a sandboxot** weboldal képernyőkép rögzítésére, HTML mentésére PNG‑ként, és megbízható html to image conversion végrehajtására az Aspose.HTML for Java-val. A megközelítés könnyű, teljesen programozható, és megkerüli a hagyományos headless böngészők terheit.

Mi a következő? Próbáld meg a PNG kimenetet PDF‑re cserélni, kísérletezz különböző device pixel ratio‑kkal a Retina kijelzők utánzásához, vagy automatizáld több tucat URL kötegelt feldolgozását. Ugyanaz a sandbox technika felhasználható **html to png conversion**-hez CI pipeline‑okban, vizuális regressziós tesztelésben, vagy bélyegképek generálásához egy tartalomkezelő rendszerben.

Nyugodtan hagyj megjegyzést, ha elakadsz, és jó kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}