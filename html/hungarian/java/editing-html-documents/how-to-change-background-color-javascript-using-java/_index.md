---
category: general
date: 2026-09-29
description: Háttérszín változtatása JavaScript segítségével egy HTML-fájlban Java
  használatával. Tanulja meg, hogyan töltsön be HTML-t Java-ban, futtassa a JS-t a
  HTML-ben, és módosítsa a HTML-t Java-val egy új oldal háttéréhez.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change background color javascript
- load html in java
- run js in html
- modify html with java
- set page background
language: hu
lastmod: 2026-09-29
og_description: Háttérszín módosítása JavaScript-tel egy HTML oldalon Java használatával.
  Ez az útmutató megmutatja, hogyan töltsünk be HTML-t Java-ban, futtassunk JS-t HTML-ben,
  és állítsuk be programozottan az oldal háttérszínét.
og_image_alt: Screenshot of Java code that changes the page background color
og_title: Háttérszín változtatása JavaScript-tel Java segítségével – lépésről lépésre
  útmutató
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Change background color javascript in an HTML file using Java. Learn
    to load html in java, run js in html, and modify html with java for a new page
    background.
  headline: How to change background color javascript using Java
  type: TechArticle
tags:
- Java
- HTMLUnit
- JavaScript
- HTML manipulation
title: Hogyan változtassuk meg a háttérszínt JavaScript-ben Java használatával
url: /hu/java/editing-html-documents/how-to-change-background-color-javascript-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan változtassuk meg a háttérszínt JavaScript‑ben Java használatával

Ha egy meglévő HTML fájlban **change background color javascript**‑t szeretnél módosítani, teljesen Java‑ból megteheted böngésző megnyitása nélkül. Ez a tutorial bemutatja, hogyan **load html in java**, egy kis JavaScript kódrészletet hajts végre, majd **modify html with java**, hogy az oldal háttérszíne frissüljön.  

A megoldás az nyílt forráskódú **HTMLUnit** könyvtárral működik, amely egy fej nélküli böngészőt biztosít, ami a JavaScript‑et pontosan úgy értékeli, mint egy valódi böngésző. A útmutató végére egy újrahasználható metódust kapsz, amely **sets page background**‑t bármilyen általad választott színre.

## Előfeltételek

| Szükséges | Miért fontos |
|---------------|----------------|
| Java 8 or newer | A HTMLUnit legalább Java 8-at igényel. |
| Maven or Gradle build tool | A HTMLUnit függőség automatikus lekéréséhez. |
| An HTML file you want to edit (e.g., `input.html`) | A forrásdokumentum, amelyet be fogunk tölteni és módosítani. |

Add HTMLUnit to your project:

*Maven*  

```xml
<dependency>
    <groupId>net.sourceforge.htmlunit</groupId>
    <artifactId>htmlunit</artifactId>
    <version>2.71.0</version>
</dependency>
```

*Gradle*  

```gradle
implementation 'net.sourceforge.htmlunit:htmlunit:2.71.0'
```

> **Pro tip:** Használd a HTMLUnit legújabb stabil verzióját a legpontosabb JavaScript motorért.

## Change background color javascript – HTML betöltése Java‑ban

Az első lépés, hogy betöltsük a HTML dokumentumot egy `HTMLPage` objektumba. Ez egy DOM‑szerű API‑t és egy JavaScript végrehajtási kontextust biztosít.

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;

public class BackgroundColorChanger {

    /**
     * Loads an HTML file from the given path.
     *
     * @param htmlPath absolute or relative path to the source HTML file
     * @return HtmlPage representing the loaded document
     * @throws IOException if the file cannot be read
     */
    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        // WebClient acts as a headless browser; disabling CSS speeds up loading.
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);

        // Convert the file path to a URL that HTMLUnit can understand.
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }
}
```

*Why this matters*: `WebClient` egy sandbox környezetet hoz létre, ahol a JavaScript futtatható, így **run js in html**‑t pontosan úgy tudod végrehajtani, ahogy egy felhasználó böngészője.

## Run js in html a page background beállításához

Miután az oldal betöltődött, bármely JavaScript kifejezést kiértékelhetsz. Az alábbi kódrészlet megváltoztatja a `<body>` elem `backgroundColor` stílusát.

```java
/**
 * Executes JavaScript that changes the page background color.
 *
 * @param page   the HtmlPage loaded earlier
 * @param color  any valid CSS color string, e.g., "lightblue" or "#ffcc00"
 */
private static void changeBackground(HtmlPage page, String color) {
    // The eval method runs JavaScript in the page's context.
    String script = "document.body.style.backgroundColor = '" + color + "';";
    page.getEnclosingWindow().getScriptableObject().eval(script);
}
```

*Magyarázat*:
- `document.body.style.backgroundColor` a szabványos DOM tulajdonság az oldal háttérszínéhez.  
- `eval` hívásával **run js in html**-t hajtunk végre anélkül, hogy valódi böngészőablakra lenne szükség.  
- A metódus újrahasználható bármilyen színhez, ezáltal teljesíti a **set page background** követelményt.

## Modify html with java és az eredmény mentése

A szkript futása után a DOM tükrözi az új stílust. Most már visszaírhatod a frissített HTML‑t a lemezre.

```java
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Saves the modified HTML content to a new file.
 *
 * @param page          the HtmlPage that has been altered
 * @param outputPath    destination file path
 * @throws IOException  if writing fails
 */
private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
    // page.asXml() returns the current HTML markup, including the changed style.
    String updatedHtml = page.asXml();
    Files.write(Paths.get(outputPath), updatedHtml.getBytes());
}
```

Az összes összetevő egyesítése egyetlen, futtatható programot eredményez:

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

public class BackgroundColorChanger {

    public static void main(String[] args) {
        // Adjust these paths for your environment.
        String inputFile = "YOUR_DIRECTORY/input.html";
        String outputFile = "YOUR_DIRECTORY/js_modified.html";
        String newColor = "lightblue"; // Change to any CSS color you need.

        try {
            HtmlPage page = loadHtml(inputFile);
            changeBackground(page, newColor);
            saveModifiedHtml(page, outputFile);
            System.out.println("Background color changed to '" + newColor + "' and saved to " + outputFile);
        } catch (IOException e) {
            System.err.println("Error processing HTML file: " + e.getMessage());
        }
    }

    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }

    private static void changeBackground(HtmlPage page, String color) {
        String script = "document.body.style.backgroundColor = '" + color + "';";
        page.getEnclosingWindow().getScriptableObject().eval(script);
    }

    private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
        String updatedHtml = page.asXml();
        Files.write(Paths.get(outputPath), updatedHtml.getBytes());
    }
}
```

### Várható kimenet

A program futtatása kiírja:

```
Background color changed to 'lightblue' and saved to YOUR_DIRECTORY/js_modified.html
```

`js_modified.html` megnyitása bármely böngészőben egy világoskék háttérrel jeleníti meg az oldalt, ami megerősíti, hogy a **change background color javascript** művelet sikeres volt.

## Gyakori variációk és szélsőséges esetek

| Helyzet | Hogyan kezelhető |
|-----------|------------------|
| **Different color formats** | Adj meg bármilyen CSS‑kompatibilis értéket (`"red"`, `"#ff0000"`, `"rgb(255,0,0)"`). |
| **Missing `<body>` tag** | A szkript csendben hibát fog jelezni; először ellenőrizheted, hogy `<body>` létezik-e a `page.getFirstByXPath("//body")` segítségével. |
| **Large HTML files** | Kapcsold ki a CSS‑t (`setCssEnabled(false)`) és csak a szükséges JavaScript funkciókat engedélyezd a memóriahasználat csökkentése érdekében. |
| **Running multiple scripts** | Hívd meg többször a `changeBackground`‑t, vagy hozz létre egy segédmetódust, amely JavaScript parancsok listáját fogadja. |

## Összegzés

Most már tudod, hogyan **change background color javascript** egy HTML fájl Java‑ban történő betöltésével, **run js in html**, és **modify html with java**, hogy **set page background**‑t bármilyen általad választott színre állítsd. A fenti teljes példa a legújabb HTMLUnit könyvtárral működik, és beépíthető nagyobb automatizálási folyamatokba, például HTML jelentések kötegelt feldolgozásába vagy e‑mail sablonok előkészítésébe.

**Next steps**  
- Fedezd fel a többi DOM manipulációt (pl. elemek beszúrása, szkriptek eltávolítása).  
- Kombináld ezt a megközelítést egy PDF renderelővel, hogy a stílusos oldalakról PDF‑eket generálj.  
- Próbálj ki egy másik fej nélküli motorot, például a Selenium WebDriver‑t, ha teljes böngésző‑hűséget igényelsz.

Boldog kódolást!

## Mit érdemes legközelebb megtanulni?

A következő tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsenek további API‑funkciók elsajátításában és alternatív megvalósítási megközelítések felfedezésében a saját projektjeidben.

- [Get Computed Style Java – Extract Background Color from HTML](/html/english/java/css-html-form-editing/get-computed-style-java-extract-background-color-from-html/)
- [How to Load HTML, Set Device DPI & Read Background Color](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Generate HTML from JavaScript in Java – Complete Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/generate-html-from-javascript-in-java-complete-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}