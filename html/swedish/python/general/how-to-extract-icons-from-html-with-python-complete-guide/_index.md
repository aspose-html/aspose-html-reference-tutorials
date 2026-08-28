---
category: general
date: 2026-07-02
description: Hur man extraherar ikoner från en HTML‑fil med Python. Lär dig att läsa
  HTML‑fil i Python, parsra HTML‑dokument och extrahera href‑attributet för att få
  favicon‑URL:er.
draft: false
keywords:
- how to extract icons
- read html file python
- parse html document
- extract href attribute
- extract favicon urls
language: sv
og_description: Hur man extraherar ikoner från en HTML-sida med Python. Denna handledning
  visar hur du läser en HTML-fil i Python, parsar dokumentet och hämtar favicon‑URL:er.
og_title: Hur man extraherar ikoner från HTML – Python‑guide
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: How to extract icons from an HTML file using Python. Learn to read
    HTML file python, parse HTML document, and extract href attribute to get favicon
    URLs.
  headline: How to Extract Icons from HTML with Python – Complete Guide
  type: TechArticle
- questions:
  - answer: Some sites embed icons via `<meta itemprop="image">`. Extend `is_icon_link`
      to also check for `meta` with `itemprop="image"` and pull its `content` attribute.
    question: What if the HTML uses `<meta>` tags for icons?
  - answer: Yes—just feed each URL into `requests.get(url, stream=True)` and write
      the content to a file. Remember to handle relative URLs with `urljoin`.
    question: Can I fetch the icons automatically?
  - answer: 'Absolutely. Replace the file‑reading step with `requests.get(page_url).text`
      and pass the HTML string to BeautifulSoup. Just be mindful of robots.txt and
      rate limits. --- ## Wrap‑Up We’ve covered **how to extract icons** from any
      static HTML using Python, from reading the file to printing out each f'
    question: Does this work on remote pages?
  type: FAQPage
tags:
- python
- html-parsing
- web‑scraping
- favicon
title: Hur man extraherar ikoner från HTML med Python – Komplett guide
url: /sv/python/general/how-to-extract-icons-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så extraherar du ikoner från HTML med Python – Komplett guide

Har du någonsin undrat **hur man extraherar ikoner** från en webbsida utan att öppna en webbläsare? Kanske bygger du ett webb‑katalog, ett SEO‑granskningsverktyg, eller är bara nyfiken på de små favicons som visas i flikar. Den goda nyheten är att du kan göra det på några rader Python—utan Selenium, utan headless Chrome, bara en ren‑text HTML‑fil.

I den här handledningen går vi igenom hur man läser en HTML‑fil med Python, parsar HTML‑dokumentet, och slutligen **extraherar href‑attributet** från `<link rel="icon">`‑taggar för att få dessa favicon‑URL:er. I slutet har du ett återanvändbart kodsnutt som fungerar på vilken statisk HTML du än kastar på den, och du får också se hur man hanterar kantfall som relativa sökvägar eller flera ikon‑deklarationer.

## Vad du kommer att lära dig

- Läs in en lokal HTML‑fil med Python (read html file python)  
- Använd en lättviktig parser för att **parse html document** säkert  
- Hitta `<link>`‑element som deklarerar en ikon  
- **Extrahera href‑attribut**‑värden och omvandla dem till absoluta URL:er  
- Samla och skriv ut alla upptäckta **favicon‑URL:er**  

Inga externa tjänster behövs—bara standardbiblioteket och det populära **BeautifulSoup**‑paketet.

---

![Screenshot showing Python script extracting icons – how to extract icons](https://example.com/images/extract-icons-python.png "how to extract icons")

*Image alt text: "hur man extraherar ikoner med ett Python‑skript"*

## Förutsättningar

- Python 3.8+ installerat  
- `beautifulsoup4`‑bibliotek (`pip install beautifulsoup4`)  
- En lokal HTML‑fil du vill skanna (t.ex. `sample.html`)  

Om du redan har dem, låt oss köra igång.

## Steg 1: Läs HTML‑fil med Python – Ladda dokumentet

Först och främst: vi måste öppna filen och mata dess innehåll till en parser. Att använda `with open(..., "r", encoding="utf‑8")` garanterar att filen stängs automatiskt, och UTF‑8‑kodningen hanterar de flesta moderna sidor.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Step 1: Load the HTML document from disk
html_path = Path("sample.html")          # adjust the path as needed
html_content = html_path.read_text(encoding="utf-8")
```

**Varför detta är viktigt:** Att öppna filen med rätt kodning förhindrar mystiska `�`‑tecken som kan bryta parsern senare. Att använda `Path` från standardbiblioteket gör också koden plattformsoberoende.

## Steg 2: Pars HTML‑dokument – Hitta alla ikon‑länkar

Nu ger vi den råa HTML‑koden till **BeautifulSoup**, som bygger ett navigerbart träd. Vi kommer att leta efter varje `<link>`‑tagg vars `rel`‑attribut innehåller ordet `icon`. Observera att `rel` kan vara en mellanslagsseparerad lista (`rel="shortcut icon"`), så vi behöver en flexibel kontroll.

```python
# Step 2: Parse the HTML and locate <link> tags that declare an icon
soup = BeautifulSoup(html_content, "html.parser")

def is_icon_link(tag):
    """Return True if a <link> tag declares an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    # BeautifulSoup may return a list or a string; handle both
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

icon_links = [tag for tag in soup.find_all(is_icon_link)]
```

**Varför detta steg är avgörande:** En naiv `soup.find_all("link", rel="icon")` skulle missa varianter som `rel="shortcut icon"` eller `rel="apple-touch-icon"`. Vår hjälpfunktion `is_icon_link` täcker dessa fall, vilket gör extraktionen robust.

## Steg 3: Extrahera href‑attribut – Hämta URL:erna

Med de relevanta taggarna samlade, hämtar vi nu `href`‑attributet från var och en. Vissa sidor kan utelämna `href` (sällsynt, men möjligt), så vi skyddar mot `None`. Dessutom anges favicons ofta med relativa URL:er, så vi kommer att lösa dem mot sidans bas‑URL om du känner till den. För en lokal fil behåller vi bara sökvägen som den är.

```python
# Step 3: Grab the href attribute from each icon link
icon_urls = []
for tag in icon_links:
    href = tag.get("href")
    if href:
        icon_urls.append(href.strip())
```

**Varför vi tar bort blanksteg:** HTML‑författare lägger ibland av misstag till mellanslag runt URL:er, vilket skulle bryta en efterföljande förfrågan. Trimning säkerställer att vi får rena strängar.

## Steg 4: Extrahera favicon‑URL:er – Visa resultatet

Till sist skriver vi ut (eller returnerar) listan med upptäckta URL:er. I ett verkligt skript kan du skriva dem till en CSV, ladda ner ikonerna, eller skicka dem till en annan tjänst. Här är en enkel loop som visar resultatet i konsolen.

```python
# Step 4: Display each discovered favicon URL
if not icon_urls:
    print("No icon links found in the document.")
else:
    for url in icon_urls:
        print("Favicon URL:", url)
```

### Hantera kantfall

- **Flera rel‑värden:** Vår `is_icon_link`‑kontroll fångar redan `rel="shortcut icon"` och `rel="apple-touch-icon"`.  
- **Relativa sökvägar:** Om du senare behöver absoluta URL:er, använd `urllib.parse.urljoin(base_url, href)`.  
- **Saknad href:** Guarden `if href:` hoppar över felaktiga taggar, vilket undviker `NoneType`‑fel.  
- **Duplicerade poster:** Du kan `icon_urls = list(dict.fromkeys(icon_urls))` för att ta bort dubbletter.

---

## Fullt skript – En‑stopp‑lösning

När vi sätter ihop allt, här är det kompletta, färdiga programmet. Spara det som `extract_icons.py` och peka `html_path` på vilken fil du vill.

```python
#!/usr/bin/env python3
"""
How to extract icons from an HTML file using Python.

This script:
- Reads an HTML file (read html file python)
- Parses the HTML document (parse html document)
- Finds <link> tags with rel containing "icon"
- Extracts the href attribute (extract href attribute)
- Prints each favicon URL (extract favicon urls)
"""

from pathlib import Path
from bs4 import BeautifulSoup

def is_icon_link(tag):
    """Detect <link> tags that declare an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

def extract_favicon_urls(html_path: Path):
    """Return a list of favicon URLs found in the given HTML file."""
    html_content = html_path.read_text(encoding="utf-8")
    soup = BeautifulSoup(html_content, "html.parser")
    icon_links = [t for t in soup.find_all(is_icon_link)]

    urls = []
    for tag in icon_links:
        href = tag.get("href")
        if href:
            urls.append(href.strip())
    # Remove duplicates while preserving order
    return list(dict.fromkeys(urls))

if __name__ == "__main__":
    # Adjust the path to point to your HTML file
    html_file = Path("sample.html")
    favicon_urls = extract_favicon_urls(html_file)

    if not favicon_urls:
        print("No icon links found in the document.")
    else:
        for url in favicon_urls:
            print("Favicon URL:", url)
```

**Förväntad output** (förutsatt att `sample.html` innehåller två ikoner):

```
Favicon URL: /images/favicon.ico
Favicon URL: https://example.com/assets/apple-touch-icon.png
```

Kör det med `python extract_icons.py` så ser du URL:erna skrivas ut i konsolen.

---

## Vanliga frågor

**Q: Vad händer om HTML använder `<meta>`‑taggar för ikoner?**  
**A:** Vissa webbplatser bäddar in ikoner via `<meta itemprop="image">`. Utöka `is_icon_link` för att också kontrollera `meta` med `itemprop="image"` och hämta dess `content`‑attribut.

**Q: Kan jag hämta ikonerna automatiskt?**  
**A:** Ja—mata bara varje URL i `requests.get(url, stream=True)` och skriv innehållet till en fil. Kom ihåg att hantera relativa URL:er med `urljoin`.

**Q: Fungerar detta på fjärrsidor?**  
**A:** Absolut. Ersätt fil‑läsningssteget med `requests.get(page_url).text` och skicka HTML‑strängen till BeautifulSoup. Tänk bara på robots.txt och hastighetsbegränsningar.

---

## Sammanfattning

Vi har gått igenom **hur man extraherar ikoner** från vilken statisk HTML som helst med Python, från att läsa filen till att skriva ut varje favicon‑URL. De grundläggande idéerna—läsa filen, parsra dokumentet, hitta rätt taggar och hämta `href`‑attributet—är återanvändbara mönster du kommer att stöta på i många web‑scraping‑uppgifter.

**Nästa steg?** Prova att utöka skriptet till:

- Lösa relativa URL:er mot sidans bas‑URL  
- Ladda ner varje ikon och spara den lokalt  
- Stödja ytterligare ikonformat (`rel="mask-icon"` för Safari)  

Experimentera gärna, och om du stöter på konstigheter, lämna en kommentar nedanför. Lycka till med parsningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Hur man frågar HTML i Java – Komplett handledning](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Hur man redigerar HTML-dokumentträd i Aspose.HTML för Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Spara HTML-dokument till fil i Aspose.HTML för Java](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}