---
category: general
date: 2026-07-31
description: Lernen Sie, wie man ein SVG‑Dokument erstellt, einen Kreis hinzufügt
  und die SVG‑Datei schnell speichert. Exportieren Sie die Grafik als SVG mit wenigen
  Zeilen Python‑Code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg document
- save svg file
- export graphic as svg
- add circle to svg
language: de
lastmod: 2026-07-31
og_description: Erstelle ein SVG‑Dokument, füge einen Kreis hinzu und speichere die
  SVG‑Datei in Sekundenschnelle. Dieser Leitfaden zeigt, wie du eine Grafik als SVG
  exportierst, mit klarem, ausführbarem Code.
og_image_alt: Screenshot of a red circle inside an SVG file named circle.svg
og_title: SVG-Dokument erstellen – Kreis hinzufügen und als SVG speichern
schemas:
- author: Aspose
  dateModified: '2026-07-31'
  description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  headline: Create SVG Document – Add a Circle and Save as SVG
  type: TechArticle
- description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  name: Create SVG Document – Add a Circle and Save as SVG
  steps:
  - name: Pro tip
    text: If you plan to generate many files in a loop, give each `Drawing` a unique
      name or use `io.BytesIO` to keep everything in memory until you’re ready to
      write.
  - name: Edge case – Transparent background
    text: 'If you need a transparent background (the default for SVG), you can skip
      setting a `fill` on the root. For a white background, add:'
  - name: 'Bonus: Export graphic as SVG programmatically'
    text: 'If you need the SVG content as a string—for example, to embed it in an
      HTML email—you can call `dwg.tostring()` instead of `save()`:'
  type: HowTo
- questions:
  - answer: Swap `dwg.circle` for `dwg.rect`, `dwg.ellipse`, or even a custom `<path>`
      string. The API is consistent across shapes.
    question: What if I want a different shape?
  - answer: Absolutely. The file you just created can be referenced with `<img src="circle.svg"
      alt="Red circle">` or inlined with `<svg>` tags.
    question: Can I embed the SVG directly in HTML?
  - answer: You could, but libraries like `svgwrite` handle namespace quirks and make
      the code far more maintainable—especially when you start adding gradients or
      animations.
    question: Why not write raw XML?
  type: FAQPage
tags:
- svg
- python
- vector-graphics
- programming-tutorial
title: SVG-Dokument erstellen – Kreis hinzufügen und als SVG speichern
url: /de/python/general/create-svg-document-add-a-circle-and-save-as-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SVG-Dokument erstellen – Kreis hinzufügen und als SVG speichern

Haben Sie jemals **ein SVG-Dokument** aus Code erstellen müssen, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht allein; viele Entwickler stoßen an diese Grenze, wenn sie das erste Mal mit Vektorgrafiken experimentieren. In diesem Tutorial gehen wir ein kleines, eigenständiges Beispiel durch, das zeigt, wie man **einen Kreis zu SVG hinzufügt**, dann **die SVG‑Datei speichert**, sodass Sie **die Grafik als SVG exportieren** können, um sie im Web oder in Design‑Tools zu verwenden.

Wir halten es leichtgewichtig: nur ein paar Zeilen Python, eine beliebte SVG‑Hilfsbibliothek und ein wenig Erklärung. Am Ende haben Sie ein einsatzbereites `circle.svg` in Ihrem Ordner und verstehen, warum jeder Schritt wichtig ist – ohne vage „siehe Dokumentation“-Abkürzungen.

## Was Sie benötigen

- Python 3.8+ (jede aktuelle Version funktioniert)
- Das `svgwrite`‑Paket – installieren Sie es mit `pip install svgwrite`
- Ein Texteditor oder eine IDE (VS Code, PyCharm oder sogar Notepad reicht aus)
- Schreibberechtigung für das Verzeichnis, in dem Sie die Datei speichern möchten

Das war's. Keine schweren Abhängigkeiten, keine externen Dienste.

## Schritt 1: SVG-Dokument einrichten

Ein SVG‑Dokument zu erstellen ist so einfach wie das Instanziieren eines `Drawing`‑Objekts aus `svgwrite`. Betrachten Sie dieses Objekt als die leere Leinwand, auf der jede Form lebt.

```python
import svgwrite

# Step 1: Create a new SVG document (canvas) 800×800 pixels
dwg = svgwrite.Drawing(filename="circle.svg", size=("200px", "200px"))
```

> **Warum das wichtig ist:** Die `Drawing`‑Klasse übernimmt den gesamten XML‑Boilerplate für Sie – Namespaces, Header und das Wurzelelement `<svg>`. Indem wir gleich zu Beginn einen Dateinamen angeben, wissen wir bereits, wo die Datei landen wird, was den späteren **save svg file**‑Schritt trivial macht.

### Profi‑Tipp
Wenn Sie planen, viele Dateien in einer Schleife zu erzeugen, geben Sie jedem `Drawing` einen eindeutigen Namen oder verwenden Sie `io.BytesIO`, um alles im Speicher zu behalten, bis Sie bereit zum Schreiben sind.

## Schritt 2: Einen Kreis zum SVG hinzufügen

Jetzt, wo das Dokument existiert, lassen Sie uns **einen Kreis zu SVG hinzufügen**. Die Methode `add()` akzeptiert jedes Form‑Objekt; ein `Circle` ist perfekt für einen einfachen roten Punkt in der Mitte.

```python
# Step 2: Add a red circle element to the SVG root
center = (100, 100)          # x, y coordinates (half of 200px canvas)
radius = 80                  # radius in pixels
circle = dwg.circle(center=center, r=radius, fill='red')
dwg.add(circle)
```

> **Warum wir die Variablen `center` und `radius` verwenden:** Zahlen hart zu codieren macht den Code schwerer lesbar und wartbar. Durch Benennen der Werte verdeutlichen wir die Absicht – dieser Kreis sitzt genau in der Mitte einer 200 × 200‑Leinwand und ist groß genug, um auffallen.

### Sonderfall – Transparenter Hintergrund
Wenn Sie einen transparenten Hintergrund benötigen (der Standard für SVG), können Sie das Setzen eines `fill` auf dem Wurzelelement überspringen. Für einen weißen Hintergrund fügen Sie hinzu:

```python
dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))
```

Platzieren Sie dies vor dem Hinzufügen des Kreises, damit das Rechteck darunter liegt.

## Schritt 3: SVG‑Datei speichern

Mit der Form an Ort und Stelle ist der letzte Schritt, **die SVG‑Datei zu speichern**. Die Methode `save()` schreibt das XML auf die Festplatte, und da wir dem `Drawing` bereits einen Dateinamen gegeben haben, erledigt ein einziger Aufruf die Arbeit.

```python
# Step 3: Save the SVG document to a file
dwg.save()
print("✅ circle.svg has been created in the current directory.")
```

> **Was passiert im Hintergrund?** `svgwrite` serialisiert den Elementbaum zu einem String, fügt die XML‑Deklaration hinzu und schreibt ihn mit UTF‑8‑Kodierung. Wenn das Zielverzeichnis nicht existiert, wirft Python einen `FileNotFoundError`; stellen Sie sicher, dass der Pfad gültig ist oder erstellen Sie ihn mit `os.makedirs()`.

### Bonus: Grafik programmgesteuert als SVG exportieren
Wenn Sie den SVG‑Inhalt als String benötigen – zum Beispiel, um ihn in eine HTML‑E‑Mail einzubetten – können Sie `dwg.tostring()` anstelle von `save()` aufrufen:

```python
svg_content = dwg.tostring()
# Now you can send svg_content over a network, store it in a DB, etc.
```

## Vollständiges funktionierendes Beispiel

Alles zusammengefügt, hier ein komplettes, sofort ausführbares Skript:

```python
import svgwrite
import os

def create_svg_with_circle(output_path: str):
    """
    Creates an SVG file containing a single red circle.
    Parameters
    ----------
    output_path: str
        Full path where the SVG file will be saved.
    """
    # Ensure the directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Initialise the SVG document (800×800 canvas)
    dwg = svgwrite.Drawing(filename=output_path, size=("200px", "200px"))

    # Optional: add a white background rectangle
    dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))

    # Add a red circle in the centre
    center = (100, 100)
    radius = 80
    circle = dwg.circle(center=center, r=radius, fill='red')
    dwg.add(circle)

    # Save the file – this is the key step to **save svg file**
    dwg.save()
    print(f"✅ SVG saved to {output_path}")

if __name__ == "__main__":
    # Change this path to wherever you want the file
    output_file = os.path.join(os.getcwd(), "circle.svg")
    create_svg_with_circle(output_file)
```

**Erwartete Ausgabe:** Nach dem Ausführen des Skripts sehen Sie eine `circle.svg`‑Datei im selben Ordner. Öffnen Sie sie in einem Browser oder einem Vektor-Editor, zeigt sie einen roten Kreis, zentriert auf einem weißen Quadrat – genau das, was wir programmiert haben.

## Häufige Fragen & Stolperfallen

- **Was, wenn ich eine andere Form möchte?** Ersetzen Sie `dwg.circle` durch `dwg.rect`, `dwg.ellipse` oder sogar einen benutzerdefinierten `<path>`‑String. Die API ist für alle Formen konsistent.
- **Kann ich das SVG direkt in HTML einbetten?** Absolut. Die Datei, die Sie gerade erstellt haben, kann mit `<img src="circle.svg" alt="Red circle">` referenziert oder mit `<svg>`‑Tags inline eingebettet werden.
- **Warum nicht rohes XML schreiben?** Sie könnten, aber Bibliotheken wie `svgwrite` kümmern sich um Namespace‑Eigenheiten und machen den Code viel wartbarer – besonders wenn Sie beginnen, Verläufe oder Animationen hinzuzufügen.

## Fazit

Sie wissen jetzt, wie man **ein SVG‑Dokument erstellt**, **einen Kreis zu SVG hinzufügt** und **die SVG‑Datei speichert**, sodass Sie **die Grafik als SVG exportieren** können, mit nur wenigen Python‑Zeilen. Das Muster skaliert: Ersetzen Sie den Kreis durch jede Vektorform, iterieren Sie über Daten, um Diagramme zu erzeugen, oder verarbeiten Sie Assets stapelweise für ein Design‑System.

Nächste Schritte? Versuchen Sie, Textbeschriftungen hinzuzufügen, mit Verläufen zu experimentieren oder eine ganze Galerie von Icons in einem einzigen Skript zu erzeugen. Wenn Sie neugierig auf weiterführende Funktionen sind, schauen Sie sich die `svgwrite`‑Dokumentation zu Gruppen (`<g>`), Transformationen und Animationsunterstützung an.

Viel Spaß beim Coden, und mögen Ihre Vektoren immer scharf bleiben!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [SVG-Dokument in Aspose.HTML für Java speichern](/html/english/java/saving-html-documents/save-svg-document/)
- [SVG-Dokumente in Aspose.HTML für Java erstellen und verwalten](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg zu png java – SVG in Bild konvertieren mit Aspose.HTML für Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}