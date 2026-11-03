---
category: general
date: 2026-03-05
description: Készíts PDF-et HTML-ből gyorsan az Aspose.HTML segítségével – állíts
  be egy egyedi PDF oldalméretet, ágyazz be betűtípusokat, és tanuld meg, hogyan konvertálj
  HTML-t PDF-be teljes kóddal.
draft: false
keywords:
- create pdf from html
- convert html to pdf
- html to pdf conversion
- custom pdf page size
- embed fonts pdf
language: hu
og_description: PDF létrehozása HTML-ből az Aspose.HTML segítségével. Ez az útmutató
  bemutatja, hogyan állíthat be egy egyedi PDF oldalméretet, ágyazhat be betűtípusokat
  a PDF-be, és hajthat végre HTML‑PDF konverziót.
og_title: PDF létrehozása HTML‑ből – Egyedi oldalméret és beágyazott betűtípusok
tags:
- Java
- PDF
- Aspose.HTML
title: PDF létrehozása HTML-ből egyedi oldalmérettel és beágyazott betűtípusokkal
url: /hu/java/conversion-html-to-other-formats/create-pdf-from-html-with-custom-page-size-and-embedded-font/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF létrehozása HTML-ből egyedi oldalmérettel és beágyazott betűtípusokkal

Valaha is szükséged volt **PDF létrehozására HTML-ből**, de a stílusozásnál elakadtál? Nem vagy egyedül. Akár egy marketing landing oldalt szeretnél nyomtatható brosúrává alakítani, akár egy webalkalmazásban generált számlákat archiválsz, valószínűleg egy olyan PDF-re vágysz, amely pontosan megfelel a márkád méreteinek, és minden betűtípust élesen jelenít meg.

Ebben az útmutatóban egy teljes, azonnal futtatható példán keresztül mutatjuk be, hogyan **konvertálhatod a HTML-t PDF-re** az Aspose.HTML for Java segítségével, hogyan állíthatsz be **egyedi PDF oldalméretet**, és hogyan engedélyezheted a **betűtípusok beágyazását PDF-be**, hogy a kimenet minden gépen azonos legyen. A végére egyetlen Java osztályod lesz, amelyet beilleszthetsz a projektedbe, és azonnal PDF-eket generálhatsz.

## Mit fogsz megtanulni

* Hogyan adhatod hozzá az Aspose.HTML könyvtárat egy Maven vagy Gradle projekthez.  
* Hogyan konfigurálhatod a **PdfConversionOptions**-t egy **egyedi pdf oldalméret** beállításához (ebben az esetben 8,5 × 11 hüvelyk).  
* Hogyan kapcsolhatod be a **betűtípusok beágyazását pdf**-ben, hogy a szöveg helyesen jelenjen meg akkor is, ha a célrendszer nem rendelkezik az eredeti betűtípusokkal.  
* Hogyan futtathatod a **HTML to PDF conversion**-t, és olvashatod ki a kapott oldalszámot.  

Nincs felesleges részlet, csak egy gyakorlati, vég‑től‑végig megoldás, amelyet egyszerűen átmásolhatsz.

## Előfeltételek

Mielőtt belemerülnénk, győződj meg róla, hogy rendelkezel:

* Java 17 vagy újabb telepítve (az API Java 8+ verzióval is működik, de az újabb JDK-k jobb teljesítményt nyújtanak).  
* Egy build eszköz – Maven vagy Gradle – az Aspose.HTML JAR letöltéséhez a Maven Central tárolóból.  
* Egy HTML fájl (`sample.html`), amelyet PDF‑vé szeretnél alakítani.  
* Egy kis kíváncsiság a PDF oldalelrendezés iránt – ezt a kódban fogjuk lefedni.  

> **Pro tipp:** Ha nincs kéznél HTML fájlod, egyszerűen hozz létre egyet egy `<h1>` és egy bekezdés segítségével; a konverzió ugyanúgy működik.

## 1. lépés: Aspose.HTML hozzáadása a projekthez (HTML konvertálása PDF-re)

Ha **Maven**-t használsz, helyezd el a következő függőséget a `pom.xml`-edbe:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- latest at time of writing -->
</dependency>
```

Gradle esetén add hozzá ezt a sort a `build.gradle`-hez:

```gradle
implementation 'com.aspose:aspose-html:23.12'
```

Ez az egyetlen sor mindent biztosít, amire a **html to pdf conversion**-hez szükséged van – a `Converter`‑t, az opció osztályokat és a rajzoló segédeszközöket.

## 2. lépés: Egyedi PDF oldalméret konfigurálása (Custom PDF Page Size)

Most, hogy a könyvtár a classpath‑on van, elkezdhetjük formálni a kimenetet. A `PdfConversionOptions` objektum lehetővé teszi az oldal méreteinek, margóinak és a betűtípusok beágyazásának beállítását. Íme a kód, amely **egyedi pdf oldalméretet** állít be 8,5 × 11 hüvelyk mérettel, fél hüvelykes margókkal minden oldalon:

```java
// Step 2: Create PDF conversion options and configure page size, margins, and font embedding
PdfConversionOptions pdfOptions = new PdfConversionOptions();

// Set a custom PDF page size – 8.5 × 11 inches (Letter)
pdfOptions.setPageSize(new SizeF(Unit.inch(8.5), Unit.inch(11)));

// Margins are also expressed in inches; here we use 0.5 in on each side
pdfOptions.setMargins(0.5, 0.5, 0.5, 0.5); // left, top, right, bottom

// Enable font embedding so the PDF looks the same everywhere
pdfOptions.setEmbedFonts(true);
```

Vedd észre a `setEmbedFonts(true)` hívást. Ez a jelző azt mondja az Aspose.HTML-nek, hogy **betűtípusokat ágyazzon be PDF** fájlokba, ezzel megszüntetve a “hiányzó betűtípus” problémát, amelyet néha láthatsz, amikor egy PDF-et másik számítógépen nyitsz meg.

## 3. lépés: HTML‑PDF konverzió végrehajtása

Miután az opciók készen állnak, a tényleges konverzió egyetlen soros. A `Converter`‑t a forrás HTML fájlra és a cél PDF fájlra irányítjuk, majd átadjuk neki a most épített opciókat:

```java
// Step 3: Convert the HTML file to PDF using the configured options
String htmlPath = "YOUR_DIRECTORY/sample.html";
String pdfPath  = "YOUR_DIRECTORY/custom.pdf";

PdfConversionResult conversionResult = Converter.convertHTML(htmlPath, pdfPath, pdfOptions);
```

Ha minden simán megy, a `conversionResult` tartalmazni fogja a generált PDF metaadatait, például az oldalak számát.

## 4. lépés: Kimenet ellenőrzése – Oldalszám ellenőrzése

Mindig jó megerősíteni, hogy a konverzió sikeres volt. A `PdfConversionResult` gyors módot biztosít az oldalszám kiolvasására:

```java
// Step 4: Output the number of pages in the generated PDF
System.out.println("Custom PDF created, pages: " + conversionResult.getPageCount());
```

A program futtatása valami ilyesmit kell, hogy kiírjon:

```
Custom PDF created, pages: 1
```

Ez a sor azt jelzi, hogy a **html to pdf conversion** egy egyoldalas PDF-et hozott létre, amely megfelel a megadott **custom pdf page size**-nek. Ha a forrás HTML hosszabb, automatikusan nagyobb oldalszámot fogsz látni.

## Teljes működő példa

Az alábbiakban a teljes Java osztály található, amelyet bemásolhatsz egy `ConvertHtmlToPdfWithOptions.java` nevű fájlba. Cseréld ki a `YOUR_DIRECTORY`-t arra a tényleges mappára, ahol a `sample.html` található.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.pdf.PdfConversionOptions;
import com.aspose.html.converters.pdf.PdfConversionResult;
import com.aspose.html.drawing.SizeF;
import com.aspose.html.drawing.Unit;

public class ConvertHtmlToPdfWithOptions {
    public static void main(String[] args) throws Exception {

        // Step 1: Create PDF conversion options and configure page size, margins, and font embedding
        PdfConversionOptions pdfOptions = new PdfConversionOptions();
        pdfOptions.setPageSize(new SizeF(Unit.inch(8.5), Unit.inch(11)));
        pdfOptions.setMargins(0.5, 0.5, 0.5, 0.5);   // left, top, right, bottom (in inches)
        pdfOptions.setEmbedFonts(true);            // embed fonts PDF for consistent rendering

        // Step 2: Convert the HTML file to PDF using the configured options
        String htmlPath = "YOUR_DIRECTORY/sample.html";
        String pdfPath  = "YOUR_DIRECTORY/custom.pdf";
        PdfConversionResult conversionResult = Converter.convertHTML(htmlPath, pdfPath, pdfOptions);

        // Step 3: Output the number of pages in the generated PDF
        System.out.println("Custom PDF created, pages: " + conversionResult.getPageCount());
    }
}
```

### Várható eredmény

Miután lefordítod (`javac ConvertHtmlToPdfWithOptions.java`) és futtatod az osztályt (`java ConvertHtmlToPdfWithOptions`), a `custom.pdf` fájlt ugyanabban a mappában fogod megtalálni. Nyisd meg bármely PDF‑megjelenítővel; a **custom pdf page size**-en megjelenő eredeti HTML‑t kell látnod, minden betűtípus helyesen beágyazva. Nincsenek hiányzó karakter figyelmeztetések, nincs eltolódás a layoutban.

![Create PDF from HTML example showing the generated PDF preview](/images/create-pdf-from-html-preview.png "create pdf from html preview")

## Gyakori kérdések és speciális esetek

**Mi van, ha a HTML külső CSS‑re vagy képekre hivatkozik?**  
Az Aspose.HTML ugyanazokat a szabályokat követi, mint egy böngésző. Amíg az útvonalak abszolútak vagy a HTML fájl helyéhez relatívak, a konverter be fogja húzni őket. Távoli URL‑ek esetén győződj meg róla, hogy a konverziót futtató gépnek van internetkapcsolata.

**Meg tudom változtatni az oldal tájolását fekvőre?**  
Természetesen. Csak cseréld fel a szélesség és magasság értékeket a `setPageSize` hívásakor:

```java
pdfOptions.setPageSize(new SizeF(Unit.inch(11), Unit.inch(8.5)));
```

**Szükségem van licencre az Aspose.HTML használatához éles környezetben?**  
A könyvtár értékelő módban működik, de vízjelet helyez a PDF‑be. Kereskedelmi projektekhez érvényes licencfájlra lesz szükséged – egyszerűen töltsd be a program elején a `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` kóddal.

**Mi a helyzet az Unicode betűtípusokkal?**  
Ha a HTML nem latin karaktereket tartalmaz, győződj meg arról, hogy a beágyazott betűtípusok támogatják ezeket a kódpontokat. A `setEmbedFonts(true)` beállítása az egész betűtípusfájlt beágyazza, így a PDF Unicode‑ot helyesen jelenít meg bármely eszközön.

## Összegzés

Most már pontosan tudod, hogyan **hozz létre PDF-et HTML‑ből**, miközben a **custom pdf page size**-t szabályozod, és biztosítod, hogy a végső dokumentum **betűtípusok beágyazásával PDF** legyen, a hibátlan, platformok közötti megjelenítés érdekében. A példa lefedi a teljes **html to pdf conversion** folyamatot – a függőség beállításától, az opciók konfigurálásán át, egészen a kimenet ellenőrzéséig.

Szeretnél tovább menni? Próbálj ki például:

* **Több oldalméret** egyetlen dokumentumban (különböző opciók konverziónként).  
* **Fejléc/lábléc sablonok** az Aspose.HTML `PdfPageSettings`‑ével.  
* **Biztonsági funkciók**, például jelszóvédelem (`PdfEncryptionOptions`).  

Mindegyik ezek közül ugyanarra az alapra épül, amelyet most felállítottunk, így könnyedén meg tudod valósítani őket problémamentesen.

Boldog kódolást, és élvezd, ahogy a weboldalaid tökéletesen formázott PDF‑ekké válnak!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}