---
category: general
date: 2026-07-21
description: Skapa alternativ för resurshantering i Python och lär dig hur du ställer
  in maximalt hanteringsdjup för HTML‑parsing. Följ denna steg‑för‑steg‑handledning
  för pålitlig resurshantering.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to set max handling depth
language: sv
lastmod: 2026-07-21
og_description: Skapa resurshanteringsalternativ i Python och se omedelbart hur du
  ställer in maximalt hanteringsdjup för säker laddning av HTML-dokument. Bemästra
  tekniken på några minuter.
og_image_alt: Screenshot of Python code that creates resource handling options with
  max handling depth set
og_title: Skapa resurshanteringsalternativ i Python – Komplett steg‑för‑steg‑guide
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
title: Skapa resurshanteringsalternativ i Python – Fullständig guide
url: /sv/python/general/create-resource-handling-options-in-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa resurs‑hanteringsalternativ i Python – Fullständig guide

Har du någonsin undrat hur man **skapar resurs‑hanteringsalternativ** för en massiv HTML‑sida utan att spränga minnet? Du är inte ensam. När du matar in ett gigantiskt dokument i en parser kan nästlade resurser som frames, iframes eller länkad CSS snabbt gå överstyr.  

Den goda nyheten? Du kan instruera parsern att stoppa efter ett visst antal nästlade nivåer. I den här handledningen visar vi dig **hur du ställer in max hanteringsdjup** och håller din applikation responsiv. Är du redo? Låt oss dyka ner.

## Vad du kommer att lära dig

- Varför begränsning av nästlingsdjup är viktigt för prestanda och säkerhet.  
- Den exakta koden du behöver för att **skapa resurs‑hanteringsalternativ** med hjälp av `ResourceHandlingOptions`‑klassen.  
- Hur du konfigurerar `max_handling_depth` så att parsern stoppar efter tre nivåer.  
- Tips för att hantera kantfall, såsom dokument med cirkulära referenser eller saknade resurser.  

Ingen förkunskap om biblioteket krävs—bara en fungerande Python 3‑installation och en grundläggande förståelse för fil‑I/O.

## Förutsättningar

- Python 3.8+ (biblioteket fungerar på alla nyliga versioner).  
- `htmlparser`‑paketet som tillhandahåller `HTMLDocument` och `ResourceHandlingOptions`.  
- En exempel‑HTML‑fil (`big_page.html`) placerad i en mapp du kan referera till.  

Om du ännu inte har installerat paketet, kör:

```bash
pip install htmlparser
```

Nu när grunderna är på plats, låt oss gå till själva kärnan av ämnet.

## Skapa resurs‑hanteringsalternativ – Steg 1

Först och främst: du behöver en instans av `ResourceHandlingOptions`. Tänk på den som en verktygslåda där du kan sätta gränser och policyer som parsern ska följa.

```python
# Step 1: Create resource handling options and limit nesting depth
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # Stop after three levels of nested resources
```

**Varför detta är viktigt:**  
När parsern stöter på ett `<iframe>` inuti ett annat `<iframe>` följer den normalt kedjan i all oändlighet. Genom att begränsa djupet till `3` förhindrar du okontrollerad rekursion som annars kan tömma RAM eller orsaka stack‑overflow.  

> **Pro tip:** Om du parserar opålitligt innehåll (t.ex. användar‑uppladdad HTML), överväg att sänka djupet till `1` eller `2` för att minska risken för attacker.

## Ladda HTML‑dokumentet – Steg 2

Med ditt alternativ‑objekt redo, skicka det till `HTMLDocument`. Konstruktorn respekterar `max_handling_depth` som du just satt.

```python
# Step 2: Load the HTML document using the configured options
html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
```

**Vad som händer under huven:**  
`HTMLDocument` läser filen, bygger ett DOM‑träd och går sedan igenom varje extern resurs (stilmallar, skript, bilder). När den stöter på en nästlad resurs kontrollerar den `resource_options.max_handling_depth`. Om gränsen nås loggar parsern en varning och hoppar över vidare nästling.  

Det betyder att du får ett fullt användbart DOM för de första tre lagren, och resten ignoreras säkert.

## Verifiera konfigurationen – Steg 3

Det är alltid en bra idé att bekräfta att dina inställningar trätt i kraft. `resource_options`‑objektet exponerar sitt aktuella tillstånd, så du kan skriva ut det eller göra ett påstående i ett test.

```python
# Step 3: Verify that the max handling depth is set correctly
assert resource_options.max_handling_depth == 3, "Depth limit not applied!"

print(f"Resource handling options configured: max depth = {resource_options.max_handling_depth}")
```

Om påståendet passerar kan du vara säker på att parsern kommer att följa gränsen under hela körningen.

## Hantera kantfall

### Cirkulära referenser

Vissa äldre webbplatser bäddar in ett iframe som pekar tillbaka till den ursprungliga sidan, vilket skapar en slinga. Med `max_handling_depth` satt bryts slingan automatiskt efter den tredje iterationen. Du kan dock fortfarande se en varning i loggarna. För att tysta bullriga loggar, justera logger‑nivån:

```python
import logging
logging.getLogger("htmlparser").setLevel(logging.ERROR)
```

### Saknade resurser

Om en nästlad resurs misslyckas med att laddas (404 eller nätverkstidsgräns) kastar parsern som standard ett undantag. Omge laddningsanropet med ett `try/except`‑block för att hålla din applikation vid liv:

```python
try:
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
except Exception as e:
    print(f"Failed to load a nested resource: {e}")
    # Fallback: load the document without additional resources
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

### Justera djup dynamiskt

Ibland behöver du olika djup för olika delar av din pipeline. Eftersom `resource_options` är ett muterbart objekt kan du ändra `max_handling_depth` i farten:

```python
resource_options.max_handling_depth = 5   # Temporarily allow deeper nesting
html_doc_deep = HTMLDocument("deep_page.html", resource_options)

resource_options.max_handling_depth = 2   # Tighten for a lightweight preview
html_doc_preview = HTMLDocument("preview.html", resource_options)
```

Kom bara ihåg att återställa värdet innan du återanvänder samma alternativ‑instans i en annan tråd.

## Fullt fungerande exempel

Nedan är ett komplett skript som du kan kopiera‑klistra, justera fil‑sökvägarna och köra direkt.

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

**Förväntad output (när filer finns och är väl‑formade):**

```
Loaded 'YOUR_DIRECTORY/big_page.html' with max depth 3.
Loaded 'YOUR_DIRECTORY/complex_page.html' with max depth 5.
Loaded 'YOUR_DIRECTORY/preview_page.html' with max depth 1.
```

Om en fil inte kan läsas får du ett felmeddelande istället för en krasch.

![Skapa resurs‑hanteringsalternativ i Python](/images/resource-options.png){alt="Skapa resurs‑hanteringsalternativ i Python"}

## Sammanfattning – Varför detta tillvägagångssätt är fantastiskt

- **Säkerhet först:** Att begränsa nästlingsdjup förhindrar okontrollerad rekursion och minnesuppblåsthet.  
- **Flexibilitet:** Du kan ändra `max_handling_depth` vid körning för att passa olika scenarier.  
- **Enkelhet:** Ett fåtal kodrader låter dig **skapa resurs‑hanteringsalternativ** och omedelbart tillämpa dem.  

Kort sagt, du har nu ett robust mönster för att kontrollera hur djupt din parser följer externa resurser.

## Vad blir nästa steg?

- Utforska `ResourceHandlingOptions`‑klassen vidare—det finns flaggor för cachning, timeout‑hantering och MIME‑type‑filtrering.  
- Kombinera djupbegränsning med en anpassad `UserAgent`‑sträng för att undvika att blockeras av aggressiva servrar.  
- Om du arbetar med asynkron I/O, titta på `aiohtmlparser`‑varianten som respekterar samma alternativ men fungerar med `asyncio`.  

Känn dig fri att experimentera: prova att sätta djupet till `0` och se parsern ignorera varje extern referens. Det är ett praktiskt kortkommando när du bara behöver den råa HTML‑markupen.

Har du frågor eller en knepig sida som fortfarande får dig att snubbla? Lägg en kommentar nedan, så hjälper jag dig gärna att finjustera inställningarna. Lycka till med parsingen!

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa HTML från sträng i C# – Guide för anpassad resurs‑hanterare](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Hur man sparar HTML i C# – Komplett guide med anpassad resurs‑hanterare](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Skapa sandbox för HTML i Java – Steg‑för‑steg‑guide](/html/english/java/creating-managing-html-documents/create-sandbox-for-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}