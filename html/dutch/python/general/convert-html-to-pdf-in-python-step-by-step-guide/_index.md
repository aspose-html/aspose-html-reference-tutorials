---
category: general
date: 2026-08-06
description: Converteer HTML naar PDF in Python met een volledig voorbeeld. Leer PDF
  genereren vanuit HTML, HTML opslaan als PDF, en veelvoorkomende randgevallen afhandelen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to pdf
- generate pdf from html
- save html as pdf
- create pdf from html file
- how to convert html to pdf
language: nl
lastmod: 2026-08-06
og_description: Converteer HTML naar PDF in Python en automatiseer documentcreatie.
  Volg deze gids om PDF te genereren vanuit HTML, HTML op te slaan als PDF en de output
  aan te passen.
og_image_alt: Example of convert html to pdf script in Python
og_title: HTML naar PDF converteren in Python – uitgebreide tutorial
schemas:
- author: Aspose
  dateModified: '2026-08-06'
  description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  headline: Convert HTML to PDF in Python – step‑by‑step guide
  type: TechArticle
- description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  name: Convert HTML to PDF in Python – step‑by‑step guide
  steps:
  - name: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
    text: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
  - name: '**Input handling** – read the HTML file or build the markup programmatically.'
    text: '**Input handling** – read the HTML file or build the markup programmatically.'
  - name: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
    text: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
  type: HowTo
tags:
- HTML to PDF
- Python
- Document conversion
title: HTML naar PDF converteren in Python – stapsgewijze handleiding
url: /nl/python/general/convert-html-to-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML naar PDF converteren in Python – stapsgewijze handleiding

Als je snel **HTML naar PDF** wilt converteren, laat deze tutorial een complete oplossing zien in Python. Je zult zien hoe je PDF uit HTML kunt genereren, HTML als PDF kunt opslaan en het conversieproces kunt beheersen zonder je code te verlaten.

De gids leidt je stap voor stap door het installeren van een betrouwbare bibliotheek, het laden van een HTML‑document, het uitvoeren van de conversie en het verifiëren van het resultaat. Aan het einde kun je PDF uit een HTML‑bestand maken in elk Python‑project, of de bron nu een statische pagina of dynamisch gegenereerde markup is.

## Wat je zult leren

* Installeer de `pdfkit`- en `wkhtmltopdf`-afhankelijkheden die nodig zijn voor HTML‑naar‑PDF-conversie.  
* Laad een HTML‑document van schijf of uit een string.  
* Genereer PDF uit HTML met aangepaste paginagrootte, marges en coderingopties.  
* Sla HTML op als PDF met één functie‑aanroep.  
* Behandel typische randgevallen zoals ontbrekende assets, Unicode‑tekens en grote bestanden.  

**Voorwaarden** – Python 3.8+ en basiskennis van bestands‑I/O. Er zijn geen externe services vereist.

## HTML naar PDF converteren – algemeen werkproces

Het conversieproces bestaat uit drie logische fasen:

1. **Voorbereiding** – installeer de converter en zorg ervoor dat de `wkhtmltopdf`‑binary bereikbaar is.  
2. **Invoerafhandeling** – lees het HTML‑bestand of bouw de markup programmatisch op.  
3. **Uitvoergeneratie** – roep de converter aan, schrijf het PDF‑bestand en bevestig het resultaat.

Elke fase wordt hieronder behandeld in een aparte stap.

## Stap 1: Vereiste bibliotheken installeren

`pdfkit` biedt een dunne Python‑wrapper rond de veelgebruikte `wkhtmltopdf`‑engine. Installeer beide met `pip` en controleer het pad naar de binary.

```bash
# Install the Python wrapper
pip install pdfkit

# On Ubuntu/Debian install wkhtmltopdf package
sudo apt-get install wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf
```

Als je een draagbare binary verkiest, download dan de juiste release van de [wkhtmltopdf GitHub‑pagina](https://github.com/wkhtmltopdf/wkhtmltopdf/releases) en plaats deze in een map die aan je `PATH` is toegevoegd. Het script controleert later automatisch het pad.

## Stap 2: Het HTML‑document laden

Je kunt een statisch bestand lezen, externe inhoud ophalen, of HTML dynamisch samenstellen. Het voorbeeld hieronder laadt een lokaal bestand genaamd `sample.html` dat zich bevindt in een door jou opgegeven map.

```python
import pathlib
import pdfkit

# Define the directory that holds the HTML source
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")

# Resolve the full path to the HTML file
html_path = BASE_DIR / "sample.html"

# Read the file content as a UTF‑8 string
with html_path.open(encoding="utf-8") as f:
    html_content = f.read()
```

Het lezen van het bestand als een Unicode‑string zorgt ervoor dat tekens zoals “é”, “ß” of Aziatische glyphs behouden blijven tijdens de conversie. Deze stap is essentieel wanneer je **PDF uit HTML genereert** die internationale tekst bevat.

## Stap 3: PDF genereren uit HTML

`pdfkit.from_string` zet een string met HTML‑markup om in een PDF‑bestand. Je kunt een woordenboek met opties doorgeven om paginagrootte, marges en header/footer‑gedrag te regelen.

```python
# Define the output PDF path
pdf_path = BASE_DIR / "sample.pdf"

# Conversion options – adjust as needed
options = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left": "0.75in",
    "encoding": "UTF-8",
    "enable-local-file-access": None,  # Allows loading local images/CSS
}

# Perform the conversion
pdfkit.from_string(html_content, str(pdf_path), options=options)
```

De bovenstaande aanroep **maakt een PDF uit een HTML‑bestand** dat is opgeslagen als `sample.pdf`. Als de bron‑HTML lokale CSS of afbeeldingen verwijst, laat de `enable‑local‑file‑access`‑vlag `wkhtmltopdf` die bronnen oplossen.

### Waarom deze aanpak werkt

* `pdfkit` delegeert het zware werk aan `wkhtmltopdf`, dat HTML rendert met de WebKit‑engine, waardoor een hoge getrouwheid aan de oorspronkelijke lay-out wordt gegarandeerd.  
* Het aanbieden van een opties‑woordenboek stelt je in staat de output fijn af te stemmen zonder de HTML zelf te wijzigen.  
* Het gebruik van `from_string` houdt de workflow in het geheugen, wat handig is wanneer de HTML dynamisch wordt gegenereerd.

## Stap 4: HTML opslaan als PDF en output verifiëren

Na de conversie wil je mogelijk bevestigen dat de PDF bestaat en leesbaar is. Het fragment hieronder controleert de bestandsgrootte en opent de PDF met de standaard systeemviewer (platform‑specifiek).

```python
import os
import subprocess
import sys

# Verify that the PDF file was created
if pdf_path.is_file() and pdf_path.stat().st_size > 0:
    print(f"✅ PDF generated successfully: {pdf_path}")

    # Open the PDF for visual verification (optional)
    if sys.platform.startswith("darwin"):      # macOS
        subprocess.run(["open", str(pdf_path)])
    elif os.name == "nt":                      # Windows
        os.startfile(str(pdf_path))
    else:                                      # Linux and others
        subprocess.run(["xdg-open", str(pdf_path)])
else:
    raise FileNotFoundError("PDF generation failed – file not found or empty.")
```

Het uitvoeren van het script geeft een succesbericht weer en start de PDF‑viewer zodat je direct kunt bevestigen dat de lay-out overeenkomt met de oorspronkelijke HTML. Deze stap voltooit de **html opslaan als pdf**‑cyclus.

## Stap 5: Geavanceerde opties – PDF maken uit HTML‑bestand met aangepaste instellingen

Soms heb je een fysiek HTML‑bestand op schijf en geef je de voorkeur aan `pdfkit.from_file` in plaats van de inhoud zelf te laden. Deze methode is handig wanneer de HTML al complexe relatieve paden bevat.

```python
# Directly convert a file path to PDF
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

Je kunt ook een voorpagina, inhoudsopgave of JavaScript‑uitvoervlaggen toevoegen door het `options`‑woordenboek uit te breiden. Bijvoorbeeld, om een voorpagina toe te voegen:

```python
options.update({
    "cover": str(BASE_DIR / "cover.html"),
    "toc": None,  # Generates a table of contents
})
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

Deze aanpassingen tonen **hoe je HTML naar PDF converteert** voor meer geavanceerde publicatie‑pijplijnen.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Probleem | Oorzaak | Oplossing |
|----------|---------|-----------|
| Afbeeldingen of CSS worden niet weergegeven | `wkhtmltopdf` blokkeert standaard lokale bestands‑toegang | Voeg `"enable-local-file-access": None` toe aan het opties‑woordenboek |
| Unicode‑tekens worden vervormd | Ontbrekende `encoding`‑optie of bestand gelezen met de verkeerde charset | Stel altijd `"encoding": "UTF-8"` in en lees het HTML‑bestand met UTF‑8 |
| PDF is leeg | Onjuist pad naar `wkhtmltopdf`‑binary | Geef het pad expliciet op: `pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")` |
| Grote HTML‑bestanden veroorzaken time‑out | Standaard time‑out is te kort | Stel `"javascript-delay": "2000"` in of vergroot de time‑out met `"timeout": "60"` |

Het aanpakken van deze problemen zorgt voor een betrouwbaar **pdf‑genereren uit html**‑proces in verschillende omgevingen.

## Volledig script – end‑to‑end voorbeeld

Sla het volgende op als `html_to_pdf.py` en voer het uit met `python html_to_pdf.py`. Pas `YOUR_DIRECTORY` aan zodat het naar je projectmap wijst.

```python
#!/usr/bin/env python3
"""
Convert HTML to PDF in Python – complete, runnable example.
"""

import pathlib
import pdfkit
import os
import subprocess
import sys

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")          # <-- change this
HTML_FILE = BASE_DIR / "sample.html"
PDF_FILE = BASE_DIR / "sample.pdf"

# wkhtmltopdf configuration (optional – only needed if binary is not on PATH)
# config = pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")

# Conversion options – customize as required
OPTIONS = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left":


## Wat je hierna zou moeten leren

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Convert HTML to PDF in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [How to Convert HTML to PDF Java - Set Page Margins with Aspose.HTML](/html/english/java/advanced-usage/css-extensions-adding-title-page-number/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}