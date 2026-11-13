---
category: general
date: 2026-05-06
description: Jak nastavit DPI pro konverzi SVG do PNG ve vysokém rozlišení v Javě
  pomocí Aspose.HTML. Naučte se převádět SVG na PNG, exportovat SVG jako PNG a převádět
  vektor na rastrový obrázek.
draft: false
keywords:
- how to set dpi
- convert svg to png
- how to convert svg
- export svg as png
- convert vector to raster
language: cs
og_description: Jak nastavit DPI pro konverzi SVG na PNG ve vysokém rozlišení v Javě
  pomocí Aspose.HTML. Získejte krok‑za‑krokem kód a odborné tipy.
og_title: Jak nastavit DPI při převodu SVG na PNG – Java průvodce
tags:
- Java
- Aspose.HTML
- Image Conversion
title: Jak nastavit DPI při převodu SVG na PNG – Java průvodce
url: /cs/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak nastavit DPI při konverzi SVG na PNG – Průvodce pro Java

Už jste se někdy zamysleli **jak nastavit DPI** při konverzi SVG‑na‑PNG a získat ostrý, připravený pro tisk obrázek? Nejste v tom sami. Mnoho vývojářů narazí na problém, když jejich exportovaný PNG vypadá rozmazaně, protože výchozí DPI (obvykle 96) není dostatečné pro profesionální výstup.

V tomto tutoriálu projdeme kompletním, připraveným příkladem, který ukazuje **jak nastavit DPI** pomocí Aspose.HTML pro Java. Na konci budete schopni **převést SVG na PNG**, **exportovat SVG jako PNG** a dokonce **převést vektor na rastrový** s libovolným DPI, které potřebujete—žádná záhada, jen přehledný kód.

## Co se naučíte

- Přesné kroky pro nastavení DPI před konverzí.
- Proč je DPI důležité, když **převádíte vektor na rastrový**.
- Jak **převést SVG na PNG** jedním řádkem kódu.
- Tipy pro práci s velkými SVG a dávkovým zpracováním.
- Kompletní, kompilovatelný program, který můžete okamžitě vložit do svého projektu.

## Požadavky

Než se pustíme dál, ujistěte se, že máte:

- Java 17 nebo novější (nejnovější LTS verze funguje nejlépe).
- Maven nebo Gradle pro stažení knihovny Aspose.HTML.
- Jednoduchý SVG soubor, který chcete rasterizovat (např. `logo.svg`).
- IDE nebo textový editor—IntelliJ IDEA, VS Code nebo i starý Notepad vám postačí.

Žádné další externí nástroje nejsou potřeba; knihovna provede veškerou těžkou práci.

## Krok 1: Přidejte Aspose.HTML do svého projektu

Nejprve potřebujete JAR Aspose.HTML. Pokud používáte Maven, přidejte tento úryvek do svého `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

Pro Gradle to vypadá takto:

```groovy
implementation 'com.aspose:aspose-html:23.10'
```

> **Tip:** Vždy používejte nejnovější stabilní verzi; novější vydání obsahují opravy výkonu pro renderování ve vysokém DPI.

## Krok 2: Jak nastavit DPI pro konverzi

Nyní přicházíme k podstatě—**jak nastavit DPI**. Aspose.HTML poskytuje `ImageConversionOptions`, kde můžete určit jak horizontální (`dpiX`), tak vertikální (`dpiY`) rozlišení. Nastavením obou na `300` získáte klasickou tiskovou kvalitu.

```java
import com.aspose.html.converters.ImageConversionOptions;
import com.aspose.html.rendering.Converter;

public class SvgHighRes {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create conversion options
        ImageConversionOptions conversionOptions = new ImageConversionOptions();

        // 2️⃣ Set target DPI for high‑resolution output (300 dpi → crisp print quality)
        conversionOptions.setDpiX(300);
        conversionOptions.setDpiY(300);

        // 3️⃣ Convert the SVG file to a PNG using the configured options
        Converter.convertSvgToPng(
                "YOUR_DIRECTORY/logo.svg",        // source SVG
                "YOUR_DIRECTORY/logo_300dpi.png", // destination PNG
                conversionOptions);
    }
}
```

> **Proč 300 dpi?** Je to de‑facto standard pro profesionální tisk. Pokud potřebujete obrázek pro web, 72 dpi stačí, ale pro letáky nebo brožury budete chtít alespoň 300 dpi.

### Náhled obrázku

![Jak nastavit DPI při konverzi SVG na PNG](https://example.com/placeholder.png "Jak nastavit DPI při konverzi SVG na PNG")

*Obrázek výše ilustruje rozdíl mezi PNG s nízkým DPI (vlevo) a výstupem 300 dpi (vpravo).*

## Krok 3: Převod SVG na PNG – Jednořádkový kód

Pokud chcete jen rychlý **convert svg to png** bez manipulace s DPI, můžete objekt s možnostmi úplně vynechat:

```java
Converter.convertSvgToPng("logo.svg", "logo_default.png", null);
```

Předáním `null` řeknete Aspose.HTML, aby použil výchozí DPI (obvykle 96). To je užitečné pro náhledy nebo když vám nezáleží na kvalitě tisku.

## Krok 4: Ověření výsledku – Export SVG jako PNG

Po dokončení konverze otevřete vygenerovaný PNG v libovolném prohlížeči obrázků. Měli byste vidět rastrový obrázek, který odpovídá rozměrům původního vektoru, ale nyní nese nastavené DPI. Většina prohlížečů zobrazuje DPI v vlastnostech obrázku; ve Windows klikněte pravým tlačítkem → Vlastnosti → Podrobnosti.

Pokud potřebujete programově ověřit DPI, Java `ImageIO` jej může načíst:

```java
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;

BufferedImage img = ImageIO.read(new File("logo_300dpi.png"));
int dpi = (int) img.getProperty("dpi");
System.out.println("Exported PNG DPI: " + dpi);
```

> **Poznámka:** Ne všechny formáty obrázků ukládají metadata DPI; PNG ano, ale JPEG může vyžadovat další zpracování.

## Okrajové případy a varianty

### 1️⃣ Různé hodnoty DPI

Možná se ptáte, „Co když potřebuji 600 dpi pro velký plakát?“ Stačí změnit čísla:

```java
conversionOptions.setDpiX(600);
conversionOptions.setDpiY(600);
```

Vyšší DPI znamená větší velikost souboru, takže buďte opatrní s paměťovými omezeními při zpracování mnoha souborů.

### 2️⃣ Dávková konverze složky

Když máte desítky SVG, zabalte konverzi do jednoduché smyčky:

```java
File dir = new File("YOUR_DIRECTORY");
for (File svg : dir.listFiles((d, name) -> name.endsWith(".svg"))) {
    String pngName = svg.getName().replace(".svg", "_300dpi.png");
    Converter.convertSvgToPng(svg.getAbsolutePath(),
                              new File(dir, pngName).getAbsolutePath(),
                              conversionOptions);
}
```

Tento vzor **převádí vektor na rastrový** hromadně, ušetří vám hodiny ruční práce.

### 3️⃣ Zpracování průhledných pozadí

Pokud váš SVG obsahuje průhlednost a chcete bílé pozadí, nejprve renderujte do `BufferedImage` a poté vyplňte pozadí:

```java
// Render SVG to BufferedImage with DPI
BufferedImage raster = Converter.convertSvgToImage(
        "logo.svg", conversionOptions);

// Fill background (optional)
Graphics2D g = raster.createGraphics();
g.setComposite(AlphaComposite.SrcOver);
g.setColor(Color.WHITE);
g.fillRect(0, 0, raster.getWidth(), raster.getHeight());
g.dispose();

// Write out PNG
ImageIO.write(raster, "png", new File("logo_whitebg.png"));
```

## Časté otázky

**Q: Funguje to na Linuxu?**  
A: Naprosto. Aspose.HTML je platformově nezávislý; stačí zajistit, že máte správné Java runtime.

**Q: Co když můj SVG odkazuje na externí obrázky?**  
A: Ujistěte se, že jsou tyto zdroje dostupné pomocí absolutních cest nebo URL; jinak je renderer přeskočí.

**Q: Můžu převést SVG do jiných rastrových formátů jako JPEG nebo BMP?**  
A: Ano. Použijte `Converter.convertSvgToJpeg` nebo `Converter.convertSvgToBmp` se stejným `ImageConversionOptions`.

## Profesionální tipy pro vysoce kvalitní rasterizaci

- **Přizpůsobte DPI finální velikosti výstupu.** Logo o velikosti 2 palce tištěné při 300 dpi potřebuje šířku 600 px (2 in × 300 dpi). Před konverzí SVG podle toho přepočítejte, pokud potřebujete konkrétní rozměr v pixelech.
- **Dávejte pozor na barevný profil.** PNG standardně neobsahuje ICC profily; pokud záleží na přesnosti barev, převádějte do TIFF nebo použijte knihovnu, která podporuje vkládání profilů.
- **Znovu používejte objekt `ImageConversionOptions`** při konverzi mnoha souborů—vyhnete se zbytečnému vytváření objektů a můžete zlepšit výkon.

## Závěr

Nyní víte **jak nastavit DPI** pro konverzi SVG‑na‑PNG v Javě a viděli jste, jak stejný přístup umožňuje **convert svg to png**, **export svg as png** a obecně **convert vector to raster** s plnou kontrolou nad rozlišením. Kompletní příklad výše funguje ihned a další tipy vám poskytují plán pro rozšíření řešení na reálné projekty.

Co dál? Vyzkoušejte výměnu hodnoty 300 dpi za 600 dpi, experimentujte s dávkovým zpracováním nebo prozkoumejte jiné rastrové formáty. Stejné principy platí—stačí změnit výstupní metodu a můžete jít dál.

Máte obtížný SVG nebo otázku ohledně výkonu? Zanechte komentář a šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}