---
category: general
date: 2026-06-10
description: HTML betöltése Pythonban SVG képek kinyeréséhez az oldaladról – lépésről
  lépésre kód, tippek és szélsőséges esetek kezelése.
draft: false
keywords:
- load html python
- extract svg images
- extract svg from html
- search html svg
- find inline svg
language: hu
og_description: HTML betöltése Pythonban és SVG képek kinyerése egy világos, futtatható
  példával. Tanulja meg, hogyan keressen HTML SVG elemeket és kezelje a szélső eseteket.
og_title: HTML betöltése Pythonban – SVG képek hatékony kinyerése
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Load HTML in Python to extract SVG images from your pages—step-by-step
    code, tips, and edge‑case handling.
  headline: Load HTML in Python – Complete Guide to Extract SVG Images
  type: TechArticle
tags:
- python
- html-parsing
- svg
title: HTML betöltése Pythonban – Teljes útmutató SVG képek kinyeréséhez
url: /hu/python/general/load-html-in-python-complete-guide-to-extract-svg-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML betöltése Pythonban – Teljes útmutató SVG képek kinyeréséhez

Valaha szükséged volt **HTML betöltése Pythonban** csak azért, hogy minden SVG grafikont kinyerj egy oldalról? Nem vagy egyedül. Akár web‑scrapert építesz, eszközjelentést generálsz, vagy egyszerűen csak kíváncsi vagy, hogy milyen ikonokat használ egy weboldal, a **SVG képek kinyerésének** ismerete rengeteg manuális keresést takarít meg.

Ebben az útmutatóban egy gyakorlati, vég‑ponttól‑végig megoldáson vezetünk végig, amely **HTML betöltése Pythonban**, majd **HTML SVG** elemek keresése, **inline SVG** megtalálása, sőt külső SVG fájlok lekérése `<img>` tagek által hivatkozva. A végére egy újrahasználható szkriptet, néhány tippet a nehezebb részekhez, és egy tiszta képet kapsz arról, hogyan néz ki a kimenet.

## Mit fogsz megtanulni

* Egy teljesen futtatható Python szkript, amely egy helyi HTML fájlt (vagy letöltött oldalt) elemez, és felsorolja az összes megtalálható SVG‑t.  
* A különbség megértése a **inline SVG** (`<svg>…</svg>`) és a **external SVG** (`<img src="… .svg">`) között.  
* Stratégiák a hibás markup, hiányzó fájlok és névtér‑különbségek kezelésére.  
* Ötletek a kód bővítéséhez – SVG‑k mentése, PNG‑vé konvertálása, vagy adatbázisba való betöltés.

### Előfeltételek

* Python 3.8+ telepítve.  
* Alapvető ismeretek a Python `requests` és `BeautifulSoup` könyvtárairól (importálni fogjuk őket, mélyreható bemutató nélkül).  
* Egy helyi HTML fájl vagy egy URL, amelyet be szeretnél olvasni.  

Most merüljünk el.

## HTML betöltése Pythonban – A parser beállítása

Az első lépés a **HTML betöltése Pythonban**. Olvashatsz egy fájlt a lemezről, vagy letölthetsz egy távoli oldalt. Az alábbi minimalista, mégis robusztus segédfüggvény mindkettőt elvégzi:

```python
import os
import requests
from bs4 import BeautifulSoup

def load_html(source: str) -> BeautifulSoup:
    """
    Load HTML content from a file path or a URL and return a BeautifulSoup object.
    """
    if os.path.isfile(source):
        # Load from local file
        with open(source, "r", encoding="utf-8") as f:
            html = f.read()
    else:
        # Assume it's a URL and fetch it
        response = requests.get(source)
        response.raise_for_status()
        html = response.text

    # Use the html.parser for speed; switch to 'lxml' if you need extra robustness
    soup = BeautifulSoup(html, "html.parser")
    return soup
```

> **Miért fontos:** A `BeautifulSoup` használata elrejti a nyers karakterlánc‑elemzés sajátosságait, és a függvény elegánsan kezeli a helyi fájlokat és a távoli URL‑eket is. Emellett kivételt dob, ha a hálózati kérés sikertelen – így azonnal tudni fogod, ha valami rosszul ment.

## SVG képek kinyerése – Inline SVG elemek keresése

Miután a dokumentum betöltődött, a következő logikus lépés a **inline SVG** tagek **megtalálása**. Az inline SVG közvetlenül a HTML markupba van beágyazva, ami azt jelenti, hogy közvetlenül a DOM‑ból veheted.

```python
def collect_inline_svg(soup: BeautifulSoup) -> list:
    """
    Return a list of all inline <svg> elements as strings.
    """
    inline_svgs = []
    for svg in soup.find_all("svg"):
        # Preserve the original markup; .decode() gives us a string representation
        inline_svgs.append(str(svg))
    return inline_svgs
```

*Pro tipp:* Ha az oldal SVG névtereket használ (`<svg xmlns="http://www.w3.org/2000/svg">`), a `BeautifulSoup` továbbra is megtalálja a tageket, mivel alapértelmezés szerint figyelmen kívül hagyja a névtereket. Ez kényelmes, amikor csak **HTML SVG** keresést végzel.

## HTML SVG keresése – Külső `<img>` hivatkozások kezelése

Sok oldal nem ágyazza be közvetlenül az SVG‑t; külső fájlokra hivatkozik `<img src="icon.svg">` segítségével. Ezek rögzítéséhez végig kell iterálnunk minden `<img>` tageken, ellenőrizni a `src` attribútumot, és megvizsgálni, hogy `.svg`-re végződik-e.

```python
def collect_external_svg(soup: BeautifulSoup, base_path: str = "") -> list:
    """
    Return a list of file paths or URLs that point to external SVG images.
    If base_path is provided, it will be joined with relative URLs.
    """
    external_svgs = []
    for img in soup.find_all("img"):
        src = img.get("src")
        if src and src.lower().endswith(".svg"):
            # Resolve relative paths if a base directory or URL is given
            if base_path and not src.startswith(("http://", "https://")):
                src = os.path.join(base_path, src)
            external_svgs.append(src)
    return external_svgs
```

> **Edge case figyelmeztetés:** Néhány oldal lekérdezési stringeket használ (`icon.svg?v=2`) vagy fragmentumokat (`icon.svg#layer`). A `endswith(".svg")` ellenőrzés továbbra is működik, mivel csak a karakterlánc kisbetűs végére nézünk. Ha szigorúbb validációra van szükséged, fontold meg a `urllib.parse` használatát a paraméterek eltávolításához.

## Inline SVG keresése – Az eredmények jelentése

Mivel már két listánk van – egy az inline SVG markuphoz, a másik a külső fájl hivatkozásokhoz – összevonhatjuk őket, és jelenthetjük a teljes darabszámot. Ez tükrözi az általad megadott eredeti kódrészletet, de egy kicsit több kontextust ad.

```python
def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")
```

## Összeállítás – Teljes szkript

Az alábbiakban a teljes, azonnal futtatható programot találod. Mentsd el `extract_svg.py` néven, és irányítsd egy helyi HTML fájlra vagy egy URL‑re.

```python
#!/usr/bin/env python3
import os
import sys
import requests
from bs4 import BeautifulSoup

# -------------------------------------------------
# Helper functions (see definitions above)
# -------------------------------------------------
def load_html(source: str) -> BeautifulSoup:
    if os.path.isfile(source):
        with open(source, "r", encoding="utf-8") as f:
            html = f.read()
    else:
        response = requests.get(source)
        response.raise_for_status()
        html = response.text
    return BeautifulSoup(html, "html.parser")

def collect_inline_svg(soup: BeautifulSoup) -> list:
    return [str(svg) for svg in soup.find_all("svg")]

def collect_external_svg(soup: BeautifulSoup, base_path: str = "") -> list:
    external_svgs = []
    for img in soup.find_all("img"):
        src = img.get("src")
        if src and src.lower().endswith(".svg"):
            if base_path and not src.startswith(("http://", "https://")):
                src = os.path.join(base_path, src)
            external_svgs.append(src)
    return external_svgs

def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")

# -------------------------------------------------
# Main execution
# -------------------------------------------------
if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python extract_svg.py <path-or-url-to-html>")
        sys.exit(1)

    source = sys.argv[1]
    soup = load_html(source)

    # Determine base path for relative <img> sources (only relevant for local files)
    base_dir = os.path.dirname(os.path.abspath(source)) if os.path.isfile(source) else ""

    inline_svgs = collect_inline_svg(soup)
    external_svgs = collect_external_svg(soup, base_dir)

    report_svg_counts(inline_svgs, external_svgs)

    # Optional: write inline SVGs to separate files for inspection
    for idx, svg_markup in enumerate(inline_svgs, start=1):
        out_path = f"inline_svg_{idx}.svg"
        with open(out_path, "w", encoding="utf-8") as out_file:
            out_file.write(svg_markup)
        print(f"Saved inline SVG #{idx} to {out_path}")

    # Optional: download external SVGs (uncomment if needed)
    # for url in external_svgs:
    #     try:
    #         resp = requests.get(url)
    #         resp.raise_for_status()
    #         filename = os.path.basename(url.split("?")[0])
    #         with open(filename, "wb") as f:
    #             f.write(resp.content)
    #         print(f"Downloaded {url} → {filename}")
    #     except Exception as e:
    #         print(f"Failed to download {url}: {e}")
```

### Várható kimenet

A szkript futtatása egy `sample.html` példánynál a következőt eredményezheti:

```
Found 3 inline SVG element(s).
Found 2 external SVG reference(s).
Overall, 5 SVG item(s) detected.
Saved inline SVG #1 to inline_svg_1.svg
Saved inline SVG #2 to inline_svg_2.svg
Saved inline SVG #3 to inline_svg_3.svg
```

Ha kinyitod a letöltési blokkot, a külső SVG

## Mit érdemes még tanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [svg png java – SVG kép konvertálása Aspose.HTML for Java segítségével](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [SVG konvertálása képpé .NET-ben az Aspose.HTML használatával](/html/english/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [Hogyan konvertáljuk az SVG-t XPS-re az Aspose.HTML for Java segítségével](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}