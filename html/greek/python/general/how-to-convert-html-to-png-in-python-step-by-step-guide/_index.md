---
category: general
date: 2026-10-21
description: Μάθετε πώς να μετατρέπετε HTML σε PNG γρήγορα. Αυτό το σεμινάριο καλύπτει
  επίσης την εξαγωγή ιστοσελίδας σε PNG και τη μετατροπή αρχείου HTML σε PNG με Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to png
- export webpage to png
- how to convert html to image
- convert html file to png
language: el
lastmod: 2026-10-21
og_description: Μετατρέψτε HTML σε PNG με Python. Ακολουθήστε αυτόν τον σαφή οδηγό
  για να εξάγετε τη σελίδα σε PNG, να αντιμετωπίσετε ειδικές περιπτώσεις και να αυτοματοποιήσετε
  τη δημιουργία εικόνων.
og_image_alt: Screenshot of HTML page converted to PNG using Python
og_title: Μετατροπή HTML σε PNG με Python – πλήρης οδηγός προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  headline: How to convert HTML to PNG in Python – step‑by‑step guide
  type: TechArticle
- description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  name: How to convert HTML to PNG in Python – step‑by‑step guide
  steps:
  - name: Expected output
    text: 'Running the script prints:'
  - name: Why adjust viewport size?
    text: Web pages designed for desktop screens often look cramped if rendered at
      a small width. By increasing the `width` and `height` options, you capture the
      full layout, which is especially useful for **export webpage to PNG** tasks.
  - name: 6.1 Large pages or infinite scroll
    text: 'For pages that load content lazily (e.g., infinite scroll), increase the
      JavaScript delay and optionally set a larger viewport:'
  - name: 6.2 Authentication‑protected pages
    text: 'If a page requires a session cookie, you can embed the cookie header:'
  - name: 6.3 Missing images or fonts
    text: '`wkhtmltoimage` respects the `--disable-local-file-access` flag for security.
      If your HTML references local assets, enable them explicitly:'
  type: HowTo
tags:
- python
- html conversion
- image processing
- web automation
title: Πώς να μετατρέψετε HTML σε PNG με Python – οδηγός βήμα‑βήμα
url: /el/python/general/how-to-convert-html-to-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή HTML σε PNG με Python – πλήρης προγραμματιστικός οδηγός

Αν χρειάζεστε **convert HTML to PNG**, αυτός ο οδηγός σας δείχνει έναν αξιόπιστο τρόπο να το κάνετε με απλό Python. Είτε εξάγετε μια στατική αναφορά, δημιουργείτε μικρογραφίες για μια συλλογή, είτε αυτοματοποιείτε στιγμιότυπα οθόνης για δοκιμές, θα έχετε μια πλήρη, εκτελέσιμη λύση σε λίγα λεπτά.

Θα δείτε επίσης πώς να **export webpage to PNG**, να κατανοήσετε τη διαφορά μεταξύ μετατροπής ενός αρχείου HTML και μιας ζωντανής URL, και να μάθετε τις βέλτιστες πρακτικές για τη διαχείριση μεγάλων σελίδων ή δυναμικού περιεχομένου. Δεν απαιτούνται εξωτερικές υπηρεσίες—μόνο μερικά πακέτα Python και ένα σύντομο script.

## Προαπαιτούμενα

- Python 3.9+ εγκατεστημένο (ο κώδικας λειτουργεί σε Windows, macOS και Linux)
- Πρόσβαση σε τερματικό ή command prompt
- Βασική εξοικείωση με τον διαχειριστή πακέτων του Python (`pip`)

Θα χρειαστείτε το πακέτο `imgkit` (μια ελαφριά επικάλυψη γύρω από το `wkhtmltoimage`) και το ίδιο το εκτελέσιμο `wkhtmltoimage`. Και τα δύο είναι δωρεάν και ανοιχτού κώδικα.

## Βήμα 1: Εγκατάσταση των απαιτούμενων εργαλείων

Το πρώτο βήμα είναι η εγκατάσταση του `wkhtmltoimage` και του Python wrapper που επικοινωνεί με αυτό.

```bash
# Install wkhtmltoimage (Linux example)
sudo apt-get update && sudo apt-get install -y wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf

# On Windows download the installer from:
# https://wkhtmltopdf.org/downloads.html
# and add the installation folder to your PATH.

# Install the Python wrapper
pip install imgkit
```

> **Γιατί αυτό το βήμα είναι σημαντικό** – `wkhtmltoimage` αποδίδει HTML χρησιμοποιώντας τη μηχανή WebKit, παράγοντας PNG με τέλεια pixel. `imgkit` απλώς προωθεί τις επιλογές σας στο εκτελέσιμο, ώστε να λαμβάνετε την ίδια ποιότητα όπως από έναν browser.

## Βήμα 2: Επαλήθευση της εγκατάστασης

Εκτελέστε έναν γρήγορο έλεγχο για να επιβεβαιώσετε ότι το εκτελέσιμο είναι προσβάσιμο από το Python.

```python
import imgkit

# This will raise an exception if wkhtmltoimage is not found
print("wkhtmltoimage version:", imgkit.config().wkhtmltoimage)
```

Αν το script εκτυπώσει τη διαδρομή προς το `wkhtmltoimage`, είστε έτοιμοι να convert HTML to PNG. Αν λάβετε ένα `OSError`, ελέγξτε ξανά ότι το εκτελέσιμο βρίσκεται στο `PATH` του συστήματός σας.

## Βήμα 3: Γράψτε μια επαναχρησιμοποιήσιμη συνάρτηση μετατροπής

Η ενσωμάτωση της λογικής σε μια συνάρτηση καθιστά εύκολο το **convert HTML file to PNG** ή το **export webpage to PNG** από οπουδήποτε στο έργο σας.

```python
import os
import imgkit

def convert_html_to_png(source, output_path, *, options=None):
    """
    Convert an HTML file or URL to a PNG image.

    Parameters
    ----------
    source : str
        Path to a local HTML file (e.g., "report.html") or a URL
        (e.g., "https://example.com").
    output_path : str
        Destination file path for the PNG (e.g., "report.png").
    options : dict, optional
        imgkit options such as viewport size, zoom factor, or
        JavaScript delay. If omitted, sensible defaults are used.

    Returns
    -------
    bool
        True if the conversion succeeded, False otherwise.
    """
    # Use a default set of options if none are provided
    default_options = {
        "format": "png",
        "quality": "100",
        "encoding": "UTF-8",
        "quiet": "",
        # Render at 1280×720 – adjust for your layout
        "width": 1280,
        "height": 720,
        # Wait for JavaScript to finish (ms)
        "javascript-delay": 500,
    }
    # Merge user‑supplied options over defaults
    final_options = {**default_options, **(options or {})}

    try:
        # imgkit can handle both files and URLs transparently
        imgkit.from_file(source, output_path, options=final_options) \
            if os.path.isfile(source) else \
            imgkit.from_url(source, output_path, options=final_options)
        print(f"✅ Successfully saved PNG to: {output_path}")
        return True
    except Exception as e:
        print(f"❌ Conversion failed: {e}")
        return False
```

> **Γιατί τυλίγουμε και τα `from_file` και `from_url`** – Η ίδια συνάρτηση τώρα υποστηρίζει **how to convert HTML to image** για τοπικά αρχεία και ζωντανές ιστοσελίδες, διατηρώντας τον κώδικά σας DRY (Don’t Repeat Yourself).

## Βήμα 4: Μετατροπή τοπικού αρχείου HTML σε PNG

Τοποθετήστε ένα αρχείο HTML με όνομα `sample.html` σε φάκελο που ονομάζεται `assets`. Στη συνέχεια καλέστε τη βοηθητική συνάρτηση που μόλις ορίσαμε:

```python
if __name__ == "__main__":
    # Example: convert a static HTML file
    html_path = os.path.join("assets", "sample.html")
    png_path = os.path.join("output", "sample.png")

    # Ensure the output directory exists
    os.makedirs(os.path.dirname(png_path), exist_ok=True)

    # Perform the conversion
    success = convert_html_to_png(html_path, png_path)

    if success:
        # Show a tiny preview in the console (optional)
        from PIL import Image
        img = Image.open(png_path)
        img.thumbnail((200, 200))
        img.show()
```

### Αναμενόμενη έξοδος

Η εκτέλεση του script εκτυπώνει:

```
✅ Successfully saved PNG to: output/sample.png
```

Ένα νέο αρχείο `output/sample.png` περιέχει τώρα ένα pixel‑perfect στιγμιότυπο του `sample.html`. Το άνοιγμα του σε οποιονδήποτε προβολέα εικόνων δείχνει τη σελίδα όπως θα εμφανιζόταν σε έναν browser.

## Βήμα 5: Εξαγωγή ζωντανής ιστοσελίδας σε PNG

Αν χρειάζεστε **export webpage to PNG** για μια URL που αλλάζει συχνά (π.χ., έναν πίνακα ελέγχου), απλώς περάστε τη συμβολοσειρά URL αντί για διαδρομή αρχείου.

```python
# Example: convert a live page
url = "https://developer.mozilla.org/en-US/docs/Web/HTML"
output_file = "output/mdn_homepage.png"

convert_html_to_png(url, output_file, options={"width": 1920, "height": 1080})
```

### Γιατί να προσαρμόσετε το μέγεθος του viewport;

Οι ιστοσελίδες σχεδιασμένες για οθόνες desktop συχνά φαίνονται στενές αν αποδοθούν σε μικρό πλάτος. Αυξάνοντας τις επιλογές `width` και `height`, καταγράφετε ολόκληρη τη διάταξη, κάτι που είναι ιδιαίτερα χρήσιμο για εργασίες **export webpage to PNG**.

## Βήμα 6: Διαχείριση κοινών περιπτώσεων άκρων

### 6.1 Μεγάλες σελίδες ή άπειρο scroll

Για σελίδες που φορτώνουν περιεχόμενο αργά (π.χ., infinite scroll), αυξήστε την καθυστέρηση JavaScript και προαιρετικά ορίστε μεγαλύτερο viewport:

```python
options = {
    "javascript-delay": 2000,   # wait 2 seconds for JS to finish
    "width": 1440,
    "height": 3000,             # tall enough for the whole page
    "disable-smart-width": "", # forces the width we set
}
convert_html_to_png(url, "long_page.png", options=options)
```

### 6.2 Σελίδες προστατευμένες με authentication

Αν μια σελίδα απαιτεί cookie συνεδρίας, μπορείτε να ενσωματώσετε την κεφαλίδα cookie:

```python
options = {
    "custom-header": [
        "Cookie: sessionid=YOUR_SESSION_ID"
    ]
}
convert_html_to_png("https://internal.example.com/report", "report.png", options=options)
```

### 6.3 Ελλιπή εικόνες ή γραμματοσειρές

`wkhtmltoimage` σέβεται τη σημαία `--disable-local-file-access` για ασφάλεια. Αν το HTML σας αναφέρει τοπικά assets, ενεργοποιήστε τα ρητά:

```python
options = {"enable-local-file-access": ""}
convert_html_to_png("assets/complex.html", "complex.png", options=options)
```

## Βήμα 7: Επαλήθευση του αποτελέσματος προγραμματιστικά (προαιρετικό)

Μερικές φορές χρειάζεται να επιβεβαιώσετε ότι το PNG δημιουργήθηκε σωστά (π.χ., σε CI pipelines). Το παρακάτω απόσπασμα ελέγχει το μέγεθος αρχείου και τις διαστάσεις:

```python
from pathlib import Path
from PIL import Image

def verify_png(path):
    p = Path(path)
    if not p.is_file():
        raise FileNotFoundError(f"{path} does not exist")
    if p.stat().st_size < 10_000:  # arbitrary minimal size
        raise ValueError("Generated PNG seems too small")
    with Image.open(p) as img:
        print(f"Image size: {img.width}×{img.height}, mode: {img.mode}")

verify_png(png_path)
```

Αν το PNG περάσει αυτούς τους ελέγχους, μπορείτε με ασφάλεια να το χρησιμοποιήσετε σε επόμενες διεργασίες όπως δημιουργία PDF, συνημμένα email, ή pipelines μηχανικής μάθησης.

## Συμπέρασμα

Τώρα έχετε μια πλήρη, έτοιμη για παραγωγή μέθοδο για **convert HTML to PNG** χρησιμοποιώντας Python. Ο οδηγός κάλυψε:

- Εγκατάσταση του `wkhtmltoimage` και `imgkit`
- Επαλήθευση του περιβάλλοντος
- Μια επαναχρησιμοποιήσιμη συνάρτηση `convert_html_to_png` που διαχειρίζεται τόσο τοπικά αρχεία όσο και URLs
- Παραδείγματα πραγματικού κόσμου για **export webpage to PNG**, **how to convert HTML to image**, και **convert HTML file to PNG**
- Διαχείριση περιπτώσεων άκρων για μεγάλες σελίδες, authentication, και τοπικά assets
- Προαιρετικά βήματα επαλήθευσης για pipelines CI/CD

Μη διστάσετε να πειραματιστείτε με επιπλέον επιλογές `imgkit`—όπως `zoom`, `crop-h`, ή `crop-w`—για να ρυθμίσετε ακριβώς το αποτέλεσμα για τη συγκεκριμένη σας περίπτωση χρήσης. Για τα επόμενα βήματα, μπορείτε να εξερευνήσετε:

- Μετατροπή των PNG σε αναφορά PDF (`img2pdf` library)
- Αυτοματοποίηση μαζικής μετατροπής ολόκληρου φακέλου αρχείων HTML
- Χρήση Selenium για σελίδες που απαιτούν πλήρη απόδοση browser (π.χ., βαριές JavaScript frameworks)

Καλό προγραμματισμό, και απολαύστε τα pixel‑perfect στιγμιότυπα!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Μετατροπή HTML σε PNG – Πλήρης Οδηγός Python](/html/english/python/general/convert-html-to-png-complete-python-guide/)
- [Μετατροπή HTML σε PNG με Python – Πλήρης Οδηγός Αποθήκευσης Streaming](/html/english/python/general/convert-html-to-png-in-python-complete-streaming-save-guide/)
- [Μετατροπή SVG σε PNG με Python χρησιμοποιώντας Aspose.HTML](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}