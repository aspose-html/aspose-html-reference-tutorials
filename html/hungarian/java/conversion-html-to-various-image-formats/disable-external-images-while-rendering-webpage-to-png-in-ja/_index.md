---
category: general
date: 2026-05-31
description: Tiltsa le a külső képeket, amikor Java-ban az Aspose HTML segítségével
  weboldalt PNG formátumba renderel. Tanulja meg, hogyan töltsön be weboldalt biztonságosan
  sandbox környezetben, és mentse el a HTML dokumentumot PNG‑ként.
draft: false
keywords:
- disable external images
- render webpage to png
- load webpage in sandbox
- how to render html to image java
- save html document as png
language: hu
og_description: Külső képek letiltása weboldal PNG-re renderelésekor Java-ban. Ez
  a lépésről‑lépésre útmutató bemutatja, hogyan töltsünk be egy weboldalt sandbox
  környezetben, és hogyan mentsük el a HTML-dokumentumot PNG formátumban.
og_title: Külső képek letiltása a weboldal PNG-be renderelése közben Java-ban
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Disable external images when you render webpage to PNG in Java using
    Aspose HTML. Learn to load webpage in sandbox safely and save HTML document as
    PNG.
  headline: Disable External Images While Rendering Webpage to PNG in Java
  type: TechArticle
- questions:
  - answer: Yes. Inline `data:` URIs or base64‑encoded images are treated as part
      of the document and will appear in the PNG.
    question: Can I still display images that are bundled inside the HTML?
  - answer: The sandbox works as an all‑or‑nothing switch. For fine‑grained control,
      download the allowed images yourself, embed them as data URIs, and then render.
    question: What if I need to keep some external images but block others?
  - answer: Absolutely. Aspose.HTML is a pure‑Java library; it does not require a
      display server or browser engine.
    question: Does this approach work on headless servers?
  - answer: 'Selenium drives a real browser, which is heavyweight and harder to sandbox.
      Aspose.HTML renders HTML directly in memory, giving you deterministic performance
      and easier security controls like **disable external images**. --- ## Conclusion
      You now have a solid, end‑to‑end recipe for **disabling exter'
    question: How does this differ from using Selenium or Puppeteer?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- Image Rendering
title: Külső képek letiltása a weboldal PNG-re renderelése közben Java-ban
url: /hu/java/conversion-html-to-various-image-formats/disable-external-images-while-rendering-webpage-to-png-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Külső képek letiltása weboldal PNG-re renderelésekor Java-ban

Volt már szükséged arra, hogy **letiltsd a külső képeket**, amikor egy weboldalt PNG-re renderelsz Java-ban? Lehet, hogy egy bélyegkép‑szolgáltatást építesz, amelynek el kell zárnia a nyilvános internetet, vagy egyszerűen csak biztosítani szeretnéd, hogy a konverzió során ne szivárogjanak ki harmadik fél képei. Bármelyik esetben a megfelelő helyen vagy.

Ebben az oktatóanyagban végigvezetünk a weboldal sandboxban történő betöltésén, a külső képek letöltésének letiltásán, és végül a HTML dokumentum PNG‑ként mentésén – mindezt az Aspose.HTML for Java segítségével. A végére egy kész, futtatható példát kapsz, valamint néhány gyakorlati tippet a tipikus buktatók elkerüléséhez.

## Mit fogsz megtanulni

- **Hogyan renderelj HTML-t képre Java-ban** az Aspose.HTML `Converter`‑jével.
- A pontos lépések a **weboldal sandboxban történő betöltéséhez** egy egyedi viewporttal és DPI‑val.
- A szükséges konfiguráció a **külső képek letiltásához**, miközben a lapot továbbra is rendereljük.
- **Hogyan mentsd el a HTML dokumentumot PNG‑ként** (vagy bármely más támogatott formátumban) a lemezre.
- Szélsőséges esetek kezelése, teljesítmény tippek és hibaelhárítási tanácsok.

### Előfeltételek

- Java 8 vagy újabb telepítve (a kód JDK 11+ verzióval is működik).
- Maven vagy Gradle a Aspose.HTML for Java könyvtár letöltéséhez.
- Alapvető ismeretek a Java szintaxisról és a kivételkezelésről.
- Internetkapcsolat a kezdeti oldalbetöltéshez (kivéve, ha helyileg szolgálod ki a HTML‑t).

> **Pro tipp:** Ha vállalati proxy mögött dolgozol, állítsd be a JVM `http.proxyHost` és `http.proxyPort` tulajdonságait a példa futtatása előtt.

---

## 1. lépés: Projekt beállítása és Aspose.HTML hozzáadása

Először is adjuk hozzá az Aspose.HTML függőséget. Ha Maven‑t használsz, helyezd ezt a `pom.xml`‑be:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Gradle esetén az ekvivalens:

```gradle
implementation 'com.aspose:aspose-html:23.9'
```

Miután a könyvtár a classpath‑on van, készen állsz a kódolásra.

---

## 2. lépés: **Külső képek letiltása** sandbox környezettel

A megoldás szíve a `DocumentSandbox`. Ha a *allowExternalImages* zászlónak `false`‑t adunk, az Aspose.HTML figyelmen kívül hagy minden `<img>` elemet, amely a sandboxon kívülre mutató URL‑re hivatkozik. Ez a pontos mechanizmus, amely **letiltja a külső képeket**.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox that blocks external scripts and images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport size (width x height)
                96,                     // DPI – 96 is the screen default
                "MyApp/1.0",            // custom user‑agent string
                false,                  // allowExternalScripts = false
                false);                 // allowExternalImages = false  <-- disables external images
```

> **Miért fontos:** Sandbox nélkül a renderelő megpróbálja letölteni az oldal által hivatkozott minden képet, ami lassú, megbízhatatlan vagy akár biztonsági kockázat is lehet. A zászló `false`‑ra állítása garantálja a tiszta, önálló renderelést.

---

## 3. lépés: **Weboldal betöltése sandboxban**  

Most az Aspose.HTML‑t a rögzíteni kívánt URL‑re irányítjuk. A `HTMLDocument` konstruktor elfogadja a sandbox példányt, automatikusan alkalmazva a most definiált korlátozásokat.

```java
        // 2️⃣ Load the target page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // replace with your target URL
                sandbox);
```

Ha az oldal erősen külső szkriptekre támaszkodik a layouthoz, hiányzó tartalmat észlelhetsz, mivel a szkripteket is letiltottuk. Ebben az esetben állítsd a `allowExternalScripts` zászlót `true`‑ra, miközben a `allowExternalImages` értéke marad `false`.

---

## 4. lépés: **Weboldal renderelése PNG‑re**  

A dokumentum betöltése után a képpé konvertálás egyetlen soros hívás a `Converter.convert`‑el. Az `ImageSaveOptions` objektum lehetővé teszi a kimeneti formátum kiválasztását; itt a PNG‑t választjuk.

```java
        // 3️⃣ Render the document to a PNG image.
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png"; // ensure the folder exists

        Converter.convert(htmlDoc, saveOptions, outputPath);
        System.out.println("Image saved to: " + outputPath);
    }
}
```

Az eredményül kapott `sandboxed.png` egy pillanatképet tartalmaz az oldalról **külső képek nélkül** – csak a beágyazott SVG‑k vagy base64‑kódolt grafikák maradnak, ha vannak.

---

## 5. lépés: Kimenet ellenőrzése és gyakori problémák hibakeresése

A program futtatása után nyisd meg a `sandboxed.png`‑t bármely képnézőben. Látnod kell az oldal elrendezését, szövegét és CSS‑stílusát, de minden `<img src="http://…">` elem üres lesz (gyakran fehér téglalapként jelenik meg vagy teljesen kihagyásra kerül).

### Tipikus hibák és megoldások

| Tünet | Valószínű ok | Megoldás |
|---|---|---|
| Üres oldal | A cél URL blokkolta a kérést (pl. Cloudflare) | Adj hozzá megfelelő fejléceket a sandbox felhasználói ügynökéhez, vagy használj proxyt. |
| Hiányzó betűtípusok | A betűtípus fájlok külsőleg vannak tárolva | Telepítsd a betűtípusokat helyileg, vagy ágyazd be őket `@font-face`‑ként data URI‑kkal. |
| Elrendezés eltolódás | A CSS külső stíluslapokra hivatkozik, amelyek blokkolva lettek | Állítsd a `allowExternalScripts`‑t `true`‑ra *csak* a CSS betöltéséhez, majd futtasd újra. |
| `java.lang.OutOfMemoryError` | Nagyon nagy oldal renderelése magas DPI‑n | Csökkentsd a viewport méretét vagy a DPI‑t, vagy növeld a JVM heap méretét (`-Xmx2g`). |

---

## 6. lépés: A példa kiterjesztése – mentés más formátumokba

Ugyanez a kód működik JPEG‑re, BMP‑re vagy akár PDF‑re is. Csak a `SaveFormat` enum‑ot módosítsd:

```java
// Example: Save as JPEG with quality 80%
ImageSaveOptions jpegOptions = new ImageSaveOptions(SaveFormat.JPEG);
jpegOptions.setQuality(80);
Converter.convert(htmlDoc, jpegOptions, "output/sandboxed.jpg");
```

PDF esetén cseréld le az `ImageSaveOptions`‑t `PdfSaveOptions`‑ra, és állítsd be a megfelelő fájlkiterjesztést.

---

## Teljesen működő példa (másolás‑beillesztés kész)

Az alábbi **komplett, futtatható program**. Hozz létre egy új Java osztályt, illeszd be a kódot, győződj meg róla, hogy az `output` könyvtár létezik, majd futtasd.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1 – Create a sandbox that disables external images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport width & height
                96,                     // DPI
                "MyApp/1.0",            // custom user‑agent
                false,                  // external scripts disabled
                false);                 // external images disabled (primary goal)

        // Step 2 – Load the page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // change to your URL
                sandbox);

        // Step 3 – Render to PNG.
        ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png";

        Converter.convert(htmlDoc, pngOptions, outputPath);
        System.out.println("PNG image saved to: " + outputPath);
    }
}
```

**Várt kimenet** (konzol):

```
PNG image saved to: output/sandboxed.png
```

Nyisd meg a `sandboxed.png`‑t – láthatod az oldalt **külső képek nélkül** renderelve.

---

## Gyakran Ismételt Kérdések

**K: Megjeleníthetek még mindig olyan képeket, amelyek a HTML‑ben vannak beágyazva?**  
V: Igen. Az inline `data:` URI‑k vagy base64‑kódolt képek a dokumentum részeként kezelődnek, és megjelennek a PNG‑ben.

**K: Mi van, ha néhány külső képet meg kell tartanom, de másokat blokkolni akarok?**  
V: A sandbox egy minden‑vagy‑semmi kapcsolóként működik. Finomabb vezérléshez töltsd le a megengedett képeket saját magad, ágyazd be őket data URI‑kként, majd rendereld.

**K: Működik ez a megközelítés fej nélküli szervereken?**  
V: Teljesen. Az Aspose.HTML egy tisztán Java‑alapú könyvtár; nem igényel kijelzőszervert vagy böngészőmotort.

**K: Miben különbözik ez a Selenium vagy a Puppeteer használatától?**  
V: A Selenium egy valódi böngészőt vezérel, ami nehézkes és nehezen sandboxolható. Az Aspose.HTML közvetlenül memóriában renderel HTML‑t, ami determinisztikus teljesítményt és egyszerűbb biztonsági vezérlést (például **külső képek letiltása**) biztosít.

---

## Összegzés

Most már van egy szilárd, vég‑től‑végig útmutatód a **külső képek letiltásához weboldal PNG‑re renderelésekor Java‑ban**. A `DocumentSandbox` használatával szoros kontrollt nyerhetsz a külső erőforrások felett, biztosítva a biztonságot és a reprodukálhatóságot. Innen már kísérletezhetsz különböző viewport méretekkel, DPI beállításokkal vagy kimeneti formátumokkal – minden módosítás új lehetőséget nyit bélyegképek, előnézetek vagy archiválási pillanatképek generálásához.

Készen állsz a következő kihívásra? Próbáld meg párhuzamosan több URL‑t renderelni, vagy integráld ezt a logikát egy Spring Boot mikroszolgáltatásba, amely igény szerint PNG‑ket szolgáltat. A csillagok a határok, ha az Aspose.HTML rugalmasságát a Java párhuzamossági eszközeivel kombinálod.

Boldog kódolást, és ne felejtsd el megosztani a sikertörténeteidet a hozzászólásokban!

## Mit érdemes még tanulni?

- [Hogyan használjuk az Aspose‑t HTML PNG‑re rendereléshez – Lépésről‑lépésre útmutató](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [Hogyan renderelj HTML‑t PNG‑re Aspose‑szal – Teljes útmutató](/html/english/net/rendering-html-documents/how-to-render-html-to-png-with-aspose-complete-guide/)
- [Hogyan szerkessz CSS‑t – Haladó külső CSS szerkesztés Aspose.HTML for Java‑val](/html/english/java/editing-html-documents/advanced-external-css-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}