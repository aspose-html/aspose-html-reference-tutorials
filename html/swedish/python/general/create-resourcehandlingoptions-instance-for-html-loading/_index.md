---
category: general
date: 2026-05-31
description: Skapa ett ResourceHandlingOptions‑objekt för att kontrollera laddning
  av HTML‑resurser. Lär dig hur du begränsar resursdjupet och laddar ett HTMLDocument
  med anpassade alternativ.
draft: false
keywords:
- create resourcehandlingoptions instance
- limit resource depth
- HTMLDocument options
- resource loading configuration
- python html parsing
language: sv
og_description: Skapa en ResourceHandlingOptions‑instans för att kontrollera laddning
  av HTML‑resurser. Denna guide visar hur du ställer in maximalt hanteringsdjup och
  laddar ett HTMLDocument med anpassade alternativ.
og_title: Skapa en ResourceHandlingOptions‑instans för HTML‑inläsning
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create ResourceHandlingOptions instance to control HTML resource loading.
    Learn how to limit resource depth and load an HTMLDocument with custom options.
  headline: Create ResourceHandlingOptions Instance for HTML Loading
  type: TechArticle
tags:
- Python
- HTML parsing
- Resource handling
title: Skapa ResourceHandlingOptions‑instans för HTML‑inläsning
url: /sv/python/general/create-resourcehandlingoptions-instance-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa ResourceHandlingOptions-instans för HTML-inläsning

Har du någonsin funderat på hur du **skapar en ResourceHandlingOptions-instans** så att du kan hindra en gigantisk HTML‑sida från att krascha din parser? Du är inte ensam—stora dokument med nästlade skript, ramar eller inkluderade filer kan snabbt förvandla ett enkelt skrapande till en mardröm.  

I den här handledningen går vi igenom de exakta stegen för att skapa ett `ResourceHandlingOptions`‑objekt, begränsa nästlingsnivån och mata in det i ett `HTMLDocument`. I slutet har du ett rent, återanvändbart mönster för **resource loading configuration** som fungerar med vilken enorm HTML‑fil som helst.

## Vad du kommer att lära dig

- Varför en `ResourceHandlingOptions`‑instans är viktig när man parsar massiva sidor.  
- Hur du **begränsar resursdjupet** för att undvika oändlig rekursion.  
- Den exakta syntaxen för att ladda ett `HTMLDocument` med dina anpassade alternativ.  
- Ett komplett, körbart exempel som du kan lägga in i ditt projekt redan idag.  

**Förutsättningar:** Python 3.8+, `htmlparser`‑biblioteket som tillhandahåller `HTMLDocument` och `ResourceHandlingOptions`. Inga andra beroenden krävs.

---

## Steg 1: Skapa en ResourceHandlingOptions‑instans

Det första du behöver är ett nytt `ResourceHandlingOptions`‑objekt. Tänk på det som kontrollpanelen för varje extern resurs som parsern kan stöta på—skript, bilder, iframes, du namnger det.

```python
# Step 1: Initialize the options object
options = ResourceHandlingOptions()
```

> **Varför detta är viktigt:** Utan en explicit instans återgår parsern till sina standardinställningar, vilket ofta betyder “ladda allt”. För enorma sidor kan den standarden konsumera gigabyte minne och få ditt skript att hänga.

---

## Steg 2: Begränsa resursdjupet

Nästa steg är att tala om för alternativen hur djupt vi är villiga att gå. Att sätta `max_handling_depth` till 5, till exempel, stoppar parsern efter fem nivåer av nästlade resurser. Justera siffran så att den passar ditt användningsfall.

```python
# Step 2: Cap the nesting depth (e.g., stop after 5 levels)
options.max_handling_depth = 5
```

> **Proffstips:** Om du bara är intresserad av innehållet på toppnivå är ett djup på 1 eller 2 vanligtvis tillräckligt och påskyndar processen avsevärt.

---

## Steg 3: Ladda HTML‑dokumentet med alternativ

Nu överlämnar vi de konfigurerade `options` till `HTMLDocument`. Konstruktorn accepterar filvägen (eller URL:en) och alternativobjektet, vilket ger dig fin‑granulär kontroll över vad som laddas.

```python
# Step 3: Parse the HTML file using the configured options
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", options)
```

> **Vad du kommer att se:** Parsern kommer att läsa `big_page.html`, men alla resurser som skulle få djupet att överstiga 5 ignoreras tyst. Detta förhindrar okontrollerad rekursion och håller minnesanvändningen förutsägbar.

---

## Steg 4: Verifiera resultatet (valfritt men hjälpsamt)

Det är en god vana att kontrollera att dokumentet laddades som förväntat. Nedan är en snabb kontroll som skriver ut antalet resurser som hanterades framgångsrikt.

```python
# Step 4: Quick verification
print(f"Handled resources: {len(doc.resources)}")
print(f"Document title: {doc.title}")
```

**Förväntad utskrift** (dina siffror kommer att skilja sig beroende på indatafilen):

```
Handled resources: 12
Document title: Example Large Page
```

Om antalet är mycket lägre än du förväntade dig kan du behöva öka `max_handling_depth` eller justera andra `ResourceHandlingOptions`‑egenskaper.

---

## Vanliga variationer och kantfall

| Situation | Justering |
|-----------|------------|
| **Du behöver bara ignorera bilder** | Sätt `options.ignore_images = True`. |
| **Skript orsakar tidsgränser** | Använd `options.max_script_execution_time = 2` (sekunder). |
| **Parsa en fjärr-URL istället för en fil** | Skicka URL‑strängen till `HTMLDocument` precis som en filväg. |
| **Du vill ha en anpassad logger** | Tilldela `options.logger = my_logger` innan du laddar. |

Dessa justeringar är alla en del av verktygssatsen **HTMLDocument options** och låter dig finjustera **resource loading configuration** utan att skriva om din parser.

---

## Fullt fungerande exempel

När allt är sammansatt, här är ett självständigt skript som du kan köra direkt. Spara det som `parse_big_page.py` och kör det med `python parse_big_page.py`.

```python
# parse_big_page.py
from htmlparser import HTMLDocument, ResourceHandlingOptions

def main():
    # 1️⃣ Create the options instance
    options = ResourceHandlingOptions()
    
    # 2️⃣ Limit how deep we go into nested resources
    options.max_handling_depth = 5
    
    # Optional: ignore images to speed things up
    # options.ignore_images = True
    
    # 3️⃣ Load the document with our custom options
    doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", options)
    
    # 4️⃣ Verify the load
    print(f"Handled resources: {len(doc.resources)}")
    print(f"Document title: {doc.title}")

if __name__ == "__main__":
    main()
```

Kör det så bör du se antalet resurser och titeln skrivet ut, vilket bekräftar att du framgångsrikt **skapat en resourcehandlingoptions-instans** och tillämpat den.

---

## Slutsats

Vi har just visat dig hur du **skapar en ResourceHandlingOptions‑instans**, begränsar nästlingsnivån och matar in den i ett `HTMLDocument`. Detta mönster ger dig pålitlig **resource loading configuration** för vilken stor HTML‑fil som helst, och håller din Python‑HTML‑parsning snabb och minnesvänlig.

Redo för nästa steg? Prova att byta djupgränsen, växla `ignore_images`, eller integrera en anpassad logger—varje justering lär dig mer om **HTMLDocument options** och hur de samverkar med din datapipeline.  

Om du fann den här guiden användbar, dela gärna den, ge stjärna till repot, eller lämna en kommentar med dina egna tips. Lycka till med parsning!

## Vad bör du lära dig härnäst?

- [Create HTML from String in C# – Custom Resource Handler Guide](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Create Stream Provider in .NET with Aspose.HTML](/html/english/net/advanced-features/create-stream-provider/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}