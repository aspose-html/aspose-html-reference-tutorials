---
category: general
date: 2026-08-06
description: Μετατρέψτε HTML σε PDF με Python με ένα πλήρες παράδειγμα. Μάθετε πώς
  να δημιουργείτε PDF από HTML, να αποθηκεύετε HTML ως PDF και να αντιμετωπίζετε κοινές
  ακραίες περιπτώσεις.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to pdf
- generate pdf from html
- save html as pdf
- create pdf from html file
- how to convert html to pdf
language: el
lastmod: 2026-08-06
og_description: Μετατρέψτε το HTML σε PDF με Python και αυτοματοποιήστε τη δημιουργία
  εγγράφων. Ακολουθήστε αυτόν τον οδηγό για να δημιουργήσετε PDF από HTML, να αποθηκεύσετε
  το HTML ως PDF και να προσαρμόσετε το αποτέλεσμα.
og_image_alt: Example of convert html to pdf script in Python
og_title: Μετατροπή HTML σε PDF με Python – ολοκληρωμένος οδηγός
schemas:
- author: Aspose
  dateModified: '2026-08-06'
  description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  headline: Convert HTML to PDF in Python – step‑by‑step guide
  type: TechArticle
- description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  name: Convert HTML to PDF in Python – step‑by‑step guide
  steps:
  - name: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
    text: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
  - name: '**Input handling** – read the HTML file or build the markup programmatically.'
    text: '**Input handling** – read the HTML file or build the markup programmatically.'
  - name: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
    text: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
  type: HowTo
tags:
- HTML to PDF
- Python
- Document conversion
title: Μετατροπή HTML σε PDF με Python – οδηγός βήμα‑προς‑βήμα
url: /el/python/general/convert-html-to-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή HTML σε PDF με Python – βήμα‑βήμα οδηγός

Αν χρειάζεστε **γρήγορη μετατροπή HTML σε PDF**, αυτό το tutorial παρουσιάζει μια πλήρη λύση σε Python. Θα δείτε πώς να δημιουργήσετε PDF από HTML, να αποθηκεύσετε HTML ως PDF και να ελέγξετε τη διαδικασία μετατροπής χωρίς να φύγετε από τον κώδικά σας.

Ο οδηγός σας καθοδηγεί στην εγκατάσταση μιας αξιόπιστης βιβλιοθήκης, στη φόρτωση ενός εγγράφου HTML, στην εκτέλεση της μετατροπής και στην επαλήθευση του αποτελέσματος. Στο τέλος, θα μπορείτε να δημιουργήσετε PDF από αρχείο HTML σε οποιοδήποτε έργο Python, είτε η πηγή είναι μια στατική σελίδα είτε δυναμικά παραγόμενο markup.

## Τι θα μάθετε

* Εγκατάσταση των εξαρτήσεων `pdfkit` και `wkhtmltopdf` που απαιτούνται για τη μετατροπή HTML‑σε‑PDF.  
* Φόρτωση εγγράφου HTML από δίσκο ή από συμβολοσειρά.  
* Δημιουργία PDF από HTML με προσαρμοσμένο μέγεθος σελίδας, περιθώρια και επιλογές κωδικοποίησης.  
* Αποθήκευση HTML ως PDF με μία κλήση συνάρτησης.  
* Διαχείριση τυπικών περιπτώσεων όπως ελλιπή assets, χαρακτήρες Unicode και μεγάλα αρχεία.  

**Προαπαιτούμενα** – Python 3.8+ και βασική εξοικείωση με I/O αρχείων. Δεν απαιτούνται εξωτερικές υπηρεσίες.

## Μετατροπή HTML σε PDF – συνολική ροή εργασίας

Η διαδικασία μετατροπής αποτελείται από τρία λογικά στάδια:

1. **Προετοιμασία** – εγκατάσταση του μετατροπέα και διασφάλιση ότι το εκτελέσιμο `wkhtmltopdf` είναι προσβάσιμο.  
2. **Διαχείριση εισόδου** – ανάγνωση του αρχείου HTML ή δημιουργία του markup προγραμματιστικά.  
3. **Δημιουργία εξόδου** – κλήση του μετατροπέα, εγγραφή του αρχείου PDF και επιβεβαίωση του αποτελέσματος.

Κάθε στάδιο καλύπτεται σε ξεχωριστό βήμα παρακάτω.

## Βήμα 1: Εγκατάσταση απαιτούμενων βιβλιοθηκών

`pdfkit` παρέχει ένα ελαφρύ wrapper σε Python γύρω από τη δημοφιλή μηχανή `wkhtmltopdf`. Εγκαταστήστε και τις δύο με `pip` και επαληθεύστε τη διαδρομή του εκτελέσιμου.

```bash
# Install the Python wrapper
pip install pdfkit

# On Ubuntu/Debian install wkhtmltopdf package
sudo apt-get install wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf
```

Αν προτιμάτε ένα φορητό εκτελέσιμο, κατεβάστε την κατάλληλη έκδοση από τη [σελίδα GitHub του wkhtmltopdf](https://github.com/wkhtmltopdf/wkhtmltopdf/releases) και τοποθετήστε το σε φάκελο που είναι προστιθέμενος στο `PATH`. Το script ελέγχει αυτόματα τη διαδρομή αργότερα.

## Βήμα 2: Φόρτωση του εγγράφου HTML

Μπορείτε να διαβάσετε ένα στατικό αρχείο, να ανακτήσετε απομακρυσμένο περιεχόμενο ή να δημιουργήσετε HTML επί τόπου. Το παρακάτω παράδειγμα φορτώνει ένα τοπικό αρχείο με όνομα `sample.html` που βρίσκεται σε φάκελο που ορίζετε.

```python
import pathlib
import pdfkit

# Define the directory that holds the HTML source
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")

# Resolve the full path to the HTML file
html_path = BASE_DIR / "sample.html"

# Read the file content as a UTF‑8 string
with html_path.open(encoding="utf-8") as f:
    html_content = f.read()
```

Η ανάγνωση του αρχείου ως συμβολοσειρά Unicode εξασφαλίζει ότι χαρακτήρες όπως “é”, “ß” ή ασιατικά σύμβολα διατηρούνται κατά τη μετατροπή. Αυτό το βήμα είναι κρίσιμο όταν **δημιουργείτε PDF από HTML** που περιέχει διεθνές κείμενο.

## Βήμα 3: Δημιουργία PDF από HTML

`pdfkit.from_string` μετατρέπει μια συμβολοσειρά που περιέχει markup HTML σε αρχείο PDF. Μπορείτε να περάσετε ένα λεξικό επιλογών για να ελέγξετε το μέγεθος σελίδας, τα περιθώρια και τη συμπεριφορά header/footer.

```python
# Define the output PDF path
pdf_path = BASE_DIR / "sample.pdf"

# Conversion options – adjust as needed
options = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left": "0.75in",
    "encoding": "UTF-8",
    "enable-local-file-access": None,  # Allows loading local images/CSS
}

# Perform the conversion
pdfkit.from_string(html_content, str(pdf_path), options=options)
```

Η κλήση παραπάνω **δημιουργεί PDF από αρχείο HTML** αποθηκευμένο στο `sample.pdf`. Αν το HTML αναφέρεται σε τοπικά CSS ή εικόνες, η σημαία `enable‑local‑file‑access` επιτρέπει στο `wkhtmltopdf` να εντοπίσει αυτούς τους πόρους.

### Γιατί λειτουργεί αυτή η προσέγγιση

* Το `pdfkit` αναθέτει το βαρέως τύπου έργο στο `wkhtmltopdf`, το οποίο αποδίδει το HTML με τη μηχανή WebKit, εξασφαλίζοντας υψηλή πιστότητα στο αρχικό layout.  
* Η παροχή λεξικού επιλογών σας επιτρέπει να ρυθμίσετε ακριβώς την έξοδο χωρίς να τροποποιήσετε το ίδιο το HTML.  
* Η χρήση `from_string` διατηρεί τη ροή εργασίας στη μνήμη, χρήσιμη όταν το HTML δημιουργείται επί τόπου.

## Βήμα 4: Αποθήκευση HTML ως PDF και επαλήθευση εξόδου

Μετά τη μετατροπή, ίσως θέλετε να επιβεβαιώσετε ότι το PDF υπάρχει και είναι αναγνώσιμο. Το παρακάτω απόσπασμα ελέγχει το μέγεθος του αρχείου και ανοίγει το PDF με τον προεπιλεγμένο προβολέα του συστήματος (πλατφόρμα‑συγκεκριμένο).

```python
import os
import subprocess
import sys

# Verify that the PDF file was created
if pdf_path.is_file() and pdf_path.stat().st_size > 0:
    print(f"✅ PDF generated successfully: {pdf_path}")

    # Open the PDF for visual verification (optional)
    if sys.platform.startswith("darwin"):      # macOS
        subprocess.run(["open", str(pdf_path)])
    elif os.name == "nt":                      # Windows
        os.startfile(str(pdf_path))
    else:                                      # Linux and others
        subprocess.run(["xdg-open", str(pdf_path)])
else:
    raise FileNotFoundError("PDF generation failed – file not found or empty.")
```

Η εκτέλεση του script εμφανίζει μήνυμα επιτυχίας και εκκινεί τον προβολέα PDF ώστε να μπορείτε αμέσως να ελέγξετε ότι το layout ταιριάζει με το αρχικό HTML. Αυτό το βήμα ολοκληρώνει τον κύκλο **αποθήκευσης html ως pdf**.

## Βήμα 5: Προηγμένες επιλογές – δημιουργία PDF από αρχείο HTML με προσαρμοσμένες ρυθμίσεις

Μερικές φορές έχετε ένα φυσικό αρχείο HTML στον δίσκο και προτιμάτε το `pdfkit.from_file` αντί να φορτώνετε το περιεχόμενο μόνοι σας. Αυτή η μέθοδος είναι χρήσιμη όταν το HTML περιλαμβάνει ήδη σύνθετες σχετικές διαδρομές.

```python
# Directly convert a file path to PDF
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

Μπορείτε επίσης να ενσωματώσετε σελίδα εξωφύλλου, πίνακα περιεχομένων ή σημαίες εκτέλεσης JavaScript επεκτείνοντας το λεξικό `options`. Για παράδειγμα, για να προσθέσετε σελίδα εξωφύλλου:

```python
options.update({
    "cover": str(BASE_DIR / "cover.html"),
    "toc": None,  # Generates a table of contents
})
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

Αυτές οι προσαρμογές δείχνουν **πώς να μετατρέψετε HTML σε PDF** για πιο σύνθετες αλυσίδες δημοσίευσης.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Πρόβλημα | Αιτία | Λύση |
|----------|-------|------|
| Οι εικόνες ή το CSS δεν εμφανίζονται | Το `wkhtmltopdf` αποκλείει την πρόσβαση σε τοπικά αρχεία από προεπιλογή | Προσθέστε `"enable-local-file-access": None` στο λεξικό επιλογών |
| Οι χαρακτήρες Unicode εμφανίζονται αλλοιωμένοι | Έλλειψη επιλογής `encoding` ή ανάγνωση αρχείου με λάθος charset | Πάντα ορίστε `"encoding": "UTF-8"` και διαβάστε το HTML με UTF‑8 |
| Το PDF είναι κενό | Λανθασμένη διαδρομή προς το εκτελέσιμο `wkhtmltopdf` | Δώστε ρητά τη διαδρομή: `pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")` |
| Μεγάλα αρχεία HTML προκαλούν timeout | Το προεπιλεγμένο timeout είναι πολύ μικρό | Ορίστε `"javascript-delay": "2000"` ή αυξήστε το timeout με `"timeout": "60"` |

Η αντιμετώπιση αυτών των θεμάτων εξασφαλίζει μια αξιόπιστη διαδικασία **δημιουργίας pdf από html** σε διαφορετικά περιβάλλοντα.

## Πλήρες script – παράδειγμα από αρχή μέχρι τέλος

Αποθηκεύστε το παρακάτω ως `html_to_pdf.py` και τρέξτε το με `python html_to_pdf.py`. Προσαρμόστε το `YOUR_DIRECTORY` ώστε να δείχνει στο φάκελο του έργου σας.

```python
#!/usr/bin/env python3
"""
Convert HTML to PDF in Python – complete, runnable example.
"""

import pathlib
import pdfkit
import os
import subprocess
import sys

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")          # <-- change this
HTML_FILE = BASE_DIR / "sample.html"
PDF_FILE = BASE_DIR / "sample.pdf"

# wkhtmltopdf configuration (optional – only needed if binary is not on PATH)
# config = pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")

# Conversion options – customize as required
OPTIONS = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left":


## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Convert HTML to PDF in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [How to Convert HTML to PDF Java - Set Page Margins with Aspose.HTML](/html/english/java/advanced-usage/css-extensions-adding-title-page-number/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}