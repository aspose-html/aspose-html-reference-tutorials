---
category: general
date: 2026-05-28
description: Ismerje meg, hogyan készíthet egy egyedi erőforrás-kezelőt C#-ban, amely
  weboldalt képpé renderel, képernyőképet készít a weboldalról, és HTML-t PNG-ként
  ment, teljes kóddal.
draft: false
keywords:
- custom resource handler
- render webpage to image
- capture webpage screenshot
- render html to png
- save webpage as png
language: hu
og_description: Készíts egy egyedi erőforráskezelőt C#-ban, és renderelj egy weboldalt
  képre. Készíts képernyőképet, rendereld a HTML-t PNG-re, és mentsd el az eredményt
  egy teljes példával.
og_title: Egyéni erőforráskezelő C#-ban – Weboldal képpé renderelése
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to create a custom resource handler in C# to render webpage
    to image, capture webpage screenshot and save HTML as PNG with complete code.
  headline: Custom Resource Handler in C# – Render Webpage to Image
  type: TechArticle
- description: Learn how to create a custom resource handler in C# to render webpage
    to image, capture webpage screenshot and save HTML as PNG with complete code.
  name: Custom Resource Handler in C# – Render Webpage to Image
  steps:
  - name: Expected Output
    text: Running the full program should produce a PNG that looks like a faithful
      snapshot of `https://example.com`. Open it in any image viewer, and you’ll see
      the page rendered at the default viewport size (usually 1024 × 768 px). All
      linked images and styles are stored alongside, ready for reuse.
  - name: What if the target page uses relative URLs?
    text: Our handler already strips the leading slash (`info.Path.TrimStart('/')`)
      and combines it with the output folder, so relative paths resolve correctly.
      If you encounter a URL that starts with `//` (protocol‑relative), the renderer
      normalizes it before calling `HandleResource`.
  - name: How do I change the output dimensions?
    text: 'Pass a `Size` object to `RenderPage` overload:'
  - name: Can I render multiple pages in one run?
    text: Absolutely. Just loop over a list of URLs and call `RenderPage` each time.
      The same `MyResourceHandler` instance will keep populating the `output` folder,
      keeping everything tidy.
  - name: What about authentication‑protected sites?
    text: If the page requires cookies or HTTP headers, configure an `HttpClient`
      and assign it to the renderer’s `HttpClient` property (if your library exposes
      it). This keeps the **render html to png** flow seamless for internal dashboards.
  type: HowTo
tags:
- C#
- ImageRenderer
- WebAutomation
title: Egyéni erőforráskezelő C#‑ban – Weboldal renderelése képpé
url: /hu/net/generate-jpg-and-png-images/custom-resource-handler-in-c-render-webpage-to-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Egyéni erőforráskezelő C#‑ban – Weboldal renderelése képpé

Gondolkodtál már azon, hogyan lehet **custom resource handler**-rel tökéletes képernyőképet készíteni bármely oldalról? Nem vagy egyedül. A weboldal képernyőképének programozott rögzítése olyan, mintha egy mozgó célt próbálnál elkapni, különösen akkor, ha a képeket és betűtípusokat pontosan oda szeretnéd menteni, ahová szükséged van.

Ebben az útmutatóban végigvezetünk egy **custom resource handler** felépítésén C#‑ban, a renderelési beállítások konfigurálásán, és végül az ImageRenderer használatán a **render webpage to image** funkcióval. A végére tudni fogod, hogyan **capture webpage screenshot**, **render html to png**, és **save webpage as png** anélkül, hogy a hajadba nyúlnál.

## Amire szükséged lesz

- .NET 6.0 vagy újabb (az általunk használt API a .NET Standard 2.0‑ra céloz, így bármely modern futtatókörnyezet működik)
- Egy NuGet csomag, amely biztosítja a `ImageRenderer`, `ImageRenderingOptions` és a kapcsolódó típusokat (pl. *Aspose.HTML* vagy hasonló könyvtár)
- Alap C# ismeretek – semmi egzotikus, csak néhány `using` utasítás és egy `Main` metódus
- Egy kimeneti mappa, ahová a renderelő fájlokat helyezheti (nyugodtan hozd létre manuálisan, vagy hagyd, hogy a kód létrehozza)

Ennyi. Nincs extra szolgáltatás, nincs headless böngésző, csak tiszta .NET kód.

![Egyéni erőforráskezelő a renderelt erőforrások mentéséhez](https://example.com/assets/custom-resource-handler.png "egyéni erőforráskezelő")

## 1. lépés: **Custom Resource Handler** felépítése

Az első dolog, amire szükséged van, egy `ResourceHandler`‑ből származó osztály. Itt történik a varázslat: minden kép, CSS‑fájl vagy betűtípus, amelyet a renderelő kér, a te kezelődön keresztül kerül, és te döntöd el, hová írod.

```csharp
using System.IO;
using Aspose.Html.Rendering.Image;   // Adjust the namespace to your library

// Step 1: Create a custom resource handler to store rendered resources
class MyResourceHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info)
    {
        // Build a safe file path inside the output directory
        string filePath = Path.Combine("output", info.Path.TrimStart('/'));

        // Ensure the directory hierarchy exists
        Directory.CreateDirectory(Path.GetDirectoryName(filePath)!);

        // Return a writable stream that the renderer will fill
        return File.OpenWrite(filePath);
    }
}
```

**Why this matters:** Handler nélkül a renderelő esetleg a memóriában tartja az erőforrásokat vagy teljesen eldobja őket. A `Stream` kiadásával teljes irányítást kapsz arról, hová kerül minden eszköz – tökéletes későbbi újrahasználathoz vagy hibakereséshez.

## 2. lépés: Kép renderelési beállítások konfigurálása

Miután megvan a hely az eszközöknek, mondjuk meg a renderelőnek, hogyan szeretnénk a végső képet. Az antialiasing kisimítja az éleket, a hinting javítja a szöveg olvashatóságát, és egy betűtípus kiválasztása biztosítja, hogy a kimenet megfeleljen a tervezésednek.

```csharp
using Aspose.Html.Drawing;          // For ImageRenderingOptions, TextOptions, Font, etc.

// Step 2: Set up image rendering options (antialiasing, text hinting, font)
var imageOptions = new ImageRenderingOptions
{
    UseAntialiasing = true,
    TextOptions = new TextOptions { UseHinting = true },
    Font = new Font("Times New Roman", 14, WebFontStyle.Bold)
};
```

**Why these settings?** Az antialiasing csökkenti a lépcsőzetes pixeleket, különösen a görbéknél. A hinting azt mondja a rasterizálónak, hogy a glifeket pixelhatárokhoz igazítsa, ami kulcsfontosságú, amikor **render html to png** tipikus képernyőfelbontásokon. A félkövér Times New Roman csak egy példa; cseréld bármely web‑biztonságos vagy egyedi betűtípusra, amelyet kedvelsz.

## 3. lépés: Kezelő összekapcsolása az Image Rendererrel

Miután a beállítások és a kezelő készen áll, létrehozzuk a `ImageRenderer`‑t. A `MyResourceHandler`‑t a `ResourceHandler` tulajdonsághoz rendelve biztosítjuk, hogy minden külső fájl a lemezen landoljon.

```csharp
using Aspose.Html.Rendering.Image; // For ImageRenderer

// Step 3: Create the image renderer with the options and the custom handler
var renderer = new ImageRenderer(imageOptions)
{
    ResourceHandler = new MyResourceHandler()
};
```

**Pro tip:** Ha valaha is naplózni szeretnéd minden kérést, felülírhatod a `HandleResource`‑t, és a `Console.WriteLine(info.Path)`‑t hozzáadhatod a stream visszaadása előtt. Ez a kis kiegészítés órákat takaríthat meg a hiányzó betűtípusok vagy törött képek hibakeresésekor.

## 4. lépés: **Render Webpage to Image** és mentés

Végül mondd meg a renderelőnek, mely URL‑t kell rögzíteni, és hová kerüljön a PNG. Az alábbi hívás elvégzi a nehéz munkát: letölti az oldalt, feldolgozza a CSS‑t, betölti a betűtípusokat, és kiírja a keletkezett bitmapet.

```csharp
// Step 4: Render a web page to an image file
renderer.RenderPage("https://example.com", "output/page.png");
```

Amikor a metódus befejeződik, a `output` mappában két dologra számíthatsz:

1. `page.png` – az oldal képernyőképe (a **capture webpage screenshot** eredménye)
2. Egy alkönyvtár‑struktúra, amely tükrözi az oldal erőforrásait (CSS, képek, betűtípusok) – mind mentve a **custom resource handler**-nek köszönhetően

### Várható kimenet

A teljes program futtatása egy PNG‑t kell, hogy előállítson, amely hű mása a `https://example.com` oldalnak. Nyisd meg bármely képnézőben, és láthatod, hogy az oldal a alapértelmezett nézetablak méretben (általában 1024 × 768 px) lett renderelve. Minden hivatkozott kép és stílus mellé tárolva van, készen áll a újrahasználatra.

## Gyakori kérdések és szélhelyzetek

### Mi van, ha a céloldal relatív URL‑eket használ?

A mi kezelőnk már eltávolítja a vezető perjelet (`info.Path.TrimStart('/')`) és kombinálja a kimeneti mappával, így a relatív útvonalak helyesen feloldódnak. Ha egy `//`‑vel kezdődő URL‑t (protokoll‑relatív) találsz, a renderelő normalizálja azt, mielőtt meghívná a `HandleResource`‑t.

### Hogyan változtathatom meg a kimeneti méreteket?

Pass a `Size` object to `RenderPage` overload:

```csharp
renderer.RenderPage("https://example.com", "output/page.png", new Size(1920, 1080));
```

Így **save webpage as png** magas felbontásban, nyomtatásra kész anyagokhoz.

### Renderelhetek több oldalt egy futtatás során?

Természetesen. Csak iterálj egy URL‑listán, és minden alkalommal hívd meg a `RenderPage`‑t. Ugyanaz a `MyResourceHandler` példány folyamatosan feltölti a `output` mappát, így minden rendezett marad.

### Mi a helyzet a hitelesítéssel védett oldalakkal?

Ha az oldal sütiket vagy HTTP fejléceket igényel, konfigurálj egy `HttpClient`‑et, és rendeld hozzá a renderelő `HttpClient` tulajdonságához (ha a könyvtárad ezt lehetővé teszi). Ez zökkenőmentessé teszi a **render html to png** folyamatot a belső műszerfalak számára.

## Teljes működő példa

Összeállítva mindent, itt egy minimális konzolos alkalmazás, amelyet beilleszthetsz a Visual Studio‑ba:

```csharp
using System;
using System.IO;
using Aspose.Html.Drawing;
using Aspose.Html.Rendering.Image;

class MyResourceHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info)
    {
        string filePath = Path.Combine("output", info.Path.TrimStart('/'));
        Directory.CreateDirectory(Path.GetDirectoryName(filePath)!);
        return File.OpenWrite(filePath);
    }
}

class Program
{
    static void Main()
    {
        var imageOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            TextOptions = new TextOptions { UseHinting = true },
            Font = new Font("Times New Roman", 14, WebFontStyle.Bold)
        };

        var renderer = new ImageRenderer(imageOptions)
        {
            ResourceHandler = new MyResourceHandler()
        };

        // Render the page and save as PNG
        renderer.RenderPage("https://example.com", "output/page.png");

        Console.WriteLine("Done! Screenshot saved to output/page.png");
    }
}
```

Fordítsd le és futtasd (`dotnet run`), majd ellenőrizd a `output` könyvtárat. Most **rendered a webpage to image**, rögzítettél egy képernyőképet, és elmentetted a HTML‑t PNG‑ként – mindezt egy rendezett **custom resource handler** köszönheti.

## Következtetés

Létrehoztunk egy **custom resource handler**‑t, finomhangoltuk a renderelési beállításokat, és egy `ImageRenderer`‑t használtunk a **render webpage to image** feladatra. Az eredmény egy tiszta PNG plusz a teljes erőforráskészlet, amely mindent biztosít, ami ahhoz kell, hogy **capture webpage screenshot**, **render html to png**, és **save webpage as png** jelentéseket, bélyegképeket vagy automatizált teszteket készíts.

Mi a következő? Kísérletezz a következőkkel:

- Különböző nézetablak méretek mobil és asztali képernyőképekhez
- Vízjelek vagy átfedések hozzáadása a renderelés után
- Exportálás más formátumokba (JPEG, BMP) az `ImageRenderingOptions` módosításával

Nyugodtan hagyj megjegyzést, ha elakadsz vagy találsz egy okos trükköt. Boldog kódolást, és legyenek a képernyőképeid mindig pixel‑tökéletesek!

## Kapcsolódó oktatóanyagok

- [Hogyan mentsünk HTML‑t C#‑ban – Teljes útmutató egy egyéni erőforráskezelő használatával](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [HTML létrehozása karakterláncból C#‑ban – Egyéni erőforráskezelő útmutató](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Hogyan rendereljünk HTML‑t PNG‑ként – Teljes C# útmutató](/html/english/net/rendering-html-documents/how-to-render-html-as-png-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}