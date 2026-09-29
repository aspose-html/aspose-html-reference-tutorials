---
category: general
date: 2026-09-29
description: Jak uložit SVG pomocí Pythonu a exportovat SVG do PNG. Naučte se převést
  SVG na PNG s jemně nastavenými možnostmi během několika minut.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save svg
- convert svg to png
- save svg as png
- export svg to png
- vector svg to png
language: cs
lastmod: 2026-09-29
og_description: Jak uložit SVG pomocí Pythonu a exportovat SVG do PNG. Postupujte
  podle tohoto návodu, abyste převáděli SVG na PNG s plnou kontrolou nad možnostmi.
og_image_alt: Screenshot of Python code converting a vector SVG file to a PNG image
og_title: Jak uložit SVG jako PNG pomocí Pythonu – krok za krokem
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: How to save SVG using Python and export SVG to PNG. Learn to convert
    SVG to PNG with fine‑tuned options in minutes.
  headline: How to save SVG as PNG with Python – complete guide
  type: TechArticle
- description: How to save SVG using Python and export SVG to PNG. Learn to convert
    SVG to PNG with fine‑tuned options in minutes.
  name: How to save SVG as PNG with Python – complete guide
  steps:
  - name: Load the SVG document
    text: '```python from aspose.svg import SVGDocument'
  - name: (Optional) Create image‑save options
    text: '```python from aspose.svg import ImageSaveOptions'
  - name: Save the SVG as PNG
    text: '```python # Export the SVG to a PNG file using the options defined above
      svg_doc.save("YOUR_DIRECTORY/vector.png", options) ```'
  - name: Full script
    text: 'Putting the pieces together yields a complete, runnable program:'
  - name: Missing file or invalid path
    text: 'If `src_path` does not exist, `SVGDocument` raises a `FileNotFoundError`.
      Wrap the call in a `try/except` block to provide a friendly error message:'
  - name: Preserving aspect ratio
    text: When only one dimension (width **or** height) is set, the library automatically
      scales the other dimension to maintain the original aspect ratio. If you set
      both dimensions, the image may stretch. Choose the approach that matches your
      UI requirements.
  - name: Transparent backgrounds
    text: 'If the original SVG relies on transparency (e.g., icons), you can keep
      the PNG transparent by omitting `background_color`:'
  type: HowTo
tags:
- Python
- SVG
- Image conversion
title: Jak uložit SVG jako PNG pomocí Pythonu – kompletní průvodce
url: /cs/python/general/how-to-save-svg-as-png-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak uložit SVG jako PNG pomocí Pythonu – kompletní průvodce

Pokud potřebujete **jak uložit SVG** jako rastrový obrázek, tento tutoriál vám ukáže připravené řešení připravené k okamžitému spuštění. Naučíte se, jak načíst vektorový SVG soubor, volitelně upravit nastavení ukládání obrázku a exportovat výsledek do PNG pomocí pouhých tří řádků kódu.

Ukládání SVG souborů jako PNG je běžné, když chcete vložit grafiku do webových stránek, generovat miniatury nebo poskytovat rastrové obrázky do pipeline strojového učení. Přístup popsaný zde funguje na Windows, macOS a Linuxu bez dalších nativních závislostí.

## Požadavky

* Python 3.9 nebo novější nainstalovaný
* Balíček `aspose.svg` (oficiální Aspose SVG pro Python přes .NET). Nainstalujte jej pomocí:

```bash
pip install aspose-svg
```

* Platný SVG soubor na disku (např. `vector.svg`)

Tyto požadavky udržují příklad samostatný a vyhýbají se externím nástrojům, jako je CairoSVG.

## Jak uložit SVG pomocí Pythonu

Jádrem procesu jsou tři kroky: načtení, konfigurace a uložení. Následující sekce rozebírají každý krok.

### Krok 1: Načíst SVG dokument

```python
from aspose.svg import SVGDocument

# Load the SVG file from the local filesystem
svg_doc = SVGDocument("YOUR_DIRECTORY/vector.svg")
```

`SVGDocument` parsuje SVG XML a vytváří reprezentaci v paměti. Načtení souboru jako první je povinné; jinak operace uložení nemá žádná zdrojová data.

### Krok 2: (Volitelné) Vytvořit možnosti ukládání obrázku

```python
from aspose.svg import ImageSaveOptions

# Create default options; you can tweak width, height, and background
options = ImageSaveOptions()
options.width = 800          # Desired output width in pixels
options.height = 600         # Desired output height in pixels
options.background_color = "#FFFFFF"  # Force a white background for transparent SVGs
```

`ImageSaveOptions` vám umožňuje jemně doladit výstup PNG. Úprava šířky a výšky zachovává poměr stran, pokud nenastavíte obojí explicitně. Nastavení barvy pozadí je užitečné, když originální SVG obsahuje průhlednost, ale potřebujete neprůhledný PNG.

### Krok 3: Uložit SVG jako PNG

```python
# Export the SVG to a PNG file using the options defined above
svg_doc.save("YOUR_DIRECTORY/vector.png", options)
```

Metoda `save` zapíše PNG soubor na cílovou cestu. Pokud vynecháte argument `options`, knihovna použije výchozí rozměry odvozené z viewBox SVG.

### Kompletní skript

Sestavením všech částí získáte kompletní, spustitelný program:

```python
# -*- coding: utf-8 -*-
"""
How to save SVG as PNG with Python.
This script loads an SVG file, applies optional image‑save settings,
and exports the result to PNG.
"""

from aspose.svg import SVGDocument, ImageSaveOptions

def convert_svg_to_png(
    src_path: str,
    dst_path: str,
    width: int = 800,
    height: int = 600,
    background: str = "#FFFFFF"
) -> None:
    """Convert an SVG file to PNG with custom dimensions and background."""
    # Load the SVG document
    svg_doc = SVGDocument(src_path)

    # Prepare save options
    options = ImageSaveOptions()
    options.width = width
    options.height = height
    options.background_color = background

    # Save as PNG
    svg_doc.save(dst_path, options)


if __name__ == "__main__":
    # Example usage
    convert_svg_to_png(
        src_path="YOUR_DIRECTORY/vector.svg",
        dst_path="YOUR_DIRECTORY/vector.png",
        width=1024,
        height=768,
        background="#FFFFFF"
    )
    print("SVG successfully saved as PNG.")
```

Spuštění skriptu vypíše **„SVG úspěšně uloženo jako PNG.“** a vytvoří `vector.png` ve stejné složce.

## Převod SVG na PNG – řešení běžných problémů

### Chybějící soubor nebo neplatná cesta

Pokud `src_path` neexistuje, `SVGDocument` vyvolá `FileNotFoundError`. Zabalte volání do bloku `try/except`, abyste poskytli přátelskou chybovou zprávu:

```python
try:
    svg_doc = SVGDocument(src_path)
except FileNotFoundError:
    raise SystemExit(f"File not found: {src_path}")
```

### Zachování poměru stran

Když je nastavena pouze jedna rozměr (šířka **nebo** výška), knihovna automaticky přepočítá druhý rozměr tak, aby zachovala původní poměr stran. Pokud nastavíte oba rozměry, obrázek se může natáhnout. Zvolte přístup, který odpovídá požadavkům vašeho UI.

### Průhledná pozadí

Pokud originální SVG spoléhá na průhlednost (např. ikony), můžete PNG ponechat průhledný vynecháním `background_color`:

```python
options.background_color = None   # PNG will retain transparency
```

Tato varianta je užitečná, když bude PNG vrstvený nad jinou grafikou.

## Export SVG do PNG – tipy pro výkon

* **Znovu použijte `ImageSaveOptions`** při konverzi mnoha souborů najednou. Vytvoření nového objektu možností pro každý soubor přidává zanedbatelnou zátěž, ale opakované používání zabraňuje opakovanému alokování paměti.
* **Dávkové zpracování**: Procházejte adresář se SVG soubory a pro každý zavolejte `convert_svg_to_png`. Knihovna zpracovává každý soubor nezávisle, takže můžete smyčku paralelizovat pomocí `concurrent.futures.ThreadPoolExecutor` pro rychlejší konverzi na vícejádrových strojích.

```python
import os
from concurrent.futures import ThreadPoolExecutor

svg_folder = "YOUR_DIRECTORY"
png_folder = "YOUR_DIRECTORY/pngs"
os.makedirs(png_folder, exist_ok=True)

def batch_convert(file_name):
    src = os.path.join(svg_folder, file_name)
    dst = os.path.join(png_folder, file_name.replace('.svg', '.png'))
    convert_svg_to_png(src, dst)

with ThreadPoolExecutor(max_workers=8) as executor:
    executor.map(batch_convert, [f for f in os.listdir(svg_folder) if f.endswith('.svg')])
```

## Ověření uložení SVG jako PNG

Po konverzi můžete výstup programově ověřit:

```python
from PIL import Image

with Image.open("YOUR_DIRECTORY/vector.png") as img:
    print(f"PNG size: {img.size}, mode: {img.mode}")
```

Typický výstup:

```
PNG size: (1024, 768), mode: RGBA
```

`mode` `RGBA` potvrzuje, že obrázek obsahuje alfa kanál (průhlednost). Pokud nastavíte barvu pozadí, režim bude `RGB`.

## Závěr

Nyní víte **jak uložit SVG** jako PNG pomocí Pythonu, jak **převést SVG na PNG** a jak **exportovat SVG do PNG** s vlastními rozměry a nastavením pozadí. Kompletní skript demonstruje celý pracovní postup od načtení vektorového SVG souboru až po vytvoření rastrového PNG obrázku.

Dále prozkoumejte související témata, jako je **uložení SVG jako PNG** v dávkovém režimu, použití alternativních knihoven jako **CairoSVG**, nebo generování více‑stránkových PDF ze SVG zdrojů. Experimentujte s různými nastaveními `ImageSaveOptions`, abyste jemně doladili kvalitu, DPI a kompresi pro váš konkrétní případ použití.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [svg na png java – Převod SVG na obrázek pomocí Aspose.HTML pro Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Zobrazit SVG dokument jako PNG v .NET pomocí Aspose.HTML](/html/hindi/net/rendering-html-documents/render-svg-doc-as-png/)
- [Jak nastavit DPI při převodu SVG na PNG pomocí Javy](/html/english/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-with-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}