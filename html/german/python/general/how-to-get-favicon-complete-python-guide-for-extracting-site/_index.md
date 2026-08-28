---
category: general
date: 2026-06-26
description: Lernen Sie, wie Sie das Favicon erhalten, indem Sie HTML von einer URL
  laden und das href aus Link‑Tags extrahieren. Schritt‑für‑Schritt‑Python‑Code, um
  Website‑Icons schnell zu erhalten.
draft: false
keywords:
- how to get favicon
- load html from url
- get website icons
- extract href from link
- how to extract favicons
language: de
og_description: 'Wie man schnell ein Favicon erhält: HTML von einer URL laden, nach link rel=''icon'' suchen
  und href aus den link‑Tags mit Python extrahieren.'
og_title: Wie man ein Favicon bekommt – Python‑Tutorial
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
title: Wie man ein Favicon erhält – Vollständiger Python‑Leitfaden zum Extrahieren
  von Seiten‑Icons
url: /de/python/general/how-to-get-favicon-complete-python-guide-for-extracting-site/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein Favicon erhält – Vollständiger Python‑Leitfaden zum Extrahieren von Site‑Icons

Haben Sie sich schon einmal gefragt, **wie man ein Favicon** von einer beliebigen Website bekommt, ohne manuell den Quellcode zu durchsuchen? Sie sind nicht allein – Entwickler, SEO‑Profis und sogar Designer benötigen häufig das kleine Symbol, das eine Seite repräsentiert. In diesem Tutorial zeigen wir Ihnen einen sauberen, Python‑zentrierten Ansatz, um HTML von einer URL zu laden, die `<link rel="icon">`‑Tags zu finden und die Icon‑URLs herauszuziehen. Am Ende wissen Sie genau, **wie man ein Favicon** für jede Domain erhält, und Sie haben ein wiederverwendbares Skript für Ihre Projekte.

Wir behandeln alles vom Abrufen des HTMLs bis hin zu Sonderfällen wie relativen URLs und mehreren Icon‑Formaten. Keine externen Dienste nötig – nur die Standard‑`requests`‑Bibliothek und ein leichter HTML‑Parser. Bereit loszulegen? Dann tauchen wir ein.

## Voraussetzungen

- Python 3.8+ installiert (der Code funktioniert auch mit 3.10)  
- Grundkenntnisse in `requests` und List‑Comprehensions  
- Internetzugang zur Ziel‑Website  

Wenn Sie das bereits haben, super – springen Sie zum ersten Schritt. Andernfalls installieren Sie die einzige Abhängigkeit, die wir benötigen:

```bash
pip install requests beautifulsoup4
```

> **Pro‑Tipp:** `beautifulsoup4` ist ein erprobter Parser, der das „HTML von URL laden“ zum Kinderspiel macht.

## Schritt 1: HTML von URL mit Python laden  

Der erste Schritt, wenn Sie **wie man ein Favicon bekommt**, ist das Abrufen des Seitenquelltexts. Das ist der „HTML von URL laden“-Teil des Prozesses.

```python
import requests
from bs4 import BeautifulSoup

def fetch_html(url: str) -> str:
    """Download the raw HTML of *url* and return it as text."""
    response = requests.get(url, timeout=10)
    response.raise_for_status()   # will raise if the request failed
    return response.text
```

Warum `requests` verwenden? Es kümmert sich automatisch um Weiterleitungen, HTTPS‑Verifizierung und Timeouts, was weniger Überraschungen bedeutet, wenn Sie später **Website‑Icons erhalten** wollen.

## Schritt 2: Dokument parsen und Icon‑Links finden  

Jetzt, wo wir das HTML haben, müssen wir alle `<link>`‑Elemente finden, deren `rel`‑Attribut ein Icon angibt. Das ist das Herzstück von **wie man ein Favicon bekommt**.

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

Wir prüfen sowohl `icon` als auch `shortcut icon`, weil ältere Seiten noch Letzteres verwenden. Diese kleine Nuance verwirrt häufig, wenn man nach „wie man Favicons extrahiert“ sucht.

## Schritt 3: href aus Link‑Elementen extrahieren  

Mit den relevanten Tags in der Hand ist der nächste logische Schritt – **href aus link extrahieren** – unkompliziert.

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

`urljoin` stellt sicher, dass selbst wenn eine Seite einen relativen Pfad wie `/favicon.ico` liefert, Sie eine korrekte absolute URL erhalten – entscheidend für ein zuverlässiges **wie man ein Favicon bekommt**‑Skript.

## Schritt 4: Optional – Icon‑URLs validieren und filtern  

Manchmal listet eine Seite viele Icons auf (Apple‑Touch‑Icons, PNGs in verschiedenen Größen usw.). Wenn Sie nur die klassische `.ico`‑Datei benötigen, filtern Sie entsprechend. Dieser Schritt zeigt **wie man Favicons extrahiert** eines bestimmten Typs.

```python
def filter_ico_urls(urls: list[str]) -> list[str]:
    """Keep only URLs that end with .ico (case‑insensitive)."""
    return [u for u in urls if u.lower().endswith(".ico")]
```

Passen Sie den Filter gern an: Ersetzen Sie `".ico"` durch `".png"` oder prüfen Sie `rel="apple-touch-icon"`, wenn Sie hochauflösende Icons benötigen.

## Schritt 5: Icon‑Dateien herunterladen (falls Sie das eigentliche Bild wollen)  

Die URLs zu extrahieren ist die halbe Miete; das Herunterladen liefert Ihnen eine Datei, die Sie anzeigen oder speichern können. Hier ein kurzer Helfer:

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

Wenn Sie das nach den vorherigen Schritten ausführen, erhalten Sie eine lokale Kopie jedes gefundenen Favicons – perfekt zum Cachen oder für Offline‑Analysen.

## Schritt 6: Alles zusammenführen – vollständiges funktionierendes Beispiel  

Unten finden Sie das komplette, sofort ausführbare Skript, das **wie man ein Favicon bekommt** von jeder Site demonstriert. Kopieren, `target_url` anpassen und die Ausgabe beobachten.

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

**Erwartete Ausgabe (gekürzt zur Übersicht):**

```
Fetching HTML from https://www.python.org …
Finding <link> tags that declare icons …
Extracting href attributes – 3 candidates found.
Filtered to 1 .ico URLs: ['https://www.python.org/static/favicon.ico']
Saved favicons/favicon.ico
```

Wenn die Site nur PNG‑ oder Apple‑Touch‑Icons bereitstellt, listet das Skript stattdessen diese URLs auf und zeigt Ihnen genau **wie man ein Favicon bekommt** in jedem Szenario.

## Häufige Fragen & Sonderfälle  

### Was, wenn die Site ein `<meta>`‑Tag statt `<link>` verwendet?  
Einige ältere Seiten betten die Icon‑URL in ein `<meta name="msapplication‑TileImage">` ein. Sie können `find_icon_links` erweitern, um auch diese Meta‑Tags zu suchen und gleich zu behandeln.

### Wie gehe ich mit relativen URLs um, die mit `//` beginnen?  
`urljoin` löst protokoll‑relative URLs (`//example.com/favicon.ico`) automatisch basierend auf dem Schema der Basis‑URL auf, sodass Sie keine zusätzliche Logik benötigen.

### Kann ich mehrere Größen (z. B. 32×32, 180×180) automatisch abrufen?  
Ja – lassen Sie einfach den Schritt `filter_ico_urls` weg. Das Skript gibt jede gefundene Icon‑URL zurück, einschließlich PNGs in verschiedenen Dimensionen. Sie können dann nach Dateinamenmustern sortieren oder auswählen.

### Funktioniert das bei Sites, die Bots blockieren?  
Wenn eine Site 403 zurückgibt oder einen benutzerdefinierten User‑Agent erfordert, passen Sie den `requests.get`‑Aufruf an:

```python
headers = {"User-Agent": "Mozilla/5.0 (compatible; FaviconBot/1.0)"}
response = requests.get(url, headers=headers, timeout=10)
```

Diese kleine Änderung löst häufig das Problem „wie man ein Favicon bekommt“ bei strengeren Domains.

## Visueller Überblick  

![Diagramm, das den Ablauf zeigt, wie man ein Favicon von einer Website erhält – HTML laden, Link‑Tags parsen, href extrahieren, optional herunterladen](how-to-get-favicon-diagram.png "Diagramm zum Ablauf des Favicons abrufen")

*Der Alt‑Text des Bildes enthält das Haupt‑Keyword und erfüllt damit SEO‑Anforderungen für Bilder.*

## Fazit  

Wir haben **wie man ein Favicon bekommt** Schritt für Schritt durchgearbeitet: HTML von einer URL laden,

## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}