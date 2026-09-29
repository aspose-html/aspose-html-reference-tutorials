---
category: general
date: 2026-09-29
description: Změňte barvu pozadí pomocí JavaScriptu v HTML souboru pomocí Javy. Naučte
  se načíst HTML v Javě, spustit JavaScript v HTML a upravit HTML pomocí Javy pro
  nové pozadí stránky.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change background color javascript
- load html in java
- run js in html
- modify html with java
- set page background
language: cs
lastmod: 2026-09-29
og_description: Změňte barvu pozadí pomocí JavaScriptu v HTML stránce pomocí Javy.
  Tento tutoriál vám ukáže, jak načíst HTML v Javě, spustit JS v HTML a nastavit pozadí
  stránky programově.
og_image_alt: Screenshot of Java code that changes the page background color
og_title: Změna barvy pozadí v JavaScriptu pomocí Javy – průvodce krok po kroku
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
title: Jak změnit barvu pozadí v JavaScriptu pomocí Javy
url: /cs/java/editing-html-documents/how-to-change-background-color-javascript-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak změnit barvu pozadí javascript pomocí Javy

Pokud potřebujete **change background color javascript** v existujícím souboru HTML, můžete to provést kompletně z Javy bez otevírání prohlížeče. Tento tutoriál vám ukáže, jak **load html in java**, spustit malý úryvek JavaScriptu a poté **modify html with java**, aby se pozadí stránky aktualizovalo.  

Řešení funguje s open‑source knihovnou **HTMLUnit**, která poskytuje headless prohlížeč schopný vyhodnocovat JavaScript přesně tak, jako by to dělal skutečný prohlížeč. Na konci tohoto průvodce budete mít znovupoužitelnou metodu, která **sets page background** na libovolnou barvu, kterou si vyberete.

## Požadavky

| Co potřebujete | Proč je to důležité |
|---------------|----------------|
| Java 8 nebo novější | HTMLUnit vyžaduje alespoň Java 8. |
| Maven nebo Gradle build tool | Pro automatické stažení závislosti HTMLUnit. |
| HTML soubor, který chcete upravit (např. `input.html`) | Zdrojový dokument, který bude načten a změněn. |

Přidejte HTMLUnit do svého projektu:

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

> **Tip:** Použijte nejnovější stabilní verzi HTMLUnit, abyste získali co nejpřesnější JavaScript engine.

## Změna barvy pozadí javascript – načtení HTML v Javě

Prvním krokem je načíst HTML dokument do objektu `HTMLPage`. To vám poskytne API podobné DOM a kontext pro vykonávání JavaScriptu.

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

*Proč je to důležité*: `WebClient` vytváří sandboxované prostředí, kde může běžet JavaScript, takže můžete **run js in html** přesně tak, jak by to udělal prohlížeč uživatele.

## Spuštění js v html pro nastavení pozadí stránky

Jakmile je stránka načtena, můžete vyhodnotit libovolný JavaScript výraz. Níže uvedený úryvek mění styl `backgroundColor` elementu `<body>`.

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

*Vysvětlení*:  
- `document.body.style.backgroundColor` je standardní DOM vlastnost pro pozadí stránky.  
- Voláním `eval` **run js in html** bez potřeby skutečného okna prohlížeče.  
- Metoda je znovupoužitelná pro libovolnou barvu, splňující požadavek **set page background**.

## Úprava html pomocí Javy a uložení výsledku

Po spuštění skriptu DOM odráží nový styl. Nyní můžete zapsat aktualizované HTML zpět na disk.

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

Složení všeho dohromady vám poskytne jeden spustitelný program:

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

### Očekávaný výstup

Spuštění programu vypíše:

```
Background color changed to 'lightblue' and saved to YOUR_DIRECTORY/js_modified.html
```

Otevření `js_modified.html` v libovolném prohlížeči zobrazí stránku se světle modrým pozadím, což potvrzuje úspěšnost operace **change background color javascript**.

## Běžné varianty a okrajové případy

| Situace | Jak to řešit |
|-----------|------------------|
| **Různé formáty barev** | Předávejte libovolnou hodnotu kompatibilní s CSS (`"red"`, `"#ff0000"`, `"rgb(255,0,0)"`). |
| **Chybějící tag `<body>`** | Skript selže tiše; můžete nejprve zajistit, že `<body>` existuje pomocí `page.getFirstByXPath("//body")`. |
| **Velké HTML soubory** | Vypněte CSS (`setCssEnabled(false)`) a povolte jen JavaScriptové funkce, které potřebujete, aby se snížila spotřeba paměti. |
| **Spouštění více skriptů** | Volajte `changeBackground` opakovaně nebo vytvořte pomocnou metodu, která přijímá seznam JavaScriptových příkazů. |

## Závěr

Nyní víte, jak **change background color javascript** načtením HTML souboru v Javě, **run js in html**, a **modify html with java**, abyste **set page background** na libovolnou barvu podle vašeho výběru. Kompletní příklad výše funguje s nejnovější knihovnou HTMLUnit a může být integrován do větších automatizačních pipeline, jako je dávkové zpracování HTML reportů nebo příprava e‑mailových šablon.

**Další kroky**  
- Prozkoumejte další manipulace s DOM (např. vkládání elementů, odstraňování skriptů).  
- Kombinujte tento přístup s PDF renderérem pro generování PDF stylizovaných stránek.  
- Vyzkoušejte použití jiného headless enginu, jako je Selenium WebDriver, pokud potřebujete plnou věrnost prohlížeče.

Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Get Computed Style Java – Extract Background Color from HTML](/html/english/java/css-html-form-editing/get-computed-style-java-extract-background-color-from-html/)
- [How to Load HTML, Set Device DPI & Read Background Color](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Generate HTML from JavaScript in Java – Complete Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/generate-html-from-javascript-in-java-complete-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}