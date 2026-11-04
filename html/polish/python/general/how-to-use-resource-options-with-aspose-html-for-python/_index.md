---
category: general
date: 2026-08-09
description: Jak korzystać z opcji obsługi zasobów w Aspose.HTML dla Pythona. Dowiedz
  się, jak ustawić maksymalną głębokość obsługi i efektywnie ładować duże strony HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use resource
- resource handling options
- max handling depth
- Aspose.HTML for Python
- HTMLDocument loading
language: pl
lastmod: 2026-08-09
og_description: Jak korzystać z opcji obsługi zasobów w Aspose.HTML dla Pythona. Ten
  samouczek przeprowadzi Cię przez konfigurowanie maksymalnej głębokości obsługi oraz
  bezpieczne ładowanie dużych plików HTML.
og_image_alt: Diagram illustrating how to use resource handling options in Aspose.HTML
  for Python
og_title: Jak korzystać z opcji zasobów w Aspose.HTML dla Pythona – kompletny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-08-09'
  description: How to use resource handling options in Aspose.HTML for Python. Learn
    to set max handling depth and load large HTML pages efficiently.
  headline: How to use resource options with Aspose.HTML for Python
  type: TechArticle
- description: How to use resource handling options in Aspose.HTML for Python. Learn
    to set max handling depth and load large HTML pages efficiently.
  name: How to use resource options with Aspose.HTML for Python
  steps:
  - name: Import the required classes
    text: '```python from aspose.html import HTMLDocument, ResourceHandlingOptions
      ```'
  - name: Create a `ResourceHandlingOptions` object
    text: '```python # Step 2: Instantiate the options container resource_options
      = ResourceHandlingOptions() ```'
  - name: Set the maximum handling depth
    text: '```python # Step 3: Limit recursion to 5 levels of nested resources resource_options.max_handling_depth
      = 5 ```'
  - name: Load the HTML document with the configured options
    text: '```python # Step 4: Load the document using the options we just configured
      doc = HTMLDocument("YOUR_DIRECTORY/bigpage.html", resource_options) ```'
  - name: Verify that the document loaded correctly
    text: '```python # Step 5: Simple sanity check – print the document title print("Document
      title:", doc.title) ```'
  - name: Optional – handle missing resources gracefully
    text: '```python # Step 6: Attach an event handler to log missing resources def
      on_resource_not_found(sender, args): print(f"Resource not found: {args.resource_url}")'
  - name: Clean up
    text: '```python # Step 7: Release native resources when done doc.dispose() ```'
  - name: Pro tip
    text: When processing many HTML files in a batch, reuse a single `ResourceHandlingOptions`
      instance. Creating it once reduces object‑allocation overhead and guarantees
      consistent settings across all documents.
  type: HowTo
tags:
- Aspose.HTML
- Python
- HTML processing
- resource handling
title: Jak używać opcji zasobów w Aspose.HTML dla Pythona
url: /pl/python/general/how-to-use-resource-options-with-aspose-html-for-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać opcji zasobów z Aspose.HTML dla Pythona

Jeśli zastanawiasz się **jak używać opcji obsługi zasobów** z Aspose.HTML dla Pythona, ten samouczek dostarcza kompletną, gotową do uruchomienia rozwiązanie. Nauczysz się konfigurować `ResourceHandlingOptions`, ograniczać maksymalną głębokość obsługi oraz ładować dużą stronę HTML bez wyczerpywania pamięci.

Przetwarzanie złożonych stron internetowych często pobiera wiele zagnieżdżonych zasobów — arkuszy stylów, obrazów, skryptów i iframe‑ów. Bez odpowiednich limitów ładowarka może rekurencyjnie działać w nieskończoność, co prowadzi do problemów z wydajnością lub awarii. Po zakończeniu tego przewodnika będziesz w stanie:

* Utworzyć instancję `ResourceHandlingOptions`.
* Ustawić `max_handling_depth` na bezpieczną wartość.
* Załadować `HTMLDocument` z tymi opcjami.
* Obsłużyć typowe przypadki brzegowe, takie jak brakujące zasoby lub głębsze zagnieżdżenie.

Do działania nie są potrzebne żadne zewnętrzne narzędzia poza biblioteką Aspose.HTML dla Pythona oraz standardowym środowiskiem Python 3.

## Wymagania wstępne

* Zainstalowany Python 3.8 lub nowszy.
* Pakiet Aspose.HTML dla Pythona (`aspose-html`) zainstalowany (`pip install aspose-html`).
* Przykładowy plik HTML (np. `bigpage.html`) zawierający zagnieżdżone zasoby.
* Podstawowa znajomość składni Pythona i programowania obiektowego.

## Jak używać opcji obsługi zasobów – krok po kroku

Poniższe sekcje dzielą implementację na odrębne, wielokrotnego użytku kroki. Każdy krok zawiera **dlaczego** dany kod jest potrzebny oraz pełny fragment kodu, który możesz skopiować do swojego projektu.

### Krok 1: Importuj wymagane klasy

```python
from aspose.html import HTMLDocument, ResourceHandlingOptions
```

**Dlaczego to jest ważne:**  
`HTMLDocument` jest punktem wejścia do ładowania i manipulacji treścią HTML. `ResourceHandlingOptions` pozwala kontrolować, jak zewnętrzne zasoby są pobierane, buforowane lub ignorowane. Importowanie ich na początku utrzymuje skrypt w porządku i jest zgodne z najlepszymi praktykami Pythona.

### Krok 2: Utwórz obiekt `ResourceHandlingOptions`

```python
# Step 2: Instantiate the options container
resource_options = ResourceHandlingOptions()
```

**Dlaczego to jest ważne:**  
Obiekt opcji działa jak torba konfiguracyjna. Możesz później podłączyć go do konstruktora `HTMLDocument`, aby każde żądanie zasobu respektowało zdefiniowane przez Ciebie ustawienia.

### Krok 3: Ustaw maksymalną głębokość obsługi

```python
# Step 3: Limit recursion to 5 levels of nested resources
resource_options.max_handling_depth = 5
```

**Dlaczego to jest ważne:**  
`max_handling_depth` zapobiega nieskończonej rekurencji, gdy strona osadza zasoby, które z kolei osadzają kolejne zasoby. Ustawienie na **5** jest bezpiecznym domyślnym dla większości rzeczywistych stron, ale możesz dostosować wartość w zależności od scenariusza. Jeśli ustawisz głębokość na **0**, ładowarka pominie wszystkie zewnętrzne zasoby, co może być przydatne przy ekstrakcji czystego tekstu.

### Krok 4: Załaduj dokument HTML z skonfigurowanymi opcjami

```python
# Step 4: Load the document using the options we just configured
doc = HTMLDocument("YOUR_DIRECTORY/bigpage.html", resource_options)
```

**Dlaczego to jest ważne:**  
Przekazanie `resource_options` do konstruktora `HTMLDocument` informuje bibliotekę, aby respektowała ustawiony `max_handling_depth`. Dokument jest teraz w pełni sparsowany, a wszystkie zasoby poza piątym poziomem są ignorowane, co utrzymuje przewidywalne zużycie pamięci.

### Krok 5: Zweryfikuj, czy dokument został poprawnie załadowany

```python
# Step 5: Simple sanity check – print the document title
print("Document title:", doc.title)
```

**Dlaczego to jest ważne:**  
Szybka kontrola potwierdza, że HTML został sparsowany bez krytycznych błędów. Jeśli tytuł zostanie wydrukowany jako `None`, plik może być brakujący lub niepoprawny, i powinieneś obsłużyć wyjątek (zobacz sekcję „Obsługa błędów” poniżej).

### Krok 6: Opcjonalnie – obsłuż brakujące zasoby w sposób elegancki

```python
# Step 6: Attach an event handler to log missing resources
def on_resource_not_found(sender, args):
    print(f"Resource not found: {args.resource_url}")

resource_options.resource_not_found += on_resource_not_found
```

**Dlaczego to jest ważne:**  
Aspose.HTML wywołuje zdarzenie `resource_not_found`, gdy nie można pobrać powiązanego zasobu. Logowanie tych zdarzeń pomaga diagnozować zepsute linki lub zdecydować, czy zapewnić alternatywy.

### Krok 7: Sprzątanie

```python
# Step 7: Release native resources when done
doc.dispose()
```

**Dlaczego to jest ważne:**  
`HTMLDocument` posiada niezarządzane zasoby (np. natywne bufory pamięci). Jawne zwolnienie obiektu zwalnia te zasoby natychmiast, co jest szczególnie ważne w długotrwałych usługach lub zadaniach wsadowych.

## Pełny, uruchamialny przykład

Poniżej znajduje się kompletny skrypt, który zawiera wszystkie powyższe kroki. Zastąp `"YOUR_DIRECTORY/bigpage.html"` rzeczywistą ścieżką do swojego pliku HTML.

```python
# ------------------------------------------------------------
# Complete example: how to use resource handling options
# with Aspose.HTML for Python
# ------------------------------------------------------------

from aspose.html import HTMLDocument, ResourceHandlingOptions

# 1️⃣ Create and configure the options
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 5  # stop after 5 levels

# 2️⃣ Optional: log missing resources
def on_resource_not_found(sender, args):
    print(f"[WARN] Missing resource: {args.resource_url}")

resource_options.resource_not_found += on_resource_not_found

# 3️⃣ Load the document using the configured options
doc_path = "YOUR_DIRECTORY/bigpage.html"
doc = HTMLDocument(doc_path, resource_options)

# 4️⃣ Verify load
print("Document title:", doc.title)

# 5️⃣ Perform any additional processing here
#    (e.g., extract text, manipulate DOM, render to PDF, etc.)

# 6️⃣ Clean up
doc.dispose()
```

**Oczekiwany wynik (zakładając, że HTML zawiera tag `<title>`):**

```
Document title: Sample Big Page
```

Jeśli jakiekolwiek zasoby są brakujące, zobaczysz linie ostrzeżeń, takie jak:

```
[WARN] Missing resource: https://example.com/missing-image.png
```

## Przypadki brzegowe i wskazówki najlepszych praktyk

| Sytuacja | Zalecane postępowanie |
|-----------|----------------------|
| **Wymagana głębokość większa niż 5** | Zwiększ `max_handling_depth` do wymaganego poziomu, ale monitoruj zużycie pamięci przy pomocy profilera. |
| **Cykliczne odwołania do zasobów** | Limit głębokości automatycznie przerywa cykle; możesz także ustawić `resource_options.enable_circular_reference_detection = True`, jeśli wersja API to obsługuje. |
| **Duże zasoby binarne (np. obrazy wysokiej rozdzielczości)** | Użyj `resource_options.max_resource_size`, aby ograniczyć rozmiar każdego pobranego zasobu. |
| **Timeouty sieciowe** | Skonfiguruj `resource_options.request_timeout` (w sekundach), aby uniknąć zawieszania przy wolnych serwerach. |
| **Uruchamianie w środowisku ograniczonym (brak internetu)** | Ustaw `resource_options.enable_external_resources = False`, aby pominąć wszystkie zdalne pobrania. |

### Porada pro

Podczas przetwarzania wielu plików HTML w partii, ponownie używaj jednej instancji `ResourceHandlingOptions`. Utworzenie jej raz zmniejsza narzut alokacji obiektów i zapewnia spójne ustawienia we wszystkich dokumentach.

## Częste pytania

**P: Czy `max_handling_depth` wpływa na zasoby inline (np. tagi `<style>`)?**  
O: Nie. Zasoby inline są częścią oryginalnego HTML i zawsze są przetwarzane. Limit głębokości dotyczy wyłącznie zewnętrznych zasobów, które wymagają dodatkowych żądań HTTP.

**

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Add Handler with Aspose.HTML for Java](/html/english/java/message-handling-networking/custom-message-handler/)
- [Data Handling and Stream Management in Aspose.HTML for Java](/html/english/java/data-handling-stream-management/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}