---
category: general
date: 2026-10-15
description: Dowiedz się, jak tworzyć opcje obsługi zasobów i jak ustawić maksymalną
  głębokość obsługi przy zapisywaniu Markdown w Pythonie. Postępuj zgodnie z przewodnikiem
  krok po kroku.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to set max handling depth
language: pl
lastmod: 2026-10-15
og_description: Utwórz opcje obsługi zasobów w Pythonie, aby kontrolować przetwarzanie
  zagnieżdżonych zasobów. Ten samouczek pokazuje, jak ustawić maksymalną głębokość
  obsługi dla niezawodnego eksportu do Markdown.
og_image_alt: Screenshot showing Python code to create resource handling options and
  set max handling depth
og_title: Utwórz opcje zarządzania zasobami – przewodnik Pythona
schemas:
- author: Aspose
  dateModified: '2026-10-15'
  description: Learn how to create resource handling options and how to set max handling
    depth for Markdown saving in Python. Follow a step‑by‑step guide.
  headline: How to create resource handling options with Python
  type: TechArticle
tags:
- resource handling
- Markdown
- Python
- options
title: Jak stworzyć opcje obsługi zasobów w Pythonie
url: /pl/python/general/how-to-create-resource-handling-options-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak utworzyć opcje obsługi zasobów w Pythonie

Jeśli potrzebujesz **utworzyć opcje obsługi zasobów** dla eksportu Markdown, ten przewodnik zapewnia pełne rozwiązanie. Zobaczysz dokładnie **jak ustawić maksymalną głębokość obsługi**, aby zagnieżdżone zasoby przestały być przetwarzane po osiągnięciu określonego poziomu.

Obsługa zasobów jest niezbędna, gdy generujesz Markdown z złożonych dokumentów zawierających obrazy, osadzone pliki lub inne powiązane zasoby. Nieograniczona rekurencja może prowadzić do problemów z wydajnością lub błędów braku pamięci. Konfigurując głębokość obsługi, utrzymujesz proces przewidywalnym i efektywnym.

W tym samouczku:

* Zainicjalizujesz obiekt `ResourceHandlingOptions`.
* Skonfigurujesz maksymalną głębokość obsługi.
* Dołączysz opcje do instancji `MarkdownSaveOptions`.
* Uruchomisz pełny przykład, który możesz skopiować do swojego projektu.

Nie są wymagane żadne zewnętrzne biblioteki poza standardowym SDK, a kod działa z najnowszą wersją pakietu Python od października 2026.

## Prerequisites

Zanim rozpoczniesz, upewnij się, że masz:

* Python 3.9 lub nowszy zainstalowany.
* SDK dostarczające `ResourceHandlingOptions` i `MarkdownSaveOptions` (np. `groupdocs-viewer` lub podobny pakiet). Zainstaluj go za pomocą:

```bash
pip install groupdocs-viewer
```

* Podstawową znajomość klas Pythona i atrybutów obiektów.

## Step 1: Create resource handling options

Pierwszym krokiem jest **utworzenie opcji obsługi zasobów**. Ten obiekt działa jako kontener dla wszystkich ustawień związanych z zasobami.

```python
from groupdocs.viewer import ResourceHandlingOptions, MarkdownSaveOptions

# Step 1: Instantiate the options object
resource_options = ResourceHandlingOptions()
```

`ResourceHandlingOptions` nie nakłada żadnych limitów domyślnie, co oznacza, że przeglądarka będzie podążać za każdym napotkanym powiązanym zasobem. Inicjalizacja obiektu daje czystą bazę do zastosowania precyzyjnych kontroli.

## Step 2: How to set max handling depth

Teraz dowiesz się **jak ustawić maksymalną głębokość obsługi**. Właściwość `max_handling_depth` określa liczbę zagnieżdżonych poziomów, które eksporter przetworzy przed zatrzymaniem się.

```python
# Step 2: Limit the handling depth to five levels
resource_options.max_handling_depth = 5
```

Dlaczego warto ograniczyć głębokość? Wyobraź sobie dokument Markdown, który odwołuje się do innego pliku Markdown, który z kolei odwołuje się do trzeciego pliku i tak dalej. Bez limitu głębokości eksporter mógłby rekurencyjnie przetwarzać nieskończenie, zużywając pamięć i CPU. Ustawienie `max_handling_depth` na `5` mówi silnikowi, aby zatrzymał się po pięciu zagnieżdżonych zasobach, co jest bezpiecznym domyślnym ustawieniem dla większości projektów.

### Edge case: unlimited depth

Jeśli celowo potrzebujesz nieograniczonej rekurencji (rzadko w środowisku produkcyjnym), ustaw wartość na `None`:

```python
resource_options.max_handling_depth = None  # No limit
```

Pamiętaj, że nieograniczona głębokość może powodować degradację wydajności przy bardzo dużych drzewach dokumentów.

## Step 3: Attach the options to MarkdownSaveOptions

Po skonfigurowaniu obsługi zasobów musisz dołączyć opcje do instancji `MarkdownSaveOptions`. To informuje eksporter, aby używał tych ustawień przy zapisie.

```python
# Step 3: Create MarkdownSaveOptions and attach the resource handling config
markdown_options = MarkdownSaveOptions()
markdown_options.resource_handling_options = resource_options
```

`MarkdownSaveOptions` agreguje wszystkie ustawienia związane z eksportem. Przypisując `resource_options` do atrybutu `resource_handling_options`, zapewniasz, że limit głębokości będzie egzekwowany podczas konwersji.

## Step 4: Run a complete conversion (optional demo)

Poniższy fragment kodu demonstruje pełną konwersję przykładowego dokumentu do Markdown przy użyciu właśnie utworzonych opcji. Dostosuj ścieżki plików do swojego środowiska.

```python
from groupdocs.viewer import Viewer

# Path to the source document (e.g., a DOCX with embedded images)
source_path = "sample.docx"
# Path where the Markdown output will be saved
output_path = "output.md"

# Initialize the viewer with the source file
viewer = Viewer(source_path)

# Perform the conversion using the configured options
viewer.save(output_path, markdown_options)

print(f"Conversion complete. Markdown saved to {output_path}")
```

**Expected output**

```
Conversion complete. Markdown saved to output.md
```

Po uruchomieniu skryptu otwórz `output.md`. Zobaczysz, że obrazy i inne zasoby są odwoływane do pięciu poziomów głębokości; wszelkie dalsze linki są pomijane, co zapobiega niekontrolowanej rekurencji.

## Pro tip: verify the handling depth at runtime

Jeśli potrzebujesz potwierdzić, że limit głębokości został zastosowany, możesz sprawdzić wygenerowany Markdown pod kątem brakujących odwołań do zasobów lub włączyć szczegółowe logowanie w SDK:

```python
viewer.set_logging(True)  # Enable detailed logs
```

Log pokaże komunikaty takie jak:

```
[INFO] Resource handling stopped at depth 5 for file 'nested_image.png'
```

## Common questions

**Co jeśli mój dokument ma mniej niż pięć zagnieżdżonych zasobów?**  
Eksporter przetworzy wszystkie dostępne zasoby, ponieważ limit głębokości jest wyższy niż rzeczywista głębokość. Żadne zasoby nie zostaną obcięte.

**Czy mogę ustawić inny limit dla różnych typów plików?**  
Tak. Utwórz osobne obiekty `ResourceHandlingOptions` dla każdego formatu eksportu i przypisz je do odpowiedniej instancji `SaveOptions`.

**Czy limit głębokości dotyczy tylko obrazów?**  
Nie. Limit ma zastosowanie do *wszystkich* zasobów, które eksporter może podążać, w tym osadzonych plików, hiperłączy i zagnieżdżonych dołączonych plików Markdown.

## Conclusion

Teraz wiesz, jak **utworzyć opcje obsługi zasobów** i **ustawić maksymalną głębokość obsługi** dla niezawodnych eksportów Markdown w Pythonie. Ograniczając rekurencję, chronisz aplikację przed nadmiernym zużyciem pamięci, jednocześnie zachowując niezbędną hierarchię treści.

Kolejne kroki, które możesz rozważyć:

* Dostosuj inne właściwości `ResourceHandlingOptions`, takie jak `extract_images` lub `preserve_links`.
* Połącz obsługę zasobów z własnymi konwencjami nazewnictwa dla wyodrębnionych plików.
* Eksperymentuj z różnymi wartościami głębokości, aby znaleźć optymalne ustawienie dla swoich zestawów dokumentów.

Śmiało dostosowuj fragmenty kodu do własnego przepływu pracy i dziel się swoimi odkryciami ze społecznością. Szczęśliwego kodowania!

## What Should You Learn Next?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każde z nich zawiera kompletne, działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Zip HTML in C# – Custom Resource Handler Tutorial](/html/english/net/html-extensions-and-conversions/how-to-zip-html-in-c-custom-resource-handler-tutorial/)
- [How to create custom schema handler with Aspose.HTML for Java](/html/english/java/custom-schema-message-handling/custom-schema-message-handler/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}