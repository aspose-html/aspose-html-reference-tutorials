---
date: 2025-12-05
description: Ismerje meg, hogyan állíthatja be a HTML oldal margóit Java-ban az Aspose.HTML
  használatával, és adjon hozzá oldalszámokat és címeket a dokumentumaihoz.
language: hu
linktitle: CSS Extensions - Adding Title and Page Number
second_title: Java HTML Processing with Aspose.HTML
title: HTML oldal margóinak beállítása Java-val az Aspose.HTML segítségével
url: /java/advanced-usage/css-extensions-adding-title-page-number/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML oldal margók beállítása Java-ban az Aspose.HTML segítségével

Ebben az útmutatóban megtudja, **hogyan állítsa be az HTML oldal margókat Java**‑stílusban az Aspose.HTML for Java használatával. Lépésről‑lépésre végigvezetjük a saját oldal margók létrehozásán, oldalszámok beszúrásán és egy dokumentumcím hozzáadásán – mindezt világos, másolható kóddal, amelyet saját projektjébe illeszthet.

## Gyors válaszok
- **Melyik könyvtár szükséges?** Aspose.HTML for Java  
- **Programozottan vezérelhetem a margókat?** Igen, egy CSS `@page` szabályon keresztül a felhasználói stíluslapon  
- **Mely kimeneti formátumok támogatják a margókat?** XPS, PDF és egyéb raszteres formátumok  
- **Szükség van licencre a termeléshez?** Érvényes Aspose.HTML licenc szükséges a nem próbaverzióhoz  
- **Kompatibilis a Java 11+ verziókkal?** Teljesen – a könyvtár működik a modern Java verziókkal  

## Mi az a „HTML oldal margók beállítása Java-ban”?
Az HTML oldal margók Java-ban történő beállítása azt jelenti, hogy a renderelő motor (az Aspose.HTML által biztosított) CSS oldal‑doboz tulajdonságokat alkalmaz a dokumentum nyomtatható formátumba (például XPS vagy PDF) történő konvertálása előtt. Egy egyedi `@page` szabály definiálásával szabályozhatja a nyomtatható területet, az oldalszámokat és a fejléc/lábléc tartalmát.

## Miért használjuk az Aspose.HTML-t a margóvezérléshez?
- **Pontos elrendezés** – a CSS `@page` pixel‑pontos kontrollt biztosít a margók, fejlécek és láblécek felett.  
- **Formátumok közötti konzisztencia** – ugyanazok a margódefiníciók működnek XPS, PDF és kép kimeneteknél.  
- **Nincs böngészőfüggőség** – a renderelés szerveroldalon történik, így nem szükséges headless böngésző.  

## Előfeltételek

Mielőtt elkezdenénk, győződjön meg róla, hogy az alábbiak rendelkezésre állnak:

1. **Java fejlesztői környezet** – JDK 11 vagy újabb telepítve.  
2. **Aspose.HTML for Java** – Töltse le és telepítse a könyvtárat [ide](https://releases.aspose.com/html/java/).  

## Csomagok importálása

A kezdéshez importálja a szükséges Aspose.HTML osztályokat:

```java
// Import Aspose.HTML packages
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

## HTML oldal margók beállítása Java-ban – Lépésről‑lépésre útmutató

### 1. lépés: Konfiguráció inicializálása és egyedi oldal margók meghatározása

```java
// Initialize configuration object and set up the page-margins for the document
Configuration configuration = new Configuration();
try {
    // Get the User Agent service
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Set the style of custom margins and create marks on it
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

Ebben a blokkban létrehozzuk a `Configuration` objektumot, lekérjük az `IUserAgentService`‑t, és egy CSS `@page` szabályt injektálunk, amely meghatározza a margókat, egy jobb‑alsó oldalszámlálót és egy felső‑középső dokumentumcímet.

### 2. lépés: HTML dokumentum létrehozása

```java
// Initialize an HTML document
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Itt egy egyszerű “Hello World” szakaszú `HTMLDocument`‑et példányosítunk. Az 1. lépésben létrehozott konfigurációt alkalmazzuk, így a saját margók a dokumentum renderelésekor érvényesülnek.

### 3. lépés: Renderelés XPS fájlba (vagy bármely támogatott kimenetre)

```java
// Initialize an output device
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    // Send the document to the output device
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

Ez a lépés egy `XpsDevice`‑et hoz létre, amely a renderelt oldalakat az `output.xps` fájlba írja. A korábban definiált margók, oldalszámok és cím megjelennek a végleges fájlban.

## Gyakori problémák és tippek

- **A margók változatlanul maradnak** – Győződjön meg róla, hogy a `@page` szabályt nem írják felül más stíluslapok. A `setUserStyleSheet` hívás a legmagasabb prioritást biztosítja.  
- **Az oldalszámok „NaN” értéket mutatnak** – Ellenőrizze, hogy az Aspose.HTML 23.10 vagy újabb verzióját használja; a régebbi verziók nem tartalmazzák a `currentPageNumber()` függvényt.  
- **A kimeneti fájl üres** – Ellenőrizze, hogy a `Resources.output` útvonal helyesen feloldódik és van írási jogosultsága.  

## Gyakran ismételt kérdések

### Q1: Mi az Aspose.HTML for Java?

**A:** Az Aspose.HTML for Java egy Java könyvtár, amely erőteljes eszközöket biztosít HTML dokumentumokkal való munkához Java alkalmazásokban, beleértve a konvertálást, renderelést és manipulációt.

### Q2: Testreszabhatom-e tovább az oldal margókat?

**A:** Igen, egyszerűen szerkessze a `setUserStyleSheet`‑ben lévő CSS‑t. Módosíthatja bármely `margin-*` értéket, vagy további `@top-*` / `@bottom-*` dobozokat adhat hozzá.

### Q3: Hogyan adhatok több tartalmat a HTML dokumentumhoz?

**A:** Cserélje le a `new HTMLDocument("<div>Hello World!!!</div>", …)`‑ben lévő karakterláncot a saját HTML‑kódjára, vagy töltsön be egy külső fájlt a `HTMLDocument(String url, …)` konstruktor segítségével.

### Q4: Az Aspose.HTML for Java kompatibilis-e más dokumentumformátumokkal?

**A:** Teljesen. Az ugyanaz a `HTMLDocument` renderelhető PDF‑be, XPS‑be, képekbe vagy akár EPUB‑ba is, ha a kimeneti eszközt (pl. `PdfDevice`, `PngDevice`) cseréli.

### Q5: Szükség van licencre az Aspose.HTML for Java használatához?

**A:** Igen, licenc szükséges a termeléshez. Próbaverziót vagy licencet szerezhet [ide](https://purchase.aspose.com/buy) vagy [ide](https://releases.aspose.com/).

### Q6: Hogyan állíthatok be különböző margókat páratlan és páros oldalakra?

**A:** Használja a `@page :left` és `@page :right` pszeudo‑osztályokat a stíluslapon, hogy külön margókat definiáljon a bal‑ (páros) és jobb‑ (páratlan) oldalakra.

### Q7: Beágyazhatok‑e egyedi betűtípusokat a renderelt dokumentumba?

**A:** Igen. Adjon `@font-face` szabályokat a felhasználói stíluslaphoz, és hivatkozzon a betűtípusokra a HTML tartalmában.

## Összegzés

Most már elsajátította, **hogyan állítsa be az HTML oldal margókat Java-ban** az Aspose.HTML segítségével, és tudja, hogyan adjon hozzá oldalszámokat és címet, hogy dokumentumai professzionális megjelenést kapjanak. Nyugodtan kísérletezzen további `@page` dobozokkal, egyedi betűtípusokkal vagy különböző kimeneti formátumokkal, hogy a projekt igényeinek megfeleljen.

Ha bármilyen problémába ütközik, a hivatalos [Aspose.HTML for Java dokumentáció](https://reference.aspose.com/html/java/) és az [Aspose támogatási fórum](https://forum.aspose.com/) kiváló helyek a segítséghez.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Legutóbb frissítve:** 2025-12-05  
**Tesztelve a következővel:** Aspose.HTML for Java 23.12  
**Szerző:** Aspose  

---