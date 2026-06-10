---
category: general
date: 2026-06-10
description: Lade HTML von einer URL, um Website‑Icons schnell zu erhalten. Lerne,
  wie man Favicons extrahiert, die Favicon‑URLs von Websites abruft und Sonderfälle
  in Python behandelt.
draft: false
keywords:
- load html from url
- get website icons
- how to extract favicons
- extract favicon urls
- fetch website favicon urls
language: de
og_description: Lade HTML von einer URL, um Favicons zu extrahieren und die Favicon‑URLs
  der Website abzurufen. Ein Schritt‑für‑Schritt‑Python‑Tutorial für Entwickler.
og_title: HTML von URL laden und Website‑Icons abrufen – Komplettanleitung
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
title: HTML von URL laden und Website‑Icons abrufen – Komplettanleitung
url: /de/python/general/load-html-from-url-and-get-website-icons-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML von URL laden und Website‑Icons abrufen – Komplettanleitung

Haben Sie schon einmal **HTML von einer URL laden** müssen, nur um das winzige Logo einer Seite zu holen? Sie sind nicht allein. Egal, ob Sie einen Lesezeichen‑Manager, ein SEO‑Dashboard oder einfach ein persönliches Hobby‑Projekt bauen – das Abrufen von Website‑Icons ist ein kleiner, aber wesentlicher Baustein.

In diesem Tutorial zeigen wir Ihnen **wie man Favicons extrahiert** mit reinem Python — ohne schweres Selenium, ohne Browser‑Magie. Am Ende können Sie **Website‑Favicon‑URLs abrufen**, relative Pfade verarbeiten und sogar mehrere Icons holen, falls eine Seite mehrere bereitstellt. Bereit? Dann legen wir los.

## Warum überhaupt HTML von einer URL laden?

Das Laden des rohen HTML einer Seite gibt Ihnen direkten Zugriff auf die `<link>`‑Tags, die Browser verwenden, um Favicons zu finden. Diese Tags sehen meist so aus:

```html
<link rel="icon" href="/favicon.ico">
<link rel="apple-touch-icon" href="https://example.com/apple-touch-icon.png">
```

Wenn Sie dieses Markup auslesen können, lesen Sie das `href`‑Attribut programmgesteuert aus und laden das Bild selbst herunter. Das ist schneller als Screenshots zu scrapen und funktioniert für jede Seite, die die gängigen Konventionen einhält.

## Schritt 1 – HTML‑Dokument von einer URL laden

Zuerst benötigen wir eine Möglichkeit, den Seitenquelltext zu holen. Die beliebteste Wahl in Python ist die **requests**‑Bibliothek, weil sie einfach, zuverlässig und Redirects von Haus aus behandelt.

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

> **Pro‑Tipp:** Arbeiten Sie hinter einem Unternehmens‑Proxy, übergeben Sie `proxies=` an `requests.get`. Außerdem verhindert ein kurzer Timeout, dass Ihr Skript bei toten Seiten hängen bleibt.

Jetzt können wir `fetch_html("https://example.com")` aufrufen und erhalten einen String mit dem Markup der Seite. Das ist das Kernstück von **HTML von URL laden** — der Rest der Pipeline arbeitet mit diesem String.

## Schritt 2 – Website‑Icons holen

Haben wir das HTML, suchen wir jedes `<link>`‑Element, dessen `rel`‑Attribut „icon“ enthält. Das eingebaute `html.parser`‑Modul kann das erledigen, aber **BeautifulSoup** macht den Code deutlich lesbarer.

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

Beachten Sie, dass wir `urljoin` verwenden, um `"/favicon.ico"` in `"https://example.com/favicon.ico"` zu verwandeln — ein häufiger Sonderfall beim **Website‑Icons holen**. Manche Seiten liefern unterschiedliche Icons für verschiedene Geräte, sodass Sie am Ende mehrere URLs erhalten können. Kein Problem; wir sammeln sie einfach alle.

## Schritt 3 – Favicon‑URLs extrahieren und anzeigen

Die einzelnen Teile zusammenzusetzen ist unkompliziert. Wir holen das HTML, führen den Extraktor aus und geben die resultierende Liste aus. Das finale Skript sieht so aus:

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

### Erwartete Ausgabe

Wird das Skript gegen eine Seite ausgeführt, die ein Standard‑Favicon bereitstellt, erhalten Sie etwa:

```
Found icon URLs: ['https://example.com/favicon.ico']
```

Falls die Seite mehrere Icons liefert (Apple‑Touch‑Icon, Shortcut‑Icon usw.), sehen Sie eine längere Liste:

```
Found icon URLs: [
    'https://example.com/favicon.ico',
    'https://example.com/apple-touch-icon.png',
    'https://example.com/favicon-32x32.png'
]
```

Damit ist der gesamte **Favicon‑URLs extrahieren**‑Workflow abgeschlossen — kompakt, mit wenigen Abhängigkeiten und bereit, in jedes Projekt integriert zu werden.

## Häufige Stolperfallen behandeln

| Problem | Warum es passiert | Schnelle Lösung |
|-------|----------------|-----------|
| **Relatives `href` ohne `<base>`‑Tag** | `urljoin` nimmt die Seiten‑URL als Basis, was in den meisten Fällen funktioniert. | Existiert ein `<base href="...">`‑Tag, lesen Sie ihn zuerst aus und übergeben Sie ihn als `base_url`. |
| **Fehlendes `rel="icon"`** | Manche Seiten nutzen `rel="shortcut icon"` oder eigene Werte. | Erweitern Sie das Lambda: `rel=lambda r: r and ("icon" in r.lower() or "shortcut" in r.lower())`. |
| **Redirects zu einer anderen Domain** | Das Favicon kann auf einem CDN liegen. | `urljoin` löst die neue Domain korrekt auf, weil es die finale Request‑URL (`response.url`) verwendet. |
| **Defekte Links (404)** | Das HTML verweist auf eine Datei, die nicht mehr existiert. | Nach dem Extrahieren der URLs können Sie jede mit einem HEAD‑Request prüfen, bevor Sie sie verwenden. |
| **Mehrere `<link>`‑Tags mit demselben Icon** | Doppelte Einträge vergrößern die Liste. | Nutzen Sie `set(icon_urls)`, um Duplikate vor der Rückgabe zu entfernen. |

## Weiterführend – Website‑Favicon‑URLs in großen Mengen holen

Möchten Sie **Website‑Favicon‑URLs** für eine Liste von Domains abrufen, verpacken Sie die `main`‑Logik in eine Schleife:

```python
domains = ["https://example.com", "https://python.org", "https://github.com"]
for site in domains:
    try:
        icons = extract_icon_links(fetch_html(site), site)
        print(site, "->", icons)
    except Exception as e:
        print(site, "error:", e)
```

Dieses Muster skaliert gut, und Sie können Caching (z. B. mit `functools.lru_cache`) hinzufügen, um dieselbe Seite nicht wiederholt zu belasten.

## Visueller Überblick

![Load HTML from URL diagram](load-html-url.png)

*Alt‑Text: Diagramm „HTML von URL laden“ zeigt die Schritte Abrufen → Parsen → Extrahieren.*

Das Bild fasst den dreischrittigen Prozess zusammen: **HTML von URL laden**, **Website‑Icons holen** und **Favicon‑URLs extrahieren**. Es ist praktisch, wenn Sie den Ablauf einem Teammitglied erklären wollen.

## Fazit

Wir haben eine vollständige, produktionsreife Lösung vorgestellt, wie man **HTML von URL lädt** und **Website‑Icons** ausschließlich mit den Python‑Bibliotheken `requests` und `BeautifulSoup` abruft. Durch das Auslesen der `href`‑Attribute von `<link rel="icon">`‑Tags können Sie **Favicon‑URLs extrahieren**, relative Pfade verarbeiten und sogar mehrere Icon‑Formate erhalten — alles in wenigen Dutzend Zeilen Code.

Was kommt als Nächstes? Versuchen Sie, die Icons in einen lokalen Ordner herunterzuladen, erzeugen Sie eine CSV‑Datei mit Domain‑zu‑Favicon‑Zuordnungen oder binden Sie die Logik in eine Flask‑API ein, die Favicons auf Abruf bereitstellt. Die Möglichkeiten, **Website‑Favicon‑URLs zu holen**, sind endlos, und die Kerntechnik bleibt gleich.

Haben Sie Fragen zu Sonderfällen oder möchten Sie einen cleveren Trick teilen? Hinterlassen Sie einen Kommentar unten — viel Spaß beim Icon‑Jagen!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [HTML‑Dokumente aus Datei laden in Aspose.HTML für Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [HTML‑Dokumente aus Stream laden in Aspose.HTML für Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-stream/)
- [Dokument‑Lade‑Events in Aspose.HTML für Java verarbeiten](/html/english/java/creating-managing-html-documents/handle-document-load-events/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}