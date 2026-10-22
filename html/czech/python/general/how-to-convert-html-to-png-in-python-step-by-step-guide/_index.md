---
category: general
date: 2026-10-21
description: Naučte se rychle převádět HTML na PNG. Tento tutoriál také pokrývá export
  webové stránky do PNG a převod HTML souboru na PNG pomocí Pythonu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to png
- export webpage to png
- how to convert html to image
- convert html file to png
language: cs
lastmod: 2026-10-21
og_description: Převod HTML na PNG pomocí Pythonu. Postupujte podle tohoto přehledného
  návodu, jak exportovat webovou stránku do PNG, řešit okrajové případy a automatizovat
  tvorbu obrázků.
og_image_alt: Screenshot of HTML page converted to PNG using Python
og_title: Převod HTML na PNG v Pythonu – kompletní programovací průvodce
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  headline: How to convert HTML to PNG in Python – step‑by‑step guide
  type: TechArticle
- description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  name: How to convert HTML to PNG in Python – step‑by‑step guide
  steps:
  - name: Expected output
    text: 'Running the script prints:'
  - name: Why adjust viewport size?
    text: Web pages designed for desktop screens often look cramped if rendered at
      a small width. By increasing the `width` and `height` options, you capture the
      full layout, which is especially useful for **export webpage to PNG** tasks.
  - name: 6.1 Large pages or infinite scroll
    text: 'For pages that load content lazily (e.g., infinite scroll), increase the
      JavaScript delay and optionally set a larger viewport:'
  - name: 6.2 Authentication‑protected pages
    text: 'If a page requires a session cookie, you can embed the cookie header:'
  - name: 6.3 Missing images or fonts
    text: '`wkhtmltoimage` respects the `--disable-local-file-access` flag for security.
      If your HTML references local assets, enable them explicitly:'
  type: HowTo
tags:
- python
- html conversion
- image processing
- web automation
title: Jak převést HTML na PNG v Pythonu – krok za krokem průvodce
url: /cs/python/general/how-to-convert-html-to-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod HTML na PNG v Pythonu – kompletní programovací průvodce

Pokud potřebujete **convert HTML to PNG**, tento průvodce vám ukáže spolehlivý způsob, jak to provést pomocí čistého Pythonu. Ať už exportujete statickou zprávu, generujete miniatury pro galerii nebo automatizujete screenshoty pro testování, získáte kompletní, spustitelný řešení během několika minut.

Také uvidíte, jak **export webpage to PNG**, pochopíte rozdíl mezi převodem HTML souboru a živým URL a naučíte se osvědčené postupy pro práci s velkými stránkami nebo dynamickým obsahem. Žádné externí služby nejsou vyžadovány – stačí jen pár Python balíčků a krátký skript.

## Požadavky

- Python 3.9+ nainstalován (kód funguje na Windows, macOS a Linuxu)
- Přístup k terminálu nebo příkazovému řádku
- Základní znalost správce balíčků Pythonu (`pip`)

Budete potřebovat balíček `imgkit` (tenký wrapper kolem `wkhtmltoimage`) a samotný binární soubor `wkhtmltoimage`. Oba jsou zdarma a open‑source.

## Krok 1: Instalace požadovaných nástrojů

Prvním krokem je nainstalovat `wkhtmltoimage` a Python wrapper, který s ním komunikuje.

```bash
# Install wkhtmltoimage (Linux example)
sudo apt-get update && sudo apt-get install -y wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf

# On Windows download the installer from:
# https://wkhtmltopdf.org/downloads.html
# and add the installation folder to your PATH.

# Install the Python wrapper
pip install imgkit
```

> **Proč je tento krok důležitý** – `wkhtmltoimage` renderuje HTML pomocí WebKit enginu a vytváří pixel‑dokonalé PNG. `imgkit` jednoduše předává vaše volby binárnímu souboru, takže získáte stejnou kvalitu jako v prohlížeči.

## Krok 2: Ověření instalace

Spusťte rychlou kontrolu, abyste potvrdili, že je binární soubor dostupný z Pythonu.

```python
import imgkit

# This will raise an exception if wkhtmltoimage is not found
print("wkhtmltoimage version:", imgkit.config().wkhtmltoimage)
```

Pokud skript vypíše cestu k `wkhtmltoimage`, jste připraveni převést HTML na PNG. Pokud dostanete `OSError`, zkontrolujte, že je binární soubor ve vašem systémovém `PATH`.

## Krok 3: Napište znovupoužitelnou konverzní funkci

Zabalení logiky do funkce usnadní **convert HTML file to PNG** nebo **export webpage to PNG** z libovolného místa ve vašem projektu.

```python
import os
import imgkit

def convert_html_to_png(source, output_path, *, options=None):
    """
    Convert an HTML file or URL to a PNG image.

    Parameters
    ----------
    source : str
        Path to a local HTML file (e.g., "report.html") or a URL
        (e.g., "https://example.com").
    output_path : str
        Destination file path for the PNG (e.g., "report.png").
    options : dict, optional
        imgkit options such as viewport size, zoom factor, or
        JavaScript delay. If omitted, sensible defaults are used.

    Returns
    -------
    bool
        True if the conversion succeeded, False otherwise.
    """
    # Use a default set of options if none are provided
    default_options = {
        "format": "png",
        "quality": "100",
        "encoding": "UTF-8",
        "quiet": "",
        # Render at 1280×720 – adjust for your layout
        "width": 1280,
        "height": 720,
        # Wait for JavaScript to finish (ms)
        "javascript-delay": 500,
    }
    # Merge user‑supplied options over defaults
    final_options = {**default_options, **(options or {})}

    try:
        # imgkit can handle both files and URLs transparently
        imgkit.from_file(source, output_path, options=final_options) \
            if os.path.isfile(source) else \
            imgkit.from_url(source, output_path, options=final_options)
        print(f"✅ Successfully saved PNG to: {output_path}")
        return True
    except Exception as e:
        print(f"❌ Conversion failed: {e}")
        return False
```

> **Proč obalujeme jak `from_file`, tak `from_url`** – Tato funkce nyní podporuje **how to convert HTML to image** pro lokální soubory i živé webové stránky, čímž udržuje váš kód DRY (Don’t Repeat Yourself).

## Krok 4: Převod lokálního HTML souboru na PNG

Umístěte HTML soubor s názvem `sample.html` do složky `assets`. Pak zavolejte pomocnou funkci, kterou jsme právě definovali:

```python
if __name__ == "__main__":
    # Example: convert a static HTML file
    html_path = os.path.join("assets", "sample.html")
    png_path = os.path.join("output", "sample.png")

    # Ensure the output directory exists
    os.makedirs(os.path.dirname(png_path), exist_ok=True)

    # Perform the conversion
    success = convert_html_to_png(html_path, png_path)

    if success:
        # Show a tiny preview in the console (optional)
        from PIL import Image
        img = Image.open(png_path)
        img.thumbnail((200, 200))
        img.show()
```

### Očekávaný výstup

Spuštěním skriptu se vypíše:

```
✅ Successfully saved PNG to: output/sample.png
```

Nový soubor `output/sample.png` nyní obsahuje pixel‑dokonalý snímek `sample.html`. Otevřením v libovolném prohlížeči obrázků uvidíte vykreslenou stránku přesně tak, jak by se zobrazila v prohlížeči.

## Krok 5: Export živé webové stránky do PNG

Pokud potřebujete **export webpage to PNG** pro URL, která se často mění (např. dashboard), stačí předat řetězec URL místo cesty k souboru.

```python
# Example: convert a live page
url = "https://developer.mozilla.org/en-US/docs/Web/HTML"
output_file = "output/mdn_homepage.png"

convert_html_to_png(url, output_file, options={"width": 1920, "height": 1080})
```

### Proč upravit velikost viewportu?

Webové stránky navržené pro desktopové obrazovky často vypadají stísněně, pokud jsou renderovány na malé šířce. Zvýšením možností `width` a `height` zachytíte kompletní rozvržení, což je zvláště užitečné pro úlohy **export webpage to PNG**.

## Krok 6: Řešení běžných okrajových případů

### 6.1 Velké stránky nebo nekonečné posouvání

Pro stránky, které načítají obsah líně (např. nekonečné posouvání), zvyšte JavaScriptové zpoždění a případně nastavte větší viewport:

```python
options = {
    "javascript-delay": 2000,   # wait 2 seconds for JS to finish
    "width": 1440,
    "height": 3000,             # tall enough for the whole page
    "disable-smart-width": "", # forces the width we set
}
convert_html_to_png(url, "long_page.png", options=options)
```

### 6.2 Stránky chráněné autentizací

Pokud stránka vyžaduje session cookie, můžete vložit hlavičku cookie:

```python
options = {
    "custom-header": [
        "Cookie: sessionid=YOUR_SESSION_ID"
    ]
}
convert_html_to_png("https://internal.example.com/report", "report.png", options=options)
```

### 6.3 Chybějící obrázky nebo fonty

`wkhtmltoimage` respektuje příznak `--disable-local-file-access` z bezpečnostních důvodů. Pokud váš HTML odkazuje na lokální zdroje, povolte je explicitně:

```python
options = {"enable-local-file-access": ""}
convert_html_to_png("assets/complex.html", "complex.png", options=options)
```

## Krok 7: Programové ověření výsledku (volitelné)

Někdy potřebujete potvrdit, že PNG byl vygenerován správně (např. v CI pipeline). Následující úryvek kontroluje velikost souboru a rozměry:

```python
from pathlib import Path
from PIL import Image

def verify_png(path):
    p = Path(path)
    if not p.is_file():
        raise FileNotFoundError(f"{path} does not exist")
    if p.stat().st_size < 10_000:  # arbitrary minimal size
        raise ValueError("Generated PNG seems too small")
    with Image.open(p) as img:
        print(f"Image size: {img.width}×{img.height}, mode: {img.mode}")

verify_png(png_path)
```

Pokud PNG projde těmito kontrolami, můžete jej bezpečně použít v následných procesech, jako je generování PDF, přílohy e‑mailů nebo strojové učení.

## Závěr

Nyní máte kompletní, produkčně připravenou metodu pro **convert HTML to PNG** pomocí Pythonu. Průvodce pokryl:

- Instalaci `wkhtmltoimage` a `imgkit`
- Ověření prostředí
- Znovupoužitelnou funkci `convert_html_to_png`, která zpracovává jak lokální soubory, tak URL
- Reálné příklady pro **export webpage to PNG**, **how to convert HTML to image** a **convert HTML file to PNG**
- Řešení okrajových případů pro velké stránky, autentizaci a lokální zdroje
- Volitelné kroky ověření pro CI/CD pipeline

Neváhejte experimentovat s dalšími možnostmi `imgkit` – například `zoom`, `crop-h` nebo `crop-w` – a doladit výstup pro váš konkrétní případ použití. Pro další kroky můžete zkusit:

- Převod PNG souborů do PDF zprávy (`img2pdf` knihovna)
- Automatizaci hromadného převodu celé složky HTML souborů
- Použití Selenium pro stránky, které vyžadují plné renderování prohlížeče (např. těžké JavaScriptové frameworky)

Šťastné programování a užívejte si pixel‑dokonalé screenshoty!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s krok‑za‑krokem vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Převod HTML na PNG – Kompletní Python průvodce](/html/english/python/general/convert-html-to-png-complete-python-guide/)
- [Převod HTML na PNG v Pythonu – Kompletní průvodce ukládáním streamu](/html/english/python/general/convert-html-to-png-in-python-complete-streaming-save-guide/)
- [Převod SVG na PNG v Pythonu pomocí Aspose.HTML](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}