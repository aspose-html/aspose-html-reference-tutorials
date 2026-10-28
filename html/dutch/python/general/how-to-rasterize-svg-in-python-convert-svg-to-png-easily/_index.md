---
category: general
date: 2026-10-28
description: Leer hoe je SVG in Python kunt rasteren en SVG naar PNG kunt converteren
  met een eenvoudig script met behulp van CairoSVG. Sla SVG op als PNG in enkele seconden.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to rasterize svg
- convert svg to png
- save svg as png
- svg to png python
- export svg as png
language: nl
lastmod: 2026-10-28
og_description: 'Hoe SVG te rasteren in Python: deze gids laat zien hoe je SVG naar
  PNG converteert met CairoSVG, inclusief installatie, code en probleemoplossing.'
og_image_alt: Screenshot of Python code that rasterizes SVG to PNG
og_title: Hoe SVG te rasteren in Python – snelle gids voor SVG naar PNG
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
title: Hoe SVG te rasteren in Python – converteer SVG eenvoudig naar PNG
url: /nl/python/general/how-to-rasterize-svg-in-python-convert-svg-to-png-easily/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe SVG rasteren in Python – converteer SVG eenvoudig naar PNG

Als je **how to rasterize svg** nodig hebt voor een web‑app, een rapport of een geautomatiseerde build, biedt deze gids een kant‑en‑klare oplossing. Je ziet hoe je **convert svg to png** kunt uitvoeren met slechts een paar regels Python, en het resultaat is een scherpe PNG die je direct kunt opslaan of serveren.

De tutorial behandelt alles, van het installeren van de benodigde bibliotheek tot het afhandelen van randgevallen zoals grote bestanden of aangepaste DPI‑instellingen. Aan het einde kun je **save svg as png**, **export svg as png** uitvoeren en het proces integreren in elke Python‑workflow.

## Wat je nodig hebt

- Python 3.8+ (de code werkt op 3.9, 3.10 en nieuwer)
- `pip` om pakketten te installeren
- Een lokaal SVG‑bestand (bijv. `logo.svg`) dat je wilt rasteren
- Optioneel: virtuele omgeving voor schoon afhankelijkheidsbeheer

> **Pro tip:** Het gebruik van een virtuele omgeving (`python -m venv .venv`) isoleert de CairoSVG‑afhankelijkheid van je globale Python‑pakketten.

## Hoe SVG rasteren in Python

De meest eenvoudige manier om **how to rasterize svg** uit te voeren is met de **CairoSVG**‑bibliotheek. CairoSVG leest de SVG‑XML, rendert deze met de Cairo‑grafische engine en schrijft de rasterafbeelding naar PNG, PDF of andere bitmap‑formaten.

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

### Why CairoSVG?

- **Pure Python**: Geen externe command‑line tools nodig zodra het pakket geïnstalleerd is.
- **SVG‑compliant**: Ondersteunt de meeste SVG 1.1‑functies, inclusief verlopen, maskers en tekst.
- **Flexible output**: Naast PNG kun je exporteren naar PDF, PS of zelfs ruwe bytes.

### Stapsgewijze uitleg

1. **Installeer de bibliotheek** – `pip install cairosvg` haalt de gecompileerde Cairo‑bindings op.
2. **Importeer de module** – `import cairosvg` geeft je toegang tot de `svg2png`‑helper.
3. **Roep `svg2png` aan** – Geef het SVG‑bestandspad (of een URL) en het doel‑PNG‑pad door. Optionele `output_width`, `output_height` en `dpi` laten je grootte en resolutie bepalen.
4. **Afhandelen van fouten** – Het `try/except`‑blok print een duidelijke melding als de SVG onjuist is of de doelmap niet beschrijfbaar is.

## Converteer SVG naar PNG met CairoSVG

Als je alleen een één‑regel oplossing nodig hebt voor snelle conversie, doet de volgende code het zonder de wrapper‑functie:

```python
import cairosvg

cairosvg.svg2png(url="logo.svg", write_to="logo.png")
```

Dit is de meest beknopte illustratie van **convert svg to png**. Het leest `logo.svg` uit de huidige map en schrijft `logo.png` ernaast.

## SVG opslaan als PNG – controleer het resultaat

Na het uitvoeren van het script zou je een PNG‑bestand op het bestemmingspad moeten zien. Open het met een willekeurige afbeeldingsviewer om te bevestigen:

```bash
# Linux/macOS
xdg-open ./output/logo.png   # or open on macOS
# Windows
start ./output/logo.png
```

Als de PNG onscherp lijkt, verhoog dan de `dpi`‑parameter (bijv. `dpi=300`) om een raster met hogere resolutie te genereren.

## Exporteer SVG als PNG in verschillende formaten

CairoSVG kan ook **PDF**, **PostScript** of ruwe **PNG‑bytes** produceren. Hieronder staat een voorbeeld van exporteren naar een `BytesIO`‑object wanneer je de afbeelding in het geheugen nodig hebt (bijv. voor een Flask‑respons):

```python
import io
import cairosvg

svg_path = "logo.svg"
png_bytes = io.BytesIO()
cairosvg.svg2png(url=Path(svg_path).as_uri(), write_to=png_bytes)
png_bytes.seek(0)  # Ready for sending over HTTP
```

### Randgevallen die je kunt tegenkomen

| Situatie                               | Aanbevolen aanpak |
|----------------------------------------|-------------------|
| **Large SVG (megapixel dimensions)**   | Verhoog `dpi` of stel expliciete `output_width`/`output_height` in om geheugenpieken te voorkomen. |
| **Missing fonts**                      | Installeer de benodigde lettertypen op het systeem of embed ze in de SVG met `<style>`‑tags. |
| **Transparency issues**                | PNG behoudt standaard alfa; als je een effen achtergrond nodig hebt, geef `background_color="#FFFFFF"` door aan `svg2png`. |
| **Batch processing**                   | Loop door een map met SVG‑bestanden en roep `rasterize_svg` aan voor elk bestand. |

## Volledig werkend voorbeeld

Hieronder staat een minimaal, zelfstandig script dat je kunt kopiëren en plakken in een bestand genaamd `svg_to_png.py` en direct kunt uitvoeren.

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


## Wat je hierna zou moeten leren

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Rasterize SVG in Python – Complete Guide](/html/english/python/general/how-to-rasterize-svg-in-python-complete-guide/)
- [Convert SVG to PNG in Python – High‑Resolution Export Guide](/html/english/python/general/convert-svg-to-png-in-python-high-resolution-export-guide/)
- [Create SVG Document in Python – Convert SVG to PNG Guide](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}