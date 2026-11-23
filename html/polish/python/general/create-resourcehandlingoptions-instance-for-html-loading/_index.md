---
category: general
date: 2026-05-31
description: Utwórz instancję ResourceHandlingOptions, aby kontrolować ładowanie zasobów
  HTML. Dowiedz się, jak ograniczyć głębokość zasobów i wczytać HTMLDocument z własnymi
  opcjami.
draft: false
keywords:
- create resourcehandlingoptions instance
- limit resource depth
- HTMLDocument options
- resource loading configuration
- python html parsing
language: pl
og_description: Utwórz instancję ResourceHandlingOptions, aby kontrolować ładowanie
  zasobów HTML. Ten przewodnik pokazuje, jak ustawić maksymalną głębokość obsługi
  i załadować HTMLDocument z niestandardowymi opcjami.
og_title: Utwórz instancję ResourceHandlingOptions dla ładowania HTML
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create ResourceHandlingOptions instance to control HTML resource loading.
    Learn how to limit resource depth and load an HTMLDocument with custom options.
  headline: Create ResourceHandlingOptions Instance for HTML Loading
  type: TechArticle
tags:
- Python
- HTML parsing
- Resource handling
title: Utwórz instancję ResourceHandlingOptions do ładowania HTML
url: /pl/python/general/create-resourcehandlingoptions-instance-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz instancję ResourceHandlingOptions dla ładowania HTML

Zastanawiałeś się kiedyś, jak **utworzyć instancję ResourceHandlingOptions**, aby zapobiec wybuchowi parsera przy przetwarzaniu gigantycznej strony HTML? Nie jesteś jedyny — duże dokumenty z zagnieżdżonymi skryptami, ramkami lub włączonymi plikami mogą szybko zamienić prostą ekstrakcję w koszmar.  

W tym samouczku przeprowadzimy Cię przez dokładne kroki, aby utworzyć obiekt `ResourceHandlingOptions`, ograniczyć poziom zagnieżdżenia i przekazać go do `HTMLDocument`. Po zakończeniu będziesz mieć czysty, powtarzalny wzorzec **konfiguracji ładowania zasobów**, który działa z dowolnym, ogromnym plikiem HTML.

## Czego się nauczysz

- Dlaczego instancja `ResourceHandlingOptions` ma znaczenie przy parsowaniu ogromnych stron.  
- Jak **ograniczyć głębokość zasobów**, aby uniknąć nieskończonej rekurencji.  
- Dokładna składnia ładowania `HTMLDocument` z własnymi opcjami.  
- Pełny, gotowy do uruchomienia przykład, który możesz od razu dodać do swojego projektu.  

**Wymagania wstępne:** Python 3.8+, biblioteka `htmlparser` dostarczająca `HTMLDocument` i `ResourceHandlingOptions`. Nie są wymagane inne zależności.

---

## Krok 1: Utwórz instancję ResourceHandlingOptions

Pierwszą rzeczą, której potrzebujesz, jest nowy obiekt `ResourceHandlingOptions`. Traktuj go jak panel sterowania dla każdego zewnętrznego zasobu, na który może natrafić parser — skrypty, obrazy, iframe'y, cokolwiek.

```python
# Step 1: Initialize the options object
options = ResourceHandlingOptions()
```

> **Dlaczego to ważne:** Bez wyraźnej instancji parser używa domyślnych ustawień, które często oznaczają „załaduj wszystko”. Dla ogromnych stron taki domyślny tryb może zużywać gigabajty pamięci i blokować Twój skrypt.

---

## Krok 2: Ogranicz głębokość zasobów

Następnie informujemy opcje, jak głęboko jesteśmy gotowi iść. Ustawienie `max_handling_depth` na 5, na przykład, zatrzymuje parser po pięciu poziomach zagnieżdżonych zasobów. Dostosuj liczbę do swojego przypadku użycia.

```python
# Step 2: Cap the nesting depth (e.g., stop after 5 levels)
options.max_handling_depth = 5
```

> **Porada:** Jeśli interesuje Cię tylko zawartość najwyższego poziomu, głębokość 1 lub 2 zazwyczaj wystarczy i znacznie przyspieszy działanie.

---

## Krok 3: Załaduj dokument HTML z opcjami

Teraz przekazujemy skonfigurowane `options` do `HTMLDocument`. Konstruktor przyjmuje ścieżkę do pliku (lub URL) oraz obiekt opcji, dając Ci precyzyjną kontrolę nad tym, co zostanie załadowane.

```python
# Step 3: Parse the HTML file using the configured options
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", options)
```

> **Co zobaczysz:** Parser odczyta `big_page.html`, ale każdy zasób, który spowodowałby przekroczenie głębokości 5, zostanie cicho zignorowany. To zapobiega niekontrolowanej rekurencji i utrzymuje przewidywalne zużycie pamięci.

---

## Krok 4: Zweryfikuj wynik (Opcjonalnie, ale przydatne)

Dobrym nawykiem jest sprawdzenie, czy dokument został załadowany zgodnie z oczekiwaniami. Poniżej szybka kontrola, która wypisuje liczbę pomyślnie obsłużonych zasobów.

```python
# Step 4: Quick verification
print(f"Handled resources: {len(doc.resources)}")
print(f"Document title: {doc.title}")
```

**Oczekiwany wynik** (Twoje liczby będą się różnić w zależności od pliku wejściowego):

```
Handled resources: 12
Document title: Example Large Page
```

Jeśli liczba jest znacznie niższa niż się spodziewałeś, może być konieczne zwiększenie `max_handling_depth` lub dostosowanie innych właściwości `ResourceHandlingOptions`.

---

## Typowe warianty i przypadki brzegowe

| Situation | Adjustment |
|-----------|------------|
| **Potrzebujesz ignorować tylko obrazy** | Set `options.ignore_images = True`. |
| **Skrypty powodują przekroczenia czasu** | Use `options.max_script_execution_time = 2` (seconds). |
| **Parsowanie zdalnego URL zamiast pliku** | Pass the URL string to `HTMLDocument` just like a file path. |
| **Chcesz własny logger** | Assign `options.logger = my_logger` before loading. |

Te drobne zmiany są częścią zestawu narzędzi **HTMLDocument options** i pozwalają precyzyjnie dostroić **konfigurację ładowania zasobów** bez przepisywania parsera.

---

## Pełny działający przykład

Łącząc wszystko razem, oto samodzielny skrypt, który możesz uruchomić od razu. Zapisz go jako `parse_big_page.py` i uruchom poleceniem `python parse_big_page.py`.

```python
# parse_big_page.py
from htmlparser import HTMLDocument, ResourceHandlingOptions

def main():
    # 1️⃣ Create the options instance
    options = ResourceHandlingOptions()
    
    # 2️⃣ Limit how deep we go into nested resources
    options.max_handling_depth = 5
    
    # Optional: ignore images to speed things up
    # options.ignore_images = True
    
    # 3️⃣ Load the document with our custom options
    doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", options)
    
    # 4️⃣ Verify the load
    print(f"Handled resources: {len(doc.resources)}")
    print(f"Document title: {doc.title}")

if __name__ == "__main__":
    main()
```

Uruchom go, a zobaczysz wypisaną liczbę zasobów i tytuł, co potwierdzi, że pomyślnie **utworzyłeś instancję resourcehandlingoptions** i zastosowałeś ją.

---

## Zakończenie

Właśnie pokazaliśmy, jak **utworzyć instancję ResourceHandlingOptions**, ograniczyć poziom zagnieżdżenia i przekazać ją do `HTMLDocument`. Ten wzorzec zapewnia niezawodną **konfigurację ładowania zasobów** dla dowolnego dużego pliku HTML, utrzymując parsowanie HTML w Pythonie szybkie i przyjazne dla pamięci.

Gotowy na kolejny krok? Spróbuj zmienić limit głębokości, przełączyć `ignore_images` lub zintegrować własny logger — każda zmiana nauczy Cię więcej o **HTMLDocument options** i ich interakcji z Twoim potokiem danych.  

Jeśli ten przewodnik był dla Ciebie przydatny, śmiało podziel się nim, daj gwiazdkę repozytorium lub zostaw komentarz z własnymi wskazówkami. Szczęśliwego parsowania!

## Co powinieneś nauczyć się dalej?

- [Utwórz HTML z łańcucha w C# – Przewodnik po własnym obsługiwaniu zasobów](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Jak zapisać HTML w C# – Kompletny przewodnik z użyciem własnego obsługiwacza zasobów](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Utwórz dostawcę strumieni w .NET z Aspose.HTML](/html/english/net/advanced-features/create-stream-provider/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}