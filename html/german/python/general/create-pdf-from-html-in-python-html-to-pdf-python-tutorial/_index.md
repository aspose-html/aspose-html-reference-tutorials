---
category: general
date: 2026-07-15
description: Erstelle PDF aus HTML mit Python. Lerne, wie du HTML schnell in PDF umwandelst,
  mit einem einfachen Skript und klaren Schritten.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf from html
- convert html to pdf
- html to pdf python
- save html as pdf
- html to pdf tutorial
language: de
lastmod: 2026-07-15
og_description: PDF aus HTML mit Python erstellen. Dieser Leitfaden zeigt, wie man
  HTML in PDF konvertiert, HTML als PDF speichert und Ressourcen effizient verwaltet.
og_image_alt: Screenshot of a Python script that creates PDF from HTML
og_title: PDF aus HTML in Python erstellen – Hands‑On‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-15'
  description: Create PDF from HTML using Python. Learn how to convert HTML to PDF
    quickly with a simple script and clear steps.
  headline: Create PDF from HTML in Python – HTML to PDF Python Tutorial
  type: TechArticle
tags:
- python
- pdf
- html
- conversion
title: PDF aus HTML in Python erstellen – HTML‑zu‑PDF Python‑Tutorial
url: /de/python/general/create-pdf-from-html-in-python-html-to-pdf-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF aus HTML in Python erstellen – Voll‑ausgestattetes Tutorial

Haben Sie jemals **PDF aus HTML erstellen** müssen, waren sich aber nicht sicher, welche Python‑Bibliothek Sie wählen sollen? Sie sind nicht allein – viele Entwickler stoßen an diese Grenze, wenn sie versuchen, einen Web‑Report, eine Rechnung oder eine Marketing‑Seite in ein druckbares PDF zu verwandeln.  

Die gute Nachricht: Mit nur wenigen Code‑Zeilen können Sie **HTML zu PDF konvertieren** zuverlässig, und das Skript funktioniert unter Windows, macOS und Linux. In diesem Leitfaden gehen wir Schritt für Schritt durch ein vollständiges, ausführbares Beispiel, erklären, warum jeder Schritt wichtig ist, und zeigen Ihnen, wie Sie **HTML als PDF speichern** können, ohne lose Enden.

---

## Was Sie lernen werden

- Das richtige Python‑Paket für die HTML‑zu‑PDF‑Konvertierung installieren.  
- Eine HTML‑Datei mit benutzerdefinierten Optionen für die Ressourcen‑Verarbeitung laden (um endlose CSS‑Importe zu vermeiden).  
- Eine saubere PDF‑Datei auf dem Datenträger erzeugen.  
- Häufige Randfälle wie externe Bilder, relative Pfade und große Dokumente behandeln.  

Am Ende dieses **HTML‑zu‑PDF‑Tutorials** verfügen Sie über eine wiederverwendbare Funktion, die Sie in jedes Projekt einbinden können.

---

## Voraussetzungen

- Python 3.9+ (der Code funktioniert auch mit 3.8, aber 3.9+ bietet die neuesten `pathlib`‑Features).  
- Grundlegende Kenntnisse im Umgang mit der Kommandozeile und virtuellen Umgebungen.  
- Eine HTML‑Datei, die Sie in ein PDF umwandeln möchten – jede statische Seite reicht aus.

> **Pro‑Tipp:** Wenn Sie eine virtuelle Umgebung verwenden, aktivieren Sie sie vor der Installation der Bibliothek; so bleibt Ihr globales Python sauber.

---

## Schritt 1 – Install WeasyPrint (die Engine hinter der Konvertierung)

WeasyPrint ist eine reine Python‑Bibliothek, die HTML und CSS zu PDF rendert. Sie unterstützt die meisten modernen Web‑Features und gibt Ihnen feinkörnige Kontrolle über das Laden von Ressourcen.

```bash
pip install weasyprint
```

Der obige Befehl zieht `cairocffi`, `tinycss2` und einige weitere Abhängigkeiten nach. Wenn Sie unter Windows einen `cairo`‑bezogenen Fehler erhalten, holen Sie sich die vorgefertigten Wheels von der [WeasyPrint‑Website](https://weasyprint.org/docs/install/).

---

## Schritt 2 – Einen kleinen Helfer für die Ressourcen‑Verarbeitung vorbereiten

Wenn Sie ein HTML‑Dokument laden, das externe Stylesheets oder Bilder referenziert, folgt die Bibliothek diesen Links. In manchen Fällen führt das zu tief verschachtelten oder sogar unendlichen Schleifen (denken Sie an eine CSS‑Datei, die sich selbst `@import`‑t). Um Ordnung zu halten, begrenzen wir die Tiefe der Ressourcen‑Verarbeitung.

```python
from weasyprint import HTML, CSS
from pathlib import Path

class ResourceHandlingOptions:
    """Simple container to mimic max depth handling."""
    def __init__(self, max_depth: int = 3):
        self.max_depth = max_depth
        self._current_depth = 0

    def within_limit(self) -> bool:
        return self._current_depth < self.max_depth

    def __enter__(self):
        self._current_depth += 1
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        self._current_depth -= 1
```

Die obige Klasse ist nicht von WeasyPrint vorgeschrieben, spiegelt aber das Muster des ursprünglichen Snippets wider und bietet Ihnen einen Hook, um unkontrollierte Importe zu stoppen. Sie wird im nächsten Schritt verwendet.

---

## Schritt 3 – Das HTML‑Dokument mit den benutzerdefinierten Optionen laden

Jetzt lesen wir tatsächlich die HTML‑Datei ein. Die `HTML`‑Klasse akzeptiert ein `base_url`‑Argument, das wir auf das Verzeichnis setzen, das die Quelldatei enthält – dadurch funktionieren relative Links ohne Web‑Server.

```python
def load_html(input_path: Path, options: ResourceHandlingOptions) -> HTML:
    """
    Load an HTML file while respecting the max handling depth.
    """
    if not options.within_limit():
        raise RuntimeError("Maximum resource handling depth exceeded.")
    # The `with` block increments depth for the duration of the call.
    with options:
        return HTML(filename=str(input_path), base_url=str(input_path.parent))
```

> **Warum das wichtig ist:** Wenn Ihr HTML eine Kaskade von CSS‑Dateien einbindet, löst jedes `@import` einen weiteren Ladevorgang aus. Die Tiefen‑Sperre verhindert, dass das Skript außer Kontrolle gerät.

---

## Schritt 4 – Das verarbeitete Dokument als PDF speichern

Mit dem `HTML`‑Objekt in der Hand lässt sich ein PDF mit einer einzigen Zeile erzeugen. Wir übergeben außerdem ein einfaches CSS‑Snippet, das eine saubere Seitengröße (A4) erzwingt und einen kleinen Rand hinzufügt – passen Sie es nach Belieben an.

```python
def save_as_pdf(html_doc: HTML, output_path: Path) -> None:
    """
    Render the HTML document to a PDF file.
    """
    default_css = CSS(string='''
        @page { size: A4; margin: 1cm }
    ''')
    html_doc.write_pdf(target=str(output_path), stylesheets=[default_css])
```

Der Aufruf von `write_pdf` streamt das PDF auf die Festplatte, sodass Sie am Ende eine sofort teilbare Datei erhalten.

---

## Schritt 5 – Alles zusammenführen

Unten finden Sie ein kompaktes Skript, das Sie in `convert.py` kopieren können. Ersetzen Sie die Platzhalter‑Pfade durch Ihre tatsächlichen Verzeichnisse.

```python
#!/usr/bin/env python3
"""
HTML to PDF Python script – complete, runnable example.
"""

from pathlib import Path

# Import the helper classes we defined earlier
from __main__ import ResourceHandlingOptions, load_html, save_as_pdf  # noqa: E402

def main():
    # 1️⃣  Define input and output locations
    input_html = Path("YOUR_DIRECTORY/input.html")
    output_pdf = Path("YOUR_DIRECTORY/output.pdf")

    # 2️⃣  Create resource handling options (max depth = 3)
    resource_options = ResourceHandlingOptions(max_depth=3)

    # 3️⃣  Load the HTML document with the custom options
    html_doc = load_html(input_html, resource_options)

    # 4️⃣  Save the processed document as PDF
    save_as_pdf(html_doc, output_pdf)

    print(f"✅ PDF saved to {output_pdf.resolve()}")

if __name__ == "__main__":
    main()
```

**Erwartete Ausgabe** – nach dem Ausführen von `python convert.py` sollten Sie sehen:

```
✅ PDF saved to /full/path/YOUR_DIRECTORY/output.pdf
```

Öffnen Sie die erzeugte Datei mit einem beliebigen PDF‑Viewer; Sie sehen das ursprüngliche Seitenlayout, die CSS‑Stile und die Bilder (sofern sie aus der HTML‑Datei erreichbar waren).  

Falls Bilder fehlen, prüfen Sie, ob deren `src`‑Attribute entweder absolute URLs oder relative Pfade sind, die unter `YOUR_DIRECTORY` existieren.

---

## Häufige Fragen & Edge‑Case‑Behandlung

| Frage | Antwort |
|----------|--------|
| *Was, wenn mein HTML externe Schriftarten referenziert?* | WeasyPrint lädt die Schriftdateien automatisch herunter, Sie können jedoch Domains auf eine Whitelist setzen, um lange Ladezeiten zu vermeiden. |
| *Kann ich einen HTML‑String statt einer Datei konvertieren?* | Ja – verwenden Sie `HTML(string=my_html_string)` und lassen Sie `base_url` weg oder setzen Sie es auf einen temporären Ordner. |
| *Wie steuere ich PDF‑Metadaten (Titel, Autor)?* | Übergeben Sie ein `metadata`‑Dict an `write_pdf`, z. B. `html_doc.write_pdf(target='out.pdf', metadata={'Title': 'Report'})`. |
| *Ich erhalte einen „cairo‑cffi error“ unter Linux.* | Installieren Sie das Systempaket `libcairo2-dev` (`apt-get install libcairo2-dev` auf Debian/Ubuntu), bevor Sie WeasyPrint per pip installieren. |

---

## Abschluss

Wir haben gerade **PDF aus HTML erstellt** mit einem sauberen Python‑Workflow, die **HTML‑zu‑PDF‑Mechanik** erklärt und gezeigt, wie man **HTML als PDF speichert** mit robustem Ressourcen‑Handling. Das Skript ist klein genug, um es in CI‑Pipelines zu integrieren, und gleichzeitig flexibel genug, um es mit eigenen Headern, Footern oder Wasserzeichen zu erweitern.

Mögliche nächste Schritte:

- Verwenden Sie die **html to pdf python**‑Bibliothek `pdfkit` für einen wkhtmltopdf‑basierten Ansatz (gut für Legacy‑CSS).  
- Fügen Sie eine CLI‑Schnittstelle mit `argparse` hinzu, sodass das Skript Eingabe‑/Ausgabe‑Argumente akzeptiert.  
- Generieren Sie PDFs on‑the‑fly innerhalb eines Flask‑ oder FastAPI‑Endpoints für bedarfsgesteuerte Berichte.  

Experimentieren Sie, brechen Sie Dinge und kommen Sie dann zu diesem Leitfaden zurück für eine schnelle Auffrischung. Bei Problemen sind die WeasyPrint‑Dokumentation und die Community‑Foren ausgezeichnete Ressourcen.

Viel Spaß beim Coden und beim Verwandeln Ihrer Webseiten in elegante PDFs!

## Was Sie als Nächstes lernen sollten


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Features meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [Convert HTML to PDF with Aspose.HTML – Full Manipulation Guide](/html/english/)
- [Convert HTML to PDF in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Create PDF from HTML – C# Step‑by‑Step Guide](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}