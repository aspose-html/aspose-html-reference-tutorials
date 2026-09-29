---
category: general
date: 2026-09-29
description: Utwórz opcje obsługi zasobów, aby efektywnie ładować duże pliki stron
  HTML, kontrolując przy tym głębokość i zużycie pamięci.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- load large html page
- HTML document parsing
- limit resource depth
- memory‑efficient HTML loading
language: pl
lastmod: 2026-09-29
og_description: Utwórz opcje obsługi zasobów, aby szybko ładować duże strony HTML,
  jednocześnie zapobiegając nadmiernemu zużyciu zasobów i utrzymując kontrolę nad
  głębokością parsowania.
og_image_alt: Screenshot showing resource handling options configuration for loading
  a large HTML page
og_title: Utwórz opcje obsługi zasobów – efektywne ładowanie dużych stron HTML
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Create resource handling options to efficiently load large HTML page
    files while controlling depth and memory usage.
  headline: Create resource handling options to load large HTML pages
  type: TechArticle
tags:
- HTML
- resource handling
- performance
title: Utwórz opcje obsługi zasobów do ładowania dużych stron HTML
url: /pl/python/general/create-resource-handling-options-to-load-large-html-pages/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz opcje obsługi zasobów do ładowania dużych stron HTML

Jeśli potrzebujesz **utworzyć opcje obsługi zasobów** dla ogromnego pliku HTML, ten przewodnik pokaże Ci dokładnie, jak je skonfigurować, a następnie **bezpiecznie ładować duże strony HTML**. Duże strony często zawierają głęboko zagnieżdżone skrypty, obrazy lub zewnętrzne zasoby, które mogą spowodować, że parser będzie rekurencyjnie przetwarzał je w nieskończoność. Ograniczając automatyczną głębokość ładowania, utrzymujesz przewidywalne zużycie pamięci i unikasz przekroczeń czasu.

W kolejnych sekcjach dowiesz się, jak:

* skonfigurować instancję `ResourceHandlingOptions`,
* zastosować tę konfigurację przy otwieraniu pliku za pomocą `HTMLDocument`,
* obsłużyć typowe przypadki brzegowe, takie jak brakujące pliki lub zasoby przekraczające dozwoloną głębokość.

Tutorial zakłada, że masz zainstalowaną bibliotekę udostępniającą `HTMLDocument` i `ResourceHandlingOptions` (na przykład pakiet *HtmlParser*) w swoim środowisku Pythona.

## Czego będziesz potrzebować

* Python 3.9 lub nowszy  
* `htmlparser` (lub równoważna biblioteka definiująca `HTMLDocument` i `ResourceHandlingOptions`)  
* Duży plik HTML, który chcesz przetworzyć – w przykładzie użyto `big_page.html` umieszczonego w folderze `YOUR_DIRECTORY`.

Pakiet wymagany można zainstalować za pomocą:

```bash
pip install htmlparser
```

## Utwórz opcje obsługi zasobów

Pierwszym krokiem jest **utworzenie opcji obsługi zasobów**, które ograniczą, jak głęboko parser będzie podążał za automatycznym ładowaniem zasobów (skrypty, iframe’y, importy CSS itp.). Ustawienie `max_handling_depth` na niską wartość zapobiega, aby parser nie podążał za niekończącymi się łańcuchami zewnętrznych zasobów.

```python
# Step 1: Create resource handling options and limit automatic loading depth
from htmlparser import ResourceHandlingOptions

# Instantiate the options object
res_opts = ResourceHandlingOptions()

# Restrict the parser to three levels of automatic resource handling
# This value balances completeness with performance for most large pages
res_opts.max_handling_depth = 3
```

**Dlaczego to ważne:**  
Gdy strona zawiera wiele zagnieżdżonych zasobów, każdy dodatkowy poziom mnoży ilość danych, które parser musi pobrać. Ograniczając głębokość, zapewniasz, że operacja pozostanie w akceptowalnych granicach pamięci i czasu, co jest niezbędne przy **ładowaniu dużych stron HTML** na serwerze o ograniczonych zasobach.

## Ładuj duże strony HTML efektywnie

Gdy obiekt opcji jest gotowy, przekaż go do konstruktora `HTMLDocument`. Parser będzie respektował limit głębokości podczas odczytu pliku.

```python
# Step 2: Load the HTML document using the configured options
from htmlparser import HTMLDocument

# Provide the path to your large HTML file and the previously defined options
doc = HTMLDocument(
    "YOUR_DIRECTORY/big_page.html",
    ResourceHandlingOptions=res_opts
)

# Verify that the document was loaded
print(f"Document title: {doc.title}")
print(f"Number of top‑level nodes: {len(doc.root.children)}")
```

**Dlaczego to działa:**  
`HTMLDocument` przyjmuje argument `ResourceHandlingOptions`, co pozwala wstrzyknąć ograniczenie głębokości bezpośrednio do potoku parsowania. Biblioteka następnie odczytuje plik, stosuje limit i buduje drzewo podobne do DOM, które możesz przeszukiwać.

### Typowe warianty

| Wariant | Kiedy używać | Zmiana w kodzie |
|---------|--------------|-----------------|
| **Zwiększ głębokość** | Strona korzysta z głęboko zagnieżdżonych include’ów (np. wielopoziomowe iframe’y). | `res_opts.max_handling_depth = 5` |
| **Wyłącz automatyczne ładowanie** | Potrzebujesz tylko statycznego HTML bez żadnych zewnętrznych zasobów. | `res_opts.max_handling_depth = 0` |
| **Niestandardowy timeout** | Opóźnienia sieciowe przy zewnętrznych zasobach są problemem. | `res_opts.resource_timeout = 10  # seconds` |

## Pełny przykład z obsługą błędów

Poniżej znajduje się kompletny, gotowy do uruchomienia skrypt, który tworzy opcje, ładuje plik i elegancko obsługuje typowe niepowodzenia, takie jak brakujące pliki lub zasoby przekraczające dozwoloną głębokość.

```python
# complete_example.py
import os
from htmlparser import HTMLDocument, ResourceHandlingOptions, ResourceError

def load_large_html(path: str, max_depth: int = 3) -> HTMLDocument | None:
    """Create resource handling options and load a large HTML page safely."""
    if not os.path.isfile(path):
        print(f"Error: file not found → {path}")
        return None

    # Create and configure the options
    res_opts = ResourceHandlingOptions()
    res_opts.max_handling_depth = max_depth

    try:
        # Load the document with the configured options
        doc = HTMLDocument(path, ResourceHandlingOptions=res_opts)
        return doc
    except ResourceError as e:
        # This exception is raised when the parser exceeds the depth limit
        print(f"Resource handling error: {e}")
        return None
    except Exception as e:
        # Catch‑all for unexpected issues (e.g., malformed HTML)
        print(f"Unexpected error while loading HTML: {e}")
        return None


if __name__ == "__main__":
    html_path = "YOUR_DIRECTORY/big_page.html"
    document = load_large_html(html_path, max_depth=3)

    if document:
        print("✅ Document loaded successfully")
        print(f"Title: {document.title}")
        print(f"Root children count: {len(document.root.children)}")
    else:
        print("❌ Failed to load the HTML document")
```

**Oczekiwany wynik** (zakładając, że plik istnieje i jest poprawnie sformatowany):

```
✅ Document loaded successfully
Title: Example Large Page
Root children count: 42
```

Jeśli parser napotka zasób, który spowodowałby przekroczenie `max_handling_depth`, blok `ResourceError` wypisze czytelną wiadomość zamiast spowodować awarię programu.

## Porady i obsługa przypadków brzegowych

* **Monitoruj pamięć** – Nawet przy limitach głębokości bardzo duże strony mogą przydzielać znaczną ilość RAM. Użyj modułu `tracemalloc` w Pythonie, aby profilować zużycie pamięci, jeśli planujesz przetwarzać wiele plików w partii.
* **Waliduj HTML przed parsowaniem** – Uruchomienie lekkiego walidatora (np. `html5lib`) może wykryć nieprawidłowe tagi, które w przeciwnym razie spowodowałyby nieoczekiwanie głębokie drzewo.
* **Przetwarzanie równoległe** – Gdy potrzebujesz **ładować duże strony HTML** jednocześnie, opakuj `load_large_html` w pulę wątków, ale utrzymuj niskie `max_handling_depth`, aby uniknąć przeciążenia zasobów sieciowych.

## Zakończenie

Teraz wiesz, jak **utworzyć opcje obsługi zasobów** i zastosować je do **ładowania dużych stron HTML** w kontrolowany, pamięcio‑oszczędny sposób. Konfigurując `max_handling_depth`, zapobiegasz niekontrolowanemu pobieraniu zasobów, a pełny przykład demonstruje solidną obsługę błędów w rzeczywistych scenariuszach.

Następnie rozważ zgłębienie technik **parsowania dokumentów HTML**, takich jak zapytania XPath, selektory CSS czy parsowanie strumieniowe, które dodatkowo zmniejszają obciążenie pamięci przy pracy z masywnymi plikami. Eksperymentuj z różnymi wartościami głębokości i ustawieniami timeout, aby znaleźć optymalne rozwiązanie dla swojego obciążenia. Szczęśliwego parsowania!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu wraz z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak renderować HTML – Kompletny przewodnik z własnym obsługiwaczem zasobów](/html/english/net/rendering-html-documents/how-to-render-html-complete-guide-with-custom-resource-handl/)
- [Jak zapisać HTML w C# – Kompletny przewodnik z własnym obsługiwaczem zasobów](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Własny obsługiwacz zasobów w Aspose HTML – Przewodnik zapisu do strumienia](/html/english/net/advanced-features/custom-resource-handler-in-aspose-html-save-to-stream-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}