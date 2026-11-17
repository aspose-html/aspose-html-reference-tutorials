---
category: general
date: 2026-04-06
description: Naučte se, jak povolit antialiasing, nastavit šířku a výšku obrázku a
  uložit dokument jako PNG v C# – rychlý průvodce exportem dokumentu do obrázku.
draft: false
keywords:
- how to enable antialiasing
- save document as png
- set image width
- set image height
- export document to image
language: cs
og_description: Jak povolit antialiasing při exportu dokumentu do obrázku. Tento návod
  vám ukáže, jak nastavit šířku obrázku, výšku obrázku a uložit dokument jako PNG.
og_title: Jak povolit antialiasing – Exportovat dokument do obrázku
tags:
- C#
- ImageRendering
- Antialiasing
title: Jak povolit antialiasing – export dokumentu do obrázku pomocí C#
url: /cs/net/generate-jpg-and-png-images/how-to-enable-antialiasing-export-document-to-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak povolit antialiasing – Export dokumentu do obrázku v C#

Už jste se někdy zamýšleli **jak povolit antialiasing** při převodu dokumentu na obrázek? Možná jste zkusili rychlé volání `Save` a výsledek vypadal zubatě, zejména u úhlopříčných čar. Dobrá zpráva je, že nepotřebujete grafického kouzelníka – stačí jen pár řádků C# a správné možnosti.

V tomto tutoriálu projdeme nastavení šířky obrázku, nastavení výšky obrázku a nakonec **uložení dokumentu jako PNG**, abyste mohli **exportovat dokument do obrázku** s hladkými hranami. Na konci budete mít připravený úryvek kódu, který vytvoří ostrý PNG 800 × 600 s povoleným antialiasingem.

## Požadavky

- .NET 6.0 nebo novější (kód funguje také na .NET Framework 4.7+)  
- Odkaz na knihovnu pro vykreslování, která podporuje `ImageRenderingOptions` (např. Aspose.Words, Syncfusion nebo jakékoli API poskytující podobné vlastnosti)  
- Základní znalost syntaxe C#  

Žádné složité nastavení – stačí přidat NuGet balíček a můžete začít.

## Krok 1: Instalace knihovny pro vykreslování

Nejprve přidejte balíček do svého projektu. Pokud používáte Aspose.Words, spusťte:

```bash
dotnet add package Aspose.Words
```

> **Tip:** Udržujte verzi knihovny aktuální; nejnovější vydání (k dubnu 2026) přidává optimalizace výkonu pro antialiasing.

## Krok 2: Vytvoření objektu Document

Načtěte nebo vytvořte dokument, který chcete vykreslit. Zde je minimální příklad, který vytvoří jednostránkový dokument s jednoduchým odstavcem:

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Create a new blank document
Document doc = new Document();

// Add a paragraph with some text
Paragraph para = new Paragraph(doc);
Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
para.AppendChild(run);
doc.FirstSection.Body.AppendChild(para);
```

Třída `Document` je vstupní bod; vše, co vykreslujete, pochází z ní. Ve skutečných projektech pravděpodobně načtete existující .docx:

```csharp
// Document doc = new Document("input.docx");
```

## Krok 3: Definování možností vykreslování (šířka, výška, antialiasing)

Nyní odpovíme na hlavní otázku: **jak povolit antialiasing**. Objekt `ImageRenderingOptions` vám umožní zapnout vyhlazování a nastavit rozměry.

```csharp
// Step 3: Define rendering options (size and antialiasing)
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Set the desired output size
    Width = 800,               // set image width
    Height = 600,              // set image height

    // Turn on antialiasing for smoother edges
    UseAntialiasing = true
};
```

Všimněte si komentářů: výslovně zmiňují **nastavit šířku obrázku**, **nastavit výšku obrázku** a **UseAntialiasing** – tři ovládací prvky, které jsou klíčové, když chcete vytvořit vylepšený PNG.

### Proč je antialiasing důležitý

Bez antialiasingu se úhlopříčné čáry a křivky jeví jako schodovité, protože vykreslovač považuje každý pixel buď za zapnutý, nebo vypnutý. Zapnutím se prolnou hrany pixelů, což vytvoří vizuální změkčení podobné tomu, co vidíte v editoru fotografií. Nevýhodou je mírné zvýšení doby zpracování, ale pro většinu UI‑orientovaných exportů je to zanedbatelné.

## Krok 4: Uložení dokumentu jako PNG (Export dokumentu do obrázku)

S připravenými možnostmi konečně **uložíme dokument jako PNG**. Metoda `Save` přijímá cestu k souboru a možnosti, které jsme právě nakonfigurovali.

```csharp
// Step 4: Render the document to a PNG file using the configured options
doc.Save("output.png", imageOptions);
```

A je to – váš dokument je nyní PNG 800 × 600 s aplikovaným antialiasingem. Pokud otevřete `output.png`, uvidíte čistý text, hladké čáry a žádné zubaté artefakty.

### Ověření výsledku

Můžete rychle zkontrolovat soubor v libovolném prohlížeči obrázků. Hledejte:

- Správné rozměry (800 × 600)  
- Žádné viditelné schodovité hrany na textu nebo tvarech  
- Průhledné pozadí, pokud váš dokument neobsahoval barvu pozadí (většina knihoven výchozí nastavení používá bílou)

Pokud obrázek vypadá zubatě, ověřte, že `UseAntialiasing = true` není někde přepsáno.

## Krok 5: Okrajové případy a varianty

### Změna výstupního formátu

Chcete JPEG místo PNG? Stačí změnit příponu souboru a případně upravit kompresi:

```csharp
imageOptions.JpegQuality = 90; // only works for JPEG output
doc.Save("output.jpg", imageOptions);
```

### Export více stránek

Když má zdrojový dokument několik stránek, vykreslovač ve výchozím nastavení vytvoří samostatné soubory obrázků pro každou stránku. Můžete projít stránky v cyklu:

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string fileName = $"page_{i + 1}.png";
    doc.Save(fileName, imageOptions);
}
```

### Uložení do streamu (např. HTTP odpověď)

Pokud budujete webové API, můžete PNG vrátit přímo:

```csharp
using (MemoryStream ms = new MemoryStream())
{
    doc.Save(ms, imageOptions);
    ms.Position = 0;
    // Return ms as FileResult in ASP.NET Core
}
```

## Kompletní funkční příklad

Níže je kompletní, připravený program, který zahrnuje všechny probírané kroky:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;

class Program
{
    static void Main()
    {
        // 1️⃣ Create or load a document
        Document doc = new Document();
        Paragraph para = new Paragraph(doc);
        Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
        para.AppendChild(run);
        doc.FirstSection.Body.AppendChild(para);

        // 2️⃣ Define rendering options (size and antialiasing)
        ImageRenderingOptions imageOptions = new ImageRenderingOptions
        {
            Width = 800,               // set image width
            Height = 600,              // set image height
            UseAntialiasing = true     // how to enable antialiasing
        };

        // 3️⃣ Export document to image (save document as PNG)
        doc.Save("output.png", imageOptions);

        Console.WriteLine("Image saved as output.png with antialiasing enabled.");
    }
}
```

Po spuštění tohoto programu se ve složce spustitelného souboru vytvoří `output.png`. Otevřete jej a uvidíte hladký PNG 800 × 600 – přesně to, co jsme chtěli dosáhnout.

## Často kladené otázky a řešení problémů

- **Co když obrázek vypadá rozmazaně?**  
  Rozmazání může nastat při zvětšování malé zdrojové stránky. Udržujte velikost zdrojové stránky blízko cílových rozměrů, nebo zvýšte DPI pomocí `imageOptions.Resolution` (např. `Resolution = 300`).

- **Funguje to na .NET Frameworku?**  
  Ano. Stejné API existuje i v klasickém frameworku; stačí odkazovat na odpovídající DLL.

- **Mohu nastavit barvu pozadí?**  
  Rozhodně. Nastavte `imageOptions.BackgroundColor = System.Drawing.Color.Transparent;` před uložením.

- **Je antialiasing hardwarově akcelerovaný?**  
  Většina knihoven provádí softwarový antialiasing. Pokud potřebujete GPU akceleraci, hledejte vykreslovací engine, který to explicitně podporuje.

## Závěr

Probrali jsme **jak povolit antialiasing** při **exportu dokumentu do obrázku**, prošli jsme **nastavením šířky obrázku** a **nastavením výšky obrázku** a ukázali vám přesné kroky k **uložení dokumentu jako PNG**. Výše uvedený úryvek je připravený pro produkci a můžete jej nyní přizpůsobit pro JPEG, vícestránkové PDF nebo dokonce streamovat obrázek přímo klientovi.

Dále můžete zkusit přidat vodoznaky, upravit DPI pro výstup v tiskové kvalitě nebo integrovat tuto logiku do endpointu ASP.NET Core. Principy zůstávají stejné – jen vyměňte cestu k souboru za stream odpovědi.

Šťastné programování a užívejte si ty ostré, antialiasované obrázky! 

![Rendered PNG with antialiasing enabled](output.png "Rendered PNG with antialiasing enabled")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}