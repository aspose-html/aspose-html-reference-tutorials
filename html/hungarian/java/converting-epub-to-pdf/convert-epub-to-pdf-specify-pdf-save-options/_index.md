---
date: 2026-05-30
description: Ismerje meg, hogyan konvertálhatja az EPUB-ot PDF-re Java-ban az Aspose.HTML
  segítségével, miközben egyéni PDF oldalméretet és egyéb PDF mentési beállításokat
  állít be.
keywords:
- custom pdf page size
- convert epub to pdf
- change pdf background color
- specify pdf page dimensions
- aspose.html java
linktitle: PDF mentési beállítások megadása EPUB → PDF esetén
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  headline: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  type: TechArticle
- description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  name: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  steps:
  - name: Open the EPUB File
    text: First, create a `FileInputStream` that points to your source `.epub`. Keeping
      the stream open until the conversion finishes prevents “blank page” errors.
  - name: Define PDF Save Options
    text: '`PdfSaveOptions` is Aspose.HTML''s configuration class that controls PDF
      output settings such as page size, background color, and margins. `Length.fromPixels`
      converts screen pixels to PDF points (1 point = 1/72 inch), allowing you to
      specify dimensions in familiar pixel units.'
  - name: Convert EPUB to PDF
    text: With the input stream and custom options ready, invoke the converter. The
      output PDF will be saved to the location you specify, preserving the exact page
      dimensions you defined. `PdfSaveOptions.setEnableParallelProcessing` is a method
      that enables parallel processing of pages during PDF conversion.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a commercial library, but you can obtain a free
      trial version from their [website](https://releases.aspose.com/).
    question: Is Aspose.HTML for Java a free library?
  - answer: Aspose.HTML for Java supports EPUB 2.0, EPUB 3.0, and EPUB 3.1, handling
      re‑flowable and fixed‑layout books with full CSS support.
    question: What EPUB formats are supported for conversion?
  - answer: Yes, you can customize the PDF output by adjusting the page setup, background
      color, compression level, and other settings in the `PdfSaveOptions`.
    question: Can I customize the PDF output further?
  - answer: The trial version may add a watermark to the first few pages and limits
      the maximum file size to 10 MB; purchase a license to remove these restrictions.
    question: Are there any limitations to the trial version of Aspose.HTML for Java?
  - answer: You can find answers to your questions and seek support on the [Aspose.HTML
      forum](https://forum.aspose.com/).
    question: Where can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: Egyéni PDF oldalméret - PDF mentési beállítások megadása EPUB → PDF esetén
url: /hu/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Egyéni PDF oldalméret: PDF mentési beállítások megadása EPUB-ból PDF-be

## Bevezetés

Aspose.HTML for Java megkönnyíti az **EPUB konvertálását PDF-be**, és teljes irányítást ad a kimenet felett, beleértve az **egyéni PDF oldalméret** beállítását is. Ebben a lépésről‑lépésre útmutatóban mindent végigvezetünk, amire szüksége lehet – a környezet előkészítésétől a `PdfSaveOptions` finomhangolásáig, hogy a generált PDF pontosan a kívánt oldalméretekkel rendelkezzen. Akár kiadói folyamatot, e‑learning platformot épít, vagy egyszerűen csak automatizálni szeretné a dokumentumkonverziót, itt hasznos technikákat talál.

## Gyors válaszok
- **Mi a fő célja ennek az útmutatónak?** Egy EPUB fájl konvertálása PDF-be egyéni PDF oldalmérettel.  
- **Melyik könyvtárat használja?** Aspose.HTML for Java.  
- **Szükségem van licencre?** Ingyenes próba elérhető; a kereskedelmi licenc szükséges a termeléshez.  
- **Megváltoztathatom a háttérszínt?** Igen, a `PdfSaveOptions` használatával.  
- **Támogatott a Java 8+?** Teljesen – bármely modern Java futtatókörnyezet működik.

## Mi az egyéni PDF oldalméret?

Egy egyéni PDF oldalméret lehetővé teszi, hogy meghatározza a kimeneti PDF minden oldalának pontos szélességét és magasságát, ahelyett, hogy a szabványos méretekre, például A4 vagy Letter, támaszkodna.  
A méreteket pontokban (1 pont = 1/72 hüvelyk) vagy pixelből konvertálva állíthatja be, így pixel‑pontos irányítást kap a végső elrendezés felett. Ez ideális e‑könyvekhez, szórólapokhoz vagy bármilyen tervezéshez, amelynek előre meghatározott formátumhoz kell illeszkednie manuális utófeldolgozás nélkül.

## Miért használja az Aspose.HTML-t EPUB‑ból PDF‑be konverzióhoz?

Aspose.HTML két kódsorban konvertálja az EPUB-et PDF-be, miközben megőrzi a komplex elrendezéseket, beágyazott betűtípusokat és a nagy felbontású képeket. Támogat **50+ bemeneti és kimeneti formátumot**, képes akár **2 000 oldalas** PDF-ek renderelésére anélkül, hogy a teljes fájlt a memóriába töltené, és Windows, Linux, valamint macOS rendszereken azonos eredményeket nyújt. A könyvtár részletes PDF‑mentési beállításokat is kínál, lehetővé téve az oldalméret, háttérszín, margók és tömörítési beállítások finomhangolását – mind Java‑ból.

## Előkövetelmények
- **Java fejlesztői környezet:** JDK 8 vagy újabb telepítve és konfigurálva.  
- **Aspose.HTML for Java:** Töltse le a legújabb JAR‑t a [weboldalról](https://releases.aspose.com/html/java/).  
- **EPUB fájl:** Egy `.epub` dokumentum, amelyet konvertálni szeretne.

Most, hogy minden készen áll, merüljünk el a tényleges konverziós lépésekben.

## Hogyan konvertáljunk EPUB-et PDF-be egyéni oldalmérettel?

`FileInputStream` egy Java osztály, amely nyers bájtokat olvas egy fájlból.  
`PdfSaveOptions` egy Aspose.HTML‑ben található osztály, amely a PDF kimeneti beállításokat konfigurálja, például az oldalméretet és a háttérszínt.  
Töltse be az EPUB-et egy `FileInputStream`‑el, konfigurálja a `PdfSaveOptions`‑t a pontos oldalméretek megadásához, és hívja meg a konvertálót. Az alábbi háromlépéses munkafolyamat egy perc alatt elvégzi a konverziót a tipikus e‑könyv méretek esetén, és minimális kómmódosítással skálázható nagyobb gyűjteményekhez is.

### 1. lépés: Az EPUB fájl megnyitása

Először hozzon létre egy `FileInputStream`‑et, amely a forrás `.epub` fájlra mutat. A stream nyitva tartása a konverzió befejezéséig megakadályozza a „blank page” (üres oldal) hibákat.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

### 2. lépés: PDF mentési beállítások meghatározása

`PdfSaveOptions` az Aspose.HTML konfigurációs osztálya, amely a PDF kimeneti beállításokat szabályozza, például az oldalméretet, háttérszínt és margókat.  
`Length.fromPixels` a képernyő pixeljeit PDF pontokra (1 pont = 1/72 hüvelyk) konvertálja, lehetővé téve a méretek megadását ismerős pixel egységekben.

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

#### Pro tipp:
- **Pixelek vs. pontok:** `Length.fromPixels` a képernyő pixeljeit PDF pontokra konvertálja (1 pont = 1/72 hüvelyk). Válasszon olyan értékeket, amelyek a kívánt végső nyomtatott méretet tükrözik.

### 3. lépés: EPUB konvertálása PDF-be

A bemeneti stream és az egyéni beállítások készen állnak, hívja meg a konvertálót. A kimeneti PDF a megadott helyre lesz mentve, megőrizve a meghatározott pontos oldalméreteket.

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

`PdfSaveOptions.setEnableParallelProcessing` egy metódus, amely a PDF konverzió során engedélyezi az oldalak párhuzamos feldolgozását.

## Teljes forráskód

A teljes, futtatható példa egyesíti a fenti három lépést egyetlen Java osztályba. Cserélje le a helyőrző útvonalakat a saját fájlhelyeire.

```java
Specifying PDF Save Options for EPUB to PDF
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of the PdfSaveOptions with a custom page-size and a background-color.
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
            // Call the ConvertEPUB method to convert the EPUB to PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```

## Gyakori problémák és megoldások

| Probléma | Ok | Megoldás |
|-------|-------|-----|
| **PDF pages are blank** | Input stream closed before conversion | Keep the `try‑with‑resources` block open until after `convertEPUB`. |
| **Incorrect page dimensions** | Using pixels that don’t map to desired print size | Convert desired inches to points (`1 inch = 72 points`) and then to pixels using `Length.fromPixels`. |
| **Missing fonts** | Fonts not embedded in EPUB | Ensure the fonts are packaged inside the EPUB or install them on the host machine. |
| **Performance slowdown on large books** | Rendering every page sequentially | Enable multi‑threaded rendering via `PdfSaveOptions.setEnableParallelProcessing(true)` for faster processing of 500+ page EPUBs. |

## Gyakran Ismételt Kérdések (GYIK)

**Q: Az Aspose.HTML for Java ingyenes könyvtár?**  
A: Az Aspose.HTML for Java egy kereskedelmi könyvtár, de ingyenes próba verziót szerezhet a [weboldalukról](https://releases.aspose.com/).

**Q: Milyen EPUB formátumok támogatottak a konverzióhoz?**  
A: Az Aspose.HTML for Java támogatja az EPUB 2.0, EPUB 3.0 és EPUB 3.1 formátumokat, kezelve a folyékony és rögzített elrendezésű könyveket teljes CSS támogatással.

**Q: Testreszabhatom a PDF kimenetet tovább?**  
A: Igen, a PDF kimenetet testreszabhatja az oldalbeállítások, háttérszín, tömörítési szint és egyéb `PdfSaveOptions` beállítások módosításával.

**Q: Vannak korlátozások az Aspose.HTML for Java próba verziójában?**  
A: A próba verzió vízjelet helyezhet az első néhány oldalra, és a maximális fájlméretet 10 MB-ra korlátozza; licenc vásárlásával eltávolíthatja ezeket a korlátozásokat.

**Q: Hol kaphatok támogatást az Aspose.HTML for Java-hoz?**  
A: Válaszokat és támogatást találhat a [Aspose.HTML fórumon](https://forum.aspose.com/).

---

**Utoljára frissítve:** 2026-05-30  
**Tesztelve ezzel:** Aspose.HTML for Java 24.11 (legújabb a megírás időpontjában)  
**Szerző:** Aspose

## Kapcsolódó oktatóanyagok

- [PDF oldalméret módosítása Aspose.HTML for Java segítségével](/html/java/advanced-usage/adjust-pdf-page-size/)
- [Hogyan konvertáljunk EPUB-et PDF-be Java‑val – Aspose.HTML használatával](/html/java/conversion-epub-to-image-and-pdf/convert-epub-to-pdf/)
- [EPUB konvertálása PDF‑be és képekké Aspose.HTML for Java segítségével](/html/java/conversion-epub-to-image-and-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}