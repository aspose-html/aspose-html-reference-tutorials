---
category: general
date: 2026-11-27
description: Készíts SVG dokumentumot és mentsd el az SVG fájlt Python segítségével.
  Tanuld meg, hogyan exportálj vektort SVG formátumba, és gyorsan generálj SVG képet.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG file
- export vector as SVG
- save SVG image
- how to create SVG
language: hu
lastmod: 2026-11-27
og_description: Készíts SVG dokumentumot és mentsd el az SVG fájlt Python segítségével.
  Ez az útmutató megmutatja, hogyan exportálj vektort SVG formátumba, és hogyan állíts
  elő SVG képet percek alatt.
og_image_alt: Screenshot of a red circle saved as an SVG document
og_title: SVG dokumentum létrehozása és SVG fájl mentése Python használatával
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  headline: Create SVG document and save SVG file with Python
  type: TechArticle
- description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  name: Create SVG document and save SVG file with Python
  steps:
  - name: Expected output
    text: 'The resulting `circle.svg` contains:'
  - name: Exporting more complex vectors
    text: 'If you need to **export vector as SVG** for multi‑shape illustrations,
      simply repeat the `dwg.add()` pattern with other primitives (`rect`, `line`,
      `path`, etc.). For example:'
  - name: Handling Unicode and text
    text: "SVG supports text elements with full Unicode support. Use `dwg.text(\"Hello,
      \U0001F30D\", insert=(5, 95), fill=\"black\")` to embed multilingual labels."
  - name: Saving to a different location
    text: 'When **save SVG image** to a user‑specified folder, validate the path to
      avoid permission errors:'
  - name: Minifying the output
    text: 'For production pipelines, you might want a smaller file size. Pass `pretty=False`
      to `dwg.tostring()` and write the result manually:'
  type: HowTo
tags:
- SVG
- Python
- Vector graphics
title: SVG dokumentum létrehozása és SVG fájl mentése Python segítségével
url: /hu/python/general/create-svg-document-and-save-svg-file-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SVG dokumentum létrehozása és SVG fájl mentése Python segítségével

Ha **SVG dokumentumot** szeretnél a semmiből létrehozni, ez az útmutató végigvezet a teljes folyamaton. Megmutatjuk, hogyan **mentheted el az SVG fájlt** a lemezen, exportálhatod a vektort SVG‑ként, és néhány sor kóddal egy használatra kész SVG képet kapsz.

A programozottan generált méretezhető grafikák hasznosak jelentésekhez, UI ikonokhoz, vagy bármilyen helyzetben, ahol felbontás‑független képekre van szükség. A tutorial végére képes leszel megválaszolni a „**how to create SVG**?” kérdést egyszerű alakzatok esetén, és kiterjeszteni a mintát összetett vektor műalkotásokra.

## Amire szükséged lesz

- Python 3.8 vagy újabb  
- A `svgwrite` csomag (a `pip`‑en keresztül telepíthető)  
- Egy írható könyvtár a kimeneti fájl számára  

Nem szükséges külső grafikus szerkesztő; minden a parancssorból fut.

## 1. lépés: A `svgwrite` könyvtár telepítése

`svgwrite` tiszta, Python‑szerű API‑t biztosít az SVG markup felépítéséhez. Telepítsd egyszer a következővel:

```bash
pip install svgwrite
```

> **Pro tipp:** Használj virtuális környezetet (`python -m venv .venv`), hogy a függőségek izoláltak maradjanak.

## 2. lépés: SVG dokumentum létrehozása

Most ténylegesen **SVG dokumentum** objektumokat hozunk létre. A `Drawing` osztály a gyökér `<svg>` elemet képviseli, és automatikusan kezeli a névtereket.

```python
import pathlib
import svgwrite

# Define where the file will be saved
output_path = pathlib.Path("output/circle.svg")
output_path.parent.mkdir(parents=True, exist_ok=True)

# Initialize a new SVG document with a 100×100 viewport
dwg = svgwrite.Drawing(
    filename=str(output_path),
    size=("100px", "100px"),
    profile="tiny"  # tiny profile keeps the file lightweight
)
```

A `Drawing` példány az összes további SVG művelet kiindulópontja. A `size` megadásával beállítjuk a vászon méreteit, ami befolyásolja, hogyan jelenítik meg a böngészők a képet.

## 3. lépés: Piros kör elem hozzáadása

Alakzatok hozzáadása egyszerű. A `circle` metódus egy `<circle>` elemet hoz létre; ezt ezután a gyökérhez csatoljuk.

```python
# Create a red circle with radius 40 centered at (50, 50)
circle = dwg.circle(
    center=(50, 50),
    r=40,
    fill="red"
)

# Append the circle to the SVG root
dwg.add(circle)
```

Miért választunk kört: a körök vektor primitívek, amelyek a skálázhatóságot minőségvesztés nélkül mutatják be, így az output ideális a **export vector as SVG** munkafolyamatok teszteléséhez.

## 4. lépés: SVG fájl mentése

Végül írjuk a markupot a lemezre. Ez a lépés teljesíti a **save SVG file** követelményt, és egy olyan fájlt hoz létre, amelyet bármely böngésző vagy vektorszerkesztő megnyithat.

```python
# Persist the SVG document to the filesystem
dwg.save()
print(f"SVG saved to {output_path.resolve()}")
```

A szkript futtatásakor egy konzolüzenetet látsz, amely megerősíti a generált fájl helyét.

### Várt kimenet

Az eredményül kapott `circle.svg` a következőket tartalmazza:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg height="100px" version="1.1" width="100px" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" fill="red"/>
</svg>
```

A fájl böngészőben megnyitva egy éles piros kört jelenít meg, és mivel vektor‑alapú, végtelenül nagyítható pixelálás nélkül.

## 5. lépés: Gyakori variációk és szélső esetek

### Összetettebb vektorok exportálása

Ha **export vector as SVG**-t kell készítened több alakzatot tartalmazó illusztrációkhoz, egyszerűen ismételd meg a `dwg.add()` mintát más primitívekkel (`rect`, `line`, `path`, stb.). Például:

```python
dwg.add(dwg.rect(insert=(10, 10), size=(30, 30), fill="blue"))
dwg.add(dwg.line(start=(0, 0), end=(100, 100), stroke="black", stroke_width=2))
```

### Unicode és szöveg kezelése

Az SVG támogatja a szövegelemeket teljes Unicode támogatással. Használd a `dwg.text("Hello, 🌍", insert=(5, 95), fill="black")` kifejezést többnyelvű címkék beágyazásához.

### Mentés más helyre

Amikor **save SVG image**-t egy felhasználó által megadott mappába mented, ellenőrizd az útvonalat a jogosultsági hibák elkerülése érdekében:

```python
if not output_path.parent.exists():
    raise PermissionError(f"Cannot write to {output_path.parent}")
dwg.save()
```

### Kimenet minifikálása

Gyártási folyamatokhoz előfordulhat, hogy kisebb fájlméretre van szükség. Add át a `pretty=False` értéket a `dwg.tostring()`-nek, és írd ki az eredményt manuálisan:

```python
minified = dwg.tostring(pretty=False)
output_path.write_text(minified)
```

## SVG létrehozása alternatív könyvtárakkal (opcionális)

Míg a `svgwrite` könnyű és tisztán Python, más ökoszisztémák is léteznek:

- **cairosvg** – PNG, PDF vagy HTML konvertálása SVG‑vé.  
- **lxml** – lehetővé teszi az SVG markup kézi felépítését XML API‑k használatával.  

A könyvtár választása a projekt összetettségétől és a meglévő függőségektől függ.

## Következtetés

Most már tudod, hogyan **create SVG document**, vektor alakzatokat adj hozzá, és hogyan **save SVG file** Python segítségével. A teljes megoldás bemutatja a **export vector as SVG** lépéseit, egy **SVG image** generálását, és megválaszolja a gyakori kérdést, hogy **how to create SVG** programozottan.

Innen tovább:

- Bővítsd a szkriptet ciklusokkal, hogy automatikusan diagramokat vagy ikonokat generáljon.  
- Integráld az SVG kimenetet webalkalmazásokba vagy e‑mail sablonokba.  
- Fedezd fel az animációt `<animate>` elemek `svgwrite`‑del történő hozzáadásával.

Kísérletezz különböző alakzatokkal, színekkel és színátmenetekkel, hogy teljes mértékben kiaknázd a méretezhető vektorgrafika erejét Python projektjeidben. Boldog kódolást!

## Mit érdemes legközelebb megtanulni?

A következő tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [SVG dokumentum létrehozása – Kör hozzáadása és mentés SVG‑ként](/html/english/python/general/create-svg-document-add-a-circle-and-save-as-svg/)
- [SVG dokumentum létrehozása Pythonban – SVG‑t PNG‑vé konvertálás útmutató](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)
- [SVG fájl betöltése Pythonban – Teljes útmutató exportáláshoz, beágyazáshoz és konvertáláshoz](/html/english/python/general/load-svg-file-python-complete-guide-to-export-embed-convert/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}