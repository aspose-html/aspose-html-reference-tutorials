---
category: general
date: 2026-10-21
description: Tanulja meg, hogyan kell HTML-t feldolgozni Pythonban, betölteni egy
  HTML-dokumentumot, CSS-szelektorokat használni, és gyorsan kinyerni a hiperhivatkozásokat
  a HTML-ből.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to parse html
- how to use selector
- extract hyperlinks from html
- load html document python
language: hu
lastmod: 2026-10-21
og_description: HTML feldolgozása Pythonban CSS szelektorokkal. HTML dokumentum betöltése,
  linkek kiválasztása és hiperhivatkozások kinyerése tiszta kóddal.
og_image_alt: Screenshot showing how to parse HTML in Python with CSS selectors
og_title: HTML feldolgozása Pythonban – lépésről lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to parse HTML in Python, load an HTML document, use CSS selectors,
    and extract hyperlinks from HTML quickly.
  headline: How to parse HTML in Python using CSS selectors
  type: TechArticle
tags:
- python
- html-parsing
- css-selectors
title: HTML feldolgozása Pythonban CSS szelektorok használatával
url: /hu/python/general/how-to-parse-html-in-python-using-css-selectors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML elemzés Pythonban CSS szelektorok használatával

Ha **how to parse html**-ra van szükséged egy Python szkriptben, ez az útmutató pontosan ezt mutatja be. Megtanulod, hogyan tölts be egy HTML dokumentumot, hogyan használd a selector szintaxist az elemek megtalálásához, és hogyan nyerj ki hiperhivatkozásokat a html-ből anélkül, hogy saját elemzőt írnál.

A HTML elemzés gyakori feladat a webkaparók, adat‑elemzési folyamatok vagy automatizált tesztelés számára. A tutorial végére lesz egy újrahasználható függvényed, amely betölti a HTML dokumentumot, kiválasztja az összes `<a>` elemet CSS szelektorral, és egy tiszta URL listát ad vissza.

## Amire szükséged lesz

- Python 3.8+ (a kód bármely friss verzión működik)  
- A **lxml** könyvtár (`pip install lxml`) – gyors HTML elemzést és CSS szelektor támogatást biztosít  
- Egy HTML fájl, amelyet elemezni szeretnél (pl. `sample.html`)  

Nem szükséges további eszköz; minden a standard könyvtárral és egyetlen harmadik‑féltől származó csomaggal fut.

## 1. lépés: HTML elemzés – a dokumentum betöltése

Az első lépés bármely HTML munkafolyamatban a fájl memóriába olvasása. A **lxml.html** használatával egy olyan faobjektumot kapsz, amely támogatja a CSS szelektorokat.

```python
# step_1_load.py
from lxml import html

def load_html(path: str) -> html.HtmlElement:
    """
    Load an HTML document from the given file path.
    Returns an lxml HtmlElement that can be queried with CSS selectors.
    """
    with open(path, "r", encoding="utf-8") as f:
        content = f.read()
    # Parse the raw HTML string into a tree
    return html.fromstring(content)

# Example usage
doc = load_html("sample.html")
print("Document loaded – ready for selector queries.")
```

**Miért fontos:**  
`load_html` elrejti a fájl‑olvasási sablont és garantálja, hogy a dokumentum egy toleráns HTML parserrel legyen feldolgozva. Ez a legbiztonságosabb módja a **load html document python**-nek, anélkül, hogy aggódnál a hibás jelölés miatt.

## 2. lépés: Selector használata – az összes hivatkozás elem megtalálása

Miután a dokumentum betöltődött, használhatsz CSS szelektort minden `<a>` tag megtalálásához. Az `"a"` szelektor minden horgonyelemre illeszkedik, de finomíthatod is (pl. `"a.external"` vagy `"nav a"`).

```python
# step_2_selector.py
def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    """
    Return a list of <a> elements using a CSS selector.
    This demonstrates how to use selector syntax with lxml.
    """
    # The CSS selector "a" selects every anchor tag
    return doc.cssselect("a")

# Example usage
links = select_links(doc)
print(f"Found {len(links)} <a> elements.")
```

**Miért fontos:**  
A **how to use selector** megközelítés lehetővé teszi összetett lekérdezések kifejezését egyetlen, olvasható karakterláncban, elkerülve a kézi fa bejárást. Bármely, az `lxml.cssselect` által támogatott CSS mintára működik.

## 3. lépés: Hiperhivatkozások kinyerése a HTML-ből és feldolgozása

Most, hogy van egy listád `<a>` elemekkel, kinyerheted minden egyes `href` attribútumát. Az alábbi segédfüggvény normalizálja a relatív URL-eket egy alap URL-hez képest (ha megadsz egyet).

```python
# step_3_extract.py
from urllib.parse import urljoin
from typing import Optional

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    """
    Return a list of href values from the given <a> elements.
    If base_url is supplied, relative URLs are resolved to absolute URLs.
    """
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            # Skip <a> tags without an href attribute
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

# Example usage
hyperlinks = extract_hyperlinks(links, base_url="https://example.com")
for url in hyperlinks:
    print(url)
```

**Várt kimenet** (feltételezve, hogy a `sample.html` három linket tartalmaz):

```
https://example.com/page1.html
https://example.com/page2.html
https://external.org/resource
```

**Miért fontos:**  
`extract_hyperlinks` a **extract hyperlinks from html** magja. Elegánsan kezeli a hiányzó `href` attribútumokat, feloldja a relatív linkeket, és egy egyszerű Python listát ad vissza, amelyet további feldolgozásra (pl. requests, pandas vagy adatbázis) használhatsz.

## Teljes vég‑től‑végig példa

A három függvény egyesítése egyetlen szkriptet eredményez, amely betölti a fájlt, kiválasztja az összes horgonyt, és kiírja minden hiperhivatkozást.

```python
# parse_links.py
from lxml import html
from urllib.parse import urljoin
from typing import Optional

def load_html(path: str) -> html.HtmlElement:
    with open(path, "r", encoding="utf-8") as f:
        return html.fromstring(f.read())

def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    return doc.cssselect("a")

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

if __name__ == "__main__":
    # 1️⃣ Load the HTML document
    document = load_html("sample.html")
    # 2️⃣ Use selector to grab all <a> tags
    anchor_elements = select_links(document)
    # 3️⃣ Extract and print each hyperlink
    for url in extract_hyperlinks(anchor_elements, base_url="https://example.com"):
        print(url)
```

A `python parse_links.py` futtatása minden hiperhivatkozást, teljesen feloldva, a konzolra ír ki. Ez a szkript bemutatja a **how to parse html**, **how to use selector**, és **extract hyperlinks from html** folyamatot egyetlen, újrahasználható áramlásban.

## Gyakori variációk és szélsőséges esetek kezelése

| Situation | What to change | Reason |
|-----------|----------------|--------|
| **Only absolute URLs needed** | Omit the `base_url` argument in `extract_hyperlinks` | Relatív URL-ek érintetlenül maradnak |
| **You need the link text as well** | Return a tuple `(href, link.text_content())` from `extract_hyperlinks` | Lehetővé teszi, hogy mind az URL-t, mind a horgonyszöveget tárold |
| **Large HTML files** | Use `lxml.etree.iterparse` with a CSS selector filter | Memóriahasználat csökkentése streaminggel |
| **Different selector** | Replace `"a"` with `"nav a[href]"` or `"div.content a.external"` | Egy linkcsoportot céloz meg, hasznos a **how to use selector**-hez összetett oldalaknál |

**Pro tipp:** Mindig ellenőrizd a kinyert URL-eket, mielőtt hálózati kéréseket küldenél. Egy gyors `urlparse` ellenőrzés kiszűrheti a hibás karakterláncokat és megvédi a kaparót a leállásoktól.

## Következtetés

Most már tudod, hogyan **how to parse html** Pythonban, hogyan **load html document python**, hogyan **how to use selector** segítségével célozhatsz elemeket, és hogyan **extract hyperlinks from html** hatékonyan. A fenti teljes példa készen áll a másolás‑beillesztésre a projektedbe, és minden függvényt testre szabhatsz fejlettebb felhasználási esetekhez, mint például lapozás, JavaScript‑generált tartalom vagy többoldalas feltérképezés.

Next steps you might explore include:

- A **requests‑html** vagy **Playwright** használata olyan oldalak lekéréséhez, amelyek JavaScript végrehajtást igényelnek.  
- A kinyert URL-ek tárolása CSV vagy SQLite adatbázisban későbbi elemzéshez.  
- Hiba‑kezelés hozzáadása hálózati időtúllépésekhez és HTTP státuszkódokhoz.

Boldog elemzést, és nyugodtan kísérletezz különböző szelektorokkal, hogy felszabadítsd a CSS‑alapú HTML lekérdezések teljes erejét Pythonban!

## Mit érdemes legközelebb megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljesen működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan konfiguráljuk a HTML erőforráskezelést Pythonban és töltsünk be egy HTML dokumentumot](/html/english/python/general/how-to-configure-html-resource-handling-in-python-and-load-a/)
- [HTML elemzés Pythonban – Teljes útmutató](/html/english/python/general/how-to-parse-html-in-python-complete-guide/)
- [HTML betöltése Pythonban – Lépésről‑lépésre útmutató](/html/english/python/general/how-to-load-html-in-python-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}