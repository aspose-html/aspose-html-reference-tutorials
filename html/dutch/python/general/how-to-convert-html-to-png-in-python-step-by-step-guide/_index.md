---
category: general
date: 2026-10-21
description: Leer hoe je HTML snel naar PNG kunt converteren. Deze tutorial behandelt
  ook het exporteren van een webpagina naar PNG en het converteren van een HTML‑bestand
  naar PNG met Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to png
- export webpage to png
- how to convert html to image
- convert html file to png
language: nl
lastmod: 2026-10-21
og_description: Converteer HTML naar PNG met Python. Volg deze duidelijke gids om
  een webpagina naar PNG te exporteren, randgevallen af te handelen en het genereren
  van afbeeldingen te automatiseren.
og_image_alt: Screenshot of HTML page converted to PNG using Python
og_title: HTML naar PNG converteren in Python – volledige programmeergids
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  headline: How to convert HTML to PNG in Python – step‑by‑step guide
  type: TechArticle
- description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  name: How to convert HTML to PNG in Python – step‑by‑step guide
  steps:
  - name: Expected output
    text: 'Running the script prints:'
  - name: Why adjust viewport size?
    text: Web pages designed for desktop screens often look cramped if rendered at
      a small width. By increasing the `width` and `height` options, you capture the
      full layout, which is especially useful for **export webpage to PNG** tasks.
  - name: 6.1 Large pages or infinite scroll
    text: 'For pages that load content lazily (e.g., infinite scroll), increase the
      JavaScript delay and optionally set a larger viewport:'
  - name: 6.2 Authentication‑protected pages
    text: 'If a page requires a session cookie, you can embed the cookie header:'
  - name: 6.3 Missing images or fonts
    text: '`wkhtmltoimage` respects the `--disable-local-file-access` flag for security.
      If your HTML references local assets, enable them explicitly:'
  type: HowTo
tags:
- python
- html conversion
- image processing
- web automation
title: Hoe HTML naar PNG te converteren in Python – stapsgewijze handleiding
url: /nl/python/general/how-to-convert-html-to-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML naar PNG converteren in Python – volledige programmeergids

Als je **HTML naar PNG wilt converteren**, laat deze gids je een betrouwbare manier zien om dit te doen met gewone Python. Of je nu een statisch rapport exporteert, miniaturen voor een galerij genereert, of screenshots automatiseert voor testen, je krijgt binnen enkele minuten een volledige, uitvoerbare oplossing.

Je ziet ook hoe je **webpagina naar PNG exporteert**, begrijpt het verschil tussen het converteren van een HTML‑bestand versus een live‑URL, en leert de beste praktijken voor het omgaan met grote pagina's of dynamische content. Er zijn geen externe services nodig—alleen een paar Python‑pakketten en een kort script.

## Vereisten

- Python 3.9+ geïnstalleerd (de code werkt op Windows, macOS en Linux)
- Toegang tot een terminal of opdrachtprompt
- Basiskennis van de pakketbeheerder van Python (`pip`)

Je hebt het `imgkit`‑pakket nodig (een dunne wrapper rond `wkhtmltoimage`) en de `wkhtmltoimage`‑binary zelf. Beide zijn gratis en open‑source.

## Stap 1: Installeer de vereiste tools

De eerste stap is om `wkhtmltoimage` en de Python‑wrapper die ermee communiceert te installeren.

```bash
# Install wkhtmltoimage (Linux example)
sudo apt-get update && sudo apt-get install -y wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf

# On Windows download the installer from:
# https://wkhtmltopdf.org/downloads.html
# and add the installation folder to your PATH.

# Install the Python wrapper
pip install imgkit
```

> **Waarom deze stap belangrijk is** – `wkhtmltoimage` rendert HTML met de WebKit‑engine, waardoor pixel‑perfecte PNG's worden geproduceerd. `imgkit` stuurt simpelweg je opties door naar de binary, zodat je dezelfde kwaliteit krijgt als in een browser.

## Stap 2: Verifieer de installatie

Voer een snelle controle uit om te bevestigen dat de binary bereikbaar is vanuit Python.

```python
import imgkit

# This will raise an exception if wkhtmltoimage is not found
print("wkhtmltoimage version:", imgkit.config().wkhtmltoimage)
```

Als het script het pad naar `wkhtmltoimage` afdrukt, ben je klaar om HTML naar PNG te converteren. Als je een `OSError` krijgt, controleer dan nogmaals of de binary in je systeem‑`PATH` staat.

## Stap 3: Schrijf een herbruikbare conversiefunctie

Het encapsuleren van de logica in een functie maakt het eenvoudig om **HTML‑bestand naar PNG te converteren** of **webpagina naar PNG te exporteren** vanuit elke plek in je project.

```python
import os
import imgkit

def convert_html_to_png(source, output_path, *, options=None):
    """
    Convert an HTML file or URL to a PNG image.

    Parameters
    ----------
    source : str
        Path to a local HTML file (e.g., "report.html") or a URL
        (e.g., "https://example.com").
    output_path : str
        Destination file path for the PNG (e.g., "report.png").
    options : dict, optional
        imgkit options such as viewport size, zoom factor, or
        JavaScript delay. If omitted, sensible defaults are used.

    Returns
    -------
    bool
        True if the conversion succeeded, False otherwise.
    """
    # Use a default set of options if none are provided
    default_options = {
        "format": "png",
        "quality": "100",
        "encoding": "UTF-8",
        "quiet": "",
        # Render at 1280×720 – adjust for your layout
        "width": 1280,
        "height": 720,
        # Wait for JavaScript to finish (ms)
        "javascript-delay": 500,
    }
    # Merge user‑supplied options over defaults
    final_options = {**default_options, **(options or {})}

    try:
        # imgkit can handle both files and URLs transparently
        imgkit.from_file(source, output_path, options=final_options) \
            if os.path.isfile(source) else \
            imgkit.from_url(source, output_path, options=final_options)
        print(f"✅ Successfully saved PNG to: {output_path}")
        return True
    except Exception as e:
        print(f"❌ Conversion failed: {e}")
        return False
```

> **Waarom we zowel `from_file` als `from_url` omhullen** – Dezelfde functie ondersteunt nu **hoe je HTML naar afbeelding converteert** voor lokale bestanden en live webpagina's, waardoor je code DRY (Don’t Repeat Yourself) blijft.

## Stap 4: Converteer een lokaal HTML‑bestand naar PNG

Plaats een HTML‑bestand genaamd `sample.html` in een map genaamd `assets`. Roep vervolgens de helper aan die we zojuist hebben gedefinieerd:

```python
if __name__ == "__main__":
    # Example: convert a static HTML file
    html_path = os.path.join("assets", "sample.html")
    png_path = os.path.join("output", "sample.png")

    # Ensure the output directory exists
    os.makedirs(os.path.dirname(png_path), exist_ok=True)

    # Perform the conversion
    success = convert_html_to_png(html_path, png_path)

    if success:
        # Show a tiny preview in the console (optional)
        from PIL import Image
        img = Image.open(png_path)
        img.thumbnail((200, 200))
        img.show()
```

### Verwachte output

Het uitvoeren van het script drukt af:

```
✅ Successfully saved PNG to: output/sample.png
```

Een nieuw bestand `output/sample.png` bevat nu een pixel‑perfecte snapshot van `sample.html`. Het openen in een willekeurige afbeeldingsviewer toont de gerenderde pagina precies zoals deze in een browser zou verschijnen.

## Stap 5: Exporteer een live webpagina naar PNG

Als je een **webpagina naar PNG wilt exporteren** voor een URL die vaak verandert (bijv. een dashboard), geef dan gewoon de URL‑string door in plaats van een bestandspad.

```python
# Example: convert a live page
url = "https://developer.mozilla.org/en-US/docs/Web/HTML"
output_file = "output/mdn_homepage.png"

convert_html_to_png(url, output_file, options={"width": 1920, "height": 1080})
```

### Waarom de viewport‑grootte aanpassen?

Webpagina's die voor desktopschermen zijn ontworpen, zien er vaak krap uit als ze op een kleine breedte worden gerenderd. Door de `width`‑ en `height`‑opties te verhogen, leg je de volledige lay-out vast, wat vooral nuttig is voor **webpagina naar PNG export** taken.

## Stap 6: Afhandelen van veelvoorkomende randgevallen

### 6.1 Grote pagina's of oneindig scrollen

Voor pagina's die inhoud lui laden (bijv. oneindig scrollen), verhoog je de JavaScript‑vertraging en stel je eventueel een grotere viewport in:

```python
options = {
    "javascript-delay": 2000,   # wait 2 seconds for JS to finish
    "width": 1440,
    "height": 3000,             # tall enough for the whole page
    "disable-smart-width": "", # forces the width we set
}
convert_html_to_png(url, "long_page.png", options=options)
```

### 6.2 Authenticatie‑beveiligde pagina's

Als een pagina een sessie‑cookie vereist, kun je de cookie‑header insluiten:

```python
options = {
    "custom-header": [
        "Cookie: sessionid=YOUR_SESSION_ID"
    ]
}
convert_html_to_png("https://internal.example.com/report", "report.png", options=options)
```

### 6.3 Ontbrekende afbeeldingen of lettertypen

`wkhtmltoimage` respecteert de `--disable-local-file-access`‑vlag voor veiligheid. Als je HTML verwijst naar lokale assets, schakel deze dan expliciet in:

```python
options = {"enable-local-file-access": ""}
convert_html_to_png("assets/complex.html", "complex.png", options=options)
```

## Stap 7: Verifieer het resultaat programmatisch (optioneel)

Soms moet je bevestigen dat de PNG correct is gegenereerd (bijv. in CI‑pipelines). Het volgende fragment controleert de bestandsgrootte en afmetingen:

```python
from pathlib import Path
from PIL import Image

def verify_png(path):
    p = Path(path)
    if not p.is_file():
        raise FileNotFoundError(f"{path} does not exist")
    if p.stat().st_size < 10_000:  # arbitrary minimal size
        raise ValueError("Generated PNG seems too small")
    with Image.open(p) as img:
        print(f"Image size: {img.width}×{img.height}, mode: {img.mode}")

verify_png(png_path)
```

Als de PNG deze controles doorstaat, kun je deze veilig gebruiken in downstream‑processen zoals PDF‑generatie, e‑mailbijlagen, of machine‑learning‑pipelines.

## Conclusie

Je hebt nu een volledige, productie‑klare methode om **HTML naar PNG te converteren** met Python. De gids behandelde:

- Het installeren van `wkhtmltoimage` en `imgkit`
- Het verifiëren van de omgeving
- Een herbruikbare `convert_html_to_png`‑functie die zowel lokale bestanden als URL's afhandelt
- Praktijkvoorbeelden voor **webpagina naar PNG export**, **hoe je HTML naar afbeelding converteert**, en **HTML‑bestand naar PNG converteren**
- Afhandeling van randgevallen voor grote pagina's, authenticatie en lokale assets
- Optionele verificatiestappen voor CI/CD‑pipelines

Voel je vrij om te experimenteren met extra `imgkit`‑opties—zoals `zoom`, `crop-h` of `crop-w`—om de output af te stemmen op jouw specifieke gebruikssituatie. Voor de volgende stappen kun je het volgende verkennen:

- De PNG's omzetten naar een PDF‑rapport (`img2pdf`‑bibliotheek)
- Het automatiseren van batch‑conversie van een volledige map met HTML‑bestanden
- Selenium gebruiken voor pagina's die volledige browser‑rendering vereisen (bijv. zware JavaScript‑frameworks)

Veel plezier met coderen, en geniet van de pixel‑perfecte screenshots!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [HTML naar PNG converteren – Complete Python‑gids](/html/english/python/general/convert-html-to-png-complete-python-guide/)
- [HTML naar PNG converteren in Python – Complete Streaming Save‑gids](/html/english/python/general/convert-html-to-png-in-python-complete-streaming-save-guide/)
- [SVG naar PNG converteren in Python met Aspose.HTML](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}