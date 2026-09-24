---
category: general
date: 2026-01-04
description: Vytvořte PDF vlastní velikosti z HTML v Javě pomocí Aspose.HTML – naučte
  se nastavit velikost stránky a zvýšit DPI při převodu HTML na PDF.
draft: false
keywords:
- create pdf custom size
- convert html to pdf
- html to pdf java
- set pdf page size
- increase pdf dpi
language: cs
og_description: Vytvořte PDF vlastní velikosti z HTML v Javě s Aspose.HTML. Nastavte
  velikost stránky, zvýšte DPI a ovládejte převod HTML do PDF.
og_title: Vytvořte PDF s vlastní velikostí z HTML v Javě – kompletní tutoriál
tags:
- Java
- PDF
- Aspose
- HTML conversion
title: Vytvořte PDF s vlastní velikostí z HTML v Javě – Kompletní průvodce
url: /cs/java/conversion-html-to-other-formats/create-pdf-custom-size-from-html-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření PDF s vlastní velikostí z HTML v Javě – Kompletní průvodce

Už jste někdy potřebovali **vytvořit PDF s vlastní velikostí** ze zdroje HTML, ale nevedeli ste, jak ovládat rozměry nebo ostrost obrázků? Nejste v tom sami – mnoho vývojářů narazí na tento problém, když výchozí výstup A4 vypadá špatně pro jejich šablony faktur nebo marketingové letáky.  

V tomto tutoriálu projdeme **kompletní, spustitelný příklad**, který ukazuje, jak **převést HTML do PDF** a zároveň **nastavit velikost stránky PDF** a **zvýšit DPI PDF** pro ostřejší grafiku. Na konci budete mít připravenou třídu v Javě, kterou můžete přizpůsobit libovolnému projektu vyžadujícímu PDF s vlastní velikostí.

## Co budete potřebovat

- **Java 17** nebo novější (kód používá moderní syntaxi `var`, ale můžete jej zpětně přenést, pokud je potřeba).  
- Knihovna **Aspose.HTML for Java** – doporučujeme verzi 23.9 nebo novější.  
- HTML soubor, který chcete převést do PDF (budeme ho nazývat `input.html`).  
- Trochu pohodlí při práci v IDE (IntelliJ IDEA, Eclipse nebo VS Code jsou v pořádku).  

Žádné další závislosti nejsou potřeba; JAR soubory Aspose obsahují vše, co je nutné.

## Krok 1: Přidejte Aspose.HTML do svého projektu

Pokud používáte Maven, vložte následující úryvek do souboru `pom.xml`. Pro Gradle nebo čisté nastavení jen s JAR soubory platí stejné koordináty.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

> **Pro tip:** Aspose nabízí bezplatnou evaluační licenci, kterou můžete vložit jako soubor zdroje. Stačí umístit `Aspose.HTML.lic` do složky `src/main/resources` a knihovna ji automaticky načte.

## Krok 2: Vytvořte Java třídu pro konverzi

Níže je celý zdrojový soubor. Všimněte si, že každý řádek je okomentován, aby vysvětlil **proč** to děláme – ne jen **co** děláme.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfConversionOptions;
import com.aspose.html.rendering.PageSize;
import com.aspose.html.rendering.Unit;

/**
 * Demonstrates how to convert an HTML file to a PDF with a custom page size
 * and a higher DPI (dots per inch) for sharper images.
 *
 * Run this class from your IDE or via `java -cp <classpath> ConvertWithOptions`.
 */
public class ConvertWithOptions {
    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1: Prepare conversion options
        // -----------------------------------------------------------------
        PdfConversionOptions conversionOptions = new PdfConversionOptions();

        // Set the page size to A5 (148 mm × 210 mm) – you can change these numbers
        // to any dimensions you need, e.g., a custom flyer size.
        conversionOptions.setPageSize(new PageSize(Unit.MILLIMETERS, 148, 210));

        // Choose a higher resolution: 150 DPI gives noticeably sharper raster images.
        // The default is usually 96 DPI, which can look blurry on printed media.
        conversionOptions.setResolution(150);

        // -----------------------------------------------------------------
        // Step 2: Perform the conversion
        // -----------------------------------------------------------------
        // Replace "YOUR_DIRECTORY" with the actual folder where your files live.
        String inputHtml = "YOUR_DIRECTORY/input.html";
        String outputPdf = "YOUR_DIRECTORY/output.pdf";

        // The static convert method does the heavy lifting.
        Converter.convert(inputHtml, outputPdf, conversionOptions);

        // -----------------------------------------------------------------
        // Step 3: Confirmation
        // -----------------------------------------------------------------
        System.out.println("Custom conversion done. PDF created at: " + outputPdf);
    }
}
```

### Proč jsou tato nastavení důležitá

- **`setPageSize`** – Ve výchozím nastavení Aspose používá A4 (210 mm × 297 mm). Změna vám umožní přizpůsobit obsah brožuře, účtenky nebo jakémukoli jinému formátu.  
- **`setResolution`** – DPI ovlivňuje rasterizaci CSS pozadí, SVG a dokonce i vykreslování textu, když je PDF zobrazováno na obrazovce. Vyšší DPI → větší soubor, ale ostřejší výstup – ideální pro tiskové materiály.  

## Krok 3: Spusťte kód a ověřte výstup

1. Zkompilujte třídu:

   ```bash
   javac -cp "path/to/aspose-html.jar" ConvertWithOptions.java
   ```

2. Spusťte ji:

   ```bash
   java -cp ".:path/to/aspose-html.jar" ConvertWithOptions
   ```

3. Otevřete `output.pdf` v libovolném prohlížeči PDF. Měli byste vidět HTML vykreslené na **stránce velikosti A5** s výrazně ostřejšími obrázky.

> **Co když potřebuji orientaci na šířku?**  
> Stačí prohozit hodnoty šířky a výšky při vytváření `PageSize`, nebo použít pomocníka `PageSize.LANDSCAPE`, pokud dáváte přednost deklarativnějšímu přístupu.

## Krok 4: Běžné variace a okrajové případy

| Scénář | Jak upravit kód |
|----------|-----------------------|
| **Různé jednotky (palce, body)** | Nahraďte `Unit.MILLIMETERS` za `Unit.INCHES` nebo `Unit.POINTS`. |
| **Více HTML souborů do jednoho PDF** | Vytvořte jednou objekt `PdfConversionOptions`, pak opakovaně volajte `Converter.convert`, přičemž každý výstup přidáte do stejné instance `PdfDocument`. |
| **Dynamická velikost stránky pro každý dokument** | Vypočítejte šířku/výšku za běhu (např. na základě JSON konfigurace) před voláním `setPageSize`. |
| **Běh ve webové službě** | Zabalte logiku konverze do servletu nebo Spring kontroleru, streamujte PDF bajty zpět jako `application/pdf`. |
| **Prostředí s omezenou pamětí** | Použijte `PdfConversionOptions.setMemoryLimit(...)` k omezení využití haldy; Aspose v případě potřeby přepíše na disk. |

## Krok 5: Tipy pro řešení problémů

- **Prázdné stránky** – Ujistěte se, že vaše HTML obsahuje element `<body>` a že všechny externí CSS/JS zdroje jsou přístupné z pracovního adresáře JVM.  
- **Chybějící fonty** – Nainstalujte požadované fonty na server nebo je vložte pomocí `PdfConversionOptions.setFontEmbeddingMode(...)`.  
- **Neočekávané DPI** – Zkontrolujte, že v pozdější fázi pipeline (např. pomocí PDF post‑processoru) nepřepisujete rozlišení.  

## Vizuální reference

Níže je rychlý snímek vygenerovaného PDF (A5 na výšku). Alt text úmyslně obsahuje hlavní klíčové slovo pro SEO účely.

![Create PDF custom size example](https://example.com/images/create-pdf-custom-size.png "Create PDF custom size example")

## Shrnutí: Co jsme dosáhli

**Vytvořili jsme Java program, který převádí HTML do PDF**, explicitně **nastavuje vlastní velikost stránky** a **zvyšuje DPI** pro ostřejší výstup. Řešení je samostatné, používá pouze Aspose.HTML a lze jej vložit do libovolného Maven‑based projektu.

## Další kroky a související témata

- **Dávkové zpracování:** Procházet adresář s HTML soubory a sloučit je do jednoho PDF.  
- **Pokročilé stylování:** Použít CSS pravidla `@page` pro kontrolu okrajů, záhlaví a zápatí.  
- **Bezpečnostní úvahy:** Očistit uživatelem poskytnuté HTML před konverzí, aby se zabránilo skriptovacím útokům.  

Pokud máte zájem o hlubší manipulaci s PDF – například přidávání záložek, šifrováníu nebo vkládání vodoznaků – podívejte se na knihovnu **PDF for Java** od Aspose. Skvěle doplňuje tok konverze HTML, který jsme právě vytvořili.

Šťastné programování a ať jsou vaše PDF vždy přesně takové, jaké potřebujete!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}