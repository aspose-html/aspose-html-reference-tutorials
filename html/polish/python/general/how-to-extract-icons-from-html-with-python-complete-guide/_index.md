---
category: general
date: 2026-07-02
description: Jak wyodrębnić ikony z pliku HTML przy użyciu Pythona. Dowiedz się, jak
  odczytać plik HTML w Pythonie, parsować dokument HTML i wyodrębnić atrybut href,
  aby uzyskać adresy URL faviconów.
draft: false
keywords:
- how to extract icons
- read html file python
- parse html document
- extract href attribute
- extract favicon urls
language: pl
og_description: Jak wyodrębnić ikony ze strony HTML przy użyciu Pythona. Ten tutorial
  pokazuje, jak odczytać plik HTML w Pythonie, sparsować dokument i wyciągnąć adresy
  URL favikonów.
og_title: Jak wyodrębnić ikony z HTML – Przewodnik Pythona
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: How to extract icons from an HTML file using Python. Learn to read
    HTML file python, parse HTML document, and extract href attribute to get favicon
    URLs.
  headline: How to Extract Icons from HTML with Python – Complete Guide
  type: TechArticle
- questions:
  - answer: Some sites embed icons via `<meta itemprop="image">`. Extend `is_icon_link`
      to also check for `meta` with `itemprop="image"` and pull its `content` attribute.
    question: What if the HTML uses `<meta>` tags for icons?
  - answer: Yes—just feed each URL into `requests.get(url, stream=True)` and write
      the content to a file. Remember to handle relative URLs with `urljoin`.
    question: Can I fetch the icons automatically?
  - answer: 'Absolutely. Replace the file‑reading step with `requests.get(page_url).text`
      and pass the HTML string to BeautifulSoup. Just be mindful of robots.txt and
      rate limits. --- ## Wrap‑Up We’ve covered **how to extract icons** from any
      static HTML using Python, from reading the file to printing out each f'
    question: Does this work on remote pages?
  type: FAQPage
tags:
- python
- html-parsing
- web‑scraping
- favicon
title: Jak wyodrębnić ikony z HTML za pomocą Pythona – kompletny przewodnik
url: /pl/python/general/how-to-extract-icons-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyodrębnić ikony z HTML przy użyciu Pythona – Kompletny przewodnik

Zastanawiałeś się kiedyś **jak wyodrębnić ikony** ze strony internetowej bez otwierania przeglądarki? Może tworzysz katalog witryn, narzędzie do audytu SEO lub po prostu jesteś ciekawy małych favikon, które pojawiają się w kartach. Dobra wiadomość jest taka, że możesz to zrobić w kilku linijkach Pythona — bez Selenium, bez headless Chrome, po prostu w zwykłym pliku HTML.

W tym samouczku przejdziemy przez odczyt pliku HTML w Pythonie, parsowanie dokumentu HTML i w końcu **wyodrębnianie atrybutu href** z tagów `<link rel="icon">`, aby uzyskać URL‑e favikon. Po zakończeniu będziesz mieć wielokrotnego użytku fragment kodu, który działa na dowolnym statycznym HTML, który mu podasz, a także zobaczysz, jak radzić sobie z przypadkami brzegowymi, takimi jak ścieżki względne czy wiele deklaracji ikon.

## Czego się nauczysz

- Wczytaj lokalny plik HTML przy użyciu Pythona (read html file python)  
- Użyj lekkiego parsera do **parsowania dokumentu html** w bezpieczny sposób  
- Znajdź elementy `<link>`, które deklarują ikonę  
- **Wyodrębnij wartości atrybutu href** i przekształć je w absolutne URL‑e  
- Zbierz i wypisz wszystkie wykryte **URL‑e favikon**  

Nie wymagane są zewnętrzne usługi — wystarczy standardowa biblioteka i popularny pakiet **BeautifulSoup**.

---

![Zrzut ekranu pokazujący skrypt Pythona wyodrębniający ikony – jak wyodrębnić ikony](https://example.com/images/extract-icons-python.png "jak wyodrębnić ikony")

*Tekst alternatywny obrazu: "jak wyodrębnić ikony przy użyciu skryptu Pythona"*

## Wymagania wstępne

- Zainstalowany Python 3.8+  
- Biblioteka `beautifulsoup4` (`pip install beautifulsoup4`)  
- Lokalny plik HTML, który chcesz przeskanować (np. `sample.html`)  

Jeśli już je masz, przejdźmy dalej.

## Krok 1: Odczyt pliku HTML w Pythonie – Załaduj dokument

Na początek: musimy otworzyć plik i przekazać jego zawartość parserowi. Użycie `with open(..., "r", encoding="utf‑8")` zapewnia automatyczne zamknięcie pliku, a kodowanie UTF‑8 obsługuje większość nowoczesnych stron.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Step 1: Load the HTML document from disk
html_path = Path("sample.html")          # adjust the path as needed
html_content = html_path.read_text(encoding="utf-8")
```

**Dlaczego to ważne:** Otwieranie pliku z właściwym kodowaniem zapobiega tajemniczym znakom `�`, które mogłyby później zepsuć parser. Użycie `Path` ze standardowej biblioteki sprawia również, że kod jest wieloplatformowy.

## Krok 2: Parsowanie dokumentu HTML – Znajdź wszystkie linki ikon

Teraz przekazujemy surowy HTML do **BeautifulSoup**, który buduje nawigowalne drzewo. Poszukamy każdego tagu `<link>`, którego atrybut `rel` zawiera słowo `icon`. Zauważ, że `rel` może być listą oddzieloną spacjami (`rel="shortcut icon"`), więc potrzebujemy elastycznego sprawdzenia.

```python
# Step 2: Parse the HTML and locate <link> tags that declare an icon
soup = BeautifulSoup(html_content, "html.parser")

def is_icon_link(tag):
    """Return True if a <link> tag declares an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    # BeautifulSoup may return a list or a string; handle both
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

icon_links = [tag for tag in soup.find_all(is_icon_link)]
```

**Dlaczego ten krok jest kluczowy:** Naiwny `soup.find_all("link", rel="icon")` pominąłby warianty takie jak `rel="shortcut icon"` czy `rel="apple-touch-icon"`. Nasz pomocniczy `is_icon_link` obejmuje te przypadki, czyniąc wyodrębnianie solidnym.

## Krok 3: Wyodrębnianie atrybutu href – Pobieranie URL‑ów

Mając zebrane odpowiednie tagi, teraz pobieramy atrybut `href` z każdego z nich. Niektóre strony mogą pomijać `href` (rzadko, ale możliwe), więc zabezpieczamy się przed `None`. Dodatkowo favikony często są podawane jako względne URL‑e, więc rozwiążemy je względem bazowego URL‑u strony, jeśli go znasz. Dla lokalnego pliku po prostu pozostawimy ścieżkę bez zmian.

```python
# Step 3: Grab the href attribute from each icon link
icon_urls = []
for tag in icon_links:
    href = tag.get("href")
    if href:
        icon_urls.append(href.strip())
```

**Dlaczego usuwamy białe znaki:** Autorzy HTML czasami przypadkowo dodają spacje wokół URL‑ów, co mogłoby zepsuć kolejne żądanie. Przycinanie zapewnia czyste łańcuchy.

## Krok 4: Wyodrębnianie URL‑ów favikon – Wyświetlenie wyników

Na koniec wypisujemy (lub zwracamy) listę wykrytych URL‑ów. W rzeczywistym skrypcie możesz zapisać je do pliku CSV, pobrać ikony lub przekazać do innej usługi. Oto prosty pętla, która wyświetla wynik w konsoli.

```python
# Step 4: Display each discovered favicon URL
if not icon_urls:
    print("No icon links found in the document.")
else:
    for url in icon_urls:
        print("Favicon URL:", url)
```

### Obsługa przypadków brzegowych

- **Wiele wartości rel:** Nasze sprawdzenie `is_icon_link` już łapie `rel="shortcut icon"` i `rel="apple-touch-icon"`.  
- **Ścieżki względne:** Jeśli później potrzebujesz absolutnych URL‑ów, użyj `urllib.parse.urljoin(base_url, href)`.  
- **Brak href:** Zabezpieczenie `if href:` pomija nieprawidłowe tagi, unikając błędów `NoneType`.  
- **Duplikaty:** Możesz użyć `icon_urls = list(dict.fromkeys(icon_urls))`, aby usunąć duplikaty.

---

## Pełny skrypt – Kompleksowe rozwiązanie

Łącząc wszystko razem, oto kompletny, gotowy do uruchomienia program. Zapisz go jako `extract_icons.py` i wskaż `html_path` na dowolny plik, który chcesz.

```python
#!/usr/bin/env python3
"""
How to extract icons from an HTML file using Python.

This script:
- Reads an HTML file (read html file python)
- Parses the HTML document (parse html document)
- Finds <link> tags with rel containing "icon"
- Extracts the href attribute (extract href attribute)
- Prints each favicon URL (extract favicon urls)
"""

from pathlib import Path
from bs4 import BeautifulSoup

def is_icon_link(tag):
    """Detect <link> tags that declare an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

def extract_favicon_urls(html_path: Path):
    """Return a list of favicon URLs found in the given HTML file."""
    html_content = html_path.read_text(encoding="utf-8")
    soup = BeautifulSoup(html_content, "html.parser")
    icon_links = [t for t in soup.find_all(is_icon_link)]

    urls = []
    for tag in icon_links:
        href = tag.get("href")
        if href:
            urls.append(href.strip())
    # Remove duplicates while preserving order
    return list(dict.fromkeys(urls))

if __name__ == "__main__":
    # Adjust the path to point to your HTML file
    html_file = Path("sample.html")
    favicon_urls = extract_favicon_urls(html_file)

    if not favicon_urls:
        print("No icon links found in the document.")
    else:
        for url in favicon_urls:
            print("Favicon URL:", url)
```

**Oczekiwany wynik** (zakładając, że `sample.html` zawiera dwie ikony):

```
Favicon URL: /images/favicon.ico
Favicon URL: https://example.com/assets/apple-touch-icon.png
```

Uruchom go poleceniem `python extract_icons.py`, a zobaczysz wypisane URL‑y w konsoli.

---

## Najczęściej zadawane pytania

**Q: Co jeśli HTML używa tagów `<meta>` dla ikon?**  
A: Niektóre witryny osadzają ikony za pomocą `<meta itemprop="image">`. Rozszerz `is_icon_link`, aby również sprawdzał `meta` z `itemprop="image"` i wyciągał jego atrybut `content`.

**Q: Czy mogę automatycznie pobrać ikony?**  
A: Tak — po prostu przekaż każdy URL do `requests.get(url, stream=True)` i zapisz zawartość do pliku. Pamiętaj o obsłudze względnych URL‑ów przy pomocy `urljoin`.

**Q: Czy to działa na zdalnych stronach?**  
A: Zdecydowanie tak. Zastąp krok odczytu pliku wywołaniem `requests.get(page_url).text` i przekaż ciąg HTML do BeautifulSoup. Pamiętaj jednak o pliku robots.txt i limitach szybkości.

---

## Podsumowanie

Omówiliśmy **jak wyodrębnić ikony** z dowolnego statycznego HTML przy użyciu Pythona, od odczytu pliku po wypisanie każdego URL‑u favikony. Główne pomysły — odczyt pliku, parsowanie dokumentu, znajdowanie odpowiednich tagów i wyciąganie atrybutu `href` — to wielokrotnego użytku wzorce, które napotkasz w wielu zadaniach web‑scrapingu.

Następne kroki? Spróbuj rozbudować skrypt, aby:

- Rozwiązywać względne URL‑y względem bazowego URL‑u strony  
- Pobierać każdą ikonę i zapisywać ją lokalnie  
- Obsługiwać dodatkowe formaty ikon (`rel="mask-icon"` dla Safari)  

Śmiało eksperymentuj, a jeśli napotkasz problemy, zostaw komentarz poniżej. Szczęśliwego parsowania!

## Co powinieneś się nauczyć dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak zapytać HTML w Javie – Kompletny samouczek](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Jak edytować drzewo dokumentu HTML w Aspose.HTML dla Javy](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Zapisz dokument HTML do pliku w Aspose.HTML dla Javy](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}