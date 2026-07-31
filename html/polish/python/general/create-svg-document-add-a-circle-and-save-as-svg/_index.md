---
category: general
date: 2026-07-31
description: Dowiedz się, jak stworzyć dokument SVG, dodać koło i szybko zapisać plik
  SVG. Eksportuj grafikę jako SVG za pomocą kilku linijek kodu w Pythonie.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg document
- save svg file
- export graphic as svg
- add circle to svg
language: pl
lastmod: 2026-07-31
og_description: Utwórz dokument SVG, dodaj koło i zapisz plik SVG w kilka sekund.
  Ten przewodnik pokazuje, jak wyeksportować grafikę jako SVG, używając przejrzystego,
  gotowego do uruchomienia kodu.
og_image_alt: Screenshot of a red circle inside an SVG file named circle.svg
og_title: Utwórz dokument SVG – dodaj koło i zapisz jako SVG
schemas:
- author: Aspose
  dateModified: '2026-07-31'
  description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  headline: Create SVG Document – Add a Circle and Save as SVG
  type: TechArticle
- description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  name: Create SVG Document – Add a Circle and Save as SVG
  steps:
  - name: Pro tip
    text: If you plan to generate many files in a loop, give each `Drawing` a unique
      name or use `io.BytesIO` to keep everything in memory until you’re ready to
      write.
  - name: Edge case – Transparent background
    text: 'If you need a transparent background (the default for SVG), you can skip
      setting a `fill` on the root. For a white background, add:'
  - name: 'Bonus: Export graphic as SVG programmatically'
    text: 'If you need the SVG content as a string—for example, to embed it in an
      HTML email—you can call `dwg.tostring()` instead of `save()`:'
  type: HowTo
- questions:
  - answer: Swap `dwg.circle` for `dwg.rect`, `dwg.ellipse`, or even a custom `<path>`
      string. The API is consistent across shapes.
    question: What if I want a different shape?
  - answer: Absolutely. The file you just created can be referenced with `<img src="circle.svg"
      alt="Red circle">` or inlined with `<svg>` tags.
    question: Can I embed the SVG directly in HTML?
  - answer: You could, but libraries like `svgwrite` handle namespace quirks and make
      the code far more maintainable—especially when you start adding gradients or
      animations.
    question: Why not write raw XML?
  type: FAQPage
tags:
- svg
- python
- vector-graphics
- programming-tutorial
title: Utwórz dokument SVG – dodaj koło i zapisz jako SVG
url: /pl/python/general/create-svg-document-add-a-circle-and-save-as-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz dokument SVG – Dodaj koło i zapisz jako SVG

Czy kiedykolwiek potrzebowałeś **create SVG document** z kodu, ale nie wiedziałeś, od czego zacząć? Nie jesteś sam; wielu programistów napotyka tę barierę, gdy po raz pierwszy bawi się grafiką wektorową. W tym tutorialu przeprowadzimy mały, samodzielny przykład, który pokaże Ci, jak **add circle to SVG**, a następnie **save SVG file**, abyś mógł **export graphic as SVG** do użycia w sieci lub w narzędziach projektowych.

Utrzymamy wszystko lekkie: kilka linijek Pythona, popularna biblioteka pomocnicza SVG i odrobinę wyjaśnień. Po zakończeniu będziesz mieć gotowy do użycia `circle.svg` w swoim folderze i zrozumiesz, dlaczego każdy krok ma znaczenie — bez niejasnych skrótów „zobacz dokumentację”.

## Czego będziesz potrzebować

- Python 3.8+ (dowolna aktualna wersja działa)
- Pakiet `svgwrite` – zainstaluj go poleceniem `pip install svgwrite`
- Edytor tekstu lub IDE (VS Code, PyCharm, a nawet Notatnik wystarczy)
- Uprawnienia do zapisu w katalogu, w którym chcesz zapisać plik

To wszystko. Brak ciężkich zależności, brak zewnętrznych usług.

## Krok 1: Przygotuj dokument SVG

Tworzenie dokumentu SVG jest tak proste, jak utworzenie obiektu `Drawing` z biblioteki `svgwrite`. Pomyśl o tym obiekcie jako o czystym płótnie, na którym żyją wszystkie kształty.

```python
import svgwrite

# Step 1: Create a new SVG document (canvas) 800×800 pixels
dwg = svgwrite.Drawing(filename="circle.svg", size=("200px", "200px"))
```

> **Dlaczego to ważne:** Klasa `Drawing` zajmuje się całym szablonem XML za Ciebie — przestrzeniami nazw, nagłówkami i elementem root `<svg>`. Określając nazwę pliku od razu, już wiemy, gdzie plik się znajdzie, co sprawia, że późniejszy krok **save svg file** jest trywialny.

### Porada
Jeśli planujesz generować wiele plików w pętli, nadaj każdemu `Drawing` unikalną nazwę lub użyj `io.BytesIO`, aby trzymać wszystko w pamięci, dopóki nie będziesz gotowy do zapisu.

## Krok 2: Dodaj koło do SVG

Teraz, gdy dokument istnieje, **add circle to SVG**. Metoda `add()` przyjmuje dowolny obiekt kształtu; `Circle` jest idealny dla prostego czerwonego punktu w centrum.

```python
# Step 2: Add a red circle element to the SVG root
center = (100, 100)          # x, y coordinates (half of 200px canvas)
radius = 80                  # radius in pixels
circle = dwg.circle(center=center, r=radius, fill='red')
dwg.add(circle)
```

> **Dlaczego używamy zmiennych `center` i `radius`:** Hard‑coding liczb utrudnia czytelność i utrzymanie kodu. Nazwając te wartości, wyjaśniamy intencję — to koło znajduje się dokładnie w środku płótna 200 × 200 i jest wystarczająco duże, by było zauważalne.

### Przypadek brzegowy – Przezroczyste tło
Jeśli potrzebujesz przezroczystego tła (domyślne dla SVG), możesz pominąć ustawianie `fill` na elemencie root. Aby uzyskać białe tło, dodaj:

```python
dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))
```

Umieść to przed dodaniem koła, aby prostokąt znajdował się pod nim.

## Krok 3: Zapisz plik SVG

Z kształtem na miejscu, ostatnim aktem jest **save SVG file**. Metoda `save()` zapisuje XML na dysk, a ponieważ już podaliśmy `Drawing` nazwę pliku, jedno wywołanie wystarczy.

```python
# Step 3: Save the SVG document to a file
dwg.save()
print("✅ circle.svg has been created in the current directory.")
```

> **Co się dzieje pod maską?** `svgwrite` serializuje drzewo elementów do łańcucha znaków, dodaje deklarację XML i zapisuje je używając kodowania UTF‑8. Jeśli docelowy katalog nie istnieje, Python zgłosi `FileNotFoundError`; upewnij się, że ścieżka jest prawidłowa lub utwórz ją za pomocą `os.makedirs()`.

### Bonus: Eksportuj grafikę jako SVG programowo

Jeśli potrzebujesz zawartości SVG jako łańcucha znaków — na przykład, aby osadzić go w e‑mailu HTML — możesz wywołać `dwg.tostring()` zamiast `save()`:

```python
svg_content = dwg.tostring()
# Now you can send svg_content over a network, store it in a DB, etc.
```

## Pełny działający przykład

Łącząc wszystko razem, oto kompletny, gotowy do uruchomienia skrypt:

```python
import svgwrite
import os

def create_svg_with_circle(output_path: str):
    """
    Creates an SVG file containing a single red circle.
    Parameters
    ----------
    output_path: str
        Full path where the SVG file will be saved.
    """
    # Ensure the directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Initialise the SVG document (800×800 canvas)
    dwg = svgwrite.Drawing(filename=output_path, size=("200px", "200px"))

    # Optional: add a white background rectangle
    dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))

    # Add a red circle in the centre
    center = (100, 100)
    radius = 80
    circle = dwg.circle(center=center, r=radius, fill='red')
    dwg.add(circle)

    # Save the file – this is the key step to **save svg file**
    dwg.save()
    print(f"✅ SVG saved to {output_path}")

if __name__ == "__main__":
    # Change this path to wherever you want the file
    output_file = os.path.join(os.getcwd(), "circle.svg")
    create_svg_with_circle(output_file)
```

**Oczekiwany wynik:** Po uruchomieniu skryptu zobaczysz plik `circle.svg` w tym samym folderze. Otwierając go w przeglądarce lub dowolnym edytorze wektorowym, zobaczysz czerwone koło wyśrodkowane na białym kwadracie — dokładnie to, co zaprogramowaliśmy.

## Częste pytania i pułapki

- **Co zrobić, jeśli chcę inny kształt?** Zamień `dwg.circle` na `dwg.rect`, `dwg.ellipse` lub nawet własny ciąg `<path>`. API jest spójne dla wszystkich kształtów.
- **Czy mogę osadzić SVG bezpośrednio w HTML?** Oczywiście. Plik, który właśnie stworzyłeś, może być odwołany za pomocą `<img src="circle.svg" alt="Red circle">` lub wstawiony inline przy użyciu tagów `<svg>`.
- **Dlaczego nie pisać surowego XML?** Można, ale biblioteki takie jak `svgwrite` radzą sobie z niuansami przestrzeni nazw i sprawiają, że kod jest znacznie bardziej utrzymywalny — szczególnie gdy zaczynasz dodawać gradienty lub animacje.

## Zakończenie

Teraz wiesz, jak **create SVG document**, **add circle to SVG** i **save SVG file**, abyś mógł **export graphic as SVG** przy użyciu zaledwie kilku linijek Pythona. Ten wzorzec skaluje się: zamień koło na dowolny kształt wektorowy, iteruj po danych, aby generować wykresy, lub przetwarzaj partie zasobów dla systemu projektowego.

Co dalej? Spróbuj dodać etykiety tekstowe, poeksperymentuj z gradientami lub wygeneruj całą galerię ikon w jednym skrypcie. Jeśli jesteś ciekawy bardziej zaawansowanych funkcji, zajrzyj do dokumentacji `svgwrite` dotyczącej grup (`<g>`), transformacji i obsługi animacji.

Miłego kodowania i niech Twoje wektory zawsze pozostają ostre!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}