---
category: general
date: 2026-10-02
description: Leer hoe je een SVG‑document maakt in Python, SVG opslaat naar een bestand
  en een SVG‑afbeelding exporteert met een kort, compleet script.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG to file
- how to generate SVG
- export SVG image
- SVG Python tutorial
language: nl
lastmod: 2026-10-02
og_description: Maak een SVG-document in Python en exporteer een SVG-afbeelding met
  deze praktische tutorial. Volg het script, sla de SVG op in een bestand en gebruik
  de vectorafbeelding direct opnieuw.
og_image_alt: Screenshot of a Python script that creates an SVG document
og_title: Maak een SVG-document in Python – stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-10-02'
  description: Learn how to create SVG document in Python, save SVG to file, and export
    SVG image with a short, complete script.
  headline: How to create SVG document and export it as an image in Python
  type: TechArticle
tags:
- SVG
- Python
- graphics
title: Hoe een SVG-document te maken en het als afbeelding te exporteren in Python
url: /nl/python/general/how-to-create-svg-document-and-export-it-as-an-image-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een SVG-document te maken en te exporteren als afbeelding in Python

Als je **een SVG-document** programmatisch moet maken, laat deze tutorial je precies zien hoe je dat doet met Python. Je ziet een compleet script dat een eenvoudige cirkel maakt, de SVG opslaat naar een bestand, en een exporteerbare SVG-afbeelding produceert die je overal kunt insluiten.

Het genereren van schaalbare vectorafbeeldingen vanuit code verwijdert de handmatige inspanning van het tekenen van vormen in een GUI-editor. Aan het einde van deze gids kun je SVG-creatie integreren in data‑visualisatie‑pijplijnen, geautomatiseerde rapportgeneratoren, of elk project dat scherpe, resolutie‑onafhankelijke graphics vereist.

## Vereisten

- Python 3.8 of nieuwer geïnstalleerd
- De `svgwrite`-bibliotheek (installeren met `pip install svgwrite`)
- Schrijfrechten voor de map waarin de SVG wordt opgeslagen

Deze vereisten houden het voorbeeld lichtgewicht en compatibel met de meeste omgevingen.

## Stap 1: Installeer en importeer de SVG-bibliotheek

De eerste stap is het toevoegen van de externe bibliotheek die een handige API biedt voor het maken van SVG.

```python
# Install the library (run once in your terminal)
# pip install svgwrite

import svgwrite  # Provides the SVGDocument class and element helpers
```

`svgwrite` abstraheert de XML-structuur van een SVG‑bestand, zodat je je kunt concentreren op geometrie in plaats van ruwe markup.

## Stap 2: Maak een SVG-documentobject

Nu kun je **een SVG-document** maken door `svgwrite.Drawing` te instantieren. Dit object vertegenwoordigt het root‑element `<svg>` en bevat alle daaropvolgende vormen.

```python
# Step 2: Initialize the SVG document
dwg = svgwrite.Drawing(
    filename="circle.svg",     # Desired output file name
    size=("100px", "100px"),   # Width and height of the canvas
    viewBox=("0 0 100 100")    # Coordinate system for drawing
)
```

Het argument `size` definieert de gerenderde pixelafmetingen, terwijl `viewBox` een coördinatensysteem vastlegt dat overeenkomt met de geometrie die je later definieert.

## Stap 3: Voeg een cirkelelement toe

Een cirkel wordt gedefinieerd door zijn middelpunt (`cx`, `cy`) en straal (`r`). Gebruik de `circle`‑helper om deze attributen toe te voegen.

```python
# Step 3: Create a <circle> element
circle = dwg.circle(
    center=("50", "50"),   # cx = 50, cy = 50
    r="40",                # radius = 40
    fill="lightcoral",     # Fill color for visual clarity
    stroke="black",        # Outline color
    stroke_width="2"
)

# Append the circle to the SVG root
dwg.add(circle)
```

De cirkel bevindt zich in het midden van het 100 × 100‑canvas, met een marge van 10 pixel aan elke kant. Pas `fill` en `stroke` aan om overeen te komen met je ontwerpstijl.

## Stap 4: Sla de SVG op als bestand

Met de grafiek samengesteld kun je **de SVG opslaan naar een bestand** met de `save`‑methode. Dit schrijft goed‑gevormde XML die browsers en vectorbewerkers begrijpen.

```python
# Step 4: Persist the SVG document
dwg.save()
print("SVG file saved as circle.svg")
```

Het bestand `circle.svg` bevindt zich nu in de huidige werkmap. Je kunt het openen in een webbrowser, Inkscape, of elk hulpmiddel dat het SVG‑formaat ondersteunt.

## Stap 5: Controleer de geëxporteerde SVG-afbeelding

Open het opgeslagen bestand in een browser om de output te bevestigen. Je zou een gecentreerde cirkel moeten zien met de opgegeven kleuren. De ruwe XML ziet er als volgt uit:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg width="100px" height="100px" viewBox="0 0 100 100"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40"
          fill="lightcoral" stroke="black" stroke-width="2"/>
</svg>
```

Omdat SVG vector‑gebaseerd is, kun je de afbeelding schalen zonder kwaliteitsverlies, waardoor het ideaal is voor responsieve webontwerpen of afdrukken met hoge resolutie.

## Pro‑tip: Exporteer SVG als PNG of JPEG

Als je een rasterversie nodig hebt, combineer dan het SVG‑bestand met een conversietool zoals **CairoSVG**:

```python
# Optional: Convert SVG to PNG
# pip install cairosvg
import cairosvg

cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

Deze stap toont **het exporteren van een SVG-afbeelding** naar een bitmap‑formaat, nuttig wanneer downstream‑systemen SVG niet direct kunnen weergeven.

## Veelvoorkomende variaties en randgevallen

| Variatie | Hoe te behandelen |
|-----------|-------------------|
| Meerdere vormen | Roep `dwg.add()` aan voor elk nieuw element (rect, line, path). |
| Dynamische afmetingen | Bereken `size` en `viewBox` uit data voordat je `Drawing` maakt. |
| Tekstlabels | Gebruik `dwg.text("Label", insert=("10", "20"))` en style met `font_size` en `fill`. |
| Het document hergebruiken | Houd het `Drawing`‑object in het geheugen en roep `save()` aan wanneer je een bijgewerkt bestand nodig hebt. |
| Grote bestanden | Stream de output met `dwg.tostring()` en schrijf handmatig naar een bestandsobject om geheugenpieken te vermijden. |

Het aanpakken van deze scenario's zorgt ervoor dat je **script om SVG te genereren** schaalt van eenvoudige iconen tot complexe diagrammen.

## Volledige scriptoverzicht

Hieronder staat het volledige, uitvoerbare voorbeeld dat alle stappen en de optionele conversie bevat:

```python
# Full SVG creation script – create SVG document, save SVG to file, export SVG image
import svgwrite
import cairosvg  # Optional, only needed for PNG conversion

# Initialize the drawing (SVG document)
dwg = svgwrite.Drawing(
    filename="circle.svg",
    size=("100px", "100px"),
    viewBox=("0 0 100 100")
)

# Define a circle element
circle = dwg.circle(
    center=("50", "50"),
    r="40",
    fill="lightcoral",
    stroke="black",
    stroke_width="2"
)

# Add the circle to the document
dwg.add(circle)

# Save the SVG file
dwg.save()
print("SVG file saved as circle.svg")

# Optional: convert SVG to PNG (export SVG image)
cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

Het uitvoeren van dit script produceert `circle.svg` en, als `cairosvg` geïnstalleerd is, `circle.png`. Beide bestanden zijn klaar voor opname in webpagina's, rapporten, of verdere verwerking.

## Conclusie

Je weet nu hoe je **een SVG-document** in Python kunt **maken**, **SVG naar een bestand kunt opslaan**, en **SVG-afbeeldingen kunt exporteren** voor bredere toepassing. Het voorbeeld behandelt de essentiële API‑aanroepen, legt uit waarom elke stap belangrijk is, en biedt uitbreidingen voor complexere graphics.

Verken vervolgens extra **SVG Python‑tutorials** zoals het tekenen van paden, toepassen van verlopen, en animeren van elementen. Het integreren van deze technieken stelt je in staat om dynamische, data‑gedreven vectorafbeeldingen direct vanuit je Python‑applicaties te genereren. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [SVG-documenten maken en beheren in Aspose.HTML voor Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [SVG-document opslaan in Aspose.HTML voor Java](/html/english/java/saving-html-documents/save-svg-document/)
- [svg naar png java – SVG converteren naar afbeelding met Aspose.HTML voor Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}