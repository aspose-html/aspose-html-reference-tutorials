---
category: general
date: 2026-10-25
description: sla SVG snel op als PNG met Python. Leer hoe je SVG naar PNG converteert,
  exporteer SVG naar PNG en krijg kant‑klaar code voor SVG naar PNG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save svg as png
- convert svg to png
- how to convert svg
- export svg to png
- svg to png code
language: nl
lastmod: 2026-10-25
og_description: sla SVG op als PNG met Python. Deze tutorial laat zien hoe je SVG
  naar PNG kunt converteren met duidelijke code, opties en tips voor probleemoplossing.
og_image_alt: Diagram illustrating saving an SVG file as a PNG image with Python
og_title: SVG opslaan als PNG in Python – volledige gids
schemas:
- author: Aspose
  dateModified: '2026-10-25'
  description: save SVG as PNG quickly with Python. Learn to convert SVG to PNG, export
    SVG to PNG, and get ready‑to‑use svg to png code.
  headline: How to save SVG as PNG in Python – step‑by‑step guide
  type: TechArticle
- description: save SVG as PNG quickly with Python. Learn to convert SVG to PNG, export
    SVG to PNG, and get ready‑to‑use svg to png code.
  name: How to save SVG as PNG in Python – step‑by‑step guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Reason | |------------|--------| | Python 3.8+ | Modern
      syntax and type hints. | | `aspose.svg` package (or any library that provides
      `SVGDocument` and `PngSaveOptions`) | Supplies the `SVGDocument` class used
      in the example. | | An SVG file you own or have permission to use | The so'
  - name: Load the SVG document
    text: '```python from aspose.svg import SVGDocument'
  - name: Convert SVG to PNG – create save options
    text: '```python from aspose.svg import PngSaveOptions'
  - name: Export SVG to PNG
    text: '```python # Destination file for the PNG image png_path = "YOUR_DIRECTORY/vector.png"
      svg_doc.save(png_path, png_options) ```'
  - name: Verify the output (optional but recommended)
    text: '```python from PIL import Image'
  type: HowTo
tags:
- SVG
- PNG
- Python
title: Hoe SVG opslaan als PNG in Python – stap‑voor‑stap gids
url: /nl/python/general/how-to-save-svg-as-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe SVG op te slaan als PNG in Python – stapsgewijze gids

Als je snel **SVG als PNG wilt opslaan**, biedt deze gids een complete, uitvoerbare oplossing. Je ziet hoe je **SVG naar PNG kunt converteren**, optionele exportparameters kunt instellen en het script kunt uitvoeren op elk platform dat Python ondersteunt.  

De tutorial behandelt alles, van het installeren van de vereiste bibliotheek tot het verifiëren van de gegenereerde afbeelding, zodat je de code kunt kopiëren‑plakken en meteen resultaten krijgt. Er is geen externe documentatie nodig—volg gewoon de onderstaande stappen.

## Wat je zult leren

* De exacte **svg to png code** die je nodig hebt voor een één‑regelige conversie.  
* Hoe je **SVG naar PNG kunt exporteren** met aangepaste DPI of achtergrondkleur.  
* Veelvoorkomende valkuilen bij het converteren van complexe SVG's en hoe je ze kunt vermijden.  
* Hoe je de conversie kunt integreren in grotere Python‑projecten.

### Vereisten

| Vereiste | Reden |
|------------|--------|
| Python 3.8+ | Moderne syntaxis en type‑hints. |
| `aspose.svg` package (or any library that provides `SVGDocument` and `PngSaveOptions`) | Levert de `SVGDocument`‑klasse die in het voorbeeld wordt gebruikt. |
| An SVG file you own or have permission to use | De bronvectorafbeelding. |

Installeer de bibliotheek met pip voordat je begint:

```bash
pip install aspose.svg
```

> **Pro tip:** Als je een lichtere afhankelijkheid verkiest, biedt `cairosvg` ook `svg2png`, maar de hier getoonde API komt overeen met het oorspronkelijke fragment en werkt voor zowel eenvoudige als complexe SVG's.

## Hoe SVG op te slaan als PNG met Python

### Stap 1: Laad het SVG‑document

```python
from aspose.svg import SVGDocument

# Replace the path with your actual SVG file location
svg_path = "YOUR_DIRECTORY/vector.svg"
svg_doc = SVGDocument(svg_path)
```

*Waarom deze stap belangrijk is* – Het laden van het bestand creëert een in‑memory representatie die de bibliotheek kan manipuleren. Zonder een juiste `SVGDocument`‑instantie zullen latere export‑aanroepen mislukken.

### Stap 2: Converteer SVG naar PNG – maak opslaan‑opties

```python
from aspose.svg import PngSaveOptions

# Default options work for most cases; you can customize them later
png_options = PngSaveOptions()
```

`PngSaveOptions` stelt je in staat de uitvoergrootte, DPI, achtergrondkleur en meer te regelen. De standaardconfiguratie behoudt de oorspronkelijke SVG‑afmetingen en produceert een verliesloze PNG.

### Stap 3: Exporteer SVG naar PNG

```python
# Destination file for the PNG image
png_path = "YOUR_DIRECTORY/vector.png"
svg_doc.save(png_path, png_options)
```

Wanneer `save` voltooid is, zal `vector.png` een gerasterde versie van de oorspronkelijke SVG bevatten. De conversie gebeurt volledig in het geheugen, waardoor het zelfs bij grote bestanden snel is.

### Stap 4: Verifieer de output (optioneel maar aanbevolen)

```python
from PIL import Image

with Image.open(png_path) as img:
    print(f"PNG size: {img.size} – mode: {img.mode}")
    img.show()  # Opens the image in the default viewer
```

Het uitvoeren van dit fragment print de pixelafmetingen en opent de PNG, waarmee wordt bevestigd dat de conversie geslaagd is.

## Aanpassen van de conversie (hoe SVG met meer controle te converteren)

Als je een specifieke DPI of een solide achtergrond voor transparante SVG's nodig hebt, pas dan de `PngSaveOptions` aan voordat je `save` aanroept:

```python
png_options = PngSaveOptions()
png_options.dpi = 300                     # High‑resolution output
png_options.background_color = "#FFFFFF" # White background for transparency
```

Deze instellingen zijn nuttig wanneer de PNG wordt afgedrukt of ingebed in documenten die geen alfakanalen ondersteunen.

## Volledig script – kant‑klaar **svg to png code**

Hieronder staat het volledige programma dat foutafhandeling en optionele aangepaste instellingen bevat. Kopieer het naar een bestand genaamd `svg_to_png.py` en voer `python svg_to_png.py` uit.

```python
"""
Complete script to save SVG as PNG using the Aspose.SVG library.
It demonstrates the basic flow and optional customizations.
"""

import sys
from aspose.svg import SVGDocument, PngSaveOptions
from PIL import Image

def convert_svg_to_png(
    svg_path: str,
    png_path: str,
    dpi: int = 96,
    background: str = None,
) -> None:
    """
    Loads an SVG file, applies PNG save options, and writes the PNG file.
    
    Args:
        svg_path: Path to the source SVG file.
        png_path: Desired output PNG file path.
        dpi: Dots per inch for the rasterized image (default 96).
        background: Hex color (e.g., "#FFFFFF") for the PNG background.
                     If None, the original SVG transparency is kept.
    """
    try:
        # Load SVG
        svg_doc = SVGDocument(svg_path)

        # Prepare PNG options
        png_options = PngSaveOptions()
        png_options.dpi = dpi
        if background:
            png_options.background_color = background

        # Save as PNG
        svg_doc.save(png_path, png_options)

        # Verify result
        with Image.open(png_path) as img:
            print(f"Successfully saved PNG → {png_path}")
            print(f"Image size: {img.size} (pixels), mode: {img.mode}")

    except Exception as e:
        print(f"Error during conversion: {e}", file=sys.stderr)
        sys.exit(1)


if __name__ == "__main__":
    # Example usage – replace paths as needed
    SVG_INPUT = "YOUR_DIRECTORY/vector.svg"
    PNG_OUTPUT = "YOUR_DIRECTORY/vector.png"

    convert_svg_to_png(
        svg_path=SVG_INPUT,
        png_path=PNG_OUTPUT,
        dpi=300,               # High‑resolution export
        background="#FFFFFF", # White background for transparent SVGs
    )
```

**Verwachte output**

```
Successfully saved PNG → YOUR_DIRECTORY/vector.png
Image size: (800, 600) (pixels), mode: RGB
```

De afbeeldingsafmetingen weerspiegelen de viewBox van de SVG of de DPI die je hebt opgegeven.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Symptoom | Oorzaak | Oplossing |
|---------|-------|-----|
| PNG is leeg of volledig transparant | `background_color` niet ingesteld voor een SVG die afhankelijk is van transparantie | Stel `png_options.background_color` in op een solide hex‑waarde. |
| Uitvoer is onscherp | DPI op standaard 96 gelaten voor een SVG met hoge detail | Verhoog `png_options.dpi` naar 300 of hoger. |
| Script crasht met `FileNotFoundError` | Verkeerd pad naar het SVG‑bestand | Gebruik absolute paden of controleer `os.path.exists(svg_path)`. |
| Kleurverschuiving in PNG | De SVG gebruikt ICC‑profielen die niet door de bibliotheek worden ondersteund | Rasteriseer met een andere bibliotheek (bijv. `cairosvg`) of vlak kleuren af vóór export. |

## Volgende stappen

* **Batchconversie** – Loop over een map met SVG's en hergebruik `convert_svg_to_png`.  
* **Integreren met webservices** – Maak de functie beschikbaar als een Flask‑endpoint om uploads direct te converteren.  
* **Verken andere formaten** – `PngSaveOptions` heeft verwanten zoals `JpegSaveOptions` en `BmpSaveOptions` voor extra exportbehoeften.

Door de **save svg as png** workflow te beheersen, kun je asset‑pijplijnen automatiseren, miniaturen voor galerijen genereren, of graphics voorbereiden voor PDF‑rapporten — allemaal vanuit één enkel Python‑script.

---


## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Convert SVG to PNG in Python – High‑Resolution Export Guide](/html/english/python/general/convert-svg-to-png-in-python-high-resolution-export-guide/)
- [Convert SVG to PNG in Python – Complete Step‑by‑Step Guide](/html/english/python/general/convert-svg-to-png-in-python-complete-step-by-step-guide/)
- [Convert SVG to PNG in Python using Aspose.HTML](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}