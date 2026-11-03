---
category: general
date: 2026-06-26
description: Dowiedz się, jak uzyskać favicon, ładując HTML z adresu URL i wyodrębniając
  atrybut href z tagów link. Krok po kroku kod w Pythonie, aby szybko pobrać ikony
  stron internetowych.
draft: false
keywords:
- how to get favicon
- load html from url
- get website icons
- extract href from link
- how to extract favicons
language: pl
og_description: 'Jak szybko uzyskać favicon: załaduj HTML z URL, znajdź link rel=''icon''
  i wyodrębnij href z tagów link przy użyciu Pythona.'
og_title: Jak pobrać favicon – samouczek Pythona
schemas:
- author: Aspose
  dateModified: '2026-06-26'
  description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  headline: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  type: TechArticle
- description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  name: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  steps:
  - name: What if the site uses a `<meta>` tag instead of `<link>`?
    text: Some older pages embed the icon URL in a `<meta name="msapplication‑TileImage">`.
      You can extend `find_icon_links` to also search for those meta tags and treat
      them the same way.
  - name: How do I handle relative URLs that start with `//`?
    text: '`urljoin` automatically resolves protocol‑relative URLs (`//example.com/favicon.ico`)
      based on the scheme of the base URL, so you don’t need extra logic.'
  - name: Can I retrieve multiple sizes (e.g., 32×32, 180×180) automatically?
    text: Yes—just drop the `filter_ico_urls` step. The script will return every icon
      URL it discovers, including PNGs of various dimensions. You can then sort or
      select based on the filename pattern.
  - name: Does this work on sites that block bots?
    text: 'If a site returns a 403 or requires a custom User‑Agent, tweak the `requests.get`
      call:'
  type: HowTo
tags:
- Python
- Web Scraping
- HTML Parsing
title: Jak pobrać favicon – Kompletny przewodnik Pythona dotyczący wyodrębniania ikon
  witryn
url: /pl/python/general/how-to-get-favicon-complete-python-guide-for-extracting-site/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak uzyskać favicon – Kompletny przewodnik Pythona po pobieraniu ikon witryn

Kiedykolwiek zastanawiałeś się **how to get favicon** z dowolnej strony bez ręcznego przeszukiwania źródła? Nie jesteś jedyny — programiści, specjaliści SEO i nawet projektanci często potrzebują tej małej ikony reprezentującej witrynę. W tym samouczku pokażemy czysty, skoncentrowany na Pythonie sposób na wczytanie HTML z URL, odnalezienie tagów `<link rel="icon">` i wyciągnięcie adresów ikon. Po zakończeniu dokładnie będziesz wiedział **how to get favicon** dla dowolnej domeny i będziesz miał gotowy skrypt do ponownego użycia w swoich projektach.

Omówimy wszystko, od pobierania HTML po obsługę przypadków brzegowych, takich jak względne URL‑e i wiele formatów ikon. Nie potrzebujesz zewnętrznych usług — wystarczy standardowa biblioteka `requests` i lekki parser HTML. Gotowy, aby rozpocząć? Zanurzmy się.

## Wymagania wstępne

- Zainstalowany Python 3.8+ (kod działa również na 3.10)  
- Podstawowa znajomość `requests` i wyrażeń listowych (list comprehensions)  
- Dostęp do Internetu dla docelowej witryny  

Jeśli już masz te elementy, świetnie — przejdź do pierwszego kroku. W przeciwnym razie zainstaluj jedyną potrzebną zależność:

```bash
pip install requests beautifulsoup4
```

> **Pro tip:** `beautifulsoup4` jest sprawdzonym parserem, który sprawia, że „load html from url” to bułka z masłem.

## Krok 1: Wczytaj HTML z URL przy użyciu Pythona  

Pierwszą rzeczą, którą musisz zrobić, ucząc się **how to get favicon**, jest pobranie źródła strony. To jest część „load html from url” procesu.

```python
import requests
from bs4 import BeautifulSoup

def fetch_html(url: str) -> str:
    """Download the raw HTML of *url* and return it as text."""
    response = requests.get(url, timeout=10)
    response.raise_for_status()   # will raise if the request failed
    return response.text
```

Dlaczego używać `requests`? Automatycznie obsługuje przekierowania, weryfikację HTTPS i timeouty, co oznacza mniej niespodzianek, gdy później spróbujesz **get website icons**.

## Krok 2: Przeanalizuj dokument i znajdź linki do ikon  

Teraz, gdy mamy HTML, musimy zlokalizować wszystkie elementy `<link>`, których atrybut `rel` wskazuje na ikonę. To jest sedno **how to get favicon**.

```python
def find_icon_links(html: str) -> list[BeautifulSoup]:
    """Return a list of <link> tags that declare an icon."""
    soup = BeautifulSoup(html, "html.parser")
    # Look for rel="icon" or rel="shortcut icon"
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]
```

Zauważ, że sprawdzamy zarówno `icon`, jak i `shortcut icon`, ponieważ starsze witryny nadal używają tego drugiego. Ta mała niuans często sprawia problemy, gdy ludzie szukają „how to extract favicons”.

## Krok 3: Wyodrębnij href z elementów link  

Mając odpowiednie tagi, kolejny logiczny krok — **extract href from link** — jest prosty.

```python
from urllib.parse import urljoin

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    """Convert each <link> tag’s href into a full absolute URL."""
    urls = []
    for tag in link_tags:
        href = tag.get("href")
        if href:
            # Resolve relative URLs against the base page
            full_url = urljoin(base_url, href)
            urls.append(full_url)
    return urls
```

Użycie `urljoin` zapewnia, że nawet jeśli witryna podaje względną ścieżkę, taką jak `/favicon.ico`, otrzymasz prawidłowy bezwzględny URL — kluczowe dla niezawodnego skryptu **how to get favicon**.

## Krok 4: Opcjonalnie – Walidacja i filtrowanie URL‑ów ikon  

Czasami strona wymienia wiele ikon (Apple touch icons, PNG‑y różnych rozmiarów itp.). Jeśli zależy Ci tylko na klasycznym pliku `.ico`, przefiltruj odpowiednio. Ten krok pokazuje **how to extract favicons** określonego typu.

```python
def filter_ico_urls(urls: list[str]) -> list[str]:
    """Keep only URLs that end with .ico (case‑insensitive)."""
    return [u for u in urls if u.lower().endswith(".ico")]
```

Śmiało modyfikuj filtr: zamień `".ico"` na `".png"` lub sprawdź `rel="apple-touch-icon"`, jeśli potrzebujesz ikon wysokiej rozdzielczości.

## Krok 5: Pobierz pliki ikon (jeśli chcesz rzeczywisty obraz)  

Wyodrębnienie URL‑ów to dopiero połowa walki; pobranie daje plik, który możesz wyświetlić lub przechować. Oto szybki pomocnik:

```python
import os

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    """Save each icon to *folder*, creating it if necessary."""
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")
```

Uruchomienie tego po poprzednich krokach daje lokalną kopię każdej znalezionej favicon, idealną do buforowania lub analizy offline.

## Krok 6: Złożenie wszystkiego razem — pełny działający przykład  

Poniżej znajduje się kompletny, gotowy do uruchomienia skrypt, który demonstruje **how to get favicon** z dowolnej witryny. Skopiuj‑wklej, zmień `target_url` i obserwuj wynik.

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin
import os

def fetch_html(url: str) -> str:
    response = requests.get(url, timeout=10)
    response.raise_for_status()
    return response.text

def find_icon_links(html: str) -> list[BeautifulSoup]:
    soup = BeautifulSoup(html, "html.parser")
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    return [urljoin(base_url, tag.get("href")) for tag in link_tags if tag.get("href")]

def filter_ico_urls(urls: list[str]) -> list[str]:
    return [u for u in urls if u.lower().endswith(".ico")]

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")

def get_favicons(target_url: str) -> None:
    print(f"Fetching HTML from {target_url} …")
    html = fetch_html(target_url)

    print("Finding <link> tags that declare icons …")
    icon_tags = find_icon_links(html)

    print(f"Extracting href attributes – {len(icon_tags)} candidates found.")
    raw_urls = extract_icon_urls(target_url, icon_tags)

    # Optional filtering – keep only .ico files
    ico_urls = filter_ico_urls(raw_urls)
    print(f"Filtered to {len(ico_urls)} .ico URLs:", ico_urls)

    if ico_urls:
        download_icons(ico_urls)
    else:
        print("No .ico favicons detected; here are all discovered URLs:")
        print(raw_urls)

# Example usage – replace with any site you want to test
if __name__ == "__main__":
    target_url = "https://www.python.org"
    get_favicons(target_url)
```

**Oczekiwany wynik (skrócony dla zwięzłości):**

```
Fetching HTML from https://www.python.org …
Finding <link> tags that declare icons …
Extracting href attributes – 3 candidates found.
Filtered to 1 .ico URLs: ['https://www.python.org/static/favicon.ico']
Saved favicons/favicon.ico
```

Jeśli witryna udostępnia tylko PNG lub Apple touch icons, skrypt wypisze te URL‑e zamiast, pokazując dokładnie **how to get favicon** w każdym scenariuszu.

## Częste pytania i przypadki brzegowe  

### Co jeśli witryna używa tagu `<meta>` zamiast `<link>`?  
Niektóre starsze strony osadzają URL ikony w `<meta name="msapplication‑TileImage">`. Możesz rozszerzyć `find_icon_links`, aby także przeszukiwać te meta‑tagi i traktować je tak samo.

### Jak obsłużyć względne URL‑e zaczynające się od `//`?  
`urljoin` automatycznie rozwiązuje protokół‑względne URL‑e (`//example.com/favicon.ico`) na podstawie schematu bazowego URL, więc nie potrzebujesz dodatkowej logiki.

### Czy mogę automatycznie pobrać wiele rozmiarów (np. 32×32, 180×180)?  
Tak — po prostu pomiń krok `filter_ico_urls`. Skrypt zwróci każdy URL ikony, który znajdzie, w tym PNG‑y różnych wymiarów. Następnie możesz posortować lub wybrać na podstawie wzorca nazwy pliku.

### Czy to działa na stronach blokujących boty?  
Jeśli strona zwraca 403 lub wymaga niestandardowego User‑Agent, zmodyfikuj wywołanie `requests.get`:

```python
headers = {"User-Agent": "Mozilla/5.0 (compatible; FaviconBot/1.0)"}
response = requests.get(url, headers=headers, timeout=10)
```

Ta mała zmiana często rozwiązuje problem „how to get favicon” na bardziej restrykcyjnych domenach.

## Przegląd wizualny  

![Diagram przedstawiający przepływ procesu uzyskiwania favicon z witryny – wczytanie HTML, parsowanie tagów link, wyodrębnienie href, opcjonalne pobranie](how-to-get-favicon-diagram.png "diagram przepływu uzyskiwania favicon")

*Tekst alternatywny obrazu zawiera główne słowo kluczowe, spełniając wymogi SEO dla obrazów.*

## Zakończenie  

Przeszliśmy krok po kroku przez **how to get favicon**: wczytywanie HTML z URL,

## Co powinieneś nauczyć się dalej?

Następujące samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak zapisać HTML w C# – Kompletny przewodnik z użyciem własnego obsługiwacza zasobów](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Jak edytować HTML przy użyciu Aspose.HTML dla Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Jak konwertować HTML do PDF w Java – przy użyciu Aspose.HTML dla Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}