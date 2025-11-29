---
date: 2025-11-29
description: Ismerje meg, hogyan konvertálhat HTML-t XPS-re, és állíthatja be az XPS
  oldal méretét az Aspose.HTML for Java segítségével. Könnyedén szabályozhatja a kimeneti
  méreteket.
language: hu
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: HTML konvertálása XPS-re és az XPS oldalméretének beállítása az Aspose.HTML
  for Java segítségével
url: /java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML konvertálása XPS-re és az XPS oldalméret beállítása az Aspose.HTML for Java segítségével

Ebben az útmutatóban megtanulja, **hogyan konvertálja a HTML-t XPS-re**, és finomhangolja a kapott oldalméretet az Aspose.HTML for Java használatával. Legyen szó nyomtatható jelentésekről, számlákról vagy archiválási dokumentumokról, az XPS méretek szabályozása biztosítja, hogy a kimenet pontosan úgy nézzen ki, ahogy elvárja. Lépésről lépésre végigvezetjük a folyamaton – a környezet beállításától a végleges XPS fájl rendereléséig – hogy ezt a képességet azonnal beépíthesse Java alkalmazásaiba.

## Gyors válaszok
- **Mit jelent a “HTML konvertálása XPS-re”?** Egy HTML dokumentumot XPS fájlba renderel, megőrizve a elrendezést és a stílusokat.  
- **Szükség van licencre?** Fejlesztéshez egy ingyenes próbaverzió elegendő; termeléshez kereskedelmi licenc szükséges.  
- **Melyik Java verzió támogatott?** Java 8 vagy újabb (JDK 11+ ajánlott).  
- **Módosítható az oldalméret?** Igen – az Aspose.HTML lehetővé teszi egyedi méretek megadását a renderelés előtt.  
- **Mennyi időt vesz igénybe a konvertálás?** Általában egy másodperc alatt standard oldalak esetén; nagyobb dokumentumok hosszabb időt vehetnek igénybe.

## Mi az a HTML konvertálása XPS-re?
A HTML XPS-re konvertálása azt jelenti, hogy egy web‑orientált jelölőfájlt egy XPS (XML Paper Specification) dokumentummá alakítunk, amely egy rögzített elrendezésű, nyomtatásra kész formátum, hasonló a PDF-hez. Ez akkor hasznos, ha magas hűségű, eszközfüggetlen dokumentumokra van szükség archiváláshoz vagy nyomtatáshoz Java alkalmazásokból.

## Miért érdemes az XPS oldalméretet módosítani?
Az oldalméret módosítása lehetővé teszi a végső dokumentum fizikai méreteinek (pl. A4, Letter, egyedi címkék) szabályozását. Megakadályozza a nem kívánt átméretezést, biztosítja, hogy a tartalom tökéletesen illeszkedjen, és csökkentheti a fájlméretet a fölösleges fehér tér eltávolításával.

## Előfeltételek

Mielőtt elkezdenénk, győződjön meg róla, hogy az alábbi előfeltételek teljesülnek:

1. **Java fejlesztői környezet** – Telepített Java Development Kit (JDK) a rendszerén.  
2. **Aspose.HTML for Java könyvtár** – Töltse le és adja hozzá az Aspose.HTML for Java könyvtárat a projektjéhez. A könyvtárat megtalálja [itt](https://releases.aspose.com/html/java/).  
3. **Bemeneti HTML fájl** – Készítsen elő egy HTML fájlt, amelyet renderelni és az XPS oldalméretét módosítani szeretné. Használhatja saját HTML fájlját ebben az útmutatóban.

## Csomagok importálása

Először importálja a szükséges osztályokat. Ezek a csomagok biztosítják a dokumentumkezelés, renderelés és oldalbeállítási funkciók elérését.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## 1. lépés: A bemeneti fájl nevének beállítása

Olvassa be a forrás HTML fájlt egy `FileInputStream` segítségével. Ez a stream a nyers HTML‑t táplálja az Aspose.HTML motorba.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

## 2. lépés: HTML dokumentum létrehozása és stílusok beállítása

Hozzon létre egy `HTMLDocument` példányt, amely a renderelni kívánt tartalmat képviseli. Ebben a példában egy kis CSS blokkot is befecskendezünk a stílus demonstrálásához – nyugodtan cserélje le a saját markupjára.

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

## 3. lépés: XPS renderelési beállítások létrehozása

Példányosítson egy `XpsRenderingOptions` objektumot, amely tartalmazza az összes beállítást, amely a HTML‑ról XPS‑re konvertálást befolyásolja.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

## 4. lépés: Az oldalméret módosítása

Határozzon meg egy egyedi oldalméretet (szélesség × magasság pontban), és adja meg a renderelőnek, hogy automatikusan kiterjesztse‑e a legszélesebb oldalra. Az `adjustToWidestPage` `false` értékre állítása megőrzi a pontosan megadott méreteket.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

## 5. lépés: A kimenet renderelése

Végül hozza létre az `XpsDevice`‑et a konfigurált beállításokkal, és renderelje a HTML dokumentumot. Az eredmény egy teljesen elkészített XPS fájl lesz a megadott egyedi oldalmérettel.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Gyakori problémák és megoldások

| Probléma | Ok | Megoldás |
|----------|----|----------|
| **Üres XPS kimenet** | A bemeneti stream nincs lezárva vagy a HTMLDocument rossz fájlra mutat. | Győződjön meg róla, hogy a `FileInputStream` megfelelően van `try‑with‑resources` blokkba ágyazva, és az elérési út helyes. |
| **Az oldalméret nem alkalmazódik** | `adjustToWidestPage` `true` értéken maradt. | Állítsa be a `pageSetup.setAdjustToWidestPage(false);` értéket, ahogy a 4. lépésben látható. |
| **Nem támogatott CSS** | Az Aspose.HTML csak egy CSS‑részhalmazt támogat. | Maradjon az alapvető elrendezéseknél, betűtípusoknál és színeknél; kerülje az összetett szelektorokat vagy a CSS Grid használatát. |
| **LicenseException** | Érvényes licenc hiánya termelési környezetben. | Alkalmazza a temporális vagy megvásárolt licencet a renderelés előtt (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Gyakran feltett kérdések

**Q: Mi az Aspose.HTML for Java?**  
A: Az Aspose.HTML for Java egy Java könyvtár, amely lehetővé teszi a fejlesztők számára, hogy HTML dokumentumokat különböző formátumokra, például XPS‑re, PDF‑re és képekre konvertáljanak és manipuláljanak.

**Q: Hol tölthetem le az Aspose.HTML for Java‑t?**  
A: Az Aspose.HTML for Java könyvtárat letöltheti [erről a linkről](https://releases.aspose.com/html/java/).

**Q: Van ingyenes próbaverzió az Aspose.HTML for Java‑hoz?**  
A: Igen, ingyenes próbaverziót kaphat az Aspose.HTML for Java‑ból [innen](https://releases.aspose.com/).

**Q: Hogyan szerezhetek ideiglenes licencet az Aspose.HTML for Java‑hoz?**  
A: Ideiglenes licencért látogasson el [erre az oldalra](https://purchase.aspose.com/temporary-license/).

**Q: Kaphatok támogatást az Aspose.HTML for Java‑hoz?**  
A: Igen, segítséget és támogatást kérhet az Aspose közösségtől a [Aspose Fórumon](https://forum.aspose.com/).

**Q: Konvertálhatok HTML‑t XPS‑re egy fej nélküli szerveren?**  
A: Teljes mértékben. Az Aspose.HTML működik GUI‑ nélküli környezetben is; csak győződjön meg róla, hogy a Java futtatókörnyezet megfelelően van beállítva.

**Q: Támogatja a könyvtár az egyedi oldal margókat?**  
A: Igen. Használja a `PageSetup.setMarginTop()`, `setMarginBottom()` stb. metódusokat, mielőtt a `PageSetup`‑ot hozzárendeli a renderelési beállításokhoz.

## Összegzés

Áttekintettük a **HTML XPS‑re konvertálásának** és az oldalméret beállításának teljes folyamatát az Aspose.HTML for Java segítségével. A lépések követésével nyomtatásra kész XPS dokumentumokat hozhat létre, amelyek pontosan megfelelnek az Ön elrendezési igényeinek. Nyugodtan kísérletezzen különböző oldalméretekkel, stílusokkal, vagy adjon hozzá fejléceket és lábléceket a projektje igényei szerint.

Ha kérdése van, vagy további segítségre van szüksége, tekintse meg az [Aspose.HTML for Java dokumentációt](https://reference.aspose.com/html/java/) vagy csatlakozzon a beszélgetéshez a [Aspose Fórumon](https://forum.aspose.com/).

---

**Utoljára frissítve:** 2025-11-29  
**Tesztelt verzió:** Aspose.HTML for Java 24.11 (a cikk írásakor elérhető legújabb)  
**Szerző:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}