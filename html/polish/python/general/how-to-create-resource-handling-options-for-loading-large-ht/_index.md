---
category: general
date: 2026-09-16
description: Dowiedz się, jak tworzyć opcje obsługi zasobów i efektywnie ładować duże
  dokumenty HTML przy użyciu Aspose.HTML dla Pythona. Przewodnik krok po kroku z pełnym
  kodem.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- load large html document
- Aspose.HTML Python
- HTML resource management
- nested HTML resources
language: pl
lastmod: 2026-09-16
og_description: Utwórz opcje obsługi zasobów i szybko wczytuj duże dokumenty HTML
  przy użyciu Aspose.HTML dla Pythona. Skorzystaj z tego pełnego samouczka, aby uzyskać
  niezawodne przetwarzanie HTML.
og_image_alt: Python code screenshot that creates resource handling options for large
  HTML documents
og_title: Stwórz opcje obsługi zasobów do ładowania dużych dokumentów HTML – przewodnik
  Pythona
schemas:
- author: Aspose
  dateModified: '2026-09-16'
  description: Learn how to create resource handling options and efficiently load
    large HTML documents with Aspose.HTML for Python. Step‑by‑step guide with full
    code.
  headline: How to create resource handling options for loading large HTML documents
    in Python
  type: TechArticle
- description: Learn how to create resource handling options and efficiently load
    large HTML documents with Aspose.HTML for Python. Step‑by‑step guide with full
    code.
  name: How to create resource handling options for loading large HTML documents in
    Python
  steps:
  - name: 'Optional: Adjust other resource‑handling flags'
    text: You can also control whether external URLs are fetched, whether CSS files
      are parsed, or whether scripts are ignored. These flags are useful when you
      only need the structural DOM and not the full rendering.
  - name: Verify the document was loaded
    text: 'A quick sanity check confirms that the document is ready for further processing:'
  - name: a) Document exceeds the configured depth
    text: 'If the HTML contains deeper nesting than `max_handling_depth`, Aspose.HTML
      stops loading further resources but still returns the partially built DOM. You
      can detect this situation by checking the `resource_options.max_handling_depth`
      after loading:'
  - name: b) Circular references
    text: 'Circular `<iframe>` inclusions can cause infinite loops if depth is not
      limited. The depth limit automatically breaks the cycle, but you may also want
      to log which URLs caused the break:'
  - name: c) Missing external files
    text: 'When `fetch_external_resources` is `True` and a linked CSS or image cannot
      be retrieved (e.g., 404), Aspose.HTML raises a `ResourceNotFoundException`.
      Wrap the loading call in a `try/except` block to handle it gracefully:'
  type: HowTo
tags:
- Aspose.HTML
- Python
- HTML processing
- Resource handling
title: Jak stworzyć opcje obsługi zasobów przy ładowaniu dużych dokumentów HTML w
  Pythonie
url: /pl/python/general/how-to-create-resource-handling-options-for-loading-large-ht/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak utworzyć opcje obsługi zasobów dla ładowania dużych dokumentów HTML w Pythonie

Jeśli potrzebujesz **utworzyć opcje obsługi zasobów** dla ogromnego pliku HTML, ten samouczek pokaże Ci dokładnie, jak to zrobić. Ładowanie dużych dokumentów HTML może szybko zużywać pamięć lub napotykać limity rekurencji, ale poprzez skonfigurowanie odpowiednich opcji utrzymujesz proces stabilny i wydajny.

W tym przewodniku dowiesz się także, jak **ładować duże dokumenty html** przy użyciu Aspose.HTML dla Pythona, jak dostroić głębokość zagnieżdżenia oraz jak obsługiwać typowe przypadki brzegowe, takie jak odwołania cykliczne czy brakujące zasoby. Nie jest wymagana żadna zewnętrzna dokumentacja — wszystko, czego potrzebujesz, znajduje się w poniższych przykładach.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:

* Zainstalowany Python 3.8 lub nowszy.
* Bibliotekę Aspose.HTML dla Pythona (`aspose-html`) zainstalowaną za pomocą `pip install aspose-html`.
* Duży plik HTML (np. `bigpage.html`) zawierający zagnieżdżone zasoby, takie jak obrazy, CSS lub iframe'y.

Jeśli którykolwiek z tych elementów jest brakujący, najpierw go zainstaluj; poniższe kroki zakładają, że środowisko jest gotowe.

## Krok 1: Importuj wymagane klasy Aspose.HTML

Pierwszą rzeczą, którą musisz zrobić, jest zaimportowanie klas umożliwiających pracę z dokumentami HTML oraz ustawieniami obsługi zasobów.

```python
# Step 1: Import the required Aspose.HTML classes
from aspose.html import HTMLDocument, ResourceHandlingOptions
```

`HTMLDocument` reprezentuje plik HTML, który chcesz przetworzyć, natomiast `ResourceHandlingOptions` daje Ci precyzyjną kontrolę nad tym, jak pobierane są zewnętrzne zasoby i jak głęboko biblioteka będzie podążać za zagnieżdżonymi odwołaniami.

## Krok 2: Utwórz opcje obsługi zasobów i ogranicz głębokość zagnieżdżenia

Kiedy **tworzysz opcje obsługi zasobów**, decydujesz, ile poziomów zagnieżdżonych zasobów parser będzie podążał. Ograniczenie głębokości zapobiega niekontrolowanej rekurencji na stronach, które wielokrotnie osadzają inne strony.

```python
# Step 2: Create resource handling options and limit nesting depth
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 5  # Stop after 5 levels of nested resources
```

*Dlaczego ograniczać głębokość zagnieżdżenia?*  
Duży dokument HTML może zawierać wiele znaczników `<iframe>` lub `<object>`, które odwołują się do innych dokumentów, które z kolei zawierają kolejne zasoby. Bez limitu głębokości parser może zużywać nadmierną pamięć lub nawet spowodować błąd `RecursionError`. Ustawienie `max_handling_depth` na rozsądną liczbę (5 w tym przykładzie) zapewnia równowagę między kompletnością a bezpieczeństwem.

### Opcjonalnie: Dostosuj inne flagi obsługi zasobów

Możesz także kontrolować, czy zewnętrzne URL-e są pobierane, czy pliki CSS są parsowane, lub czy skrypty są ignorowane. Te flagi są przydatne, gdy potrzebujesz jedynie strukturalnego DOM, a nie pełnego renderowania.

```python
resource_options.fetch_external_resources = True   # Allow HTTP/HTTPS resources
resource_options.enable_css_parsing = True        # Parse linked CSS files
resource_options.enable_script_execution = False  # Skip JavaScript for speed
```

## Krok 3: Załaduj duży dokument HTML używając skonfigurowanych opcji

Teraz, gdy **utworzyłeś opcje obsługi zasobów**, możesz bezpiecznie **ładować duże dokumenty html** bez przeciążania systemu.

```python
# Step 3: Load the HTML document using the configured options
document_path = "YOUR_DIRECTORY/bigpage.html"
document = HTMLDocument(document_path, resource_options)
```

Konstruktor przyjmuje ścieżkę do pliku oraz obiekt `resource_options`, który przygotowałeś. Aspose.HTML respektuje limit głębokości oraz wszystkie inne ustawione flagi, więc proces ładowania kończy się szybko nawet dla stron o rozmiarze w megabajtach.

### Zweryfikuj, że dokument został załadowany

Szybka kontrola poprawności potwierdza, że dokument jest gotowy do dalszego przetwarzania:

```python
print(f"Document title: {document.title}")
print(f"Root element: {document.root.tag_name}")
print(f"Number of child nodes: {len(document.root.child_nodes)}")
```

Typowy wynik:

```
Document title: Example Large Page
Root element: html
Number of child nodes: 12
```

Jeśli tytuł jest pusty, plik może nie zawierać znacznika `<title>`, ale DOM jest nadal dostępny.

## Krok 4: Przejdź przez DOM, aby policzyć zewnętrzne zasoby

Często potrzebujesz wiedzieć, ile obrazów, arkuszy stylów lub iframe'ów zostało faktycznie załadowanych. Poniższy fragment kodu pokazuje, jak przejść przez DOM i zebrać statystyki.

```python
# Step 4: Count external resources (images, stylesheets, iframes)
resource_counts = {"img": 0, "link": 0, "iframe": 0}

def count_resources(node):
    if node.node_type == node.ELEMENT_NODE:
        tag = node.tag_name.lower()
        if tag == "img":
            resource_counts["img"] += 1
        elif tag == "link" and node.get_attribute("rel") == "stylesheet":
            resource_counts["link"] += 1
        elif tag == "iframe":
            resource_counts["iframe"] += 1

    # Recurse into child nodes
    for child in node.child_nodes:
        count_resources(child)

count_resources(document.root)

print("Resource summary:")
for kind, cnt in resource_counts.items():
    print(f"  {kind}: {cnt}")
```

**Dlaczego przechodzić przez DOM?**  
Nawet przy ograniczaniu głębokości możesz chcieć zweryfikować, że wszystkie oczekiwane zasoby zostały pobrane. Ta pętla daje wyraźny obraz tego, co parser faktycznie załadował.

## Krok 5: Zapisz przetworzony dokument (opcjonalnie)

Jeśli potrzebujesz zachować znormalizowaną wersję HTML (np. po usunięciu niechcianych skryptów), możesz zapisać ją ponownie na dysk.

```python
# Step 5: Save the cleaned document
output_path = "YOUR_DIRECTORY/processed_bigpage.html"
document.save(output_path)
print(f"Processed document saved to {output_path}")
```

Zapisywanie nie zmienia oryginalnego pliku; tworzy nową kopię, która respektuje zdefiniowaną konfigurację obsługi zasobów.

## Krok 6: Obsłuż typowe przypadki brzegowe

### a) Dokument przekracza skonfigurowaną głębokość

Jeśli HTML zawiera głębsze zagnieżdżenie niż `max_handling_depth`, Aspose.HTML przestaje ładować dalsze zasoby, ale nadal zwraca częściowo zbudowany DOM. Możesz wykryć tę sytuację, sprawdzając `resource_options.max_handling_depth` po załadowaniu:

```python
if document.resource_handling_options.max_handling_depth_reached:
    print("Warning: Some nested resources were not loaded due to depth limit.")
```

### b) Odwołania cykliczne

Cykliczne wstawienia `<iframe>` mogą powodować nieskończone pętle, jeśli głębokość nie jest ograniczona. Limit głębokości automatycznie przerywa cykl, ale możesz także chcieć zalogować, które URL-e spowodowały przerwanie:

```python
if document.resource_handling_options.circular_reference_detected:
    print("Circular reference detected and ignored.")
```

### c) Brakujące pliki zewnętrzne

Gdy `fetch_external_resources` jest ustawione na `True` i powiązany CSS lub obraz nie może zostać pobrany (np. 404), Aspose.HTML podnosi `ResourceNotFoundException`. Owiń wywołanie ładowania w blok `try/except`, aby obsłużyć to w sposób elegancki:

```python
try:
    document = HTMLDocument(document_path, resource_options)
except Exception as e:
    print(f"Failed to load resources: {e}")
    # Continue with a fallback or abort as needed
```

## Krok 7: Najlepsze praktyki i wskazówki dotyczące wydajności

* **Reuse `ResourceHandlingOptions`** – Utwórz jedną instancję i przekaż ją do wielu ładowań `HTMLDocument`, jeśli przetwarzasz wiele plików. To unika wielokrotnej alokacji obiektów.
* **Set `max_handling_depth` based on expected nesting** – Dla większości stron internetowych głębokość 3‑5 jest wystarczająca. Zwiększaj ją tylko wtedy, gdy wiesz, że zawartość ma głębokie ramki.
* **Disable script execution** – JavaScript rzadko jest potrzebny przy parsowaniu po stronie serwera i może znacznie spowolnić ładowanie. Utrzymuj `enable_script_execution` ustawione na `False`, chyba że wyraźnie potrzebujesz zmian DOM generowanych przez skrypty.
* **Use streaming I/O for very large files** – Aspose.HTML obsługuje ładowanie ze strumienia; zmniejsza to obciążenie pamięci, gdy plik HTML przekracza kilkaset megabajtów.

```python
from aspose.html import FileStream

with FileStream(document_path, FileStream.READ) as stream:
    document = HTMLDocument(stream, resource_options)
```

## Podsumowanie

Teraz wiesz, jak **utworzyć opcje obsługi zasobów** i niezawodnie **ładować duże dokumenty html** przy użyciu Aspose.HTML dla Pythona. Konfigurując limity głębokości, przełączając pobieranie zewnętrznych zasobów i obsługując przypadki brzegowe, takie jak odwołania cykliczne, utrzymujesz przewidywalne zużycie pamięci i unikasz awarii.

Z tej podstawy możesz:

* Wyodrębniać lub przekształcać zawartość (np. konwertować do PDF lub tekstu prostego).
* Przeprowadzać masową analizę zużycia zasobów na całej stronie internetowej.
* Integrację parsowania HTML w automatycznych pipeline'ach testowych.

Śmiało eksperymentuj z różnymi wartościami `max_handling_depth`, włączaj lub wyłączaj parsowanie CSS i łącz to podejście z innymi bibliotekami Aspose, aby uzyskać bogatsze przepływy pracy z dokumentami. Szczęśliwego kodowania!

## Co powinieneś się nauczyć dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Create HTML from String in C# – Custom Resource Handler Guide](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Create HTML Document with Aspose.HTML – Step‑by‑Step Guide](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}