---
category: general
date: 2026-10-21
description: Lär dig hur du snabbt konverterar HTML till PNG. Denna handledning täcker
  också export av webbplats till PNG och konvertering av HTML‑fil till PNG med Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to png
- export webpage to png
- how to convert html to image
- convert html file to png
language: sv
lastmod: 2026-10-21
og_description: Konvertera HTML till PNG med Python. Följ den här tydliga guiden för
  att exportera webbsidan till PNG, hantera kantfall och automatisera bildgenerering.
og_image_alt: Screenshot of HTML page converted to PNG using Python
og_title: Konvertera HTML till PNG i Python – komplett programmeringsguide
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
title: Hur man konverterar HTML till PNG i Python – steg‑för‑steg guide
url: /sv/python/general/how-to-convert-html-to-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konvertera HTML till PNG i Python – komplett programmeringsguide

Om du behöver **konvertera HTML till PNG**, visar den här guiden ett pålitligt sätt att göra det med ren Python. Oavsett om du exporterar en statisk rapport, genererar miniatyrbilder för ett galleri eller automatiserar skärmdumpar för testning, får du en komplett, körbar lösning på några minuter.

Du får också se hur du **exporterar en webbsida till PNG**, förstå skillnaden mellan att konvertera en HTML‑fil kontra en live‑URL, och lära dig bästa praxis för att hantera stora sidor eller dynamiskt innehåll. Inga externa tjänster krävs – bara några Python‑paket och ett kort skript.

## Förutsättningar

Innan du börjar, se till att du har:

- Python 3.9+ installerat (koden fungerar på Windows, macOS och Linux)
- Tillgång till en terminal eller kommandoprompt
- Grundläggande kunskap om Pythons paket‑hanterare (`pip`)

Du kommer att behöva paketet `imgkit` (ett tunt omslag runt `wkhtmltoimage`) och själva `wkhtmltoimage`‑binären. Båda är gratis och öppen källkod.

## Steg 1: Installera de nödvändiga verktygen

Det första steget är att installera `wkhtmltoimage` och Python‑omslaget som kommunicerar med den.

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

> **Varför detta steg är viktigt** – `wkhtmltoimage` renderar HTML med WebKit‑motorn och producerar pixel‑perfekta PNG‑filer. `imgkit` vidarebefordrar bara dina alternativ till binären, så du får samma kvalitet som du skulle få från en webbläsare.

## Steg 2: Verifiera installationen

Kör en snabb kontroll för att bekräfta att binären är åtkomlig från Python.

```python
import imgkit

# This will raise an exception if wkhtmltoimage is not found
print("wkhtmltoimage version:", imgkit.config().wkhtmltoimage)
```

Om skriptet skriver ut sökvägen till `wkhtmltoimage` är du redo att konvertera HTML till PNG. Om du får ett `OSError`, dubbelkolla att binären finns i ditt systems `PATH`.

## Steg 3: Skriv en återanvändbar konverteringsfunktion

Att kapsla in logiken i en funktion gör det enkelt att **konvertera HTML‑fil till PNG** eller **exportera webbsida till PNG** från var som helst i ditt projekt.

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

> **Varför vi omsluter både `from_file` och `from_url`** – Samma funktion stödjer nu **hur man konverterar HTML till bild** för lokala filer och live‑webbsidor, vilket håller koden DRY (Don’t Repeat Yourself).

## Steg 4: Konvertera en lokal HTML‑fil till PNG

Placera en HTML‑fil som heter `sample.html` i en mapp som heter `assets`. Anropa sedan hjälpfunktionen vi just definierade:

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

### Förväntad output

När du kör skriptet skrivs följande:

```
✅ Successfully saved PNG to: output/sample.png
```

En ny fil `output/sample.png` innehåller nu en pixel‑perfekt ögonblicksbild av `sample.html`. Att öppna den i någon bildvisare visar den renderade sidan exakt som den skulle visas i en webbläsare.

## Steg 5: Exportera en live‑webbsida till PNG

Om du behöver **exportera webbsida till PNG** för en URL som förändras ofta (t.ex. en instrumentpanel), skicka bara URL‑strängen istället för en filsökväg.

```python
# Example: convert a live page
url = "https://developer.mozilla.org/en-US/docs/Web/HTML"
output_file = "output/mdn_homepage.png"

convert_html_to_png(url, output_file, options={"width": 1920, "height": 1080})
```

### Varför justera viewport‑storlek?

Webbsidor designade för skrivbords­skärmar ser ofta trånga ut om de renderas i en liten bredd. Genom att öka `width`‑ och `height`‑alternativen fångar du hela layouten, vilket är särskilt användbart för **exportera webbsida till PNG**‑uppgifter.

## Steg 6: Hantera vanliga edge‑cases

### 6.1 Stora sidor eller oändlig scroll

För sidor som laddar innehåll lazy (t.ex. oändlig scroll), öka JavaScript‑fördröjningen och sätt eventuellt en större viewport:

```python
options = {
    "javascript-delay": 2000,   # wait 2 seconds for JS to finish
    "width": 1440,
    "height": 3000,             # tall enough for the whole page
    "disable-smart-width": "", # forces the width we set
}
convert_html_to_png(url, "long_page.png", options=options)
```

### 6.2 Autentiserings‑skyddade sidor

Om en sida kräver en sessions‑cookie kan du bädda in cookie‑huvudet:

```python
options = {
    "custom-header": [
        "Cookie: sessionid=YOUR_SESSION_ID"
    ]
}
convert_html_to_png("https://internal.example.com/report", "report.png", options=options)
```

### 6.3 Saknade bilder eller typsnitt

`wkhtmltoimage` respekterar flaggan `--disable-local-file-access` av säkerhetsskäl. Om din HTML refererar till lokala resurser, aktivera dem explicit:

```python
options = {"enable-local-file-access": ""}
convert_html_to_png("assets/complex.html", "complex.png", options=options)
```

## Steg 7: Verifiera resultatet programatiskt (valfritt)

Ibland behöver du bekräfta att PNG‑filen skapades korrekt (t.ex. i CI‑pipelines). Följande kodsnutt kontrollerar filstorlek och dimensioner:

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

Om PNG‑filen klarar dessa kontroller kan du säkert använda den i efterföljande processer såsom PDF‑generering, e‑postbilagor eller maskininlärnings‑pipelines.

## Slutsats

Du har nu en komplett, produktionsklar metod för att **konvertera HTML till PNG** med Python. Guiden täckte:

- Installation av `wkhtmltoimage` och `imgkit`
- Verifiering av miljön
- En återanvändbar `convert_html_to_png`‑funktion som hanterar både lokala filer och URL:er
- Verkliga exempel för **exportera webbsida till PNG**, **hur man konverterar HTML till bild**, och **konvertera HTML‑fil till PNG**
- Edge‑case‑hantering för stora sidor, autentisering och lokala resurser
- Valfria verifieringssteg för CI/CD‑pipelines

Känn dig fri att experimentera med ytterligare `imgkit`‑alternativ – såsom `zoom`, `crop-h` eller `crop-w` – för att finjustera outputen för ditt specifika användningsfall. Som nästa steg kan du utforska:

- Konvertera PNG‑filerna till en PDF‑rapport (`img2pdf`‑biblioteket)
- Automatisera batch‑konvertering av en hel mapp med HTML‑filer
- Använda Selenium för sidor som kräver fullständig webbläsar‑rendering (t.ex. tunga JavaScript‑ramverk)

Lycka till med kodningen, och njut av de pixel‑perfekta skärmdumparna!


## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Convert HTML to PNG – Complete Python Guide](/html/english/python/general/convert-html-to-png-complete-python-guide/)
- [Convert HTML to PNG in Python – Complete Streaming Save Guide](/html/english/python/general/convert-html-to-png-in-python-complete-streaming-save-guide/)
- [Convert SVG to PNG in Python using Aspose.HTML](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}