---
category: general
date: 2026-08-15
description: Készíts egy egyéni erőforráskezelőt C#-ban, amely kezeli a HTML erőforrásokat,
  például képeket és CSS-t. Ismerkedj meg a HTMLLoadOptions, memóriaáramok és HTMLDocument
  betöltésével.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom resource handler
- C# resource handler
- HTMLLoadOptions
- HTMLDocument loading
- memory stream for resources
language: hu
lastmod: 2026-08-15
og_description: Egyedi erőforráskezelő létrehozása C#-ban az HTML-erőforrások streamelésének
  szabályozásához. Ez az útmutató bemutatja az HTMLLoadOptions beállítását, a memóriafolyam
  kezelését, valamint az HTMLDocument betöltését egyedi logikával.
og_image_alt: Screenshot of C# code defining a custom resource handler class for HTML
  loading
og_title: Egyedi erőforráskezelő létrehozása C#-ban – teljes útmutató HTML erőforrás-kezeléshez
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  headline: Create custom resource handler in C# for HTML loading
  type: TechArticle
- description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  name: Create custom resource handler in C# for HTML loading
  steps:
  - name: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
    text: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
  - name: Configure `HTMLLoadOptions` to use the handler.
    text: Configure `HTMLLoadOptions` to use the handler.
  - name: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
    text: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
  - name: (Optional) Store received resources to disk for verification.
    text: (Optional) Store received resources to disk for verification.
  type: HowTo
tags:
- C#
- HTML
- resource handling
title: Egyedi erőforráskezelő létrehozása C#-ban HTML betöltéshez
url: /hu/net/working-with-html-documents/create-custom-resource-handler-in-c-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Egyedi erőforráskezelő létrehozása C#‑ban HTML betöltéshez

Ha **egyedi erőforráskezelőt** kell létrehoznod HTML fájlokhoz, ez az útmutató pontosan megmutatja, hogyan. Megtanulod, hogyan lehet elfogni a képeket, a CSS‑t és egyéb erőforrásokat egy HTML dokumentum betöltése közben, a `HTMLLoadOptions` és egy memória‑alapú stream használatával.

Az útmutató mindent lefed, ami egy újrahasználható kezelő megvalósításához, a betöltési beállítások konfigurálásához és az erőforrások helyes rögzítésének ellenőrzéséhez szükséges. Nem kell külső dokumentáció – csak az alábbi kód és a magyarázatok.

## Előfeltételek

- .NET 6.0 vagy újabb
- Alapvető C# ismeretek
- Hivatkozás a HTML feldolgozó könyvtárra, amely biztosítja a `HTMLDocument`, `HtmlLoadOptions` és `ResourceHandler` osztályokat (pl. GroupDocs.Viewer for .NET)

## A megoldás áttekintése

A következőket fogjuk tenni:

1. **Egyedi erőforráskezelő létrehozása** a `ResourceHandler` leszármaztatásával.
2. `HTMLLoadOptions` konfigurálása a kezelő használatához.
3. HTML fájl betöltése a `HTMLDocument`‑tel, miközben a kezelő minden erőforráshoz streamet biztosít.
4. (Opcionális) A kapott erőforrások lemezre mentése ellenőrzés céljából.

Minden lépéshez teljes forráskód és a mögöttes gondolatmenet tartozik.

## 1. lépés: Az egyedi erőforráskezelő osztály definiálása

Egyedi kezelő létrehozása azt jelenti, hogy felülírjuk a `HandleResource` metódust, hogy a könyvtár a erőforrás bájtjait egy általunk irányított stream‑be írja. A `MemoryStream` használata az adatot memóriában tartja, ami ideális teszteléshez vagy további feldolgozáshoz.

```csharp
using System;
using System.IO;
using GroupDocs.Viewer.Handler;   // Adjust namespace to match your library

namespace HtmlResourceDemo
{
    /// <summary>
    /// Provides a memory stream for each HTML resource (images, CSS, etc.).
    /// </summary>
    public class MyHandler : ResourceHandler
    {
        /// <summary>
        /// Called by the viewer for every external resource referenced in the HTML.
        /// </summary>
        /// <param name="info">Information about the resource (name, MIME type, etc.).</param>
        /// <returns>A writable stream that receives the resource data.</returns>
        public override Stream HandleResource(ResourceInfo info)
        {
            // A fresh MemoryStream ensures the viewer can write the resource bytes.
            // You could replace this with a FileStream to save directly to disk.
            return new MemoryStream();
        }
    }
}
```

**Miért fontos:**  
A `HandleResource` felülírása teljes irányítást ad arra, hogy hová kerülnek az erőforrás adatok. Ha később képeket szeretnél gyorsítótárazni, CSS‑t átalakítani vagy erőforrás‑használatot naplózni, a `MemoryStream`‑et bármilyen egyedi stream megvalósítással helyettesítheted.

## 2. lépés: `HTMLLoadOptions` konfigurálása a kezelő használatához

A `HTMLLoadOptions` lehetővé teszi, hogy a kezelőt beilleszd a betöltési csővezetékbe. A `ResourceHandler` tulajdonság beállítása azt mondja a megjelenítőnek, hogy minden külső eszközhöz hívja meg a `MyHandler`‑t.

```csharp
using GroupDocs.Viewer.Options;   // Namespace for HtmlLoadOptions

// ...

var loadOptions = new HtmlLoadOptions
{
    // Attach the custom handler defined in Step 1
    ResourceHandler = new MyHandler()
};
```

**Miért fontos:**  
A `ResourceHandler` megadása nélkül a megjelenítő az erőforrásokat az alapértelmezett helyre (gyakran egy ideiglenes mappába) írná. A saját kezelő megadása **egyedi erőforráskezelő** viselkedést hoz létre, amely illeszkedik az alkalmazásod tárolási stratégiájához.

## 3. lépés: A HTML dokumentum betöltése a konfigurált beállításokkal

Most töltsd be a HTML fájlt. A megjelenítő minden megtalált erőforráshoz meghívja a `MyHandler.HandleResource`‑t.

```csharp
using GroupDocs.Viewer;           // Namespace for HTMLDocument

// Path to the source HTML file
string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// Load the document using the custom load options
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);
```

Ekkor a HTML tartalom feldolgozásra kerül, és minden külső erőforrás a `MyHandler` által biztosított memória‑bufferbe kerül.

## 4. lépés (opcionális): A rögzített erőforrások elérése

Ha meg szeretnéd vizsgálni vagy megőrizni az erőforrásokat, módosíthatod a `MyHandler`‑t úgy, hogy minden `MemoryStream`‑et egy szótárba mentse, amelynek kulcsa az erőforrás neve.

```csharp
public class MyHandler : ResourceHandler
{
    // Stores streams for later retrieval
    public Dictionary<string, MemoryStream> Resources { get; } = new();

    public override Stream HandleResource(ResourceInfo info)
    {
        var stream = new MemoryStream();
        Resources[info.Name] = stream;
        return stream;
    }
}
```

Betöltés után iterálhatsz a `handler.Resources`‑en, és mindegyiket lemezre írhatod:

```csharp
var handler = new MyHandler();
var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);

// Save each captured resource
foreach (var kvp in handler.Resources)
{
    string fileName = Path.Combine("output_resources", kvp.Key);
    File.WriteAllBytes(fileName, kvp.Value.ToArray());
    Console.WriteLine($"Saved resource: {fileName}");
}
```

**Miért fontos:**  
Az erőforrások tárolása lehetővé teszi a későbbi feldolgozást, például képek optimalizálását, CSS minifikálását vagy archiválását. Emellett kézzelfogható ellenőrzést nyújt arról, hogy a **create custom resource handler** logika a várt módon működik.

## 5. lépés: Tisztítás

A `HTMLDocument`‑et és minden stream‑et el kell engedni, hogy felszabaduljanak a nem kezelt erőforrások.

```csharp
doc.Dispose();                     // Releases internal buffers
foreach (var stream in handler.Resources.Values)
{
    stream.Dispose();              // Flushes and releases memory
}
```

## Teljes, futtatható példa

Az alábbi önálló program bemutatja az összes lépést az osztálydefiníciótól az erőforrás‑kivonásig.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Viewer;
using GroupDocs.Viewer.Handler;
using GroupDocs.Viewer.Options;

namespace HtmlResourceDemo
{
    public class MyHandler : ResourceHandler
    {
        public Dictionary<string, MemoryStream> Resources { get; } = new();

        public override Stream HandleResource(ResourceInfo info)
        {
            var stream = new MemoryStream();
            Resources[info.Name] = stream;
            return stream;
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare paths
            string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");
            string outputDir = Path.Combine("output_resources");
            Directory.CreateDirectory(outputDir);

            // 2️⃣ Create handler and load options
            var handler = new MyHandler();
            var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };

            // 3️⃣ Load the HTML document
            using (HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions))
            {
                // Document is now loaded; resources are in handler.Resources
            }

            // 4️⃣ Persist captured resources
            foreach (var kvp in handler.Resources)
            {
                string filePath = Path.Combine(outputDir, kvp.Key);
                File.WriteAllBytes(filePath, kvp.Value.ToArray());
                Console.WriteLine($"Saved: {filePath}");
            }

            // 5️⃣ Clean up streams
            foreach (var stream in handler.Resources.Values)
                stream.Dispose();

            Console.WriteLine("All resources processed.");
        }
    }
}
```

**Várt kimenet**

```
Saved: output_resources/logo.png
Saved: output_resources/styles.css
Saved: output_resources/banner.jpg
All resources processed.
```

A konzol felsorolja minden olyan erőforrást, amelyet a megjelenítő a saját egyedi kezelődön keresztül streamelt, ezzel megerősítve, hogy a **create custom resource handler** munkafolyamat sikeres volt.

## Gyakori kérdések és széljegyek

| Kérdés | Válasz |
|----------|--------|
| *Mi a teendő, ha egy erőforrás nagy (pl. nagy felbontású kép)?* | Cseréld le a `MemoryStream`‑et egy `FileStream`‑re, amely egy ideiglenes mappára mutat. Ez megakadályozza a túlzott memóriahasználatot. |
| *Szűrhetek-e erőforrásokat típus szerint?* | A `HandleResource`‑ben ellenőrizheted az `info.MimeType` vagy `info.Extension` értékét, és `null`‑t visszaadva kihagyhatod a nem kívánt típusokat. A `null` visszaadása azt jelzi a megjelenítőnek, hogy hagyja ki az erőforrást. |
| *Szükséges a szálbiztonság?* | Ha ugyanazt a kezelőpéldányt több párhuzamos betöltéshez használod, védd a `Resources` szótárat lock‑kal, vagy használj párhuzamos gyűjteményt. |
| *Hogyan kezelem a relatív URL‑eket?* | A `ResourceInfo` tartalmazza az eredeti URL‑t; kombinálhatod a HTML fájl alapútvonalával a relatív hivatkozások feloldásához, mielőtt tárolnád őket. |

## Összegzés

Most már tudod, hogyan **create custom resource handler** C#‑ban HTML betöltéshez, hogyan konfiguráld a `HTMLLoadOptions`‑t, hogyan rögzítsd a stream‑elt eszközöket, és hogyan tisztítsd meg a forrásokat felelősségteljesen. Ez a minta teljes irányítást ad az erőforrás‑kezelés felett, lehetővé téve olyan forgatókönyveket, mint a valós‑időben történő kép‑feldolgozás, CSS‑átírás vagy biztonságos tárolás.

Ezután nézd meg a kapcsolódó témákat, például a **HTMLDocument betöltését** különböző megjelenítési beállításokkal, vagy bővítsd a kezelőt **C# resource handler** megvalósításokra, amelyek közvetlenül a felhő tárolóba írnak. Kísérletezz a `HandleResource` metódussal, hogy a projekted specifikus erőforrás‑folyamataira szabjad.

## Mit tanulj meg legközelebb?

Az alábbi oktatóanyagok szorosan kapcsolódnak, és a jelen útmutatóban bemutatott technikákra építenek. Minden forrás teljes, működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek további API‑funkciók elsajátításában és alternatív megvalósítási megközelítések felfedezésében saját projektjeidben.

- [Create HTML from String in C# – Custom Resource Handler Guide](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Custom Resource Handler in C# – Convert HTML to ZIP Tutorial](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}