---
category: general
date: 2026-06-19
description: Naučte se, jak generovat PDF z HTML pomocí jednoduchého příkladu v Javě.
  Tento tutoriál HTML na PDF vám ukáže, jak převést HTML soubor na PDF pomocí OpenHTMLtoPDF.
draft: false
keywords:
- html to pdf tutorial
- generate pdf from html
- convert html file pdf
- create pdf from html
- convert webpage to pdf
language: cs
og_description: Návod html na pdf vám ukáže, jak vygenerovat PDF z HTML pomocí Javy.
  Postupujte podle kroků a rychle převádějte soubor HTML na PDF.
og_title: 'HTML na PDF tutoriál: Průvodce konverzí v Javě'
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  headline: 'html to pdf tutorial: Convert HTML to PDF in Java'
  type: TechArticle
- description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  name: 'html to pdf tutorial: Convert HTML to PDF in Java'
  steps:
  - name: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
    text: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
  - name: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
    text: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
  - name: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
    text: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
  type: HowTo
tags:
- Java
- PDF
- HTML conversion
title: 'html na pdf tutoriál: Převod HTML do PDF v Javě'
url: /cs/java/conversion-html-to-other-formats/html-to-pdf-tutorial-convert-html-to-pdf-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# html to pdf tutorial – Převod HTML stránky na PDF pomocí Javy

Už jste se někdy zamýšleli, jak převést statickou HTML stránku na elegantní PDF dokument, aniž byste opustili své IDE? Nejste v tom sami. V tomto **html to pdf tutorial** vás provedeme kompletním, připraveným k běhu Java příkladem, který **generate pdf from html** během několika minut.

Probereme vše, co potřebujete – nastavení projektu, přidání správné knihovny, psaní konverzního kódu a dokonce i rychlý tip na převod živé webové stránky do PDF. Na konci budete schopni **convert html file pdf** na svém počítači a pochopíte, jak **create pdf from html** pro jakýkoli budoucí projekt.

## Co budete potřebovat

- Java 17 nebo novější (kód funguje s jakýmkoli aktuálním JDK)
- Maven nebo Gradle (ukážeme Maven ukázku)
- Malý HTML soubor, který chcete převést na PDF (vytvoříme jej za běhu)
- IDE nebo jednoduchý textový editor – na vás

To je vše. Žádné těžkopádné servery, žádné placené SDK, jen čistá Java a bezplatná open‑source knihovna.

## Krok 1: html to pdf tutorial – Nastavení Maven projektu

First things first. Create a new Maven project (or add to an existing one). The only dependency you really need is **OpenHTMLtoPDF**, which does the heavy lifting of rendering HTML and CSS into a PDF.

```xml
<!-- pom.xml snippet -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>html-to-pdf-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- OpenHTMLtoPDF core -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-pdfbox</artifactId>
            <version>1.0.10</version>
        </dependency>
        <!-- Optional: support for SVG, if your HTML uses it -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-svg-support</artifactId>
            <version>1.0.10</version>
        </dependency>
    </dependencies>
</project>
```

> **Tip:** Pokud používáte Gradle, stejné závislosti můžete přidat pod `implementation` v souboru `build.gradle`.  

Proč je tento krok důležitý: bez knihovny JVM neví, jak převést HTML tagy na PDF kreslicí příkazy. OpenHTMLtoPDF je lehká, aktivně udržovaná a podporuje CSS‑2.1, takže vaše stylování zůstane zachováno.

## Krok 2: generate pdf from html – Připravte ukázkový HTML soubor

Pojďme vytvořit malý `input.html` vedle našeho Java zdroje. To udržuje příklad samostatný a demonstruje workflow **create pdf from html**.

```html
<!-- src/main/resources/input.html -->
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Sample Report</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        h1 { color: #2E86C1; }
        p { line-height: 1.5; }
    </style>
</head>
<body>
    <h1>Monthly Sales Report</h1>
    <p>This PDF was generated directly from an HTML file using Java.</p>
    <p>All you need is a few lines of code.</p>
</body>
</html>
```

Můžete nahradit obsah čímkoli – tabulkami, obrázky, dokonce JavaScriptem (renderovač skripty ignoruje). Důležité je, aby soubor byl na classpath, aby jej konvertor mohl najít.

## Krok 3: convert html file pdf – Napište konverzní utilitu

Nyní jádro **html to pdf tutorial**: malá třída `HtmlToPdfConverter`, která načte HTML a zapíše PDF. Níže uvedený kód je kompletní, spustitelný příklad; zkopírujte jej do `src/main/java/com/example/HtmlToPdfConverter.java`.

```java
package com.example;

import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardCopyOption;

/**
 * Simple utility that converts an HTML file to PDF.
 * It demonstrates the "convert html file pdf" use‑case.
 */
public class HtmlToPdfConverter {

    /**
     * Converts the given HTML file to a PDF file.
     *
     * @param htmlPath path to the source HTML file (can be absolute or classpath)
     * @param pdfPath  destination path for the generated PDF
     * @throws IOException if reading or writing fails
     */
    public static void convert(String htmlPath, String pdfPath) throws IOException {
        // Resolve the HTML file – support both absolute paths and classpath resources
        InputStream htmlStream = Files.exists(Path.of(htmlPath))
                ? Files.newInputStream(Path.of(htmlPath))
                : HtmlToPdfConverter.class.getResourceAsStream(htmlPath);

        if (htmlStream == null) {
            throw new FileNotFoundException("HTML source not found: " + htmlPath);
        }

        // Ensure the output directory exists
        Path pdfFile = Path.of(pdfPath);
        Files.createDirectories(pdfFile.getParent());

        try (OutputStream os = Files.newOutputStream(pdfFile);
             InputStream is = htmlStream) {

            // Builder does the heavy lifting – it parses HTML + CSS and writes PDF bytes
            new PdfRendererBuilder()
                    .withHtmlContent(new String(is.readAllBytes()), null) // base URI null = no external resources
                    .toStream(os)
                    .run();
        }
    }

    // Demo entry point – feel free to run this class directly
    public static void main(String[] args) {
        // Step 1: Specify the input HTML file location
        String htmlPath = "src/main/resources/input.html";

        // Step 2: Specify the desired output PDF file location
        String pdfPath = "target/output.pdf";

        // Step 3: Convert the HTML document to PDF using default conversion settings
        try {
            convert(htmlPath, pdfPath);
            System.out.println("✅ PDF successfully created at " + pdfPath);
        } catch (Exception e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Proč tento kód funguje

1. **Resource flexibility** – metoda nejprve zkontroluje, zda zadaná cesta ukazuje na skutečný soubor; pokud ne, přejde na zdroj v classpath. To znamená, že později můžete **convert webpage to pdf** zadáním URL řetězce (stačí nahradit volání `withHtmlContent` za `withUri`).

2. **Automatic directory creation** – `Files.createDirectories` zajišťuje, že složka `target/` existuje, takže nedostanete chybu „No such file or directory“.

3. **Single‑line conversion** – `PdfRendererBuilder` interně zpracovává CSS, fonty a rozvržení stránek. Není potřeba ručně spravovat PDF stránky; knihovna to udělá za vás, což udržuje příklad stručný a zaměřený na koncept **convert html file pdf**.

## Krok 4: create pdf from html – Spusťte program a ověřte výsledek

Otevřete terminál v kořenovém adresáři projektu a spusťte:

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HtmlToPdfConverter
```

Pokud je vše nastaveno správně, uvidíte:

```
✅ PDF successfully created at target/output.pdf
```

Otevřete `target/output.pdf` v libovolném PDF prohlížeči. Měli byste vidět stylizovaný nadpis „Monthly Sales Report“, text odstavce a stejné okraje, které jste definovali v HTML `<style>` bloku.

> **Co když nevidíte stylování?**  
> Ujistěte se, že je CSS inline nebo umístěné ve stejné složce jako HTML. OpenHTMLtoPDF řeší relativní URL na základě base URI, kterou předáte `withHtmlContent`. Ve výše uvedeném úryvku jsme předali `null`, což funguje pro jednoduché inline CSS. Pro externí styly zadejte cestu ke složce jako druhý argument.

## Krok 5: convert webpage to pdf – Zpracování vzdálených URL (volitelné)

Někdy potřebujete **convert webpage to pdf** přímo z internetu – například archivovat online účtenku. Knihovna to podporuje pomocí `withUri`. Zde je rychlá úprava:

```java
public static void convertUrl(String url, String pdfPath) throws IOException {
    Path pdfFile = Path.of(pdfPath);
    Files.createDirectories(pdfFile.getParent());

    try (OutputStream os = Files.newOutputStream(pdfFile)) {
        new PdfRendererBuilder()
                .withUri(url)          // Load HTML from the web
                .toStream(os)
                .run();
    }
}
```

Použijte ji takto:



## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční kódové příklady s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Jak převést HTML na PDF v Javě – Použití Aspose.HTML pro Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Převod HTML na PDF v Javě – Konfigurace prostředí v Aspose.HTML](/html/english/java/configuring-environment/)
- [Převod HTML na PDF v Javě – Průvodce krok za krokem s nastavením velikosti stránky](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}