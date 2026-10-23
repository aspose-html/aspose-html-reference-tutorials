---
category: general
date: 2026-10-21
description: Dowiedz się, jak parsować HTML w Pythonie, wczytywać dokument HTML, używać
  selektorów CSS i szybko wyodrębniać hiperłącza z HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to parse html
- how to use selector
- extract hyperlinks from html
- load html document python
language: pl
lastmod: 2026-10-21
og_description: Jak parsować HTML w Pythonie przy użyciu selektorów CSS. Załaduj dokument
  HTML, wybierz linki i wyodrębnij hiperłącza z HTML przy użyciu czystego kodu.
og_image_alt: Screenshot showing how to parse HTML in Python with CSS selectors
og_title: Jak parsować HTML w Pythonie – przewodnik krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to parse HTML in Python, load an HTML document, use CSS selectors,
    and extract hyperlinks from HTML quickly.
  headline: How to parse HTML in Python using CSS selectors
  type: TechArticle
tags:
- python
- html-parsing
- css-selectors
title: Jak parsować HTML w Pythonie przy użyciu selektorów CSS
url: /pl/python/general/how-to-parse-html-in-python-using-css-selectors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak parsować HTML w Pythonie przy użyciu selektorów CSS

Jeśli potrzebujesz **how to parse html** w skrypcie Pythona, ten przewodnik pokaże Ci dokładnie, jak to zrobić. Nauczysz się, jak wczytać dokument HTML, jak używać składni selektorów do znajdowania elementów oraz jak wyodrębnić hiperłącza z html bez pisania własnego parsera.

Parsowanie HTML jest powszechnym zadaniem dla scraperów internetowych, potoków analizy danych lub testów automatycznych. Po zakończeniu tego samouczka będziesz mieć funkcję wielokrotnego użytku, która wczytuje dokument HTML, wybiera wszystkie znaczniki `<a>` przy użyciu selektora CSS i zwraca czystą listę URL‑ów.

## Czego będziesz potrzebować

- Python 3.8+ (kod działa na każdej nowszej wersji)  
- Biblioteka **lxml** (`pip install lxml`) – zapewnia szybkie parsowanie HTML i obsługę selektorów CSS  
- Plik HTML, który chcesz przeanalizować (np. `sample.html`)  

Nie są wymagane dodatkowe narzędzia; wszystko działa przy użyciu standardowej biblioteki i jednego pakietu zewnętrznego.

## Krok 1: How to parse HTML – wczytaj dokument

Pierwszym krokiem w każdym przepływie pracy z HTML jest odczytanie pliku do pamięci. Użycie **lxml.html** zapewnia obiekt drzewa, który obsługuje selektory CSS.

```python
# step_1_load.py
from lxml import html

def load_html(path: str) -> html.HtmlElement:
    """
    Load an HTML document from the given file path.
    Returns an lxml HtmlElement that can be queried with CSS selectors.
    """
    with open(path, "r", encoding="utf-8") as f:
        content = f.read()
    # Parse the raw HTML string into a tree
    return html.fromstring(content)

# Example usage
doc = load_html("sample.html")
print("Document loaded – ready for selector queries.")
```

**Dlaczego to jest ważne:**  
`load_html` abstrahuje szablonowy kod odczytu pliku i zapewnia, że dokument jest parsowany przy użyciu tolerancyjnego parsera HTML. To najbezpieczniejszy sposób na **load html document python** bez obaw o niepoprawny znacznik.

## Krok 2: How to use selector – znajdź wszystkie elementy linków

Gdy dokument jest już wczytany, możesz użyć selektora CSS, aby zlokalizować każdy znacznik `<a>`. Selektor `"a"` dopasowuje wszystkie elementy kotwicy, ale możesz go doprecyzować (np. `"a.external"` lub `"nav a"`).

```python
# step_2_selector.py
def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    """
    Return a list of <a> elements using a CSS selector.
    This demonstrates how to use selector syntax with lxml.
    """
    # The CSS selector "a" selects every anchor tag
    return doc.cssselect("a")

# Example usage
links = select_links(doc)
print(f"Found {len(links)} <a> elements.")
```

**Dlaczego to jest ważne:**  
Podejście **how to use selector** pozwala wyrazić złożone zapytania w jednym, czytelnym ciągu znaków, unikając ręcznego przeglądania drzewa. Działa dla każdego wzorca CSS obsługiwanego przez `lxml.cssselect`.

## Krok 3: Extract hyperlinks from HTML i przetwarzaj je

Teraz, gdy masz listę elementów `<a>`, możesz pobrać atrybut `href` z każdego z nich. Poniższy pomocnik dodatkowo normalizuje względne adresy URL względem bazowego URL (jeśli go podasz).

```python
# step_3_extract.py
from urllib.parse import urljoin
from typing import Optional

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    """
    Return a list of href values from the given <a> elements.
    If base_url is supplied, relative URLs are resolved to absolute URLs.
    """
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            # Skip <a> tags without an href attribute
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

# Example usage
hyperlinks = extract_hyperlinks(links, base_url="https://example.com")
for url in hyperlinks:
    print(url)
```

**Oczekiwany wynik** (zakładając, że `sample.html` zawiera trzy linki):

```
https://example.com/page1.html
https://example.com/page2.html
https://external.org/resource
```

**Dlaczego to jest ważne:**  
`extract_hyperlinks` jest rdzeniem **extract hyperlinks from html**. Elegancko obsługuje brakujące atrybuty `href`, rozwiązuje względne linki i zwraca zwykłą listę Pythona, którą możesz przekazać do dalszego przetwarzania (np. requests, pandas lub baza danych).

## Pełny przykład end‑to‑end

Połączenie trzech funkcji daje pojedynczy skrypt, który wczytuje plik, wybiera wszystkie kotwice i wypisuje każdy hiperlink.

```python
# parse_links.py
from lxml import html
from urllib.parse import urljoin
from typing import Optional

def load_html(path: str) -> html.HtmlElement:
    with open(path, "r", encoding="utf-8") as f:
        return html.fromstring(f.read())

def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    return doc.cssselect("a")

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

if __name__ == "__main__":
    # 1️⃣ Load the HTML document
    document = load_html("sample.html")
    # 2️⃣ Use selector to grab all <a> tags
    anchor_elements = select_links(document)
    # 3️⃣ Extract and print each hyperlink
    for url in extract_hyperlinks(anchor_elements, base_url="https://example.com"):
        print(url)
```

Uruchomienie `python parse_links.py` wypisuje każdy hiperlink, w pełni rozdzielony, w konsoli. Ten skrypt demonstruje **how to parse html**, **how to use selector** i **extract hyperlinks from html** w jednym, wielokrotnego użytku przepływie.

## Typowe warianty i obsługa przypadków brzegowych

| Situation | What to change | Reason |
|-----------|----------------|--------|
| **Potrzebne tylko bezwzględne URL‑e** | Pomiń argument `base_url` w `extract_hyperlinks` | Pozostawia względne URL‑e niezmienione |
| **Potrzebujesz również tekstu linku** | Zwróć krotkę `(href, link.text_content())` z `extract_hyperlinks` | Umożliwia przechowywanie zarówno URL, jak i tekstu kotwicy |
| **Duże pliki HTML** | Użyj `lxml.etree.iterparse` z filtrem selektora CSS | Zmniejsza zużycie pamięci poprzez strumieniowanie |
| **Inny selektor** | Zastąp `"a"` przez `"nav a[href]"` lub `"div.content a.external"` | Celuje w podzbiór linków, przydatne dla **how to use selector** na złożonych stronach |

**Pro tip:** Zawsze waliduj wyodrębnione URL‑e przed wykonywaniem żądań sieciowych. Szybka kontrola `urlparse` może odfiltrować niepoprawne ciągi i ochronić Twój scraper przed awariami.

## Zakończenie

Teraz wiesz, jak **how to parse html** w Pythonie, jak **load html document python**, jak **how to use selector** aby celować w elementy oraz jak **extract hyperlinks from html** efektywnie. Pełny przykład powyżej jest gotowy do skopiowania i wklejenia do Twojego projektu, a każdą funkcję możesz dostosować do bardziej zaawansowanych przypadków użycia, takich jak paginacja, treść generowana przez JavaScript lub wielostronicowe crawl‑owanie.

Następne kroki, które możesz rozważyć, to:
- Użycie **requests‑html** lub **Playwright** do pobierania stron wymagających wykonania JavaScript.  
- Przechowywanie wyodrębnionych URL‑ów w pliku CSV lub bazie danych SQLite do późniejszej analizy.  
- Dodanie obsługi błędów dla timeoutów sieciowych i kodów statusu HTTP.

Miłego parsowania i zachęcamy do eksperymentowania z różnymi selektorami, aby odblokować pełną moc zapytań HTML opartych na CSS w Pythonie!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [How to configure HTML resource handling in Python and load an HTML document](/html/english/python/general/how-to-configure-html-resource-handling-in-python-and-load-a/)
- [How to Parse HTML in Python – Complete Guide](/html/english/python/general/how-to-parse-html-in-python-complete-guide/)
- [How to Load HTML in Python – Step‑by‑Step Guide](/html/english/python/general/how-to-load-html-in-python-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}