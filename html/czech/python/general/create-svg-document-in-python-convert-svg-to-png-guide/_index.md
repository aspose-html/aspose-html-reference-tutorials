---
category: general
date: 2026-07-05
description: Vytvořte SVG dokument v Pythonu a naučte se rychle převádět SVG na PNG.
  Obsahuje kroky pro uložení SVG souboru a export SVG jako PNG.
draft: false
keywords:
- create SVG document
- convert SVG to PNG
- SVG to PNG Python
- save SVG file
- export SVG as PNG
language: cs
og_description: Vytvořte SVG dokument v Pythonu a okamžitě jej převěďte na PNG. Postupujte
  podle tohoto krok‑za‑krokem průvodce, jak uložit SVG soubor a exportovat SVG jako
  PNG.
og_title: Vytvořte SVG dokument v Pythonu – převod SVG na PNG
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create SVG document in Python and learn how to convert SVG to PNG quickly.
    Includes save SVG file steps and export SVG as PNG.
  headline: Create SVG Document in Python – Convert SVG to PNG Guide
  type: TechArticle
tags:
- Python
- Aspose.HTML
- Image Conversion
title: Vytvoření SVG dokumentu v Pythonu – Průvodce převodem SVG na PNG
url: /cs/python/general/create-svg-document-in-python-convert-svg-to-png-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření SVG dokumentu v Pythonu – Průvodce převodem SVG na PNG

Už jste někdy potřebovali **create SVG document** v Pythonu, ale nebyli jste si jisti, kde začít? Nejste jediní — vývojáři se neustále ptají: „Jak převést vektorový výkres na PNG, aniž bychom se museli zabývat externími nástroji?“ Dobrou zprávou je, že s Aspose.HTML pro Python můžete vytvořit SVG, **save SVG file**, a **export SVG as PNG** během několika řádků kódu.

V tomto tutoriálu projdeme celý pracovní postup: instalaci knihovny, vytvoření jednoduchého SVG, uložení na disk a nakonec použití funkcí **convert SVG to PNG**. Na konci budete mít znovupoužitelný skript, který můžete vložit do jakéhokoli projektu — ať už generujete grafy, ikony nebo dynamické grafiky za běhu.

## Požadavky – Co budete potřebovat před zahájením

- Python 3.8 nebo novější (kód funguje také na 3.9‑3.11)  
- Instalovatelná verze **aspose.html** přes pip (bezplatná zkušební verze funguje pro většinu případů použití)  
- Oprávnění k zápisu do složky, kde budou uloženy SVG a PNG  

Pokud již máte virtuální prostředí, skvělé — aktivujte jej nyní. Jinak vytvořte nové:

```bash
python -m venv venv
source venv/bin/activate   # on Windows use `venv\Scripts\activate`
```

Poté nainstalujte balíček Aspose.HTML:

```bash
pip install aspose-html
```

> **Pro tip:** Kolo `aspose-html` obsahuje všechny nativní binární soubory, takže nebudete potřebovat žádné další systémové knihovny.

## Krok 1: Vytvoření SVG dokumentu v Pythonu

Prvním krokem je **create SVG document** pomocí třídy `SVGDocument`. Představte si tento objekt jako prázdné plátno, do kterého můžete přidávat jakýkoli platný SVG markup.

```python
from aspose.html import SVGDocument

# Initialize a new, empty SVG document
svg = SVGDocument()

# Append a simple green circle as raw SVG markup
svg.root.append_child("<circle cx='50' cy='50' r='40' fill='green'/>")
```

Proč použít `append_child` s řetězcem? Umožňuje vložit surové SVG úryvky přímo do DOM, což je ideální pro rychlé prototypy nebo když generujete markup z jiného zdroje (např. API). Vlastnost `root` ukazuje na element `<svg>`, takže v podstatě říkáte „přidej toto dítě do SVG“.

## Krok 2: Uložení SVG souboru (volitelné, ale užitečné)

Před konverzí můžete chtít **save SVG file**, abyste si mohli výstup prohlédnout nebo předat návrháři. Tento krok je volitelný, ale skvělý při ladění.

```python
# Choose a folder you have write access to
output_dir = "output"
import os
os.makedirs(output_dir, exist_ok=True)

# Persist the SVG to disk
svg_path = os.path.join(output_dir, "circle.svg")
svg.save(svg_path)
print(f"SVG saved to {svg_path}")
```

Spuštěním tohoto úryvku vznikne soubor, který vypadá takto:

```xml
<?xml version="1.0" encoding="utf-8"?>
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <circle cx="50" cy="50" r="40" fill="green"/>
</svg>
```

Otevřete jej v prohlížeči — uvidíte ostrý zelený kruh uprostřed viewboxu 100 × 100. Pokud tvar není podle očekávání, upravte markup a skript spusťte znovu. Tento iterativní cyklus je důvod, proč je **saving the SVG file** často nejrychlejší způsob, jak ověřit vaši vektorovou logiku.

## Krok 3: Nastavení možností konverze PNG

Nyní přichází zábavná část: převod vektoru na rastrový obrázek. Třída `PNGSaveOptions` vám umožní jemně doladit výstup — rozlišení, barvu pozadí, úroveň komprese atd. Pro většinu scénářů jsou výchozí hodnoty dostačující, ale ukážeme si nastavení vlastní šířky a výšky pro ilustraci API.

```python
from aspose.html import PNGSaveOptions

png_options = PNGSaveOptions()
png_options.width = 200   # pixels
png_options.height = 200  # pixels
# Optional: set a transparent background
png_options.background_color = None
```

Vlastnosti `width` a `height` řídí velikost rastru, nezávisle na vnitřních rozměrech SVG. To je užitečné, když potřebujete miniatury nebo vysoce rozlišené výtisky ze stejného SVG zdroje.

## Krok 4: Převod SVG na PNG — jednorázová magie

S připraveným dokumentem a nastavenými možnostmi je skutečné volání **convert SVG to PNG** jedním řádkem. Metoda `Converter.convert_svg` zajišťuje parsování, rasterizaci a zápis souboru pod pokličkou.

```python
from aspose.html import Converter

png_path = os.path.join(output_dir, "circle.png")
Converter.convert_svg(svg, png_options, png_path)
print(f"PNG exported to {png_path}")
```

Když otevřete `circle.png`, uvidíte 200 × 200 pixelový obrázek zeleného kruhu, perfektně antialiasovaný. Konverze respektuje vektorovou povahu SVG, takže zvětšení nezpůsobí rozmazání — na rozdíl od naivních bitmap‑to‑bitmap triků.

### Očekávaný výstup

| File | Description |
|------|-------------|
| `circle.svg` | Textový SVG obsahující jediný element `<circle>`. |
| `circle.png` | 200 × 200 PNG se zeleným kruhem na průhledném pozadí. |

Pokud porovnáte oba, PNG bude vypadat identicky jako SVG při vykreslení ve stejné velikosti, ale nyní máte přenosný rastrový formát připravený pro API, která přijímají jen PNG (např. e‑mailové přílohy, starší nástroje pro reportování).

## Krok 5: Zabalit vše dohromady — znovupoužitelná funkce

Většina reálných projektů nebude konvertovat jen jeden pevně zakódovaný tvar. Zabalme logiku do funkce, která přijímá libovolný SVG markup a vrací cestu k PNG. Tím ukážeme **export SVG as PNG** čistým a znovupoužitelným způsobem.

```python
def svg_to_png(svg_markup: str, png_path: str, width: int = 200, height: int = 200) -> None:
    """
    Converts a string containing SVG markup into a PNG file.

    Parameters
    ----------
    svg_markup : str
        Raw SVG XML to be rendered.
    png_path : str
        Destination file path for the PNG image.
    width, height : int, optional
        Desired dimensions of the output PNG (default 200×200).
    """
    # Create the SVG document and inject markup
    doc = SVGDocument()
    doc.root.append_child(svg_markup)

    # Prepare PNG options
    opts = PNGSaveOptions()
    opts.width = width
    opts.height = height
    opts.background_color = None

    # Perform the conversion
    Converter.convert_svg(doc, opts, png_path)

# Example usage
example_svg = "<rect x='10' y='10' width='80' height='80' fill='orange'/>"
svg_to_png(example_svg, os.path.join(output_dir, "rect.png"))
print("Custom rectangle PNG created.")
```

Spuštěním této funkce s libovolným platným SVG řetězcem **create SVG document**, **save SVG file** (pokud do funkce přidáte `doc.save`) a **export SVG as PNG** v jednom úhledném volání. Klidně upravte `width`, `height` nebo přidejte barvu pozadí, aby odpovídala brandingu vašeho projektu.

## Časté otázky a okrajové případy

| Question | Answer |
|----------|--------|
| *Funguje to na Linux/macOS?* | Ano — Aspose.HTML je multiplatformní. Jen se ujistěte, že máte správné wheel pro váš OS (`manylinux` wheels pokrývají většinu Linux distribucí). |
| *Co když SVG odkazuje na externí fonty?* | Konvertor automaticky vloží systémové fonty. Pro vlastní fonty umístěte soubory `.ttf`/`.otf` do stejné složky a odkažte na ně pomocí bloku `<style>` uvnitř SVG. |
| *Mohu převést více SVG najednou (batch)?* | Ano — projděte seznam SVG řetězců nebo cest k souborům a pro každý zavolejte `svg_to_png`. Knihovna je thread‑safe, takže můžete použít i `concurrent.futures` pro paralelní zpracování. |
| *Jak mohu řídit kompresi PNG?* | `PNGSaveOptions` poskytuje vlastnost `compression_level` (0‑9). Nižší čísla vedou k větším souborům, ale rychlejším zápisům; vyšší čísla produkují menší soubory na úkor času CPU. |
| *Existuje způsob, jak zachovat původní viewbox SVG?* | Vynechte nastavení `width`/`height` v `PNGSaveOptions`. Konvertor pak použije vnitřní rozměry SVG. |

## Závěr

Probrali jsme vše, co potřebujete k **create SVG document** v Pythonu, **save SVG file** a **convert SVG to PNG** pomocí Aspose.HTML. Postup krok za krokem ukazuje, proč je každá část důležitá, od inicializace DOM po jemné ladění rasterových možností, a končí znovupoužitelným pomocníkem, který vám umožní **export SVG as PNG** jedním voláním.

Dále můžete zkoumat pokročilejší funkce, jako je přidávání textových vrstev, vkládání obrázků nebo generování vícestránkových PDF ze SVG. Podívejte se na další související klíčová slova — tutoriály **SVG to PNG Python** často zkoumají výkonové benchmarky, zatímco průvodci **convert SVG to PNG** někdy diskutují alternativní knihovny jako CairoSVG nebo Pillow pro srovnání.

Máte podivný SVG, se kterým máte problémy? Zanechte komentář a společně to vyřešíme. Šťastné kódování a užívejte si převod vektorů na ostré PNG!

![Diagram zobrazující workflow vytvoření SVG dokumentu](https://example.com/images/svg-to-png-workflow.png "Diagram zobrazující workflow vytvoření SVG dokumentu")

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Uložení SVG dokumentu v Aspose.HTML pro Java](/html/english/java/saving-html-documents/save-svg-document/)
- [svg to png java – Převod SVG na obrázek pomocí Aspose.HTML pro Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Renderování SVG dokumentu jako PNG v .NET s Aspose.HTML](/html/english/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}