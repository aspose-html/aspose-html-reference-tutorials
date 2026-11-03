---
category: general
date: 2026-07-02
description: Jak extrahovat ikony z HTML souboru pomocí Pythonu. Naučte se číst HTML
  soubor v Pythonu, parsovat HTML dokument a extrahovat atribut href pro získání URL
  favikonů.
draft: false
keywords:
- how to extract icons
- read html file python
- parse html document
- extract href attribute
- extract favicon urls
language: cs
og_description: Jak extrahovat ikony z HTML stránky pomocí Pythonu. Tento tutoriál
  vám ukáže, jak načíst HTML soubor v Pythonu, parsovat dokument a získat URL favikon.
og_title: Jak extrahovat ikony z HTML – průvodce Pythonem
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
title: Jak extrahovat ikony z HTML pomocí Pythonu – kompletní průvodce
url: /cs/python/general/how-to-extract-icons-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak extrahovat ikony z HTML pomocí Pythonu – Kompletní průvodce

Už jste se někdy zamysleli **jak extrahovat ikony** z webové stránky bez otevření prohlížeče? Možná vytváříte katalog stránek, nástroj pro SEO audit, nebo jste jen zvědaví na ty malé favikony, které se objevují na kartách. Dobrou zprávou je, že to můžete udělat v několika řádcích Pythonu – žádný Selenium, žádný headless Chrome, jen obyčejný textový soubor HTML.

V tomto tutoriálu si projdeme načtení HTML souboru v Pythonu, parsování HTML dokumentu a nakonec **extrahování atributu href** z `<link rel="icon">` tagů, abychom získali URL favikon. Na konci budete mít znovupoužitelný úryvek kódu, který funguje na jakémkoli statickém HTML, které mu předáte, a také uvidíte, jak zacházet s okrajovými případy, jako jsou relativní cesty nebo více deklarací ikon.

## Co se naučíte

- Načíst lokální HTML soubor pomocí Pythonu (read html file python)  
- Použít lehký parser k **parse html document** bezpečně  
- Najít `<link>` elementy, které deklarují ikonu  
- **Extract href attribute** hodnoty a převést je na absolutní URL  
- Shromáždit a vypsat všechny nalezené **favicon URLs**  

Nejsou potřeba žádné externí služby – jen standardní knihovna a populární balíček **BeautifulSoup**.

![Snímek obrazovky ukazující Python skript extrahující ikony – jak extrahovat ikony](https://example.com/images/extract-icons-python.png "jak extrahovat ikony")

*Text alternativy obrázku: "jak extrahovat ikony pomocí Python skriptu"*

## Požadavky

- Python 3.8+ nainstalován  
- knihovna `beautifulsoup4` (`pip install beautifulsoup4`)  
- Lokální HTML soubor, který chcete prohledat (např. `sample.html`)  

Pokud je již máte, pojďme na to.

## Krok 1: Načtení HTML souboru v Pythonu – Načtení dokumentu

Nejprve musíme otevřít soubor a předat jeho obsah parseru. Použití `with open(..., "r", encoding="utf‑8")` zaručuje, že soubor bude automaticky uzavřen, a kódování UTF‑8 zvládne většinu moderních stránek.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Step 1: Load the HTML document from disk
html_path = Path("sample.html")          # adjust the path as needed
html_content = html_path.read_text(encoding="utf-8")
```

**Proč je to důležité:** Otevření souboru s správným kódováním zabraňuje tajemným znakům `�`, které by mohly později rozbít parser. Použití `Path` ze standardní knihovny také činí kód multiplatformním.

## Krok 2: Parsování HTML dokumentu – Najít všechny odkazy na ikony

Nyní předáme surové HTML **BeautifulSoup**, která vytvoří navigovatelný strom. Budeme hledat každý `<link>` tag, jehož atribut `rel` obsahuje slovo `icon`. Všimněte si, že `rel` může být seznam oddělený mezerami (`rel="shortcut icon"`), takže potřebujeme flexibilní kontrolu.

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

**Proč je tento krok klíčový:** Naivní `soup.find_all("link", rel="icon")` by minulo varianty jako `rel="shortcut icon"` nebo `rel="apple-touch-icon"`. Náš pomocný `is_icon_link` pokrývá tyto případy a dělá extrakci robustní.

## Krok 3: Extrahování atributu href – Získání URL

S relevantními tagy shromážděnými nyní získáme atribut `href` z každého. Některé stránky mohou `href` vynechat (vzácně, ale možné), takže se chráníme před `None`. Navíc jsou favikony často specifikovány relativními URL, takže je vyřešíme vůči základní URL stránky, pokud ji znáte. Pro lokální soubor ponecháme cestu tak, jak je.

```python
# Step 3: Grab the href attribute from each icon link
icon_urls = []
for tag in icon_links:
    href = tag.get("href")
    if href:
        icon_urls.append(href.strip())
```

**Proč odstraňujeme mezery:** Autoři HTML někdy omylem přidají mezery kolem URL, což by rozbilo následný požadavek. Ořezání zajišťuje čisté řetězce.

## Krok 4: Extrahování URL favikon – Výstup výsledků

Nakonec vypíšeme (nebo vrátíme) seznam nalezených URL. Ve skutečném skriptu je můžete zapsat do CSV, stáhnout ikony, nebo předat dalšímu servisu. Zde je jednoduchá smyčka, která ukazuje výsledek v konzoli.

```python
# Step 4: Display each discovered favicon URL
if not icon_urls:
    print("No icon links found in the document.")
else:
    for url in icon_urls:
        print("Favicon URL:", url)
```

### Řešení okrajových případů

- **Multiple rel values:** Naše kontrola `is_icon_link` již zachytí `rel="shortcut icon"` a `rel="apple-touch-icon"`.  
- **Relative paths:** Pokud později potřebujete absolutní URL, použijte `urllib.parse.urljoin(base_url, href)`.  
- **Missing href:** Ochrana `if href:` přeskočí poškozené tagy, čímž se vyhnete chybám `NoneType`.  
- **Duplicate entries:** Můžete použít `icon_urls = list(dict.fromkeys(icon_urls))` pro odstranění duplicit.

---

## Kompletní skript – Jedno‑stop řešení

Spojením všeho dohromady získáte kompletní, připravený ke spuštění program. Uložte jej jako `extract_icons.py` a nastavte `html_path` na libovolný soubor.

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

**Očekávaný výstup** (předpokládáme, že `sample.html` obsahuje dvě ikony):

```
Favicon URL: /images/favicon.ico
Favicon URL: https://example.com/assets/apple-touch-icon.png
```

Spusťte jej pomocí `python extract_icons.py` a uvidíte URL vytištěné v konzoli.

## Často kladené otázky

**Q: Co když HTML používá `<meta>` tagy pro ikony?**  
A: Některé stránky vkládají ikony pomocí `<meta itemprop="image">`. Rozšiřte `is_icon_link`, aby také kontroloval `meta` s `itemprop="image"` a získal jeho atribut `content`.

**Q: Můžu ikony stáhnout automaticky?**  
A: Ano – stačí předat každou URL do `requests.get(url, stream=True)` a zapsat obsah do souboru. Nezapomeňte řešit relativní URL pomocí `urljoin`.

**Q: Funguje to i na vzdálených stránkách?**  
A: Rozhodně. Nahraďte krok čtení souboru voláním `requests.get(page_url).text` a předávejte HTML řetězec do BeautifulSoup. Jen buďte opatrní na robots.txt a limity rychlosti.

## Závěr

Probrali jsme **jak extrahovat ikony** z libovolného statického HTML pomocí Pythonu, od načtení souboru po vytištění každé URL favikony. Základní myšlenky – načtení souboru, parsování dokumentu, nalezení správných tagů a získání atributu `href` – jsou znovupoužitelné vzory, se kterými se setkáte při mnoha úlohách web‑scrapingu.

Další kroky? Zkuste rozšířit skript o:

- Vyřešit relativní URL vůči základní URL stránky  
- Stáhnout každou ikonu a uložit ji lokálně  
- Podporovat další formáty ikon (`rel="mask-icon"` pro Safari)  

Klidně experimentujte, a pokud narazíte na podivnosti, zanechte komentář níže. Šťastné parsování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným vysvětlením, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy ve vašich projektech.

- [Jak dotazovat HTML v Javě – Kompletní tutoriál](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Jak upravit strom HTML dokumentu v Aspose.HTML pro Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Uložit HTML dokument do souboru v Aspose.HTML pro Java](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}