---
category: general
date: 2026-09-29
description: Hogyan menthetünk SVG-t Python segítségével, és exportálhatjuk PNG-be.
  Tanulja meg, hogyan konvertálhat SVG-t PNG-be finomhangolt beállításokkal percek
  alatt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save svg
- convert svg to png
- save svg as png
- export svg to png
- vector svg to png
language: hu
lastmod: 2026-09-29
og_description: Hogyan menthetünk SVG-t Python használatával, és exportálhatjuk SVG-t
  PNG-be. Kövesd ezt az útmutatót, hogy teljes kontrollal konvertálj SVG-t PNG-be,
  az opciók felett.
og_image_alt: Screenshot of Python code converting a vector SVG file to a PNG image
og_title: Hogyan menthetünk SVG-t PNG-ként Python segítségével – lépésről lépésre
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
title: Hogyan menthetünk SVG-t PNG-ként Python segítségével – teljes útmutató
url: /hu/python/general/how-to-save-svg-as-png-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan mentse el az SVG-t PNG-ként Python segítségével – teljes útmutató

Ha **hogyan mentse el az SVG-t** raszteres képként, ez a tutorial egy azonnal futtatható megoldást mutat be. Megtanulja, hogyan töltsön be egy vektor SVG fájlt, opcionálisan állítsa be a képm mentési beállításokat, és exportálja az eredményt PNG formátumba mindössze három sor kóddal.

Az SVG fájlok PNG‑ként való mentése gyakori, ha grafikákat szeretne beágyazni weboldalakba, előnézeti képeket generálni, vagy raszteres képeket adni gépi tanulási folyamatoknak. Az itt leírt megközelítés Windows, macOS és Linux rendszereken egyaránt működik további natív függőségek nélkül.

## Előfeltételek

Mielőtt elkezdené, győződjön meg róla, hogy rendelkezik:

* Python 3.9 vagy újabb telepítve
* Az `aspose.svg` csomaggal (az hivatalos Aspose SVG for Python via .NET). Telepítse a következővel:

```bash
pip install aspose-svg
```

* Egy érvényes SVG fájllal a lemezen (például `vector.svg`)

Ezek a követelmények biztosítják, hogy a példa önálló legyen, és elkerüljük a külső eszközök, például a CairoSVG használatát.

## Hogyan mentse el az SVG-t Python segítségével

A folyamat lényege három lépés: betöltés, konfigurálás és mentés. Az alábbi szakaszok részletezik az egyes lépéseket.

### 1. lépés: SVG dokumentum betöltése

```python
from aspose.svg import SVGDocument

# Load the SVG file from the local filesystem
svg_doc = SVGDocument("YOUR_DIRECTORY/vector.svg")
```

A `SVGDocument` beolvassa az SVG XML‑t és egy memóriában tárolt reprezentációt hoz létre. A fájl előzetes betöltése kötelező; különben a mentési műveletnek nincs forrásadata.

### 2. lépés: (Opcionális) Képm mentési beállítások létrehozása

```python
from aspose.svg import ImageSaveOptions

# Create default options; you can tweak width, height, and background
options = ImageSaveOptions()
options.width = 800          # Desired output width in pixels
options.height = 600         # Desired output height in pixels
options.background_color = "#FFFFFF"  # Force a white background for transparent SVGs
```

Az `ImageSaveOptions` lehetővé teszi a PNG kimenet finomhangolását. A szélesség és magasság beállítása megőrzi az arányt, hacsak nem adja meg mindkettőt explicit módon. Háttérszín megadása hasznos, ha az eredeti SVG átlátszóságot tartalmaz, de Önnek átlátszatlan PNG‑re van szüksége.

### 3. lépés: SVG mentése PNG-ként

```python
# Export the SVG to a PNG file using the options defined above
svg_doc.save("YOUR_DIRECTORY/vector.png", options)
```

A `save` metódus egy PNG fájlt ír a megadott célútra. Ha kihagyja a `options` argumentumot, a könyvtár az SVG viewBox‑ából származó alapértelmezett méreteket használja.

### Teljes szkript

Az összetevők egyesítése egy teljes, futtatható programot eredményez:

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

A szkript futtatása kiírja a **„SVG successfully saved as PNG.”** üzenetet, és a `vector.png` fájlt ugyanabban a mappában hozza létre.

## SVG konvertálása PNG-re – gyakori buktatók kezelése

### Hiányzó fájl vagy érvénytelen útvonal

Ha a `src_path` nem létezik, a `SVGDocument` `FileNotFoundError`‑t dob. A hívást `try/except` blokkba kell helyezni, hogy barátságos hibaüzenetet adjon:

```python
try:
    svg_doc = SVGDocument(src_path)
except FileNotFoundError:
    raise SystemExit(f"File not found: {src_path}")
```

### Arány megtartása

Ha csak egy dimenzió (szélesség **vagy** magasság) van beállítva, a könyvtár automatikusan skálázza a másik dimenziót az eredeti arány megtartásához. Ha mindkét dimenziót megadja, a kép nyúlhat. Válassza azt a megközelítést, amely megfelel a UI‑követelményeinek.

### Átlátszó háttér

Ha az eredeti SVG átlátszóságra támaszkodik (például ikonok), a PNG‑t átlátszóan tarthatja, ha kihagyja a `background_color` beállítást:

```python
options.background_color = None   # PNG will retain transparency
```

Ez a változat akkor hasznos, ha a PNG-t más grafikákra helyezi rá.

## SVG exportálása PNG-re – teljesítmény tippek

* **Újrahasználja az `ImageSaveOptions`‑t** sok fájl kötegelt konvertálásakor. Új opciós objektum létrehozása minden fájlhoz elhanyagolható, de az újrahasználat elkerüli a többszöri memóriafoglalást.
* **Kötegelt feldolgozás**: Egy SVG‑fájlok könyvtárán iterálva hívja meg a `convert_svg_to_png`‑t minden egyes fájlra. A könyvtár minden fájlt önállóan dolgoz fel, ezért a ciklust párhuzamosíthatja a `concurrent.futures.ThreadPoolExecutor`‑rel a gyorsabb konvertálás érdekében többmagos gépeken.

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

## SVG mentése PNG-ként – ellenőrzés

A konvertálás után programozottan ellenőrizheti a kimenetet:

```python
from PIL import Image

with Image.open("YOUR_DIRECTORY/vector.png") as img:
    print(f"PNG size: {img.size}, mode: {img.mode}")
```

Tipikus kimenet:

```
PNG size: (1024, 768), mode: RGBA
```

A `mode` `RGBA` megerősíti, hogy a kép alfa csatornát (átlátszóságot) tartalmaz. Ha háttérszínt állít be, a mód `RGB` lesz.

## Összegzés

Most már tudja, **hogyan mentse el az SVG-t** PNG‑ként Python használatával, **hogyan konvertálja az SVG‑t PNG‑re**, és **hogyan exportálja az SVG‑t PNG‑re** egyedi méretekkel és háttérkezeléssel. A teljes szkript bemutatja a teljes munkafolyamatot a vektor SVG fájl betöltésétől a raszteres PNG kép előállításáig.

Ezután fedezze fel a kapcsolódó témákat, például a **SVG PNG‑ként való mentését** kötegelt módban, alternatív könyvtárak, például a **CairoSVG** használatát, vagy többoldalas PDF‑ek generálását SVG forrásokból. Kísérletezzen különböző `ImageSaveOptions` beállításokkal a minőség, DPI és tömörítés finomhangolásához saját felhasználási esetéhez.

## Mihez érdemes következőként tanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [svg to png java – SVG kép konvertálása Aspose.HTML for Java segítségével](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [SVG dokumentum PNG-ként való megjelenítése .NET-ben az Aspose.HTML segítségével](/html/hindi/net/rendering-html-documents/render-svg-doc-as-png/)
- [Hogyan állítsuk be a DPI-t SVG PNG-re konvertálásakor Java-val](/html/english/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-with-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}