---
category: general
date: 2026-05-28
description: Hoe HTML snel te parseren in Python—HTML‑bestand laden, CSS‑selector
  gebruiken en href‑attributen extraheren met een XPath‑contains‑voorbeeld.
draft: false
keywords:
- how to parse html
- get href attribute
- load html file
- use css selector
- xpath contains example
language: nl
og_description: 'Hoe HTML te parseren in Python: leer een HTML‑bestand te laden, CSS‑selectoren
  te gebruiken en href‑attributen op te halen met een XPath‑contains‑voorbeeld.'
og_title: Hoe HTML te parseren in Python – Stap voor stap
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  headline: How to Parse HTML in Python – Complete Guide
  type: TechArticle
- description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  name: How to Parse HTML in Python – Complete Guide
  steps:
  - name: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
    text: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
  - name: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
    text: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
  - name: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
    text: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
  - name: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
    text: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
  type: HowTo
tags:
- html parsing
- python
- web scraping
title: Hoe HTML in Python te parseren – Complete gids
url: /nl/python/general/how-to-parse-html-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe HTML te parseren in Python – Complete gids

Heb je je ooit afgevraagd **hoe HTML te parseren** in een Python‑script zonder een zware browser te gebruiken? Je bent niet de enige. De meesten van ons hoeven alleen maar een **HTML‑bestand te laden**, een paar koppen te scrapen, en misschien een of twee download‑links te halen. In deze tutorial laat ik je precies dat zien—met een kleine bibliotheek, een CSS‑selector en een XPath contains‑voorbeeld om **href‑attribuut**‑waarden **te verkrijgen**.

We lopen het hele proces stap voor stap door, van het lezen van een lokaal HTML‑document tot het afdrukken van de gegevens die je nodig hebt. Geen poespas, alleen een praktisch, uitvoerbaar voorbeeld dat je vandaag nog in je eigen project kunt gebruiken.

## Wat je zult leren

- Hoe je een **HTML‑bestand kunt laden** met een lichtgewicht parser.
- Hoe je **CSS‑selector**‑syntaxis kunt gebruiken om elementen zoals artikel‑koppen op te halen.
- Hoe je een **XPath contains‑voorbeeld** maakt dat links filtert.
- Hoe je veilig **href‑attribuut**‑waarden kunt **verkrijgen** van de gevonden knooppunten.
- Tips voor het omgaan met slecht gevormde markup en het uitbreiden van het script.

Je hebt alleen Python 3.8+ en de `lxml`‑ en `cssselect`‑pakketten nodig—beide installeerbaar met één `pip`‑commando.

---

## Stap 1: Laad het HTML‑bestand

Voordat je iets anders doet, moet je de HTML‑inhoud in het geheugen hebben. De `lxml.html`‑module biedt een handige `fromstring`‑helper, maar wanneer je een bestand op schijf hebt is de `parse`‑functie nog netter.

```python
# Step 1: Load the HTML file
from lxml import html

# Replace the path with the location of your HTML document
html_path = "YOUR_DIRECTORY/news.html"
doc = html.parse(html_path)

# The root element gives us access to CSS and XPath methods
root = doc.getroot()
```

> **Waarom dit belangrijk is:** Het één keer laden van het bestand houdt het geheugenverbruik laag en geeft je een enkel `root`‑object dat zowel CSS‑selectors als XPath‑queries ondersteunt. Als het bestand ontbreekt of onleesbaar is, zal `html.parse` een duidelijke `OSError` werpen, die je later kunt opvangen.

### Pro‑tip
Als je met een string werkt in plaats van een bestand, vervang je `html.parse` door `html.fromstring(your_html_string)`.

---

## Stap 2: Gebruik CSS‑selector om koppen te krijgen

CSS‑selectors zijn beknopt en bekend bij iedereen die een stylesheet heeft geschreven. Laten we elke `<h2>` binnen een `<article>` pakken—perfect voor nieuws‑koppen.

```python
# Step 2: Find all article headlines using a CSS selector
headline_nodes = root.cssselect("article h2")

# Print each headline's text content
for node in headline_nodes:
    print(node.text_content().strip())
```

**Verwachte output** (ervan uitgaande dat de voorbeeld‑HTML twee artikelen bevat):

```
Breaking News: Python Takes Over the World
Local Developer Solves HTML Parsing Puzzle
```

> **Waarom CSS?** Het is leesbaar, snel, en werkt direct uit de doos met `lxml`. De `cssselect`‑methode zet de selector onder de motorkap om in een XPath‑expressie, waardoor je het beste van beide werelden krijgt.

---

## Stap 3: XPath contains‑voorbeeld – Vind “download”‑links

Soms heb je meer granulaire controle nodig dan CSS biedt. De `contains()`‑functie van XPath blinkt uit wanneer je een substring binnen een attribuut wilt matchen, zoals alle links die naar een download wijzen.

```python
# Step 3: Find all links that contain the word "download" using XPath
download_link_nodes = root.xpath("//a[contains(@href, 'download')]")

# Extract and print the href attribute from each matching node
for node in download_link_nodes:
    href = node.get("href")
    print(href)
```

**Voorbeeldoutput**:

```
/files/report_download.pdf
https://example.com/downloads/setup.exe
```

> **Waarom XPath contains?** Het stelt je in staat direct op attribuutwaarden te filteren zonder extra Python‑lussen. Dit is het klassieke **xpath contains example** dat je vaak in tutorials ziet, maar hier gekoppeld aan een praktijkvoorbeeld.

---

## Stap 4: Alles verpakken in een herbruikbare functie

Hard‑coderen van paden en prints is prima voor een snelle test, maar productcode houdt van functies. Hieronder staat een compacte helper die zowel koppen als download‑links retourneert.

```python
def parse_news_html(file_path):
    """
    Parse a news HTML file and return headlines plus download URLs.

    Parameters
    ----------
    file_path : str
        Path to the local HTML document.

    Returns
    -------
    dict
        {
            "headlines": list of strings,
            "download_links": list of href strings
        }
    """
    doc = html.parse(file_path)
    root = doc.getroot()

    # Headlines via CSS selector
    headlines = [
        node.text_content().strip()
        for node in root.cssselect("article h2")
    ]

    # Download links via XPath contains
    download_links = [
        node.get("href")
        for node in root.xpath("//a[contains(@href, 'download')]")
    ]

    return {"headlines": headlines, "download_links": download_links}
```

Je kunt nu de functie aanroepen en de resultaten mooi afdrukken:

```python
if __name__ == "__main__":
    results = parse_news_html("YOUR_DIRECTORY/news.html")
    print("Headlines:")
    for h in results["headlines"]:
        print(f"- {h}")

    print("\nDownload Links:")
    for link in results["download_links"]:
        print(f"- {link}")
```

Het uitvoeren van het script levert dezelfde output op als eerder, maar nu netjes verpakt voor hergebruik.

---

## Stap 5: Omgaan met randgevallen en veelvoorkomende valkuilen

1. **Missing `href` attribute** – XPath zal nog steeds het `<a>`‑knooppunt retourneren zelfs als `href` ontbreekt. Bescherm tegen `None`:

   ```python
   href = node.get("href")
   if href:
       download_links.append(href)
   ```

2. **Relative vs. absolute URLs** – Als je links relatief zijn, wil je ze misschien resolven ten opzichte van de basis‑URL:

   ```python
   from urllib.parse import urljoin
   base_url = "https://example.com"
   absolute = urljoin(base_url, href)
   ```

3. **Malformed HTML** – `lxml` is vergevingsgezind, maar extreem gebroken markup kan `html.parse` een `XMLSyntaxError` laten werpen. Plaats de parse‑aanroep in een `try/except`‑blok om te loggen en problematische bestanden over te slaan.

4. **Performance with large files** – Voor pagina’s van meerdere megabytes kun je overwegen te streamen met `iterparse` in plaats van het hele DOM in het geheugen te laden.

---

## Visueel overzicht (optioneel)

![Hoe HTML te parseren stroomdiagram dat bestand laden → CSS selector → XPath contains → href‑attribuut ophalen](how-to-parse-html-flow.png "Hoe HTML te parseren stroomdiagram")

*Alt‑tekst bevat het primaire zoekwoord om aan SEO‑vereisten te voldoen.*

---

## Conclusie

We hebben behandeld **hoe HTML te parseren** in Python van begin tot eind: een HTML‑bestand laden, een CSS‑selector gebruiken om artikel‑koppen te halen, een XPath contains‑voorbeeld maken om download‑links te vinden, en uiteindelijk **href‑attribuut**‑waarden veilig **verkrijgen**. De herbruikbare `parse_news_html`‑functie toont een schone, onderhoudbare aanpak die je kunt aanpassen aan elke scrape‑taak.

Klaar voor de volgende uitdaging? Probeer het script uit te breiden om:

- Tabellen te parseren met `//table//tr` XPath‑queries.
- Afbeeldings‑`src`‑attributen te extraheren met een ander **xpath contains example**.
- Over te schakelen naar asynchrone fetching met `aiohttp` voor live webpagina’s.

Veel plezier met parseren, en onthoud—als je deze basis onder de knie hebt, wordt de rest van HTML‑scraping een eitje. Als je ergens vastloopt, laat dan een reactie achter—laten we samen het probleem oplossen!

## Gerelateerde tutorials

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}