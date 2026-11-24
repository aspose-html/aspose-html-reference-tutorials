---
category: general
date: 2026-11-24
description: Dowiedz się, jak używać ResourceHandlingOptions w Aspose.HTML dla Pythona,
  aby kontrolować obsługę zasobów HTML, ograniczyć głębokość rekurencji i zapisać
  przetworzony plik.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use resourcehandlingoptions in aspose
- Aspose.HTML Python
- HTMLDocument processing
- limit recursion depth
- resource handling options
- save processed HTML
language: pl
lastmod: 2026-11-24
og_description: Użyj ResourceHandlingOptions w Aspose.HTML dla Pythona, aby bezpiecznie
  przetwarzać duże pliki HTML, ograniczyć głębokość rekurencji i zapisać oczyszczony
  wynik.
og_image_alt: Diagram showing use ResourceHandlingOptions in Aspose to control HTML
  resource handling
og_title: Jak używać ResourceHandlingOptions w Aspose.HTML z Pythonem
schemas:
- author: Aspose
  dateModified: '2026-11-24'
  description: Learn how to use ResourceHandlingOptions in Aspose.HTML for Python
    to control HTML resource handling, limit recursion depth, and save a processed
    file.
  headline: How to use ResourceHandlingOptions in Aspose.HTML with Python
  type: TechArticle
tags:
- Aspose
- Python
- HTML processing
title: Jak używać ResourceHandlingOptions w Aspose.HTML w Pythonie
url: /pl/python/general/how-to-use-resourcehandlingoptions-in-aspose-html-with-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać ResourceHandlingOptions w Aspose.HTML z Pythonem

Jeśli potrzebujesz **use ResourceHandlingOptions in Aspose** dla Pythona, ten przewodnik pokaże Ci kompletną, gotową do uruchomienia rozwiązanie. Kontrolowanie obsługi zasobów zapobiega niekontrolowanej rekurencji podczas przetwarzania dużych lub złożonych stron HTML, a poniższe kroki pozwolą Ci bezpiecznie zastosować tę opcję i zweryfikować wynik.

Nauczysz się, jak skonfigurować **resource handling options**, załadować dokument HTML z tymi ustawieniami i zapisać przetworzony wynik. Samouczek omawia także typowe pułapki, takie jak odwołania cykliczne i brakujące zasoby, dzięki czemu możesz dostosować kod do dowolnego projektu, który opiera się na **HTMLDocument processing**.

## Wymagania wstępne

- Zainstalowany Python 3.8 lub nowszy.
- Ważna licencja Aspose.HTML dla Pythona (darmowa wersja ewaluacyjna działa do testów).
- Wykonane wirtualnym środowisku polecenie `pip install aspose-html`.
- Plik HTML (`big.html`), który chcesz przetworzyć.

Te wymagania zapewniają, że przykład uruchomi się bez dodatkowej konfiguracji.

## Krok 1: Zainstaluj Aspose.HTML dla Pythona

```bash
pip install aspose-html
```

Uruchomienie polecenia instaluje pakiet **Aspose.HTML Python** oraz wszystkie jego zależności. Biblioteka udostępnia `HTMLDocument`, `ResourceHandlingOptions` i inne klasy potrzebne do **HTMLDocument processing**.

## Krok 2: Zaimportuj wymagane klasy

```python
# Import the core classes needed for resource handling and document loading
from aspose.html import ResourceHandlingOptions, HTMLDocument
```

Zaimportowanie `ResourceHandlingOptions` daje dostęp do obiektu **resource handling options**, natomiast `HTMLDocument` jest punktem wejścia do ładowania i zapisywania plików HTML.

## Krok 3: Skonfiguruj ResourceHandlingOptions

```python
# Create an options instance that limits how deep the engine will follow linked resources
resource_options = ResourceHandlingOptions(max_handling_depth=5)
```

**Dlaczego to ważne:**  
Gdy strona HTML odwołuje się do innych stron, obrazów lub skryptów, Aspose.HTML może podążać za tymi linkami rekurencyjnie. Bez limitu złośliwa lub źle skonstruowana witryna może spowodować nieskończoną pętlę. Ustawienie `max_handling_depth` na `5` (lub dowolną wartość pasującą do Twojego scenariusza) **ogranicza głębokość rekurencji**, chroniąc aplikację przed nadmiernym zużyciem pamięci.

> **Pro tip:** Jeśli wiesz, że Twoje dokumenty nie osadzają się głębiej niż trzy poziomy, ustaw `max_handling_depth=3`, aby skrócić czas przetwarzania.

## Krok 4: Załaduj dokument HTML z skonfigurowanymi opcjami

```python
# Load the source HTML file while applying the resource handling options
doc = HTMLDocument(
    "YOUR_DIRECTORY/big.html",
    resource_handling_options=resource_options
)
```

Przekazanie `resource_handling_options` do konstruktora informuje Aspose.HTML, aby respektował limit głębokości podczas parsowania. Ten krok jest niezbędny do **use ResourceHandlingOptions in Aspose**; bez niego domyślna nieograniczona rekurencja może nadal wystąpić.

## Krok 5: Zapisz przetworzony dokument

```python
# Save the processed HTML to a new file; the output reflects any resources that were trimmed
doc.save("YOUR_DIRECTORY/big_processed.html")
```

Metoda `save` zapisuje oczyszczony kod HTML na dysku. Powstały plik (`big_processed.html`) zawiera tylko zasoby, które zostały pomyślnie obsłużone w określonej głębokości, co czyni go bezpiecznym do udostępniania lub dalszej manipulacji.

## Krok 6: Zweryfikuj wynik (opcjonalnie, ale zalecane)

```python
# Quick verification: read the saved file and print the first 200 characters
with open("YOUR_DIRECTORY/big_processed.html", "r", encoding="utf-8") as f:
    print(f.read()[:200])
```

Uruchomienie tego fragmentu kodu potwierdza, że plik został utworzony i że zawartość wygląda zgodnie z oczekiwaniami. Jeśli wynik jest pusty lub brakuje kluczowych elementów, rozważ zwiększenie `max_handling_depth` lub sprawdzenie oryginalnego HTML pod kątem uszkodzonych linków.

## Typowe przypadki brzegowe i jak je obsłużyć

| Situation                              | Recommended adjustment                                 |
|----------------------------------------|--------------------------------------------------------|
| **Circular references** (A → B → A)    | Ustaw `max_handling_depth` na niską wartość (np. 2).     |
| **Missing external resources**         | Użyj `resource_options.ignore_missing_resources = True`, aby pominąć błędy. |
| **Huge HTML files (> 100 MB)**         | Zwiększ limit pamięci procesu za pomocą `ResourceHandlingOptions(max_memory_usage=…)`. |
| **Need to process CSS/JS inline only** | Wyłącz obsługę zewnętrznych zasobów: `resource_options.handle_external_resources = False`. |

Te warianty demonstrują elastyczność **resource handling options** i pomagają dostosować rozwiązanie do różnych wymagań projektowych.

## Pełny działający przykład

Poniżej znajduje się kompletny skrypt, który możesz skopiować i wkleić do pliku o nazwie `process_html.py`. Zamień `YOUR_DIRECTORY` na rzeczywistą ścieżkę do swoich plików.

```python
# process_html.py
# Complete example showing how to use ResourceHandlingOptions in Aspose.HTML for Python

from aspose.html import ResourceHandlingOptions, HTMLDocument

# ----------------------------------------------------------------------
# Step 1: Configure resource handling – limit recursion depth to 5 levels
# ----------------------------------------------------------------------
resource_options = ResourceHandlingOptions(max_handling_depth=5)

# ----------------------------------------------------------------------
# Step 2: Load the source HTML document with the configured options
# ----------------------------------------------------------------------
doc = HTMLDocument(
    "YOUR_DIRECTORY/big.html",               # Path to the original HTML file
    resource_handling_options=resource_options
)

# ----------------------------------------------------------------------
# Step 3: Save the processed HTML to a new location
# ----------------------------------------------------------------------
doc.save("YOUR_DIRECTORY/big_processed.html")

# ----------------------------------------------------------------------
# Optional verification step
# ----------------------------------------------------------------------
if __name__ == "__main__":
    with open("YOUR_DIRECTORY/big_processed.html", "r", encoding="utf-8") as f:
        print("First 200 characters of the processed file:")
        print(f.read()[:200])
```

Uruchomienie `python process_html.py` generuje `big_processed.html`, jednocześnie bezpiecznie respektując limit rekurencji ustawiony za pomocą **ResourceHandlingOptions**.

## Podsumowanie

Teraz wiesz, jak **use ResourceHandlingOptions in Aspose** kontrolować obsługę zasobów HTML, ograniczać głębokość rekurencji i **save processed HTML** pliki w sposób niezawodny. To podejście chroni Twoją aplikację przed nieskończonymi pętlami, zmniejsza zużycie pamięci i daje precyzyjną kontrolę nad tym, jak zewnętrzne zasoby są obsługiwane podczas **HTMLDocument processing**.

### Co dalej?

- Eksperymentuj z innymi **resource handling options**, takimi jak `ignore_missing_resources` lub `handle_external_resources`.
- Połącz tę technikę z funkcjami **CSS/JS inlining** Aspose.HTML, aby tworzyć w pełni samodzielne strony.
- Zapoznaj się z API **Aspose.HTML Python** w celu konwersji do PDF, renderowania obrazów lub manipulacji DOM, aby rozszerzyć przepływ pracy.

Śmiało dostosuj przykład do przetwarzania wsadowego wielu plików lub zintegrowania go z usługą internetową, która sanitizuje przesyłany przez użytkowników HTML. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Limit HTML Resource Depth with Aspose.HTML for Python – Complete Guide](/html/english/python/general/limit-html-resource-depth-with-aspose-html-for-python-comple/)
- [How to Set max_handling_depth in Aspose.HTML Python – Complete Guide](/html/english/python/general/how-to-set-max-handling-depth-in-aspose-html-python-complete/)
- [How to limit nested resources when processing HTML with Aspose.HTML for Python](/html/english/python/general/how-to-limit-nested-resources-when-processing-html-with-aspo/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}