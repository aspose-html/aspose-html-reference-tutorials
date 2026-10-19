---
category: general
date: 2026-07-21
description: Maak resource‑verwerkingsopties in Python en leer hoe je de maximale
  verwerkingsdiepte voor HTML‑parsing instelt. Volg deze stapsgewijze tutorial voor
  betrouwbaar resourcebeheer.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to set max handling depth
language: nl
lastmod: 2026-07-21
og_description: Maak resource‑afhandelingsopties in Python en zie meteen hoe je de
  maximale afhandelingsdiepte instelt voor veilig laden van HTML‑documenten. Beheers
  de techniek in enkele minuten.
og_image_alt: Screenshot of Python code that creates resource handling options with
  max handling depth set
og_title: Maak resource‑verwerkingsopties in Python – Volledige stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  headline: Create Resource handling options in Python – Full Guide
  type: TechArticle
- description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  name: Create Resource handling options in Python – Full Guide
  steps:
  - name: Circular References
    text: 'Some legacy sites embed an iframe that points back to the original page,
      creating a loop. With `max_handling_depth` set, the loop is automatically broken
      after the third iteration. However, you might still see a warning in the logs.
      To silence noisy logs, adjust the logger level:'
  - name: Missing Resources
    text: 'If a nested resource fails to load (404 or network timeout), the parser
      throws an exception by default. Wrap the loading call in a `try/except` block
      to keep your application alive:'
  - name: Adjusting Depth Dynamically
    text: 'Sometimes you need different depths for different parts of your pipeline.
      Because `resource_options` is a mutable object, you can change `max_handling_depth`
      on the fly:'
  type: HowTo
tags:
- Python
- HTML parsing
- resource management
title: Maak opties voor resourcebeheer in Python – volledige gids
url: /nl/python/general/create-resource-handling-options-in-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak resource handling opties in Python – Volledige gids

Heb je je ooit afgevraagd hoe je **resource handling opties maken** voor een enorme HTML‑pagina zonder je geheugen te overbelasten? Je bent niet de enige. Wanneer je een gigantisch document aan een parser geeft, kunnen geneste resources zoals frames, iframes of gekoppelde CSS snel uit de hand lopen.  

Het goede nieuws? Je kunt de parser vertellen om te stoppen na een bepaald aantal geneste niveaus. In deze tutorial laten we je zien **hoe je max handling depth instelt** en je applicatie responsief houdt. Klaar? Laten we beginnen.

## Wat je zult leren

- Waarom het beperken van de nestingsdiepte belangrijk is voor prestaties en beveiliging.  
- De exacte code die je nodig hebt om **resource handling opties te maken** met de `ResourceHandlingOptions`‑klasse.  
- Hoe je `max_handling_depth` configureert zodat de parser stopt na drie niveaus.  
- Tips voor het afhandelen van randgevallen, zoals documenten met circulaire referenties of ontbrekende resources.  

Ervaring met de bibliotheek is niet vereist—alleen een werkende Python 3‑installatie en een basisbegrip van bestands‑I/O.

## Vereisten

- Python 3.8+ (de bibliotheek werkt op alle recente versies).  
- Het `htmlparser`‑pakket dat `HTMLDocument` en `ResourceHandlingOptions` levert.  
- Een voorbeeld‑HTML‑bestand (`big_page.html`) geplaatst in een map die je kunt refereren.  

Als je het pakket nog niet hebt geïnstalleerd, voer dan uit:

```bash
pip install htmlparser
```

Nu de basis op orde is, gaan we verder met het belangrijkste deel.

## Maak resource handling opties – Stap 1

Allereerst: je hebt een instantie van `ResourceHandlingOptions` nodig. Beschouw het als een gereedschapskist waarin je de limieten en beleidsregels kunt instellen die de parser moet volgen.

```python
# Step 1: Create resource handling options and limit nesting depth
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # Stop after three levels of nested resources
```

**Waarom dit belangrijk is:**  
Wanneer de parser een `<iframe>` binnen een andere `<iframe>` tegenkomt, volgt hij normaal gesproken de keten eindeloos. Door de diepte te beperken tot `3`, voorkom je een uit de hand gelopen recursie die anders het RAM-geheugen kan uitputten of een stack‑overflow kan veroorzaken.  

> **Pro tip:** Als je onbetrouwbare inhoud parseert (bijv. door gebruikers geüploade HTML), overweeg dan de diepte te verlagen naar `1` of `2` om mogelijke aanvallen te beperken.

## Laad het HTML‑document – Stap 2

Met je opties‑object klaar, geef je het door aan `HTMLDocument`. De constructor respecteert de `max_handling_depth` die je zojuist hebt ingesteld.

```python
# Step 2: Load the HTML document using the configured options
html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
```

**Wat er onder de motorkap gebeurt:**  
`HTMLDocument` leest het bestand, bouwt een DOM‑boom en doorloopt vervolgens elke externe resource (stylesheets, scripts, afbeeldingen). Telkens wanneer het een geneste resource tegenkomt, controleert het `resource_options.max_handling_depth`. Als de limiet is bereikt, logt de parser een waarschuwing en slaat verdere nesting over.  

Dat betekent dat je een volledig bruikbare DOM krijgt voor de eerste drie lagen, en de rest veilig wordt genegeerd.

## Verifieer de configuratie – Stap 3

Het is altijd een goed idee om te bevestigen dat je instellingen effect hebben. Het `resource_options`‑object maakt zijn huidige staat zichtbaar, zodat je het kunt afdrukken of in een test kunt controleren.

```python
# Step 3: Verify that the max handling depth is set correctly
assert resource_options.max_handling_depth == 3, "Depth limit not applied!"

print(f"Resource handling options configured: max depth = {resource_options.max_handling_depth}")
```

Als de assertie slaagt, kun je er zeker van zijn dat de parser de limiet gedurende de rest van de uitvoering zal respecteren.

## Randgevallen afhandelen

### Circulaire referenties

Sommige oudere sites embedden een iframe die terugverwijst naar de oorspronkelijke pagina, waardoor een lus ontstaat. Met `max_handling_depth` ingesteld, wordt de lus automatisch verbroken na de derde iteratie. Je kunt echter nog steeds een waarschuwing in de logs zien. Om storende logs te dempen, pas je het logger‑niveau aan:

```python
import logging
logging.getLogger("htmlparser").setLevel(logging.ERROR)
```

### Ontbrekende resources

Als een geneste resource niet kan worden geladen (404 of netwerk‑timeout), gooit de parser standaard een uitzondering. Omring de laad‑aanroep met een `try/except`‑blok om je applicatie draaiende te houden:

```python
try:
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
except Exception as e:
    print(f"Failed to load a nested resource: {e}")
    # Fallback: load the document without additional resources
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

### Diepte dynamisch aanpassen

Soms heb je verschillende dieptes nodig voor verschillende delen van je pipeline. Omdat `resource_options` een mutabel object is, kun je `max_handling_depth` tijdens runtime aanpassen:

```python
resource_options.max_handling_depth = 5   # Temporarily allow deeper nesting
html_doc_deep = HTMLDocument("deep_page.html", resource_options)

resource_options.max_handling_depth = 2   # Tighten for a lightweight preview
html_doc_preview = HTMLDocument("preview.html", resource_options)
```

Vergeet alleen niet de waarde te resetten voordat je dezelfde opties‑instantie in een andere thread hergebruikt.

## Volledig werkend voorbeeld

Hieronder staat een compleet script dat je kunt kopiëren‑plakken, de bestands‑paden kunt aanpassen en direct kunt uitvoeren.

```python
import logging
from htmlparser import HTMLDocument, ResourceHandlingOptions

# Optional: Reduce noisy output
logging.getLogger("htmlparser").setLevel(logging.ERROR)

def load_document(path: str, max_depth: int = 3):
    """
    Load an HTML document with a controlled resource handling depth.
    Returns the HTMLDocument instance.
    """
    opts = ResourceHandlingOptions()
    opts.max_handling_depth = max_depth    # How to set max handling depth
    try:
        doc = HTMLDocument(path, opts)
        print(f"Loaded '{path}' with max depth {max_depth}.")
        return doc
    except Exception as exc:
        print(f"Error loading '{path}': {exc}")
        # Fallback to a simple load without resource handling
        return HTMLDocument(path)

if __name__ == "__main__":
    # Example 1: Standard depth
    doc1 = load_document("YOUR_DIRECTORY/big_page.html", max_depth=3)

    # Example 2: Deeper inspection for debugging
    doc2 = load_document("YOUR_DIRECTORY/complex_page.html", max_depth=5)

    # Example 3: Very shallow preview (e.g., thumbnail generation)
    doc3 = load_document("YOUR_DIRECTORY/preview_page.html", max_depth=1)
```

**Verwachte output (wanneer bestanden bestaan en goed gevormd zijn):**

```
Loaded 'YOUR_DIRECTORY/big_page.html' with max depth 3.
Loaded 'YOUR_DIRECTORY/complex_page.html' with max depth 5.
Loaded 'YOUR_DIRECTORY/preview_page.html' with max depth 1.
```

Als een bestand niet kan worden gelezen, zie je een foutmelding in plaats van een crash.

![Maak resource handling opties in Python](/images/resource-options.png){alt="Maak resource handling opties in Python"}

## Samenvatting – Waarom deze aanpak geweldig is

- **Veiligheid eerst:** Het beperken van de nestingsdiepte voorkomt uit de hand gelopen recursie en geheugenopblazing.  
- **Flexibiliteit:** Je kunt `max_handling_depth` tijdens runtime aanpassen aan verschillende scenario's.  
- **Eenvoud:** Een handvol code‑regels laten je **resource handling opties maken** en direct toepassen.  

Kortom, je hebt nu een robuust patroon om te bepalen hoe diep je parser externe resources volgt.

## Wat is het volgende?

- Verken de `ResourceHandlingOptions`‑klasse verder—er zijn vlaggen voor caching, timeout‑afhandeling en MIME‑type filtering.  
- Combineer diepte‑limitering met een aangepaste `UserAgent`‑string om te voorkomen dat je door agressieve servers wordt geblokkeerd.  
- Als je werkt met asynchrone I/O, kijk dan naar de `aiohtmlparser`‑variant die dezelfde opties respecteert maar werkt met `asyncio`.  

Voel je vrij om te experimenteren: probeer de diepte op `0` te zetten en zie hoe de parser elke externe referentie negeert. Het is een handige snelkoppeling wanneer je alleen de ruwe HTML‑markup nodig hebt.

Heb je vragen of een lastige pagina die je nog steeds tegenkomt? Laat een reactie achter hieronder, en ik help je graag de instellingen fijn af te stemmen. Veel plezier met parsen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [HTML maken vanuit string in C# – Gids voor aangepaste resource handler](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [HTML opslaan in C# – Complete gids met een aangepaste resource handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Sandbox maken voor HTML in Java – Stapsgewijze gids](/html/english/java/creating-managing-html-documents/create-sandbox-for-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}