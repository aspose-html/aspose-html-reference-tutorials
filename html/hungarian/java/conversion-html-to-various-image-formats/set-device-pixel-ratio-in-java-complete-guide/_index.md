---
category: general
date: 2026-02-22
description: Állítsa be az eszköz pixelarányát Java-ban az Aspose.HTML sandbox segítségével.
  Tanulja meg, hogyan állíthat be egyedi felhasználói ügynököt, hogyan kérdezheti
  le az oldal címét Java-ban, és hogyan konvertálhat HTML-t PNG-re egyetlen oktatóanyagon
  belül.
draft: false
keywords:
- set device pixel ratio
- set custom user agent
- save html as image
- convert html to png
- get page title java
language: hu
og_description: Állítsd be az eszköz pixelarányát Java-ban az Aspose.HTML sandbox
  használatával. Ez az útmutató bemutatja, hogyan állítható be egyéni felhasználói
  ügynök, hogyan lehet lekérni az oldal címét Java-ban, és hogyan konvertálható a
  HTML PNG-re.
og_title: A Device Pixel Ratio beállítása Java-ban – Teljes útmutató
tags:
- Aspose.HTML
- Java
- Web Rendering
title: Készülék pixelarány beállítása Java-ban – Teljes útmutató
url: /hu/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eszköz pixelarány beállítása Java-ban – Teljes útmutató

Gondolkodtál már azon, hogyan **állítsd be az eszköz pixelarányt** weboldal Java-ból történő renderelésekor? Nem vagy egyedül. Sok fejlesztőnek szüksége van a magas DPI‑ú mobil képernyők emulálására, hogy a képernyőképek élesek legyenek, különösen akkor, amikor később **html-t képként mentik** jelentésekhez vagy marketing anyagokhoz. Ebben az útmutatóban egy gyakorlati példán keresztül mutatjuk be, hogyan lehet ezt pontosan megtenni—miközben azt is megmutatjuk, hogyan **állíts be egyedi felhasználói ügynököt**, **kapd meg a oldal címét Java-ban**, és **konvertáld a html-t png-re** az Aspose.HTML segítségével.

Kezdetben egy rövid áttekintést adunk a sandbox API-ról, majd részletesen bemutatjuk az egyes konfigurációs lépéseket, végül egy PNG fájlt generálunk, amely egy valódi iPhone kijelzőt tükröz. A végére egy újrahasználható kódrészletet kapsz, amelyet bármely Java projektbe beilleszthetsz. Nincs szükség külső eszközökre, csak tiszta Java és az Aspose.HTML 7.x (vagy újabb).

---

## Előfeltételek

- Java 17 vagy újabb (a kód korábbi verziókkal is lefordítható, de a 17 ajánlott).
- Aspose.HTML for Java könyvtár (töltsd le a hivatalos Aspose weboldalról; Maven koordináták: `com.aspose:aspose-html:23.10`).
- A kedvenc IDE-d vagy szövegszerkesztőd (IntelliJ IDEA, VS Code, Eclipse… mind működik).
- Internetkapcsolat a demó URL-hez (`https://example.com/responsive.html`), vagy cseréld le egy saját nyilvános HTML oldalra.

> **Pro tipp:** Ha proxy mögött vagy, állítsd be a JVM `http.proxyHost` és `http.proxyPort` rendszer tulajdonságait a kód futtatása előtt.

## 1. lépés: Eszköz pixelarány és egyéb sandbox beállítások

Az első dolog, amire szükségünk van, egy **SandboxOptions** példány, ahol meghatározzuk a virtuális képernyőméretet és a *device pixel ratio* (DPR) értékét. A DPR-t úgy kell elképzelni, mint azt a tényezőt, amely megmondja a böngészőnek, hány fizikai pixel felel meg egy CSS pixelnek. Egy Retina iPhone esetén a DPR általában **2.0**, ezért ezt az értéket fogjuk használni.

```java
// Step 1: Create and configure SandboxOptions
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS width of an iPhone X
sandboxOptions.setScreenHeight(667);         // CSS height
sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
```

> **Miért fontos:** A helyes DPR beállítása nélkül a renderelt kép elmosódott vagy túl nagy lesz, mivel a rasterizáló 1:1 pixel leképezést feltételez.

## 2. lépés: Egyedi felhasználói ügynök beállítása

A weboldalak gyakran különböző markup-ot szolgáltatnak a **User‑Agent** fejléc alapján. Annak érdekében, hogy az oldal úgy viselkedjen, mint egy valódi iPhone-on, egy egyedi karakterláncot injektálunk, amely a Safari iOS változatát utánozza.

```java
// Step 2: Define a mobile‑specific user agent
String iphoneUA = "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                  "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                  "Version/14.0 Mobile/15E148 Safari/604.1";

sandboxOptions.setUserAgent(iphoneUA);   // <-- set custom user agent
```

> **Különleges eset:** Néhány oldal a `Accept-Language` fejlécet is ellenőrzi. Ha hiányzó fordításokat észlelsz, add hozzá a `sandboxOptions.setAcceptLanguage("en-US,en;q=0.9");` sort.

## 3. lépés: Az oldal betöltése a sandboxban és a cím lekérése

Most elindítjuk a sandboxot a most definiált beállításokkal. A **Sandbox** objektum izolálja a renderelési folyamatot, biztosítva, hogy a DPR és a felhasználói ügynök beállításaink érvényesüljenek.

```java
// Step 3: Create the sandbox and load the HTML document
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
HTMLDocument htmlDoc = new HTMLDocument(
        "https://example.com/responsive.html", mobileSandbox);
```

Miután az oldal betöltődött, a cím lekérése olyan egyszerű, mint a `getTitle()` meghívása. Ez teljesíti a **get page title java** követelményt.

```java
// Step 3b: Print the page title to the console
System.out.println("Title: " + htmlDoc.getTitle());   // <-- get page title java
```

**Várható konzolkimenet**

```
Title: Responsive Demo – Mobile View
```

Ha a cím üres, ellenőrizd újra az URL-t, vagy győződj meg róla, hogy az oldalt nem blokkolja a CORS szabályzat.

## 4. lépés: HTML konvertálása PNG-re és HTML mentése képként

Az Aspose.HTML lehetővé teszi, hogy a DOM-ot közvetlenül képfájlba rendereld. Mivel már beállítottuk a DPR-t 2.0-ra, a kapott PNG dupla pixel sűrűségű lesz, így éles képernyőképet eredményez.

```java
// Step 4: Render and save as PNG (convert html to png)
htmlDoc.save("mobile_view.png");   // <-- save html as image
```

A `save` metódus automatikusan felismeri a fájl kiterjesztését és a megfelelő renderelőt választja. Ha más formátumra (JPEG, BMP) van szükséged, egyszerűen módosítsd a fájlnevet ennek megfelelően.

> **Mi van, ha egy adott képméretre van szükséged?**  
> Használd a `ImageSaveOptions`-t a szélesség, magasság és háttérszín szabályozásához:

```java
ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
pngOptions.setWidth(750);   // 375 CSS px * DPR 2
pngOptions.setHeight(1334);
htmlDoc.save("mobile_view_custom.png", pngOptions);
```

## Teljes működő példa

Az alábbiakban a teljes, azonnal futtatható program látható, amely összekapcsolja az összes lépést. Másold be egy `SandboxDemo.java` fájlba, add hozzá az Aspose.HTML függőséget, és futtasd a `java SandboxDemo` parancsot.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.rendering.image.ImageSaveOptions;
import com.aspose.html.rendering.image.SaveFormat;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Configure sandbox – set device pixel ratio, screen size, and user agent
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS width (iPhone)
        sandboxOptions.setScreenHeight(667);         // CSS height
        sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
        sandboxOptions.setUserAgent(
                "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                "Version/14.0 Mobile/15E148 Safari/604.1");   // <-- set custom user agent

        // 2️⃣ Create sandbox instance
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // 3️⃣ Load the target page inside the sandboxed environment
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com/responsive.html", mobileSandbox);

        // 4️⃣ Retrieve and print the page title (get page title java)
        System.out.println("Title: " + htmlDoc.getTitle());

        // 5️⃣ Render the page – convert html to png and save html as image
        // Simple save (auto‑detect PNG)
        htmlDoc.save("mobile_view.png");   // <-- save html as image

        // 6️⃣ Optional: custom size rendering
        ImageSaveOptions opts = new ImageSaveOptions(SaveFormat.PNG);
        opts.setWidth(750);   // 375 * DPR 2
        opts.setHeight(1334);
        htmlDoc.save("mobile_view_custom.png", opts); // another convert html to png example
    }
}
```

A program futtatása két PNG fájlt hoz létre:

| File | Description |
|------|-------------|
| `mobile_view.png` | Alapértelmezett renderelés a beállított DPR-rel. |
| `mobile_view_custom.png` | Renderelés explicit szélességgel/magassággal (hasznos fix‑méretű eszközökhöz). |

Bármelyik fájlt megnyithatod egy képnézegetőben, hogy ellenőrizd a nagy felbontású kimenetet.

## Gyakori kérdések és speciális esetek

| Kérdés | Válasz |
|----------|--------|
| **Mi van, ha az oldal JavaScript-et tartalmaz, amely a betöltés után módosítja a DOM-ot?** | Az Aspose.HTML alapértelmezés szerint végrehajtja a szkripteket. Ha a szkript végrehajtása előtt statikus pillanatképet szeretnél, állítsd be a `sandboxOptions.setEnableJavaScript(false)`-t. |
| **Renderelhetek olyan oldalt, amely hitelesítést igényel?** | Igen. Használd a `sandboxOptions.setCredentials(new NetworkCredential("user","pass"))`-t vagy injektáld a cookie-kat a `sandboxOptions.getCookies().add(...)` segítségével. |
| **A DPR korlátozva van 2.0-ra?** | Nem. Bármely pozitív double értéket beállíthatsz (pl. 3.0 ultra‑magas DPI‑es eszközökhöz). Ne feledd, hogy a nagyobb DPR nagyobb képfájlokat eredményez. |
| **Hogyan kezeljem a nagy eszközöket (képek, betűtípusok) tartalmazó oldalakat?** | Növeld a sandbox memória limitjét a `sandboxOptions.setMemoryLimit(512 * 1024 * 1024)` (bájt) beállítással. Ez megakadályozza a memóriahiányos hibákat a nehéz oldalakon. |
| **Kell-e manuálisan bezárni a sandboxot?** | A `Sandbox` implementálja az `AutoCloseable` interfészt. Tedd try‑with‑resources blokkba a automatikus takarításért. |

## Összegzés

Bemutattuk, hogyan **állítsd be az eszköz pixelarányt** egy Java sandboxban, **állíts be egyedi felhasználói ügynököt**, **kapd meg a oldal címét Java-ban**, és **konvertáld a html-t png-re** (vagyis **html-t képként mentés**), az Aspose.HTML segítségével. A teljes példa egy gyakorlati munkafolyamatot mutat be, amelyet automatizált képernyőkép-generáláshoz, vizuális regressziós teszteléshez vagy bármely olyan helyzethez adaptálhatsz, ahol egy pixel‑tökéletes weboldal-reprezentációra van szükség.

Nyugodtan kísérletezz—állítsd a DPR-t 3.0-ra, cseréld le a felhasználói ügynököt egy Android karakterláncra, vagy irányítsd az URL-t egy helyi HTML fájlra. Ugyanez a minta működik PDF-ekkel, SVG-kkel vagy akár többoldalas rendereléssel is.

Ha hasznosnak találtad ezt az útmutatót, érdemes megtekinteni a kapcsolódó témákat, például **PDF generálás Aspose.HTML‑del**, **headless Chrome alternatívák**, vagy **több URL kötegelt renderelése**. Boldog kódolást, és legyenek a képernyőképeid mindig élesek!

![set device pixel ratio in Java sandbox](image.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}