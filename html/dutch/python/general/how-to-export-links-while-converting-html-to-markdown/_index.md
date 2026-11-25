---
category: general
date: 2026-08-22
description: Hoe links uit HTML te exporteren en deze om te zetten naar een markdown‑bestand,
  inclusief alinea’s. Stapsgewijze handleiding voor HTML‑naar‑markdown conversie.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export links
- convert html to markdown
- how to convert html
- how to extract paragraphs
- html to markdown file
language: nl
lastmod: 2026-08-22
og_description: Hoe je links uit een HTML‑document exporteert en converteert naar
  een markdown‑bestand, inclusief alinea’s. Volg deze volledige tutorial voor betrouwbare
  HTML‑naar‑markdown conversie.
og_image_alt: How to export links while converting HTML to Markdown
og_title: Hoe links exporteren tijdens het converteren van HTML naar Markdown – stapsgewijze
  handleiding
schemas:
- author: GroupDocs
  dateModified: '2026-08-22'
  description: How to export links from HTML and convert it to a markdown file, including
    paragraphs. Step‑by‑step guide for HTML to markdown conversion.
  headline: How to export links while converting HTML to Markdown
  type: TechArticle
tags:
- HTML conversion
- Markdown
- Python
title: Hoe links exporteren tijdens het converteren van HTML naar Markdown
url: /nl/python/general/how-to-export-links-while-converting-html-to-markdown/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe links exporteren tijdens het converteren van HTML naar Markdown

Als je **links exporteren** van een HTML‑pagina en het resultaat wilt omzetten naar een schoon **html‑naar‑markdown‑bestand**, laat deze gids je de exacte stappen zien. Je ontdekt ook **alinea's extraheren** zodat de markdown‑output de hoofdinhoud bevat waar je om geeft. Aan het einde van de tutorial kun je de vraag “**hoe html te converteren** naar markdown” beantwoorden met een kant‑klaar script.

Links exporteren en alinea's extraheren zijn veelvoorkomende taken wanneer je webinhoud migreert naar statische sites, documentatieportalen of headless CMS‑back‑ends. De onderstaande aanpak werkt met de GroupDocs Conversion SDK voor Python, maar de concepten zijn toepasbaar op elke bibliotheek die je toestaat exportfuncties te configureren.

---

## Wat je nodig hebt

- Python 3.9 of nieuwer  
- `groupdocs-conversion`‑pakket (installeren met `pip install groupdocs-conversion`)  
- Een HTML‑bestand dat je wilt verwerken (bijv. `input.html`)  
- Basiskennis van Python‑scripting  

---

## Hoe links exporteren met HTML‑naar‑Markdown‑conversie

De eerste belangrijke stap is het configureren van de conversie zodat alleen de gewenste functies—links en alinea's—worden weggeschreven naar het **html‑naar‑markdown‑bestand**. De SDK laat je een bitmask van `MarkdownFeature`‑waarden instellen; we combineren `LINKS` en `PARAGRAPHS` om de output gefocust te houden.

```python
# Import the required classes from the GroupDocs Conversion SDK
from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeature, Converter

# Step 1: Load the source HTML document
html_doc = HTMLDocument("YOUR_DIRECTORY/input.html")

# Step 2: Create Markdown save options and select the features to export
markdown_options = MarkdownSaveOptions()
# Export only links and paragraphs from the HTML
markdown_options.features = MarkdownFeature.LINKS | MarkdownFeature.PARAGRAPHS

# Step 3: Convert the HTML to Markdown using the configured options
output_path = "YOUR_DIRECTORY/links_and_paragraphs.md"
Converter.convert(html_doc, markdown_options, output_path)

print(f"Conversion complete. Markdown saved to {output_path}")
```

### Waarom dit werkt

- **`HTMLDocument`** parseert het originele bestand en bouwt een DOM op die de converter kan doorlopen.  
- **`MarkdownSaveOptions`** geeft je fijnmazige controle over wat de SDK schrijft. Het instellen van `features` op `LINKS | PARAGRAPHS` vertelt de engine om afbeeldingen, tabellen of scripts te negeren, wat ruis in het uiteindelijke **html‑naar‑markdown‑bestand** vermindert.  
- **`Converter.convert`** voert het zware werk uit. Het respecteert het feature‑masker, extraheert anker‑tags (`<a>`) en alinea‑tags (`<p>`), en schrijft ze met de standaard Markdown‑syntaxis.

---

## Hoe HTML naar Markdown te converteren met volledige inhoud (optioneel)

Als je later besluit dat je de volledige pagina nodig hebt—niet alleen links en alinea's—pas dan eenvoudig het feature‑masker aan:

```python
# Export everything the SDK supports (links, paragraphs, images, tables, etc.)
markdown_options.features = MarkdownFeature.ALL
```

Het uitvoeren van dezelfde conversie levert nu een compleet **html‑naar‑markdown‑bestand** op dat de oorspronkelijke lay-out weerspiegelt. Dit toont **hoe html te converteren** op een flexibele manier: je beheert de output door feature‑flags te schakelen.

---

## Hoe alleen alinea's extraheren

Soms ben je alleen geïnteresseerd in de tekstuele inhoud van een artikel, niet in de hyperlinks. Je kunt alinea's isoleren door het masker uitsluitend op `PARAGRAPHS` te zetten:

```python
markdown_options.features = MarkdownFeature.PARAGRAPHS
output_path = "YOUR_DIRECTORY/only_paragraphs.md"
Converter.convert(html_doc, markdown_options, output_path)
```

De resulterende markdown zal schone, regel‑gebroken tekst bevatten zonder enige link‑opmaak. Deze snippet beantwoordt de vraag **hoe alinea's te extraheren** uit een HTML‑bron.

---

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|----------|
| Leeg uitvoerbestand | De bron‑HTML bevat geen `<a>`‑ of `<p>`‑tags die overeenkomen met de geselecteerde functies. | Controleer de HTML‑structuur of breid het feature‑masker uit (bijv. `HEADINGS` opnemen). |
| Coderingproblemen | De HTML gebruikt een niet‑UTF‑8‑tekenset en de SDK leest deze onjuist. | Geef een expliciete codering door aan `HTMLDocument`, bijv. `HTMLDocument(path, encoding="iso-8859-1")`. |
| Bestaande markdown overschrijven | Het script meerdere keren uitvoeren vervangt het vorige bestand. | Voeg een tijdstempel toe aan de output‑bestandsnaam of controleer `os.path.exists` vóór het schrijven. |

**Pro tip:** Bij het verwerken van veel bestanden in een map, wikkel de conversielogica in een lus en log elk resultaat. Dit geeft je een duidelijk audit‑pad en maakt het eenvoudig om na een fout te hervatten.

---

## Volledig script dat je kunt copy‑pasten

Hieronder staat een zelfstandige Python‑file (`convert_links_paragraphs.py`) die je direct kunt uitvoeren. Het bevat argument‑parsing zodat je invoer‑ en uitvoer‑paden kunt opgeven zonder de code te bewerken.

```python
#!/usr/bin/env python3
"""
convert_links_paragraphs.py

A complete example that shows how to export links and extract paragraphs
when converting HTML to a markdown file using GroupDocs Conversion SDK.
"""

import argparse
import os
from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeature, Converter

def convert_html_to_md(input_html: str, output_md: str, features: int) -> None:
    """Perform the conversion with the given feature mask."""
    if not os.path.isfile(input_html):
        raise FileNotFoundError(f"Input file not found: {input_html}")

    # Load the HTML document
    html_doc = HTMLDocument(input_html)

    # Configure markdown options
    md_options = MarkdownSaveOptions()
    md_options.features = features

    # Run the conversion
    Converter.convert(html_doc, md_options, output_md)
    print(f"✅ Conversion finished – markdown saved to: {output_md}")

def main() -> None:
    parser = argparse.ArgumentParser(
        description="How to export links while converting HTML to Markdown."
    )
    parser.add_argument("input", help="Path to the source HTML file.")
    parser.add_argument(
        "output",
        help="Path for the resulting markdown file (e.g., links_and_paragraphs.md).",
    )
    parser.add_argument(
        "--links",
        action="store_true",
        help="Include links in the markdown output.",
    )
    parser.add_argument(
        "--paragraphs",
        action="store_true",
        help="Include paragraphs in the markdown output.",
    )
    args = parser.parse_args()

    # Build the feature mask based on user flags
    selected_features = 0
    if args.links:
        selected_features |= MarkdownFeature.LINKS
    if args.paragraphs:
        selected_features |= MarkdownFeature.PARAGRAPHS

    # Default to both links and paragraphs if no flag is provided
    if selected_features == 0:
        selected_features = MarkdownFeature.LINKS | MarkdownFeature.PARAGRAPHS

    try:
        convert_html_to_md(args.input, args.output, selected_features)
    except Exception as exc:
        print(f"❌ Conversion failed: {exc}")

if __name__ == "__main__":
    main()
```

**Hoe uit te voeren**

```bash
python convert_links_paragraphs.py YOUR_DIRECTORY/input.html YOUR_DIRECTORY/links_and_paragraphs.md --links --paragraphs
```

Het bovenstaande commando demonstreert **links exporteren** en **alinea's extraheren** in één enkele oproep. Laat `--links` of `--paragraphs` weg om de output aan te passen aan je behoeften.

---

## Verificatie – hoe de output eruitziet

Gegeven de volgende eenvoudige HTML (`input.html`):

```html
<!DOCTYPE html>
<html>
<head><title>Sample page</title></head>
<body>
  <p>Welcome to the tutorial.</p>
  <p>Visit <a href="https://example.com">our site</a> for more info.</p>
</body>
</html>
```

Het uitvoeren van het script met beide vlaggen produceert `links_and_paragraphs.md`:

```markdown
Welcome to the tutorial.

Visit [our site](https://example.com) for more info.
```

Je ziet dat alleen de twee alinea's en de hyperlink aanwezig zijn—precies wat je vroeg toen je zocht naar **links exporteren** tijdens het uitvoeren van **html naar markdown converteren**.

---

## Volgende stappen en gerelateerde onderwerpen

- **Hoe html naar markdown te converteren** met afbeeldingen: voeg `MarkdownFeature.IMAGES` toe aan het masker.  
- **Hoe alinea's te extraheren** en vervolgens post‑processen  

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe offset in te stellen bij het converteren van HTML naar Markdown in Java](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)
- [Markdown naar HTML Java - Converteren met Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)
- [HTML naar Markdown converteren – Complete C#‑gids](/html/english/java/conversion-html-to-other-formats/convert-html-to-markdown-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}