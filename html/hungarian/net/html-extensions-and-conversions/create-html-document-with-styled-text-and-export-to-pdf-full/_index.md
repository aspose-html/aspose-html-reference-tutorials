---
category: general
date: 2025-12-29
description: HTML dokumentum létrehozása C#-ban, és megtanulni, hogyan állítsuk be
  a betűcsaládot, a betűméretet, majd hogyan mentsük el az HTML-t PDF-ként, vagy hogyan
  konvertáljuk az HTML-t PDF-re az Aspose.HTML segítségével.
draft: false
keywords:
- create html document
- set font family
- set font size
- save html as pdf
- convert html to pdf
language: hu
og_description: HTML dokumentum létrehozása C#-ban, és azonnal megtekintheted, hogyan
  állítsd be a betűcsaládot, a betűméretet, majd mentheted a HTML-t PDF-ként, vagy
  konvertálhatod a HTML-t PDF-re az Aspose.HTML segítségével.
og_title: HTML dokumentum létrehozása – Formázott szöveg és PDF export
tags:
- aspnet
- csharp
- pdf-generation
title: HTML-dokumentum létrehozása stílusos szöveggel és exportálása PDF-be – Teljes
  útmutató
url: /hu/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML dokumentum létrehozása formázott szöveggel és exportálása PDF-be

Ever needed to **create HTML document** on the fly and turn it into a PDF without leaving your C# code? Maybe you’re building a reporting engine, an invoice generator, or just a quick‑look preview for users. The good news is you can do it in a few lines using Aspose.HTML, and you’ll get full control over font family, font size, and even bold‑italic styling.

In this tutorial we’ll walk through the entire process—from spinning up an in‑memory HTML document to saving it as a PDF file. By the end you’ll know exactly how to **set font family**, **set font size**, and **save HTML as PDF** (a.k.a. **convert HTML to PDF**) with a clean, production‑ready code sample.

## Amire szükséged lesz

- .NET 6+ (az API működik .NET Core‑ral és .NET Framework‑kel egyaránt)  
- Aspose.HTML for .NET NuGet csomag (`Aspose.Html`) – telepítés: `dotnet add package Aspose.Html`  
- Egy mappa a lemezen, ahová a generált PDF‑t írhatod  

![HTML dokumentum létrehozása illusztráció](/images/create-html-document.png){alt="HTML dokumentum létrehozása példa"}

## 1. lépés: HTML dokumentum létrehozása

Először egy üres HTML dokumentum objektumra van szükségünk. Tekintsd úgy, mint egy friss vászonra, ahol később a formázott bekezdést festheted.

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

// Step 1 – initialize a new HTML document in memory
HTMLDocument htmlDocument = new HTMLDocument();

// Grab a reference to the <body> element for later use
HTMLBodyElement body = htmlDocument.Body;
```

**Miért fontos:** A `HTMLDocument` egy DOM‑szerű struktúrát biztosít, amelyet programozottan manipulálhatsz. Nem kell nyers karakterláncokkal vagy fájl‑I/O‑val bajlódni a végéig.

## 2. lépés: Bekezdés hozzáadása és betűtípus-család és betűméret beállítása

Most létrehozunk egy `<p>` elemet, beillesztünk egy szöveget, és kifejezetten meghatározzuk a betűtípus-családot és a méretet. Itt jönnek képbe a **set font family** és **set font size** kulcsszavak.

```csharp
// Step 2 – create a <p> element with some sample text
HtmlElement paragraph = htmlDocument.CreateElement("p");
paragraph.InnerHtml = "Bold & Italic text";

// Define the base font style
paragraph.Style.FontFamily = "Arial";   // set font family
paragraph.Style.FontSize = "18px";      // set font size

// Attach the paragraph to the document body
body.AppendChild(paragraph);
```

**Pro tipp:** Ha web‑biztonságos tartalékot szeretnél, megadhatsz egy vesszővel elválasztott listát, például `"Arial, Helvetica, sans-serif"`; a böngésző (vagy az Aspose) az első elérhető betűtípust választja.

## 3. lépés: Félkövér és dőlt stílus alkalmazása WebFontStyle zászlókkal

Az Aspose.HTML egy praktikus `WebFontStyle` felsorolást biztosít, amely lehetővé teszi a stílusok bitwise OR‑ral való kombinálását. Tegyük a szöveget egyszerre félkövér **és** dőlt.

```csharp
// Step 3 – apply bold and italic using WebFontStyle flags
paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

**Mi történik a háttérben?** A `FontStyle` tulajdonság a CSS `font-weight` és `font-style` deklarációkra fordítódik. A zászlók OR‑olásával elkerüljük két külön CSS‑sor írását.

## 4. lépés: HTML konvertálása PDF‑be (HTML mentése PDF‑ként)

Az utolsó lépés a tényleges konvertálás. Egyetlen `Save` hívással az Aspose.HTML rendereli a DOM‑ot, és PDF fájlt ír a lemezre. Ez teljesíti mind a **save html as pdf**, mind a **convert html to pdf** követelményeket.

```csharp
// Step 4 – save the HTML document as a PDF file
string outputPath = @"C:\Temp\styled.pdf";
htmlDocument.Save(outputPath, new PDFSaveOptions());

// Optional: open the PDF automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Várt eredmény:** Nyisd meg a `styled.pdf` fájlt, és egyetlen bekezdést látsz, amely a “Bold & Italic text” szöveget 18‑px Arial betűtípussal, félkövér és dőlt formában jeleníti meg. A PDF méretei egy szabványos A4 lapnak felelnek meg, és a szöveg kiválasztható – a vektoralapú renderelésnek köszönhetően.

## Teljes működő példa

Mindent összevonva, itt a teljes, azonnal futtatható program:

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new HTML document
        HTMLDocument htmlDocument = new HTMLDocument();
        HTMLBodyElement body = htmlDocument.Body;

        // 2️⃣ Add a styled paragraph
        HtmlElement paragraph = htmlDocument.CreateElement("p");
        paragraph.InnerHtml = "Bold & Italic text";

        // Set font family and size
        paragraph.Style.FontFamily = "Arial";
        paragraph.Style.FontSize = "18px";

        // 3️⃣ Apply bold + italic
        paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // Append to body
        body.AppendChild(paragraph);

        // 4️⃣ Save as PDF (convert HTML to PDF)
        string outputFile = @"C:\Temp\styled.pdf";
        htmlDocument.Save(outputFile, new PDFSaveOptions());

        Console.WriteLine($"PDF generated at: {outputFile}");
    }
}
```

### A kód futtatása

1. Telepítsd az Aspose.HTML NuGet csomagot:  
   ```bash
   dotnet add package Aspose.Html
   ```
2. `C:\Temp\styled.pdf` helyettesítsd egy olyan mappával, amelybe írási jogosultsággal rendelkezel.  
3. Építsd és futtasd: `dotnet run`.  

## Gyakori kérdések és szélhelyzetek

- **Mi van, ha egyedi web‑fontot kell használnom?**  
  Töltsd be a betűtípust `HTMLFontFaceRule`‑nal, vagy hivatkozz egy távoli `@font-face` CSS fájlra a bekezdés létrehozása előtt.

- **Hozzáadhatok képeket a konvertálás előtt?**  
  Természetesen. Használd a `HTMLImageElement img = (HTMLImageElement)htmlDocument.CreateElement("img");` kódot, és állítsd be az `img.Source`‑t egy helyi útvonalra vagy data URI‑ra.

- **Mi a helyzet a többoldalas PDF‑ekkel?**  
  Adj hozzá további elemeket (táblázatok, div‑ek stb.), és az Aspose.HTML automatikusan oldaltörést végez, ha a tartalom meghaladja az oldal magasságát.

- **Van mód a PDF metaadatok szabályozására?**  
  Adj át egy `PdfSaveOptions` példányt, és állíts be olyan tulajdonságokat, mint `Author`, `Title`, vagy `PdfAConformanceLevel`.

## Összefoglalás

Áttekintettük, hogyan lehet **create HTML document** C#‑ben, **set font family**, **set font size**, félkövér‑dőlt stílusokat alkalmazni, és végül **save HTML as PDF** – hatékonyan **convert HTML to PDF** az Aspose.HTML‑el. A kódrészlet elég rövid ahhoz, hogy bármely .NET projektbe beilleszthető legyen, ugyanakkor elég teljes ahhoz, hogy szilárd alapot nyújtson összetettebb jelentéskészítési forgatókönyvekhez.

## Következő lépések

- Kísérletezz CSS osztályokkal az újrahasználható stílusokhoz.  
- Kombinálj több bekezdést, táblázatot és képet, hogy gazdagabb PDF‑eket építs.  
- Fedezd fel a PDF/A megfelelőséget, ha archiválási szintű dokumentumokra van szükséged.  

Nyugodtan módosítsd a betűtípust, méretet vagy színeket – nincs korlát arra, hogy mit generálhatsz programozottan. Boldog kódolást, és legyenek a PDF‑eid mindig pontosan úgy megjelenítve, ahogy elképzeled!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}