---
category: general
date: 2026-10-21
description: Tanulja meg, hogyan konvertálhatja gyorsan a HTML-t PNG-re. Ez az útmutató
  a weboldal PNG-be exportálását és a HTML-fájl PNG-re konvertálását Python segítségével
  is bemutatja.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to png
- export webpage to png
- how to convert html to image
- convert html file to png
language: hu
lastmod: 2026-10-21
og_description: HTML konvertálása PNG-re Python segítségével. Kövesd ezt az átlátható
  útmutatót a weboldal PNG-be exportálásához, a szélhelyzetek kezeléséhez és a képgenerálás
  automatizálásához.
og_image_alt: Screenshot of HTML page converted to PNG using Python
og_title: HTML konvertálása PNG-re Pythonban – teljes programozási útmutató
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  headline: How to convert HTML to PNG in Python – step‑by‑step guide
  type: TechArticle
- description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  name: How to convert HTML to PNG in Python – step‑by‑step guide
  steps:
  - name: Expected output
    text: 'Running the script prints:'
  - name: Why adjust viewport size?
    text: Web pages designed for desktop screens often look cramped if rendered at
      a small width. By increasing the `width` and `height` options, you capture the
      full layout, which is especially useful for **export webpage to PNG** tasks.
  - name: 6.1 Large pages or infinite scroll
    text: 'For pages that load content lazily (e.g., infinite scroll), increase the
      JavaScript delay and optionally set a larger viewport:'
  - name: 6.2 Authentication‑protected pages
    text: 'If a page requires a session cookie, you can embed the cookie header:'
  - name: 6.3 Missing images or fonts
    text: '`wkhtmltoimage` respects the `--disable-local-file-access` flag for security.
      If your HTML references local assets, enable them explicitly:'
  type: HowTo
tags:
- python
- html conversion
- image processing
- web automation
title: Hogyan konvertáljunk HTML-t PNG-re Pythonban – lépésről lépésre útmutató
url: /hu/python/general/how-to-convert-html-to-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML konvertálása PNG-re Pythonban – teljes programozási útmutató

Ha **HTML-t PNG-re kell konvertálni**, ez az útmutató megbízható módot mutat be, hogyan teheted meg egyszerű Python segítségével. Akár statikus jelentést exportálsz, galéria számára bélyegképeket generálsz, vagy teszteléshez automatizálsz képernyőképeket, percek alatt egy teljes, futtatható megoldást kapsz.

Meg fogod látni, hogyan **exportálj weboldalt PNG-re**, megérted a különbséget egy HTML fájl konvertálása és egy élő URL konvertálása között, és megtanulod a legjobb gyakorlatokat nagy oldalak vagy dinamikus tartalom kezelése során. Külső szolgáltatás nem szükséges – csak néhány Python csomag és egy rövid szkript.

## Előfeltételek

- Python 3.9+ telepítve (a kód Windows, macOS és Linux rendszereken működik)
- Hozzáférés egy terminálhoz vagy parancssorhoz
- Alapvető ismeretek a Python csomagkezelőjéről (`pip`)

Szükséged lesz az `imgkit` csomagra (egy vékony wrapper a `wkhtmltoimage` köré) és magára a `wkhtmltoimage` binárisra. Mindkettő ingyenes és nyílt forráskódú.

## 1. lépés: A szükséges eszközök telepítése

Az első lépés a `wkhtmltoimage` és a hozzá kapcsolódó Python wrapper telepítése.

```bash
# Install wkhtmltoimage (Linux example)
sudo apt-get update && sudo apt-get install -y wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf

# On Windows download the installer from:
# https://wkhtmltopdf.org/downloads.html
# and add the installation folder to your PATH.

# Install the Python wrapper
pip install imgkit
```

> **Miért fontos ez a lépés** – a `wkhtmltoimage` a WebKit motor segítségével rendereli a HTML-t, pixel‑tökéletes PNG-ket hozva létre. Az `imgkit` egyszerűen továbbítja a beállításaidat a binárisnak, így ugyanazt a minőséget kapod, mint egy böngészőben.

## 2. lépés: A telepítés ellenőrzése

Futtass egy gyors ellenőrzést, hogy megbizonyosodj róla, hogy a bináris elérhető a Pythonból.

```python
import imgkit

# This will raise an exception if wkhtmltoimage is not found
print("wkhtmltoimage version:", imgkit.config().wkhtmltoimage)
```

Ha a szkript kiírja a `wkhtmltoimage` elérési útját, készen állsz a HTML PNG-re konvertálására. Ha `OSError`-t kapsz, ellenőrizd újra, hogy a bináris szerepel-e a rendszer `PATH` változójában.

## 3. lépés: Újrafelhasználható konverziós függvény írása

A logika függvénybe kapszulázása megkönnyíti a **HTML fájl PNG-re konvertálását** vagy a **weboldal PNG-re exportálását** a projekt bármely részéről.

```python
import os
import imgkit

def convert_html_to_png(source, output_path, *, options=None):
    """
    Convert an HTML file or URL to a PNG image.

    Parameters
    ----------
    source : str
        Path to a local HTML file (e.g., "report.html") or a URL
        (e.g., "https://example.com").
    output_path : str
        Destination file path for the PNG (e.g., "report.png").
    options : dict, optional
        imgkit options such as viewport size, zoom factor, or
        JavaScript delay. If omitted, sensible defaults are used.

    Returns
    -------
    bool
        True if the conversion succeeded, False otherwise.
    """
    # Use a default set of options if none are provided
    default_options = {
        "format": "png",
        "quality": "100",
        "encoding": "UTF-8",
        "quiet": "",
        # Render at 1280×720 – adjust for your layout
        "width": 1280,
        "height": 720,
        # Wait for JavaScript to finish (ms)
        "javascript-delay": 500,
    }
    # Merge user‑supplied options over defaults
    final_options = {**default_options, **(options or {})}

    try:
        # imgkit can handle both files and URLs transparently
        imgkit.from_file(source, output_path, options=final_options) \
            if os.path.isfile(source) else \
            imgkit.from_url(source, output_path, options=final_options)
        print(f"✅ Successfully saved PNG to: {output_path}")
        return True
    except Exception as e:
        print(f"❌ Conversion failed: {e}")
        return False
```

> **Miért csomagoljuk be mind a `from_file`, mind a `from_url`-t** – ugyanaz a függvény most támogatja a **hogyan konvertáljunk HTML-t képre** helyi fájlok és élő weboldalak esetén is, így a kódod DRY marad (Don’t Repeat Yourself).

## 4. lépés: Helyi HTML fájl PNG-re konvertálása

Helyezz el egy `sample.html` nevű HTML fájlt egy `assets` nevű mappában. Ezután hívd meg a most definiált segédfüggvényt:

```python
if __name__ == "__main__":
    # Example: convert a static HTML file
    html_path = os.path.join("assets", "sample.html")
    png_path = os.path.join("output", "sample.png")

    # Ensure the output directory exists
    os.makedirs(os.path.dirname(png_path), exist_ok=True)

    # Perform the conversion
    success = convert_html_to_png(html_path, png_path)

    if success:
        # Show a tiny preview in the console (optional)
        from PIL import Image
        img = Image.open(png_path)
        img.thumbnail((200, 200))
        img.show()
```

### Várt kimenet

A szkript futtatása kiírja:

```
✅ Successfully saved PNG to: output/sample.png
```

Az új `output/sample.png` fájl most egy pixel‑tökéletes pillanatképet tartalmaz a `sample.html`-ről. Bármely képnézőben megnyitva a renderelt oldalt pontosan úgy mutatja, ahogy egy böngészőben látnád.

## 5. lépés: Élő weboldal PNG-re exportálása

Ha **weboldalt kell PNG-re exportálni** egy gyakran változó URL-hez (például egy műszerfal), egyszerűen add át az URL karakterláncot a fájlútvonal helyett.

```python
# Example: convert a live page
url = "https://developer.mozilla.org/en-US/docs/Web/HTML"
output_file = "output/mdn_homepage.png"

convert_html_to_png(url, output_file, options={"width": 1920, "height": 1080})
```

### Miért kell a viewport méretét módosítani?

Az asztali képernyőkre tervezett weboldalak gyakran szűknek tűnnek, ha kis szélességen renderelünk. A `width` és `height` opciók növelésével a teljes elrendezést rögzíted, ami különösen hasznos a **weboldal PNG-re exportálása** feladatoknál.

## 6. lépés: Gyakori szélső esetek kezelése

### 6.1 Nagy oldalak vagy végtelen görgetés

Azoknál az oldalaknál, amelyek tartalmat lazán töltnek (például végtelen görgetés), növeld a JavaScript késleltetést, és opcionálisan állíts be nagyobb viewport-ot:

```python
options = {
    "javascript-delay": 2000,   # wait 2 seconds for JS to finish
    "width": 1440,
    "height": 3000,             # tall enough for the whole page
    "disable-smart-width": "", # forces the width we set
}
convert_html_to_png(url, "long_page.png", options=options)
```

### 6.2 Hitelesítéssel védett oldalak

Ha egy oldal session cookie-t igényel, beágyazhatod a cookie fejlécet:

```python
options = {
    "custom-header": [
        "Cookie: sessionid=YOUR_SESSION_ID"
    ]
}
convert_html_to_png("https://internal.example.com/report", "report.png", options=options)
```

### 6.3 Hiányzó képek vagy betűtípusok

A `wkhtmltoimage` a `--disable-local-file-access` kapcsolót biztonsági okokból tiszteletben tartja. Ha a HTML helyi erőforrásokra hivatkozik, engedélyezd őket kifejezetten:

```python
options = {"enable-local-file-access": ""}
convert_html_to_png("assets/complex.html", "complex.png", options=options)
```

## 7. lépés: Az eredmény programozott ellenőrzése (opcionális)

Néha szükség van arra, hogy megerősítsd, a PNG helyesen lett-e generálva (például CI pipeline-okban). Az alábbi kódrészlet ellenőrzi a fájl méretét és dimenzióit:

```python
from pathlib import Path
from PIL import Image

def verify_png(path):
    p = Path(path)
    if not p.is_file():
        raise FileNotFoundError(f"{path} does not exist")
    if p.stat().st_size < 10_000:  # arbitrary minimal size
        raise ValueError("Generated PNG seems too small")
    with Image.open(p) as img:
        print(f"Image size: {img.width}×{img.height}, mode: {img.mode}")

verify_png(png_path)
```

Ha a PNG átmegy ezeken az ellenőrzéseken, biztonságosan használhatod további folyamatokban, például PDF generálásban, e‑mail mellékletekben vagy gépi tanulási pipeline‑okban.

## Összegzés

Most már van egy teljes, termelés‑kész módszered a **HTML PNG-re konvertálására** Python használatával. Az útmutató a következőket fedte le:

- `wkhtmltoimage` és `imgkit` telepítése
- A környezet ellenőrzése
- Egy újrafelhasználható `convert_html_to_png` függvény, amely kezeli a helyi fájlokat és az URL-eket is
- Valós példák **weboldal PNG-re exportálására**, **hogyan konvertáljunk HTML-t képre**, és **HTML fájl PNG-re konvertálására**
- Szélső esetek kezelése nagy oldalak, hitelesítés és helyi erőforrások esetén
- Opcionális ellenőrzési lépések CI/CD pipeline-okhoz

Nyugodtan kísérletezz további `imgkit` opciókkal – például `zoom`, `crop-h` vagy `crop-w` – hogy finomhangold a kimenetet a saját felhasználási esetedhez. A következő lépésekhez érdemes lehet:

- A PNG-k PDF jelentéssé konvertálása (`img2pdf` könyvtár)
- Egy teljes HTML fájlok mappájának kötegelt konvertálásának automatizálása
- Selenium használata olyan oldalakhoz, amelyek teljes böngésző renderelést igényelnek (például nehéz JavaScript keretrendszerek)

Boldog kódolást, és élvezd a pixel‑tökéletes képernyőképeket!

## Mit érdemes még megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [HTML konvertálása PNG-re – Teljes Python útmutató](/html/english/python/general/convert-html-to-png-complete-python-guide/)
- [HTML konvertálása PNG-re Pythonban – Teljes Streaming mentés útmutató](/html/english/python/general/convert-html-to-png-in-python-complete-streaming-save-guide/)
- [SVG konvertálása PNG-re Pythonban az Aspose.HTML használatával](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}