---
category: general
date: 2026-06-19
description: Oldalcím kinyerése Java-ban egy weboldal offline betöltésével, a képernyőméretek
  beállításával és a külső erőforrások letiltásával. Tanulja meg lépésről lépésre
  a HTML-dokumentum URL betöltését.
draft: false
keywords:
- extract page title
- set screen dimensions
- load webpage offline
- disable external resources
- load html document url
language: hu
og_description: Gyorsan kinyerni az oldal címét Java-ban. Ez az útmutató bemutatja,
  hogyan töltsünk be egy weboldalt offline módon, állítsuk be a képernyő méreteit,
  és tiltsuk le a külső erőforrásokat a megbízható HTML feldolgozáshoz.
og_title: Oldalcím kinyerése Java-ban – Teljes Aspose.HTML útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Extract page title in Java by loading a webpage offline, setting screen
    dimensions, and disabling external resources. Learn to load HTML document URL
    step‑by‑step.
  headline: Extract Page Title with Java – Full Guide Using Aspose.HTML
  type: TechArticle
- description: Extract page title in Java by loading a webpage offline, setting screen
    dimensions, and disabling external resources. Learn to load HTML document URL
    step‑by‑step.
  name: Extract Page Title with Java – Full Guide Using Aspose.HTML
  steps:
  - name: What if the page redirects?
    text: Aspose.HTML follows HTTP redirects by default. The final destination’s title
      will be returned. If you need to capture intermediate titles, you’d have to
      handle the `HttpResponse` manually—something rarely required for simple title
      extraction.
  - name: How do I handle non‑HTML responses (e.g., PDFs)?
    text: The `HTMLDocument.load` method throws an exception if the content type isn’t
      HTML. Wrap the call in a `try/catch` and inspect the `Content-Type` header if
      you need a fallback strategy.
  - name: Can I extract other meta tags at the same time?
    text: 'Absolutely. Once you have the `HTMLDocument` instance, you can query the
      DOM:'
  - name: Does the sandbox support JavaScript execution?
    text: Yes, but only if you enable it. By default, the sandbox runs in a “safe
      mode” where scripts are ignored. If you ever need to evaluate inline scripts
      for title generation (rare, but possible with SPA frameworks), set `setAllowExternalResources(true)`
      and optionally enable `setEnableJavaScript(true)`.
  type: HowTo
tags:
- Java
- Aspose.HTML
- Web Scraping
title: Oldalcím kinyerése Java-val – Teljes útmutató az Aspose.HTML használatához
url: /hu/java/creating-managing-html-documents/extract-page-title-with-java-full-guide-using-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Oldal címének kinyerése Java-val – Teljes útmutató az Aspose.HTML használatával

Valaha szükséged volt **oldal címének kinyerésére** egy távoli webhelyről, de nem akartad, hogy az alkalmazásod letöltse az összes felesleges CSS fájlt, szkriptet vagy képet? Nem vagy egyedül. Sok automatizálási helyzetben – gondolj SEO auditokra vagy tartalomfigyelésre – csak a lap metaadataira vagyunk kíváncsiak, nem a teljes vizuális megjelenítésre.  

Ez a bemutató pontosan megmutatja, hogyan **kinyerheted az oldal címét** az Aspose.HTML for Java segítségével, miközben **offline töltöd be a weboldalt**, **beállítod a képernyő méretét**, és **letiltod a külső erőforrásokat**. A végére egy kompakt, production‑ready kódrészletet kapsz, amely bármely **HTML dokumentum URL‑t** egy sandbox környezetben betölti, és a címét a konzolra írja.

## Mit fogsz megtanulni

- Hogyan konfigurálj egy Aspose.HTML sandbox‑ot a **képernyő méretének beállítására**, amely egy asztali böngészőt utánz.
- Hogyan tiltsd le a hálózati hívásokat CSS, JavaScript és képek esetén, hogy a betöltés **offline** történjen.
- Hogyan használd a `HTMLDocument.load`‑t **HTML dokumentum URL betöltésére**, és hogyan olvasd ki a `<title>` elemet.
- Hogyan kezeld az erőforrásokat biztonságosan a try‑with‑resources segítségével, elkerülve a memória szivárgásokat.  

Nem szükséges semmilyen külső könyvtár az Aspose.HTML‑en kívül, a kód Java 8+ és bármely modern JDK alatt működik.

---

## Előfeltételek

Mielőtt belevágnánk, győződj meg róla, hogy a következők telepítve vannak:

1. **Java Development Kit (JDK) 8 vagy újabb**.  
2. **Aspose.HTML for Java** (a legújabb verzió 2026. június állapotában). Maven Central‑ról szerezhető be:

   ```xml
   <dependency>
       <groupId>com.aspose</groupId>
       <artifactId>aspose-html</artifactId>
       <version>23.9</version>
   </dependency>
   ```

3. **Alap IDE** (IntelliJ IDEA, Eclipse vagy VS Code) vagy egy egyszerű szövegszerkesztő és parancssor.  

Ennyi – nincs extra beállítás, nincs headless böngésző, csak az Aspose.HTML végzi a nehéz munkát.

---

## 1. lépés: Sandbox létrehozása és **képernyő méretének beállítása**

Az első dolog, amit a mintakódban látsz, a sandbox konfigurációja. A sandbox egy könnyű, in‑process böngésző‑emulátor. Alapértelmezés szerint egy kis mobil eszközként viselkedik, ami torzíthatja a kapott DOM‑ot. Ahhoz, hogy az oldal úgy viselkedjen, mintha egy tipikus asztali gépen néznénk, **be kell állítanod a képernyő méretét**.

```java
// Initialize load options
HtmlLoadOptions loadOptions = new HtmlLoadOptions();

// Emulate a 1024×768 screen – this is a common desktop resolution
loadOptions.getSandbox()
           .setScreenWidth(1024)   // set screen width
           .setScreenHeight(768); // set screen height
```

> **Miért fontos?** Sok modern oldal a viewport mérete alapján különböző HTML fragmentumokat szolgál ki. Ha 1024 px szélességet kényszerítesz, biztos lehetsz benne, hogy a kapott markup tartalmazza a teljes `<title>` elemet, akárcsak egy normál böngésző.

---

## 2. lépés: **Külső erőforrások letiltása** offline betöltéshez

Amikor csak az oldal címére van szükséged, minden külső stíluslap, szkript vagy kép betöltése pazarló. Emellett lelassítja az alkalmazást, és váratlan mellékhatásokat okozhat (például JavaScript, amely harmadik fél API‑hoz próbál csatlakozni). Az Aspose.HTML egyetlen sorral **letiltja a külső erőforrásokat**:

```java
// Prevent the sandbox from fetching CSS, JS, images, etc.
loadOptions.getSandbox().setAllowExternalResources(false);
```

> **Tipp:** Ha később rájössz, hogy a cím helyes kinyeréséhez inline CSS‑re van szükség (ritka, de előfordulhat), egyszerűen állítsd vissza ezt a flag-et `true`‑ra.

---

## 3. lépés: **HTML dokumentum URL betöltése** a sandbox‑ban

Most, hogy a sandbox elő van készítve, biztonságosan **betöltheted a HTML dokumentum URL‑t**, anélkül, hogy extra hálózati forgalomra kellene számítanod. A `HTMLDocument.load` metódus elfogadja a cél URL‑t és a korábban épített opciókat.

```java
String url = "https://example.com"; // replace with the page you want to inspect

try (HTMLDocument doc = HTMLDocument.load(url, loadOptions)) {
    // Extract the title once the document is fully parsed
    String title = doc.getTitle();
    System.out.println("Title: " + title);
}
```

A `try‑with‑resources` blokk garantálja, hogy a dokumentum megfelelően el legyen dobva, elkerülve a memória szivárgásokat – különösen fontos, ha sok oldalt dolgozol fel egy kötegelt feladatban.

> **Ami megjelenik:** A konzol például `Title: Example Domain`‑et ír ki. Ez a **oldal címének kinyerése** eredménye, amit kerestél.

---

## 4. lépés: Teljes, futtatható példa

Az alábbiakban a teljes program látható, amelyet egyszerűen másolj be egy `LoadWithSandbox.java` fájlba. Minden rész – sandbox beállítás, képernyő mérete, erőforrás letiltás és cím kinyerés – egy helyen van.

```java
import com.aspose.html.*;
import com.aspose.html.load.*;

public class LoadWithSandbox {
    public static void main(String[] args) throws Exception {
        // Step 1: Specify the URL of the page to load
        String url = "https://example.com";

        // Step 2: Create load options and configure a sandbox that mimics a desktop browser
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        loadOptions.getSandbox()
                   .setScreenWidth(1024)                     // emulate 1024‑pixel wide screen
                   .setScreenHeight(768)                     // emulate 768‑pixel tall screen
                   .setUserAgent("Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36");

        // Step 3: Disable external network resources (CSS, JS, images) for offline processing
        loadOptions.getSandbox().setAllowExternalResources(false);

        // Step 4: Load the HTML document using the configured sandbox and display its title
        try (HTMLDocument doc = HTMLDocument.load(url, loadOptions)) {
            System.out.println("Title: " + doc.getTitle());
        }
    }
}
```

**Várható kimenet** (ha a `https://example.com`‑ra futtatod):

```
Title: Example Domain
```

Ha a `url` változót bármely más oldalra állítod, a program továbbra is **gyorsan kinyeri az oldal címét**, mivel a nehéz assetek le vannak tiltva.

---

## 5. lépés: Gyakori kérdések és széljegyek

### Mi van, ha az oldal átirányít?

Az Aspose.HTML alapértelmezés szerint követi a HTTP átirányításokat. A végső céloldal címe lesz visszaadva. Ha a közbenső címeket is le kell kérned, manuálisan kell kezelni a `HttpResponse`‑t – ez ritkán szükséges egyszerű címkinyerés esetén.

### Hogyan kezelem a nem‑HTML válaszokat (pl. PDF‑ek)?

A `HTMLDocument.load` metódus kivételt dob, ha a tartalom típusa nem HTML. Tedd a hívást egy `try/catch`‑be, és ellenőrizd a `Content-Type` fejlécet, ha fallback stratégiára van szükséged.

### Kinyerhetek más meta tageket is egyszerre?

Természetesen. Miután megvan a `HTMLDocument` példány, lekérdezheted a DOM‑ot:

```java
String description = doc.querySelector("meta[name='description']").getAttribute("content");
```

Csak ne feledd, hogy a **külső erőforrások letiltása** továbbra is legyen bekapcsolva, ha csak metaadatokra vagy kíváncsi; egyébként nagy assetek letöltésére is sor kerülhet.

### Támogatja a sandbox a JavaScript végrehajtását?

Igen, de csak akkor, ha engedélyezed. Alapértelmezés szerint a sandbox „biztonságos módban” fut, ahol a szkriptek figyelmen kívül maradnak. Ha valaha inline szkriptek alapján kell a címet generálni (ritka, de SPA kereteknél előfordulhat), állítsd be a `setAllowExternalResources(true)`‑t, és opcionálisan engedélyezd a `setEnableJavaScript(true)`‑t.

---

## Pro tippek és buktatók

- **Használd újra a `HtmlLoadOptions`‑t** sok URL feldolgozásakor. Új sandbox minden kérésnél felesleges overhead‑et jelent.  
- **Cache‑eld a user‑agent stringet**, ha ugyanarra a domainre gyakran kérsz; egyes oldalak a UA alapján különböző címeket szolgálnak ki.  
- **Figyelj a Cloudflare vagy bot‑detektálásra**. Még a külső erőforrások letiltása mellett is a szerver blokkolhatja a hiányos fejlécekkel érkező kéréseket. Egy reális user‑agent hozzáadása (ahogy fent látható) általában megoldja a problémát.

---

## Összegzés

Lépésről‑lépésre végigvettük, hogyan **nyerheted ki az oldal címét** bármely URL‑ről Java és Aspose.HTML segítségével. A **képernyő méretének beállításával**, a **külső erőforrások letiltásával**, és a HTML dokumentum sandbox‑ban történő betöltésével gyors, megbízható eredményt kapsz anélkül, hogy egy teljes böngésző motor felesleges súlya terhelné.  

Innen tovább bővítheted a megoldást – meta leírások, Open Graph tagek, vagy akár képernyőképek generálása is lehetséges, ha később engedélyezed a vizuális pipeline‑t. A fő minta változatlan: konfiguráld a sandbox‑ot, kapcsold ki a fölösleges funkciókat, töltsd be az URL‑t, és olvasd ki a DOM‑ot.

Készen állsz, hogy ezt egy nagyobb crawler‑be integráld? Adj hozzá egy szálkezelőt, tápláld URL‑listával, és tárold a címeket egy adatbázisban. A lehetőségek végtelenek.

*Boldog kódolást, és legyenek a címeid mindig pontosak!*

![Screenshot showing console output of extracting page title using Aspose.HTML sandbox](extract-page-title.png "Képernyőkép, amely a konzol kimenetét mutatja az Aspose.HTML sandbox használatával történő oldal címének kinyerése során")


## Mit érdemes még megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódnak ehhez a leíráshoz, és a bemutatott technikákra építenek. Minden forrás komplett, működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy könnyedén elsajátíthasd az API további funkcióit, vagy alternatív megvalósítási módokat saját projektjeidben.

- [HTML dokumentumok betöltése URL‑ről az Aspose.HTML for Java-ban](/html/english/java/creating-managing-html-documents/load-html-documents-from-url/)
- [Dokumentum betöltési események kezelése az Aspose.HTML for Java-ban](/html/english/java/creating-managing-html-documents/handle-document-load-events/)
- [Sandbox létrehozása HTML‑hez Java‑ban – Lépés‑ről‑lépés útmutató](/html/english/java/creating-managing-html-documents/create-sandbox-for-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}