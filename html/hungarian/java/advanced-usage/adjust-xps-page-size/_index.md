---
title: Állítsa be az XPS oldalméretét az Aspose.HTML for Java segítségével
linktitle: XPS oldalméret beállítása
second_title: Java HTML feldolgozás Aspose.HTML-lel
description: Ismerje meg, hogyan állíthatja be az XPS oldalméretét az Aspose.HTML for Java segítségével. Egyszerűen szabályozhatja XPS-dokumentumai kimeneti méreteit.
weight: 16
url: /hu/java/advanced-usage/adjust-xps-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Állítsa be az XPS oldalméretét az Aspose.HTML for Java segítségével


Ebben az oktatóanyagban végigvezetjük az XPS-oldalméret beállításának folyamatán az Aspose.HTML for Java használatával. Ez a nagy teljesítményű könyvtár lehetővé teszi a HTML-dokumentumok kezelését és különféle formátumokba, köztük XPS-be való renderelését. Az oldalméret beállítása elengedhetetlen, ha szabályozni kell az XPS-dokumentum kimeneti méreteit.

## Előfeltételek

Mielőtt elkezdené, győződjön meg arról, hogy a következő előfeltételek teljesülnek:

1. Java fejlesztői környezet: Győződjön meg arról, hogy a Java Development Kit (JDK) telepítve van a rendszerén.

2.  Aspose.HTML for Java Library: Le kell töltenie és bele kell foglalnia az Aspose.HTML for Java könyvtárat a Java projektbe. Megtalálhatod a könyvtárat[itt](https://releases.aspose.com/html/java/).

3. HTML-fájl bevitele: Készítsen elő egy HTML-fájlt, amelyet elő szeretne készíteni, és állítsa be az XPS-oldal méretét. Ehhez az oktatóanyaghoz használhatja saját HTML-fájlját.

## Csomagok importálása

Először is importálnia kell a szükséges csomagokat az Aspose.HTML for Java használatához. Szerelje be ezeket a csomagokat a Java osztály elejére:

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## 1. lépés: Állítsa be a bemeneti fájl nevét

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

 Ebben a lépésben a HTML beviteli fájlt olvassuk be a`FileInputStream`.

## 2. lépés: Hozzon létre egy HTML-dokumentumot, és állítson be stílusokat

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
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n";

// ...
```

 Ez a lépés egy`HTMLDocument` és stílusokat ad hozzá.

## 3. lépés: Hozzon létre XPS renderelési beállításokat

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

Itt XPS-leképezési beállításokat hozunk létre a renderelési folyamat konfigurálásához.

## 4. lépés: Állítsa be az oldalméretet

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

Ebben a lépésben be kell állítani az oldalméretet, és meg kell adni, hogy a legszélesebb oldalra kell-e igazítani.

## 5. lépés: Renderje le a kimenetet

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

Az utolsó lépésben az XPS kimenetet jelenítjük meg a beállított opciók segítségével.

## Következtetés

Ebben az oktatóanyagban megmutattuk, hogyan állíthatja be az XPS oldalméretét az Aspose.HTML for Java használatával. Szabályozhatja XPS-dokumentumai kimeneti méreteit, biztosítva, hogy megfeleljenek az Ön egyedi követelményeinek. A mellékelt kóddal és lépésekkel könnyedén megvalósíthatja ezt a funkciót Java alkalmazásaiban.

 Ha bármilyen kérdése van, vagy további segítségre van szüksége, keresse fel a[Aspose.HTML a Java dokumentációhoz](https://reference.aspose.com/html/java/) vagy kérjen segítséget a[Aspose fórum](https://forum.aspose.com/).

## GYIK

### 1. kérdés: Mi az Aspose.HTML for Java?

1. válasz: Az Aspose.HTML for Java egy Java-könyvtár, amely lehetővé teszi a fejlesztők számára a HTML-dokumentumok manipulálását és konvertálását különféle formátumokba, például XPS-be, PDF-be és képekké.

### 2. kérdés: Honnan tölthetem le az Aspose.HTML for Java-t?

 2. válasz: Letöltheti az Aspose.HTML for Java könyvtárat innen[ezt a linket](https://releases.aspose.com/html/java/).

### 3. kérdés: Elérhető ingyenes próbaverzió az Aspose.HTML for Java számára?

 3. válasz: Igen, letöltheti az Aspose.HTML for Java ingyenes próbaverzióját a webhelyről[itt](https://releases.aspose.com/).

### 4. kérdés: Hogyan szerezhetek ideiglenes licencet az Aspose.HTML for Java számára?

 4. válasz: Ha ideiglenes licencet szeretne szerezni az Aspose.HTML for Java számára, látogasson el a webhelyre[ezt az oldalt](https://purchase.aspose.com/temporary-license/).

### 5. kérdés: Kaphatok támogatást az Aspose.HTML for Java számára?

 V5: Igen, segítséget és támogatást kérhet az Aspose közösségtől a webhelyen[Aspose fórum](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
