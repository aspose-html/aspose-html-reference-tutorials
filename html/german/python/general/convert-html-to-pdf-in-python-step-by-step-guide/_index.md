---
category: general
date: 2026-08-06
description: HTML in PDF mit Python konvertieren – mit einem vollständigen Beispiel.
  Lernen Sie, PDF aus HTML zu erzeugen, HTML als PDF zu speichern und gängige Sonderfälle
  zu behandeln.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to pdf
- generate pdf from html
- save html as pdf
- create pdf from html file
- how to convert html to pdf
language: de
lastmod: 2026-08-06
og_description: HTML in PDF mit Python konvertieren und die Dokumentenerstellung automatisieren.
  Folgen Sie dieser Anleitung, um PDFs aus HTML zu erzeugen, HTML als PDF zu speichern
  und die Ausgabe anzupassen.
og_image_alt: Example of convert html to pdf script in Python
og_title: HTML in PDF mit Python konvertieren – umfassendes Tutorial
schemas:
- author: Aspose
  dateModified: '2026-08-06'
  description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  headline: Convert HTML to PDF in Python – step‑by‑step guide
  type: TechArticle
- description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  name: Convert HTML to PDF in Python – step‑by‑step guide
  steps:
  - name: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
    text: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
  - name: '**Input handling** – read the HTML file or build the markup programmatically.'
    text: '**Input handling** – read the HTML file or build the markup programmatically.'
  - name: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
    text: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
  type: HowTo
tags:
- HTML to PDF
- Python
- Document conversion
title: HTML in PDF mit Python konvertieren – Schritt‑für‑Schritt‑Anleitung
url: /de/python/general/convert-html-to-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML in PDF konvertieren in Python – Schritt‑für‑Schritt‑Anleitung

Wenn Sie **HTML in PDF** schnell konvertieren müssen, zeigt dieses Tutorial eine vollständige Lösung in Python. Sie sehen, wie man PDF aus HTML erzeugt, HTML als PDF speichert und den Konvertierungsprozess steuert, ohne den Code zu verlassen.

Der Leitfaden führt Sie durch die Installation einer zuverlässigen Bibliothek, das Laden eines HTML‑Dokuments, die Durchführung der Konvertierung und die Überprüfung des Ergebnisses. Am Ende können Sie PDF aus einer HTML‑Datei in jedem Python‑Projekt erstellen, egal ob die Quelle eine statische Seite oder dynamisch erzeugtes Markup ist.

## Was Sie lernen werden

* Installieren Sie die `pdfkit`‑ und `wkhtmltopdf`‑Abhängigkeiten, die für die HTML‑zu‑PDF‑Konvertierung erforderlich sind.  
* Laden Sie ein HTML‑Dokument von der Festplatte oder aus einem String.  
* Generieren Sie PDF aus HTML mit benutzerdefinierten Seitenformaten, Rändern und Kodierungsoptionen.  
* Speichern Sie HTML als PDF mit einem einzigen Funktionsaufruf.  
* Behandeln Sie typische Randfälle wie fehlende Assets, Unicode‑Zeichen und große Dateien.  

**Voraussetzungen** – Python 3.8+ und grundlegende Kenntnisse im Umgang mit Datei‑I/O. Keine externen Dienste erforderlich.

## HTML in PDF konvertieren – Gesamt‑Ablauf

Der Konvertierungsprozess besteht aus drei logischen Phasen:

1. **Preparation** – installieren Sie den Konverter und stellen Sie sicher, dass die `wkhtmltopdf`‑Binärdatei erreichbar ist.  
2. **Input handling** – lesen Sie die HTML‑Datei oder erzeugen Sie das Markup programmgesteuert.  
3. **Output generation** – rufen Sie den Konverter auf, schreiben Sie die PDF‑Datei und bestätigen Sie das Ergebnis.  

Jede Phase wird im folgenden Schritt detailliert behandelt.

## Schritt 1: Erforderliche Bibliotheken installieren

`pdfkit` bietet einen dünnen Python‑Wrapper um die weit verbreitete `wkhtmltopdf`‑Engine. Installieren Sie beide mit `pip` und prüfen Sie den Pfad zur Binärdatei.

```bash
# Install the Python wrapper
pip install pdfkit

# On Ubuntu/Debian install wkhtmltopdf package
sudo apt-get install wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf
```

Wenn Sie eine portable Binärdatei bevorzugen, laden Sie das passende Release von der [wkhtmltopdf GitHub page](https://github.com/wkhtmltopdf/wkhtmltopdf/releases) herunter und legen Sie sie in ein Verzeichnis, das zu Ihrem `PATH` hinzugefügt wird. Das Skript prüft den Pfad später automatisch.

## Schritt 2: Das HTML‑Dokument laden

Sie können eine statische Datei lesen, entfernte Inhalte abrufen oder HTML on the fly erzeugen. Das Beispiel unten lädt eine lokale Datei namens `sample.html`, die sich in einem von Ihnen definierten Verzeichnis befindet.

```python
import pathlib
import pdfkit

# Define the directory that holds the HTML source
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")

# Resolve the full path to the HTML file
html_path = BASE_DIR / "sample.html"

# Read the file content as a UTF‑8 string
with html_path.open(encoding="utf-8") as f:
    html_content = f.read()
```

Das Lesen der Datei als Unicode‑String stellt sicher, dass Zeichen wie „é“, „ß“ oder asiatische Glyphen während der Konvertierung erhalten bleiben. Dieser Schritt ist essenziell, wenn Sie **generate PDF from HTML** erzeugen, das internationalen Text enthält.

## Schritt 3: PDF aus HTML erzeugen

`pdfkit.from_string` konvertiert einen String, der HTML‑Markup enthält, in eine PDF‑Datei. Sie können ein Wörterbuch von Optionen übergeben, um Seitenformat, Ränder und Header/Footer‑Verhalten zu steuern.

```python
# Define the output PDF path
pdf_path = BASE_DIR / "sample.pdf"

# Conversion options – adjust as needed
options = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left": "0.75in",
    "encoding": "UTF-8",
    "enable-local-file-access": None,  # Allows loading local images/CSS
}

# Perform the conversion
pdfkit.from_string(html_content, str(pdf_path), options=options)
```

Der Aufruf oben **creates PDF from HTML file** und speichert sie in `sample.pdf`. Wenn das Quell‑HTML lokale CSS‑ oder Bilddateien referenziert, lässt das Flag `enable‑local‑file‑access` `wkhtmltopdf` diese Ressourcen auflösen.

### Warum dieser Ansatz funktioniert

* `pdfkit` delegiert die schwere Arbeit an `wkhtmltopdf`, das HTML mit der WebKit‑Engine rendert und so eine hohe Treue zum Original‑Layout garantiert.  
* Das Bereitstellen eines Options‑Dictionaries ermöglicht feine Abstimmungen der Ausgabe, ohne das HTML selbst zu ändern.  
* Die Verwendung von `from_string` hält den Workflow im Speicher, was nützlich ist, wenn das HTML on the fly erzeugt wird.

## Schritt 4: HTML als PDF speichern und Ausgabe überprüfen

Nach der Konvertierung möchten Sie möglicherweise bestätigen, dass das PDF existiert und lesbar ist. Das Snippet unten prüft die Dateigröße und öffnet das PDF mit dem standardmäßigen System‑Viewer (plattformabhängig).

```python
import os
import subprocess
import sys

# Verify that the PDF file was created
if pdf_path.is_file() and pdf_path.stat().st_size > 0:
    print(f"✅ PDF generated successfully: {pdf_path}")

    # Open the PDF for visual verification (optional)
    if sys.platform.startswith("darwin"):      # macOS
        subprocess.run(["open", str(pdf_path)])
    elif os.name == "nt":                      # Windows
        os.startfile(str(pdf_path))
    else:                                      # Linux and others
        subprocess.run(["xdg-open", str(pdf_path)])
else:
    raise FileNotFoundError("PDF generation failed – file not found or empty.")
```

Das Ausführen des Skripts gibt eine Erfolgsmeldung aus und startet den PDF‑Viewer, sodass Sie sofort bestätigen können, dass das Layout dem ursprünglichen HTML entspricht. Dieser Schritt schließt den **save html as pdf**‑Zyklus ab.

## Schritt 5: Erweiterte Optionen – PDF aus HTML‑Datei mit benutzerdefinierten Einstellungen erstellen

Manchmal haben Sie eine physische HTML‑Datei auf der Festplatte und bevorzugen `pdfkit.from_file` statt das Laden des Inhalts selbst. Diese Methode ist praktisch, wenn das HTML bereits komplexe relative Pfade enthält.

```python
# Directly convert a file path to PDF
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

Sie können außerdem eine Titelseite, ein Inhaltsverzeichnis oder JavaScript‑Ausführungsflags einbetten, indem Sie das `options`‑Dictionary erweitern. Zum Beispiel, um eine Titelseite hinzuzufügen:

```python
options.update({
    "cover": str(BASE_DIR / "cover.html"),
    "toc": None,  # Generates a table of contents
})
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

Diese Anpassungen zeigen **how to convert HTML to PDF** für anspruchsvollere Publishing‑Pipelines.

## Häufige Fallstricke und wie man sie vermeidet

| Problem | Ursache | Lösung |
|---------|---------|--------|
| Bilder oder CSS werden nicht angezeigt | `wkhtmltopdf` blockiert standardmäßig den Zugriff auf lokale Dateien | Fügen Sie `"enable-local-file-access": None` zum Options‑Dictionary hinzu |
| Unicode‑Zeichen werden verzerrt | Fehlende `encoding`‑Option oder falsches Charset beim Lesen der Datei | Immer `"encoding": "UTF-8"` setzen und die HTML‑Datei mit UTF‑8 lesen |
| PDF ist leer | Falscher Pfad zur `wkhtmltopdf`‑Binärdatei | Pfad explizit angeben: `pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")` |
| Große HTML‑Dateien führen zu Timeout | Standard‑Timeout zu kurz | `"javascript-delay": "2000"` setzen oder den Timeout mit `"timeout": "60"` erhöhen |

Durch das Beheben dieser Probleme wird ein zuverlässiger **generate pdf from html**‑Prozess in unterschiedlichen Umgebungen sichergestellt.

## Vollständiges Skript – End‑to‑End‑Beispiel

Speichern Sie das Folgende als `html_to_pdf.py` und führen Sie es mit `python html_to_pdf.py` aus. Passen Sie `YOUR_DIRECTORY` an, damit es auf Ihren Projektordner zeigt.

```python
#!/usr/bin/env python3
"""
Convert HTML to PDF in Python – complete, runnable example.
"""

import pathlib
import pdfkit
import os
import subprocess
import sys

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")          # <-- change this
HTML_FILE = BASE_DIR / "sample.html"
PDF_FILE = BASE_DIR / "sample.pdf"

# wkhtmltopdf configuration (optional – only needed if binary is not on PATH)
# config = pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")

# Conversion options – customize as required
OPTIONS = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left":


## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man HTML in PDF Java konvertiert – Verwendung von Aspose.HTML für Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [HTML in PDF konvertieren in .NET mit Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Wie man HTML in PDF Java konvertiert – Seitenränder mit Aspose.HTML festlegen](/html/english/java/advanced-usage/css-extensions-adding-title-page-number/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}