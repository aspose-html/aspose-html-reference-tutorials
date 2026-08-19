---
category: general
date: 2026-08-19
description: Utwórz opcje obsługi zasobów w Pythonie i dowiedz się, jak wczytać dokument
  HTML, nawet dużą stronę HTML, przy użyciu Aspose.HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to load html document
- load large html page
language: pl
lastmod: 2026-08-19
og_description: Utwórz opcje obsługi zasobów w Pythonie i zobacz, jak wczytać dokument
  HTML, w tym duże strony HTML, przy użyciu Aspose.HTML.
og_image_alt: Screenshot of Python code that creates resource handling options and
  loads a large HTML page
og_title: Utwórz opcje obsługi zasobów i wczytaj dokument HTML – przewodnik Pythona
schemas:
- author: Aspose
  dateModified: '2026-08-19'
  description: Create resource handling options in Python and learn how to load an
    HTML document, even a large HTML page, with Aspose.HTML.
  headline: Create resource handling options and load an HTML document in Python
  type: TechArticle
- description: Create resource handling options in Python and learn how to load an
    HTML document, even a large HTML page, with Aspose.HTML.
  name: Create resource handling options and load an HTML document in Python
  steps:
  - name: Verify that the page loaded successfully
    text: 'A quick way to confirm that the document is ready is to print the number
      of child nodes in the root element:'
  - name: 1. Missing resources
    text: 'When a linked CSS or JS file is unavailable, Aspose.HTML silently skips
      it but logs a warning. To capture these warnings, enable logging:'
  - name: 2. Circular references
    text: Even with a depth limit, circular references can cause the parser to waste
      time. If you notice unusually long load times, consider reducing `max_handling_depth`
      to `2` or `1`.
  - name: 3. Very large pages (> 10 MB)
    text: 'For extremely large pages, increase Python’s recursion limit **only if**
      you have verified that the depth is safe:'
  type: HowTo
tags:
- Aspose.HTML
- Python
- HTML processing
title: Utwórz opcje obsługi zasobów i załaduj dokument HTML w Pythonie
url: /pl/python/general/create-resource-handling-options-and-load-an-html-document-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create resource handling options and load an HTML document in Python

Jeśli potrzebujesz **create resource handling options** dla importu HTML, ten przewodnik pokaże Ci dokładnie, jak to zrobić. Niezależnie od tego, czy masz do czynienia z niewielką stroną, czy *large HTML page*, która pobiera wiele zewnętrznych zasobów, poniższe kroki pozwolą Ci kontrolować głębokość, unikać odwołań cyklicznych i utrzymać przewidywalne zużycie pamięci.

W tym samouczku dowiesz się **how to load HTML document** plików z Aspose.HTML for Python, skonfigurujesz maksymalną głębokość obsługi i zweryfikujesz, że strona ładuje się bez wyczerpywania zasobów. Podejście działa dla dowolnego źródła HTML, od prostych statycznych plików po złożone strony, które odwołują się do dziesiątek skryptów, arkuszy stylów i obrazów.

## Co będzie potrzebne

- Python 3.8 lub nowszy zainstalowany.  
- Pakiet `aspose-html` (zainstaluj za pomocą `pip install aspose-html`).  
- Lokalny plik HTML (np. `big_page.html`), który chcesz przetestować.  
- Podstawowa znajomość Pythona i ładowania zasobów HTML.  

Te wymagania zapewniają, że kod działa niezmieniony na systemach Windows, macOS lub Linux.

## Krok 1: Create resource handling options

Pierwszym krokiem jest **create resource handling options**. Ten obiekt informuje Aspose.HTML, jak traktować powiązane zasoby (CSS, JS, obrazy) podczas parsowania dokumentu.

```python
# Step 1: Import the Aspose.HTML library
from aspose.html import *

# Step 2: Instantiate the options container
# This is where we will configure resource handling behavior.
resource_options = ResourceHandlingOptions()
```

> **Dlaczego to ważne:** Bez explicite określonych opcji Aspose.HTML podąża za każdym napotkanym linkiem, co może prowadzić do nieskończonej rekurencji na stronach, które odwołują się do siebie nawzajem. Tworząc obiekt opcji, zyskujesz precyzyjną kontrolę nad procesem importu.

## Krok 2: Limit the handling depth

Aby zapobiec niekontrolowanym wywołaniom sieciowym, ustaw maksymalną głębokość. Głębokość `3` jest bezpiecznym domyślnym ustawieniem dla większości witryn, umożliwiając główną stronę i dwa poziomy zagnieżdżonych zasobów.

```python
# Step 3: Limit the depth to three levels
resource_options.max_handling_depth = 3
```

- **Depth 1** – sam plik HTML.  
- **Depth 2** – zasoby bezpośrednio odwoływane przez HTML (np. znaczniki `<link>` lub `<script>`).  
- **Depth 3** – zasoby odwoływane przez te zasoby pierwszego poziomu (np. importy CSS wewnątrz arkusza stylów).  

Ustawienie `max_handling_depth` zatrzymuje parser po trzech przeskokach, co jest szczególnie przydatne, gdy **load large HTML pages**, które zawierają wiele bibliotek zewnętrznych.

## Krok 3: Load the HTML document (how to load html document)

Teraz, gdy opcje są gotowe, możesz **load the HTML document**. Przekaż skonfigurowane `resource_options` do konstruktora `HTMLDocument`.

```python
# Step 4: Load the HTML document using the configured options
doc = HTMLDocument(
    "YOUR_DIRECTORY/big_page.html",
    resource_handling_options=resource_options
)
```

> **Wyjaśnienie:** Klasa `HTMLDocument` odczytuje plik, rozwiązuje zasoby zgodnie z limitem głębokości i buduje DOM, który możesz zapytać lub wyrenderować. Jeśli plik nie istnieje lub ścieżka jest nieprawidłowa, Aspose.HTML zgłasza `FileNotFoundError`.

### Zweryfikuj, że strona została załadowana pomyślnie

Szybki sposób, aby potwierdzić, że dokument jest gotowy, to wydrukowanie liczby węzłów potomnych w elemencie root:

```python
print(f"Root has {len(doc.root.child_nodes)} child nodes.")
```

Jeśli wynik pokazuje liczbę różną od zera, parser zakończył się sukcesem. Dla *large HTML page* możesz także chcieć sprawdzić liczbę zewnętrznych zasobów, które zostały faktycznie pobrane:

```python
fetched = doc.resource_handling_options.fetched_resources
print(f"Fetched {len(fetched)} external resources (max depth = {resource_options.max_handling_depth}).")
```

## Obsługa przypadków brzegowych i typowych pułapek

### 1. Brakujące zasoby

Gdy powiązany plik CSS lub JS jest niedostępny, Aspose.HTML pomija go cicho, ale zapisuje ostrzeżenie. Aby przechwycić te ostrzeżenia, włącz logowanie:

```python
import logging
logging.basicConfig(level=logging.WARNING)
```

### 2. Odwołania cykliczne

Nawet przy limicie głębokości, odwołania cykliczne mogą powodować marnowanie czasu przez parser. Jeśli zauważysz wyjątkowo długie czasy ładowania, rozważ zmniejszenie `max_handling_depth` do `2` lub `1`.

### 3. Bardzo duże strony (> 10 MB)

Dla niezwykle dużych stron zwiększ limit rekurencji Pythona **tylko jeśli** zweryfikowałeś, że głębokość jest bezpieczna:

```python
import sys
sys.setrecursionlimit(2000)  # optional, use with caution
```

Jednak zalecane podejście to utrzymanie niskiej głębokości i pozwolenie opcjom na odfiltrowanie niepotrzebnych zasobów.

## Pełny, działający przykład

Poniżej znajduje się kompletny skrypt, który możesz skopiować i wkleić do pliku o nazwie `load_html.py`. Dostosuj ścieżkę pliku, aby wskazywała na Twój własny plik HTML.

```python
# load_html.py
# Demonstrates how to create resource handling options,
# limit handling depth, and load a large HTML page with Aspose.HTML.

from aspose.html import *
import logging
import sys

# Optional: show warnings about missing resources
logging.basicConfig(level=logging.WARNING)

def main():
    # 1️⃣ Create and configure resource handling options
    resource_options = ResourceHandlingOptions()
    resource_options.max_handling_depth = 3  # limit to three levels

    # 2️⃣ Load the HTML document using the options
    html_path = "YOUR_DIRECTORY/big_page.html"  # <-- replace with your file
    doc = HTMLDocument(html_path, resource_handling_options=resource_options)

    # 3️⃣ Verify the load
    print(f"Root has {len(doc.root.child_nodes)} child nodes.")
    fetched = doc.resource_handling_options.fetched_resources
    print(f"Fetched {len(fetched)} external resources (max depth = {resource_options.max_handling_depth}).")

    # Optional: increase recursion limit for huge documents (use with care)
    # sys.setrecursionlimit(2000)

if __name__ == "__main__":
    main()
```

Uruchomienie skryptu:

```bash
python load_html.py
```

**Oczekiwany wynik** (przykład dla umiarkowanej strony):

```
Root has 12 child nodes.
Fetched 8 external resources (max depth = 3).
```

Dla naprawdę ogromnej strony liczby będą wyższe, ale skrypt nadal będzie respektował ustawiony limit głębokości.

## Najlepsze praktyki i dalsze kroki

- **Reuse options:** Jeśli przetwarzasz wiele stron w partii, utwórz jedną instancję `ResourceHandlingOptions` i używaj jej ponownie, aby uniknąć zbędnego tworzenia obiektów.  
- **Combine with rendering:** Po załadowaniu możesz wyrenderować DOM do PDF, obrazu lub nawet oczyszczonego ciągu HTML przy użyciu `HTMLRenderer` z Aspose.HTML.  
- **Explore other options:** `ResourceHandlingOptions` pozwala także definiować własne obsługi pobierania, ustawiać limity czasu lub listy dozwolonych/zakazanych domen. Są one przydatne, gdy musisz **load large HTML pages** z niepewnych źródeł.  

## Podsumowanie

Teraz wiesz, jak **create resource handling options**, skonfigurować bezpieczną głębokość i **load an HTML document** — w tym *large HTML pages* — przy użyciu Aspose.HTML for Python. Ograniczając głębokość obsługi, chronisz swoją aplikację przed niekontrolowanymi żądaniami sieciowymi, jednocześnie pobierając niezbędne zasoby potrzebne do dokładnego renderowania.

Śmiało eksperymentuj z różnymi wartościami głębokości, własnymi obsługami pobierania lub integruj załadowany DOM w dalszych pipeline'ach przetwarzania, takich jak generowanie PDF czy analiza treści. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [How to Render HTML – Complete Guide with Custom Resource Handler](/html/english/net/rendering-html-documents/how-to-render-html-complete-guide-with-custom-resource-handl/)
- [Load HTML Using URL in .NET with Aspose.HTML](/html/english/net/html-document-manipulation/load-html-using-url/)
- [Load HTML Using a Remote Server in .NET with Aspose.HTML](/html/english/net/html-document-manipulation/load-html-using-remote-server/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}