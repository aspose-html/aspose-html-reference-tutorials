---
date: 2026-03-18
description: Tanulja meg, hogyan konvertálhat HTML-t XPS-re, és állíthatja be az XPS
  oldalméretet az Aspose.HTML for Java segítségével. Könnyedén szabályozhatja a kimeneti
  méreteket.
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: HTML konvertálása XPS-re és XPS oldalméretének beállítása az Aspose.HTML for
  Java segítségével
url: /hu/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML konvertálása XPS-re és XPS oldalméret beállítása az Aspose.HTML for Java segítségével

Ebben az útmutatóban megtudja, **hogyan konvertálja a HTML-t XPS-re** és finomhangolja a kapott oldal méretét az Aspose.HTML for Java használatával. Legyen szó nyomtatható jelentésekről, számlákról vagy archiválási dokumentumokról, az XPS méretek szabályozása biztosítja, hogy a kimenet pontosan úgy nézzen ki, ahogy elvárja. Lépésről‑lépésre végigvezetjük a folyamaton – a környezet beállításától a végleges XPS fájl rendereléséig – hogy ezt a képességet azonnal beépíthesse Java alkalmazásaiba.

## Gyors válaszok
- **Mit jelent a „HTML konvertálása XPS-re”?** HTML dokumentumot renderel XPS fájlba, megőrizve a elrendezést és a stílusokat.  
- **Szükségem van licencre?** Fejlesztéshez egy ingyenes próba verzió működik; a termeléshez kereskedelmi licenc szükséges.  
- **Melyik Java verzió támogatott?** Java 8 vagy újabb (JDK 11+ ajánlott).  
- **Módosíthatom az oldal méretét?** Igen – az Aspose.HTML lehetővé teszi egyedi méretek megadását a renderelés előtt.  
- **Mennyi időt vesz igénybe a konverzió?** Általában egy másodpercnél kevesebb a szabványos oldalak esetén; nagyobb dokumentumok hosszabb időt vehetnek igénybe.

## Mi a HTML XPS-re konvertálása?
A HTML XPS-re konvertálása azt jelenti, hogy egy web‑orientált jelölőfájlt XPS (XML Paper Specification) dokumentummá alakítunk – egy rögzített elrendezésű, nyomtatásra kész formátummá, amely hasonló a PDF‑hez. Ez akkor hasznos, ha magas hűségű, eszközfüggetlen dokumentumokra van szükség archiváláshoz vagy nyomtatáshoz Java alkalmazásokból.

## Miért kell beállítani az XPS oldal méretét?
Az oldal méretének beállítása lehetővé teszi a végső dokumentum fizikai méretének (pl. A4, Letter, egyedi címkék) szabályozását. Megakadályozza a nem kívánt átméretezést, biztosítja, hogy a tartalom tökéletesen illeszkedjen, és csökkentheti a fájlméretet a felesleges üres tér eltávolításával.

## Előfeltételek

Mielőtt elkezdenénk, győződjön meg róla, hogy az alábbiak rendelkezésre állnak:

1. **Java fejlesztői környezet** – Java Development Kit (JDK) telepítve a rendszerén.  
2. **Aspose.HTML for Java könyvtár** – Töltse le és vegye fel a projektjébe az Aspose.HTML for Java könyvtárat. A könyvtárat megtalálja [itt](https://releases.aspose.com/html/java/).  
3. **Bemeneti HTML fájl** – Készítsen egy HTML fájlt, amelyet renderelni és az XPS oldal méretét beállítani szeretne. A saját HTML fájlját is használhatja ebben az útmutatóban.

## Csomagok importálása

Először importálja a szükséges osztályokat. Ezek a csomagok hozzáférést biztosítanak a dokumentumkezeléshez, rendereléshez és oldal‑beállítási funkciókhoz.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Lépésről‑lépésre útmutató

Az alábbiakban egy tömör, számozott útmutatót talál, amely tükrözi az eredeti lépéseket, miközben további kontextust ad a tisztánlátáshoz.

### 1. lépés: Állítsa be a bemeneti fájl nevét

Olvassa be a forrás‑HTML fájlt egy `FileInputStream`‑nel. Ez a stream táplálja a nyers HTML‑t az Aspose.HTML motorba.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

### 2. lépés: HTML dokumentum létrehozása és stílusok beállítása

Hozzon létre egy `HTMLDocument` példányt, amely a renderelni kívánt tartalmat képviseli. Ebben a példában egy kis CSS blokkot is beszúrunk a stílus demonstrálásához – nyugodtan cserélje le a saját jelölőjére.

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n" +
               "\n";

// ...
```

### 3. lépés: XPS renderelési beállítások létrehozása

Hozzon létre egy `XpsRenderingOptions` példányt, amely minden olyan beállítást tartalmaz, amely a HTML‑ről XPS‑re történő konverziót befolyásolja.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

### 4. lépés: Az oldal méretének beállítása  

**Hogyan állítsuk be az XPS oldal méretét** – Definiáljon egy egyedi oldalméretet (szélesség × magasság pontban), és adja meg a renderelőnek, hogy automatikusan kibővítse-e a legszélesebb oldalra. Az `adjustToWidestPage` `false` értékre állítása megőrzi a megadott pontos méreteket.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

### 5. lépés: Kimenet renderelése

Végül hozza létre az `XpsDevice`‑et a konfigurált beállításokkal, és renderelje a HTML dokumentumot. Az eredmény egy teljesen kialakított XPS fájl lesz a megadott egyedi oldalméretekkel.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Gyakori problémák és megoldások

| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| **Üres XPS kimenet** | A bemeneti stream nincs lezárva, vagy az HTMLDocument rossz fájlra mutat. | Győződjön meg arról, hogy a `FileInputStream` megfelelően van try‑with‑resources blokkba ágyazva, és a fájl útvonal helyes. |
| **Az oldal mérete nem alkalmazódik** | `adjustToWidestPage` értéke `true` maradt. | Állítsa be a `pageSetup.setAdjustToWidestPage(false);` értéket, ahogy a 4. lépésben látható. |
| **Nem támogatott CSS** | Az Aspose.HTML csak a CSS egy részhalmazát támogatja. | Használjon egyszerű elrendezést, betűtípusokat és színeket; kerülje a fejlett szelektorokat vagy a CSS Grid-et. |
| **LicenseException** | Érvényes licenc nélkül futtatás termelésben. | Alkalmazza a ideiglenes vagy megvásárolt licencet a renderelés előtt (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Gyakran ismételt kérdések

**Q:** Mi az Aspose.HTML for Java?  
**A:** Az Aspose.HTML for Java egy Java könyvtár, amely lehetővé teszi a fejlesztők számára HTML dokumentumok manipulálását és különböző formátumokba, például XPS, PDF és képek, konvertálását.

**Q:** Hol tölthetem le az Aspose.HTML for Java-t?  
**A:** Az Aspose.HTML for Java könyvtárat letöltheti [erről a linkről](https://releases.aspose.com/html/java/).

**Q:** Elérhető ingyenes próba verzió az Aspose.HTML for Java-hoz?  
**A:** Igen, ingyenes próba verziót kaphat az Aspose.HTML for Java-hoz [innen](https://releases.aspose.com/).

**Q:** Hogyan szerezhetek ideiglenes licencet az Aspose.HTML for Java-hoz?  
**A:** Az Aspose.HTML for Java ideiglenes licencének megszerzéséhez látogassa meg [ezt az oldalt](https://purchase.aspose.com/temporary-license/).

**Q:** Kaphatok támogatást az Aspose.HTML for Java-hoz?  
**A:** Igen, segítséget és támogatást kérhet az Aspose közösségtől a [Aspose Fórumon](https://forum.aspose.com/).

**Q:** Konvertálhatok HTML-t XPS-re egy fej nélküli szerveren?  
**A:** Természetesen. Az Aspose.HTML olyan környezetekben is működik, ahol nincs grafikus felület; csak győződjön meg róla, hogy a Java futtatókörnyezet megfelelően van beállítva.

**Q:** Támogatja a könyvtár az egyedi oldal margókat?  
**A:** Igen. Használja a `PageSetup.setMarginTop()`, `setMarginBottom()` stb. metódusokat, mielőtt a `PageSetup`‑ot a renderelési beállításokhoz rendeli.

## Összegzés

Áttekintettük a **HTML XPS-re konvertálásának** és az oldal méretének beállításának teljes folyamatát az Aspose.HTML for Java segítségével. A lépések követésével nyomtatható XPS dokumentumokat hozhat létre, amelyek pontosan megfelelnek a kívánt elrendezési követelményeknek. Nyugodtan kísérletezzen különböző oldalméretekkel, stílusokkal, vagy adjon hozzá fejléceket és lábléceket a projekt igényei szerint.

Ha kérdése van vagy további segítségre van szüksége, tekintse meg az [Aspose.HTML for Java dokumentációt](https://reference.aspose.com/html/java/) vagy csatlakozzon a beszélgetéshez a [Aspose Fórumon](https://forum.aspose.com/).

---

**Utoljára frissítve:** 2026-03-18  
**Tesztelve a következővel:** Aspose.HTML for Java 24.11 (a cikk írásakor legújabb)  
**Szerző:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}