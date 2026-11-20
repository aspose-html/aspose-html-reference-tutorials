---
category: general
date: 2026-07-02
description: Erstelle SVG‑Dokumente schnell mit Python. Lerne, SVG‑Dateien zu speichern,
  ein einfaches SVG‑Bild zu erzeugen und SVG aus dem Code mit nur wenigen Zeilen zu
  exportieren.
draft: false
keywords:
- create svg document
- save svg file
- how to generate svg
- export svg from code
- create basic svg image
language: de
og_description: Erstellen Sie SVG-Dokumente einfach. Dieser Leitfaden zeigt, wie man
  SVG generiert, SVG-Dateien speichert und SVG aus Code exportiert, anhand eines klaren
  Python-Beispiels.
og_title: SVG-Dokument erstellen – Schnelles Python‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Create SVG document quickly with Python. Learn to save SVG file, generate
    a basic SVG image, and export SVG from code in just a few lines.
  headline: Create SVG Document – Step‑by‑Step Guide for Beginners
  type: TechArticle
- description: Create SVG document quickly with Python. Learn to save SVG file, generate
    a basic SVG image, and export SVG from code in just a few lines.
  name: Create SVG Document – Step‑by‑Step Guide for Beginners
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: How can I add text or other shapes?
    text: Just call `svg.create_element("text", {...})` or `svg.create_element("circle",
      {...})` and append them just like the rectangle. The same **how to generate
      SVG** logic applies.
  - name: What if I need to **export SVG from code** with a transparent background?
    text: Remove any `fill` attribute from the root `<svg>` element or set `fill="none"`
      on shapes that should be transparent. The XML stays valid; browsers will render
      the transparency automatically.
  - name: Can I **save SVG file** with pretty‑printed formatting?
    text: '`ElementTree` writes compact XML by default. For a human‑readable version,
      you can use `xml.dom.minidom` to re‑format:'
  - name: What about performance for large SVGs?
    text: When generating thousands of elements, consider building a list of `ET.Element`
      objects first and then extending the root in one go. This reduces the number
      of tree mutations and speeds up the **save SVG file** operation.
  type: HowTo
tags:
- SVG
- Python
- Graphics
- File I/O
title: SVG-Dokument erstellen – Schritt‑für‑Schritt‑Anleitung für Anfänger
url: /de/python/general/create-svg-document-step-by-step-guide-for-beginners/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SVG-Dokument erstellen – Schritt‑für‑Schritt‑Anleitung für Anfänger

Haben Sie sich jemals gefragt, wie man **create SVG document** ohne einen Grafikeditor zu öffnen? Sie sind nicht allein. Egal, ob Sie ein winziges Symbol für eine Webseite oder ein dynamisches Diagramm benötigen, das on‑the‑fly generiert wird – die Möglichkeit, **create SVG document** programmgesteuert zu erstellen, spart Zeit und hält alles versionskontrolliert.

In diesem Tutorial führen wir Sie durch ein vollständiges, ausführbares Beispiel, das genau zeigt, wie man **create SVG document**, **save SVG file** und sogar die hartnäckige Frage „**how to generate SVG**“ beantwortet, die beim Automatisieren von Grafiken auftaucht. Am Ende haben Sie ein rotes Quadrat auf der Festplatte und wissen, wie man **export SVG from code** für jedes zukünftige Projekt verwendet.

## Was Sie benötigen

Bevor wir starten, stellen Sie sicher, dass Sie Folgendes haben:

* Python 3.9 oder neuer (die Standardbibliothek erledigt die schwere Arbeit)
* Einen Texteditor oder eine IDE Ihrer Wahl – VS Code, PyCharm oder sogar Notepad reichen aus
* Schreibrechte für einen Ordner, in dem Sie **save SVG file** (wir verwenden ein `output/`‑Verzeichnis)

Keine externen Pakete sind erforderlich, sodass die Einrichtung buchstäblich ein paar Minuten dauert.

## Schritt 1: SVG‑Hilfsfunktionen einrichten (Dokument erstellen)

Zuerst benötigen wir einen kleinen Helfer, der die XML‑Struktur hinter einem SVG aufbaut. Betrachten Sie dies als die Leinwand, auf der wir später **create basic SVG image**‑Elemente platzieren.

```python
import pathlib
import xml.etree.ElementTree as ET

# ----------------------------------------------------------------------
# Helper class that mimics a minimal SVG library.
# ----------------------------------------------------------------------
class SVGDocument:
    """Simple wrapper to generate an SVG document using ElementTree."""
    
    SVG_NS = "http://www.w3.org/2000/svg"
    def __init__(self, width: int = 200, height: int = 200):
        # Register the SVG namespace so the output looks clean
        ET.register_namespace("", self.SVG_NS)
        self.root = ET.Element(
            "svg",
            attrib={
                "xmlns": self.SVG_NS,
                "width": str(width),
                "height": str(height),
                "version": "1.1"
            }
        )
    
    def create_element(self, tag: str, attributes: dict) -> ET.Element:
        """Create an SVG element with the given attributes."""
        return ET.Element(tag, attrib=attributes)
    
    def append_child(self, element: ET.Element):
        """Append a child element to the root <svg> node."""
        self.root.append(element)
    
    def save(self, file_path: str):
        """Write the SVG XML to a file, creating directories as needed."""
        path = pathlib.Path(file_path)
        path.parent.mkdir(parents=True, exist_ok=True)
        tree = ET.ElementTree(self.root)
        tree.write(str(path), encoding="utf-8", xml_declaration=True)
```

**Warum dieser Schritt wichtig ist:** Die Klasse `SVGDocument` abstrahiert das low‑level XML‑Handling. Indem wir sie in einer Klasse kapseln, bleibt der Rest des Codes sauber – eine bewährte Praxis, wenn Sie **export SVG from code** in größeren Anwendungen durchführen.

## Schritt 2: Ein Rechteck hinzufügen – Der Kern eines **Create Basic SVG Image**‑Beispiels

Jetzt, wo wir ein Dokumentobjekt haben, fügen wir ein rotes Quadrat hinzu. Das ist das Herzstück des **create basic SVG image**‑Abschnitts des Tutorials.

```python
# ----------------------------------------------------------------------
# Step 2: Build the SVG content
# ----------------------------------------------------------------------
svg = SVGDocument(width=120, height=120)   # canvas size a little larger than the square

# Define rectangle attributes: 100x100 size, red fill, positioned at (10,10)
rect_attrs = {
    "x": "10",
    "y": "10",
    "width": "100",
    "height": "100",
    "fill": "red"
}

# Create the <rect> element and attach it to the SVG root
rect_element = svg.create_element("rect", rect_attrs)
svg.append_child(rect_element)
```

**Erklärung:**  
* Die `x`‑ und `y`‑Koordinaten des Rechtecks geben ihm einen Rand von 10 Pixel, sodass es nicht bündig am Rand sitzt.  
* Die Verwendung eines Dictionaries für Attribute macht den Code lesbar und spiegelt wider, wie Sie **save SVG file**‑Attribute in jedem XML‑basierten Format setzen würden.  
* Wenn Sie jemals **how to generate SVG**‑Formen außer Rechtecken benötigen, ändern Sie einfach das Tag zu `"circle"` oder `"path"` und passen das Attribut‑Dictionary entsprechend an.

## Schritt 3: SVG speichern – Schließlich **Save SVG File** auf die Festplatte

Wir haben das Dokument im Speicher aufgebaut; jetzt schreiben wir es aus. Das ist der Moment, in dem das abstrakte **create SVG document** zu einer greifbaren Datei wird, die Sie im Browser öffnen können.

```python
# ----------------------------------------------------------------------
# Step 3: Persist the SVG to the filesystem
# ----------------------------------------------------------------------
output_path = "output/square.svg"
svg.save(output_path)

print(f"✅ SVG saved! Open {output_path} in any browser to see the red square.")
```

**Was Sie sehen werden:** Das Öffnen von `output/square.svg` in Chrome, Firefox oder einem beliebigen SVG‑fähigen Viewer zeigt ein einfaches rotes Quadrat mit einem dünnen weißen Rand (der Hintergrund der SVG‑Leinwand). Das beweist, dass wir erfolgreich **exported SVG from code** haben.

## Vollständiges Skript – Ein‑Datei‑Lösung

Unten finden Sie das gesamte Skript, bereit zum Kopieren und Einfügen in `create_svg.py`. Das Ausführen von `python create_svg.py` erzeugt die oben beschriebene Datei.

```python
import pathlib
import xml.etree.ElementTree as ET

class SVGDocument:
    """Simple wrapper to generate an SVG document using ElementTree."""
    SVG_NS = "http://www.w3.org/2000/svg"
    def __init__(self, width: int = 200, height: int = 200):
        ET.register_namespace("", self.SVG_NS)
        self.root = ET.Element(
            "svg",
            attrib={
                "xmlns": self.SVG_NS,
                "width": str(width),
                "height": str(height),
                "version": "1.1"
            }
        )
    def create_element(self, tag: str, attributes: dict) -> ET.Element:
        return ET.Element(tag, attrib=attributes)
    def append_child(self, element: ET.Element):
        self.root.append(element)
    def save(self, file_path: str):
        path = pathlib.Path(file_path)
        path.parent.mkdir(parents=True, exist_ok=True)
        tree = ET.ElementTree(self.root)
        tree.write(str(path), encoding="utf-8", xml_declaration=True)

# -------------------- Build the SVG --------------------
svg = SVGDocument(width=120, height=120)

rect_attrs = {
    "x": "10",
    "y": "10",
    "width": "100",
    "height": "100",
    "fill": "red"
}
svg.append_child(svg.create_element("rect", rect_attrs))

# -------------------- Save the file --------------------
output_path = "output/square.svg"
svg.save(output_path)

print(f"✅ SVG saved! Open {output_path} in any browser to see the red square.")
```

### Erwartete Ausgabe

Das Ausführen des Skripts gibt aus:

```
✅ SVG saved! Open output/square.svg in any browser to see the red square.
```

Und das erzeugte `square.svg` sieht so aus (vereinfacht dargestellt):

```xml
<?xml version='1.0' encoding='utf-8'?>
<svg xmlns="http://www.w3.org/2000/svg" width="120" height="120" version="1.1">
  <rect x="10" y="10" width="100" height="100" fill="red" />
</svg>
```

Das Öffnen der Datei rendert ein klares rotes Quadrat – genau das, was wir mit **create basic SVG image** erreichen wollten.

## Beispiel erweitern – Häufig gestellte Fragen beantwortet

### Wie kann ich Text oder andere Formen hinzufügen?

Rufen Sie einfach `svg.create_element("text", {...})` oder `svg.create_element("circle", {...})` auf und hängen Sie sie genauso an wie das Rechteck. Die gleiche **how to generate SVG**‑Logik gilt.

### Was ist, wenn ich **export SVG from code** mit transparentem Hintergrund benötige?

Entfernen Sie jedes `fill`‑Attribut vom Wurzel‑`<svg>`‑Element oder setzen Sie `fill="none"` bei Formen, die transparent sein sollen. Das XML bleibt gültig; Browser rendern die Transparenz automatisch.

### Kann ich **save SVG file** mit pretty‑printed Formatierung speichern?

`ElementTree` schreibt standardmäßig kompaktes XML. Für eine menschenlesbare Version können Sie `xml.dom.minidom` zum Neuformatieren verwenden:

```python
import xml.dom.minidom as minidom

def pretty_save(svg_doc, path):
    rough_string = ET.tostring(svg_doc.root, 'utf-8')
    reparsed = minidom.parseString(rough_string)
    with open(path, 'w', encoding='utf-8') as f:
        f.write(reparsed.toprettyxml(indent="  "))
```

Ersetzen Sie `svg.save(output_path)` durch `pretty_save(svg, output_path)`.

### Wie sieht es mit der Performance bei großen SVGs aus?

Wenn Sie Tausende von Elementen erzeugen, sollten Sie zuerst eine Liste von `ET.Element`‑Objekten bauen und dann die Wurzel in einem Schritt erweitern. Das reduziert die Anzahl der Baum‑Mutationen und beschleunigt die **save SVG file**‑Operation.

## Pro‑Tipps & Fallstricke

* **Pro‑Tipp:** Verwenden Sie immer absolute Pfade (oder `pathlib.Path`), wenn Sie **saving SVG file**; relative Pfade können brechen, wenn Ihr Skript aus einem anderen Arbeitsverzeichnis ausgeführt wird.  
* **Achten Sie auf:** Das Vergessen, den SVG‑Namensraum zu registrieren. Ohne `ET.register_namespace("", SVGDocument.SVG_NS)` enthält die Ausgabe ein redundantes `ns0`‑Präfix, das manche Browser missverstehen.  
* **Typischer Fehler:** Mischen von Ganzzahl‑ und String‑Typen in Attributwerten. XML erwartet Strings, daher casten wir alles mit `str()` – die Hilfsklasse übernimmt das für Sie, aber wenn Sie sie umgehen, kann ein `TypeError` auftreten.  

## Fazit

Wir haben gerade ein vollständiges End‑to‑End‑Beispiel durchgearbeitet, das zeigt, wie man **create SVG document**, **save SVG file** und beantwortet

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden demonstrierten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}