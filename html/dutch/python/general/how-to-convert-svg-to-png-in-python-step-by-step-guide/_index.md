---
category: general
date: 2026-11-17
description: Converteer SVG naar PNG met Python in een paar regels. Leer SVG opslaan
  als PNG met optionele conversie‑instellingen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert svg to png
- save svg as png
- export svg as png
- svg to raster image
- how to convert svg to png
language: nl
lastmod: 2026-11-17
og_description: Converteer SVG naar PNG in Python met een beknopt voorbeeld. Volg
  de stappen om SVG efficiënt als PNG te exporteren.
og_image_alt: Diagram illustrating convert svg to png workflow in Python
og_title: svg naar png converteren in Python – snelle gids
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: convert svg to png using Python in a few lines. Learn to save SVG as
    PNG with optional conversion settings.
  headline: How to convert SVG to PNG in Python – step‑by‑step guide
  type: TechArticle
tags:
- svg
- png
- python
- image conversion
title: Hoe SVG naar PNG te converteren in Python – stapsgewijze handleiding
url: /nl/python/general/how-to-convert-svg-to-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe SVG naar PNG te converteren in Python – stapsgewijze handleiding

Als je **svg naar png wilt converteren**, laat deze gids een volledige oplossing zien die je vandaag nog kunt uitvoeren. Je ziet ook hoe je **svg als png kunt opslaan** met optionele instellingen voor grootte en achtergrondkleur.

Rasterafbeeldingen genereren vanuit vector‑SVG‑bestanden is gebruikelijk wanneer je graphics aan browsers levert, thumbnails maakt of afbeeldingen in PDF’s embedt. De tutorial behandelt alles, van het installeren van de benodigde bibliotheek tot het afhandelen van randgevallen zoals ontbrekende bestanden of zeer grote SVG’s.

## Vereisten

* Python 3.8 of nieuwer geïnstalleerd.
* Toegang tot een terminal of opdrachtprompt.
* Het `cairosvg`‑pakket, dat het zware werk doet voor **svg naar raster‑afbeelding** conversie.

Je kunt het pakket installeren met één pip‑opdracht:

```bash
pip install cairosvg
```

> **Pro tip:** Gebruik een virtuele omgeving om afhankelijkheden geïsoleerd te houden van andere projecten.

## Hoe SVG naar PNG te converteren in Python

De kern van het proces bestaat uit drie handelingen: de SVG laden, optioneel conversie‑parameters aanpassen, en het PNG‑bestand schrijven. De onderstaande code implementeert alle drie stappen in een herbruikbare functie.

```python
import cairosvg
from pathlib import Path

def convert_svg_to_png(svg_path: str, png_path: str) -> None:
    """
    Convert an SVG file to a PNG raster image.

    Parameters
    ----------
    svg_path : str
        Path to the source SVG file.
    png_path : str
        Destination path for the generated PNG file.
    """
    # Verify that the SVG file exists
    if not Path(svg_path).is_file():
        raise FileNotFoundError(f"SVG file not found: {svg_path}")

    # Perform the conversion using default settings
    cairosvg.svg2png(url=svg_path, write_to=png_path)

# Example usage
if __name__ == "__main__":
    svg_file = "YOUR_DIRECTORY/image.svg"
    png_file = "YOUR_DIRECTORY/image.png"
    convert_svg_to_png(svg_file, png_file)
    print(f"Converted {svg_file} to {png_file}")
```

### Waarom dit werkt

* `cairosvg.svg2png` leest het SVG‑bestand (`url=svg_path`) en schrijft een PNG‑bestand (`write_to=png_path`).  
* De functie geeft een duidelijke foutmelding als de bron‑SVG niet gevonden kan worden, wat je helpt om bestands‑padproblemen vroegtijdig te debuggen.  
* Het houden van de conversielogica binnen een functie maakt het gemakkelijk om deze te hergebruiken in meerdere scripts of te integreren in grotere applicaties.

## Optioneel: de conversie fijn afstemmen

Als je een specifieke uitvoergrootte of een andere achtergrond nodig hebt, accepteert `cairosvg.svg2png` extra argumenten. Hieronder staat een variant die een breedte van 300 px en een witte achtergrond instelt.

```python
def convert_svg_to_png_custom(svg_path: str, png_path: str,
                              width: int = 300,
                              background_color: str = "white") -> None:
    """
    Convert an SVG to PNG with custom dimensions and background.

    Parameters
    ----------
    width : int
        Desired width of the PNG in pixels; height scales proportionally.
    background_color : str
        Hex or named color for the PNG background.
    """
    if not Path(svg_path).is_file():
        raise FileNotFoundError(f"SVG file not found: {svg_path}")

    cairosvg.svg2png(
        url=svg_path,
        write_to=png_path,
        output_width=width,
        background_color=background_color
    )
```

Je kunt deze functie op dezelfde manier aanroepen als de basisversie, waarbij je elke gewenste breedte of kleur doorgeeft.

## Veelgestelde vragen en randgevallen

**Wat als de SVG externe lettertypen bevat?**  
`cairosvg` embedt verwijzende lettertypen automatisch, maar de lettertypebestanden moeten bereikbaar zijn vanaf de locatie van de SVG. Plaats de lettertypebestanden naast de SVG of gebruik absolute URL’s.

**Hoe ga ik om met zeer grote SVG‑bestanden?**  
Grote bestanden kunnen veel geheugen verbruiken. Je kunt de SVG‑inhoud streamen in plaats van deze van de schijf te laden:

```python
with open(svg_path, "rb") as svg_stream:
    cairosvg.svg2png(file_obj=svg_stream, write_to=png_path)
```

**Kan ik meerdere bestanden in één batch converteren?**  
Wikkel de conversie‑aanroep in een lus en gebruik `Path.glob("*.svg")` om alle SVG‑bestanden in een map te vinden.

## Verwachte output

Het uitvoeren van het voorbeeldscript print één regel die de conversie bevestigt:

```
Converted YOUR_DIRECTORY/image.svg to YOUR_DIRECTORY/image.png
```

Het resulterende `image.png`‑bestand bevindt zich in dezelfde map en kan worden geopend met elke afbeeldingsviewer.

## Conclusie

Je weet nu hoe je **svg naar png kunt converteren** in Python, hoe je **svg als png kunt opslaan**, en hoe je **svg als png kunt exporteren** met aangepaste afmetingen. dezelfde aanpak werkt voor elk SVG‑bestand, waarbij vector‑graphics worden omgezet naar een **svg naar raster‑afbeelding** formaat dat geschikt is voor webpagina’s, rapporten of thumbnails.

Volgende stappen kunnen zijn:

* De `export svg as png`‑parameters verkennen voor DPI‑controle.
* De conversiefunctie integreren in een Flask‑ of Django‑endpoint om on‑the‑fly afbeeldingsgeneratie te bieden.
* Het secundaire trefwoord **how to convert svg to png** gebruiken om te zoeken naar meer geavanceerde use‑cases zoals batchverwerking of CI/CD‑pipelines.

Voel je vrij om te experimenteren met verschillende instellingen en deel je resultaten met de community!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [SVG naar PNG converteren in Python – High‑Resolution Export Guide](/html/english/python/general/convert-svg-to-png-in-python-high-resolution-export-guide/)
- [SVG naar PNG converteren in Python met Aspose.HTML](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)
- [SVG naar PNG converteren in Python – Complete stap‑voor‑stap gids](/html/english/python/general/convert-svg-to-png-in-python-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}