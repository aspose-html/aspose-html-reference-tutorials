---
category: general
date: 2026-11-17
description: Konvertálja az SVG-t PNG-re Python segítségével néhány sorban. Tanulja
  meg, hogyan mentse el az SVG-t PNG formátumban opcionális konverziós beállításokkal.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert svg to png
- save svg as png
- export svg as png
- svg to raster image
- how to convert svg to png
language: hu
lastmod: 2026-11-17
og_description: Konvertálja az SVG-t PNG-re Pythonban egy tömör példával. Kövesse
  a lépéseket az SVG hatékony PNG-re exportálásához.
og_image_alt: Diagram illustrating convert svg to png workflow in Python
og_title: SVG konvertálása PNG-re Pythonban – gyors útmutató
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: convert svg to png using Python in a few lines. Learn to save SVG as
    PNG with optional conversion settings.
  headline: How to convert SVG to PNG in Python – step‑by‑step guide
  type: TechArticle
tags:
- svg
- png
- python
- image conversion
title: Hogyan konvertáljuk az SVG-t PNG-re Pythonban – lépésről lépésre útmutató
url: /hu/python/general/how-to-convert-svg-to-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan konvertáljunk SVG-t PNG-re Pythonban – lépésről‑lépésre útmutató

Ha **svg-t png-re kell konvertálni**, ez az útmutató egy teljes megoldást mutat, amelyet már ma futtathatsz. Emellett megmutatjuk, hogyan **mentheted el az svg-t png-ként** opcionális méret- és háttérszín beállításokkal.

Vektor SVG fájlokból raszteres képek generálása gyakori, amikor grafikákat szolgáltatsz a böngészőknek, előnézeti képeket (thumbnail) készítesz, vagy képeket ágyazol be PDF-ekbe. A tutorial mindent lefed, az szükséges könyvtár telepítésétől a hiányzó fájlok vagy nagyon nagy SVG-k esetén felmerülő szélhelyzetek kezeléséig.

## Előfeltételek

* Telepített Python 3.8 vagy újabb.
* Hozzáférés egy terminálhoz vagy parancssorhoz.
* A `cairosvg` csomag, amely a **svg to raster image** konverzió nehéz munkáját végzi.

A csomagot egyetlen pip paranccsal telepítheted:

```bash
pip install cairosvg
```

> **Pro tipp:** Használj virtuális környezetet, hogy a függőségek elkülönüljenek a többi projekttől.

## Hogyan konvertáljunk SVG-t PNG-re Pythonban

A folyamat központja három lépésből áll: az SVG betöltése, opcionálisan a konverziós paraméterek módosítása, és a PNG fájl írása. Az alábbi kód mindhárom lépést egy újrahasználható függvényben valósítja meg.

```python
import cairosvg
from pathlib import Path

def convert_svg_to_png(svg_path: str, png_path: str) -> None:
    """
    Convert an SVG file to a PNG raster image.

    Parameters
    ----------
    svg_path : str
        Path to the source SVG file.
    png_path : str
        Destination path for the generated PNG file.
    """
    # Verify that the SVG file exists
    if not Path(svg_path).is_file():
        raise FileNotFoundError(f"SVG file not found: {svg_path}")

    # Perform the conversion using default settings
    cairosvg.svg2png(url=svg_path, write_to=png_path)

# Example usage
if __name__ == "__main__":
    svg_file = "YOUR_DIRECTORY/image.svg"
    png_file = "YOUR_DIRECTORY/image.png"
    convert_svg_to_png(svg_file, png_file)
    print(f"Converted {svg_file} to {png_file}")
```

### Miért működik ez

* `cairosvg.svg2png` beolvassa az SVG fájlt (`url=svg_path`) és PNG fájlt ír (`write_to=png_path`).
* A függvény egyértelmű hibát dob, ha a forrás SVG nem található, ami segít a fájl‑útvonal problémák korai hibakeresésében.
* A konverziós logika függvényben tartása megkönnyíti az újbóli felhasználást több szkriptben vagy nagyobb alkalmazásokba való integrálást.

## Opcionális: a konverzió finomhangolása

Ha konkrét kimeneti méretre vagy más háttérre van szükséged, a `cairosvg.svg2png` további argumentumokat is elfogad. Az alábbi változat 300 px szélességet és fehér hátteret állít be.

```python
def convert_svg_to_png_custom(svg_path: str, png_path: str,
                              width: int = 300,
                              background_color: str = "white") -> None:
    """
    Convert an SVG to PNG with custom dimensions and background.

    Parameters
    ----------
    width : int
        Desired width of the PNG in pixels; height scales proportionally.
    background_color : str
        Hex or named color for the PNG background.
    """
    if not Path(svg_path).is_file():
        raise FileNotFoundError(f"SVG file not found: {svg_path}")

    cairosvg.svg2png(
        url=svg_path,
        write_to=png_path,
        output_width=width,
        background_color=background_color
    )
```

Ezt a függvényt ugyanúgy hívhatod, mint az alapverziót, megadva a kívánt szélességet vagy színt.

## Gyakori kérdések és szélhelyzetek

**Mi van, ha az SVG külső betűtípusokat tartalmaz?**  
`cairosvg` automatikusan beágyazza a hivatkozott betűtípusokat, de a betűtípus fájloknak elérhetőnek kell lenniük az SVG helyétől. Helyezd a betűtípus fájlokat az SVG mellé, vagy használj abszolút URL-eket.

**Hogyan kezeljem a nagyon nagy SVG-ket?**  
A nagy fájlok jelentős memóriát fogyaszthatnak. Az SVG tartalmat streamelheted a lemezről betöltés helyett:

```python
with open(svg_path, "rb") as svg_stream:
    cairosvg.svg2png(file_obj=svg_stream, write_to=png_path)
```

**Konvertálhatok több fájlt egyszerre?**  
A konverzióhívást egy ciklusba helyezheted, és a `Path.glob("*.svg")` segítségével felfedezheted a könyvtárban lévő összes SVG-t.

## Várt kimenet

A példascript futtatása egyetlen sort ír ki, amely megerősíti a konverziót:

```
Converted YOUR_DIRECTORY/image.svg to YOUR_DIRECTORY/image.png
```

Az eredményül kapott `image.png` fájl ugyanabban a könyvtárban található, és bármely képnézővel megnyitható.

## Következtetés

Most már tudod, hogyan **convert svg to png** Pythonban, hogyan **save svg as png**, és hogyan **export svg as png** egyedi méretekkel. Ugyanaz a megközelítés minden SVG fájlra működik, a vektoros grafikákat **svg to raster image** formátummá alakítva, amely alkalmas weboldalak, jelentések vagy előnézeti képek (thumbnails) számára.

A következő lépések lehetnek:

* A `export svg as png` paraméterek felfedezése DPI szabályozáshoz.
* A konverziós függvény integrálása Flask vagy Django végpontra, hogy valós időben képgenerálást biztosítson.
* A másodlagos kulcsszó **how to convert svg to png** használata fejlettebb felhasználási esetek kereséséhez, például kötegelt feldolgozás vagy CI/CD pipeline-ok.

Nyugodtan kísérletezz különböző beállításokkal, és oszd meg az eredményeidet a közösséggel!

## Mit érdemes legközelebb megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API funkciókat, és alternatív megvalósítási megközelítéseket fedezhess fel saját projektjeidben.

- [SVG konvertálása PNG-re Pythonban – Magas felbontású export útmutató](/html/english/python/general/convert-svg-to-png-in-python-high-resolution-export-guide/)
- [SVG konvertálása PNG-re Pythonban Aspose.HTML használatával](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)
- [SVG konvertálása PNG-re Pythonban – Teljes lépésről‑lépésre útmutató](/html/english/python/general/convert-svg-to-png-in-python-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}