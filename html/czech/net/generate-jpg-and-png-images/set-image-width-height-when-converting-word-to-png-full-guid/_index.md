---
category: general
date: 2026-05-22
description: Nastavte šířku a výšku obrázku při převodu dokumentu Word do PNG. Naučte
  se, jak exportovat docx jako obrázek s vysoce kvalitním vykreslením v podrobném
  návodu krok za krokem.
draft: false
keywords:
- set image width height
- convert word to png
- save docx as png
- export docx as image
- how to render word
language: cs
og_description: Nastavte šířku a výšku obrázku při převodu dokumentu Word do PNG.
  Tento tutoriál ukazuje, jak exportovat docx jako obrázek s nastavením vysoké kvality.
og_title: Nastavte šířku a výšku obrázku při převodu Wordu na PNG – kompletní průvodce
schemas:
- author: Aspose
  dateModified: '2026-05-22'
  description: Set image width height while converting a Word document to PNG. Learn
    how to export docx as image with high‑quality rendering in a step‑by‑step tutorial.
  headline: Set Image Width Height When Converting Word to PNG – Full Guide
  type: TechArticle
- description: Set image width height while converting a Word document to PNG. Learn
    how to export docx as image with high‑quality rendering in a step‑by‑step tutorial.
  name: Set Image Width Height When Converting Word to PNG – Full Guide
  steps:
  - name: 1. Preserve Transparent Backgrounds
    text: 'If your Word document contains shapes with transparent backgrounds and
      you want to keep that transparency, set the `BackgroundColor` to `Color.Transparent`:'
  - name: 2. Render Only a Specific Range
    text: Sometimes you only need a paragraph or a table, not the whole page. Use
      `DocumentVisitor` to extract the node and render it separately. That’s a more
      advanced scenario, but it shows **how to render word** content at a granular
      level.
  - name: 3. Adjust DPI Dynamically
    text: 'If you need different DPI per page (e.g., high‑resolution for the cover
      page), modify `Resolution` inside the loop:'
  - name: 4. Batch Processing
    text: When converting dozens of documents, wrap the whole flow in a method and
      reuse the same `ImageRenderingOptions` instance. Re‑using the options object
      reduces allocation overhead.
  type: HowTo
tags:
- Aspose.Words
- C#
- Image Rendering
title: Nastavte šířku a výšku obrázku při převodu Wordu na PNG – kompletní průvodce
url: /cs/net/generate-jpg-and-png-images/set-image-width-height-when-converting-word-to-png-full-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nastavte šířku a výšku obrázku při převodu Wordu na PNG – Kompletní průvodce

Už jste se někdy zamýšleli, jak **nastavit šířku a výšku obrázku**, když **převádíte Word na PNG**? Nejste jediní. Mnoho vývojářů narazí na problém, když výchozí export vytvoří rozmazaný obrázek nebo nesprávné rozměry, a pak stráví hodiny hledáním oprav, které skutečně fungují.

V tomto tutoriálu projdeme čistým, end‑to‑end řešením, které ukazuje **jak renderovat word** dokumenty jako PNG obrázky, což vám umožní **uložit docx jako PNG** s přesnou kontrolou šířky‑výšky a vysoce kvalitním antialiasingem. Na konci budete mít připravený kód, solidní pochopení možností API a několik profesionálních tipů, jak se vyhnout běžným úskalím.

## Co se naučíte

- Načíst soubor `.docx` pomocí Aspose.Words for .NET.
- **Nastavit šířku a výšku obrázku** pomocí `ImageRenderingOptions`.
- **Exportovat docx jako obrázek** (PNG) s povoleným antialiasingem.
- Jak **převést word na png** pro jednu stránku nebo celý dokument.
- Tipy pro práci s velkými dokumenty, úvahy o DPI a cesty v souborovém systému.

Žádné externí nástroje, žádné nešikovné příkazy v terminálu — jen čistý C# kód, který můžete vložit do libovolného .NET projektu.

---

## Předpoklady

Než se pustíme dál, ujistěte se, že máte následující:

| Požadavek | Proč je důležité |
|-------------|----------------|
| **.NET 6.0+** (nebo .NET Framework 4.7.2) | Aspose.Words podporuje oba, ale novější runtime poskytuje lepší výkon. |
| **Aspose.Words for .NET** NuGet balíček (`Install-Package Aspose.Words`) | Poskytuje třídu `Document` a renderovací engine. |
| Wordový dokument (`.docx`), který chcete převést na PNG. | Zdroj, který budete konvertovat. |
| Základní znalost C# — budete rozumět `using` příkazům a inicializaci objektů. | Umožní plynulejší učení. |

Pokud vám chybí NuGet balíček, spusťte následující příkaz v Package Manager Console:

```powershell
Install-Package Aspose.Words
```

A to je vše — jakmile je balíček nainstalován, můžete začít kódovat.

---

## Krok 1: Načtěte zdrojový dokument

První věc, kterou musíte udělat, je nasměrovat knihovnu na Word soubor, který chcete transformovat.

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Load the .docx file from disk
Document doc = new Document(@"C:\MyFiles\input.docx");
```

**Proč je to důležité:** Třída `Document` načte celý Word balíček do paměti, čímž získáte přístup ke stránkám, stylům a všemu ostatnímu. Pokud je cesta špatná, dostanete `FileNotFoundException`, takže dvakrát zkontrolujte, že soubor existuje a že cesta používá escapované zpětné lomítka (`\\`) nebo doslovný řetězec (`@`).  

> **Pro tip:** Zabalte volání načtení do `try/catch` bloku, pokud očekáváte, že soubor může během běhu chybět.

---

## Krok 2: Nakonfigurujte možnosti renderování obrázku (Set Image Width Height)

Nyní přichází jádro tutoriálu: **jak nastavit šířku a výšku obrázku**, aby výsledný PNG nebyl roztažený nebo pixelovaný. Třída `ImageRenderingOptions` vám poskytuje detailní kontrolu nad rozměry, DPI a vyhlazováním.

```csharp
// Create rendering options and explicitly set width and height
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Desired output size in pixels
    Width = 1024,          // Set image width height: 1024px wide
    Height = 768,          // Set image width height: 768px tall

    // High‑quality antialiasing works on Windows, Linux, and macOS
    UseAntialiasing = true,

    // Optional: increase DPI for sharper output (default is 96)
    Resolution = 300
};
```

**Vysvětlení klíčových vlastností:**

- `Width` a `Height` — Jedná se o přesné rozměry v pixelech, které chcete. Nastavením těchto hodnot **nastavíte šířku a výšku obrázku** přímo a přepíšete výchozí velikost stránky.
- `UseAntialiasing` — Povoluje vysoce kvalitní vyhlazování textu a vektorové grafiky, což je klíčové, když **převádíte word na png** a chcete ostré hrany.
- `Resolution` — Vyšší DPI poskytuje více detailů, zejména u složitých rozvržení. Dávejte pozor na spotřebu paměti; 300 DPI obrázek může být velký.

> **Proč nepoužít jen výchozí velikost?** Výchozí používá fyzické rozměry stránky (např. A4 při 96 DPI). To často vytvoří obrázek 794 × 1123 pixelů — v pořádku pro některé případy, ale ne když potřebujete konkrétní náhled UI nebo fixní velikost.

---

## Krok 3: Renderujte a uložte jako PNG (Export Docx as Image)

Po načtení dokumentu a nastavení možností můžete konečně **exportovat docx jako obrázek**. Metoda `RenderToImage` udělá těžkou práci.

```csharp
// Render the first page (page index 0) to a PNG file
doc.RenderToImage(@"C:\MyFiles\output.png", imageOptions);
```

Pokud chcete renderovat **celý dokument** (všechny stránky) do samostatných PNG souborů, projděte kolekci stránek ve smyčce:

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string outPath = $@"C:\MyFiles\page_{i + 1}.png";
    doc.RenderToImage(outPath, imageOptions, i);
}
```

**Co se děje pod kapotou?** Renderér rasterizuje každou stránku pomocí vámi zadaných rozměrů, aplikuje antialiasing a zapíše PNG bajtový proud na disk. Protože PNG je bezztrátový, zachováte plnou věrnost původního rozvržení Wordu.

**Očekávaný výstup:** Ostrý PNG soubor přesně 1024 × 768 pixelů (nebo jakoukoliv velikost jste nastavili). Otevřete jej v libovolném prohlížeči obrázků a uvidíte Word obsah vykreslený přesně tak, jak je v původním dokumentu, ale nyní jako bitmapový obrázek.

---

## Pokročilé tipy a variace

### 1. Zachování transparentního pozadí

Pokud váš Word dokument obsahuje tvary s transparentním pozadím a chcete tuto transparentnost zachovat, nastavte `BackgroundColor` na `Color.Transparent`:

```csharp
imageOptions.BackgroundColor = System.Drawing.Color.Transparent;
```

### 2. Renderovat jen konkrétní rozsah

Někdy potřebujete jen odstavec nebo tabulku, ne celou stránku. Použijte `DocumentVisitor` k extrakci uzlu a renderujte jej samostatně. Jedná se o pokročilejší scénář, ale ukazuje **jak renderovat word** obsah na granulární úrovni.

### 3. Dynamické nastavení DPI

Pokud potřebujete jiné DPI pro různé stránky (např. vysoké rozlišení pro obálku), upravte `Resolution` uvnitř smyčky:

```csharp
if (i == 0) imageOptions.Resolution = 600; // cover page
else imageOptions.Resolution = 300;
```

### 4. Hromadné zpracování

Při konverzi desítek dokumentů zabalte celý tok do metody a znovu použijte stejnou instanci `ImageRenderingOptions`. Opakované používání objektu s možnostmi snižuje alokační režii.

---

## Běžné úskalí a jak se jim vyhnout

| Symptom | Pravděpodobná příčina | Řešení |
|---------|-----------------------|--------|
| PNG je rozmazaný i přes vysoké DPI | `UseAntialiasing` zůstalo `false` | Nastavte `UseAntialiasing = true`. |
| Výstupní velikost neodpovídá `Width`/`Height` | DPI nebylo zohledněno | Vynásobte požadovanou velikost hodnotou `Resolution / 96` nebo upravte `Resolution`. |
| Výjimka Out‑of‑memory u velkých dokumentů | Renderování celého dokumentu při 300 DPI | Renderujte po jedné stránce, po uložení každého obrázku uvolněte paměť. |
| PNG má bílou barvu pozadí u transparentních obrázků | `BackgroundColor` nebylo nastaveno | Nastavte `imageOptions.BackgroundColor = Color.Transparent`. |

---

## Kompletní funkční příklad

Níže je samostatný program, který můžete zkopírovat do konzolové aplikace. Demonstruje **convert word to png**, **save docx as png** a samozřejmě **set image width height**.

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;
using System.Drawing; // For Color

namespace WordToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            string inputPath = @"C:\MyFiles\input.docx";
            Document doc = new Document(inputPath);

            // 2️⃣ Configure rendering options (set image width height)
            ImageRenderingOptions options = new ImageRenderingOptions
            {
                Width = 1024,          // Desired pixel width
                Height = 768,          // Desired pixel height
                UseAntialiasing = true,
                Resolution = 300,
                BackgroundColor = Color.Transparent // Keep transparency if needed
            };

            // 3️⃣ Render the first page to PNG (export docx as image)
            string outputPath = @"C:\MyFiles\output.png";
            doc.RenderToImage(outputPath, options);

            Console.WriteLine($"✅ Document rendered successfully to {outputPath}");
            // Optional: render all pages
            //RenderAllPages(doc, options);
        }

        // Helper method for batch rendering (uncomment if needed)
        static void RenderAllPages(Document doc, ImageRenderingOptions options)
        {
            for (int i = 0; i < doc.PageCount; i++)
            {
                string pagePath = $@"C:\MyFiles\page_{i + 1}.png";
                doc.RenderToImage(pagePath, options, i);
                Console.WriteLine($"Page {i + 1} saved to {pagePath}");
            }
        }
    }
}
```

**Spusťte ho:** Sestavte projekt, umístěte platný `input.docx` na zadanou cestu a spusťte. Měli byste získat `output.png` přesně **1024 × 768** pixelů, renderovaný s hladkými hranami.

## Související tutoriály

- [How to Enable Antialiasing When Converting DOCX to PNG/JPG](/html/english/net/generate-jpg-and-png-images/how-to-enable-antialiasing-when-converting-docx-to-png-jpg/)
- [convert docx to png – create zip archive c# tutorial](/html/english/net/generate-jpg-and-png-images/convert-docx-to-png-create-zip-archive-c-tutorial/)
- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}