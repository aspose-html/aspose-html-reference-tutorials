---
category: general
date: 2026-07-02
description: Hoe iconen uit een HTML‑bestand te extraheren met Python. Leer een HTML‑bestand
  te lezen met Python, een HTML‑document te parseren en het href‑attribuut te extraheren
  om favicon‑URL’s te verkrijgen.
draft: false
keywords:
- how to extract icons
- read html file python
- parse html document
- extract href attribute
- extract favicon urls
language: nl
og_description: Hoe je iconen uit een HTML-pagina haalt met Python. Deze tutorial
  laat zien hoe je een HTML‑bestand leest met Python, het document parseert en favicon‑URL’s
  ophaalt.
og_title: Hoe iconen uit HTML te extraheren – Python‑gids
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
title: Hoe iconen uit HTML te extraheren met Python – Complete gids
url: /nl/python/general/how-to-extract-icons-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe icoontjes uit HTML te extraheren met Python – Complete gids

Heb je je ooit afgevraagd **hoe je iconen** uit een webpagina kunt extraheren zonder een browser te openen? Misschien bouw je een site‑catalogus, een SEO‑audittool, of ben je gewoon nieuwsgierig naar die kleine favicons die in tabbladen verschijnen. Het goede nieuws is dat je het in een paar regels Python kunt doen—geen Selenium, geen headless Chrome, alleen een platte‑tekst HTML‑bestand.

In deze tutorial lopen we stap voor stap door het lezen van een HTML‑bestand met Python, het parseren van het HTML‑document, en uiteindelijk **het extraheren van het href‑attribuut** uit `<link rel="icon">`‑tags om die favicon‑URL's te krijgen. Aan het einde heb je een herbruikbare snippet die werkt op elke statische HTML die je erin gooit, en zie je ook hoe je omgaat met randgevallen zoals relatieve paden of meerdere icoon‑declaraties.

## Wat je zult leren

- Laad een lokaal HTML‑bestand met Python (read html file python)  
- Gebruik een lichtgewicht parser om **parse html document** veilig  
- Zoek `<link>`‑elementen die een icoon declareren  
- **Extract href attribute** waarden en zet ze om naar absolute URL's  
- Verzamel en print alle gevonden **favicon URLs**  

Geen externe services vereist—alleen de standaardbibliotheek en het populaire **BeautifulSoup**‑pakket.

---

![Schermafbeelding van Python‑script dat iconen extraheert – hoe iconen te extraheren](https://example.com/images/extract-icons-python.png "hoe iconen te extraheren")

*Afbeeldingsalt‑tekst: "hoe iconen te extraheren met een Python‑script"*

## Vereisten

- Python 3.8+ geïnstalleerd  
- `beautifulsoup4`‑bibliotheek (`pip install beautifulsoup4`)  
- Een lokaal HTML‑bestand dat je wilt scannen (bijv. `sample.html`)  

Als je die al hebt, laten we beginnen.

## Stap 1: HTML‑bestand lezen met Python – Laad het document

Allereerst moeten we het bestand openen en de inhoud aan een parser geven. Het gebruik van `with open(..., "r", encoding="utf‑8")` garandeert dat het bestand automatisch wordt gesloten, en de UTF‑8‑codering behandelt de meeste moderne pagina's.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Step 1: Load the HTML document from disk
html_path = Path("sample.html")          # adjust the path as needed
html_content = html_path.read_text(encoding="utf-8")
```

**Waarom dit belangrijk is:** Het openen van het bestand met de juiste codering voorkomt mysterieuze `�`‑tekens die later de parser kunnen breken. Het gebruik van `Path` uit de standaardbibliotheek maakt de code bovendien platform‑onafhankelijk.

## Stap 2: HTML‑document parseren – Alle icoon‑links vinden

Nu geven we de ruwe HTML aan **BeautifulSoup**, die een doorzoekbare boom opbouwt. We zoeken naar elke `<link>`‑tag waarvan het `rel`‑attribuut het woord `icon` bevat. Let op dat `rel` een door spaties gescheiden lijst kan zijn (`rel="shortcut icon"`), dus we hebben een flexibele controle nodig.

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

**Waarom deze stap cruciaal is:** Een naïeve `soup.find_all("link", rel="icon")` zou variaties missen zoals `rel="shortcut icon"` of `rel="apple-touch-icon"`. Onze helper `is_icon_link` dekt die gevallen, waardoor de extractie robuust is.

## Stap 3: href‑attribuut extraheren – De URL's ophalen

Met de relevante tags verzameld, halen we nu het `href`‑attribuut van elk op. Sommige pagina's kunnen `href` weglaten (zeldzaam, maar mogelijk), dus we beschermen tegen `None`. Bovendien worden favicons vaak opgegeven met relatieve URL's, dus we zullen ze resolven ten opzichte van de basis‑URL van de pagina als je die kent. Voor een lokaal bestand houden we het pad gewoon onveranderd.

```python
# Step 3: Grab the href attribute from each icon link
icon_urls = []
for tag in icon_links:
    href = tag.get("href")
    if href:
        icon_urls.append(href.strip())
```

**Waarom we witruimte verwijderen:** HTML‑auteurs voegen soms per ongeluk spaties rond URL's toe, wat een latere aanvraag zou breken. Trimmen zorgt ervoor dat we schone strings krijgen.

## Stap 4: Favicon‑URL's extraheren – Resultaten weergeven

Tot slot printen (of retourneren) we de lijst met gevonden URL's. In een script voor de echte wereld zou je ze naar een CSV kunnen schrijven, de iconen downloaden, of ze in een andere service gebruiken. Hier is een eenvoudige lus die het resultaat op de console toont.

```python
# Step 4: Display each discovered favicon URL
if not icon_urls:
    print("No icon links found in the document.")
else:
    for url in icon_urls:
        print("Favicon URL:", url)
```

### Randgevallen afhandelen

- **Meerdere rel‑waarden:** Onze `is_icon_link`‑controle vangt al `rel="shortcut icon"` en `rel="apple-touch-icon"`.  
- **Relatieve paden:** Als je later absolute URL's nodig hebt, gebruik dan `urllib.parse.urljoin(base_url, href)`.  
- **Ontbrekende href:** De guard `if href:` slaat misvormde tags over, waardoor `NoneType`‑fouten worden vermeden.  
- **Dubbele vermeldingen:** Je kunt `icon_urls = list(dict.fromkeys(icon_urls))` gebruiken om te dedupliceren.

---

## Volledig script – Alles‑in‑één oplossing

Alles bij elkaar genomen, hier is het volledige, kant‑klaar script. Sla het op als `extract_icons.py` en wijs `html_path` naar elk bestand dat je wilt.

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

**Verwachte output** (ervan uitgaande dat `sample.html` twee iconen bevat):

```
Favicon URL: /images/favicon.ico
Favicon URL: https://example.com/assets/apple-touch-icon.png
```

Voer het uit met `python extract_icons.py` en je zult de URL's op de console zien verschijnen.

---

## Veelgestelde vragen

**V: Wat als de HTML `<meta>`‑tags voor iconen gebruikt?**  
A: Sommige sites embedden iconen via `<meta itemprop="image">`. Breid `is_icon_link` uit om ook `meta` met `itemprop="image"` te controleren en haal het `content`‑attribuut op.

**V: Kan ik de iconen automatisch ophalen?**  
A: Ja—voer elke URL in `requests.get(url, stream=True)` in en schrijf de inhoud naar een bestand. Vergeet niet relatieve URL's te behandelen met `urljoin`.

**V: Werkt dit op externe pagina's?**  
A: Absoluut. Vervang de stap van het lezen van een bestand door `requests.get(page_url).text` en geef de HTML‑string door aan BeautifulSoup. Let wel op robots.txt en snelheidslimieten.

---

## Samenvatting

We hebben **hoe je iconen** uit elke statische HTML kunt extraheren met Python behandeld, van het lezen van het bestand tot het afdrukken van elke favicon‑URL. De kernideeën—het lezen van het bestand, het parseren van het document, het vinden van de juiste tags, en het ophalen van het `href`‑attribuut—zijn herbruikbare patronen die je in veel web‑scraping‑taken zult tegenkomen.

Volgende stappen? Probeer het script uit te breiden naar:

- Relatieve URL's resolven ten opzichte van de basis‑URL van de pagina  
- Elke icoon downloaden en lokaal opslaan  
- Extra icoonformaten ondersteunen (`rel="mask-icon"` voor Safari)  

Voel je vrij om te experimenteren, en als je tegen eigenaardigheden aanloopt, laat dan een reactie achter. Veel plezier met parseren!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe HTML te queryen in Java – Complete tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Hoe de HTML‑documentboom te bewerken in Aspose.HTML voor Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [HTML‑document opslaan naar bestand in Aspose.HTML voor Java](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}