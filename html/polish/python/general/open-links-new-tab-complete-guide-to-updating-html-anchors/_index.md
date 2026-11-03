---
category: general
date: 2026-07-05
description: Otwieraj linki w nowej karcie przy użyciu Pythona – dowiedz się, jak
  dodać target='_blank', zmienić docelowy adres linku, używać selektora zawierającego
  atrybut oraz łatwo zapisywać zmodyfikowany HTML.
draft: false
keywords:
- open links new tab
- add target blank
- change link target
- attribute contains selector
- save modified html
language: pl
og_description: Szybko otwieraj linki w nowej karcie. Ten tutorial pokazuje, jak dodać target="_blank",
  zmienić docelowy link i zapisać zmodyfikowany HTML przy użyciu Pythona.
og_title: Otwieranie linków w nowej karcie – Przewodnik krok po kroku aktualizacji
  HTML
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  headline: Open Links New Tab – Complete Guide to Updating HTML Anchors
  type: TechArticle
- description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  name: Open Links New Tab – Complete Guide to Updating HTML Anchors
  steps:
  - name: Expected Result
    text: 'Suppose `links.html` originally contained:'
  - name: What if a link already has a `rel` attribute?
    text: 'Our loop overwrites it with `"noopener"`. If you need to preserve existing
      values (e.g., `"nofollow"`), concatenate instead:'
  - name: How to handle multiple domains?
    text: 'Just expand the selector list:'
  - name: Does `prettify()` change the original HTML structure?
    text: It re‑indents but doesn’t alter tag order or attribute values. If you must
      keep the exact original whitespace, replace `prettify()` with `str(soup)` as
      mentioned earlier.
  type: HowTo
tags:
- HTML manipulation
- Python
- web automation
title: Otwieranie linków w nowej karcie – Kompletny przewodnik po aktualizacji kotwic
  HTML
url: /pl/python/general/open-links-new-tab-complete-guide-to-updating-html-anchors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Otwieranie linków w nowej karcie – Kompletny przewodnik po aktualizacji kotwic HTML

Czy kiedykolwiek potrzebowałeś **otworzyć linki w nowej karcie** na statycznej stronie HTML, ale nie wiedziałeś, od czego zacząć? Nie jesteś sam. Wielu programistów napotyka ten problem przy czyszczeniu starszych witryn lub dodawaniu poprawek dostępności. W tym samouczku przeprowadzimy praktyczne rozwiązanie, które **dodaje target blank**, **zmienia docelowy link**, i bezpiecznie **zapisuje zmodyfikowany html** — wszystko w kilku linijkach Pythona.

Omówimy także, jak używać **attribute contains selector**, aby modyfikować tylko te kotwice, które naprawdę Cię interesują (na przykład każdy link prowadzący do *example.com*). Po zakończeniu będziesz mieć skrypt, który możesz wstawić do dowolnego projektu, niezależnie od jego rozmiaru.

## Czego się nauczysz

- Wczytaj plik HTML do manipulowalnego obiektu dokumentu.  
- Wybierz elementy `<a>`, których atrybut `href` zawiera określony podciąg.  
- **Add target blank** i ustaw atrybut `rel="noopener"` w celu zwiększenia bezpieczeństwa.  
- **Save modified html** z powrotem na dysk bez utraty formatowania.  

Nie potrzebujesz zewnętrznych zależności poza standardową biblioteką i **beautifulsoup4** (mała instalacja). Jeśli używasz innego parsera, koncepcje działają bezpośrednio.

---

## Wymagania wstępne

- Python 3.8+ zainstalowany na Twoim komputerze.  
- Podstawowa znajomość HTML i Pythona.  
- Pakiet `beautifulsoup4` (`pip install beautifulsoup4`).  

To wszystko — nie są potrzebne ciężkie frameworki.

---

## Krok 1: Wczytaj dokument HTML

Najpierw musimy odczytać plik źródłowy i przekazać go do BeautifulSoup. Pomyśl o tym jak o otwarciu pustego płótna, na którym możesz rysować nowe atrybuty.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Path to the original HTML file
html_path = Path("YOUR_DIRECTORY/links.html")

# Read the file content
with html_path.open(encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")
```

> **Why this matters:** Using `Path` keeps the code OS‑agnostic, and `html.parser` is built‑in, so you don’t need extra parsers for simple tasks.

---

## Krok 2: Użyj selektora zawierającego atrybut, aby znaleźć właściwe linki

Chcemy modyfikować tylko te kotwice, które prowadzą do *example.com*. Selektor CSS `a[href*='example.com']` robi dokładnie to — `*=` oznacza „zawiera”. Metoda `select` w BeautifulSoup rozumie tę składnię.

```python
# Find all <a> tags whose href contains 'example.com'
selector = "a[href*='example.com']"
anchor_elements = soup.select(selector)
```

> **Pro tip:** If you need a case‑insensitive match, switch to a small loop that checks `if 'example.com' in a.get('href', '').lower()`.

Teraz `anchor_elements` zawiera wszystkie linki, które nas interesują, gotowe do kolejnej transformacji.

---

## Krok 3: Zmień docelowy link – dodaj target blank i zabezpiecz link

Otwieranie linku w nowej karcie jest tak proste, jak ustawienie `target="_blank"`. Jednak nowoczesne przeglądarki zalecają także dodanie `rel="noopener"` (lub `noreferrer`), aby zapobiec dostępowi nowo otwartej strony do oryginalnego okna poprzez `window.opener`. Ten mały zabieg bezpieczeństwa może powstrzymać ataki phishingowe.

```python
for anchor in anchor_elements:
    # Open in a new tab
    anchor['target'] = "_blank"          # add target blank
    # Harden security
    anchor['rel'] = "noopener"           # prevent access to the opener page
```

> **Why we use direct dictionary assignment:** It automatically creates the attribute if it’s missing, and overwrites it if it already exists—perfect for a **change link target** operation.

---

## Krok 4: Zapisz zmodyfikowany HTML na dysku

Ostatnim krokiem jest zapisanie zaktualizowanego kodu do nowego pliku. Pozostawienie oryginału nietkniętego pozwala na cofnięcie zmian, jeśli coś pójdzie nie tak.

```python
# Destination path for the updated HTML
output_path = Path("YOUR_DIRECTORY/links-updated.html")

# Write the prettified HTML (preserves indentation)
with output_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())
```

> **What `prettify()` does:** It formats the HTML with nice indentation, making the saved file easier to read and diff later. If you prefer the original whitespace, replace `prettify()` with `str(soup)`.

---

## Pełny skrypt – rozwiązanie jednym kliknięciem

Poniżej znajduje się kompletny, gotowy do uruchomienia skrypt. Zapisz go jako `update_links.py` i uruchom `python update_links.py` w terminalu.

```python
#!/usr/bin/env python3
"""
Open Links New Tab – script that adds target blank,
sets rel="noopener", and saves modified html.
"""

from pathlib import Path
from bs4 import BeautifulSoup

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Load the HTML document
    # ------------------------------------------------------------------
    html_path = Path("YOUR_DIRECTORY/links.html")
    with html_path.open(encoding="utf-8") as f:
        soup = BeautifulSoup(f, "html.parser")

    # ------------------------------------------------------------------
    # 2️⃣ Select anchors with an attribute contains selector
    # ------------------------------------------------------------------
    selector = "a[href*='example.com']"
    anchors = soup.select(selector)

    # ------------------------------------------------------------------
    # 3️⃣ Change link target – add target blank & secure the link
    # ------------------------------------------------------------------
    for a in anchors:
        a['target'] = "_blank"          # add target blank
        a['rel'] = "noopener"           # prevent opener access

    # ------------------------------------------------------------------
    # 4️⃣ Save modified html to a new file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/links-updated.html")
    with output_path.open("w", encoding="utf-8") as f:
        f.write(soup.prettify())

    print(f"✅ Updated {len(anchors)} link(s) and saved to {output_path}")

if __name__ == "__main__":
    main()
```

### Oczekiwany rezultat

Załóżmy, że `links.html` pierwotnie zawierał:

```html
<a href="https://example.com/page1">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Po uruchomieniu skryptu, `links-updated.html` będzie wyglądał tak:

```html
<a href="https://example.com/page1" target="_blank" rel="noopener">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Tylko link do *example.com* otrzymał atrybuty **add target blank**, co pokazuje, że nasz **attribute contains selector** działał dokładnie tak, jak zamierzono.

---

## Często zadawane pytania i przypadki brzegowe

### Co zrobić, jeśli link już ma atrybut `rel`?

Nasza pętla nadpisuje go wartością `"noopener"`. Jeśli musisz zachować istniejące wartości (np. `"nofollow"`), połącz je zamiast tego:

```python
existing = a.get('rel', '')
a['rel'] = f"{existing} noopener".strip()
```

### Jak obsłużyć wiele domen?

Po prostu rozbuduj listę selektorów:

```python
domains = ["example.com", "sample.org"]
selector = ",".join([f"a[href*='{d}']" for d in domains])
anchors = soup.select(selector)
```

### Czy `prettify()` zmienia oryginalną strukturę HTML?

Ponownie wcięcie, ale nie zmienia kolejności tagów ani wartości atrybutów. Jeśli musisz zachować dokładnie oryginalne białe znaki, zamień `prettify()` na `str(soup)` jak wspomniano wcześniej.

---

## Pro tipy dla skryptów gotowych do produkcji

- **Backup before overwriting:** Add a copy step (`shutil.copy`) to keep the original file safe.  
- **Logging instead of print:** Use the `logging` module for scalable projects.  
- **Batch processing:** Loop over a directory with `Path.rglob("*.html")` to update many files in one run.  

These tweaks turn a simple **open links new tab** script into a robust utility for any web‑maintenance workflow.

---

## Zakończenie

Masz teraz solidną, wielokrotnego użytku metodę do **open links new tab** w dowolnej kolekcji statycznych plików HTML. Dzięki wykorzystaniu **attribute contains selector** możesz **change link target** dokładnie tam, gdzie tego potrzebujesz, **add target blank** i **save modified html** bez utraty formatowania. 

Wypróbuj to na stronie testowej, a potem zastosuj na całej witrynie. Potrzebujesz dostosować selektor dla plików PDF, obrazów lub innych domen? Po prostu zmień ciąg CSS — wszystko inne pozostaje bez zmian.

Śmiało zostaw komentarz, jeśli napotkasz problemy, lub podziel się, jak rozbudowałeś skrypt w swoich projektach. Szczęśliwego kodowania i niech wszystkie Twoje kotwice otwierają się dokładnie tam, gdzie chcesz!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu z krok po kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak edytować HTML przy użyciu Aspose.HTML dla Javy](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Jak dodać CSS – CSS inline do dokumentów HTML w Aspose.HTML dla Javy](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}