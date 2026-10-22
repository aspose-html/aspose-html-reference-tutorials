---
category: general
date: 2026-10-21
description: Lernen Sie, wie man HTML in Python parst, ein HTML‑Dokument lädt, CSS‑Selektoren
  verwendet und schnell Hyperlinks aus HTML extrahiert.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to parse html
- how to use selector
- extract hyperlinks from html
- load html document python
language: de
lastmod: 2026-10-21
og_description: Wie man HTML in Python mit CSS-Selektoren parst. Laden Sie ein HTML-Dokument,
  wählen Sie Links aus und extrahieren Sie Hyperlinks aus HTML mit sauberem Code.
og_image_alt: Screenshot showing how to parse HTML in Python with CSS selectors
og_title: HTML in Python parsen – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to parse HTML in Python, load an HTML document, use CSS selectors,
    and extract hyperlinks from HTML quickly.
  headline: How to parse HTML in Python using CSS selectors
  type: TechArticle
tags:
- python
- html-parsing
- css-selectors
title: Wie man HTML in Python mit CSS-Selektoren parst
url: /de/python/general/how-to-parse-html-in-python-using-css-selectors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man HTML in Python mit CSS‑Selektoren parst

Wenn Sie **how to parse html** in einem Python‑Skript benötigen, zeigt Ihnen diese Anleitung genau das. Sie lernen, wie man ein HTML‑Dokument lädt, wie man Selektor‑Syntax verwendet, um Elemente zu finden, und wie man Hyperlinks aus HTML extrahiert, ohne einen eigenen Parser zu schreiben.

HTML zu parsen ist eine gängige Aufgabe für Web‑Scraper, Daten‑Analyse‑Pipelines oder automatisierte Tests. Am Ende dieses Tutorials haben Sie eine wiederverwendbare Funktion, die ein HTML‑Dokument lädt, alle `<a>`‑Tags mit einem CSS‑Selektor auswählt und eine saubere Liste von URLs zurückgibt.

## Was Sie benötigen

- Python 3.8+ (der Code funktioniert mit jeder aktuellen Version)  
- Die **lxml**‑Bibliothek (`pip install lxml`) – bietet schnelles HTML‑Parsing und Unterstützung für CSS‑Selektoren  
- Eine HTML‑Datei, die Sie analysieren möchten (z. B. `sample.html`)  

Keine zusätzlichen Werkzeuge sind nötig; alles läuft mit der Standardbibliothek und einem einzigen Drittanbieter‑Paket.

## Schritt 1: How to parse HTML – Dokument laden

Der erste Schritt in jedem HTML‑Workflow ist, die Datei in den Speicher zu lesen. Die Verwendung von **lxml.html** liefert Ihnen ein Baum‑Objekt, das CSS‑Selektoren unterstützt.

```python
# step_1_load.py
from lxml import html

def load_html(path: str) -> html.HtmlElement:
    """
    Load an HTML document from the given file path.
    Returns an lxml HtmlElement that can be queried with CSS selectors.
    """
    with open(path, "r", encoding="utf-8") as f:
        content = f.read()
    # Parse the raw HTML string into a tree
    return html.fromstring(content)

# Example usage
doc = load_html("sample.html")
print("Document loaded – ready for selector queries.")
```

**Warum das wichtig ist:**  
`load_html` abstrahiert das Boilerplate‑Code‑Muster zum Einlesen von Dateien und garantiert, dass das Dokument mit einem fehlertoleranten HTML‑Parser geparst wird. Das ist der sicherste Weg, **load html document python** zu verwenden, ohne sich um fehlerhaftes Markup sorgen zu müssen.

## Schritt 2: How to use selector – alle Link‑Elemente finden

Sobald das Dokument geladen ist, können Sie einen CSS‑Selektor verwenden, um jedes `<a>`‑Tag zu finden. Der Selektor `"a"` trifft auf alle Anker‑Elemente zu, aber Sie können ihn verfeinern (z. B. `"a.external"` oder `"nav a"`).

```python
# step_2_selector.py
def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    """
    Return a list of <a> elements using a CSS selector.
    This demonstrates how to use selector syntax with lxml.
    """
    # The CSS selector "a" selects every anchor tag
    return doc.cssselect("a")

# Example usage
links = select_links(doc)
print(f"Found {len(links)} <a> elements.")
```

**Warum das wichtig ist:**  
Der **how to use selector**‑Ansatz lässt Sie komplexe Abfragen in einem einzigen, lesbaren String ausdrücken und vermeidet manuelle Baum‑Durchläufe. Er funktioniert für jedes von `lxml.cssselect` unterstützte CSS‑Muster.

## Schritt 3: Hyperlinks aus HTML extrahieren und verarbeiten

Jetzt, wo Sie eine Liste von `<a>`‑Elementen haben, können Sie das `href`‑Attribut jedes Elements auslesen. Der untenstehende Helfer normalisiert zudem relative URLs gegenüber einer Basis‑URL (falls Sie eine angeben).

```python
# step_3_extract.py
from urllib.parse import urljoin
from typing import Optional

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    """
    Return a list of href values from the given <a> elements.
    If base_url is supplied, relative URLs are resolved to absolute URLs.
    """
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            # Skip <a> tags without an href attribute
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

# Example usage
hyperlinks = extract_hyperlinks(links, base_url="https://example.com")
for url in hyperlinks:
    print(url)
```

**Erwartete Ausgabe** (angenommen, `sample.html` enthält drei Links):

```
https://example.com/page1.html
https://example.com/page2.html
https://external.org/resource
```

**Warum das wichtig ist:**  
`extract_hyperlinks` ist das Kernstück von **extract hyperlinks from html**. Es geht elegant mit fehlenden `href`‑Attributen um, löst relative Links auf und gibt eine reine Python‑Liste zurück, die Sie weiterverarbeiten können (z. B. mit requests, pandas oder einer Datenbank).

## Vollständiges End‑zu‑End‑Beispiel

Wenn Sie die drei Funktionen zusammenführen, erhalten Sie ein einzelnes Skript, das eine Datei lädt, alle Anker auswählt und jeden Hyperlink ausgibt.

```python
# parse_links.py
from lxml import html
from urllib.parse import urljoin
from typing import Optional

def load_html(path: str) -> html.HtmlElement:
    with open(path, "r", encoding="utf-8") as f:
        return html.fromstring(f.read())

def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    return doc.cssselect("a")

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

if __name__ == "__main__":
    # 1️⃣ Load the HTML document
    document = load_html("sample.html")
    # 2️⃣ Use selector to grab all <a> tags
    anchor_elements = select_links(document)
    # 3️⃣ Extract and print each hyperlink
    for url in extract_hyperlinks(anchor_elements, base_url="https://example.com"):
        print(url)
```

Das Ausführen von `python parse_links.py` gibt jeden vollständig aufgelösten Hyperlink in der Konsole aus. Dieses Skript demonstriert **how to parse html**, **how to use selector** und **extract hyperlinks from html** in einem einzigen, wiederverwendbaren Ablauf.

## Häufige Varianten und Edge‑Case‑Behandlung

| Situation | Was zu ändern ist | Grund |
|-----------|-------------------|-------|
| **Nur absolute URLs benötigt** | Das Argument `base_url` in `extract_hyperlinks` weglassen | Belässt relative URLs unverändert |
| **Sie benötigen auch den Link‑Text** | Ein Tupel `(href, link.text_content())` von `extract_hyperlinks` zurückgeben | Ermöglicht das Speichern von URL und Anker‑Text |
| **Große HTML‑Dateien** | `lxml.etree.iterparse` mit einem CSS‑Selektor‑Filter verwenden | Reduziert den Speicherverbrauch durch Streaming |
| **Anderer Selektor** | `"a"` durch `"nav a[href]"` oder `"div.content a.external"` ersetzen | Zielgerichtet eine Teilmenge von Links, nützlich für **how to use selector** auf komplexen Seiten |

**Pro‑Tipp:** Validieren Sie immer die extrahierten URLs, bevor Sie Netzwerk‑Requests durchführen. Ein kurzer `urlparse`‑Check kann fehlerhafte Zeichenketten herausfiltern und Ihren Scraper vor Abstürzen schützen.

## Fazit

Sie wissen jetzt, **how to parse html** in Python, wie man **load html document python** verwendet, wie man **how to use selector** einsetzt, um Elemente zu adressieren, und wie man **extract hyperlinks from html** effizient extrahiert. Das komplette Beispiel oben kann Sie‑r direkt in Ihr Projekt kopieren‑und‑einfügen, und Sie können jede Funktion an fortgeschrittene Anwendungsfälle wie Pagination, JavaScript‑generierten Content oder mehrseitiges Crawlen anpassen.

Nächste Schritte, die Sie erkunden könnten:

- Verwendung von **requests‑html** oder **Playwright**, um Seiten zu holen, die JavaScript‑Ausführung benötigen.  
- Speicherung der extrahierten URLs in einer CSV‑ oder SQLite‑Datenbank für spätere Analysen.  
- Hinzufügen von Fehlerbehandlung für Netzwerk‑Timeouts und HTTP‑Statuscodes.

Viel Spaß beim Parsen und experimentieren Sie gern mit verschiedenen Selektoren, um die volle Power von CSS‑basierten HTML‑Abfragen in Python freizuschalten!


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [How to configure HTML resource handling in Python and load an HTML document](/html/english/python/general/how-to-configure-html-resource-handling-in-python-and-load-a/)
- [How to Parse HTML in Python – Complete Guide](/html/english/python/general/how-to-parse-html-in-python-complete-guide/)
- [How to Load HTML in Python – Step‑by‑Step Guide](/html/english/python/general/how-to-load-html-in-python-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}