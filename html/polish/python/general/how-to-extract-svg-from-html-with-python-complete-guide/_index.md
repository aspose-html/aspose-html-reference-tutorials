---
category: general
date: 2026-05-31
description: Dowiedz się, jak wyodrębnić SVG z HTML przy użyciu Pythona. Ten krok
  po kroku poradnik pokazuje, jak odczytać dokument HTML, zapisać pliki SVG oraz efektywnie
  zapisać wbudowane SVG.
draft: false
keywords:
- how to extract svg
- read html document
- save svg files
- save inline svg
- extract svg from html
language: pl
og_description: Jak wyodrębnić SVG z HTML przy użyciu Pythona. Skorzystaj z tego samouczka,
  aby odczytać dokument HTML, zapisać pliki SVG i bezproblemowo obsługiwać wbudowane
  SVG.
og_title: Jak wyodrębnić SVG z HTML przy użyciu Pythona – Kompletny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  headline: How to extract SVG from HTML with Python – Complete Guide
  type: TechArticle
- description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  name: How to extract SVG from HTML with Python – Complete Guide
  steps:
  - name: Reads an HTML file.
    text: Reads an HTML file.
  - name: Collects inline <svg> markup.
    text: Collects inline <svg> markup.
  - name: Finds external SVG references (<img> and <object> tags).
    text: Finds external SVG references (<img> and <object> tags).
  - name: Saves each SVG to a separate .svg file.
    text: Saves each SVG to a separate .svg file.
  type: HowTo
tags:
- Python
- SVG
- HTML parsing
- Aspose
title: Jak wyodrębnić SVG z HTML w Pythonie – Kompletny przewodnik
url: /pl/python/general/how-to-extract-svg-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyodrębnić SVG z HTML przy użyciu Pythona – Kompletny przewodnik

Zastanawiałeś się kiedyś **jak wyodrębnić SVG** z nieuporządkowanej strony HTML, nie tracąc przy tym włosów? Nie jesteś sam. Niezależnie od tego, czy tworzysz web‑scrapera, pipeline projektowy, czy po prostu potrzebujesz masowo eksportować ikony, znajomość **jak wyodrębnić SVG** to przydatny trik, który oszczędza czas i nerwy.

W tym samouczku pokażemy dokładnie **jak wyodrębnić SVG** przy użyciu biblioteki Aspose.HTML dla Pythona. Odczytamy dokument HTML, wyciągniemy zarówno wbudowany kod `<svg>` **i** zewnętrzne odwołania do SVG, a następnie **zapiszemy pliki SVG** na dysku — wszystko w schludnym, wielokrotnego użytku skrypcie. Po zakończeniu będziesz mieć gotowe rozwiązanie, które możesz dostosować do własnych projektów.

> **Pro tip:** Jeśli potrzebujesz tylko szybkiego podglądu strony, `BeautifulSoup` też się sprawdzi, ale Aspose.HTML zapewnia pełny DOM, co sprawia, że wyodrębnianie zarówno wbudowanych, jak i powiązanych SVG jest dziecinnie proste.

## Czego będziesz potrzebować

* Python 3.8+ (kod używa f‑strings, więc minimalna wersja to 3.6+)
* `pip install aspose-html` – komercyjna biblioteka napędzająca nasze parsowanie HTML
* Folder zawierający plik `input.html` z SVG, które chcesz wyodrębnić
* Uprawnienia do zapisu w katalogu wyjściowym (nazwijmy go `YOUR_DIRECTORY`)

To wszystko — bez dodatkowych binarek, bez przeglądarek headless. Proste, prawda?

## Krok 1: Odczyt dokumentu HTML przy użyciu Aspose.HTML

Pierwszą rzeczą, którą musisz zrobić, jest **odczyt dokumentu HTML**, aby móc przechodzić po jego drzewie DOM. Aspose.HTML udostępnia obiekt `HTMLDocument`, który zachowuje się jak `document` w przeglądarce.

```python
from aspose.html import HTMLDocument

# Load the HTML file – replace YOUR_DIRECTORY with the actual path
doc = HTMLDocument("YOUR_DIRECTORY/input.html")
```

*Dlaczego to ważne:* Ładowanie HTML do prawidłowego DOM pozwala uniknąć pułapek parsowania opartego na wyrażeniach regularnych i zapewnia metody takie jak `get_elements_by_tag_name` oraz `query_selector_all` za darmo.

## Krok 2: Zbierz wszystkie wbudowane elementy <svg>

Wbudowane SVG to bloki `<svg>…</svg>` znajdujące się bezpośrednio w HTML. Aby **zapisać wbudowane SVG**, potrzebujemy jedynie ich zewnętrznego HTML.

```python
svg_contents = []  # We'll collect both markup and file paths here

# Find every <svg> element in the document
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)   # Store the raw markup
```

Zauważ, że do `svg_contents` dodajemy surowy kod bezpośrednio. Później zdecydujemy, czy każdy wpis jest kodem, czy ścieżką do pliku.

## Krok 3: Znajdź zewnętrzne odwołania do SVG (tagi img i object)

Wiele stron odwołuje się do zewnętrznych plików SVG za pomocą `<img src="icon.svg">` lub `<object data="logo.svg">`. Aby **wyodrębnić SVG z HTML**, musimy również przechwycić te adresy URL.

```python
# CSS selector: img or object whose src/data ends with .svg (case‑insensitive)
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    # For <img> we read the src attribute, for <object> the data attribute
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:                                   # Guard against missing attribute
        svg_contents.append(src)
```

*Uwaga na przypadki brzegowe:* Jeśli adres URL SVG jest względny, należy połączyć go ze ścieżką bazową pliku HTML. Dla zwięzłości zakładamy, że HTML znajduje się obok plików SVG.

## Krok 4: Zapisz każdy SVG do osobnego pliku

Teraz, gdy mamy mieszczoną listę ciągów kodu i ścieżek plików, przeiterujemy ją i **zapiszemy pliki SVG**. Skrypt automatycznie rozróżnia wbudowany kod od odwołania do istniejącego pliku.

```python
import os
import shutil

for index, content in enumerate(svg_contents):
    output_path = f"YOUR_DIRECTORY/svg_{index}.svg"

    # Trim leading whitespace and check if it looks like markup
    if content.lstrip().startswith("<svg"):
        # Inline SVG – write the markup directly
        with open(output_path, "w", encoding="utf-8") as file:
            file.write(content)
        print(f"Saved inline SVG to {output_path}")
    else:
        # External reference – copy the source file's contents
        src_path = os.path.abspath(content)  # Resolve relative paths
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, output_path)
            print(f"Copied external SVG from {src_path} to {output_path}")
        else:
            print(f"⚠️  Warning: referenced SVG not found: {src_path}")
```

**Co zobaczysz:** Po zakończeniu skryptu, `YOUR_DIRECTORY` będzie zawierać pliki o nazwach `svg_0.svg`, `svg_1.svg`, …, z których każdy będzie zawierał albo oryginalny wbudowany kod, albo kopię zewnętrznego SVG.

### Oczekiwany wynik

```
Saved inline SVG to YOUR_DIRECTORY/svg_0.svg
Saved inline SVG to YOUR_DIRECTORY/svg_1.svg
Copied external SVG from /path/to/logo.svg to YOUR_DIRECTORY/svg_2.svg
...
```

Jeśli odwoływany plik nie istnieje, skrypt wypisze ostrzeżenie, ale będzie kontynuował — więc jeden uszkodzony link nie zatrzyma całego procesu wyodrębniania.

## Radzenie sobie z typowymi problemami

| Problem | Dlaczego się pojawia | Szybka naprawa |
|---------|----------------------|----------------|
| **Względne URL-e przerywają** | Atrybut `src` może być `"../assets/icon.svg"` | Użyj `os.path.join(os.path.dirname(html_path), src)` aby rozwiązać. |
| **Duplikaty nazw plików** | Dwa SVG o tej samej nazwie zostaną nadpisane | Dodaj hash zawartości do nazwy pliku (`hashlib.md5(content.encode()).hexdigest()[:8]`). |
| **Duże wbudowane SVG powodują skoki pamięci** | Przechowywanie całego kodu w liście przed zapisem | Strumieniuj każdy element bezpośrednio do pliku zamiast buforować. |
| **Obrazy nie‑SVG przechodzą** | Niektóre tagi `<img>` kończą się na `.svg?version=1` | Usuń ciągi zapytań przed sprawdzeniem rozszerzenia (`src.split('?')[0]`). |

## Pełny skrypt, który możesz skopiować i wkleić

Poniżej znajduje się kompletny, gotowy do uruchomienia program. Zapisz go jako `extract_svg.py`, dostosuj `YOUR_DIRECTORY` i uruchom `python extract_svg.py`.

```python
"""
extract_svg.py – How to extract SVG from HTML using Aspose.HTML for Python

This script:
1. Reads an HTML file.
2. Collects inline <svg> markup.
3. Finds external SVG references (<img> and <object> tags).
4. Saves each SVG to a separate .svg file.

Author: Your Name
Date: 2026-05-31
"""

import os
import shutil
from aspose.html import HTMLDocument

# ----------------------------------------------------------------------
# Configuration – change these paths to suit your environment
# ----------------------------------------------------------------------
HTML_PATH = "YOUR_DIRECTORY/input.html"          # Path to source HTML
OUTPUT_DIR = "YOUR_DIRECTORY"                    # Where SVGs will be written

# Ensure output directory exists
os.makedirs(OUTPUT_DIR, exist_ok=True)

# ----------------------------------------------------------------------
# Step 1: Load the HTML document (read html document)
# ----------------------------------------------------------------------
doc = HTMLDocument(HTML_PATH)

# ----------------------------------------------------------------------
# Step 2: Collect inline <svg> elements (save inline svg)
# ----------------------------------------------------------------------
svg_contents = []
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)

# ----------------------------------------------------------------------
# Step 3: Collect external SVG references (extract svg from html)
# ----------------------------------------------------------------------
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:
        # Resolve relative paths relative to the HTML file location
        src_path = os.path.join(os.path.dirname(HTML_PATH), src)
        svg_contents.append(src_path)

# ----------------------------------------------------------------------
# Step 4: Save each gathered SVG (save svg files)
# ----------------------------------------------------------------------
for idx, content in enumerate(svg_contents):
    out_path = os.path.join(OUTPUT_DIR, f"svg_{idx}.svg")

    # Detect inline markup vs file path
    if isinstance(content, str) and content.lstrip().startswith("<svg"):
        # Inline SVG – write directly
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(content)
        print(f"[✓] Inline SVG saved → {out_path}")
    else:
        # External file – copy its contents
        src_path = os.path.abspath(content)
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, out_path)
            print(f"[✓] External SVG copied → {out_path}")
        else:
            print(f"[⚠] Missing SVG file: {src_path}")

print("\n✅ Extraction complete. Check the", OUTPUT_DIR, "folder for your SVGs.")
```

## Podsumowanie – Jak wyodrębnić SVG w skrócie

* **Odczytaj dokument HTML** przy użyciu `HTMLDocument`.
* **Zbierz wbudowane `<svg>`** za pomocą `get_elements_by_tag_name`.
* **Zlokalizuj zewnętrzne SVG** używając selektora CSS kończącego się na `.svg`.
* **Zapisz każdy element** — zapisz kod bezpośrednio do pliku lub skopiuj odwołany plik.
* **Obsłuż przypadki brzegowe** takie jak ścieżki względne, duplikaty i brakujące pliki.

To pełna odpowiedź na pytanie **jak wyodrębnić SVG** z strony HTML, zamknięta w jednym, łatwym do modyfikacji skrypcie.

## Co dalej?

Teraz, gdy możesz **wyodrębnić SVG** niezawodnie, rozważ następujące pomysły:

* **Przetwarzanie wsadowe:** Przejdź przez katalog plików HTML, aby zbudować bibliotekę ikon.
* **Optymalizacja:** Przetwarzaj każdy zapisany SVG przy użyciu SVGO (optymalizatora Node.js), aby zmniejszyć rozmiar pliku.
* **Konwersja:** Użyj `cairosvg` lub `svglib`, aby przekształcić SVG w PNG dla starszych przeglądarek.
* **Ekstrakcja metadanych:** Przeanalizuj tagi `<title>` lub `<desc>` w każdym SVG, aby uzyskać etykiety możliwe do wyszukiwania.

Każdy z tych tematów odnosi się do naszych drugorzędnych słów kluczowych — **read HTML document**, **save svg files**, **save inline svg**, **extract svg from html** — więc znajdziesz mnóstwo materiałów do dalszej eksploracji.

*​Szczęśliwego hackowania! Jeśli napotkasz problemy, zostaw komentarz poniżej lub napisz do mnie na GitHubie. Świat SVG jest ogromny, ale z odpowiednimi narzędziami wyodrębnianie ich to bułka z masłem.*

## Co powinieneś nauczyć się dalej?

- [Zapisz dokument SVG w Aspose.HTML dla Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Jak przekonwertować SVG do XPS przy użyciu Aspose.HTML dla Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [Renderowanie dokumentu SVG w formacie PNG w .NET przy użyciu Aspose.HTML](/html/french/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}