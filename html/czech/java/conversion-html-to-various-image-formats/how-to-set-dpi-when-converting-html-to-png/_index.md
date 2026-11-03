---
category: general
date: 2026-03-04
description: Naučte se, jak nastavit DPI při převodu HTML na PNG. Tento průvodce také
  zahrnuje export HTML jako PNG, uložení HTML jako PNG a generování PNG z HTML pomocí
  Aspose.HTML pro Javu.
draft: false
keywords:
- how to set dpi
- convert html to png
- export html as png
- save html as png
- generate png from html
language: cs
og_description: Jak nastavit DPI pro konverzi HTML na PNG, vysvětleno. Postupujte
  podle krok‑za‑krokem průvodce pro export HTML jako PNG, uložení HTML jako PNG a
  generování PNG z HTML.
og_title: Jak nastavit DPI při převodu HTML na PNG
tags:
- Aspose.HTML
- Java
- Image Conversion
title: Jak nastavit DPI při převodu HTML na PNG
url: /cs/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-html-to-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak nastavit DPI při konverzi HTML na PNG

Už jste se někdy zamysleli **jak nastavit DPI** pro rastrový obrázek, který generujete z webové stránky? Možná vytváříte nástroj pro reportování, službu pro miniatury nebo pipeline pro tiskové materiály – všechny tyto scénáře obvykle začínají HTML dokumentem, který má být převeden na vysoké rozlišení PNG.  

Dobrou zprávou je, že Aspose.HTML pro Java vám umožní snadno **převést HTML na PNG**, a DPI můžete ovládat jediným řádkem kódu. V tomto tutoriálu projdeme celý proces, od načtení vašeho HTML souboru až po export jako PNG při 300 DPI, a také se dotkneme souvisejících úkolů jako **export HTML as PNG**, **save HTML as PNG** a **generate PNG from HTML**.

## Co se naučíte

- Jak nakonfigurovat DPI (dots per inch) pro výstupní obrázek.
- Rozdíl mezi DPI, rozlišením a kvalitou komprese.
- Kompletní, spustitelný Java příklad, který můžete zkopírovat a vložit.
- Běžné úskalí (např. chybějící fonty, velké stránky) a jak se jim vyhnout.
- Rychlé tipy pro úpravu výstupu, když potřebujete **convert HTML to PNG** v různých prostředích.

### Požadavky

- Java 8 nebo novější nainstalovaná na vašem počítači.
- Knihovna Aspose.HTML pro Java (nejnovější verze k březnu 2026). Můžete ji získat z Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

- Jednoduchý soubor `input.html`, který chcete převést na PNG obrázek.

---

## Jak nastavit DPI pro konverzi HTML na PNG

![Diagram ukazující nastavení DPI v kódu – jak nastavit dpi při konverzi HTML na PNG](https://example.com/images/dpi-setting.png)

**Hlavní krok**, který řídí ostrost obrázku, je vlastnost `Resolution` třídy `ImageSaveOptions`. Níže rozdělíme proces na malé kroky.

### Krok 1: Definujte vstupní a výstupní cesty (convert html to png)

Nejprve řekněte konvertoru, kde se nachází váš zdrojový HTML soubor a kam má být PNG zapsáno.

```java
// Step 1 – file locations
String htmlFilePath = "YOUR_DIRECTORY/input.html";
String pngFilePath  = "YOUR_DIRECTORY/output.png";
```

> **Proč je to důležité:** Hard‑coding cest je v pořádku pro ukázku, ale ve výrobě je pravděpodobně budete získávat z konfigurace nebo argumentů příkazové řádky. Umožní to kódu být flexibilní pro jakýkoli **save HTML as PNG** workflow.

### Krok 2: Vytvořte ImageSaveOptions a nastavte DPI (how to set dpi)

Nyní vytvoříme instanci `ImageSaveOptions` pro PNG a nastavíme DPI na 300. DPI určuje, kolik pixelů je zabalených do každého palce, když je obrázek tištěn nebo zobrazen v původní velikosti.

```java
// Step 2 – configure PNG options
ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
saveOptions.setResolution(300);   // <-- This is the DPI you asked for
saveOptions.setQuality(95);       // PNG compression (0‑100); higher = larger file, better fidelity
```

> **Vysvětlení:**  
> - `setResolution(300)` říká Aspose.HTML, aby vykreslil stránku při 300 dots per inch.  
> - `setQuality(95)` je pro PNG volitelný; řídí úroveň ZLIB komprese. Můžete ji snížit pro menší soubory, pokud nepotřebujete, aby byl každý pixel dokonalý.

### Krok 3: Proveďte konverzi (export html as png)

S připravenými možnostmi je samotná konverze jedním řádkem.

```java
// Step 3 – run the conversion
Converter.convert(htmlFilePath, pngFilePath, saveOptions);
```

> **Co se děje pod kapotou?** Aspose.HTML parsuje HTML, aplikuje CSS, rozvrhne DOM, rasterizuje rozvržení při požadovaném DPI a nakonec zapíše PNG soubor. Pokud potřebujete **generate PNG from HTML** ve webové službě, můžete nahradit cesty k souborům proudy.

### Kompletní funkční příklad

Spojením všeho dohromady získáte kompletní Java třídu, kterou můžete zkompilovat a spustit.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.*;
import com.aspose.html.saving.*;

public class ConvertHtmlToPngWithDpi {
    public static void main(String[] args) throws Exception {

        // Step 1: Define the input HTML file and the output PNG file
        String htmlFilePath = "YOUR_DIRECTORY/input.html";
        String pngFilePath  = "YOUR_DIRECTORY/output.png";

        // Step 2: Create image save options for PNG and configure high‑resolution output
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        saveOptions.setResolution(300);   // Set resolution to 300 DPI (how to set dpi)
        saveOptions.setQuality(95);       // PNG compression quality (0‑100)

        // Step 3: Perform the conversion from HTML to PNG using the configured options
        Converter.convert(htmlFilePath, pngFilePath, saveOptions);

        System.out.println("Conversion complete! PNG saved at " + pngFilePath);
    }
}
```

Spusťte program a najdete ostrý 300 DPI PNG na zadaném místě. Otevřete jej v libovolném prohlížeči obrázků a zkontrolujte vlastnosti obrázku – DPI by mělo být **300**.

---

## Časté otázky a okrajové případy

### Co když se nastavení DPI zdá být ignorováno?

- **Ujistěte se, že používáte aktuální verzi Aspose.HTML.** Starší verze ignorovaly `Resolution` pro PNG.
- **Zkontrolujte velikost zdrojového HTML.** Malá HTML stránka vykreslená při 300 DPI může stále vytvořit malý rozměr v pixelech. DPI ovlivňuje pouze faktor škálování, ne inherentní velikost stránky.

### Jak se DPI liší od rozměrů obrázku?

DPI je *fyzické* měření (dots per inch). Skutečná šířka/výška v pixelech se vypočítá jako:

```
pixel width  = CSS width  * DPI / 96
pixel height = CSS height * DPI / 96
```

Pokud je tělo vašeho HTML široké 800 px, při 300 DPI bude výstupní PNG přibližně 2500 px široký (800 × 300 ÷ 96).

### Můžu použít jiné formáty (JPEG, BMP) a stále řídit DPI?

Určitě. Stačí změnit `SaveFormat.PNG` na `SaveFormat.JPEG` (nebo `BMP`) a ponechat `setResolution`. Pamatujte, že JPEG také respektuje nastavení `Quality`, které odpovídá úrovni komprese.

### Co s fonty, které nejsou nainstalovány na serveru?

Aspose.HTML se vrátí k výchozímu fontu, což může změnit rozvržení. Pro zajištění identického vykreslení vložte požadované fonty pomocí `FontSettings`:

```java
FontSettings fontSettings = new FontSettings();
fontSettings.setFontFolder("YOUR_FONT_DIRECTORY", true);
saveOptions.setFontSettings(fontSettings);
```

### Generování více PNG souborů v dávce

Pokud potřebujete **generate PNG from HTML** pro mnoho souborů, zabalte logiku konverze do smyčky a znovu použijte jedinou instanci `ImageSaveOptions`. Tím snížíte zatížení paměti a urychlíte zpracování.

```java
for (Path htmlPath : Files.newDirectoryStream(Paths.get("batch_html"))) {
    String outPath = htmlPath.toString().replace(".html", ".png");
    Converter.convert(htmlPath.toString(), outPath, saveOptions);
}
```

---

## Profesionální tipy pro export PNG ve vysoké kvalitě

1. Používejte CSS přátelské k vektorům (např. `transform: scale(1)`), abyste se vyhnuli artefaktům anti‑aliasingu při vysokém DPI.  
2. Nastavte barvu pozadí, pokud má vaše HTML transparentní prvky a potřebujete pevné plátno:

   ```java
   saveOptions.setBackgroundColor(Color.WHITE);
   ```

3. Vyhněte se vloženým base64 obrázkům větším než několik MB – mohou nafouknout využití paměti během konverze.  
4. Testujte na různých DPI obrazovek (např. 72 DPI monitory vs. 300 DPI tiskárny), abyste zajistili, že vizuální kvalita splňuje očekávání.  
5. Využijte `setPageSize()`, pokud chcete, aby PNG odpovídalo konkrétní tiskové velikosti (A4, Letter atd.) bez ohledu na původní rozměry HTML.

---

## Závěr

Probrali jsme **jak nastavit DPI** při **convert HTML to PNG** pomocí Aspose.HTML pro Java, ukázali kompletní připravený příklad a prozkoumali související úkoly jako **export HTML as PNG**, **save HTML as PNG** a **generate PNG from HTML**. Úpravou `ImageSaveOptions.setResolution` řídíte fyzickou ostrost výstupu, zatímco `setQuality` vám umožní vyvážit velikost souboru a vizuální věrnost.

Další kroky? Zkuste vyměnit formát PNG za JPEG a podívejte se, jak komprese interaguje s DPI, nebo experimentujte s dávkovým zpracováním pro **convert HTML to PNG** ve velkém měřítku. Můžete také prozkoumat přidání vodoznaků nebo vlastních metadat – oba jsou podporovány bohatým API Aspose.HTML.

Máte složitý scénář, který nebyl pokryt? Zanechte komentář a společně to vyřešíme. Šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}