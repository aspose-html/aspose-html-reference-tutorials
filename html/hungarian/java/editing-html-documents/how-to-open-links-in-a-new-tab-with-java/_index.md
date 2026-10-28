---
category: general
date: 2026-10-28
description: Tanulja meg, hogyan nyisson meg linkeket új lapon Java-ban HTML elemzésével,
  külső linkek megtalálásával és a target='_blank' hozzáadásával.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- open links new tab
- find external links
- add target blank
- parse html in java
- save modified html
language: hu
lastmod: 2026-10-28
og_description: 'Nyissa meg a linkeket új lapon Java-val: HTML elemzése, külső hivatkozások
  megtalálása, target=''_blank'' hozzáadása, és a módosított HTML mentése.'
og_image_alt: Screenshot of Java code that parses HTML and updates external links
  to open in a new tab
og_title: Linkek megnyitása új lapon Java‑val – lépésről‑lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to open links in a new tab by parsing HTML in Java, finding
    external links and adding target blank.
  headline: How to open links in a new tab with Java
  type: TechArticle
tags:
- Java
- HTML parsing
- jsoup
- web automation
title: Hogyan nyissunk meg linkeket új lapon Java-val
url: /hu/java/editing-html-documents/how-to-open-links-in-a-new-tab-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan nyissunk meg linkeket új lapon Java-val

Ha **új lapon szeretnél megnyitni linkeket** egy statikus HTML fájlból, ez az útmutató pontosan megmutatja, hogyan teheted ezt. Megtanulod, hogyan **parse-olod a HTML-t Java-ban**, **keresd meg a külső linkeket**, **add hozzá a target="_blank" attribútumot**, és **mentsd el a módosított HTML-t** anélkül, hogy elhagynád az IDE-det.

Az externális linkek új böngészőlapon való megnyitása javítja a felhasználói élményt és a látogatókat az eredeti oldalon tartja. Az alábbi megoldás bármely HTML dokumentummal működik, csak a népszerű jsoup könyvtárra van szükség, és Java 8 vagy újabb verzióval fut.

## Előfeltételek

* JDK 8 + telepítve  
* Egy build eszköz (Maven vagy Gradle) a **jsoup** függőség behozzáadásához  
* Egy HTML fájl, amelyben a `external` osztályú <a> elemek vannak

Nem szükséges webkiszolgáló vagy további keretrendszer – a jsoup mindent helyben kezel.

## 1. lépés: Állítsd be a jsoup-ot a projektedben

Add hozzá a jsoup-ot függőségként. Ha Maven-t használsz, helyezd ezt a `pom.xml`-be:

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

Gradle esetén add hozzá a következő sort a `build.gradle`-hez:

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

Ezek a koordináták a legújabb stabil kiadást húzzák (2026. október állapotában). A szinkronizálás után importálhatod az `org.jsoup` osztályokat a Java forrásfájlokba.

## 2. lépés: A HTML dokumentum parse-olása

Az állomány parse-olása az első lépés a **linkek új lapon való megnyitása** felé. A `Jsoup.parse` metódus beolvassa a fájlt egy módosítható DOM‑szerű struktúrába.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // Load the HTML document from disk
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");
        
        // Continue with link processing...
    }
}
```

*Miért fontos*: A `Document` CSS‑stílusú szelektorokat biztosít, így egyszerűen megtalálhatod a szükséges elemeket.

## 3. lépés: Külső linkek megtalálása

Most keresd meg minden `<a>` elemet, amely a `external` osztályt tartalmazza. Ez megfelel a **külső linkek megtalálása** követelménynek.

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

// Inside main after parsing:
Elements externalLinks = doc.select("a.external");
```

A `Elements` a megfelelő csomópontok gyűjteménye. Ha a selector üres halmazt ad vissza, a HTML-ed vagy hiányolja az osztályt, vagy más elnevezést használ – módosítsd ennek megfelelően a selectort.

## 4. lépés: `target="_blank"` hozzáadása minden linkhez

Minden, a **külső linkek megtalálása** által visszaadott csomópontra állítsd be a `target` attribútumot `_blank`-ra. Ez teljesíti a **target blank hozzáadása** lépést, és biztosítja, hogy a böngészők új lapon nyissák meg a linket.

```java
for (Element link : externalLinks) {
    link.attr("target", "_blank");
}
```

A `attr` metódus felülírja a meglévő `target` értéket, garantálva a konzisztens viselkedést minden külső horgonynál.

## 5. lépés: A módosított HTML mentése

A DOM frissítése után írd vissza a változásokat egy fájlba. Ezzel befejeződik a **módosított html mentése** része az útmutatónak.

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

// Still inside main:
Path output = Path.of("YOUR_DIRECTORY/updated.html");
Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
System.out.println("Updated file written to " + output);
```

A `doc.outerHtml()` sorosítja az egész dokumentumot, megőrizve a behúzást és a formázást, ahogy a jsoup eredetileg beolvasta.

## Teljes működő példa

Az összes lépés egyesítése egy önálló programot eredményez, amelyet másolhatsz, beilleszthetsz és futtathatsz.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

/**
 * Updates all external links so they open in a new tab.
 */
public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // 1️⃣ Parse the HTML file
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");

        // 2️⃣ Find external links (a.external)
        Elements externalLinks = doc.select("a.external");

        // 3️⃣ Add target="_blank" to each link
        for (Element link : externalLinks) {
            link.attr("target", "_blank");
        }

        // 4️⃣ Save the modified HTML
        Path output = Path.of("YOUR_DIRECTORY/updated.html");
        Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
        System.out.println("Updated file written to " + output);
    }
}
```

### Várható kimenet

Tegyük fel, hogy a `sample.html` a következőt tartalmazza:

```html
<a href="https://example.com" class="external">Example</a>
<a href="/internal/page.html">Internal</a>
```

A program futtatása után a `updated.html` a következőt fogja tartalmazni:

```html
<a href="https://example.com" class="external" target="_blank">Example</a>
<a href="/internal/page.html">Internal</a>
```

Csak a külső link kapta meg a `target="_blank"` attribútumot, ami azt jelenti, hogy a böngészők most már új lapon nyitják meg.

## Pro tippek és gyakori buktatók

* **Pro tip:** Ha olyan linkeket is külsőnek szeretnél tekinteni, amelyek `http://` vagy `https://`-vel kezdődnek, CSS osztály nélkül, bővítsd a selectort: `doc.select("a[href^=http]")`.
* **Edge case:** Néhány oldal már megadja a `target="_self"` attribútumot; az `attr` hívás felülírja, biztosítva a konzisztens viselkedést.
* **Performance:** Nagyon nagy HTML fájlok esetén fontold meg a streaming parse-olást (`Jsoup.parse(File, String, String, Parser.htmlParser())`) a memóriahasználat csökkentése érdekében.
* **Testing:** Ellenőrizd az eredményt úgy, hogy megnyitod az `updated.html`-t egy böngészőben, és a fejlesztői eszközökkel megnézed a linket – keresd a `target` attribútumot.

## Következtetés

Most már van egy teljes, futtatható megoldásod a **linkek új lapon való megnyitására** Java-val. Az útmutató bemutatta, hogyan **parse-oljuk a html-t java-ban**, **keressük meg a külső linkeket**, **adjunk hozzá target blank-ot**, és **mentsük el a módosított html-t**, mindezt a könnyű jsoup könyvtárral.

Innen tovább:

* Bővítsd a selectort más link minták kezelésére (pl. `rel="external"`).  
* Kombináld ezt a logikát egy build lépéssel, amely egy projekt összes HTML fájlját feldolgozza.  
* Integráld a kódot egy nagyobb tartalomkezelő folyamatba.

Nyugodtan kísérletezz különböző szelektorokkal vagy kimeneti formátumokkal, és oszd meg az eredményeidet a közösséggel!

## Mit érdemes következőként megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan használjunk CSS-t Java-ban – HTML betöltése, linkek számlálása és XPath kiértékelése](/html/english/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/)
- [Hogyan parse-oljuk a HTML-t Java-ban – Szöveg kinyerése HTML cikkekből](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Új HTML elem létrehozása Java-val – Teljes Aspose.HTML útmutató](/html/english/java/editing-html-documents/create-new-html-element-with-java-full-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}