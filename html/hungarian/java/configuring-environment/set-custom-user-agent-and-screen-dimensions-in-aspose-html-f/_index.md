---
category: general
date: 2026-09-29
description: Állíts be egyedi felhasználói ügynököt az Aspose.HTML for Java-ban, és
  tanuld meg, hogyan állítható be a virtuális képernyőméret a pontos HTML rendereléshez.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom user agent
- set virtual screen size
- specify user agent
- set screen dimensions
- set screen width
language: hu
lastmod: 2026-09-29
og_description: Állíts be egyedi felhasználói ügynököt az Aspose.HTML for Java-ban,
  és tanuld meg, hogyan állíts be virtuális képernyőméretet a pontos HTML rendereléshez.
og_image_alt: Diagram showing how to set custom user agent and screen dimensions in
  a Java sandbox
og_title: Egyéni felhasználói ügynök és képernyőméretek beállítása az Aspose.HTML
  for Java-ban
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Set custom user agent in Aspose.HTML for Java and learn how to set
    virtual screen size for accurate HTML rendering.
  headline: Set custom user agent and screen dimensions in Aspose.HTML for Java
  type: TechArticle
tags:
- Aspose.HTML
- Java
- sandbox
- user agent
- screen size
title: Egyéni felhasználói ügynök és képernyőméretek beállítása az Aspose.HTML for
  Java-ban
url: /hu/java/configuring-environment/set-custom-user-agent-and-screen-dimensions-in-aspose-html-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Egyedi felhasználói ügynök és képernyőméretek beállítása az Aspose.HTML for Java-ban

Ha **egyedi felhasználói ügynököt** kell beállítania HTML renderelésekor az Aspose.HTML for Java-val, ez az útmutató pontosan megmutatja, hogyan teheti ezt. A sandbox konfigurálásával lehetősége van **virtuális képernyőméret beállítására** is, biztosítva, hogy a layout egy valódi böngésző nézetablakhoz igazodjon.

A tutorial végére egy teljes, futtatható programot kap, amely **megadja a felhasználói ügynököt**, **beállítja a képernyő szélességét**, és **beállítja a képernyő magasságát**. Külső eszközök nem szükségesek – csak az Aspose.HTML for Java és egy Java 8+ futtatókörnyezet.

## Amit megtanul

* Hogyan hozzon létre egy `SandboxConfiguration`-t a renderelés izolálásához.
* Hogyan **állítson be egyedi felhasználói ügynököt**, és miért fontos ez a reszponzív oldalaknál.
* Hogyan **állítson be virtuális képernyőméretet** (képernyő szélesség és magasság) a pontos elrendezéshez.
* Hogyan töltsön be egy HTML fájlt a sandboxba, és mentse el a feldolgozott eredményt.
* Gyakori buktatók és legjobb gyakorlatok a sandboxolt rendereléshez.

> **Előfeltételek** – Szüksége van egy érvényes Aspose.HTML for Java licencre, Java 8 vagy újabb verzióra, valamint egy IDE-re (IntelliJ IDEA, Eclipse vagy VS Code). A példa egy helyi `input.html` fájlt használ, de bármely elérhető URL működik.

![Sandbox flow diagram](sandbox-flow.png "egyedi felhasználói ügynök beállítása példa Java-ban")

## 1. lépés: Sandbox konfiguráció létrehozása (az alap)

A sandbox elkülöníti a renderelési környezetet a host JVM-től, ami elengedhetetlen, ha **egyedi felhasználói ügynököt** szeretne **beállítani** vagy megváltoztatni a nézetablak méretét.

```java
import com.aspose.html.sandbox.SandboxConfiguration;

// Create a fresh sandbox configuration object
SandboxConfiguration sandboxConfig = new SandboxConfiguration();
```

*Miért ez a lépés?*  
`SandboxConfiguration` tartalmazza az összes renderelési beállítást, beleértve a **képernyőméreteket** és a **felhasználói‑ügynök** karakterláncokat. Ha a dokumentum betöltése előtt konfigurálja, garantálja, hogy a HTML motor ezeket a beállításokat már az első kérésnél figyelembe veszi.

## 2. lépés: Képernyőméretek beállítása a valós eszköz utánzása érdekében

A reszponzív oldalak gyakran a `window.innerWidth` és `window.innerHeight` értékeket olvassák. Ahhoz, hogy a motor úgy gondolja, egy 1024 × 768 képernyőn fut, **virtuális képernyőméretet** állít be:

```java
// Define the virtual screen size for the sandboxed document
sandboxConfig.setScreenWidth(1024);   // set screen width
sandboxConfig.setScreenHeight(768);   // set screen height
```

*Miért fontos* – Ha kihagyja a **képernyőméretek beállítását**, a renderelő egy nagyon kicsi nézetablakra válthat, ami miatt a CSS media query‑k a mobil elrendezést választják. A **képernyő szélességének** és **képernyő magasságának** kifejezett beállításával szabályozhatja, mely CSS szabályok lépnek életbe.

## 3. lépés: Egyedi felhasználói‑ügynök karakterlánc megadása

Néhány weboldal a felhasználói‑ügynök fejléc alapján különböző tartalmat szolgáltat. A **felhasználói ügynök megadásához** egyszerűen állítsa be a sandbox konfigurációban:

```java
// Set a custom user‑agent string that will be sent during resource loading
sandboxConfig.setUserAgent("AsposeHTML/1.0");
```

*Miért használjunk egyedi felhasználói ügynököt?*  
Egy egyedi karakterlánc megkerülheti a botdetektálást, aktiválhatja csak asztali környezetben elérhető funkciókat, vagy tesztelheti, hogyan viselkedik egy oldal egy adott böngésző verzióval. Az Aspose motor ezt az értéket minden, a külső erőforrások (CSS, képek, szkriptek) betöltésekor küldött HTTP kéréshez továbbítja.

## 4. lépés: HTML dokumentum betöltése a sandboxban

Miután a sandbox teljesen konfigurálva van, töltsük be a HTML fájlt. Az a konstruktor, amely fájlútvonalat és egy `SandboxConfiguration`‑t kap, automatikusan alkalmazza a korábban definiált beállításokat.

```java
import com.aspose.html.HTMLDocument;

// Load the HTML file using the previously configured sandbox
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);
```

Ha távoli URL‑ről szeretne betölteni, cserélje le a fájlútvonalat az URL karakterláncra – az Aspose.HTML továbbra is tiszteletben tartja a **egyedi felhasználói ügynök** és a **képernyőméretek** beállításait.

## 5. lépés: A feldolgozott kimenet mentése

Miután a dokumentum befejezte a betöltést, bármely támogatott formátumban menthet. Itt egy sandboxolt HTML fájlt írunk, amely tükrözi a saját beállításaink által okozott DOM‑változásokat.

```java
// Save the processed document to the desired output location
document.save("YOUR_DIRECTORY/sandboxed_output.html");
```

A mentett fájl ugyanazt a markup‑ot tartalmazza, de minden olyan szkript, amely a `navigator.userAgent`‑et vagy a `window.innerWidth`‑et kérdezi le, most a megadott értékeket fogja látni.

## Teljes, futtatható példa

Az összes lépés egyesítése egy önálló programot eredményez, amelyet egyszerűen másolhat, beilleszthet és futtathat.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.SandboxConfiguration;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox configuration to isolate the rendering environment
        SandboxConfiguration sandboxConfig = new SandboxConfiguration();

        // Step 2: Define the virtual screen size for the sandboxed document
        sandboxConfig.setScreenWidth(1024);   // set screen width
        sandboxConfig.setScreenHeight(768);   // set screen height

        // Step 3: Set a custom user‑agent string to be used during loading
        sandboxConfig.setUserAgent("AsposeHTML/1.0"); // set custom user agent

        // Step 4: Load the HTML document within the sandbox using the configuration
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);

        // Step 5: Save the processed document to the desired output location
        document.save("YOUR_DIRECTORY/sandboxed_output.html");
    }
}
```

### Várható kimenet

A program futtatása `sandboxed_output.html` fájlt hoz létre. Ha megnyitja egy böngészőben és a konzolon lekéri a `navigator.userAgent`‑et, **AsposeHTML/1.0**-t fog látni. Hasonlóképpen a `window.innerWidth` **1024**‑et jelez, ami megerősíti, hogy a **képernyőméretek beállítása** a várt módon működött.

## Gyakori kérdések és szél‑eset kezelése

| Kérdés | Válasz |
|----------|--------|
| **Mi van, ha az oldal további erőforrásokat tölt be egy másik domainről?** | A sandbox minden kérésnél továbbítja a **egyedi felhasználói ügynököt**, de a cross‑origin szabályok továbbra is érvényesek. Ha lazítani szeretné ezeket a korlátozásokat, használja a `sandboxConfig.setAllowCrossDomain(true)` beállítást. |
| **Megváltoztathatom a képernyőméretet a dokumentum betöltése után?** | Nem. A képernyőméreteket az első elrendezési lépés során olvassa be a motor. Más mérettel való rendereléshez hozzon létre egy új `SandboxConfiguration`‑t, és töltse újra a dokumentumot. |
| **Kell-e meghívni a `document.close()`‑t?** | A `HTMLDocument` implementálja az `AutoCloseable` interfészt. A try‑with‑resources blokk használata biztosítja a megfelelő takarítást, de egyszerű szkriptekben az explicit `close()` opcionális. |
| **Miben különbözik ez az HTTP‑kliensben történő felhasználói‑ügynök beállításától?** | A sandboxon beállított felhasználói‑ügynök **minden** erőforráskérésre hat, amit a HTML motor indít, nem csak az első HTML letöltésre. Így sokkal inkább egy valódi böngésző viselkedését utánozza. |
| **Biztonságos-e a sandbox megbízhatatlan HTML‑hez?** | Igen. A sandbox izolálja a fájlrendszer hozzáférését és a hálózati hívásokat a konfiguráció szerint, csökkentve a rosszindulatú szkriptek által a host JVM-re gyakorolt kockázatot. |

## Profi tippek

* **Konfigurációk újrahasználata** – Ha sok oldalt renderel ugyanazzal a nézetablakkal, hozzon létre egyetlen `SandboxConfiguration`‑t, és használja újra, hogy elkerülje az objektum‑létrehozási többletterhet.
* **Hibakeresés naplózással** – Engedélyezze az Aspose.HTML naplózást (`sandboxConfig.setLogLevel(LogLevel.DEBUG)`) a megtekintett erőforrások és a használt egyedi felhasználói‑ügynök nyomon követéséhez.
* **Kombinálja CSS media query‑kkel** – A **képernyő szélességének** módosításával tesztelheti, hogyan viselkedik a reszponzív dizájn táblagépeken, telefonokon vagy nagy asztali monitorokon anélkül, hogy valódi böngészőt nyitna.

## Következtetés

Most már tudja, hogyan **állítson be egyedi felhasználói ügynököt** és **képernyőméreteket**, amikor HTML‑t renderel az Aspose.HTML for Java‑val. A sandbox konfigurálásával izolálja a környezetet, szabályozza a nézetablakot, és biztosítja, hogy a külső erőforrások pontosan az Ön által megadott fejléceket kapják. Ez a technika elengedhetetlen a reszponzív elrendezések teszteléséhez, a botblokkok megkerüléséhez vagy asztali‑specifikus funkciók automatizált pipeline‑okban történő reprodukálásához.

A következő lépésként érdemes megismerni **hogyan állítsunk be egyedi cookie‑kat** vagy **hogyan rögzítsünk renderelt képernyőképeket** az Aspose.HTML renderelési API‑jával – mindkettő ugyanazon sandbox konfigurációs mintára épül, amelyet most elsajátított.

Boldog kódolást!

## Mit érdemes még megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket és lépésről‑lépésre magyarázatokat tartalmaz, hogy további API‑funkciókat saját projektjeiben is könnyedén alkalmazhasson.

- [Nagy DPI renderelés Java-ban – Weboldalak képernyőképeinek rögzítése egyedi felhasználói ügynökkel](/html/english/java/conversion-html-to-various-image-formats/high-dpi-rendering-in-java-capture-webpage-screenshots-with/)
- [Hogyan töltsünk be HTML-t, állítsunk be eszköz DPI-t és olvassuk ki a háttérszínt](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [HTML fájl létrehozása Java-ban és hálózati szolgáltatás beállítása (Aspose.HTML)](/html/english/java/configuring-environment/setup-network-service/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}