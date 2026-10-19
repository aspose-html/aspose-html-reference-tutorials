---
category: general
date: 2026-06-10
description: Wczytaj HTML z adresu URL, aby szybko uzyskać ikony witryny. Dowiedz
  się, jak wyodrębniać favikony, pobierać adresy URL favikonów witryny i obsługiwać
  przypadki brzegowe w Pythonie.
draft: false
keywords:
- load html from url
- get website icons
- how to extract favicons
- extract favicon urls
- fetch website favicon urls
language: pl
og_description: Wczytaj HTML z adresu URL, aby wyodrębnić favikony i pobrać adresy
  URL favikonów witryny. Krok po kroku tutorial Pythona dla programistów.
og_title: Ładowanie HTML z adresu URL i pobieranie ikon strony – kompletny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Load HTML from URL to get website icons quickly. Learn how to extract
    favicons, fetch website favicon URLs, and handle edge cases in Python.
  headline: Load HTML from URL and Get Website Icons – Complete Guide
  type: TechArticle
tags:
- web scraping
- favicon extraction
- python
- html parsing
title: Załaduj HTML z adresu URL i pobierz ikony witryny – kompletny przewodnik
url: /pl/python/general/load-html-from-url-and-get-website-icons-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ładowanie HTML z URL i Pobieranie Ikon Strony – Kompletny Przewodnik

Kiedykolwiek potrzebowałeś **load HTML from URL**, aby pobrać małe logo strony? Nie jesteś sam. Niezależnie od tego, czy tworzysz menedżer zakładek, pulpit SEO, czy po prostu osobisty projekt hobbystyczny, pobieranie ikon stron to mały, ale istotny element układanki.

W tym samouczku pokażemy, jak **extract favicons** przy użyciu czystego Pythona — bez ciężkiego Selenium, bez magii przeglądarki. Po zakończeniu będziesz w stanie **fetch website favicon URLs**, obsługiwać ścieżki względne i nawet pobierać wiele ikon, jeśli strona je udostępnia. Gotowy? Zanurzmy się.

## Dlaczego w ogóle ładować HTML z URL?

Ładowanie surowego HTML strony daje bezpośredni dostęp do znaczników `<link>`, które przeglądarki używają do znajdowania favikonów. Te znaczniki zazwyczaj wyglądają tak:

```html
<link rel="icon" href="/favicon.ico">
<link rel="apple-touch-icon" href="https://example.com/apple-touch-icon.png">
```

Jeśli uda ci się pobrać ten znacznik, możesz programowo odczytać atrybut `href` i samodzielnie pobrać obraz. To szybsze niż zrzuty ekranu i działa na każdej stronie, która stosuje standardowe konwencje.

## Krok 1 – Ładowanie dokumentu HTML z URL

Pierwszą rzeczą, której potrzebujemy, jest sposób na pobranie źródła strony. Najpopularniejszym wyborem w Pythonie jest biblioteka **requests**, ponieważ jest prosta, niezawodna i obsługuje przekierowania od razu.

```python
import requests

def fetch_html(url: str) -> str:
    """
    Retrieve the raw HTML from the given URL.
    Raises an exception if the request fails.
    """
    response = requests.get(url, timeout=10)
    response.raise_for_status()          # Fail fast on HTTP errors
    return response.text
```

> **Pro tip:** Jeśli pracujesz za korporacyjnym proxy, przekaż `proxies=` do `requests.get`. Dodatkowo, ustawienie krótkiego timeoutu zapobiega zawieszaniu się skryptu na nieaktywnych stronach.

Teraz możemy wywołać `fetch_html("https://example.com")` i otrzymać ciąg znaków zawierający znacznik strony. To jest rdzeń **load HTML from URL** — reszta potoku działa na tym ciągu.

## Krok 2 – Pobieranie ikon strony

Gdy już mamy HTML, następnym krokiem jest znalezienie każdego elementu `<link>`, którego atrybut `rel` zawiera „icon”. Wbudowany moduł `html.parser` może wykonać zadanie, ale **BeautifulSoup** sprawia, że kod jest znacznie czytelniejszy.

```python
from bs4 import BeautifulSoup
from urllib.parse import urljoin

def extract_icon_links(html: str, base_url: str) -> list[str]:
    """
    Parse the HTML and return a list of absolute URLs pointing to icons.
    Handles relative hrefs by joining them with the page’s base URL.
    """
    soup = BeautifulSoup(html, "html.parser")
    icons = []

    # Look for any <link> tag where rel contains "icon"
    for link in soup.find_all("link", rel=lambda r: r and "icon" in r.lower()):
        href = link.get("href")
        if href:
            # Convert relative URLs to absolute ones
            absolute_url = urljoin(base_url, href)
            icons.append(absolute_url)

    return icons
```

Zauważ, że używamy `urljoin`, aby zamienić `"/favicon.ico"` na `"https://example.com/favicon.ico"` — to typowy przypadek brzegowy przy **get website icons**. Niektóre strony serwują różne ikony dla różnych urządzeń, więc możesz otrzymać kilka URL‑i. Żaden problem; po prostu zbieramy je wszystkie.

## Krok 3 – Wyodrębnianie URL‑ów favikony i ich wyświetlanie

Połączenie elementów jest proste. Pobierzemy HTML, uruchomimy ekstraktor i wydrukujemy wynikową listę. Końcowy skrypt wygląda tak:

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin

def fetch_html(url: str) -> str:
    response = requests.get(url, timeout=10)
    response.raise_for_status()
    return response.text

def extract_icon_links(html: str, base_url: str) -> list[str]:
    soup = BeautifulSoup(html, "html.parser")
    icons = []
    for link in soup.find_all("link", rel=lambda r: r and "icon" in r.lower()):
        href = link.get("href")
        if href:
            icons.append(urljoin(base_url, href))
    return icons

def main():
    target = "https://example.com"
    html = fetch_html(target)
    icon_urls = extract_icon_links(html, target)
    print("Found icon URLs:", icon_urls)

if __name__ == "__main__":
    main()
```

### Oczekiwany wynik

Uruchomienie skryptu na stronie, która udostępnia standardową favikonę, może zwrócić:

```
Found icon URLs: ['https://example.com/favicon.ico']
```

Jeśli strona udostępnia wiele ikon (Apple touch icon, shortcut icon itp.), zobaczysz dłuższą listę:

```
Found icon URLs: [
    'https://example.com/favicon.ico',
    'https://example.com/apple-touch-icon.png',
    'https://example.com/favicon-32x32.png'
]
```

To cały przepływ **extract favicon urls** — kompaktowy, lekki pod względem zależności i gotowy do wstawienia w dowolny projekt.

## Radzenie sobie z typowymi problemami

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Względny `href` bez tagu `<base>`** | `urljoin` zakłada URL strony jako bazę, co działa w większości przypadków. | Jeśli istnieje tag `<base href="...">`, odczytaj go najpierw i przekaż jako `base_url`. |
| **Brak `rel="icon"`** | Niektóre strony używają `rel="shortcut icon"` lub własnych wartości. | Rozszerz lambda: `rel=lambda r: r and ("icon" in r.lower() or "shortcut" in r.lower())`. |
| **Przekierowania do innej domeny** | Favikona może znajdować się na CDN. | `urljoin` poprawnie rozwiąże nową domenę, ponieważ używa finalnego URL‑u żądania (`response.url`). |
| **Uszkodzone linki (404)** | HTML wskazuje na plik, który już nie istnieje. | Po wyodrębnieniu URL‑ów możesz zweryfikować każdy za pomocą żądania HEAD przed użyciem. |
| **Wiele tagów `<link>` z tą samą ikoną** | Duplikaty zwiększają listę. | Użyj `set(icon_urls)`, aby usunąć duplikaty przed zwróceniem. |

## Rozszerzenie – Pobieranie URL‑ów favikon w trybie masowym

Jeśli potrzebujesz **fetch website favicon URLs** dla listy domen, otocz logikę `main` pętlą:

```python
domains = ["https://example.com", "https://python.org", "https://github.com"]
for site in domains:
    try:
        icons = extract_icon_links(fetch_html(site), site)
        print(site, "->", icons)
    except Exception as e:
        print(site, "error:", e)
```

Ten wzorzec skaluje się dobrze i możesz dodać buforowanie (np. przy użyciu `functools.lru_cache`), aby nie obciążać wielokrotnie tej samej strony.

## Przegląd wizualny

![Diagram ładowania HTML z URL](load-html-url.png)

*Tekst alternatywny: Diagram ładowania HTML z URL pokazujący kroki pobierania → parsowania → ekstrakcji.*

Powyższy obraz podsumowuje trzyetapowy proces: **load HTML from URL**, **get website icons** i **extract favicon URLs**. Jest przydatny, gdy musisz wyjaśnić przepływ koledze z zespołu.

## Zakończenie

Przeszliśmy przez kompletną, gotową do produkcji metodę, jak **load HTML from URL** i **get website icons** przy użyciu jedynie bibliotek requests i BeautifulSoup w Pythonie. Wyodrębniając atrybuty `href` znaczników `<link rel="icon">`, możesz **extract favicon URLs**, obsługiwać ścieżki względne i nawet pobierać wiele formatów ikon — wszystko w kilku dziesiątkach linii kodu.

Co dalej? Spróbuj pobrać ikony do lokalnego folderu, wygenerować CSV mapujące domeny na favikony lub wbudować tę logikę w API Flask, które serwuje favikony na żądanie. Możliwości dla **fetch website favicon URLs** są nieograniczone, a podstawowa technika pozostaje ta sama.

Masz pytania o przypadki brzegowe lub chcesz podzielić się sprytną modyfikacją? zostaw komentarz poniżej — udanego polowania na ikony!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z krok po kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Ładowanie dokumentów HTML z pliku w Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Ładowanie dokumentów HTML ze strumienia w Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-stream/)
- [Obsługa zdarzeń ładowania dokumentu w Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/handle-document-load-events/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}