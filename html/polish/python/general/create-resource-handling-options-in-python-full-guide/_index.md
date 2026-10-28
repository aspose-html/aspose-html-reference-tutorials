---
category: general
date: 2026-07-21
description: Utwórz opcje obsługi zasobów w Pythonie i dowiedz się, jak ustawić maksymalną
  głębokość obsługi przy parsowaniu HTML. Skorzystaj z tego samouczka krok po kroku,
  aby zapewnić niezawodne zarządzanie zasobami.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to set max handling depth
language: pl
lastmod: 2026-07-21
og_description: Utwórz opcje obsługi zasobów w Pythonie i natychmiast zobacz, jak
  ustawić maksymalną głębokość obsługi dla bezpiecznego ładowania dokumentów HTML.
  Opanuj tę technikę w kilka minut.
og_image_alt: Screenshot of Python code that creates resource handling options with
  max handling depth set
og_title: Tworzenie opcji obsługi zasobów w Pythonie – Kompletny przewodnik krok po
  kroku
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  headline: Create Resource handling options in Python – Full Guide
  type: TechArticle
- description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  name: Create Resource handling options in Python – Full Guide
  steps:
  - name: Circular References
    text: 'Some legacy sites embed an iframe that points back to the original page,
      creating a loop. With `max_handling_depth` set, the loop is automatically broken
      after the third iteration. However, you might still see a warning in the logs.
      To silence noisy logs, adjust the logger level:'
  - name: Missing Resources
    text: 'If a nested resource fails to load (404 or network timeout), the parser
      throws an exception by default. Wrap the loading call in a `try/except` block
      to keep your application alive:'
  - name: Adjusting Depth Dynamically
    text: 'Sometimes you need different depths for different parts of your pipeline.
      Because `resource_options` is a mutable object, you can change `max_handling_depth`
      on the fly:'
  type: HowTo
tags:
- Python
- HTML parsing
- resource management
title: Tworzenie opcji obsługi zasobów w Pythonie – pełny przewodnik
url: /pl/python/general/create-resource-handling-options-in-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz Resource handling options w Pythonie – Pełny przewodnik

Ever wondered how to **create resource handling options** for a massive HTML page without blowing up your memory? You're not the only one. When you feed a gigantic document into a parser, nested resources like frames, iframes, or linked CSS can quickly spiral out of control.  

The good news? You can tell the parser to stop after a certain number of nested levels. In this tutorial we'll show you **how to set max handling depth** and keep your application responsive. Ready? Let’s dive in.

## Czego się nauczysz

- Why limiting nesting depth matters for performance and security.  
- The exact code you need to **create resource handling options** using the `ResourceHandlingOptions` class.  
- How to configure `max_handling_depth` so the parser stops after three levels.  
- Tips for handling edge cases, such as documents with circular references or missing resources.  

Wcześniejsze doświadczenie z biblioteką nie jest wymagane — wystarczy działająca instalacja Python 3 oraz podstawowa znajomość operacji I/O na plikach.

## Wymagania wstępne

- Python 3.8+ (biblioteka działa na wszystkich nowszych wersjach).  
- The `htmlparser` package that provides `HTMLDocument` and `ResourceHandlingOptions`.  
- A sample HTML file (`big_page.html`) placed in a folder you can reference.  

If you haven’t installed the package yet, run:

```bash
pip install htmlparser
```

Teraz, gdy przygotowania są za sobą, przejdźmy do sedna sprawy.

## Utwórz Resource handling options – Krok 1

Na początek potrzebujesz instancji `ResourceHandlingOptions`. Pomyśl o niej jak o skrzynce narzędziowej, w której możesz ustawić limity i zasady, których parser ma przestrzegać.

```python
# Step 1: Create resource handling options and limit nesting depth
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # Stop after three levels of nested resources
```

**Dlaczego to ważne:**  
Gdy parser napotyka `<iframe>` wewnątrz kolejnego `<iframe>`, zwykle podąża za łańcuchem w nieskończoność. Ograniczając głębokość do `3`, zapobiegasz niekontrolowanej rekurencji, która mogłaby wyczerpać pamięć RAM lub spowodować przepełnienie stosu.

> **Pro tip:** Jeśli parsujesz nieufne treści (np. HTML przesłany przez użytkownika), rozważ obniżenie głębokości do `1` lub `2`, aby złagodzić potencjalne ataki.

## Wczytaj dokument HTML – Krok 2

Gdy obiekt opcji jest gotowy, przekaż go do `HTMLDocument`. Konstruktor uwzględni ustawiony `max_handling_depth`.

```python
# Step 2: Load the HTML document using the configured options
html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
```

**Co się dzieje pod maską?**  
`HTMLDocument` odczytuje plik, buduje drzewo DOM, a następnie przegląda każdy zewnętrzny zasób (arkusze stylów, skrypty, obrazy). Gdy natrafi na zagnieżdżony zasób, sprawdza `resource_options.max_handling_depth`. Jeśli limit zostanie osiągnięty, parser zapisuje ostrzeżenie i pomija dalsze zagnieżdżanie.

Oznacza to, że otrzymujesz w pełni użyteczny DOM dla pierwszych trzech warstw, a reszta jest bezpiecznie pomijana.

## Zweryfikuj konfigurację – Krok 3

Zawsze warto potwierdzić, że Twoje ustawienia weszły w życie. Obiekt `resource_options` udostępnia swój aktualny stan, więc możesz go wydrukować lub sprawdzić w teście.

```python
# Step 3: Verify that the max handling depth is set correctly
assert resource_options.max_handling_depth == 3, "Depth limit not applied!"

print(f"Resource handling options configured: max depth = {resource_options.max_handling_depth}")
```

Jeśli asercja przejdzie, możesz być pewny, że parser będzie przestrzegał limitu przez cały dalszy przebieg.

## Obsługa przypadków brzegowych

### Odwołania cykliczne

Niektóre starsze witryny osadzają iframe, który odwołuje się do pierwotnej strony, tworząc pętlę. Przy ustawionym `max_handling_depth` pętla jest automatycznie przerywana po trzeciej iteracji. Jednak w logach może nadal pojawiać się ostrzeżenie. Aby wyciszyć hałaśliwe logi, dostosuj poziom loggera:

```python
import logging
logging.getLogger("htmlparser").setLevel(logging.ERROR)
```

### Brakujące zasoby

Jeśli zagnieżdżony zasób nie uda się załadować (404 lub timeout sieci), parser domyślnie zgłasza wyjątek. Owiń wywołanie ładowania w blok `try/except`, aby utrzymać aplikację przy życiu:

```python
try:
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
except Exception as e:
    print(f"Failed to load a nested resource: {e}")
    # Fallback: load the document without additional resources
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

### Dynamiczna zmiana głębokości

Czasami potrzebujesz różnych głębokości dla różnych części swojego potoku. Ponieważ `resource_options` jest obiektem mutowalnym, możesz zmienić `max_handling_depth` w locie:

```python
resource_options.max_handling_depth = 5   # Temporarily allow deeper nesting
html_doc_deep = HTMLDocument("deep_page.html", resource_options)

resource_options.max_handling_depth = 2   # Tighten for a lightweight preview
html_doc_preview = HTMLDocument("preview.html", resource_options)
```

Pamiętaj tylko, aby zresetować wartość przed ponownym użyciem tej samej instancji opcji w innym wątku.

## Pełny działający przykład

Poniżej znajduje się kompletny skrypt, który możesz skopiować‑wkleić, dostosować ścieżki plików i uruchomić od razu.

```python
import logging
from htmlparser import HTMLDocument, ResourceHandlingOptions

# Optional: Reduce noisy output
logging.getLogger("htmlparser").setLevel(logging.ERROR)

def load_document(path: str, max_depth: int = 3):
    """
    Load an HTML document with a controlled resource handling depth.
    Returns the HTMLDocument instance.
    """
    opts = ResourceHandlingOptions()
    opts.max_handling_depth = max_depth    # How to set max handling depth
    try:
        doc = HTMLDocument(path, opts)
        print(f"Loaded '{path}' with max depth {max_depth}.")
        return doc
    except Exception as exc:
        print(f"Error loading '{path}': {exc}")
        # Fallback to a simple load without resource handling
        return HTMLDocument(path)

if __name__ == "__main__":
    # Example 1: Standard depth
    doc1 = load_document("YOUR_DIRECTORY/big_page.html", max_depth=3)

    # Example 2: Deeper inspection for debugging
    doc2 = load_document("YOUR_DIRECTORY/complex_page.html", max_depth=5)

    # Example 3: Very shallow preview (e.g., thumbnail generation)
    doc3 = load_document("YOUR_DIRECTORY/preview_page.html", max_depth=1)
```

**Oczekiwany wynik (gdy pliki istnieją i są poprawnie sformatowane):**

```
Loaded 'YOUR_DIRECTORY/big_page.html' with max depth 3.
Loaded 'YOUR_DIRECTORY/complex_page.html' with max depth 5.
Loaded 'YOUR_DIRECTORY/preview_page.html' with max depth 1.
```

Jeśli plik nie może zostać odczytany, zobaczysz komunikat o błędzie zamiast awarii.

![Create resource handling options in Python](/images/resource-options.png){alt="Utwórz Resource handling options w Pythonie"}

## Podsumowanie – Dlaczego to podejście jest świetne

- **Safety first:** Ograniczanie głębokości zagnieżdżenia zapobiega niekontrolowanej rekurencji i nadmiernemu zużyciu pamięci.  
- **Flexibility:** Możesz zmienić `max_handling_depth` w czasie działania, aby dopasować go do różnych scenariuszy.  
- **Simplicity:** Kilka linijek kodu pozwala Ci **create resource handling options** i natychmiast je zastosować.  

Krótko mówiąc, masz teraz solidny wzorzec do kontrolowania, jak głęboko Twój parser podąża za zewnętrznymi zasobami.

## Co dalej?

- Zbadaj dalej klasę `ResourceHandlingOptions` — istnieją flagi dla buforowania, obsługi timeoutów i filtrowania typów MIME.  
- Połącz ograniczanie głębokości z niestandardowym ciągiem `UserAgent`, aby uniknąć blokowania przez agresywne serwery.  
- Jeśli pracujesz z asynchronicznym I/O, przyjrzyj się wariantowi `aiohtmlparser`, który respektuje te same opcje, ale działa z `asyncio`.  

Śmiało eksperymentuj: spróbuj ustawić głębokość na `0` i zobacz, jak parser ignoruje wszystkie zewnętrzne odwołania. To przydatny skrót, gdy potrzebujesz tylko surowego kodu HTML.

Masz pytania lub trudną stronę, która wciąż sprawia problemy? zostaw komentarz poniżej, a chętnie pomogę Ci dopasować ustawienia. Szczęśliwego parsowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Utwórz HTML z łańcucha w C# – Przewodnik po niestandardowym obsługiwaniu zasobów](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Jak zapisać HTML w C# – Kompletny przewodnik z użyciem niestandardowego obsługiwacza zasobów](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Utwórz sandbox dla HTML w Java – Przewodnik krok po kroku](/html/english/java/creating-managing-html-documents/create-sandbox-for-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}