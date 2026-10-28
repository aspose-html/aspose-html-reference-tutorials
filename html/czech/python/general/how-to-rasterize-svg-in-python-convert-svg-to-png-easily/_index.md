---
category: general
date: 2026-10-28
description: Naučte se rasterizovat SVG v Pythonu a převést SVG na PNG pomocí jednoduchého
  skriptu s využitím CairoSVG. Uložte SVG jako PNG během několika sekund.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to rasterize svg
- convert svg to png
- save svg as png
- svg to png python
- export svg as png
language: cs
lastmod: 2026-10-28
og_description: 'Jak rasterizovat SVG v Pythonu: tento průvodce vám ukáže, jak převést
  SVG na PNG pomocí CairoSVG, zahrnující instalaci, kód a řešení problémů.'
og_image_alt: Screenshot of Python code that rasterizes SVG to PNG
og_title: Jak rasterizovat SVG v Pythonu – rychlý průvodce převodem SVG na PNG
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to rasterize SVG in Python and convert SVG to PNG with a
    simple script using CairoSVG. Save SVG as PNG in seconds.
  headline: How to rasterize SVG in Python – convert SVG to PNG easily
  type: TechArticle
- description: Learn how to rasterize SVG in Python and convert SVG to PNG with a
    simple script using CairoSVG. Save SVG as PNG in seconds.
  name: How to rasterize SVG in Python – convert SVG to PNG easily
  steps:
  - name: Why CairoSVG?
    text: '- **Pure Python**: No need for external command‑line tools once the package
      is installed. - **SVG‑compliant**: Supports most SVG 1.1 features, including
      gradients, masks, and text. - **Flexible output**: Besides PNG, you can export
      to PDF, PS, or even raw bytes.'
  - name: Step‑by‑step breakdown
    text: 1. **Install the library** – `pip install cairosvg` pulls in the compiled
      Cairo bindings. 2. **Import the module** – `import cairosvg` gives you access
      to the `svg2png` helper. 3. **Call `svg2png`** – Pass the SVG file path (or
      a URL) and the destination PNG path. Optional `output_width`, `output_he
  - name: Edge cases you might encounter
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | **Large SVG (megapixel dimensions)** | Increase `dpi` or set explicit `output_width`/`output_height`
      to avoid memory spikes. | | **Missing fonts** | Install the required fonts on
      the system or em'
  type: HowTo
tags:
- svg
- python
- image processing
- cairosvg
title: Jak rasterizovat SVG v Pythonu – snadno převést SVG na PNG
url: /cs/python/general/how-to-rasterize-svg-in-python-convert-svg-to-png-easily/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak rasterizovat SVG v Pythonu – snadno převést SVG na PNG

Pokud potřebujete **how to rasterize svg** pro webovou aplikaci, zprávu nebo automatizovaný build, tento průvodce vám poskytne připravené řešení. Uvidíte, jak **convert svg to png** pomocí několika řádků Pythonu, a výsledek je ostrý PNG, který můžete okamžitě uložit nebo naservírovat.

Tutoriál pokrývá vše od instalace potřebné knihovny až po řešení okrajových případů, jako jsou velké soubory nebo vlastní nastavení DPI. Na konci budete schopni **save svg as png**, **export svg as png**, a integrovat tento proces do jakéhokoli Python workflow.

## Co budete potřebovat

- Python 3.8+ (kód funguje na 3.9, 3.10 a novějších)
- `pip` pro instalaci balíčků
- Lokální SVG soubor (např. `logo.svg`), který chcete rasterizovat
- Volitelně: virtuální prostředí pro čistou správu závislostí

> **Tip:** Použití virtuálního prostředí (`python -m venv .venv`) izoluje závislost CairoSVG od vašich globálních Python balíčků.

## Jak rasterizovat SVG v Pythonu

Nejjednodušší způsob, jak **how to rasterize svg**, je pomocí knihovny **CairoSVG**. CairoSVG čte SVG XML, vykresluje jej pomocí grafického enginu Cairo a zapisuje rastrový obrázek do PNG, PDF nebo jiných bitmapových formátů.

```bash
# Install CairoSVG and its binary dependencies
pip install cairosvg
```

```python
# rasterize_svg.py
import sys
from pathlib import Path
import cairosvg

def rasterize_svg(input_path: str, output_path: str,
                  width: int | None = None,
                  height: int | None = None,
                  dpi: int = 96) -> None:
    """
    Convert an SVG file to a PNG image.

    Parameters
    ----------
    input_path : str
        Path to the source SVG file.
    output_path : str
        Destination path for the PNG file.
    width : int | None
        Desired output width in pixels (maintains aspect ratio if height is None).
    height : int | None
        Desired output height in pixels (maintains aspect ratio if width is None).
    dpi : int
        Dots per inch for the rasterization. Higher DPI yields larger files but more detail.
    """
    try:
        # CairoSVG can read from a file path directly
        cairosvg.svg2png(url=Path(input_path).as_uri(),
                         write_to=output_path,
                         output_width=width,
                         output_height=height,
                         dpi=dpi)
        print(f"✅ Successfully saved PNG to {output_path}")
    except Exception as e:
        print(f"❌ Failed to rasterize {input_path}: {e}", file=sys.stderr)
        raise

if __name__ == "__main__":
    # Example usage:
    # python rasterize_svg.py ./assets/logo.svg ./output/logo.png 300 300
    if len(sys.argv) < 3:
        print("Usage: python rasterize_svg.py <input_svg> <output_png> [width] [height] [dpi]")
        sys.exit(1)

    input_svg = sys.argv[1]
    output_png = sys.argv[2]
    w = int(sys.argv[3]) if len(sys.argv) > 3 else None
    h = int(sys.argv[4]) if len(sys.argv) > 4 else None
    d = int(sys.argv[5]) if len(sys.argv) > 5 else 96

    rasterize_svg(input_svg, output_png, width=w, height=h, dpi=d)
```

### Proč CairoSVG?

- **Pure Python**: Není potřeba žádné externí příkazové nástroje po instalaci balíčku.
- **SVG‑compliant**: Podporuje většinu funkcí SVG 1.1, včetně gradientů, masek a textu.
- **Flexible output**: Kromě PNG můžete exportovat do PDF, PS nebo dokonce surových bajtů.

### Postupný rozpis

1. **Install the library** – `pip install cairosvg` stáhne a nainstaluje kompilované vazby Cairo.  
2. **Import the module** – `import cairosvg` vám poskytne přístup k pomocné funkci `svg2png`.  
3. **Call `svg2png`** – Předá cestu k SVG souboru (nebo URL) a cílovou cestu PNG. Volitelné `output_width`, `output_height` a `dpi` vám umožní řídit velikost a rozlišení.  
4. **Handle errors** – Blok `try/except` vypíše srozumitelnou zprávu, pokud je SVG poškozené nebo je výstupní adresář nezapisovatelný.

## Převod SVG na PNG pomocí CairoSVG

Pokud potřebujete jen jednorázový řádek pro rychlý převod, následující úryvek provede úkol bez obalové funkce:

```python
import cairosvg

cairosvg.svg2png(url="logo.svg", write_to="logo.png")
```

Toto je nejstručnější ukázka **convert svg to png**. Načte `logo.svg` ze současného adresáře a zapíše `logo.png` vedle něj.

## Uložení SVG jako PNG – ověření výsledku

Po spuštění skriptu byste měli v cílové cestě vidět soubor PNG. Otevřete jej libovolným prohlížečem obrázků pro potvrzení:

```bash
# Linux/macOS
xdg-open ./output/logo.png   # or open on macOS
# Windows
start ./output/logo.png
```

Pokud PNG vypadá rozmazaně, zvyšte argument `dpi` (např. `dpi=300`) pro vytvoření vyššího rozlišení rastru.

## Export SVG jako PNG v různých formátech

CairoSVG může také výstupem být **PDF**, **PostScript** nebo surové **PNG bajty**. Níže je příklad exportu do objektu `BytesIO`, když potřebujete obrázek v paměti (např. pro Flask odpověď):

```python
import io
import cairosvg

svg_path = "logo.svg"
png_bytes = io.BytesIO()
cairosvg.svg2png(url=Path(svg_path).as_uri(), write_to=png_bytes)
png_bytes.seek(0)  # Ready for sending over HTTP
```

### Okrajové případy, na které můžete narazit

| Situation                               | Recommended handling |
|----------------------------------------|----------------------|
| **Velké SVG (megapixelové rozměry)**   | Zvyšte `dpi` nebo nastavte explicitní `output_width`/`output_height`, aby se předešlo špičkám v paměti. |
| **Chybějící fonty**                    | Nainstalujte požadované fonty do systému nebo je vložte do SVG pomocí `<style>` tagů. |
| **Problémy s průhledností**            | PNG standardně zachovává alfa kanál; pokud potřebujete pevné pozadí, předávejte `background_color="#FFFFFF"` do `svg2png`. |
| **Dávkové zpracování**                 | Procházejte adresář SVG souborů a pro každý soubor zavolejte `rasterize_svg`. |

## Kompletní funkční příklad

Níže je minimální, samostatný skript, který můžete zkopírovat a vložit do souboru pojmenovaného `svg_to_png.py` a spustit okamžitě.

```python
# svg_to_png.py
import cairosvg
from pathlib import Path

def main():
    src = Path("example.svg")
    dst = Path("example.png")
    if not src.is_file():
        raise FileNotFoundError(f"Source SVG not found: {src}")

    # Convert with default DPI (96) and keep original dimensions
    cairosvg.svg2png(url=src.as_uri(), write_to=dst)
    print(f"✅ {src.name} → {dst.name} created successfully.")

if __name__ == "__main__":
    main()
```

Running `python svg_to_png

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohly ovládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak rasterizovat SVG v Pythonu – Kompletní průvodce](/html/english/python/general/how-to-rasterize-svg-in-python-complete-guide/)
- [Převod SVG na PNG v Pythonu – Průvodce exportem ve vysokém rozlišení](/html/english/python/general/convert-svg-to-png-in-python-high-resolution-export-guide/)
- [Vytvoření SVG dokumentu v Pythonu – Průvodce převodem SVG na PNG](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}