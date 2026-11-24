---
category: general
date: 2026-11-24
description: Módosított HTML mentése és target="_blank" linkek hozzáadása Pythonban
  az Aspose.HTML használatával. Tanulja meg, hogyan változtassa meg az href célját
  az összes <a> címkében, és nyissa meg az összes linket új lapon.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save modified html
- add target blank links
- change href target
- open all links newtab
language: hu
lastmod: 2026-11-24
og_description: Mentsd el a módosított HTML-t, és adj hozzá target="_blank" linkeket
  Pythonban az Aspose.HTML segítségével. Kövesd ezt a lépésről‑lépésre útmutatót,
  hogy megváltoztasd a href célját, és minden linket új lapon nyiss meg.
og_image_alt: Screenshot of a Python script that saves modified HTML with target='_blank'
  on every link
og_title: Módosított HTML mentése és target='_blank' linkek hozzáadása Pythonban –
  teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-11-24'
  description: Save modified HTML and add target blank links in Python using Aspose.HTML.
    Learn how to change href target for all <a> tags and open all links newtab.
  headline: Save modified HTML and add target blank links in Python
  type: TechArticle
tags:
- Aspose.HTML
- Python
- HTML manipulation
- Web automation
title: Módosított HTML mentése és target="_blank" linkek hozzáadása Pythonban
url: /hu/python/general/save-modified-html-and-add-target-blank-links-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Módosított HTML mentése és target blank linkek hozzáadása Pythonban

Ha **módosított HTML-t** kell menteni minden link frissítése után, ez az útmutató megmutatja, hogyan teheted ezt meg az Aspose.HTML for Python segítségével. Megtanulod, hogyan **adj hozzá target blank linkeket**, módosítsd a href célját, és tedd úgy, hogy minden link új lapon nyíljon meg.

Az útmutató mindent lefed a HTML fájl betöltésétől a változtatások helyes írásának ellenőrzéséig. Az Aspose.HTML könyvtáron kívül nincs szükség külső eszközökre.

## Előkövetelmények

Mielőtt elkezdenéd, győződj meg róla, hogy rendelkezel:

* Python 3.8 vagy újabb telepítve  
* Aktív Aspose.HTML for Python licenc (vagy egy ingyenes értékelő kulcs)  
* Egy helyi HTML fájl, amelyet módosítani szeretnél (pl. `index.html`)  

A könyvtárat a pip segítségével telepítheted:

```bash
pip install aspose-html
```

## 1. lépés: HTML dokumentum betöltése

Az első lépés egy `HTMLDocument` példány létrehozása, amely a forrásfájlra mutat. Ez az objektum a teljes DOM-fát képviseli, lehetővé téve az elemek lekérdezését és szerkesztését.

```python
from aspose.html import HTMLDocument

# Load the original HTML file
doc = HTMLDocument("YOUR_DIRECTORY/index.html")
```

*Miért fontos*: A dokumentum betöltése programozott hozzáférést biztosít minden csomóponthoz, ami szükséges a tömeges frissítésekhez, például az összes `<a>` elem `target` attribútumának módosításához.

## 2. lépés: target blank linkek hozzáadása minden horgonyhoz

Ahhoz, hogy minden hiperhivatkozás új lapon nyíljon meg, a `target` attribútumot `_blank` értékre állítod. A `query_selector_all` metódus élő gyűjteményt ad vissza az összes `<a>` elemről, függetlenül a beágyazás mélységétől.

```python
# Update all <a> tags to open links in a new tab
for link in doc.query_selector_all("a"):
    link.set_attribute("target", "_blank")
```

**Kulcspontok**

* A ciklus minden horgonyt pontosan egyszer érint, biztosítva, hogy a **add target blank links** egységesen alkalmazásra kerüljön.  
* Ha egy link már rendelkezik `target` attribútummal, a hívás felülírja azt, garantálva a konzisztens viselkedést.  

### Létező `target` értékek kezelése (opcionális)

Ha inkább meg szeretnéd őrizni a meglévő célokat, és csak akkor állítanád `_blank`-re, ha az attribútum hiányzik, adj hozzá egy feltételes ellenőrzést:

```python
for link in doc.query_selector_all("a"):
    if not link.has_attribute("target"):
        link.set_attribute("target", "_blank")
```

## 3. lépés: href cél módosítása és minden link új lapon megnyitása

Néha a `href` attribútumot magát kell átírni – például egy alap URL előtaggal vagy relatív útvonalak abszolút URL-re konvertálásával. Ugyanaz a DOM‑traversálási technika működik a `href` változtatásokhoz is.

```python
base_url = "https://example.com/"

for link in doc.query_selector_all("a"):
    href = link.get_attribute("href")
    # Skip empty or already absolute URLs
    if href and not href.startswith("http"):
        new_href = base_url + href.lstrip("/")
        link.set_attribute("href", new_href)
    # Ensure the link opens in a new tab
    link.set_attribute("target", "_blank")
```

*Miért fontos*: A **changing href target** és a **open all links newtab** biztosítja, hogy a felhasználók a megfelelő helyre legyenek irányítva, és a navigáció a jelenlegi oldal elhagyása nélkül történjen.

## 4. lépés: Módosított dokumentum mentése

Miután minden módosítás befejeződött, hívd meg a `save` metódust a változtatások új fájlba írásához. Itt történik meg a **save modified html** tényleges végrehajtása.

```python
# Save the updated HTML to a new file
doc.save("YOUR_DIRECTORY/index_modified.html")
```

Az eredményül kapott `index_modified.html` minden `<a>` elemet tartalmaz `target="_blank"` attribútummal és az esetleg frissített `href` értékekkel. A fájlt megnyithatod egy böngészőben, hogy ellenőrizd, minden link új lapon nyílik-e meg.

## 5. lépés: Az eredmény ellenőrzése (opcionális)

Egy gyors szanitás ellenőrzés segít megerősíteni, hogy a művelet sikeres volt:

```python
# Reload the saved file to verify changes
verify_doc = HTMLDocument("YOUR_DIRECTORY/index_modified.html")
for link in verify_doc.query_selector_all("a"):
    assert link.get_attribute("target") == "_blank", "Target attribute not set correctly"
print("All links have target='_blank' and the file was saved successfully.")
```

Ha az állítás meghiúsul, a szkript hibát dob, és rámutat a problémás elemre.

## Profi tipp: Több fájl kötegelt feldolgozása

Ha egy könyvtárban sok HTML fájl található, csomagold a logikát egy függvénybe, és iterálj minden fájlon:

```python
import os
from aspose.html import HTMLDocument

def process_file(input_path: str, output_path: str, base_url: str = None):
    doc = HTMLDocument(input_path)
    for link in doc.query_selector_all("a"):
        if base_url:
            href = link.get_attribute("href")
            if href and not href.startswith("http"):
                link.set_attribute("href", base_url + href.lstrip("/"))
        link.set_attribute("target", "_blank")
    doc.save(output_path)

source_dir = "YOUR_DIRECTORY"
for filename in os.listdir(source_dir):
    if filename.endswith(".html"):
        src = os.path.join(source_dir, filename)
        dst = os.path.join(source_dir, f"{os.path.splitext(filename)[0]}_modified.html")
        process_file(src, dst, base_url="https://example.com/")
```

Ez a minta skálázza a **save modified html** munkafolyamatot tetszőleges számú oldalra, miközben következetesen **add target blank links** és **change href target** műveleteket hajt végre.

## Várt kimenet

A `index_modified.html` megnyitása a böngészőben ugyanazt a vizuális elrendezést kell, hogy mutassa, mint az eredeti oldal, de minden hiperhivatkozás most már tartalmazza:

```html
<a href="https://example.com/about.html" target="_blank">About Us</a>
```

A linkre kattintva a cél új böngészőlapon nyílik meg, megőrizve a felhasználó aktuális oldalát.

## Gyakori buktatók és hogyan kerüld el őket

| Buktató | Magyarázat | Megoldás |
|---------|-------------|-----|
| Missing Aspose.HTML license | A könyvtár futásidőben licenchibát dob. | Szerezz be egy licencfájlt, és a dokumentum betöltése előtt állítsd be: `aspose.html.License().set_license("license_path")`. |
| Relative URLs that start with `//` | Protokoll‑relatív URL‑ként kezelődnek, és változatlanul maradhatnak. | Ellenőrizd a `href.startswith("//")` feltételt, és szükség esetén előtagként add hozzá a `https:`-t. |
| Very large HTML files | Nagy fájlok betöltése jelentős memóriát fogyaszthat. | Használj streaming API‑kat, vagy oszd fel a fájlt kisebb fragmentumokra, ha a memória szűkölködik. |

## Összegzés

Most már tudod, hogyan **save modified HTML** után alkalmazd a **add target blank links**, **change href target**, és biztosítsd a **open all links newtab** funkciót az Aspose.HTML for Python segítségével. A teljes megoldás betölti a HTML fájlt, frissíti az összes `<a>` elemet, és az eredményt egy új fájlba írja, kezelve az olyan edge case‑eket, mint a meglévő `target` attribútumok és a relatív URL‑k.

A következőket is érdemes felfedezni:

* CSS szelektorok használata csak külső linkek célzásához (`a[href^="http"]`)  
* JavaScript beágyazása, amely `rel="noopener"` attribútumot ad hozzá a biztonság érdekében új lapok megnyitásakor  
* A módosított HTML konvertálása PDF‑be az Aspose.PDF for Python segítségével  

Nyugodtan adaptáld a kódot a saját projektstruktúrádhoz, és kísérletezz további DOM‑manipulációkkal. Boldog kódolást!

## Mit érdemes még megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek további API‑funkciók elsajátításában és alternatív megvalósítási megközelítések felfedezésében a saját projektjeidben.

- [Hogyan mentsünk HTML-t PDF-be az Aspose.HTML for Python segítségével](/html/english/python/general/how-to-save-html-as-pdf-with-aspose-html-for-python/)
- [Hogyan mentsünk HTML-t Markdown formátumba az Aspose.HTML for Python segítségével](/html/english/python/general/how-to-save-html-as-markdown-with-aspose-html-for-python/)
- [Hogyan használjuk az Aspose‑t – HTML konvertálása Markdown-re és linkek kinyerése](/html/english/python/general/how-to-use-aspose-convert-html-to-markdown-and-extract-links/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}