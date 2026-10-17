---
category: general
date: 2026-05-31
description: Μάθετε πώς να εξάγετε SVG από HTML χρησιμοποιώντας Python. Αυτός ο βήμα‑προς‑βήμα
  οδηγός δείχνει πώς να διαβάσετε ένα έγγραφο HTML, να αποθηκεύσετε αρχεία SVG και
  να αποθηκεύσετε ενσωματωμένο SVG αποδοτικά.
draft: false
keywords:
- how to extract svg
- read html document
- save svg files
- save inline svg
- extract svg from html
language: el
og_description: Πώς να εξάγετε SVG από HTML χρησιμοποιώντας Python. Ακολουθήστε αυτό
  το σεμινάριο για να διαβάσετε το έγγραφο HTML, να αποθηκεύσετε αρχεία SVG και να
  διαχειριστείτε το ενσωματωμένο SVG με ευκολία.
og_title: Πώς να εξάγετε SVG από HTML με Python – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  headline: How to extract SVG from HTML with Python – Complete Guide
  type: TechArticle
- description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  name: How to extract SVG from HTML with Python – Complete Guide
  steps:
  - name: Reads an HTML file.
    text: Reads an HTML file.
  - name: Collects inline <svg> markup.
    text: Collects inline <svg> markup.
  - name: Finds external SVG references (<img> and <object> tags).
    text: Finds external SVG references (<img> and <object> tags).
  - name: Saves each SVG to a separate .svg file.
    text: Saves each SVG to a separate .svg file.
  type: HowTo
tags:
- Python
- SVG
- HTML parsing
- Aspose
title: Πώς να εξάγετε SVG από HTML με Python – Πλήρης Οδηγός
url: /el/python/general/how-to-extract-svg-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εξάγετε SVG από HTML με Python – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να εξάγετε SVG** από μια ακατάστατη σελίδα HTML χωρίς να τσακίζετε τα μαλλιά σας; Δεν είστε μόνοι. Είτε δημιουργείτε έναν web‑scraper, μια γραμμή εργασίας σχεδίασης, είτε απλώς χρειάζεστε να εξάγετε μαζικά εικονίδια, το να ξέρετε **πώς να εξάγετε SVG** είναι ένα χρήσιμο κόλπο που εξοικονομεί χρόνο και κεφάλι.

Σε αυτό το tutorial θα σας δείξουμε ακριβώς **πώς να εξάγετε SVG** χρησιμοποιώντας τη βιβλιοθήκη Aspose.HTML για Python. Θα διαβάσουμε το έγγραφο HTML, θα εξάγουμε τόσο το ενσωματωμένο `<svg>` markup **και** τις εξωτερικές αναφορές SVG, μετά θα **αποθηκεύσουμε αρχεία SVG** στο δίσκο—όλα σε ένα τακτοποιημένο, επαναχρησιμοποιήσιμο script. Στο τέλος θα έχετε μια έτοιμη προς εκτέλεση λύση που μπορείτε να προσαρμόσετε στα δικά σας έργα.

> **Pro tip:** Αν θέλετε μόνο μια γρήγορη ματιά στη σελίδα, το `BeautifulSoup` λειτουργεί επίσης, αλλά το Aspose.HTML σας παρέχει ένα πλήρες DOM, κάνοντας την εξαγωγή τόσο των ενσωματωμένων όσο και των συνδεδεμένων SVG μια ευκολία.

## Τι Θα Χρειαστεί

* Python 3.8+ (ο κώδικας χρησιμοποιεί f‑strings, οπότε το 3.6+ είναι το απόλυτο ελάχιστο)
* `pip install aspose-html` – η εμπορική βιβλιοθήκη που τροφοδοτεί την ανάλυση HTML μας
* Ένας φάκελος με ένα αρχείο `input.html` που περιέχει τα SVG που θέλετε να εξάγετε
* Δικαίωμα εγγραφής στον φάκελο εξόδου (θα τον ονομάσουμε `YOUR_DIRECTORY`)

Αυτό είναι—χωρίς επιπλέον εκτελέσιμα, χωρίς headless browsers. Απλό, έτσι;

## Βήμα 1: Διαβάστε το έγγραφο HTML με Aspose.HTML

Το πρώτο που πρέπει να κάνετε είναι **να διαβάσετε το έγγραφο HTML** ώστε να μπορείτε να περιηγηθείτε στο δέντρο DOM του. Το Aspose.HTML σας παρέχει ένα αντικείμενο `HTMLDocument` που συμπεριφέρεται όπως το `document` ενός προγράμματος περιήγησης.

```python
from aspose.html import HTMLDocument

# Load the HTML file – replace YOUR_DIRECTORY with the actual path
doc = HTMLDocument("YOUR_DIRECTORY/input.html")
```

*Γιατί είναι σημαντικό:* Φορτώνοντας το HTML σε ένα σωστό DOM, αποφεύγετε τις παγίδες της ανάλυσης με regex και λαμβάνετε δωρεάν μεθόδους όπως `get_elements_by_tag_name` και `query_selector_all`.

## Βήμα 2: Συλλέξτε όλα τα ενσωματωμένα στοιχεία <svg>

Τα ενσωματωμένα SVG είναι εκείνα τα μπλοκ `<svg>…</svg>` που βρίσκονται απευθείας μέσα στο HTML. Για να **αποθηκεύσετε ενσωματωμένο SVG** χρειαζόμαστε απλώς το εξωτερικό HTML τους.

```python
svg_contents = []  # We'll collect both markup and file paths here

# Find every <svg> element in the document
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)   # Store the raw markup
```

Παρατηρήστε ότι προσθέτουμε το ακατέργαστο markup απευθείας στο `svg_contents`. Αργότερα θα αποφασίσουμε αν κάθε καταχώρηση είναι markup ή διαδρομή αρχείου.

## Βήμα 3: Βρείτε εξωτερικές αναφορές SVG (ετικέτες img και object)

Πολλές σελίδες συνδέουν εξωτερικά αρχεία SVG μέσω `<img src="icon.svg">` ή `<object data="logo.svg">`. Για να **εξάγετε SVG από HTML** πρέπει επίσης να συλλάβουμε αυτές τις URL.

```python
# CSS selector: img or object whose src/data ends with .svg (case‑insensitive)
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    # For <img> we read the src attribute, for <object> the data attribute
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:                                   # Guard against missing attribute
        svg_contents.append(src)
```

*Προειδοποίηση για ειδικές περιπτώσεις:* Αν η URL του SVG είναι σχετική, θα θέλετε να τη συνδυάσετε με τη βασική διαδρομή του αρχείου HTML. Για συντομία υποθέτουμε ότι το HTML βρίσκεται δίπλα στα αρχεία SVG.

## Βήμα 4: Γράψτε κάθε SVG σε ξεχωριστό αρχείο

Τώρα που έχουμε έναν μικτό κατάλογο από συμβολοσειρές markup και διαδρομές αρχείων, θα επαναλάβουμε και **αποθηκεύσουμε αρχεία SVG**. Το script διακρίνει αυτόματα μεταξύ ενσωματωμένου markup και αναφοράς σε υπάρχον αρχείο.

```python
import os
import shutil

for index, content in enumerate(svg_contents):
    output_path = f"YOUR_DIRECTORY/svg_{index}.svg"

    # Trim leading whitespace and check if it looks like markup
    if content.lstrip().startswith("<svg"):
        # Inline SVG – write the markup directly
        with open(output_path, "w", encoding="utf-8") as file:
            file.write(content)
        print(f"Saved inline SVG to {output_path}")
    else:
        # External reference – copy the source file's contents
        src_path = os.path.abspath(content)  # Resolve relative paths
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, output_path)
            print(f"Copied external SVG from {src_path} to {output_path}")
        else:
            print(f"⚠️  Warning: referenced SVG not found: {src_path}")
```

**Τι θα δείτε:** Μετά το τέλος του script, το `YOUR_DIRECTORY` θα περιέχει αρχεία με ονόματα `svg_0.svg`, `svg_1.svg`, … το καθένα περιέχει είτε το αρχικό ενσωματωμένο markup είτε ένα αντίγραφο του εξωτερικού SVG.

### Αναμενόμενο Αποτέλεσμα

```
Saved inline SVG to YOUR_DIRECTORY/svg_0.svg
Saved inline SVG to YOUR_DIRECTORY/svg_1.svg
Copied external SVG from /path/to/logo.svg to YOUR_DIRECTORY/svg_2.svg
...
```

Αν ένα αναφερόμενο αρχείο λείπει, το script εκτυπώνει μια προειδοποίηση αλλά συνεχίζει—ώστε ένας σπασμένος σύνδεσμος δεν θα σταματήσει ολόκληρη την εξαγωγή.

## Διαχείριση Συνηθισμένων Προβλημάτων

| Πρόβλημα | Γιατί συμβαίνει | Γρήγορη Διόρθωση |
|----------|----------------|-------------------|
| **Σχετικές URLs σπάζουν** | Το χαρακτηριστικό `src` μπορεί να είναι `"../assets/icon.svg"` | Χρησιμοποιήστε `os.path.join(os.path.dirname(html_path), src)` για επίλυση. |
| **Διπλότυπα ονόματα αρχείων** | Δύο SVG με το ίδιο όνομα αντικαθίστανται | Συμπεριλάβετε ένα hash του περιεχομένου στο όνομα αρχείου (`hashlib.md5(content.encode()).hexdigest()[:8]`). |
| **Μεγάλα ενσωματωμένα SVG προκαλούν άλματα μνήμης** | Αποθήκευση όλου του markup σε λίστα πριν τη γραφή | Ροή (stream) κάθε στοιχείου απευθείας σε αρχείο αντί για buffer. |
| **Μη‑SVG εικόνες περνούν διαφθορά** | Κάποιες ετικέτες `<img>` τελειώνουν με `.svg?version=1` | Αφαιρέστε τα query strings πριν τον έλεγχο επέκτασης (`src.split('?')[0]`). |

## Πλήρες Script που Μπορείτε να Αντιγράψετε‑Κολλήσετε

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Αποθηκεύστε το ως `extract_svg.py`, προσαρμόστε το `YOUR_DIRECTORY` και τρέξτε `python extract_svg.py`.

```python
"""
extract_svg.py – How to extract SVG from HTML using Aspose.HTML for Python

This script:
1. Reads an HTML file.
2. Collects inline <svg> markup.
3. Finds external SVG references (<img> and <object> tags).
4. Saves each SVG to a separate .svg file.

Author: Your Name
Date: 2026-05-31
"""

import os
import shutil
from aspose.html import HTMLDocument

# ----------------------------------------------------------------------
# Configuration – change these paths to suit your environment
# ----------------------------------------------------------------------
HTML_PATH = "YOUR_DIRECTORY/input.html"          # Path to source HTML
OUTPUT_DIR = "YOUR_DIRECTORY"                    # Where SVGs will be written

# Ensure output directory exists
os.makedirs(OUTPUT_DIR, exist_ok=True)

# ----------------------------------------------------------------------
# Step 1: Load the HTML document (read html document)
# ----------------------------------------------------------------------
doc = HTMLDocument(HTML_PATH)

# ----------------------------------------------------------------------
# Step 2: Collect inline <svg> elements (save inline svg)
# ----------------------------------------------------------------------
svg_contents = []
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)

# ----------------------------------------------------------------------
# Step 3: Collect external SVG references (extract svg from html)
# ----------------------------------------------------------------------
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:
        # Resolve relative paths relative to the HTML file location
        src_path = os.path.join(os.path.dirname(HTML_PATH), src)
        svg_contents.append(src_path)

# ----------------------------------------------------------------------
# Step 4: Save each gathered SVG (save svg files)
# ----------------------------------------------------------------------
for idx, content in enumerate(svg_contents):
    out_path = os.path.join(OUTPUT_DIR, f"svg_{idx}.svg")

    # Detect inline markup vs file path
    if isinstance(content, str) and content.lstrip().startswith("<svg"):
        # Inline SVG – write directly
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(content)
        print(f"[✓] Inline SVG saved → {out_path}")
    else:
        # External file – copy its contents
        src_path = os.path.abspath(content)
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, out_path)
            print(f"[✓] External SVG copied → {out_path}")
        else:
            print(f"[⚠] Missing SVG file: {src_path}")

print("\n✅ Extraction complete. Check the", OUTPUT_DIR, "folder for your SVGs.")
```

## Ανακεφαλαίωση – Πώς να εξάγετε SVG συνοπτικά

* **Διαβάστε το έγγραφο HTML** με `HTMLDocument`.
* **Συλλέξτε ενσωματωμένα `<svg>`** μέσω `get_elements_by_tag_name`.
* **Εντοπίστε εξωτερικά SVG** χρησιμοποιώντας έναν CSS selector που τελειώνει σε `.svg`.
* **Αποθηκεύστε κάθε κομμάτι**—γράψτε το markup απευθείας σε αρχείο ή αντιγράψτε το αναφερόμενο αρχείο.
* **Διαχειριστείτε ειδικές περιπτώσεις** όπως σχετικές διαδρομές, διπλότυπα και ελλιπή αρχεία.

Αυτή είναι η πλήρης απάντηση στο **πώς να εξάγετε SVG** από μια σελίδα HTML, ενσωματωμένη σε ένα ενιαίο, εύκολο‑προς‑τροποποίηση script.

## Τι Ακολουθεί;

Τώρα που μπορείτε να **εξάγετε SVG** αξιόπιστα, σκεφτείτε αυτές τις ιδέες:

* **Μαζική επεξεργασία:** Επανάληψη πάνω σε έναν φάκελο αρχείων HTML για τη δημιουργία βιβλιοθήκης εικονιδίων.
* **Βελτιστοποίηση:** Εκτελέστε κάθε αποθηκευμένο SVG μέσω SVGO (βελτιστοποιητής Node.js) για να μειώσετε το μέγεθος του αρχείου.
* **Μετατροπή:** Χρησιμοποιήστε `cairosvg` ή `svglib` για να μετατρέψετε τα SVG σε PNG για παλαιότερα προγράμματα περιήγησης.
* **Εξαγωγή μεταδεδομένων:** Αναλύστε ετικέτες `<title>` ή `<desc>` μέσα σε κάθε SVG για ετικέτες αναζήτησης.

Κάθε ένα από αυτά τα θέματα αγγίζει τις δευτερεύουσες λέξεις‑κλειδιά μας—**read HTML document**, **save svg files**, **save inline svg**, **extract svg from html**—οπότε θα βρείτε άφθονο υλικό για εξερεύνηση.

---

*Καλή προγραμματιστική! Αν αντιμετωπίσετε προβλήματα, αφήστε ένα σχόλιο παρακάτω ή στείλτε μου μήνυμα στο GitHub. Ο κόσμος των SVG είναι τεράστιος, αλλά με τα σωστά εργαλεία, η εξαγωγή τους είναι παιγνίδι.*

## Τι Θα Μάθετε Στη Σειρά;

- [Αποθήκευση Εγγράφου SVG στο Aspose.HTML για Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Πώς να Μετατρέψετε SVG σε XPS με Aspose.HTML για Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [Μετατροπή εγγράφου SVG σε μορφή PNG στο .NET με Aspose.HTML](/html/french/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}