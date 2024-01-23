---
title: Testreszabhatja a HTML oldalmargóit az Aspose.HTML segítségével
linktitle: CSS-kiterjesztések – Cím és oldalszám hozzáadása
second_title: Java HTML feldolgozás Aspose.HTML-lel
description: Ismerje meg, hogyan szabhatja testre az oldalmargókat, hogyan adhat hozzá oldalszámokat és címeket HTML-dokumentumokhoz az Aspose.HTML for Java használatával.
type: docs
weight: 10
url: /hu/java/advanced-usage/css-extensions-adding-title-page-number/
---
Az Aspose.HTML for Java egy hatékony könyvtár a HTML dokumentumok Java alkalmazásokban történő feldolgozásához. Ebben az oktatóanyagban megvizsgáljuk, hogyan hozhat létre egyéni oldalmargókat, és hogyan adhat hozzá oldalszámokat és címeket a HTML-dokumentumokhoz az Aspose.HTML for Java használatával. Ez a lépésenkénti útmutató a folyamatot kezelhető lépésekre bontja, hogy megkönnyítse ezeknek a szolgáltatásoknak a HTML-dokumentumaiba való integrálását.

## Előfeltételek

Mielőtt elkezdené, győződjön meg arról, hogy a következő előfeltételek teljesülnek:

1. Java fejlesztői környezet: Győződjön meg arról, hogy a számítógépén be van állítva Java fejlesztői környezet.

2.  Aspose.HTML for Java: Töltse le és telepítse az Aspose.HTML for Java könyvtárat innen[itt](https://releases.aspose.com/html/java/).

## Csomagok importálása

kezdéshez importálnia kell a szükséges csomagokat az Aspose.HTML for Java-ból. Adja hozzá a következő importálási utasításokat a Java-kódhoz:

```java
// Az Aspose.HTML csomagok importálása
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

Most bontsuk fel az egyéni oldalmargók, oldalszámok és címek hozzáadásának folyamatát kezelhető lépésekre:

## 1. lépés: Inicializálja a konfigurációt és az oldalmargókat

```java
// Inicializálja a konfigurációs objektumot, és állítsa be a dokumentum oldalmargóit
Configuration configuration = new Configuration();
try {
    // Szerezze be a User Agent szolgáltatást
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Állítsa be az egyéni margók stílusát, és jelöljön meg rajta
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

Ebben a lépésben inicializáljuk a konfigurációs objektumot, és egyéni oldalmargókat állítunk be, beleértve az oldalszámláló pozícióját és az oldal címét.

## 2. lépés: Inicializáljon egy HTML-dokumentumot

```java
// HTML dokumentum inicializálása
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Itt létrehozunk egy HTML-dokumentumot egy mintatartalommal (jelen esetben egy "Hello World" üzenettel), és alkalmazzuk az 1. lépés konfigurációját.

## 3. lépés: Inicializáljon egy kimeneti eszközt, és jelenítse meg a dokumentumot

```java
// Inicializáljon egy kimeneti eszközt
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    //Küldje el a dokumentumot a kimeneti eszközre
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

Ebben a lépésben beállítunk egy kimeneti eszközt és rendereljük a HTML dokumentumot. A dokumentum feldolgozása és mentése XPS-fájlként történik a megadott oldalmargókkal, oldalszámokkal és címmel.

## Következtetés

Gratulálunk! Sikeresen megtanulta, hogyan hozhat létre egyéni oldalmargókat, és hogyan adhat hozzá oldalszámokat és címeket HTML-dokumentumaihoz az Aspose.HTML for Java használatával. Ezzel a testreszabással professzionálisabb és látványosabb dokumentumokat hozhat létre.

 Ha bármilyen kérdése van, vagy bármilyen problémája van, keresse fel a[Aspose.HTML a Java dokumentációhoz](https://reference.aspose.com/html/java/) vagy kérjen segítséget a[Aspose támogatási fórum](https://forum.aspose.com/).

## GYIK

### 1. kérdés: Mi az Aspose.HTML for Java?

1. válasz: Az Aspose.HTML for Java egy Java-könyvtár, amely hatékony eszközöket biztosít a HTML-dokumentumok Java alkalmazásokban történő kezeléséhez.

### 2. kérdés: Tovább szabhatom az oldal margóit?

2. válasz: Igen, az 1. lépésben módosíthatja a CSS-stílusokat az oldalmargók igényei szerint testreszabásához.

### 3. kérdés: Hogyan adhatok több tartalmat a HTML-dokumentumhoz?

3. válasz: A 2. lépésben módosíthatja a HTML-tartalmat, ha lecseréli a mintatartalmat a sajátjára.

### 4. kérdés: Az Aspose.HTML for Java kompatibilis más dokumentumformátumokkal?

4. válasz: Igen, az Aspose.HTML for Java használható HTML-dokumentumok konvertálására különféle formátumokká, beleértve a PDF-t, XPS-t és képeket.

### 5. kérdés: Szükségem van licencre az Aspose.HTML for Java használatához?

 5. válasz: Igen, licencet vagy ingyenes próbaverziót szerezhet be[itt](https://purchase.aspose.com/buy) vagy[itt](https://releases.aspose.com/).