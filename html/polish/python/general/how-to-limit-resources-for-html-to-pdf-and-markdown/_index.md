---
category: general
date: 2026-08-09
description: Jak ograniczyć zasoby podczas konwertowania HTML na PDF lub Markdown.
  Dowiedz się, jak eksportować PDF, wyodrębniać linki z HTML i kontrolować głębokość
  zasobów.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to limit resources
- convert html to pdf
- convert html to markdown
- extract links from html
- how to export pdf
language: pl
lastmod: 2026-08-09
og_description: Jak ograniczyć zasoby podczas konwertowania HTML na PDF lub Markdown.
  Ten przewodnik pokazuje, jak wyeksportować PDF, wyodrębnić linki z HTML i utrzymać
  płytkie przetwarzanie zasobów.
og_image_alt: Screenshot showing how to limit resources in HTML conversion script
og_title: Jak ograniczyć zasoby przy konwersji HTML‑do‑PDF i HTML‑do‑Markdown
schemas:
- author: GroupDocs
  dateModified: '2026-08-09'
  description: How to limit resources while converting HTML to PDF or Markdown. Learn
    to export PDF, extract links from HTML, and control resource depth.
  headline: How to limit resources for HTML to PDF and Markdown
  type: TechArticle
tags:
- HTML conversion
- PDF export
- Markdown generation
- Resource handling
title: Jak ograniczyć zasoby przy konwersji HTML na PDF i Markdown
url: /pl/python/general/how-to-limit-resources-for-html-to-pdf-and-markdown/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak ograniczyć zasoby przy konwersji HTML do PDF i Markdown

Jeśli potrzebujesz **jak ograniczyć zasoby** podczas konwersji dużej skali HTML, ten przewodnik pokazuje pełne rozwiązanie. Konfigurując opcje obsługi zasobów, zapobiegasz głębokim pobraniom zewnętrznym, utrzymujesz niskie zużycie pamięci i nadal otrzymujesz dokładny wynik w PDF i Markdown.

Dowiesz się także, jak **convert html to pdf**, jak **convert html to markdown**, jak **extract links from html**, oraz najlepszy sposób **how to export pdf** z tego samego dokumentu źródłowego. Nie jest wymagane żadne zewnętrzne narzędzie poza GroupDocs.Conversion SDK.

## Co osiągniesz

* Ogranicz przetwarzanie zewnętrznych zasobów do bezpiecznej głębokości.  
* Wygeneruj plik PDF z dużego raportu HTML.  
* Utwórz plik Markdown w stylu Git, który zawiera tylko linki i akapity.  
* Zweryfikuj, że eksport PDF powiódł się oraz że plik Markdown zawiera oczekiwane linki.

### Wymagania wstępne

* Python 3.8+ (kod używa typowanego Pythona).  
* Zainstalowany pakiet `groupdocs-conversion` (`pip install groupdocs-conversion`).  
* Duży plik HTML (np. `big_report.html`) znajdujący się w zapisywalnym katalogu.  

---

## Jak ograniczyć zasoby przy konwersji HTML

Kontrolowanie, ile poziomów zewnętrznych zasobów (obrazów, CSS, skryptów) konwerter podąża, jest kluczowe dla wydajności i bezpieczeństwa. Klasa `ResourceHandlingOptions` pozwala ustawić maksymalną głębokość obsługi. Głębokość **3** oznacza, że konwerter będzie podążał za linkami do trzech poziomów i następnie zatrzyma się, zapobiegając niekontrolowanym wywołaniom sieciowym.

```python
from groupdocs.conversion import ResourceHandlingOptions, HTMLDocument, Converter, MarkdownSaveOptions

# Step 1: Create a ResourceHandlingOptions instance and cap the depth
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3  # limit external resource traversal
```

*Dlaczego to ważne*: Duże raporty często odwołują się do wielu zewnętrznych zasobów. Bez limitu głębokości konwerter może próbować pobrać każdy powiązany skrypt lub obraz, wyczerpując przepustowość i pamięć. Ustawienie `max_handling_depth` na 3 równoważy kompletność z bezpieczeństwem.

---

## Konwertuj HTML do PDF z kontrolowaną głębokością zasobów

Gdy opcje zasobów są gotowe, załaduj dokument HTML przy użyciu tych opcji i wywołaj konwersję do PDF. Metoda `Converter.convert_html` wykrywa format wyjściowy na podstawie rozszerzenia pliku.

```python
# Step 2: Load the HTML document with the resource options
html_doc = HTMLDocument("YOUR_DIRECTORY/big_report.html", resource_options)

# Step 3: Convert the HTML document to PDF
Converter.convert_html(html_doc, "YOUR_DIRECTORY/big_report.pdf")
```

*Dlaczego to działa*: Konstruktor `HTMLDocument` przyjmuje argument `ResourceHandlingOptions`, zapewniając, że ten sam limit głębokości obowiązuje podczas generowania PDF. SDK automatycznie renderuje układ strony, osadza dozwolone obrazy i tworzy wysokiej jakości PDF.

**Oczekiwany wynik**: `big_report.pdf` pojawia się w `YOUR_DIRECTORY`. Otwórz go w dowolnym przeglądarce PDF, aby potwierdzić, że obrazy, tabele i tekst są renderowane poprawnie, a zasoby zewnętrzne poza głębokością 3 są pomijane.

---

## Przygotuj opcje zapisu Markdown do wyodrębniania linków

Gdy potrzebujesz lekkiej reprezentacji HTML, konwersja do Markdown jest idealna. Klasa `MarkdownSaveOptions` pozwala wybrać formatowanie (Git‑flavoured) i określić, które elementy treści zachować. W tym samouczku zachowujemy tylko **links** i **paragraphs**, co spełnia wymaganie **extract links from html**.

```python
# Step 4: Configure MarkdownSaveOptions for link‑only output
markdown_options = MarkdownSaveOptions()
markdown_options.formatter = MarkdownSaveOptions.Formatter.GIT
markdown_options.features = (
    MarkdownSaveOptions.Features.LINK |
    MarkdownSaveOptions.Features.PARAGRAPH
)
```

*Dlaczego te flagi*:
* `Formatter.GIT` generuje Markdown, który działa bezproblemowo z GitHub i GitLab.  
* `Features.LINK | Features.PARAGRAPH` usuwa obrazy, tabele i skrypty, pozostawiając czystą listę hiperłączy i czytelnych bloków tekstu.

---

## Konwertuj HTML do Markdown przy użyciu skonfigurowanych opcji

Teraz uruchom konwersję przy użyciu tego samego obiektu `HTMLDocument`. Przeciążona metoda `convert_html` przyjmuje obiekt `MarkdownSaveOptions`, po którym następuje ścieżka docelowego pliku.

```python
# Step 5: Convert the same HTML document to Markdown
Converter.convert_html(html_doc, markdown_options, "YOUR_DIRECTORY/big_report.md")
```

**Wynik**: `big_report.md` zawiera tylko linki i akapity sformatowane w Markdown. Otwórz plik w dowolnym edytorze, aby zobaczyć zwięzłą listę URL‑ów wyodrębnionych z oryginalnego HTML.

---

## Jak wyeksportować PDF i zweryfikować wyniki

Eksportowanie PDF jest już opisane w Kroku 3, ale warto potwierdzić, że plik został zapisany poprawnie i że limit zasobów zachował się zgodnie z oczekiwaniami.

```python
import os

pdf_path = "YOUR_DIRECTORY/big_report.pdf"
md_path = "YOUR_DIRECTORY/big_report.md"

# Verify PDF existence and size
if os.path.isfile(pdf_path):
    print(f"PDF exported successfully – size: {os.path.getsize(pdf_path)} bytes")
else:
    raise FileNotFoundError("PDF export failed")

# Verify Markdown existence and preview first 5 lines
if os.path.isfile(md_path):
    print("Markdown export successful. First lines:")
    with open(md_path, "r", encoding="utf-8") as f:
        for _ in range(5):
            print(f.readline().strip())
else:
    raise FileNotFoundError("Markdown export failed")
```

*Dlaczego to sprawdzenie*: Kontrola rozmiaru pliku pomaga wykryć nieprawidłowo małe pliki PDF, które mogą wskazywać na brakujące zasoby. Podgląd Markdown potwierdza, że zachowano tylko linki i akapity, spełniając cel **extract links from html**.

---

## Typowe warianty i obsługa przypadków brzegowych

| Sytuacja | Zalecana modyfikacja |
|-----------|-------------------|
| **HTML references deeper than 3 levels** | Zwiększ `max_handling_depth` do 5 lub 7, ale monitoruj użycie pamięci. |
| **Need to keep images in Markdown** | Dodaj `MarkdownSaveOptions.Features.IMAGE` do flagi `features`. |
| **Generating a single‑page PDF** | Ustaw `PDFSaveOptions.page_width` i `page_height`, aby dopasować zawartość, lub użyj `pdf_options.split_into_pages = False`. |
| **Running on a headless server** | Upewnij się, że natywne zależności SDK są zainstalowane (`libcairo`, `libpango`), aby uniknąć błędów renderowania. |
| **Large files cause timeout** | Przetwarzaj HTML w częściach, ładując sekcje za pomocą `HTMLDocument.load_range(start, end)`. |

**Wskazówka**: Ponownie używaj tego samego obiektu `HTMLDocument` do wielu konwersji. SDK buforuje sparsowany DOM, co zmniejsza czas CPU przy kolejnych eksportach PDF lub Markdown.

---

## Zakończenie

Teraz wiesz, **jak ograniczyć zasoby** przy **convert html to pdf** i **convert html to markdown**, jak **extract links from html**, oraz jakie są właściwe kroki **how to export pdf** w sposób bezpieczny. Konfigurując `ResourceHandlingOptions` i `MarkdownSaveOptions`, kontrolujesz głębokość pobierania zewnętrznych zasobów, utrzymujesz wyjście lekkie i tworzysz niezawodne artefakty do dalszego przetwarzania.

Następnie, poznaj zaawansowane funkcje, takie jak **custom CSS injection**, **watermarking PDFs** lub **batch converting multiple HTML files**. Te tematy opierają się na tych samych zasadach omówionych tutaj i dalej rozszerzają Twój pipeline przetwarzania dokumentów.

---

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z instrukcjami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak konwertować HTML do PDF w Javie – przy użyciu Aspose.HTML dla Javy](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Jak używać Aspose.HTML do konfigurowania czcionek dla HTML‑to‑PDF w Javie](/html/english/java/configuring-environment/configure-fonts/)
- [Jak konwertować HTML do MHTML przy użyciu Aspose.HTML dla Javy](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}