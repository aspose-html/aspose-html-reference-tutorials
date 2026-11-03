---
category: general
date: 2026-03-31
description: Hozzon létre memóriafolyamot C#-ban, és tanulja meg, hogyan rendereljen
  HTML-t PNG-re, használjon egy egyéni erőforráskezelőt, mentse az HTML-t ZIP-be,
  valamint programozottan állítsa be a betűstílust – mindezt egyetlen oktatóanyagon
  belül.
draft: false
keywords:
- create memory stream
- render html to png
- custom resource handler
- save html to zip
- set font style programmatically
language: hu
og_description: Memóriastream létrehozása C#-ban, és azonnali HTML PNG-re renderelése,
  egyedi erőforráskezelők használata, HTML mentése ZIP-be, valamint a betűstílus programozott
  beállítása.
og_title: Memória Stream létrehozása C#‑ban – Teljes programozási útmutató
tags:
- C#
- HTML rendering
- Streams
- ZIP archives
- Image processing
title: Memóriastream létrehozása C#-ban – Teljes útmutató HTML rendereléssel és ZIP
  exporttal
url: /hu/net/rendering-html-documents/create-memory-stream-in-c-full-guide-with-html-rendering-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Memóriafolyam létrehozása C#‑ban – Teljes útmutató HTML rendereléssel és ZIP exporttal

Gondolkodtál már azon, hogyan **hozz létre memóriafolyamot** C#‑ban, majd egy HTML dokumentumot PNG‑képpé, ZIP‑fájllá alakíts, vagy akár futás közben megváltoztasd a betűstílusát? Nem vagy egyedül. Sok fejlesztő akad el, amikor egy dokumentum memória‑alapú reprezentációjára van szüksége, de nem akar a fájlrendszert érinteni.  

Ebben az útmutatóban egy teljes, vég‑től‑végig megoldást mutatunk be: felépítünk egy egyedi erőforrás‑kezelőt, HTML‑t egy `MemoryStream`‑be pumpálunk, ugyanazt a dokumentumot ZIP‑be csomagoljuk, majd végül antialiasinggal képpé rendereljük. A végére **HTML‑t PNG‑re renderelhetsz**, **HTML‑t ZIP‑be menthetsz**, és **programozottan beállíthatod a betűstílust** anélkül, hogy ideiglenes fájlokat írnál a lemezre.

## Előfeltételek

- .NET 6.0 vagy újabb (az API felület stabil a legújabb verziókban).  
- Hivatkozás egy HTML‑kép‑könyvtárra, amely biztosítja a `HTMLDocument`, `ImageRenderer` és a kapcsolódó típusokat – például a **HtmlRenderer.Core** (cseréld le a ténylegesen használt csomagra).  
- Alapvető ismeretek a streamekről, `using` blokkokról és a C# objektum‑orientált mintákról.

> **Pro tipp:** Ha Visual Studio‑t használsz, engedélyezd a **nullable referencia típusokat** (`<Nullable>enable</Nullable>`), hogy korán elkapd a finom hibákat.

## 1. lépés: Memóriafolyam létrehozása egy egyedi erőforrás‑kezelővel

Az első dolog, amire szükségünk van, egy kezelő, amely megmondja a HTML‑motornak, *hova* írja az egyes erőforrásokat (képek, CSS‑ek stb.). A `ResourceHandler` öröklésével minden kimenetet egyetlen `MemoryStream`‑be irányíthatunk.

```csharp
using System;
using System.IO;

// Step 1: Define a handler that writes resources to an in‑memory stream
class MemoryResourceHandler : ResourceHandler
{
    // The stream lives for the whole lifetime of the handler
    public MemoryStream OutputStream = new MemoryStream();

    // The engine calls this for every resource it needs to write
    public override Stream HandleResource(ResourceInfo info) => OutputStream;
}
```

**Miért fontos:**  
A `MemoryStream` teljesen a RAM‑ban él, nincs lemez‑I/O, ami tökéletes a nagy teljesítményű szcenáriókhoz, mint a webszolgáltatások vagy egységtesztek. A kezelő emellett az API‑t is boldoggá teszi, mivel a motor minden erőforráshoz egy `Stream`‑et vár.

## 2. lépés: HTML‑dokumentum betöltése és mentése a memóriafolyamba

Most betöltünk egy meglévő HTML‑fájlt (vagy egy stringet), és megadjuk, hogy a `MemoryResourceHandler`‑t használja. A `Save` hívás után az `OutputStream` tartalmazza a teljes HTML‑payload‑ot.

```csharp
using System.IO;

// Assume the HTML file lives under YOUR_DIRECTORY
HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");

// Instantiate the memory handler
MemoryResourceHandler memoryHandler = new MemoryResourceHandler();

// Save the document – all resources flow into the same MemoryStream
htmlDoc.Save(memoryHandler);
```

Ebben a pontban a stream pozíciója a végén van, ezért vissza kell tekerni, mielőtt olvasnánk a tartalmat.

```csharp
// Reset the stream position to the beginning
memoryHandler.OutputStream.Position = 0;

// Quick verification (optional)
// string htmlContent = new StreamReader(memoryHandler.OutputStream).ReadToEnd();
// Console.WriteLine(htmlContent);
```

> **Megjegyzés:** A fenti `ReadToEnd` sor ki van kommentelve, mert egy éles környezetben valószínűleg a streamet egy másik komponensnek adnád át, nem pedig kiíratnád.

## 3. lépés: Ugyanazon HTML ZIP‑ba csomagolása egy egyedi ZIP erőforrás‑kezelővel

Néha szükség van arra, hogy a HTML‑t az eszközeivel együtt szállítsuk. Egy második egyedi kezelő képes a ZIP‑be minden erőforráshoz egy bejegyzést létrehozni menet közben.

```csharp
using System.IO.Compression;

// Step 4: Define a handler that writes each resource into a ZIP archive
class ZipResourceHandler : ResourceHandler, IDisposable
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(string zipPath)
    {
        // Open (or create) the archive in write mode
        _zipArchive = ZipFile.Open(zipPath, ZipArchiveMode.Create);
    }

    // The engine calls this for each resource; we create a ZIP entry with the same name
    public override Stream HandleResource(ResourceInfo info) =>
        _zipArchive.CreateEntry(info.Name).Open();

    // Proper disposal of the underlying ZipArchive
    protected override void Dispose(bool disposing)
    {
        if (disposing) _zipArchive.Dispose();
        base.Dispose(disposing);
    }

    public void Dispose() => Dispose(true);
}
```

Most újra felhasználjuk ugyanazt a `htmlDoc` példányt, és egy ZIP‑fájlba írjuk.

```csharp
// Step 5: Save the HTML document into a ZIP file
using (var zipHandler = new ZipResourceHandler("YOUR_DIRECTORY/output.zip"))
{
    htmlDoc.Save(zipHandler);
}
```

**Edge case tipp:** Ha a HTML ugyanazt a képet többször hivatkozza, a ZIP‑kezelő duplikált bejegyzéseket hoz létre. Ennek elkerülésére tarthatunk egy `HashSet<string>`‑et a már hozzáadott nevekből, és a meglévő bejegyzés stream‑jét adhatjuk vissza.

## 4. lépés: Programozott betűstílus beállítása az alapértelmezett stíluslapon

A dokumentum kinézetének megváltoztatása a forrás‑HTML módosítása nélkül gyakran hasznos – például egy PDF‑előnézet generálásakor, ahol félkövér fejlécre van szükség. A könyvtár egy `DefaultViewStyleSheet`‑et biztosít, amelyet módosíthatunk.

```csharp
// Step 6: Apply bold and italic styling to the default view stylesheet
htmlDoc.DefaultViewStyleSheet.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

Bármely `WebFontStyle`‑ban definiált flag‑et kombinálhatsz. A változás azonnal érvényesül, és a későbbi renderelésekre vagy mentésekre hatással lesz.

## 5. lépés: HTML‑dokumentum renderelése PNG‑képpé

Végül alakítsuk a HTML‑t raszteres képpé. Az antialiasing és a hinting engedélyezésével éles szöveget és sima éleket kapunk.

```csharp
using System.Drawing; // For ImageRenderingOptions if needed

// Step 7: Render the document to an image with antialiasing and hinting
var renderingOptions = new ImageRenderingOptions
{
    UseAntialiasing = true,
    UseHinting = true
};

new ImageRenderer(renderingOptions).Render(htmlDoc, "YOUR_DIRECTORY/out.png");
```

**Ami látható lesz:** Egy `out.png` nevű PNG‑fájl a `YOUR_DIRECTORY` könyvtárban, amely pontosan úgy néz ki, mint a böngésző által renderelt HTML, de a korábban beállított félkövér‑dőlt stílussal.

![Screenshot of create memory stream output](placeholder-image.png "create memory stream example")

*Az alt‑szöveg tartalmazza az elsődleges kulcsszót a SEO‑igényeknek megfelelően.*

## Gyakori kérdések és buktatók

| Kérdés | Válasz |
|----------|--------|
| **Újra felhasználhatom ugyanazt a `HTMLDocument`‑et ZIP‑ba mentés után?** | Igen. A dokumentumobjektum a memóriában marad; többször is meghívhatod a `Save`‑t különböző kezelőkkel. |
| **Mi van, ha a HTML nagy bináris eszközöket tartalmaz?** | A `MemoryStream` ennek megfelelően növekszik. Nagyon nagy fájlok esetén fontold meg a közvetlen fájl‑streamelést vagy egy `BufferedStream` használatát. |
| **Kell-e meghívni a `Dispose`‑t a `MemoryResourceHandler`‑en?** | Nem kötelező, mivel csak egy `MemoryStream`‑et tart, amely a kezelő garbage‑collected‑je során felszabadul. Azonban a `Dispose` hívása jó szokás. |
| **Hogyan változtathatom meg a képformátumot (pl. JPEG a PNG helyett)?** | Adj másik fájlkiterjesztést az `ImageRenderer.Render`‑nek, vagy használd az `ImageRenderer.RenderToBitmap`‑et, majd mentsd `bitmap.Save("out.jpg", ImageFormat.Jpeg)`‑vel. |
| **A ZIP‑kezelő szál‑biztonságú?** | Nem. A `ZipArchive` nem szál‑biztonságú, ezért szinkronizáld a hozzáférést vagy hozz létre külön kezelőt szálanként. |

## Teljes működő példa

Az alábbi egyetlen, másolás‑beillesztés‑kész program, amely bemutatja a fent tárgyalt minden lépést. Cseréld le a `YOUR_DIRECTORY`‑t egy valós útvonalra a gépeden.

```csharp
// FullExample.cs
using System;
using System.IO;
using System.IO.Compression;

// Assume these types come from your HTML rendering library
using HtmlRendering; // placeholder namespace

class MemoryResourceHandler : ResourceHandler
{
    public MemoryStream OutputStream = new MemoryStream();
    public override Stream HandleResource(ResourceInfo info) => OutputStream;
}

class ZipResourceHandler : ResourceHandler, IDisposable
{
    private readonly ZipArchive _zipArchive;
    public ZipResourceHandler(string zipPath) =>
        _zipArchive = ZipFile.Open(zipPath, ZipArchiveMode.Create);

    public override Stream HandleResource(ResourceInfo info) =>
        _zipArchive.CreateEntry(info.Name).Open();

    protected override void Dispose(bool disposing)
    {
        if (disposing) _zipArchive.Dispose();
        base.Dispose(disposing);
    }

    public void Dispose() => Dispose(true);
}

class Program
{
    static void Main()
    {
        // 1️⃣ Load HTML
        var htmlDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");

        // 2️⃣ Write to a memory stream
        var memHandler = new MemoryResourceHandler();
        htmlDoc.Save(memHandler);
        memHandler.OutputStream.Position = 0;
        // Optional: verify content
        // Console.WriteLine(new StreamReader(memHandler.OutputStream).ReadToEnd());

        // 3️⃣ Zip the same document
        using (var zipHandler = new ZipResourceHandler("YOUR_DIRECTORY/output.zip"))
        {
            htmlDoc.Save(zipHandler);
        }

        // 4️⃣ Change font style programmatically
        htmlDoc.DefaultViewStyleSheet.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // 5️⃣ Render to PNG with antialiasing & hinting
        var renderOpts = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            UseHinting = true
        };
        new ImageRenderer(renderOpts).Render(htmlDoc, "YOUR_DIRECTORY/out.png");

        Console.WriteLine("All operations completed successfully.");
    }
}
```

A program futtatásakor három artefaktot kapsz:

1. **Memóriában lévő HTML** a `memHandler.OutputStream`‑ben.  
2. **`output.zip`**, amely a HTML‑t és az összes hivatkozott erőforrást tartalmazza.  
3. **`out.png`** – egy renderelt kép, amely a félkövér‑dőlt stílust is alkalmazza.

## Összegzés

Megmutattuk, hogyan **hozz létre memóriafolyamot** C#‑ban, és hogyan integráld zökkenőmentesen HTML rendereléssel, ZIP archiválással és képgenerálással. A fő tanulság, hogy egyetlen `HTMLDocument` többféleképpen menthető – `MemoryStream`‑be, ZIP‑archívumba vagy PNG‑fájlba – egyszerűen a `ResourceHandler` cseréjével.  

Ha tovább szeretnél menni, próbáld ki:

- **Renderelés PDF‑re** egy olyan PDF‑rendererrel, amely `Stream`‑et fogad.  
- **A memóriafolyam tömörítése** hálózaton keresztüli küldés előtt (pl. `GZipStream`).  
- **Több HTML‑oldal egyesítése** egy ZIP‑be a tömeges exporthoz.

Kísérletezz nyugodtan, és ne habozz kommentet írni, ha elakadsz. Boldog kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}