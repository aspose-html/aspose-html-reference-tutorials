---
category: general
date: 2026-02-13
description: Tanulja meg, hogyan építsen egy egyéni erőforráskezelőt C#‑ban, amely
  HTML‑t ZIP archívummá konvertál, memóriából ZIP‑et készít az Aspose.HTML segítségével
  – lépésről lépésre útmutató.
draft: false
keywords:
- custom resource handler
- convert html zip archive
- create zip from memory
- Aspose HTML
- in‑memory streaming
- C# zip compression
language: hu
og_description: Ismerje meg a teljes C# megoldást, amely egy egyedi erőforráskezelő
  segítségével közvetlenül a memóriában alakítja át a HTML-t ZIP-archívummá.
og_title: Egyedi erőforráskezelő – HTML konvertálása ZIP-be memóriából
tags:
- C#
- Aspose.HTML
- ZipArchive
- MemoryStream
title: Egyéni erőforráskezelő C#-ban – HTML konvertálása ZIP archívummá memóriából
url: /hu/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-archive-fro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Egyéni erőforráskezelő – HTML konvertálása ZIP archívummá memóriából

Volt már szükséged **custom resource handler**‑re, hogy minden képet, CSS‑fájlt vagy szkriptet, amelyet egy HTML‑oldal betölt, összegyűjts, majd mindent ZIP‑be csomagolj anélkül, hogy a lemezt érintenéd? Nem vagy egyedül. Sok web‑automatizálási vagy e‑mail‑sablonozási helyzetben szeretnéd az egész oldalt egyetlen, hordozható csomagba foglalni, és inkább a RAM‑ban tartanád a gyorsaság és a biztonság érdekében.

Ebben az útmutatóban egy teljes, futtatható példán keresztül mutatjuk be, hogyan **convert HTML zip archive** egy **custom resource handler** segítségével, majd hogyan **create zip from memory** a .NET `System.IO.Compression` osztályával. A végére egy önálló módszert kapsz, amelyet bármely, Aspose.HTML‑t használó C# projektbe beilleszthetsz.

## Amire szükséged lesz

- .NET 6+ (vagy .NET Framework 4.7.2+)  
- Aspose.HTML for .NET (NuGet csomag `Aspose.HTML`)  
- Alapvető ismeretek a streamekkel és a `ZipArchive` osztállyal  

Nincs külső eszköz, nincs ideiglenes fájl, csak tiszta memóriában történő feldolgozás.

## 1. lépés: Define the Custom Resource Handler

A megoldás szíve egy osztály, amely örökli a `Aspose.Html.ResourceHandler`‑t. Feladata, hogy minden külső erőforráshoz, amelyet a HTML motor kér, egy friss `Stream`‑et biztosítson. Minden alkalommal új `MemoryStream` visszaadásával az adatot elkülönítve és későbbi csomagolásra készen tartjuk.

```csharp
using System.IO;
using Aspose.Html;

// Step 1 – Custom handler that stores resources in memory
class MemoryResourceHandler : ResourceHandler
{
    // The framework calls this method for every external resource (images, CSS, etc.)
    public override Stream HandleResource(Resource resource)
    {
        // We give the engine an empty stream; later we’ll fill it with the actual bytes.
        // Using MemoryStream means everything stays in RAM.
        return new MemoryStream();
    }
}
```

**Miért fontos ez:**  
Ha engeded, hogy az Aspose.HTML az erőforrásokat lemezre írja, később takarítanod kell. Egy memóriában működő kezelő kiküszöböli a I/O terhelést, és biztonságossá teszi a kódot elszigetelt környezetekben (pl. Azure Functions).

## 2. lépés: A HTML dokumentum betöltése

Ezután mutasd az Aspose.HTML‑t arra a HTML fájlra, amelyet csomagolni szeretnél. A dokumentum lehet lemezen, URL‑en vagy akár nyers szövegként. Itt egyszerűség kedvéért egy fájlútvonalat használunk.

```csharp
using Aspose.Html;

// Step 2 – Load the source HTML
HtmlDocument document = new HtmlDocument("YOUR_DIRECTORY/input.html");
```

> **Pro tipp:** Ha a HTML relatív erőforrásokra hivatkozik, győződj meg róla, hogy az `input.html` ugyanabban a mappában van, mint azok az eszközök, különben a handler nem fogja megtalálni őket.

## 3. lépés: A handler bekötése és mentés MemoryStream‑be

Most példányosítjuk a handlert, és megmondjuk az Aspose.HTML‑nek, hogy használja a `HtmlSaveOptions.OutputStorage`‑on keresztül. A keletkező HTML (az átírt erőforrás‑URL‑ekkel együtt) egy `MemoryStream`‑be kerül.

```csharp
using Aspose.Html.Saving;
using System.IO;

// Step 3 – Prepare the handler and an in‑memory buffer for the final HTML
var resourceHandler = new MemoryResourceHandler();

using (MemoryStream htmlMemoryStream = new MemoryStream())
{
    document.Save(htmlMemoryStream, new HtmlSaveOptions
    {
        OutputStorage = resourceHandler // redirects all resources to the handler
    });

    // At this point htmlMemoryStream contains the full HTML file,
    // while each external resource resides in the streams returned by the handler.
```

**Mi történik a háttérben?**  
Amikor a `document.Save` lefut, az Aspose.HTML a `MemoryResourceHandler`‑től kér egy streamet minden erőforráshoz. Mivel üres `MemoryStream`‑eket adtunk vissza, a motor a nyers bájtokat közvetlenül a memóriába írja. Ideiglenes fájlok nem jönnek létre.

## 4. lépés: A ZIP archívum teljes összeállítása memóriában

Most jön a szórakoztató rész: létrehozunk egy `ZipArchive`‑t, amely egy másik `MemoryStream`‑ben él. Ez lehetővé teszi, hogy **create zip from memory** anélkül, hogy valaha is a fájlrendszert érintenénk.

```csharp
    // Step 4 – Build the ZIP archive in memory
    using (MemoryStream zipMemoryStream = new MemoryStream())
    using (var zipArchive = new ZipArchive(zipMemoryStream, ZipArchiveMode.Create, leaveOpen: true))
    {
        // 4a – Add the main HTML file
        var htmlEntry = zipArchive.CreateEntry("index.html");
        using (var entryStream = htmlEntry.Open())
        {
            // Reset the position of the HTML stream before copying
            htmlMemoryStream.Position = 0;
            htmlMemoryStream.CopyTo(entryStream);
        }

        // 4b – Add each resource that the handler captured
        // The handler stored each resource in a fresh MemoryStream, which we can enumerate.
        // For demonstration, assume we kept a list of those streams (you could store them in a dictionary).
        // Example placeholder – replace with your actual collection:
        // foreach (var kvp in capturedResources)
        // {
        //     var resourceEntry = zipArchive.CreateEntry(kvp.Key); // kvp.Key = relative path
        //     using var entry = resourceEntry.Open();
        //     kvp.Value.Position = 0;
        //     kvp.Value.CopyTo(entry);
        // }

        // When we’re done, flush everything
        zipArchive.Dispose(); // optional because of using, but makes intent clear
    }

    // At this stage zipMemoryStream holds the complete ZIP file.
    // You can return it, write it to a response stream, or save it to disk if you wish.
}
```

> **Megjegyzés:** A kikommentált rész azt mutatja, hogyan gyűjtheted össze a streameket a `MemoryResourceHandler`‑ben. Egy éles környezetben minden `MemoryStream`‑et egy szótárban tárolnál, amelynek kulcsa az eredeti erőforrás URL, majd itt iterálva adod hozzá őket az archívumhoz.

**Miért tartsuk a ZIP‑et memóriában?**  
Az archívum `MemoryStream`‑ben való tárolása lehetővé teszi, hogy egyszerűen elküldd közvetlenül egy HTTP kliensnek (`FileResult` az ASP.NET Core‑ban) vagy feltöltsd felhő tárolóba köztes fájl nélkül.

## 5. lépés: (Opcionális) A ZIP mentése lemezre

Ha még mindig szükséged van egy fizikai fájlra – esetleg hibakereséshez – egyszerűen írd a `zipMemoryStream`‑et a lemezre:

```csharp
// Optional: write the in‑memory ZIP to a file for inspection
File.WriteAllBytes("YOUR_DIRECTORY/output.zip", zipMemoryStream.ToArray());
```

## Teljes működő példa

Mindent összevonva, itt egy egyetlen, másolás‑beillesztésre kész program, amely **converts HTML to a ZIP archive** teljesen memóriában.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class MemoryResourceHandler : ResourceHandler
{
    // Capture each resource in a dictionary for later retrieval
    public static readonly System.Collections.Generic.Dictionary<string, MemoryStream> Captured = new();

    public override Stream HandleResource(Resource resource)
    {
        var ms = new MemoryStream();
        // Store the stream using the resource's absolute URL as the key
        Captured[resource.Uri.AbsoluteUri] = ms;
        return ms;
    }
}

class Program
{
    static void Main()
    {
        // Load the HTML file
        HtmlDocument doc = new HtmlDocument("YOUR_DIRECTORY/input.html");

        // Attach the custom handler
        var handler = new MemoryResourceHandler();

        // Save HTML + resources to memory
        using var htmlStream = new MemoryStream();
        doc.Save(htmlStream, new HtmlSaveOptions { OutputStorage = handler });

        // Create the ZIP archive in memory
        using var zipStream = new MemoryStream();
        using (var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, true))
        {
            // Add the HTML file
            var htmlEntry = zip.CreateEntry("index.html");
            using (var entry = htmlEntry.Open())
            {
                htmlStream.Position = 0;
                htmlStream.CopyTo(entry);
            }

            // Add each captured resource
            foreach (var kvp in MemoryResourceHandler.Captured)
            {
                // Derive a sane relative path from the URL
                var uri = new Uri(kvp.Key);
                var relativePath = uri.AbsolutePath.TrimStart('/');
                var resEntry = zip.CreateEntry(relativePath);
                using var entry = resEntry.Open();
                kvp.Value.Position = 0;
                kvp.Value.CopyTo(entry);
            }
        }

        // The ZIP is ready – write it out or return it from a web API
        File.WriteAllBytes("YOUR_DIRECTORY/output.zip", zipStream.ToArray());

        Console.WriteLine("HTML successfully packaged into output.zip");
    }
}
```

### Várható eredmény

A program futtatása létrehozza az `output.zip` fájlt, amely a következőket tartalmazza:

- `index.html` – az átírt HTML, amely a csomagolt erőforrásokra mutat.  
- Az összes kép, CSS és JavaScript fájl, amelyet az eredeti oldal hivatkozott, az eredeti relatív útvonalakon tárolva.

Nyisd meg a `index.html`‑t a ZIP‑ből bármely böngészőben, és a lap pontosan úgy jelenik meg, ahogy a fájlrendszeren volt.

## Gyakori kérdések és szélhelyzetek

| Kérdés | Válasz |
|----------|--------|
| **Mi van, ha egy erőforrás hatalmas (pl. egy videó)?** | Mivel minden memóriaalapon működik, a nagyon nagy fájlok `OutOfMemoryException`-t okozhatnak. Ebben az esetben közvetlenül streamelj egy ideiglenes fájlba, vagy korlátozd a elfogadott méretet. |
| **Kell kezelnem a duplikált erőforrás‑URL‑eket?** | A handler szótára felülírja a duplikátumokat. Ha csak egy példányt szeretnél megtartani, ellenőrizd a `Captured.ContainsKey`‑t a hozzáadás előtt. |
| **Használhatom ezt egy ASP.NET Core controllerben?** | Természetesen. Egy akciómetódusból térj vissza a `File(zipStream.ToArray(), "application/zip", "page.zip")` értékkel. |
| **Mi van a HTTPS erőforrásokkal?** | Az Aspose.HTML automatikusan letölti őket, amíg a futtatókörnyezet megbízik az SSL tanúsítványban. Önaláírt tanúsítványok esetén állítsd be a `ServicePointManager.ServerCertificateValidationCallback`‑t. |
| **A custom handler szálbiztos?** | A példa egy statikus szótárat használ, amely *nem* szálbiztos. Ha sok dokumentumot szeretnél párhuzamosan feldolgozni, csomagold a hozzáféréseket lock‑ba vagy használj `ConcurrentDictionary`‑t. |

## Pro tippek a produkciós használathoz

- **Reuse the handler** csak egyetlen dokumentumhoz; kérésenként hozz létre egy új példányt, hogy elkerüld a felhasználók közötti átfedéseket.  
- **Dispose streams** gyorsan. Bár a `using` blokkok a legtöbb esetet kezelik, a szótárban tárolt streameket a ZIP felépítése után el kell dobni.  
- **Validate the HTML** a feldolgozás előtt, hogy elkapd a hibás markupot, amely miatt a handler váratlan erőforrásokat kérhet.  
- **Compress aggressively** úgy, hogy beállítod a `ZipArchiveEntry.CompressionLevel = CompressionLevel.Optimal` értéket, ha a fájlméret számít.  

## Összegzés

Mindezt lefedtük, ami szükséges ahhoz, hogy **custom resource handler**-rel végigmenj egy HTML oldalon, elkapd minden hivatkozott eszközt, és **create zip from memory** anélkül, hogy a lemezt érintenéd. A bemutatott minta elég rugalmas web‑szolgáltatási helyzetekhez, háttérfeladatokhoz vagy akár asztali segédprogramokhoz, amelyeknek önálló HTML csomagra van szükségük.

Próbáld ki – cseréld le a `YOUR_DIRECTORY/input.html`‑t bármelyik oldalra, módosítsd a handlert, hogy a erőforrásokat egy `ConcurrentDictionary`‑ben tárolja, és egy robusztus, memóriában működő HTML‑to‑ZIP csővezetéket kapsz, amely készen áll a produkcióra.

---

*Készen állsz a következő szintre?* Ezután fedezd fel, hogyan **convert HTML to PDF** az Aspose.HTML‑del, vagy kísérletezz a ZIP titkosításával a biztonság növelése érdekében. A határ a csillagos ég, ha elsajátítod a memóriában történő streaminget C#‑ban. Boldog kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}