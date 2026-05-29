---
category: general
date: 2026-05-28
description: Jak szybko parsować HTML w Pythonie — wczytać plik HTML, użyć selektora
  CSS i wyodrębnić atrybuty href przy użyciu przykładu XPath contains.
draft: false
keywords:
- how to parse html
- get href attribute
- load html file
- use css selector
- xpath contains example
language: pl
og_description: 'Jak parsować HTML w Pythonie: dowiedz się, jak wczytać plik HTML,
  używać selektorów CSS i pobierać atrybuty href przy użyciu przykładu XPath contains.'
og_title: Jak parsować HTML w Pythonie – krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  headline: How to Parse HTML in Python – Complete Guide
  type: TechArticle
- description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  name: How to Parse HTML in Python – Complete Guide
  steps:
  - name: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
    text: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
  - name: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
    text: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
  - name: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
    text: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
  - name: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
    text: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
  type: HowTo
tags:
- html parsing
- python
- web scraping
title: Jak parsować HTML w Pythonie – Kompletny przewodnik
url: /pl/python/general/how-to-parse-html-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak parsować HTML w Pythonie – Kompletny przewodnik

Zastanawiałeś się kiedyś, **jak parsować HTML** w skrypcie Pythona bez wciągania ciężkiej przeglądarki? Nie jesteś sam. Większość z nas potrzebuje tylko **załadować plik HTML**, wyciągnąć kilka nagłówków i może pobrać jeden‑dwa linki do pobrania. W tym tutorialu pokażę dokładnie to — przy użyciu małej biblioteki, selektora CSS i przykładu XPath contains, aby **pobrać wartości atrybutu href**.

Przejdziemy przez cały proces, od odczytania lokalnego dokumentu HTML po wypisanie danych, które Cię interesują. Bez zbędnego balastu, tylko praktyczny, działający przykład, który możesz od razu wstawić do własnego projektu.

## Co się nauczysz

- Jak **załadować plik HTML** przy użyciu lekkiego parsera.  
- Jak **używać składni selektora CSS** do pobierania elementów, takich jak nagłówki artykułów.  
- Jak stworzyć **przykład XPath contains**, który filtruje linki.  
- Jak bezpiecznie **pobrać wartości atrybutu href** z dopasowanych węzłów.  
- Wskazówki dotyczące obsługi niepoprawnego markupu i rozbudowy skryptu.

Wystarczy Python 3.8+ oraz pakiety `lxml` i `cssselect` — oba instalowalne jednym poleceniem `pip`.

---

## Krok 1: Załaduj plik HTML

Zanim cokolwiek zrobisz, potrzebujesz treści HTML w pamięci. Moduł `lxml.html` udostępnia wygodny pomocnik `fromstring`, ale gdy masz plik na dysku, funkcja `parse` jest jeszcze czytelniejsza.

```python
# Step 1: Load the HTML file
from lxml import html

# Replace the path with the location of your HTML document
html_path = "YOUR_DIRECTORY/news.html"
doc = html.parse(html_path)

# The root element gives us access to CSS and XPath methods
root = doc.getroot()
```

> **Dlaczego to ważne:** Załadowanie pliku raz utrzymuje niskie zużycie pamięci i daje Ci pojedynczy obiekt `root`, który obsługuje zarówno selektory CSS, jak i zapytania XPath. Jeśli plik jest nieobecny lub nieczytelny, `html.parse` podniesie czytelny `OSError`, który możesz przechwycić później.

### Wskazówka
Jeśli pracujesz ze stringiem zamiast z plikiem, zamień `html.parse` na `html.fromstring(your_html_string)`.

---

## Krok 2: Użyj selektora CSS, aby pobrać nagłówki

Selektory CSS są zwięzłe i znane każdemu, kto pisał arkusz stylów. Pobierzmy wszystkie `<h2>` wewnątrz `<article>` — idealne dla nagłówków wiadomości.

```python
# Step 2: Find all article headlines using a CSS selector
headline_nodes = root.cssselect("article h2")

# Print each headline's text content
for node in headline_nodes:
    print(node.text_content().strip())
```

**Oczekiwany wynik** (zakładając, że przykładowy HTML zawiera dwa artykuły):

```
Breaking News: Python Takes Over the World
Local Developer Solves HTML Parsing Puzzle
```

> **Dlaczego CSS?** Jest czytelny, szybki i działa od ręki z `lxml`. Metoda `cssselect` pod maską tłumaczy selektor na wyrażenie XPath, dając Ci to, co najlepsze z obu światów.

---

## Krok 3: Przykład XPath contains – znajdź linki „download”

Czasami potrzebna jest bardziej szczegółowa kontrola niż oferuje CSS. Funkcja `contains()` w XPath błyszczy, gdy chcesz dopasować podciąg w atrybucie, np. wszystkie linki prowadzące do pobrania.

```python
# Step 3: Find all links that contain the word "download" using XPath
download_link_nodes = root.xpath("//a[contains(@href, 'download')]")

# Extract and print the href attribute from each matching node
for node in download_link_nodes:
    href = node.get("href")
    print(href)
```

**Przykładowy wynik**:

```
/files/report_download.pdf
https://example.com/downloads/setup.exe
```

> **Dlaczego XPath contains?** Pozwala filtrować bezpośrednio na wartościach atrybutów, bez dodatkowych pętli w Pythonie. To klasyczny **xpath contains example**, który często pojawia się w tutorialach, ale tutaj jest połączony z rzeczywistym przypadkiem użycia.

---

## Krok 4: Zawiń wszystko w funkcję wielokrotnego użytku

Hard‑kodowanie ścieżek i `print`‑ów jest w porządku dla szybkiego testu, ale kod produkcyjny lubi funkcje. Poniżej kompaktowy helper, który zwraca zarówno nagłówki, jak i linki do pobrania.

```python
def parse_news_html(file_path):
    """
    Parse a news HTML file and return headlines plus download URLs.

    Parameters
    ----------
    file_path : str
        Path to the local HTML document.

    Returns
    -------
    dict
        {
            "headlines": list of strings,
            "download_links": list of href strings
        }
    """
    doc = html.parse(file_path)
    root = doc.getroot()

    # Headlines via CSS selector
    headlines = [
        node.text_content().strip()
        for node in root.cssselect("article h2")
    ]

    # Download links via XPath contains
    download_links = [
        node.get("href")
        for node in root.xpath("//a[contains(@href, 'download')]")
    ]

    return {"headlines": headlines, "download_links": download_links}
```

Teraz możesz wywołać funkcję i ładnie wydrukować wyniki:

```python
if __name__ == "__main__":
    results = parse_news_html("YOUR_DIRECTORY/news.html")
    print("Headlines:")
    for h in results["headlines"]:
        print(f"- {h}")

    print("\nDownload Links:")
    for link in results["download_links"]:
        print(f"- {link}")
```

Uruchomienie skryptu daje ten sam wynik co wcześniej, ale teraz jest elegancko spakowane do ponownego użycia.

---

## Krok 5: Obsługa przypadków brzegowych i typowych pułapek

1. **Brak atrybutu `href`** – XPath i tak zwróci węzeł `<a>`, nawet jeśli `href` jest nieobecny. Zabezpiecz się przed `None`:

   ```python
   href = node.get("href")
   if href:
       download_links.append(href)
   ```

2. **URL‑e względne vs. bezwzględne** – Jeśli Twoje linki są względne, możesz chcieć rozwiązać je względem bazowego URL:

   ```python
   from urllib.parse import urljoin
   base_url = "https://example.com"
   absolute = urljoin(base_url, href)
   ```

3. **Niepoprawny HTML** – `lxml` jest wyrozumiały, ale ekstremalnie zepsuty markup może spowodować podniesienie `XMLSyntaxError` przez `html.parse`. Owiń wywołanie parsowania w blok `try/except`, aby zalogować i pominąć problematyczne pliki.

4. **Wydajność przy dużych plikach** – Dla stron wielokilobajtowych rozważ strumieniowanie przy pomocy `iterparse` zamiast ładowania całego DOM do pamięci.

---

## Przegląd wizualny (opcjonalnie)

![Jak parsować HTML – diagram przepływu pokazujący: załaduj plik → selektor CSS → XPath contains → pobierz atrybut href](how-to-parse-html-flow.png "Jak parsować HTML – diagram przepływu")

*Tekst alternatywny zawiera główne słowo kluczowe, aby spełnić wymagania SEO.*

---

## Zakończenie

Omówiliśmy **jak parsować HTML** w Pythonie od początku do końca: ładowanie pliku HTML, użycie selektora CSS do pobrania nagłówków artykułów, stworzenie przykładu XPath contains w celu znalezienia linków do pobrania oraz bezpieczne **pobieranie wartości atrybutu href**. Funkcja `parse_news_html` demonstruje czyste, utrzymywalne podejście, które możesz dostosować do dowolnego zadania scrapowania.

Gotowy na kolejny wyzwanie? Spróbuj rozbudować skrypt, aby:

- Parsować tabele przy użyciu zapytań XPath `//table//tr`.  
- Wyciągać atrybuty `src` obrazków, używając kolejnego **xpath contains example**.  
- Przejść na asynchroniczne pobieranie przy pomocy `aiohttp` dla stron w czasie rzeczywistym.

Szczęśliwego parsowania i pamiętaj — gdy opanujesz te podstawy, reszta scrapowania HTML stanie się bułką z masłem. Jeśli napotkasz problemy, zostaw komentarz poniżej — rozwiążemy je razem!

## Powiązane tutoriale

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}