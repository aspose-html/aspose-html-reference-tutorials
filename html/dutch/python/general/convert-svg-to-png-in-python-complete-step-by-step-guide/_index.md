---
category: general
date: 2026-06-19
description: Converteer SVG naar PNG in Python snel en gemakkelijk. Leer hoe je SVG
  als PNG opslaat, de conversie van SVG naar PNG afhandelt en SVG naar PNG exporteert
  met een eenvoudig script.
draft: false
keywords:
- convert svg to png
- save svg as png
- svg to png conversion
- svg to png python
- export svg to png
language: nl
og_description: Converteer SVG naar PNG in Python met deze praktische tutorial. Leer
  het volledige SVG‑naar‑PNG conversieproces en hoe je SVG efficiënt naar PNG exporteert.
og_title: Converteer SVG naar PNG in Python – Complete gids
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Convert SVG to PNG in Python quickly and easily. Learn how to save
    SVG as PNG, handle svg to png conversion, and export SVG to PNG with a simple
    script.
  headline: Convert SVG to PNG in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Convert SVG to PNG in Python quickly and easily. Learn how to save
    SVG as PNG, handle svg to png conversion, and export SVG to PNG with a simple
    script.
  name: Convert SVG to PNG in Python – Complete Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - Basic familiarity with pip and
      virtual environments. - An SVG file you want to transform (we’ll use `logo.svg`
      as an example).'
  - name: Why This Approach Works
    text: '- **Explicit I/O handling:** By reading the SVG as bytes, we avoid issues
      with Unicode encodings that sometimes crop up on Windows. - **Custom DPI:**
      Scaling is often required when the target PNG must match a specific pixel density
      (think print vs. screen). - **Optional background:** Some SVGs have '
  - name: Expected Result
    text: '- `output/logo.png` – a 1:1 raster of the original SVG, preserving any
      transparency. - `output/logo_highres.png` – a 300 DPI version with a white background,
      perfect for print.'
  - name: 1. **What if the SVG uses external fonts?**
    text: '`cairosvg` tries to embed referenced fonts, but it only sees files on the
      local filesystem. Copy the font files next to the SVG or embed them directly
      in the SVG with `<style>` tags. Otherwise you’ll get fallback fonts in the PNG.'
  - name: 2. **How do I keep the original aspect ratio when scaling?**
    text: Pass only `dpi` and let Cairo compute the pixel dimensions from the SVG’s
      viewBox. If you need a fixed width/height, calculate the appropriate DPI yourself
      or use the `output_width`/`output_height` arguments provided by `svg2png`.
  - name: 3. **Can I convert large SVGs without exhausting memory?**
    text: Yes. `cairosvg` streams the rasterization, but you should avoid loading
      massive SVGs into memory all at once. Process them one by one, as shown in the
      batch example.
  - name: 4. **Is the conversion thread‑safe?**
    text: The underlying Cairo library is not fully thread‑safe on all platforms.
      If you plan to run conversions in parallel, wrap calls in a multiprocessing
      pool rather than threading.
  - name: What’s Next?
    text: '- Explore **svg to png conversion** with alternative libraries like `svglib`
      + `reportlab` for PDF‑first workflows. - Combine this script with image‑optimization
      tools (e.g., `pngquant`) to shrink file size for the web. - Add a CLI wrapper
      using `argparse` or `click` so you can run `python -m conver'
  type: HowTo
tags:
- Python
- Image Processing
- SVG
title: SVG naar PNG converteren in Python – Complete stapsgewijze handleiding
url: /nl/python/general/convert-svg-to-png-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SVG naar PNG converteren in Python – Complete stapsgewijze gids

Heb je ooit **SVG naar PNG moeten converteren** maar wist je niet welke bibliotheek je moest kiezen? Je bent niet de enige—veel ontwikkelaars lopen tegen dit probleem aan wanneer ze vectorafbeeldingen in webassets willen insluiten of thumbnails on‑the‑fly willen genereren. Het goede nieuws? Met slechts een paar regels Python kun je **SVG opslaan als PNG** en je build‑pipeline soepel houden.

In deze tutorial lopen we een praktische **svg naar png conversie** door met een populaire bibliotheek, behandelen we de nuances van **svg naar png python** code, en laten we je zien hoe je **SVG naar PNG kunt exporteren** met juiste foutafhandeling. Aan het einde heb je een herbruikbare functie die je in elk project kunt gebruiken, of je nu een CLI‑tool bouwt of een server‑side beeldservice.

## Wat je zult leren

- De minimale afhankelijkheden die nodig zijn voor **svg naar png converteren** in Python.  
- Hoe je een SVG‑bestand laadt, PNG‑exportopties configureert en de uitvoerafbeelding schrijft.  
- Veelvoorkomende valkuilen (transparante achtergronden, grote afmetingen) en hoe je ze vermijdt.  
- Een kant‑klaar script dat je kunt aanpassen voor batchverwerking of integreren in een Flask/Django‑endpoint.

### Vereisten

- Python 3.8+ geïnstalleerd op je machine.  
- Basiskennis van pip en virtuele omgevingen.  
- Een SVG‑bestand dat je wilt transformeren (we gebruiken `logo.svg` als voorbeeld).

Als je die al hebt, geweldig—laten we beginnen.

## Stap 1: Installeer de vereiste bibliotheek

De meest eenvoudige manier om **SVG naar PNG te converteren** in Python is met het `cairosvg`‑pakket. Het omsluit de Cairo‑grafiekbibliotheek en handelt vector‑rasterisatie onder de motorkap af.

```bash
pip install cairosvg
```

> **Pro tip:** Pin de versie (bijv. `cairosvg==2.7.0`) in je `requirements.txt` om onverwachte breuken te voorkomen wanneer er een nieuwe hoofdrelease verschijnt.

## Stap 2: Schrijf een eenvoudige conversiefunctie

Nu de bibliotheek aanwezig is, maken we een kleine helper die het zware werk doet. Deze functie omsluit de **svg naar png python** logica, waardoor hij gemakkelijk herbruikbaar is.

```python
# convert_svg_to_png.py
import os
from cairosvg import svg2png

def convert_svg_to_png(
    input_path: str,
    output_path: str,
    dpi: int = 96,
    background_color: str = None,
) -> None:
    """
    Convert an SVG file to a PNG image.

    Parameters
    ----------
    input_path : str
        Path to the source SVG file.
    output_path : str
        Destination path for the generated PNG.
    dpi : int, optional
        Dots per inch for the rasterized image (default: 96).
    background_color : str, optional
        Hex color (e.g., "#FFFFFF") to use as background.
        If None, the SVG's own transparency is preserved.

    Raises
    ------
    FileNotFoundError
        If the input SVG does not exist.
    ValueError
        If the output directory cannot be created.
    """
    # Validate input file
    if not os.path.isfile(input_path):
        raise FileNotFoundError(f"SVG file not found: {input_path}")

    # Ensure output directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Read the SVG content
    with open(input_path, "rb") as svg_file:
        svg_bytes = svg_file.read()

    # Perform the conversion
    svg2png(
        bytestring=svg_bytes,
        write_to=output_path,
        dpi=dpi,
        background_color=background_color,
    )
    print(f"✅ Successfully saved PNG to {output_path}")
```

### Waarom deze aanpak werkt

- **Expliciete I/O‑afhandeling:** Door de SVG als bytes te lezen, vermijden we problemen met Unicode‑encoderingen die soms op Windows opduiken.  
- **Aangepaste DPI:** Schalen is vaak nodig wanneer de doel‑PNG moet overeenkomen met een specifieke pixeldichtheid (denk aan print versus scherm).  
- **Optionele achtergrond:** Sommige SVG’s hebben transparante gebieden; een hex‑kleur doorgeven laat je **SVG naar PNG exporteren** met een solide achtergrond, wat handig is voor UI‑thumbnails.

## Stap 3: Voer het conversiescript uit

Met de functie klaar, laten we een echt bestand converteren. Plaats `logo.svg` in een map genaamd `assets/` en voer het script uit vanuit de project‑root.

```python
# demo_conversion.py
from convert_svg_to_png import convert_svg_to_png

if __name__ == "__main__":
    INPUT_SVG = "assets/logo.svg"
    OUTPUT_PNG = "output/logo.png"

    # Simple call – defaults keep transparency and 96 DPI
    convert_svg_to_png(INPUT_SVG, OUTPUT_PNG)

    # Example with a white background and higher DPI for sharper output
    convert_svg_to_png(
        INPUT_SVG,
        "output/logo_highres.png",
        dpi=300,
        background_color="#FFFFFF",
    )
```

Voer het uit:

```bash
python demo_conversion.py
```

Je zou console‑output moeten zien die bevestigt dat de bestanden zijn geschreven:

```
✅ Successfully saved PNG to output/logo.png
✅ Successfully saved PNG to output/logo_highres.png
```

### Verwacht resultaat

- `output/logo.png` – een 1:1 raster van de originele SVG, met behoud van eventuele transparantie.  
- `output/logo_highres.png` – een 300 DPI versie met een witte achtergrond, perfect voor print.

![voorbeeld van SVG naar PNG output](example.png){alt="voorbeeld van SVG naar PNG output"}

*(De screenshot toont de PNG‑bestanden geopend in een afbeeldingsviewer, wat bevestigt dat de conversie geslaagd is.)*

## Stap 4: Batch‑verwerk meerdere SVG’s (optioneel)

Als je **SVG als PNG wilt opslaan** voor een volledige map, doet een korte lus het werk. Deze snippet demonstreert ook elegante foutafhandeling—handig wanneer sommige SVG’s mogelijk beschadigd zijn.

```python
import glob
from pathlib import Path

def batch_convert(source_dir: str, dest_dir: str, **options):
    svg_paths = glob.glob(os.path.join(source_dir, "*.svg"))
    for svg_path in svg_paths:
        try:
            filename = Path(svg_path).stem + ".png"
            output_path = os.path.join(dest_dir, filename)
            convert_svg_to_png(svg_path, output_path, **options)
        except Exception as e:
            print(f"⚠️  Failed to convert {svg_path}: {e}")

if __name__ == "__main__":
    batch_convert(
        source_dir="assets/",
        dest_dir="output/batch/",
        dpi=150,
        background_color="#F0F0F0",
    )
```

Het uitvoeren hiervan vult `output/batch/` met PNG’s voor elke SVG in `assets/`. Als een bestand faalt, logt het script de fout en gaat door—geen noodzaak om de hele taak te stoppen.

## Veelgestelde vragen & randgevallen

### 1. **Wat als de SVG externe lettertypen gebruikt?**  
`cairosvg` probeert de verwijzende lettertypen in te sluiten, maar ziet alleen bestanden op het lokale bestandssysteem. Kopieer de lettertypebestanden naast de SVG of sluit ze direct in de SVG in met `<style>`‑tags. Anders krijg je fallback‑lettertypen in de PNG.

### 2. **Hoe behoud ik de oorspronkelijke beeldverhouding bij schalen?**  
Geef alleen `dpi` door en laat Cairo de pixelafmetingen berekenen vanuit de viewBox van de SVG. Als je een vaste breedte/hoogte nodig hebt, bereken dan zelf de juiste DPI of gebruik de `output_width`/`output_height` argumenten die `svg2png` biedt.

### 3. **Kan ik grote SVG’s converteren zonder geheugen uit te putten?**  
Ja. `cairosvg` streamt de rasterisatie, maar je moet vermijden om enorme SVG’s in één keer in het geheugen te laden. Verwerk ze één voor één, zoals getoond in het batch‑voorbeeld.

### 4. **Is de conversie thread‑safe?**  
De onderliggende Cairo‑bibliotheek is niet volledig thread‑safe op alle platformen. Als je van plan bent om conversies parallel uit te voeren, wikkel de aanroepen dan in een multiprocessing‑pool in plaats van threading.

## Prestatietips

- **Cache de PNG** als de SVG zelden verandert; elke keer opnieuw berekenen verspilt CPU‑cycli.  
- **Herbruik dezelfde DPI** bij opeenvolgende aanroepen om herhaalde schaalberekeningen te vermijden.  
- Voor webservices kun je overwegen de PNG als een `BytesIO`‑stream terug te geven in plaats van naar schijf te schrijven—dit verkort I/O‑latentie.

```python
from io import BytesIO
def convert_svg_to_png_bytes(svg_path: str, dpi: int = 96) -> BytesIO:
    with open(svg_path, "rb") as f:
        svg_bytes = f.read()
    png_bytes = BytesIO()
    svg2png(bytestring=svg_bytes, write_to=png_bytes, dpi=dpi)
    png_bytes.seek(0)
    return png_bytes
```

## Samenvatting

We hebben alles behandeld wat je nodig hebt om **SVG naar PNG te converteren** met Python:

1. Installeer `cairosvg`.  
2. Schrijf een herbruikbare `convert_svg_to_png`‑functie die DPI, achtergrondkleuren en foutcontrole afhandelt.  
3. Voer het script uit op één bestand of batch‑verwerk een hele map.  
4. Pak veelvoorkomende eigenaardigheden aan zoals externe lettertypen, behoud van beeldverhouding en thread‑veiligheid.

Gewapend met deze kennis kun je nu **SVG als PNG opslaan** in elke automatiseringspipeline, de conversie integreren in web‑API’s, of eenvoudig assets genereren voor een design‑systeem. 

### Wat is het volgende?

- Verken **svg naar png conversie** met alternatieve bibliotheken zoals `svglib` + `reportlab` voor PDF‑first workflows.  
- Combineer dit script met beeld‑optimalisatietools (bijv. `pngquant`) om de bestandsgrootte voor het web te verkleinen.  
- Voeg een CLI‑wrapper toe met `argparse` of `click` zodat je `python -m convert_svg_to_png INPUT.svg OUTPUT.png` vanuit de terminal kunt uitvoeren.

Heb je meer vragen? Laat een reactie achter hieronder, of fork de repo en experimenteer met verschillende exportinstellingen. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [svg naar png java – SVG naar afbeelding converteren met Aspose.HTML voor Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [SVG-doc renderen als PNG in .NET met Aspose.HTML](/html/english/net/rendering-html-documents/render-svg-doc-as-png/)
- [svg naar png java – SVG naar afbeelding converteren met Aspose.HTML voor Java](/html/spanish/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}