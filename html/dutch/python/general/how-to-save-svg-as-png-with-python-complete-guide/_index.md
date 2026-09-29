---
category: general
date: 2026-09-29
description: Hoe je SVG opslaat met Python en SVG exporteert naar PNG. Leer hoe je
  SVG naar PNG converteert met fijn afgestemde opties in enkele minuten.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save svg
- convert svg to png
- save svg as png
- export svg to png
- vector svg to png
language: nl
lastmod: 2026-09-29
og_description: Hoe SVG op te slaan met Python en SVG naar PNG te exporteren. Volg
  deze gids om SVG naar PNG te converteren met volledige controle over de opties.
og_image_alt: Screenshot of Python code converting a vector SVG file to a PNG image
og_title: Hoe SVG opslaan als PNG met Python – stap voor stap
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: How to save SVG using Python and export SVG to PNG. Learn to convert
    SVG to PNG with fine‑tuned options in minutes.
  headline: How to save SVG as PNG with Python – complete guide
  type: TechArticle
- description: How to save SVG using Python and export SVG to PNG. Learn to convert
    SVG to PNG with fine‑tuned options in minutes.
  name: How to save SVG as PNG with Python – complete guide
  steps:
  - name: Load the SVG document
    text: '```python from aspose.svg import SVGDocument'
  - name: (Optional) Create image‑save options
    text: '```python from aspose.svg import ImageSaveOptions'
  - name: Save the SVG as PNG
    text: '```python # Export the SVG to a PNG file using the options defined above
      svg_doc.save("YOUR_DIRECTORY/vector.png", options) ```'
  - name: Full script
    text: 'Putting the pieces together yields a complete, runnable program:'
  - name: Missing file or invalid path
    text: 'If `src_path` does not exist, `SVGDocument` raises a `FileNotFoundError`.
      Wrap the call in a `try/except` block to provide a friendly error message:'
  - name: Preserving aspect ratio
    text: When only one dimension (width **or** height) is set, the library automatically
      scales the other dimension to maintain the original aspect ratio. If you set
      both dimensions, the image may stretch. Choose the approach that matches your
      UI requirements.
  - name: Transparent backgrounds
    text: 'If the original SVG relies on transparency (e.g., icons), you can keep
      the PNG transparent by omitting `background_color`:'
  type: HowTo
tags:
- Python
- SVG
- Image conversion
title: Hoe SVG opslaan als PNG met Python – volledige gids
url: /nl/python/general/how-to-save-svg-as-png-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe SVG op te slaan als PNG met Python – volledige gids

Als je **hoe SVG op te slaan** als rasterafbeelding nodig hebt, laat deze tutorial je een kant‑klaar werkende oplossing zien. Je leert hoe je een vector‑SVG‑bestand laadt, optioneel de instellingen voor het opslaan van de afbeelding aanpast, en het resultaat exporteert naar PNG in slechts drie regels code.

Het opslaan van SVG‑bestanden als PNG is gebruikelijk wanneer je graphics in webpagina’s wilt insluiten, miniaturen wilt genereren, of rasterafbeeldingen wilt voeden aan machine‑learning‑pijplijnen. De hier beschreven aanpak werkt op Windows, macOS en Linux zonder extra native afhankelijkheden.

## Vereisten

* Python 3.9 of nieuwer geïnstalleerd
* Het `aspose.svg`‑pakket (de officiële Aspose SVG voor Python via .NET). Installeer het met:

```bash
pip install aspose-svg
```

* Een geldig SVG‑bestand op schijf (bijv. `vector.svg`)

Deze vereisten houden het voorbeeld zelf‑voorzienend en vermijden externe tools zoals CairoSVG.

## Hoe SVG op te slaan met Python

De kern van het proces bestaat uit drie stappen: laden, configureren en opslaan. De volgende secties splitsen elke stap uit.

### Stap 1: Laad het SVG‑document

```python
from aspose.svg import SVGDocument

# Load the SVG file from the local filesystem
svg_doc = SVGDocument("YOUR_DIRECTORY/vector.svg")
```

`SVGDocument` parseert de SVG‑XML en bouwt een in‑memory representatie. Het bestand eerst laden is verplicht; anders heeft de opslaan‑operatie geen brongegevens.

### Stap 2: (Optioneel) Maak afbeeldings‑opslaanopties

```python
from aspose.svg import ImageSaveOptions

# Create default options; you can tweak width, height, and background
options = ImageSaveOptions()
options.width = 800          # Desired output width in pixels
options.height = 600         # Desired output height in pixels
options.background_color = "#FFFFFF"  # Force a white background for transparent SVGs
```

`ImageSaveOptions` stelt je in staat de PNG‑output fijn af te stemmen. Het aanpassen van breedte en hoogte behoudt de beeldverhouding tenzij je beide expliciet instelt. Het instellen van een achtergrondkleur is handig wanneer de originele SVG transparantie bevat maar je een ondoorzichtige PNG nodig hebt.

### Stap 3: Sla de SVG op als PNG

```python
# Export the SVG to a PNG file using the options defined above
svg_doc.save("YOUR_DIRECTORY/vector.png", options)
```

De `save`‑methode schrijft een PNG‑bestand naar het doelpad. Als je het argument `options` weglaten, gebruikt de bibliotheek standaardafmetingen die zijn afgeleid van de viewBox van de SVG.

### Volledig script

Door de onderdelen samen te voegen ontstaat een compleet, uitvoerbaar programma:

```python
# -*- coding: utf-8 -*-
"""
How to save SVG as PNG with Python.
This script loads an SVG file, applies optional image‑save settings,
and exports the result to PNG.
"""

from aspose.svg import SVGDocument, ImageSaveOptions

def convert_svg_to_png(
    src_path: str,
    dst_path: str,
    width: int = 800,
    height: int = 600,
    background: str = "#FFFFFF"
) -> None:
    """Convert an SVG file to PNG with custom dimensions and background."""
    # Load the SVG document
    svg_doc = SVGDocument(src_path)

    # Prepare save options
    options = ImageSaveOptions()
    options.width = width
    options.height = height
    options.background_color = background

    # Save as PNG
    svg_doc.save(dst_path, options)


if __name__ == "__main__":
    # Example usage
    convert_svg_to_png(
        src_path="YOUR_DIRECTORY/vector.svg",
        dst_path="YOUR_DIRECTORY/vector.png",
        width=1024,
        height=768,
        background="#FFFFFF"
    )
    print("SVG successfully saved as PNG.")
```

Het uitvoeren van het script print **“SVG successfully saved as PNG.”** en maakt `vector.png` aan in dezelfde map.

## SVG naar PNG converteren – veelvoorkomende valkuilen

### Ontbrekend bestand of ongeldige pad

Als `src_path` niet bestaat, werpt `SVGDocument` een `FileNotFoundError`. Plaats de aanroep in een `try/except`‑blok om een vriendelijke foutmelding te geven:

```python
try:
    svg_doc = SVGDocument(src_path)
except FileNotFoundError:
    raise SystemExit(f"File not found: {src_path}")
```

### Behoud van beeldverhouding

Wanneer slechts één dimensie (breedte **of** hoogte) is ingesteld, schaalt de bibliotheek automatisch de andere dimensie om de oorspronkelijke beeldverhouding te behouden. Als je beide dimensies instelt, kan de afbeelding uitrekken. Kies de aanpak die past bij je UI‑vereisten.

### Transparante achtergronden

Als de originele SVG vertrouwt op transparantie (bijv. iconen), kun je de PNG transparant houden door `background_color` weg te laten:

```python
options.background_color = None   # PNG will retain transparency
```

Deze variant is nuttig wanneer de PNG over andere graphics wordt gelegd.

## SVG exporteren naar PNG – prestatie‑tips

* **Hergebruik `ImageSaveOptions`** bij het batch‑converteren van veel bestanden. Het maken van een nieuw opties‑object voor elk bestand voegt nauwelijks overhead toe, maar hergebruik voorkomt herhaalde geheugenallocatie.
* **Batchverwerking**: Loop over een map met SVG‑bestanden en roep `convert_svg_to_png` voor elk aan. De bibliotheek verwerkt elk bestand onafhankelijk, dus je kunt de lus paralleliseren met `concurrent.futures.ThreadPoolExecutor` voor snellere conversie op multi‑core machines.

```python
import os
from concurrent.futures import ThreadPoolExecutor

svg_folder = "YOUR_DIRECTORY"
png_folder = "YOUR_DIRECTORY/pngs"
os.makedirs(png_folder, exist_ok=True)

def batch_convert(file_name):
    src = os.path.join(svg_folder, file_name)
    dst = os.path.join(png_folder, file_name.replace('.svg', '.png'))
    convert_svg_to_png(src, dst)

with ThreadPoolExecutor(max_workers=8) as executor:
    executor.map(batch_convert, [f for f in os.listdir(svg_folder) if f.endswith('.svg')])
```

## SVG opslaan als PNG – verificatie

Na conversie kun je de output programmatisch verifiëren:

```python
from PIL import Image

with Image.open("YOUR_DIRECTORY/vector.png") as img:
    print(f"PNG size: {img.size}, mode: {img.mode}")
```

Typische output:

```
PNG size: (1024, 768), mode: RGBA
```

De `mode` `RGBA` bevestigt dat de afbeelding een alfakanaal (transparantie) bevat. Als je een achtergrondkleur instelt, zal de modus `RGB` zijn.

## Conclusie

Je weet nu **hoe SVG op te slaan** als PNG met Python, hoe **SVG naar PNG te converteren**, en hoe **SVG te exporteren naar PNG** met aangepaste afmetingen en achtergrondafhandeling. Het volledige script demonstreert de volledige workflow van het laden van een vector‑SVG‑bestand tot het produceren van een raster‑PNG‑beeld.

Vervolgens kun je gerelateerde onderwerpen verkennen, zoals **SVG opslaan als PNG** in batch‑modus, het gebruik van alternatieve bibliotheken zoals **CairoSVG**, of het genereren van meer‑pagina‑PDF’s vanuit SVG‑bronnen. Experimenteer met verschillende `ImageSaveOptions`‑instellingen om kwaliteit, DPI en compressie fijn af te stemmen op jouw specifieke gebruikssituatie.

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [svg naar png java – Converteer SVG naar afbeelding met Aspose.HTML voor Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [SVG-document in .NET weergeven als PNG met Aspose.HTML](/html/hindi/net/rendering-html-documents/render-svg-doc-as-png/)
- [Hoe DPI in te stellen bij het converteren van SVG naar PNG met Java](/html/english/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-with-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}