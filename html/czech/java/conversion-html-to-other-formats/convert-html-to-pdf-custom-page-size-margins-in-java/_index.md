---
category: general
date: 2026-04-03
description: Převod HTML do PDF pomocí Aspose.HTML v Javě s vlastním rozměrem stránky
  PDF, nastavením okrajů PDF a šířkou stránky PDF. Naučte se, jak rychle převést HTML.
draft: false
keywords:
- convert html to pdf
- custom pdf page size
- set pdf margins
- how to convert html
- set pdf page width
language: cs
og_description: Převod HTML na PDF pomocí Aspose.HTML v Javě. Tento průvodce ukazuje,
  jak nastavit vlastní velikost stránky PDF, okraje a šířku stránky pro dokonalé výsledky.
og_title: Převod HTML na PDF – Vlastní velikost stránky a okraje v Javě
tags:
- Java
- PDF
- Aspose.HTML
title: Převod HTML do PDF – Vlastní velikost stránky a okraje v Javě
url: /cs/java/conversion-html-to-other-formats/convert-html-to-pdf-custom-page-size-margins-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod HTML do PDF – Vlastní velikost stránky a okraje v Javě

Už jste někdy potřebovali **převést HTML do PDF** a přemýšleli, jak ovládat rozměry stránky? V tomto tutoriálu vás provedeme kompletním, připraveným řešením, které ukazuje, jak **převést HTML do PDF** s *vlastní velikostí PDF stránky*, jak **nastavit okraje PDF**, a dokonce jak **nastavit šířku PDF stránky** pomocí Aspose.HTML pro Java.  

Pokud vytváříte faktury, zprávy nebo e‑knihy, tyto úpravy rozvržení jsou rozdílem mezi nudným výpisem textu a vylepšeným dokumentem, který vypadá přesně tak, jak chcete.

## Co se naučíte

* Jak nastavit jednoduchý Maven/Gradle projekt s Aspose.HTML.
* Proč výběr správné velikosti stránky má význam pro tisk a vykreslování na obrazovce.
* Krok‑za‑krokem kód pro **převod HTML do PDF** s úpravou výšky, šířky a okrajů.
* Časté úskalí (např. chybějící CSS media queries) a jak se jim vyhnout.
* Jak ověřit, že PDF bylo vygenerováno správně.

Žádná předchozí zkušenost s Aspose není vyžadována — stačí základní Java IDE a schopnost spustit metodu `main`.

## Požadavky

* **Java 17** (nebo jakýkoli aktuální JDK) nainstalovaný na vašem počítači.  
* Knihovna **Aspose.HTML for Java** – můžete stáhnout nejnovější JAR z Maven Central (`com.aspose:aspose-html:23.9` v době psaní).  
* Jednoduchý HTML soubor (`input.html`), který chcete převést na PDF.  
* Volitelné: editor obrázků, pokud chcete náhled výstupu PDF.

> **Tip:** Pokud používáte Maven, přidejte níže uvedenou závislost do vašeho `pom.xml`. Pokud dáváte přednost Gradle, stejné souřadnice fungují s konfigurací `implementation`.

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

```groovy
// Gradle
implementation 'com.aspose:aspose-html:23.9'
```

## Převod HTML do PDF – Nastavení projektu

Nejprve vytvořte novou třídu Java s názvem `PdfConversionAdvanced`. Tato třída bude obsahovat veškerou logiku konverze. Importy, které potřebujete, jsou uvedeny na začátku souboru — klidně je zkopírujte přímo.

```java
import com.aspose.html.*;
import com.aspose.html.converters.*;
import com.aspose.html.converters.pdf.*;

public class PdfConversionAdvanced {
    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1: Point to the source HTML file you want to convert.
        // -----------------------------------------------------------------
        String inputHtmlPath = "YOUR_DIRECTORY/input.html";

        // -----------------------------------------------------------------
        // Step 2: Create PdfSaveOptions and configure custom page size.
        // -----------------------------------------------------------------
        PdfSaveOptions pdfOptions = new PdfSaveOptions();

        // A5 size in points (1 pt = 1/72 inch). Adjust as needed.
        pdfOptions.setPageWidth(420);   // set pdf page width
        pdfOptions.setPageHeight(595);  // set pdf page height

        // -----------------------------------------------------------------
        // Step 3: Define margins – 10 mm ≈ 28.35 points.
        // -----------------------------------------------------------------
        pdfOptions.setMarginTop(28.35);
        pdfOptions.setMarginBottom(28.35);
        pdfOptions.setMarginLeft(28.35);
        pdfOptions.setMarginRight(28.35);

        // -----------------------------------------------------------------
        // Step 4: Make sure the converter uses the "print" media type.
        // -----------------------------------------------------------------
        pdfOptions.setMediaType("print");

        // -----------------------------------------------------------------
        // Step 5: Perform the conversion.
        // -----------------------------------------------------------------
        String outputPdfPath = "YOUR_DIRECTORY/output.pdf";
        Converter.convert(inputHtmlPath, outputPdfPath, pdfOptions);

        // -----------------------------------------------------------------
        // Step 6: Confirm the file was created.
        // -----------------------------------------------------------------
        System.out.println("PDF created with custom layout at " + outputPdfPath);
    }
}
```

### Proč jsou tato nastavení důležitá

* **Custom PDF page size** (`setPageWidth` / `setPageHeight`) vám umožní cílit na A5, Letter nebo jakýkoli vlastní rozměr, který potřebujete. Pokud to vynecháte, Aspose použije výchozí A4, což může plýtvat papírem nebo narušit design.
* **Set PDF margins** zajišťuje, že obsah nebude přiléhat k okrajům stránky — kritické pro tiskárny, které vyžadují ne‑tisknutelnou oblast.
* **Media type “print”** nutí engine použít jakýkoli `@media print` CSS, který jste definovali, a dává vám jemnou kontrolu nad fonty, barvami a rozvržením, které se liší od zobrazení na obrazovce.

## Definování vlastní velikosti PDF stránky

Pokud výchozí velikost A4 nevyhovuje vašemu projektu, můžete použít libovolné rozměry. Výše uvedený úryvek kódu již ukazuje klasické rozvržení A5, ale podívejme se na několik alternativ:

| Velikost | Šířka (pt) | Výška (pt) |
|----------|------------|------------|
| **Letter** | 612 | 792 |
| **Legal** | 612 | 1008 |
| **Custom 8×10 inches** | 576 | 720 |

Pro použití vlastní velikosti stačí nahradit hodnoty předávané do `setPageWidth` a `setPageHeight`. Pamatujte: **1 point = 1/72 inch**, takže rychlým násobením získáte správná čísla.

> **Poznámka:** Pokud potřebujete přepnout z portrétu na krajinu, stačí prohodit hodnoty šířky a výšky.

## Nastavení okrajů PDF pro přesné rozvržení

Okraje jsou také vyjádřeny v bodech. Příklad používá **10 mm** (≈ 28,35 pt) na všech stranách. Chcete těsnější rozvržení? Změňte čísla:

```java
pdfOptions.setMarginTop(14.18);    // 5 mm
pdfOptions.setMarginBottom(14.18);
pdfOptions.setMarginLeft(21.26);   // 7.5 mm
pdfOptions.setMarginRight(21.26);
```

Proč to dělat? Tiskárny často mají minimální tisknutelnou oblast — nastavením okrajů zabráníte oříznutí obsahu. Navíc konzistentní okraj dodá vašemu PDF profesionální vzhled, zejména při generování smluv nebo certifikátů.

## Dynamické nastavení šířky (a výšky) PDF stránky

Někdy HTML, které obdržíte, již obsahuje nápovědu o šířce (např. `<div>` stylovaný na 800 px). Můžete vypočítat požadovanou šířku PDF za běhu:

```java
int htmlWidthPx = 800;                     // example from HTML
double pointsPerPixel = 0.75;              // 96 DPI => 0.75 pt per pixel
pdfOptions.setPageWidth(htmlWidthPx * pointsPerPixel);
```

Tato technika zajišťuje, že PDF odráží původní rozvržení bez deformace. Je to užitečný trik, když **jak převést HTML**, která byla původně navržena pro zobrazení na obrazovce.

## Spuštění konverze a ověření výstupu

Jakmile máte vše nastavené, spusťte metodu `main`. Pokud je vše správně propojeno, uvidíte:

```
PDF created with custom layout at YOUR_DIRECTORY/output.pdf
```

Otevřete výsledné PDF v libovolném prohlížeči (Adobe Reader, Chrome nebo náhled vašeho OS). Měli byste vidět:

* Přesnou velikost stránky, kterou jste definovali.
* Jednotné okraje kolem obsahu.
* CSS aplikované, jako by stránka byla tištěna (díky `setMediaType("print")`).

![Příklad výstupu převodu HTML do PDF](https://example.com/convert-html-to-pdf-output.png "příklad výstupu převodu html do pdf")

*Alt text obrázku obsahuje primární klíčové slovo pro SEO.*

## Běžné okrajové případy a jak je řešit

| Problém | Příznak | Řešení |
|---------|---------|--------|
| **Missing CSS** | Text vypadá obyčejně, chybí fonty nebo barvy. | Ujistěte se, že je nastaveno `pdfOptions.setMediaType("print")` a že váš HTML odkazuje na stylopis s absolutní cestou nebo vložený CSS inline. |
| **Large Images Cut Off** | Obrázky jsou oříznuty na okrajích stránky. | Zmenšete obrázky v HTML nebo nastavte `pdfOptions.setImageResolution(300)` pro zvýšení DPI, poté upravte okraje. |
| **Unicode Characters Not Rendered** | Speciální symboly se zobrazují jako čtverečky. | Přidejte font, který podporuje dané znaky, a odkažte na něj ve vašem CSS (`@font-face`). |
| **Performance Lag on Huge Docs** | Konverze trvá >30 sekund. | Použijte `pdfOptions.setEnableThreading(true)` (pokud je podporováno) nebo rozdělte HTML na menší úseky a později je sloučte do PDF. |

## Kompletní funkční příklad (vše dohromady)

Zde je celý soubor, který můžete vložit do nového projektu. Nahraďte `YOUR_DIRECTORY` skutečnou cestou ke složce na vašem počítači.

```java
import com.aspose.html.*;
import com.aspose.html.converters.*;
import com.aspose.html.converters.pdf.*;

public class PdfConversionAdvanced {
    public static void main(String[] args) throws Exception {

        // Step 1: Source HTML location
        String inputHtmlPath = "C:/pdf-demo/input.html";

        // Step 2: Configure PDF options – custom size and margins
        PdfSaveOptions pdfOptions = new PdfSaveOptions();
        pdfOptions.setPageWidth(420);   // custom pdf page width (A5)
        pdfOptions.setPageHeight(595);  // custom pdf page height (A5)

        // Set margins – 10 mm ≈ 28.35 pt
        pdfOptions.setMarginTop(28.35);
        pdfOptions.setMarginBottom(28.35);
        pdfOptions.setMarginLeft(28.35);
        pdfOptions.setMarginRight(28.35);

        // Ensure print CSS is used
        pdfOptions.setMediaType("print");

        // Step 3: Destination PDF file
        String outputPdfPath = "C:/pdf-demo/output.pdf";

        // Step 4: Perform conversion
        Converter.convert(inputHtmlPath, outputPdfPath, pdfOptions);

        // Step 5: Confirmation
        System.out.println("PDF created with custom layout at " + outputPdfPath);
    }
}
```

Running this program generates `output.pdf` with the exact dimensions and margins you specified, giving you a

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}