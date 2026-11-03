---
category: general
date: 2026-04-19
description: Gyorsan kinyerhet HTML-t MHTML-ből Java használatával. Tanulja meg, hogyan
  konvertálja az MHTML-t HTML-re, hogyan nyerje ki az e‑mail törzset, hogyan írjon
  sztringet fájlba, és hogyan kezelje az MHT konverziót.
draft: false
keywords:
- extract html from mhtml
- convert mhtml to html
- extract email body
- write string to file
- convert mht to html
language: hu
og_description: HTML kinyerése MHTML-ből Java-ban. Ez az útmutató bemutatja, hogyan
  konvertáljuk az MHTML-t HTML-re, hogyan nyerjük ki az e-mail törzsét, és hogyan
  írjuk a karakterláncot fájlba.
og_title: HTML kinyerése MHTML‑ből – Java lépésről‑lépésre
tags:
- Java
- Aspose.HTML
- Email Processing
title: HTML kinyerése MHTML‑ből – Teljes Java útmutató
url: /hu/java/creating-managing-html-documents/extract-html-from-mhtml-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML kinyerése MHTML‑ből – Teljes Java útmutató

Szükséged volt már **HTML kinyerésére MHTML‑ből**, de nem tudtad, hol kezdjed? Lehet, hogy egy archivált e‑mailt (`.mht`) kaptál, és a tiszta törzset szeretnéd webes előnézethez, vagy egy migrációs szkriptet írsz, ami a régi archívumokat modern HTML oldalakká alakítja. Mindkét esetben ugyanaz a feladat: egy egyetlen fájlból álló webarchívumod van, és ki kell nyerned belőle a nyers HTML‑kódot.

A jó hír? Néhány Java sorral és az Aspose.HTML könyvtárral **át tudod konvertálni az MHTML‑t HTML‑re**, kinyerheted az e‑mail törzsét, és akár egy fájlba is írhatod a sztringet – mindezt anélkül, hogy elhagynád a fejlesztői környezetet. Ebben a tutorialban végigvezetünk a teljes folyamaton, elmagyarázzuk, miért fontos minden lépés, és megmutatjuk, hogyan kezeld a gyakori edge case‑eket, mint a hiányzó erőforrások vagy a nem‑UTF‑8 kódolású fájlok.

> **Gyors összefoglaló:** A végére el tudod **kinyerni az e‑mail törzsét**, **át tudod konvertálni az MHTML‑t HTML‑re**, és **sztringet tudsz fájlba írni** egy tiszta, újrahasználható kódrészlettel, amely bármely `.mht` vagy `.mhtml` fájlra működik.

---

## Amire szükséged lesz

Mielőtt belemerülnénk, győződj meg róla, hogy rendelkezel a következőkkel:

- **Java 17+** (a kód a try‑with‑resources mintát használja, amely Java 7‑től elérhető, de a Java 17 a jelenlegi LTS).
- **Aspose.HTML for Java** JAR‑ok a classpath‑odban. Letöltheted őket az [Aspose weboldaláról](https://products.aspose.com/html/java/) vagy Maven‑en keresztül:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

- Egy minta **`.mht` vagy `.mhtml`** fájl, amelyet feldolgozni szeretnél. A bemutatóhoz `email.mht`‑nek hívjuk, és helyezzük el a `YOUR_DIRECTORY`‑ben.

Ennyi – nincs extra keretrendszer, nincs nehéz parser. Csak tiszta Java és egy jól dokumentált könyvtár.

---

## 1. lépés – MHTML fájl megnyitása stream‑ként

Az első dolog, amit teszünk, hogy megnyitjuk az archivált e‑mailt `InputStream`‑ként. A stream használata alacsony memóriahasználatot biztosít, különösen nagy `.mht` fájlok esetén, amelyek beágyazott képeket vagy CSS‑t tartalmazhatnak.

```java
// Step 1: Open the MHTML file as a stream
try (InputStream mhtmlStream = new FileInputStream("YOUR_DIRECTORY/email.mht")) {
    // Subsequent steps go inside this block
}
```

**Miért stream?**  
A stream lehetővé teszi, hogy a `MhtmlDocument` adatot olvasson „on‑the‑fly”, ami azt jelenti, hogy nem kapod meg a `OutOfMemoryError`‑t még akkor sem, ha az archívum több megabájtnyi. Emellett később könnyen átállhatsz más forrásokra is (pl. `ByteArrayInputStream` adatbázisból).

---

## 2. lépés – MHTML dokumentum betöltése a stream‑ből

Most átadjuk a stream‑et az Aspose `MhtmlDocument` osztályának. Ez az osztály a MIME‑kódolt archívumot elemzi, és egy DOM‑szerű reprezentációt épít a beágyazott HTML‑ből.

```java
// Step 2: Load the MHTML document from the stream
MhtmlDocument mhtmlDoc = new MhtmlDocument(mhtmlStream);
```

**A háttérben:**  
Az Aspose kicsomagolja minden MIME részt (HTML, képek, CSS) és belsőleg újra összerakja őket. Ezért később egyszerűen kérheted csak a HTML‑részt, anélkül, hogy az beágyazott erőforrások miatt aggódnál.

---

## 3. lépés – A fő HTML tartalom lekérése

A dokumentum betöltése után a nyers HTML kinyerése egyetlen sorban megoldható. A `getHtmlContent()` metódus egy `String`‑et ad vissza, amely megőrzi az eredeti markup‑ot.

```java
// Step 3: Retrieve the main HTML content as a string
String htmlContent = mhtmlDoc.getHtmlContent();
```

**Ami visszakapod:**  
`htmlContent` a teljes HTML oldalt tartalmazza – beleértve a `<head>` és `<body>` tageket – pontosan úgy, ahogy az e‑mail mentésekor megjelent. Ha csak a látható részt szeretnéd, később feldolgozhatod Jsoup‑pal, és eltávolíthatod a `<head>`‑et.

---

## 4. lépés – Kinyert HTML mentése külön fájlba

A sztring lemezre írása egyszerű a `java.nio.file` API‑val. Ez a lépés bemutatja a **sztring fájlba írása** mintát, amely minden platformon működik.

```java
// Step 4: Save the extracted HTML to a separate file
Files.writeString(Path.of("YOUR_DIRECTORY/email_body.html"), htmlContent);
```

**Tipp:**  
Ha konkrét karakterkódolásra van szükséged, használd a `Files.writeString(Path, CharSequence, Charset)` metódust. Alapértelmezés szerint UTF‑8‑at használ, ami a legtöbb modern e‑mailhez megfelelő.

---

## 5. lépés – Ellenőrzés

Egy gyors `System.out.println` segítségével ellenőrizheted, hogy minden hiba nélkül lefutott. Egy éles környezetben ezt helyettesítheted megfelelő naplózással.

```java
// Step 5: Indicate successful extraction
System.out.println("HTML extracted.");
```

A program futtatásakor a konzolon a `HTML extracted.` szöveget kell látnod, és a `email_body.html` fájl megjelenik a `YOUR_DIRECTORY`‑ben.

---

## Teljes, futtatható példa

Összeállítva, itt a komplett, önálló Java osztály. Nyugodtan másold be az IDE‑dbe, és nyomd meg a **Run** gombot.

```java
import com.aspose.html.MhtmlDocument;
import java.io.FileInputStream;
import java.io.InputStream;
import java.nio.file.Files;
import java.nio.file.Path;

public class MhtmlToHtmlConverter {

    public static void main(String[] args) {
        // Adjust the path to point to your .mht/.mhtml file
        String sourcePath = "YOUR_DIRECTORY/email.mht";
        String targetPath = "YOUR_DIRECTORY/email_body.html";

        // Try-with-resources ensures the stream is closed automatically
        try (InputStream mhtmlStream = new FileInputStream(sourcePath)) {

            // Load the MHTML document
            MhtmlDocument mhtmlDoc = new MhtmlDocument(mhtmlStream);

            // Extract the HTML content
            String htmlContent = mhtmlDoc.getHtmlContent();

            // Write the HTML string to a new file
            Files.writeString(Path.of(targetPath), htmlContent);

            // Simple confirmation output
            System.out.println("HTML extracted to " + targetPath);
        } catch (Exception e) {
            // In real code you might want to log this instead of printing
            System.err.println("Failed to extract HTML: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Várt kimenet

A program futtatása valami ilyesmit ír ki:

```
HTML extracted to YOUR_DIRECTORY/email_body.html
```

És az `email_body.html` tartalmazni fogja az eredeti e‑mail teljes HTML forrását. Nyisd meg egy böngészőben – ugyanazt a vizuális megjelenést kell látnod, mint az archivált üzenetnél (kivéve a nem beágyazott külső erőforrásokat).

---

## Gyakori edge case‑ek kezelése

### 1. Hiányzó beágyazott erőforrások

Előfordulhat, hogy az MHTML fájl külső képeket hivatkozik, amelyek nincsenek elmentve az archívumba. Ilyenkor a `getHtmlContent()` még mindig visszaadja a `<img src="...">` markup‑ot, de az URL‑ek az eredeti webcímre mutatnak. Ha teljesen önálló HTML fájlt akarsz, megteheted:

- Használd a `MhtmlDocument.save(Path, SaveFormat.HTML)` metódust, hogy az Aspose kicsomagolja az összes erőforrást egy mappába.
- Vagy utófeldolgozd a HTML‑t egy olyan könyvtárral, mint a **Jsoup**, és cseréld le a távoli URL‑eket base64‑kódolt data URI‑kra.

### 2. Nem‑UTF‑8 kódolás

Ha az e‑mail más karakterkészlettel (pl. `windows-1252`) lett mentve, a visszakapott sztring torz karaktereket tartalmazhat. Ilyenkor kényszerítheted a kívánt karakterkódolást íráskor:

```java
Files.writeString(
    Path.of(targetPath),
    htmlContent,
    StandardCharsets.ISO_8859_1
);
```

### 3. Nagy fájlok

Ha az archívum néhány száz megabájtnál nagyobb, fontold meg a HTML kimenet közvetlen stream‑elését egy `BufferedWriter`‑rel, ahelyett, hogy az egész sztringet memóriába töltenéd. Az Aspose emellett kínál egy **`save`** metódust, amely közvetlenül fájlba ír, megkerülve a köztes `String`‑et.

---

## Pro tippek és legjobb gyakorlatok

- **Használd újra a `MhtmlDocument` objektumot**, ha több részt (pl. CSS, képek) kell kinyerned. Így csak egyszer kell az archívumot elemezni.
- **Érvényesítsd a kimenetet** egy HTML validatorral (W3C validator vagy `jsoup.isValid()`), ha más rendszernek kell továbbadnod.
- **Naplózz, ne nyomtatás** éles környezetben. Cseréld le a `System.out.println`‑t egy naplókeretrendszerre, például SLF4J‑ra, hogy időbélyegek és súlyossági szintek is rögzüljenek.
- **Verziókezelés a függőségekhez.** Az Aspose gyakran ad ki frissítéseket; rögzítsd a verziót a `pom.xml`‑ben, hogy elkerüld a váratlan tör breaking változásokat.

---

## Összegzés

Most egy gyakorlati, vég‑től‑végig megoldást láttál a **HTML kinyerésére MHTML‑ből** Java‑val. Az archívum stream‑ként való megnyitásával, az Aspose.HTML‑lel való betöltéssel, a HTML sztring lekérésével és a **sztring fájlba írásával** megbízható módon **konvertálhatod az MHTML‑t HTML‑re**, **kinyerheted az e‑mail törzsét**, és akár **MHT‑t HTML‑re** is átalakíthatod további feldolgozáshoz.

Nyugodtan módosítsd a kódrészletet: cseréld le a `FileInputStream`‑t `ByteArrayInputStream`‑re, ha az archívumaid adatbázisban élnek, vagy integráld a kódot egy nagyobb batch feladatba, amely egyszerre több e‑mailt dolgoz fel. A lényeg ugyanaz – hagyd, hogy egy dedikált könyvtár végezze a nehéz munkát, te pedig a tiszta szöveggel foglalkozz, ahogy csak szükséges.

**Következő lépések**, amiket érdemes felfedezni:

- Használd a Jsoup‑ot a **kinyert HTML tisztításához** (tracking pixel eltávolítása, inline CSS stb.).
- Automatizáld a **tömeges konvertálást** úgy, hogy egy könyvtár `.mht` fájljait ciklikusan feldolgozod.
- Kombináld ezt az **Apache POI**‑val, hogy a megtisztított HTML‑t Word vagy PDF dokumentumokba ágyazd.

Van kérdésed egy konkrét edge case‑ről, vagy szeretnéd megosztani, hogyan bővítetted a szkriptet? Írj egy kommentet alább – jó kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}