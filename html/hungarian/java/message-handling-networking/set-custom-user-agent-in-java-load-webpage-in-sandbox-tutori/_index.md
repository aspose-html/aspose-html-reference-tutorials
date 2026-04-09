---
category: general
date: 2026-04-09
description: Állíts be egyedi felhasználói ügynököt Java-ban, hogy weboldalt tölts
  be sandbox környezetben. Tanulj lépésről lépésre, hogyan állítsd be a felhasználói
  ügynököt Java-ban, és hogyan emulálj mobil eszközöket.
draft: false
keywords:
- set custom user agent
- set user agent java
- load webpage in sandbox
- Aspose HTML sandbox
- Java web automation
language: hu
og_description: Állíts be egyedi felhasználói ügynököt Java-ban a weboldal sandboxban
  történő betöltéséhez. Kövesd ezt az útmutatót a Java felhasználói ügynök beállításához,
  eszközök emulálásához és az oldal adatainak kinyeréséhez.
og_title: Egyéni felhasználói ügynök beállítása Java-ban – Teljes Sandbox útmutató
tags:
- Aspose.HTML
- Java
- Web Scraping
title: Egyéni felhasználói ügynök beállítása Java-ban – Weboldal betöltése sandbox
  környezetben.
url: /hu/java/message-handling-networking/set-custom-user-agent-in-java-load-webpage-in-sandbox-tutori/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Egyedi felhasználói ügynök beállítása Java-ban – Weboldal betöltése sandboxban

Valaha szükséged volt **egyedi felhasználói ügynök beállítására Java-ban**, de nem tudtad, hogyan tudod a céloldalt azt hinni, hogy mobil böngésző vagy? Nem vagy egyedül. Sok oldal más HTML-t szolgáltat, vagy akár blokkolja a kéréseket, ha az *User‑Agent* fejléc nem ismerős. A jó hír? Az Aspose.HTML segítségével **egyedi felhasználói ügynököt állíthatsz be** egy sandboxon belül, betöltheted az oldalt, és a DOM-mal úgy dolgozhatsz, mintha egy valódi eszköz renderelte volna.

Ebben az útmutatóban végigvezetünk egy teljes, futtatható példán, amely megmutatja, hogyan **állíts be felhasználói ügynököt Java-ban**, konfigurálj egy sandboxot iPhone emulálásához, majd **betölts egy weboldalt sandboxban**. A végére egy önálló programod lesz, amelyet bármely Java projektbe beilleszthetsz, és azonnal elkezdhetsz adatgyűjtést vagy tesztelést.

## Amire szükséged lesz

- Java 17 vagy újabb (a kód a modern modulrendszert használja, de régebbi JDK-k kisebb módosításokkal is működnek)  
- Aspose.HTML for Java (a cikk írásakor elérhető legújabb verzió, 23.10)  
- Egyszerű IDE vagy szövegszerkesztő; a Maven/Gradle nem szükséges a kódrészlethez, de a JAR‑nak a classpath‑on kell lennie  
- Internetkapcsolat a példában szereplő URL‑hez (`https://example.com`)

Ennyi—nincsenek extra szerverek, nincs headless böngésző, csak néhány sor tiszta Java.

![Egyedi felhasználói ügynök beállítása példa](https://example.com/image.png "egyedi felhasználói ügynök beállítása Java sandboxban")

## 1. lépés: A sandbox konfigurálása – a hely, ahol **egyedi felhasználói ügynököt állítasz be**

A sandbox egy könnyű, izolált környezet, amely egy böngészőt utánz. Először létrehozunk egy `SandboxOptions` objektumot, és megadjuk neki, milyen képernyőméretet és *User‑Agent* karakterláncot szeretnénk.

```java
import com.aspose.html.sandbox.SandboxOptions;

// Step 1 – define sandbox options
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);               // iPhone width in CSS pixels
sandboxOptions.setScreenHeight(667);              // iPhone height
sandboxOptions.setUserAgent(
        "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
        "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.0 Mobile/15E148 Safari/604.1");
```

**Miért fontos:** A `setUserAgent` hívás az a hely, ahol **egyedi felhasználói ügynököt állítasz be**. Ha egy valódi eszköz karakterláncát használod, meggyőzöd a szervert, hogy a mobil elrendezést szolgáltassa, ami gyakran egyszerűbb markup-ot tartalmaz—hasznos adatgyűjtéshez vagy UI teszteléshez.

## 2. lépés: A sandbox példány elindítása

Miután a beállítások készen állnak, átadjuk őket a `HtmlDocumentSandbox`-nek. Ez az objektum érvényesíti a beállításokat minden számára, ami benne fut.

```java
import com.aspose.html.sandbox.HtmlDocumentSandbox;

// Step 2 – create the sandbox with our options
HtmlDocumentSandbox sandbox = new HtmlDocumentSandbox(sandboxOptions);
```

**Pro tipp:** Ugyanazt a sandboxot újra felhasználhatod több oldal betöltéséhez, ami memóriát takarít meg a minden alkalommal új böngésző indításához képest.

## 3. lépés: Oldal betöltése, miközben **felhasználói ügynököt állítasz be Java-ban** a háttérben

A sandbox aktív állapotában egy oldal betöltése olyan egyszerű, mint egy `HTMLDocument` példányosítása. A konstruktor megkapja az URL-t és a most létrehozott sandboxot.

```java
import com.aspose.html.HTMLDocument;

// Step 3 – load the target page inside the sandbox
HTMLDocument htmlDoc = new HTMLDocument("https://example.com", sandbox);
```

Ekkor a kérés már magában hordozza az egyedi *User‑Agent* fejlécet. Ha megvizsgálod a hálózati forgalmat (pl. Wiresharkkal vagy egy proxyval), látni fogod a korábban definiált pontos karakterláncot.

## 4. lépés: Ellenőrizd, hogy az oldal helyesen betöltődött‑‑ a **weboldal betöltése sandboxban** eredménye

Húzzuk ki a címét a dokumentumból, hogy bizonyítsuk, minden működik. Ez azt is bemutatja, hogyan léphetsz interakcióba a DOM-mal az oldal renderelése után.

```java
// Step 4 – read the title to confirm we loaded the page
System.out.println("Title (in sandbox): " + htmlDoc.getTitle());
```

**Várható kimenet (eltérhet):**

```
Title (in sandbox): Example Domain
```

Ha a cím megjelenik, a **weboldal betöltése sandboxban** sikeres volt, és az egyedi felhasználói ügynök alkalmazásra került.

## Teljes, futtatható példa

Az összes rész összeállításával egyetlen osztályt kapsz, amelyet lefordíthatsz és futtathatsz:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.HtmlDocumentSandbox;
import com.aspose.html.sandbox.SandboxOptions;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Configure the sandbox to emulate a mobile device
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);   // iPhone width in CSS pixels
        sandboxOptions.setScreenHeight(667);
        sandboxOptions.setUserAgent(
                "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 2: Create a sandbox instance with the configured options
        HtmlDocumentSandbox sandbox = new HtmlDocumentSandbox(sandboxOptions);

        // Step 3: Load the web page inside the sandboxed environment
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com", sandbox);

        // Step 4: Work with the document as if it were rendered on the simulated device
        System.out.println("Title (in sandbox): " + htmlDoc.getTitle());
    }
}
```

Fordítás:

```bash
javac -cp "path/to/aspose-html.jar" SandboxExample.java
java -cp ".:path/to/aspose-html.jar" SandboxExample
```

Cseréld le a `path/to/aspose-html.jar`‑t a tényleges Aspose.HTML JAR fájl helyére.

## Gyakori variációk és szélhelyzetek

### Másik eszközprofil használata

Ha **egyedi felhasználói ügynököt kell beállítanod** egy Android táblagéphez, csak módosítsd a képernyőméreteket és a user‑agent karakterláncot:

```java
sandboxOptions.setScreenWidth(800);
sandboxOptions.setScreenHeight(1280);
sandboxOptions.setUserAgent(
        "Mozilla/5.0 (Linux; Android 12; SM-G991U) " +
        "AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.5249.91 Mobile Safari/537.36");
```

### Átirányítások kezelése

Az Aspose.HTML automatikusan követi az átirányításokat, de a *User‑Agent* fejléc csak akkor marad meg, ha ugyanabban a sandboxban maradsz. Ha minden átirányításhoz új `HTMLDocument`‑et hozol létre, ne felejtsd el átadni ugyanazt a `sandbox` példányt.

### HTTPS oldalak betöltése önaláírt tanúsítványokkal

Belső tesztelés során előfordulhat, hogy egy önaláírt tanúsítvánnyal rendelkező oldalra ütközöl. A tanúsítvány ellenőrzését lazíthatod a `SandboxOptions` módosításával:

```java
sandboxOptions.setIgnoreCertificateErrors(true);
```

Ezt csak megbízható környezetben használd; egyébként gyengíti a biztonságot.

## Tippek és buktatók

- **Pro tipp:** Tartsd a sandboxot élő állapotban kötegelt feladatokhoz. Kérésenkénti létrehozása és megsemmisítése többletterhet jelent.
- **Figyelj:** Egyes oldalak további fejléceket vizsgálnak (pl. `Accept-Language`). Ha még mindig blokkolnak, add hozzá ezeket a fejléceket a `sandboxOptions.getHeaders().add("Accept-Language", "en-US")` segítségével.
- **Teljesítményjegyzet:** A sandbox a folyamaton belül fut, így a memóriahasználat mérsékelt a Seleniumhoz hasonló teljes böngészőkhöz képest. Azonban nagyon nagy oldalak még mindig jelentős RAM-ot fogyaszthatnak—figyeld ezt, ha több tucat oldalt szeretnél egyszerre betölteni.

## Következtetés

Most már tudod, hogyan **állíts be egyedi felhasználói ügynököt Java-ban**, konfigurálj egy sandboxot, és **tölts be egy weboldalt sandboxban** az Aspose.HTML segítségével. A fenti teljes kód bemutatja az egész folyamatot – a `SandboxOptions` definiálásától a oldal címének kiírásáig – így azonnal másolhatod, beillesztheted és futtathatod.

Ezután gondold meg a példa kibővítését specifikus elemek kinyerésére (`htmlDoc.getElementById(...)`), képernyőképek készítésére (`sandbox.getScreenCapture()`), vagy több URL láncolására egy feltérképező feladathoz. Mindezek a feladatok ugyanabból a **felhasználói ügynök beállítása Java-ban** technikából profitálnak, amelyet most elsajátítottál.

Nyugodtan kísérletezz különböző eszközkarakterláncokkal, képernyőméretekkel vagy akár egyedi fejlécekkel. Minél többet játszol velük, annál jobban megérted, hogyan reagálnak a szerverek a különböző ügynökökre – ez egy kulcsfontosságú képesség a webes automatizálás, tesztelés és adatkinyerés terén.

Boldog kódolást, és legyenek a kéréseid mindig szívesen fogadva!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}