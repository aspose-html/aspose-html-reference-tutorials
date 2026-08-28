---
category: general
date: 2026-06-16
description: Hoe je SVG snel kunt verkleinen in Python – SVG‑bestand laden met Python,
  SVG‑bestand bewerken met Python, en zelfs batch‑gewijs SVG‑bestanden verkleinen
  met een klein script.
draft: false
keywords:
- how to resize svg
- batch resize svg files
- load svg file python
- edit svg file python
language: nl
og_description: Hoe SVG te verkleinen in Python? Leer hoe je een SVG‑bestand laadt
  in Python, een SVG‑bestand bewerkt in Python, en SVG‑bestanden batchgewijs verkleint
  met een duidelijk, uitvoerbaar voorbeeld.
og_title: Hoe SVG te schalen in Python – Complete tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to resize SVG in Python quickly – load SVG file Python, edit SVG
    file Python, and even batch resize SVG files with a tiny script.
  headline: How to Resize SVG in Python – Step‑by‑Step Guide
  type: TechArticle
- description: How to resize SVG in Python quickly – load SVG file Python, edit SVG
    file Python, and even batch resize SVG files with a tiny script.
  name: How to Resize SVG in Python – Step‑by‑Step Guide
  steps:
  - name: '**Collects** every `.svg` file in the source folder.'
    text: '**Collects** every `.svg` file in the source folder.'
  - name: '**Loads** each file using the same routine we used for a single SVG.'
    text: '**Loads** each file using the same routine we used for a single SVG.'
  - name: '**Resizes** to the desired width while keeping the aspect ratio.'
    text: '**Resizes** to the desired width while keeping the aspect ratio.'
  - name: '**Writes** the result to a new folder, leaving originals untouched.'
    text: '**Writes** the result to a new folder, leaving originals untouched.'
  type: HowTo
tags:
- Python
- SVG
- Automation
title: Hoe SVG in Python te schalen – Stapsgewijze handleiding
url: /nl/python/general/how-to-resize-svg-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe SVG te schalen in Python – Complete tutorial

Heb je je ooit afgevraagd **hoe je SVG kunt verkleinen** zonder een grafische editor te openen? Misschien heb je een logo dat 200 px breed moet zijn voor een webbanner, of ben je tientallen iconen aan het voorbereiden voor een mobiele app. Het goede nieuws? Je kunt het allemaal in Python doen—geen Photoshop, geen Inkscape UI, slechts een paar regels code.

In deze gids lopen we stap voor stap door het laden van een SVG‑bestand in Python, het bewerken van de afmetingen, en zelfs het schalen van een hele map met SVG's in één keer. Aan het einde kun je **load SVG file Python**, **edit SVG file Python**, en **batch resize SVG files** vol vertrouwen uitvoeren.

## Vereisten

- Python 3.8+ geïnstalleerd (het standaard `python`-commando werkt)
- De `svgwrite` of `lxml` bibliotheek – we gebruiken `lxml` omdat het directe DOM-toegang biedt.
- Een map met SVG's die je wilt verkleinen (bijv. `assets/icons/`)

Je hebt geen GUI‑tools nodig; alles draait vanuit de terminal.

---

## Stap 1: Installeer de vereiste bibliotheek

Eerst haal je `lxml` van PyPI. Het is klein, snel, en laat ons XML‑attributen direct manipuleren.

```bash
pip install lxml
```

> **Pro tip:** Als je in een virtuele omgeving werkt, activeer deze dan voordat je het commando uitvoert. Dit houdt de projectafhankelijkheden netjes.

## Stap 2: Laad een SVG‑bestand in Python

Nu gaan we **load SVG file Python**-stijl—het XML lezen, het root‑element `<svg>` ophalen, en de huidige grootte afdrukken.

```python
from lxml import etree

def load_svg(path: str) -> etree._ElementTree:
    """
    Load an SVG document and return the parsed XML tree.
    """
    parser = etree.XMLParser(remove_blank_text=True)
    tree = etree.parse(path, parser)
    return tree

# Example usage
svg_path = "assets/logo.svg"
svg_tree = load_svg(svg_path)
root = svg_tree.getroot()
print(f"Original width: {root.get('width')}, height: {root.get('height')}")
```

**Waarom dit belangrijk is:** `lxml` geeft ons een echte DOM, zodat we elk attribuut kunnen opvragen of wijzigen—perfect voor **edit SVG file Python**‑taken.

## Stap 3: Verander de breedte (en hoogte) – Hoe SVG te schalen

SVG's zijn vector, dus je kunt de breedte, hoogte, of beide instellen. Als je alleen de breedte wijzigt, behoudt de viewBox de beeldverhouding, maar veel tools respecteren ook een overeenkomend hoogte‑attribuut. Hier is een hulpfunctie die schaalt terwijl de oorspronkelijke beeldverhouding behouden blijft:

```python
def resize_svg(tree: etree._ElementTree, new_width: int) -> None:
    """
    Resize the root <svg> element to `new_width` while preserving aspect ratio.
    """
    root = tree.getroot()
    # Grab original dimensions (they may be in px, pt, or just numbers)
    orig_width = float(root.get("width").replace("px", ""))
    orig_height = float(root.get("height").replace("px", ""))

    # Compute scale factor and new height
    scale = new_width / orig_width
    new_height = round(orig_height * scale, 2)

    # Update attributes
    root.set("width", f"{new_width}px")
    root.set("height", f"{new_height}px")

    # Optional: ensure viewBox exists for better scaling in browsers
    if "viewBox" not in root.attrib:
        viewbox = f"0 0 {orig_width} {orig_height}"
        root.set("viewBox", viewbox)

# Resize to 200 px wide
resize_svg(svg_tree, 200)
```

De bovenstaande functie is de kern van **how to resize SVG**. Hij leest de huidige grootte, berekent een proportionele hoogte, en schrijft de nieuwe attributen terug naar het bestand.

## Stap 4: Sla de aangepaste SVG op

Na het bewerken moet je de wijzigingen terug naar de schijf schrijven. Dit voltooit de **edit SVG file Python**‑cyclus.

```python
def save_svg(tree: etree._ElementTree, destination: str) -> None:
    """
    Write the modified SVG tree to `destination`.
    """
    tree.write(
        destination,
        pretty_print=True,
        xml_declaration=True,
        encoding="UTF-8"
    )
    print(f"Saved resized SVG to {destination}")

# Save as a new file so the original stays untouched
output_path = "assets/logo_resized.svg"
save_svg(svg_tree, output_path)
```

Voer het volledige script uit en je ziet een nieuwe `logo_resized.svg` die precies 200 px breed is.

## Stap 5: Batch‑schalen van SVG‑bestanden – Schaal een volledige map

Nu we **load SVG file Python**, **edit SVG file Python**, en kunnen opslaan, laten we over een map itereren en dezelfde transformatie op elk bestand toepassen. Dit is het antwoord op **batch resize SVG files**.

```python
import pathlib

def batch_resize(source_dir: str, target_dir: str, width: int) -> None:
    """
    Resize every .svg file in `source_dir` to `width` pixels and store
    the results in `target_dir`.
    """
    src = pathlib.Path(source_dir)
    tgt = pathlib.Path(target_dir)
    tgt.mkdir(parents=True, exist_ok=True)

    svg_files = list(src.glob("*.svg"))
    if not svg_files:
        print("No SVG files found.")
        return

    for svg_path in svg_files:
        try:
            tree = load_svg(str(svg_path))
            resize_svg(tree, width)
            out_path = tgt / svg_path.name
            save_svg(tree, str(out_path))
        except Exception as e:
            print(f"Failed on {svg_path.name}: {e}")

# Example: resize everything in 'assets/icons' to 64 px wide
batch_resize("assets/icons", "assets/icons_resized", 64)
```

### Wat dit doet:

1. **Verzamelt** elk `.svg`‑bestand in de bronmap.
2. **Laadt** elk bestand met dezelfde routine die we voor een enkele SVG gebruikten.
3. **Schaalt** naar de gewenste breedte terwijl de beeldverhouding behouden blijft.
4. **Schrijft** het resultaat naar een nieuwe map, waarbij de originelen onaangeroerd blijven.

Je hebt nu een kant‑en‑klaar pipeline voor **batch resize SVG files**.

## Stap 6: Randgevallen & Veelvoorkomende valkuilen

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| Ontbrekende `width`/`height` attributen | Sommige SVG's vertrouwen alleen op `viewBox`. | Als attributen ontbreken, val terug op viewBox-afmetingen (`viewBox="0 0 w h"`). |
| Eenheden anders dan `px` (bijv. `pt`, `%`) | Het script verwijdert alleen `px`. | Breid de `replace`‑aanroep uit of gebruik een regex om elke eenheid te vangen. |
| Complexe `<symbol>`‑ of `<use>`‑elementen | Het schalen van de root heeft mogelijk geen effect op geneste symbolen. | Pas dezelfde attribuutwijzigingen toe op elk `<symbol>`‑tag, of gebruik CSS `transform: scale()`. |
| Unicode‑ of speciale tekens in bestandsnamen | `pathlib` behandelt de meeste gevallen, maar Windows kan problemen hebben met bepaalde tekens. | Zorg ervoor dat bestandsnamen UTF‑8‑veilig zijn, of hernoem ze vóór verwerking. |

Deze van tevoren aanpakken bespaart je later verrassende kapotte iconen.

## Stap 7: Controleer het resultaat

Een snelle sanity‑check kan worden gedaan met een klein HTML‑fragment:

```html
<!DOCTYPE html>
<html>
<head><title>SVG Test</title></head>
<body>
  <h3>Original</h3>
  <img src="assets/logo.svg" alt="original logo">
  <h3>Resized</h3>
  <img src="assets/logo_resized.svg" alt="resized logo">
</body>
</html>
```

Open het bestand in een browser—beide afbeeldingen moeten er identiek uitzien, maar de geschaalde zal een breedte van **200 px** melden in de ontwikkelaarstools.

---

## Conclusie

Je weet nu **how to resize SVG** met puur Python, van één enkel bestand tot een volledige map. De workflow omvat **load SVG file Python**, **edit SVG file Python**, en **batch resize SVG files**—allemaal met slechts een handvol functies.

Probeer het: test verschillende breedtes, experimenteer met alleen‑hoogte‑schaling, of voeg een command‑line‑interface toe met `argparse`. De mogelijkheden zijn eindeloos, en het script is licht genoeg om in build‑pipelines, CI‑taken, of desktop‑hulpmiddelen te integreren.

Heb je vragen over het omgaan met gradients, ingesloten lettertypen, of het integreren hiervan in een Flask‑app? Laat een reactie achter, en we verkennen die aspecten samen. Veel plezier met coderen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Aspose.HTML के साथ .NET में SVG को इमेज में बदलें](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [Aspose.HTML के साथ .NET में SVG को PDF में बदलें](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-pdf/)
- [Aspose.HTML के साथ .NET में SVG दस्तावेज़ को PNG के रूप में प्रस्तुत करें](/html/hindi/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}