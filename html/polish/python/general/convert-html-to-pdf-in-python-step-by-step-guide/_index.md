---
category: general
date: 2026-08-06
description: Konwertuj HTML na PDF w Pythonie z pełnym przykładem. Dowiedz się, jak
  generować PDF z HTML, zapisywać HTML jako PDF oraz obsługiwać typowe przypadki brzegowe.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to pdf
- generate pdf from html
- save html as pdf
- create pdf from html file
- how to convert html to pdf
language: pl
lastmod: 2026-08-06
og_description: Konwertuj HTML na PDF w Pythonie i automatyzuj tworzenie dokumentów.
  Skorzystaj z tego przewodnika, aby wygenerować PDF z HTML, zapisać HTML jako PDF
  i dostosować wynik.
og_image_alt: Example of convert html to pdf script in Python
og_title: Konwertuj HTML na PDF w Pythonie – kompleksowy poradnik
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
title: Konwertuj HTML do PDF w Pythonie – przewodnik krok po kroku
url: /pl/python/general/convert-html-to-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwertowanie HTML do PDF w Pythonie – przewodnik krok po kroku

Jeśli potrzebujesz **szybkiego konwertowania HTML do PDF**, ten samouczek przedstawia kompletną rozwiązanie w Pythonie. Zobaczysz, jak generować PDF z HTML, zapisywać HTML jako PDF oraz kontrolować proces konwersji bez opuszczania kodu.

Poradnik prowadzi Cię przez instalację niezawodnej biblioteki, wczytywanie dokumentu HTML, przeprowadzanie konwersji i weryfikację wyniku. Po zakończeniu będziesz mógł tworzyć PDF z pliku HTML w dowolnym projekcie Pythona, niezależnie od tego, czy źródło jest statyczną stroną, czy dynamicznie generowanym kodem.

## Czego się nauczysz

* Zainstalować zależności `pdfkit` i `wkhtmltopdf` niezbędne do konwersji HTML‑do‑PDF.  
* Wczytać dokument HTML z dysku lub jako ciąg znaków.  
* Wygenerować PDF z HTML z własnym rozmiarem strony, marginesami i opcjami kodowania.  
* Zapisać HTML jako PDF przy użyciu jednego wywołania funkcji.  
* Obsłużyć typowe przypadki brzegowe, takie jak brakujące zasoby, znaki Unicode i duże pliki.  

**Wymagania wstępne** – Python 3.8+ oraz podstawowa znajomość operacji na plikach. Nie są wymagane żadne zewnętrzne usługi.

## Konwersja HTML do PDF – ogólny przepływ pracy

Proces konwersji składa się z trzech logicznych faz:

1. **Przygotowanie** – zainstaluj konwerter i upewnij się, że plik binarny `wkhtmltopdf` jest dostępny.  
2. **Obsługa wejścia** – odczytaj plik HTML lub zbuduj znacznik programowo.  
3. **Generowanie wyjścia** – wywołaj konwerter, zapisz plik PDF i potwierdź wynik.  

Każda faza jest omówiona w dedykowanym kroku poniżej.

## Krok 1: Instalacja wymaganych bibliotek

`pdfkit` zapewnia cienką nakładkę Pythona na szeroko używany silnik `wkhtmltopdf`. Zainstaluj oba przy pomocy `pip` i zweryfikuj ścieżkę do pliku binarnego.

```bash
# Install the Python wrapper
pip install pdfkit

# On Ubuntu/Debian install wkhtmltopdf package
sudo apt-get install wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf
```

Jeśli wolisz przenośny plik binarny, pobierz odpowiednie wydanie ze [strony wkhtmltopdf na GitHubie](https://github.com/wkhtmltopdf/wkhtmltopdf/releases) i umieść je w katalogu dodanym do Twojej zmiennej `PATH`. Skrypt później automatycznie sprawdzi ścieżkę.

## Krok 2: Wczytanie dokumentu HTML

Możesz odczytać statyczny plik, pobrać zdalną treść lub skonstruować HTML w locie. Poniższy przykład wczytuje lokalny plik o nazwie `sample.html` znajdujący się w katalogu, który określisz.

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

Odczytanie pliku jako ciągu Unicode zapewnia, że znaki takie jak „é”, „ß” czy azjatyckie glify zostaną zachowane podczas konwersji. Ten krok jest niezbędny, gdy **generujesz PDF z HTML**, który zawiera tekst międzynarodowy.

## Krok 3: Generowanie PDF z HTML

`pdfkit.from_string` konwertuje ciąg zawierający znacznik HTML do pliku PDF. Możesz przekazać słownik opcji, aby kontrolować rozmiar strony, marginesy oraz zachowanie nagłówka/stopki.

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

Powyższe wywołanie **tworzy PDF z pliku HTML** zapisanego jako `sample.pdf`. Jeśli źródłowy HTML odwołuje się do lokalnych plików CSS lub obrazów, flaga `enable‑local‑file‑access` pozwala `wkhtmltopdf` rozwiązać te zasoby.

### Dlaczego to podejście działa

* `pdfkit` deleguje ciężką pracę do `wkhtmltopdf`, który renderuje HTML przy użyciu silnika WebKit, zapewniając wysoką wierność oryginalnemu układowi.  
* Dostarczenie słownika opcji pozwala precyzyjnie dostroić wynik bez modyfikowania samego HTML.  
* Użycie `from_string` utrzymuje przepływ pracy w pamięci, co jest przydatne, gdy HTML jest generowany w locie.

## Krok 4: Zapisz HTML jako PDF i zweryfikuj wynik

Po konwersji możesz chcieć potwierdzić, że PDF istnieje i jest czytelny. Poniższy fragment sprawdza rozmiar pliku i otwiera PDF domyślną przeglądarką systemową (specyficzną dla platformy).

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

Uruchomienie skryptu wyświetla komunikat o sukcesie i uruchamia przeglądarkę PDF, dzięki czemu możesz natychmiast potwierdzić, że układ odpowiada oryginalnemu HTML. Ten krok kończy cykl **save html as pdf**.

## Krok 5: Zaawansowane opcje – tworzenie PDF z pliku HTML z własnymi ustawieniami

Czasami masz fizyczny plik HTML na dysku i wolisz użyć `pdfkit.from_file` zamiast samodzielnego wczytywania zawartości. Ta metoda jest przydatna, gdy HTML już zawiera złożone ścieżki względne.

```python
# Directly convert a file path to PDF
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

Możesz także osadzić stronę tytułową, spis treści lub flagi wykonywania JavaScript, rozszerzając słownik `options`. Na przykład, aby dodać stronę tytułową:

```python
options.update({
    "cover": str(BASE_DIR / "cover.html"),
    "toc": None,  # Generates a table of contents
})
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

Te modyfikacje pokazują **jak konwertować HTML do PDF** w bardziej zaawansowanych pipeline'ach publikacji.

## Typowe pułapki i jak ich unikać

| Problem | Przyczyna | Rozwiązanie |
|-------|-------|--------|
| Obrazy lub CSS nie wyświetlają się | `wkhtmltopdf` domyślnie blokuje dostęp do lokalnych plików | Dodaj `"enable-local-file-access": None` do słownika opcji |
| Znaki Unicode stają się zniekształcone | Brak opcji `encoding` lub odczyt pliku z niewłaściwym zestawem znaków | Zawsze ustaw `"encoding": "UTF-8"` i odczytuj plik HTML w UTF‑8 |
| PDF jest pusty | Nieprawidłowa ścieżka do pliku binarnego `wkhtmltopdf` | Podaj ścieżkę explicite: `pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")` |
| Duże pliki HTML powodują przekroczenie limitu czasu | Domyślny timeout jest za krótki | Ustaw `"javascript-delay": "2000"` lub zwiększ timeout przy użyciu `"timeout": "60"` |

Rozwiązanie tych problemów zapewnia niezawodny proces **generate pdf from html** w różnych środowiskach.

## Pełny skrypt – przykład od początku do końca

Zapisz poniższy kod jako `html_to_pdf.py` i uruchom go poleceniem `python html_to_pdf.py`. Dostosuj `YOUR_DIRECTORY`, aby wskazywał na folder Twojego projektu.

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

# wkhtmltopdf configuration (optional – only needed if binary is not on PATH)
# config = pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")

# Conversion options – customize as required
OPTIONS = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left":


## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak konwertować HTML do PDF w Java – używając Aspose.HTML dla Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Konwertuj HTML do PDF w .NET przy użyciu Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Jak konwertować HTML do PDF w Java – ustawianie marginesów strony przy użyciu Aspose.HTML](/html/english/java/advanced-usage/css-extensions-adding-title-page-number/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}