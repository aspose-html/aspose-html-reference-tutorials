---
category: general
date: 2026-10-09
description: Naucz się ograniczać głębokość zagnieżdżonych zasobów przy użyciu Aspose.HTML
  ResourceHandlingOptions w Pythonie. Kontroluj max_handling_depth, aby zapewnić bezpieczną
  konwersję HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- limit nested resource depth
- Aspose.HTML ResourceHandlingOptions
- Python resource handling
- max_handling_depth
- nested HTML resources
language: pl
lastmod: 2026-10-09
og_description: Ogranicz głębokość zagnieżdżonych zasobów, używając Aspose.HTML ResourceHandlingOptions
  w Pythonie. Ustaw max_handling_depth, aby chronić swój proces konwersji HTML.
og_image_alt: Screenshot showing limit nested resource depth setting in Python
og_title: Jak ograniczyć głębokość zagnieżdżonych zasobów w Aspose.HTML w Pythonie
schemas:
- author: Aspose
  dateModified: '2026-10-09'
  description: Learn to limit nested resource depth using Aspose.HTML ResourceHandlingOptions
    in Python. Control max_handling_depth for safe HTML conversion.
  headline: How to limit nested resource depth with Aspose.HTML in Python
  type: TechArticle
- description: Learn to limit nested resource depth using Aspose.HTML ResourceHandlingOptions
    in Python. Control max_handling_depth for safe HTML conversion.
  name: How to limit nested resource depth with Aspose.HTML in Python
  steps:
  - name: What the setting does
    text: '- **Depth 0** – The root HTML document is processed, but no external resources
      are fetched. - **Depth 1** – Direct resources referenced by the root (e.g.,
      `<img src="...">`, `<link href="...">`) are fetched. - **Depth 2** – Resources
      referenced by the first‑level resources (e.g., CSS files that impo'
  - name: Using the options with a converter
    text: After configuring the depth limit, pass the `resource_options` object to
      the `HtmlConverter` (or any Aspose.HTML API that accepts `ResourceHandlingOptions`).
  - name: 1. Disabling depth limiting entirely
    text: Set the property to a very high number (e.g., `sys.maxsize`) or `None` if
      you want unrestricted handling. Use this only when you trust the source HTML.
  - name: 2. Handling missing resources
    text: When the depth limit stops a resource from being fetched, Aspose.HTML logs
      a warning but continues. You can capture these warnings by attaching a custom
      logger to the converter if you need audit trails.
  - name: 3. Combining with other resource options
    text: '`ResourceHandlingOptions` also offers `allow_external_resources`, `download_timeout`,
      and `max_resource_size`. Pairing a depth limit with a size limit provides a
      robust safety net.'
  - name: 4. Testing the limit
    text: Create a test HTML hierarchy with nested `<iframe>` tags or CSS `@import`
      statements to verify that your depth limit behaves as expected before deploying
      to production.
  type: HowTo
tags:
- Aspose.HTML
- Python
- HTML conversion
- Resource handling
title: Jak ograniczyć głębokość zagnieżdżonych zasobów w Aspose.HTML w Pythonie
url: /pl/python/general/how-to-limit-nested-resource-depth-with-aspose-html-in-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak ograniczyć głębokość zagnieżdżonych zasobów przy użyciu Aspose.HTML w Pythonie

Jeśli potrzebujesz **ograniczyć głębokość zagnieżdżonych zasobów** podczas konwertowania HTML przy użyciu Aspose.HTML, ten przewodnik pokaże Ci dokładnie, jak to zrobić w Pythonie. Kontrolowanie właściwości `max_handling_depth` zapobiega niekontrolowanej rekurencji, gdy strona zawiera głęboko zagnieżdżone zasoby, takie jak ramki lub powiązane arkusze stylów.

Dowiesz się również, dlaczego ustawienie limitu głębokości ma znaczenie, zobaczysz kompletny przykład kodu oraz odkryjesz typowe pułapki i wskazówki najlepszych praktyk. Nie jest wymagana żadna zewnętrzna dokumentacja — wszystko, czego potrzebujesz, znajduje się tutaj.

## Wymagania wstępne

- Zainstalowany Python 3.8 lub nowszy  
- Pakiet `aspose.html` (`pip install aspose-html`)  
- Podstawowa znajomość przepływu konwersji w Aspose.HTML  

Te elementy są jedynymi zależnościami dla poniższych przykładów.

## Krok 1: Importuj klasę **ResourceHandlingOptions**

Pierwszym krokiem jest wprowadzenie klasy `ResourceHandlingOptions` do Twojego skryptu. Klasa ta grupuje wszystkie opcje wpływające na sposób pobierania i przetwarzania zewnętrznych zasobów (obrazów, CSS, skryptów itp.) podczas konwersji.

```python
# Step 1: Import the ResourceHandlingOptions class
from aspose.html import ResourceHandlingOptions
```

**Dlaczego to jest ważne:**  
`ResourceHandlingOptions` izoluje ustawienia związane z zasobami od innych opcji konwersji, pozwalając precyzyjnie dostosować sposób obsługi zagnieżdżonych zasobów bez wpływu na renderowanie czy format wyjściowy.

## Krok 2: Utwórz instancję obiektu opcji

Zainicjuj `ResourceHandlingOptions`, aby móc modyfikować jego właściwości. Domyślna instancja zezwala na nieograniczone zagnieżdżanie, co może powodować problemy z wydajnością lub nawet przepełnienie stosu w przypadku złośliwie skonstruowanych stron.

```python
# Step 2: Create an instance of the options object
resource_options = ResourceHandlingOptions()
```

**Wskazówka:**  
Jeśli planujesz ponownie używać tego samego limitu głębokości w wielu konwersjach, przechowaj skonfigurowany obiekt w zmiennej na poziomie modułu, aby uniknąć jego tworzenia przy każdym wywołaniu.

## Krok 3: Ustaw **max_handling_depth**, aby ograniczyć głębokość zagnieżdżonych zasobów

Przypisz właściwość `max_handling_depth` do maksymalnej liczby poziomów zagnieżdżenia, które chcesz zezwolić. W tym przykładzie zatrzymujemy się po **3** poziomach, ale możesz wybrać dowolną liczbę całkowitą odpowiadającą Twojemu scenariuszowi.

```python
# Step 3: Limit the depth of nested resource handling (stop after 3 levels)
resource_options.max_handling_depth = 3
```

### Co robi to ustawienie

- **Depth 0** – Przetwarzany jest główny dokument HTML, ale żadne zewnętrzne zasoby nie są pobierane.  
- **Depth 1** – Bezpośrednie zasoby odwoływane przez główny dokument (np. `<img src="...">`, `<link href="...">`) są pobierane.  
- **Depth 2** – Zasoby odwoływane przez zasoby pierwszego poziomu (np. pliki CSS importujące inne CSS) są pobierane.  
- **Depth 3** – Proces zatrzymuje się po obsłużeniu zasobów trzeciego poziomu. Wszystkie dalsze zagnieżdżone odwołania są ignorowane.  

Ustawienie `max_handling_depth` chroni Twoją aplikację przed:

| Ryzyko | Jak limit pomaga |
|------|----------------------|
| **Nieskończona rekurencja** spowodowana odwołaniami cyklicznymi | Konwerter zatrzymuje się po osiągnięciu określonej głębokości, przerywając pętlę. |
| **Nadmierny ruch sieciowy** gdy strona ładuje dziesiątki powiązanych arkuszy stylów | Pobierane są tylko pierwsze kilka poziomów, co zmniejsza zużycie pasma. |
| **Wyciek pamięci** spowodowany ładowaniem ogromnych drzew zasobów | Tworzone jest mniej obiektów, co utrzymuje przewidywalne zużycie pamięci. |

### Używanie opcji z konwerterem

Po skonfigurowaniu limitu głębokości przekaż obiekt `resource_options` do `HtmlConverter` (lub dowolnego interfejsu API Aspose.HTML, który akceptuje `ResourceHandlingOptions`).

```python
from aspose.html import HtmlConverter, SaveFormat

# Create a converter with the resource handling options
converter = HtmlConverter(resource_options)

# Convert a sample HTML file to PDF while respecting the depth limit
converter.convert("sample.html", "output.pdf", SaveFormat.PDF)

print("Conversion completed with max_handling_depth =", resource_options.max_handling_depth)
```

**Oczekiwany wynik**

```
Conversion completed with max_handling_depth = 3
```

Jeśli źródłowy HTML zawiera zasoby poza trzecim poziomem, zostaną one pominięte w PDF, a konwersja nadal zakończy się szybko.

## Przypadki brzegowe i typowe wariacje

### 1. Wyłączenie limitu głębokości całkowicie

Ustaw właściwość na bardzo dużą liczbę (np. `sys.maxsize`) lub `None`, jeśli chcesz nieograniczoną obsługę. Używaj tego tylko wtedy, gdy masz zaufanie do źródłowego HTML.

```python
import sys
resource_options.max_handling_depth = sys.maxsize  # effectively unlimited
```

### 2. Obsługa brakujących zasobów

Gdy limit głębokości uniemożliwia pobranie zasobu, Aspose.HTML zapisuje ostrzeżenie, ale kontynuuje działanie. Możesz przechwycić te ostrzeżenia, podłączając własny logger do konwertera, jeśli potrzebujesz ścieżek audytu.

### 3. Łączenie z innymi opcjami zasobów

`ResourceHandlingOptions` oferuje również `allow_external_resources`, `download_timeout` oraz `max_resource_size`. Połączenie limitu głębokości z limitem rozmiaru zapewnia solidną ochronę.

```python
resource_options.allow_external_resources = True
resource_options.max_resource_size = 5 * 1024 * 1024  # 5 MiB per resource
```

### 4. Testowanie limitu

Utwórz testową hierarchię HTML z zagnieżdżonymi tagami `<iframe>` lub instrukcjami CSS `@import`, aby zweryfikować, że limit głębokości działa zgodnie z oczekiwaniami przed wdrożeniem do produkcji.

## Praktyczne wskazówki (E‑E‑A‑T)

- **Zweryfikuj adresy URL wejściowe** przed konwersją, aby uniknąć niepotrzebnych wywołań sieciowych.  
- **Zaloguj rzeczywistą osiągniętą głębokość** (`converter.handling_depth_reached`) w celu monitorowania.  
- **Ponownie używaj tego samego `ResourceHandlingOptions`** w wielu konwersjach, aby zachować spójną konfigurację.  
- **Profiluj wydajność** przy zmianie głębokości; niższy limit zazwyczaj przyspiesza konwersję, ale może pominąć potrzebne zasoby.  

## Zakończenie

Teraz wiesz, jak **ograniczyć głębokość zagnieżdżonych zasobów** podczas pracy z Aspose.HTML w Pythonie, konfigurując właściwość `max_handling_depth` w `ResourceHandlingOptions`. To pojedyncze ustawienie chroni Twój proces konwersji przed niekontrolowaną rekurencją, nadmiernym zużyciem sieci i nagłymi skokami pamięci, jednocześnie dając precyzyjną kontrolę nad tym, jak głęboko przetwarzane są drzewa zasobów.

Gotowy, aby dowiedzieć się więcej? Spróbuj połączyć limit głębokości z `max_resource_size`, aby stworzyć w pełni zabezpieczony przepływ konwersji HTML‑do‑PDF, lub przeczytaj nasz przewodnik o **obsłudze zasobów Aspose.HTML**, aby uzyskać głębsze informacje o `allow_external_resources` i zarządzaniu limitami czasu.

--- 

*Obraz ilustrujący ustawienie limitu głębokości (opcjonalnie):*  
![Zrzut ekranu pokazujący ustawienie limitu zagnieżdżonych zasobów w Pythonie](placeholder.png "limit głębokości zagnieżdżonych zasobów")


## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Niestandardowy obsługiwacz zasobów w Aspose HTML – przewodnik zapisu do strumienia](/html/english/net/advanced-features/custom-resource-handler-in-aspose-html-save-to-stream-guide/)
- [Jak zapisać HTML w C# – kompletny przewodnik z użyciem niestandardowego obsługiwacza zasobów](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Obsługa komunikatów i sieci w Aspose.HTML dla Javy](/html/english/java/message-handling-networking/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}