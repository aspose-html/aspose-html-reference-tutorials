---
title: Konvertálja az EPUB-t XPS-re .NET-ben az Aspose.HTML segítségével
linktitle: Az EPUB konvertálása XPS-re .NET-ben
second_title: Aspose.HTML .NET HTML manipulációs API
description: Ismerje meg, hogyan konvertálhat EPUB-t XPS-re .NET-ben az Aspose.HTML for .NET használatával. Kövesse lépésről lépésre útmutatónkat a könnyű konverzió érdekében.
type: docs
weight: 13
url: /hu/net/html-extensions-and-conversions/convert-epub-to-xps/
---

Zökkenőmentes módot keres az EPUB-fájlok XPS-formátumba konvertálására .NET-alkalmazásaiban? Az Aspose.HTML for .NET hatékony megoldást kínál ennek könnyed elérésére. Ebben a részletes útmutatóban végigvezetjük az Aspose.HTML használatával az EPUB XPS formátumba konvertálásának folyamatán. Kezdjük is!

## Előfeltételek

Mielőtt belevágna az EPUB–XPS átalakítási folyamatba, meg kell győződnie arról, hogy a következő előfeltételek teljesülnek:

### 1. Aspose.HTML for .NET Library

 Győződjön meg arról, hogy az Aspose.HTML for .NET könyvtár telepítve van a projektben. Ha még nem tette meg, beszerezheti a[Aspose.HTML for .NET letöltési oldal](https://releases.aspose.com/html/net/).

### 2. Írja be az EPUB fájlt

Szüksége lesz egy EPUB-fájlra, amelyet XPS-re szeretne konvertálni. Győződjön meg arról, hogy rendelkezik egy EPUB-fájllal a konvertáláshoz.

### 3. .NET fejlesztői környezet

Ez az útmutató feltételezi, hogy a gépen működő .NET fejlesztői környezet van beállítva.

## Névtér importálása

Kezdésként importálja az Aspose.HTML szükséges névterét:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## Az EPUB konvertálása XPS-re

Bontsuk le több lépésre az EPUB-fájl XPS-formátumba konvertálásának folyamatát.

### 1.1. lépés: Nyissa meg az EPUB-fájlt

Először nyissa meg a meglévő EPUB-fájlt a FileStream használatával való olvasáshoz:

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Folytassa az átalakítási folyamatot
}
```

### 1.2. lépés: Hozzon létre XpsSaveOptions

Hozzon létre egy XpsSaveOptions példányt. Ez a lépés kulcsfontosságú az XPS kimenet konfigurálásához:

```csharp
var options = new XpsSaveOptions();
```

### 1.3. lépés: Az EPUB konvertálása XPS-re

Most hívjuk meg a ConvertEPUB metódust az EPUB XPS-re konvertálásához:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Adja meg az Egyéni XPS-beállításokat

Tovább szabhatja az XPS-kimenetet egyéni beállítások, például oldalméret és háttérszín megadásával.

### 2.1. lépés: Egyedi oldalméret és háttérszín

Hozzon létre egy XpsSaveOptions példányt egyéni oldalmérettel és háttérszínnel:

```csharp
var options = new XpsSaveOptions()
{
    PageSetup =
    {
        AnyPage = new Page()
        {
            Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
        }
    },
    BackgroundColor = System.Drawing.Color.AliceBlue,
};
```

### 2.2. lépés: Az EPUB konvertálása XPS-re egyéni beállításokkal

Most hívja meg a ConvertEPUB metódust az EPUB XPS-re konvertálásához az egyéni beállításokkal:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Használja az Egyéni adatfolyam-szolgáltatót

Ebben a lépésben az EPUB-t XPS-re konvertáljuk egy egyéni adatfolyam-szolgáltató segítségével, amely lehetővé teszi a kapott adatok kezelését.

### 3.1. lépés: Hozzon létre egy MemoryStreamProvider-t

Hozzon létre egy MemoryStreamProvider példányt:

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    // Folytassa az átalakítási folyamatot
}
```

### 3.2. lépés: Az EPUB konvertálása XPS-re a Stream Provider segítségével

Az EPUB konvertálása XPS-re a MemoryStreamProvider segítségével:

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### 3.3. lépés: Eredmény elérése és mentése

Töltse le a konvertált adatokat tartalmazó memóriafolyamot, és mentse el egy kimeneti fájlba:

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### Class MemoryStreamProvider forráskód

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // A dokumentum megjelenítése során létrehozott MemoryStream objektumok listája
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // Ezt a módszert akkor hívják meg, ha az egyetlen kimeneti adatfolyamra van szükség, például XPS, PDF vagy TIFF formátumok esetén.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // Ezt a módszert akkor hívják meg, ha több kimeneti adatfolyam létrehozására van szükség. Például a HTML megjelenítése során a képfájlok listájához (JPG, PNG stb.)
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // Itt felszabadíthatja az adatokkal teli adatfolyamot, és például kihúzhatja a merevlemezre
            }
            public void Dispose()
            {
                // Erőforrások felszabadítása
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
Gratulálok! Sikeresen konvertált egy EPUB-fájlt XPS-formátumba az Aspose.HTML for .NET használatával.

## Következtetés

Ebben az átfogó oktatóanyagban megvizsgáltuk, hogyan használhatjuk fel az Aspose.HTML for .NET-et az EPUB-fájlok XPS-formátumba konvertálásához különféle testreszabási lehetőségekkel. Akár tapasztalt fejlesztő, akár csak kezdő, az Aspose.HTML leegyszerűsíti a folyamatot, lehetővé téve az EPUB-ból XPS-be történő konverziók egyszerű kezelését.

 Van kérdése vagy problémája van? Nézze meg a[Aspose.HTML dokumentáció](https://reference.aspose.com/html/net/) további információkért, vagy kérjen segítséget a[Aspose.HTML közösségi fórum](https://forum.aspose.com/).

## Gyakran Ismételt Kérdések

### Mi az Aspose.HTML a .NET számára?
Az Aspose.HTML for .NET egy hatékony könyvtár, amely lehetővé teszi a fejlesztők számára, hogy HTML-, EPUB- és XPS-dokumentumokkal dolgozzanak .NET-alkalmazásokban.

### Honnan tölthetem le az Aspose.HTML-t .NET-hez?
 Letöltheti az Aspose.HTML for .NET webhelyet[letöltési oldal](https://releases.aspose.com/html/net/).

### Létezik ingyenes próbaverzió az Aspose.HTML for .NET számára?
 Igen, ingyenes próbaverziót kaphat a webhelyen[itt](https://releases.aspose.com/).

### Hogyan szerezhetek ideiglenes licencet az Aspose.HTML for .NET számára?
 Ideiglenes engedély megszerzéséhez látogassa meg a[ideiglenes licenc oldal](https://purchase.aspose.com/temporary-license/).

### Hol találok további oktatóanyagokat és dokumentációt az Aspose.HTML for .NET-hez?
 Fedezze fel az oktatóanyagok és a részletes dokumentáció széles skáláját[Aspose.HTML dokumentáció](https://reference.aspose.com/html/net/) oldalon.