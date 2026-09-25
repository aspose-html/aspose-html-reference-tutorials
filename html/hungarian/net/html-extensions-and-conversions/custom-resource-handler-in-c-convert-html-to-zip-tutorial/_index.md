---
category: general
date: 2026-02-10
description: Az egyedi erőforráskezelő lehetővé teszi, hogy C#-ban HTML-t ZIP-be konvertálj.
  Ismerd meg, hogyan lehet HTML-t ZIP-fájlba menteni, és hatékonyan streamelni a HTML‑erőforrásokat.
draft: false
keywords:
- custom resource handler
- convert html to zip
- save html as zip
- create zip with html
- stream html resources
language: hu
og_description: Az egyedi erőforráskezelő lehetővé teszi, hogy C#‑ban HTML‑t ZIP‑fájlra
  konvertálj. Kövesd ezt a lépésről‑lépésre útmutatót, hogy HTML‑t ZIP‑be ments és
  HTML‑erőforrásokat streamelj.
og_title: Egyéni erőforráskezelő C#-ban – HTML konvertálása ZIP-be
tags:
- Aspose.HTML
- C#
- ZIP archive
- file streaming
title: Egyéni erőforráskezelő C#-ban – HTML ZIP-be konvertálás útmutató
url: /hu/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Egyedi erőforráskezelő – HTML konvertálása ZIP-be C#‑ban

Gondoltad már, hogyan **egyedi erőforráskezelő** segítségével alakíthatod át a nyers HTML‑t egy ZIP‑fájlba? Nem vagy egyedül. Sok fejlesztő akad el, amikor egy HTML‑oldalt kell összecsomagolni az összes asset‑jével anélkül, hogy ideiglenes fájlokkal szennyezné a lemezt. A jó hír? Az Aspose.HTML‑del mindezt memóriában megteheted, és a trükk egy egyedi erőforráskezelőben rejlik.

Ebben az útmutatóban egy teljes, futtatható példán keresztül mutatjuk be, hogyan **konvertálhatod a HTML‑t ZIP‑be**, **mentheted a HTML‑t ZIP‑ként**, és **streamelheted a HTML‑erőforrásokat** menet közben. A végére egyetlen metódusod lesz, amely egy HTML‑stringet vesz, és egy letölthető `result.zip`‑et ad vissza, amely tartalmazza az oldalt és minden hivatkozott erőforrást.

> **Előfeltételek** – .NET 6+ (vagy .NET Framework 4.6+), Aspose.HTML for .NET telepítve, valamint az áramlások (streams) alapvető ismerete. Külső eszközök nem szükségesek.

---

## Egyedi erőforráskezelő – Alapgondolat

Az *erőforráskezelő* az Aspose.HTML‑ben egy olyan objektum, amely eldönti, **hova** kerül a dokumentum egyes részei – legyen az fájl a lemezen, memória‑buffer, vagy, ahogy mi megmutatjuk, egy ZIP‑archívum bejegyzése. A `ResourceHandler` alosztályozásával teljes irányítást kapsz a fő HTML fájl **és** minden kiegészítő erőforrás (CSS, képek, betűkészletek stb.) kimeneti helye felett.

Gondolj rá úgy, mint egy forgalomirányítóra a dokumentumod asset‑jeihez: a `HandleResource` metódus egy `Stream`‑et ad a fő HTML‑hez, míg a `ResourceSaving` esemény lehetővé teszi, hogy minden függő fájlt a tényleges írás előtt elkapj.

---

## 1. lépés: Egyedi erőforráskezelő megvalósítása

Először hozz létre egy osztályt, amely a `ResourceHandler`‑ből származik. Felülírjuk a `HandleResource`‑t, hogy az Aspose‑nek egy friss `MemoryStream`‑et adjunk a fő HTML kimenethez. A hivatkozott asset‑ekhez később a `ResourceSaving`‑t használjuk.

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using System.IO;

/// <summary>
/// Supplies a stream for every resource the HTML document needs to save.
/// </summary>
class MyHandler : ResourceHandler
{
    /// <summary>
    /// Returns a new stream for the main HTML content.
    /// </summary>
    public override Stream HandleResource(ResourceInfo info)
    {
        // In real life you might return a FileStream or a ZipEntry stream.
        // Here we just hand back a clean MemoryStream.
        return new MemoryStream();
    }
}
```

**Miért fontos:** Egy új `MemoryStream` visszaadása azt jelenti, hogy a HTML soha nem érinti a fájlrendszert. Ez a tiszta, memóriában történő ZIP‑létrehozás alapja.

---

## 2. lépés: HTML mentése egyetlen MemoryStream‑be

Miután megvan a kezelő, generálhatunk egy HTML‑dokumentumot, és teljes egészében memóriában rögzíthetjük. Ez a lépés opcionális, ha csak a ZIP‑re van szükséged, de jól szemlélteti, hogyan működik a kezelő önmagában.

```csharp
using Aspose.Html;

// Sample HTML – replace with your own markup or load from a file.
string htmlContent = "<html><head><title>Demo</title></head><body>Hello world!</body></html>";

// Create the document from a string.
HTMLDocument htmlDocument = new HTMLDocument(htmlContent);

// Instantiate our custom handler.
MyHandler memoryHandler = new MyHandler();

using (MemoryStream htmlStream = new MemoryStream())
{
    // Save triggers HandleResource and writes the HTML into htmlStream.
    htmlDocument.Save(htmlStream, memoryHandler);

    // Reset position for potential reading.
    htmlStream.Position = 0;

    // For demo purposes, dump the HTML to console.
    using (StreamReader reader = new StreamReader(htmlStream))
    {
        Console.WriteLine("Generated HTML:");
        Console.WriteLine(reader.ReadToEnd());
    }
}
```

**Várt kimenet** (olvasóbarát formázásban):

```
Generated HTML:
<html><head><title>Demo</title></head><body>Hello world!</body></html>
```

Ha ezt a kódrészletet futtatod, láthatod, hogy a HTML csak a RAM‑ban él – nincs létrehozva ideiglenes fájl.

---

## 3. lépés: HTML és erőforrások csomagolása ZIP‑archívumba

Most jön a lényeg: a HTML **és** minden hivatkozott asset egy ZIP‑fájlba csomagolása anélkül, hogy köztes fájlokat írnánk a lemezre. A `System.IO.Compression.ZipArchive`‑t használjuk a `ResourceSaving` eseménnyel együtt.

```csharp
using Aspose.Html;
using System.IO;
using System.IO.Compression;

// Re‑use the same HTMLDocument from the previous step.
HTMLDocument htmlDocument = new HTMLDocument("<html><body>Hello world!</body></html>");

// Path where the final ZIP will be written.
string zipPath = Path.Combine(Environment.CurrentDirectory, "result.zip");

// Open a FileStream for the ZIP file.
using (FileStream zipFile = new FileStream(zipPath, FileMode.Create))
using (ZipArchive zipArchive = new ZipArchive(zipFile, ZipArchiveMode.Update))
{
    // Create a fresh handler for the ZIP operation.
    MyHandler zipHandler = new MyHandler();

    // Hook the ResourceSaving event – this fires for every resource.
    zipHandler.ResourceSaving += (sender, e) =>
    {
        // Ensure we don't create leading folder entries like "/css/style.css".
        string entryName = e.ResourceInfo.Path.TrimStart('/');

        // Create a new entry inside the ZIP.
        ZipArchiveEntry entry = zipArchive.CreateEntry(entryName);

        // Provide the stream that Aspose will write into.
        e.Stream = entry.Open();
    };

    // Save the document; the handler will fill the ZIP for us.
    htmlDocument.Save(zipHandler);
}

// Verify the ZIP exists.
Console.WriteLine($"ZIP created at: {zipPath}");
```

### Mi történik a háttérben?

1. **`ResourceSaving` lefut** a fő HTML fájlra és minden hivatkozott assetre.
2. A lambda egy megfelelő bejegyzést hoz létre (`CreateEntry`) a nyitott ZIP‑ben.
3. Az `e.Stream = entry.Open()` sorral egy írható áramlást adunk az Aspose‑nek, amely közvetlenül a ZIP‑bejegyzésbe ír.
4. Amikor a `htmlDocument.Save` befejeződik, a ZIP egy teljes HTML‑oldalt tartalmaz plusz minden CSS‑t, képet vagy betűkészletet, amelyet a markup hivatkozott.

**Eredmény:** Egyetlen `result.zip` fájl, amelyet böngészőbe küldhetsz, e‑mailhez csatolhatsz, vagy blob tárolóba menthetsz – semmilyen ideiglenes fájl nem marad hátra.

---

## Bónusz: A ZIP használata Web API‑ban

Ha ASP.NET Core végpontot építesz, amely igény szerint visszaadja a ZIP‑et, ugyanaz a logika érvényes. Íme egy tömör controller‑action:

```csharp
[ApiController]
[Route("api/[controller]")]
public class HtmlZipController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult DownloadZip()
    {
        // Build the document (could be loaded from a DB, etc.).
        var html = "<html><body><h1>Dynamic report</h1></body></html>";
        var doc = new HTMLDocument(html);
        var handler = new MyHandler();

        // Prepare an in‑memory ZIP.
        using var zipStream = new MemoryStream();
        using (var archive = new ZipArchive(zipStream, ZipArchiveMode.Create, true))
        {
            handler.ResourceSaving += (s, e) =>
            {
                var entry = archive.CreateEntry(e.ResourceInfo.Path.TrimStart('/'));
                e.Stream = entry.Open();
            };
            doc.Save(handler);
        }

        zipStream.Position = 0;
        return File(zipStream, "application/zip", "report.zip");
    }
}
```

Most egy GET kérés a `/api/HtmlZip/download`‑ra közvetlenül a kliensnek streameli a generált ZIP‑et – tökéletes a menet közbeni jelentésekhez.

---

## Gyakori hibák és tippek

| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| **Üres mappák a ZIP‑ben** | A `ResourceInfo.Path` `/`‑vel kezdődik, így `/` bejegyzés jön létre | Használd a `TrimStart('/')`‑t, ahogy az eseménykezelőben látható. |
| **Hiányzó képek** | Az abszolút URL‑ekkel hivatkozott képek nem kerülnek automatikusan letöltésre | Állítsd be `htmlDocument.Options.ResourceLoading = ResourceLoadingMode.Stream`‑et, és adj meg egy egyedi `ResourceHandler`‑t, amely letölti a távoli asset‑eket. |
| **Nagy fájlok memória‑nyomást okoznak** | Minden áramlás memóriában marad, amíg a ZIP be nem zárul | Válts `ZipArchiveMode.Update`‑ról `Create`‑ra, és írd minden bejegyzést közvetlenül anélkül, hogy bufferelnél, vagy streamelj lemezről, ha a méret meghaladja a RAM‑ot. |
| **„The stream does not support seeking” kivétel** | Ugyanazt a nem‑kereshető áramlást próbálod újra felhasználni több erőforráshoz | Mindig adj friss `MemoryStream`‑et vagy `entry.Open()`‑t minden erőforráshoz. |

---

## Összegzés

Megmutattuk, hogyan teszi lehetővé egy **egyedi erőforráskezelő** a **HTML‑ZIP konvertálást**, a **HTML ZIP‑ként való mentését**, és a **HTML erőforrások streamelését** anélkül, hogy a fájlrendszert megérintenéd. A `HandleResource` felülírásával és a `ResourceSaving` esemény kihasználásával finomhangolhatod minden egyes bájtot, amely az Aspose.HTML‑ből kilép.

A minta skálázható: cseréld ki a memóriabeli `MemoryStream`‑et egy felhő‑blob áramlásra, adj hozzá tömörítési beállításokat, vagy építs be egy naplózási réteget, amely nyomon követi, mely assetek kerülnek csomagolásra. A lehetőségek végtelenek, amint uralod az erőforrás‑pipeline‑t.

Készen állsz a következő lépésre? Próbáld meg beágyazni a CSS‑t és a képeket a HTML‑be, kísérletezz távoli erőforrások betöltésével, vagy integráld ezt a folyamatot egy Azure Function‑be, amely igény szerint visszaad egy ZIP‑et. Boldog kódolást!

--- 

*Az egyedi erőforráskezelő HTML‑t ZIP‑fájlba alakító folyamata.*

![egyedi erőforráskezelő munkafolyama](https://example.com/placeholder-image.png "egyedi erőforráskezelő munkafolyama")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}