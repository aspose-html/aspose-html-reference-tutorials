---
category: general
date: 2026-06-10
description: Φορτώστε HTML στην Python για να εξάγετε εικόνες SVG από τις σελίδες
  σας—βήμα‑βήμα κώδικας, συμβουλές και αντιμετώπιση ειδικών περιπτώσεων.
draft: false
keywords:
- load html python
- extract svg images
- extract svg from html
- search html svg
- find inline svg
language: el
og_description: Φορτώστε HTML σε Python και εξάγετε εικόνες SVG με ένα σαφές, εκτελέσιμο
  παράδειγμα. Μάθετε πώς να αναζητάτε στοιχεία SVG σε HTML και να αντιμετωπίζετε ειδικές
  περιπτώσεις.
og_title: Φόρτωση HTML σε Python – Αποδοτική εξαγωγή εικόνων SVG
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Load HTML in Python to extract SVG images from your pages—step-by-step
    code, tips, and edge‑case handling.
  headline: Load HTML in Python – Complete Guide to Extract SVG Images
  type: TechArticle
tags:
- python
- html-parsing
- svg
title: Φόρτωση HTML σε Python – Πλήρης Οδηγός για την Εξαγωγή Εικόνων SVG
url: /el/python/general/load-html-in-python-complete-guide-to-extract-svg-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Φόρτωση HTML σε Python – Πλήρης Οδηγός για Εξαγωγή Εικόνων SVG

Έχετε χρειαστεί ποτέ να **φορτώσετε HTML σε Python** μόνο για να εξάγετε κάθε γραφικό SVG από μια σελίδα; Δεν είστε οι μόνοι. Είτε χτίζετε έναν web‑scraper, δημιουργείτε μια αναφορά περιουσιακών στοιχείων, είτε απλώς θέλετε να μάθετε ποια εικονίδια χρησιμοποιεί ένας ιστότοπος, η γνώση του πώς να **εξάγετε εικόνες SVG** σας εξοικονομεί πολύ χειροκίνητη αναζήτηση.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια πρακτική, ολοκληρωμένη λύση που **φορτώνει HTML σε Python**, στη συνέχεια **αναζητά στοιχεία HTML SVG**, **βρίσκει ενσωματωμένα SVG** και ακόμη και παίρνει εξωτερικά αρχεία SVG που αναφέρονται από ετικέτες `<img>`. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο script, μερικές συμβουλές για τα πιο δύσκολα σημεία, και μια σαφή εικόνα του τι παράγει το αποτέλεσμα.

## Τι Θα Κερδίσετε

* Ένα πλήρως εκτελέσιμο script Python που αναλύει ένα τοπικό αρχείο HTML (ή μια ληφθείσα σελίδα) και καταγράφει κάθε SVG που μπορεί να βρει.  
* Κατανόηση της διαφοράς μεταξύ **ενσωματωμένου SVG** (`<svg>…</svg>`) και **εξωτερικού SVG** (`<img src="… .svg">`).  
* Στρατηγικές για τη διαχείριση κακοδιατυπωμένου markup, ελλιπών αρχείων και ιδιαιτεροτήτων namespace.  
* Ιδέες για επέκταση του κώδικα — αποθήκευση των SVG, μετατροπή τους σε PNG, ή ενσωμάτωση σε βάση δεδομένων.

### Προαπαιτούμενα

* Python 3.8+ εγκατεστημένο.  
* Βασική εξοικείωση με τις βιβλιοθήκες `requests` και `BeautifulSoup` της Python (θα τις εισάγουμε, χωρίς βαθειά εξήγηση).  
* Ένα τοπικό αρχείο HTML ή ένα URL που θέλετε να σαρώσετε.  

Τώρα, ας βουτήξουμε.

## Φόρτωση HTML σε Python – Ρύθμιση του Parser

Το πρώτο βήμα είναι να **φορτώσετε HTML σε Python**. Μπορείτε είτε να διαβάσετε ένα αρχείο από το δίσκο είτε να λάβετε μια απομακρυσμένη σελίδα. Παρακάτω υπάρχει ένας ελάχιστος, αλλά στιβαρός, βοηθός που κάνει και τα δύο:

```python
import os
import requests
from bs4 import BeautifulSoup

def load_html(source: str) -> BeautifulSoup:
    """
    Load HTML content from a file path or a URL and return a BeautifulSoup object.
    """
    if os.path.isfile(source):
        # Load from local file
        with open(source, "r", encoding="utf-8") as f:
            html = f.read()
    else:
        # Assume it's a URL and fetch it
        response = requests.get(source)
        response.raise_for_status()
        html = response.text

    # Use the html.parser for speed; switch to 'lxml' if you need extra robustness
    soup = BeautifulSoup(html, "html.parser")
    return soup
```

> **Γιατί είναι σημαντικό:** Η χρήση του `BeautifulSoup` αφαιρεί τις ιδιαιτερότητες της ακατέργαστης ανάλυσης συμβολοσειρών, και η συνάρτηση διαχειρίζεται ομαλά τόσο τοπικά αρχεία όσο και απομακρυσμένα URLs. Επιπλέον, ρίχνει εξαίρεση αν αποτύχει ένα αίτημα δικτύου — ώστε να γνωρίζετε αμέσως πότε κάτι πήγε στραβά.

## Εξαγωγή Εικόνων SVG – Εύρεση Ενσωματωμένων Στοιχείων SVG

Μόλις φορτωθεί το έγγραφο, το επόμενο λογικό βήμα είναι να **βρείτε ετικέτες ενσωματωμένου SVG**. Το ενσωματωμένο SVG είναι ενσωματωμένο απευθείας στο markup του HTML, πράγμα που σημαίνει ότι μπορείτε να το πάρετε κατευθείαν από το DOM.

```python
def collect_inline_svg(soup: BeautifulSoup) -> list:
    """
    Return a list of all inline <svg> elements as strings.
    """
    inline_svgs = []
    for svg in soup.find_all("svg"):
        # Preserve the original markup; .decode() gives us a string representation
        inline_svgs.append(str(svg))
    return inline_svgs
```

*Συμβουλή:* Αν η σελίδα χρησιμοποιεί namespaces SVG (`<svg xmlns="http://www.w3.org/2000/svg">`), το `BeautifulSoup` εξακολουθεί να βρίσκει την ετικέτα επειδή αγνοεί τα namespaces από προεπιλογή. Αυτό είναι ένα ωραίο πλεονέκτημα όταν απλώς **αναζητάτε HTML SVG**.

## Αναζήτηση HTML SVG – Διαχείριση Εξωτερικών Αναφορών `<img>`

Πολλοί ιστότοποι δεν ενσωματώνουν SVG απευθείας· αναφέρονται σε εξωτερικά αρχεία μέσω `<img src="icon.svg">`. Για να τα συλλάβετε, πρέπει να διατρέξουμε κάθε ετικέτα `<img>`, να ελέγξουμε το `src` της και να δούμε αν λήγει σε `.svg`.

```python
def collect_external_svg(soup: BeautifulSoup, base_path: str = "") -> list:
    """
    Return a list of file paths or URLs that point to external SVG images.
    If base_path is provided, it will be joined with relative URLs.
    """
    external_svgs = []
    for img in soup.find_all("img"):
        src = img.get("src")
        if src and src.lower().endswith(".svg"):
            # Resolve relative paths if a base directory or URL is given
            if base_path and not src.startswith(("http://", "https://")):
                src = os.path.join(base_path, src)
            external_svgs.append(src)
    return external_svgs
```

> **Προειδοποίηση για ειδικές περιπτώσεις:** Κάποιες σελίδες χρησιμοποιούν query strings (`icon.svg?v=2`) ή fragments (`icon.svg#layer`). Ο έλεγχος `endswith(".svg")` λειτουργεί ακόμη επειδή κοιτάμε μόνο το κάτω‑περιττό τμήμα της συμβολοσειράς. Αν χρειάζεστε πιο αυστηρή επικύρωση, σκεφτείτε να χρησιμοποιήσετε το `urllib.parse` για να αφαιρέσετε πρώτα τις παραμέτρους.

## Εύρεση Ενσωματωμένου SVG – Αναφορά των Αποτελεσμάτων

Τώρα που έχουμε δύο λίστες — μία για το markup ενσωματωμένου SVG και μία για εξωτερικές αναφορές αρχείων — μπορούμε να τις ενώσουμε και να αναφέρουμε το συνολικό πλήθος. Αυτό αντικατοπτρίζει το αρχικό απόσπασμα που δημοσιεύσατε, αλλά προσθέτει λίγο περισσότερο πλαίσιο.

```python
def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")
```

## Συνδυάζοντας Όλα – Πλήρες Script

Παρακάτω είναι το ολοκληρωμένο, έτοιμο‑για‑εκτέλεση πρόγραμμα. Αποθηκεύστε το ως `extract_svg.py` και τρέξτε το είτε με τοπικό αρχείο HTML είτε με URL.

```python
#!/usr/bin/env python3
import os
import sys
import requests
from bs4 import BeautifulSoup

# -------------------------------------------------
# Helper functions (see definitions above)
# -------------------------------------------------
def load_html(source: str) -> BeautifulSoup:
    if os.path.isfile(source):
        with open(source, "r", encoding="utf-8") as f:
            html = f.read()
    else:
        response = requests.get(source)
        response.raise_for_status()
        html = response.text
    return BeautifulSoup(html, "html.parser")

def collect_inline_svg(soup: BeautifulSoup) -> list:
    return [str(svg) for svg in soup.find_all("svg")]

def collect_external_svg(soup: BeautifulSoup, base_path: str = "") -> list:
    external_svgs = []
    for img in soup.find_all("img"):
        src = img.get("src")
        if src and src.lower().endswith(".svg"):
            if base_path and not src.startswith(("http://", "https://")):
                src = os.path.join(base_path, src)
            external_svgs.append(src)
    return external_svgs

def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")

# -------------------------------------------------
# Main execution
# -------------------------------------------------
if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python extract_svg.py <path-or-url-to-html>")
        sys.exit(1)

    source = sys.argv[1]
    soup = load_html(source)

    # Determine base path for relative <img> sources (only relevant for local files)
    base_dir = os.path.dirname(os.path.abspath(source)) if os.path.isfile(source) else ""

    inline_svgs = collect_inline_svg(soup)
    external_svgs = collect_external_svg(soup, base_dir)

    report_svg_counts(inline_svgs, external_svgs)

    # Optional: write inline SVGs to separate files for inspection
    for idx, svg_markup in enumerate(inline_svgs, start=1):
        out_path = f"inline_svg_{idx}.svg"
        with open(out_path, "w", encoding="utf-8") as out_file:
            out_file.write(svg_markup)
        print(f"Saved inline SVG #{idx} to {out_path}")

    # Optional: download external SVGs (uncomment if needed)
    # for url in external_svgs:
    #     try:
    #         resp = requests.get(url)
    #         resp.raise_for_status()
    #         filename = os.path.basename(url.split("?")[0])
    #         with open(filename, "wb") as f:
    #             f.write(resp.content)
    #         print(f"Downloaded {url} → {filename}")
    #     except Exception as e:
    #         print(f"Failed to download {url}: {e}")
```

### Αναμενόμενο Αποτέλεσμα

Η εκτέλεση του script σε ένα δείγμα `sample.html` μπορεί να εμφανίσει:

```
Found 3 inline SVG element(s).
Found 2 external SVG reference(s).
Overall, 5 SVG item(s) detected.
Saved inline SVG #1 to inline_svg_1.svg
Saved inline SVG #2 to inline_svg_2.svg
Saved inline SVG #3 to inline_svg_3.svg
```

Αν ξεσχολιάσετε το τμήμα λήψης, το εξωτερικό SVG


## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Convert SVG to Image in .NET with Aspose.HTML](/html/english/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}