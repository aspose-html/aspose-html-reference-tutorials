---
category: general
date: 2026-07-02
description: Maak snel een SVG‑document met Python. Leer hoe je een SVG‑bestand opslaat,
  een basis‑SVG‑afbeelding genereert en SVG vanuit code exporteert in slechts een
  paar regels.
draft: false
keywords:
- create svg document
- save svg file
- how to generate svg
- export svg from code
- create basic svg image
language: nl
og_description: Maak eenvoudig een SVG‑document. Deze gids laat zien hoe je SVG genereert,
  een SVG‑bestand opslaat en SVG exporteert vanuit code met een helder Python‑voorbeeld.
og_title: Maak SVG-document – Snelle Python‑tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Create SVG document quickly with Python. Learn to save SVG file, generate
    a basic SVG image, and export SVG from code in just a few lines.
  headline: Create SVG Document – Step‑by‑Step Guide for Beginners
  type: TechArticle
- description: Create SVG document quickly with Python. Learn to save SVG file, generate
    a basic SVG image, and export SVG from code in just a few lines.
  name: Create SVG Document – Step‑by‑Step Guide for Beginners
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: How can I add text or other shapes?
    text: Just call `svg.create_element("text", {...})` or `svg.create_element("circle",
      {...})` and append them just like the rectangle. The same **how to generate
      SVG** logic applies.
  - name: What if I need to **export SVG from code** with a transparent background?
    text: Remove any `fill` attribute from the root `<svg>` element or set `fill="none"`
      on shapes that should be transparent. The XML stays valid; browsers will render
      the transparency automatically.
  - name: Can I **save SVG file** with pretty‑printed formatting?
    text: '`ElementTree` writes compact XML by default. For a human‑readable version,
      you can use `xml.dom.minidom` to re‑format:'
  - name: What about performance for large SVGs?
    text: When generating thousands of elements, consider building a list of `ET.Element`
      objects first and then extending the root in one go. This reduces the number
      of tree mutations and speeds up the **save SVG file** operation.
  type: HowTo
tags:
- SVG
- Python
- Graphics
- File I/O
title: SVG-document maken – Stapsgewijze gids voor beginners
url: /nl/python/general/create-svg-document-step-by-step-guide-for-beginners/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SVG-document maken – Stapsgewijze handleiding voor beginners

Heb je je ooit afgevraagd hoe je **SVG-document kunt maken** zonder een grafische editor te openen? Je bent niet de enige. Of je nu een klein pictogram voor een webpagina nodig hebt of een dynamische grafiek die on‑the‑fly wordt gegenereerd, het kunnen **SVG-document maken** via code bespaart tijd en houdt alles versie‑gecontroleerd.

In deze tutorial lopen we een compleet, uitvoerbaar voorbeeld door dat je precies laat zien hoe je **SVG-document kunt maken**, **SVG-bestand kunt opslaan**, en zelfs de blijvende “**hoe SVG te genereren**” vraag beantwoordt die opduikt wanneer je grafische afbeeldingen automatiseert. Aan het einde heb je een rood vierkant op schijf, en weet je hoe je **SVG vanuit code kunt exporteren** voor elk toekomstig project.

## Wat je nodig hebt

* Python 3.9 of nieuwer (de standaardbibliotheek doet al het zware werk)
* Een teksteditor of IDE die je prettig vindt — VS Code, PyCharm, of zelfs Notepad volstaat
* Schrijfrechten voor een map waarin je **SVG-bestand opslaat** (we gebruiken een `output/` map)

Er zijn geen externe pakketten nodig, dus de installatie duurt letterlijk een paar minuten.

## Stap 1: De SVG-hulpfuncties instellen (Document maken)

Allereerst: we hebben een kleine helper nodig die de XML-structuur achter een SVG opbouwt. Beschouw dit als het canvas waarop we later **basis‑SVG‑afbeelding maken** elementen zullen **maken**.

```python
import pathlib
import xml.etree.ElementTree as ET

# ----------------------------------------------------------------------
# Helper class that mimics a minimal SVG library.
# ----------------------------------------------------------------------
class SVGDocument:
    """Simple wrapper to generate an SVG document using ElementTree."""
    
    SVG_NS = "http://www.w3.org/2000/svg"
    def __init__(self, width: int = 200, height: int = 200):
        # Register the SVG namespace so the output looks clean
        ET.register_namespace("", self.SVG_NS)
        self.root = ET.Element(
            "svg",
            attrib={
                "xmlns": self.SVG_NS,
                "width": str(width),
                "height": str(height),
                "version": "1.1"
            }
        )
    
    def create_element(self, tag: str, attributes: dict) -> ET.Element:
        """Create an SVG element with the given attributes."""
        return ET.Element(tag, attrib=attributes)
    
    def append_child(self, element: ET.Element):
        """Append a child element to the root <svg> node."""
        self.root.append(element)
    
    def save(self, file_path: str):
        """Write the SVG XML to a file, creating directories as needed."""
        path = pathlib.Path(file_path)
        path.parent.mkdir(parents=True, exist_ok=True)
        tree = ET.ElementTree(self.root)
        tree.write(str(path), encoding="utf-8", xml_declaration=True)
```

**Waarom deze stap belangrijk is:** De `SVGDocument`‑klasse abstraheert het low‑level XML‑geklungel. Door het in een klasse te wikkelen houden we de rest van de code schoon, wat een best practice is wanneer je **SVG vanuit code exporteert** in grotere applicaties.

## Stap 2: Een rechthoek toevoegen – De kern van een **basis‑SVG‑afbeelding maken** voorbeeld

Nu we een documentobject hebben, laten we een rood vierkant toevoegen. Dit is de kern van het **basis‑SVG‑afbeelding maken** gedeelte van de tutorial.

```python
# ----------------------------------------------------------------------
# Step 2: Build the SVG content
# ----------------------------------------------------------------------
svg = SVGDocument(width=120, height=120)   # canvas size a little larger than the square

# Define rectangle attributes: 100x100 size, red fill, positioned at (10,10)
rect_attrs = {
    "x": "10",
    "y": "10",
    "width": "100",
    "height": "100",
    "fill": "red"
}

# Create the <rect> element and attach it to the SVG root
rect_element = svg.create_element("rect", rect_attrs)
svg.append_child(rect_element)
```

**Uitleg:**  
* De `x`‑ en `y`‑coördinaten van de rechthoek geven een marge van 10 pixel zodat hij niet direct tegen de rand zit.  
* Het gebruik van een dictionary voor attributen maakt de code leesbaar en weerspiegelt hoe je **SVG-bestand opslaat** attributen in elk XML‑gebaseerd formaat.  
* Als je ooit **hoe SVG te genereren** vormen nodig hebt die geen rechthoeken zijn, wijzig dan simpelweg de tag naar `"circle"` of `"path"` en pas de attributendictionary dienovereenkomstig aan.

## Stap 3: De SVG behouden – Uiteindelijk **SVG-bestand opslaan** naar schijf

We hebben het document in het geheugen opgebouwd; nu schrijven we het weg. Dit is het moment waarop het abstracte **SVG-document maken** een tastbaar bestand wordt dat je in een browser kunt openen.

```python
# ----------------------------------------------------------------------
# Step 3: Persist the SVG to the filesystem
# ----------------------------------------------------------------------
output_path = "output/square.svg"
svg.save(output_path)

print(f"✅ SVG saved! Open {output_path} in any browser to see the red square.")
```

**Wat je zult zien:** Het openen van `output/square.svg` in Chrome, Firefox of een andere SVG‑ondersteunende viewer toont een eenvoudig rood vierkant met een dunne witte rand (de achtergrond van het SVG‑canvas). Dat bewijst dat we succesvol **SVG vanuit code hebben geëxporteerd**.

## Volledig script – Eén‑bestand oplossing

Hieronder staat het volledige script, klaar om te kopiëren‑en‑plakken in `create_svg.py`. Het uitvoeren van `python create_svg.py` genereert het hierboven beschreven bestand.

```python
import pathlib
import xml.etree.ElementTree as ET

class SVGDocument:
    """Simple wrapper to generate an SVG document using ElementTree."""
    SVG_NS = "http://www.w3.org/2000/svg"
    def __init__(self, width: int = 200, height: int = 200):
        ET.register_namespace("", self.SVG_NS)
        self.root = ET.Element(
            "svg",
            attrib={
                "xmlns": self.SVG_NS,
                "width": str(width),
                "height": str(height),
                "version": "1.1"
            }
        )
    def create_element(self, tag: str, attributes: dict) -> ET.Element:
        return ET.Element(tag, attrib=attributes)
    def append_child(self, element: ET.Element):
        self.root.append(element)
    def save(self, file_path: str):
        path = pathlib.Path(file_path)
        path.parent.mkdir(parents=True, exist_ok=True)
        tree = ET.ElementTree(self.root)
        tree.write(str(path), encoding="utf-8", xml_declaration=True)

# -------------------- Build the SVG --------------------
svg = SVGDocument(width=120, height=120)

rect_attrs = {
    "x": "10",
    "y": "10",
    "width": "100",
    "height": "100",
    "fill": "red"
}
svg.append_child(svg.create_element("rect", rect_attrs))

# -------------------- Save the file --------------------
output_path = "output/square.svg"
svg.save(output_path)

print(f"✅ SVG saved! Open {output_path} in any browser to see the red square.")
```

### Verwachte output

Het uitvoeren van het script geeft het volgende weer:

```
✅ SVG saved! Open output/square.svg in any browser to see the red square.
```

En de gegenereerde `square.svg` ziet er als volgt uit (vereenvoudigde weergave):

```xml
<?xml version='1.0' encoding='utf-8'?>
<svg xmlns="http://www.w3.org/2000/svg" width="120" height="120" version="1.1">
  <rect x="10" y="10" width="100" height="100" fill="red" />
</svg>
```

Het openen van het bestand rendert een scherp rood vierkant — precies wat we wilden **basis‑SVG‑afbeelding maken**.

## Voorbeeld uitbreiden – Veelgestelde vragen beantwoord

### Hoe kan ik tekst of andere vormen toevoegen?

Roep gewoon `svg.create_element("text", {...})` of `svg.create_element("circle", {...})` aan en voeg ze toe net als de rechthoek. Dezelfde **hoe SVG te genereren** logica is van toepassing.

### Wat als ik **SVG vanuit code moet exporteren** met een transparante achtergrond?

Verwijder elk `fill`‑attribuut van het root‑element `<svg>` of stel `fill="none"` in voor vormen die transparant moeten zijn. De XML blijft geldig; browsers renderen de transparantie automatisch.

### Kan ik **SVG-bestand opslaan** met mooi‑geformatteerde weergave?

`ElementTree` schrijft standaard compacte XML. Voor een mens‑leesbare versie kun je `xml.dom.minidom` gebruiken om opnieuw te formatteren:

```python
import xml.dom.minidom as minidom

def pretty_save(svg_doc, path):
    rough_string = ET.tostring(svg_doc.root, 'utf-8')
    reparsed = minidom.parseString(rough_string)
    with open(path, 'w', encoding='utf-8') as f:
        f.write(reparsed.toprettyxml(indent="  "))
```

Vervang `svg.save(output_path)` door `pretty_save(svg, output_path)`.

### Hoe zit het met de prestaties voor grote SVG's?

Bij het genereren van duizenden elementen, overweeg eerst een lijst van `ET.Element`‑objecten te bouwen en vervolgens de root in één keer uit te breiden. Dit vermindert het aantal boommutaties en versnelt de **SVG-bestand opslaan** operatie.

## Pro‑tips & valkuilen

* **Pro tip:** Gebruik altijd absolute paden (of `pathlib.Path`) wanneer je **SVG-bestand opslaat**; relatieve paden kunnen breken wanneer je script vanuit een andere werkmap wordt uitgevoerd.  
* **Let op:** Het vergeten te registreren van de SVG‑namespace. Zonder `ET.register_namespace("", SVGDocument.SVG_NS)` bevat de output een overbodige `ns0`‑prefix die sommige browsers verkeerd interpreteren.  
* **Typische fout:** Het mengen van gehele getallen en strings in attribuutwaarden. XML verwacht strings, dus we casten alles met `str()` — de hulpprogrammaclasse doet dit voor je, maar als je het omzeilt, kun je een `TypeError` krijgen.  

## Conclusie

We hebben zojuist een compleet, end‑to‑end voorbeeld doorlopen dat laat zien hoe je **SVG-document maakt**, **SVG-bestand opslaat**, en beantwoordt

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}