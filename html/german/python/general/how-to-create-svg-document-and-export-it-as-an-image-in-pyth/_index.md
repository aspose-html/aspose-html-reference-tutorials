---
category: general
date: 2026-10-02
description: Lernen Sie, wie man ein SVG-Dokument in Python erstellt, das SVG in einer
  Datei speichert und das SVG-Bild mit einem kurzen, vollständigen Skript exportiert.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG to file
- how to generate SVG
- export SVG image
- SVG Python tutorial
language: de
lastmod: 2026-10-02
og_description: Erstelle ein SVG-Dokument in Python und exportiere das SVG-Bild mit
  diesem praktischen Tutorial. Folge dem Skript, speichere das SVG in einer Datei
  und verwende die Vektorgrafik sofort wieder.
og_image_alt: Screenshot of a Python script that creates an SVG document
og_title: SVG-Dokument in Python erstellen – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-10-02'
  description: Learn how to create SVG document in Python, save SVG to file, and export
    SVG image with a short, complete script.
  headline: How to create SVG document and export it as an image in Python
  type: TechArticle
tags:
- SVG
- Python
- graphics
title: Wie man ein SVG‑Dokument erstellt und es in Python als Bild exportiert
url: /de/python/general/how-to-create-svg-document-and-export-it-as-an-image-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein SVG-Dokument erstellt und es als Bild in Python exportiert

Wenn Sie **SVG-Dokument erstellen** programmgesteuert benötigen, zeigt Ihnen dieses Tutorial genau, wie Sie das mit Python machen. Sie sehen ein vollständiges Skript, das einen einfachen Kreis erzeugt, das SVG in eine Datei speichert und ein exportierbares SVG‑Bild erzeugt, das Sie überall einbetten können.

Das Erzeugen skalierbarer Vektorgrafiken aus Code eliminiert den manuellen Aufwand, Formen in einem GUI‑Editor zu zeichnen. Am Ende dieses Leitfadens können Sie die SVG‑Erstellung in Daten‑Visualisierungs‑Pipelines, automatisierte Berichtsgeneratoren oder jedes Projekt integrieren, das gestochen scharfe, auflösungsunabhängige Grafiken erfordert.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

- Python 3.8 oder neuer installiert
- Die Bibliothek `svgwrite` (Installation mit `pip install svgwrite`)
- Schreibrechte für das Verzeichnis, in dem das SVG gespeichert wird

Diese Voraussetzungen halten das Beispiel leichtgewichtig und mit den meisten Umgebungen kompatibel.

## Schritt 1: Installieren und importieren der SVG‑Bibliothek

Der erste Schritt besteht darin, die Drittanbieter‑Bibliothek hinzuzufügen, die eine bequeme API für die SVG‑Erstellung bereitstellt.

```python
# Install the library (run once in your terminal)
# pip install svgwrite

import svgwrite  # Provides the SVGDocument class and element helpers
```

`svgwrite` abstrahiert die XML‑Struktur einer SVG‑Datei, sodass Sie sich auf Geometrie statt auf rohes Markup konzentrieren können.

## Schritt 2: Ein SVG‑Dokumentobjekt erstellen

Jetzt können Sie **SVG-Dokument erstellen** indem Sie `svgwrite.Drawing` instanziieren. Dieses Objekt repräsentiert das Wurzelelement `<svg>` und enthält alle nachfolgenden Formen.

```python
# Step 2: Initialize the SVG document
dwg = svgwrite.Drawing(
    filename="circle.svg",     # Desired output file name
    size=("100px", "100px"),   # Width and height of the canvas
    viewBox=("0 0 100 100")    # Coordinate system for drawing
)
```

Das Argument `size` definiert die gerenderten Pixelabmessungen, während `viewBox` ein Koordinatensystem festlegt, das zur später definierten Geometrie passt.

## Schritt 3: Ein Kreiselement hinzufügen

Ein Kreis wird durch sein Zentrum (`cx`, `cy`) und seinen Radius (`r`) definiert. Verwenden Sie den Helfer `circle`, um diese Attribute anzuhängen.

```python
# Step 3: Create a <circle> element
circle = dwg.circle(
    center=("50", "50"),   # cx = 50, cy = 50
    r="40",                # radius = 40
    fill="lightcoral",     # Fill color for visual clarity
    stroke="black",        # Outline color
    stroke_width="2"
)

# Append the circle to the SVG root
dwg.add(circle)
```

Der Kreis befindet sich in der Mitte der 100 × 100‑Leinwand und lässt an jeder Seite einen Rand von 10 Pixeln. Passen Sie `fill` und `stroke` an, um Ihrer Designsprache zu entsprechen.

## Schritt 4: Das SVG in eine Datei speichern

Nachdem die Grafik zusammengesetzt ist, können Sie **SVG in Datei speichern** mit der Methode `save`. Dies schreibt wohlgeformtes XML, das Browser und Vektor‑Editoren verstehen.

```python
# Step 4: Persist the SVG document
dwg.save()
print("SVG file saved as circle.svg")
```

Die Datei `circle.svg` befindet sich nun im aktuellen Arbeitsverzeichnis. Sie können sie in einem Web‑Browser, Inkscape oder einem anderen Tool, das das SVG‑Format unterstützt, öffnen.

## Schritt 5: Das exportierte SVG‑Bild überprüfen

Öffnen Sie die gespeicherte Datei in einem Browser, um das Ergebnis zu bestätigen. Sie sollten einen zentrierten Kreis mit den angegebenen Farben sehen. Das rohe XML sieht folgendermaßen aus:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg width="100px" height="100px" viewBox="0 0 100 100"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40"
          fill="lightcoral" stroke="black" stroke-width="2"/>
</svg>
```

Da SVG vektor‑basiert ist, können Sie das Bild ohne Qualitätsverlust skalieren, was es ideal für responsive Web‑Designs oder hochauflösenden Druck macht.

## Profi‑Tipp: SVG als PNG oder JPEG exportieren

Falls Sie eine Raster‑Version benötigen, kombinieren Sie die SVG‑Datei mit einem Konvertierungstool wie **CairoSVG**:

```python
# Optional: Convert SVG to PNG
# pip install cairosvg
import cairosvg

cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

Dieser Schritt demonstriert **SVG‑Bild exportieren** in ein Bitmap‑Format, nützlich, wenn nachgelagerte Systeme SVG nicht direkt rendern können.

## Häufige Variationen und Sonderfälle

| Variation | Wie man damit umgeht |
|-----------|----------------------|
| Mehrere Formen | Rufen Sie `dwg.add()` für jedes neue Element (rect, line, path) auf. |
| Dynamische Abmessungen | Berechnen Sie `size` und `viewBox` aus den Daten, bevor Sie `Drawing` erstellen. |
| Textbeschriftungen | Verwenden Sie `dwg.text("Label", insert=("10", "20"))` und stylen Sie mit `font_size` und `fill`. |
| Wiederverwendung des Dokuments | Halten Sie das `Drawing`‑Objekt im Speicher und rufen Sie `save()` auf, wann immer Sie eine aktualisierte Datei benötigen. |
| Große Dateien | Streamen Sie die Ausgabe mit `dwg.tostring()` und schreiben Sie manuell in ein Datei‑Objekt, um Speicher‑Spikes zu vermeiden. |

Die Behandlung dieser Szenarien stellt sicher, dass Ihr **wie man SVG generiert**‑Skript von einfachen Icons bis zu komplexen Diagrammen skaliert.

## Vollständige Skript‑Zusammenfassung

Unten finden Sie das komplette, ausführbare Beispiel, das alle Schritte und die optionale Konvertierung integriert:

```python
# Full SVG creation script – create SVG document, save SVG to file, export SVG image
import svgwrite
import cairosvg  # Optional, only needed for PNG conversion

# Initialize the drawing (SVG document)
dwg = svgwrite.Drawing(
    filename="circle.svg",
    size=("100px", "100px"),
    viewBox=("0 0 100 100")
)

# Define a circle element
circle = dwg.circle(
    center=("50", "50"),
    r="40",
    fill="lightcoral",
    stroke="black",
    stroke_width="2"
)

# Add the circle to the document
dwg.add(circle)

# Save the SVG file
dwg.save()
print("SVG file saved as circle.svg")

# Optional: convert SVG to PNG (export SVG image)
cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

Wenn Sie dieses Skript ausführen, entsteht `circle.svg` und, falls `cairosvg` installiert ist, `circle.png`. Beide Dateien sind bereit für die Einbindung in Webseiten, Berichte oder weitere Verarbeitung.

## Fazit

Sie wissen jetzt, wie man **SVG-Dokument erstellen** in Python, **SVG in Datei speichern** und **SVG‑Bild exportieren** für breitere Nutzung. Das Beispiel deckt die wesentlichen API‑Aufrufe ab, erklärt, warum jeder Schritt wichtig ist, und bietet Erweiterungen für komplexere Grafiken.

Als Nächstes können Sie weitere **SVG‑Python‑Tutorial**‑Themen erkunden, etwa das Zeichnen von Pfaden, das Anwenden von Farbverläufen und das Animieren von Elementen. Die Integration dieser Techniken ermöglicht es Ihnen, dynamische, datengetriebene Vektorgrafiken direkt aus Ihren Python‑Anwendungen zu erzeugen. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [SVG-Dokumente in Aspose.HTML für Java erstellen und verwalten](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [SVG-Dokument in Aspose.HTML für Java speichern](/html/english/java/saving-html-documents/save-svg-document/)
- [svg to png java – SVG mit Aspose.HTML für Java in Bild konvertieren](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}