---
category: general
date: 2026-07-05
description: Öffne Links in neuem Tab mit Python – lerne, wie man target="_blank"
  hinzufügt, das Linkziel ändert, den Attribut‑Enthält‑Selektor verwendet und das
  modifizierte HTML mühelos speichert.
draft: false
keywords:
- open links new tab
- add target blank
- change link target
- attribute contains selector
- save modified html
language: de
og_description: Öffne Links schnell in einem neuen Tab. Dieses Tutorial zeigt, wie
  man target="_blank" hinzufügt, das Linkziel ändert und das modifizierte HTML mit
  Python speichert.
og_title: Links in neuem Tab öffnen – Schritt‑für‑Schritt HTML‑Aktualisierungs‑Guide
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  headline: Open Links New Tab – Complete Guide to Updating HTML Anchors
  type: TechArticle
- description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  name: Open Links New Tab – Complete Guide to Updating HTML Anchors
  steps:
  - name: Expected Result
    text: 'Suppose `links.html` originally contained:'
  - name: What if a link already has a `rel` attribute?
    text: 'Our loop overwrites it with `"noopener"`. If you need to preserve existing
      values (e.g., `"nofollow"`), concatenate instead:'
  - name: How to handle multiple domains?
    text: 'Just expand the selector list:'
  - name: Does `prettify()` change the original HTML structure?
    text: It re‑indents but doesn’t alter tag order or attribute values. If you must
      keep the exact original whitespace, replace `prettify()` with `str(soup)` as
      mentioned earlier.
  type: HowTo
tags:
- HTML manipulation
- Python
- web automation
title: Links im neuen Tab öffnen – Vollständiger Leitfaden zum Aktualisieren von HTML-Ankern
url: /de/python/general/open-links-new-tab-complete-guide-to-updating-html-anchors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Links in neuem Tab öffnen – Komplett‑Guide zum Aktualisieren von HTML‑Ankern

Haben Sie schon einmal **Links in neuem Tab öffnen** auf einer statischen HTML‑Seite benötigt, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht allein. Viele Entwickler stoßen auf dieses Problem, wenn sie Legacy‑Seiten bereinigen oder Barrierefreiheits‑Optimierungen vornehmen. In diesem Tutorial zeigen wir Ihnen eine praktische Lösung, die **target blank hinzufügt**, **Link‑Ziel ändert** und sicher **modifiziertes HTML speichert** – alles mit wenigen Zeilen Python.

Wir erklären außerdem, wie Sie einen **attribute contains selector** verwenden, sodass Sie nur die Anker berühren, die Sie wirklich interessieren (z. B. jeder Link, der auf *example.com* zeigt). Am Ende haben Sie ein wiederverwendbares Skript, das Sie in jedes Projekt einbinden können, egal wie groß oder klein.

## Was Sie lernen werden

- Laden einer HTML‑Datei in ein manipulierbares Dokument‑Objekt.  
- Auswahl von `<a>`‑Elementen, deren `href`‑Attribut einen bestimmten Teilstring enthält.  
- **target blank hinzufügen** und das Attribut `rel="noopener"` setzen, um die Sicherheit zu erhöhen.  
- **modifiziertes HTML** wieder auf die Festplatte schreiben, ohne die Formatierung zu verlieren.  

Keine externen Abhängigkeiten außer der Standardbibliothek und **beautifulsoup4** (eine winzige Installation). Wenn Sie bereits einen anderen Parser verwenden, lassen sich die Konzepte direkt übernehmen.

---

## Voraussetzungen

- Python 3.8+ auf Ihrem Rechner installiert.  
- Grundlegende Kenntnisse in HTML und Python.  
- `beautifulsoup4`‑Paket (`pip install beautifulsoup4`).  

Das war’s – keine schweren Frameworks nötig.

---

## Schritt 1: Das HTML‑Dokument laden

Zuerst müssen wir die Quelldatei einlesen und an BeautifulSoup übergeben. Stellen Sie sich das vor wie das Öffnen einer leeren Leinwand, auf der Sie neue Attribute zeichnen können.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Path to the original HTML file
html_path = Path("YOUR_DIRECTORY/links.html")

# Read the file content
with html_path.open(encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")
```

> **Warum das wichtig ist:** Die Verwendung von `Path` macht den Code OS‑unabhängig, und `html.parser` ist eingebaut, sodass Sie für einfache Aufgaben keine zusätzlichen Parser benötigen.

---

## Schritt 2: Einen Attribute‑Contains‑Selector verwenden, um die richtigen Links zu finden

Wir wollen nur Anker berühren, die auf *example.com* zeigen. Der CSS‑Selector `a[href*='example.com']` erledigt genau das – `*=` bedeutet „enthält“. BeautifulSoups `select`‑Methode versteht diese Syntax.

```python
# Find all <a> tags whose href contains 'example.com'
selector = "a[href*='example.com']"
anchor_elements = soup.select(selector)
```

> **Pro‑Tipp:** Wenn Sie eine case‑insensitive Übereinstimmung benötigen, wechseln Sie zu einer kleinen Schleife, die prüft `if 'example.com' in a.get('href', '').lower()`.

Jetzt enthält `anchor_elements` jeden Link, der uns interessiert, bereit für die nächste Transformation.

---

## Schritt 3: Link‑Ziel ändern – target blank hinzufügen und den Link sichern

Einen Link in einem neuen Tab zu öffnen ist so einfach wie `target="_blank"` zu setzen. Moderne Browser empfehlen jedoch zusätzlich `rel="noopener"` (oder `noreferrer`) hinzuzufügen, um zu verhindern, dass die neu geöffnete Seite über `window.opener` auf das ursprüngliche Fenster zugreift. Dieser kleine Sicherheitsschritt kann Phishing‑Angriffe verhindern.

```python
for anchor in anchor_elements:
    # Open in a new tab
    anchor['target'] = "_blank"          # add target blank
    # Harden security
    anchor['rel'] = "noopener"           # prevent access to the opener page
```

> **Warum wir direkte Dictionary‑Zuweisung verwenden:** Sie erstellt das Attribut automatisch, falls es fehlt, und überschreibt es, falls es bereits existiert – perfekt für eine **change link target**‑Operation.

---

## Schritt 4: Modifiziertes HTML wieder auf die Festplatte schreiben

Der letzte Schritt besteht darin, das aktualisierte Markup in eine neue Datei zu schreiben. Das Original unverändert zu lassen, ermöglicht ein Zurücksetzen, falls etwas schiefgeht.

```python
# Destination path for the updated HTML
output_path = Path("YOUR_DIRECTORY/links-updated.html")

# Write the prettified HTML (preserves indentation)
with output_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())
```

> **Was `prettify()` macht:** Es formatiert das HTML mit schöner Einrückung, sodass die gespeicherte Datei später leichter zu lesen und zu vergleichen ist. Wenn Sie die ursprüngliche Whitespace‑Struktur beibehalten wollen, ersetzen Sie `prettify()` durch `str(soup)`.

---

## Komplettes Skript – Ein‑Klick‑Lösung

Unten finden Sie das vollständige, sofort ausführbare Skript. Speichern Sie es als `update_links.py` und führen Sie `python update_links.py` im Terminal aus.

```python
#!/usr/bin/env python3
"""
Open Links New Tab – script that adds target blank,
sets rel="noopener", and saves modified html.
"""

from pathlib import Path
from bs4 import BeautifulSoup

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Load the HTML document
    # ------------------------------------------------------------------
    html_path = Path("YOUR_DIRECTORY/links.html")
    with html_path.open(encoding="utf-8") as f:
        soup = BeautifulSoup(f, "html.parser")

    # ------------------------------------------------------------------
    # 2️⃣ Select anchors with an attribute contains selector
    # ------------------------------------------------------------------
    selector = "a[href*='example.com']"
    anchors = soup.select(selector)

    # ------------------------------------------------------------------
    # 3️⃣ Change link target – add target blank & secure the link
    # ------------------------------------------------------------------
    for a in anchors:
        a['target'] = "_blank"          # add target blank
        a['rel'] = "noopener"           # prevent opener access

    # ------------------------------------------------------------------
    # 4️⃣ Save modified html to a new file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/links-updated.html")
    with output_path.open("w", encoding="utf-8") as f:
        f.write(soup.prettify())

    print(f"✅ Updated {len(anchors)} link(s) and saved to {output_path}")

if __name__ == "__main__":
    main()
```

### Erwartetes Ergebnis

Angenommen, `links.html` enthielt ursprünglich:

```html
<a href="https://example.com/page1">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Nach dem Ausführen des Skripts sieht `links-updated.html` folgendermaßen aus:

```html
<a href="https://example.com/page1" target="_blank" rel="noopener">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Nur der Link zu *example.com* erhielt die **add target blank**‑Attribute, was zeigt, dass unser **attribute contains selector** exakt wie gewünscht funktioniert hat.

---

## Häufige Fragen & Sonderfälle

### Was, wenn ein Link bereits ein `rel`‑Attribut hat?

Unsere Schleife überschreibt es mit `"noopener"`. Wenn Sie bestehende Werte (z. B. `"nofollow"`) erhalten wollen, verketten Sie stattdessen:

```python
existing = a.get('rel', '')
a['rel'] = f"{existing} noopener".strip()
```

### Wie gehe ich mit mehreren Domains um?

Erweitern Sie einfach die Selektor‑Liste:

```python
domains = ["example.com", "sample.org"]
selector = ",".join([f"a[href*='{d}']" for d in domains])
anchors = soup.select(selector)
```

### Ändert `prettify()` die ursprüngliche HTML‑Struktur?

Es rückt ein, ändert aber weder die Reihenfolge der Tags noch die Attributwerte. Wenn Sie exakt die ursprüngliche Whitespace‑Struktur benötigen, ersetzen Sie `prettify()` durch `str(soup)`, wie bereits erwähnt.

---

## Pro‑Tipps für produktionsreife Skripte

- **Backup vor dem Überschreiben:** Fügen Sie einen Kopierschritt (`shutil.copy`) hinzu, um die Originaldatei zu sichern.  
- **Logging statt print:** Nutzen Sie das `logging`‑Modul für skalierbare Projekte.  
- **Batch‑Verarbeitung:** Durchlaufen Sie ein Verzeichnis mit `Path.rglob("*.html")`, um viele Dateien in einem Durchlauf zu aktualisieren.  

Diese Anpassungen verwandeln ein einfaches **open links new tab**‑Skript in ein robustes Werkzeug für jede Web‑Wartungs‑Workflow.

---

## Fazit

Sie haben nun eine solide, wiederverwendbare Methode, um **Links in neuem Tab öffnen** über jede statische HTML‑Sammlung hinweg zu implementieren. Durch die Nutzung eines **attribute contains selector** können Sie **change link target** präzise dort anwenden, wo Sie es benötigen, **target blank hinzufügen** und **modifiziertes HTML** speichern, ohne die Formatierung zu verlieren.

Probieren Sie es an einer Testseite aus und skalieren Sie es dann auf Ihre gesamte Site. Müssen Sie den Selektor für PDFs, DOCX oder andere Domains anpassen? Ändern Sie einfach den CSS‑String – alles andere bleibt gleich.

Hinterlassen Sie gern einen Kommentar, falls Sie auf Besonderheiten stoßen, oder teilen Sie, wie Sie das Skript für Ihre eigenen Projekte erweitert haben. Viel Spaß beim Coden, und mögen all Ihre Anker genau dort öffnen, wo Sie es wünschen!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungs‑Ansätze in Ihren eigenen Projekten erkunden können.

- [Wie man HTML mit Aspose.HTML für Java bearbeitet](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Wie man CSS – Inline‑CSS zu HTML‑Dokumenten in Aspose.HTML für Java hinzufügt](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}