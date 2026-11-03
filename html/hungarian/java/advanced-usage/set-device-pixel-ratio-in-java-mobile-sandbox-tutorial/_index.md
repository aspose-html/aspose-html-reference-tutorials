---
category: general
date: 2026-02-10
description: Állítsa be az eszköz pixelarányát Java-ban az Aspose.HTML sandbox használatával.
  Tanulja meg, hogyan állíthatja be a képernyő szélességét és magasságát, valamint
  hogyan szerezheti meg az oldal címét Java-ban egy teljes, futtatható példával.
draft: false
keywords:
- set device pixel ratio
- get page title java
- set screen width height
language: hu
og_description: Állítsa be az eszköz pixelarányát Java-ban az Aspose.HTML sandbox
  segítségével. Ez az útmutató néhány egyszerű lépésben megmutatja, hogyan állíthatja
  be a képernyő szélességét és magasságát, valamint hogyan szerezheti meg az oldal
  címét Java-ban.
og_title: Eszköz pixelarány beállítása Java-ban – Mobile Sandbox útmutató
tags:
- Aspose.HTML
- Java
- Mobile Emulation
title: Eszköz pixelarány beállítása Java‑ban – Mobil Sandbox oktató
url: /hu/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# eszköz pixel arány beállítása Java-ban – Mobil Sandbox útmutató

Volt már szükséged arra, hogy **set device pixel ratio**-t állíts be egy reszponzív weboldal tesztelése közben Java-ban? Nem vagy egyedül. Sok fejlesztő akad el, amikor az oldal tökéletesen néz ki asztali gépen, de magas DPI‑ú telefonokon elromlik. A jó hír? Az Aspose.HTML sandbox segítségével egy iPhone X-et (vagy bármilyen más eszközt) emulálhatsz közvetlenül a Java kódodból – böngésző nélkül.

Ebben az útmutatóban végigvezetünk a **how to set screen width height** beállításán, a **device pixel ratio** konfigurálásán, és végül a **get page title java** használatán, hogy ellenőrizd, minden helyesen renderelődik-e. A végére egy önálló programod lesz, amelyet bármelyik projektbe beilleszthetsz, és azonnal elkezdhetsz mobil elrendezéseket tesztelni.

## Előkövetelmények

- Java 8 vagy újabb (a kód JDK 11‑el is fordítható)  
- Aspose.HTML for Java könyvtár (23.7‑es vagy újabb verzió) – Maven Central‑ról letölthető  
- Egy IDE vagy egyszerű `javac` parancssori beállítás  
- Internetkapcsolat a bemutató URL-hez (`https://responsive.example.com`)

Nincs extra keretrendszer, nincs Selenium, csak tiszta Java és Aspose.HTML.

---

## 1. lépés: Képernyő szélesség és magasság beállítása és device pixel ratio

Az első dolog, amire szükségünk van, egy `SandboxOptions` objektum, amely megmondja a sandboxnak, milyen „eszköznek” akarunk látszani. Itt az iPhone X méreteket (375 × 812 CSS pixel) használjuk, és egy **device pixel ratio** értéket 3.0, ami tükrözi a magas DPI‑ú retina kijelzőt.

```java
// Step 1 – configure the virtual device
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixels width
sandboxOptions.setScreenHeight(812);         // CSS pixels height
sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI factor (set device pixel ratio)
```

> **Miért fontos:**  
> A `setDevicePixelRatio` hívás mindent skáláz—a képektől a betűk megjelenítéséig—így az oldal úgy gondolja, mintha egy valódi telefonon lenne. Ha kihagyod, a layout visszatérhet az asztali stílusú CSS media query‑khez, aláássa a mobil tesztelés célját.

---

## 2. lépés: Sandbox példány létrehozása

Most ezeket a beállításokat élő sandbox-sá alakítjuk. Tekintsd a sandbox-ot egy kis, fej nélküli böngészőnek, amely tiszteletben tartja a most megadott méreteket és pixel arányt.

```java
// Step 2 – spin up the sandbox with the options above
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

> **Pro tipp:** Újra felhasználhatod ugyanazt a `Sandbox` objektumot több oldal betöltéséhez; csak változtasd meg az URL-t, és a sandbox megtartja ugyanazokat az eszközjellemzőket.

---

## 3. lépés: Oldal betöltése a sandboxon belül

A sandbox készen áll, egy oldal betöltése olyan egyszerű, mint egy `HTMLDocument` létrehozása és a sandbox átadása második argumentumként. Ez arra kényszeríti a dokumentumot, hogy a korábban beállított virtuális eszközzel rendereljen.

```java
// Step 3 – fetch the target page using the sandbox
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("https://responsive.example.com"), mobileSandbox);
```

Ha az URL elérhetetlen vagy az oldal hibákat tartalmaz, az Aspose.HTML kivételt dob. Gyártási kódban valószínűleg `try‑catch`‑be tennéd és naplóznád a hibát, de a bemutatóban egyszerűen hagyjuk.

---

## 4. lépés: Ellenőrzés a get page title java segítségével

A leggyorsabb ellenőrzés a dokumentum címének kiolvasása. Ha a sandbox helyesen alkalmazta a **device pixel ratio**-t, a cím megegyezik azzal, amit egy valódi iPhone X-en látnál.

```java
// Step 4 – retrieve and print the page title (get page title java)
System.out.println("Title under sandbox: " + htmlDoc.getTitle());
```

**Várható kimenet (példa):**

```
Title under sandbox: Responsive Demo – Mobile View
```

Ha a cím megjelenik, sikeresen **set device pixel ratio**‑t, **set screen width height**‑t állítottál be, és **got the page title**‑t használtál Java-val.

---

## Teljes, futtatható példa

Alább a teljes program, amelyet beilleszthetsz egy `SandboxDemo.java` nevű fájlba. Győződj meg róla, hogy az Aspose.HTML JAR-ok a classpath‑on (`-cp` kapcsoló) vannak, mielőtt lefordítod.

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

Fordítás és futtatás:

```bash
javac -cp "aspose-html-23.7.jar" SandboxDemo.java
java -cp ".:aspose-html-23.7.jar" SandboxDemo
```

A konzolon meg kell jelennie a címnek, ami megerősíti, hogy az oldal a kívánt **device pixel ratio**-val renderelődött.

---

## Gyakran Ismételt Kérdések és Szélsőséges Esetek

| Kérdés | Válasz |
|----------|--------|
| **Módosíthatom a pixel arányt futás közben?** | Igen—csak hozz létre egy új `SandboxOptions` objektumot egy másik `setDevicePixelRatio` értékkel, és példányosíts egy új `Sandbox`‑t. A már meglévő sandbox újrahasználata a beállítások módosítása után nem támogatott. |
| **Mi van, ha több eszközt kell tesztelnem?** | Iterálj egy `SandboxOptions` listán (pl. iPhone 8, Pixel 4), és minden egyeshez futtasd ugyanazt a betöltés‑és‑cím logikát. |
| **Működik ez HTTPS oldalakkal, amelyek önaláírt tanúsítvánnyal rendelkeznek?** | Az Aspose.HTML tiszteletben tartja a Java alapértelmezett SSL trust store‑ját. Add hozzá a tanúsítványt a JVM keystore‑jához, vagy csak tesztelés céljából tiltsd le a hitelesítést (nem ajánlott éles környezetben). |
| **Hogyan készítsek képernyőképet a cím helyett?** | Az `HTMLDocument` API `save` metódusokat kínál, amelyekkel a renderelt oldalt PNG‑ vagy JPEG‑formátumba exportálhatod. Használd a `htmlDoc.save("output.png", SaveFormat.PNG);` hívást a betöltés után. |
| **A sandbox szálbiztos?** | Minden `Sandbox` példány izolált, de kerülni kell egyetlen példány több szál közötti megosztását szinkronizáció nélkül. |

---

## Vizuális áttekintés

![Diagram a mobil sandboxban beállított device pixel ratio-ról](https://example.com/images/sandbox-diagram.png "device pixel ratio diagram")

*A fenti ábra a folyamatot ábrázolja a `SandboxOptions` konfigurálásától (beleértve a **set screen width height**‑t és a **set device pixel ratio**‑t) a URL betöltéséig és a cím kinyeréséig.*

---

## Következtetés

Most már tudod, hogyan **set device pixel ratio**‑t állíts be Java-ban, hogyan **set screen width height**‑t a pontos mobil emulációhoz, és hogyan **get page title java**‑t használj a renderelés sikerességének ellenőrzésére. Ez a kompakt munkafolyamat megszünteti a nehéz böngészők szükségességét az automatizált UI tesztelés során, és könnyen illeszkedik a CI csővezetékekbe.

Készen állsz a következő lépésre? Próbáld meg exportálni a renderelt oldalt képként, vagy kísérletezz a CSS media‑query hibakereséssel a `devicePixelRatio` 1.0 és 3.0 közötti váltogatásával. Emellett felfedezheted az Aspose.HTML PDF konverziós funkcióit, hogy nyomtatható változatot készíts a mobil nézetről.

Boldog kódolást, és legyenek a mobil elrendezéseid mindig élesek—függetlenül a pixel sűrűségtől!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}