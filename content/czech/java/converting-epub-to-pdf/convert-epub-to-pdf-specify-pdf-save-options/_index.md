---
title: Určení možností uložení PDF pro EPUB do PDF
linktitle: Určení možností uložení PDF pro EPUB do PDF
second_title: Java HTML zpracování s Aspose.HTML
description: Naučte se převádět EPUB do PDF v Javě pomocí Aspose.HTML, výkonné knihovny pro manipulaci s HTML.
type: docs
weight: 12
url: /cs/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
---

## Úvod

Aspose.HTML for Java je výkonný nástroj pro práci s dokumenty HTML a EPUB. V tomto podrobném průvodci vás provedeme procesem převodu souboru EPUB do PDF pomocí Aspose.HTML for Java. Ať už jste zkušený vývojář nebo teprve začínáte, tento tutoriál vám poskytne znalosti a dovednosti potřebné k efektivnímu provádění tohoto úkolu.

## Předpoklady

Než začneme, ujistěte se, že máte splněny následující předpoklady:

- Vývojové prostředí Java: Ve vašem systému musíte mít nastavené vývojové prostředí Java.

-  Aspose.HTML for Java: Stáhněte a nainstalujte knihovnu Aspose.HTML for Java. Knihovnu a související dokumentaci najdete na[webová stránka](https://releases.aspose.com/html/java/).

- Soubor EPUB: Budete potřebovat soubor EPUB, který chcete převést do PDF.

Nyní se pojďme ponořit do podrobného průvodce převodem EPUB do PDF pomocí Aspose.HTML pro Java.

## Krok 1: Otevřete soubor EPUB

 Chcete-li začít, otevřete existující soubor EPUB ke čtení. Můžete použít a`FileInputStream` dosáhnout toho. Zde je kód pro tento krok:

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Zde bude váš kód pro další kroky.
}
```

## Krok 2: Definujte možnosti uložení PDF

 Vytvořte instanci`PdfSaveOptions` s vlastní velikostí stránky a barvou pozadí. Nastavení stránky můžete nakonfigurovat podle svých požadavků. Můžete to udělat takto:

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

## Krok 3: Převeďte EPUB do PDF

 Nyní zavolejte`ConvertEPUB` způsob převodu souboru EPUB do formátu PDF. Určete vstupní proud, možnosti uložení PDF a výstupní umístění. Zde je návod, jak se to dělá:

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

Gratulujeme! Úspěšně jste převedli soubor EPUB do PDF pomocí Aspose.HTML pro Java. Nyní máte přístup k převedenému souboru PDF v zadaném výstupním umístění.

## Kompletní zdrojový kód
```java
Specifying PDF Save Options for EPUB to PDF
        // Otevřete existující soubor EPUB ke čtení.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Vytvořte instanci PdfSaveOptions s vlastní velikostí stránky a barvou pozadí.
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
            // Pro převod EPUB do PDF zavolejte metodu ConvertEPUB.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```


## Závěr

tomto tutoriálu jsme se naučili, jak používat Aspose.HTML pro Java k převodu souborů EPUB do formátu PDF. Tato všestranná knihovna poskytuje vývojářům výkonné nástroje pro manipulaci s dokumenty. Podle kroků uvedených v této příručce můžete bez problémů integrovat převod EPUB do PDF do svých aplikací Java.

## Často kladené otázky (FAQ)

### Je Aspose.HTML for Java bezplatná knihovna?
 Aspose.HTML for Java je komerční knihovna, ale můžete z ní získat bezplatnou zkušební verzi[webová stránka](https://releases.aspose.com/).

### Jaké formáty EPUB jsou podporovány pro převod?
Aspose.HTML for Java podporuje konverzi různých formátů EPUB, což zajišťuje kompatibilitu s většinou dokumentů EPUB.

### Mohu dále upravit výstup PDF?
 Ano, výstup PDF můžete upravit úpravou nastavení stránky, barvy pozadí a dalších nastavení v`PdfSaveOptions`.

### Existují nějaká omezení zkušební verze Aspose.HTML pro Javu?
Zkušební verze může mít určitá omezení, proto se doporučuje podívat se na podrobnosti v dokumentaci.

### Kde mohu získat podporu pro Aspose.HTML pro Java?
Můžete najít odpovědi na své otázky a hledat podporu na[Fórum Aspose.HTML](https://forum.aspose.com/).
