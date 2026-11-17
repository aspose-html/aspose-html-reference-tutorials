---
category: general
date: 2026-08-06
description: Převod HTML do PDF v Pythonu s kompletním příkladem. Naučte se generovat
  PDF z HTML, uložit HTML jako PDF a řešit běžné okrajové případy.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to pdf
- generate pdf from html
- save html as pdf
- create pdf from html file
- how to convert html to pdf
language: cs
lastmod: 2026-08-06
og_description: Převádějte HTML do PDF v Pythonu a automatizujte tvorbu dokumentů.
  Postupujte podle tohoto návodu k vytvoření PDF z HTML, uložení HTML jako PDF a přizpůsobení
  výstupu.
og_image_alt: Example of convert html to pdf script in Python
og_title: Převod HTML do PDF v Pythonu – komplexní tutoriál
schemas:
- author: Aspose
  dateModified: '2026-08-06'
  description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  headline: Convert HTML to PDF in Python – step‑by‑step guide
  type: TechArticle
- description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  name: Convert HTML to PDF in Python – step‑by‑step guide
  steps:
  - name: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
    text: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
  - name: '**Input handling** – read the HTML file or build the markup programmatically.'
    text: '**Input handling** – read the HTML file or build the markup programmatically.'
  - name: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
    text: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
  type: HowTo
tags:
- HTML to PDF
- Python
- Document conversion
title: Převod HTML do PDF v Pythonu – krok za krokem
url: /cs/python/general/convert-html-to-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod HTML do PDF v Pythonu – krok za krokem průvodce

Pokud potřebujete **rychle převést HTML do PDF**, tento tutoriál ukazuje kompletní řešení v Pythonu. Uvidíte, jak generovat PDF z HTML, uložit HTML jako PDF a řídit proces převodu, aniž byste opustili svůj kód.

Průvodce vás provede instalací spolehlivé knihovny, načtením HTML dokumentu, provedením převodu a ověřením výsledku. Na konci budete schopni vytvořit PDF z HTML souboru v jakémkoli Python projektu, ať už je zdroj statická stránka nebo dynamicky generovaný markup.

## Co se naučíte

* Nainstalovat závislosti `pdfkit` a `wkhtmltopdf` potřebné pro převod HTML → PDF.  
* Načíst HTML dokument z disku nebo z řetězce.  
* Generovat PDF z HTML s vlastní velikostí stránky, okraji a nastavením kódování.  
* Uložit HTML jako PDF pomocí jediné funkce.  
* Zvládnout typické okrajové případy, jako chybějící assety, Unicode znaky a velké soubory.  

**Předpoklady** – Python 3.8+ a základní znalost práce se soubory. Žádné externí služby nejsou vyžadovány.

## Převod HTML do PDF – celkový pracovní postup

Proces převodu se skládá ze tří logických fází:

1. **Příprava** – nainstalovat konvertor a zajistit, aby byl binární soubor `wkhtmltopdf` dostupný.  
2. **Zpracování vstupu** – přečíst HTML soubor nebo vytvořit markup programově.  
3. **Generování výstupu** – spustit konvertor, zapsat PDF soubor a potvrdit výsledek.

Každá fáze je podrobně popsána v následujících krocích.

## Krok 1: Instalace požadovaných knihoven

`pdfkit` poskytuje tenký Python wrapper kolem široce používaného enginu `wkhtmltopdf`. Nainstalujte oba pomocí `pip` a ověřte cestu k binárnímu souboru.

```bash
# Install the Python wrapper
pip install pdfkit

# On Ubuntu/Debian install wkhtmltopdf package
sudo apt-get install wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf
```

Pokud dáváte přednost přenosnému binárnímu souboru, stáhněte si vhodné vydání ze [stránky wkhtmltopdf na GitHubu](https://github.com/wkhtmltopdf/wkhtmltopdf/releases) a umístěte jej do adresáře, který je zahrnut ve vaší `PATH`. Skript později automaticky zkontroluje cestu.

## Krok 2: Načtení HTML dokumentu

Můžete číst statický soubor, stáhnout vzdálený obsah nebo sestavit HTML za běhu. Níže uvedený příklad načte lokální soubor `sample.html` umístěný v adresáři, který určíte.

```python
import pathlib
import pdfkit

# Define the directory that holds the HTML source
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")

# Resolve the full path to the HTML file
html_path = BASE_DIR / "sample.html"

# Read the file content as a UTF‑8 string
with html_path.open(encoding="utf-8") as f:
    html_content = f.read()
```

Čtení souboru jako Unicode řetězce zajišťuje, že znaky jako “é”, “ß” nebo asijské glyfy zůstanou během převodu zachovány. Tento krok je nezbytný, když **generujete PDF z HTML**, které obsahuje mezinárodní text.

## Krok 3: Generování PDF z HTML

`pdfkit.from_string` převádí řetězec obsahující HTML markup do PDF souboru. Do funkce můžete předat slovník s volbami pro nastavení velikosti stránky, okrajů a chování hlaviček/patiček.

```python
# Define the output PDF path
pdf_path = BASE_DIR / "sample.pdf"

# Conversion options – adjust as needed
options = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left": "0.75in",
    "encoding": "UTF-8",
    "enable-local-file-access": None,  # Allows loading local images/CSS
}

# Perform the conversion
pdfkit.from_string(html_content, str(pdf_path), options=options)
```

Volání výše **vytvoří PDF ze souboru HTML** uloženého v `sample.pdf`. Pokud zdrojové HTML odkazuje na lokální CSS nebo obrázky, příznak `enable‑local‑file‑access` umožní `wkhtmltopdf` tyto zdroje vyřešit.

### Proč tento přístup funguje

* `pdfkit` deleguje těžkou práci na `wkhtmltopdf`, který renderuje HTML pomocí WebKit enginu a zaručuje vysokou věrnost původnímu rozvržení.  
* Poskytnutí slovníku s volbami vám umožní jemně doladit výstup, aniž byste museli měnit samotné HTML.  
* Použití `from_string` udržuje celý workflow v paměti, což je užitečné, když je HTML generováno za běhu.

## Krok 4: Uložení HTML jako PDF a ověření výstupu

Po převodu můžete chtít potvrdit, že PDF existuje a je čitelné. Níže uvedený úryvek kontroluje velikost souboru a otevře PDF ve výchozím prohlížeči systému (platform‑specifické).

```python
import os
import subprocess
import sys

# Verify that the PDF file was created
if pdf_path.is_file() and pdf_path.stat().st_size > 0:
    print(f"✅ PDF generated successfully: {pdf_path}")

    # Open the PDF for visual verification (optional)
    if sys.platform.startswith("darwin"):      # macOS
        subprocess.run(["open", str(pdf_path)])
    elif os.name == "nt":                      # Windows
        os.startfile(str(pdf_path))
    else:                                      # Linux and others
        subprocess.run(["xdg-open", str(pdf_path)])
else:
    raise FileNotFoundError("PDF generation failed – file not found or empty.")
```

Spuštění skriptu vypíše zprávu o úspěchu a spustí PDF prohlížeč, takže můžete okamžitě ověřit, že rozvržení odpovídá původnímu HTML. Tento krok dokončuje cyklus **uložit html jako pdf**.

## Krok 5: Pokročilé možnosti – vytvořit PDF ze souboru HTML s vlastními nastaveními

Někdy máte fyzický HTML soubor na disku a raději použijete `pdfkit.from_file` místo načítání obsahu sami. Tento způsob je užitečný, když HTML již obsahuje složité relativní cesty.

```python
# Directly convert a file path to PDF
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

Můžete také vložit titulní stránku, obsah nebo příznaky pro spuštění JavaScriptu rozšířením slovníku `options`. Například pro přidání titulní stránky:

```python
options.update({
    "cover": str(BASE_DIR / "cover.html"),
    "toc": None,  # Generates a table of contents
})
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

Tyto úpravy demonstrují **jak převést HTML do PDF** pro sofistikovanější publikační pipeline.

## Časté úskalí a jak se jim vyhnout

| Problém | Příčina | Řešení |
|-------|-------|--------|
| Obrázky nebo CSS se nezobrazují | `wkhtmltopdf` ve výchozím nastavení blokuje lokální přístup k souborům | Přidejte `"enable-local-file-access": None` do slovníku s volbami |
| Unicode znaky jsou poškozené | Chybějící volba `encoding` nebo čtení souboru s nesprávným charsetem | Vždy nastavte `"encoding": "UTF-8"` a čtěte HTML soubor s UTF‑8 |
| PDF je prázdné | Nesprávná cesta k binárnímu souboru `wkhtmltopdf` | Zadejte cestu explicitně: `pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")` |
| Velké HTML soubory způsobují timeout | Výchozí timeout je příliš krátký | Nastavte `"javascript-delay": "2000"` nebo prodlužte timeout pomocí `"timeout": "60"` |

Řešením těchto problémů zajistíte spolehlivý **generate pdf from html** proces napříč různými prostředími.

## Kompletní skript – end‑to‑end příklad

Uložte následující kód jako `html_to_pdf.py` a spusťte jej pomocí `python html_to_pdf.py`. Upravit `YOUR_DIRECTORY` tak, aby ukazoval na váš projektový adresář.

```python
#!/usr/bin/env python3
"""
Convert HTML to PDF in Python – complete, runnable example.
"""

import pathlib
import pdfkit
import os
import subprocess
import sys

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")          # <-- change this
HTML_FILE = BASE_DIR / "sample.html"
PDF_FILE = BASE_DIR / "sample.pdf"

# wkhtmltopdf configuration (optional – only needed if binary is not on PATH)
# config = pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")

# Conversion options – customize as required
OPTIONS = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left":


## Co byste se měli naučit dál?


Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s krok‑za‑krokem vysvětlením, které vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vlastních projektech.

- [Jak převést HTML do PDF v Javě – pomocí Aspose.HTML pro Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Převod HTML do PDF v .NET s Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Jak převést HTML do PDF v Javě – nastavit okraje stránky s Aspose.HTML](/html/english/java/advanced-usage/css-extensions-adding-title-page-number/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}