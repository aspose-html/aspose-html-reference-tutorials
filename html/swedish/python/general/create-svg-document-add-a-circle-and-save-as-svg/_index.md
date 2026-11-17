---
category: general
date: 2026-07-31
description: Lär dig hur du skapar ett SVG-dokument, lägger till en cirkel och sparar
  SVG-filen snabbt. Exportera grafik som SVG med några få rader Python‑kod.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg document
- save svg file
- export graphic as svg
- add circle to svg
language: sv
lastmod: 2026-07-31
og_description: Skapa SVG-dokument, lägg till en cirkel och spara SVG-filen på några
  sekunder. Den här guiden visar hur du exporterar grafik som SVG med tydlig, körbar
  kod.
og_image_alt: Screenshot of a red circle inside an SVG file named circle.svg
og_title: Skapa SVG-dokument – Lägg till en cirkel och spara som SVG
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
title: Skapa SVG-dokument – Lägg till en cirkel och spara som SVG
url: /sv/python/general/create-svg-document-add-a-circle-and-save-as-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa SVG-dokument – Lägg till en cirkel och spara som SVG

Har du någonsin behövt **create SVG document** från kod men varit osäker på var du ska börja? Du är inte ensam; många utvecklare stöter på den muren när de först provar på vektorgrafik. I den här handledningen går vi igenom ett litet, självständigt exempel som visar hur du **add circle to SVG**, sedan **save SVG file** så att du kan **export graphic as SVG** för användning på webben eller i designverktyg.

Vi håller det lättviktigt: bara några rader Python, ett populärt SVG‑hjälpbibliotek och en liten förklaring. I slutet har du en färdig `circle.svg` i din mapp, och du förstår varför varje steg är viktigt—utan vaga “see docs”-genvägar.

## Vad du behöver

- Python 3.8+ (någon nyare version fungerar)
- Paketet `svgwrite` – installera det med `pip install svgwrite`
- En textredigerare eller IDE (VS Code, PyCharm, eller till och med Notepad räcker)
- Skrivbehörighet till den katalog där du vill spara filen

Det är allt. Inga tunga beroenden, inga externa tjänster.

## Steg 1: Ställ in SVG-dokumentet

Att skapa ett SVG-dokument är lika enkelt som att instansiera ett `Drawing`‑objekt från `svgwrite`. Tänk på detta objekt som den tomma canvasen där varje form lever.

```python
import svgwrite

# Step 1: Create a new SVG document (canvas) 800×800 pixels
dwg = svgwrite.Drawing(filename="circle.svg", size=("200px", "200px"))
```

> **Varför detta är viktigt:** `Drawing`‑klassen hanterar all XML‑boilerplate åt dig—namnrymder, rubriker och rot‑elementet `<svg>`. Genom att ange ett filnamn i förväg vet vi redan var filen hamnar, vilket gör det senare **save svg file**‑steget trivialt.

### Proffstips
Om du planerar att generera många filer i en loop, ge varje `Drawing` ett unikt namn eller använd `io.BytesIO` för att hålla allt i minnet tills du är redo att skriva.

## Steg 2: Lägg till en cirkel i SVG

Nu när dokumentet finns, låt oss **add circle to SVG**. Metoden `add()` accepterar vilket formobjekt som helst; en `Circle` är perfekt för en enkel röd prick i mitten.

```python
# Step 2: Add a red circle element to the SVG root
center = (100, 100)          # x, y coordinates (half of 200px canvas)
radius = 80                  # radius in pixels
circle = dwg.circle(center=center, r=radius, fill='red')
dwg.add(circle)
```

> **Varför vi använder variablerna `center` och `radius`:** Att hårdkoda siffror gör koden svårare att läsa och underhålla. Genom att namnge värdena klargör vi avsikten—denna cirkel sitter mitt i en 200 × 200‑canvas och är tillräckligt stor för att märkas.

### Edge case – Transparent bakgrund
Om du behöver en transparent bakgrund (standard för SVG) kan du hoppa över att sätta ett `fill` på roten. För en vit bakgrund, lägg till:

```python
dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))
```

Placera detta innan du lägger till cirkeln så att rektangeln ligger under.

## Steg 3: Spara SVG-filen

Med formen på plats är sista steget att **save SVG file**. Metoden `save()` skriver XML till disk, och eftersom vi redan har gett `Drawing` ett filnamn räcker ett enda anrop.

```python
# Step 3: Save the SVG document to a file
dwg.save()
print("✅ circle.svg has been created in the current directory.")
```

> **Vad händer under huven?** `svgwrite` serialiserar elementträdet till en sträng, lägger till XML‑deklarationen och skriver den med UTF‑8‑kodning. Om mål‑katalogen inte finns, kommer Python att kasta ett `FileNotFoundError`; se till att sökvägen är giltig eller skapa den med `os.makedirs()`.

### Bonus: Exportera grafik som SVG programatiskt
Om du behöver SVG‑innehållet som en sträng—till exempel för att bädda in det i ett HTML‑mail—kan du anropa `dwg.tostring()` istället för `save()`:

```python
svg_content = dwg.tostring()
# Now you can send svg_content over a network, store it in a DB, etc.
```

## Fullständigt fungerande exempel

Sätter ihop allt, här är ett komplett, färdigt att köra‑skript:

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

**Förväntat resultat:** Efter att ha kört skriptet ser du en `circle.svg`‑fil i samma mapp. Att öppna den i en webbläsare eller någon vektorredigerare visar en röd cirkel centrerad på en vit ruta—precis vad vi programmerade.

## Vanliga frågor & fallgropar

- **What if I want a different shape?** Byt `dwg.circle` mot `dwg.rect`, `dwg.ellipse` eller till och med en anpassad `<path>`‑sträng. API‑et är konsekvent över former.
- **Can I embed the SVG directly in HTML?** Absolut. Filen du just skapade kan refereras med `<img src="circle.svg" alt="Red circle">` eller inbäddas med `<svg>`‑taggar.
- **Why not write raw XML?** Du skulle kunna, men bibliotek som `svgwrite` hanterar namnrymds‑nyanser och gör koden mycket mer underhållbar—särskilt när du börjar lägga till gradienter eller animationer.

## Slutsats

Du vet nu hur du **create SVG document**, **add circle to SVG**, och **save SVG file** så att du kan **export graphic as SVG** med bara ett fåtal Python‑rader. Mönstret skalar: ersätt cirkeln med vilken vektorform som helst, loopa över data för att generera diagram, eller batch‑processa resurser för ett designsystem.

Nästa steg? Prova att lägga till textetiketter, experimentera med gradienter, eller generera ett helt galleri av ikoner i ett enda skript. Om du är nyfiken på mer avancerade funktioner, kolla in `svgwrite`‑dokumentationen om grupper (`<g>`), transformationer och animationsstöd.

Lycka till med kodandet, och må dina vektorer alltid förbli skarpa!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}