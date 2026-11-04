---
category: general
date: 2026-08-06
description: HTML konvertálása PDF-be Pythonban egy teljes példával. Tanulja meg,
  hogyan generáljon PDF-et HTML-ből, hogyan mentse el a HTML-t PDF-ként, és hogyan
  kezelje a gyakori szélhelyzeteket.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to pdf
- generate pdf from html
- save html as pdf
- create pdf from html file
- how to convert html to pdf
language: hu
lastmod: 2026-08-06
og_description: HTML konvertálása PDF-re Pythonban és a dokumentumkészítés automatizálása.
  Kövesd ezt az útmutatót, hogy HTML-ből PDF-et generálj, HTML-t PDF-ként ments, és
  testre szabd a kimenetet.
og_image_alt: Example of convert html to pdf script in Python
og_title: HTML konvertálása PDF-be Pythonban – átfogó útmutató
schemas:
- author: Aspose
  dateModified: '2026-08-06'
  description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  headline: Convert HTML to PDF in Python – step‑by‑step guide
  type: TechArticle
- description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  name: Convert HTML to PDF in Python – step‑by‑step guide
  steps:
  - name: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
    text: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
  - name: '**Input handling** – read the HTML file or build the markup programmatically.'
    text: '**Input handling** – read the HTML file or build the markup programmatically.'
  - name: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
    text: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
  type: HowTo
tags:
- HTML to PDF
- Python
- Document conversion
title: HTML konvertálása PDF-re Pythonban – lépésről‑lépésre útmutató
url: /hu/python/general/convert-html-to-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML PDF-re konvertálása Pythonban – lépésről‑lépésre útmutató

Ha gyorsan **HTML‑t PDF‑re** kell konvertálni, ez a bemutató egy teljes megoldást mutat be Pythonban. Megmutatja, hogyan generálj PDF‑et HTML‑ből, hogyan mentsd el a HTML‑t PDF‑ként, és hogyan irányíthatod a konverziós folyamatot anélkül, hogy elhagynád a kódodat.

Az útmutató végigvezet a megbízható könyvtár telepítésén, egy HTML‑dokumentum betöltésén, a konverzió végrehajtásán és az eredmény ellenőrzésén. A végére képes leszel PDF‑et létrehozni HTML‑fájlból bármely Python‑projektben, legyen az statikus oldal vagy dinamikusan generált markup.

## Mit fogsz megtanulni

* Telepítsd a HTML‑PDF konverzióhoz szükséges `pdfkit` és `wkhtmltopdf` függőségeket.  
* Tölts be egy HTML‑dokumentumot lemezről vagy egy karakterláncból.  
* Generálj PDF‑et HTML‑ből egyedi oldalmérettel, margókkal és kódolási beállításokkal.  
* Mentsd el a HTML‑t PDF‑ként egyetlen függvényhívással.  
* Kezeld a tipikus szélhelyzeteket, például hiányzó erőforrásokat, Unicode karaktereket és nagy fájlokat.  

**Előfeltételek** – Python 3.8+ és az alapvető fájl‑I/O ismeretek. Külső szolgáltatások nem szükségesek.

## HTML PDF-re konvertálása – általános munkafolyamat

A konverziós folyamat három logikai fázisból áll:

1. **Előkészítés** – telepítsd a konvertert és győződj meg róla, hogy a `wkhtmltopdf` bináris elérhető.  
2. **Bemenet kezelése** – olvasd be a HTML‑fájlt vagy építsd fel a markupot programozottan.  
3. **Kimenet generálása** – hívd meg a konvertert, írd ki a PDF‑fájlt, és erősítsd meg az eredményt.

Minden fázist egy dedikált lépésben tárgyalunk alább.

## 1. lépés: A szükséges könyvtárak telepítése

`pdfkit` egy vékony Python‑csomagot biztosít a széles körben használt `wkhtmltopdf` motor köré. Telepítsd mindkettőt `pip`‑pel, és ellenőrizd a bináris útvonalat.

```bash
# Install the Python wrapper
pip install pdfkit

# On Ubuntu/Debian install wkhtmltopdf package
sudo apt-get install wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf
```

Ha hordozható binárist kedvelsz, töltsd le a megfelelő kiadást a [wkhtmltopdf GitHub oldalról](https://github.com/wkhtmltopdf/wkhtmltopdf/releases), és helyezd egy olyan könyvtárba, amely a `PATH`‑hez van hozzáadva. A szkript később automatikusan ellenőrzi az útvonalat.

## 2. lépés: A HTML‑dokumentum betöltése

Olvashatsz egy statikus fájlt, lekérhetsz távoli tartalmat, vagy futás közben építhetsz HTML‑t. Az alábbi példa betölt egy helyi `sample.html` nevű fájlt, amelyet egy általad definiált könyvtárban helyezel el.

```python
import pathlib
import pdfkit

# Define the directory that holds the HTML source
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")

# Resolve the full path to the HTML file
html_path = BASE_DIR / "sample.html"

# Read the file content as a UTF‑8 string
with html_path.open(encoding="utf-8") as f:
    html_content = f.read()
```

A fájl Unicode karakterláncként történő olvasása biztosítja, hogy az olyan karakterek, mint a „é”, „ß” vagy ázsiai jelek megmaradjanak a konverzió során. Ez a lépés elengedhetetlen, ha **PDF‑et generálsz HTML‑ből**, amely nemzetközi szöveget tartalmaz.

## 3. lépés: PDF generálása HTML‑ből

`pdfkit.from_string` egy HTML‑markupot tartalmazó karakterláncot konvertál PDF‑fájllá. Egy opciókat tartalmazó szótárat adhatunk meg az oldalméret, margók és fejléc/lábléc viselkedésének szabályozásához.

```python
# Define the output PDF path
pdf_path = BASE_DIR / "sample.pdf"

# Conversion options – adjust as needed
options = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left": "0.75in",
    "encoding": "UTF-8",
    "enable-local-file-access": None,  # Allows loading local images/CSS
}

# Perform the conversion
pdfkit.from_string(html_content, str(pdf_path), options=options)
```

A fenti hívás **PDF‑et hoz létre HTML‑fájlból**, amely a `sample.pdf`‑ben tárolódik. Ha a forrás HTML helyi CSS‑re vagy képekre hivatkozik, az `enable‑local‑file‑access` kapcsoló lehetővé teszi a `wkhtmltopdf` számára, hogy feloldja ezeket az erőforrásokat.

### Miért működik ez a megközelítés

* A `pdfkit` a nehéz munkát a `wkhtmltopdf`‑nek adja át, amely a WebKit motorral rendereli a HTML‑t, garantálva a magas hűséget az eredeti elrendezéshez.  
* Az opciókat tartalmazó szótár biztosítja, hogy finomhangolhasd a kimenetet anélkül, hogy módosítanád magát a HTML‑t.  
* A `from_string` használata a munkafolyamatot memóriában tartja, ami hasznos, ha a HTML futás közben generálódik.

## 4. lépés: HTML mentése PDF‑ként és a kimenet ellenőrzése

A konverzió után érdemes ellenőrizni, hogy a PDF létezik-e és olvasható-e. Az alábbi kódrészlet ellenőrzi a fájl méretét, és megnyitja a PDF‑et az alapértelmezett rendszer‑nézővel (platform‑specifikus).

```python
import os
import subprocess
import sys

# Verify that the PDF file was created
if pdf_path.is_file() and pdf_path.stat().st_size > 0:
    print(f"✅ PDF generated successfully: {pdf_path}")

    # Open the PDF for visual verification (optional)
    if sys.platform.startswith("darwin"):      # macOS
        subprocess.run(["open", str(pdf_path)])
    elif os.name == "nt":                      # Windows
        os.startfile(str(pdf_path))
    else:                                      # Linux and others
        subprocess.run(["xdg-open", str(pdf_path)])
else:
    raise FileNotFoundError("PDF generation failed – file not found or empty.")
```

A szkript futtatása sikerüzenetet ír ki, és elindítja a PDF‑nézőt, így azonnal ellenőrizheted, hogy az elrendezés megegyezik-e az eredeti HTML‑lel. Ez a lépés befejezi a **save html as pdf** ciklust.

## 5. lépés: Haladó beállítások – PDF létrehozása HTML‑fájlból egyedi beállításokkal

Néha van egy fizikai HTML‑fájl a lemezen, és inkább a `pdfkit.from_file`‑t használod, ahelyett, hogy magad töltenéd be a tartalmat. Ez a módszer hasznos, ha a HTML már tartalmaz komplex relatív útvonalakat.

```python
# Directly convert a file path to PDF
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

A `options` szótár kibővítésével beágyazhatsz egy címlapot, tartalomjegyzéket vagy JavaScript végrehajtási kapcsolókat. Például egy címlap hozzáadásához:

```python
options.update({
    "cover": str(BASE_DIR / "cover.html"),
    "toc": None,  # Generates a table of contents
})
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

Ezek a finomhangolások bemutatják, **hogyan konvertálj HTML‑t PDF‑re** összetettebb kiadási folyamatokhoz.

## Gyakori buktatók és elkerülésük módjai

| Probléma | Ok | Megoldás |
|----------|----|----------|
| Képek vagy CSS nem jelenik meg | `wkhtmltopdf` alapértelmezés szerint blokkolja a helyi fájlhozzáférést | Add hozzá az `"enable-local-file-access": None` beállítást az options szótárhoz |
| Unicode karakterek eltorzulnak | Hiányzó `encoding` opció vagy a fájl rossz karakterkódolással való olvasása | Mindig állítsd be az `"encoding": "UTF-8"` értéket, és olvasd a HTML‑fájlt UTF‑8‑kal |
| A PDF üres | Helytelen útvonal a `wkhtmltopdf` binárishoz | Add meg explicit módon az útvonalat: `pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")` |
| Nagy HTML fájlok időtúllépést okoznak | Az alapértelmezett timeout túl rövid | Állítsd be a `"javascript-delay": "2000"` értéket, vagy növeld a timeout-ot a `"timeout": "60"` használatával |

Ezeknek a problémáknak a kezelése biztosítja a megbízható **generate pdf from html** folyamatot különböző környezetekben.

## Teljes szkript – vég‑től‑végig példa

Mentsd el a következőt `html_to_pdf.py`‑ként, és futtasd a `python html_to_pdf.py` paranccsal. Állítsd be a `YOUR_DIRECTORY`‑t a projekt mappádra mutatva.

```python
#!/usr/bin/env python3
"""
Convert HTML to PDF in Python – complete, runnable example.
"""

import pathlib
import pdfkit
import os
import subprocess
import sys

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")          # <-- change this
HTML_FILE = BASE_DIR / "sample.html"
PDF_FILE = BASE_DIR / "sample.pdf"

# wkhtmltopdf configuration (optional – only needed if binary is not on PATH)
# config = pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")

# Conversion options – customize as required
OPTIONS = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left":


## Mit érdemes még megtanulni?

Az alábbi bemutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészletet tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan konvertáljunk HTML‑t PDF‑re Java‑ban – Aspose.HTML használata Java‑hoz](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [HTML konvertálása PDF‑re .NET‑ben az Aspose.HTML‑el](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Hogyan konvertáljunk HTML‑t PDF‑re Java‑ban – Oldalmargók beállítása Aspose.HTML‑el](/html/english/java/advanced-usage/css-extensions-adding-title-page-number/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}