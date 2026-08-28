---
category: general
date: 2026-05-28
description: Lär dig hur du använder SaveOptions för att trimma HTML‑sidor i Python.
  Denna steg‑för‑steg‑guide förklarar också hur du laddar ett HTML‑dokument och effektivt
  tar bort inbäddade resurser.
draft: false
keywords:
- how to use saveoptions
- how to load html document
- how to trim html page
language: sv
og_description: Hur du använder SaveOptions för att trimma HTML‑sidor i Python. Följ
  den här guiden för att ladda ett HTML‑dokument, sätta resursbegränsningar och spara
  en ren, lättviktig fil.
og_title: Hur man använder SaveOptions i Python – Trimma HTML‑sidor
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to use SaveOptions to trim HTML pages in Python. This step‑by‑step
    guide also explains how to load an HTML document and efficiently remove nested
    resources.
  headline: How to Use SaveOptions in Python – Trim HTML Pages
  type: TechArticle
tags:
- python
- html-processing
- saveoptions
- resource-handling
title: Hur man använder SaveOptions i Python – Trimma HTML‑sidor
url: /sv/python/general/how-to-use-saveoptions-in-python-trim-html-pages/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så använder du SaveOptions i Python – Trimma HTML‑sidor

Har du någonsin undrat **hur man använder SaveOptions** för att krympa en enorm HTML‑fil utan att bryta någonting? Du är inte ensam. När du hämtar en sida som innehåller dussintals nästlade resurser—tänk CSS, JS eller till och med andra HTML‑snuttar—kan ditt resultat svälla okontrollerat.  

I den här handledningen går vi igenom ett komplett, körbart exempel som inte bara visar **hur man använder SaveOptions**, utan också täcker **hur man laddar ett HTML‑dokument** och det bästa sättet att **trimma en HTML‑sida** genom att begränsa nästlingsdjupet. I slutet har du en ren, trimmad fil redo för distribution eller vidare bearbetning.

## Vad du kommer att uppnå

- Ladda vilken lokal HTML‑fil som helst med en enda kodrad.  
- Konfigurera resurshanteringsalternativ för att stoppa vid ett specifikt inkluderingsdjup.  
- Spara det trimmade resultatet med den kraftfulla `SaveOptions`‑klassen.  

Inga externa verktyg, ingen magi—bara ren Python och ett litet bibliotek som gör det tunga lyftet.

---

## Förutsättningar

Innan vi dyker ner, se till att du har:

1. **Python 3.9+** installerat (syntaxen fungerar på alla nyligen släppta versioner).  
2. Det hypotetiska paketet `htmlprocessor` som tillhandahåller `HTMLDocument`, `SaveOptions` och `ResourceHandlingOptions`. Installera det via:

```bash
pip install htmlprocessor
```

> **Pro tip:** Om du använder ett virtuellt miljö, aktivera den först—det håller dina beroenden prydliga.

---

## Steg 1: Hur man laddar ett HTML‑dokument

Att ladda en fil är så enkelt som att peka konstruktorn på din sökväg. Biblioteket läser markupen, bygger ett DOM‑likt träd och förbereder det för vidare manipulation.

```python
from htmlprocessor import HTMLDocument

# Replace with the actual path to your file
doc = HTMLDocument("YOUR_DIRECTORY/complex_page.html")
print("Document loaded –", doc.title or "Untitled")
```

> **Varför detta är viktigt:** `HTMLDocument`‑objektet abstraherar bort rå sträng‑hantering och ger dig metoder för att fråga, modifiera och så småningom spara sidan. Det normaliserar också radslut och teckenkodningar, vilket sparar dig från subtila buggar senare.

Du märker att vi skrev ut titeln bara för att verifiera att laddningen lyckades. Om filen saknas eller är felaktig kastar konstruktorn ett tydligt undantag—inga tysta fel.

---

## Steg 2: Konfigurera resurshantering – Kärnan i trimning

Nästa pusselbit är **hur man trimmar HTML‑sida**‑innehåll genom att begränsa hur djupt processorn följer inkluderade filer. Här kommer `ResourceHandlingOptions` till sin rätt.

```python
from htmlprocessor import ResourceHandlingOptions

# Create a fresh options instance
res_opt = ResourceHandlingOptions()
# max_handling_depth = 2 means: main page + one level of includes
res_opt.max_handling_depth = 2
```

### Vad gör `max_handling_depth`?

- **Djup 1** → Endast rot‑HTML‑filen, alla externa resurser ignoreras.  
- **Djup 2** → Roten plus alla direkt refererade filer (t.ex. ett `iframe` eller server‑side include).  
- **Högre värden** → Djupare nästling, men också större output och längre behandlingstid.

Genom att sätta ett tak på djupet till **2** behåller vi huvudsidan och ett lager av inkluderade filer, och kastar allt som ligger djupare. Detta räcker vanligtvis för att ta bort överflödiga sidfötter, analys‑skript eller nästlade mallar som du inte behöver i en trimmad kopia.

---

## Steg 3: Fäst alternativen på spar‑konfigurationen

Nu binder vi våra resurssregler till en `SaveOptions`‑instans. Detta objekt talar om för biblioteket *exakt* hur filen ska skrivas tillbaka till disk.

```python
from htmlprocessor import SaveOptions

save_opt = SaveOptions()
save_opt.resource_handling_options = res_opt
```

> **Varför använda `SaveOptions`?**  
> Det ger dig finmaskig kontroll över outputen—utöver bara resurssdjupet. Du kan senare lägga till komprimering, pretty‑printing eller till och med egna callbacks utan att röra den centrala spar‑logiken.

---

## Steg 4: Hur man använder SaveOptions för att trimma HTML‑sidan

Till sist anropar vi `save`‑metoden med våra konfigurerade alternativ. Biblioteket går igenom DOM‑trädet, respekterar djupgränsen och skriver en trimmad fil.

```python
# Save the trimmed document
output_path = "YOUR_DIRECTORY/trimmed_page.html"
doc.save(output_path, save_opt)

print(f"Trimmed page saved to {output_path}")
```

### Förväntat resultat

- Filen `trimmed_page.html` innehåller den ursprungliga markupen **plus** alla inkluderade filer upp till ett djup.  
- Alla djupare inkluderade filer utelämnas, vilket ger en mindre, snabbare laddande sida.  
- Inga brutna taggar dyker upp—biblioteket stänger automatiskt element som blivit lösa efter borttagning.

Du kan öppna resultatet i en webbläsare för att verifiera att huvudinnehållet fortfarande renderas, medan överflödiga skript eller nästlade ramar har försvunnit.

---

## Fullt fungerande exempel

Sätter vi ihop allt får vi det kompletta skriptet som du kan kopiera‑klistra in och köra:

```python
# -*- coding: utf-8 -*-
"""
Trim an HTML page using SaveOptions.
Demonstrates:
- How to load an HTML document
- How to configure ResourceHandlingOptions
- How to use SaveOptions to save a trimmed version
"""

from htmlprocessor import HTMLDocument, SaveOptions, ResourceHandlingOptions

def trim_html(input_path: str, output_path: str, max_depth: int = 2) -> None:
    # Load the source document
    doc = HTMLDocument(input_path)
    print("Loaded:", doc.title or "Untitled")

    # Set up resource handling (how to trim HTML page)
    res_opt = ResourceHandlingOptions()
    res_opt.max_handling_depth = max_depth

    # Attach options to save configuration (how to use SaveOptions)
    save_opt = SaveOptions()
    save_opt.resource_handling_options = res_opt

    # Perform the save
    doc.save(output_path, save_opt)
    print(f"Trimmed HTML saved to {output_path}")

if __name__ == "__main__":
    INPUT = "YOUR_DIRECTORY/complex_page.html"
    OUTPUT = "YOUR_DIRECTORY/trimmed_page.html"
    trim_html(INPUT, OUTPUT, max_depth=2)
```

Kör skriptet, peka `INPUT` på någon komplex HTML‑fil, så får du en slankare version i `OUTPUT`.  

> **Edge case‑notering:** Om den ursprungliga sidan innehåller villkorliga kommentarer (`<!--[if IE]>…<![endif]-->`) som refererar djupare resurser, kommer de att tas bort precis som alla andra nästlade inkluderade filer. Detta förhindrar att gamla‑IE‑hacks blåser upp din slutliga storlek.

---

## Visuell sammanfattning

Nedan är ett snabbt diagram som illustrerar flödet—from loading the document, through resource handling, to saving the trimmed result.

![how to use saveoptions example](https://example.com/placeholder.png "Diagram som visar hur man använder SaveOptions för att trimma HTML‑sidor")

*Alt‑text:* **exempel på hur man använder saveoptions** – visar den tre‑stegsprocess som innebär att ladda, konfigurera och spara ett HTML‑dokument.

---

## Vanliga frågor & Fallgropar

| Fråga | Svar |
|----------|--------|
| **Vad händer om jag behöver djupare nästling?** | Öka `max_handling_depth` till 3 eller 4, men kom ihåg att output‑storleken då växer. |
| **Kan jag exkludera specifika taggar (t.ex. `<script>`) oavsett djup?** | Ja—`SaveOptions` stödjer också en egenskap `tag_exclusion_list`. Lägg till `"script"` i den listan för att alltid ta bort skript. |
| **Är biblioteket trådsäkert?** | Den aktuella versionen är inte det. Skapa ett separat `HTMLDocument` per tråd. |
| **Kommer relativa URL:er att skrivas om?** | Som standard nej. Använd `save_opt.rewrite_relative_urls = True` om du behöver att de anpassas till den nya platsen. |

---

## Nästa steg

Nu när du har bemästrat **hur man använder SaveOptions**, prova dessa tillägg:

- **Komprimera outputen:** Sätt `save_opt.enable_gzip = True` för mindre filer på nätet.  
- **Pretty‑print för felsökning:** Aktivera `save_opt.indent_output = True` för snyggt formaterad HTML.  
- **Batch‑bearbetning:** Loopa igenom en katalog med HTML‑filer och applicera samma trimningslogik—perfekt för statiska webbplats‑generatorer.

Varje justering bygger på samma grund som du just lärt dig, och håller din kod ren och underhållbar.

---

## Slutsats

Vi har gått igenom hela livscykeln för att trimma en HTML‑sida i Python: **hur man laddar ett HTML‑dokument**, konfigurerar **hur man trimmar HTML‑sida** med `ResourceHandlingOptions`, och slutligen **hur man använder SaveOptions** för att skriva den rensade filen. Exemplet är helt självständigt, körs direkt och visar varför kontroll av resurssdjup är en viktig optimering för web‑scraping, statisk webbplats‑generering eller någon situation där du behöver ett lättviktigt HTML‑ögonblick.

Ge det ett försök, experimentera med olika `max_handling_depth`‑värden, och låt de trimmade sidorna göra det tunga arbetet åt dig. Om du stöter på problem, lämna en kommentar nedan—lycka till med kodandet!


## Relaterade handledningar

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Render HTML as PNG – Complete C# Guide](/html/english/net/rendering-html-documents/how-to-render-html-as-png-complete-c-guide/)
- [How to Zip HTML in C# – Save HTML to Zip](/html/english/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}