---
category: general
date: 2026-04-01
description: Az egyéni erőforráskezelő megkönnyíti az URL zip-fájlba konvertálását.
  Kövesse ezt az útmutatót a weboldal zip letöltéséhez, a HTML-ből zip létrehozásához,
  és a HTML zip mentéséhez az Aspose.HTML segítségével.
draft: false
keywords:
- custom resource handler
- convert url to zip
- download webpage zip
- create zip from html
- save html zip
language: hu
og_description: Az egyéni erőforráskezelő egyszerűvé teszi az URL zip-fájlba konvertálását.
  Tanulja meg, hogyan tölthet le weboldal zip-et, és hogyan mentheti el a HTML zip-et
  az Aspose.HTML segítségével.
og_title: egyedi erőforráskezelő – Weboldal ZIP-be konvertálása C#-ban
tags:
- Aspose.HTML
- C#
- ZIP archive
- Web scraping
title: egyedi erőforráskezelő – Weboldal ZIP-be konvertálása C#-ban
url: /hu/net/html-extensions-and-conversions/custom-resource-handler-convert-webpage-to-zip-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# egyéni erőforráskezelő – Weboldal konvertálása ZIP-be C#-ban

Valaha szükséged volt már **custom resource handler**-re, hogy egy élő oldalt lekérj és minden eszközt egyetlen ZIP fájlba helyezz? Igen, ez egy olyan helyzet, amellyel sokan szembesülünk, amikor egy marketing landing oldalt szeretnénk archiválni vagy egy súgó cikk offline másolatát szállítani. A jó hír? Az Aspose.HTML‑vel **convert URL to zip**-t néhány C# sorral megvalósíthatsz – nincs szükség külső eszközökre, nincs kézi zip‑elés.

Ebben az útmutatóban végigvezetünk a teljes folyamaton: egy távoli URL betöltése, egy `ResourceHandler` bekötése, amely minden erőforrást közvetlenül egy ZIP bejegyzésbe streamel, és végül az eredmény mentése, így egy kész **download webpage zip** csomagot kapsz. A végére képes leszel **create zip from html**-t készíteni menet közben, és **save html zip** fájlokat bárhol elmenteni.

## Amire szükséged lesz

- .NET 6+ (a kód működik .NET Core‑on és .NET Framework‑ön is)
- Aspose.HTML for .NET NuGet csomag (`Aspose.HTML`)
- Alapvető ismeretek a C# streamekkel és a `System.IO.Compression` névtérrel kapcsolatban
- Egy IDE vagy szerkesztő a választásod szerint (Visual Studio, VS Code, Rider…)

Ennyi—nincs extra könyvtár, nincs bonyolult parancssori manőver. Ha megvan a fenti, akkor készen állsz.

## egyéni erőforráskezelő – Áttekintés

Az Aspose.HTML-ben a *resource handler* egy hurok, amely minden alkalommal meghívódik, amikor a motornak egy függő fájlt (CSS, képek, betűtípusok stb.) kell írnia. A `ResourceHandler` alosztályozásával teljes irányítást kapsz arról, *hol* és *hogyan* kerülnek tárolásra ezek a bájtok. A mi esetünkben egy `ZipArchive`‑ba irányítjuk őket, minden URI útvonalhoz külön bejegyzést létrehozva.

Miért érdemes egyedi kezelőt használni az alapértelmezett fájlrendszer helyett? Két fő ok:

1. **Atomicity** – minden ugyanabban az archívumban landol, így soha nem maradnak elhagyott fájlok.
2. **Flexibility** – közvetlenül streamelhetsz memóriába, hálózati megosztásra, vagy akár felhő bucketbe anélkül, hogy a lemezt érintenéd.

Most, hogy a „miért” világos, merüljünk el a **how** részben.

## 1. lépés: A projekt előkészítése és az Aspose.HTML telepítése

Nyisd meg a terminált, és hozz létre egy új konzolos alkalmazást (később nyugodtan adaptálhatod ASP.NET‑re vagy háttérszolgáltatásra).

```bash
dotnet new console -n WebPageToZipDemo
cd WebPageToZipDemo
dotnet add package Aspose.HTML
```

Láthatod, hogy megjelenik egy `Program.cs` fájl. Később lecseréljük a tartalmát a teljes példára, de először adjuk hozzá a szükséges `using` direktívákat a fájl tetejéhez:

```csharp
using Aspose.Html;
using Aspose.Html.Saving;
using System.IO;
using System.IO.Compression;
```

Ez minden szükséges csővezeték.

## 2. lépés: ZipResourceHandler implementálása (convert url to zip)

Itt van a megoldás szíve – egy osztály, amely a `ResourceHandler`‑ből származik. Minden eszközhöz kap egy `ResourceInfo` objektumot, és egy `Stream`‑et ad vissza, amely közvetlenül egy ZIP bejegyzésbe ír.

```csharp
// Step 2: Define a custom resource handler that writes each resource into a ZIP entry
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;

    // The handler receives a ready‑made ZipArchive (opened in Create mode)
    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo info)
    {
        // Build a safe entry name – strip leading '/' to avoid root folder creation
        var entryName = info.Uri.AbsolutePath.TrimStart('/');
        // Ensure the entry name is not empty (happens for the main HTML document)
        if (string.IsNullOrWhiteSpace(entryName))
            entryName = "index.html";

        // Create the entry; if it already exists, replace it
        var entry = _zip.CreateEntry(entryName, CompressionLevel.Optimal);
        // Return the stream that writes directly into the ZIP entry
        return entry.Open();
    }
}
```

**Mi történik?**  
- `info.Uri` adja meg a forrás pontos URL‑jét (pl. `/styles/main.css`).  
- Ebből tiszta fájlnevet készítünk az archívumban.  
- `entry.Open()` egy írható streamet ad vissza, amelyet az Aspose.HTML a forrás bájtjaival tölt fel.

> **Pro tipp:** Ha meg kell őrizned az almappákat, tartsd meg a teljes útvonalat (pl. `assets/images/logo.png`). A fenti kód már ezt megteszi, mivel nem távolítjuk el a köztes könyvtárakat.

## 3. lépés: HTML dokumentum betöltése (convert url to zip)

Most megkérjük az Aspose.HTML‑t, hogy lekérjen egy oldalt. Lehet távoli URL, helyi fájl, vagy akár nyers HTML szöveg. A bemutatóhoz egy nyilvános oldalt használunk:

```csharp
// Step 3: Load the HTML document from a URL
var document = new Document("https://example.com");
```

Ha az oldal hitelesítést vagy egyedi fejléceket igényel, átadhatsz egy `Request` objektumot – csak ne feledd, hogy a resource handler továbbra is minden hivatkozott fájlt rögzít.

## 4. lépés: ZIP archívum létrehozása (download webpage zip)

Megnyitunk egy `FileStream`‑et a kimeneti ZIP‑hez, és egy `ZipArchive`‑ba csomagoljuk. A `leaveOpen: true` beállítás lehetővé teszi, hogy az Aspose.HTML később bezárja a streamet anélkül, hogy előre eldobná az alatta lévő fájlkezelőt.

```csharp
// Step 4: Create a ZIP archive that will hold the document and its resources
using var zipStream = new FileStream("output.zip", FileMode.Create, FileAccess.Write);
using var zipArchive = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: true);
```

Nyugodtan módosítsd az útvonalat a saját mappádra (`YOUR_DIRECTORY/output.zip`). Az archívum a beérkező erőforrásokkal valós időben jön létre.

## 5. lépés: A handler csatlakoztatása a HtmlSaveOptions-hez (save html zip)

Most megmondjuk az Aspose.HTML‑nek, hogy a dokumentum mentésekor a saját `ZipResourceHandler`‑ünket használja. Az `OutputStorage` tulajdonság egy `ResourceHandler` példányt vár.

```csharp
// Step 5: Configure HTML save options to use the custom ZIP resource handler
var htmlSaveOptions = new HtmlSaveOptions
{
    // The handler will receive each resource and write it into the ZIP
    OutputStorage = new ZipResourceHandler(zipArchive)
};

// Save the document – this triggers the handler for every linked asset
document.Save(htmlSaveOptions);
```

Amikor a `Save` befejeződik, az Aspose.HTML a következőket írja:

- `index.html` (a fő oldal)
- Minden CSS fájl (`styles/*.css`)
- Képek (`images/*.png`, `*.jpg`, stb.)
- Betűtípusok és minden egyéb hivatkozott erőforrás

Ezek mind külön bejegyzésként kerülnek az `output.zip`‑be.

## 6. lépés: Az eredmény ellenőrzése (expected output)

Miután a `using` blokkok kilépnek, a ZIP fájl bezáródik és készen áll a felhasználásra. Nyisd meg bármely archívumkezelővel, és egy hasonló szerkezetet kell látnod:

```
output.zip
│   index.html
│
├── css
│   └── main.css
│
├── images
│   ├── logo.png
│   └── banner.jpg
│
└── fonts
    └── open-sans.woff2
```

Ha kicsomagolod a `index.html`‑t és helyben megnyitod, az oldal pontosan úgy jelenik meg, mint az élő webhely – köszönhetően a csomagolt eszközöknek. Ez a **download webpage zip**, amit kerestél.

## Opcionális: A ZIP közvetlen streamelése egy kliensnek (create zip from html on the fly)

Néha nem szeretnél fizikai fájlt a lemezen; előfordulhat, hogy HTTP‑n keresztül szolgálod ki az archívumot. Ugyanaz a handler működik egy `MemoryStream`‑nel:

```csharp
using var memoryZip = new MemoryStream();
using (var zipArchive = new ZipArchive(memoryZip, ZipArchiveMode.Create, leaveOpen: true))
{
    var options = new HtmlSaveOptions
    {
        OutputStorage = new ZipResourceHandler(zipArchive)
    };
    document.Save(options);
}

// Reset the stream position before sending it
memoryZip.Position = 0;

// Example: ASP.NET Core controller returning the ZIP
// return File(memoryZip, "application/zip", "page.zip");
```

Ez a kódrészlet bemutatja, hogyan **create zip from html**-t készíthetsz anélkül, hogy a fájlrendszert érintenéd – tökéletes felhő‑natív mikroszolgáltatásokhoz.

## Gyakori buktatók és hogyan kerüld el őket

| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| Üres bejegyzések jelennek meg | `info.Uri.AbsolutePath` `/`-t ad vissza a fő dokumentumhoz | Győződj meg róla, hogy üres útvonal esetén `"index.html"`-re visszaesel (lásd a fenti kódot) |
| Duplikált fájlnevek | Két erőforrás ugyanazt a fájlnevet használja, de különböző mappákban | A bejegyzés neve létrehozásakor őrizd meg a teljes relatív útvonalat |
| Nagy oldalak memória nyomást okoznak | `MemoryStream` használata korlátlan mérettel | Nagy oldalak esetén streamelj közvetlenül egy fájlba (`FileStream`) |
| Hiányzó betűtípusok | A betűtípus URL-ek gyakran abszolútak és CDN domainre mutatnak | A handler bármely URL-t kezel; csak győződj meg róla, hogy a webhely engedélyezi a betűtípus fájlok letöltését |

## Teljes működő példa (Minden lépés egyben)

Az alábbiakban a teljes, másolás‑beillesztésre kész program látható. Megjegyzéseket tartalmaz minden logikai blokkhoz, így egyszerűen beillesztheted a `Program.cs`‑be és futtathatod.

```csharp
using Aspose.Html;
using Aspose.Html.Saving;
using System;
using System.IO;
using System.IO.Compression;

class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;
    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo info)
    {
        var entryName = info.Uri.AbsolutePath.TrimStart('/');
        if (string.IsNullOrWhiteSpace(entryName))
            entryName = "index.html";

        var entry = _zip.CreateEntry(entryName, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Load the remote page (convert url to zip)
        var document = new Document("https://example.com");

        // 2️⃣ Prepare the ZIP file (download webpage zip)
        using var zipStream = new FileStream("output.zip", FileMode.Create, FileAccess.Write);
        using var zipArchive = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: true);

        // 3️⃣ Wire the custom handler (save html zip)
        var saveOptions = new HtmlSaveOptions
        {
            OutputStorage = new ZipResourceHandler(zipArchive)
        };

        // 4️⃣ Save – Aspose.HTML streams each resource into the archive
        document.Save(saveOptions);

        Console.WriteLine("✅ ZIP archive created at: output.zip");
    }
}
```

Futtasd a `dotnet run` paranccsal. Néhány másodperc után a projekt mappájában megjelenik az `output.zip`, készen áll a megosztásra vagy tárolásra.

## Összegzés

Most bemutattuk, hogyan alakíthat egy **custom resource handler** bármely élő URL-t egy rendezett ZIP csomaggá – lényegében egy **download webpage zip** segédeszközt, amely néhány C# sorból áll. A megközelítés

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}