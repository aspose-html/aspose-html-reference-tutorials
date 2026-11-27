---
category: general
date: 2026-11-27
description: Erstelle ein SVG‑Dokument und speichere die SVG‑Datei mit Python. Lerne,
  Vektoren als SVG zu exportieren und schnell ein SVG‑Bild zu erzeugen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG file
- export vector as SVG
- save SVG image
- how to create SVG
language: de
lastmod: 2026-11-27
og_description: Erstelle ein SVG-Dokument und speichere die SVG-Datei mit Python.
  Diese Anleitung zeigt dir, wie du Vektoren als SVG exportierst und in wenigen Minuten
  ein SVG‑Bild erzeugst.
og_image_alt: Screenshot of a red circle saved as an SVG document
og_title: SVG-Dokument erstellen und SVG-Datei mit Python speichern
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  headline: Create SVG document and save SVG file with Python
  type: TechArticle
- description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  name: Create SVG document and save SVG file with Python
  steps:
  - name: Expected output
    text: 'The resulting `circle.svg` contains:'
  - name: Exporting more complex vectors
    text: 'If you need to **export vector as SVG** for multi‑shape illustrations,
      simply repeat the `dwg.add()` pattern with other primitives (`rect`, `line`,
      `path`, etc.). For example:'
  - name: Handling Unicode and text
    text: "SVG supports text elements with full Unicode support. Use `dwg.text(\"Hello,
      \U0001F30D\", insert=(5, 95), fill=\"black\")` to embed multilingual labels."
  - name: Saving to a different location
    text: 'When **save SVG image** to a user‑specified folder, validate the path to
      avoid permission errors:'
  - name: Minifying the output
    text: 'For production pipelines, you might want a smaller file size. Pass `pretty=False`
      to `dwg.tostring()` and write the result manually:'
  type: HowTo
tags:
- SVG
- Python
- Vector graphics
title: SVG-Dokument erstellen und SVG-Datei mit Python speichern
url: /de/python/general/create-svg-document-and-save-svg-file-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SVG-Dokument erstellen und SVG-Datei mit Python speichern

Wenn Sie ein **SVG-Dokument** von Grund auf neu **erstellen** müssen, führt Sie diese Anleitung durch den gesamten Prozess. Sie sehen, wie Sie eine **SVG-Datei** auf der Festplatte **speichern**, den Vektor als SVG exportieren und mit nur wenigen Codezeilen ein einsatzbereites SVG‑Bild erhalten.

Das programmgesteuerte Erzeugen skalierbarer Grafiken ist nützlich für Berichte, UI‑Icons oder jede Situation, in der Sie auflösungsunabhängige Bilder benötigen. Am Ende dieses Tutorials können Sie die Frage “**how to create SVG**?” für einfache Formen beantworten und das Muster auf komplexe Vektorkunstwerke erweitern.

## Was Sie benötigen

- Python 3.8 oder neuer  
- Das `svgwrite`‑Paket (installierbar über `pip`)  
- Ein beschreibbares Verzeichnis für die Ausgabedatei  

Keine externen Grafikeditoren sind erforderlich; alles läuft über die Befehlszeile.

## Schritt 1: Die Bibliothek `svgwrite` installieren

`svgwrite` bietet eine saubere, Python‑artige API zum Erstellen von SVG‑Markup. Installieren Sie es einmal mit:

```bash
pip install svgwrite
```

> **Pro‑Tipp:** Verwenden Sie eine virtuelle Umgebung (`python -m venv .venv`), um Abhängigkeiten zu isolieren.

## Schritt 2: SVG-Dokument erstellen

Jetzt erstellen wir tatsächlich **SVG‑Dokument**‑Objekte. Die Klasse `Drawing` repräsentiert das Wurzelelement `<svg>` und verwaltet Namespaces automatisch.

```python
import pathlib
import svgwrite

# Define where the file will be saved
output_path = pathlib.Path("output/circle.svg")
output_path.parent.mkdir(parents=True, exist_ok=True)

# Initialize a new SVG document with a 100×100 viewport
dwg = svgwrite.Drawing(
    filename=str(output_path),
    size=("100px", "100px"),
    profile="tiny"  # tiny profile keeps the file lightweight
)
```

Die `Drawing`‑Instanz ist der Einstiegspunkt für alle nachfolgenden SVG‑Operationen. Durch Angabe von `size` setzen wir die Canvas‑Abmessungen, was beeinflusst, wie Browser das Bild rendern.

## Schritt 3: Ein rotes Kreiselement hinzufügen

Das Hinzufügen von Formen ist unkompliziert. Die Methode `circle` erzeugt ein `<circle>`‑Element; wir fügen es dann dem Wurzelelement hinzu.

```python
# Create a red circle with radius 40 centered at (50, 50)
circle = dwg.circle(
    center=(50, 50),
    r=40,
    fill="red"
)

# Append the circle to the SVG root
dwg.add(circle)
```

Warum wir einen Kreis wählen: Kreise sind Vektor‑Primitive, die Skalierbarkeit ohne Qualitätsverlust demonstrieren und die Ausgabe ideal für das Testen von **export vector as SVG**‑Workflows machen.

## Schritt 4: SVG-Datei speichern

Abschließend schreiben wir das Markup auf die Festplatte. Dieser Schritt erfüllt die Anforderung **save SVG file** und erzeugt eine Datei, die Sie in jedem Browser oder Vektor‑Editor öffnen können.

```python
# Persist the SVG document to the filesystem
dwg.save()
print(f"SVG saved to {output_path.resolve()}")
```

Wenn Sie das Skript ausführen, sehen Sie eine Konsolennachricht, die den Speicherort der erzeugten Datei bestätigt.

### Erwartete Ausgabe

Die resultierende `circle.svg` enthält:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg height="100px" version="1.1" width="100px" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" fill="red"/>
</svg>
```

Öffnet man die Datei in einem Browser, wird ein scharfer roter Kreis angezeigt, und da sie vektor‑basiert ist, kann man unbegrenzt zoomen, ohne Pixelbildung.

## Schritt 5: Häufige Variationen und Randfälle

### Export komplexerer Vektoren

Wenn Sie **export vector as SVG** für mehrteilige Illustrationen benötigen, wiederholen Sie einfach das Muster `dwg.add()` mit anderen Primitive (`rect`, `line`, `path` usw.). Zum Beispiel:

```python
dwg.add(dwg.rect(insert=(10, 10), size=(30, 30), fill="blue"))
dwg.add(dwg.line(start=(0, 0), end=(100, 100), stroke="black", stroke_width=2))
```

### Umgang mit Unicode und Text

SVG unterstützt Textelemente mit voller Unicode‑Unterstützung. Verwenden Sie `dwg.text("Hello, 🌍", insert=(5, 95), fill="black")`, um mehrsprachige Beschriftungen einzubetten.

### Speichern an einem anderen Ort

Wenn Sie **save SVG image** in einen vom Benutzer angegebenen Ordner speichern, prüfen Sie den Pfad, um Berechtigungsfehler zu vermeiden:

```python
if not output_path.parent.exists():
    raise PermissionError(f"Cannot write to {output_path.parent}")
dwg.save()
```

### Ausgabe minifizieren

Für Produktionspipelines möchten Sie möglicherweise eine kleinere Dateigröße. Übergeben Sie `pretty=False` an `dwg.tostring()` und schreiben Sie das Ergebnis manuell:

```python
minified = dwg.tostring(pretty=False)
output_path.write_text(minified)
```

## Wie man SVG mit alternativen Bibliotheken erstellt (optional)

Während `svgwrite` leichtgewichtig und reines Python ist, gibt es andere Ökosysteme:

- **cairosvg** – konvertiert PNG, PDF oder HTML zu SVG.  
- **lxml** – ermöglicht das manuelle Erstellen von SVG‑Markup mittels XML‑APIs.  

Die Wahl einer Bibliothek hängt von der Komplexität Ihres Projekts und vorhandenen Abhängigkeiten ab.

## Fazit

Sie wissen jetzt, wie man ein **SVG‑Dokument** erstellt, Vektorformen hinzufügt und eine **SVG‑Datei** mit Python **speichert**. Die vollständige Lösung zeigt die Schritte zum **export vector as SVG**, zum Erzeugen eines **SVG‑Bildes** und beantwortet die häufige Frage **how to create SVG** programmgesteuert.

Ab hier können Sie:

- Das Skript mit Schleifen erweitern, um Diagramme oder Icons automatisch zu erzeugen.  
- Die SVG‑Ausgabe in Webanwendungen oder E‑Mail‑Vorlagen integrieren.  
- Animationen erkunden, indem Sie `<animate>`‑Elemente mit `svgwrite` hinzufügen.

Experimentieren Sie mit verschiedenen Formen, Farben und Verläufen, um die Leistungsfähigkeit skalierbarer Vektorgrafiken in Ihren Python‑Projekten voll auszuschöpfen. Viel Spaß beim Programmieren!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu beherrschen und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [SVG-Dokument erstellen – Kreis hinzufügen und als SVG speichern](/html/english/python/general/create-svg-document-add-a-circle-and-save-as-svg/)
- [SVG-Dokument in Python erstellen – Anleitung zum Konvertieren von SVG zu PNG](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)
- [SVG-Datei in Python laden – Vollständige Anleitung zum Exportieren, Einbetten & Konvertieren](/html/english/python/general/load-svg-file-python-complete-guide-to-export-embed-convert/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}