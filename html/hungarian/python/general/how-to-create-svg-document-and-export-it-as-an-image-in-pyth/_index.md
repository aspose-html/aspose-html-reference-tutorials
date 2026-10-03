---
category: general
date: 2026-10-02
description: Tanulja meg, hogyan hozhat létre SVG-dokumentumot Pythonban, hogyan mentheti
  el az SVG-t fájlba, és hogyan exportálhat SVG-képet egy rövid, teljes szkripttel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG to file
- how to generate SVG
- export SVG image
- SVG Python tutorial
language: hu
lastmod: 2026-10-02
og_description: Készíts SVG dokumentumot Pythonban, és exportáld az SVG képet ezzel
  a gyakorlati útmutatóval. Kövesd a szkriptet, mentsd el az SVG‑t fájlba, és azonnal
  használd újra a vektorgrafikát.
og_image_alt: Screenshot of a Python script that creates an SVG document
og_title: SVG dokumentum létrehozása Pythonban – lépésről lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-10-02'
  description: Learn how to create SVG document in Python, save SVG to file, and export
    SVG image with a short, complete script.
  headline: How to create SVG document and export it as an image in Python
  type: TechArticle
tags:
- SVG
- Python
- graphics
title: Hogyan lehet SVG dokumentumot létrehozni és képként exportálni Pythonban
url: /hu/python/general/how-to-create-svg-document-and-export-it-as-an-image-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan hozhatunk létre SVG dokumentumot, és exportálhatjuk képként Pythonban

Ha programozott módon **create SVG document**-ot kell létrehoznod, ez a bemutató pontosan megmutatja, hogyan teheted ezt Pythonban. Egy teljes szkriptet láthatsz, amely egy egyszerű kört épít, elmenti az SVG-t fájlba, és egy exportálható SVG képet hoz létre, amelyet bárhol beágyazhatsz.

A kódból történő skálázható vektorgrafika generálása megszünteti a kézi rajzolás szükségességét egy GUI szerkesztőben. A útmutató végére képes leszel az SVG létrehozását integrálni adat‑vizualizációs folyamatokba, automatizált jelentéskészítő rendszerekbe, vagy bármely olyan projektbe, amely éles, felbontás‑független grafikát igényel.

## Prerequisites

Mielőtt elkezdenéd, győződj meg róla, hogy a következők telepítve vannak:

- Python 3.8 vagy újabb
- A `svgwrite` könyvtár (telepítés: `pip install svgwrite`)
- Írási jogosultság a könyvtárban, ahová az SVG-t menteni fogod

Ezek a követelmények biztosítják, hogy a példa könnyű maradjon, és a legtöbb környezetben kompatibilis legyen.

## Step 1: Install and import the SVG library

Az első lépés a harmadik féltől származó könyvtár hozzáadása, amely kényelmes API‑t biztosít az SVG létrehozásához.

```python
# Install the library (run once in your terminal)
# pip install svgwrite

import svgwrite  # Provides the SVGDocument class and element helpers
```

A `svgwrite` elrejti az SVG fájl XML‑szerkezetét, így a geometriára koncentrálhatsz a nyers markup helyett.

## Step 2: Create an SVG document object

Most már **create SVG document**-ot hozhatsz létre a `svgwrite.Drawing` példányosításával. Ez az objektum képviseli a gyökér `<svg>` elemet, és tartalmazza az összes későbbi alakzatot.

```python
# Step 2: Initialize the SVG document
dwg = svgwrite.Drawing(
    filename="circle.svg",     # Desired output file name
    size=("100px", "100px"),   # Width and height of the canvas
    viewBox=("0 0 100 100")    # Coordinate system for drawing
)
```

A `size` argumentum határozza meg a megjelenített pixelméreteket, míg a `viewBox` egy koordináta‑rendszert állít fel, amely megfelel a később definiált geometriának.

## Step 3: Add a circle element

A kör középpontját (`cx`, `cy`) és a sugarát (`r`) határozza meg. Használd a `circle` segédfüggvényt ezeknek az attribútumoknak a beállításához.

```python
# Step 3: Create a <circle> element
circle = dwg.circle(
    center=("50", "50"),   # cx = 50, cy = 50
    r="40",                # radius = 40
    fill="lightcoral",     # Fill color for visual clarity
    stroke="black",        # Outline color
    stroke_width="2"
)

# Append the circle to the SVG root
dwg.add(circle)
```

A kör a 100 × 100‑as vászon közepén helyezkedik el, mindkét oldalon 10‑pixel margóval. Állítsd be a `fill` és `stroke` értékeket a tervezési nyelvednek megfelelően.

## Step 4: Save the SVG to file

Miután a grafika összeállt, **save SVG to file**-t használhatsz a `save` metódussal. Ez jól formált XML‑t ír, amelyet a böngészők és vektorszerkesztők is értenek.

```python
# Step 4: Persist the SVG document
dwg.save()
print("SVG file saved as circle.svg")
```

A `circle.svg` fájl most a jelenlegi munkakönyvtárban található. Megnyithatod egy webböngészőben, az Inkscape‑ben vagy bármely SVG‑t támogató eszközben.

## Step 5: Verify the exported SVG image

Nyisd meg a mentett fájlt egy böngészőben, hogy ellenőrizd a kimenetet. Középen egy körnek kell látszania a megadott színekkel. A nyers XML így néz ki:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg width="100px" height="100px" viewBox="0 0 100 100"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40"
          fill="lightcoral" stroke="black" stroke-width="2"/>
</svg>
```

Mivel az SVG vektor‑alapú, a képet minőségromlás nélkül skálázhatod, ami ideálissá teszi reszponzív webdesignokhoz vagy nagy felbontású nyomtatáshoz.

## Pro tip: Export SVG as PNG or JPEG

Ha raszteres változatra van szükséged, kombináld az SVG fájlt egy konverziós eszközzel, például a **CairoSVG**‑vel:

```python
# Optional: Convert SVG to PNG
# pip install cairosvg
import cairosvg

cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

Ez a lépés bemutatja a **export SVG image**-t bitmap formátumba, ami hasznos, ha a downstream rendszerek nem képesek közvetlenül SVG‑t renderelni.

## Common variations and edge cases

| Variation | How to handle |
|-----------|---------------|
| Multiple shapes | Hívj `dwg.add()`‑t minden új elemhez (rect, line, path). |
| Dynamic dimensions | Számold ki a `size` és `viewBox` értékeket adatból, mielőtt a `Drawing`‑t létrehoznád. |
| Text labels | Használd `dwg.text("Label", insert=("10", "20"))`‑t, és stílusozd `font_size`‑szel és `fill`‑el. |
| Re‑using the document | Tartsd a `Drawing` objektumot memóriában, és hívd a `save()`‑t, amikor friss fájlra van szükség. |
| Large files | Streameld a kimenetet a `dwg.tostring()`‑val, és írd egy fájlobjektumba manuálisan, hogy elkerüld a memória‑spike‑eket. |

Ezeknek a forgatókönyveknek a kezelése biztosítja, hogy a **how to generate SVG** szkripted a egyszerű ikonoktól a komplex diagramokig skálázható legyen.

## Full script recap

Az alábbiakban a teljes, futtatható példát láthatod, amely tartalmazza az összes lépést és az opcionális konverziót:

```python
# Full SVG creation script – create SVG document, save SVG to file, export SVG image
import svgwrite
import cairosvg  # Optional, only needed for PNG conversion

# Initialize the drawing (SVG document)
dwg = svgwrite.Drawing(
    filename="circle.svg",
    size=("100px", "100px"),
    viewBox=("0 0 100 100")
)

# Define a circle element
circle = dwg.circle(
    center=("50", "50"),
    r="40",
    fill="lightcoral",
    stroke="black",
    stroke_width="2"
)

# Add the circle to the document
dwg.add(circle)

# Save the SVG file
dwg.save()
print("SVG file saved as circle.svg")

# Optional: convert SVG to PNG (export SVG image)
cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

A szkript futtatása `circle.svg`‑t és, ha a `cairosvg` telepítve van, `circle.png`‑t hoz létre. Mindkét fájl készen áll a weboldalakba, jelentésekbe vagy további feldolgozásba való beillesztésre.

## Conclusion

Most már tudod, hogyan **create SVG document**-ot készíts Pythonban, hogyan **save SVG to file**, és hogyan **export SVG image**-et használhatsz szélesebb körben. A példa lefedi a legfontosabb API‑hívásokat, elmagyarázza, miért fontos minden egyes lépés, és kiterjesztéseket kínál összetettebb grafikákhoz.

Ezután fedezd fel a további **SVG Python tutorial** témákat, például útvonalak rajzolását, gradientek alkalmazását és elemek animálását. Ezeknek a technikáknak az integrálásával dinamikus, adat‑vezérelt vektorgrafikákat generálhatsz közvetlenül Python‑alkalmazásaidból. Boldog kódolást!

## What Should You Learn Next?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek az API további funkcióinak elsajátításában és alternatív megvalósítási megközelítések felfedezésében a saját projektjeidben.

- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}