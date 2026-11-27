---
category: general
date: 2026-11-27
description: Maak een SVG-document en sla het SVG‑bestand op met Python. Leer een
  vector te exporteren als SVG en genereer snel een SVG‑afbeelding.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG file
- export vector as SVG
- save SVG image
- how to create SVG
language: nl
lastmod: 2026-11-27
og_description: Maak een SVG-document en sla een SVG-bestand op met Python. Deze gids
  laat zien hoe je een vector exporteert als SVG en in enkele minuten een SVG-afbeelding
  maakt.
og_image_alt: Screenshot of a red circle saved as an SVG document
og_title: Maak een SVG-document en sla het SVG-bestand op met Python
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  headline: Create SVG document and save SVG file with Python
  type: TechArticle
- description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  name: Create SVG document and save SVG file with Python
  steps:
  - name: Expected output
    text: 'The resulting `circle.svg` contains:'
  - name: Exporting more complex vectors
    text: 'If you need to **export vector as SVG** for multi‑shape illustrations,
      simply repeat the `dwg.add()` pattern with other primitives (`rect`, `line`,
      `path`, etc.). For example:'
  - name: Handling Unicode and text
    text: "SVG supports text elements with full Unicode support. Use `dwg.text(\"Hello,
      \U0001F30D\", insert=(5, 95), fill=\"black\")` to embed multilingual labels."
  - name: Saving to a different location
    text: 'When **save SVG image** to a user‑specified folder, validate the path to
      avoid permission errors:'
  - name: Minifying the output
    text: 'For production pipelines, you might want a smaller file size. Pass `pretty=False`
      to `dwg.tostring()` and write the result manually:'
  type: HowTo
tags:
- SVG
- Python
- Vector graphics
title: Maak SVG-document en sla SVG-bestand op met Python
url: /nl/python/general/create-svg-document-and-save-svg-file-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SVG-document maken en SVG-bestand opslaan met Python

Als je een **SVG-document wilt maken** vanaf nul, leidt deze gids je door het volledige proces. Je ziet hoe je een **SVG-bestand opslaat** op schijf, de vector exporteert als SVG, en eindigt met een kant‑klaar SVG‑beeld in slechts een paar regels code.

Het programmatisch genereren van schaalbare graphics is nuttig voor rapporten, UI‑iconen, of elke situatie waarin je resolutie‑onafhankelijke afbeeldingen wilt. Aan het einde van deze tutorial kun je de vraag “**how to create SVG**?” beantwoorden voor eenvoudige vormen en het patroon uitbreiden naar complexe vector‑kunstwerken.

## Wat je nodig hebt

- Python 3.8 of nieuwer  
- Het `svgwrite`‑pakket (installeerbaar via `pip`)  
- Een beschrijfbare map voor het uitvoerbestand  

Er zijn geen externe grafische editors nodig; alles draait vanaf de opdrachtregel.

## Stap 1: Installeer de `svgwrite`‑bibliotheek

`svgwrite` biedt een schone, Pythonic API voor het bouwen van SVG‑markup. Installeer het één keer met:

```bash
pip install svgwrite
```

> **Pro tip:** Gebruik een virtuele omgeving (`python -m venv .venv`) om afhankelijkheden geïsoleerd te houden.

## Stap 2: Maak SVG-document

Nu maken we daadwerkelijk **SVG-document** objecten. De `Drawing`‑klasse vertegenwoordigt het root‑element `<svg>` en behandelt namespaces automatisch.

```python
import pathlib
import svgwrite

# Define where the file will be saved
output_path = pathlib.Path("output/circle.svg")
output_path.parent.mkdir(parents=True, exist_ok=True)

# Initialize a new SVG document with a 100×100 viewport
dwg = svgwrite.Drawing(
    filename=str(output_path),
    size=("100px", "100px"),
    profile="tiny"  # tiny profile keeps the file lightweight
)
```

De `Drawing`‑instantie is het toegangspunt voor alle volgende SVG‑bewerkingen. Door `size` op te geven, stellen we de afmetingen van het canvas in, wat invloed heeft op hoe browsers de afbeelding weergeven.

## Stap 3: Voeg een rood cirkelelement toe

Vormen toevoegen is eenvoudig. De `circle`‑methode maakt een `<circle>`‑element aan; we koppelen het vervolgens aan de root.

```python
# Create a red circle with radius 40 centered at (50, 50)
circle = dwg.circle(
    center=(50, 50),
    r=40,
    fill="red"
)

# Append the circle to the SVG root
dwg.add(circle)
```

Waarom we een cirkel kiezen: cirkels zijn vector‑primitieven die schaalbaarheid demonstreren zonder kwaliteitsverlies, waardoor de output ideaal is voor het testen van **export vector as SVG**‑workflows.

## Stap 4: SVG-bestand opslaan

Tot slot schrijf je de markup naar schijf. Deze stap voldoet aan de **save SVG file**‑vereiste en produceert een bestand dat je in elke browser of vector‑editor kunt openen.

```python
# Persist the SVG document to the filesystem
dwg.save()
print(f"SVG saved to {output_path.resolve()}")
```

Wanneer je het script uitvoert, zie je een console‑bericht dat de locatie van het gegenereerde bestand bevestigt.

### Verwachte output

Het resulterende `circle.svg` bevat:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg height="100px" version="1.1" width="100px" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" fill="red"/>
</svg>
```

Het openen van het bestand in een browser toont een scherpe rode cirkel, en omdat het vector‑gebaseerd is kun je onbeperkt inzoomen zonder pixelatie.

## Stap 5: Veelvoorkomende variaties en randgevallen

### Complexere vectoren exporteren

Als je **export vector as SVG** nodig hebt voor illustraties met meerdere vormen, herhaal dan eenvoudig het `dwg.add()`‑patroon met andere primitieven (`rect`, `line`, `path`, enz.). Bijvoorbeeld:

```python
dwg.add(dwg.rect(insert=(10, 10), size=(30, 30), fill="blue"))
dwg.add(dwg.line(start=(0, 0), end=(100, 100), stroke="black", stroke_width=2))
```

### Unicode en tekst verwerken

SVG ondersteunt textelementen met volledige Unicode‑ondersteuning. Gebruik `dwg.text("Hello, 🌍", insert=(5, 95), fill="black")` om meertalige labels in te sluiten.

### Opslaan op een andere locatie

Wanneer je **save SVG image** naar een door de gebruiker opgegeven map opslaat, valideer dan het pad om permissiefouten te voorkomen:

```python
if not output_path.parent.exists():
    raise PermissionError(f"Cannot write to {output_path.parent}")
dwg.save()
```

### Output minifieren

Voor productiepijplijnen wil je misschien een kleinere bestandsgrootte. Geef `pretty=False` door aan `dwg.tostring()` en schrijf het resultaat handmatig:

```python
minified = dwg.tostring(pretty=False)
output_path.write_text(minified)
```

## Hoe SVG maken met alternatieve bibliotheken (optioneel)

Hoewel `svgwrite` lichtgewicht en pure‑Python is, bestaan er andere ecosystemen:

- **cairosvg** – converteert PNG, PDF of HTML naar SVG.  
- **lxml** – stelt je in staat SVG‑markup handmatig te bouwen met XML‑API’s.  

De keuze voor een bibliotheek hangt af van de complexiteit van je project en bestaande afhankelijkheden.

## Conclusie

Je weet nu hoe je een **SVG-document** maakt, vectorvormen toevoegt, en een **SVG-bestand** opslaat met Python. De volledige oplossing toont de stappen om **export vector as SVG** uit te voeren, een **SVG‑image** te genereren, en de veelvoorkomende vraag **how to create SVG** programmatisch te beantwoorden.

Vanaf hier kun je:

- Het script uitbreiden met lussen om automatisch diagrammen of iconen te genereren.  
- De SVG‑output integreren in webapplicaties of e‑mail‑templates.  
- Animatie verkennen door `<animate>`‑elementen toe te voegen met `svgwrite`.

Experimenteer met verschillende vormen, kleuren en verlopen om de kracht van schaalbare vector‑graphics volledig te benutten in je Python‑projecten. Veel plezier met coderen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Create SVG Document – Add a Circle and Save as SVG](/html/english/python/general/create-svg-document-add-a-circle-and-save-as-svg/)
- [Create SVG Document in Python – Convert SVG to PNG Guide](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)
- [Load SVG File Python – Complete Guide to Export, Embed & Convert](/html/english/python/general/load-svg-file-python-complete-guide-to-export-embed-convert/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}