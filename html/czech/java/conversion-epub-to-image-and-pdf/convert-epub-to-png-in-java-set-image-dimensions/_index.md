---
category: general
date: 2026-04-09
description: Naučte se, jak v Javě převést EPUB na PNG, nastavit rozměry obrázku v
  Java stylu a extrahovat pouze první stránku jako PNG obálku. Krátký ukázkový kód
  je zahrnut.
draft: false
keywords:
- convert epub to png
- set image dimensions java
- convert first page png
- aspose html java
- ebook cover generation
language: cs
og_description: Převod EPUB na PNG v Javě, nastavení rozměrů obrázku v Javě a extrakce
  pouze první stránky jako PNG obálky s kompletním, spustitelným příkladem.
og_title: Převod EPUB na PNG v Javě – Nastavení rozměrů obrázku
tags:
- Java
- Aspose.HTML
- Image Processing
title: Převod EPUB na PNG v Javě – Nastavení rozměrů obrázku
url: /cs/java/conversion-epub-to-image-and-pdf/convert-epub-to-png-in-java-set-image-dimensions/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod EPUB na PNG v Javě – Nastavení rozměrů obrázku

Už jste se někdy zamýšleli, jak **převést EPUB na PNG** bez tahání těžké grafické knihovny? Nejste v tom sami. Mnoho vývojářů potřebuje rychlý způsob, jak vygenerovat obrázek obálky nebo miniaturu z e‑knihy, ale naráží na to, že API vyžaduje další kroky pro výběr stránky a nastavení velikosti.  

V tomto průvodci projdeme kompletní řešení, které nejen **převádí EPUB na PNG**, ale také vám umožní **nastavit rozměry obrázku v Javě** a **převést první stránku do PNG** pomocí několika řádků kódu. Na konci budete mít připravený program, který vytvoří ostrý PNG o rozměrech 1024 × 1440 první stránky libovolného EPUB souboru.

## Co budete potřebovat

- Java 17 nebo novější (kód funguje i se staršími verzemi, ale 17 je aktuální LTS).  
- Knihovna Aspose.HTML for Java (Maven koordináta je `com.aspose:aspose-html:23.10`).  
- EPUB soubor, který chcete převést na obrázek.  
- Jakékoli IDE nebo prostý příkazový řádek `javac`/`java`.

To je vše – žádné další nástroje na zpracování obrázků, žádné nativní binárky. Pouze jeden JAR a kousek Javy.

## Krok 1: Načtení EPUB dokumentu  

První věc, kterou musíme udělat, je dát Aspose.HTML něco, s čím může pracovat. Načtení EPUB je tak jednoduché, jako předat konstruktoru `HTMLDocument` cestu k souboru.

```java
import com.aspose.html.HTMLDocument;

// ...

// Replace with the actual path to your EPUB file
String epubPath = "YOUR_DIRECTORY/input.epub";

// Load the EPUB into an HTMLDocument object
HTMLDocument epubDocument = new HTMLDocument(epubPath);
```

*Proč je to důležité:* `HTMLDocument` abstrahuje interní HTML, CSS a assety EPUB do jediného objektu, který může konvertor vykreslit. Pokud tento krok vynecháte, knihovna nebude vědět, co má kreslit.

## Krok 2: Nastavení rozměrů obrázku v Javě  

Dále nakonfigurujeme, jak má výstupní PNG vypadat. Třída `ImageSaveOptions` vám umožní řídit číslo stránky, šířku, výšku a několik dalších příznaků vykreslování.

```java
import com.aspose.html.converters.ImageSaveOptions;

// ...

ImageSaveOptions imageOptions = new ImageSaveOptions();

// Render only the first page (the cover is usually page 1)
imageOptions.setPageNumber(1);

// Define the desired output size – this is where we **set image dimensions java**
imageOptions.setWidth(1024);   // pixels
imageOptions.setHeight(1440); // pixels
```

*Proč můžete chtít změnit tato čísla:* Různé platformy vyžadují různé velikosti miniatur. Pro obálku Kindle můžete použít 1600 × 2400, zatímco webová ukázka může být tak malá jako 300 × 400. Upravit šířku/výšku podle vašeho použití.

## Krok 3: Převod první stránky do PNG  

Nyní přichází samotný převod. Předáme `HTMLDocument`, právě vytvořené možnosti a cílovou cestu statické metodě `Converter.convertHTML`.

```java
import com.aspose.html.converters.Converter;

// ...

// Output file – this will be the PNG of the first page
String outputPath = "YOUR_DIRECTORY/cover.png";

// Perform the conversion
Converter.convertHTML(epubDocument, imageOptions, outputPath);
```

*Proč to funguje:* Aspose.HTML vykreslí první stránku EPUB do off‑screen bitmapy a poté tuto bitmapu zapíše do PNG souboru s rozměry, které jste zadali. Operace je synchronní a v případě chyby vyhodí výjimku, takže ji můžete obalit do `try‑catch` bloku pro produkční kód.

## Krok 4: Ověření výsledku  

Po dokončení programu by se v určeném umístění měl objevit soubor `cover.png`. Otevřete jej v libovolném prohlížeči obrázků a zkontrolujte:

- Rozměry obrázku odpovídají nastaveným hodnotám (v našem příkladu 1024 × 1440).  
- Obsah odpovídá první stránce EPUB (obvykle obálka nebo titulní stránka).  

Pokud obrázek vypadá deformovaně, zkontrolujte poměr stran, který jste zvolili; můžete zachovat původní proporci tím, že nastavíte buď šířku **nebo** výšku.

## Krok 5: Časté problémy a tipy  

| Problém | Proč se vyskytuje | Řešení |
|------|----------------|-----|
| **Prázdný obrázek** | EPUB obsahuje externí fonty, které nejsou vloženy. | Nainstalujte chybějící fonty na hostitelském počítači nebo je vložte do EPUB. |
| **Špatná stránka vykreslena** | `setPageNumber` je v některých starších verzích číslováno od nuly. | Ověřte verzi knihovny; pro Aspose.HTML 23.x je API číslováno od jedné, jak je ukázáno. |
| **Chyby out‑of‑memory** u velkých stránek | Vykreslování ve velmi vysokých rozlišeních spotřebuje hodně RAM. | Snižte šířku/výšku nebo zvětšete haldu JVM (`-Xmx2g`). |
| **Soubor nenalezen** | Cesty používají zpětná lomítka ve Windows bez escapování. | Používejte lomítka dopředu nebo `Paths.get(...)` pro tvorbu platformně nezávislých cest. |

*Tip:* Pokud potřebujete generovat miniatury pro každou stránku EPUB, jednoduše projděte čísla stránek ve smyčce a změňte `imageOptions.setPageNumber(i)` uvnitř smyčky. Nezapomeňte každému výstupnímu souboru dát unikátní název, např. `cover_page_1.png`, `cover_page_2.png` atd.

## Kompletní funkční příklad  

Níže je kompletní, připravená Java třída. Zkopírujte ji do souboru s názvem `EpubToPng.java`, upravte cesty a spusťte.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.ImageSaveOptions;

/**
 * Demonstrates how to convert an EPUB file to a PNG image,
 * set custom image dimensions, and export only the first page.
 */
public class EpubToPng {
    public static void main(String[] args) throws Exception {

        // --------------------------------------------------------------------
        // Step 1: Load the EPUB document
        // --------------------------------------------------------------------
        // Replace with your actual EPUB location
        HTMLDocument epubDocument = new HTMLDocument("YOUR_DIRECTORY/input.epub");

        // --------------------------------------------------------------------
        // Step 2: Configure conversion options (first page, dimensions)
        // --------------------------------------------------------------------
        ImageSaveOptions imageOptions = new ImageSaveOptions();
        imageOptions.setPageNumber(1);   // Render only the first page
        imageOptions.setWidth(1024);     // Desired width in pixels
        imageOptions.setHeight(1440);    // Desired height in pixels

        // --------------------------------------------------------------------
        // Step 3: Convert the selected page to a PNG image
        // --------------------------------------------------------------------
        // Output PNG path – this will hold the result of the conversion
        Converter.convertHTML(epubDocument, imageOptions, "YOUR_DIRECTORY/cover.png");

        System.out.println("✅ Conversion complete! Check YOUR_DIRECTORY/cover.png");
    }
}
```

**Očekávaný výstup:** Po spuštění `java EpubToPng` konzole vypíše zprávu o úspěchu a v adresáři najdete `cover.png` o rozměrech **1024 × 1440** pixelů, zobrazující první stránku vašeho EPUB.

## Závěr  

Nyní máte solidní, samostatný recept na **převod EPUB na PNG** v Javě, **nastavení rozměrů obrázku v Javě** podle potřeby a **převod první stránky do PNG** pro generování obálek nebo miniatur. Přístup je lehký, spoléhá se na jediný volání Aspose.HTML a lze jej snadno rozšířit na hromadné zpracování více EPUBů nebo více stránek s minimálními úpravami.

---

### Co dál?

- **Hromadný převod:** Zabalte logiku do skeneru adresářů a automaticky zpracovávejte desítky EPUB souborů.  
- **Dynamické velikosti:** Vypočítejte šířku/výšku na základě poměru stran původní stránky, abyste předešli roztažení.  
- **Alternativní výstupní formáty:** Vyměňte `ImageSaveOptions` za `PdfSaveOptions` nebo `JpegSaveOptions`, pokud potřebujete místo PNG PDF nebo JPEG.  

Klidně experimentujte – změňte rozměry, vyzkoušejte jinou číslici stránky nebo integrujte tento úryvek do většího nástroje pro správu e‑knih. Pokud narazíte na problémy, dokumentace Aspose.HTML for Java je dobrým průvodcem, ale výše uvedený kód by měl fungovat „out‑of‑the‑box“ ve většině scénářů.

Šťastné kódování a užijte si ostré PNG obálky!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}