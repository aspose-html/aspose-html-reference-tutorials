---
category: general
date: 2026-09-16
description: Parse HTML‑bestand in Python, laad een HTML‑document vanuit een bestand
  en maak een HTML‑document vanuit een string met eenvoudige, kant‑en‑klare code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- parse html file in python
- create html document from string
- load html document from file
- read local html file python
language: nl
lastmod: 2026-09-16
og_description: Parse HTML-bestand in Python om lokale HTML-bestanden te lezen en
  HTML-documenten snel en betrouwbaar uit strings te genereren.
og_image_alt: Screenshot of Python code parsing an HTML file and creating a document
  from a string
og_title: HTML-bestand parseren in Python – document maken vanuit een string
schemas:
- author: Aspose
  dateModified: '2026-09-16'
  description: Parse HTML file in Python, load HTML document from file, and create
    HTML document from string with simple, ready‑to‑run code.
  headline: Parse HTML file in Python and create document from string
  type: TechArticle
- description: Parse HTML file in Python, load HTML document from file, and create
    HTML document from string with simple, ready‑to‑run code.
  name: Parse HTML file in Python and create document from string
  steps:
  - name: '**Detect source type** – The constructor checks whether the supplied `source`
      exists on disk. If it does, we **load html document from file**; otherwise we
      treat it as a raw string, satisfying the **create html document from string**
      requirement.'
    text: '**Detect source type** – The constructor checks whether the supplied `source`
      exists on disk. If it does, we **load html document from file**; otherwise we
      treat it as a raw string, satisfying the **create html document from string**
      requirement.'
  - name: '**Read the file** – We use `Path.read_text(encoding="utf-8")` which is
      the recommended way to **read local html file python** safely.'
    text: '**Read the file** – We use `Path.read_text(encoding="utf-8")` which is
      the recommended way to **read local html file python** safely.'
  - name: '**Parse with BeautifulSoup** – The `lxml` parser is fast and tolerant of
      malformed markup.'
    text: '**Parse with BeautifulSoup** – The `lxml` parser is fast and tolerant of
      malformed markup.'
  type: HowTo
tags:
- python html parsing
- html document creation
- file handling python
title: HTML-bestand parseren in Python en document maken vanuit een string
url: /nl/python/general/parse-html-file-in-python-and-create-document-from-string/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Parse HTML file in Python and create document from string

Als je **HTML‑bestand in Python moet parseren**, laat deze gids je precies zien hoe je een lokaal HTML‑bestand leest, een HTML‑document uit een bestand laadt, en ook **een HTML‑document vanuit een string maakt**. Of je nu data scraped, templates test of dynamische content genereert, de onderstaande stappen geven je een volledige, uitvoerbare oplossing.

In deze tutorial leer je hoe je:

* Een lokaal HTML‑bestand leest met de standaardbibliotheken van Python.
* Een HTML‑document laadt vanaf een bestands­pad.
* Direct een HTML‑document maakt vanuit een HTML‑string.
* Veelvoorkomende randgevallen afhandelt, zoals ontbrekende bestanden en codering‑problemen.

De enige vereisten zijn Python 3.8+ en de `beautifulsoup4`‑bibliotheek, die we in de eerste stap installeren.

## Prerequisites

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| Python 3.8 of nieuwer | Garandeert compatibiliteit met type‑hints en moderne syntaxis. |
| `beautifulsoup4` en `lxml` pakketten | Bieden een robuuste parser die slecht gevormde HTML aankan en je een handig `HTMLDocument`‑achtig object geeft. |
| Een voorbeeld‑HTML‑bestand (`index.html`) in je projectmap | Dient als invoer voor het **load html document from file**‑voorbeeld. |

Installeer de afhankelijkheden met pip:

```bash
pip install beautifulsoup4 lxml
```

## Parse HTML file in Python

De kern van de tutorial is de **parse html file in python**‑operatie. We wikkelen BeautifulSoup in een kleine hulpprogrammaclasse genaamd `HTMLDocument` zodat de API overeenkomt met het voorbeeld dat je eerder zag.

```python
from pathlib import Path
from bs4 import BeautifulSoup
from typing import Union

class HTMLDocument:
    """
    Simple wrapper that mimics a “document” object.
    Accepts either a file path or a raw HTML string.
    """
    def __init__(self, source: Union[str, Path]):
        if Path(source).exists():
            # Load html document from file
            self._load_from_file(Path(source))
        else:
            # Assume source is a raw HTML string
            self._load_from_string(source)

    def _load_from_file(self, file_path: Path):
        try:
            # read local html file python – explicit UTF‑8 handling
            html = file_path.read_text(encoding="utf-8")
        except FileNotFoundError:
            raise FileNotFoundError(f"File not found: {file_path}")
        self.soup = BeautifulSoup(html, "lxml")

    def _load_from_string(self, html_string: str):
        self.soup = BeautifulSoup(html_string, "lxml")

    def title(self) -> str:
        """Return the content of the <title> tag, or an empty string."""
        if self.soup.title:
            return self.soup.title.string.strip()
        return ""

    def pretty(self) -> str:
        """Return a nicely formatted HTML representation."""
        return self.soup.prettify()
```

### How it works

1. **Detect source type** – De constructor controleert of de opgegeven `source` op schijf bestaat. Als dat zo is, **load html document from file**; anders behandelen we het als een ruwe string, waarmee we voldoen aan de **create html document from string**‑vereiste.
2. **Read the file** – We gebruiken `Path.read_text(encoding="utf-8")`, de aanbevolen manier om **read local html file python** veilig uit te voeren.
3. **Parse with BeautifulSoup** – De `lxml`‑parser is snel en tolerant voor slecht gevormde markup.

## Load HTML document from file

Nu we de `HTMLDocument`‑klasse hebben, is het laden van een bestand eenvoudig:

```python
# Step 1: Load an HTML document from a local file
doc = HTMLDocument("YOUR_DIRECTORY/index.html")

# Verify that the file was parsed correctly
print("Document title:", doc.title())
```

**Verwachte output** (ervan uitgaande dat `index.html` `<title>My Page</title>` bevat):

```
Document title: My Page
```

Als het bestand niet bestaat, werpt de klasse een duidelijke `FileNotFoundError`, die je in productiecodel kunt opvangen.

## Create HTML document from string

Een document direct uit een string maken is handig voor testen of het dynamisch genereren van HTML:

```python
# Step 2: Create an HTML document directly from an HTML string
html_content = "<html><head><title>Hello</title></head><body><h1>Hello</h1></body></html>"
doc_from_string = HTMLDocument(html_content)

print("String‑based title:", doc_from_string.title())
```

**Verwachte output**:

```
String-based title: Hello
```

Omdat dezelfde `HTMLDocument`‑klasse beide scenario’s afhandelt, krijg je een consistente API voor **parse html file in python**, ongeacht of de bron een bestand of een string is.

## Read local HTML file Python – handling edge cases

Bij het werken met real‑world bestanden kom je vaak het volgende tegen:

* **Ontbrekende bestanden** – al afgehandeld door de `FileNotFoundError`.
* **Verschillende coderingen** – je kunt BeautifulSoup de codering laten raden, maar expliciete UTF‑8 is het veiligst.
* **Grote bestanden** – het volledig in het geheugen lezen kan duur zijn; je kunt streamen met `BeautifulSoup(open(...), "lxml")` indien nodig.

Hier is een defensieve wrapper die deze beveiligingen toevoegt:

```python
def safe_load_html(path: Union[str, Path]) -> HTMLDocument:
    """
    Load an HTML file safely, handling missing files and encoding issues.
    Returns an HTMLDocument instance or raises a descriptive exception.
    """
    try:
        return HTMLDocument(path)
    except FileNotFoundError as e:
        raise RuntimeError(f"Unable to read local HTML file Python: {e}")
    except UnicodeDecodeError:
        raise RuntimeError("File encoding is not UTF-8; consider specifying the correct encoding.")
```

Je kunt nu `safe_load_html("index.html")` aanroepen en krijg je hetzelfde `HTMLDocument`‑object met de zekerheid dat fouten duidelijk worden gerapporteerd.

## Pro tips and common pitfalls

* **Vermijd “gewoon” `open(...).read()`** – `Path.read_text` behandelt pad‑expansie en codering in één regel.
* **Vergeet niet bestands‑handles te sluiten** – `Path.read_text` doet dit automatisch; als je `open()` gebruikt, wikkel het dan in een `with`‑blok.
* **Geef de voorkeur aan `lxml` boven de standaardparser** – deze is sneller en toleranter voor gebroken markup, wat essentieel is wanneer je **parse html file in python** van het web uitvoert.
* **Zorg er bij het maken vanuit een string voor dat het een volledig HTML‑document is** – ontbrekende `<html>`‑ of `<body>`‑tags kunnen onverwachte `None`‑resultaten opleveren bij het opvragen van elementen.

## Full script you can copy‑paste

Below is a self‑contained script that demonstrates every step discussed. Save it as `html_demo.py` and run `python html_demo.py`.

```python
#!/usr/bin/env python3
"""
Complete example: parse html file in python, load html document from file,
and create html document from string.
"""

from pathlib import Path
from bs4 import BeautifulSoup
from typing import Union

class HTMLDocument:
    """Wraps BeautifulSoup to provide a simple document interface."""
    def __init__(self, source: Union[str, Path]):
        if Path(source).exists():
            self._load_from_file(Path(source))
        else:
            self._load_from_string(source)

    def _load_from_file(self, file_path: Path):
        try:
            html = file_path.read_text(encoding="utf-8")
        except FileNotFoundError:
            raise FileNotFoundError(f"File not found: {file_path}")
        self.soup = BeautifulSoup(html, "lxml")

    def _load_from_string(self, html_string: str):
        self.soup = BeautifulSoup(html_string, "lxml")

    def title(self) -> str:
        return self.soup.title.string.strip() if self.soup.title else ""

    def pretty(self) -> str:
        return self.soup.prettify()


def safe_load_html(path: Union[str, Path]) -> HTMLDocument:
    """Safely load a local HTML file, handling common errors."""
    try:
        return HTMLDocument(path)
    except FileNotFoundError as e:
        raise RuntimeError(f"Unable to read local HTML file Python: {e}")
    except UnicodeDecodeError:
        raise RuntimeError("File encoding is not UTF-8; specify the correct encoding.")


def main():
    # Load from a real file (replace with your actual path)
    file_doc = safe_load_html("YOUR_DIRECTORY/index.html")
    print("File‑based title :", file_doc.title())
    print("\nPretty‑printed HTML from file:\n", file_doc.pretty()[:200], "...")

    # Create from a raw string
    html_str = "<html><head><title>Hello</title></head><body><h1>Hello</h1></body></html>"
    string_doc = HTMLDocument(html


## What Should You Learn Next?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [HTML-document opslaan naar bestand in Aspose.HTML voor Java](/html/english/java/saving-html-documents/save-html-to-file/)
- [HTML-documenten laden vanaf bestand in Aspose.HTML voor Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [HTML-document maken met Aspose.HTML – Stapsgewijze handleiding](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}