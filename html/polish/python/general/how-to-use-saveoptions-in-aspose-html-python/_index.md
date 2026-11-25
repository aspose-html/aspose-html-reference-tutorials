---
category: general
date: 2026-07-27
description: Jak używać SaveOptions w Aspose.HTML (Python) do konwersji dużej strony
  HTML i efektywnego zarządzania zasobami.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use SaveOptions
- convert large html page
- apply resource handling
- Aspose.HTML Python
- HTML resource handling
language: pl
lastmod: 2026-07-27
og_description: Jak używać SaveOptions w Aspose.HTML (Python) umożliwia konwersję
  dużych stron HTML przy jednoczesnym zarządzaniu zasobami dla czystych, szybkich
  wyników.
og_image_alt: Screenshot illustrating how to use SaveOptions in Aspose.HTML for Python
og_title: Jak korzystać z SaveOptions w Aspose.HTML – przewodnik Pythona
schemas:
- author: Aspose
  dateModified: '2026-07-27'
  description: How to use SaveOptions in Aspose.HTML (Python) to convert large HTML
    page and apply resource handling efficiently.
  headline: How to Use SaveOptions in Aspose.HTML (Python)
  type: TechArticle
- questions:
  - answer: Aspose.HTML follows redirects but won’t send credentials automatically.
      You can pre‑download those assets or use a custom `WebRequest` handler (beyond
      this guide’s scope).
    question: What if the page references resources over HTTPS that require authentication?
  - answer: Yes—set `resource_options.max_handling_depth = 0`. This skips external
      files but leaves any `<style>` blocks intact.
    question: Can I preserve inline CSS while stripping external files?
  - answer: After saving, you can run a secondary pass with Pillow to downscale images,
      or let Aspose.HTML’s built‑in image compression options handle it (use `save_options.image_quality`).
    question: What about very large images that still bloat the output?
  - answer: The limit is global across all resource types (images, scripts, styles).
      If you need granular control, you’d have to filter resources manually after
      loading the document.
    question: Is the depth limit applied per‑resource type?
  type: FAQPage
tags:
- Aspose.HTML
- Python
- HTML processing
title: Jak używać SaveOptions w Aspose.HTML (Python)
url: /pl/python/general/how-to-use-saveoptions-in-aspose-html-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać SaveOptions w Aspose.HTML (Python)

Jak używać SaveOptions w Aspose.HTML dla Pythona to pytanie, które zadaje wielu programistów, pracując z ogromnymi plikami HTML. Jeśli potrzebujesz **konwertować dużą stronę HTML**, zachowując jednocześnie ścisłą kontrolę nad **zarządzaniem zasobami**, jesteś we właściwym miejscu.  

W tym samouczku przeprowadzimy Cię przez scenariusz z prawdziwego życia: weźmy masywną stronę HTML, ograniczmy głębokość pobierania zagnieżdżonych zasobów, a na koniec zapiszmy (lub skonwertujmy) wynik z krystalicznie czystą kontrolą. Bez niejasnych odniesień, tylko kompletny, gotowy do uruchomienia przykład, który możesz skopiować‑wkleić do swojego projektu już dziś.

> **Wskazówka:** `SaveOptions` w Aspose.HTML działa nie tylko przy zapisywaniu z powrotem do HTML, ale także przy konwersji do PDF, PNG czy nawet DOCX. Ten sam wzorzec, który omówimy poniżej, ma zastosowanie do wszystkich tych formatów.

---

## Czego będziesz potrzebować

- **Python 3.8+** (kod używa podpowiedzi typów, ale działa na każdej nowszej wersji)  
- **Aspose.HTML for Python via .NET** – zainstaluj poleceniem `pip install aspose-html`  
- **Duży plik HTML**, który chcesz zmniejszyć lub przekształcić (w przykładzie użyto `big_page.html`)  
- Trochę wolnego miejsca na dysku na plik wyjściowy  

To wszystko – żadnych dodatkowych bibliotek, żadnych ciężkich narzędzi budujących.

---

## Jak używać SaveOptions z opcjami zarządzania zasobami

To jest sedno sprawy. Utworzymy instancję `SaveOptions`, dołączymy obiekt `ResourceHandlingOptions`, który mówi Aspose.HTML, jak głęboko ma podążać za powiązanymi zasobami, a następnie przekażemy wszystko metodzie `save` dokumentu.

```python
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

# Load the source HTML document
input_path = "YOUR_DIRECTORY/big_page.html"
doc = HTMLDocument(input_path)

# Define how deep nested resources should be processed (limit to 3 levels)
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # <-- controls depth of resource fetching

# Attach the resource handling configuration to the save options
save_options = SaveOptions()
save_options.resource_handling_options = resource_options

# Save the processed document (or convert to another format if desired)
output_path = "YOUR_DIRECTORY/big_page_processed.html"
doc.save(output_path, save_options)
```

**Dlaczego to działa:**  
- `HTMLDocument` ładuje oryginalny plik, parsując każdy `<img>`, `<link>`, `<script>` itd.  
- `ResourceHandlingOptions.max_handling_depth` instruuje silnik, aby przestał podążać za zasobami po trzech poziomach zagnieżdżenia – idealne, aby uniknąć nieskończonych pętli na stronach, które osadzają inne strony.  
- `SaveOptions` jest naczyniem, które przenosi zarówno format wyjściowy (domyślnie HTML), jak i zasady zarządzania zasobami.  
- Na koniec `doc.save` zapisuje nowy plik, stosując właśnie ustawione reguły.

Po uruchomieniu skryptu zobaczysz nowy plik w `big_page_processed.html`. Otwórz go w przeglądarce; zauważysz, że wszystkie obrazy, style i skrypty do trzech poziomów głębokości nadal są obecne, a głębsze odwołania zostały usunięte. To drastycznie zmniejsza rozmiar pliku bez łamania podstawowego układu strony – dokładnie tego potrzebujesz, gdy **konwertujesz dużą stronę HTML** do użytku offline lub wysyłki e‑mailowej.

---

## Efektywna konwersja dużej strony HTML

Jeśli Twoim celem jest *konwersja dużej strony HTML* do lżejszej wersji, powyższy fragment kodu już wykonuje większość ciężkiej roboty. Możesz jednak chcieć zmienić format wyjściowy całkowicie. Aspose.HTML umożliwia to jedną linią:

```python
# Convert to PDF instead of HTML
pdf_save_options = SaveOptions()
pdf_save_options.resource_handling_options = resource_options
pdf_save_options.format = "PDF"   # specify desired format

doc.save("YOUR_DIRECTORY/big_page.pdf", pdf_save_options)
```

Wystarczy podmienić właściwość `format` na `"PNG"`, `"JPEG"` lub `"DOCX"` i masz pełny potok konwersji. Te same zasady **zarządzania zasobami** pozostają niezmienione, więc powstały PDF nie będzie osadzał każdego zewnętrznego pliku CSS ze strony źródłowej – tylko te znajdujące się w trzech poziomach głębokości, które określiłeś.

---

## Stosowanie zarządzania zasobami do zagnieżdżonych zasobów

Zanurzmy się nieco głębiej w **zarządzanie zasobami**. Załóżmy, że Twój HTML zawiera arkusz stylów, który sam importuje inne arkusze, a te z kolei wciągają obrazy. Bez limitu głębokości Aspose.HTML mógłby podążać za łańcuchem w nieskończoność, zwiększając zużycie pamięci i CPU.

```python
# Example: limit to 1 level for aggressive trimming
resource_options.max_handling_depth = 1
save_options.resource_handling_options = resource_options
doc.save("trimmed_page.html", save_options)
```

- **Głębokość 0** – Nie pobierane są żadne zewnętrzne zasoby; otrzymujesz szkielet HTML bez dodatków.  
- **Głębokość 1** – Uwzględniane są tylko zasoby pierwszego rzędu (bezpośrednie tagi `<img>`, natychmiastowe pliki CSS).  
- **Głębokość 2+** – Respektowane jest głębsze zagnieżdżenie, przydatne w skomplikowanych witrynach, gdzie style zależą od innych stylów.

Wybierz głębokość, która pasuje do Twojego scenariusza **konwersji dużej strony HTML**. Dla newsletterów e‑mailowych zazwyczaj wystarczy głębokość 1. Dla lokalnego archiwum, głębokość 3 (jak w głównym przykładzie) zapewnia ładny kompromis.

---

## Pełny działający przykład – od początku do końca

Poniżej znajduje się samodzielny skrypt, który możesz umieścić w pliku o nazwie `process_html.py`. Zawiera obsługę błędów, logowanie oraz mały pomocnik, który wypisuje uzyskaną redukcję rozmiaru.

```python
import os
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

def process_html(
    src_path: str,
    dst_path: str,
    depth: int = 3,
    fmt: str = "HTML"
) -> None:
    """
    Loads an HTML file, applies resource handling, and saves it in the requested format.
    Returns nothing; prints size statistics for quick verification.
    """
    if not os.path.isfile(src_path):
        raise FileNotFoundError(f"Source file not found: {src_path}")

    # Load document
    doc = HTMLDocument(src_path)

    # Set up resource handling
    res_opts = ResourceHandlingOptions()
    res_opts.max_handling_depth = depth

    # Configure save options (including format)
    save_opts = SaveOptions()
    save_opts.resource_handling_options = res_opts
    save_opts.format = fmt.upper()   # Aspose expects upper‑case format strings

    # Perform save / conversion
    doc.save(dst_path, save_opts)

    # Report size change
    original = os.path.getsize(src_path)
    final = os.path.getsize(dst_path)
    reduction = (original - final) / original * 100
    print(f"Saved {fmt.lower()} to '{dst_path}'. Size reduced by {reduction:.2f}%.")

# -------------------------------------------------------------------------
# Example usage
if __name__ == "__main__":
    input_file = "YOUR_DIRECTORY/big_page.html"
    output_file = "YOUR_DIRECTORY/big_page_processed.html"

    process_html(
        src_path=input_file,
        dst_path=output_file,
        depth=3,          # apply resource handling up to three levels
        fmt="HTML"       # change to "PDF" or "PNG" to convert format
    )
```

**Oczekiwany wynik (konsola):**

```
Saved html to 'YOUR_DIRECTORY/big_page_processed.html'. Size reduced by 42.57%.
```

Otwórz przetworzony plik; zobaczysz lżejszą stronę, która wciąż wygląda jak oryginał. Jeśli zmienisz `fmt` na `"PDF"`, konsola zgłosi rozmiar pliku PDF i będziesz mógł otworzyć go w dowolnym przeglądarce PDF.

---

## Często zadawane pytania i przypadki brzegowe

- **Co zrobić, gdy strona odwołuje się do zasobów przez HTTPS wymagających uwierzytelnienia?**  
  Aspose.HTML podąża za przekierowaniami, ale nie wysyła poświadczeń automatycznie. Możesz wcześniej pobrać te zasoby lub użyć własnego obsługującego `WebRequest` (poza zakresem tego przewodnika).

- **Czy mogę zachować inline CSS, jednocześnie usuwając pliki zewnętrzne?**  
  Tak – ustaw `resource_options.max_handling_depth = 0`. Pominie to pliki zewnętrzne, ale pozostawi wszystkie bloki `<style>`.

- **Co z bardzo dużymi obrazami, które nadal zwiększają rozmiar wyjścia?**  
  Po zapisaniu możesz wykonać drugi przebieg przy użyciu Pillow, aby zmniejszyć rozmiar obrazów, lub skorzystać z wbudowanych opcji kompresji obrazów w Aspose.HTML (użyj `save_options.image_quality`).

- **Czy limit głębokości jest stosowany osobno dla każdego typu zasobu?**  
  Limit jest globalny dla wszystkich typów zasobów (obrazy, skrypty, style). Jeśli potrzebujesz bardziej szczegółowej kontroli, musisz ręcznie filtrować zasoby po załadowaniu dokumentu.

---

## Zakończenie

Masz teraz solidne pojęcie o **tym, jak używać SaveOptions** w Aspose.HTML


## Co powinieneś nauczyć się dalej?


Poniższe samouczki dotyczą ściśle powiązanych tematów, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu wraz z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [How to Convert HTML to MHTML with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}