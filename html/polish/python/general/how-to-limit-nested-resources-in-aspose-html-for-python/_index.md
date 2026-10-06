---
category: general
date: 2026-10-05
description: Dowiedz się, jak ograniczyć zagnieżdżone zasoby w Aspose.HTML dla Pythona,
  aby zapobiec nieskończonej rekurencji i kontrolować głębokość zasobów.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- limit nested resources
- prevent infinite recursion
language: pl
lastmod: 2026-10-05
og_description: Ogranicz zagnieżdżone zasoby w Aspose.HTML dla Pythona, aby zapobiec
  nieskończonej rekurencji. Postępuj zgodnie z tym przewodnikiem krok po kroku, aby
  bezpiecznie kontrolować głębokość zasobów.
og_image_alt: Diagram illustrating limit nested resources setting in Aspose.HTML
og_title: Ogranicz zagnieżdżone zasoby w Aspose.HTML – zatrzymaj nieskończoną rekurencję
schemas:
- author: Aspose
  dateModified: '2026-10-05'
  description: Learn how to limit nested resources in Aspose.HTML for Python to prevent
    infinite recursion and control resource depth.
  headline: How to limit nested resources in Aspose.HTML for Python
  type: TechArticle
- description: Learn how to limit nested resources in Aspose.HTML for Python to prevent
    infinite recursion and control resource depth.
  name: How to limit nested resources in Aspose.HTML for Python
  steps:
  - name: Prerequisites
    text: '* Python 3.8 or newer. * Aspose.HTML for Python installed (`pip install
      aspose-html`). * A local HTML file that includes multiple levels of linked resources
      (e.g., CSS → @import → more CSS).'
  - name: Common patterns that trigger recursion
    text: '| Pattern | Why it recurses | How the depth limit helps | |---------|----------------|---------------------------|
      | CSS `@import` chain that loops back to the original file | Each import creates
      a new resource request | The parser stops after `max_handling_depth` levels
      | | JavaScript that dynamica'
  - name: Tips for fine‑tuning the limit
    text: '* **Start with `3`** – most sites need at most two levels (page → CSS →
      imported CSS). * **Increase to `5`** only if you know the page legitimately
      uses deeper nesting. * **Set to `1`** when you only need the main document and
      want to skip all external resources (great for quick text extraction).'
  type: HowTo
tags:
- Aspose.HTML
- Python
- HTML processing
- resource handling
title: Jak ograniczyć zagnieżdżone zasoby w Aspose.HTML dla Pythona
url: /pl/python/general/how-to-limit-nested-resources-in-aspose-html-for-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak ograniczyć zagnieżdżone zasoby w Aspose.HTML dla Pythona

Jeśli potrzebujesz **ograniczyć zagnieżdżone zasoby** podczas ładowania dokumentu HTML przy użyciu Aspose.HTML, ten przewodnik pokaże Ci dokładnie, jak to zrobić. Kontrolowanie głębokości obsługi zasobów **zapobiega nieskończonej rekurencji**, gdy strona odwołuje się do siebie poprzez CSS, skrypty lub obrazy.

W kolejnych sekcjach dowiesz się, dlaczego ograniczanie zagnieżdżonych zasobów ma znaczenie, jak skonfigurować `ResourceHandlingOptions` oraz jak zweryfikować, że dokument ładuje się bez wyczerpania pamięci lub wystąpienia przepełnienia stosu.

## Czego się nauczysz

* Dlaczego zagnieżdżone zasoby mogą powodować nieskończoną pętlę rekurencji.
* Jak ustawić maksymalną głębokość obsługi za pomocą `ResourceHandlingOptions`.
* Kompletny, gotowy do uruchomienia przykład w Pythonie, który demonstruje tę technikę.
* Wskazówki dotyczące rozwiązywania typowych problemów, takich jak cykliczne importy CSS.

### Wymagania wstępne

* Python 3.8 lub nowszy.
* Aspose.HTML dla Pythona zainstalowany (`pip install aspose-html`).
* Lokalny plik HTML zawierający wiele poziomów powiązanych zasobów (np. CSS → @import → kolejny CSS).

---

## Krok 1: Import wymaganych klas Aspose.HTML

Pierwszym krokiem jest wprowadzenie niezbędnych klas do zakresu. `HTMLDocument` parsuje plik, natomiast `ResourceHandlingOptions` pozwala kontrolować, jak głęboko parser podąża za powiązanymi zasobami.

```python
# Import required classes from the Aspose.HTML package
from aspose.html import HTMLDocument, ResourceHandlingOptions
```

*Dlaczego to ważne*: Bez importu `ResourceHandlingOptions` nie możesz ustawić limitu głębokości, co oznacza, że parser będzie podążał za każdym powiązanym zasobem w nieskończoność.

---

## Krok 2: Skonfiguruj głębokość obsługi zasobów

Utwórz instancję `ResourceHandlingOptions` i ustaw `max_handling_depth`. Głębokość **3** zatrzymuje parser po trzech poziomach zagnieżdżonych zasobów, co zazwyczaj wystarcza dla typowych stron internetowych, jednocześnie chroniąc przed niekontrolowaną rekurencją.

```python
# Create a ResourceHandlingOptions object
resource_options = ResourceHandlingOptions()

# Limit nested resources to three levels
resource_options.max_handling_depth = 3  # This value prevents infinite recursion
```

*Dlaczego to ważne*: Jeśli strona odwołuje się do pliku CSS, który z kolei importuje kolejny plik CSS odwołujący się do pierwotnego, parser mógłby działać w nieskończoność. Właściwość `max_handling_depth` mówi Aspose.HTML, aby zatrzymał się po określonej liczbie poziomów, skutecznie **zapobiegając nieskończonej rekurencji**.

---

## Krok 3: Załaduj dokument HTML z skonfigurowanymi opcjami

Przekaż obiekt `resource_options` do konstruktora `HTMLDocument`. Parser będzie teraz respektował ustalony limit głębokości.

```python
# Load the HTML document using the configured resource handling options
doc = HTMLDocument(
    "YOUR_DIRECTORY/big_page.html",
    resource_handling_options=resource_options
)

# Optional: verify that the document loaded successfully
print("Document loaded. Number of pages:", doc.pages.count)
```

*Dlaczego to ważne*: Dostarczając `resource_handling_options`, zapewniasz, że wszelkie zagnieżdżone obrazy, arkusze stylów lub skrypty są przetwarzane tylko do dozwolonej głębokości. Instrukcja `print` potwierdza, że dokument został załadowany bez wystąpienia błędu rekurencji.

---

## Jak **zapobiegać nieskończonej rekurencji** w rzeczywistych scenariuszach

### Typowe wzorce wywołujące rekurencję

| Wzorzec | Dlaczego powoduje rekurencję | Jak pomaga limit głębokości |
|---------|-----------------------------|-----------------------------|
| Łańcuch `@import` w CSS, który wraca do pierwotnego pliku | Każdy import tworzy nowe żądanie zasobu | Parser zatrzymuje się po osiągnięciu poziomu `max_handling_depth` |
| JavaScript dynamicznie ładujący dodatkowe skrypty odwołujące się do pierwotnego skryptu | Skrypty mogą wywoływać kolejne połączenia sieciowe w nieskończoność | Limit głębokości ogranicza liczbę ładowań skryptów |
| Obrazy generowane za pomocą data URL odwołujących się do innych zasobów | Parser traktuje każdy data URL jako osobny zasób | Po przekroczeniu limitu dalsze data URL są ignorowane |

### Wskazówki dotyczące dopasowywania limitu

* **Zacznij od `3`** – większość witryn potrzebuje maksymalnie dwóch poziomów (strona → CSS → importowany CSS).  
* **Zwiększ do `5`** tylko wtedy, gdy wiesz, że strona rzeczywiście używa głębszego zagnieżdżenia.  
* **Ustaw na `1`**, gdy potrzebujesz jedynie głównego dokumentu i chcesz pominąć wszystkie zewnętrzne zasoby (idealne do szybkiego wyodrębniania tekstu).

---

## Pełny, gotowy do uruchomienia przykład

Poniżej znajduje się samodzielny skrypt, który możesz skopiować, dostosować ścieżkę do pliku i uruchomić od razu.

```python
# limit_nested_resources_example.py
# -------------------------------------------------
# Demonstrates how to limit nested resources in Aspose.HTML
# to prevent infinite recursion when loading large pages.
# -------------------------------------------------

from aspose.html import HTMLDocument, ResourceHandlingOptions

def load_html_with_limit(html_path: str, max_depth: int = 3):
    """
    Loads an HTML file while limiting the depth of nested resources.

    Args:
        html_path: Path to the local HTML file.
        max_depth: Maximum number of nested resource levels.

    Returns:
        An HTMLDocument instance if loading succeeds.
    """
    # Configure the depth limit
    options = ResourceHandlingOptions()
    options.max_handling_depth = max_depth

    # Load the document using the configured options
    document = HTMLDocument(html_path, resource_handling_options=options)

    # Simple verification output
    print(f"Loaded '{html_path}' with max depth {max_depth}.")
    print(f"Total pages: {document.pages.count}")

    return document

if __name__ == "__main__":
    # Replace with the path to your HTML file
    html_file = "YOUR_DIRECTORY/big_page.html"
    load_html_with_limit(html_file, max_depth=3)
```

**Oczekiwany wynik**

```
Loaded 'YOUR_DIRECTORY/big_page.html' with max depth 3.
Total pages: 1
```

Jeśli parser napotka rekurencję głębszą niż trzy poziomy, przestanie przetwarzać dalsze zasoby i skrypt zakończy się bez podnoszenia wyjątku — dokładnie to, czego potrzebujesz, aby **zapobiec nieskończonej rekurencji**.

---

## Pro tip: logowanie zdarzeń obsługi zasobów

Aspose.HTML może emitować zdarzenia, gdy pomija zasób z powodu limitu głębokości. Włączenie logowania pomaga zrozumieć, które zasoby zostały pominięte.

```python
import logging
logging.basicConfig(level=logging.INFO)

# Inside load_html_with_limit, after creating `options`:
options.resource_handling_event_handler = lambda sender, args: \
    logging.info(f"Skipped resource: {args.resource_uri} (depth {args.current_depth})")
```

Ten fragment wypisuje linię dla każdego zasobu, który przekracza limit, dając wgląd w to, co zostało pominięte.

---

## Podsumowanie

Wiesz już, jak **ograniczyć zagnieżdżone zasoby** w Aspose.HTML dla Pythona i dlaczego jest to niezbędne do **zapobiegania nieskończonej rekurencji**. Konfigurując `ResourceHandlingOptions.max_handling_depth`, chronisz aplikację przed niekontrolowanym ładowaniem zasobów, zmniejszasz zużycie pamięci i utrzymujesz przewidywalność przetwarzania HTML.

Gotowy na kolejny krok? Zapoznaj się z powiązanymi tematami:

* **Parsowanie HTML bez zasobów zewnętrznych** – ustaw `max_handling_depth` na 1.  
* **Wyodrębnianie tekstu z dużych stron HTML** – połącz limit głębokości z `HTMLDocument.text`.  
* **Konwersja HTML do PDF przy kontrolowaniu głębokości zasobów** – przekaż te same `ResourceHandlingOptions` do API konwersji PDF.

Śmiało eksperymentuj z różnymi wartościami limitu i podziel się swoimi spostrzeżeniami w komentarzach. Szczęśliwego kodowania!  

![Diagram illustrating limit nested resources setting in Aspose.HTML](limit_nested_resources.png "limit nested resources diagram")


## Co powinieneś nauczyć się dalej?


Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu z krok po kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Custom Resource Handler in Aspose HTML – Save to Stream Guide](/html/english/net/advanced-features/custom-resource-handler-in-aspose-html-save-to-stream-guide/)
- [How to Sandbox JavaScript – Complete Aspose.HTML Guide](/html/english/java/advanced-usage/how-to-sandbox-javascript-complete-aspose-html-guide/)
- [Render HTML to PDF with Aspose.HTML – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/render-html-to-pdf-with-aspose-html-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}