---
category: general
date: 2026-04-12
description: Naučte se, jak nastavit velikost stránky PDF a vložit písma při převodu
  EPUB do PDF v Javě pomocí Aspose.HTML. Tento průvodce vás provede kompletním pracovním
  postupem převodu EPUB do PDF v Javě.
draft: false
keywords:
- set pdf page size
- embed fonts pdf
- convert epub to pdf
- java epub to pdf
- custom pdf page size
og_description: Naučte se, jak nastavit velikost stránky PDF a vložit písma při převodu
  EPUB na PDF v Javě s Aspose.HTML.
og_title: Nastavte velikost stránky PDF a vložte písma při převodu EPUB do PDF v Javě
tags:
- Java
- PDF
- EPUB
title: Nastavte velikost stránky PDF a vložte písma při převodu EPUB do PDF v Javě
url: /cs/java/converting-epub-to-pdf/how-to-embed-fonts-when-converting-epub-to-pdf-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nastavte velikost stránky PDF a vložte písma pro konverzi EPUB na PDF v Javě

Pokud potřebujete **nastavit velikost stránky PDF** při **konverzi EPUB na PDF** a zajistit, aby výsledný dokument vypadal přesně jako zdroj, jste na správném místě. V tomto tutoriálu projdeme kompletním, připraveným pro produkci Java příkladem, který ukazuje, jak **vložit písma do PDF**, vybrat **vlastní velikost stránky PDF** a spustit konverzi pomocí Aspose.HTML. Na konci budete mít připravený program, který pokaždé vytvoří věrný PDF.

## Rychlé odpovědi
- **Jaký je hlavní cíl?** Nastavit velikost stránky PDF a vložit písma při konverzi EPUB na PDF v Javě.  
- **Kterou knihovnu mám použít?** Aspose.HTML pro Javu (k dispozici bezplatná zkušební verze).  
- **Potřebuji licenci pro produkci?** Ano – licence odstraňuje vodotisk z hodnocení.  
- **Mohu použít vlastní velikost stránky?** Rozhodně – můžete zadat přesné rozměry nebo použít vestavěné výčty jako A4, LETTER atd.  
- **Jaká verze Javy je požadována?** Doporučuje se Java 17 nebo novější.

### Požadavky
- Nainstalována Java 17+.  
- Aspose.HTML pro Javu přidán do vašeho projektu (Maven, Gradle nebo ruční JAR).  
- EPUB soubor, který chcete převést.

> Pokud dáváte přednost Gradlu, stačí nahradit úryvek Mavenu ekvivalentními koordináty pro Gradle.

---

## Proč vložit písma do PDF?

Vložení písem uzamkne vizuální design zdrojového EPUB, takže PDF se vykreslí správně na jakémkoli zařízení – i když prohlížeč nemá nainstalované původní typy písma. Bez vložení se nadpisy mohou vrátit k výchozím písmům, jako je Arial, což rozbije rozvržení, na kterém jste tak tvrdě pracovali.

**Pro tip:** Pokud znáte přesná písma použitá v EPUB, nasměrujte Aspose na složku, která obsahuje tyto soubory `.ttf` nebo `.otf` pomocí `pdfOptions.setFontsFolder("path/to/fonts")`. To urychlí konverzi a sníží konečnou velikost souboru.

```java
// Configure PDF save options
PdfSaveOptions pdfOptions = new PdfSaveOptions();
pdfOptions.setEmbedFonts(true);               // <-- This line embeds all used fonts
```

---

## Jak převést EPUB na PDF v Javě – kompletní workflow

Níže je minimální, ale kompletní kód, který potřebujete. Pokrývá tři základní kroky: nalezení zdrojového EPUB, konfiguraci PDF možností (včetně **nastavení velikosti stránky PDF**) a vyvolání konverze.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfSaveOptions;

public class EpubToPdfDemo {

    public static void main(String[] args) throws Exception {
        // Step 1: Point to your source EPUB file
        String epubPath = "YOUR_DIRECTORY/input.epub";

        // Step 2: Set up PDF save options (embed fonts + page size)
        PdfSaveOptions pdfOptions = new PdfSaveOptions();
        pdfOptions.setEmbedFonts(true);                         // Embed fonts for accurate rendering
        pdfOptions.setPageSize(PdfSaveOptions.PageSize.LETTER); // Set PDF page size to Letter (8.5"x11")

        // Step 3: Perform the conversion
        String outputPdf = "YOUR_DIRECTORY/output.pdf";
        Converter.convert(epubPath, outputPdf, pdfOptions);

        System.out.println("Conversion complete! PDF saved to: " + outputPdf);
    }
}
```

### Co se děje pod kapotou?

1. **Zdrojový EPUB** – `epubPath` říká Aspose, kde má číst kontejner EPUB.  
2. **PDF možnosti** – `PdfSaveOptions` vám umožňuje zapnout/vypnout vložení písem (`setEmbedFonts`) a definovat rozměry stránky (`setPageSize`). Výčet `PageSize.LETTER` je užitečný pro US‑letter; můžete také zvolit `A4`, `A5` atd.  
3. **Volání konverze** – `Converter.convert` parsuje EPUB, vykresluje každou XHTML stránku na PDF stránku, aplikuje možnosti a zapíše výsledek.

Metoda pro stručnost hází obecnou `Exception`; v produkci byste zachytili konkrétní podtřídy (např. `IOException`, `FileNotFoundException`) a ošetřili je elegantně.

---

## Jak nastavit velikost stránky PDF pro výsledek

Výběr správné velikosti stránky ovlivňuje stránkování, škálování obrázků a rozvržení tisku. Aspose.HTML poskytuje pohodlný výčet, ale můžete také zadat vlastní velikost, pokud výchozí nevyhovují vašim potřebám.

```java
// Example: Custom size – 6" x 9"
pdfOptions.setPageSize(new PdfSaveOptions.PageSize(6.0, 9.0));
```

**Kdy byste potřebovali vlastní velikost?**  
Možná vytváříte kapesní e‑knihy, tisknutelný brožuru nebo zprávu, která má specifickou ořezovou velikost. API přijímá rozměry v palcích (nebo můžete převést z milimetrů), což vám dává plnou kontrolu.

## Kompletní funkční příklad (včetně Maven závislosti)

Pokud používáte Maven, přidejte následující závislost do vašeho `pom.xml`. Tím zajistíte, že třídy `Converter` a `PdfSaveOptions` jsou na classpath.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

**Plný zdrojový soubor (`EpubToPdfDemo.java`)**

```java
package com.example.epubtopdf;

import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfSaveOptions;

/**
 * Demonstrates how to embed fonts and set PDF page size while converting an EPUB file to PDF.
 * Run this class from your IDE or via `java -cp <classpath> com.example.epubtopdf.EpubToPdfDemo`.
 */
public class EpubToPdfDemo {

    public static void main(String[] args) {
        try {
            // -----------------------------------------------------------------
            // 1️⃣ Locate the EPUB file
            // -----------------------------------------------------------------
            String epubPath = "C:/Docs/input.epub";

            // -----------------------------------------------------------------
            // 2️⃣ Configure PDF options – embed fonts & choose page size
            // -----------------------------------------------------------------
            PdfSaveOptions pdfOptions = new PdfSaveOptions();
            pdfOptions.setEmbedFonts(true);                         // Embed every font used in the EPUB
            pdfOptions.setPageSize(PdfSaveOptions.PageSize.LETTER); // Letter size (8.5"x11")

            // -----------------------------------------------------------------
            // 3️⃣ Convert and save the PDF
            // -----------------------------------------------------------------
            String outputPdf = "C:/Docs/output.pdf";
            Converter.convert(epubPath, outputPdf, pdfOptions);

            System.out.println("✅ Success! PDF created at: " + outputPdf);
        } catch (Exception e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Očekávaný výstup

Spuštění programu vypíše potvrzovací řádek:

```
✅ Success! PDF created at: C:/Docs/output.pdf
```

Otevřete výsledné PDF v libovolném prohlížeči (Adobe Reader, Chrome atd.) a uvidíte:

* Všechny textové elementy zachovávají původní styl písma.  
* Rozměry stránky odpovídají zvolené velikosti **Letter** (nebo jakékoli vlastní velikosti, kterou nastavíte).  
* Obrázky, tabulky a hypertextové odkazy z EPUB jsou zachovány.

Pokud prozkoumáte vlastnosti PDF (Soubor → Vlastnosti → Písma), všimnete si, že každé písmo je uvedeno jako **Embedded Subset**, což potvrzuje, že volání `setEmbedFonts(true)` splnilo svůj úkol.

---

## Často kladené otázky

**Q: Co když můj EPUB používá vlastní písmo, které není nainstalováno na serveru?**  
A: Umístěte soubory `.ttf` nebo `.otf` do složky a nasměrujte Aspose na ni pomocí `pdfOptions.setFontsFolder("path/to/custom/fonts")`. Konvertor načte a vloží tato písma automaticky.

**Q: Mohu převést více EPUB souborů najednou?**  
A: Ano. Zabalte logiku konverze do smyčky, změňte `epubPath` a `outputPdf` pro každý soubor a případně spusťte smyčku paralelně pomocí `ExecutorService`, protože Aspose je thread‑safe.

**Q: Existuje limit velikosti pro vstupní EPUB?**  
A: Neexistuje pevný limit, ale velmi velké EPUB (stovky MB) mohou spotřebovat značnou paměť. Zvyšte haldu JVM (`-Xmx2g` nebo více) pro obrovské knihy.

**Q: Jak vypnout vkládání písem pro snížení velikosti PDF?**  
A: Zavolejte `pdfOptions.setEmbedFonts(false)`. PDF bude spoléhat na písma nainstalovaná v prohlížeči, což snižuje velikost souboru, ale může změnit vzhled.

**Q: Potřebuji licenci pro Aspose.HTML?**  
A: Bezplatná evaluační licence funguje pro testování, ale přidává vodotisk. Pro produkční použití zakupte licenci a načtěte ji pomocí `License license = new License(); license.setLicense("path/to/license.xml");`.

---

## Závěr

Nyní víte, **jak nastavit velikost stránky PDF** a **vložit písma do PDF**, když **převádíte EPUB na PDF** v Javě pomocí Aspose.HTML. Kompletní, spustitelný příklad výše by měl fungovat ihned – stačí nahradit zástupné cesty vlastními soubory.

Další kroky? Vyzkoušejte různé formáty stránek jako **A4** nebo vlastní velikost 6×9, prozkoumejte další `PdfSaveOptions` (komprese obrázků, PDF/A kompatibilita) nebo programově přidejte titulní stránku. Stejný vzor funguje i pro jiné zdrojové formáty (HTML, Markdown), protože Aspose.HTML je zpracovává jednotně.

Šťastné programování a ať vaše PDF vždy vypadají přesně tak, jak jste zamýšleli! 

![Jak vložit písma při konverzi PDF](https://example.com/images/embed-fonts.png "Jak vložit písma při konverzi PDF")

---

**Poslední aktualizace:** 2026-04-12  
**Testováno s:** Aspose.HTML for Java 23.10  
**Autor:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}