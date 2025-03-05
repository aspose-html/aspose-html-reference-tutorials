---
title: Alkalmazza a mért licencet a .NET-ben az Aspose.HTML segítségével
linktitle: Alkalmazza a mért licencet a .NET-ben
second_title: Aspose.HTML .NET HTML manipulációs API
description: Ismerje meg, hogyan alkalmazhat fizetős licencet az Aspose.HTML for .NET-ben. Hatékonyan kezelheti HTML-kezelési igényeit. Kezdje el most!
type: docs
weight: 10
url: /hu/net/licensing-and-initialization/apply-metered-license/
---
Ebben az oktatóanyagban végigvezetjük a mérőszámos licenc alkalmazásának folyamatán az Aspose.HTML használatával. A mérőszámos licenc kényelmes módja a HTML-kezelési igények licenckezelésének. Az alábbi lépések követésével mérős licencet alkalmazhat Aspose.HTML for .NET projektjéhez.

## Előfeltételek

Mielőtt folytatná, győződjön meg arról, hogy a következő előfeltételek teljesülnek:

-  Érvényes Aspose.HTML .NET licenchez. től szerezheti be[Aspose Vásárlás](https://purchase.aspose.com/buy).
-  Az Aspose.HTML for .NET könyvtár, amelyről letölthető[itt](https://releases.aspose.com/html/net/).
- Az adatkönyvtár elérési útja, ahol a bemeneti HTML-fájlt tárolta.

Most bontsuk fel a példakódot, és magyarázzuk el részletesen az egyes lépéseket:

## Névterek importálása

A .NET-projektben tartalmaznia kell a szükséges névtereket. Adja hozzá a következőket utasításokkal a C# fájl tetején:

```csharp
using Aspose.Html;
```

## Lépésről lépésre útmutató

Itt a példakódot több lépésre bontjuk, és minden lépést részletesen elmagyarázunk.

### Adatkönyvtár elérési út beállítása:

   Először is be kell állítania az adatkönyvtár elérési útját, ahol a bemeneti HTML-fájl található. Cserélnie kell`"Your Data Directory"` a tényleges úttal.

   ```csharp
   string dataDir = "Your Data Directory";
   ```

### Állítsa be a mért nyilvános és privát kulcsokat:

    A fizetős licenc alkalmazásához meg kell adnia nyilvános és privát kulcsait. Ezeket a kulcsokat akkor szerezheti be, ha megvásárolja az Aspose-tól mért licencet. Cserélje ki`"*****"` tényleges nyilvános és privát kulcsaival.

   ```csharp
   Aspose.Html.Metered metered = new Aspose.Html.Metered();
   metered.SetMeteredKey("YOUR_PUBLIC_KEY", "YOUR_PRIVATE_KEY");
   ```

### Töltse be a HTML dokumentumot:

    Töltse be a HTML dokumentumot az adatkönyvtárából a HTMLDocument osztály használatával. Ügyeljen arra, hogy cserélje ki`"input.html"` a tényleges fájlnévvel.

   ```csharp
   HTMLDocument document = new HTMLDocument(dataDir + "input.html");
   ```

### Nyomtassa ki a belső HTML-t:

   A HTML dokumentum betöltése után elérheti és kinyomtathatja a fájl belső HTML-kódját a konzolra ellenőrzés céljából.

   ```csharp
   Console.WriteLine(document.Body.InnerHTML);
   ```

Ennyi! Sikeresen alkalmazta a fizetős licencet .NET-projektjéhez, és betöltött egy HTML-dokumentumot.

## Következtetés

Ebben az oktatóanyagban bemutattuk, hogyan kell mérőszámú licencet alkalmazni az Aspose.HTML for .NET használatával. Az alábbi lépések követésével zökkenőmentesen integrálhatja az Aspose.HTML-t .NET-alkalmazásaiba a HTML-kezeléshez.

---

## Gyakran Ismételt Kérdések (GYIK)

### Mit jelent a fizetős licenc az Aspose.HTML-ben .NET-hez?
A mért licenc lehetővé teszi, hogy az Aspose.HTML-ért felosztó-kirovó alapon fizessen, a használattól függően. Ez egy rugalmas licencelési lehetőség.

### Hol szerezhetek fizetős licencet az Aspose.HTML for .NET-hez?
 Mérőszámlás engedélyt vásárolhat innen[Aspose Vásárlás](https://purchase.aspose.com/buy).

### Hogyan tölthetem le az Aspose.HTML for .NET könyvtárat?
 A könyvtárat innen töltheti le[itt](https://releases.aspose.com/html/net/).

### Vannak ingyenes próbaverziók az Aspose.HTML for .NET számára?
 Igen, elérheti az ingyenes próbaverziót innen[itt](https://releases.aspose.com/).

### Hol kaphatok támogatást, vagy hol tehetek fel kérdéseket az Aspose.HTML for .NET-hez kapcsolódóan?
 Csatlakozhat a közösséghez, és támogatást kérhet a[Aspose fórumok](https://forum.aspose.com/).