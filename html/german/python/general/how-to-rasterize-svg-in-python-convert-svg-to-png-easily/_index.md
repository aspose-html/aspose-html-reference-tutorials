---
category: general
date: 2026-10-28
description: Lernen Sie, wie Sie SVG in Python rasterisieren und SVG mit einem einfachen
  Skript mithilfe von CairoSVG in PNG konvertieren. Speichern Sie SVG in Sekunden
  als PNG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to rasterize svg
- convert svg to png
- save svg as png
- svg to png python
- export svg as png
language: de
lastmod: 2026-10-28
og_description: 'Wie man SVG in Python rasterisiert: Dieser Leitfaden zeigt, wie man
  SVG mit CairoSVG in PNG konvertiert, inklusive Installation, Code und Fehlersuche.'
og_image_alt: Screenshot of Python code that rasterizes SVG to PNG
og_title: Wie man SVG in Python rasterisiert – kurzer SVG‑zu‑PNG‑Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to rasterize SVG in Python and convert SVG to PNG with a
    simple script using CairoSVG. Save SVG as PNG in seconds.
  headline: How to rasterize SVG in Python – convert SVG to PNG easily
  type: TechArticle
- description: Learn how to rasterize SVG in Python and convert SVG to PNG with a
    simple script using CairoSVG. Save SVG as PNG in seconds.
  name: How to rasterize SVG in Python – convert SVG to PNG easily
  steps:
  - name: Why CairoSVG?
    text: '- **Pure Python**: No need for external command‑line tools once the package
      is installed. - **SVG‑compliant**: Supports most SVG 1.1 features, including
      gradients, masks, and text. - **Flexible output**: Besides PNG, you can export
      to PDF, PS, or even raw bytes.'
  - name: Step‑by‑step breakdown
    text: 1. **Install the library** – `pip install cairosvg` pulls in the compiled
      Cairo bindings. 2. **Import the module** – `import cairosvg` gives you access
      to the `svg2png` helper. 3. **Call `svg2png`** – Pass the SVG file path (or
      a URL) and the destination PNG path. Optional `output_width`, `output_he
  - name: Edge cases you might encounter
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | **Large SVG (megapixel dimensions)** | Increase `dpi` or set explicit `output_width`/`output_height`
      to avoid memory spikes. | | **Missing fonts** | Install the required fonts on
      the system or em'
  type: HowTo
tags:
- svg
- python
- image processing
- cairosvg
title: Wie man SVG in Python rasterisiert – SVG einfach in PNG konvertieren
url: /de/python/general/how-to-rasterize-svg-in-python-convert-svg-to-png-easily/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man SVG in Python rasterisiert – SVG einfach in PNG konvertieren

Wenn Sie **how to rasterize svg** für eine Web‑App, einen Bericht oder einen automatisierten Build benötigen, bietet Ihnen dieser Leitfaden eine sofort einsatzbereite Lösung. Sie sehen, wie Sie **convert svg to png** mit nur wenigen Zeilen Python durchführen können, und das Ergebnis ist ein scharfes PNG, das Sie sofort speichern oder bereitstellen können.

Das Tutorial behandelt alles von der Installation der erforderlichen Bibliothek bis hin zum Umgang mit Sonderfällen wie großen Dateien oder benutzerdefinierten DPI‑Einstellungen. Am Ende können Sie **save svg as png**, **export svg as png** und den Prozess in jeden Python‑Workflow integrieren.

## Was Sie benötigen

- Python 3.8+ (der Code funktioniert mit 3.9, 3.10 und neueren Versionen)
- `pip` zum Installieren von Paketen
- Eine lokale SVG‑Datei (z. B. `logo.svg`), die Sie rasterisieren möchten
- Optional: virtuelle Umgebung für sauberes Abhängigkeitsmanagement

> **Profi‑Tipp:** Die Verwendung einer virtuellen Umgebung (`python -m venv .venv`) isoliert die CairoSVG‑Abhängigkeit von Ihren globalen Python‑Paketen.

## Wie man SVG in Python rasterisiert

Der einfachste Weg, **how to rasterize svg** zu erledigen, ist die **CairoSVG**‑Bibliothek. CairoSVG liest das SVG‑XML, rendert es mit der Cairo‑Grafikengine und schreibt das Rasterbild als PNG, PDF oder andere Bitmap‑Formate.

```bash
# Install CairoSVG and its binary dependencies
pip install cairosvg
```

```python
# rasterize_svg.py
import sys
from pathlib import Path
import cairosvg

def rasterize_svg(input_path: str, output_path: str,
                  width: int | None = None,
                  height: int | None = None,
                  dpi: int = 96) -> None:
    """
    Convert an SVG file to a PNG image.

    Parameters
    ----------
    input_path : str
        Path to the source SVG file.
    output_path : str
        Destination path for the PNG file.
    width : int | None
        Desired output width in pixels (maintains aspect ratio if height is None).
    height : int | None
        Desired output height in pixels (maintains aspect ratio if width is None).
    dpi : int
        Dots per inch for the rasterization. Higher DPI yields larger files but more detail.
    """
    try:
        # CairoSVG can read from a file path directly
        cairosvg.svg2png(url=Path(input_path).as_uri(),
                         write_to=output_path,
                         output_width=width,
                         output_height=height,
                         dpi=dpi)
        print(f"✅ Successfully saved PNG to {output_path}")
    except Exception as e:
        print(f"❌ Failed to rasterize {input_path}: {e}", file=sys.stderr)
        raise

if __name__ == "__main__":
    # Example usage:
    # python rasterize_svg.py ./assets/logo.svg ./output/logo.png 300 300
    if len(sys.argv) < 3:
        print("Usage: python rasterize_svg.py <input_svg> <output_png> [width] [height] [dpi]")
        sys.exit(1)

    input_svg = sys.argv[1]
    output_png = sys.argv[2]
    w = int(sys.argv[3]) if len(sys.argv) > 3 else None
    h = int(sys.argv[4]) if len(sys.argv) > 4 else None
    d = int(sys.argv[5]) if len(sys.argv) > 5 else 96

    rasterize_svg(input_svg, output_png, width=w, height=h, dpi=d)
```

### Warum CairoSVG?

- **Pure Python**: Keine externen Befehlszeilentools nötig, sobald das Paket installiert ist.
- **SVG‑konform**: Unterstützt die meisten SVG 1.1‑Features, einschließlich Verläufen, Masken und Text.
- **Flexibler Output**: Neben PNG können Sie auch nach PDF, PS oder sogar rohen Bytes exportieren.

### Schritt‑für‑Schritt‑Aufschlüsselung

1. **Bibliothek installieren** – `pip install cairosvg` zieht die kompilierten Cairo‑Bindings nach.
2. **Modul importieren** – `import cairosvg` gibt Ihnen Zugriff auf die Hilfsfunktion `svg2png`.
3. **`svg2png` aufrufen** – Übergeben Sie den Pfad zur SVG‑Datei (oder eine URL) und den Ziel‑PNG‑Pfad. Optionale Parameter `output_width`, `output_height` und `dpi` ermöglichen die Kontrolle von Größe und Auflösung.
4. **Fehler behandeln** – Der `try/except`‑Block gibt eine klare Meldung aus, wenn das SVG fehlerhaft ist oder das Ausgabeverzeichnis nicht beschreibbar ist.

## SVG mit CairoSVG in PNG konvertieren

Wenn Sie nur einen Einzeiler für eine schnelle Konvertierung benötigen, erledigt das folgende Snippet die Aufgabe ohne Wrapper‑Funktion:

```python
import cairosvg

cairosvg.svg2png(url="logo.svg", write_to="logo.png")
```

Dies ist die knappste Darstellung von **convert svg to png**. Es liest `logo.svg` aus dem aktuellen Verzeichnis und schreibt `logo.png` daneben.

## SVG als PNG speichern – Ergebnis prüfen

Nach dem Ausführen des Skripts sollten Sie eine PNG‑Datei am Zielort sehen. Öffnen Sie sie mit einem beliebigen Bildbetrachter, um die Korrektheit zu bestätigen:

```bash
# Linux/macOS
xdg-open ./output/logo.png   # or open on macOS
# Windows
start ./output/logo.png
```

Wenn das PNG unscharf wirkt, erhöhen Sie das Argument `dpi` (z. B. `dpi=300`), um ein hochauflösendes Raster zu erzeugen.

## SVG als PNG in verschiedenen Formaten exportieren

CairoSVG kann auch **PDF**, **PostScript** oder rohe **PNG‑Bytes** ausgeben. Unten finden Sie ein Beispiel, das in ein `BytesIO`‑Objekt exportiert, wenn Sie das Bild im Speicher benötigen (z. B. für eine Flask‑Antwort):

```python
import io
import cairosvg

svg_path = "logo.svg"
png_bytes = io.BytesIO()
cairosvg.svg2png(url=Path(svg_path).as_uri(), write_to=png_bytes)
png_bytes.seek(0)  # Ready for sending over HTTP
```

### Sonderfälle, denen Sie begegnen könnten

| Situation                               | Empfohlene Vorgehensweise |
|----------------------------------------|---------------------------|
| **Großes SVG (Megapixel‑Abmessungen)**   | Erhöhen Sie `dpi` oder setzen Sie explizite `output_width`/`output_height`, um Speicherspitzen zu vermeiden. |
| **Fehlende Schriftarten**               | Installieren Sie die benötigten Schriftarten im System oder betten Sie sie in das SVG mittels `<style>`‑Tags ein. |
| **Transparenz‑Probleme**                | PNG bewahrt Alpha‑Kanäle standardmäßig; wenn Sie einen festen Hintergrund benötigen, übergeben Sie `background_color="#FFFFFF"` an `svg2png`. |
| **Batch‑Verarbeitung**                  | Durchlaufen Sie ein Verzeichnis mit SVGs und rufen Sie `rasterize_svg` für jede Datei auf. |

## Vollständiges funktionierendes Beispiel

Unten steht ein minimales, eigenständiges Skript, das Sie in eine Datei namens `svg_to_png.py` kopieren und sofort ausführen können.

```python
# svg_to_png.py
import cairosvg
from pathlib import Path

def main():
    src = Path("example.svg")
    dst = Path("example.png")
    if not src.is_file():
        raise FileNotFoundError(f"Source SVG not found: {src}")

    # Convert with default DPI (96) and keep original dimensions
    cairosvg.svg2png(url=src.as_uri(), write_to=dst)
    print(f"✅ {src.name} → {dst.name} created successfully.")

if __name__ == "__main__":
    main()
```

Running `python svg_to_png


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [How to Rasterize SVG in Python – Complete Guide](/html/english/python/general/how-to-rasterize-svg-in-python-complete-guide/)
- [Convert SVG to PNG in Python – High‑Resolution Export Guide](/html/english/python/general/convert-svg-to-png-in-python-high-resolution-export-guide/)
- [Create SVG Document in Python – Convert SVG to PNG Guide](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}