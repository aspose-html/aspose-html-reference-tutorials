---
category: general
date: 2026-07-31
description: Tanulja meg, hogyan hozhat létre SVG-dokumentumot, adjon hozzá egy kört,
  és gyorsan mentse el az SVG-fájlt. Exportálja a grafikát SVG formátumba néhány Python
  kódsorral.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg document
- save svg file
- export graphic as svg
- add circle to svg
language: hu
lastmod: 2026-07-31
og_description: Hozz létre SVG dokumentumot, adj hozzá egy kört, és néhány másodperc
  alatt mentsd el az SVG fájlt. Ez az útmutató megmutatja, hogyan exportálhatod a
  grafikát SVG formátumba tiszta, futtatható kóddal.
og_image_alt: Screenshot of a red circle inside an SVG file named circle.svg
og_title: SVG-dokumentum létrehozása – Kör hozzáadása és mentés SVG‑ként
schemas:
- author: Aspose
  dateModified: '2026-07-31'
  description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  headline: Create SVG Document – Add a Circle and Save as SVG
  type: TechArticle
- description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  name: Create SVG Document – Add a Circle and Save as SVG
  steps:
  - name: Pro tip
    text: If you plan to generate many files in a loop, give each `Drawing` a unique
      name or use `io.BytesIO` to keep everything in memory until you’re ready to
      write.
  - name: Edge case – Transparent background
    text: 'If you need a transparent background (the default for SVG), you can skip
      setting a `fill` on the root. For a white background, add:'
  - name: 'Bonus: Export graphic as SVG programmatically'
    text: 'If you need the SVG content as a string—for example, to embed it in an
      HTML email—you can call `dwg.tostring()` instead of `save()`:'
  type: HowTo
- questions:
  - answer: Swap `dwg.circle` for `dwg.rect`, `dwg.ellipse`, or even a custom `<path>`
      string. The API is consistent across shapes.
    question: What if I want a different shape?
  - answer: Absolutely. The file you just created can be referenced with `<img src="circle.svg"
      alt="Red circle">` or inlined with `<svg>` tags.
    question: Can I embed the SVG directly in HTML?
  - answer: You could, but libraries like `svgwrite` handle namespace quirks and make
      the code far more maintainable—especially when you start adding gradients or
      animations.
    question: Why not write raw XML?
  type: FAQPage
tags:
- svg
- python
- vector-graphics
- programming-tutorial
title: SVG-dokumentum létrehozása – Kör hozzáadása és mentés SVG‑ként
url: /hu/python/general/create-svg-document-add-a-circle-and-save-as-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SVG dokumentum létrehozása – Kör hozzáadása és mentés SVG-ként

Valaha is szükséged volt **create SVG document** kód alapján, de nem tudtad, hol kezdj? Nem vagy egyedül; sok fejlesztő találkozik ezzel a problémával, amikor először próbálkozik vektorgrafikákkal. Ebben az útmutatóban egy kis, önálló példán keresztül mutatjuk be, hogyan **add circle to SVG**, majd **save SVG file**, hogy **export graphic as SVG**-t használhass a weben vagy tervezőeszközökben.

Könnyű maradunk: csak néhány Python sor, egy népszerű SVG segédkönyvtár, és egy kis magyarázat. A végére lesz egy használatra kész `circle.svg` a mappádban, és megérted, miért fontos minden lépés – nincs homályos „lásd a dokumentációt” rövidítés.

## Amire szükséged lesz

- Python 3.8+ (bármely friss verzió működik)
- A `svgwrite` csomag – telepítsd a `pip install svgwrite` paranccsal
- Egy szövegszerkesztő vagy IDE (VS Code, PyCharm, vagy akár a Notepad is megfelel)
- Írási jogosultság a könyvtárban, ahová a fájlt menteni szeretnéd

Ennyi. Nincs nehéz függőség, nincs külső szolgáltatás.

## 1. lépés: SVG dokumentum előkészítése

SVG dokumentum létrehozása olyan egyszerű, mint egy `Drawing` objektum példányosítása a `svgwrite`‑ből. Gondolj erre az objektumra, mint egy üres vászonra, ahol minden alakzat él.

```python
import svgwrite

# Step 1: Create a new SVG document (canvas) 800×800 pixels
dwg = svgwrite.Drawing(filename="circle.svg", size=("200px", "200px"))
```

> **Miért fontos ez:** A `Drawing` osztály kezeli helyetted az összes XML sablont – névterek, fejlécek és a gyökér `<svg>` elem. Ha már a kezdetekkor megadod a fájlnevet, tudjuk, hová kerül a fájl, ami a későbbi **save svg file** lépést egyszerűvé teszi.

### Profi tipp
Ha sok fájlt szeretnél egy ciklusban generálni, adj minden `Drawing`‑nek egyedi nevet, vagy használd az `io.BytesIO`‑t, hogy mindent a memóriában tarts, amíg készen nem állsz a kiírásra.

## 2. lépés: Kör hozzáadása az SVG-hez

Most, hogy a dokumentum létezik, **add circle to SVG**. Az `add()` metódus bármilyen alakzat objektumot elfogad; egy `Circle` tökéletes egy egyszerű piros pont középpontba helyezéséhez.

```python
# Step 2: Add a red circle element to the SVG root
center = (100, 100)          # x, y coordinates (half of 200px canvas)
radius = 80                  # radius in pixels
circle = dwg.circle(center=center, r=radius, fill='red')
dwg.add(circle)
```

> **Miért használunk `center` és `radius` változókat:** A számok kemény kódolása megnehezíti a kód olvasását és karbantartását. Az értékek elnevezésével egyértelművé tesszük a szándékot – ez a kör pontosan a 200 × 200 vászon közepén helyezkedik el, és elég nagy ahhoz, hogy észrevehető legyen.

### Szélső eset – Átlátszó háttér
Ha átlátszó háttérre van szükséged (az SVG alapértelmezettje), kihagyhatod a `fill` beállítását a gyökérnél. Fehér háttérhez add hozzá:

```python
dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))
```

Ezt a kör hozzáadása előtt helyezd el, hogy a téglalap alatta legyen.

## 3. lépés: SVG fájl mentése

Miután az alakzat a helyén van, az utolsó lépés a **save SVG file**. A `save()` metódus az XML‑t a lemezre írja, és mivel már megadtuk a `Drawing`‑nek a fájlnevet, egyetlen hívás elvégzi a feladatot.

```python
# Step 3: Save the SVG document to a file
dwg.save()
print("✅ circle.svg has been created in the current directory.")
```

> **Mi történik a háttérben?** A `svgwrite` sorosítja az elemfát egy karakterláncra, hozzáadja az XML deklarációt, és UTF‑8 kódolással írja ki. Ha a célkönyvtár nem létezik, a Python `FileNotFoundError`‑t dob; ellenőrizd, hogy az útvonal érvényes, vagy hozd létre az `os.makedirs()`‑sel.

### Bónusz: Grafika exportálása SVG‑ként programból
Ha SVG tartalomra szövegként van szükséged – például HTML e‑mailbe beágyazáshoz – hívhatod a `dwg.tostring()`‑t a `save()` helyett:

```python
svg_content = dwg.tostring()
# Now you can send svg_content over a network, store it in a DB, etc.
```

## Teljes működő példa

Összeállítva, itt egy teljes, futtatható szkript:

```python
import svgwrite
import os

def create_svg_with_circle(output_path: str):
    """
    Creates an SVG file containing a single red circle.
    Parameters
    ----------
    output_path: str
        Full path where the SVG file will be saved.
    """
    # Ensure the directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Initialise the SVG document (800×800 canvas)
    dwg = svgwrite.Drawing(filename=output_path, size=("200px", "200px"))

    # Optional: add a white background rectangle
    dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))

    # Add a red circle in the centre
    center = (100, 100)
    radius = 80
    circle = dwg.circle(center=center, r=radius, fill='red')
    dwg.add(circle)

    # Save the file – this is the key step to **save svg file**
    dwg.save()
    print(f"✅ SVG saved to {output_path}")

if __name__ == "__main__":
    # Change this path to wherever you want the file
    output_file = os.path.join(os.getcwd(), "circle.svg")
    create_svg_with_circle(output_file)
```

**Várható kimenet:** A szkript futtatása után egy `circle.svg` fájlt találsz ugyanabban a mappában. A böngészőben vagy bármely vektorszerkesztőben megnyitva egy piros kört látsz, amely egy fehér négyzet közepén helyezkedik el – pontosan úgy, ahogy programoztuk.

## Gyakori kérdések és buktatók

- **Mi van, ha másik alakzatot szeretnék?** Cseréld le a `dwg.circle`‑t `dwg.rect`‑re, `dwg.ellipse`‑re, vagy akár egy egyedi `<path>` karakterláncra. Az API minden alakzatra egységes.
- **Beágyazhatom közvetlenül a HTML‑be az SVG‑t?** Természetesen. A most létrehozott fájl hivatkozható a `<img src="circle.svg" alt="Red circle">` taggel vagy beágyazható `<svg>` tagekkel.
- **Miért ne írjunk nyers XML‑t?** Lehet, de az `svgwrite`‑hez hasonló könyvtárak kezelik a névtér sajátosságait, és sokkal karbantarthatóbbá teszik a kódot – különösen, ha gradienteket vagy animációkat kezdesz hozzáadni.

## Összegzés

Most már tudod, hogyan **create SVG document**, **add circle to SVG**, és **save SVG file**, hogy **export graphic as SVG** csak néhány Python sorral. A minta skálázható: cseréld le a kört bármilyen vektoros alakzatra, iterálj adatokat diagramok generálásához, vagy kötegelt feldolgozással készítsd el a design rendszerhez szükséges eszközöket.

Következő lépések? Próbálj meg szövegcímkéket hozzáadni, kísérletezz gradientekkel, vagy generálj egy teljes ikon galériát egyetlen szkriptben. Ha érdekelnek a haladóbb funkciók, nézd meg az `svgwrite` dokumentációját a csoportokról (`<g>`), transzformációkról és az animáció támogatásáról.

Boldog kódolást, és legyenek a vektoraid mindig élesek!

## Mit érdemes legközelebb megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}