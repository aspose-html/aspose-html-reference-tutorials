---
category: general
date: 2026-04-23
description: Naučte se, jak nastavit DPI pro ultra‑vysokou kvalitu převodu SVG na
  PNG v Javě pomocí Aspose. Obsahuje krok‑za‑krokem kód, tipy a řešení okrajových
  případů.
draft: false
keywords:
- how to set dpi
- convert svg to png
- svg to png java
- how to convert svg
- aspose svg to png
language: cs
og_description: Zvládněte, jak nastavit DPI při konverzi SVG na PNG pomocí Aspose
  HTML v Javě. Kompletní kód, vysvětlení a tipy na nejlepší postupy.
og_title: Jak nastavit DPI při převodu SVG na PNG – Java tutoriál
tags:
- Aspose
- Java
- SVG
- PNG
- Image Conversion
title: Jak nastavit DPI při převodu SVG na PNG pomocí Aspose – Java průvodce
url: /cs/java/advanced-usage/how-to-set-dpi-when-converting-svg-to-png-with-aspose-java-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak nastavit DPI při konverzi SVG na PNG pomocí Aspose – Java průvodce

Už jste se někdy zamysleli **jak nastavit DPI** pro krystalicky čistý PNG, který vznikl ze SVG? Možná budujete branding pipeline a potřebujete logo s 600 dpi pro tisk, nebo prostě chcete, aby rastrový obrázek vypadal ostrý na obrazovkách s vysokým rozlišením. Dobrá zpráva je, že nemusíte hádat — Aspose HTML for Java to usnadní.

V tomto tutoriálu si projdeme **jak nastavit DPI** při **konverzi SVG na PNG** pomocí knihovny Aspose. Dostanete kompletní, připravený k spuštění ukázkový kód, vysvětlení každé konfigurační volby a několik praktických tipů pro reálné projekty. Žádné externí odkazy nejsou potřeba — vše, co potřebujete, je zde.

## Požadavky

Než se pustíme dál, ujistěte se, že máte:

- Java 17 (nebo jakýkoli novější JDK) nainstalovaný.
- Maven nebo Gradle pro správu závislostí (ukážeme ukázku pro Maven).
- SVG soubor, který chcete rasterizovat (např. `logo.svg`).
- Základní znalost syntaxe Javy — nic složitého, jen obvyklý `public static void main`.

Pokud vám něco chybí, nejprve to doplňte; zbytek průvodce předpokládá, že jsou všechny požadavky splněny.

## Závislost Maven

Přidejte závislost Aspose HTML for Java do svého `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Uživatelé Gradlu mohou nahradit tento úryvek ekvivalentním řádkem `implementation "com.aspose:aspose-html:23.12"`.

## Krok 1: Vytvořte objekt možností konverze

První věc, kterou musíte udělat, je vytvořit instanci `SvgConversionOptions`. Tento objekt obsahuje všechny možné úpravy, které můžete potřebovat — DPI, barvu pozadí, škálování atd.

```java
// Step 1: Build conversion options for SVG → PNG
SvgConversionOptions conversionOptions = new SvgConversionOptions();
```

Proč je to důležité: pokud explicitně nenastavíte DPI, Aspose použije výchozí 96 dpi, což je v pořádku pro web, ale rozhodně ne pro tisk. Vytvořením objektu možností získáte plnou kontrolu nad procesem rasterizace.

## Krok 2: Nastavte požadované DPI

Nyní odpovíme na hlavní otázku: **jak nastavit DPI**. Metoda `setDpi(int)` očekává celé číslo; typické hodnoty se pohybují od 72 dpi (nízké rozlišení) až po 1200 dpi (ultra‑vysoké rozlišení). Pro většinu tiskových úloh je 300 dpi ideální; pro loga, která potřebují škálování, je 600 dpi bezpečná volba.

```java
// Step 2: Define the resolution (DPI) – 600 DPI for ultra‑high‑quality output
conversionOptions.setDpi(600);
```

> **Tip:** Hodnoty DPI, které nejsou násobky 72, mohou někdy vytvořit necelé rozměry pixelů. Pokud potřebujete přesnou velikost v pixelech, vypočítejte `pixel = inches * DPI` předem a upravte viewBox SVG podle toho.

## Krok 3: Práce s průhledností pomocí barvy pozadí

SVG soubory často obsahují průhledné oblasti. PNG podporuje průhlednost, ale pokud cílíte na tiskový workflow, který očekává neprůhledné pozadí, budete chtít tuto oblast nahradit. Metoda `setBackgroundColor(String)` přijímá libovolný CSS‑kompatibilní řetězec barvy.

```java
// Step 3: Replace transparent areas with white (or any color you prefer)
conversionOptions.setBackgroundColor("white");
```

Můžete také použít `#FFFFFF`, `rgb(255,255,255)` nebo dokonce `transparent`, pokud *chcete* zachovat alfa kanál.

## Krok 4: Proveďte konverzi

Po nastavení možností je samotná konverze jediným statickým voláním `Converter.convert`. Zadejte vstupní cestu k SVG, požadovanou výstupní cestu k PNG a objekt možností.

```java
// Step 4: Convert the SVG file to a PNG using the configured options
Converter.convert(
        "YOUR_DIRECTORY/logo.svg",   // Input SVG
        "YOUR_DIRECTORY/logo.png",   // Output PNG
        conversionOptions);          // Options we just set
```

A to je vše — Aspose se postará o parsování SVG, aplikaci DPI škálování, vyplnění pozadí a zápis PNG souboru na disk.

## Kompletní spustitelný příklad

Níže je kompletní třída Java, kterou můžete zkopírovat a vložit do souboru pojmenovaného `SvgToPngHighRes.java`. Nahraďte `YOUR_DIRECTORY` skutečnou cestou ke složce na vašem počítači.

```java
import com.aspose.html.converters.SvgConversionOptions;
import com.aspose.html.converters.Converter;

/**
 * Demonstrates how to set DPI when converting an SVG file to a high‑resolution PNG
 * using Aspose.HTML for Java.
 *
 * Prerequisites:
 *   - Aspose.HTML for Java library (Maven dependency shown earlier)
 *   - Java 17+ runtime
 *
 * Expected result:
 *   - logo.png created at 600 DPI with a white background.
 */
public class SvgToPngHighRes {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create conversion options for SVG → PNG
        SvgConversionOptions conversionOptions = new SvgConversionOptions();

        // 2️⃣ Set the desired resolution (DPI) – 600 DPI yields ultra‑high‑quality output
        conversionOptions.setDpi(600);

        // 3️⃣ Define a background color to replace any transparency (white works for most prints)
        conversionOptions.setBackgroundColor("white");

        // 4️⃣ Convert the SVG file to a PNG using the configured options
        Converter.convert(
                "YOUR_DIRECTORY/logo.svg",   // <-- change this to your source file
                "YOUR_DIRECTORY/logo.png",   // <-- change this to your target file
                conversionOptions);

        System.out.println("Conversion complete! Check YOUR_DIRECTORY/logo.png");
    }
}
```

### Očekávaný výstup

Spuštěním programu se ve stejné složce vygeneruje soubor `logo.png`. Otevřete jej v prohlížeči obrázků a podívejte se na **vlastnosti obrázku** — měli byste vidět:

- **Rozlišení:** 600 dpi (nebo jakoukoliv hodnotu, kterou jste nastavili)
- **Rozměry:** Škálováno podle původního viewBox SVG vynásobeného faktorem DPI
- **Pozadí:** Jednobarevně bílé (žádné průhledné pixely)

Pokud otevřete PNG v nástroji jako Photoshop, metadata DPI budou viditelná pod *Image → Image Size*.

## Běžné okrajové případy a jak je řešit

| Situace | Na co si dát pozor | Doporučené řešení |
|-----------|-------------------|-----------------|
| **Chybějící SVG soubor** | `FileNotFoundException` vyvolaná metodou `Converter.convert` | Ověřte cestu před konverzí pomocí `Files.exists(Paths.get(...))`. |
| **Není podporována některá SVG funkce** (např. filtry, které ještě nejsou implementovány) | Aspose může tyto funkce tiše vynechat | Použijte `SvgConversionOptions.setEnableSvgFilters(true)`, pokud potřebujete podporu filtrů (k dispozici v novějších verzích). |
| **Velmi vysoké DPI (≥1200)** | Výstupní soubor může být obrovský (stovky MB) | Zvažte streamování výsledku nebo snížení DPI pro velké obrázky. |
| **Zachování průhlednosti** | Nastavili jste barvu pozadí, ale ve skutečnosti chcete alfa kanál | Vynechte `setBackgroundColor` nebo předávejte `"transparent"` pro zachování původního alfa kanálu. |
| **Dávková konverze** | Vytváření nového `SvgConversionOptions` pro každý soubor je neefektivní | Vytvořte jedinou instanci `SvgConversionOptions` a znovu ji použijte ve smyčce. |

## Často kladené otázky

**Q: Funguje to i s jinými rastrovými formáty jako JPEG nebo BMP?**  
A: Ano. Nahraďte příponu výstupního souboru (`.png`) za `.jpg` nebo `.bmp` a Aspose automaticky vybere odpovídající enkodér. Kvalitu JPEG můžete doladit pomocí `JpegConversionOptions`.

**Q: Můžu konvertovat SVG uložené v byte array místo souboru?**  
A: Rozhodně. Použijte přetížené metody `Converter.convert(InputStream, OutputStream, conversionOptions)`, které pracují se streamy – ideální pro webové služby.

**Q: Je nastavení DPI stejné jako škálování obrázku?**  
A: DPI je metadata, která říká tiskárnám, kolik pixelů představuje jeden palec. Interně Aspose škáluje rastrový obrázek tak, aby odpovídal DPI, takže vizuální velikost se změní, pokud PNG zobrazíte při 100 % zoomu v prohlížeči, který DPI respektuje.

## Tipy pro produkčně připravený kód

1. **Cache možností** — pokud konvertujete desítky log, která mají stejné DPI a pozadí, vytvořte `SvgConversionOptions` jednou a znovu ji použijte. Tím snížíte režii vytváření objektů.
2. **Ověřte vstupní rozměry** — pro extrémně velké SVG vypočítejte očekávanou velikost v pixelech (`width * DPI/96`) a ukončete proces, pokud překročí bezpečný limit (např. 20 000 px), abyste předešli `OutOfMemoryError`.
3. **Logujte metadata konverze** — uložte DPI, název zdrojového souboru a časové razítko do logu; usnadní to pozdější ladění.
4. **Thread‑safety** — `Converter.convert` je thread‑safe, takže můžete dávkové úlohy paralelizovat pomocí `ExecutorService`.

## Vizualizace

![how to set dpi example](image.png){: .align-center alt="příklad nastavení dpi"}

Diagram výše ilustruje tok: **SVG → nastavení DPI & pozadí → PNG**.

## Závěr

Nyní už víte **jak nastavit DPI** při **konverzi SVG na PNG** pomocí Aspose HTML for Java. Konfigurací `SvgConversionOptions` ovládáte rozlišení, zacházení s pozadím a další parametry, čímž ze základního vektorového souboru vytvoříte tiskové rastrové obrázky pomocí několika řádků kódu.

Vyzkoušejte další kroky:

- Konverzi celé složky SVG v dávkovém cyklu.
- Přepnutí výstupního formátu na JPEG pro web‑optimalizovaná aktiva.
- Použití dalších Aspose možností konverze, jako je `setScaleX/Y` pro vlastní škálování nad rámec DPI.

Šťastné programování a ať jsou vaše PNG vždy tak ostré, jak potřebujete!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}