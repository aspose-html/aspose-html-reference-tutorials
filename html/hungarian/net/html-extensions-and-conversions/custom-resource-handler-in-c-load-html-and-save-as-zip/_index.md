---
category: general
date: 2026-03-15
description: Az egyéni erőforráskezelő lehetővé teszi, hogy HTML-t töltsön be URL-ről,
  és HTML-t ZIP-ként mentse. Tanulja meg, hogyan konvertálja a weboldalt ZIP-be, és
  töltse le a HTML-t erőforrásokkal néhány perc alatt.
draft: false
keywords:
- custom resource handler
- load html from url
- save html as zip
- convert webpage to zip
- download html with resources
language: hu
og_description: Az egyéni erőforráskezelő lehetővé teszi, hogy HTML-t töltsön be URL-ről,
  a weboldalt ZIP-fájlba konvertálja, és HTML-t erőforrásokkal együtt töltsön le.
  Teljes lépésről‑lépésre útmutató.
og_title: Egyéni erőforráskezelő C#-ban – HTML betöltése és ZIP-be mentése
tags:
- Aspose.Html
- C#
- Web Scraping
title: Egyéni erőforráskezelő C#-ban – HTML betöltése és ZIP-ként mentése
url: /hu/net/html-extensions-and-conversions/custom-resource-handler-in-c-load-html-and-save-as-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Egyedi erőforráskezelő – HTML betöltése URL‑ről és HTML mentése ZIP‑ként

Szükséged volt már **custom resource handler**‑re, hogy egy élő oldalt lekérj, minden képet, szkriptet és stíluslapot elments, majd az egészet egy rendezett ZIP‑fájlban szállítsd? Nem vagy egyedül. Sok automatizálási projektben – gondolj offline olvasókra, archiváló eszközökre vagy tesztkészletekre – **load HTML from URL**‑t szeretnél, minden külső erőforrást rögzíteni, majd **save HTML as ZIP**‑t anélkül, hogy a lemezhez nyúlnál.  

Ebben az útmutatóban pontosan ezt fogjuk végigjárni: az Aspose.HTML for .NET használatával **custom resource handler**‑t létrehozni, egy távoli oldalt lekérni, és **convert webpage to ZIP**‑t végrehajtani, hogy később **download HTML with resources**‑t tudj letölteni. Nincs felesleges részlet, csak egy működő megoldás, amit beilleszthetsz a Visual Studio‑ba és ma futtathatsz.

## Amire szükséged lesz

- .NET 6 SDK vagy újabb (az API működik .NET Core‑on és .NET Framework‑ön is)  
- Aspose.HTML for .NET NuGet csomag (`Aspose.HTML`) – telepítés: `dotnet add package Aspose.HTML`  
- Alap C# ismeretek – a kódot úgy tartjuk egyszerűnek, hogy a kezdők is értsék  
- Internetkapcsolat a cél‑URL‑hez (például `https://example.com`)  

Ennyi. Ha már van projekted, csak illeszd be a kódot; egyébként hozz létre egy konzolos alkalmazást a `dotnet new console` paranccsal.

## 1. lépés: A custom resource handler szerepének megértése

Mielőtt kódot írnánk, tisztázzuk, **miért** fontos egy egyedi kezelő. Az Aspose.HTML igény szerint tölti be a külső erőforrásokat (képek, CSS, JS). Alapértelmezés szerint közvetlenül a lemezre streameli őket, ami lassú lehet, és ideiglenes fájlokat hagy maga után. Egy **custom resource handler** minden kérést elfog, egy `Stream`‑et ad, amelybe írhatod, és eldöntheted, hogy az adatot memóriában tartod, átalakítod vagy teljesen eldobod.

Gondolj a kezelőre úgy, mint egy közvetítőre, amely azt mondja: „Hé, szükségem van arra a képre – itt egy vödör; töltsd fel, és add vissza, amikor kész vagy.” Minden alkalommal egy új `MemoryStream`‑et visszaadva mindent a RAM‑ban tartunk, így később egyszerűen zip‑elhetjük őket.

## 2. lépés: A custom resource handler megvalósítása

Az alábbiakban a teljes osztálydefiníció látható. Figyeld meg a `HandleResource` `override`‑ját, amely egy `ResourceInfo` objektumot kap, amely leírja a kért erőforrást (URL, MIME‑típus stb.). Egyszerűen egy új `MemoryStream`‑et adunk vissza. Valós környezetben esetleg `info`‑t vizsgálnád, hogy kiszűrd a hirdetéseket vagy nagy videókat, de a **download HTML with resources** demóhoz egyszerűen tartjuk.

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using Aspose.Html.Rendering.Image;
using System.IO;

/// <summary>
/// Captures every external resource (images, CSS, scripts) in memory.
/// </summary>
class MyHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info)
    {
        // Returning a fresh MemoryStream keeps the resource data in memory.
        // Aspose.HTML will write the incoming bytes into this stream.
        return new MemoryStream();
    }
}
```

> **Pro tipp:** Ha valaha memóriakihasználtságot kell korlátozni, a `MemoryStream`‑et egy egyedi stream‑be csomagolhatod, amely méretkorlátot kényszerít.

## 3. lépés: HTML betöltése URL‑ről a kezelő használatával

Most létrehozunk egy `HTMLDocument`‑et, amely a távoli címre mutat. A konstruktor automatikusan elkezdi lekérni az oldalt, és köszönhetően a mi kezelőnknek, minden hivatkozott erőforrás az általunk most beállított memóriabeli stream‑ekhez kerül.

```csharp
using Aspose.Html;
using System;

// Step 3: Load the HTML document you want to process.
var url = "https://example.com"; // <-- replace with your target page
var htmlDocument = new HTMLDocument(url);
```

Ha az URL elérhetetlen, az Aspose.HTML kivételt dob – ezért érdemes `try/catch`‑be csomagolni a termelési kódban. A rövidség kedvéért itt kihagyjuk.

## 4. lépés: A csomagolt HTML (vagy ZIP) mentése egy Memory Stream‑be

Miután a dokumentum teljesen betöltődött, meghívjuk a `Save`‑et. Ha átadjuk a `MyHandler` példányt, az Aspose.HTML tudja, hogy a későbbi mentési műveleteknél ugyanazokat a memóriabeli stream‑eket használja. A használt `Save` overload egy **packed HTML** formátumot ír, amely lényegében egy ZIP archívum, amely a fő `.html` fájlt és az összegyűjtött erőforrásokat tartalmazza.

```csharp
using System.IO;

// Step 4: Save the entire document, including its resources, into a memory stream.
using (var packedHtmlStream = new MemoryStream())
{
    // The handler is optional here because the document already captured resources,
    // but passing it again ensures consistency if you later switch to a different save mode.
    htmlDocument.Save(packedHtmlStream, new MyHandler());

    // At this point `packedHtmlStream` holds the packed HTML (ZIP format).
    // You can write it to disk, send it over a network, or keep it in memory.
    
    // Example: write to a file for verification
    File.WriteAllBytes("packed_page.zip", packedHtmlStream.ToArray());
    Console.WriteLine($"Saved packed HTML as ZIP – size: {packedHtmlStream.Length / 1024} KB");
}
```

**Ami látnod kell:** A program futtatása után egy `packed_page.zip` fájl jelenik meg a projekt mappádban. Nyisd meg, és megtalálod az `index.html`‑t, valamint egy eszközkönyvtárat (`images/`, `css/`, stb.). Ez a **convert webpage to zip** működésének eredménye.

## 5. lépés: A kimenet ellenőrzése – Valóban tartalmazza az összes erőforrást?

Egy gyors ellenőrzés segít megbizonyosodni arról, hogy a kezelő elvégezte a munkáját. A ZIP bejegyzéseit felsorolva ellenőrizheted, hogy minden külső fájl benne van-e.

```csharp
using System.IO.Compression;

// Verify contents
using (var zip = new ZipArchive(new MemoryStream(File.ReadAllBytes("packed_page.zip")), ZipArchiveMode.Read))
{
    Console.WriteLine("ZIP contains the following entries:");
    foreach (var entry in zip.Entries)
    {
        Console.WriteLine($"- {entry.FullName} ({entry.Length / 1024} KB)");
    }
}
```

Ha hiányzó képeket vagy CSS‑fájlokat találsz, ellenőrizd újra az eredeti oldal hálózati kéréseit. Néha az erőforrások JavaScript‑ből töltődnek be a kezdeti HTML‑elemzés után; az Aspose.HTML csak a markup‑ban közvetlenül hivatkozott erőforrásokat rögzíti. Az ilyen dinamikus esetekhez headless böngésző megközelítésre lenne szükség, ami meghaladja ennek a **custom resource handler** útmutatónak a keretét.

## Gyakori kérdések és szélhelyzetek

### Mi van, ha a ZIP‑nak egyedi nevet szeretnék adni a belépő HTML fájlnak?

Adj át egy `SaveOptions` objektumot `HtmlSaveOptions`‑szel, és állítsd be a `DocumentFileName`‑t. Példa:

```csharp
var options = new HtmlSaveOptions { DocumentFileName = "myPage.html" };
htmlDocument.Save(packedHtmlStream, options, new MyHandler());
```

### Korlátozhatom, hogy mely erőforrások legyenek mentve?

Természetesen. A `HandleResource`‑ben vizsgáld meg az `info.SourceUrl`‑t vagy az `info.MimeType`‑t. Adj vissza `null`‑t azoknak az erőforrásoknak, amelyeket ki szeretnél hagyni (pl. nagy videófájlok). Az Aspose.HTML egyszerűen figyelmen kívül hagyja őket.

### Biztonságos-e mindent memóriában tartani nagy oldalak esetén?

Közepes méretű oldalak (néhány megabájt) esetén ez rendben van. Ha több megabájtnyi erőforrást vársz, fontold meg a közvetlen streamelést egy ideiglenes fájlba vagy egy korlátozott puffert, hogy elkerüld a `OutOfMemoryException`‑t.

## Teljes működő példa

Összegezve, itt egy egyetlen fájl, amelyet beilleszthetsz egy új konzolos projektbe:

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using System;
using System.IO;
using System.IO.Compression;

class MyHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info)
    {
        return new MemoryStream(); // Keep each resource in memory
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Load the remote page
        var url = "https://example.com"; // change as needed
        var htmlDocument = new HTMLDocument(url);

        // 2️⃣ Prepare a memory stream for the packed output
        using (var packedHtmlStream = new MemoryStream())
        {
            // 3️⃣ Save as a ZIP (packed HTML) using our custom handler
            htmlDocument.Save(packedHtmlStream, new MyHandler());

            // 4️⃣ Persist to disk for inspection (optional)
            File.WriteAllBytes("packed_page.zip", packedHtmlStream.ToArray());
            Console.WriteLine($"Saved ZIP – {packedHtmlStream.Length / 1024} KB");
        }

        // 5️⃣ Quick verification of ZIP contents
        using (var zip = new ZipArchive(File.OpenRead("packed_page.zip"), ZipArchiveMode.Read))
        {
            Console.WriteLine("ZIP entries:");
            foreach (var entry in zip.Entries)
                Console.WriteLine($"- {entry.FullName}");
        }
    }
}
```

Futtasd a `dotnet run` parancsot, és kapsz egy `packed_page.zip` fájlt, amely az egész oldalt tartalmazza. Ez a teljes **download HTML with resources** munkafolyamat.

## Összegzés

Most bemutattuk, hogyan lehet egy **custom resource handler** a kulcs a **load HTML from URL**‑hez, minden hivatkozott eszköz rögzítéséhez, és a **save HTML as ZIP**‑hez – hatékonyan **convert webpage to ZIP** offline fogyasztásra. A megközelítés könnyű, memóriában marad, és teljes irányítást ad arról, hogy mely erőforrások maradjanak meg.

Következő lépések? Próbáld meg a `MemoryStream`‑et fájl‑alapú stream‑re cserélni, hogy nagyobb oldalakat kezelj, vagy kísérletezz a `HtmlSaveOptions`‑szel a kimeneti elrendezés testreszabásához. Érdemes megvizsgálni az Aspose.HTML PDF konverziós képességeit is, ha valaha **download HTML with resources**-t PDF‑ként szeretnéd, a ZIP helyett.

Boldog kódolást, és legyenek a archiváid mindig rendezettek!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}