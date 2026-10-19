---
category: general
date: 2026-07-27
description: Hur man använder SaveOptions i Aspose.HTML (Python) för att konvertera
  en stor HTML-sida och tillämpa resurs‑hantering effektivt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use SaveOptions
- convert large html page
- apply resource handling
- Aspose.HTML Python
- HTML resource handling
language: sv
lastmod: 2026-07-27
og_description: Hur du använder SaveOptions i Aspose.HTML (Python) låter dig konvertera
  stora HTML‑sidor samtidigt som du tillämpar resurshantering för rena, snabba resultat.
og_image_alt: Screenshot illustrating how to use SaveOptions in Aspose.HTML for Python
og_title: Hur man använder SaveOptions i Aspose.HTML – Python‑guide
schemas:
- author: Aspose
  dateModified: '2026-07-27'
  description: How to use SaveOptions in Aspose.HTML (Python) to convert large HTML
    page and apply resource handling efficiently.
  headline: How to Use SaveOptions in Aspose.HTML (Python)
  type: TechArticle
- questions:
  - answer: Aspose.HTML follows redirects but won’t send credentials automatically.
      You can pre‑download those assets or use a custom `WebRequest` handler (beyond
      this guide’s scope).
    question: What if the page references resources over HTTPS that require authentication?
  - answer: Yes—set `resource_options.max_handling_depth = 0`. This skips external
      files but leaves any `<style>` blocks intact.
    question: Can I preserve inline CSS while stripping external files?
  - answer: After saving, you can run a secondary pass with Pillow to downscale images,
      or let Aspose.HTML’s built‑in image compression options handle it (use `save_options.image_quality`).
    question: What about very large images that still bloat the output?
  - answer: The limit is global across all resource types (images, scripts, styles).
      If you need granular control, you’d have to filter resources manually after
      loading the document.
    question: Is the depth limit applied per‑resource type?
  type: FAQPage
tags:
- Aspose.HTML
- Python
- HTML processing
title: Hur man använder SaveOptions i Aspose.HTML (Python)
url: /sv/python/general/how-to-use-saveoptions-in-aspose-html-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder SaveOptions i Aspose.HTML (Python)

Att använda SaveOptions i Aspose.HTML för Python är något som många utvecklare frågar om när de hanterar massiva HTML‑filer. Om du behöver **convert large HTML page** medan du har ett fast grepp om **apply resource handling**, är du på rätt plats.  

I den här handledningen går vi igenom ett verkligt scenario: att ta en skrymmande HTML‑sida, begränsa hur djupt nästlade resurser hämtas, och slutligen spara (eller konvertera) resultatet med kristallklar kontroll. Inga vaga referenser, bara ett komplett, körbart exempel som du kan kopiera‑klistra in i ditt projekt idag.

> **Pro tip:** Aspose.HTML:s `SaveOptions` fungerar inte bara för att spara tillbaka till HTML utan även för att konvertera till PDF, PNG eller till och med DOCX. Mönstret vi beskriver nedan gäller för alla dessa format.

---

## Vad du behöver

- **Python 3.8+** (koden använder typindikatorer men körs på vilken recent version som helst)  
- **Aspose.HTML for Python via .NET** – installera med `pip install aspose-html`  
- En **large HTML file** du vill krympa eller transformera (exemplet använder `big_page.html`)  
- En måttlig mängd diskutrymme för utdatafilen  

Det är allt—inga extra bibliotek, inga tunga byggverktyg.

## Så använder du SaveOptions med Resource Handling Options

Detta är kärnan i saken. Vi skapar en `SaveOptions`‑instans, bifogar ett `ResourceHandlingOptions`‑objekt som talar om för Aspose.HTML hur djupt det ska följa länkade resurser, och sedan överlämnar vi allt till dokumentets `save`‑metod.

```python
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

# Load the source HTML document
input_path = "YOUR_DIRECTORY/big_page.html"
doc = HTMLDocument(input_path)

# Define how deep nested resources should be processed (limit to 3 levels)
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # <-- controls depth of resource fetching

# Attach the resource handling configuration to the save options
save_options = SaveOptions()
save_options.resource_handling_options = resource_options

# Save the processed document (or convert to another format if desired)
output_path = "YOUR_DIRECTORY/big_page_processed.html"
doc.save(output_path, save_options)
```

**Varför detta fungerar:**  
- `HTMLDocument` laddar den ursprungliga filen och parsar varje `<img>`, `<link>`, `<script>` osv.  
- `ResourceHandlingOptions.max_handling_depth` talar om för motorn att sluta följa resurser efter tre nivåer av nästling—perfekt för att undvika oändliga slingor på sidor som bäddar in andra sidor.  
- `SaveOptions` är behållaren som bär både utdataformatet (HTML som standard) och reglerna för resource handling.  
- Slutligen skriver `doc.save` den nya filen och tillämpar de regler vi just ställt in.

När du kör skriptet kommer du att se en ny fil på `big_page_processed.html`. Öppna den i en webbläsare; du kommer att märka att alla bilder, stilar och skript upp till tre nivåer djup fortfarande finns kvar, medan djupare referenser har tagits bort. Detta minskar filstorleken dramatiskt utan att bryta sidans grundläggande layout—precis vad du behöver när du **convert large HTML page** för offline‑användning eller e‑postleverans.

## Konvertera stora HTML‑sidor effektivt

Om ditt mål är att *convert large HTML page* till en smalare version, gör kodsnutten ovan redan det mesta av det tunga arbetet. Du kanske ändå vill ändra utdataformatet helt och hållet. Aspose.HTML gör det till en enradare:

```python
# Convert to PDF instead of HTML
pdf_save_options = SaveOptions()
pdf_save_options.resource_handling_options = resource_options
pdf_save_options.format = "PDF"   # specify desired format

doc.save("YOUR_DIRECTORY/big_page.pdf", pdf_save_options)
```

Byt bara ut `format`‑egenskapen mot `"PNG"`, `"JPEG"` eller `"DOCX"` så har du en komplett konverteringspipeline. Samma **apply resource handling**‑regler förblir intakta, så den resulterande PDF‑filen kommer inte att bädda in varje extern CSS‑fil från den ursprungliga webbplatsen—endast de inom den tre‑nivå djup du definierade.

## Tillämpa Resource Handling på nästlade resurser

Låt oss gräva lite djupare i **apply resource handling** på ett effektivt sätt. Föreställ dig att din HTML innehåller en stilmall som i sin tur importerar andra stilmallar, var och en som hämtar bilder. Utan en djupgräns kan Aspose.HTML följa kedjan i all oändlighet, vilket ökar minne och CPU‑användning.

```python
# Example: limit to 1 level for aggressive trimming
resource_options.max_handling_depth = 1
save_options.resource_handling_options = resource_options
doc.save("trimmed_page.html", save_options)
```

- **Depth 0** – Inga externa resurser hämtas; du får ett minimalistiskt HTML‑skelett.  
- **Depth 1** – Endast resurser på första nivån (direkta `<img>`‑taggar, omedelbara CSS‑filer) inkluderas.  
- **Depth 2+** – Djupare nästling respekteras, användbart för komplexa webbplatser där stilar beror på andra stilar.

Välj det djup som matchar ditt **convert large HTML page**‑scenario. För e‑postnyhetsbrev räcker ofta depth 1. För ett lokalt arkiv ger depth 3 (som i huvudexemplet) en bra balans.

## Fullt fungerande exempel – Från början till slut

Nedan är ett fristående skript som du kan lägga i en fil som heter `process_html.py`. Det innehåller felhantering, loggning och en liten hjälpfunktion som skriver ut den storleksreduktion du uppnått.

```python
import os
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

def process_html(
    src_path: str,
    dst_path: str,
    depth: int = 3,
    fmt: str = "HTML"
) -> None:
    """
    Loads an HTML file, applies resource handling, and saves it in the requested format.
    Returns nothing; prints size statistics for quick verification.
    """
    if not os.path.isfile(src_path):
        raise FileNotFoundError(f"Source file not found: {src_path}")

    # Load document
    doc = HTMLDocument(src_path)

    # Set up resource handling
    res_opts = ResourceHandlingOptions()
    res_opts.max_handling_depth = depth

    # Configure save options (including format)
    save_opts = SaveOptions()
    save_opts.resource_handling_options = res_opts
    save_opts.format = fmt.upper()   # Aspose expects upper‑case format strings

    # Perform save / conversion
    doc.save(dst_path, save_opts)

    # Report size change
    original = os.path.getsize(src_path)
    final = os.path.getsize(dst_path)
    reduction = (original - final) / original * 100
    print(f"Saved {fmt.lower()} to '{dst_path}'. Size reduced by {reduction:.2f}%.")

# -------------------------------------------------------------------------
# Example usage
if __name__ == "__main__":
    input_file = "YOUR_DIRECTORY/big_page.html"
    output_file = "YOUR_DIRECTORY/big_page_processed.html"

    process_html(
        src_path=input_file,
        dst_path=output_file,
        depth=3,          # apply resource handling up to three levels
        fmt="HTML"       # change to "PDF" or "PNG" to convert format
    )
```

**Förväntad utdata (konsol):**

```
Saved html to 'YOUR_DIRECTORY/big_page_processed.html'. Size reduced by 42.57%.
```

Öppna den bearbetade filen; du kommer att se en smalare sida som fortfarande ser ut som originalet. Om du bytte `fmt` till `"PDF"` skulle konsolen rapportera en PDF‑filstorlek och du kan öppna den i vilken PDF‑visare som helst.

## Vanliga frågor & edge‑cases

- **What if the page references resources over HTTPS that require authentication?**  
  Aspose.HTML följer omdirigeringar men skickar inte automatiskt autentiseringsuppgifter. Du kan för‑ladda dessa tillgångar eller använda en anpassad `WebRequest`‑hanterare (utanför denna guides omfattning).

- **Can I preserve inline CSS while stripping external files?**  
  Ja—sätt `resource_options.max_handling_depth = 0`. Detta hoppar över externa filer men lämnar alla `<style>`‑block intakta.

- **What about very large images that still bloat the output?**  
  Efter sparande kan du köra ett sekundärt pass med Pillow för att skala ner bilder, eller låta Aspose.HTML:s inbyggda bildkomprimeringsalternativ hantera det (använd `save_options.image_quality`).

- **Is the depth limit applied per‑resource type?**  
  Gränsen är global över alla resurstyper (bilder, skript, stilar). Om du behöver finare kontroll måste du filtrera resurser manuellt efter att dokumentet har laddats.

## Slutsats

Du har nu en solid förståelse för **how to use SaveOptions** i Aspose.HTML

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Hur man konverterar HTML till PDF Java – med Aspose.HTML för Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Hur man konverterar HTML till MHTML med Aspose.HTML för Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [Hur man använder Aspose för att rendera HTML till PNG – steg‑för‑steg‑guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}