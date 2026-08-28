---
category: general
date: 2026-06-10
description: Načtěte HTML v Pythonu a extrahujte SVG obrázky ze svých stránek – krok
  za krokem kód, tipy a řešení okrajových případů.
draft: false
keywords:
- load html python
- extract svg images
- extract svg from html
- search html svg
- find inline svg
language: cs
og_description: Načtěte HTML v Pythonu a extrahujte SVG obrázky s jasným, spustitelným
  příkladem. Naučte se, jak vyhledávat HTML SVG elementy a řešit okrajové případy.
og_title: Načtení HTML v Pythonu – Efektivní extrakce SVG obrázků
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
title: Načtení HTML v Pythonu – Kompletní průvodce extrakcí SVG obrázků
url: /cs/python/general/load-html-in-python-complete-guide-to-extract-svg-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Načtení HTML v Pythonu – Kompletní průvodce extrakcí SVG obrázků

Už jste někdy potřebovali **load HTML in Python** jen proto, abyste získali všechny SVG grafiky z stránky? Nejste v tom sami. Ať už vytváříte web‑scraper, generujete zprávu o aktivech, nebo jste jen zvědaví na ikony, které stránka používá, znalost toho, jak **extract SVG images**, vám ušetří spoustu ručního hledání.

V tomto tutoriálu projdeme praktickým, end‑to‑end řešením, které **loads HTML in Python**, poté **searches HTML SVG** elementy, **finds inline SVG**, a dokonce zachytí externí SVG soubory odkazované pomocí značek `<img>`. Na konci budete mít znovupoužitelný skript, několik tipů pro obtížné části a jasnou představu o tom, jak vypadá výstup.

## Co si odnesete

* Plně spustitelný Python skript, který parsuje lokální HTML soubor (nebo staženou stránku) a vypíše všechny SVG, které najde.  
* Porozumění rozdílu mezi **inline SVG** (`<svg>…</svg>`) a **external SVG** (`<img src="… .svg">`).  
* Strategie pro zpracování špatně formovaného markupu, chybějících souborů a zvláštností jmenných prostorů.  
* Nápady, jak kód rozšířit – ukládat SVG, převádět je na PNG, nebo je vložit do databáze.

### Požadavky

* Nainstalovaný Python 3.8+.  
* Základní znalost knihoven Pythonu `requests` a `BeautifulSoup` (budeme je importovat, není potřeba hluboký ponor).  
* Lokální HTML soubor nebo URL, kterou chcete prohledat.  

Teď se ponořme.

## Načtení HTML v Pythonu – Nastavení parseru

Prvním krokem je **load HTML in Python**. Můžete buď načíst soubor z disku, nebo stáhnout vzdálenou stránku. Níže je minimální, ale robustní pomocník, který dělá obojí:

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

> **Proč je to důležité:** Použití `BeautifulSoup` abstrahuje zvláštnosti surového řetězcového parsování a funkce elegantně zvládá jak lokální soubory, tak vzdálené URL. Také vyvolá výjimku, pokud síťový požadavek selže – takže okamžitě poznáte, že se něco pokazilo.

## Extrakce SVG obrázků – Vyhledávání inline SVG elementů

Jakmile je dokument načten, dalším logickým krokem je **find inline SVG** značky. Inline SVG je vložený přímo v HTML markupu, což znamená, že jej můžete získat přímo z DOM.

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

*Pro tip:* Pokud stránka používá SVG jmenné prostory (`<svg xmlns="http://www.w3.org/2000/svg">`), `BeautifulSoup` stále najde značku, protože ve výchozím nastavení ignoruje jmenné prostory. To je pohodlné, když jen **searches HTML SVG**.

## Vyhledávání HTML SVG – Zpracování externích `<img>` odkazů

Mnoho stránek SVG neembeduje přímo; odkazují na externí soubory pomocí `<img src="icon.svg">`. Pro zachycení těchto musíme projít každou značku `<img>`, zkontrolovat její `src` a zjistit, zda končí na `.svg`.

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

> **Upozornění na okrajový případ:** Některé stránky používají dotazové řetězce (`icon.svg?v=2`) nebo fragmenty (`icon.svg#layer`). Kontrola `endswith(".svg")` stále funguje, protože se díváme jen na koncový, malými písmeny psaný řetězec. Pokud potřebujete přísnější validaci, zvažte použití `urllib.parse` k odebrání parametrů nejprve.

## Najděte inline SVG – Reportování výsledků

Nyní, když máme dva seznamy – jeden pro inline SVG markup a druhý pro odkazy na externí soubory – můžeme je sloučit a nahlásit celkový počet. Toto odráží původní úryvek, který jste zveřejnili, ale přidává trochu více kontextu.

```python
def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")
```

## Sestavení všeho dohromady – Kompletní skript

Níže je kompletní, připravený ke spuštění program. Uložte jej jako `extract_svg.py` a nasměrujte buď na lokální HTML soubor, nebo na URL.

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

### Očekávaný výstup

Spuštění skriptu proti ukázkovému `sample.html` může vyprodukovat:

```
Found 3 inline SVG element(s).
Found 2 external SVG reference(s).
Overall, 5 SVG item(s) detected.
Saved inline SVG #1 to inline_svg_1.svg
Saved inline SVG #2 to inline_svg_2.svg
Saved inline SVG #3 to inline_svg_3.svg
```

Pokud odkomentujete blok pro stahování, externí SVG

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Convert SVG to Image in .NET with Aspose.HTML](/html/english/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}