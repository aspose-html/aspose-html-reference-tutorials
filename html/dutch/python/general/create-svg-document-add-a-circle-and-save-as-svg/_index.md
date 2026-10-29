---
category: general
date: 2026-07-31
description: Leer hoe je een SVG‑document maakt, een cirkel toevoegt en snel een SVG‑bestand
  opslaat. Exporteer de afbeelding als SVG met een paar regels Python‑code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg document
- save svg file
- export graphic as svg
- add circle to svg
language: nl
lastmod: 2026-07-31
og_description: Maak een SVG‑document, voeg een cirkel toe en sla het SVG‑bestand
  binnen enkele seconden op. Deze gids laat zien hoe je een afbeelding exporteert
  als SVG met duidelijke, uitvoerbare code.
og_image_alt: Screenshot of a red circle inside an SVG file named circle.svg
og_title: Maak een SVG‑document – Voeg een cirkel toe en sla op als SVG
schemas:
- author: Aspose
  dateModified: '2026-07-31'
  description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  headline: Create SVG Document – Add a Circle and Save as SVG
  type: TechArticle
- description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  name: Create SVG Document – Add a Circle and Save as SVG
  steps:
  - name: Pro tip
    text: If you plan to generate many files in a loop, give each `Drawing` a unique
      name or use `io.BytesIO` to keep everything in memory until you’re ready to
      write.
  - name: Edge case – Transparent background
    text: 'If you need a transparent background (the default for SVG), you can skip
      setting a `fill` on the root. For a white background, add:'
  - name: 'Bonus: Export graphic as SVG programmatically'
    text: 'If you need the SVG content as a string—for example, to embed it in an
      HTML email—you can call `dwg.tostring()` instead of `save()`:'
  type: HowTo
- questions:
  - answer: Swap `dwg.circle` for `dwg.rect`, `dwg.ellipse`, or even a custom `<path>`
      string. The API is consistent across shapes.
    question: What if I want a different shape?
  - answer: Absolutely. The file you just created can be referenced with `<img src="circle.svg"
      alt="Red circle">` or inlined with `<svg>` tags.
    question: Can I embed the SVG directly in HTML?
  - answer: You could, but libraries like `svgwrite` handle namespace quirks and make
      the code far more maintainable—especially when you start adding gradients or
      animations.
    question: Why not write raw XML?
  type: FAQPage
tags:
- svg
- python
- vector-graphics
- programming-tutorial
title: SVG-document maken – Voeg een cirkel toe en sla op als SVG
url: /nl/python/general/create-svg-document-add-a-circle-and-save-as-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak SVG-document – Voeg een cirkel toe en sla op als SVG

Heb je ooit **create SVG document** nodig gehad vanuit code maar wist je niet waar je moest beginnen? Je bent niet alleen; veel ontwikkelaars lopen tegen die muur aan wanneer ze voor het eerst met vectorafbeeldingen spelen. In deze tutorial lopen we een klein, zelfstandig voorbeeld door dat je laat zien hoe je **add circle to SVG** kunt doen, vervolgens **save SVG file** zodat je **export graphic as SVG** kunt gebruiken op het web of in ontwerptools.

We houden het lichtgewicht: slechts een paar regels Python, een populaire SVG‑helperbibliotheek, en een vleugje uitleg. Aan het einde heb je een kant‑klaar `circle.svg` in je map, en begrijp je waarom elke stap belangrijk is—geen vage “see docs” shortcuts.

## Wat je nodig hebt

- Python 3.8+ (elke recente versie werkt)
- Het `svgwrite`‑pakket – installeer het met `pip install svgwrite`
- Een teksteditor of IDE (VS Code, PyCharm, of zelfs Notepad volstaat)
- Schrijfrechten voor de map waarin je het bestand wilt opslaan

Dat is alles. Geen zware afhankelijkheden, geen externe services.

## Stap 1: Maak het SVG-document

Het maken van een SVG-document is zo simpel als het instantieren van een `Drawing`‑object uit `svgwrite`. Beschouw dit object als het lege canvas waarop elke vorm leeft.

```python
import svgwrite

# Step 1: Create a new SVG document (canvas) 800×800 pixels
dwg = svgwrite.Drawing(filename="circle.svg", size=("200px", "200px"))
```

> **Waarom dit belangrijk is:** De `Drawing`‑klasse behandelt al het XML‑boilerplate voor je—namespaces, headers en het root‑element `<svg>`. Door vooraf een bestandsnaam op te geven weten we al waar het bestand terechtkomt, waardoor de latere **save svg file**‑stap triviaal wordt.

### Pro‑tip
Als je van plan bent om veel bestanden in een lus te genereren, geef elk `Drawing` een unieke naam of gebruik `io.BytesIO` om alles in het geheugen te houden totdat je klaar bent om te schrijven.

## Stap 2: Voeg een cirkel toe aan de SVG

Nu het document bestaat, laten we **add circle to SVG**. De `add()`‑methode accepteert elk vormobject; een `Circle` is perfect voor een eenvoudige rode stip in het midden.

```python
# Step 2: Add a red circle element to the SVG root
center = (100, 100)          # x, y coordinates (half of 200px canvas)
radius = 80                  # radius in pixels
circle = dwg.circle(center=center, r=radius, fill='red')
dwg.add(circle)
```

> **Waarom we `center`‑ en `radius`‑variabelen gebruiken:** Hard‑coded getallen maken de code moeilijker leesbaar en onderhoudbaar. Door de waarden een naam te geven verduidelijken we de intentie—deze cirkel zit precies in het midden van een 200 × 200 canvas en is groot genoeg om op te vallen.

### Randgeval – Transparante achtergrond
Als je een transparante achtergrond nodig hebt (de standaard voor SVG), kun je het instellen van een `fill` op het root‑element overslaan. Voor een witte achtergrond, voeg toe:

```python
dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))
```

Plaats dit vóór het toevoegen van de cirkel zodat het rechthoek eronder zit.

## Stap 3: Sla het SVG‑bestand op

Met de vorm op zijn plaats, is de laatste handeling om **save SVG file**. De `save()`‑methode schrijft de XML naar schijf, en omdat we het `Drawing` al een bestandsnaam hebben gegeven, doet één aanroep het werk.

```python
# Step 3: Save the SVG document to a file
dwg.save()
print("✅ circle.svg has been created in the current directory.")
```

> **Wat er onder de motorkap gebeurt:** `svgwrite` serialiseert de elementboom naar een string, voegt de XML‑declaratie toe, en schrijft deze met UTF‑8‑codering. Als de doelmap niet bestaat, zal Python een `FileNotFoundError` werpen; zorg dat het pad geldig is of maak het aan met `os.makedirs()`.

### Bonus: Exporteer grafiek als SVG programmatisch

Als je de SVG‑inhoud als string nodig hebt—bijvoorbeeld om in een HTML‑e‑mail in te sluiten—kun je `dwg.tostring()` aanroepen in plaats van `save()`:

```python
svg_content = dwg.tostring()
# Now you can send svg_content over a network, store it in a DB, etc.
```

## Volledig werkend voorbeeld

Alles samenvoegend, hier is een compleet, kant‑klaar script:

```python
import svgwrite
import os

def create_svg_with_circle(output_path: str):
    """
    Creates an SVG file containing a single red circle.
    Parameters
    ----------
    output_path: str
        Full path where the SVG file will be saved.
    """
    # Ensure the directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Initialise the SVG document (800×800 canvas)
    dwg = svgwrite.Drawing(filename=output_path, size=("200px", "200px"))

    # Optional: add a white background rectangle
    dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))

    # Add a red circle in the centre
    center = (100, 100)
    radius = 80
    circle = dwg.circle(center=center, r=radius, fill='red')
    dwg.add(circle)

    # Save the file – this is the key step to **save svg file**
    dwg.save()
    print(f"✅ SVG saved to {output_path}")

if __name__ == "__main__":
    # Change this path to wherever you want the file
    output_file = os.path.join(os.getcwd(), "circle.svg")
    create_svg_with_circle(output_file)
```

**Verwachte output:** Na het uitvoeren van het script zie je een `circle.svg`‑bestand in dezelfde map. Het openen in een browser of een vector‑editor toont een rode cirkel gecentreerd op een wit vierkant—precies wat we geprogrammeerd hebben.

## Veelgestelde vragen & valkuilen

- **Wat als ik een andere vorm wil?** Vervang `dwg.circle` door `dwg.rect`, `dwg.ellipse`, of zelfs een aangepaste `<path>`‑string. De API is consistent over vormen.
- **Kan ik de SVG direct in HTML insluiten?** Zeker. Het bestand dat je zojuist hebt gemaakt kan worden gerefereerd met `<img src="circle.svg" alt="Red circle">` of inline met `<svg>`‑tags.
- **Waarom geen ruwe XML schrijven?** Je zou het kunnen, maar bibliotheken zoals `svgwrite` behandelen namespace‑eigenaardigheden en maken de code veel beter onderhoudbaar—vooral wanneer je begint met het toevoegen van verlopen of animaties.

## Conclusie

Je weet nu hoe je **create SVG document**, **add circle to SVG**, en **save SVG file** kunt doen zodat je **export graphic as SVG** kunt uitvoeren met slechts een handvol Python‑regels. Het patroon schaalt: vervang de cirkel door elke vectorvorm, loop over data om grafieken te genereren, of batch‑verwerk assets voor een designsysteem.

Volgende stappen? Probeer tekstlabels toe te voegen, te experimenteren met verlopen, of een hele galerij iconen te genereren in één script. Als je nieuwsgierig bent naar meer geavanceerde functies, bekijk dan de `svgwrite`‑documentatie over groepen (`<g>`), transformaties en animatie‑ondersteuning.

Veel plezier met coderen, en moge je vectoren altijd scherp blijven!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [SVG-document opslaan in Aspose.HTML voor Java](/html/english/java/saving-html-documents/save-svg-document/)
- [SVG-documenten maken en beheren in Aspose.HTML voor Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg naar png java – SVG naar afbeelding converteren met Aspose.HTML voor Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}