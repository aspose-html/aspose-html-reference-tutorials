---
category: general
date: 2026-06-10
description: Načtěte HTML z URL a rychle získávejte ikony webových stránek. Naučte
  se, jak extrahovat favikony, získávat URL favikon webových stránek a řešit okrajové
  případy v Pythonu.
draft: false
keywords:
- load html from url
- get website icons
- how to extract favicons
- extract favicon urls
- fetch website favicon urls
language: cs
og_description: Načtěte HTML z URL pro extrakci faviconů a získání URL faviconů webových
  stránek. Krok po kroku Python tutoriál pro vývojáře.
og_title: Načíst HTML z URL a získat ikony webu – kompletní průvodce
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Load HTML from URL to get website icons quickly. Learn how to extract
    favicons, fetch website favicon URLs, and handle edge cases in Python.
  headline: Load HTML from URL and Get Website Icons – Complete Guide
  type: TechArticle
tags:
- web scraping
- favicon extraction
- python
- html parsing
title: Načtení HTML z URL a získání ikon webových stránek – kompletní průvodce
url: /cs/python/general/load-html-from-url-and-get-website-icons-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Načtení HTML z URL a získání ikon webových stránek – kompletní průvodce

Už jste někdy potřebovali **načíst HTML z URL**, jen abyste získali malý logo stránky? Nejste sami. Ať už vytváříte správce záložek, SEO dashboard, nebo jen osobní koníčkový projekt, získání ikon webových stránek je malý, ale nezbytný kousek skládačky.

V tomto tutoriálu vám ukážeme **jak extrahovat favikony** pomocí čistého Pythonu — žádný těžký Selenium, žádná kouzla prohlížeče. Na konci budete schopni **získat URL favikon webových stránek**, pracovat s relativními cestami a dokonce stáhnout více ikon, pokud je stránka poskytuje. Připravení? Ponořme se do toho.

## Proč načíst HTML z URL v první řadě?

Načtení surového HTML stránky vám dává přímý přístup k `<link>` tagům, které prohlížeče používají k nalezení favikon. Tyto tagy obvykle vypadají takto:

```html
<link rel="icon" href="/favicon.ico">
<link rel="apple-touch-icon" href="https://example.com/apple-touch-icon.png">
```

Pokud dokážete tento markup stáhnout, můžete programově přečíst atribut `href` a stáhnout obrázek sami. Je to rychlejší než scrapování screenshotů a funguje pro jakoukoli stránku, která dodržuje standardní konvence.

## Krok 1 – Načtení HTML dokumentu z URL

První, co potřebujeme, je způsob, jak získat zdrojovou stránku. Nejoblíbenější volbou v Pythonu je knihovna **requests**, protože je jednoduchá, spolehlivá a automaticky zvládá přesměrování.

```python
import requests

def fetch_html(url: str) -> str:
    """
    Retrieve the raw HTML from the given URL.
    Raises an exception if the request fails.
    """
    response = requests.get(url, timeout=10)
    response.raise_for_status()          # Fail fast on HTTP errors
    return response.text
```

> **Pro tip:** Pokud pracujete za firemním proxy, předávejte `proxies=` do `requests.get`. Také nastavení krátkého timeoutu zabrání tomu, aby váš skript visel na nefunkčních stránkách.

Nyní můžeme zavolat `fetch_html("https://example.com")` a získat řetězec obsahující markup stránky. To je jádro **načtení HTML z URL** — zbytek pipeline pracuje s tímto řetězcem.

## Krok 2 – Získání ikon webových stránek

Jakmile máme HTML, dalším krokem je najít každý `<link>` element, jehož atribut `rel` zmiňuje „icon“. Vestavěný modul `html.parser` to zvládne, ale **BeautifulSoup** dělá kód mnohem čitelnějším.

```python
from bs4 import BeautifulSoup
from urllib.parse import urljoin

def extract_icon_links(html: str, base_url: str) -> list[str]:
    """
    Parse the HTML and return a list of absolute URLs pointing to icons.
    Handles relative hrefs by joining them with the page’s base URL.
    """
    soup = BeautifulSoup(html, "html.parser")
    icons = []

    # Look for any <link> tag where rel contains "icon"
    for link in soup.find_all("link", rel=lambda r: r and "icon" in r.lower()):
        href = link.get("href")
        if href:
            # Convert relative URLs to absolute ones
            absolute_url = urljoin(base_url, href)
            icons.append(absolute_url)

    return icons
```

Všimněte si, že používáme `urljoin`, abychom proměnili `"/favicon.ico"` na `"https://example.com/favicon.ico"` — to je běžný okrajový případ při **získávání ikon webových stránek**. Některé stránky dokonce poskytují různé ikony pro různá zařízení, takže můžete skončit s několika URL. Žádný problém; prostě je všechny shromáždíme.

## Krok 3 – Extrahování URL favikon a jejich zobrazení

Skládání jednotlivých částí je přímočaré. Načteme HTML, spustíme extraktor a vytiskneme výsledný seznam. Výsledný skript vypadá takto:

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin

def fetch_html(url: str) -> str:
    response = requests.get(url, timeout=10)
    response.raise_for_status()
    return response.text

def extract_icon_links(html: str, base_url: str) -> list[str]:
    soup = BeautifulSoup(html, "html.parser")
    icons = []
    for link in soup.find_all("link", rel=lambda r: r and "icon" in r.lower()):
        href = link.get("href")
        if href:
            icons.append(urljoin(base_url, href))
    return icons

def main():
    target = "https://example.com"
    html = fetch_html(target)
    icon_urls = extract_icon_links(html, target)
    print("Found icon URLs:", icon_urls)

if __name__ == "__main__":
    main()
```

### Očekávaný výstup

Spuštění skriptu proti stránce, která poskytuje standardní favikon, může vypadat takto:

```
Found icon URLs: ['https://example.com/favicon.ico']
```

Pokud stránka poskytuje více ikon (Apple touch icon, shortcut icon atd.), uvidíte delší seznam:

```
Found icon URLs: [
    'https://example.com/favicon.ico',
    'https://example.com/apple-touch-icon.png',
    'https://example.com/favicon-32x32.png'
]
```

To je celý workflow **extrahování URL favikon** — kompaktní, s minimálními závislostmi a připravený k vložení do jakéhokoli projektu.

## Řešení běžných problémů

| Problém | Proč se to děje | Rychlé řešení |
|-------|----------------|-----------|
| **Relativní `href` bez `<base>` tagu** | `urljoin` předpokládá URL stránky jako základ, což funguje ve většině případů. | Pokud existuje tag `<base href="...">`, načtěte jej nejprve a použijte jako `base_url`. |
| **Chybějící `rel="icon"`** | Některé stránky používají `rel="shortcut icon"` nebo vlastní hodnoty. | Rozšiřte lambda výraz: `rel=lambda r: r and ("icon" in r.lower() or "shortcut" in r.lower())`. |
| **Přesměrování na jinou doménu** | Favikon může být umístěn na CDN. | `urljoin` správně vyřeší novou doménu, protože používá finální URL požadavku (`response.url`). |
| **Poškozené odkazy (404)** | HTML odkazuje na soubor, který již neexistuje. | Po extrahování URL můžete každou ověřit HEAD požadavkem před dalším použitím. |
| **Více `<link>` tagů se stejnou ikonou** | Duplicitní položky nafouknou seznam. | Použijte `set(icon_urls)` pro odstranění duplicit před návratem. |

## Další krok – Hromadné získávání URL favikon webových stránek

Pokud potřebujete **získat URL favikon webových stránek** pro seznam domén, zabalte logiku `main` do smyčky:

```python
domains = ["https://example.com", "https://python.org", "https://github.com"]
for site in domains:
    try:
        icons = extract_icon_links(fetch_html(site), site)
        print(site, "->", icons)
    except Exception as e:
        print(site, "error:", e)
```

Tento vzor se dobře škáluje a můžete přidat kešování (např. pomocí `functools.lru_cache`), abyste se vyhnuli opakovanému zatěžování stejné stránky.

## Vizualizace

![Diagram načtení HTML z URL](load-html-url.png)

*Alt text: Diagram načtení HTML z URL ukazující kroky načtení → parsování → extrakce.*

Obrázek výše shrnuje tříkrokový proces: **načíst HTML z URL**, **získat ikony webových stránek** a **extrahovat URL favikon**. Je užitečný, když potřebujete vysvětlit tok kolegovi.

## Závěr

Prošli jsme kompletním, produkčně připraveným řešením, jak **načíst HTML z URL** a **získat ikony webových stránek** pomocí pouze knihoven requests a BeautifulSoup v Pythonu. Extrahováním atributů `href` z `<link rel="icon">` tagů můžete **extrahovat URL favikon**, pracovat s relativními cestami a dokonce získat více formátů ikon — vše během několika desítek řádků kódu.

Co dál? Zkuste stáhnout ikony do lokální složky, vygenerovat CSV mapování doména → favikon, nebo zapojit tuto logiku do Flask API, které na požádání poskytuje favikony. Možnosti pro **získání URL favikon webových stránek** jsou nekonečné a základní technika zůstává stejná.

Máte otázky ohledně okrajových případů, nebo chcete sdílet chytrý tip? Zanechte komentář níže — šťastné lovení ikon!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, která vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich vlastních projektech.

- [Načtení HTML dokumentů ze souboru v Aspose.HTML pro Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Načtení HTML dokumentů ze streamu v Aspose.HTML pro Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-stream/)
- [Zpracování událostí načítání dokumentu v Aspose.HTML pro Java](/html/english/java/creating-managing-html-documents/handle-document-load-events/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}