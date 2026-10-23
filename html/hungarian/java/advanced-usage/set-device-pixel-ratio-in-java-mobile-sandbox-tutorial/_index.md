---
category: general
date: 2026-10-19
description: Állítsa be a device pixel ratio-t Java-ban az Aspose.HTML sandbox használatával.
  Tanulja meg, hogyan állíthatja be a screen width height-et, és hogyan kérheti le
  a page title java-t egy teljes, futtatható példával.
draft: false
keywords:
- get page title java
- device pixel ratio java
- create virtual device java
- set screen width height
lastmod: 2026-10-19
og_description: Java oldal cím lekérése az Aspose.HTML sandbox segítségével. Ez az
  útmutató megmutatja, hogyan állíthatja be a screen width height-et és a device pixel
  ratio-t Java-ban néhány egyszerű lépésben.
og_image_alt: 'Developer guide: set device pixel ratio in Java using Aspose.HTML sandbox'
og_title: Java oldal cím lekérése – device pixel ratio beállítása Java sandbox útmutatóban
schemas:
- author: Aspose
  dateModified: '2026-10-19'
  description: set device pixel ratio in Java using Aspose.HTML sandbox. Learn how
    to set screen width height and get page title java with a complete, runnable example.
  headline: Get page title java – set device pixel ratio in Java sandbox tutorial
  type: TechArticle
- questions:
  - answer: Yes—create a new `SandboxOptions` with a different `setDevicePixelRatio`
      value and instantiate a fresh `Sandbox`. Re‑using the same sandbox after changing
      its options is not supported.
    question: Can I change the pixel ratio at runtime?
  - answer: Loop over a list of `SandboxOptions` (e.g., iPhone 8, Pixel 4) and run
      the same load‑and‑title logic for each.
    question: What if I need to test multiple devices?
  - answer: Aspose.HTML respects Java’s default SSL trust store. Add the cert to the
      JVM’s keystore or, for testing only, disable verification (not recommended for
      production).
    question: Does this work with HTTPS sites that have self‑signed certificates?
  - answer: The `HTMLDocument` API provides `save` methods that can export the rendered
      page to PNG or JPEG. Use `htmlDoc.save("output.png", SaveFormat.PNG);` after
      loading.
    question: How do I capture a screenshot instead of just the title?
  - answer: Each `Sandbox` instance is isolated, but you should avoid sharing a single
      instance across multiple threads without synchronization.
    question: Is the sandbox thread‑safe?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- mobile emulation
title: Java oldal cím lekérése – device pixel ratio beállítása Java sandbox útmutatóban
url: /hu/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java oldal cím lekérése – eszköz pixelarány beállítása Java sandbox tutorialban

Valaha is szükséged volt **set device pixel ratio** beállítására egy reszponzív weboldal tesztelésekor Java-ban? Nem vagy egyedül. Sok fejlesztő szembesül a problémával, amikor az oldal tökéletesen néz ki asztali gépen, de magas DPI‑ú telefonokon elromlik. A jó hír? Az Aspose.HTML sandbox segítségével egy iPhone X‑et (vagy bármilyen eszközt) emulálhatsz közvetlenül a Java kódodból — böngésző nélkül.

Ebben az útmutatóban végigvezetünk a **how to set screen width height** beállításán, konfiguráljuk a **device pixel ratio**‑t, és végül **get page title java**‑t, hogy ellenőrizzük, minden helyesen renderelődött. A végére egy önálló programod lesz, amelyet bármely projektbe beilleszthetsz, és azonnal elkezdhetsz mobil elrendezéseket tesztelni.

## Gyors válaszok
- **Hogyan állíthatom be a device pixel ratio‑t Java-ban?** Használd a `SandboxOptions.setDevicePixelRatio(double)`‑t a sandbox létrehozása előtt.  
- **Melyik metódus adja vissza az oldal címét?** Hívd meg a `htmlDocument.getTitle()`‑t a betöltött `HTMLDocument`‑on.  
- **Emulálhatok más eszközöket?** Igen — hozz létre egy új `SandboxOptions`‑t a kívánt szélességgel, magassággal és pixelarányával.  
- **Szükségem van böngésző driverre?** Nem, az Aspose.HTML sandbox fej nélküli és tisztán Java-ban fut.  
- **Melyik Aspose.HTML verzió szükséges?** A 23.7 vagy újabb verzió támogatja az összes mobil‑emulációs funkciót.

## Mi az a get page title java?
`get page title java` a `<title>` elem lekérésének művelete egy HTML dokumentumból Java kóddal. Lehetővé teszi, hogy megerősítsd, egy virtuális eszköz kontextusban betöltött oldal a várt címet jelenítette meg. A cím lekérése gyakori lépés az automatizált validációban, hogy biztosítsuk a helyes oldal betöltését az eszköz emulációs paraméterek alkalmazása után.

## Miért használjuk az Aspose.HTML sandboxot mobil emulációhoz?
Az Aspose.HTML **30+** bemeneti és kimeneti formátumot támogat — beleértve a HTML‑t, CSS‑t, SVG‑t és PDF‑et — és képes oldalakat renderelni anélkül, hogy teljes böngészőt indítana. A sandbox több száz oldalas webhelyeket dolgoz fel, miközben a memóriahasználatot 200 MB alatt tartja, így ideális CI csővezetékekhez.

## Előfeltételek

- Java 8 vagy újabb (a kód JDK 11‑el is fordítható)  
- Aspose.HTML for Java könyvtár (version 23.7 vagy later) – Maven Central‑ról letölthető  
- IDE vagy egyszerű `javac` parancssori beállítás  
- Internet hozzáférés a demo URL‑hez (`https://responsive.example.com`)

Nincs szükség extra keretrendszerekre, nincs Selenium, csak tiszta Java és Aspose.HTML.

## Hogyan állítsuk be a képernyő szélesség‑magasság és a device pixel ratio értékét Java-ban

A `SandboxOptions` osztály lehetővé teszi a virtuális eszköz képernyőméreteinek és pixel sűrűségének megadását. Egy adott mobil eszköz emulálásához a sandboxot a kívánt képernyőszélességgel, magassággal és device pixel ratio‑val kell konfigurálni. Egy `SandboxOptions` objektum létrehozásával és ezen tulajdonságok beállításával a renderelő motor úgy kezeli az oldalt, mintha az az adott eszközön jelenne meg, biztosítva, hogy a CSS media query‑k és a képméretezés helyesen működjön.

Hozz létre egy `SandboxOptions` példányt, állítsd be a szélességet **375**, a magasságot **812**, és a device pixel ratio‑t **3.0**. Ezután add át ezeket a beállításokat egy új `Sandbox`‑nak. Ez teljesen konfigurálja a virtuális eszközt, mielőtt bármely oldal betöltődne.

A `SandboxOptions` osztály definiálja a virtuális eszköz képernyőméretét és pixel sűrűségét. Ez a belépési pont minden mobil‑emulációs forgatókönyvhöz.

```java
// Step 1 – configure the virtual device
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixels width
sandboxOptions.setScreenHeight(812);         // CSS pixels height
sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI factor (set device pixel ratio)
```

> **Miért fontos:**  
> A `setDevicePixelRatio` hívás mindent skáláz — a képektől a betűtípus rendereléséig —, így az oldal úgy gondolja, mintha egy valódi telefonon lenne. Ha kihagyod, a layout visszatérhet az asztali stílusú CSS media query‑khez, aláássa a mobil tesztelés célját.

## Hogyan hozzuk létre a sandbox példányt

A `Sandbox` osztály egy fej nélküli böngésző környezetet képvisel, amely a korábban definiált beállításokkal rendereli a HTML‑t. A `SandboxOptions` konfigurálása után egy `Sandbox`‑t kell példányosítani ezekkel a beállításokkal, hogy izolált renderelési kontextust kapjunk. Ez a sandbox egy könnyűsúlyú böngészőként működik, alkalmazva a megadott képernyőméretet és pixel sűrűséget, és több oldal betöltésére is újrahasználható, miközben a környezet tiszta marad.

Példányosíts egy `Sandbox`‑t a korábban konfigurált `SandboxOptions`‑szal. A sandbox úgy viselkedik, mint egy apró, fej nélküli böngésző, amely tiszteletben tartja a definiált méreteket és pixelarányt.

A `Sandbox` objektum az Aspose.HTML izolált renderelő motorja, amely UI nélkül fut. Garantálja, hogy minden teszt tiszta környezetben fusson.

```java
// Step 2 – spin up the sandbox with the options above
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

> **Pro tipp:** Ugyanazt a `Sandbox` objektumot újra felhasználhatod több oldal betöltéséhez; csak változtasd meg az URL‑t, és a sandbox megtartja ugyanazokat az eszközjellemzőket.

## Hogyan töltsük be az oldalt a sandboxon belül

A `HTMLDocument` osztály egy memóriában elemzett HTML fájlt képvisel, DOM hozzáférést és renderelési lehetőséget biztosítva. A sandbox készen áll, hozd létre az `HTMLDocument`‑et a cél URL és a sandbox példány átadásával. Ez betölti és rendereli az oldalt a virtuális eszköz beállításokkal, lehetővé téve a DOM‑mal való interakciót vagy információk, például a cím kinyerését.

Hozz létre egy `HTMLDocument`‑et a cél URL és a `Sandbox` példány átadásával. Ez a dokumentumot arra kényszeríti, hogy a korábban beállított virtuális eszközzel renderelje.

A `HTMLDocument` osztály egy memóriában elemzett HTML fájlt képvisel, és módszereket biztosít a DOM manipulációhoz és metaadatok kinyeréséhez.

```java
// Step 3 – fetch the target page using the sandbox
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("https://responsive.example.com"), mobileSandbox);
```

Ha az URL elérhetetlen vagy az oldal hibákat tartalmaz, az Aspose.HTML kivételt dob. Termelési kódban ezt `try‑catch`‑ben kellene kezelni és naplózni a hibát, de a tutorial egyszerűen tartja.

## Hogyan ellenőrizzük a get page title java‑val

A `getTitle()` metódus a HTML dokumentum `<title>` elemének tartalmát egyszerű sztringként adja vissza. A cím olvasása a leggyorsabb ellenőrzés. Az oldal betöltése után hívd meg a `htmlDocument.getTitle()`‑t a cím szövegének lekéréséhez. Ez az egyszerű ellenőrzés megerősíti, hogy az oldal helyesen renderelődött az emulált eszköz beállításai alatt, és gyors módot biztosít a navigáció vagy tartalomváltozások automatizált teszteléséhez.

Hívd meg a `htmlDocument.getTitle()`‑t a betöltött dokumentumon, és írd ki az eredményt. Ha a sandbox helyesen alkalmazta a **device pixel ratio**‑t, a cím megegyezik azzal, amit egy valódi iPhone X‑en látnál.

A `getTitle()` metódus a `<title>` elem tartalmát egyszerű sztringként adja vissza, lehetővé téve a renderelés validálását vizuális ellenőrzés nélkül.

```java
// Step 4 – retrieve and print the page title (get page title java)
System.out.println("Title under sandbox: " + htmlDoc.getTitle());
```

**Várható kimenet (példa):**

```
Title under sandbox: Responsive Demo – Mobile View
```

Ha látod a kiírt címet, sikeresen **set device pixel ratio**, **set screen width height**, és **got the page title** értékeket használtad Java‑val.

## Teljes, futtatható példa

Az alábbiakban a teljes program található, amelyet beilleszthetsz egy `SandboxDemo.java` nevű fájlba. Győződj meg róla, hogy az Aspose.HTML JAR‑ok a classpath‑on (`-cp` flag) vannak a fordítás előtt.

A `SandboxDemo` osztály összekapcsolja az eddigi lépéseket egyetlen, futtatható példában.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.net.URL;

/**
 * Demonstrates how to set device pixel ratio, set screen width height,
 * and get page title java using Aspose.HTML sandbox.
 */
public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define device characteristics ----------
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS pixels width
        sandboxOptions.setScreenHeight(812);         // CSS pixels height
        sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI screen factor (set device pixel ratio)

        // ---------- Step 2: Create the sandbox ----------
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // ---------- Step 3: Load a web page inside the sandbox ----------
        HTMLDocument htmlDoc = new HTMLDocument(
                new URL("https://responsive.example.com"), mobileSandbox);

        // ---------- Step 4: Verify the document loaded correctly ----------
        System.out.println("Title under sandbox: " + htmlDoc.getTitle());
    }
}
```

Fordíts és futtasd:

```bash
javac -cp "aspose-html-23.7.jar" SandboxDemo.java
java -cp ".:aspose-html-23.7.jar" SandboxDemo
```

A konzolon meg kell jelennie a címnek, ami megerősíti, hogy az oldal a kívánt **device pixel ratio**‑val renderelődött.

## Gyakran feltett kérdések és szélhelyzetek

**Q: Can I change the pixel ratio at runtime?**  
A: Yes—create a new `SandboxOptions` with a different `setDevicePixelRatio` value and instantiate a fresh `Sandbox`. Re‑using the same sandbox after changing its options is not supported.

**Q: What if I need to test multiple devices?**  
A: Loop over a list of `SandboxOptions` (e.g., iPhone 8, Pixel 4) and run the same load‑and‑title logic for each.

**Q: Does this work with HTTPS sites that have self‑signed certificates?**  
A: Aspose.HTML respects Java’s default SSL trust store. Add the cert to the JVM’s keystore or, for testing only, disable verification (not recommended for production).

**Q: How do I capture a screenshot instead of just the title?**  
A: The `HTMLDocument` API provides `save` methods that can export the rendered page to PNG or JPEG. Use `htmlDoc.save("output.png", SaveFormat.PNG);` after loading.

**Q: Is the sandbox thread‑safe?**  
A: Each `Sandbox` instance is isolated, but you should avoid sharing a single instance across multiple threads without synchronization.

## Vizuális áttekintés

![Diagram showing set device pixel ratio in mobile sandbox](https://example.com/images/sandbox-diagram.png "set device pixel ratio diagram")

[Diagram showing set device pixel ratio in mobile sandbox](https://example.com/images/sandbox-diagram.png "set device pixel ratio diagram")

*A fenti illusztráció a folyamatot mutatja a `SandboxOptions` konfigurálásától (beleértve a **set screen width height** és **set device pixel ratio** beállításokat) egy URL betöltéséig és a cím kinyeréséig.*

## Következtetés

Most már tudod, **how to set device pixel ratio** Java‑ban, hogyan **set screen width height** a pontos mobil emulációhoz, és hogyan **get page title java**‑val ellenőrizheted, hogy a renderelés sikeres volt-e. Ez a kompakt munkafolyamat megszünteti a nehéz böngészők szükségességét az automatizált UI‑tesztelés során, és könnyen beilleszthető CI csővezetékekbe.

Készen állsz a következő lépésre? Próbáld meg exportálni a renderelt oldalt képként, vagy kísérletezz a CSS media‑query hibakereséssel a `devicePixelRatio` 1.0 és 3.0 közötti váltogatásával. Felfedezheted továbbá az Aspose.HTML PDF konverziós funkcióit is, hogy nyomtatható változatot készíts a mobil nézetről.

Boldog kódolást, és legyenek a mobil elrendezéseid mindig élesek — függetlenül a pixel sűrűségtől!

---

**Legutóbb frissítve:** 2026-10-19  
**Tesztelve a:** Aspose.HTML 23.7 for Java  
**Szerző:** Aspose

## Kapcsolódó oktatóanyagok

- [HTML cím lekérése Java-ban, oldal renderelése sandboxban képernyő szélességgel](/html/java/advanced-usage/get-html-title-java-render-page-in-sandbox-with-screen-width/)
- [Aspose HTML sandbox létrehozása – teljes Java útmutató](/html/java/configuring-environment/create-aspose-html-sandbox-complete-java-guide/)
- [Device pixel ratio beállítása Java-ban – teljes útmutató](/html/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}