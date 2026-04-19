---
category: general
date: 2026-04-19
description: Převod SVG na PNG v Javě s Aspose.HTML. Naučte se, jak exportovat SVG
  jako PNG, nastavit rozlišení PNG a uložit SVG jako PNG při 300 DPI během několika
  minut.
draft: false
keywords:
- convert svg to png
- export svg as png
- save svg as png
- set png resolution
- svg to png java
language: cs
og_description: Převod SVG na PNG v Javě pomocí Aspose.HTML. Tento tutoriál ukazuje,
  jak exportovat SVG do PNG, nastavit rozlišení PNG a uložit SVG jako PNG s 300 DPI.
og_title: Převod SVG na PNG v Javě – Průvodce pro vysoké rozlišení
tags:
- Java
- Image Processing
title: Převod SVG na PNG v Javě – Průvodce pro vysoké rozlišení
url: /cs/java/conversion-html-to-various-image-formats/convert-svg-to-png-in-java-high-resolution-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod SVG na PNG v Javě – Průvodce pro vysoké rozlišení

Už jste někdy potřebovali **převést SVG na PNG**, ale nevedeli jste, jak zachovat ostrost obrázku? Možná budujete nástroj pro reportování, generátor miniatur nebo jen potřebujete rastrovou kopii vektorového loga. Ať už je to jakkoli, jste na správném místě. V tomto tutoriálu projdeme export SVG jako PNG s přesným DPI, takže získáte bitmapu ve vysokém rozlišení, která vypadá přesně tak, jak očekáváte.

Použijeme Aspose.HTML pro Java, knihovnu, která usnadňuje práci se soubory SVG. Na konci tohoto průvodce budete vědět, jak **uložit SVG jako PNG**, jak nastavit **set PNG resolution** a jak řešit nejčastější problémy, které se objeví při konverzi vektor‑na‑raster. Žádné externí nástroje, žádné příkazy v terminálu – jen čistý Java kód, který můžete dnes vložit do svého projektu.

> **Co budete potřebovat**  
> - Java 17 (nebo jakýkoli novější JDK)  
> - Aspose.HTML pro Java (Maven artefakt `com.aspose:aspose-html`)  
> - SVG soubor, který chcete rasterizovat  

Pokud to máte, pojďme na to.

---

## Krok 1: Načtení SVG souboru – první krok k převodu SVG na PNG

Než může dojít k jakékoli konverzi, musíte načíst SVG dokument do paměti. Třída `SvgDocument` to za vás udělá.

```java
import com.aspose.html.SvgDocument;

// Load the source SVG
SvgDocument svg = new SvgDocument("C:/images/vector.svg");
```

*Proč je to důležité*: Načtení souboru ověří syntaxi SVG už na začátku, takže zachytíte špatně vytvořený markup dříve, než ztratíte čas na operaci uložení. Z mé zkušenosti vede poškozené SVG často k prázdnému PNG, což může být frustrující a těžko laditelný problém.

---

## Krok 2: Nastavení možností uložení PNG – jak nastavit rozlišení PNG

Kvalita rastrového obrázku je do značné míry určena DPI (bodů na palec). Výchozí hodnota mnoha knihoven je 96 DPI, což vypadá dobře na obrazovce, ale může být rozmazané při tisku. Pro ostrý tiskový výstup budete chtít **set PNG resolution** na něco jako 300 DPI.

```java
import com.aspose.html.saving.PngSaveOptions;

// Create PNG options and set DPI
PngSaveOptions pngOptions = new PngSaveOptions();
pngOptions.setDpiX(300);   // Horizontal DPI
pngOptions.setDpiY(300);   // Vertical DPI
```

*Tip*: Pokud potřebujete jiné DPI (např. 150 pro webové miniatury), stačí změnit čísla. Knihovna provede rasterizaci podle nového DPI a zachová poměr stran vektoru.

---

## Krok 3: Export SVG jako PNG – okamžik, kdy **save SVG as PNG**

Jakmile je dokument načtený a možnosti nastavené, samotná konverze je jediný řádek.

```java
// Save the SVG as a high‑resolution PNG
svg.save("C:/images/vector_300dpi.png", pngOptions);
System.out.println("High‑res PNG created.");
```

A to je vše. Metoda `save` udělá vše těžké: parsuje SVG, aplikuje DPI škálování a zapíše PNG soubor na disk.

---

## Krok 4: Ověření výstupu ve vysokém rozlišení

Po dokončení konverze je dobré výsledek zkontrolovat, zejména pokud tuto operaci automatizujete v dávkovém procesu.

```java
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import java.io.File;

BufferedImage img = ImageIO.read(new File("C:/images/vector_300dpi.png"));
System.out.println("Width: " + img.getWidth() + " px");
System.out.println("Height: " + img.getHeight() + " px");
System.out.println("DPI (X): " + pngOptions.getDpiX());
```

Měli byste vidět rozměry v pixelech, které odpovídají původní velikosti SVG vynásobené faktorem DPI. Například SVG 200 × 100 pt při 300 DPI se změní přibližně na 833 × 417 px.

---

## Časté problémy a jak se jim vyhnout

| Problém | Proč k tomu dochází | Řešení |
|-------|----------------|-----|
| **Blank PNG** | SVG obsahuje externí zdroje (fonty, obrázky), které nejsou dostupné. | Vložte zdroje nebo použijte absolutní URL; případně nastavte `svg.setBaseUrl("file:///C:/images/")`. |
| **Incorrect size** | DPI nebylo aplikováno, protože jste použili `PngExportOptions` místo `PngSaveOptions`. | Vždy používejte `PngSaveOptions` a zavolejte `setDpiX/Y`. |
| **Out‑of‑memory errors** | Velmi velké SVG způsobí, že rasterizér alokuje obrovské buffery. | Zvyšte heap JVM (`-Xmx2g`) nebo rozdělte SVG na menší části. |
| **Color shift** | SVG používá barevný profil, který knihovna ignoruje. | Před uložením převěďte barvy na sRGB, nebo použijte `pngOptions.setColorProfile(...)`, pokud je podporováno. |

Řešení těchto problémů včas vám ušetří nespočet ladicích seancí později.

---

## Kompletní funkční příklad – připravený ke zkopírování

Níže je celý program, včetně importů, ošetření chyb a komentářů vysvětlujících každý řádek.

```java
import com.aspose.html.SvgDocument;
import com.aspose.html.saving.PngSaveOptions;
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import java.io.File;

/**
 * Demonstrates how to convert an SVG file to a high‑resolution PNG in Java.
 * The output image will be saved at 300 DPI.
 */
public class SvgToPngHighRes {
    public static void main(String[] args) {
        try {
            // -------------------------------------------------
            // Step 1: Load the SVG file you want to convert
            // -------------------------------------------------
            SvgDocument svg = new SvgDocument("C:/images/vector.svg");

            // -------------------------------------------------
            // Step 2: Create PNG save options and set the desired DPI
            // -------------------------------------------------
            PngSaveOptions pngOptions = new PngSaveOptions();
            pngOptions.setDpiX(300);   // Horizontal DPI
            pngOptions.setDpiY(300);   // Vertical DPI

            // -------------------------------------------------
            // Step 3: Export SVG as PNG using the configured options
            // -------------------------------------------------
            String outputPath = "C:/images/vector_300dpi.png";
            svg.save(outputPath, pngOptions);
            System.out.println("High‑res PNG created at " + outputPath);

            // -------------------------------------------------
            // Step 4: Verify the result (optional but recommended)
            // -------------------------------------------------
            BufferedImage img = ImageIO.read(new File(outputPath));
            System.out.println("Resulting image size: " + img.getWidth() + "×" + img.getHeight() + " px");
            System.out.println("DPI set to: " + pngOptions.getDpiX() + " (X), " + pngOptions.getDpiY() + " (Y)");
        } catch (Exception e) {
            // Graceful error handling – prints stack trace and exits
            System.err.println("Error during SVG to PNG conversion:");
            e.printStackTrace();
        }
    }
}
```

Spusťte tuto třídu z IDE nebo pomocí `java -cp path/to/aspose-html.jar;. SvgToPngHighRes`. Pokud je vše správně nastaveno, uvidíte výstup v konzoli potvrzující rozměry a DPI PNG.

---

## Když potřebujete větší kontrolu – pokročilé možnosti

Někdy pouhá změna DPI nestačí. Zde jsou některé scénáře, se kterými se můžete setkat, a rychlé úryvky kódu.

### Škálování bez změny DPI

Pokud chcete PNG přesně 800 px široké bez ohledu na původní velikost, spočítejte faktor škálování a aplikujte jej na `PngSaveOptions`.

```java
int targetWidth = 800;
double scale = (double) targetWidth / svg.getDocumentElement().getClientWidth();
pngOptions.setScaleX(scale);
pngOptions.setScaleY(scale);
```

### Práce s průhledným pozadím

Ve výchozím nastavení Aspose.HTML zachovává průhlednost. Pokud potřebujete pevné pozadí (např. bílé pro konverzi na JPEG), nastavte barvu pozadí:

```java
pngOptions.setBackgroundColor(java.awt.Color.WHITE);
```

### Konverze dávky SVG souborů

Zabalte logiku do smyčky a dynamicky nahrazujte cesty k souborům.

```java
File folder = new File("C:/images/svg_batch/");
for (File svgFile : folder.listFiles((dir, name) -> name.endsWith(".svg"))) {
    SvgDocument doc = new SvgDocument(svgFile.getAbsolutePath());
    String pngPath = svgFile.getAbsolutePath().replace(".svg", "_300dpi.png");
    doc.save(pngPath, pngOptions);
    System.out.println("Converted: " + svgFile.getName());
}
```

---

## Závěr

Nyní máte solidní, produkčně připravený recept na **convert SVG to PNG** v Javě, včetně možnosti **set PNG resolution** a **export SVG as PNG** při libovolném DPI. Výše uvedený kompletní příklad můžete vložit do libovolného Java projektu a s několika úpravami můžete dávkově zpracovat desítky souborů, měnit faktory škálování nebo upravovat barvu pozadí.

Další kroky? Zkuste integrovat tuto rutinu do REST endpointu, aby váš webový servis mohl přijímat SVG nahrávky a vracet vysoké rozlišení PNG „na požádání“. Nebo experimentujte s dalšími formáty Aspose.HTML – možná budete chtít **save SVG as PNG** a poté jej vložit do PDF. Ať už se rozhodnete jakkoli, základy zde pokryté vám poslouží jako spolehlivý základ.

Máte otázky ohledně okrajových případů, licencování nebo ladění výkonu? Zanechte komentář a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}