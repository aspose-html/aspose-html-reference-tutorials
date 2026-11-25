---
category: general
date: 2026-09-19
description: Dowiedz się, jak ograniczyć zagnieżdżone zasoby w Aspose.HTML dla Pythona
  przy użyciu ResourceHandlingOptions. Kontroluj maksymalną głębokość obsługi i unikaj
  nieskończonych pętli.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- limit nested resources
- resource handling options
- Aspose HTML Python
- max handling depth
- nested resource handling
language: pl
lastmod: 2026-09-19
og_description: Ogranicz zagnieżdżone zasoby w Aspose.HTML dla Pythona przy użyciu
  ResourceHandlingOptions. Ustaw maksymalną głębokość obsługi, aby zapobiec głębokiej
  rekurencji i poprawić wydajność.
og_image_alt: Screenshot of Python code that limits nested resources with Aspose.HTML
og_title: Jak ograniczyć zagnieżdżone zasoby w Aspose.HTML dla Pythona – przewodnik
  krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-09-19'
  description: Learn how to limit nested resources in Aspose.HTML for Python using
    ResourceHandlingOptions. Control max handling depth and avoid infinite loops.
  headline: How to limit nested resources when processing HTML with Aspose.HTML for
    Python
  type: TechArticle
- description: Learn how to limit nested resources in Aspose.HTML for Python using
    ResourceHandlingOptions. Control max handling depth and avoid infinite loops.
  name: How to limit nested resources when processing HTML with Aspose.HTML for Python
  steps:
  - name: Explanation of each step
    text: 1. **Install the package** – The `aspose-html` wheel is required. The `pip
      install` command is shown as a comment for completeness. 2. **Import classes**
      – `HtmlDocument` loads the page, `ResourceHandlingOptions` holds the limit,
      and `HtmlLoadOptions` ties the two together. 3. **Create the options o
  - name: Changing the depth limit
    text: 'You might need a deeper or shallower limit based on your environment:'
  - name: Disabling the limit completely
    text: 'Setting the property to `0` tells Aspose.HTML to **remove any depth restriction**:'
  - name: Handling circular references
    text: 'Even with a depth limit, circular references can still appear at the same
      level. Aspose.HTML detects cycles and stops loading a resource that has already
      been processed, regardless of the depth setting. However, setting a lower `max_handling_depth`
      reduces the chance of hitting a cycle in the first '
  - name: Using the limit with local files
    text: 'The same approach works for local HTML files:'
  - name: Integrating with other Aspose.HTML features
    text: 'If you also need to control **resource download timeout**, you can combine
      `ResourceHandlingOptions` with `NetworkOptions`:'
  type: HowTo
tags:
- Aspose
- Python
- HTML processing
- Resource management
title: Jak ograniczyć zagnieżdżone zasoby podczas przetwarzania HTML przy użyciu Aspose.HTML
  dla Pythona
url: /pl/python/general/how-to-limit-nested-resources-when-processing-html-with-aspo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak ograniczyć zagnieżdżone zasoby podczas przetwarzania HTML przy użyciu Aspose.HTML dla Pythona

Jeśli potrzebujesz **ograniczyć zagnieżdżone zasoby** podczas renderowania lub konwertowania HTML, ten przewodnik pokaże Ci dokładne kroki konfiguracyjne Aspose.HTML dla Pythona. Kontrolowanie głębokości obsługi zasobów zapobiega niekontrolowanej rekurencji, gdy strona zawiera wiele warstw odwołań do CSS, JavaScript lub obrazów.

Ograniczanie zagnieżdżonych zasobów jest szczególnie ważne dla dużych crawlerów, potoków renderowania e‑maili lub dowolnych zautomatyzowanych przepływów pracy, które muszą mieścić się w określonych limitach pamięci i czasu. W kolejnych sekcjach dowiesz się, dlaczego warto ustawić limit głębokości, jak używać klasy `ResourceHandlingOptions` oraz jak zweryfikować, że limit działa zgodnie z oczekiwaniami.

## Dlaczego warto ograniczyć zagnieżdżone zasoby

Dokumenty HTML często odwołują się do innych zasobów — arkuszy stylów, skryptów, obrazów, czcionek czy nawet innych plików HTML. Każdy z tych zasobów może z kolei odwoływać się do kolejnych plików, tworząc drzewo zależności. Bez zabezpieczenia drzewo może stać się dowolnie głębokie:

* Strona ładuje plik CSS, który importuje kolejny plik CSS, który znowu importuje kolejny i tak dalej.
* JavaScript może dynamicznie ładować dodatkowe skrypty.
* Szablon e‑maila może osadzać obrazy, które odwołują się do zewnętrznych URL‑ów przekierowujących do kolejnych zasobów.

Gdy głębokość rekurencji rośnie niekontrolowanie, ryzykujesz:

* **Nadmierne zużycie pamięci** – każdy pobrany zasób zajmuje bufor.
* **Dłuższy czas przetwarzania** – opóźnienia sieciowe mnożą się z każdym poziomem.
* **Potencjalne pętle nieskończone** – odwołania cykliczne mogą spowodować, że silnik nigdy nie zakończy działania.

Ustawienie **maksymalnej głębokości obsługi** mówi Aspose.HTML, aby przestał podążać za linkami zasobów po określonej liczbie poziomów, zapewniając przewidywalną wydajność.

## Jak ograniczyć zagnieżdżone zasoby w Aspose.HTML dla Pythona

Aspose.HTML udostępnia klasę `ResourceHandlingOptions`, która zawiera właściwość `max_handling_depth`. Przypisując jej wartość liczbową (np. `3`), instruujesz silnik, aby zatrzymał się po trzech poziomach zagnieżdżenia.

Poniżej znajduje się kompletny, gotowy do uruchomienia przykład, który demonstruje cały przepływ pracy:

```python
# ---------------------------------------------------------
# Step 0: Install the Aspose.HTML package (if not already)
# ---------------------------------------------------------
# pip install aspose-html

# ---------------------------------------------------------
# Step 1: Import the required classes
# ---------------------------------------------------------
from aspose.html import HtmlDocument, ResourceHandlingOptions, HtmlLoadOptions

# ---------------------------------------------------------
# Step 2: Create a ResourceHandlingOptions instance
# ---------------------------------------------------------
resource_options = ResourceHandlingOptions()
# Limit the handling depth to three levels of nested resources
resource_options.max_handling_depth = 3

# ---------------------------------------------------------
# Step 3: Attach the options to the HTML load configuration
# ---------------------------------------------------------
load_options = HtmlLoadOptions()
load_options.resource_handling_options = resource_options

# ---------------------------------------------------------
# Step 4: Load an HTML page using the configured options
# ---------------------------------------------------------
# Replace the URL with any page that has deep resource nesting
html_url = "https://example.com/deep-nested.html"
document = HtmlDocument(html_url, load_options)

# ---------------------------------------------------------
# Step 5: Verify the depth limit worked
# ---------------------------------------------------------
# The Document object exposes a collection of loaded resources.
# We'll print the total number of resources and the deepest level reached.
print(f"Total resources loaded: {len(document.resources)}")
deepest_level = max((res.depth for res in document.resources), default=0)
print(f"Deepest resource level: {deepest_level}")

# ---------------------------------------------------------
# Step 6: (Optional) Save the processed HTML to disk
# ---------------------------------------------------------
output_path = "output_limited.html"
document.save(output_path)
print(f"Processed HTML saved to {output_path}")
```

### Wyjaśnienie poszczególnych kroków

1. **Instalacja pakietu** – Koło `aspose-html` jest wymagane. Komenda `pip install` jest podana jako komentarz dla pełności.
2. **Import klas** – `HtmlDocument` ładuje stronę, `ResourceHandlingOptions` przechowuje limit, a `HtmlLoadOptions` łączy je ze sobą.
3. **Utworzenie obiektu opcji** – Instancja `ResourceHandlingOptions` daje Ci mutowalny kontener.
4. **Ustawienie `max_handling_depth`** – Przypisz `3` (lub dowolną liczbę całkowitą), aby ograniczyć silnik do trzech poziomów zagnieżdżonych zasobów. To jest sedno **ograniczania zagnieżdżonych zasobów**.
5. **Dołączenie opcji do konfiguracji ładowania** – `HtmlLoadOptions` pozwala przekazać `resource_options` do loadera.
6. **Załadowanie HTML** – Konstruktor `HtmlDocument` przyjmuje URL lub ścieżkę do pliku wraz z `load_options`. Silnik teraz respektuje limit głębokości.
7. **Weryfikacja** – Iterując po `document.resources`, możesz zobaczyć, ile zasobów faktycznie pobrano oraz jak głęboki poziom został osiągnięty. Jeśli najgłębszy poziom wynosi `3` lub mniej, limit się powiódł.
8. **Zapis** – Zapisz przetworzony dokument. Zapisany plik zawiera jedynie zasoby do dozwolonej głębokości.

#### Oczekiwany wynik

```
Total resources loaded: 12
Deepest resource level: 3
Processed HTML saved to output_limited.html
```

Liczby będą się różnić w zależności od źródłowej strony, ale najgłębszy poziom nigdy nie powinien przekroczyć `3`, ponieważ ustawiliśmy `max_handling_depth = 3`.

## Typowe wariacje i przypadki brzegowe

### Zmiana limitu głębokości

Możesz potrzebować głębszego lub płytszego limitu w zależności od środowiska:

```python
resource_options.max_handling_depth = 1   # Only top‑level resources (e.g., images directly referenced)
resource_options.max_handling_depth = 5   # Allow deeper CSS imports but still guard against runaway recursion
```

### Wyłączenie limitu całkowicie

Ustawienie właściwości na `0` mówi Aspose.HTML, aby **usunął wszelkie ograniczenia głębokości**:

```python
resource_options.max_handling_depth = 0   # No limit – use with caution
```

Rób to tylko wtedy, gdy masz pewność, że źródłowy HTML jest dobrze zachowującym się.

### Obsługa odwołań cyklicznych

Nawet przy limicie głębokości odwołania cykliczne mogą pojawić się na tym samym poziomie. Aspose.HTML wykrywa cykle i przestaje ładować zasób, który już został przetworzony, niezależnie od ustawienia głębokości. Jednak ustawienie niższego `max_handling_depth` zmniejsza szansę na napotkanie cyklu w pierwszej kolejności.

### Użycie limitu z plikami lokalnymi

To samo podejście działa dla lokalnych plików HTML:

```python
document = HtmlDocument("C:/myproject/templates/email.html", load_options)
```

Silnik traktuje względne atrybuty `href` lub `src` tak samo jak zdalne URL‑e, stosując limit głębokości również do zasobów systemu plików.

### Integracja z innymi funkcjami Aspose.HTML

Jeśli potrzebujesz także kontrolować **czas oczekiwania na pobranie zasobu**, możesz połączyć `ResourceHandlingOptions` z `NetworkOptions`:

```python
from aspose.html import NetworkOptions

network_opts = NetworkOptions()
network_opts.timeout = 5000   # milliseconds
load_options.network_options = network_opts
```

Obie opcje są niezależne, więc możesz jednocześnie precyzyjnie dostroić wydajność i bezpieczeństwo.

## Profesjonalne wskazówki dla środowisk produkcyjnych

* **Loguj drzewo zasobów** – Podczas debugowania iteruj po `document.resources` i loguj URL oraz poziom każdego zasobu. To pomaga zrozumieć, dlaczego dana strona przekracza Twoje oczekiwania.
* **Cache’uj pobrane zasoby** – Jeśli przetwarzasz te same zewnętrzne zasoby wielokrotnie, włącz cache, aby uniknąć zbędnych wywołań sieciowych.
* **Połącz z białą listą** – Jeśli zaufane są tylko określone domeny, przefiltruj `document.resources` po załadowaniu i odrzuć te, które nie znajdują się na białej liście.
* **Testuj na stronach brzegowych** – Stwórz syntetyczny plik HTML, który importuje łańcuch 10 plików CSS. Zweryfikuj, że Twój limit przycina łańcuch zgodnie z zamierzeniami.

## Podsumowanie

Wiesz już, jak **ograniczyć zagnieżdżone zasoby** w Aspose.HTML dla Pythona, konfigurując `ResourceHandlingOptions.max_handling_depth`. Ustawienie limitu głębokości chroni Twoją aplikację przed nadmiernym zużyciem pamięci, długim czasem przetwarzania i potencjalnymi pętlami nieskończonymi wywołanymi przez głęboko zagnieżdżone lub cykliczne odwołania zasobów.

Od tego momentu możesz:

* Dostosować głębokość do swojego budżetu wydajności (`resource_handling_options.max_handling_depth`).
* Połączyć limit z timeoutami sieciowymi, cache’owaniem lub białymi listami domen, aby uzyskać solidne potoki.
* Zgłębiać pokrewne tematy, takie jak **resource handling options**, **max handling depth** i **nested resource handling**, aby jeszcze lepiej kontrolować przetwarzanie HTML.

Eksperymentuj z różnymi wartościami głębokości i obserwuj, jak zmienia się liczba załadowanych zasobów. Gdy będziesz gotowy, włącz ten wzorzec do większej usługi konwersji lub renderowania HTML, aby zapewnić przewidywalne, bezpieczne i wydajne działanie.

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz szczegółowe wyjaśnienia krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Message Handling and Networking in Aspose.HTML for Java](/html/english/java/message-handling-networking/)
- [Custom Schema Filter and Message Handling in Aspose.HTML for Java](/html/english/java/custom-schema-message-handling/)
- [Data Handling and Stream Management in Aspose.HTML for Java](/html/english/java/data-handling-stream-management/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}