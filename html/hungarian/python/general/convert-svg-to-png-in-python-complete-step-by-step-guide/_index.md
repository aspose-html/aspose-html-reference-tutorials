---
category: general
date: 2026-06-19
description: Konvertálja az SVG-t PNG-re Pythonban gyorsan és egyszerűen. Tanulja
  meg, hogyan mentse az SVG-t PNG-ként, kezelje az SVG‑PNG átalakítást, és exportálja
  az SVG-t PNG-re egy egyszerű szkript segítségével.
draft: false
keywords:
- convert svg to png
- save svg as png
- svg to png conversion
- svg to png python
- export svg to png
language: hu
og_description: Konvertálja az SVG-t PNG-re Pythonban ezzel a gyakorlati útmutatóval.
  Ismerje meg a teljes SVG‑PNG átalakítási folyamatot, és tanulja meg, hogyan exportálja
  hatékonyan az SVG-t PNG‑be.
og_title: SVG konvertálása PNG-re Pythonban – Teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Convert SVG to PNG in Python quickly and easily. Learn how to save
    SVG as PNG, handle svg to png conversion, and export SVG to PNG with a simple
    script.
  headline: Convert SVG to PNG in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Convert SVG to PNG in Python quickly and easily. Learn how to save
    SVG as PNG, handle svg to png conversion, and export SVG to PNG with a simple
    script.
  name: Convert SVG to PNG in Python – Complete Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - Basic familiarity with pip and
      virtual environments. - An SVG file you want to transform (we’ll use `logo.svg`
      as an example).'
  - name: Why This Approach Works
    text: '- **Explicit I/O handling:** By reading the SVG as bytes, we avoid issues
      with Unicode encodings that sometimes crop up on Windows. - **Custom DPI:**
      Scaling is often required when the target PNG must match a specific pixel density
      (think print vs. screen). - **Optional background:** Some SVGs have '
  - name: Expected Result
    text: '- `output/logo.png` – a 1:1 raster of the original SVG, preserving any
      transparency. - `output/logo_highres.png` – a 300 DPI version with a white background,
      perfect for print.'
  - name: 1. **What if the SVG uses external fonts?**
    text: '`cairosvg` tries to embed referenced fonts, but it only sees files on the
      local filesystem. Copy the font files next to the SVG or embed them directly
      in the SVG with `<style>` tags. Otherwise you’ll get fallback fonts in the PNG.'
  - name: 2. **How do I keep the original aspect ratio when scaling?**
    text: Pass only `dpi` and let Cairo compute the pixel dimensions from the SVG’s
      viewBox. If you need a fixed width/height, calculate the appropriate DPI yourself
      or use the `output_width`/`output_height` arguments provided by `svg2png`.
  - name: 3. **Can I convert large SVGs without exhausting memory?**
    text: Yes. `cairosvg` streams the rasterization, but you should avoid loading
      massive SVGs into memory all at once. Process them one by one, as shown in the
      batch example.
  - name: 4. **Is the conversion thread‑safe?**
    text: The underlying Cairo library is not fully thread‑safe on all platforms.
      If you plan to run conversions in parallel, wrap calls in a multiprocessing
      pool rather than threading.
  - name: What’s Next?
    text: '- Explore **svg to png conversion** with alternative libraries like `svglib`
      + `reportlab` for PDF‑first workflows. - Combine this script with image‑optimization
      tools (e.g., `pngquant`) to shrink file size for the web. - Add a CLI wrapper
      using `argparse` or `click` so you can run `python -m conver'
  type: HowTo
tags:
- Python
- Image Processing
- SVG
title: SVG konvertálása PNG-re Pythonban – Teljes lépésről‑lépésre útmutató
url: /hu/python/general/convert-svg-to-png-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SVG PNG-re konvertálása Pythonban – Teljes lépésről‑lépésre útmutató

Valaha is szükséged volt **convert SVG to PNG**-re, de nem tudtad, melyik könyvtárat válaszd? Nem vagy egyedül – sok fejlesztő szembesül ezzel a problémával, amikor vektorgrafikákat szeretne beágyazni webes eszközökbe vagy helyben generálni bélyegképeket. A jó hír? Néhány Python sorral **save SVG as PNG**-t menthetsz, és a build folyamatod zökkenőmentes marad.

Ebben az útmutatóban egy gyakorlati **svg to png conversion** mutatunk be egy népszerű könyvtár segítségével, áttekintjük a **svg to png python** kód finomságait, és megmutatjuk, hogyan **export SVG to PNG** megfelelő hibakezeléssel. A végére egy újrahasználható függvényt kapsz, amelyet bármely projektbe beilleszthetsz, legyen szó CLI eszközről vagy szerver‑oldali képszolgáltatásról.

## Mit fogsz megtanulni

- A **convert svg to png** Pythonhoz szükséges minimális függőségek.  
- Hogyan töltsünk be egy SVG fájlt, állítsuk be a PNG exportálási opciókat, és írjuk ki a kimeneti képet.  
- Gyakori buktatók (átlátszó háttér, nagy méretek) és azok elkerülése.  
- Egy azonnal futtatható szkript, amelyet testreszabhatsz kötegelt feldolgozáshoz vagy beilleszthetsz egy Flask/Django végponthoz.

### Előfeltételek

- Python 3.8+ telepítve a gépeden.  
- Alapvető ismeretek a pip‑ről és a virtuális környezetekről.  
- Egy SVG fájl, amelyet át szeretnél alakítani (példaként a `logo.svg`-t használjuk).

Ha már megvannak ezek, nagyszerű – merüljünk el benne.

## 1. lépés: A szükséges könyvtár telepítése

A legegyszerűbb módja a **convert SVG to PNG** Pythonban a `cairosvg` csomag használata. Ez a Cairo grafikai könyvtárat csomagolja, és a háttérben kezeli a vektor rasterizálást.

```bash
pip install cairosvg
```

> **Pro tip:** Rögzítsd a verziót (pl. `cairosvg==2.7.0`) a `requirements.txt`‑ben, hogy elkerüld a váratlan hibákat, amikor egy új fő kiadás jelenik meg.

## 2. lépés: Egyszerű konverziós függvény írása

Miután a könyvtár rendelkezésre áll, egy kis segédfüggvényt hozunk létre, amely elvégzi a nehéz munkát. Ez a függvény magába foglalja a **svg to png python** logikát, így könnyen újrahasználható.

```python
# convert_svg_to_png.py
import os
from cairosvg import svg2png

def convert_svg_to_png(
    input_path: str,
    output_path: str,
    dpi: int = 96,
    background_color: str = None,
) -> None:
    """
    Convert an SVG file to a PNG image.

    Parameters
    ----------
    input_path : str
        Path to the source SVG file.
    output_path : str
        Destination path for the generated PNG.
    dpi : int, optional
        Dots per inch for the rasterized image (default: 96).
    background_color : str, optional
        Hex color (e.g., "#FFFFFF") to use as background.
        If None, the SVG's own transparency is preserved.

    Raises
    ------
    FileNotFoundError
        If the input SVG does not exist.
    ValueError
        If the output directory cannot be created.
    """
    # Validate input file
    if not os.path.isfile(input_path):
        raise FileNotFoundError(f"SVG file not found: {input_path}")

    # Ensure output directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Read the SVG content
    with open(input_path, "rb") as svg_file:
        svg_bytes = svg_file.read()

    # Perform the conversion
    svg2png(
        bytestring=svg_bytes,
        write_to=output_path,
        dpi=dpi,
        background_color=background_color,
    )
    print(f"✅ Successfully saved PNG to {output_path}")
```

### Miért működik ez a megközelítés

- **Explicit I/O handling:** Az SVG bájtokként történő olvasásával elkerülhetjük a Unicode kódolási problémákat, amelyek néha Windowson jelentkeznek.  
- **Custom DPI:** A méretezés gyakran szükséges, amikor a cél PNG-nek egy adott képpontsűrűségnek (gondolj nyomtatásra vs. képernyőre) kell megfelelnie.  
- **Optional background:** Néhány SVG átlátszó területekkel rendelkezik; egy hex szín megadása lehetővé teszi, hogy **export SVG to PNG** egy szilárd háttérrel, ami hasznos UI bélyegképekhez.

## 3. lépés: A konverziós szkript futtatása

A függvény készen áll, konvertáljunk egy valós fájlt. Helyezd a `logo.svg`-t egy `assets/` nevű mappába, és futtasd a szkriptet a projekt gyökeréből.

```python
# demo_conversion.py
from convert_svg_to_png import convert_svg_to_png

if __name__ == "__main__":
    INPUT_SVG = "assets/logo.svg"
    OUTPUT_PNG = "output/logo.png"

    # Simple call – defaults keep transparency and 96 DPI
    convert_svg_to_png(INPUT_SVG, OUTPUT_PNG)

    # Example with a white background and higher DPI for sharper output
    convert_svg_to_png(
        INPUT_SVG,
        "output/logo_highres.png",
        dpi=300,
        background_color="#FFFFFF",
    )
```

Futtasd:

```bash
python demo_conversion.py
```

A konzolon látnod kell a fájlok írását megerősítő üzenetet:

```
✅ Successfully saved PNG to output/logo.png
✅ Successfully saved PNG to output/logo_highres.png
```

### Várható eredmény

- `output/logo.png` – az eredeti SVG 1:1 rastere, megőrizve az esetleges átlátszóságot.  
- `output/logo_highres.png` – egy 300 DPI-s változat fehér háttérrel, tökéletes nyomtatáshoz.

![svg png konvertálás példa kimenet](example.png){alt="svg png konvertálás példa kimenet"}

*(A képernyőkép a PNG fájlokat mutatja egy képnézőben megnyitva, megerősítve, hogy a konverzió sikeres volt.)*

## 4. lépés: Tömeges SVG-feldolgozás (opcionális)

Ha egy teljes könyvtár **save SVG as PNG** konvertálására van szükséged, egy rövid ciklus megoldja a feladatot. Ez a kódrészlet a hibakezelés eleganciáját is bemutatja – hasznos, ha néhány SVG hibás lehet.

```python
import glob
from pathlib import Path

def batch_convert(source_dir: str, dest_dir: str, **options):
    svg_paths = glob.glob(os.path.join(source_dir, "*.svg"))
    for svg_path in svg_paths:
        try:
            filename = Path(svg_path).stem + ".png"
            output_path = os.path.join(dest_dir, filename)
            convert_svg_to_png(svg_path, output_path, **options)
        except Exception as e:
            print(f"⚠️  Failed to convert {svg_path}: {e}")

if __name__ == "__main__":
    batch_convert(
        source_dir="assets/",
        dest_dir="output/batch/",
        dpi=150,
        background_color="#F0F0F0",
    )
```

A futtatás `output/batch/` könyvtárat tölti fel PNG-kkel minden `assets/`-beli SVG-hez. Ha egy fájl hibát okoz, a szkript naplózza a hibát és folytatja – nem kell leállítani az egész feladatot.

## Gyakori kérdések és szélhelyzetek

### 1. **Mi van, ha az SVG külső betűtípusokat használ?**  
`cairosvg` megpróbálja beágyazni a hivatkozott betűtípusokat, de csak a helyi fájlrendszeren lévő fájlokat látja. Másold a betűtípus fájlokat az SVG mellé, vagy ágyazd be őket közvetlenül az SVG-be `<style>` címkékkel. Ellenkező esetben a PNG-ben helyettesítő betűtípusok jelennek meg.

### 2. **Hogyan őrizhetem meg az eredeti képarányt méretezéskor?**  
Csak a `dpi`-t add meg, és hagyd, hogy a Cairo a SVG viewBox‑ából számolja ki a pixelméreteket. Ha fix szélesség/magasság szükséges, saját magad számold ki a megfelelő DPI-t, vagy használd a `svg2png` által biztosított `output_width`/`output_height` argumentumokat.

### 3. **Konvertálhatok nagy SVG-ket anélkül, hogy kimeríteném a memóriát?**  
Igen. A `cairosvg` streameli a rasterizálást, de kerülni kell a hatalmas SVG-k egyszerre való betöltését a memóriába. Dolgozd fel őket egyesével, ahogy a tömeges példában is látható.

### 4. **A konvertálás szálbiztos?**  
Az alatta lévő Cairo könyvtár nem teljesen szálbiztos minden platformon. Ha párhuzamosan szeretnél konvertálásokat futtatni, a hívásokat multiprocessz pool‑ba csomagold, ne szálakba.

## Teljesítmény tippek

- **Cache the PNG**: ha az SVG ritkán változik, a PNG gyorsítótárazása megakadályozza a felesleges CPU-ciklusokat minden kérésnél.  
- **Reuse the same DPI**: ugyanazt a DPI-t használva a hívások között elkerülheted az ismétlődő méretezési számításokat.  
- Webszolgáltatások esetén fontold meg, hogy a PNG-t `BytesIO` streamként adod vissza a lemez írása helyett – ez csökkenti az I/O késleltetést.

```python
from io import BytesIO
def convert_svg_to_png_bytes(svg_path: str, dpi: int = 96) -> BytesIO:
    with open(svg_path, "rb") as f:
        svg_bytes = f.read()
    png_bytes = BytesIO()
    svg2png(bytestring=svg_bytes, write_to=png_bytes, dpi=dpi)
    png_bytes.seek(0)
    return png_bytes
```

## Összefoglalás

Minden szükségeset áttekintettük a **convert SVG to PNG** Pythonban:

1. Telepítsd a `cairosvg`‑t.  
2. Írj egy újrahasználható `convert_svg_to_png` függvényt, amely kezeli a DPI‑t, a háttérszíneket és a hibakezelést.  
3. Futtasd a szkriptet egyetlen fájlon vagy kötegelt feldolgozással egy egész mappán.  
4. Kezeld a gyakori sajátosságokat, mint a külső betűtípusok, a képarány megőrzése és a szálbiztonság.

Ezzel a tudással most már **save SVG as PNG** bármely automatizálási folyamatban, web‑API‑ba integrálva, vagy egyszerűen design rendszerhez generálva.

### Mi következik?

- Fedezd fel a **svg to png conversion** alternatív könyvtárakkal, mint a `svglib` + `reportlab` PDF‑első munkafolyamatokhoz.  
- Kombináld ezt a szkriptet képtömörítő eszközökkel (pl. `pngquant`), hogy csökkentsd a fájlméretet a webhez.  
- Adj hozzá egy CLI burkot `argparse` vagy `click` használatával, így a terminálból futtathatod: `python -m convert_svg_to_png INPUT.svg OUTPUT.png`.

Van még kérdésed? Hagyj egy megjegyzést alul, vagy forkold a repót és kísérletezz különböző export beállításokkal. Boldog kódolást!

## Mit érdemes legközelebb megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljesen működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API‑funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [svg to png java – SVG kép konvertálása Aspose.HTML for Java-val](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Render SVG Doc as PNG in .NET with Aspose.HTML](/html/english/net/rendering-html-documents/render-svg-doc-as-png/)
- [svg a png java – SVG átalakítása képpé Aspose.HTML for Java-val](/html/spanish/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}