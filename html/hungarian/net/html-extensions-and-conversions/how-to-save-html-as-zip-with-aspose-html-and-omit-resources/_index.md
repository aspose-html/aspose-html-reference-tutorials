---
category: general
date: 2026-10-21
description: Ismerje meg, hogyan menthet HTML-t ZIP-fájlba az Aspose.HTML használatával,
  hogyan konvertálhatja a HTML-t ZIP-be, és hogyan szűrheti ki az erőforrásokat egy
  tiszta csomag érdekében.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save html as zip
- convert html to zip
- how to omit resources
- how to strip resources
- create html zip
language: hu
lastmod: 2026-10-21
og_description: Mentse a HTML-t ZIP-ként az Aspose.HTML segítségével, tanulja meg,
  hogyan konvertálhatja a HTML-t ZIP-re, és hogyan szűrheti ki az erőforrásokat egy
  könnyű archívumhoz.
og_image_alt: Screenshot showing the save html as zip process with resources omitted
og_title: HTML mentése ZIP-be az Aspose.HTML segítségével – erőforrások kihagyása
  egy lépésben
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to save HTML as ZIP using Aspose.HTML, convert HTML to ZIP,
    and strip resources for a clean package.
  headline: How to save HTML as ZIP with Aspose.HTML and omit resources
  type: TechArticle
tags:
- Aspose.HTML
- C#
- ZIP archive
- HTML conversion
- Resource handling
title: HTML mentése ZIP-ként az Aspose.HTML használatával, erőforrások kihagyásával
url: /hu/net/html-extensions-and-conversions/how-to-save-html-as-zip-with-aspose-html-and-omit-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan mentse el a HTML-t ZIP-ként az Aspose.HTML segítségével, és hagyja ki az erőforrásokat

Ha **HTML-t szeretne ZIP-ként menteni**, miközben eltávolítja a külső fájlokat, ez az útmutató egy teljes, azonnal futtatható megoldást mutat be. A tutorial végére képes lesz **HTML-t ZIP-re konvertálni**, szabályozni, mely erőforrások maradnak meg, és egy tiszta archívumot előállítani, amely csak a lényegi markup-ot tartalmazza.

Sok web‑automatizálási forgatókönyv megköveteli egy oldal csomagolását offline használatra, e‑mail mellékletként vagy archiválásra. A képek, betűkészletek vagy szkriptek belefoglalása gyakran feleslegesen megnöveli az archívum méretét. Az alábbi lépések bemutatják, **hogyan hagyjuk ki az erőforrásokat** és **hogyan szűrjük le az erőforrásokat** a kimenetből, így a kapott ZIP könnyű marad.

## Prerequisites

Mielőtt elkezdené, győződjön meg róla, hogy rendelkezik:

- .NET 6.0 vagy újabb telepítve  
- Aspose.HTML for .NET licenccel (vagy ingyenes értékelő verzióval)  
- Alap C# fejlesztői környezettel (Visual Studio, VS Code vagy Rider)  

A `Aspose.Html`‑n kívül nincs szükség további NuGet csomagokra.

## Step 1: Create a custom resource handler

A **hogyan hagyjuk ki az erőforrásokat** kérdés központja egy `ResourceHandler` alosztály. Az Aspose.HTML minden külső eszköz (képek, CSS, szkriptek) esetén meghívja ezt a kezelőt. Egy üres stream visszaadása hatékonyan azt mondja a konvertálónak, hogy hagyja ki az adott eszközt.

```csharp
using System.IO;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Prevents external resources from being written to the output package.
/// </summary>
class CustomResourceHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info)
    {
        // Returning an empty MemoryStream strips the resource from the ZIP.
        return new MemoryStream();
    }
}
```

**Miért fontos:** Az alapértelmezett viselkedés minden hivatkozott fájlt bemásol a ZIP-be, ami akár duplázhatja vagy megháromszorozhatja a fájlméretet. A `HandleResource` felülírásával finomhangolt vezérlést kap anélkül, hogy módosítaná az eredeti HTML-t.

## Step 2: Load the HTML document

Töltse be a forrásfájlt a `HTMLDocument`‑del. A konstruktor elfogad fájlútvonalat, URL‑t vagy streamet. Ebben a példában egy helyi `input.html` nevű fájlt olvasunk be.

```csharp
// Load the source HTML file from the local file system.
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

Ha a HTML memóriában van, vagy egy webkérésből származik, helyette átadhat egy `MemoryStream`‑et vagy egy URL‑stringet. Az API ugyanúgy működik.

## Step 3: Configure the save options

Hozzon létre egy `HtmlSaveOptions` példányt, és állítsa be az 1. lépésben létrehozott egyéni kezelőt. Ez azt mondja az Aspose.HTML‑nek, hogy minden erőforrás esetén használja a kezelőt.

```csharp
// Prepare save options and attach the custom resource handler.
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // The ResourceHandler property is what enables resource stripping.
    ResourceHandler = new CustomResourceHandler()
};
```

Itt további beállításokat is módosíthat, például `CompressImages = false`‑t, ha meg akarja tartani a képadatokat, de továbbra is ki szeretné hagyni a többi eszközt. A példában az alapértelmezett tömörítési beállítások maradnak.

## Step 4: Save the document as a ZIP archive

Végül hívja meg a `Save`‑t a célúttal és a konfigurált beállításokkal. A kimeneti fájl egy `.zip` lesz, amely tartalmazza az `index.html`‑t (vagy az eredeti fájlnevet) és **semilyen külső erőforrást** nem tartalmaz.

```csharp
// Save the HTML document as a ZIP file. The archive will contain only the HTML markup.
document.Save("YOUR_DIRECTORY/output.zip", saveOptions);
```

### Expected result

- `output.zip` → egyetlen `index.html` fájlt tartalmaz.  
- Minden kép, CSS‑fájl és JavaScript‑hivatkozás ki van hagyva, mivel az egyéni kezelő minden esetben üres streamet adott vissza.  

Az archívumot bármely ZIP‑nézővel ellenőrizheti. A HTML oldal továbbra is az eredeti URL‑kre hivatkozik, de ezek a fájlok nincsenek jelen az archívumban, így a csomag minimális marad.

## Full, runnable example

Az alábbi teljes programot másolja, illessze be és futtassa. Cserélje le a `YOUR_DIRECTORY`‑t egy valós mappára a gépén.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Converters;

class Program
{
    static void Main()
    {
        // Step 1: Define a custom resource handler to control how external resources are saved.
        class CustomResourceHandler : ResourceHandler
        {
            public override Stream HandleResource(ResourceInfo info)
            {
                // Returning an empty stream strips the resource from the ZIP output.
                return new MemoryStream();
            }
        }

        // Step 2: Load an HTML document from a file.
        string inputPath = "YOUR_DIRECTORY/input.html";
        HTMLDocument document = new HTMLDocument(inputPath);

        // Step 3: Create HTML save options and assign the custom handler.
        HtmlSaveOptions saveOptions = new HtmlSaveOptions
        {
            ResourceHandler = new CustomResourceHandler()
        };

        // Step 4: Save the document as a ZIP archive containing the HTML and (now omitted) resources.
        string outputPath = "YOUR_DIRECTORY/output.zip";
        document.Save(outputPath, saveOptions);

        Console.WriteLine($"HTML has been saved as ZIP at: {outputPath}");
    }
}
```

A program futtatása előállítja a korábban leírt ZIP‑fájlt. Most már terjesztheti a HTML‑oldalt anélkül, hogy felesleges eszközöket csomagolna bele.

## Common variations and edge cases

| Scenario | Adjustment |
|----------|------------|
| **Keep images but drop CSS/JS** | A `CustomResourceHandler`‑ben vizsgálja meg az `info.MimeType` értékét. Csak `text/css` és `application/javascript` esetén adjon vissza `MemoryStream`‑et. |
| **Preserve external fonts** | A `font/woff2` MIME‑típusoknál adja vissza az eredeti streamet, egyébként üres streamet. |
| **Generate a ZIP with a custom entry name** | Használja a `HtmlSaveOptions` `Save(string path, SaveOptions options, string entryName)` túlterhelését, hogy másik gyökérfájlnév legyen. |
| **Convert multiple HTML files into a single ZIP** | Iteráljon a fájlokon, minden egyeshez hozzon létre külön `HTMLDocument`‑et, majd adja hozzá ugyanahhoz a `ZipArchive`‑hez a `System.IO.Compression` segítségével. |

Ezek a variációk bemutatják, **hogyan szűrhet le erőforrásokat** szelektíven, teljes kontrollt biztosítva a végső archívum mérete felett.

## Pro tips

- **Validate the result**: Mentés után nyissa meg a ZIP‑et, és töltse be az `index.html`‑t egy böngészőben. A hiányzó erőforrások törött linkként fognak megjelenni, ami megerősíti, hogy a kezelő működött.  
- **Performance**: Egy üres `MemoryStream` visszaadása olcsó, de ha több ezer eszköz van, fontolja meg a döntés gyorsítótárazását (pl. egy `HashSet<string>` a kihagyandó MIME‑típusokhoz).  
- **Licensing**: Az Aspose.HTML ingyenes értékelő verziója vízjel‑kommentet helyez el a HTML‑ben. A licencelt verzió eltávolítja ezt a megjegyzést a termelésben.

## Conclusion

Most már tudja, hogyan **mentse el a HTML-t ZIP‑ként**, **konvertálja a HTML-t ZIP‑re**, és **szűrje le az erőforrásokat** az Aspose.HTML for .NET segítségével. Egy egyéni `ResourceHandler` megvalósításával kihagyhatja a nem kívánt fájlokat, és könnyű archívumot hozhat létre. Kísérletezzen a kezelő logikájával, hogy csak a valóban szükséges erőforrásokat tartsa meg, és építse be ezt a mintát nagyobb automatizálási folyamatokba.

---

**Next steps**

- Fedezze fel a `HtmlSaveOptions` további funkcióit, például az `EmbedImages`‑t, amely közvetlenül a HTML‑be ágyazza be a képeket.  
- Kombinálja ezt a megközelítést az `Aspose.PDF`‑vel, hogy a ZIP létrehozása után ugyanazt a HTML‑t PDF‑vé konvertálja.  
- Tekintse át a szerver‑oldali forgatókönyveket, ahol a ZIP‑et kérésre generálja, és közvetlenül a kliensnek streameli lemezre írás nélkül.  

Boldog kódolást!


## What Should You Learn Next?

A következő tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljesen működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [How to Use ZipArchive – Save HTML and Resources to a ZIP File](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [How to Save HTML in C# – Custom Resource Handlers & ZIP](/html/english/net/working-with-html-documents/how-to-save-html-in-c-custom-resource-handlers-zip/)
- [How to Save HTML as ZIP in C# – Complete Aspose.HTML Guide](/html/english/net/html-extensions-and-conversions/how-to-save-html-as-zip-in-c-complete-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}