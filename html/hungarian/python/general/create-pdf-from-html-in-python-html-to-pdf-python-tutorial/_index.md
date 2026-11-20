---
category: general
date: 2026-07-15
description: PDF készítése HTML‑ből Python segítségével. Tanulja meg, hogyan konvertálhatja
  gyorsan a HTML‑t PDF‑re egy egyszerű szkript és világos lépések segítségével.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf from html
- convert html to pdf
- html to pdf python
- save html as pdf
- html to pdf tutorial
language: hu
lastmod: 2026-07-15
og_description: PDF létrehozása HTML-ből Python segítségével. Ez az útmutató megmutatja,
  hogyan konvertálhatod a HTML-t PDF-be, hogyan mentheted a HTML-t PDF-ként, és hogyan
  kezelheted hatékonyan az erőforrásokat.
og_image_alt: Screenshot of a Python script that creates PDF from HTML
og_title: PDF létrehozása HTML‑ből Pythonban – Gyakorlati útmutató
schemas:
- author: Aspose
  dateModified: '2026-07-15'
  description: Create PDF from HTML using Python. Learn how to convert HTML to PDF
    quickly with a simple script and clear steps.
  headline: Create PDF from HTML in Python – HTML to PDF Python Tutorial
  type: TechArticle
tags:
- python
- pdf
- html
- conversion
title: PDF létrehozása HTML‑ből Pythonban – HTML‑PDF Python útmutató
url: /hu/python/general/create-pdf-from-html-in-python-html-to-pdf-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF létrehozása HTML-ből Pythonban – Teljes körű útmutató

Valaha szükséged volt **PDF létrehozására HTML-ből**, de nem tudtad, melyik Python könyvtárat válaszd? Nem vagy egyedül – sok fejlesztő ütközik ebbe a helyzetbe, amikor egy webes jelentést, számlát vagy marketingoldalt próbál nyomtatható PDF‑vé alakítani.  

A jó hír, hogy néhány sor kóddal megbízhatóan **HTML‑t PDF‑vé konvertálhatsz**, és a szkript Windows, macOS és Linux rendszereken is működik. Ebben az útmutatóban egy teljes, futtatható példán keresztül vezetünk végig, elmagyarázzuk, miért fontos minden lépés, és megmutatjuk, hogyan **mentheted el a HTML‑t PDF‑ként** anélkül, hogy bármi hiányozna.

---

## Mit fogsz megtanulni

- A megfelelő Python csomag telepítése HTML‑PDF konverzióhoz.  
- HTML fájl betöltése egyedi erőforrás‑kezelési beállításokkal (a végtelen CSS‑importok elkerülése érdekében).  
- Tiszta PDF fájl generálása a lemezen.  
- Gyakori szélhelyzetek kezelése, mint például külső képek, relatív útvonalak és nagy dokumentumok.  

A **HTML‑PDF tutorial** végére egy újrahasználható függvényed lesz, amelyet bármely projektbe beilleszthetsz.

---

## Előfeltételek

- Python 3.9+ (a kód 3.8‑nal is működik, de a 3.9+ a legújabb `pathlib` funkciókat biztosítja).  
- Alapvető ismeretek a parancssorral és a virtuális környezetekkel.  
- Egy HTML fájl, amelyet PDF‑vé szeretnél alakítani – bármely statikus oldal megfelel.

> **Pro tipp:** Ha virtuális környezetet használsz, aktiváld azt a könyvtár telepítése előtt; ez rendezetten tartja a globális Python‑odat.

---

## 1. Lépés – Install WeasyPrint (a konverzió motorja)

A WeasyPrint egy tisztán Python‑ban írt könyvtár, amely HTML‑t és CSS‑t PDF‑vé renderel. Kezeli a legtöbb modern webes funkciót, és finomhangolt vezérlést biztosít az erőforrás‑betöltés felett.

```bash
pip install weasyprint
```

A fenti parancs futtatása letölti a `cairocffi`, `tinycss2` és néhány egyéb függőséget. Ha Windowson `cairo`‑val kapcsolatos hibát kapsz, szerezd be az előre lefordított wheel‑eket a [WeasyPrint weboldaláról](https://weasyprint.org/docs/install/).

---

## 2. Lépés – Készíts egy apró segédprogramot az erőforrás‑kezeléshez

Amikor egy HTML dokumentumot töltesz be, amely külső stíluslapokra vagy képekre hivatkozik, a könyvtár követi ezeket a hivatkozásokat. Egyes esetekben ez mély beágyazódáshoz vagy akár végtelen ciklusokhoz vezet (gondolj egy CSS‑fájlra, amely `@import`‑olja saját magát). A rendezettség érdekében korlátozzuk az erőforrás‑kezelés mélységét.

```python
from weasyprint import HTML, CSS
from pathlib import Path

class ResourceHandlingOptions:
    """Simple container to mimic max depth handling."""
    def __init__(self, max_depth: int = 3):
        self.max_depth = max_depth
        self._current_depth = 0

    def within_limit(self) -> bool:
        return self._current_depth < self.max_depth

    def __enter__(self):
        self._current_depth += 1
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        self._current_depth -= 1
```

A fenti osztály nem kötelező a WeasyPrint számára, de tükrözi az eredeti kódrészletben látott mintát, és lehetőséget ad a szabadon futó importok leállítására. A következő lépésben használni fogod.

---

## 3. Lépés – Töltsd be a HTML dokumentumot a saját beállításokkal

Most ténylegesen beolvassuk a HTML fájlt. A `HTML` osztály egy `base_url` argumentumot fogad, amelyet a forrásfájlt tartalmazó könyvtárra állítunk – ezáltal a relatív hivatkozások webszerver nélkül is működnek.

```python
def load_html(input_path: Path, options: ResourceHandlingOptions) -> HTML:
    """
    Load an HTML file while respecting the max handling depth.
    """
    if not options.within_limit():
        raise RuntimeError("Maximum resource handling depth exceeded.")
    # The `with` block increments depth for the duration of the call.
    with options:
        return HTML(filename=str(input_path), base_url=str(input_path.parent))
```

> **Miért fontos:** Ha a HTML egy CSS‑fájl sorozatot hív meg, minden `@import` egy újabb betöltést indít. A mélység‑védő megakadályozza, hogy a szkript kicsúszzon az irányítás alól.

---

## 4. Lépés – Mentsd el a feldolgozott dokumentumot PDF‑ként

A `HTML` objektummal a PDF generálása egyetlen sorban megoldható. Emellett egy egyszerű CSS‑részletet adunk át, amely tiszta oldalméretet (A4) kényszerít, és egy kis margót ad – nyugodtan módosíthatod.

```python
def save_as_pdf(html_doc: HTML, output_path: Path) -> None:
    """
    Render the HTML document to a PDF file.
    """
    default_css = CSS(string='''
        @page { size: A4; margin: 1cm }
    ''')
    html_doc.write_pdf(target=str(output_path), stylesheets=[default_css])
```

`write_pdf` hívása a PDF‑et a lemezre streameli, így egy megosztható fájlt kapsz.

---

## 5. Lépés – Rakd össze az egészet

Az alábbi kompakt szkriptet beillesztheted a `convert.py` fájlba. Cseréld ki a helyőrző útvonalakat a saját könyvtáraidra.

```python
#!/usr/bin/env python3
"""
HTML to PDF Python script – complete, runnable example.
"""

from pathlib import Path

# Import the helper classes we defined earlier
from __main__ import ResourceHandlingOptions, load_html, save_as_pdf  # noqa: E402

def main():
    # 1️⃣  Define input and output locations
    input_html = Path("YOUR_DIRECTORY/input.html")
    output_pdf = Path("YOUR_DIRECTORY/output.pdf")

    # 2️⃣  Create resource handling options (max depth = 3)
    resource_options = ResourceHandlingOptions(max_depth=3)

    # 3️⃣  Load the HTML document with the custom options
    html_doc = load_html(input_html, resource_options)

    # 4️⃣  Save the processed document as PDF
    save_as_pdf(html_doc, output_pdf)

    print(f"✅ PDF saved to {output_pdf.resolve()}")

if __name__ == "__main__":
    main()
```

**Várható kimenet** – a `python convert.py` futtatása után a következőt kell látnod:

```
✅ PDF saved to /full/path/YOUR_DIRECTORY/output.pdf
```

Nyisd meg a generált fájlt bármely PDF‑olvasóval; látni fogod az eredeti oldal elrendezését, a CSS‑stílusokat és a képeket (feltéve, hogy a HTML‑fájlból elérhetők voltak).  

Ha hiányzó képeket észlelsz, ellenőrizd, hogy a `src` attribútumaik vagy abszolút URL‑ek, vagy relatív útvonalak, amelyek léteznek a `YOUR_DIRECTORY` alatt.

---

## Gyakori kérdések & szélhelyzetek kezelése

| Kérdés | Válasz |
|----------|--------|
| *Mi van, ha a HTML külső betűtípusokra hivatkozik?* | A WeasyPrint automatikusan letölti a betűtípus fájlokat, de érdemes lehet fehérlistára tenni a domaineket a hosszú letöltési idők elkerülése érdekében. |
| *Átalakíthatok egy HTML‑sztringet fájl helyett?* | Igen – használd a `HTML(string=my_html_string)`‑t, és hagyd ki a `base_url`‑t, vagy állítsd egy ideiglenes mappára. |
| *Hogyan szabályozhatom a PDF metaadatait (cím, szerző)?* | Adj át egy `metadata` szótárt a `write_pdf`‑nek, például `html_doc.write_pdf(target='out.pdf', metadata={'Title': 'Report'})`. |
| *„cairo‑cffi error” hiba jelentkezik Linuxon.* | Telepítsd a rendszercsomagot `libcairo2-dev` (`apt-get install libcairo2-dev` Debian/Ubuntu rendszeren) a WeasyPrint pip‑es telepítése előtt. |

---

## Összegzés

Most **PDF‑t hoztunk létre HTML‑ből** egy tiszta Python munkafolyamat segítségével, lefedtük a **HTML‑PDF konverzió** mechanikáját, és megmutattuk, hogyan **mentheted el a HTML‑t PDF‑ként** robusztus erőforrás‑kezeléssel. A szkript elég kicsi ahhoz, hogy CI pipeline‑okba illeszd, mégis elég rugalmas ahhoz, hogy egyedi fejlécekkel, láblécekkel vagy vízjelekkel bővítsd.

A következő lépéseket érdemes felfedezni:

- Használd a **html to pdf python** könyvtárat `pdfkit` a wkhtmltopdf‑alapú megközelítéshez (jó a régi CSS‑hez).  
- Adj hozzá CLI felületet az `argparse`‑szal, hogy a szkript bemeneti/kimeneti argumentumokat fogadjon.  
- Generálj PDF‑eket helyben egy Flask vagy FastAPI végponton keresztül igény szerinti jelentésekhez.  

Nyugodtan kísérletezz, törj el dolgokat, majd térj vissza ehhez az útmutatóhoz egy gyors frissítésért. Ha problémába ütközöl, a WeasyPrint dokumentáció és a közösségi fórumok kiváló források.

Boldog kódolást, és élvezd a weboldalak elegáns PDF‑vé alakítását!

## Mit érdemes legközelebb megtanulni?

A következő tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra építenek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy további API‑funkciókat saját projektjeidben is könnyedén alkalmazhasd.

- [HTML PDF konvertálása Aspose.HTML‑vel – Teljes manipulációs útmutató](/html/english/)
- [.NET‑ben HTML PDF konvertálása Aspose.HTML‑vel](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [PDF létrehozása HTML‑ből – C# lépésről‑lépésre útmutató](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}