---
category: general
date: 2026-07-02
description: Wie man Icons aus einer HTML-Datei mit Python extrahiert. Lernen Sie,
  HTML-Dateien mit Python zu lesen, HTML-Dokumente zu parsen und das href-Attribut
  zu extrahieren, um Favicon-URLs zu erhalten.
draft: false
keywords:
- how to extract icons
- read html file python
- parse html document
- extract href attribute
- extract favicon urls
language: de
og_description: Wie man Icons aus einer HTML‑Seite mit Python extrahiert. Dieses Tutorial
  zeigt, wie man eine HTML‑Datei mit Python liest, das Dokument parst und die Favicon‑URLs
  extrahiert.
og_title: Wie man Symbole aus HTML extrahiert – Python‑Leitfaden
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
title: Wie man Icons aus HTML mit Python extrahiert – Vollständige Anleitung
url: /de/python/general/how-to-extract-icons-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Icons aus HTML mit Python extrahiert – Komplettanleitung

Haben Sie sich schon einmal gefragt, **wie man Icons** von einer Webseite extrahiert, ohne einen Browser zu öffnen? Vielleicht bauen Sie einen Site‑Katalog, ein SEO‑Audit‑Tool oder sind einfach nur neugierig auf die kleinen Favicons, die in Tabs erscheinen. Die gute Nachricht: Das geht in wenigen Zeilen Python – ohne Selenium, ohne headless Chrome, nur mit einer reinen HTML‑Datei.

In diesem Tutorial zeigen wir, wie man eine HTML‑Datei mit Python einliest, das HTML‑Dokument parst und schließlich **das href‑Attribut** aus `<link rel="icon">`‑Tags extrahiert, um die Favicon‑URLs zu erhalten. Am Ende haben Sie ein wiederverwendbares Snippet, das mit jedem statischen HTML funktioniert, das Sie ihm geben, und Sie sehen zudem, wie man Sonderfälle wie relative Pfade oder mehrere Icon‑Deklarationen behandelt.

## Was Sie lernen werden

- Laden einer lokalen HTML‑Datei mit Python (read html file python)  
- Verwenden eines leichten Parsers zum **parse html document** sicher  
- Finden von `<link>`‑Elementen, die ein Icon deklarieren  
- **Extract href attribute**‑Werte und in absolute URLs umwandeln  
- Sammeln und Ausgeben aller gefundenen **favicon URLs**  

Keine externen Dienste nötig – nur die Standardbibliothek und das beliebte **BeautifulSoup**‑Paket.

---

![Screenshot showing Python script extracting icons – how to extract icons](https://example.com/images/extract-icons-python.png "how to extract icons")

*Image alt text: "how to extract icons using a Python script"*

## Voraussetzungen

- Python 3.8+ installiert  
- `beautifulsoup4`‑Bibliothek (`pip install beautifulsoup4`)  
- Eine lokale HTML‑Datei, die Sie durchsuchen möchten (z. B. `sample.html`)  

Wenn Sie das bereits haben, legen wir los.

## Schritt 1: Read HTML File Python – Load the Document

Zuerst müssen wir die Datei öffnen und ihren Inhalt an einen Parser übergeben. Mit `with open(..., "r", encoding="utf‑8")` wird die Datei automatisch geschlossen, und die UTF‑8‑Kodierung deckt die meisten modernen Seiten ab.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Step 1: Load the HTML document from disk
html_path = Path("sample.html")          # adjust the path as needed
html_content = html_path.read_text(encoding="utf-8")
```

**Warum das wichtig ist:** Das Öffnen der Datei mit der richtigen Kodierung verhindert mysteriöse `�`‑Zeichen, die den Parser später zum Absturz bringen könnten. Die Verwendung von `Path` aus der Standardbibliothek macht den Code zudem plattformübergreifend.

## Schritt 2: Parse HTML Document – Find All Icon Links

Jetzt übergeben wir das rohe HTML an **BeautifulSoup**, das einen navigierbaren Baum aufbaut. Wir suchen nach jedem `<link>`‑Tag, dessen `rel`‑Attribut das Wort `icon` enthält. Beachten Sie, dass `rel` eine durch Leerzeichen getrennte Liste sein kann (`rel="shortcut icon"`), daher benötigen wir eine flexible Prüfung.

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

**Warum dieser Schritt entscheidend ist:** Ein naiver `soup.find_all("link", rel="icon")` würde Varianten wie `rel="shortcut icon"` oder `rel="apple-touch-icon"` übersehen. Unser Helfer `is_icon_link` deckt diese Fälle ab und macht die Extraktion robust.

## Schritt 3: Extract href Attribute – Pull the URLs

Nachdem wir die relevanten Tags gesammelt haben, holen wir nun das `href`‑Attribut aus jedem. Manche Seiten lassen `href` weg (selten, aber möglich), daher prüfen wir auf `None`. Außerdem werden Favicons häufig mit relativen URLs angegeben, sodass wir sie bei Bedarf gegen die Basis‑URL der Seite auflösen. Für eine lokale Datei behalten wir den Pfad einfach unverändert.

```python
# Step 3: Grab the href attribute from each icon link
icon_urls = []
for tag in icon_links:
    href = tag.get("href")
    if href:
        icon_urls.append(href.strip())
```

**Warum wir Whitespace entfernen:** HTML‑Autoren fügen manchmal versehentlich Leerzeichen um URLs herum ein, was spätere Anfragen zum Scheitern bringen würde. Das Trimmen sorgt für saubere Zeichenketten.

## Schritt 4: Extract Favicon URLs – Output the Results

Zum Schluss geben wir (oder returnen) die Liste der gefundenen URLs aus. In einem echten Skript würden Sie sie vielleicht in eine CSV schreiben, die Icons herunterladen oder an einen anderen Service weitergeben. Hier ein einfacher Loop, der das Ergebnis in der Konsole anzeigt.

```python
# Step 4: Display each discovered favicon URL
if not icon_urls:
    print("No icon links found in the document.")
else:
    for url in icon_urls:
        print("Favicon URL:", url)
```

### Umgang mit Sonderfällen

- **Multiple rel‑Werte:** Unsere `is_icon_link`‑Prüfung erkennt bereits `rel="shortcut icon"` und `rel="apple-touch-icon"`.  
- **Relative Pfade:** Wenn Sie später absolute URLs benötigen, verwenden Sie `urllib.parse.urljoin(base_url, href)`.  
- **Fehlendes href:** Die Prüfung `if href:` überspringt fehlerhafte Tags und verhindert `NoneType`‑Fehler.  
- **Doppelte Einträge:** Mit `icon_urls = list(dict.fromkeys(icon_urls))` können Sie Duplikate entfernen.

---

## Vollständiges Skript – All‑in‑One‑Lösung

Alles zusammengeführt, hier das komplette, sofort ausführbare Programm. Speichern Sie es als `extract_icons.py` und setzen Sie `html_path` auf eine beliebige Datei.

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

**Erwartete Ausgabe** (angenommen, `sample.html` enthält zwei Icons):

```
Favicon URL: /images/favicon.ico
Favicon URL: https://example.com/assets/apple-touch-icon.png
```

Führen Sie es mit `python extract_icons.py` aus und Sie sehen die URLs in der Konsole ausgegeben.

---

## Häufig gestellte Fragen

**Q: Was, wenn das HTML `<meta>`‑Tags für Icons verwendet?**  
A: Einige Seiten betten Icons über `<meta itemprop="image">` ein. Erweitern Sie `is_icon_link`, sodass es auch `meta` mit `itemprop="image"` prüft und dessen `content`‑Attribut ausliest.

**Q: Kann ich die Icons automatisch herunterladen?**  
A: Ja – übergeben Sie jede URL an `requests.get(url, stream=True)` und schreiben Sie den Inhalt in eine Datei. Denken Sie daran, relative URLs mit `urljoin` zu behandeln.

**Q: Funktioniert das auch bei entfernten Seiten?**  
A: Absolut. Ersetzen Sie den Datei‑Lese‑Schritt durch `requests.get(page_url).text` und übergeben Sie den HTML‑String an BeautifulSoup. Achten Sie dabei auf robots.txt und Rate‑Limits.

---

## Fazit

Wir haben gezeigt, **wie man Icons** aus beliebigem statischem HTML mit Python extrahiert – vom Einlesen der Datei bis zum Ausgeben jeder Favicon‑URL. Die Kernideen – Datei lesen, Dokument parsen, passende Tags finden und das `href`‑Attribut holen – sind wiederverwendbare Muster, die Sie bei vielen Web‑Scraping‑Aufgaben einsetzen können.

Nächste Schritte? Versuchen Sie, das Skript zu erweitern:

- Relative URLs gegen die Basis‑URL der Seite auflösen  
- Jede Icon‑Datei herunterladen und lokal speichern  
- Weitere Icon‑Formate unterstützen (`rel="mask-icon"` für Safari)  

Experimentieren Sie gern, und falls Sie auf Eigenheiten stoßen, hinterlassen Sie einen Kommentar unten. Viel Spaß beim Parsen!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren Projekten erkunden können.

- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Save HTML Document to File in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}