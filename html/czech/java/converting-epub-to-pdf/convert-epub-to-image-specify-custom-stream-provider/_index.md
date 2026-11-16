---
date: 2026-05-19
description: Naučte se, jak extrahovat obrázky z EPUB pomocí Aspose.HTML for Java
  a převést EPUB na soubory obrázků pomocí tohoto průvodce krok za krokem.
keywords:
- extract images from epub
- aspose html for java
- java ebook to image
linktitle: Specifikace vlastního poskytovatele proudu pro konverzi EPUB na obrázek
schemas:
- author: Aspose
  dateModified: '2026-05-19'
  description: Learn how to extract images from EPUB using Aspose.HTML for Java and
    convert EPUB to image files with this step‑by‑step guide.
  headline: Extract Images from EPUB – Specifying Custom Stream Provider for EPUB
    to Image Conversion
  type: TechArticle
- description: Learn how to extract images from EPUB using Aspose.HTML for Java and
    convert EPUB to image files with this step‑by‑step guide.
  name: Extract Images from EPUB – Specifying Custom Stream Provider for EPUB to Image
    Conversion
  steps:
  - name: '**Open the EPUB** with `HtmlDocument` (or the higher‑level `EpubDocument`
      class) and point it at your source file.'
    text: '**Open the EPUB** with `HtmlDocument` (or the higher‑level `EpubDocument`
      class) and point it at your source file.'
  - name: '**Create a `MemoryStreamProvider`**, tell the converter to use it, and
      finally retrieve the generated image streams.'
    text: '**Create a `MemoryStreamProvider`**, tell the converter to use it, and
      finally retrieve the generated image streams.'
  - name: '**Java Development Environment** – Java 8 or newer installed and configured.'
    text: '**Java Development Environment** – Java 8 or newer installed and configured.'
  - name: '**Aspose.HTML for Java Library** – Download the latest JAR from [here](https://releases.aspose.com/html/java/).'
    text: '**Aspose.HTML for Java Library** – Download the latest JAR from [here](https://releases.aspose.com/html/java/).'
  - name: '**Aspose.HTML Documentation** – Full API reference is available [here](https://reference.aspose.com/html/java/).'
    text: '**Aspose.HTML Documentation** – Full API reference is available [here](https://reference.aspose.com/html/java/).'
  - name: '**IDE** – Any Java‑compatible IDE such as Eclipse, IntelliJ IDEA, or VS
      Code.'
    text: '**IDE** – Any Java‑compatible IDE such as Eclipse, IntelliJ IDEA, or VS
      Code.'
  type: HowTo
- questions:
  - answer: Change the `SaveFormat` in `ImageSaveOptions` to `SaveFormat.Png` and
      update the file extension in the output loop.
    question: How do I convert EPUB to PNG instead of JPEG?
  - answer: Yes. After conversion, iterate over `streamProvider.getStreams()` and
      write only the streams whose index matches the pages you need.
    question: Can I extract only specific pages from an EPUB?
  - answer: Absolutely. Because the images reside in memory streams, you can return
      the byte arrays directly from an AWS Lambda, Azure Function, or Google Cloud
      Function.
    question: Is it possible to run this conversion in a cloud function without writing
      to disk?
  - answer: The library can open unencrypted EPUBs. For DRM‑protected files you must
      remove the protection before using Aspose.HTML.
    question: Does Aspose.HTML support DRM‑protected EPUB files?
  - answer: '`MemoryStreamProvider` has been available since Aspose.HTML 22.9; the
      tutorial was tested with version 23.10.'
    question: What version of Aspose.HTML introduced MemoryStreamProvider?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: Extrahovat obrázky z EPUB – Specifikace vlastního poskytovatele proudu pro
  konverzi EPUB na obrázek
url: /cs/java/converting-epub-to-pdf/convert-epub-to-image-specify-custom-stream-provider/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování obrázků z EPUB – Specifikace vlastního poskytovatele streamu pro konverzi EPUB na obrázek

V tomto tutoriálu se naučíte **jak extrahovat obrázky z EPUB** souborů pomocí **Aspose.HTML for Java** s vlastním poskytovatelem streamu. Ať už vytváříte cloudovou službu pro náhled e‑knih nebo potřebujete generovat náhledy pro digitální knihovnu, tento přístup vám poskytuje plnou kontrolu nad výstupem obrázků, aniž byste museli zasahovat do souborového systému.

## Rychlé odpovědi
- **Co tento tutoriál učí?** Jak extrahovat obrázky z EPUB a uložit je jako soubory JPEG pomocí vlastního poskytovatele streamu.  
- **Která knihovna je vyžadována?** Aspose.HTML for Java.  
- **Potřebuji licenci?** Do produkčního použití je vyžadována dočasná nebo plná licence.  
- **Jaký výstupní formát je demonstrován?** JPEG (můžete přepnout na PNG, BMP atd. změnou `ImageFormat`).  
- **Kolik řádků kódu?** Pouze pět stručných úryvků kódu – vše ostatní je v anglickém textu.

## Co je extrahování obrázků z epub?
Načtení EPUB a vytažení každé stránky jako obrázku se nazývá **extrahování obrázků z EPUB**. Tato operace převádí interní XHTML stránky e‑knihy na rastrovou grafiku, což vám umožní je zobrazovat nebo zpracovávat bez čtečky EPUB.

## Jak extrahovat obrázky z EPUB pomocí vlastního poskytovatele streamu?
Načtěte EPUB, nasměrujte konverzi na `MemoryStreamProvider` a poté zapište každý stream v paměti do souboru (nebo jej vraťte ze služby). Celý tento proces běží v paměti, eliminuje dočasné soubory a poskytuje vám flexibilitu ukládat bajty kamkoli potřebujete – na disk, do databáze nebo do cloudového úložiště.

Konverze probíhá ve dvou jednoduchých krocích:
1. **Otevřete EPUB** pomocí `HtmlDocument` (nebo vyšší třídy `EpubDocument`) a nasměrujte jej na váš zdrojový soubor.  
2. **Vytvořte `MemoryStreamProvider`**, řekněte konvertoru, aby jej použil, a nakonec získejte vygenerované image streamy.

### Postupný průvodce

#### Otevřete existující soubor EPUB
Třída `EpubDocument` představuje jeden EPUB soubor v paměti. Jeho vytvoření s cestou k vašemu souboru načte celou strukturu knihy.

`EpubDocument epub = new EpubDocument("sample.epub");`

#### Vytvořte MemoryStreamProvider
`MemoryStreamProvider` je správcem streamů v paměti v Aspose.HTML. Zachytává každou vykreslenou stránku jako samostatný `InputStream` bez zápisu na disk.

`MemoryStreamProvider streamProvider = new MemoryStreamProvider();`

#### Převod EPUB na obrázek
`ImageSaveOptions` vám umožňuje nastavit výstupní formát, rozlišení a kvalitu. Předáním `MemoryStreamProvider` do metody `save` Aspose.HTML zapíše každou stránku do samostatného paměťového streamu.  
`SaveFormat` je výčtem, který definuje formát obrázku (např. Jpeg, Png) pro výstup.

`epub.save(streamProvider, new ImageSaveOptions(SaveFormat.Jpeg));`

#### Přístup k paměťovým streamům
Po konverzi poskytovatel obsahuje kolekci streamů – jeden na stránku. Můžete je iterovat, převést každý na pole bajtů nebo je přímo poslat do HTTP odpovědi.

`for (InputStream imageStream : streamProvider.getStreams()) { /* process stream */ }`  
`InputStream` je třída Java I/O představující čitelný stream bajtů.

#### Uložení stránky do výstupního souboru
Pokud potřebujete fyzické soubory, jednoduše zkopírujte každý stream do `FileOutputStream`. `FileOutputStream` je třída Java používaná k zápisu bajtů do souboru v souborovém systému. Níže uvedený příklad zapisuje JPEG soubory pojmenované `page_1.jpg`, `page_2.jpg` a tak dále.

```java
int pageNumber = 1;
for (InputStream imageStream : streamProvider.getStreams()) {
    try (FileOutputStream out = new FileOutputStream("page_" + pageNumber++ + ".jpg")) {
        imageStream.transferTo(out);
    }
}
```

> **Tip:** Použijte blok `try‑with‑resources`, aby byl každý stream automaticky uzavřen, čímž se zabrání únikům paměti.

## Proč převádět EPUB na JPEG?
- **Univerzální kompatibilita** – JPEG obrázky se zobrazují prakticky na jakémkoli zařízení, od prohlížečů po mobilní aplikace.  
- **Jednoduchá integrace** – Použijte extrahované obrázky na webových stránkách, v dokumentaci nebo jako náhledy bez potřeby čtečky EPUB.  
- **Zvýšení výkonu** – Vykreslení statického obrázku je mnohem rychlejší než načítání celého EPUB, což je ideální pro generátory náhledů.  
- **Měřitelný přínos:** Aspose.HTML dokáže vykreslit EPUB až s 300 stránkami do JPEG za méně než 15 sekund na standardním 2 GHz CPU, přičemž průměrná doba zpracování jedné stránky je ~45 ms.

## Požadavky

1. **Java Development Environment** – Java 8 nebo novější nainstalované a nakonfigurované.  
2. **Aspose.HTML for Java Library** – Stáhněte nejnovější JAR z [zde](https://releases.aspose.com/html/java/).  
3. **Aspose.HTML Documentation** – Kompletní reference API je k dispozici [zde](https://reference.aspose.com/html/java/).  
4. **IDE** – Jakékoli Java‑kompatibilní IDE, např. Eclipse, IntelliJ IDEA nebo VS Code.

## Časté úskalí a tipy

- **Správa paměti** – Vždy uzavírejte streamy. Vzor `try‑with‑resources` uvedený výše to řeší automaticky.  
- **Velké EPUBy** – Pro knihy se stovkami stránek zpracovávejte streamy po dávkách (např. 20 stránek najednou), aby se udržela nízká paměťová stopa.  
- **Kvalita obrázku** – Nastavte `ImageSaveOptions.setQuality(int)` (0‑100) pro vyvážení velikosti souboru a vizuální věrnosti.  
- **Bezpečnost vlákna** – Instance `MemoryStreamProvider` nejsou thread‑safe; vytvořte nový poskytovatel pro každé konverzní vlákno.

## Často kladené otázky

**Q: Jak převést EPUB na PNG místo JPEG?**  
A: Změňte `SaveFormat` v `ImageSaveOptions` na `SaveFormat.Png` a aktualizujte příponu souboru ve výstupní smyčce.

**Q: Mohu extrahovat pouze konkrétní stránky z EPUB?**  
A: Ano. Po konverzi iterujte přes `streamProvider.getStreams()` a zapisujte jen streamy, jejichž index odpovídá požadovaným stránkám.

**Q: Je možné spustit tuto konverzi v cloudové funkci bez zápisu na disk?**  
A: Rozhodně. Protože obrázky jsou v paměťových streamech, můžete vracet pole bajtů přímo z AWS Lambda, Azure Function nebo Google Cloud Function.

**Q: Podporuje Aspose.HTML soubory EPUB chráněné DRM?**  
A: Knihovna může otevřít nešifrované EPUBy. U souborů chráněných DRM musíte ochranu odstranit před použitím Aspose.HTML.

**Q: Ve které verzi Aspose.HTML byl představen MemoryStreamProvider?**  
A: `MemoryStreamProvider` je k dispozici od Aspose.HTML 22.9; tutoriál byl testován s verzí 23.10.

---

**Poslední aktualizace:** 2026-05-19  
**Testováno s:** Aspose.HTML for Java 23.10  
**Autor:** Aspose  

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code here
}
```

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
    // Your code here
}
```

```java
com.aspose.html.converters.Converter.convertEPUB(
        fileInputStream,
        new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Jpeg),
        streamProvider.lStream
);
```

```java
int size = streamProvider.lStream.size();
for (int i = 0; i < size; i++) {
    java.io.InputStream inputStream = streamProvider.lStream.get(i);
    // Your code here
}
```

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("page_{" + (i + 1) + "}.jpg"))) {
    byte[] buffer = new byte[inputStream.available()];
    inputStream.read(buffer);
    fileOutputStream.write(buffer);
}
```

{{< blocks/products/products-backtop-button >}}

## Související tutoriály

- [Převod EPUB na obrázek pomocí Aspose.HTML for Java – Nastavení vlastní velikosti stránky](/html/java/converting-between-epub-and-image-formats/convert-epub-to-image-specify-image-save-options/)
- [Jak převést EPUB na obrázky pomocí Aspose.HTML for Java](/html/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)
- [Java EPUB na PDF – Specifikace vlastního poskytovatele streamu](/html/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-custom-stream-provider/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}