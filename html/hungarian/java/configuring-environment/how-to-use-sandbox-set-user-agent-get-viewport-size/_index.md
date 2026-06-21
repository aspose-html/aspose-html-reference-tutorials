---
category: general
date: 2026-04-03
description: Tanulja meg, hogyan használja a sandboxot az Aspose.HTML Java-ban a felhasználói
  ügynök beállításához, a méret beállításához, és a nézetablak méretének azonnali
  lekéréséhez. Teljes kód, magyarázatok és tippek benne.
draft: false
keywords:
- how to use sandbox
- set user agent
- get viewport size
- how to set size
- how to get viewport
language: hu
og_description: Tanulja meg, hogyan használja a sandboxot az Aspose.HTML Java-ban
  a felhasználói ügynök, a méret beállításához, és a nézetablak méretének azonnali
  lekéréséhez. Teljes útmutató kóddal és legjobb gyakorlatokkal.
og_title: Hogyan használjuk a Sandboxot – Állítsd be a felhasználói ügynököt és szerezd
  meg a nézetablak méretét
tags:
- AsposeHTML
- Java
- Sandbox
title: Hogyan használjuk a Sandboxot – Felhasználói ügynök beállítása és a nézetablak
  méretének lekérése
url: /hu/java/configuring-environment/how-to-use-sandbox-set-user-agent-get-viewport-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjuk a Sandboxot – Felhasználói ügynök beállítása és a nézetablak méretének lekérése

Gondolkodtál már azon, **hogyan használjuk a sandboxot** HTML rendereléskor az Aspose.HTML for Java-val? Lehet, hogy elakadtál egy adott képernyőméret szimulálásánál, vagy egy user‑agent karakterláncot kellene hamisítanod, hogy az oldal úgy viselkedjen, mintha egy mobil böngészőből érkezne.  

A jó hír, hogy a sandbox API pontosan ezt teszi lehetővé, és a betöltött oldal után lekérheted a kiszámított viewport méretet is. Ebben az útmutatóban végigvezetünk a sandbox létrehozásán, a méret beállításán, egy egyedi felhasználói ügynök megadásán, egy távoli oldal betöltésén, és végül a viewport dimenziók kiolvasásán. A végére megtudod, **hogyan állítsuk be a méretet**, **hogyan szerezzük meg a viewportot**, és miért fontosak ezek a lépések a megbízható headless rendereléshez.

> **Gyors nyeremény:** néhány másodperc alatt lesz egy futtatható Java osztályod, amely például `Viewport: 1280×800`‑at ír ki.

---

## Amire szükséged lesz

- **Aspose.HTML for Java** 24.6 vagy újabb verzió (az általunk használt API a 24.5‑ben került bevezetésre).  
- Java 17+ fejlesztői csomag (bármely friss JDK megfelelő).  
- IDE vagy egyszerű szövegszerkesztő – nincs szükség külön pluginekre.  
- Internetkapcsolat, ha külső URL-t szeretnél betölteni, például `https://example.com`.

Ez minden. Nem kötelező Maven/Gradle varázslat; ha szeretnéd, a JAR‑okat manuálisan is felveheted a classpath‑ba.

---

## Hogyan használjuk a Sandboxot – Áttekintés

A sandbox elkülöníti a renderelő motort a gazda operációs rendszertől, lehetővé téve egy virtuális képernyő (szélesség, magasság, DPI) és egy egyedi **user agent** karakterlánc definiálását. Olyan mini böngészőablak, amely teljesen a memóriában él. Amikor később a `HTMLDocument`‑tól lekéred az alapértelmezett nézetet, a motor a sandbox beállításai alapján számított **viewport méretet** adja vissza.

Az alábbi magas szintű folyamat:

1. **Létrehozni** egy `DocumentSandbox`‑ot, és beállítani a szélességet, magasságot, DPI‑t és a user‑agent‑et.  
2. **Betölteni** egy `HTMLDocument`‑ot ebben a sandboxban.  
3. **Lekérdezni** a dokumentum alapértelmezett nézetét a viewport méretéért.  

Merüljünk el az egyes lépésekben.

---

## 1. lépés: Sandbox létrehozása és méret beállítása

Először felállítunk egy sandboxot, és megadjuk, mekkora legyen a virtuális képernyő. Itt válaszolod meg a **hogyan állítsuk be a méretet** kérdést egy headless rendereléshez.

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.drawing.Size2D;

/* Step 1 – instantiate the sandbox */
DocumentSandbox sandbox = new DocumentSandbox();

/* Set the virtual screen width & height (in pixels) */
sandbox.setScreenWidth(1280);   // width in pixels
sandbox.setScreenHeight(800);   // height in pixels

/* DPI influences CSS pixel calculations – 96 is the CSS default */
sandbox.setDeviceDpi(96);

/* Optional: give the sandbox a friendly name for debugging */
sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");
```

> **Pro tipp:** Ha reszponzív elrendezést tesztelsz, próbálj ki egy keskeny szélességet, például `360`‑at, hogy telefonra emulálj, vagy egy széleset, például `1920`‑at, asztali gépre. A sandbox tiszteletben tartja a beállított DPI‑t, így egy nagy sűrűségű képernyő (pl. 144 DPI) befolyásolja a `device-pixel-ratio`‑t használó media‑query‑ket.

---

## 2. lépés: Felhasználói ügynök beállítása a Sandboxhoz

Miért érdemes egy egyedi **user agent**‑et használni? Egyes oldalak a bejelentett böngésző alapján különböző markup‑ot vagy szkripteket szolgáltatnak. A `setUserAgent` meghívásával megtévesztheted az oldalt, hogy Chrome‑ból, Firefox‑ból vagy egy mobil eszközről érkezik a kérés.

```java
/* Step 2 – customize the user‑agent string */
sandbox.setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                     "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                     "Version/15.0 Mobile/15E148 Safari/604.1");
```

Most az oldal úgy gondolja, hogy egy iPhone‑on renderelődik. Ha vissza szeretnéd állítani a **user agent**‑et az alapértelmezettre, egyszerűen használd újra a korábbi “AsposeHTML/24.6 …” karakterláncot.

---

## 3. lépés: HTML dokumentum betöltése a Sandboxban

A sandbox készen áll, ezért betölthetünk bármilyen URL‑t vagy helyi HTML fájlt. A `HTMLDocument` konstruktor második argumentumaként a sandboxot adja meg, így a két komponens összekapcsolódik.

```java
import com.aspose.html.HTMLDocument;

/* Step 3 – load the page using the configured sandbox */
try (HTMLDocument doc = new HTMLDocument("https://example.com", sandbox)) {
    // The document is now rendered inside the sandbox environment.
    // Any JavaScript or CSS will see the size and user‑agent we defined.
```

A `try‑with‑resources` blokk biztosítja, hogy a dokumentum megfelelően felszabaduljon, és a natív erőforrások, amelyeket az Aspose.HTML a háttérben allokál, felszabaduljanak.

---

## 4. lépés: Viewport méretének lekérése a dokumentumból

Itt a várt pillanat: a **viewport méretének** lekérése, amelyet a renderelő motor számolt ki. Ez válaszol a **hogyan szerezzük meg a viewportot** kérdésre a layout után.

```java
    /* Step 4 – fetch the viewport dimensions */
    Size2D viewport = doc.getDefaultView().getScreenSize();
    System.out.println("Viewport: " + viewport.getWidth() + "×" + viewport.getHeight());
}
```

A program futtatásakor valami ilyesmit kell látnod:

```
Viewport: 1280×800
```

Ha az 1. lépésben megváltoztattad a sandbox méreteit, a kiírt számok tükrözni fogják az új értékeket – tökéletes automatizált tesztekhez, amelyek a reszponzív breakpoint‑okat ellenőrzik.

---

## Teljes működő példa

Az alábbiakban a komplett, azonnal futtatható osztály található, amely minden elemet egyesít. Másold be egy `SandboxExample.java` nevű fájlba, add hozzá az Aspose.HTML JAR‑okat a classpath‑hoz, és futtasd a `java SandboxExample` parancsot.

```java
import com.aspose.html.*;
import com.aspose.html.drawing.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox with a custom screen size and DPI
        DocumentSandbox sandbox = new DocumentSandbox();
        sandbox.setScreenWidth(1280);          // width in pixels
        sandbox.setScreenHeight(800);          // height in pixels
        sandbox.setDeviceDpi(96);              // screen DPI
        sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");

        // Step 2: (Optional) Override the user agent if you need a mobile profile
        sandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
            "Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 3: Load the HTML document inside the configured sandbox
        try (HTMLDocument htmlDocument = new HTMLDocument("https://example.com", sandbox)) {

            // Step 4: Retrieve and display the computed viewport size
            Size2D viewportSize = htmlDocument.getDefaultView().getScreenSize();
            System.out.println("Viewport: " + viewportSize.getWidth() + "×" + viewportSize.getHeight());
        }
    }
}
```

**Várható kimenet** (a fenti sandbox beállításokkal):

```
Viewport: 1280×800
```

Ha a sandboxban más szélességet/magasságot állítasz be, a kimenet ennek megfelelően változik – pontosan az, amire szükséged van a reszponzív tervezés teszteléséhez.

---

## Szélsőséges esetek és gyakori kérdések

### Mi van, ha az oldal a `window.innerWidth`‑t használja a CSS média lekérdezések helyett?

A sandbox virtuális képernyőmérete mind a CSS layoutot, mind a JavaScript `window.innerWidth/innerHeight` értékét befolyásolja. Így a **viewport lekérése** JavaScript‑ben ugyanazokat a számokat adja vissza, mint a Java konzol.

### Futtathatok több sandboxot párhuzamosan?

Igen. Minden `DocumentSandbox` példány független, így létrehozhatsz egy szálkészletet, ahol minden szál saját sandboxot kap különböző méretekkel, és egyszerre több tucat oldalt renderelhetsz. Csak ne feledd, hogy a JAR‑ok szálbiztosak (így is vannak).

### Befolyásolja a DPI beállítás a képek méretezését?

Abszolút. A magasabb DPI több eszközpixelhez rendeli egy CSS pixelt, ami a nagy felbontású képek élesebb megjelenését eredményezheti. Ha retina‑stílusú asseteket tesztelsz, próbáld ki a `sandbox.setDeviceDpi(144)` beállítást.

### Hogyan kezeljem a saját aláírású HTTPS tanúsítványokat

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}