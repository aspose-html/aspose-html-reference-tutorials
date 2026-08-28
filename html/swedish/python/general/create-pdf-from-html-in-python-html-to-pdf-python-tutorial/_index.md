---
category: general
date: 2026-07-15
description: Skapa PDF från HTML med Python. Lär dig hur du snabbt konverterar HTML
  till PDF med ett enkelt skript och tydliga steg.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf from html
- convert html to pdf
- html to pdf python
- save html as pdf
- html to pdf tutorial
language: sv
lastmod: 2026-07-15
og_description: Skapa PDF från HTML med Python. Den här guiden visar hur du konverterar
  HTML till PDF, sparar HTML som PDF och hanterar resurser effektivt.
og_image_alt: Screenshot of a Python script that creates PDF from HTML
og_title: Skapa PDF från HTML i Python – Praktisk handledning
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
title: Skapa PDF från HTML i Python – HTML till PDF Python‑handledning
url: /sv/python/general/create-pdf-from-html-in-python-html-to-pdf-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa PDF från HTML i Python – Full‑funktionell handledning

Har du någonsin behövt **skapa PDF från HTML** men varit osäker på vilket Python‑bibliotek du ska välja? Du är inte ensam—många utvecklare stöter på samma problem när de försöker omvandla en webbrapport, faktura eller marknadsföringssida till en utskrivbar PDF.  

Den goda nyheten är att du med bara några rader kod kan **konvertera HTML till PDF** på ett pålitligt sätt, och skriptet fungerar på Windows, macOS och Linux. I den här guiden går vi igenom ett komplett, körbart exempel, förklarar varför varje steg är viktigt och visar dig hur du **sparar HTML som PDF** utan lösa trådar.

---

## Vad du kommer att lära dig

- Installera rätt Python‑paket för HTML‑till‑PDF‑konvertering.  
- Läs in en HTML‑fil med anpassade resurshanteringsalternativ (för att undvika oändliga CSS‑import).  
- Generera en ren PDF‑fil på disk.  
- Hantera vanliga kantfall som externa bilder, relativa sökvägar och stora dokument.  

I slutet av den här **HTML‑till‑PDF‑handledningen** har du en återanvändbar funktion som du kan lägga in i vilket projekt som helst.

---

## Förutsättningar

- Python 3.9+ (koden fungerar även med 3.8, men 3.9+ ger dig de senaste `pathlib`‑funktionerna).  
- Grundläggande kunskap om kommandoraden och virtuella miljöer.  
- En HTML‑fil som du vill omvandla till en PDF—vilken statisk sida som helst fungerar.

> **Proffstips:** Om du använder en virtuell miljö, aktivera den innan du installerar biblioteket; det håller din globala Python‑installation ren.

---

## Steg 1 – Installera WeasyPrint (motorn bakom konverteringen)

WeasyPrint är ett rent Python‑bibliotek som renderar HTML och CSS till PDF. Det hanterar de flesta moderna webbfunktioner och ger dig fin‑granulär kontroll över resurshämtning.

```bash
pip install weasyprint
```

Att köra kommandot ovan hämtar `cairocffi`, `tinycss2` och några andra beroenden. Om du får ett `cairo`‑relaterat fel på Windows, hämta de förbyggda wheels från [WeasyPrint website](https://weasyprint.org/docs/install/).

---

## Steg 2 – Förbered en liten hjälparfunktion för resurshantering

När du laddar ett HTML‑dokument som refererar till externa stilmallar eller bilder, kommer biblioteket att följa dessa länkar. I vissa fall leder det till djup nästling eller till och med oändliga slingor (tänk på en CSS‑fil som `@import`ar sig själv). För att hålla det ordnat begränsar vi djupet för resurshanteringen.

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

Klassen ovan krävs inte av WeasyPrint, men den speglar mönstret du såg i det ursprungliga kodsnutten och ger dig en möjlighet att stoppa okontrollerade importeringar. Du kommer att se den användas i nästa steg.

---

## Steg 3 – Läs in HTML‑dokumentet med de anpassade alternativen

Nu läser vi faktiskt HTML‑filen. `HTML`‑klassen accepterar ett `base_url`‑argument, som vi sätter till katalogen som innehåller källfilen—detta får relativa länkar att fungera utan en webbserver.

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

> **Varför detta är viktigt:** Om ditt HTML‑dokument hämtar en kaskad av CSS‑filer, kommer varje `@import` att trigga en ny hämtning. Djupskyddet förhindrar att skriptet spårar ur.

---

## Steg 4 – Spara det bearbetade dokumentet som PDF

Med `HTML`‑objektet i handen är genereringen av en PDF en endasrad. Vi skickar också med ett enkelt CSS‑snutt som tvingar en ren sidstorlek (A4) och lägger till en liten marginal—justera gärna efter behov.

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

Genom att anropa `write_pdf` strömmar PDF‑filen till disk, så du får en färdig‑att‑dela fil.

---

## Steg 5 – Sätt ihop allt

Nedan är ett kompakt skript som du kan kopiera och klistra in i `convert.py`. Ersätt platshållar‑sökvägarna med dina faktiska kataloger.

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

**Förväntad output** – efter att ha kört `python convert.py` bör du se:

```
✅ PDF saved to /full/path/YOUR_DIRECTORY/output.pdf
```

Öppna den genererade filen med någon PDF‑visare; du kommer att se den ursprungliga sidlayouten, CSS‑stilarna och bilderna (förutsatt att de var åtkomliga från HTML‑filen).  

Om du märker saknade bilder, dubbelkolla att deras `src`‑attribut antingen är absoluta URL:er eller relativa sökvägar som finns under `YOUR_DIRECTORY`.

---

## Vanliga frågor & hantering av kantfall

| Question | Answer |
|----------|--------|
| *Vad händer om mitt HTML refererar till externa typsnitt?* | WeasyPrint kommer att ladda ner typsnitts‑filerna automatiskt, men du kanske vill vitlista domäner för att undvika långa hämtningstider. |
| *Kan jag konvertera en HTML‑sträng istället för en fil?* | Ja—använd `HTML(string=my_html_string)` och hoppa över `base_url` eller sätt den till en temporär mapp. |
| *Hur styr jag PDF‑metadata (titel, författare)?* | Skicka en `metadata`‑dict till `write_pdf`, t.ex. `html_doc.write_pdf(target='out.pdf', metadata={'Title': 'Report'})`. |
| *Jag får ett “cairo‑cffi error” på Linux.* | Installera systempaketet `libcairo2-dev` (`apt-get install libcairo2-dev` på Debian/Ubuntu) innan du pip‑installerar WeasyPrint. |

---

## Sammanfattning

Vi har just **skapat PDF från HTML** med ett rent Python‑arbetsflöde, gått igenom **konvertera HTML till PDF**‑mekaniken och visat dig hur du **sparar HTML som PDF** med robust resurshantering. Skriptet är tillräckligt litet för att läggas in i CI‑pipelines, men ändå flexibelt nog att utökas med anpassade sidhuvuden, sidfötter eller vattenstämplar.

Nästa steg du kan utforska:

- Använd **html to pdf python**‑biblioteket `pdfkit` för en wkhtmltopdf‑baserad metod (bra för äldre CSS).  
- Lägg till ett CLI‑gränssnitt med `argparse` så att skriptet accepterar in‑/ut‑argument.  
- Generera PDF‑filer i realtid i ett Flask‑ eller FastAPI‑endpoint för rapporter på begäran.  

Känn dig fri att experimentera, bryta saker, och sedan återvända till den här guiden för en snabb uppfriskning. Om du stöter på problem är WeasyPrint‑dokumentationen och community‑forumen utmärkta resurser.

Lycka till med kodandet, och njut av att förvandla dessa webbsidor till slanka PDF‑filer!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Konvertera HTML till PDF med Aspose.HTML – Fullständig manipuleringsguide](/html/english/)
- [Konvertera HTML till PDF i .NET med Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Skapa PDF från HTML – C# steg‑för‑steg‑guide](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}