---
category: general
date: 2026-02-22
description: Az egyéni erőforráskezelő lehetővé teszi a HTML‑kimenet rögzítését. Ismerje
  meg, hogyan töltsön be HTML‑dokumentumot, használja az Aspose HTML mentést, és mentse
  a HTML‑t adatfolyamba egy egyszerű C# példával.
draft: false
keywords:
- custom resource handler
- load html document
- aspose html save
- save html to stream
- capture html output
language: hu
og_description: Ismerje meg, hogyan rögzít egy egyedi erőforráskezelő HTML kimenetet,
  tölt be HTML dokumentumot, és menti a HTML-t adatfolyamba az Aspose HTML C#-ban.
og_title: Egyéni erőforráskezelő az Aspose HTML-ben – Útmutató a stream-be mentéshez
tags:
- aspose-html
- csharp
- streaming
- resource-handler
title: Egyéni erőforráskezelő az Aspose HTML-ben – Útmutató a streambe mentéshez
url: /hu/net/advanced-features/custom-resource-handler-in-aspose-html-save-to-stream-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Egyéni erőforráskezelő – HTML kimenet rögzítése az Aspose HTML-lel

Volt már szükséged **custom resource handler**‑re, hogy elkapja minden fájlt, amelyet az Aspose HTML egy konverzió során ír? Lehet, hogy a HTML‑t, képeket vagy CSS‑t közvetlenül a memóriába szeretnéd irányítani a lemez helyett. Ez egy nagyon gyakori helyzet, amikor web‑szolgáltatást építesz, amelynek állapotmentesnek kell maradnia, vagy egyszerűen csak **HTML mentése stream‑be** szeretnéd későbbi feldolgozáshoz.

> **Miért fontos?**  
> HTML kimenet memóriában való rögzítése lehetővé teszi a fájlrendszeri I/O elkerülését, csökkenti a felhőfüggvények késleltetését, és teljes irányítást ad a névadás, tömörítés vagy akár a futás közbeni átalakítások felett.

---

## Amire szükséged lesz

- **.NET 6** vagy újabb (a kód .NET Framework 4.7+‑on is működik).  
- **Aspose.HTML for .NET** NuGet csomag (`Aspose.Html`).  
- Egy egyszerű HTML fájl (`input.html`), amelyet egy hivatkozható mappában helyezel el.  
- Bármelyik kedvenc IDE – Visual Studio, Rider vagy VS Code C# kiegészítőkkel.

Nem szükséges extra konfiguráció; az API elvégzi a nehéz munkát.

## 1. lépés – Egyéni erőforráskezelő létrehozása

Ennek a technikának a lényege a `Aspose.Html.Rendering.ResourceHandler` alosztályozása. A `HandleResource` felülírásával döntheted el, **hova** kerül minden erőforrás‑stream. A mi esetünkben minden kéréshez egy új `MemoryStream`‑et adunk vissza, ami azt jelenti, hogy minden CSS, kép vagy al‑HTML töredék csak a RAM‑ban él.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

/// <summary>
/// Custom handler that writes every resource to a new MemoryStream.
/// </summary>
class MemoryStreamHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // The ResourceInfo gives you the original URL and MIME type.
        // You could inspect it here to decide whether to skip certain files.
        // For this tutorial we just allocate a fresh stream.
        return new MemoryStream();
    }
}
```

**Pro tipp:** Ha nyomon kell követned a stream‑eket (pl. később ZIP archívumba szeretnéd őket írni), tárold őket egy `Dictionary<string, MemoryStream>`‑ben, amelynek kulcsa a `resourceInfo.Uri`.

## 2. lépés – HTML dokumentum betöltése

Mielőtt bármit mentenél, **be kell töltened a HTML dokumentumot** egy `HTMLDocument` példányba. Az Aspose HTML olvashat fájlútvonalról, URL‑ről vagy akár karakterláncról is. Itt egyszerűség kedvéért egy helyi fájlt használunk.

```csharp
// Adjust the path to point at your real HTML file.
string htmlPath = Path.Combine(Environment.CurrentDirectory, "input.html");

// Load the source HTML document.
HTMLDocument htmlDocument = new HTMLDocument(htmlPath);
```

Ha a HTML külső erőforrásokra (képek, betűkészletek stb.) hivatkozik, győződj meg róla, hogy az alap‑URI helyes; különben a kezelő nem fogja megtalálni őket.

## 3. lépés – Egyéni kezelő példányosítása

Most létrehozzuk a korábban definiált kezelő egy példányát. Semmi bonyolult – egyszerűen egy `new`. Ez az objektum a következő lépésben a `Save` metódusnak lesz átadva.

```csharp
// Step 3: Instantiate the custom handler.
MemoryStreamHandler resourceHandler = new MemoryStreamHandler();
```

Mivel a kezelő csak a memóriában létezik, nem kell aggódnod a fájlengedélyek vagy a lemez tisztítása miatt.

## 4. lépés – Dokumentum mentése az Aspose HTML Save‑el

A **Aspose HTML save** művelet egy `ResourceHandler`‑t fogad. Ahogy a motor végigjárja a DOM‑ot és feloldja az egyes hivatkozott erőforrásokat, meghívja a `HandleResource`‑t. A mi megvalósításunk egy `MemoryStream`‑et ad vissza, így minden részlet a RAM‑ban landol.

```csharp
// Step 4: Save the document.
// The handler's HandleResource method will be invoked for each output stream.
htmlDocument.Save(resourceHandler);
```

Ekkor a konverzió befejeződött, de a stream‑ek még a memóriában vannak. Most már olvashatod őket, adatbázisba írhatod, vagy egy API válaszban visszaküldheted.

## 5. lépés – Rögzített stream‑ek lekérése és ellenőrzése

Mivel minden alkalommal egy új `MemoryStream`‑et adtunk vissza, szükség van egy módra, hogy megőrizzük a hivatkozásokat. Az alábbiakban egy gyors kiterjesztést láthatsz a korábbi kezelőhöz, amely minden stream‑et egy szótárban tárol, így a mentés után is megvizsgálhatod őket.

```csharp
class TrackingMemoryStreamHandler : ResourceHandler
{
    public Dictionary<string, MemoryStream> Streams { get; } = new();

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var ms = new MemoryStream();
        Streams[resourceInfo.Uri] = ms;   // Remember the stream by its URI.
        return ms;
    }
}

// Usage:
var trackingHandler = new TrackingMemoryStreamHandler();
htmlDocument.Save(trackingHandler);

// Example: write the main HTML output to console (as text)
if (trackingHandler.Streams.TryGetValue(htmlPath, out var mainStream))
{
    mainStream.Position = 0; // rewind
    using var reader = new StreamReader(mainStream);
    string html = reader.ReadToEnd();
    Console.WriteLine("=== Rendered HTML ===");
    Console.WriteLine(html);
}
```

A kód futtatása kiírja az Aspose által generált végső HTML‑t, ezzel megerősítve, hogy a **capture html output** a várt módon működik.

## Szélhelyzetek és gyakori kérdések

### 1. Mi van, ha a dokumentum hatalmas?

A memóriahasználat gyorsan nőhet. Nagy PDF‑ek vagy sok nagy felbontású képet tartalmazó HTML esetén érdemes közvetlenül egy `FileStream`‑be vagy egy **pufferelt hálózati stream**‑be streamelni a `MemoryStream` helyett. A kezelő dönthet a `resourceInfo.MimeType` alapján.

### 2. Szükséges-e a stream‑ek felszabadítása?

**Igen.** Miután befejezted a feldolgozást, hívd meg a `Dispose()`‑t minden `MemoryStream`‑en (vagy egy `using` blokk végezze el). A nyomonkövető példában hozzáadhatnánk:

```csharp
foreach (var ms in trackingHandler.Streams.Values)
    ms.Dispose();
```

### 3. Át tudom-e nevezni az erőforrásokat mentés előtt?

Természetesen. A `HandleResource`‑ben hozzáférsz a `resourceInfo.Uri`‑hoz. Átírhatod, előtagot adhatod hozzá, vagy akár bizonyos fájlokat kihagyhatsz úgy, hogy `null`‑t adsz vissza.

```csharp
if (resourceInfo.MimeType.StartsWith("image/"))
    return null; // Skip images completely.
```

### 4. Szálbiztonság kérdése

Egyetlen kezelőpéldányt **nem** szabad megosztani párhuzamos `Save` hívások között. Minden konverzióhoz hozz létre egy új kezelőt, vagy ha újra kell használni, védd a belső szótárat egy lock‑kal.

## Teljes működő példa

Az alábbiakban a teljes program látható, amelyet beilleszthetsz egy konzolos alkalmazásba. Bemutatja az egészet – a HTML fájl betöltésétől a rögzített kimenet kiírásáig.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering;

class TrackingMemoryStreamHandler : ResourceHandler
{
    public Dictionary<string, MemoryStream> Streams { get; } = new();

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var ms = new MemoryStream();
        Streams[resourceInfo.Uri] = ms;
        return ms;
    }
}

class SaveToStreamTutorial
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the HTML document you want to render.
        // -------------------------------------------------
        string htmlPath = Path.Combine(Environment.CurrentDirectory, "input.html");
        if (!File.Exists(htmlPath))
        {
            Console.WriteLine($"Cannot find {htmlPath}");
            return;
        }

        HTMLDocument htmlDocument = new HTMLDocument(htmlPath);

        // -------------------------------------------------
        // Step 2: Create the custom handler that captures streams.
        // -------------------------------------------------
        var handler = new TrackingMemoryStreamHandler();

        // -------------------------------------------------
        // Step 3: Save the document – Aspose will invoke our handler.
        // -------------------------------------------------
        htmlDocument.Save(handler);

        // -------------------------------------------------
        // Step 4: Retrieve the main HTML output and display it.
        // -------------------------------------------------
        if (handler.Streams.TryGetValue(htmlPath, out var mainStream))
        {
            mainStream.Position = 0; // rewind to start
            using var reader = new StreamReader(mainStream);
            string renderedHtml = reader.ReadToEnd();
            Console.WriteLine("=== Rendered HTML Output ===");
            Console.WriteLine(renderedHtml);
        }
        else
        {
            Console.WriteLine("Main HTML stream not found.");
        }

        // -------------------------------------------------
        // Step 5: Clean up.
        // -------------------------------------------------
        foreach (var ms in handler.Streams.Values)
            ms.Dispose();

        Console.WriteLine("All streams disposed. Done.");
    }
}
```

**Várható kimenet:** A konzol kiírja a teljesen renderelt HTML‑t (beleértve minden beágyazott CSS‑t, amelyet az Aspose generált), majd egy megerősítést, hogy minden stream fel lett szabadítva.

## Következtetés

Most megtanultad, hogyan valósíts meg egy **custom resource handler**‑t az Aspose HTML‑ben, **tölts be egy HTML dokumentumot**, és **mentsd a HTML‑t stream‑be**, miközben **rögzíted a HTML kimenetet** további feldolgozáshoz. A minta könnyű, szál‑tudatos és teljesen kiterjeszthető – néhány sor kóddal kicserélheted a `MemoryStream`‑et egy fájlra, hálózati socketre vagy felhő tároló API‑ra.

Ezután érdemes lehet felfedezni:

- **ZIP archívumba mentés** (tökéletes HTML, CSS és képek csomagolásához).  
- **Átalakítások alkalmazása** (pl. CSS minifikálás futás közben).  
- **Közvetlen streamelés HTTP válaszba** az ASP.NET Core‑ban az azonnali letöltéshez.

Próbáld ki ezeket, és meglátod, milyen erőteljes egy testreszabott **custom resource handler** a valós helyzetekben. Boldog kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}