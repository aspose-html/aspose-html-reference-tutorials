---
category: general
date: 2026-04-06
description: Vykreslete HTML do PNG v C# a vytvořte ZIP v paměti. Naučte se, jak načíst
  HTML ze řetězce, přidat tučný styl HTML a uložit HTML jako ZIP pomocí Aspose.HTML.
draft: false
keywords:
- render html to png
- create zip in memory
- load html from string
- save html as zip
- add bold style html
language: cs
og_description: Vykreslete HTML do PNG v C# a vytvořte ZIP v paměti. Tento tutoriál
  ukazuje, jak načíst HTML ze řetězce, přidat tučný styl HTML a uložit HTML jako ZIP.
og_title: Vykreslení HTML do PNG a ZIP v paměti – Kompletní průvodce C#
tags:
- Aspose.HTML
- C#
- Image Rendering
- ZIP Archives
title: Vykreslení HTML do PNG a ZIP v paměti – Kompletní průvodce C#
url: /cs/net/rendering-html-documents/render-html-to-png-and-zip-in-memory-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Renderování HTML do PNG a ZIP v paměti – kompletní průvodce v C#

Už jste někdy potřebovali **renderovat HTML do PNG** za běhu a zabalit zdroj spolu s jeho prostředky? Možná stavíte službu pro miniatury, generátor náhledů e‑mailů nebo nástroj pro reportování, který dodává samostatný HTML balíček. Ať už je scénář jakýkoli, problém je obvykle stejný: máte řetězec značkovacího jazyka, chcete jej stylovat, potřebujete rastrový obrázek a chtěli byste vše zkomprimovat do ZIPu, aniž byste se dotýkali souborového systému.

Takže tady je věc—Aspose.HTML dělá celý tento workflow hračkou. V tomto průvodci načteme HTML ze řetězce, **přidáme tučný styl HTML**, vykreslíme stránku do PNG a nakonec **vytvoříme ZIP v paměti**, který obsahuje jak HTML, tak všechny externí zdroje. Na konci budete mít připravený `ResultArchive.zip` a ostrý `final.png`, které budou ležet vedle sebe.

Probereme:

* Načítání HTML ze řetězce (ano, žádné soubory nejsou potřeba)  
* Stylování elementu tučným písmem  
* Konfiguraci možností renderování obrázku (velikost, antialiasing, hinting)  
* Uložení HTML do **ZIP archivu**, který existuje jen v paměti  
* Renderování stejného dokumentu jako PNG obrázku  

Žádné exotické závislosti, jen Aspose.HTML pro .NET a pár řádků idiomatického C#. Pojďme na to.

## Renderování HTML do PNG – Přehled

Než se ponoříme do kódu, pomůže rychlý mentální model. Představte si proces jako tři vrstvy:

1. **Vytvoření dokumentu** – předáte surový markup do Aspose.HTML a získáte objekt `Document`.  
2. **Transformace** – manipulujete s DOM (přidáte tučný text, změníte barvy atd.).  
3. **Export** – buď rasterizujete do PNG **nebo** serializujete celý výstup do ZIPu pro pozdější použití.

Oba exporty sdílejí stejný podkladový dokument, takže DOM vytvoříte jen jednou. Proto je tento přístup efektivní a snadno udržovatelný.

> **Pro tip:** Pokud plánujete obsluhovat mnoho miniatur, udržujte instanci `Document` v cache a renderujte jen tehdy, když se markup skutečně změní. Ušetříte tak spoustu CPU cyklů.

## Načíst HTML ze řetězce

Prvním krokem je předat markup přímo do `Document`. Žádné dočasné soubory, žádné streamy — jen obyčejný řetězec.

```csharp
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

// Step 1: Load an HTML document from a string.
var htmlContent = "<html><body><img src='logo.png'><span id='title'>Demo</span></body></html>";
var doc = new Document(htmlContent);
```

**Proč je to důležité:** Načítání ze řetězce (`load html from string`) vám umožní generovat markup za běhu — myslete na e‑mailové šablony, uživatelsky generované reporty nebo dokonce konverze z Markdownu do HTML. Konstruktor `Document` parsuje markup a vytvoří v‑paměti DOM připravený k manipulaci.

## Přidat tučný styl HTML

Nyní, když máme `Document`, udělejme titulek výraznější. Najdeme element podle jeho `id` a aplikujeme tučný styl písma.

```csharp
// Step 2: Apply a bold font style to the element with id 'title'.
doc.GetElementById("title").Style.FontStyle = WebFontStyle.Bold;
```

**Co se děje pod kapotou?** `GetElementById` vrací `IElement`, který představuje `<span id='title'>`. Nastavení `FontStyle` na `WebFontStyle.Bold` vloží CSS `font-weight: bold;` do inline stylu elementu. Toto je nejjednodušší způsob, jak **přidat tučný styl HTML** bez zásahu do externích stylových souborů.

> **Pozor:** Pokud element neexistuje, `GetElementById` vrátí `null` a řádek vyhodí `NullReferenceException`. V produkčním kódu byste to ošetřili, ale pro tento tutoriál víme, že element je přítomen.

## Vytvořit ZIP v paměti

Chceme přenosný balíček, který obsahuje HTML soubor *a* všechny externí zdroje jako `logo.png`. Pomocí `System.IO.Compression.ZipArchive` můžeme ZIP postavit kompletně v paměti, čímž se vyhneme jakémukoli I/O na disku, dokud ho nakonec neuložíme.

```csharp
// Step 3: Prepare a ZIP archive that will hold the HTML and its external resources.
using var zipStream = new MemoryStream();
using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: true);
var resourceHandler = new ZipResourceHandler(zip);
```

**Proč ZIP založený na paměti?**  
* **Výkon:** Žádné mezisouborové soubory znamenají méně zátěže disku.  
* **Bezpečnost:** Dočasný archiv se nikdy nedotkne souborového systému, což je výhodné v sandboxovaných prostředích.  
* **Flexibilita:** ZIP můžete streamovat přímo do odpovědi, Azure Blobu nebo jakéhokoli jiného úložiště.

`ZipResourceHandler` je Aspose pomocník, který umí automaticky zapisovat externí zdroje (např. obrázky) do stejného archivu, když později zavoláme `doc.Save`.

## Konfigurace možností renderování obrázku

Renderování HTML do bitmapy vyžaduje několik nastavení. Nastavíme šířku, výšku, antialiasing a hinting textu, abychom získali ostrý PNG.

```csharp
// Step 4: Configure image rendering options (size, antialiasing, and hinting).
var imgOptions = new ImageRenderingOptions
{
    Width = 600,
    Height = 400,
    UseAntialiasing = true,
    TextOptions = new TextOptions { UseHinting = true }
};
```

**Vysvětlení:**  
* `Width`/`Height` definují velikost výstupního plátna.  
* `UseAntialiasing` vyhlazuje hrany a zabraňuje zubatým čarám.  
* `TextOptions.UseHinting` zlepšuje čitelnost malých fontů, zejména na Windows, kde je běžný ClearType.

Tyto hodnoty můžete ladit podle požadavků vašeho UI. Pro high‑DPI miniatury zvýšte rozměry a později PNG zmenšete pomocí knihovny pro zpracování obrázků.

## Uložit HTML jako ZIP a renderovat PNG

Nyní přichází dvojí export: serializujeme HTML do ZIPu v paměti a ve stejném průchodu renderujeme dokument do PNG souboru na disku.

```csharp
// Step 5: Save the HTML into the ZIP and render the document as a PNG image.
doc.Save(zipStream, new HtmlSaveOptions { OutputStorage = resourceHandler });
doc.Save("YOUR_DIRECTORY/final.png", imgOptions);
```

**Co dělá `HtmlSaveOptions.OutputStorage`:** Říká Aspose, aby zapisoval každou externí referenci (např. `logo.png`) do `resourceHandler`, který pak soubor umístí do našeho `zip`. Samotný HTML soubor je také umístěn do archivu, čímž se zachová původní struktura složek.

Druhé volání `Save` renderuje stejný `Document` do rastrového obrázku pomocí dříve definovaných možností. Výsledkem je `final.png`, který vypadá přesně jako HTML, které byste viděli v prohlížeči.

> **Poznámka:** Pokud potřebujete PNG jako pole bajtů místo souboru, použijte `doc.Save(new MemoryStream(), imgOptions)` a poté stream přečtěte.

## Uložit ZIP archiv na disk

Nakonec vyprázdníme ZIP v paměti do fyzického souboru, aby bylo možné jej distribuovat nebo uložit pro pozdější použití.

```csharp
// Step 6: Persist the ZIP archive (contains HTML + external files) to disk.
zipStream.Position = 0;
File.WriteAllBytes("YOUR_DIRECTORY/ResultArchive.zip", zipStream.ToArray());
```

Nastavení `Position = 0` přetočí stream před čtením, čímž zajistí, že se zapíše celý archiv. Výsledný `ResultArchive.zip` obsahuje:

* `index.html` (původní markup)  
* `logo.png` (obrázek odkazovaný v HTML)  

Můžete jej rozbalit a otevřít `index.html` v libovolném prohlížeči; vykreslí se přesně jako právě vygenerovaný PNG.

![příklad renderování html do png](render-html-png.png)

*Image alt text: příklad renderování html do png*

## Kompletní funkční příklad

Sestavením všeho dohromady získáte kompletní, připravený program. Stačí nahradit `YOUR_DIRECTORY` skutečnou cestou ke složce na vašem počítači.

```csharp
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

class Program
{
    static void Main()
    {
        // 1️⃣ Load HTML from a string.
        var htmlContent = "<html><body><img src='logo.png'><span id='title'>Demo</span></body></html>";
        var doc = new Document(htmlContent);

        // 2️⃣ Add bold style to the title.
        doc.GetElementById("title").Style.FontStyle = WebFontStyle.Bold;

        // 3️⃣ Create a ZIP archive in memory.
        using var zipStream = new MemoryStream();
        using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: true);
        var resourceHandler = new ZipResourceHandler(zip);

        // 4️⃣ Set up image rendering options.
        var imgOptions = new ImageRenderingOptions
        {
            Width = 600,
            Height = 400,
            UseAntialiasing = true,
            TextOptions = new TextOptions { UseHinting = true }
        };

        // 5️⃣ Save HTML into the ZIP and render a PNG.
        doc.Save(zipStream, new HtmlSaveOptions { OutputStorage = resourceHandler });
        doc.Save("C:/Temp/final.png", imgOptions); // Adjust path as needed

        // 6️⃣ Write the ZIP to disk.
        zipStream.Position = 0;
        File.WriteAllBytes("C:/Temp/ResultArchive.zip", zipStream.ToArray());

        // 🎉 Done! You now have a PNG thumbnail and a self‑contained ZIP.
    }
}
```

### Očekávaný výstup

* **`final.png`** – 600 × 400 pixelový obrázek zobrazující logo a slovo **Demo** tučným písmem.  
* **`ResultArchive.zip`** – obsahuje `index.html` (stejný markup, který jste předali) a `logo.png`. Otevřením `index.html` v prohlížeči se reprodukuje PNG přesně.

## Závěr

Prošli jsme kompletním **render html to png** workflow a zároveň **create zip in memory**, **load html from string**, **add bold style html** a **save html as zip**. Kód je samostatný, používá jen Aspose.HTML a .NET základní knihovnu a demonstruje jak rasterové, tak archivní výstupy.

Další kroky? Zkuste nahradit PNG JPEGem, experimentujte s CSS transformacemi nebo streamujte ZIP přímo do HTTP odpovědi pro endpoint ke stažení. Můžete také vložit více HTML stránek do stejného archivu — stačí vytvořit další `Document` objekty a zavolat `doc.Save` se stejným `resourceHandler`.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}