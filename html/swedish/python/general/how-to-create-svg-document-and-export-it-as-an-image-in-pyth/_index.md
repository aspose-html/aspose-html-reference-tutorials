---
category: general
date: 2026-10-02
description: Lär dig hur du skapar SVG-dokument i Python, sparar SVG till fil och
  exporterar SVG-bilden med ett kort, komplett skript.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG to file
- how to generate SVG
- export SVG image
- SVG Python tutorial
language: sv
lastmod: 2026-10-02
og_description: Skapa SVG-dokument i Python och exportera SVG-bilden med den här praktiska
  handledningen. Följ skriptet, spara SVG till fil och återanvänd vektorgrafiken omedelbart.
og_image_alt: Screenshot of a Python script that creates an SVG document
og_title: Skapa SVG-dokument i Python – steg‑för‑steg guide
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
title: Hur man skapar SVG-dokument och exporterar det som en bild i Python
url: /sv/python/general/how-to-create-svg-document-and-export-it-as-an-image-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så skapar du SVG-dokument och exporterar det som en bild i Python

Om du behöver **skapa SVG-dokument** programatiskt, visar den här handledningen exakt hur du gör det med Python. Du kommer att se ett komplett skript som bygger en enkel cirkel, sparar SVG-filen, och producerar en exportbar SVG-bild som du kan bädda in var som helst.

Att generera skalbara vektorgrafik från kod tar bort det manuella arbetet med att rita former i en GUI-redigerare. I slutet av den här guiden kan du integrera SVG-skapande i data‑visualiserings‑pipelines, automatiska rapportgeneratorer eller vilket projekt som helst som kräver skarpa, upplösningsoberoende grafik.

## Förutsättningar

- Python 3.8 eller nyare installerat
- Biblioteket `svgwrite` (installera med `pip install svgwrite`)
- Skrivbehörighet till den katalog där SVG-filen kommer att sparas

Dessa krav håller exemplet lättviktigt och kompatibelt med de flesta miljöer.

## Steg 1: Installera och importera SVG-biblioteket

Det första steget är att lägga till det tredjepartsbibliotek som erbjuder ett bekvämt API för SVG-skapande.

```python
# Install the library (run once in your terminal)
# pip install svgwrite

import svgwrite  # Provides the SVGDocument class and element helpers
```

`svgwrite` abstraherar XML‑strukturen i en SVG‑fil, så att du kan fokusera på geometri istället för rå markup.

## Steg 2: Skapa ett SVG-dokumentobjekt

Nu kan du **skapa SVG-dokument** genom att instansiera `svgwrite.Drawing`. Detta objekt representerar rot‑elementet `<svg>` och innehåller alla efterföljande former.

```python
# Step 2: Initialize the SVG document
dwg = svgwrite.Drawing(
    filename="circle.svg",     # Desired output file name
    size=("100px", "100px"),   # Width and height of the canvas
    viewBox=("0 0 100 100")    # Coordinate system for drawing
)
```

`size`‑argumentet definierar de renderade pixelmåtten, medan `viewBox` etablerar ett koordinatsystem som matchar den geometri du kommer att definiera senare.

## Steg 3: Lägg till ett cirkelelement

En cirkel definieras av dess centrum (`cx`, `cy`) och radie (`r`). Använd `circle`‑hjälpen för att tilldela dessa attribut.

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

Cirkeln sitter i mitten av en 100 × 100‑canvas, med en marginal på 10 pixlar på varje sida. Justera `fill` och `stroke` för att matcha ditt design‑språk.

## Steg 4: Spara SVG till fil

När grafiken är sammansatt kan du **spara SVG till fil** med `save`‑metoden. Detta skriver välformad XML som webbläsare och vektorredigerare förstår.

```python
# Step 4: Persist the SVG document
dwg.save()
print("SVG file saved as circle.svg")
```

Filen `circle.svg` finns nu i den aktuella arbetskatalogen. Du kan öppna den i en webbläsare, Inkscape eller vilket verktyg som helst som stödjer SVG‑formatet.

## Steg 5: Verifiera den exporterade SVG‑bilden

Öppna den sparade filen i en webbläsare för att bekräfta resultatet. Du bör se en centrerad cirkel med de angivna färgerna. Den råa XML‑koden ser ut så här:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg width="100px" height="100px" viewBox="0 0 100 100"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40"
          fill="lightcoral" stroke="black" stroke-width="2"/>
</svg>
```

Eftersom SVG är vektorbaserat kan du skala bilden utan kvalitetsförlust, vilket gör den idealisk för responsiv webbdesign eller högupplöst tryck.

## Proffstips: Exportera SVG som PNG eller JPEG

Om du behöver en rasterversion, kombinera SVG‑filen med ett konverteringsverktyg som **CairoSVG**:

```python
# Optional: Convert SVG to PNG
# pip install cairosvg
import cairosvg

cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

Detta steg demonstrerar **exportera SVG‑bild** till ett bitmapformat, användbart när nedströms system inte kan rendera SVG direkt.

## Vanliga variationer och kantfall

| Variation | Hur man hanterar |
|-----------|------------------|
| Flera former | Anropa `dwg.add()` för varje nytt element (rect, line, path). |
| Dynamiska dimensioner | Beräkna `size` och `viewBox` från data innan du skapar `Drawing`. |
| Textetiketter | Använd `dwg.text("Label", insert=("10", "20"))` och stilisera med `font_size` och `fill`. |
| Återanvända dokumentet | Behåll `Drawing`‑objektet i minnet och anropa `save()` när du behöver en uppdaterad fil. |
| Stora filer | Strömma utdata med `dwg.tostring()` och skriv till ett filobjekt manuellt för att undvika minnesspikar. |

Att hantera dessa scenarier säkerställer att ditt **how to generate SVG**‑skript skalar från enkla ikoner till komplexa diagram.

## Fullständig skriptöversikt

Nedan är det kompletta, körbara exemplet som inkluderar alla steg och valfri konvertering:

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

## Slutsats

Du vet nu hur du **skapar SVG-dokument** i Python, **sparar SVG till fil**, och **exporterar SVG-bild** för bredare användning. Exemplet täcker de väsentliga API‑anropen, förklarar varför varje steg är viktigt, och erbjuder utökningar för mer komplex grafik.

Nästa steg är att utforska ytterligare **SVG Python tutorial**‑ämnen som att rita banor, applicera gradienter och animera element. Att integrera dessa tekniker låter dig generera dynamisk, datadriven vektorgrafik direkt från dina Python‑applikationer. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa och hantera SVG-dokument i Aspose.HTML för Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [Spara SVG-dokument i Aspose.HTML för Java](/html/english/java/saving-html-documents/save-svg-document/)
- [svg till png java – Konvertera SVG till bild med Aspose.HTML för Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}