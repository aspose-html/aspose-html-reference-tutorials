---
category: general
date: 2026-11-27
description: Skapa ett SVG-dokument och spara SVG-filen med Python. Lär dig att exportera
  vektorgrafik som SVG och snabbt generera en SVG-bild.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG file
- export vector as SVG
- save SVG image
- how to create SVG
language: sv
lastmod: 2026-11-27
og_description: Skapa SVG-dokument och spara SVG-fil med Python. Denna guide visar
  hur du exporterar vektorgrafik som SVG och skapar en SVG-bild på några minuter.
og_image_alt: Screenshot of a red circle saved as an SVG document
og_title: Skapa SVG-dokument och spara SVG-fil med Python
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
title: Skapa SVG-dokument och spara SVG-fil med Python
url: /sv/python/general/create-svg-document-and-save-svg-file-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa SVG-dokument och spara SVG-fil med Python

Om du behöver **create SVG document** från grunden, går den här guiden dig igenom hela processen. Du kommer att se hur du **save SVG file** på disk, exporterar vektorn som SVG, och får en färdig‑att‑använda SVG-bild på bara några rader kod.

Att generera skalbara grafik programatiskt är användbart för rapporter, UI‑ikoner eller någon situation där du vill ha upplösningsoberoende bilder. I slutet av den här handledningen kommer du att kunna svara på “**how to create SVG**?” för enkla former och utöka mönstret till komplexa vektorillustrationer.

## Vad du behöver

- Python 3.8 eller nyare  
- `svgwrite`‑paketet (kan installeras via `pip`)  
- En skrivbar katalog för utdatafilen  

Inga externa grafikredigerare krävs; allt körs från kommandoraden.

## Steg 1: Installera `svgwrite`‑biblioteket

`svgwrite` tillhandahåller ett rent, Python‑likt API för att bygga SVG‑markup. Installera det en gång med:

```bash
pip install svgwrite
```

> **Pro tip:** Använd en virtuell miljö (`python -m venv .venv`) för att hålla beroenden isolerade.

## Steg 2: Skapa SVG-dokument

Nu skapar vi faktiskt **create SVG document**‑objekt. Klassen `Drawing` representerar rot‑elementet `<svg>` och hanterar namnrymder automatiskt.

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

`Drawing`‑instansen är ingångspunkten för alla efterföljande SVG‑operationer. Genom att ange `size` sätter vi canvas‑dimensionerna, vilket påverkar hur webbläsare renderar bilden.

## Steg 3: Lägg till ett rött cirkelelement

Att lägga till former är enkelt. Metoden `circle` skapar ett `<circle>`‑element; vi fäster det sedan på roten.

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

Varför vi väljer en cirkel: cirklar är vektor‑primitiver som demonstrerar skalbarhet utan någon kvalitetsförlust, vilket gör resultatet idealiskt för att testa **export vector as SVG**‑arbetsflöden.

## Steg 4: Spara SVG-fil

Slutligen skriver vi markupen till disk. Detta steg uppfyller kravet **save SVG file** och skapar en fil som du kan öppna i vilken webbläsare eller vektorredigerare som helst.

```python
# Persist the SVG document to the filesystem
dwg.save()
print(f"SVG saved to {output_path.resolve()}")
```

När du kör skriptet kommer du att se ett konsolmeddelande som bekräftar var den genererade filen ligger.

### Förväntad output

Den resulterande `circle.svg` innehåller:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg height="100px" version="1.1" width="100px" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" fill="red"/>
</svg>
```

Att öppna filen i en webbläsare visar en skarp röd cirkel, och eftersom den är vektor‑baserad kan du zooma obegränsat utan pixling.

## Steg 5: Vanliga variationer och kantfall

### Exportera mer komplexa vektorer

Om du behöver **export vector as SVG** för illustrationer med flera former, upprepa helt enkelt `dwg.add()`‑mönstret med andra primitiva (`rect`, `line`, `path`, etc.). Till exempel:

```python
dwg.add(dwg.rect(insert=(10, 10), size=(30, 30), fill="blue"))
dwg.add(dwg.line(start=(0, 0), end=(100, 100), stroke="black", stroke_width=2))
```

### Hantera Unicode och text

SVG stödjer textelement med full Unicode‑stöd. Använd `dwg.text("Hello, 🌍", insert=(5, 95), fill="black")` för att bädda in flerspråkiga etiketter.

### Spara till en annan plats

När du **save SVG image** till en användarspecificerad mapp, validera sökvägen för att undvika behörighetsfel:

```python
if not output_path.parent.exists():
    raise PermissionError(f"Cannot write to {output_path.parent}")
dwg.save()
```

### Minimera outputen

För produktionspipelines kan du vilja ha en mindre filstorlek. Skicka `pretty=False` till `dwg.tostring()` och skriv resultatet manuellt:

```python
minified = dwg.tostring(pretty=False)
output_path.write_text(minified)
```

## Hur man skapar SVG med alternativa bibliotek (valfritt)

Även om `svgwrite` är lättviktigt och ren‑Python, finns andra ekosystem:

- **cairosvg** – konverterar PNG, PDF eller HTML till SVG.  
- **lxml** – låter dig bygga SVG‑markup manuellt med XML‑API:er.  

Valet av bibliotek beror på ditt projekts komplexitet och befintliga beroenden.

## Slutsats

Du vet nu hur man **create SVG document**, lägger till vektorformer och **save SVG file** med Python. Den kompletta lösningen visar stegen för att **export vector as SVG**, generera en **SVG image**, och svara på den vanliga frågan **how to create SVG** programatiskt.

Från här kan du:

- Utöka skriptet med loopar för att automatiskt generera diagram eller ikoner.  
- Integrera SVG‑outputen i webbapplikationer eller e‑postmallar.  
- Utforska animation genom att lägga till `<animate>`‑element med `svgwrite`.

Experimentera med olika former, färger och gradienter för att fullt utnyttja kraften i skalbara vektorgrafik i dina Python‑projekt. Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa SVG-dokument – Lägg till en cirkel och spara som SVG](/html/english/python/general/create-svg-document-add-a-circle-and-save-as-svg/)
- [Skapa SVG-dokument i Python – Guide för att konvertera SVG till PNG](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)
- [Ladda SVG-fil Python – Komplett guide för export, inbäddning & konvertering](/html/english/python/general/load-svg-file-python-complete-guide-to-export-embed-convert/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}