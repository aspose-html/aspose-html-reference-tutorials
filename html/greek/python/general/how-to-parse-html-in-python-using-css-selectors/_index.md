---
category: general
date: 2026-10-21
description: Μάθετε πώς να αναλύετε HTML με Python, να φορτώνετε ένα έγγραφο HTML,
  να χρησιμοποιείτε επιλεκτές CSS και να εξάγετε γρήγορα υπερσυνδέσμους από το HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to parse html
- how to use selector
- extract hyperlinks from html
- load html document python
language: el
lastmod: 2026-10-21
og_description: Πώς να αναλύσετε HTML σε Python χρησιμοποιώντας επιλεκτές CSS. Φορτώστε
  ένα έγγραφο HTML, επιλέξτε συνδέσμους και εξάγετε υπερσυνδέσμους από το HTML με
  καθαρό κώδικα.
og_image_alt: Screenshot showing how to parse HTML in Python with CSS selectors
og_title: Πώς να αναλύσετε HTML με Python – οδηγός βήμα‑βήμα
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
title: Πώς να αναλύσετε HTML στην Python χρησιμοποιώντας CSS selectors
url: /el/python/general/how-to-parse-html-in-python-using-css-selectors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αναλύσετε HTML σε Python χρησιμοποιώντας CSS selectors

Αν χρειάζεστε **how to parse html** σε ένα script Python, αυτός ο οδηγός σας δείχνει ακριβώς πώς. Θα μάθετε πώς να φορτώνετε ένα έγγραφο HTML, πώς να χρησιμοποιείτε τη σύνταξη selector για να βρίσκετε στοιχεία, και πώς να εξάγετε υπερσυνδέσμους από html χωρίς να γράψετε προσαρμοσμένο parser.

Η ανάλυση HTML είναι μια κοινή εργασία για web scrapers, pipelines ανάλυσης δεδομένων ή αυτοματοποιημένες δοκιμές. Στο τέλος αυτού του tutorial θα έχετε μια επαναχρησιμοποιήσιμη συνάρτηση που φορτώνει ένα έγγραφο HTML, επιλέγει όλα τα `<a>` tags με έναν CSS selector, και επιστρέφει μια καθαρή λίστα URLs.

## Τι θα χρειαστείτε

- Python 3.8+ (ο κώδικας λειτουργεί σε οποιαδήποτε πρόσφατη έκδοση)  
- Η βιβλιοθήκη **lxml** (`pip install lxml`) – παρέχει γρήγορη ανάλυση HTML και υποστήριξη CSS selectors  
- Ένα αρχείο HTML που θέλετε να αναλύσετε (π.χ., `sample.html`)  

Δεν απαιτούνται πρόσθετα εργαλεία· όλα τρέχουν με τη standard library και ένα τρίτο πακέτο.

## Βήμα 1: Πώς να αναλύσετε HTML – φόρτωση του εγγράφου

Το πρώτο βήμα σε οποιαδήποτε ροή εργασίας HTML είναι η ανάγνωση του αρχείου στη μνήμη. Η χρήση του **lxml.html** σας δίνει ένα αντικείμενο δέντρου που υποστηρίζει CSS selectors.

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

**Γιατί είναι σημαντικό:**  
`load_html` αφαιρεί το boilerplate της ανάγνωσης αρχείου και εγγυάται ότι το έγγραφο αναλύεται με έναν ανεκτικό HTML parser. Αυτός είναι ο πιο ασφαλής τρόπος για **load html document python** χωρίς να ανησυχείτε για κακοσχηματισμένο markup.

## Βήμα 2: Πώς να χρησιμοποιήσετε selector – εύρεση όλων των στοιχείων link

Μόλις το έγγραφο φορτωθεί, μπορείτε να χρησιμοποιήσετε έναν CSS selector για να εντοπίσετε κάθε `<a>` tag. Ο selector `"a"` ταιριάζει με όλα τα anchor elements, αλλά μπορείτε να τον περιορίσετε (π.χ., `"a.external"` ή `"nav a"`).

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

**Γιατί είναι σημαντικό:**  
Η προσέγγιση **how to use selector** σας επιτρέπει να εκφράζετε σύνθετα ερωτήματα σε μια μόνο, αναγνώσιμη συμβολοσειρά, αποφεύγοντας την χειροκίνητη διέλευση του δέντρου. Λειτουργεί για οποιοδήποτε CSS pattern υποστηρίζεται από `lxml.cssselect`.

## Βήμα 3: Εξαγωγή υπερσυνδέσμων από HTML και επεξεργασία τους

Τώρα που έχετε μια λίστα με στοιχεία `<a>`, μπορείτε να εξάγετε το attribute `href` από το καθένα. Ο βοηθός παρακάτω επίσης κανονικοποιεί σχετικές URLs έναντι μιας base URL (αν την παρέχετε).

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

**Αναμενόμενη έξοδος** (υποθέτοντας ότι το `sample.html` περιέχει τρεις συνδέσμους):

```
https://example.com/page1.html
https://example.com/page2.html
https://external.org/resource
```

**Γιατί είναι σημαντικό:**  
`extract_hyperlinks` είναι ο πυρήνας του **extract hyperlinks from html**. Διαχειρίζεται κομψά τα ελλιπή attributes `href`, επιλύει σχετικούς συνδέσμους, και επιστρέφει μια απλή λίστα Python που μπορείτε να περάσετε σε περαιτέρω επεξεργασία (π.χ., requests, pandas ή μια βάση δεδομένων).

## Πλήρες παράδειγμα από‑αρχή‑μέχρι‑τέλος

Συνδυάζοντας τις τρεις συναρτήσεις παίρνετε ένα ενιαίο script που φορτώνει ένα αρχείο, επιλέγει όλα τα anchors, και εκτυπώνει κάθε υπερσύνδεσμο.

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

Η εκτέλεση `python parse_links.py` εκτυπώνει κάθε υπερσύνδεσμο, πλήρως επιλυμένο, στην κονσόλα. Αυτό το script δείχνει **how to parse html**, **how to use selector**, και **extract hyperlinks from html** σε μια ενιαία, επαναχρησιμοποιήσιμη ροή.

## Συνηθισμένες παραλλαγές και διαχείριση edge‑case

| Situation | What to change | Reason |
|-----------|----------------|--------|
| **Only absolute URLs needed** | Omit the `base_url` argument in `extract_hyperlinks` | Keeps relative URLs untouched |
| **You need the link text as well** | Return a tuple `(href, link.text_content())` from `extract_hyperlinks` | Allows you to store both URL and anchor text |
| **Large HTML files** | Use `lxml.etree.iterparse` with a CSS selector filter | Reduces memory usage by streaming |
| **Different selector** | Replace `"a"` with `"nav a[href]"` or `"div.content a.external"` | Targets a subset of links, useful for **how to use selector** in complex pages |

**Pro tip:** Πάντα να επικυρώνετε τα εξαγόμενα URLs πριν κάνετε network requests. Μια γρήγορη έλεγχος με `urlparse` μπορεί να φιλτράρει κακοσχηματισμένες συμβολοσειρές και να προστατεύσει το scraper σας από crashes.

## Συμπέρασμα

Τώρα ξέρετε **how to parse html** σε Python, πώς να **load html document python**, πώς να **how to use selector** για στόχευση στοιχείων, και πώς να **extract hyperlinks from html** αποδοτικά. Το πλήρες παράδειγμα παραπάνω είναι έτοιμο για copy‑paste στο πρότζεκτ σας, και μπορείτε να προσαρμόσετε κάθε συνάρτηση για πιο προχωρημένες περιπτώσεις χρήσης όπως pagination, περιεχόμενο που δημιουργείται από JavaScript, ή crawling πολλαπλών σελίδων.

Επόμενα βήματα που μπορεί να εξερευνήσετε:

- Χρήση του **requests‑html** ή **Playwright** για λήψη σελίδων που απαιτούν εκτέλεση JavaScript.  
- Αποθήκευση των εξαγόμενων URLs σε CSV ή SQLite database για μεταγενέστερη ανάλυση.  
- Προσθήκη διαχείρισης σφαλμάτων για time‑outs δικτύου και κωδικούς κατάστασης HTTP.

Καλή ανάλυση, και μη διστάσετε να πειραματιστείτε με διαφορετικούς selectors για να αξιοποιήσετε πλήρως τη δύναμη των CSS‑based HTML ερωτημάτων σε Python!

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to configure HTML resource handling in Python and load an HTML document](/html/english/python/general/how-to-configure-html-resource-handling-in-python-and-load-a/)
- [How to Parse HTML in Python – Complete Guide](/html/english/python/general/how-to-parse-html-in-python-complete-guide/)
- [How to Load HTML in Python – Step‑by‑Step Guide](/html/english/python/general/how-to-load-html-in-python-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}