---
category: general
date: 2026-03-26
description: Vytvořte PDF vlastní velikosti z HTML pomocí Aspose.HTML pro Java. Naučte
  se, jak převést HTML do PDF a nastavit velikost stránky PDF během několika kroků.
draft: false
keywords:
- create pdf custom size
- convert html to pdf
- change pdf page size
- generate pdf from html
- set pdf page size
language: cs
og_description: Vytvořte PDF vlastní velikosti z HTML pomocí Aspose. Tento průvodce
  vám ukáže, jak převést HTML do PDF, změnit velikost stránky PDF a nastavit velikost
  stránky PDF snadno.
og_title: Vytvořte PDF vlastní velikosti – rychlý průvodce převodem HTML do PDF
tags:
- aspose
- java
- pdf
- html
title: Vytvořte PDF vlastní velikosti – Převod HTML do PDF pomocí Aspose
url: /cs/java/conversion-html-to-other-formats/create-pdf-custom-size-convert-html-to-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření PDF vlastní velikosti – převod HTML na PDF pomocí Aspose

Už jste někdy potřebovali **vytvořit PDF vlastní velikosti** z HTML souboru? V tomto tutoriálu vám ukážeme, jak **převést HTML na PDF** a nastavit velikost stránky PDF pomocí Aspose.HTML pro Java.  

Pokud vytváříte faktury, zprávy nebo e‑knihy, získání přesných rozměrů stránky je důležité – jinak bude váš rozvrh nesprávně vycentrovaný nebo oříznutý.  

Provedeme vás každým krokem, od načtení zdrojového HTML po úpravu okrajů, a skončíme připraveným PDF. Žádné vágní odkazy, jen kompletní, spustitelný příklad, který můžete dnes zkopírovat a vložit.

## Co budete potřebovat

- **Java 17** (nebo jakýkoli aktuální JDK).  
- **Aspose.HTML for Java** JAR soubory – můžete získat nejnovější verzi z Maven repozitáře nebo webu Aspose.  
- Jednoduchý soubor `input.html` umístěný ve složce, kterou ovládáte.  
- IDE nebo textový editor dle vašeho výběru; obvykle programuji v IntelliJ IDEA, ale Eclipse také dobře funguje.

Mít tyto předpoklady znamená, že se během práce nesetkáte s chybami „class not found“.  

Nyní se ponořme.

![Create PDF custom size example](/images/create-pdf-custom-size.png "Screenshot showing a PDF generated with custom page size and margins – create pdf custom size")

## Vytvoření PDF vlastní velikosti – Hlavní kroky

Níže je celý Java program, který získáte. Klidně jej zkopírujte do souboru s názvem `ConvertHtmlToPdfCustomPage.java` a spusťte po přidání Aspose závislostí do vašeho projektu.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.PdfConversionOptions;
import com.aspose.html.saving.PageSize;
import com.aspose.html.saving.Margin;

public class ConvertHtmlToPdfCustomPage {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the source HTML document
        HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/input.html");

        // Step 2: Set up PDF conversion options
        PdfConversionOptions pdfOptions = new PdfConversionOptions();
        pdfOptions.setPageSize(PageSize.A4); // Choose page size (A4, Letter, etc.)
        pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Portrait); // Portrait or Landscape
        pdfOptions.setMargins(new Margin(20, 20, 20, 20)); // Margins: left, top, right, bottom (points)

        // Step 3: Convert the HTML document to a PDF file with the custom settings
        Converter.convertHTML(htmlDoc, "YOUR_DIRECTORY/custom_page.pdf", pdfOptions);

        // Step 4: Inform the user that the PDF has been created
        System.out.println("PDF generated with custom page size and margins.");
    }
}
```

### Krok 1 – Převod HTML na PDF: Načtení dokumentu

První věc, kterou uděláme, je **načíst HTML**, které chceme převést na PDF.  
`HTMLDocument` načte soubor, vyřeší relativní odkazy a vytvoří DOM, který Aspose může vykreslit.  

> **Proč je to důležité:** Pokud HTML odkazuje na CSS nebo obrázky, Aspose je načte relativně k cestě souboru. Použití absolutní cesty (`YOUR_DIRECTORY/input.html`) zabraňuje překvapením typu „file not found“.

### Krok 2 – Změna velikosti stránky PDF: Konfigurace možností

Zde vytvoříme objekt `PdfConversionOptions`.  
- `setPageSize(PageSize.A4)` říká Aspose použít standardní rozměry A4 (210 × 297 mm).  
- `setPageOrientation(...)` otočí stránku, pokud potřebujete orientaci na šířku.  
- `setMargins(new Margin(20, 20, 20, 20))` nastaví okraj 20 bodů na každé straně.

Můžete nahradit `PageSize.A4` za `PageSize.LETTER` nebo dokonce **vlastní velikost** předáním objektu `SizeF`, např.:

```java
pdfOptions.setPageSize(new SizeF(500, 800)); // width, height in points
```

> **Tip:** Jeden bod odpovídá 1/72 palce. Pokud počítáte v milimetrech, vynásobte 2.83465 pro získání bodů.

### Krok 3 – Generování PDF z HTML: Spuštění konverze

`Converter.convertHTML` provádí těžkou práci. Přijímá načtený `HTMLDocument`, výstupní cestu a možnosti, které jsme právě nakonfigurovali.  

Pokud chcete **nastavit velikost stránky PDF** dynamicky na základě obsahu, můžete před tímto krokem vypočítat požadované rozměry a podle toho upravit `pdfOptions`.

### Krok 4 – Ověření výsledku

Řádek `System.out.println` je volitelný, ale poskytuje rychlou zpětnou vazbu při spuštění programu z konzole. Po dokončení otevřete `custom_page.pdf` – měli byste vidět PDF formátu A4 na výšku s jednotnými okraji 20 bodů, přesně tak, jak jsme zadali.

## Převod HTML na PDF – Běžné varianty

### Použití streamu místo cesty k souboru

Někdy nemáte fyzický soubor; HTML může pocházet z databáze nebo API. V takovém případě zabalte řetězec do `ByteArrayInputStream`:

```java
String htmlContent = "<html><body><h1>Hello, PDF!</h1></body></html>";
HTMLDocument htmlDoc = new HTMLDocument(
        new ByteArrayInputStream(htmlContent.getBytes(StandardCharsets.UTF_8)),
        "http://example.com/");
```

Druhý argument je základní URL pro řešení relativních zdrojů.

### Změna orientace stránky

Pokud je vaše zpráva široká, přepněte na orientaci na šířku:

```java
pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Landscape);
```

### Jemné doladění okrajů

Okraje přijímají hodnoty s plovoucí desetinnou čárkou, takže můžete nastavit 0,5 pt pro velmi tenký okraj:

```java
pdfOptions.setMargins(new Margin(5.5, 10.2, 5.5, 10.2));
```

### Zpracování velkých HTML souborů

U velkých dokumentů zvažte povolení **paměťově úsporného streamování**:

```java
pdfOptions.setUseMemoryCache(true);
```

Tím se Aspose řekne, aby zapisoval mezilehlá data do dočasných souborů místo toho, aby vše drželo v RAM.

## Nastavení velikosti stránky PDF – Okrajové případy a úskalí

- **Missing Fonts:** Pokud vaše HTML používá vlastní font, který není nainstalován na serveru, PDF se vrátí k výchozímu. Vložte font pomocí `pdfOptions.getFontEmbeddingMode().setEmbeddingMode(EmbeddingMode.Always);`.  
- **Image Scaling:** Vysoce rozlišené obrázky mohou PDF nafouknout. Použijte `pdfOptions.setImageResolution(150);` pro zmenšení při zachování kvality.  
- **CSS Compatibility:** Ne všechny CSS vlastnosti jsou plně podporovány. Držte se standardních technik rozvržení (flexbox funguje, ale grid může mít nedostatky).  
- **Path Permissions:** Ujistěte se, že proces má právo zápisu do `YOUR_DIRECTORY`. Jinak bude vyhozena `IOException`.

## Očekávaný výstup

Spuštěním programu se vytvoří PDF, které vypadá takto (konceptuální ilustrace):

```
+---------------------------------------------------+
|                     Header                        |
|                                                   |
|   (HTML rendered content goes here)               |
|                                                   |
|                     Footer                        |
+---------------------------------------------------+
```

- Velikost stránky: **A4** (210 × 297 mm).  
- Orientace: **Portrait**.  
- Okraje: **20 pt** na každé straně.  

Otevřete soubor v libovolném PDF prohlížeči (Adobe Reader, Chrome atd.) pro ověření.

## Závěr

Nyní víte, jak **vytvořit PDF vlastní velikosti** ze zdroje HTML pomocí Aspose.HTML pro Java. Tutoriál pokryl celý proces: **převod HTML na PDF**, **změnu velikosti stránky PDF**, **nastavení velikosti stránky PDF** a **generování PDF z HTML** s vlastními okraji.  

Klidně experimentujte – vyměňte `PageSize.LETTER` za právnický formát, upravte okraje nebo vložte vlastní fonty. Dále můžete zkoumat **přidávání vodoznaků**, **šifrování PDF** nebo **hromadné zpracování více HTML souborů**. Všechny tyto témata staví na stejných základních konceptech, které jsme právě probrali.

Máte otázku ohledně konkrétního okrajového případu? Zanechte komentář níže a já vám pomohu s řešením. Šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}