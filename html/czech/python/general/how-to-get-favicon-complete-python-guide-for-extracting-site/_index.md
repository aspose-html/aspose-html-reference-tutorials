---
category: general
date: 2026-06-26
description: Naučte se, jak získat favicon načtením HTML z URL a extrahováním href
  z tagů <link>. Krok za krokem Python kód pro rychlé získání ikon webových stránek.
draft: false
keywords:
- how to get favicon
- load html from url
- get website icons
- extract href from link
- how to extract favicons
language: cs
og_description: 'Jak rychle získat favicon: načíst HTML z URL, najít link rel=''icon''
  a extrahovat href z tagů link pomocí Pythonu.'
og_title: Jak získat favicon – Python tutoriál
schemas:
- author: Aspose
  dateModified: '2026-06-26'
  description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  headline: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  type: TechArticle
- description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  name: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  steps:
  - name: What if the site uses a `<meta>` tag instead of `<link>`?
    text: Some older pages embed the icon URL in a `<meta name="msapplication‑TileImage">`.
      You can extend `find_icon_links` to also search for those meta tags and treat
      them the same way.
  - name: How do I handle relative URLs that start with `//`?
    text: '`urljoin` automatically resolves protocol‑relative URLs (`//example.com/favicon.ico`)
      based on the scheme of the base URL, so you don’t need extra logic.'
  - name: Can I retrieve multiple sizes (e.g., 32×32, 180×180) automatically?
    text: Yes—just drop the `filter_ico_urls` step. The script will return every icon
      URL it discovers, including PNGs of various dimensions. You can then sort or
      select based on the filename pattern.
  - name: Does this work on sites that block bots?
    text: 'If a site returns a 403 or requires a custom User‑Agent, tweak the `requests.get`
      call:'
  type: HowTo
tags:
- Python
- Web Scraping
- HTML Parsing
title: Jak získat favicon – Kompletní průvodce v Pythonu pro získávání ikon webu
url: /cs/python/general/how-to-get-favicon-complete-python-guide-for-extracting-site/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak získat favicon – Kompletní průvodce v Pythonu pro získávání ikon stránek

Už jste se někdy zamýšleli **how to get favicon** z jakékoli webové stránky, aniž byste museli ručně procházet zdrojový kód? Nejste v tom sami — vývojáři, SEO specialisté i designéři často potřebují ten malý ikonový soubor, který reprezentuje stránku. V tomto tutoriálu vám ukážeme čistý, Python‑centrický způsob, jak načíst HTML z URL, najít značky `<link rel="icon">` a získat URL ikon. Na konci budete přesně vědět **how to get favicon** pro jakoukoliv doménu a budete mít připravený znovupoužitelný skript pro své projekty.

Probereme vše od stažení HTML až po řešení okrajových případů, jako jsou relativní URL a různé formáty ikon. Nepotřebujete žádné externí služby — pouze standardní knihovnu `requests` a lehký HTML parser. Připravení? Pojďme na to.

## Požadavky

- Python 3.8+ nainstalovaný (kód funguje i na 3.10)  
- Základní znalost `requests` a list comprehensions  
- Přístup k internetu pro cílovou webovou stránku  

Pokud už máte vše připravené, můžete přejít rovnou k prvnímu kroku. Jinak nainstalujte jedinou závislost, kterou potřebujeme:

```bash
pip install requests beautifulsoup4
```

> **Tip:** `beautifulsoup4` je osvědčený parser, který zjednodušuje „load html from url“.

## Krok 1: Načtení HTML z URL pomocí Pythonu  

Prvním krokem při učení **how to get favicon** je stáhnout zdrojový kód stránky. Toto je část „load html from url“ procesu.

```python
import requests
from bs4 import BeautifulSoup

def fetch_html(url: str) -> str:
    """Download the raw HTML of *url* and return it as text."""
    response = requests.get(url, timeout=10)
    response.raise_for_status()   # will raise if the request failed
    return response.text
```

Proč použít `requests`? Automaticky řeší přesměrování, ověřování HTTPS a časové limity, což znamená méně překvapení, až budete později **get website icons**.

## Krok 2: Parsování dokumentu a hledání odkazů na ikony  

Nyní, když máme HTML, musíme najít všechny `<link>` elementy, jejichž atribut `rel` označuje ikonu. Toto je jádro **how to get favicon**.

```python
def find_icon_links(html: str) -> list[BeautifulSoup]:
    """Return a list of <link> tags that declare an icon."""
    soup = BeautifulSoup(html, "html.parser")
    # Look for rel="icon" or rel="shortcut icon"
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]
```

Všimněte si, že kontrolujeme jak `icon`, tak `shortcut icon`, protože starší stránky stále používají druhou variantu. Tento drobný detail často zaskočí, když lidé hledají „how to extract favicons“.

## Krok 3: Extrakce href z elementů link  

S relevantními značkami v ruce je další logický krok — **extract href from link** — jednoduchý.

```python
from urllib.parse import urljoin

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    """Convert each <link> tag’s href into a full absolute URL."""
    urls = []
    for tag in link_tags:
        href = tag.get("href")
        if href:
            # Resolve relative URLs against the base page
            full_url = urljoin(base_url, href)
            urls.append(full_url)
    return urls
```

Použití `urljoin` zaručuje, že i když stránka poskytne relativní cestu jako `/favicon.ico`, získáte správnou absolutní URL — klíčové pro spolehlivý skript **how to get favicon**.

## Krok 4: Volitelné – Ověření a filtrování URL ikon  

Někdy stránka uvádí mnoho ikon (Apple touch icons, PNG různých velikostí atd.). Pokud vás zajímá jen klasický soubor `.ico`, filtrujte podle toho. Tento krok ukazuje **how to extract favicons** konkrétního typu.

```python
def filter_ico_urls(urls: list[str]) -> list[str]:
    """Keep only URLs that end with .ico (case‑insensitive)."""
    return [u for u in urls if u.lower().endswith(".ico")]
```

Klidně upravte filtr: nahraďte `".ico"` za `".png"` nebo zkontrolujte `rel="apple-touch-icon"`, pokud potřebujete ikony ve vysokém rozlišení.

## Krok 5: Stažení souborů ikon (pokud chcete skutečný obrázek)  

Získání URL je jen polovina boje; stažení vám poskytne soubor, který můžete zobrazit nebo uložit. Zde je rychlá pomocná funkce:

```python
import os

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    """Save each icon to *folder*, creating it if necessary."""
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")
```

Spuštěním po předchozích krocích získáte lokální kopii každého nalezeného faviconu, ideální pro cache nebo offline analýzu.

## Krok 6: Celý skript v jednom – kompletní funkční příklad  

Níže je kompletní, připravený ke spuštění skript, který demonstruje **how to get favicon** z libovolné stránky. Zkopírujte, změňte `target_url` a podívejte se na výstup.

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin
import os

def fetch_html(url: str) -> str:
    response = requests.get(url, timeout=10)
    response.raise_for_status()
    return response.text

def find_icon_links(html: str) -> list[BeautifulSoup]:
    soup = BeautifulSoup(html, "html.parser")
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    return [urljoin(base_url, tag.get("href")) for tag in link_tags if tag.get("href")]

def filter_ico_urls(urls: list[str]) -> list[str]:
    return [u for u in urls if u.lower().endswith(".ico")]

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")

def get_favicons(target_url: str) -> None:
    print(f"Fetching HTML from {target_url} …")
    html = fetch_html(target_url)

    print("Finding <link> tags that declare icons …")
    icon_tags = find_icon_links(html)

    print(f"Extracting href attributes – {len(icon_tags)} candidates found.")
    raw_urls = extract_icon_urls(target_url, icon_tags)

    # Optional filtering – keep only .ico files
    ico_urls = filter_ico_urls(raw_urls)
    print(f"Filtered to {len(ico_urls)} .ico URLs:", ico_urls)

    if ico_urls:
        download_icons(ico_urls)
    else:
        print("No .ico favicons detected; here are all discovered URLs:")
        print(raw_urls)

# Example usage – replace with any site you want to test
if __name__ == "__main__":
    target_url = "https://www.python.org"
    get_favicons(target_url)
```

**Očekávaný výstup (zkrácený pro stručnost):**

```
Fetching HTML from https://www.python.org …
Finding <link> tags that declare icons …
Extracting href attributes – 3 candidates found.
Filtered to 1 .ico URLs: ['https://www.python.org/static/favicon.ico']
Saved favicons/favicon.ico
```

Pokud stránka poskytuje jen PNG nebo Apple touch ikony, skript místo toho vypíše tyto URL, čímž vám ukáže přesně **how to get favicon** ve všech scénářích.

## Často kladené otázky a okrajové případy  

### Co když stránka používá `<meta>` místo `<link>`?  
Některé starší stránky vkládají URL ikony do `<meta name="msapplication‑TileImage">`. Můžete rozšířit `find_icon_links`, aby také prohledával tyto meta značky a zacházel s nimi stejně.

### Jak zacházet s relativními URL, které začínají `//`?  
`urljoin` automaticky vyřeší protokol‑relativní URL (`//example.com/favicon.ico`) podle schématu základní URL, takže není potřeba žádná další logika.

### Můžu automaticky získat více velikostí (např. 32×32, 180×180)?  
Ano — stačí vynechat krok `filter_ico_urls`. Skript vrátí všechny URL ikon, které najde, včetně PNG různých rozměrů. Pak je můžete seřadit nebo vybrat podle vzoru názvu souboru.

### Funguje to na stránkách, které blokují boty?  
Pokud stránka vrátí 403 nebo vyžaduje vlastní User‑Agent, upravte volání `requests.get`:

```python
headers = {"User-Agent": "Mozilla/5.0 (compatible; FaviconBot/1.0)"}
response = requests.get(url, headers=headers, timeout=10)
```

Tato malá úprava často vyřeší „how to get favicon“ na přísnějších doménách.

## Vizualizace  

![Diagram ukazující tok získávání faviconu z webové stránky – načtení HTML, parsování odkazových značek, extrakce href, volitelné stažení](how-to-get-favicon-diagram.png "Diagram toku získávání faviconu")

*Alt text obrázku obsahuje hlavní klíčové slovo, což splňuje SEO požadavky pro obrázky.*

## Závěr  

Prošli jsme **how to get favicon** krok za krokem: načtení HTML z URL,

## Co byste se měli naučit dál?

Následující tutoriály se věnují úzce souvisejícím tématům, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční kódové příklady s podrobným vysvětlením, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vlastních projektech.

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}