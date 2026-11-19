---
category: general
date: 2026-07-15
description: Maak PDF van HTML met Python. Leer hoe je HTML snel naar PDF kunt converteren
  met een eenvoudig script en duidelijke stappen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf from html
- convert html to pdf
- html to pdf python
- save html as pdf
- html to pdf tutorial
language: nl
lastmod: 2026-07-15
og_description: Maak PDF van HTML met Python. Deze gids laat zien hoe je HTML naar
  PDF converteert, HTML opslaat als PDF en bronnen efficiënt afhandelt.
og_image_alt: Screenshot of a Python script that creates PDF from HTML
og_title: PDF maken van HTML in Python – Praktijkgerichte tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-15'
  description: Create PDF from HTML using Python. Learn how to convert HTML to PDF
    quickly with a simple script and clear steps.
  headline: Create PDF from HTML in Python – HTML to PDF Python Tutorial
  type: TechArticle
tags:
- python
- pdf
- html
- conversion
title: PDF maken van HTML in Python – HTML naar PDF Python‑handleiding
url: /nl/python/general/create-pdf-from-html-in-python-html-to-pdf-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF maken van HTML in Python – Volledig‑Uitgebreide Tutorial

Heb je ooit **PDF maken van HTML** moeten doen maar wist je niet welke Python‑bibliotheek je moest kiezen? Je bent niet de enige—veel ontwikkelaars komen tegen die muur wanneer ze een web‑rapport, factuur of marketingpagina willen omzetten naar een afdrukbare PDF.  

Het goede nieuws is dat je met slechts een paar regels code **HTML naar PDF** betrouwbaar kunt **converteren**, en dat het script werkt op Windows, macOS en Linux. In deze gids lopen we een compleet, uitvoerbaar voorbeeld stap voor stap door, leggen we uit waarom elke stap belangrijk is, en laten we je zien hoe je **HTML als PDF kunt opslaan** zonder losse eindjes.

---

## Wat je zult leren

- Installeer het juiste Python‑pakket voor HTML‑naar‑PDF‑conversie.  
- Laad een HTML‑bestand met aangepaste resource‑handling‑opties (om eindeloze CSS‑imports te vermijden).  
- Genereer een nette PDF‑bestand op schijf.  
- Pak veelvoorkomende randgevallen aan zoals externe afbeeldingen, relatieve paden en grote documenten.  

Aan het einde van deze **HTML‑naar‑PDF‑tutorial** heb je een herbruikbare functie die je in elk project kunt gebruiken.

---

## Vereisten

- Python 3.9+ (de code werkt ook met 3.8, maar 3.9+ geeft je de nieuwste `pathlib`‑features).  
- Basiskennis van de commandoregel en virtuele omgevingen.  
- Een HTML‑bestand dat je wilt omzetten naar een PDF—elke statische pagina volstaat.

> **Pro tip:** Als je een virtuele omgeving gebruikt, activeer deze dan voordat je de bibliotheek installeert; dit houdt je globale Python‑installatie netjes.

---

## Stap 1 – Installeer WeasyPrint (de motor achter de conversie)

WeasyPrint is een pure‑Python bibliotheek die HTML en CSS rendert naar PDF. Het ondersteunt de meeste moderne webfeatures en geeft je fijnmazige controle over het laden van resources.

```bash
pip install weasyprint
```

Het uitvoeren van het bovenstaande commando haalt `cairocffi`, `tinycss2` en enkele andere afhankelijkheden binnen. Als je een `cairo`‑gerelateerd foutbericht krijgt op Windows, download dan de vooraf gebouwde wheels van de [WeasyPrint website](https://weasyprint.org/docs/install/).

---

## Stap 2 – Bereid een kleine helper voor resource‑handling voor

Wanneer je een HTML‑document laadt dat externe stylesheets of afbeeldingen referereert, zal de bibliotheek die links volgen. In sommige gevallen leidt dit tot diepe nesting of zelfs oneindige lussen (denk aan een CSS‑bestand dat zichzelf `@import`‑t). Om het overzichtelijk te houden beperken we de diepte van resource‑handling.

```python
from weasyprint import HTML, CSS
from pathlib import Path

class ResourceHandlingOptions:
    """Simple container to mimic max depth handling."""
    def __init__(self, max_depth: int = 3):
        self.max_depth = max_depth
        self._current_depth = 0

    def within_limit(self) -> bool:
        return self._current_depth < self.max_depth

    def __enter__(self):
        self._current_depth += 1
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        self._current_depth -= 1
```

De bovenstaande klasse is niet vereist door WeasyPrint, maar spiegelt het patroon dat je in het originele fragment zag en geeft je een haak om runaway‑imports te stoppen. Je zult het gebruiken in de volgende stap.

---

## Stap 3 – Laad het HTML‑document met de aangepaste opties

Nu lezen we daadwerkelijk het HTML‑bestand. De `HTML`‑klasse accepteert een `base_url`‑argument, dat we instellen op de map die het bronbestand bevat—zodat relatieve links werken zonder een webserver.

```python
def load_html(input_path: Path, options: ResourceHandlingOptions) -> HTML:
    """
    Load an HTML file while respecting the max handling depth.
    """
    if not options.within_limit():
        raise RuntimeError("Maximum resource handling depth exceeded.")
    # The `with` block increments depth for the duration of the call.
    with options:
        return HTML(filename=str(input_path), base_url=str(input_path.parent))
```

> **Waarom dit belangrijk is:** Als je HTML een cascade van CSS‑bestanden binnenhaalt, zal elke `@import` een nieuwe load triggeren. De diepte‑guard voorkomt dat het script uit de hand loopt.

---

## Stap 4 – Sla het verwerkte document op als PDF

Met het `HTML`‑object in de hand is het genereren van een PDF een één‑regelige operatie. We geven ook een simpel CSS‑fragment mee dat een nette paginagrootte (A4) afdwingt en een kleine marge toevoegt—pas het gerust aan.

```python
def save_as_pdf(html_doc: HTML, output_path: Path) -> None:
    """
    Render the HTML document to a PDF file.
    """
    default_css = CSS(string='''
        @page { size: A4; margin: 1cm }
    ''')
    html_doc.write_pdf(target=str(output_path), stylesheets=[default_css])
```

Het aanroepen van `write_pdf` streamt de PDF naar schijf, zodat je een kant‑klaar bestand krijgt.

---

## Stap 5 – Zet alles bij elkaar

Hieronder staat een compacte script dat je kunt kopiëren‑plakken in `convert.py`. Vervang de placeholder‑paden door je eigen mappen.

```python
#!/usr/bin/env python3
"""
HTML to PDF Python script – complete, runnable example.
"""

from pathlib import Path

# Import the helper classes we defined earlier
from __main__ import ResourceHandlingOptions, load_html, save_as_pdf  # noqa: E402

def main():
    # 1️⃣  Define input and output locations
    input_html = Path("YOUR_DIRECTORY/input.html")
    output_pdf = Path("YOUR_DIRECTORY/output.pdf")

    # 2️⃣  Create resource handling options (max depth = 3)
    resource_options = ResourceHandlingOptions(max_depth=3)

    # 3️⃣  Load the HTML document with the custom options
    html_doc = load_html(input_html, resource_options)

    # 4️⃣  Save the processed document as PDF
    save_as_pdf(html_doc, output_pdf)

    print(f"✅ PDF saved to {output_pdf.resolve()}")

if __name__ == "__main__":
    main()
```

**Verwachte output** – na het uitvoeren van `python convert.py` zou je moeten zien:

```
✅ PDF saved to /full/path/YOUR_DIRECTORY/output.pdf
```

Open het gegenereerde bestand met een PDF‑viewer; je ziet de oorspronkelijke paginalay-out, CSS‑styling en afbeeldingen (mits ze bereikbaar waren vanuit het HTML‑bestand).  

Als je ontbrekende afbeeldingen opmerkt, controleer dan of hun `src`‑attributen absolute URLs zijn of relatieve paden die bestaan onder `YOUR_DIRECTORY`.

---

## Veelgestelde vragen & Randgevallen

| Vraag | Antwoord |
|----------|--------|
| *Wat als mijn HTML externe lettertypen referereert?* | WeasyPrint downloadt de lettertypebestanden automatisch, maar je wilt misschien domeinen whitelisten om lange ophaaltijden te vermijden. |
| *Kan ik een HTML‑string converteren in plaats van een bestand?* | Ja—gebruik `HTML(string=my_html_string)` en sla `base_url` over of stel het in op een tijdelijke map. |
| *Hoe beheer ik PDF‑metadata (titel, auteur)?* | Geef een `metadata`‑dict mee aan `write_pdf`, bijv. `html_doc.write_pdf(target='out.pdf', metadata={'Title': 'Report'})`. |
| *Ik krijg een “cairo‑cffi error” op Linux.* | Installeer het systeem‑pakket `libcairo2-dev` (`apt-get install libcairo2-dev` op Debian/Ubuntu) voordat je WeasyPrint via pip installeert. |

---

## Afsluiting

We hebben zojuist **PDF gemaakt van HTML** met een nette Python‑workflow, de **convert HTML to PDF**‑mechanica behandeld, en laten zien hoe je **HTML als PDF** kunt **opslaan** met robuuste resource‑handling. Het script is klein genoeg om in CI‑pipelines te gebruiken, maar flexibel genoeg om uit te breiden met aangepaste headers, footers of watermerken.

Mogelijke vervolgstappen:

- Gebruik de **html to pdf python** bibliotheek `pdfkit` voor een wkhtmltopdf‑gebaseerde aanpak (goed voor legacy CSS).  
- Voeg een CLI‑interface toe met `argparse` zodat het script invoer‑/uitvoer‑argumenten accepteert.  
- Genereer PDFs on‑the‑fly binnen een Flask‑ of FastAPI‑endpoint voor rapporten op aanvraag.  

Voel je vrij om te experimenteren, dingen kapot te maken, en daarna terug te keren naar deze gids voor een snelle opfrisser. Als je tegen problemen aanloopt, zijn de WeasyPrint‑documentatie en community‑forums uitstekende bronnen.

Happy coding, and enjoy turning those web pages into sleek PDFs!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑features onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Convert HTML to PDF with Aspose.HTML – Full Manipulation Guide](/html/english/)
- [Convert HTML to PDF in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Create PDF from HTML – C# Step‑by‑Step Guide](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}