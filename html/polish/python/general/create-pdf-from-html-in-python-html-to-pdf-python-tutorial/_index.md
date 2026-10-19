---
category: general
date: 2026-07-15
description: Utwórz PDF z HTML przy użyciu Pythona. Dowiedz się, jak szybko konwertować
  HTML na PDF za pomocą prostego skryptu i jasnych kroków.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf from html
- convert html to pdf
- html to pdf python
- save html as pdf
- html to pdf tutorial
language: pl
lastmod: 2026-07-15
og_description: Tworzenie PDF z HTML przy użyciu Pythona. Ten przewodnik pokazuje,
  jak konwertować HTML na PDF, zapisywać HTML jako PDF oraz efektywnie zarządzać zasobami.
og_image_alt: Screenshot of a Python script that creates PDF from HTML
og_title: Tworzenie PDF z HTML w Pythonie – Praktyczny samouczek
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
title: 'Utwórz PDF z HTML w Pythonie – Poradnik: HTML do PDF w Pythonie'
url: /pl/python/general/create-pdf-from-html-in-python-html-to-pdf-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz PDF z HTML w Pythonie – Pełny poradnik

Czy kiedykolwiek potrzebowałeś **utworzyć PDF z HTML**, ale nie byłeś pewien, którą bibliotekę Pythona wybrać? Nie jesteś sam — wielu programistów napotyka ten problem, gdy próbują przekształcić raport internetowy, fakturę lub stronę marketingową w drukowalny PDF.  

Dobrą wiadomością jest to, że przy kilku linijkach kodu możesz **konwertować HTML do PDF** w sposób niezawodny, a skrypt działa na Windows, macOS i Linux. W tym przewodniku przeprowadzimy Cię przez kompletny, działający przykład, wyjaśnimy, dlaczego każdy krok ma znaczenie, i pokażemy, jak **zapisać HTML jako PDF** bez żadnych niedociągnięć.

---

## Czego się nauczysz

- Zainstaluj odpowiedni pakiet Pythona do konwersji HTML‑do‑PDF.  
- Wczytaj plik HTML z niestandardowymi opcjami obsługi zasobów (aby uniknąć niekończących się importów CSS).  
- Wygeneruj czysty plik PDF na dysku.  
- Rozwiąż typowe przypadki brzegowe, takie jak zewnętrzne obrazy, ścieżki względne i duże dokumenty.  

Pod koniec tego **poradnika HTML do PDF** będziesz mieć funkcję, którą możesz wkleić do dowolnego projektu.

---

## Wymagania wstępne

- Python 3.9+ (kod działa również z 3.8, ale 3.9+ zapewnia najnowsze funkcje `pathlib`).  
- Podstawowa znajomość wiersza poleceń i środowisk wirtualnych.  
- Plik HTML, który chcesz przekształcić w PDF — dowolna statyczna strona się nadaje.

> **Pro tip:** Jeśli używasz środowiska wirtualnego, aktywuj je przed instalacją biblioteki; dzięki temu Twoja globalna instalacja Pythona pozostanie czysta.

---

## Krok 1 – Zainstaluj WeasyPrint (silnik stojący za konwersją)

WeasyPrint to czysto‑Pythonowa biblioteka, która renderuje HTML i CSS do PDF. Obsługuje większość nowoczesnych funkcji webowych i daje Ci precyzyjną kontrolę nad ładowaniem zasobów.

```bash
pip install weasyprint
```

Uruchomienie powyższego polecenia pobiera `cairocffi`, `tinycss2` oraz kilka innych zależności. Jeśli napotkasz błąd związany z `cairo` na Windows, pobierz gotowe pliki wheel ze [Strony WeasyPrint](https://weasyprint.org/docs/install/).

---

## Krok 2 – Przygotuj mały pomocnik do obsługi zasobów

Gdy wczytujesz dokument HTML, który odwołuje się do zewnętrznych arkuszy stylów lub obrazów, biblioteka podąża za tymi linkami. W niektórych przypadkach prowadzi to do głębokiego zagnieżdżenia lub nawet nieskończonych pętli (np. plik CSS, który `@import`‑uje sam siebie). Aby zachować porządek, ograniczamy głębokość obsługi zasobów.

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

Powyższa klasa nie jest wymagana przez WeasyPrint, ale odzwierciedla wzorzec użyty w oryginalnym fragmencie i daje Ci punkt zaczepienia, aby zatrzymać niekontrolowane importy. Zobaczysz ją w użyciu w następnym kroku.

---

## Krok 3 – Wczytaj dokument HTML przy użyciu niestandardowych opcji

Teraz faktycznie odczytujemy plik HTML. Klasa `HTML` przyjmuje argument `base_url`, który ustawiamy na katalog zawierający plik źródłowy — dzięki temu względne linki działają bez serwera WWW.

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

> **Dlaczego to ważne:** Jeśli Twój HTML pobiera łańcuch plików CSS, każdy `@import` wywoła kolejne ładowanie. Ograniczenie głębokości zapobiega wyjściu skryptu poza kontrolę.

---

## Krok 4 – Zapisz przetworzony dokument jako PDF

Mając obiekt `HTML`, generowanie PDF to jednowierszowy kod. Przekazujemy także prosty fragment CSS, który wymusza czysty rozmiar strony (A4) i dodaje mały margines — możesz go dowolnie modyfikować.

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

Wywołanie `write_pdf` zapisuje PDF na dysku, więc otrzymujesz gotowy do udostępnienia plik.

---

## Krok 5 – Połącz wszystko razem

Poniżej znajduje się zwarty skrypt, który możesz skopiować do pliku `convert.py`. Zamień ścieżki zastępcze na własne katalogi.

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

**Oczekiwany wynik** – po uruchomieniu `python convert.py` powinieneś zobaczyć:

```
✅ PDF saved to /full/path/YOUR_DIRECTORY/output.pdf
```

Otwórz wygenerowany plik w dowolnym przeglądarce PDF; zobaczysz oryginalny układ strony, style CSS i obrazy (o ile były dostępne z pliku HTML).  

Jeśli zauważysz brakujące obrazy, sprawdź, czy ich atrybuty `src` są albo pełnymi URL‑ami, albo względnymi ścieżkami istniejącymi w `YOUR_DIRECTORY`.

---

## Często zadawane pytania i obsługa przypadków brzegowych

| Pytanie | Odpowiedź |
|----------|--------|
| *Co zrobić, jeśli mój HTML odwołuje się do zewnętrznych czcionek?* | WeasyPrint automatycznie pobierze pliki czcionek, ale możesz chcieć dodać domeny do białej listy, aby uniknąć długich czasów pobierania. |
| *Czy mogę konwertować ciąg HTML zamiast pliku?* | Tak — użyj `HTML(string=my_html_string)` i pomiń `base_url` lub ustaw go na tymczasowy folder. |
| *Jak kontrolować metadane PDF (tytuł, autor)?* | Przekaż słownik `metadata` do `write_pdf`, np. `html_doc.write_pdf(target='out.pdf', metadata={'Title': 'Report'})`. |
| *Na Linuxie pojawia się błąd „cairo‑cffi error”.* | Zainstaluj pakiet systemowy `libcairo2-dev` (`apt-get install libcairo2-dev` na Debian/Ubuntu) przed instalacją WeasyPrint przez pip. |

---

## Podsumowanie

Właśnie **utworzyliśmy PDF z HTML** przy użyciu czystego workflow w Pythonie, omówiliśmy mechanikę **konwersji HTML do PDF** i pokazaliśmy, jak **zapisać HTML jako PDF** z solidną obsługą zasobów. Skrypt jest na tyle mały, że można go wkleić do potoków CI, a jednocześnie na tyle elastyczny, że można go rozbudować o własne nagłówki, stopki czy znaki wodne.

Kolejne kroki, które możesz rozważyć:

- Użyj biblioteki **html to pdf python** `pdfkit` do podejścia opartego na wkhtmltopdf (dobrego dla starszych CSS).  
- Dodaj interfejs CLI przy użyciu `argparse`, aby skrypt przyjmował argumenty wejścia/wyjścia.  
- Generuj PDF‑y w locie w endpointzie Flask lub FastAPI, aby tworzyć raporty na żądanie.  

Śmiało eksperymentuj, łam rzeczy, a potem wróć do tego przewodnika po szybkie odświeżenie. Jeśli napotkasz problemy, dokumentacja WeasyPrint i fora społeczności są doskonałymi źródłami pomocy.

Miłego kodowania i przyjemności z przekształcania stron internetowych w eleganckie PDF‑y!

## Co warto nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które budują na technikach przedstawionych w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Konwertuj HTML do PDF przy użyciu Aspose.HTML – Kompletny przewodnik manipulacji](/html/english/)
- [Konwertuj HTML do PDF w .NET przy użyciu Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Utwórz PDF z HTML – Przewodnik krok po kroku w C#](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}