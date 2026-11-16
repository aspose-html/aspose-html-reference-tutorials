---
category: general
date: 2026-04-02
description: Tanulja meg, hogyan állíthatja be a DPI-t, a nézetablak méretét és a
  felhasználói ügynököt az Aspose.HTML Sandboxban. Lépésről lépésre Java példa teljes
  kóddal és tippekkel.
draft: false
keywords:
- how to set dpi
- set viewport size
- set user agent
- Aspose.HTML sandbox
- Java rendering settings
language: hu
og_description: Tanulja meg, hogyan állíthatja be a DPI-t, a nézetablak méretét és
  a felhasználói ügynököt az Aspose.HTML Sandbox-ban egy teljes Java példával.
og_title: Hogyan állítsuk be a DPI-t az Aspose.HTML Sandboxban – Java útmutató
tags:
- Aspose.HTML
- Java
- Rendering
- Sandbox
title: Hogyan állítsuk be a DPI-t az Aspose.HTML Sandboxban – Teljes Java útmutató
url: /hu/java/configuring-environment/how-to-set-dpi-in-aspose-html-sandbox-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan állítsuk be a DPI-t az Aspose.HTML Sandboxban – Teljes Java útmutató

Gondolkodtál már azon, **hogyan állítsuk be a DPI-t** egy weboldal renderelésekor az Aspose.HTML segítségével? Nem vagy egyedül. Sok tesztelési helyzetben szükség van arra, hogy a layout egy adott képernyősűrűségnek megfelelő legyen – gondolj nyomtatásra kész PDF-ekre vagy nagy felbontású képernyőképekre. A jó hír, hogy az Aspose.HTML sandbox lehetővé teszi a DPI, a viewport méret és még a user‑agent karakterlánc egyetlen praktikus csomagban történő vezérlését.

Ebben az útmutatóban egy gyakorlati Java példán keresztül mutatjuk be, hogyan **állítható be a DPI**, **állítható be a viewport méret**, és **állítható be a user agent** egyszerre. A végére egy futtatható programmal, a beállítások jelentőségének megértésével és a sandbox saját projektjeidhez való testreszabásához szükséges tudással leszel felvértezve.

---

## Amire szükséged lesz

- **Java 17** (vagy bármely friss JDK; az API kompatibilis a Java 8+ verzióval)
- **Aspose.HTML for Java** könyvtár (23.12 vagy újabb verzió)
- Egy IDE vagy egyszerű szövegszerkesztő + parancssori fordítás
- Internetkapcsolat a minta URL-hez (`https://example.com`)

Külső build eszközök nem szükségesek; a kód `javac`‑el fordítható és `java`‑val futtatható. Ha inkább Maven‑t vagy Gradle‑t használsz, csak add hozzá az Aspose.HTML függőséget – semmi bonyolult.

## 1. lépés: Sandbox létrehozása, amely meghatározza a renderelési környezetet

A sandbox az a hely, ahol megmondod az Aspose.HTML‑nek, milyen “képernyővel” szeretnél szimulálni. Itt beállítunk egy **1024 × 768-as viewport-ot**, egy **96 DPI‑t**, és egy egyedi **user‑agent karakterláncot**.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Define the sandbox – this is the core of how to set dpi, viewport, and user agent.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent
```

**Miért fontos ez:**
- **DPI** befolyásolja, hogy a CSS `pt` egységek hogyan alakulnak pixelekké; a magasabb DPI élesebb renderelést eredményez.
- **Viewport méret** meghatározza a layout töréspontjait, amelyeket a responsív CSS elér.
- **User‑agent** képes szerveroldali tartalomváltozatokat kiváltani (mobil vs asztali).

> **Pro tipp:** Ha később PDF‑eket generálsz, állítsd a DPI‑t a célnyomtatási felbontáshoz (pl. 300 dpi a magas minőségű nyomtatáshoz).

## 2. lépés: Weboldal betöltése a Sandboxban

Most a sandboxot egy URL-re irányítjuk. A `HTMLDocument` konstruktor elfogadja a sandboxot, így a layout motor tiszteletben tartja a most beállított paramétereket.

```java
        // Load the page using the sandbox we just configured.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {
```

**Mi történik a háttérben?**  
Aspose.HTML egy izolált renderelési kontextust hoz létre, amely a headless böngészőhöz hasonló, de a teljes Chromium példány terhe nélkül. Ez gyors és memória‑kímélő működést biztosít – tökéletes kötegelt feldolgozáshoz.

## 3. lépés: Interakció a DOM‑mal – Az oldal címének kiolvasása

Bemutatóként kiolvassuk a címet és kiírjuk. Valódi környezetben készíthetsz képernyőképet, exportálhatsz PDF‑be, vagy adatot gyűjthetsz.

```java
            // Simple DOM interaction – fetch and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());
        }
    }
}
```

**Várható kimenet** (ha a `https://example.com` elérhető):

```
Title inside sandbox: Example Domain
```

Ha a weboldal más címet ad vissza, azt fogod látni – egyébként nem kell módosítanod semmit.

## 4. lépés: Beállítások ellenőrzése (opcionális hibakeresés)

Néha szeretnéd duplán ellenőrizni, hogy a sandbox valóban tiszteletben tartja a DPI‑t és a viewport‑ot. Az Aspose.HTML nem adja közvetlenül ezeket az értékeket, de a elemek méretének mérésével következtethetsz rájuk.

```java
        // Example: measure a known element's width in pixels.
        int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
        System.out.println("Measured width (px): " + elementWidth);
```

Ha tudod, hogy a CSS `width: 200pt;`‑ként deklarálja az elemet, **96 dpi** esetén `200pt * (96/72) ≈ 267px`-ot kell látnod. Módosítsd a DPI‑t és futtasd újra, hogy lásd a szám változását – bizonyíték arra, hogy a **hogyan állítsuk be a dpi** valóban működik.

## Teljes forráskód egy blokkban

Másold be a következőt a `SandboxExample.java` fájlba. Ahogy van, lefordítható; csak győződj meg róla, hogy az Aspose.HTML JAR a classpath‑on van.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox that defines the rendering environment
        // (viewport size 1024×768 and 96 dpi) and a custom user‑agent string.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent

        // Step 2: Load a web page inside the sandbox so layout respects the settings.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {

            // Step 3: Interact with the DOM – here we simply read and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());

            // Optional: verify DPI effect by measuring an element (if you know its CSS size).
            // int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
            // System.out.println("Measured width (px): " + elementWidth);
        }
    }
}
```

Fordítás és futtatás:

```bash
javac -cp "aspose-html-23.12.jar" SandboxExample.java
java -cp ".:aspose-html-23.12.jar" SandboxExample
```

A címnek ki kell nyomtatódnia, ami megerősíti, hogy a sandbox a megadott **beállított dpi**, **beállított viewport méret**, és **beállított user agent** értékekkel működik.

## Gyakori kérdések és speciális esetek

### Mi van, ha más DPI‑ra van szükségem?

Csak módosítsd a `DocumentSandbox` második argumentumát. Nyomtatásra kész PDF‑ekhez például `300`-at használhatsz:

```java
new DocumentSandbox(new Size(1024, 768), 300, "MyCustomUserAgent/1.0");
```

A magasabb DPI nagyobb pixelméreteket eredményez ugyanazokhoz a CSS pontokhoz, ami javítja a raszter minőségét, de több memóriát igényel.

### Betölthetek helyi HTML fájlt URL helyett?

Természetesen. Cseréld le az URL‑t egy fájl útvonalra:

```java
HTMLDocument webDoc = new HTMLDocument("file:///C:/myfolder/page.html", renderingSandbox);
```

Győződj meg róla, hogy az útvonal abszolút és a `file:///` sémát használja.

### Hogyan változtathatom meg a user‑agent‑et a sandbox létrehozása után?

A sandbox immutable – miután átadtad a `HTMLDocument`‑nek, a beállítások rögzülnek. Más user‑agent használatához hozz létre egy új `DocumentSandbox`‑t a kívánt karakterlánccal.

### Támogatja az Aspose.HTML a JavaScript végrehajtását?

Igen, a motor a legtöbb kliensoldali scriptet futtatja. Ha egy script a betöltés után módosítja a DOM‑ot, várhatsz egy kicsit:

```java
webDoc.waitForLoad();
```

Vagy használj `setTimeout`‑szerű logikát az oldalon, mielőtt elemeket kérdeznél le.

## Vizuális megerősítés (Kép)

Az alábbi képernyőképen látható a konzol sikeres futása. Figyeld meg, hogy a cím kimenete megegyezik az oldallal, ami megerősíti, hogy a sandbox tiszteletben tartotta a beállításainkat.

![Konzol kimenet, amely bemutatja a DPI beállítását az Aspose.HTML Sandboxban](/images/console-output.png)

*Alt szöveg:* *Konzol kimenet, amely bemutatja a DPI, a viewport méret és a user agent beállítását az Aspose.HTML Sandboxban.*

## Összefoglalás és következő lépések

Áttekintettük, **hogyan állítsuk be a DPI‑t** (96 dpi a példában), **hogyan állítsuk be a viewport méretet** (1024 × 768), és **hogyan állítsuk be a user agent‑et** (egyedi karakterlánc) az Aspose.HTML sandbox API‑jával. A teljes, futtatható Java program bizonyítja, hogy ezek a beállítások nem csak elméletiak – közvetlenül befolyásolják a renderelést és a DOM‑interakciót.

Készen állsz a továbbiakra?
- **Exportálás PDF‑be:** Az oldal betöltése után hívd meg a `webDoc.save("output.pdf", SaveFormat.PDF);` metódust, hogy a beállított DPI‑t tükröző nagy felbontású PDF‑et generálj.  
- **Képernyőkép készítése:** Használd a `webDoc.renderToBitmap("screenshot.png");` metódust pixel‑tökéletes képekhez.  
- **Responsív layoutok kísérletezése:** Módosítsd a viewport méreteket, hogy mobil töréspontokat tesztelj valódi eszköz nélkül.  

Kísérletezz különböző DPI értékekkel, viewport kombinációkkal és user‑agent‑ekkel, hogy lásd, hogyan reagálnak a szerverek és a CSS. A sandbox egy könnyű játszótér, amely megkímél attól, hogy teljes böngészőket kelljen indítanod.

### Fedezd fel tovább
- **Aspose.HTML dokumentáció** – mélyebb betekintés a `DocumentSandbox` opciókba.  
- **Haladó CSS media query‑k** – tanuld meg, hogyan vált ki a viewport méret különböző stílusokat.  
- **User‑Agent hamisítás** – fedezd fel, hogyan szolgáltatnak egyes oldalak alternatív markup‑ot az agent karakterlánc alapján.

Van kérdésed vagy egy bonyolult eset? Írj egy megjegyzést, és együtt megoldjuk. Boldog kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}