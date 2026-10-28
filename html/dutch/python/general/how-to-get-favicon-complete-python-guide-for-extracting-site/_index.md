---
category: general
date: 2026-06-26
description: Leer hoe je een favicon kunt ophalen door HTML van een URL te laden en
  de href uit link‑tags te extraheren. Stapsgewijze Python‑code om snel website‑iconen
  te krijgen.
draft: false
keywords:
- how to get favicon
- load html from url
- get website icons
- extract href from link
- how to extract favicons
language: nl
og_description: 'Hoe je snel een favicon krijgt: laad HTML van een URL, zoek naar
  link rel=''icon'' en haal de href uit link‑tags met Python.'
og_title: Hoe een favicon te krijgen – Python‑tutorial
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
title: Hoe je een favicon krijgt – Complete Python-gids voor het extraheren van site‑iconen
url: /nl/python/general/how-to-get-favicon-complete-python-guide-for-extracting-site/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een Favicon te krijgen – Complete Python-gids voor het extraheren van site‑iconen

Heb je je ooit afgevraagd **how to get favicon** van een willekeurige website zonder handmatig door de paginabron te graven? Je bent niet de enige—ontwikkelaars, SEO‑professionals en zelfs ontwerpers hebben vaak het kleine pictogram nodig dat een site vertegenwoordigt. In deze tutorial laten we je een schone, Python‑gerichte manier zien om HTML van een URL te laden, de `<link rel="icon">`‑tags te vinden en de icoon‑URL's te halen. Aan het einde weet je precies **how to get favicon** voor elk domein, en heb je een herbruikbaar script klaar voor je projecten.

We behandelen alles, van het ophalen van de HTML tot het afhandelen van randgevallen zoals relatieve URL's en meerdere icoonformaten. Geen externe services nodig—alleen de standaard `requests`‑bibliotheek en een lichtgewicht HTML‑parser. Klaar om te beginnen? Laten we erin duiken.

## Vereisten

- Python 3.8+ geïnstalleerd (de code werkt ook op 3.10)  
- Basiskennis van `requests` en list comprehensions  
- Internettoegang voor de doelwebsite  

Als je deze al hebt, prima—ga door naar de eerste stap. Anders, installeer de enige afhankelijkheid die we nodig hebben:

```bash
pip install requests beautifulsoup4
```

> **Pro tip:** `beautifulsoup4` is een beproefde parser die “load html from url” een fluitje van een cent maakt.

## Stap 1: HTML laden van URL met Python  

Het eerste wat je moet doen bij het leren van **how to get favicon** is de bron van de pagina ophalen. Dit is het “load html from url”‑deel van het proces.

```python
import requests
from bs4 import BeautifulSoup

def fetch_html(url: str) -> str:
    """Download the raw HTML of *url* and return it as text."""
    response = requests.get(url, timeout=10)
    response.raise_for_status()   # will raise if the request failed
    return response.text
```

Waarom `requests` gebruiken? Het behandelt redirects, HTTPS‑verificatie en time‑outs automatisch, wat betekent dat er minder verrassingen zijn wanneer je later probeert **get website icons**.

## Stap 2: Document parseren en icoon‑links vinden  

Nu we de HTML hebben, moeten we alle `<link>`‑elementen vinden waarvan het `rel`‑attribuut een icoon aangeeft. Dit is de kern van **how to get favicon**.

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

Let op dat we zowel `icon` als `shortcut icon` controleren omdat oudere sites nog het laatste gebruiken. Deze kleine nuance brengt mensen vaak in de problemen wanneer ze zoeken naar “how to extract favicons.”

## Stap 3: href uit link‑elementen extraheren  

Met de relevante tags in de hand, is de volgende logische stap—**extract href from link**—eenvoudig.

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

Het gebruik van `urljoin` garandeert dat zelfs als een site een relatief pad zoals `/favicon.ico` opgeeft, je eindigt met een juiste absolute URL—cruciaal voor een betrouwbaar **how to get favicon**‑script.

## Stap 4: Optioneel – Icon‑URL's valideren en filteren  

Soms geeft een pagina veel iconen weer (Apple touch‑iconen, PNG’s van verschillende groottes, enz.). Als je alleen de klassieke `.ico`‑file nodig hebt, filter dan dienovereenkomstig. Deze stap toont **how to extract favicons** van een specifiek type.

```python
def filter_ico_urls(urls: list[str]) -> list[str]:
    """Keep only URLs that end with .ico (case‑insensitive)."""
    return [u for u in urls if u.lower().endswith(".ico")]
```

Voel je vrij om het filter aan te passen: vervang `".ico"` door `".png"` of controleer op `rel="apple-touch-icon"` als je hoge‑resolutie‑iconen nodig hebt.

## Stap 5: De icoonbestanden downloaden (als je de daadwerkelijke afbeelding wilt)

Het extraheren van de URL's is de helft van de strijd; downloaden geeft je een bestand dat je kunt weergeven of opslaan. Hier is een snelle helper:

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

Dit uitvoeren na de vorige stappen geeft je een lokale kopie van elke gevonden favicon, perfect voor caching of offline analyse.

## Stap 6: Alles samenvoegen – Volledig werkend voorbeeld  

Hieronder staat het volledige, kant‑klaar script dat **how to get favicon** van elke site demonstreert. Kopieer‑plak, wijzig de `target_url`, en bekijk de output.

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

**Verwachte output (afgekapt voor beknoptheid):**

```
Fetching HTML from https://www.python.org …
Finding <link> tags that declare icons …
Extracting href attributes – 3 candidates found.
Filtered to 1 .ico URLs: ['https://www.python.org/static/favicon.ico']
Saved favicons/favicon.ico
```

Als de site alleen PNG‑ of Apple touch‑iconen levert, zal het script die URL's in plaats daarvan weergeven, en je precies laten zien **how to get favicon** in elk scenario.

## Veelgestelde vragen & randgevallen  

### Wat als de site een `<meta>`‑tag gebruikt in plaats van `<link>`?  
Sommige oudere pagina's embedden de icoon‑URL in een `<meta name="msapplication‑TileImage">`. Je kunt `find_icon_links` uitbreiden om ook naar die meta‑tags te zoeken en ze op dezelfde manier te behandelen.

### Hoe ga ik om met relatieve URL's die beginnen met `//`?  
`urljoin` lost protocol‑relatieve URL's (`//example.com/favicon.ico`) automatisch op basis van het schema van de basis‑URL, dus je hebt geen extra logica nodig.

### Kan ik automatisch meerdere groottes (bijv. 32×32, 180×180) ophalen?  
Ja—verwijder gewoon de `filter_ico_urls`‑stap. Het script zal elke gevonden icoon‑URL teruggeven, inclusief PNG’s van verschillende afmetingen. Je kunt vervolgens sorteren of selecteren op basis van het bestandsnaampatroon.

### Werkt dit op sites die bots blokkeren?  
Als een site een 403 teruggeeft of een aangepaste User‑Agent vereist, pas dan de `requests.get`‑aanroep aan:

```python
headers = {"User-Agent": "Mozilla/5.0 (compatible; FaviconBot/1.0)"}
response = requests.get(url, headers=headers, timeout=10)
```

Die kleine wijziging lost vaak “how to get favicon” op bij strengere domeinen.

## Visueel overzicht  

![Diagram dat de stroom van how to get favicon van een website toont – HTML laden, link‑tags parseren, href extraheren, optioneel downloaden](how-to-get-favicon-diagram.png "how to get favicon flow diagram")

*De alt‑tekst van de afbeelding bevat het primaire zoekwoord, wat voldoet aan SEO voor afbeeldingen.*

## Conclusie  

We hebben stap voor stap **how to get favicon** doorlopen: HTML laden van een URL,

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}