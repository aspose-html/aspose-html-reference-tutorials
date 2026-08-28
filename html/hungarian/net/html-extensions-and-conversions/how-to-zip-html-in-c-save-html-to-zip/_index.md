---
category: general
date: 2025-12-29
description: Hogyan csomagoljunk be HTML-t C#-ban gyorsan az Aspose.HTML használatával
  – mentse a HTML-t zip-be egy egyedi ZipResourceHandler-rel. Tanulja meg lépésről
  lépésre.
draft: false
keywords:
- how to zip html
- save html to zip
- create zip archive c#
- Aspose HTML zip
- C# resource handling
language: hu
og_description: Hogyan lehet gyorsan zip-olni a HTML-t C#-ban az Aspose.HTML használatával.
  Kövesse ezt az útmutatót, hogy HTML-t zip-fájlba mentse, és egyedi erőforráskezeléssel
  zip-archívumot hozzon létre.
og_title: HTML ZIP-elése C#‑ban – HTML mentése ZIP‑be
tags:
- C#
- Aspose.HTML
- ZipArchive
- File I/O
title: HTML zipelése C#‑ban – HTML mentése ZIP‑be
url: /hu/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan csomagoljuk be a HTML-t ZIP-be C#‑ban – HTML mentése ZIP-be

A HTML ZIP‑be csomagolása C#‑ban gyakori igény, ha weboldalakat szeretnénk offline használatra csomagolni. Akár egyetlen oldalt és annak képeit, akár egy teljes webhelyet exportálunk, az **HTML ZIP‑be mentése** minden fájlt rendezett és hordozható formában tart. Ebben az útmutatóban egy teljes, azonnal futtatható megoldáson keresztül vezetünk végig, amely nemcsak a HTML‑markupt csomagolja be, hanem minden hivatkozott erőforrást közvetlenül az archívumba stream‑eli.

Megtanulod, hogyan:

* Programozottan hozhatsz létre ZIP‑archívumot a .NET `System.IO.Compression` segítségével.
* Egy egyedi `ResourceHandler`‑t integrálhatsz az Aspose.HTML‑be, hogy az erőforrások közvetlenül a ZIP‑be kerüljenek.
* Kezelheted az olyan speciális eseteket, mint a már létező ZIP‑fájlok vagy nagy bináris eszközök.

Nincs szükség külső eszközökre – csak C#, Aspose.HTML és néhány kódsor.

## Amire szükséged lesz

Mielőtt belevágnánk, győződj meg róla, hogy rendelkezel:

* **.NET 6+** (a kód .NET Framework 4.6.2‑n és újabb verziókon is működik).
* **Aspose.HTML for .NET** – letöltheted a próba verziót az Aspose weboldaláról, vagy használhatsz licencelt példányt.
* Fejlesztői környezet (Visual Studio, VS Code, Rider – bármelyik, amit kedvelsz).

Ennyi. Nincs szükség további NuGet csomagokra a `System.IO.Compression` (a .NET‑hez tartozik) és az `Aspose.HTML` mellett.

## 1. lépés: Projekt létrehozása és importok

Hozz létre egy új konzolos projektet (vagy illeszd be a kódot egy meglévőbe). Add hozzá a szükséges `using` direktívákat a fájl tetejéhez:

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;
```

> **Pro tipp:** Ha Visual Studio‑t használsz, az IDE felajánlja a hiányzó NuGet csomag (`Aspose.Html`) hozzáadását. Fogadd el, és már indulhat a munka.

## 2. lépés: Egyedi ZipResourceHandler megvalósítása

Az Aspose.HTML minden alkalommal meghív egy `ResourceHandler`‑t, amikor erőforrást (például képet, CSS‑fájlt vagy szkriptet) kell írnia. A `HandleResource` felülírásával pontosan meghatározhatjuk, hová kerül az adott erőforrás. Az alábbi handler egy ZIP‑bejegyzést hoz létre, amely tükrözi az erőforrás logikai útvonalát, majd egy írható streamet ad vissza, amely közvetlenül arra a bejegyzésre mutat.

```csharp
/// <summary>
/// Streams each HTML resource straight into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;

    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // Ensure the entry's directory structure exists inside the zip.
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        // The returned stream writes directly into the zip entry.
        return entry.Open();
    }
}
```

**Miért fontos:**  
Ahelyett, hogy az erőforrásokat egy ideiglenes mappába írnánk, majd azt zip‑elnénk, ez a handler a repülőben stream‑eli az adatokat, csökkentve a lemez‑I/O‑t és az memóriahasználatot. Emellett garantálja, hogy a ZIP belső mappaszerkezete megegyezzen a HTML relatív útvonalaival, amit a böngészők elvárnak a kicsomagolt oldal megnyitásakor.

## 3. lépés: A ZIP‑archívum előkészítése

Most nyitjuk meg (vagy hozzuk létre) a cél‑ZIP‑fájlt. A `FileMode.Create` zászló felülír minden létező fájlt – tökéletes ismételhető build‑ekhez. Ha inkább meg szeretnéd őrizni a meglévő archívumot, válts `FileMode.OpenOrCreate`‑ra, és kezeld a duplikált bejegyzéseket ennek megfelelően.

```csharp
string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");

// Ensure the directory exists (useful if you run the code from a nested folder)
Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);

using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);
```

> **Speciális eset:** Ha a folyamat összeomlik a `using` blokk lezárása előtt, egy sérült ZIP‑fájl maradhat. A kódot try/catch‑ben futtatni, és hiba esetén a részben létrehozott fájlt törölni egyszerű védelmi megoldás.

## 4. lépés: HTML‑dokumentum építése beágyazott erőforrással

Demóként egy apró HTML‑oldalt hozunk létre, amely egy `image.png` nevű képet hivatkozik. Valódi környezetben a HTML‑t fájlból vagy adatbázisból származó stringből töltenéd be.

```csharp
// Sample HTML containing an <img> tag.
// Aspose.HTML will ask the ResourceHandler for "image.png".
string htmlContent = @"
<html>
<head><title>Sample Zip</title></head>
<body>
    <h1>Hello, zipped world!</h1>
    <img src='image.png' alt='Demo image'>
</body>
</html>";

// Create the document from the string.
var html = new HTMLDocument(htmlContent);
```

Ha a lemezen tényleges képfájlok vannak, manuálisan hozzáadhatod őket a ZIP‑hez a HTML mentése előtt, vagy hagyhatod, hogy az Aspose.HTML a handleren keresztül töltse le őket (például URL‑ről). A fent írt handler mind helyi útvonalakra, mind távoli URL‑ekre működik.

## 5. lépés: Mentési beállítások konfigurálása a ZipResourceHandler használatához

Most megmondjuk az Aspose.HTML‑nek, hogy a saját handlerünket használja az erőforrások írásakor. Az `HTMLSaveOptions` osztály lehetővé teszi, hogy megadd a ZIP‑en belüli kimeneti fájl nevét (alapértelmezés szerint `index.html`).

```csharp
var saveOptions = new HTMLSaveOptions
{
    // The HTML file itself will be saved as "index.html" inside the zip.
    OutputFileName = "index.html",
    // Plug in our handler so resources go straight into the archive.
    OutputStorage = new ZipResourceHandler(zip)
};
```

## 6. lépés: Dokumentum mentése – minden adat a ZIP‑be stream‑el

Végül meghívjuk a `Save` metódust. Az Aspose.HTML elemzi a markup‑ot, megtalálja a `<img>` tag-et, meghívja a `HandleResource`‑t az `image.png`‑hez, és a HTML‑fájlt valamint a képet egyaránt a ZIP‑archívumba írja.

```csharp
html.Save(saveOptions);
Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
```

Amikor a `using` blokkok kilépnek, a `ZipArchive` befejezi a fájl írását, így az készen áll a terjesztésre.

### Teljes működő példa

Az alábbiakban a teljes program látható egyben. Másold be a `Program.cs`‑be és futtasd – nincs szükség további módosításra.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;
    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare the zip file.
        string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");
        Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);
        using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
        using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);

        // 2️⃣ Build a simple HTML document with an image reference.
        string htmlContent = @"
        <html>
        <head><title>Sample Zip</title></head>
        <body>
            <h1>Hello, zipped world!</h1>
            <img src='image.png' alt='Demo image'>
        </body>
        </html>";
        var html = new HTMLDocument(htmlContent);

        // 3️⃣ Set save options to stream resources into the zip.
        var saveOptions = new HTMLSaveOptions
        {
            OutputFileName = "index.html",
            OutputStorage = new ZipResourceHandler(zip)
        };

        // 4️⃣ Save – everything ends up in output.zip.
        html.Save(saveOptions);
        Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
    }
}
```

**Várt eredmény:** A futtatás után az `output.zip` két bejegyzést tartalmaz:

```
index.html
image.png
```

Ha kicsomagolod a fájlt és megnyitod az `index.html`‑t egy böngészőben, a kép helyesen jelenik meg, mivel a relatív útvonal megmaradt.

## Gyakran feltett kérdések

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}