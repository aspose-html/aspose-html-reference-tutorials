---
date: 2026-01-02
description: Naučte se, jak v Javě převést EPUB na PDF pomocí Aspose.HTML a nastavit
  vlastní velikost stránky PDF a další možnosti ukládání PDF.
linktitle: Specifying PDF Save Options for EPUB to PDF
second_title: Java HTML Processing with Aspose.HTML
title: 'Vlastní velikost stránky PDF: Specifikace možností uložení PDF pro EPUB do
  PDF'
url: /cs/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vlastní velikost stránky PDF: Specifikace možností uložení PDF pro konverzi EPUB na PDF

## Úvod

Aspose.HTML for Java usnadňuje **konverzi EPUB do PDF** a poskytuje vám plnou kontrolu nad výstupem, včetně nastavení **vlastní velikosti stránky PDF**. V tomto krok‑za‑krokem průvodci projdeme vše, co potřebujete—od přípravy prostředí až po úpravu `PdfSaveOptions`, aby vygenerované PDF odpovídalo přesným rozměrům stránky, které požadujete. Ať už budujete publikační řetězec, e‑learning platformu, nebo jen potřebujete automatizovat konverzi dokumentů, najdete zde užitečné techniky.

## Rychlé odpovědi
- **What is the primary purpose of this tutorial?** Převést soubor EPUB do PDF a aplikovat vlastní velikost stránky PDF.  
- **Which library is used?** Aspose.HTML for Java.  
- **Do I need a license?** Je k dispozici bezplatná zkušební verze; pro produkční nasazení je vyžadována komerční licence.  
- **Can I change background color?** Ano, pomocí `PdfSaveOptions`.  
- **Is Java 8+ supported?** Ano—jakékoli moderní prostředí Java funguje.

## Co je vlastní velikost stránky PDF?

Vlastní velikost stránky PDF vám umožňuje definovat přesnou šířku a výšku každé stránky ve výstupním PDF, místo spoléhaní se na standardní velikosti jako A4 nebo Letter. To je zvláště užitečné pro e‑knihy, letáky nebo jakýkoli scénář, kde vizuální rozvržení musí odpovídat konkrétnímu návrhu.

## Proč použít Aspose.HTML pro konverzi EPUB do PDF?

- **High fidelity:** Zachovává složité rozvržení, písma a obrázky.  
- **Fine‑grained control:** Umožňuje nastavit velikost stránky, pozadí, okraje a další pomocí `PdfSaveOptions`.  
- **Cross‑platform:** Funguje na Windows, Linux a macOS se stejným Java kódem.  
- **Performance:** Optimalizovaný renderovací engine pro rychlé konverze.

## Požadavky

Předtím, než začneme, ujistěte se, že máte:

- **Java Development Environment:** Nainstalovaný a nakonfigurovaný JDK 8 nebo novější.  
- **Aspose.HTML for Java:** Stáhněte nejnovější JAR z [webu](https://releases.aspose.com/html/java/).  
- **EPUB File:** Dokument `.epub`, který chcete převést.  

Nyní, když je vše připraveno, ponořme se do skutečných kroků konverze.

## Krok 1: Otevřete soubor EPUB

Nejprve musíme otevřít soubor EPUB pomocí `FileInputStream`. Tento stream bude později předán konvertoru.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

## Krok 2: Definujte možnosti uložení PDF

Zde nastavíme **vlastní velikost stránky PDF** a volitelnou barvu pozadí. Upravit hodnoty v pixelech tak, aby odpovídaly požadovaným rozměrům.

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

### Tip:
- **Pixels vs. Points:** `Length.fromPixels` převádí pixely obrazovky na PDF body (1 bod = 1/72 palce). Vyberte hodnoty, které odpovídají požadované konečné tištěné velikosti.

## Krok 3: Převod EPUB do PDF

S připraveným vstupním streamem a vlastními možnostmi zavolejte konvertor. Výstupní PDF bude uloženo na zadané místo.

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

## Kompletní zdrojový kód

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
| **PDF stránky jsou prázdné** | Vstupní stream byl uzavřen před konverzí | Udržujte blok `try‑with‑resources` otevřený až po volání `convertEPUB`. |
| **Nesprávné rozměry stránky** | Použití pixelů, které neodpovídají požadované tiskové velikosti | Převést požadované palce na body (`1 inch = 72 points`) a poté na pixely pomocí `Length.fromPixels`. |
| **Chybějící písma** | Písma nejsou vložena v EPUB | Ujistěte se, že písma jsou zabalená v EPUB nebo je nainstalujte na hostitelském stroji. |

## Často kladené otázky (FAQ)

### Je Aspose.HTML pro Java zdarma?
Aspose.HTML pro Java je komerční knihovna, ale můžete získat bezplatnou zkušební verzi na jejich [webu](https://releases.aspose.com/).

### Jaké formáty EPUB jsou podporovány pro konverzi?
Aspose.HTML pro Java podporuje konverzi různých formátů EPUB, což zajišťuje kompatibilitu s většinou EPUB dokumentů.

### Mohu dále přizpůsobit výstup PDF?
Ano, můžete přizpůsobit výstup PDF úpravou nastavení stránky, barvy pozadí a dalších nastavení v `PdfSaveOptions`.

### Existují nějaká omezení zkušební verze Aspose.HTML pro Java?
Zkušební verze může mít některá omezení, proto je doporučeno zkontrolovat dokumentaci pro podrobnosti.

### Kde mohu získat podporu pro Aspose.HTML pro Java?
Odpovědi na své otázky a podporu můžete najít na [fóru Aspose.HTML](https://forum.aspose.com/).

---

**Poslední aktualizace:** 2026-01-02  
**Testováno s:** Aspose.HTML for Java 24.11 (nejnovější v době psaní)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}