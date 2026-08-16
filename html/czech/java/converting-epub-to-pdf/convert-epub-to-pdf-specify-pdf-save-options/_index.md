---
date: 2026-05-30
description: Zjistěte, jak převést EPUB na PDF v Javě pomocí Aspose.HTML a nastavit
  vlastní velikost stránky PDF a další možnosti uložení PDF.
keywords:
- custom pdf page size
- convert epub to pdf
- change pdf background color
- specify pdf page dimensions
- aspose.html java
linktitle: Specifikace možností uložení PDF pro EPUB na PDF
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  headline: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  type: TechArticle
- description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  name: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  steps:
  - name: Open the EPUB File
    text: First, create a `FileInputStream` that points to your source `.epub`. Keeping
      the stream open until the conversion finishes prevents “blank page” errors.
  - name: Define PDF Save Options
    text: '`PdfSaveOptions` is Aspose.HTML''s configuration class that controls PDF
      output settings such as page size, background color, and margins. `Length.fromPixels`
      converts screen pixels to PDF points (1 point = 1/72 inch), allowing you to
      specify dimensions in familiar pixel units.'
  - name: Convert EPUB to PDF
    text: With the input stream and custom options ready, invoke the converter. The
      output PDF will be saved to the location you specify, preserving the exact page
      dimensions you defined. `PdfSaveOptions.setEnableParallelProcessing` is a method
      that enables parallel processing of pages during PDF conversion.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a commercial library, but you can obtain a free
      trial version from their [website](https://releases.aspose.com/).
    question: Is Aspose.HTML for Java a free library?
  - answer: Aspose.HTML for Java supports EPUB 2.0, EPUB 3.0, and EPUB 3.1, handling
      re‑flowable and fixed‑layout books with full CSS support.
    question: What EPUB formats are supported for conversion?
  - answer: Yes, you can customize the PDF output by adjusting the page setup, background
      color, compression level, and other settings in the `PdfSaveOptions`.
    question: Can I customize the PDF output further?
  - answer: The trial version may add a watermark to the first few pages and limits
      the maximum file size to 10 MB; purchase a license to remove these restrictions.
    question: Are there any limitations to the trial version of Aspose.HTML for Java?
  - answer: You can find answers to your questions and seek support on the [Aspose.HTML
      forum](https://forum.aspose.com/).
    question: Where can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: Vlastní velikost stránky PDF – Specifikace možností uložení PDF pro EPUB na
  PDF
url: /cs/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vlastní velikost stránky PDF: Specifikace možností uložení PDF pro převod EPUB na PDF

## Úvod

Aspose.HTML for Java usnadňuje **převod EPUB na PDF** a dává vám plnou kontrolu nad výstupem, včetně nastavení **vlastní velikosti stránky PDF**. V tomto krok‑za‑krokem průvodci projdeme vše, co potřebujete—od přípravy prostředí až po ladění `PdfSaveOptions`, aby vygenerované PDF odpovídalo přesným rozměrům stránky, které požadujete. Ať už budujete publikační pipeline, e‑learning platformu, nebo jen potřebujete automatizovat konverzi dokumentů, najdete zde užitečné techniky.

## Rychlé odpovědi
- **Jaký je hlavní cíl tohoto tutoriálu?** Převést soubor EPUB na PDF a použít vlastní velikost stránky PDF.  
- **Která knihovna je použita?** Aspose.HTML for Java.  
- **Potřebuji licenci?** K dispozici je bezplatná zkušební verze; pro produkční nasazení je vyžadována komerční licence.  
- **Mohu změnit barvu pozadí?** Ano, pomocí `PdfSaveOptions`.  
- **Je podporováno Java 8+?** Rozhodně—funguje na jakémkoli moderním Java runtime.

## Co je vlastní velikost stránky PDF?

Vlastní velikost stránky PDF vám umožňuje definovat přesnou šířku a výšku každé stránky ve výstupním PDF, místo aby se spoléhalo na standardní formáty jako A4 nebo Letter.  
Rozměry můžete nastavit v bodech (1 bod = 1/72 palce) nebo převést z pixelů, což vám dává pixel‑dokonalou kontrolu nad finálním rozvržením. To je ideální pro e‑knihy, letáky nebo jakýkoli design, který musí odpovídat předdefinovanému formátu bez ručního post‑processingu.

## Proč použít Aspose.HTML pro převod EPUB na PDF?

Aspose.HTML převádí EPUB na PDF během dvou řádků kódu a zachovává složité rozvržení, vložená písma a vysoce‑rozlišovací obrázky. Podporuje **více než 50 vstupních a výstupních formátů**, dokáže renderovat PDF až **2 000 stránek** bez načítání celého souboru do paměti a běží na Windows, Linuxu i macOS s identickými výsledky. Knihovna také nabízí podrobné možnosti uložení PDF, které vám umožní ladit velikost stránky, barvu pozadí, okraje a nastavení komprese—vše z Java.

## Požadavky
- **Vývojové prostředí Java:** Nainstalovaný a nakonfigurovaný JDK 8 nebo novější.  
- **Aspose.HTML for Java:** Stáhněte si nejnovější JAR ze [stránky](https://releases.aspose.com/html/java/).  
- **Soubor EPUB:** Dokument `.epub`, který chcete převést.  

Nyní, když je vše připraveno, ponořme se do samotných kroků převodu.

## Jak převést EPUB na PDF s vlastní velikostí stránky?

`FileInputStream` je třída Java, která čte surová data ze souboru.  
`PdfSaveOptions` je třída v Aspose.HTML, která konfiguruje nastavení výstupu PDF, jako je velikost stránky a barva pozadí.  
Načtěte svůj EPUB pomocí `FileInputStream`, nastavte `PdfSaveOptions` tak, aby specifikovaly přesné rozměry stránky, a zavolejte konvertor. Následující tříkrokový postup provádí konverzi během méně než minuty pro typické velikosti e‑knih a škáluje na větší kolekce s minimálními úpravami kódu.

### Krok 1: Otevřete soubor EPUB

Nejprve vytvořte `FileInputStream`, který ukazuje na váš zdrojový `.epub`. Držení streamu otevřeného až do dokončení konverze zabraňuje chybám „prázdná stránka“.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

### Krok 2: Definujte možnosti uložení PDF

`PdfSaveOptions` je konfigurační třída Aspose.HTML, která řídí nastavení výstupu PDF, jako je velikost stránky, barva pozadí a okraje.  
`Length.fromPixels` převádí obrazovkové pixely na body PDF (1 bod = 1/72 palce), což vám umožní zadat rozměry v dobře známých jednotkách pixelů.

```java
com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
anyPage.setSize(new com.aspose.html.drawing.Size(
    com.aspose.html.drawing.Length.fromPixels(3000),
    com.aspose.html.drawing.Length.fromPixels(1000))
);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
```

#### Tip pro profesionály:
- **Pixely vs. Body:** `Length.fromPixels` převádí obrazovkové pixely na body PDF (1 bod = 1/72 palce). Zvolte hodnoty, které odpovídají finální tištěné velikosti, kterou potřebujete.

### Krok 3: Převést EPUB na PDF

S otevřeným vstupním streamem a vlastními možnostmi zavolejte konvertor. Výstupní PDF bude uloženo na vámi zadané místo a zachová přesné rozměry stránky, které jste definovali.

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

`PdfSaveOptions.setEnableParallelProcessing` je metoda, která umožňuje paralelní zpracování stránek během konverze PDF.

## Kompletní zdrojový kód

Celý, spustitelný příklad kombinuje výše uvedené tři kroky do jedné Java třídy. Nahraďte zástupné cesty vlastními umístěními souborů.

```java
Specifying PDF Save Options for EPUB to PDF
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of the PdfSaveOptions with a custom page-size and a background-color.
            com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
            com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
            com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
            anyPage.setSize(new com.aspose.html.drawing.Size(
                    com.aspose.html.drawing.Length.fromPixels(3000),
                    com.aspose.html.drawing.Length.fromPixels(1000))
            );
            pageSetup.setAnyPage(anyPage);
            options.setPageSetup(pageSetup);
            options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
            // Call the ConvertEPUB method to convert the EPUB to PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```

## Časté problémy a řešení

| Problém | Příčina | Řešení |
|-------|-------|-----|
| **PDF stránky jsou prázdné** | Vstupní stream byl uzavřen před konverzí | Nechte blok `try‑with‑resources` otevřený až po volání `convertEPUB`. |
| **Nesprávné rozměry stránky** | Použité pixely neodpovídají požadované tiskové velikosti | Převěďte požadované palce na body (`1 palec = 72 bodů`) a poté na pixely pomocí `Length.fromPixels`. |
| **Chybějící písma** | Písma nejsou vložena v EPUB | Ujistěte se, že písma jsou zabalená v EPUB nebo je nainstalujte na hostitelském počítači. |
| **Zpomalení výkonu u velkých knih** | Renderování každé stránky sekvenčně | Povolit vícevláknové renderování pomocí `PdfSaveOptions.setEnableParallelProcessing(true)` pro rychlejší zpracování EPUB s více než 500 stránkami. |

## Často kladené otázky (FAQ)

**Q: Je Aspose.HTML pro Java volná knihovna?**  
A: Aspose.HTML for Java je komerční knihovna, ale můžete získat bezplatnou zkušební verzi na jejich [webu](https://releases.aspose.com/).

**Q: Jaké formáty EPUB jsou podporovány pro konverzi?**  
A: Aspose.HTML for Java podporuje EPUB 2.0, EPUB 3.0 a EPUB 3.1, zpracovává reflow‑able i fixed‑layout knihy s plnou podporou CSS.

**Q: Mohu dále přizpůsobit výstup PDF?**  
A: Ano, můžete upravit nastavení PDF změnou nastavení stránky, barvy pozadí, úrovně komprese a dalších parametrů v `PdfSaveOptions`.

**Q: Existují nějaká omezení zkušební verze Aspose.HTML pro Java?**  
A: Zkušební verze může přidat vodoznak na první několik stránek a omezuje maximální velikost souboru na 10 MB; zakoupením licence tato omezení odstraníte.

**Q: Kde mohu získat podporu pro Aspose.HTML for Java?**  
A: Odpovědi na otázky a podporu najdete na [fóru Aspose.HTML](https://forum.aspose.com/).

---

**Poslední aktualizace:** 2026-05-30  
**Testováno s:** Aspose.HTML for Java 24.11 (nejnovější v době psaní)  
**Autor:** Aspose

## Související tutoriály

- [Upravit velikost stránky PDF pomocí Aspose.HTML for Java](/html/java/advanced-usage/adjust-pdf-page-size/)
- [Jak převést EPUB na PDF pomocí Java – s využitím Aspose.HTML](/html/java/conversion-epub-to-image-and-pdf/convert-epub-to-pdf/)
- [Převod EPUB na PDF a obrázky s Aspose.HTML for Java](/html/java/conversion-epub-to-image-and-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}