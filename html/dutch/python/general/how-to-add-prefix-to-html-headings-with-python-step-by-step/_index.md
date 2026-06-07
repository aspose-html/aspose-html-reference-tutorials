---
category: general
date: 2026-06-07
description: Hoe je een voorvoegsel toevoegt aan HTML‑koppen met Python. Leer meerdere
  koppen selecteren, HTML‑titels aanpassen en de gewijzigde HTML efficiënt opslaan.
draft: false
keywords:
- how to add prefix
- select multiple headings
- save modified html
- change html titles
- modify html with python
language: nl
og_description: Hoe je een prefix toevoegt aan HTML‑koppen met Python. Deze tutorial
  laat zien hoe je meerdere koppen selecteert, HTML‑titels wijzigt en de aangepaste
  HTML in slechts een paar regels opslaat.
og_title: Hoe je een prefix toevoegt aan HTML‑koppen met Python – Snelle gids
schemas:
- author: Aspose
  dateModified: '2026-06-07'
  description: How to add prefix to HTML headings using Python. Learn to select multiple
    headings, change HTML titles, and save modified HTML efficiently.
  headline: How to Add Prefix to HTML Headings with Python – Step‑by‑Step Guide
  type: TechArticle
- description: How to add prefix to HTML headings using Python. Learn to select multiple
    headings, change HTML titles, and save modified HTML efficiently.
  name: How to Add Prefix to HTML Headings with Python – Step‑by‑Step Guide
  steps:
  - name: Verify the changes in a diff tool.
    text: Verify the changes in a diff tool.
  - name: Roll back instantly if something looks off.
    text: Roll back instantly if something looks off.
  - name: Keep the original untouched for audit purposes.
    text: Keep the original untouched for audit purposes.
  type: HowTo
tags:
- Python
- HTML
- Automation
- Web Scraping
title: Hoe je een prefix toevoegt aan HTML‑koppen met Python – Stapsgewijze gids
url: /nl/python/general/how-to-add-prefix-to-html-headings-with-python-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een prefix aan HTML-koppen toe te voegen met Python – Complete tutorial

Het toevoegen van een prefix aan HTML-koppen met Python is een veelvoorkomende behoefte wanneer je een site onderhoudt die vaak wordt bijgewerkt. In deze gids lopen we door het selecteren van meerdere koppen, het wijzigen van HTML-titels, en het opslaan van de aangepaste HTML—alles zonder je editor te verlaten.  

Als je je ooit hebt afgevraagd of je het “gemarkeerd als bijgewerkt” badge over tientallen pagina's kunt automatiseren, ben je op de juiste plek. We zullen ook ingaan op hoe je **modify html with python** op een schaalbare manier kunt doen, zodat je elk bestand niet handmatig hoeft te openen.

## Wat je zult bereiken

* **Select multiple headings** (`h1`, `h2`, `h3`) in één enkele doorgang.  
* **Add a custom prefix** (bijv. `[Updated]`) aan de tekst van elke kop.  
* **Save modified html** terug naar schijf, behoudende de oorspronkelijke bestandsstructuur.  
* Begrijp de afwegingen tussen verschillende Python HTML‑parsers, en kies degene die bij je project past.

Geen externe services, geen zware frameworks—alleen pure Python en een paar goed onderhouden bibliotheken.

---

## Hoe een prefix aan koptekst toevoegen in Python

Hieronder staat een minimaal, uitvoerbaar voorbeeld dat het kernidee demonstreert. Het gebruikt de **`lxml`** bibliotheek samen met **`cssselect`** voor selectorondersteuning, wat overeenkomt met de `query_selector_all` methode die je in het oorspronkelijke fragment zag.

```python
# -------------------------------------------------
# Step 0: Install dependencies (run once)
# -------------------------------------------------
# pip install lxml cssselect

# -------------------------------------------------
# Step 1: Load the HTML document
# -------------------------------------------------
from lxml import html

# Replace with your actual file path
input_path = "YOUR_DIRECTORY/article.html"
with open(input_path, "r", encoding="utf-8") as f:
    doc = html.fromstring(f.read())

# -------------------------------------------------
# Step 2: Select multiple headings (h1, h2, h3)
# -------------------------------------------------
# The CSS selector "h1, h2, h3" grabs all three levels.
headings = doc.cssselect("h1, h2, h3")

# -------------------------------------------------
# Step 3: Add the prefix "[Updated] " to each heading
# -------------------------------------------------
prefix = "[Updated] "
for heading in headings:
    # Preserve existing whitespace but prepend our tag
    heading.text = f"{prefix}{heading.text_content().strip()}"

# -------------------------------------------------
# Step 4: Save the modified HTML
# -------------------------------------------------
output_path = "YOUR_DIRECTORY/article_updated.html"
with open(output_path, "w", encoding="utf-8") as f:
    f.write(html.tostring(doc, pretty_print=True, encoding="unicode"))

print(f"✅ Finished! Modified file saved to {output_path}")
```

**Verwachte output** (excerpt uit `article_updated.html`):

```html
<h1>[Updated] Introduction to Machine Learning</h1>
<h2>[Updated] Data Pre‑processing Steps</h2>
<h3>[Updated] Feature Engineering Techniques</h3>
```

Let op hoe elke kop nu begint met de `[Updated]` tag—precies wat we wilden toen we vroegen **how to add prefix** aan onze titels.

### Waarom deze aanpak werkt

* **`lxml` + `cssselect`** geeft je volledige CSS‑selector kracht, waardoor de “select multiple headings” stap één regel wordt.  
* De `text_content()` methode haalt veilig de binnenste tekst op, waardoor HTML‑entiteiten of kind‑tags worden vermeden.  
* Terugschrijven met `pretty_print=True` houdt het bestand mens‑leesbaar, wat handig is voor diff‑weergaven in versiebeheer.

---

## Meerdere koppen selecteren met CSS-selectors

Als je een JavaScript‑achtergrond hebt, zal de `cssselect` syntaxis je meteen thuis laten voelen. De selector "h1, h2, h3" is een **komma‑gescheiden lijst**, wat betekent “pak elk element dat *een* van deze drie overeenkomt”.  

Je kunt ook de reikwijdte verbreden:

```python
# Grab every heading from h1 through h6
all_headings = doc.cssselect("h1, h2, h3, h4, h5, h6")
```

Of deze beperken tot een specifieke sectie:

```python
# Only headings inside the <article> tag
article_headings = doc.cssselect("article h1, article h2, article h3")
```

Deze kleine aanpassingen laten je **select multiple headings** met laserprecisie doen, wat vooral handig is wanneer je een enorme documentatiesite hebt en alleen een subsectie wilt bijwerken.

---

## Aangepaste HTML‑bestanden veilig opslaan

Wanneer je **save modified html**, wil je voorkomen dat het originele bestand corrupt raakt. Het patroon hierboven schrijft naar een nieuw bestand (`article_updated.html`). Op die manier kun je:

1. De wijzigingen verifiëren in een diff‑tool.  
2. Direct terugrollen als iets er niet goed uitziet.  
3. Het origineel onaangeroerd houden voor auditdoeleinden.

Als je een in‑place bewerking verkiest, verwissel dan gewoon de paden:

```python
import shutil
shutil.move(output_path, input_path)  # Overwrites the original
```

Maar onthoud: **always back up** voordat je overschrijft, vooral op productieservers.

---

## HTML‑titels wijzigen versus koppen

Je vraagt je misschien af of “changing HTML titles” hetzelfde is als het prefixen van koppen. In HTML‑terminologie bevindt de `<title>` tag zich binnen `<head>` en bepaalt de titel van het browsertabblad, terwijl koppen (`<h1>…<h3>`) in de paginacontent verschijnen.

Als je ook **change html titles** moet doen, geldt dezelfde `lxml` workflow:

```python
# Change the <title> tag
title_elem = doc.find(".//title")
if title_elem is not None:
    title_elem.text = f"{prefix}{title_elem.text}"
```

Nu dragen zowel de paginatitel als de zichtbare koppen dezelfde `[Updated]` vlag—perfect voor SEO‑audits waar je consistentie wilt tussen meta‑data en on‑page content.

---

## Alternatieve bibliotheken voor modify html with python

Hoewel `lxml` snel en feature‑rich is, gebruik je misschien al **BeautifulSoup** (bs4) in je project. Hier is dezelfde logica in een meer “pythonic” stijl:

```python
from bs4 import BeautifulSoup

with open(input_path, "r", encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")

for tag in soup.select("h1, h2, h3"):
    tag.string = f"{prefix}{tag.get_text(strip=True)}"

with open(output_path, "w", encoding="utf-8") as f:
    f.write(str(soup.prettify()))
```

Beide bibliotheken laten je **modify html with python** doen, dus kies degene die bij je bestaande stack past. `BeautifulSoup` blinkt uit wanneer je vergevingsgezinde parsing van misvormde markup nodig hebt, terwijl `lxml` superieure snelheid biedt voor grote batches.

---

## Pro‑tips & veelvoorkomende valkuilen

* **Encoding matters** – open altijd bestanden met `encoding="utf-8"` om Unicode‑fouten bij niet‑ASCII tekens te voorkomen.  
* **Avoid double‑prefixing** – als je het script twee keer uitvoert, krijg je `[Updated] [Updated] …`. Bescherm hiertegen door te controleren of `heading.text.startswith(prefix)`.  
* **Preserve whitespace** – de `strip()` aanroep verwijdert losse spaties, waardoor de output netjes blijft.  
* **Batch processing** – wikkel de hele flow in een `for file in pathlib.Path("YOUR_DIRECTORY").glob("*.html"):` lus om een volledige map met één commando bij te werken.  

---

## Volledig werkend voorbeeld: batch‑update van een map

Hieronder staat een compact script dat over elk `.html`‑bestand in een map iterereert, koppen prefixeert, de `<title>` bijwerkt, en een nieuw bestand schrijft met `_updated` toegevoegd.

```python
import pathlib
from lxml import html

prefix = "[Updated] "
source_dir = pathlib.Path("YOUR_DIRECTORY")
output_dir = source_dir / "updated"
output_dir.mkdir(exist_ok=True)

for html_path in source_dir.glob("*.html"):
    # Load
    with open(html_path, "r", encoding="utf-8") as f:
        doc = html.fromstring(f.read())

    # Headings
    for h in doc.cssselect("h1, h2, h3"):
        if not h.text_content().startswith(prefix):
            h.text = f"{prefix}{h.text_content().strip()}"

    # Title
    title_elem = doc.find(".//title")
    if title_elem is not None and not title_elem.text.startswith(prefix):
        title_elem.text = f"{prefix}{title_elem.text}"

    # Save
    out_path = output_dir / f"{html_path.stem}_updated.html"
    with open(out_path, "w", encoding="utf-8") as f:
        f.write(html.tostring(doc, pretty_print=True, encoding="unicode"))

    print(f"✅ Processed {html_path.name} → {out_path.name}")
```

Voer het één keer uit, en elk HTML‑bestand in `YOUR_DIRECTORY` krijgt een nieuwe `[Updated]` badge—geen handmatige bewerking nodig.

---

## Conclusie

We hebben **how to add prefix** aan HTML‑koppen met Python behandeld, laten zien hoe je **select multiple headings** kunt uitvoeren, laten zien hoe je **save modified html** veilig kunt doen, en zelfs aangeraakt **change html titles** voor een volledige revisie. Door gebruik te maken van `lxml` of `BeautifulSoup` heb je nu een solide toolbox voor **modify html with python** in real‑world projecten.

Volgende stappen? Probeer timestamps toe te voegen in plaats van een statische tag, of genereer een changelog‑bestand dat elke door jou aangepaste file opsomt. Je kunt dit script ook koppelen aan een CI‑pipeline zodat elke deployment automatisch

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies te beheersen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe HTML bewerken met Aspose.HTML voor Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Hoe CSS toevoegen – Inline CSS aan HTML‑documenten in Aspose.HTML voor Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [Hoe HTML queryen in Java – Complete tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}