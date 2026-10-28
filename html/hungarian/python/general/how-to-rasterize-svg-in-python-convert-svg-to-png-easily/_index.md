---
category: general
date: 2026-10-28
description: Tanulja meg, hogyan rasterizálhatja az SVG-t Pythonban, és konvertálhatja
  SVG‑t PNG‑re egy egyszerű CairoSVG‑es szkript segítségével. Mentse el az SVG‑t PNG‑ként
  néhány másodperc alatt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to rasterize svg
- convert svg to png
- save svg as png
- svg to png python
- export svg as png
language: hu
lastmod: 2026-10-28
og_description: 'Hogyan rasterizáljunk SVG-t Pythonban: ez az útmutató megmutatja,
  hogyan konvertálhatjuk az SVG-t PNG-re a CairoSVG használatával, bemutatva a telepítést,
  a kódot és a hibaelhárítást.'
og_image_alt: Screenshot of Python code that rasterizes SVG to PNG
og_title: Hogyan rasterizáljunk SVG-t Pythonban – gyors SVG‑PNG útmutató
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
title: Hogyan rasterizáljuk az SVG-t Pythonban – SVG egyszerű konvertálása PNG-re
url: /hu/python/general/how-to-rasterize-svg-in-python-convert-svg-to-png-easily/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan rasterizáljunk SVG-t Pythonban – konvertáljuk az SVG-t PNG-re könnyedén

Ha **hogyan rasterizáljunk SVG-t** kell egy web‑app, egy jelentés vagy egy automatizált build számára, ez az útmutató egy készen‑álló megoldást nyújt. Megmutatjuk, hogyan **konvertálhatod az SVG-t PNG-re** néhány Python sorral, és az eredmény egy éles PNG, amelyet azonnal tárolhatsz vagy kiszolgálhatsz.

Az útmutató mindent lefed a szükséges könyvtár telepítésétől a nagy fájlok vagy egyedi DPI beállítások kezeléséig. A végére képes leszel **svg mentésére png‑ként**, **svg exportálására png‑ként**, és a folyamat beillesztésére bármely Python munkafolyamatba.

## Amire szükséged lesz

- Python 3.8+ (a kód működik 3.9, 3.10 és újabb verziókon)
- `pip` a csomagok telepítéséhez
- Egy helyi SVG fájl (pl. `logo.svg`), amelyet rasterizálni szeretnél
- Opcionális: virtuális környezet a tiszta függőségkezeléshez

> **Pro tip:** Egy virtuális környezet (`python -m venv .venv`) használata elkülöníti a CairoSVG függőséget a globális Python csomagjaidtól.

## Hogyan rasterizáljunk SVG-t Pythonban

A legegyszerűbb módja a **hogyan rasterizáljunk SVG-t** a **CairoSVG** könyvtárral. A CairoSVG beolvassa az SVG XML‑t, a Cairo grafikai motorral rendereli, és a raszteres képet PNG‑re, PDF‑re vagy más bitmap formátumokra írja.

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

### Miért a CairoSVG?

- **Pure Python**: Nincs szükség külső parancssori eszközökre, amint a csomag telepítve van.
- **SVG‑compliant**: Támogatja a legtöbb SVG 1.1 funkciót, beleértve a gradienteket, maszkokat és a szöveget.
- **Flexible output**: A PNG‑en kívül exportálhatsz PDF‑re, PS‑re vagy akár nyers bájtokra is.

### Lépésről‑lépésre bontás

1. **Install the library** – `pip install cairosvg` letölti a lefordított Cairo kötéseket.
2. **Import the module** – `import cairosvg` hozzáférést biztosít a `svg2png` segédfüggvényhez.
3. **Call `svg2png`** – Add meg az SVG fájl útvonalát (vagy egy URL‑t) és a cél PNG útvonalát. Az opcionális `output_width`, `output_height` és `dpi` paraméterekkel szabályozhatod a méretet és a felbontást.
4. **Handle errors** – A `try/except` blokk egyértelmű üzenetet ír ki, ha az SVG hibás vagy a kimeneti könyvtár nem írható.

## SVG konvertálása PNG-re a CairoSVG-vel

Ha csak egy egy‑soros megoldásra van szükséged a gyors konvertáláshoz, az alábbi kódrészlet elvégzi a feladatot a wrapper függvény nélkül:

```python
import cairosvg

cairosvg.svg2png(url="logo.svg", write_to="logo.png")
```

Ez a legrövidebb illusztrációja a **convert svg to png** műveletnek. A `logo.svg`‑t a jelenlegi könyvtárból olvassa be, és a `logo.png`‑t ugyanabba a könyvtárba írja.

## SVG mentése PNG-ként – ellenőrizd az eredményt

A szkript futtatása után a megadott útvonalon PNG fájlt kell látnod. Nyisd meg bármely képnéző programmal a megerősítéshez:

```bash
# Linux/macOS
xdg-open ./output/logo.png   # or open on macOS
# Windows
start ./output/logo.png
```

Ha a PNG elmosódottnak tűnik, növeld a `dpi` argumentumot (pl. `dpi=300`), hogy nagyobb felbontású rasztert generálj.

## SVG exportálása PNG-ként különböző formátumokban

A CairoSVG képes **PDF**, **PostScript** vagy nyers **PNG bytes** kimenetre is. Az alábbi példa egy `BytesIO` objektumba exportál, amikor a képre memóriában van szükség (pl. Flask válaszhoz):

```python
import io
import cairosvg

svg_path = "logo.svg"
png_bytes = io.BytesIO()
cairosvg.svg2png(url=Path(svg_path).as_uri(), write_to=png_bytes)
png_bytes.seek(0)  # Ready for sending over HTTP
```

### Olyan szélhelyzetek, amelyekkel találkozhatsz

| Situation                               | Recommended handling |
|----------------------------------------|----------------------|
| **Large SVG (megapixel dimensions)**   | Növeld a `dpi`‑t vagy állíts be explicit `output_width`/`output_height` értékeket a memóriahasználat csökkentéséhez. |
| **Missing fonts**                      | Telepítsd a szükséges betűtípusokat a rendszerre, vagy ágyazd be őket az SVG‑be `<style>` tagekkel. |
| **Transparency issues**                | A PNG alapértelmezés szerint megőrzi az alfát; ha szilárd háttérre van szükséged, add meg a `background_color="#FFFFFF"` paramétert a `svg2png`‑nek. |
| **Batch processing**                   | Iterálj egy SVG‑könyvtáron, és hívd meg a `rasterize_svg`‑t minden egyes fájlra. |

## Teljes működő példa

Az alábbi minimális, önálló szkriptet másold be egy `svg_to_png.py` nevű fájlba, és futtasd azonnal.

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


## Mit érdemes legközelebb megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [How to Rasterize SVG in Python – Complete Guide](/html/english/python/general/how-to-rasterize-svg-in-python-complete-guide/)
- [Convert SVG to PNG in Python – High‑Resolution Export Guide](/html/english/python/general/convert-svg-to-png-in-python-high-resolution-export-guide/)
- [Create SVG Document in Python – Convert SVG to PNG Guide](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}