---
category: general
date: 2026-06-16
description: Hur man snabbt ändrar storlek på SVG i Python – ladda SVG‑fil i Python,
  redigera SVG‑fil i Python, och till och med batch‑ändra storlek på SVG‑filer med
  ett litet skript.
draft: false
keywords:
- how to resize svg
- batch resize svg files
- load svg file python
- edit svg file python
language: sv
og_description: Hur man ändrar storlek på SVG i Python? Lär dig att ladda SVG-filer
  i Python, redigera SVG-filer i Python och batch‑ändra storlek på SVG-filer med ett
  tydligt, körbart exempel.
og_title: Hur man ändrar storlek på SVG i Python – Komplett handledning
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
title: Hur man ändrar storlek på SVG i Python – Steg‑för‑steg‑guide
url: /sv/python/general/how-to-resize-svg-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man ändrar storlek på SVG i Python – Komplett handledning

Har du någonsin undrat **how to resize SVG** utan att öppna ett grafikprogram? Kanske har du en logotyp som måste vara 200 px bred för en webbannons, eller så förbereder du dussintals ikoner för en mobilapp. Den goda nyheten? Du kan göra allt i Python—ingen Photoshop, ingen Inkscape‑UI, bara några rader kod.

I den här guiden går vi igenom hur man laddar en SVG‑fil i Python, redigerar dess dimensioner och till och med skalar en hel mapp med SVG‑filer på en gång. I slutet kommer du att kunna **load SVG file Python**, **edit SVG file Python**, och **batch resize SVG files** med självförtroende.

## Förutsättningar

- Python 3.8+ installerat (kommandot `python` fungerar som standard)
- Biblioteket `svgwrite` eller `lxml` – vi använder `lxml` eftersom det ger direkt DOM‑åtkomst.
- En mapp med SVG‑filer som du vill ändra storlek (t.ex. `assets/icons/`)

Du behöver inga GUI‑verktyg; allt körs från terminalen.

---

## Steg 1: Installera det nödvändiga biblioteket

Först, hämta `lxml` från PyPI. Det är litet, snabbt och låter oss manipulera XML‑attribut direkt.

```bash
pip install lxml
```

> **Pro tip:** Om du arbetar i en virtuell miljö, aktivera den innan du kör kommandot. Detta håller dina projektberoenden prydliga.

## Steg 2: Ladda en SVG‑fil i Python

Nu kommer vi att **load SVG file Python**‑stil—läsa XML‑filen, hämta rot‑elementet `<svg>` och skriva ut dess aktuella storlek.

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

**Varför detta är viktigt:** `lxml` ger oss ett riktigt DOM, så vi kan fråga eller ändra vilket attribut som helst—perfekt för **edit SVG file Python**‑uppgifter.

## Steg 3: Ändra bredden (och höjden) – How to Resize SVG

SVG‑filer är vektorgrafik, så du kan ange antingen bredd, höjd eller båda. Om du bara ändrar bredden behåller viewBox förhållandet, men många verktyg respekterar också ett matchande höjd‑attribut. Här är en hjälpfunktion som ändrar storlek samtidigt som den bevarar det ursprungliga bildförhållandet:

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

Funktionen ovan är kärnan i **how to resize SVG**. Den läser den aktuella storleken, beräknar en proportionell höjd och skriver tillbaka de nya attributen till filen.

## Steg 4: Spara den modifierade SVG‑filen

Efter redigering måste du skriva tillbaka ändringarna till disk. Detta slutför **edit SVG file Python**‑cykeln.

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

Kör hela skriptet så får du en ny `logo_resized.svg` som är exakt 200 px bred.

## Steg 5: Batch‑ändra storlek på SVG‑filer – Skala en hel mapp

Nu när vi kan **load SVG file Python**, **edit SVG file Python** och spara den, låt oss loopa över en katalog och tillämpa samma transformation på varje fil. Detta är svaret på **batch resize SVG files**.

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

### Vad detta gör:

1. **Collects** varje `.svg`‑fil i källmappen.
2. **Loads** varje fil med samma rutin som vi använde för en enskild SVG.
3. **Resizes** till önskad bredd samtidigt som bildförhållandet behålls.
4. **Writes** resultatet till en ny mapp, utan att röra originalen.

Du har nu en färdig‑till‑användning pipeline för **batch resize SVG files**.

## Steg 6: Edge Cases & Common Pitfalls

| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| Saknade `width`/`height`‑attribut | Vissa SVG‑filer förlitar sig enbart på `viewBox`. | Om attributen saknas, falla tillbaka på viewBox‑dimensionerna (`viewBox="0 0 w h"`). |
| Enheter annat än `px` (t.ex. `pt`, `%`) | Skriptet tar bara bort `px`. | Utöka `replace`‑anropet eller använd ett regex för att fånga vilken enhet som helst. |
| Komplexa `<symbol>`‑ eller `<use>`‑element | Att ändra storlek på roten påverkar kanske inte inbäddade symboler. | Applicera samma attributändringar på varje `<symbol>`‑tagg, eller använd CSS `transform: scale()`. |
| Unicode‑ eller specialtecken i filnamn | `pathlib` hanterar de flesta fall, men Windows kan ha problem med vissa tecken. | Se till att filnamn är UTF‑8‑säkra, eller byt namn innan bearbetning. |

## Steg 7: Verifiera resultatet

En snabb kontroll kan göras med ett litet HTML‑snutt:

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

Öppna filen i en webbläsare—båda bilderna bör se identiska ut, men den ändrade bilden kommer att rapportera en bredd på **200 px** i utvecklarverktygen.

---

## Slutsats

Du vet nu **how to resize SVG** med ren Python, från en enskild fil till en hel katalog. Arbetsflödet täcker **load SVG file Python**, **edit SVG file Python**, och **batch resize SVG files**—allt med bara ett fåtal funktioner.

Prova det: testa olika bredder, experimentera med endast höjd‑ändring, eller lägg till ett kommandoradsgränssnitt med `argparse`. Möjligheterna är oändliga, och skriptet är så lätt att det kan bäddas in i byggpipelines, CI‑jobb eller skrivbordsverktyg.

Har du frågor om hantering av gradienter, inbäddade typsnitt, eller integration i en Flask‑app? Lämna en kommentar så utforskar vi de områdena tillsammans. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Aspose.HTML के साथ .NET में SVG को इमेज में बदलें](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [Aspose.HTML के साथ .NET में SVG को PDF में बदलें](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-pdf/)
- [Aspose.HTML के साथ .NET में SVG दस्तावेज़ को PNG के रूप में प्रस्तुत करें](/html/hindi/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}