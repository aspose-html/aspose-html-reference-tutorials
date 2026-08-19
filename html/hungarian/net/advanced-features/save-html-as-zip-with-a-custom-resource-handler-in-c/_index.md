---
category: general
date: 2026-08-19
description: HTML mentése ZIP formátumban C#‑ban az Aspose.HTML és egy egyéni erőforráskezelő
  használatával. Kövesse ezt a lépésről‑lépésre útmutatót az erőforrások beágyazásához
  és egy hordozható archívum létrehozásához.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save HTML as ZIP
- custom resource handler
- Aspose.HTML C#
- HTML archive generation
- resource streaming C#
language: hu
lastmod: 2026-08-19
og_description: HTML mentése ZIP-ként C#-ban az Aspose.HTML és egy egyéni erőforráskezelő
  használatával. Ez az útmutató bemutatja a teljes kódot, elmagyarázza, miért fontos
  minden lépés, és kitér a gyakori buktatókra.
og_image_alt: Screenshot of C# code that saves an HTML document as a ZIP archive
og_title: HTML mentése ZIP-fájlba egy egyedi erőforráskezelővel C#-ban – teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-08-19'
  description: Save HTML as ZIP in C# using Aspose.HTML and a custom resource handler.
    Follow this step‑by‑step guide to embed resources and generate a portable archive.
  headline: Save HTML as ZIP with a custom resource handler in C#
  type: TechArticle
- description: Save HTML as ZIP in C# using Aspose.HTML and a custom resource handler.
    Follow this step‑by‑step guide to embed resources and generate a portable archive.
  name: Save HTML as ZIP with a custom resource handler in C#
  steps:
  - name: Saving to a specific folder inside the ZIP
    text: 'If you want all resources to reside under a subfolder (e.g., `assets/`),
      modify the handler to prepend the folder name to each file name:'
  - name: Streaming directly to a network location
    text: 'When the ZIP must be sent over HTTP without touching the local file system,
      use a `MemoryStream` for the final archive:'
  - name: Handling large resources
    text: 'Large images or videos can exhaust memory if you keep everything in `MemoryStream`.
      Switch to a file‑based stream inside the handler:'
  - name: Preserving original URLs
    text: 'Aspose.HTML rewrites the `src`/`href` attributes to point to the new locations
      inside the ZIP. If you need to keep the original URLs for later processing,
      capture them before saving:'
  type: HowTo
tags:
- C#
- Aspose.HTML
- ZIP archive
- resource handling
title: HTML mentése ZIP-be egy egyéni erőforráskezelővel C#-ban
url: /hu/net/advanced-features/save-html-as-zip-with-a-custom-resource-handler-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML mentése ZIP-be egy egyedi erőforráskezelővel C#-ban

Ha **HTML-t ZIP-be kell menteni**, miközben szabályozni szeretné, hogyan tárolódnak a hivatkozott erőforrások, ez az útmutató teljes megoldást nyújt. Megtanulja, hogyan hozhat létre egy egyedi erőforráskezelőt, hogyan konfigurálja az Aspose.HTML mentési beállításait, és hogyan generál egy hordozható ZIP-archívumot, amely tartalmazza a HTML-fájlt és annak eszközeit.

A megfelelő erőforrásbeágyazás akkor fontos, ha önálló weboldalt szeretne szállítani, jelentést archivál compliance célból, vagy egy offline használatra szánt pillanatfelvételt szeretne gyorsítótárazni. Az alábbi lépések az Aspose.HTML 23.10 vagy újabb verzióval működnek, és csak egy .NET fejlesztői környezetet igényelnek.

## Mit fog építeni

A tutorial végére a következőkkel fog rendelkezni:

* Egy C# osztály, amely megvalósítja a `ResourceHandler`‑t, és minden erőforráshoz streamet ad vissza.
* Kód, amely betölti a meglévő HTML-fájlt a lemezről.
* `HTMLSaveOptions` konfiguráció az egyedi kezelő használatához.
* Egy hívás a `HTMLDocument.Save`‑ra, amely létrehozza a `output.zip`‑et, egy ZIP-archívumot, amely tartalmazza a HTML-dokumentumot és az összes hivatkozott erőforrást.

## Előfeltételek

* .NET 6.0 SDK vagy újabb (a példa .NET Framework 4.7.2‑n is fut).
* Visual Studio 2022 vagy bármely IDE, amely támogatja a C# projekteket.
* Aspose.HTML for .NET NuGet csomag (`Aspose.Html`).
* Egy HTML-fájl (`example.html`) legalább egy külső erőforrással (kép, CSS, script), hogy lássa a kezelő működését.

## 1. lépés: Egyedi erőforráskezelő létrehozása

Az **egyedi erőforráskezelő** határozza meg, hová kerül minden külső eszköz. A `ResourceHandler` megvalósítása teljes irányítást ad a kimeneti stream felett.

```csharp
using Aspose.Html;
using System.IO;

/// <summary>
/// Provides a stream for each resource referenced by the HTML document.
/// </summary>
class MyResourceHandler : ResourceHandler
{
    /// <summary>
    /// Returns a writable stream for the given resource.
    /// </summary>
    /// <param name="resource">Metadata about the resource being saved.</param>
    /// <returns>A stream that Aspose.HTML will write the resource to.</returns>
    public override Stream HandleResource(Resource resource)
    {
        // Create a memory stream for the resource.
        // In production you might write to a file on disk, a cloud blob, or a database.
        return new MemoryStream();
    }
}
```

**Miért fontos:**  
A `HandleResource` minden külső fájlhoz (képek, stíluslapok, szkriptek) meghívásra kerül. Egy új `MemoryStream` visszaadásával az Aspose.HTML a memóriában gyűjti az adatokat, amelyet a mentési rutin később a ZIP-archívumba csomagol. Ha a erőforrásokat lemezen szeretné tárolni, cserélje a `new MemoryStream()`‑t `File.Create(Path.Combine(outputFolder, resource.FileName))`‑re.

## 2. lépés: A HTML-dokumentum betöltése

Töltse be a forrásfájlt a `HTMLDocument`‑del. A konstruktor elfogad fájlútvonalat, URL‑t vagy streamet.

```csharp
using Aspose.Html;

// Adjust the path to point to your HTML file.
string htmlPath = Path.Combine("YOUR_DIRECTORY", "example.html");

// Load the document into memory.
HTMLDocument doc = new HTMLDocument(htmlPath);
```

**Miért fontos:**  
A dokumentum előzetes betöltése biztosítja, hogy az Aspose.HTML elemezze a DOM‑ot és felfedezze az összes hivatkozott erőforrást. A könyvtár ezután minden felderített erőforrást átad a korábban definiált kezelőnek.

## 3. lépés: Mentési beállítások konfigurálása az egyedi kezelővel

A `HTMLSaveOptions` lehetővé teszi a kimeneti formátum és az erőforráskezelő megadását.

```csharp
using Aspose.Html.Saving;

// Create default save options.
HTMLSaveOptions saveOptions = new HTMLSaveOptions();

// Attach the custom resource handler.
saveOptions.ResourceHandler = new MyResourceHandler();
```

**Miért fontos:**  
`ResourceHandler` megadása nélkül az Aspose.HTML a lemezen egy ideiglenes mappába írja az erőforrásokat, amit nem tud szabályozni. Az Ön `MyResourceHandler`‑jének csatolásával pontosan meghatározhatja, hogyan tárolódik minden erőforrás a ZIP-archívum létrehozása előtt.

## 4. lépés: A dokumentum mentése ZIP-archívumként

Végül hívja meg a `HTMLDocument.Save`‑t a `SaveFormat.Zip`‑el. A metódus tömöríti a HTML-fájlt és az összes, a kezelő által biztosított streamet.

```csharp
// Define the output ZIP path.
string zipPath = Path.Combine("YOUR_DIRECTORY", "output.zip");

// Save the document as a ZIP archive.
doc.Save(zipPath, SaveFormat.Zip, saveOptions);
```

A hívás befejezése után a `output.zip` a következőket tartalmazza:

* `example.html` – az eredeti HTML-fájl frissített erőforráshivatkozásokkal.
* Az összes külső eszköz (képek, CSS, JS) különálló bejegyzésként, mindegyiket az egyedi kezelő hozta létre.

## Az eredmény ellenőrzése

Nyissa meg a generált ZIP-et bármely archívum‑böngészővel. Egy hasonló mappaszerkezetet kell látnia:

```
output.zip
│─ example.html
│─ images/
│   └─ logo.png
│─ styles/
│   └─ main.css
│─ scripts/
│   └─ app.js
```

Nyissa meg a kicsomagolt mappában lévő `example.html`‑t egy böngészőben; az oldalnak pontosan úgy kell megjelenítenie, mint az eredeti, ami azt igazolja, hogy az erőforrások helyesen lettek beágyazva.

## Gyakori variációk és szélhelyzetek

### Mentés egy adott mappába a ZIP-en belül

Ha minden erőforrást egy almappában (pl. `assets/`) szeretne elhelyezni, módosítsa a kezelőt úgy, hogy a fájlnév elé előtagként hozzáadja a mappa nevét:

```csharp
public override Stream HandleResource(Resource resource)
{
    string folder = "assets";
    string entryName = Path.Combine(folder, resource.FileName);
    // Aspose.HTML uses the entry name when packing the ZIP.
    resource.FileName = entryName;
    return new MemoryStream();
}
```

### Közvetlen streaming hálózati helyre

Amikor a ZIP-et HTTP‑n keresztül kell elküldeni anélkül, hogy a helyi fájlrendszert érintené, használjon `MemoryStream`‑et a végleges archívumhoz:

```csharp
using (var zipStream = new MemoryStream())
{
    doc.Save(zipStream, SaveFormat.Zip, saveOptions);
    zipStream.Position = 0; // Reset for reading.
    // Send zipStream to a web API, store in Azure Blob, etc.
}
```

### Nagy erőforrások kezelése

Nagy képek vagy videók kimeríthetik a memóriát, ha mindent `MemoryStream`‑ben tart. Váltson fájl‑alapú streamre a kezelőben:

```csharp
public override Stream HandleResource(Resource resource)
{
    string tempPath = Path.GetTempFileName();
    return new FileStream(tempPath, FileMode.Create, FileAccess.Write);
}
```

A `doc.Save` befejezése után törölheti az ideiglenes fájlokat.

### Eredeti URL-ek megőrzése

Az Aspose.HTML átírja a `src`/`href` attribútumokat, hogy az új helyekre mutassanak a ZIP‑ben. Ha a későbbi feldolgozáshoz meg kell tartania az eredeti URL‑eket, mentse el őket a mentés előtt:

```csharp
foreach (var img in doc.Images)
{
    Console.WriteLine($"Original src: {img.Source}");
}
```

## Profi tippek

* **A kezelő újrahasználata** – Hozzon létre egyetlen `MyResourceHandler` példányt, és használja újra több mentésnél, hogy elkerülje az ismételt allokációt.
* **Erőforrások validálása** – A `HandleResource`‑ben ellenőrizheti a `resource.MimeType`‑ot vagy a `resource.FileName`‑t, hogy kiszűrje a nem kívánt fájlokat (pl. analitikai szkriptek kihagyása).
* **Tömörítési szint beállítása** – A `HTMLSaveOptions` tartalmazza a `CompressionLevel`‑t (0–9). A magasabb értékek kisebb ZIP‑et eredményeznek, de több CPU‑időt igényelnek.

## Teljes, futtatható példa

Az alábbi programot másolja be egy új konzolos projektbe (`dotnet new console`). Bemutatja a teljes folyamatot a HTML-fájl betöltésétől a `output.zip` előállításáig.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Saving;

class MyResourceHandler : ResourceHandler
{
    public override Stream HandleResource(Resource resource)
    {
        // Return a memory stream for each resource.
        // Replace with FileStream if you need disk persistence.
        return new MemoryStream();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Define paths.
        string baseDir = Path.Combine(Environment.CurrentDirectory, "YOUR_DIRECTORY");
        string htmlPath = Path.Combine(baseDir, "example.html");
        string zipPath = Path.Combine(baseDir, "output.zip");

        // 2️⃣ Load the HTML document.
        HTMLDocument doc = new HTMLDocument(htmlPath);

        // 3️⃣ Configure save options with the custom handler.
        HTMLSaveOptions saveOptions = new HTMLSaveOptions
        {
            ResourceHandler = new MyResourceHandler()
        };

        // 4️⃣ Save as a ZIP archive.
        doc.Save(zipPath, SaveFormat.Zip, saveOptions);

        Console.WriteLine($"HTML saved as ZIP at: {zipPath}");
    }
}
```

**Várt kimenet**

```
HTML saved as ZIP at: C:\path\to\YOUR_DIRECTORY\output.zip
```

Csomagolja ki a ZIP-et, hogy ellenőrizze a korábban leírt szerkezetet.

## Következtetés

Most már tudja, hogyan **mentse HTML-t ZIP-be** az Aspose.HTML for .NET segítségével, miközben egy **egyedi erőforráskezelő** segítségével szabályozza, hová kerül minden eszköz. Ez a megközelítés teljes rugalmasságot biztosít az erőforrások tárolásában, lehetővé teszi a memóriában történő feldolgozást, és könnyen integrálható felhő- vagy helyi munkafolyamatokba.

Innen tovább:

* Bővítse a kezelőt, hogy az erőforrásokat Azure Blob Storage‑ba írja (másodlagos kulcsszó: custom resource handler).
* Kombinálja a ZIP-et digitális aláírással a biztonságos dokumentumszállításhoz.
* Használja a `HTMLSaveOptions`‑t más formátumok (pl. MHTML) generálásához, miközben továbbra is programozottan kezeli az erőforrásokat.

Kísérletezzen különböző stream‑típusokkal, tömörítési szintekkel és mappaszerkezetekkel, hogy megfeleljen projektje követelményeinek. Boldog kódolást!

## Mit érdemes még megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Custom Resource Handler in C# – Convert HTML to ZIP Tutorial](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [How to Render HTML – Complete Guide with Custom Resource Handler](/html/english/net/rendering-html-documents/how-to-render-html-complete-guide-with-custom-resource-handl/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}