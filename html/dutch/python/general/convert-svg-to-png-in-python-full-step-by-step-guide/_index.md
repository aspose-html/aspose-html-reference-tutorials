---
category: general
date: 2026-06-10
description: Converteer SVG naar PNG in Python snel. Leer hoe je een SVG‑bestand laadt,
  een Python‑SVG‑converter gebruikt en SVG opslaat als PNG met betrouwbare code.
draft: false
keywords:
- convert svg to png
- save svg as png
- export svg as png
- python svg converter
- load svg file python
language: nl
og_description: Converteer SVG naar PNG in Python snel. Deze tutorial laat zien hoe
  je een SVG‑bestand laadt, een Python‑SVG‑converter gebruikt en SVG exporteert als
  PNG.
og_title: SVG naar PNG converteren in Python – Complete gids
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Convert SVG to PNG in Python quickly. Learn how to load SVG file, use
    a python svg converter, and save SVG as PNG with reliable code.
  headline: Convert SVG to PNG in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: Convert SVG to PNG in Python quickly. Learn how to load SVG file, use
    a python svg converter, and save SVG as PNG with reliable code.
  name: Convert SVG to PNG in Python – Full Step‑by‑Step Guide
  steps:
  - name: Loads an SVG file.
    text: Loads an SVG file.
  - name: Converts it to PNG.
    text: Converts it to PNG.
  - name: Saves the PNG to a user‑specified location.
    text: Saves the PNG to a user‑specified location.
  - name: Optionally prints a success message.
    text: Optionally prints a success message.
  - name: '**External fonts** – If the SVG references a font not installed on the
      system, CairoSVG will fall back to a generic one. Embed fonts in the SVG or
      install them locally.'
    text: '**External fonts** – If the SVG references a font not installed on the
      system, CairoSVG will fall back to a generic one. Embed fonts in the SVG or
      install them locally.'
  - name: '**Embedded images** – Base64‑encoded images work fine; external image links
      need to be reachable at conversion time.'
    text: '**Embedded images** – Base64‑encoded images work fine; external image links
      need to be reachable at conversion time.'
  - name: '**Large dimensions** – Converting a massive SVG at high DPI can consume
      a lot of RAM. Consider scaling down with the `output_width`/`output_height`
      arguments.'
    text: '**Large dimensions** – Converting a massive SVG at high DPI can consume
      a lot of RAM. Consider scaling down with the `output_width`/`output_height`
      arguments.'
  - name: '**Transparency** – PNG supports alpha, but some viewers may display a white
      background. Test the output in the target environment.'
    text: '**Transparency** – PNG supports alpha, but some viewers may display a white
      background. Test the output in the target environment.'
  type: HowTo
tags:
- Python
- SVG
- Image Processing
title: SVG naar PNG converteren in Python – Volledige stapsgewijze handleiding
url: /nl/python/general/convert-svg-to-png-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SVG naar PNG converteren in Python – Volledige stapsgewijze handleiding

Heb je ooit **SVG naar PNG moeten converteren** met Python, maar wist je niet welke bibliotheek je moet kiezen? Je bent niet de enige; veel ontwikkelaars lopen tegen dit probleem aan wanneer ze rasterafbeeldingen nodig hebben voor web‑miniaturen of PDF‑rapporten. In deze handleiding lopen we stap voor stap door het laden van een SVG‑bestand, het kiezen van een degelijke *python svg converter*, en uiteindelijk **SVG opslaan als PNG** met slechts een paar regels code. Aan het einde heb je een herbruikbaar script dat werkt op Windows, macOS en Linux.

We zullen ook ingaan op hoe je **SVG als PNG kunt exporteren** in bulk, transparantie‑eigenaardigheden afhandelt, en je code netjes houdt. Geen poespas, alleen praktische stappen die je direct kunt kopiëren‑plakken in je project.

---

## SVG naar PNG converteren – Overzicht

Voordat we in de code duiken, laten we de onderdelen verduidelijken:

| Component | Waarom het belangrijk is |
|-----------|--------------------------|
| **SVG loader** | Leest de vector‑markup zodat de converter vormen, verlopen en lettertypen kan begrijpen. |
| **Conversion engine** | Zet de vectorbeschrijving om in rasterpixels. Populaire keuzes zijn **CairoSVG**, **svglib** + **ReportLab**, of **Pillow** met een helper. |
| **Output writer** | Slaat de resulterende bitmap op als een PNG‑bestand, waarbij transparantie behouden blijft indien nodig. |

Het kiezen van de juiste *python svg converter* kan je later hoofdpijn besparen — sommige verwerken CSS‑stijlen, andere niet. We richten ons op **CairoSVG** omdat het pure Python is, minimale afhankelijkheden heeft, en direct PNG’s van hoge kwaliteit produceert.

## SVG‑bestand laden in Python

De eerste stap is om de SVG‑data in het geheugen te krijgen. Je kunt het bestand als een string lezen of de converter het direct laten openen. Hier is een kleine helper die de bestands‑laadlogica abstraheert en een duidelijke foutmelding geeft als het pad onjuist is:

```python
import pathlib

def load_svg(path: str) -> pathlib.Path:
    """
    Validate that the SVG file exists and return a pathlib.Path object.
    This function makes it easy to reuse the same check throughout your code.
    """
    svg_path = pathlib.Path(path).expanduser().resolve()
    if not svg_path.is_file():
        raise FileNotFoundError(f"SVG file not found: {svg_path}")
    if svg_path.suffix.lower() != ".svg":
        raise ValueError(f"Expected an .svg file, got: {svg_path.suffix}")
    return svg_path
```

*Waarom dit belangrijk is*: Een schone loader isoleert bestands‑systeemzorgen van de conversielogica, waardoor het script beter onderhoudbaar is. Het beantwoordt ook de veelgestelde vraag “**load svg file python**” die ontwikkelaars op forums stellen.

## Een Python SVG‑converter kiezen

Er zijn een paar concurrenten, maar laten we de twee meest voorkomende vergelijken:

| Bibliotheek | Installatie‑commando | Voordelen | Nadelen |
|-------------|----------------------|-----------|----------|
| **CairoSVG** | `pip install cairosvg` | Verwerkt CSS, verlopen, lettertypen; één‑regelige conversie; pure Python wrapper rond Cairo | Vereist `cairo` binaries op sommige platforms (installeren via systeem‑pakketbeheer) |
| **svglib + ReportLab** | `pip install svglib reportlab` | Goed voor PDF‑pijplijnen; geen externe C‑bibliotheken | Iets meer code; trager voor grote batches |

Voor de eenvoud blijven we bij **CairoSVG**. Als je de voorkeur geeft aan een pure‑Python stack zonder externe binaries, kun je later `svglib` gebruiken — wijzig gewoon de conversiefunctie.

```bash
pip install cairosvg
```

*Pro tip*: Op Ubuntu moet je mogelijk `sudo apt-get install libcairo2-dev` uitvoeren voordat je het wheel installeert; macOS‑gebruikers kunnen `brew install cairo` uitvoeren.

## SVG exporteren als PNG en het resultaat opslaan

Nu we een loader en een converter hebben, is de kernoperatie een tweeregel‑oproep. Hieronder staat een compleet, kant‑klaar script dat:

1. Een SVG‑bestand laadt.  
2. Het converteert naar PNG.  
3. De PNG opslaat op een door de gebruiker opgegeven locatie.  
4. Optioneel een succesbericht afdrukt.

```python
import pathlib
import sys
from cairosvg import svg2png

def convert_svg_to_png(svg_path: pathlib.Path, png_path: pathlib.Path, dpi: int = 96) -> None:
    """
    Convert an SVG file to PNG and write the result to disk.
    
    Parameters
    ----------
    svg_path : pathlib.Path
        Path to the source .svg file.
    png_path : pathlib.Path
        Destination path for the .png output.
    dpi : int, optional
        Dots‑per‑inch for the raster image. Higher DPI yields larger files.
    """
    # Read raw SVG data (CairoSVG can also accept a filename directly)
    svg_data = svg_path.read_bytes()
    
    # Perform the conversion; we write directly to a file-like object.
    try:
        svg2png(bytestring=svg_data, write_to=str(png_path), dpi=dpi)
    except Exception as exc:
        raise RuntimeError(f"Failed to convert {svg_path} to PNG: {exc}") from exc

def main():
    if len(sys.argv) != 3:
        print("Usage: python convert_svg.py <input.svg> <output.png>")
        sys.exit(1)

    input_svg = load_svg(sys.argv[1])
    output_png = pathlib.Path(sys.argv[2]).expanduser().resolve()
    
    # Ensure parent directory exists
    output_png.parent.mkdir(parents=True, exist_ok=True)

    convert_svg_to_png(input_svg, output_png)
    print(f"✅ Successfully saved PNG to: {output_png}")

if __name__ == "__main__":
    main()
```

**Uitleg van het “waarom”**:

- **Bytes lezen** (`read_bytes()`) voorkomt onverwachte codering die kan optreden bij `read_text()`.  
- **`dpi`‑parameter** laat je de scherpte van de afbeelding regelen; 96 dpi komt overeen met de meeste schermen, terwijl 300 dpi beter is voor afdrukken.  
- **Foutafhandeling** (`try/except`) brengt conversieproblemen vroeg naar voren — vaak wanneer de SVG externe lettertypen of afbeeldingen verwijst.  
- **Map‑aanmaak** (`mkdir(parents=True, exist_ok=True)`) betekent dat je het script naar een nieuwe map kunt wijzen zonder deze vooraf aan te maken.

Het script uitvoeren:

```bash
python convert_svg.py ./assets/logo.svg ./output/logo.png
```

Je zou een groen vinkje moeten zien en het PNG‑bestand verschijnt in `./output`.  

![converteer svg naar png uitvoer](https://example.com/images/convert-svg-to-png.png "Resultaat van de conversie van svg naar png")

*De bovenstaande afbeelding toont een klein logo dat oorspronkelijk een SVG was, nu gerasterd als een scherp PNG.*

## Randgevallen en veelvoorkomende valkuilen behandelen

Zelfs een degelijke **python svg converter** kan struikelen over enkele lastige SVG‑eigenschappen. Hier is een snelle checklist:

1. **Externe lettertypen** – Als de SVG een lettertype verwijst dat niet op het systeem is geïnstalleerd, zal CairoSVG terugvallen op een generiek lettertype. Integreer lettertypen in de SVG of installeer ze lokaal.  
2. **Ingesloten afbeeldingen** – Base64‑gecodeerde afbeeldingen werken prima; externe afbeeldingslinks moeten bereikbaar zijn op het moment van conversie.  
3. **Grote afmetingen** – Het converteren van een enorme SVG bij hoge DPI kan veel RAM verbruiken. Overweeg te verkleinen met de `output_width`/`output_height` argumenten.  
4. **Transparantie** – PNG ondersteunt alfa, maar sommige viewers kunnen een witte achtergrond tonen. Test de output in de doelomgeving.

Als je een van deze tegenkomt, kun je de conversie‑aanroep aanpassen:

```python
svg2png(
    bytestring=svg_data,
    write_to=str(png_path),
    dpi=150,
    output_width=800,          # force width, preserve aspect ratio
    background_color="#FFFFFF"  # optional background for fully transparent images
)
```

## Bulk‑export – Een hele map converteren

Vaak moet je **SVG opslaan als PNG** voor tientallen iconen. Het volgende fragment bouwt voort op de vorige functies en doorloopt een mapstructuur:

```python
def batch_convert(source_dir: pathlib.Path, dest_dir: pathlib.Path, dpi: int = 96) -> None:
    """
    Recursively find all .svg files under source_dir and convert each to PNG
    in the mirrored structure under dest_dir.
    """
    for svg_file in source_dir.rglob("*.svg"):
        relative_path = svg_file.relative_to(source_dir).with_suffix(".png")
        target_png = dest_dir / relative_path
        target_png.parent.mkdir(parents=True, exist_ok=True)
        convert_svg_to_png(svg_file, target_png, dpi=dpi)
        print(f"✔︎ {svg_file} → {target_png}")

# Example usage:
# batch_convert(pathlib.Path("./icons"), pathlib.Path("./pngs"), dpi=150)
```

Dit hulpprogramma laat zien hoe eenvoudig het is om **SVG als PNG te exporteren** in massa zodra je de workflow voor één bestand onder de knie hebt.

## Conclusie

We hebben alles behandeld wat je nodig hebt om **SVG naar PNG te converteren** in Python: het laden van het SVG‑bestand, het kiezen van een betrouwbare *python svg converter* (CairoSVG), het exporteren van de rasterafbeelding, en zelfs het verwerken van bulkconversies. Het kernscript is slechts ~30 regels, maar toch robuust genoeg voor productiegebruik.

Volgende stappen? Probeer CairoSVG te vervangen door `svglib` als je strakkere PDF‑integratie nodig hebt, experimenteer met verschillende DPI‑instellingen voor print‑klare assets, of voeg een CLI‑vlag toe om uitvoerformaten te kiezen (JPG, TIFF). De mogelijkheden zijn eindeloos zodra je de basis onder de knie hebt.

Heb je vragen over **SVG opslaan als PNG** of loop je tegen een eigenzinnige SVG aan? Laat een reactie achter hieronder, en happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [svg naar png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Render SVG Doc as PNG in .NET with Aspose.HTML](/html/english/net/rendering-html-documents/render-svg-doc-as-png/)
- [Gebruik Aspose.HTML om een SVG‑document in .NET als PNG te renderen](/html/chinese/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}