---
category: general
date: 2026-03-07
description: Vykreslete HTML v Javě do PNG převodem dlouhé HTML stránky na obrázek.
  Naučte se, jak převést HTML na obrázek, získat PNG z HTML a vytvořit obrázek z dlouhého
  HTML pomocí Aspose.
draft: false
keywords:
- render html java
- convert html to image
- output png from html
- create image from long html
language: cs
og_description: Vykreslete HTML Java do souboru PNG. Tento průvodce ukazuje, jak převést
  HTML na obrázek, výstup PNG z HTML a vytvořit obrázek z dlouhého HTML pomocí Aspose.
og_title: Renderovat HTML v Javě – Převést dlouhou stránku na PNG
tags:
- Java
- Aspose.HTML
- Image Rendering
title: 'Render HTML v Javě: Převést dlouhou stránku na PNG'
url: /cs/java/conversion-html-to-various-image-formats/render-html-java-convert-long-page-to-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Render HTML Java – Převod dlouhé stránky na PNG

Už jste někdy potřebovali **render HTML Java** a získat ostrý soubor PNG, ale stránka, se kterou pracujete, se táhne donekonečna? Je to častý problém, když máte dlouhou zprávu, seznam faktur nebo rolovací blogový příspěvek, který chcete zachytit jako snímek pro e‑mail nebo archivaci.  

Dobrá zpráva? Můžete **convert HTML to image** pomocí několika řádků Java kódu, díky vykreslovacímu enginu Aspose.HTML. V tomto tutoriálu vás provedeme převodem rozsáhlého HTML dokumentu na jednostránkový PNG, vysvětlíme, proč je každé nastavení důležité, a ukážeme, jak upravit workflow pro jiné výstupní formáty.

Na konci tohoto průvodce budete schopni **output PNG from HTML**, rozdělit multi‑kilobajtovou stránku na zvládnutelné obrazové úseky a dokonce znovu použít stejný přístup k **create image from long HTML** pro PDF, JPEG nebo BMP.

## Co budete potřebovat

- **Java Development Kit (JDK) 8 nebo novější** – kód běží na jakémkoli aktuálním JDK.
- **Aspose.HTML for Java** knihovna (verze 23.10 nebo novější). Můžete ji získat z Maven Central nebo z webu Aspose.
- **Dlouhý HTML soubor**, který chcete vykreslit (v příkladu se používá `longpage.html`).
- IDE nebo textový editor (IntelliJ IDEA, Eclipse, VS Code… podle vás).

Žádné externí služby, žádné nativní binární soubory – vše probíhá v čistém Javě.

## Krok 1: Nastavte projekt a přidejte Aspose.HTML

Nejprve vytvořte nový Maven (nebo Gradle) projekt. Pokud používáte Maven, přidejte závislost Aspose.HTML do souboru `pom.xml`:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

> **Pro tip:** Aspose nabízí bezplatnou 30‑denní zkušební licenci. Umístěte soubor `aspose.html.lic` do classpath, aby se zabránilo vodoznaku z hodnocení.

## Krok 2: Načtěte zdrojový HTML dokument

Nyní načteme HTML, které chcete převést. Třída `HTMLDocument` přijímá URI, takže lokální cestu převedeme na souborové URI pomocí `java.nio.file.Paths`.

```java
import com.aspose.html.HTMLDocument;
import java.nio.file.Paths;

// ...

// Load the HTML file from disk
HTMLDocument htmlDoc = new HTMLDocument(
        Paths.get("YOUR_DIRECTORY/longpage.html")
             .toUri()
             .toString()
);
```

Proč použít **URI**? Aspose.HTML dokáže vyřešit relativní zdroje (CSS, obrázky, fonty) na základě umístění dokumentu, což zajišťuje, že vykreslený obrázek vypadá přesně jako v prohlížeči.

## Krok 3: Definujte možnosti konverze pro jediný úsek

„Dlouhá“ stránka často překračuje výchozí velikost vykreslování. Místo vykreslení celé posouvatelné výšky (která může mít desítky tisíc pixelů) požádáme renderer, aby vytvořil **page slice** – představte si to jako virtuální stránku v PDF.  

Klíčové vlastnosti jsou:

- `setPageWidth(int)`: šířka výstupního obrázku v pixelech.
- `setPageHeight(int)`: výška úseku, který chcete.
- `setPageNumber(int)`: který úsek vykreslit (index od 1).

```java
import com.aspose.html.rendering.ImageConversionOptions;

// ...

ImageConversionOptions conversionOptions = new ImageConversionOptions();
conversionOptions.setPageWidth(1024);   // Desired PNG width
conversionOptions.setPageHeight(1000); // Height of one slice
conversionOptions.setPageNumber(2);    // Render the second slice (1‑based)
```

> **Proč úsek?** Vykreslení celého dokumentu může spotřebovat gigabajty RAM a vytvořit neovladatelný obrázek. Rozdělením zůstáváte šetrní k paměti a můžete úseky později spojit, pokud potřebujete kompletní pohled na stránku.

## Krok 4: Vykreslete úsek do PNG

S připraveným dokumentem a možnostmi provádí `Renderer` těžkou práci. Zabalíme jej do bloku try‑with‑resources, aby se nativní zdroje uvolnily automaticky.

```java
import com.aspose.html.rendering.Renderer;
import java.nio.file.Paths;

// ...

try (Renderer renderer = new Renderer()) {
    renderer.render(
            htmlDoc,
            Paths.get("YOUR_DIRECTORY/page2.png"),
            conversionOptions
    );
}
System.out.println("Second slice rendered to page2.png");
```

Pokud vše proběhne hladce, najdete `page2.png` ve složce target. Otevřete jej v libovolném prohlížeči obrázků – měli byste vidět přesnou část původního HTML, která odpovídá druhému úseku vysokému 1000 pixelů.

## Krok 5: Ověřte výstup a volitelné úpravy

Rychlá kontrola vám pomůže včas zachytit chybějící zdroje nebo problémy s rozvržením.

```java
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import java.io.File;

// ...

BufferedImage img = ImageIO.read(new File("YOUR_DIRECTORY/page2.png"));
System.out.println("Image dimensions: " + img.getWidth() + "x" + img.getHeight());
```

Pokud se rozměry neshodují s nastavenými `PageWidth`/`PageHeight`, zkontrolujte nastavení DPI nebo CSS pravidla `@media print`, která mohou přepisovat velikost.

### Běžné úpravy

| Cíl | Nastavení k úpravě |
|------|------------------|
| **Higher resolution** | `conversionOptions.setResolution(300);` (DPI) |
| **Transparent background** | `conversionOptions.setBackgroundColor(Color.TRANSPARENT);` |
| **Render the whole page** | Vynechte `setPageHeight`/`setPageNumber` – renderer vytvoří výstup celé výšky scrollu jako jeden obrovský PNG. |
| **Create JPEG instead of PNG** | Změňte příponu výstupního souboru na `.jpg`; renderer určí formát podle názvu souboru. |

## Kompletní, spustitelný příklad

Níže je kompletní třída, kterou můžete zkopírovat a vložit do souboru pojmenovaného `PartialImageRender.java`. Nahraďte `YOUR_DIRECTORY` skutečnou cestou ke složce, která obsahuje `longpage.html`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.*;
import java.nio.file.Paths;

/**
 * Demonstrates how to render a specific slice of a long HTML page to PNG.
 * This example uses Aspose.HTML for Java and works with JDK 8+.
 */
public class PartialImageRender {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the source HTML document
        HTMLDocument htmlDoc = new HTMLDocument(
                Paths.get("YOUR_DIRECTORY/longpage.html")
                     .toUri()
                     .toString());

        // Step 2: Define conversion options to render only a specific page slice
        ImageConversionOptions conversionOptions = new ImageConversionOptions();
        conversionOptions.setPageWidth(1024);   // width of the output image
        conversionOptions.setPageHeight(1000); // height of a single page slice
        conversionOptions.setPageNumber(2);    // render the second slice (1‑based)

        // Optional: increase DPI for sharper output
        // conversionOptions.setResolution(300);

        // Step 3: Render the selected page slice to a PNG file
        try (Renderer renderer = new Renderer()) {
            renderer.render(htmlDoc,
                    Paths.get("YOUR_DIRECTORY/page2.png"),
                    conversionOptions);
        }

        // Step 4: Confirm that the image has been created
        System.out.println("Second slice rendered to page2.png");
    }
}
```

Uložte, zkompilujte a spusťte:

```bash
javac -cp "path/to/aspose-html.jar" PartialImageRender.java
java -cp ".:path/to/aspose-html.jar" PartialImageRender
```

Měli byste vidět zprávu v konzoli potvrzující vytvoření PNG.

## Často kladené otázky

**Q: Funguje to s HTML, které obsahuje externí CSS nebo JavaScript?**  
A: Ano. Pokud jsou externí zdroje dostupné přes absolutní URL nebo relativně ke složce HTML souboru, Aspose.HTML je během vykreslování načte. Pro offline scénáře přiložte CSS/JS vedle HTML souboru.

**Q: Co když HTML používá webové fonty?**  
A: Aspose.HTML podporuje `@font-face`. Ujistěte se, že soubory fontů jsou buď vloženy jako base64, nebo umístěny na místo, ke kterému má renderer přístup.

**Q: Můžu vykreslit do PDF místo PNG?**  
A: Rozhodně. Vyměňte `ImageConversionOptions` za `PdfConversionOptions` a změňte příponu výstupního souboru na `.pdf`. Stejná logika rozdělení úseků platí.

**Q: Moje stránka je širší než 1024 px – bude oříznuta?**  
A: Renderer škáluje obsah tak, aby se vešel do zadané šířky, přičemž zachovává poměr stran. Pokud potřebujete plnou šířku, zvyšte `setPageWidth`.

## Závěr

Právě jsme **render HTML Java** do PNG obrázku, rozdělili dlouhou stránku na zvládnutelný úsek a probrali nejčastější úpravy, které můžete potřebovat. Ať už generujete náhledy pro CMS

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}