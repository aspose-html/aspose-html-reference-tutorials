---
category: general
date: 2026-06-10
description: Laad HTML van een URL om snel website‑iconen te krijgen. Leer hoe je
  favicons kunt extraheren, website‑favicon‑URL’s kunt ophalen en randgevallen in
  Python kunt afhandelen.
draft: false
keywords:
- load html from url
- get website icons
- how to extract favicons
- extract favicon urls
- fetch website favicon urls
language: nl
og_description: Laad HTML van URL om favicons te extraheren en website‑favicon‑URL’s
  op te halen. Een stapsgewijze Python‑tutorial voor ontwikkelaars.
og_title: HTML laden van URL en website‑iconen ophalen – Complete gids
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
title: HTML laden van URL en website‑iconen ophalen – Complete gids
url: /nl/python/general/load-html-from-url-and-get-website-icons-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML laden van URL en website‑pictogrammen ophalen – Complete gids

Heb je ooit **HTML van URL laden** nodig gehad alleen om het kleine logo van een site te halen? Je bent niet de enige. Of je nu een bladwijzer‑manager, een SEO‑dashboard bouwt, of gewoon een persoonlijk hobby‑project, het ophalen van website‑pictogrammen is een klein maar essentieel onderdeel van de puzzel.

In deze tutorial laten we je **hoe je favicons kunt extraheren** met gewone Python—geen zware Selenium, geen browser‑magie. Aan het einde kun je **website‑favicon‑URL's ophalen**, relatieve paden verwerken, en zelfs meerdere pictogrammen pakken als een site ze aanbiedt. Klaar? Laten we beginnen.

## Waarom HTML van URL laden in de eerste plaats?

Het laden van de ruwe HTML van een pagina geeft je directe toegang tot de `<link>`‑tags die browsers gebruiken om favicons te vinden. Die tags zien er meestal zo uit:

```html
<link rel="icon" href="/favicon.ico">
<link rel="apple-touch-icon" href="https://example.com/apple-touch-icon.png">
```

Als je die markup kunt ophalen, kun je programmatisch het `href`‑attribuut lezen en de afbeelding zelf downloaden. Het is sneller dan het scrapen van screenshots, en het werkt voor elke site die de standaardconventies volgt.

## Stap 1 – Laad het HTML‑document van een URL

Het eerste wat we nodig hebben is een manier om de paginabron op te halen. De populairste keuze in Python is de **requests**‑bibliotheek omdat deze eenvoudig, betrouwbaar is en redirects automatisch afhandelt.

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

> **Pro tip:** Als je achter een bedrijfsproxy werkt, geef `proxies=` mee aan `requests.get`. Ook voorkomt het instellen van een korte timeout dat je script blijft hangen bij dode sites.

Nu kunnen we `fetch_html("https://example.com")` aanroepen en een string krijgen die de markup van de pagina bevat. Dit is de kern van **HTML van URL laden**—de rest van de pijplijn werkt met die string.

## Stap 2 – Haal website‑pictogrammen op

Zodra we de HTML hebben, is de volgende stap om elk `<link>`‑element te vinden waarvan het `rel`‑attribuut “icon” vermeldt. De ingebouwde `html.parser`‑module kan de klus klaren, maar **BeautifulSoup** maakt de code veel leesbaarder.

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

Let op hoe we `urljoin` gebruiken om `"/favicon.ico"` om te zetten naar `"https://example.com/favicon.ico"`—dat is een veelvoorkomend randgeval bij **website‑pictogrammen ophalen**. Sommige sites leveren zelfs verschillende pictogrammen voor verschillende apparaten, dus je kunt eindigen met een handvol URL's. Geen probleem; we verzamelen ze gewoon allemaal.

## Stap 3 – Extraheer favicon‑URL's en toon ze

Het samenvoegen van de onderdelen is eenvoudig. We halen de HTML op, voeren de extractor uit, en printen de resulterende lijst. Het uiteindelijke script ziet er zo uit:

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

### Verwachte output

Het uitvoeren van het script tegen een site die een standaard favicon levert, kan je geven:

```
Found icon URLs: ['https://example.com/favicon.ico']
```

Als de site meerdere pictogrammen levert (Apple touch‑icon, shortcut‑icon, enz.), zie je een langere lijst:

```
Found icon URLs: [
    'https://example.com/favicon.ico',
    'https://example.com/apple-touch-icon.png',
    'https://example.com/favicon-32x32.png'
]
```

Dat is de volledige **extract favicon urls**‑workflow—compact, met weinig afhankelijkheden, en klaar om in elk project te gebruiken.

## Veelvoorkomende valkuilen behandelen

| Probleem | Waarom het gebeurt | Snelle oplossing |
|----------|--------------------|------------------|
| **Relative `href` without a `<base>` tag** | `urljoin` gaat ervan uit dat de pagin URL de basis is, wat in de meeste gevallen werkt. | Als er een `<base href="...">`‑tag bestaat, lees die dan eerst en geef die door als `base_url`. |
| **Missing `rel="icon"`** | Sommige sites gebruiken `rel="shortcut icon"` of aangepaste waarden. | Breid de lambda uit: `rel=lambda r: r and ("icon" in r.lower() or "shortcut" in r.lower())`. |
| **Redirects to a different domain** | De favicon kan op een CDN staan. | `urljoin` zal het nieuwe domein correct oplossen omdat het de uiteindelijke request‑URL gebruikt (`response.url`). |
| **Broken links (404)** | De HTML verwijst naar een bestand dat niet meer bestaat. | Na het extraheren van URL's kun je elk verifiëren met een HEAD‑request voordat je ze gebruikt. |
| **Multiple `<link>` tags with the same icon** | Duplicaatvermeldingen vergroten de lijst. | Gebruik `set(icon_urls)` om te dedupliceren voordat je teruggeeft. |

## Verder gaan – Website‑favicon‑URL's in bulk ophalen

Als je **website‑favicon‑URL's wilt ophalen** voor een lijst van domeinen, wikkel dan de `main`‑logica in een lus:

```python
domains = ["https://example.com", "https://python.org", "https://github.com"]
for site in domains:
    try:
        icons = extract_icon_links(fetch_html(site), site)
        print(site, "->", icons)
    except Exception as e:
        print(site, "error:", e)
```

Dit patroon schaalt goed, en je kunt caching toevoegen (bijv. met `functools.lru_cache`) om te voorkomen dat je dezelfde site herhaaldelijk belast.

## Visueel overzicht

![Diagram HTML laden van URL](load-html-url.png)

*Alt-tekst: Diagram HTML laden van URL dat fetch → parse → extract stappen toont.*

De afbeelding hierboven vat het drie‑stappen‑proces samen: **HTML van URL laden**, **website‑pictogrammen ophalen**, en **favicon‑URL's extraheren**. Het is handig wanneer je de stroom aan een teamgenoot moet uitleggen.

## Conclusie

We hebben een volledige, productie‑klare oplossing doorgenomen voor hoe je **HTML van URL kunt laden** en **website‑pictogrammen kunt ophalen** met alleen de requests‑ en BeautifulSoup‑bibliotheken van Python. Door de `href`‑attributen van `<link rel="icon">`‑tags te extraheren, kun je **favicon‑URL's extraheren**, relatieve paden verwerken, en zelfs meerdere pictogramformaten ophalen—alles in een paar tientallen regels code.

Wat nu? Probeer de pictogrammen naar een lokale map te downloaden, genereer een CSV met domein‑naar‑favicon‑toewijzingen, of koppel deze logica aan een Flask‑API die favicons op aanvraag levert. De mogelijkheden voor **website‑favicon‑URL's ophalen** zijn eindeloos, en de kerntechniek blijft hetzelfde.

Heb je vragen over randgevallen, of wil je een slimme aanpassing delen? Laat een reactie achter hieronder—veel plezier met het zoeken naar pictogrammen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [HTML‑documenten laden vanuit bestand in Aspose.HTML voor Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [HTML‑documenten laden vanuit stream met Aspose.HTML voor Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-stream/)
- [Document‑laad‑gebeurtenissen afhandelen in Aspose.HTML voor Java](/html/english/java/creating-managing-html-documents/handle-document-load-events/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}