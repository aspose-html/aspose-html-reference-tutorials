---
category: general
date: 2026-05-28
description: Wie man HTML in Python schnell parst – HTML‑Datei laden, CSS‑Selektor
  verwenden und href‑Attribute mit einem XPath‑contains‑Beispiel extrahieren.
draft: false
keywords:
- how to parse html
- get href attribute
- load html file
- use css selector
- xpath contains example
language: de
og_description: 'HTML in Python parsen: Lernen Sie, eine HTML‑Datei zu laden, CSS‑Selektoren
  zu verwenden und href‑Attribute mit einem XPath‑Contains‑Beispiel zu extrahieren.'
og_title: HTML in Python parsen – Schritt für Schritt
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
title: HTML in Python parsen – Vollständiger Leitfaden
url: /de/python/general/how-to-parse-html-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man HTML in Python parst – Komplettanleitung

Haben Sie sich schon einmal gefragt, **wie man HTML** in einem Python‑Skript parst, ohne einen schweren Browser zu verwenden? Sie sind nicht allein. Die meisten von uns müssen nur **eine HTML‑Datei laden**, ein paar Überschriften auslesen und vielleicht ein oder zwei Download‑Links holen. In diesem Tutorial zeige ich Ihnen genau das – mit einer winzigen Bibliothek, einem CSS‑Selektor und einem XPath contains‑Beispiel, um **href‑Attribute** zu erhalten.

Wir gehen den gesamten Prozess durch, vom Einlesen einer lokalen HTML‑Datei bis zum Ausgeben der Daten, die Sie benötigen. Kein Schnickschnack, nur ein praktisches, ausführbares Beispiel, das Sie noch heute in Ihr eigenes Projekt übernehmen können.

## Was Sie lernen werden

- Wie man **eine HTML‑Datei lädt** mit einem leichten Parser.
- Wie man **CSS‑Selektoren** verwendet, um Elemente wie Artikel‑Überschriften zu holen.
- Wie man ein **XPath contains‑Beispiel** erstellt, das Links filtert.
- Wie man sicher **href‑Attribute** aus den gefundenen Knoten ausliest.
- Tipps zum Umgang mit fehlerhaftem Markup und zur Erweiterung des Skripts.

Sie benötigen lediglich Python 3.8+ sowie die Pakete `lxml` und `cssselect` – beide mit einem einzigen `pip`‑Befehl installierbar.

---

## Schritt 1: Die HTML‑Datei laden

Bevor Sie irgendetwas tun, müssen Sie den HTML‑Inhalt im Speicher haben. Das Modul `lxml.html` bietet einen praktischen Helfer `fromstring`, aber wenn Sie eine Datei auf der Festplatte haben, ist die Funktion `parse` noch sauberer.

```python
# Step 1: Load the HTML file
from lxml import html

# Replace the path with the location of your HTML document
html_path = "YOUR_DIRECTORY/news.html"
doc = html.parse(html_path)

# The root element gives us access to CSS and XPath methods
root = doc.getroot()
```

> **Warum das wichtig ist:** Das Laden der Datei nur einmal hält den Speicherverbrauch niedrig und liefert Ihnen ein einzelnes `root`‑Objekt, das sowohl CSS‑Selektoren als auch XPath‑Abfragen unterstützt. Wenn die Datei fehlt oder nicht lesbar ist, wirft `html.parse` einen klaren `OSError`, den Sie später abfangen können.

### Profi‑Tipp
Falls Sie mit einem String statt einer Datei arbeiten, ersetzen Sie `html.parse` durch `html.fromstring(your_html_string)`.

---

## Schritt 2: CSS‑Selektor verwenden, um Überschriften zu holen

CSS‑Selektoren sind kompakt und jedem vertraut, der schon einmal ein Stylesheet geschrieben hat. Lassen Sie uns jedes `<h2>` innerhalb eines `<article>` holen – perfekt für Nachrichten‑Überschriften.

```python
# Step 2: Find all article headlines using a CSS selector
headline_nodes = root.cssselect("article h2")

# Print each headline's text content
for node in headline_nodes:
    print(node.text_content().strip())
```

**Erwartete Ausgabe** (unter der Annahme, dass das Beispiel‑HTML zwei Artikel enthält):

```
Breaking News: Python Takes Over the World
Local Developer Solves HTML Parsing Puzzle
```

> **Warum CSS?** Es ist lesbar, schnell und funktioniert out‑of‑the‑box mit `lxml`. Die Methode `cssselect` übersetzt den Selektor im Hintergrund in einen XPath‑Ausdruck, sodass Sie das Beste aus beiden Welten erhalten.

---

## Schritt 3: XPath contains‑Beispiel – “download”‑Links finden

Manchmal benötigen Sie eine feinere Kontrolle als CSS bietet. Die XPath‑Funktion `contains()` glänzt, wenn Sie einen Teilstring in einem Attribut abgleichen wollen, etwa alle Links, die auf einen Download zeigen.

```python
# Step 3: Find all links that contain the word "download" using XPath
download_link_nodes = root.xpath("//a[contains(@href, 'download')]")

# Extract and print the href attribute from each matching node
for node in download_link_nodes:
    href = node.get("href")
    print(href)
```

**Beispielausgabe**:

```
/files/report_download.pdf
https://example.com/downloads/setup.exe
```

> **Warum XPath contains?** Es ermöglicht Ihnen, direkt nach Attributwerten zu filtern, ohne zusätzliche Python‑Schleifen. Das ist das klassische **xpath contains example**, das Sie häufig in Tutorials sehen, hier jedoch mit einem realen Anwendungsfall kombiniert.

---

## Schritt 4: Alles in eine wiederverwendbare Funktion packen

Hard‑Coding von Pfaden und `print`‑Aufrufen ist für einen schnellen Test okay, aber Produktionscode mag Funktionen. Unten finden Sie einen kompakten Helfer, der sowohl Überschriften als auch Download‑Links zurückgibt.

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

Sie können die Funktion jetzt aufrufen und die Ergebnisse hübsch ausgeben:

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

Das Ausführen des Skripts liefert dieselbe Ausgabe wie zuvor, ist aber jetzt sauber verpackt für die Wiederverwendung.

---

## Schritt 5: Edge Cases und häufige Stolperfallen behandeln

1. **Fehlendes `href`‑Attribut** – XPath gibt trotzdem den `<a>`‑Knoten zurück, selbst wenn `href` fehlt. Schützen Sie sich vor `None`:

   ```python
   href = node.get("href")
   if href:
       download_links.append(href)
   ```

2. **Relative vs. absolute URLs** – Sind Ihre Links relativ, möchten Sie sie vielleicht gegen die Basis‑URL auflösen:

   ```python
   from urllib.parse import urljoin
   base_url = "https://example.com"
   absolute = urljoin(base_url, href)
   ```

3. **Fehlerhaftes HTML** – `lxml` ist tolerant, aber extrem kaputtes Markup kann `html.parse` zu einem `XMLSyntaxError` führen. Wickeln Sie den Parse‑Aufruf in einen `try/except`‑Block, um zu protokollieren und problematische Dateien zu überspringen.

4. **Performance bei großen Dateien** – Für mehr‑megabyte‑große Seiten sollten Sie `iterparse` streamen, anstatt das gesamte DOM in den Speicher zu laden.

---

## Visueller Überblick (optional)

![How to parse HTML flow diagram showing load file → CSS selector → XPath contains → get href attribute](how-to-parse-html-flow.png "How to parse HTML flow diagram")

*Alt‑Text enthält das primäre Schlüsselwort für SEO.*

---

## Fazit

Wir haben **wie man HTML in Python parst** von Anfang bis Ende behandelt: Laden einer HTML‑Datei, Verwendung eines CSS‑Selektors zum Auslesen von Artikel‑Überschriften, Erstellen eines XPath contains‑Beispiels zum Finden von Download‑Links und schließlich sicheres **Auslesen von href‑Attributen**. Die wiederverwendbare Funktion `parse_news_html` zeigt einen sauberen, wartbaren Ansatz, den Sie für jede Scraping‑Aufgabe anpassen können.

Bereit für die nächste Herausforderung? Versuchen Sie, das Skript zu erweitern, um:

- Tabellen mit `//table//tr`‑XPath‑Abfragen zu parsen.
- Bild‑`src`‑Attribute mit einem weiteren **xpath contains example** zu extrahieren.
- Asynchrones Abrufen mit `aiohttp` für Live‑Webseiten zu nutzen.

Viel Spaß beim Parsen und denken Sie daran – sobald Sie diese Grundlagen beherrschen, wird das restliche HTML‑Scraping zum Kinderspiel. Wenn Sie auf Probleme stoßen, hinterlassen Sie einen Kommentar unten – wir lösen das gemeinsam!

## Verwandte Tutorials

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}