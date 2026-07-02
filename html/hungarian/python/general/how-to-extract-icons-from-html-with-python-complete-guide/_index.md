---
category: general
date: 2026-07-02
description: Hogyan lehet ikonokat kinyerni egy HTML-fájlból Python segítségével.
  Tanulja meg, hogyan olvasson be HTML-fájlt Pythonban, hogyan elemezze a HTML-dokumentumot,
  és hogyan nyerje ki a href attribútumot a favicon URL-ek megszerzéséhez.
draft: false
keywords:
- how to extract icons
- read html file python
- parse html document
- extract href attribute
- extract favicon urls
language: hu
og_description: Hogyan lehet ikonokat kinyerni egy HTML oldalról Python segítségével.
  Ez a bemutató megmutatja, hogyan olvassunk be HTML-fájlt Pythonban, hogyan elemezzük
  a dokumentumot, és hogyan nyerjük ki a favicon URL-eket.
og_title: Hogyan nyerjünk ki ikonokat HTML-ből – Python útmutató
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: How to extract icons from an HTML file using Python. Learn to read
    HTML file python, parse HTML document, and extract href attribute to get favicon
    URLs.
  headline: How to Extract Icons from HTML with Python – Complete Guide
  type: TechArticle
- questions:
  - answer: Some sites embed icons via `<meta itemprop="image">`. Extend `is_icon_link`
      to also check for `meta` with `itemprop="image"` and pull its `content` attribute.
    question: What if the HTML uses `<meta>` tags for icons?
  - answer: Yes—just feed each URL into `requests.get(url, stream=True)` and write
      the content to a file. Remember to handle relative URLs with `urljoin`.
    question: Can I fetch the icons automatically?
  - answer: 'Absolutely. Replace the file‑reading step with `requests.get(page_url).text`
      and pass the HTML string to BeautifulSoup. Just be mindful of robots.txt and
      rate limits. --- ## Wrap‑Up We’ve covered **how to extract icons** from any
      static HTML using Python, from reading the file to printing out each f'
    question: Does this work on remote pages?
  type: FAQPage
tags:
- python
- html-parsing
- web‑scraping
- favicon
title: Hogyan lehet ikonokat kinyerni HTML‑ből Python segítségével – Teljes útmutató
url: /hu/python/general/how-to-extract-icons-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan vonjunk ki ikonokat HTML‑ből Python‑nal – Teljes útmutató

Gondolkodtál már azon, **hogyan vonjunk ki ikonokat** egy weboldalról anélkül, hogy böngészőt nyitnál? Lehet, hogy egy webkatalógust, egy SEO audit eszközt építesz, vagy egyszerűen csak kíváncsi vagy a tabokban megjelenő apró favikonokra. A jó hír, hogy néhány Python‑sorral megoldható – nincs szükség Seleniumra, headless Chrome‑ra, csak egy egyszerű szöveges HTML‑fájlra.

Ebben az útmutatóban végigvezetünk egy HTML‑fájl Python‑ban történő beolvasásán, a HTML‑dokumentum elemzésén, és végül **a href attribútum kinyerésén** a `<link rel="icon">` tagekből, hogy megkapjuk a favicon URL‑eket. A végére egy újrahasználható kódrészletet kapsz, amely bármely statikus HTML‑en működik, és megmutatjuk, hogyan kezeljünk olyan szélhelyzeteket, mint a relatív útvonalak vagy a több ikon deklarációja.

## Mit fogsz megtanulni

- Tölts be egy helyi HTML‑fájlt Python‑nal (read html file python)  
- Használj egy könnyűsúlyú elemzőt a **html dokumentum feldolgozásához** biztonságosan  
- Keress `<link>` elemeket, amelyek ikont deklarálnak  
- **A href attribútum** értékeinek kinyerése és abszolút URL‑ekké alakítása  
- Gyűjtsd össze és írd ki az összes felfedezett **favicon URL‑t**  

Nincs szükség külső szolgáltatásokra – csak a standard könyvtár és a népszerű **BeautifulSoup** csomag.

![Képernyőkép, amely a Python‑szkript ikonjainak kinyerését mutatja – hogyan vonjunk ki ikonokat](https://example.com/images/extract-icons-python.png "hogyan vonjunk ki ikonokat")
*Kép alternatív szövege: "hogyan vonjunk ki ikonokat egy Python‑szkripttel"*

## Előfeltételek

- Python 3.8+ telepítve  
- `beautifulsoup4` könyvtár (`pip install beautifulsoup4`)  
- Egy helyi HTML‑fájl, amelyet be szeretnél olvasni (pl. `sample.html`)  

Ha már megvannak, ugorjunk bele.

## 1. lépés: HTML‑fájl beolvasása Python‑nal – Dokumentum betöltése

Először is: meg kell nyitnunk a fájlt, és a tartalmát egy elemzőnek átadni. A `with open(..., "r", encoding="utf‑8")` használata garantálja, hogy a fájl automatikusan bezáródik, és az UTF‑8 kódolás a legtöbb modern oldalt helyesen kezeli.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Step 1: Load the HTML document from disk
html_path = Path("sample.html")          # adjust the path as needed
html_content = html_path.read_text(encoding="utf-8")
```

**Miért fontos ez:** A fájl a megfelelő kódolással való megnyitása megakadályozza a rejtélyes `�` karakterek megjelenését, amelyek később tönkretehetik az elemzőt. A standard könyvtár `Path`‑jának használata szintén platform‑függetlenné teszi a kódot.

## 2. lépés: HTML‑dokumentum elemzése – Az összes ikon‑link megtalálása

Most átadjuk a nyers HTML‑t a **BeautifulSoup**‑nak, amely egy navigálható fát épít. Megkeressük minden `<link>` tag-et, amelynek a `rel` attribútuma tartalmazza az `icon` szót. Figyeljünk, hogy a `rel` lehet szóközzel elválasztott lista (`rel="shortcut icon"`), ezért rugalmas ellenőrzésre van szükség.

```python
# Step 2: Parse the HTML and locate <link> tags that declare an icon
soup = BeautifulSoup(html_content, "html.parser")

def is_icon_link(tag):
    """Return True if a <link> tag declares an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    # BeautifulSoup may return a list or a string; handle both
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

icon_links = [tag for tag in soup.find_all(is_icon_link)]
```

**Miért kulcsfontosságú ez a lépés:** Egy naiv `soup.find_all("link", rel="icon")` kihagyja a `rel="shortcut icon"` vagy `rel="apple-touch-icon"` változatokat. A mi segédfüggvényünk `is_icon_link` lefedi ezeket az eseteket, így a kinyerés robusztus.

## 3. lépés: href attribútum kinyerése – URL‑ek lekérése

Miután összegyűjtöttük a releváns tageket, most kinyerjük mindegyikből a `href` attribútumot. Egyes oldalak elhagyhatják a `href`‑t (ritka, de előfordulhat), ezért ellenőrizzük, hogy ne legyen `None`. Továbbá a favikonok gyakran relatív URL‑ekkel vannak megadva, ezért a lap alap‑URL‑jével fogjuk őket feloldani, ha ismered. Helyi fájl esetén egyszerűen megtartjuk az útvonalat változatlanul.

```python
# Step 3: Grab the href attribute from each icon link
icon_urls = []
for tag in icon_links:
    href = tag.get("href")
    if href:
        icon_urls.append(href.strip())
```

**Miért távolítjuk el a szóközöket:** A HTML‑szerzők néha véletlenül szóközöket helyeznek az URL‑ek köré, ami egy későbbi kérésnél hibát okozhat. A vágás biztosítja, hogy tiszta karakterláncokat kapjunk.

## 4. lépés: Favicon URL‑ek kinyerése – Eredmények kiírása

Végül kiírjuk (vagy visszaadjuk) a felfedezett URL‑ek listáját. Egy valós környezetben a szkript esetleg CSV‑be írná őket, letöltené az ikonokat, vagy egy másik szolgáltatásba továbbítaná. Íme egy egyszerű ciklus, amely a konzolon mutatja az eredményt.

```python
# Step 4: Display each discovered favicon URL
if not icon_urls:
    print("No icon links found in the document.")
else:
    for url in icon_urls:
        print("Favicon URL:", url)
```

### Szélhelyzetek kezelése

- **Több rel érték:** A `is_icon_link` ellenőrzésünk már elkapja a `rel="shortcut icon"` és a `rel="apple-touch-icon"` értékeket.  
- **Relatív útvonalak:** Ha később abszolút URL‑ekre van szükséged, használd a `urllib.parse.urljoin(base_url, href)` függvényt.  
- **Hiányzó href:** Az `if href:` ellenőrzés kihagyja a hibás tageket, elkerülve a `NoneType` hibákat.  
- **Duplikált bejegyzések:** A `icon_urls = list(dict.fromkeys(icon_urls))` kifejezéssel szűrheted ki a duplikátumokat.

---

## Teljes szkript – Egy‑állomásos megoldás

Összegezve, itt a teljes, azonnal futtatható program. Mentsd el `extract_icons.py`‑ként, és állítsd be az `html_path`‑t bármelyik kívánt fájlra.

```python
#!/usr/bin/env python3
"""
How to extract icons from an HTML file using Python.

This script:
- Reads an HTML file (read html file python)
- Parses the HTML document (parse html document)
- Finds <link> tags with rel containing "icon"
- Extracts the href attribute (extract href attribute)
- Prints each favicon URL (extract favicon urls)
"""

from pathlib import Path
from bs4 import BeautifulSoup

def is_icon_link(tag):
    """Detect <link> tags that declare an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

def extract_favicon_urls(html_path: Path):
    """Return a list of favicon URLs found in the given HTML file."""
    html_content = html_path.read_text(encoding="utf-8")
    soup = BeautifulSoup(html_content, "html.parser")
    icon_links = [t for t in soup.find_all(is_icon_link)]

    urls = []
    for tag in icon_links:
        href = tag.get("href")
        if href:
            urls.append(href.strip())
    # Remove duplicates while preserving order
    return list(dict.fromkeys(urls))

if __name__ == "__main__":
    # Adjust the path to point to your HTML file
    html_file = Path("sample.html")
    favicon_urls = extract_favicon_urls(html_file)

    if not favicon_urls:
        print("No icon links found in the document.")
    else:
        for url in favicon_urls:
            print("Favicon URL:", url)
```

**Várható kimenet** (feltételezve, hogy a `sample.html` két ikont tartalmaz):

```
Favicon URL: /images/favicon.ico
Favicon URL: https://example.com/assets/apple-touch-icon.png
```

Futtasd a `python extract_icons.py` paranccsal, és a konzolon megjelennek az URL‑ek.

## Gyakran Ismételt Kérdések

**Q: Mi van, ha a HTML `<meta>` tageket használ ikonokhoz?**  
A: Néhány oldal `<meta itemprop="image">` segítségével ágyazza be az ikonokat. Bővítsd a `is_icon_link`‑et, hogy ellenőrizze a `meta`‑t `itemprop="image"` attribútummal, és a `content` attribútumát vedd ki.

**Q: Letölthetem automatikusan az ikonokat?**  
A: Igen – egyszerűen add át minden URL‑t a `requests.get(url, stream=True)` függvénynek, és írd a tartalmat fájlba. Ne feledd a relatív URL‑ek kezelését a `urljoin`‑nal.

**Q: Működik ez távoli oldalakon is?**  
A: Teljesen. Cseréld le a fájl‑olvasási lépést a `requests.get(page_url).text`‑re, és add át a HTML‑szöveget a BeautifulSoup‑nak. Csak vedd figyelembe a robots.txt‑t és a lekérdezési korlátokat.

## Összegzés

Áttekintettük, **hogyan vonjunk ki ikonokat** bármely statikus HTML‑ből Python‑nal, a fájl beolvasásától a favicon URL‑ek kiírásáig. A fő gondolatok – a fájl beolvasása, a dokumentum elemzése, a megfelelő tagek megtalálása és a `href` attribútum kinyerése – újrahasználható minták, amelyekkel számos web‑kaparási feladat során találkozni fogsz.

Következő lépések? Próbáld bővíteni a szkriptet a következőkkel:

- Relatív URL‑ek feloldása a lap alap‑URL‑jével  
- Minden ikon letöltése és helyi mentése  
- További ikonformátumok támogatása (`rel="mask-icon"` Safari‑hoz)  

Nyugodtan kísérletezz, és ha bármilyen furcsasággal találkozol, hagyj egy megjegyzést alább. Jó kaparást!

## Mit érdemes legközelebb megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API‑funkciókat, és alternatív megvalósítási megközelítéseket fedezhess fel saját projektjeidben.

- [Hogyan kérdezzünk le HTML‑t Java‑ban – Teljes útmutató](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Hogyan szerkesszük a HTML‑dokumentum fát Aspose.HTML for Java‑ban](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [HTML‑dokumentum mentése fájlba Aspose.HTML for Java‑ban](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}