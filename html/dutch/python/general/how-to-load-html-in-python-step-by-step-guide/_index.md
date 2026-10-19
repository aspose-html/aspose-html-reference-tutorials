---
category: general
date: 2026-07-02
description: Leer hoe je HTML laadt in Python, een element op id krijgt en tekst uit
  een bestand extraheert. Deze praktische tutorial laat zien hoe je HTML‑bestanden
  leest met BeautifulSoup.
draft: false
keywords:
- how to load html
- how to get element
- how to extract text
- get element by id
- read html file python
language: nl
og_description: Hoe HTML te laden in Python en tekst te extraheren met BeautifulSoup.
  Volg de handleiding om een HTML‑bestand te lezen, een element op basis van id op
  te halen en de inhoud ervan af te drukken.
og_title: Hoe HTML te laden in Python – Complete tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Learn how to load HTML in Python, get element by id, and extract text
    from a file. This practical tutorial shows reading HTML files with BeautifulSoup.
  headline: How to Load HTML in Python – Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to load HTML in Python, get element by id, and extract text
    from a file. This practical tutorial shows reading HTML files with BeautifulSoup.
  name: How to Load HTML in Python – Step‑by‑Step Guide
  steps:
  - name: What if the HTML is malformed?
    text: BeautifulSoup’s `lxml` parser is forgiving, but for severely broken markup
      you might want to fallback to the built‑in `html.parser`. Swap `"lxml"` with
      `"html.parser"` in the `BeautifulSoup` constructor.
  - name: How to handle multiple elements with the same ID?
    text: HTML spec says IDs should be unique, but reality sometimes disagrees. Use
      `soup.find_all(id="duplicate-id")` to retrieve a list, then iterate over it.
  - name: Need to read from a URL instead of a file?
    text: Replace the file‑reading logic with `requests.get(url).text`. Remember to
      install the `requests` package (`pip install requests`) and handle network errors
      gracefully.
  - name: Want to extract other attributes (e.g., `class` or `href`)?
    text: 'Simply access them like a dictionary: `header[''class'']` or `header[''href'']`.
      If the attribute might be missing, use `.get(''class'')` to avoid `KeyError`.'
  type: HowTo
tags:
- Python
- HTML parsing
- BeautifulSoup
title: Hoe HTML in Python te laden – Stapsgewijze gids
url: /nl/python/general/how-to-load-html-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe HTML te Laden in Python – Complete Tutorial

Heb je je ooit afgevraagd **hoe je HTML kunt laden** in een Python‑script zonder je haar uit te trekken? Je bent niet de enige. Of je nu een nieuwssite scraped, een lokaal rapport verwerkt, of gewoon een kopregel uit een e‑mailtemplate wilt halen, het beheersen van het laden van HTML is een onmisbare vaardigheid voor elke ontwikkelaar.

In deze gids lopen we stap voor stap door **hoe je een element** op basis van zijn ID kunt krijgen, **hoe je tekst kunt extraheren**, en tenslotte het resultaat af te drukken – allemaal terwijl we de code schoon en Pythonic houden. We behandelen ook de nuances van **het lezen van een HTML‑bestand in Python**, zodat je nu meteen een werkende oplossing kunt kopiëren‑plakken.

> **Pro tip:** Het voorbeeld maakt gebruik van de populaire *BeautifulSoup*‑bibliotheek omdat deze lichtgewicht, goed gedocumenteerd en geschikt is voor zowel eenvoudige als complexe HTML‑structuren.

## Wat je nodig hebt

Voordat we beginnen, zorg dat je het volgende hebt:

- Python 3.9 of nieuwer (de code werkt ook op 3.10+)
- `beautifulsoup4` en `lxml` geïnstalleerd (`pip install beautifulsoup4 lxml`)
- Een voorbeeld‑HTML‑bestand – we noemen het `sample.html` en plaatsen het in een map genaamd `YOUR_DIRECTORY`

Dat is alles. Geen zware browsers, geen Selenium, alleen pure Python.

## Stap 1: Hoe HTML te Laden – Lees het Bestand in het Geheugen

Het allereerste wat je moet doen is **het HTML‑bestand lezen** vanaf de schijf. Dit is de basis voor elke volgende stap, dus laten we het goed doen.

```python
from pathlib import Path

# Define the path to the HTML file
html_path = Path("YOUR_DIRECTORY/sample.html")

# Read the file contents as a string
html_content = html_path.read_text(encoding="utf-8")
```

*Waarom dit belangrijk is:* Met `Path.read_text` worden OS‑specifieke regeleinden afgehandeld en UTF‑8 automatisch verwerkt, wat de facto‑codering is voor moderne webpagina’s. Als het bestand ontbreekt, zal `Path.read_text` een duidelijke `FileNotFoundError` werpen, waardoor debuggen moeiteloos verloopt.

## Stap 2: Parse het HTML‑Document

Nu we een ruwe string hebben, moeten we **HTML laden** in een parser‑object. BeautifulSoup biedt ons een handige API om door de DOM te navigeren.

```python
from bs4 import BeautifulSoup

# Create a BeautifulSoup object using the lxml parser (fast and reliable)
soup = BeautifulSoup(html_content, "lxml")
```

*Waarom lxml?* De `lxml`‑parser is aanzienlijk sneller dan de ingebouwde parser van Python en gaat beter om met slecht gevormde markup – perfect voor real‑world HTML die je mogelijk scraped.

## Stap 3: Element op ID Ophalen – Zoek de Header

Met het document geparsed, beantwoorden we de vraag **hoe je een element** met een specifieke ID kunt krijgen. In ons voorbeeld zoeken we een `<h1>`‑tag waarvan het `id`‑attribuut gelijk is aan `"main-header"`.

```python
# Retrieve the element with the specific ID
header = soup.find(id="main-header")
```

Als het element niet wordt gevonden, is `header` `None`. Het is goede gewoonte om hierop te controleren:

```python
if header is None:
    raise ValueError("Element with id='main-header' not found in the HTML file.")
```

## Stap 4: Hoe Tekst Extraheren – Haal de Inhoud Binnenin

Nu we het element hebben, is het extraheren van de tekstinhoud een fluitje van een cent. Dit beantwoordt **hoe je tekst kunt extraheren** uit een tag.

```python
# Extract the visible text inside the element
header_text = header.get_text(strip=True)  # strip removes surrounding whitespace
```

`get_text` concateneert automatisch alle geneste tekstknooppunten, zodat je niet handmatig over kinderen hoeft te itereren. De `strip=True`‑optie verwijdert regeleinden en spaties, waardoor je een schone string krijgt.

## Stap 5: Print het Resultaat – Controleer of Alles Werkt

Tot slot, laten we de waarde naar de console schrijven. Dit correspondeert met de `print(header.text_content)`‑regel in het oorspronkelijke fragment.

```python
print(header_text)  # prints: The text inside <h1 id="main-header">
```

Als je het script uitvoert en de verwachte kopregel ziet, gefeliciteerd – je hebt met succes **een HTML‑bestand gelezen in Python**, een element op ID gevonden en de tekst geëxtraheerd.

## Volledig Werkend Voorbeeld

Hieronder staat het complete, kant‑klaar script. Kopieer het naar een bestand genaamd `extract_header.py` en voer `python extract_header.py` uit.

```python
# extract_header.py
from pathlib import Path
from bs4 import BeautifulSoup

def load_html(file_path: str) -> str:
    """Read an HTML file and return its contents as a string."""
    path = Path(file_path)
    if not path.is_file():
        raise FileNotFoundError(f"Unable to locate the file: {file_path}")
    return path.read_text(encoding="utf-8")

def get_element_by_id(soup: BeautifulSoup, element_id: str):
    """Return the first tag with the given id, or raise an informative error."""
    element = soup.find(id=element_id)
    if element is None:
        raise ValueError(f"Element with id='{element_id}' not found.")
    return element

def main():
    # Step 1: Load the HTML document
    html = load_html("YOUR_DIRECTORY/sample.html")
    
    # Step 2: Parse the HTML with BeautifulSoup
    soup = BeautifulSoup(html, "lxml")
    
    # Step 3: Retrieve the element by its ID
    header = get_element_by_id(soup, "main-header")
    
    # Step 4: Extract and print the text content
    print(header.get_text(strip=True))

if __name__ == "__main__":
    main()
```

**Verwachte output** (ervan uitgaande dat `sample.html` `<h1 id="main-header">Welcome to My Site</h1>` bevat):

```
Welcome to My Site
```

Dat is alles – één script, geen extra afhankelijkheden buiten BeautifulSoup en lxml.

## Veelgestelde Vragen & Randgevallen

### Wat als de HTML slecht gevormd is?

De `lxml`‑parser van BeautifulSoup is vergevingsgezind, maar bij ernstig gebroken markup kun je beter terugvallen op de ingebouwde `html.parser`. Vervang `"lxml"` door `"html.parser"` in de `BeautifulSoup`‑constructor.

### Hoe ga je om met meerdere elementen met dezelfde ID?

De HTML‑specificatie stelt dat IDs uniek moeten zijn, maar de realiteit wijkt soms af. Gebruik `soup.find_all(id="duplicate-id")` om een lijst op te halen en itereren.

### Moet je van een URL lezen in plaats van een bestand?

Vervang de bestands‑leeslogica door `requests.get(url).text`. Vergeet niet het `requests`‑pakket te installeren (`pip install requests`) en netwerkfouten netjes af te handelen.

### Wil je andere attributen extraheren (bijv. `class` of `href`)?

Toegang is net als bij een dictionary: `header['class']` of `header['href']`. Als het attribuut mogelijk ontbreekt, gebruik dan `.get('class')` om een `KeyError` te vermijden.

## Visuele Samenvatting

![how to load html example](https://example.com/placeholder-image.png "how to load html example")

*Alt‑tekst:* how to load html example – een diagram dat de stroom van bestandslezen naar tekste­xtractie toont.

## Samenvatting

We hebben **hoe je HTML laadt** in Python behandeld, laten zien **hoe je een element** op zijn ID kunt krijgen, en demonstreren **hoe je tekst** uit dat element kunt extraheren. Door de bovenstaande stappen te volgen kun je betrouwbaar **een HTML‑bestand lezen in Python**, de DOM manipuleren en precies krijgen wat je nodig hebt.

## Wat is het Volgende?

- **Verken CSS‑selectoren:** Gebruik `soup.select_one('.my-class')` voor flexibelere queries.
- **Scrape meerdere pagina’s:** Combineer dit patroon met `requests` en een lus om sites in batch te verwerken.
- **Schrijf terug naar HTML:** BeautifulSoup laat je ook de boom wijzigen en opslaan – handig voor templating‑taken.
- **Prestatie‑optimalisatie:** Voor enorme bestanden kun je overwegen streaming‑parsers zoals `lxml.etree.iterparse` te gebruiken.

Voel je vrij om te experimenteren – wissel de ID, probeer andere tags, of schakel over naar `xml.etree.ElementTree` als je met XHTML werkt. De concepten blijven gelijk, en je hebt nu een stevige basis voor elk HTML‑parsing‑avontuur.

Happy coding! Als je tegen een probleem aanloopt of een cool use‑case wilt delen, laat dan een reactie achter.


## Wat moet je hierna leren?


De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementaties in je eigen projecten te verkennen.

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}