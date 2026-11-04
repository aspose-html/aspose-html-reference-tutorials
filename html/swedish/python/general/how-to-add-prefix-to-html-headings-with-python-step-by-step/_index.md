---
category: general
date: 2026-06-07
description: Hur man lägger till ett prefix till HTML‑rubriker med Python. Lär dig
  att välja flera rubriker, ändra HTML‑titlar och spara den modifierade HTML‑koden
  effektivt.
draft: false
keywords:
- how to add prefix
- select multiple headings
- save modified html
- change html titles
- modify html with python
language: sv
og_description: Hur man lägger till ett prefix till HTML‑rubriker med Python. Den
  här handledningen visar hur man väljer flera rubriker, ändrar HTML‑titlar och sparar
  den modifierade HTML‑koden på bara några rader.
og_title: Hur man lägger till prefix till HTML‑rubriker med Python – Snabbguide
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
title: Hur man lägger till prefix till HTML‑rubriker med Python – Steg‑för‑steg‑guide
url: /sv/python/general/how-to-add-prefix-to-html-headings-with-python-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man lägger till prefix till HTML‑rubriker med Python – Komplett handledning

Att lägga till prefix till HTML‑rubriker med Python är ett vanligt behov när du underhåller en webbplats som uppdateras ofta. I den här guiden går vi igenom hur du väljer flera rubriker, ändrar HTML‑titlar och sparar den modifierade HTML‑koden – allt utan att lämna din editor.  

Om du någonsin har undrat om du kan automatisera “markerad som uppdaterad”-märket på dussintals sidor, är du på rätt plats. Vi berör också hur du **modify html with python** på ett skalbart sätt, så att du slipper öppna varje fil manuellt.

## Vad du kommer att uppnå

När du är klar med den här handledningen kommer du att kunna:

* **Välja flera rubriker** (`h1`, `h2`, `h3`) i ett enda pass.  
* **Lägga till ett eget prefix** (t.ex. `[Updated]`) till varje rubriktext.  
* **Spara modifierad html** tillbaka till disk, samtidigt som du bevarar den ursprungliga filstrukturen.  
* Förstå för- och nackdelar med olika Python‑HTML‑parsers och välja den som passar ditt projekt.

Inga externa tjänster, inga tunga ramverk – bara ren Python och ett par välunderhållna bibliotek.

---

## Hur man lägger till prefix till rubriktext i Python

Nedan är ett minimalt, körbart exempel som demonstrerar kärnidén. Det använder **`lxml`**‑biblioteket tillsammans med **`cssselect`** för stöd av selektorer, vilket motsvarar `query_selector_all`‑metoden du såg i originalsnutten.

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

**Förväntad output** (utdrag från `article_updated.html`):

```html
<h1>[Updated] Introduction to Machine Learning</h1>
<h2>[Updated] Data Pre‑processing Steps</h2>
<h3>[Updated] Feature Engineering Techniques</h3>
```

Lägg märke till hur varje rubrik nu börjar med taggen `[Updated]` – exakt vad vi ville ha när vi frågade **how to add prefix** till våra titlar.

### Varför detta tillvägagångssätt fungerar

* **`lxml` + `cssselect`** ger dig full CSS‑selektor‑kraft, vilket gör steget “select multiple headings” till en enradare.  
* Metoden `text_content()` extraherar säkert den inre texten och undviker HTML‑entiteter eller barn‑taggar.  
* Att skriva tillbaka med `pretty_print=True` håller filen mänskligt läsbar, vilket är praktiskt för diff‑verktyg i versionskontroll.

---

## Välja flera rubriker med CSS‑selektorer

Om du kommer från en JavaScript‑bakgrund kommer `cssselect`‑syntaxen att kännas naturlig. Selektorn `"h1, h2, h3"` är en **komma‑separerad lista**, vilket betyder “hämta alla element som matchar *något* av dessa tre”.  

Du kan också bredda urvalet:

```python
# Grab every heading from h1 through h6
all_headings = doc.cssselect("h1, h2, h3, h4, h5, h6")
```

Eller begränsa det till ett specifikt avsnitt:

```python
# Only headings inside the <article> tag
article_headings = doc.cssselect("article h1, article h2, article h3")
```

Dessa små justeringar låter dig **select multiple headings** med laserprecision, vilket är särskilt användbart när du har en massiv dokumentationssajt och bara vill uppdatera ett delavsnitt.

---

## Spara modifierade HTML‑filer på ett säkert sätt

När du **save modified html** vill du undvika att korrupta den ursprungliga filen. Mönstret ovan skriver till en ny fil (`article_updated.html`). På så sätt kan du:

1. Verifiera förändringarna i ett diff‑verktyg.  
2. Återgå omedelbart om något ser felaktigt ut.  
3. Lämna originalet orört för revisionsändamål.

Om du föredrar en in‑place‑redigering, byt bara ut sökvägarna:

```python
import shutil
shutil.move(output_path, input_path)  # Overwrites the original
```

Men kom ihåg: **säkerhetskopiera alltid** innan du skriver över, särskilt på produktionsservrar.

---

## Ändra HTML‑titlar vs. rubriker

Du kanske undrar om “changing HTML titles” är detsamma som att prefixa rubriker. I HTML‑terminologi lever `<title>`‑taggen i `<head>` och styr flikens titel i webbläsaren, medan rubriker (`<h1>…<h3>`) visas i sidans kropp.

Om du också behöver **change html titles**, fungerar samma `lxml`‑arbetsflöde:

```python
# Change the <title> tag
title_elem = doc.find(".//title")
if title_elem is not None:
    title_elem.text = f"{prefix}{title_elem.text}"
```

Nu har både sidtiteln och de synliga rubrikerna samma `[Updated]`‑flagga – perfekt för SEO‑granskningar där du vill ha konsistens mellan metadata och innehåll på sidan.

---

## Alternativa bibliotek för modify html with python

Medan `lxml` är snabbt och funktionsrikt, kanske du redan använder **BeautifulSoup** (bs4) i ditt projekt. Här är samma logik i en mer “pythonic” stil:

```python
from bs4 import BeautifulSoup

with open(input_path, "r", encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")

for tag in soup.select("h1, h2, h3"):
    tag.string = f"{prefix}{tag.get_text(strip=True)}"

with open(output_path, "w", encoding="utf-8") as f:
    f.write(str(soup.prettify()))
```

Båda biblioteken låter dig **modify html with python**, så välj det som passar din befintliga stack. `BeautifulSoup` glänser när du behöver förlåtande parsning av felaktig markup, medan `lxml` erbjuder överlägsen hastighet för stora batcher.

---

## Pro‑tips & vanliga fallgropar

* **Encoding är viktigt** – öppna alltid filer med `encoding="utf-8"` för att undvika Unicode‑fel på icke‑ASCII‑tecken.  
* **Undvik dubbel‑prefix** – om du kör skriptet två gånger får du `[Updated] [Updated] …`. Förhindra detta genom att kontrollera `heading.text.startswith(prefix)`.  
* **Bevara whitespace** – anropet `strip()` tar bort oönskade mellanslag och håller outputen prydlig.  
* **Batch‑bearbetning** – slå in hela flödet i en `for file in pathlib.Path("YOUR_DIRECTORY").glob("*.html"):`‑loop för att uppdatera en hel mapp med ett enda kommando.  

---

## Fullt fungerande exempel: batch‑uppdatering av en katalog

Nedan är ett kompakt skript som itererar över varje `.html`‑fil i en katalog, lägger till prefix på rubriker, uppdaterar `<title>` och skriver en ny fil med `_updated` tillagt.

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

Kör det en gång, så får varje HTML‑fil i `YOUR_DIRECTORY` ett fräscht `[Updated]`‑märke – ingen manuell redigering behövs.

---

## Slutsats

Vi har gått igenom **how to add prefix** till HTML‑rubriker med Python, demonstrerat hur du **select multiple headings**, visat hur du **save modified html** på ett säkert sätt, och även berört **change html titles** för en komplett översyn. Genom att utnyttja antingen `lxml` eller `BeautifulSoup` har du nu en solid verktygslåda för **modify html with python** i verkliga projekt.

Nästa steg? Prova att lägga till tidsstämplar istället för en statisk tagg, eller generera en changelog‑fil som listar varje fil du har berört. Du kan också koppla detta skript till en CI‑pipeline så att varje distribution automatiskt


## Vad bör du lära dig härnäst?


Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}