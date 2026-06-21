---
category: general
date: 2026-04-26
description: HTML konvertálása PDF-re Java-ban az Aspose.HTML segítségével – tanulja
  meg, hogyan állíthatja be a PDF oldalméretét, adhat hozzá PDF margókat, és néhány
  sorban exportálhatja a HTML-t PDF-be.
draft: false
keywords:
- convert html to pdf
- set pdf page size
- add pdf margins
- export html as pdf
- how to set margins
language: hu
og_description: HTML konvertálása PDF-re Java-ban az Aspose.HTML segítségével. Ez
  az útmutató megmutatja, hogyan állítható be a PDF oldalmérete, hogyan adhatók hozzá
  PDF margók, és hogyan exportálható gyorsan a HTML PDF formátumba.
og_title: HTML konvertálása PDF-re Java-ban – Oldalméret és margók beállítása
tags:
- Java
- Aspose.HTML
- PDF conversion
title: HTML konvertálása PDF-re Java-ban – Oldalméret és margók beállítása
url: /hu/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-set-page-size-margins/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML konvertálása PDF-be Java-ban – Oldalméret és margók beállítása

Szükséged van **HTML PDF-be konvertálására Java-ban**? Küzdesz a **PDF oldalméret beállításával** vagy a **PDF margók hozzáadásával**? Nem vagy egyedül. Sok projektben a végső PDF-nek meg kell felelnie a vállalati arculatnak, ami pontos oldalméreteket és rendezett margókat jelent.  

Ebben az útmutatóban egy teljes, azonnal futtatható példán keresztül mutatjuk be, hogyan **exportálhatod a HTML-t PDF-be** az Aspose.HTML könyvtár segítségével. A végére megtanulod, *hogyan állíts be margókat*, és miért lehet a PDF‑A‑1b megfelelés életmentő az archiválás során. Nincsenek homályos hivatkozások – csak a kód, amit másolhatsz és futtathatsz.

## Amire szükséged lesz

- **Java 17** (vagy bármely friss JDK) – az API Java 8+ verzióval működik, de az újabb verziók jobb teljesítményt nyújtanak.  
- **Aspose.HTML for Java** JAR-ok – letöltheted őket a Maven Central tárolóból vagy az Aspose weboldaláról.  
- Egy egyszerű **input.html** fájl, amelyet PDF‑be szeretnél konvertálni.  
- Egy kis lemezterület a kimeneti fájlhoz (a PDF néhány száz kilobájt lesz).  

Ennyi. Nincs szükség további keretrendszerekre, nincs külső szolgáltatás. Ha megvannak ezek a részek, kezdhetünk.

## HTML PDF-be konvertálása – Lépésről‑lépésre áttekintés

Az alábbiakban a magas szintű folyamatot láthatod, amelyet követni fogunk:

1. **Point to the HTML source** – helyi fájl, távoli URL vagy egy `InputStream`.  
2. **Configure PDF saving options** – oldalméret, margók és PDF‑A megfelelőség beállítása.  
3. **Run the conversion** – hagyd, hogy az Aspose végezze a nehéz munkát.  

Ezek a lépések külön szekciókba vannak bontva, így a szükséges részeket könnyen kiválaszthatod.

## 1. lépés: A HTML forrás megadása

Az első dolog, amire a konvertálónak szüksége van, egy hivatkozás a PDF‑be konvertálni kívánt HTML-re. Az Aspose.HTML rugalmas: megadhatsz neki egy útvonalat, egy URL-t vagy akár egy stream-et, ha a HTML memóriában él.

```java
// Step 1 – Define where the HTML comes from
String htmlPath = "YOUR_DIRECTORY/input.html"; // replace with your actual file
```

> **Miért fontos:** Egy egyszerű karakterlánc használata egyszerűvé teszi a példát, de a valós helyzetekben a HTML-t egy webszolgáltatásból vagy adatbázisból is beolvashatod. Az API elfogadja a `java.net.URL` vagy a `java.io.InputStream` típusokat is, ami hasznos, ha nem akarsz ideiglenes fájlt írni.

## 2. lépés: PDF oldalméret beállítása

A legtöbb PDF alapértelmezés szerint **Letter** méretű, ami furcsán nézhet ki, ha a közönséged **A4**-et vár. Az oldalméret módosítása egyetlen sorban megoldható a `PdfSaveOptions` segítségével.

```java
// Step 2 – Create PDF options and set the page size to A4
PdfSaveOptions pdfOptions = new PdfSaveOptions();
pdfOptions.setPageSize(PdfPageSize.A4); // this is the “set pdf page size” step
```

> **Pro tipp:** Ha egyedi méretre van szükséged (például egy nyugta formátum), az Aspose lehetővé teszi, hogy egy `SizeF` objektumot adj meg pontos szélességgel és magassággal pontokban.

## 3. lépés: PDF margók hozzáadása

A margók megakadályozzák, hogy a tartalom a lap szélénél legyen. Pontokban mérik őket (1 mm ≈ 2.8346 pt), de az Aspose egy kényelmes `Margin` osztályt biztosít, amely közvetlenül milliméterben fogadja a méreteket.

```java
// Step 3 – Define 20 mm margins on all sides (how to set margins)
pdfOptions.setMargins(new Margin(20, 20, 20, 20));
```

> **Miért fontos:** Margók nélkül a fejlécek nyomtatáskor levághatók, és a láblécek a nyomtató nem nyomtatható területébe tűnhetnek. Az egységes margók professzionális megjelenést kölcsönöznek a PDF-nek.

## 4. lépés: PDF‑A‑1b megfelelés engedélyezése (opcionális, de ajánlott)

Ha jogi vagy szabályozási okokból archiválsz dokumentumokat, a PDF‑A‑1b biztosítja, hogy a fájl önálló és jövőálló legyen.

```java
// Step 4 – Make the PDF archival‑ready
pdfOptions.setPdfACompliance(PdfACompliance.PdfA1b);
```

> **Gyors megjegyzés:** A PDF‑A megfelelés kissé megnövelheti a fájlméretet, mivel a betűkészletek beágyazódnak. Ez egy kis árat jelent a hosszú távú olvashatóságért.

## 5. lépés: A konverzió végrehajtása

Miután minden be van állítva, a tényleges konverzió egyetlen statikus hívás. Az Aspose kezeli a renderelő motorját, a CSS-t, a JavaScriptet (ha engedélyezve van) és a képek beágyazását a háttérben.

```java
// Step 5 – Convert the HTML to PDF using the configured options
Converter.convertHtmlToPdf(htmlPath, "YOUR_DIRECTORY/output.pdf", pdfOptions);
```

Ez az egész program! Ha összerakod az összes kódrészletet, egy futtatható osztályod lesz.

## Teljes működő példa

Az alábbiakban a teljes Java programot láthatod, amelyet beilleszthetsz a `ConvertHtmlToPdfCustom.java` fájlba. Cseréld ki a helyőrző útvonalakat a géped valós helyeire.

```java
import com.aspose.html.*;
import com.aspose.html.converters.*;
import com.aspose.html.saving.*;

public class ConvertHtmlToPdfCustom {
    public static void main(String[] args) throws Exception {

        // Step 1: Specify the source HTML file (local file, URL, or stream)
        String htmlPath = "YOUR_DIRECTORY/input.html";

        // Step 2: Configure PDF output options
        //   • A4 page size
        //   • 20 mm margins on all sides
        //   • PDF‑A‑1b compliance for archival
        PdfSaveOptions pdfOptions = new PdfSaveOptions();
        pdfOptions.setPageSize(PdfPageSize.A4);
        pdfOptions.setMargins(new Margin(20, 20, 20, 20));
        pdfOptions.setPdfACompliance(PdfACompliance.PdfA1b);

        // Step 3: Convert the HTML to PDF using the configured options
        Converter.convertHtmlToPdf(htmlPath, "YOUR_DIRECTORY/output.pdf", pdfOptions);
    }
}
```

### Várható eredmény

Running the program creates `output.pdf` that:

- **A4** méretű (210 mm × 297 mm).  
- **20 mm** margóval rendelkezik balra, jobbra, felül és alul.  
- **PDF‑A‑1b** megfelelőséggel bír, ami azt jelenti, hogy minden betűkészlet be van ágyazva és a fájl önálló.  
- Hűen reprodukálja a `input.html` elrendezését (képek, táblázatok és CSS stílusok megmaradnak).

Megnyithatod a PDF-et bármely nézőben (Adobe Acrobat, Foxit vagy akár Chrome), és egy tiszta oldalt kell látnod, amely kényelmes fehér szegéllyel körülveszi a tartalmat.

![convert html to pdf output preview](/images/convert-html-to-pdf.png)

*Ábra: Gyors pillantás a konvertálás után létrehozott PDF-re.*

## Gyakori kérdések és szélhelyzetek

### Mi van, ha a HTML külső CSS-t vagy képeket tartalmaz?

Az Aspose.HTML ugyanazokat a szabályokat követi, mint a böngészők. Amíg az URL-ek elérhetők (abszolút vagy a HTML fájl mappájához relatív), a konvertáló le fogja tölteni őket. Ha a kódot egy internetkapcsolat nélküli szerveren futtatod, fontold meg az erőforrások **data‑URI** karakterláncokként való beágyazását vagy előzetes betöltését egy `MemoryStream`‑be.

### Hogyan konvertáljak egy **URL**-t fájl helyett?

Csak cseréld le a `htmlPath` karakterláncot egy URL-re:

```java
String htmlPath = "https://example.com/report.html";
```

### Át tudom-e váltani a margó egységeit hüvelykre vagy pontokra?

Igen. A `Margin` konstruktor elfogadja a `float left, float top, float right, float bottom` paramétereket **pontokban**. Ha hüvelyket szeretnél, szorozd meg 72-vel (1 inch = 72 pt). Például 0,5 inch margó `new Margin(36, 36, 36, 36)` lenne.

### Mi van, ha **másik oldalorientációra** van szükség (fekvő)?

Állítsd be a `PageOrientation` tulajdonságot a `setPageSize` hívása előtt:

```java
pdfOptions.setPageOrientation(PageOrientation.Landscape);
pdfOptions.setPageSize(PdfPageSize.A4);
```

### Van mód **automatikusan fejlécet/láblécet** hozzáadni?

Az Aspose.HTML lehetővé teszi, hogy HTML töredékeket injektálj, amelyek fejlécként vagy láblécként működnek a `PdfPageTemplate` osztályon keresztül. Létrehozol egy kis HTML fragmentumot a kívánt szöveggel, majd hozzárendeled a `pdfOptions.getPageTemplate().setHeaderHtml(...)` (vagy `.setFooterHtml(...)`) metódushoz. Ez egy önálló téma, de a lényeg, hogy a fejléceket/lábléceket normál HTML‑ként kezelheted.

## Tippek a termelésre kész kódhoz

- **Licenceld a könyvtárat** – the free

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}