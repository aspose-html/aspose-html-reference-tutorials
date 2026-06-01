---
category: general
date: 2026-05-31
description: Naučte se, jak stahovat ikony pomocí Pythonu. Také se podíváme na to,
  jak extrahovat favicon, číst HTML dokument v Pythonu a zapisovat binární soubory
  v Pythonu, vše v jednom tutoriálu.
draft: false
keywords:
- how to download icons
- how to extract favicon
- write binary file python
- read html document python
- load html python
language: cs
og_description: Jak stahovat ikony pomocí Pythonu, krok za krokem. Naučte se extrahovat
  favicon, číst HTML dokument v Pythonu a zapisovat binární soubor v Pythonu.
og_title: Jak stáhnout ikony pomocí Pythonu – kompletní průvodce
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to download icons using Python. We'll also cover how to extract
    favicon, read HTML document Python, and write binary file python in a single tutorial.
  headline: How to Download Icons with Python – Complete Guide
  type: TechArticle
tags:
- python
- web-scraping
- favicon
- file-io
title: Jak stáhnout ikony pomocí Pythonu – kompletní průvodce
url: /cs/python/general/how-to-download-icons-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak stáhnout ikony pomocí Pythonu – Kompletní průvodce

Už jste se někdy zamýšleli **jak stáhnout ikony** z webové stránky, aniž byste museli ručně pravým tlačítkem kliknout na každou z nich? Nejste sami. Ať už vytváříte nástroj pro audit značek nebo jen chcete mít lokální kopii každé favikony, na kterou narazíte, zvládnutí tohoto úkolu vám ušetří čas i úsilí.

V tomto tutoriálu si ukážeme **jak stáhnout ikony** z HTML souboru pomocí čistého Pythonu. Také vám ukážeme **jak extrahovat favicon**, předvedeme **read html document python** a vysvětlíme **write binary file python**, abyste získali přehlednou složku .ico souborů připravených pro jakýkoli projekt.

---

## Co budete potřebovat

- Python 3.8+ (standardní knihovna stačí)
- Lokální kopie HTML stránky, kterou chcete prohledat (nebo URL, kterou můžete stáhnout)
- Základní znalost práce se soubory v Pythonu  
- Žádné externí balíčky nejsou vyžadovány, ale `beautifulsoup4` může práci usnadnit, pokud jej preferujete (volitelné)

Máte to? Skvělé — pojďme na to.

![Příklad stažení ikon](https://example.com/placeholder.png "how to download icons example")

---

## Krok 1: Načtěte HTML dokument v Pythonu  

Nejprve musíme **load html python** styl—načíst soubor do paměti, abychom mohli prozkoumat jeho `<link>` tagy. Nejjednodušší je otevřít soubor vestavěnou funkcí `open` a přečíst jej jako text.

```python
# Step 1: Load the HTML document
HTML_PATH = "YOUR_DIRECTORY/sample.html"

# Using the built‑in open() to read the file as a string
with open(HTML_PATH, "r", encoding="utf-8") as f:
    html_content = f.read()
```

*Proč je tento krok důležitý?*  
Načtení HTML nám poskytne surový řetězec, který můžeme parsovat. Pokud tento krok přeskočíte a pokusíte se pracovat přímo s cestou, parser nebude mít co zkoumat.

---

## Krok 2: Parsujte dokument a najděte odkazy na ikony  

Nyní potřebujeme **read html document python** styl. I když by šlo použít regulární výrazy, malý HTML parser je spolehlivější. Python obsahuje `html.parser`, který si můžeme podtřídit pro náš účel.

```python
from html.parser import HTMLParser

class IconLinkParser(HTMLParser):
    """Collects href attributes from <link rel='icon'> tags."""
    def __init__(self):
        super().__init__()
        self.icon_hrefs = []

    def handle_starttag(self, tag, attrs):
        if tag.lower() != "link":
            return
        attrs_dict = dict(attrs)
        # Look for rel="icon" (or rel="shortcut icon")
        rel = attrs_dict.get("rel", "").lower()
        if "icon" in rel:
            href = attrs_dict.get("href")
            if href:
                self.icon_hrefs.append(href)

# Instantiate and feed the HTML content
parser = IconLinkParser()
parser.feed(html_content)

# Now we have a list of all icon URLs
icon_hrefs = parser.icon_hrefs
print(f"Found {len(icon_hrefs)} icon link(s):", icon_hrefs)
```

**Vysvětlení**  
- `handle_starttag` se spustí pro každý otevírací tag.  
- Filtrujeme `<link>` elementy, jejichž atribut `rel` obsahuje slovo *icon*. To zahrnuje jak `rel="icon"`, tak starší `rel="shortcut icon"`.  
- Hodnoty `href` ukládáme do `icon_hrefs`, připravené pro další krok.

---

## Krok 3: Převod relativních cest (volitelné, ale užitečné)

Pokud HTML používá relativní URL, musíme je převést na absolutní cesty v souborovém systému. Zde se setkává **load html python** znalost s `urllib.parse`.

```python
import os
from urllib.parse import urljoin

# Base directory where the HTML file lives
BASE_DIR = os.path.dirname(os.path.abspath(HTML_PATH))

def resolve_path(href):
    # If href already looks like an absolute path, return it unchanged
    if os.path.isabs(href):
        return href
    # Otherwise, join it with the base directory
    return os.path.normpath(os.path.join(BASE_DIR, href))

resolved_icon_paths = [resolve_path(h) for h in icon_hrefs]
print("Resolved paths:", resolved_icon_paths)
```

*Proč se tím zabývat?*  
Když později **write binary file python**, potřebujete skutečnou cestu k souboru. Relativní URL jako `images/favicon.ico` by jinak vedly k `FileNotFoundError`.

---

## Krok 4: Zapište každou ikonu do lokálního binárního souboru  

Tady je jádro **how to download icons**. Projdeme všechny vyřešené cesty, načteme každou ikonu jako binární data a zapíšeme ji do nového souboru ve složce `icons/`.

```python
import shutil

OUTPUT_DIR = "YOUR_DIRECTORY/icons"
os.makedirs(OUTPUT_DIR, exist_ok=True)

for index, icon_path in enumerate(resolved_icon_paths):
    # Guard against missing files
    if not os.path.isfile(icon_path):
        print(f"⚠️  Icon file not found: {icon_path}")
        continue

    # Destination filename: icon_0.ico, icon_1.ico, …
    dest_path = os.path.join(OUTPUT_DIR, f"icon_{index}.ico")

    # **write binary file python** – copy the binary data
    with open(icon_path, "rb") as src_file, open(dest_path, "wb") as dst_file:
        shutil.copyfileobj(src_file, dst_file)

    print(f"✅ Saved {dest_path}")
```

**Co se děje?**  

- `os.makedirs(..., exist_ok=True)` zajistí, že výstupní složka existuje.  
- `shutil.copyfileobj` streamuje bajty ze zdroje do cíle, což je nejpaměťově úspornější způsob, jak **write binary file python**.  
- Každý soubor pojmenujeme `icon_<index>.ico`, abychom předešli kolizím.

**Očekávaný výstup**

```
Found 2 icon link(s): ['images/favicon.ico', 'icons/custom.ico']
Resolved paths: ['/path/to/YOUR_DIRECTORY/images/favicon.ico',
                '/path/to/YOUR_DIRECTORY/icons/custom.ico']
✅ Saved YOUR_DIRECTORY/icons/icon_0.ico
✅ Saved YOUR_DIRECTORY/icons/icon_1.ico
```

Po dokončení skriptu budete mít čistou kolekci souborů s ikonami připravenou pro jakýkoli následný úkol.

---

## Krok 5: Bonus – Stáhněte ikony přímo z vzdálené URL  

Pokud se vaše HTML nachází na webu místo lokálního disku, nahraďte část čtení souboru malým voláním `requests`. Tento úsek ukazuje **how to extract favicon** z libovolné živé stránky.

```python
import requests

REMOTE_URL = "https://example.com"

# Grab the HTML
response = requests.get(REMOTE_URL)
response.raise_for_status()
html_content = response.text

# Re‑run the parser (same as before) to get icon URLs
parser = IconLinkParser()
parser.feed(html_content)
icon_hrefs = parser.icon_hrefs

# Download each icon via HTTP
for index, href in enumerate(icon_hrefs):
    # Resolve relative URLs against the page URL
    icon_url = urljoin(REMOTE_URL, href)
    r = requests.get(icon_url, stream=True)
    r.raise_for_status()
    dest_path = os.path.join(OUTPUT_DIR, f"remote_icon_{index}.ico")
    with open(dest_path, "wb") as out_file:
        shutil.copyfileobj(r.raw, out_file)
    print(f"✅ Downloaded {icon_url} → {dest_path}")
```

*Proč to přidat?*  
Mnoho reálných projektů potřebuje stahovat favikony z živých webů. Tento úryvek vám ukáže, jak rozšířit stejnou logiku **how to download icons** na internet pomocí jen několika řádků.

---

## Časté úskalí a tipy

- **Chybějící `rel="icon"`** – Některé stránky vkládají ikony přes `<meta>` tagy nebo CSS. Pokud je potřebujete, rozšiřte parser o hledání `<meta name="msapplication‑TileImage">` nebo URL v `background-image`.  
- **Formáty jiné než ICO** – Moderní favikony často používají `.png` nebo `.svg`. Výše uvedený kód funguje pro jakýkoli binární obrázek; stačí upravit příponu v `dest_path`, pokud chcete zachovat původní formát.  
- **Chyby oprávnění** – Při zápisu souborů se ujistěte, že skript má právo zapisovat do cílové složky. Použití `os.makedirs(..., exist_ok=True)` zabraňuje pádům s chybou „adresář nenalezen“.  
- **Velké HTML soubory** – Pro obrovské stránky zvažte čtení souboru po řádcích místo načítání celého řetězce do paměti. Vestavěný `HTMLParser` dokáže zpracovávat data po částech.

---

## Závěr

Právě jste se naučili **how to download icons** z HTML dokumentu pomocí čistého Pythonu. Tím, že **read html document python**, parsujete `<link rel="icon">` tagy, vyřešíte relativní cesty a nakonec **write binary file python** uložíte každou ikonu lokálně, máte nyní znovupoužitelný skript fungující jak pro lokální, tak pro vzdálené stránky.  

Další kroky? Zkuste rozšířit parser tak, aby zachytil Apple touch ikony (`rel="apple-touch-icon"`), nebo integrujte skript do většího web‑crawling pipeline, která sbírá favikony pro stovky domén. Základy, které zde proběhly — parsování HTML, řešení cest a práce s binárními soubory — jsou stavebními kameny mnoha úloh automatizace webu.

Máte otázky nebo chcete sdílet zajímavý případ použití? Zanechte komentář níže a šťastné lovení ikon!

## Co se učit dál?

- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [How to Convert HTML to JPEG Using Aspose.HTML for Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-jpeg/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}