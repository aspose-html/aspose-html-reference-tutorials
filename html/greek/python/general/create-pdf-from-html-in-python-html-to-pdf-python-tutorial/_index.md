---
category: general
date: 2026-07-15
description: Δημιουργήστε PDF από HTML χρησιμοποιώντας Python. Μάθετε πώς να μετατρέψετε
  HTML σε PDF γρήγορα με ένα απλό script και σαφή βήματα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf from html
- convert html to pdf
- html to pdf python
- save html as pdf
- html to pdf tutorial
language: el
lastmod: 2026-07-15
og_description: Δημιουργήστε PDF από HTML με Python. Αυτός ο οδηγός σας δείχνει πώς
  να μετατρέψετε HTML σε PDF, να αποθηκεύσετε HTML ως PDF και να διαχειρίζεστε τους
  πόρους αποδοτικά.
og_image_alt: Screenshot of a Python script that creates PDF from HTML
og_title: Δημιουργία PDF από HTML σε Python – Πρακτικό σεμινάριο
schemas:
- author: Aspose
  dateModified: '2026-07-15'
  description: Create PDF from HTML using Python. Learn how to convert HTML to PDF
    quickly with a simple script and clear steps.
  headline: Create PDF from HTML in Python – HTML to PDF Python Tutorial
  type: TechArticle
tags:
- python
- pdf
- html
- conversion
title: Δημιουργία PDF από HTML με Python – Εκπαιδευτικό σεμινάριο Python για HTML
  σε PDF
url: /el/python/general/create-pdf-from-html-in-python-html-to-pdf-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία PDF από HTML σε Python – Πλήρης‑Χαρακτηριστικά Οδηγός

Έχετε ποτέ χρειαστεί να **να δημιουργήσετε PDF από HTML** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη Python να επιλέξετε; Δεν είστε μόνοι—πολλοί προγραμματιστές συναντούν αυτό το πρόβλημα όταν προσπαθούν να μετατρέψουν μια αναφορά ιστού, τιμολόγιο ή σελίδα μάρκετινγκ σε εκτυπώσιμο PDF.  

Τα καλά νέα είναι ότι με λίγες μόνο γραμμές κώδικα μπορείτε να **convert HTML to PDF** αξιόπιστα, και το script λειτουργεί σε Windows, macOS και Linux. Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα, θα εξηγήσουμε γιατί κάθε βήμα είναι σημαντικό, και θα σας δείξουμε πώς να **save HTML as PDF** χωρίς να αφήσετε χαλαρά άκρα.

---

## Τι Θα Μάθετε

- Εγκαταστήστε το σωστό πακέτο Python για μετατροπή HTML‑σε‑PDF.  
- Φορτώστε ένα αρχείο HTML με προσαρμοσμένες επιλογές διαχείρισης πόρων (για αποφυγή ατελείωτων εισαγωγών CSS).  
- Δημιουργήστε ένα καθαρό αρχείο PDF στον δίσκο.  
- Αντιμετωπίστε κοινές περιπτώσεις άκρων όπως εξωτερικές εικόνες, σχετικές διαδρομές και μεγάλα έγγραφα.  

Στο τέλος αυτού του **HTML to PDF tutorial** θα έχετε μια επαναχρησιμοποιήσιμη συνάρτηση που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο.

---

## Προαπαιτούμενα

- Python 3.9+ (ο κώδικας λειτουργεί επίσης με 3.8, αλλά το 3.9+ παρέχει τις πιο πρόσφατες δυνατότητες του `pathlib`).  
- Βασική εξοικείωση με τη γραμμή εντολών και τα εικονικά περιβάλλοντα.  
- Ένα αρχείο HTML που θέλετε να μετατρέψετε σε PDF—οποιαδήποτε στατική σελίδα αρκεί.

> **Pro tip:** Αν χρησιμοποιείτε εικονικό περιβάλλον, ενεργοποιήστε το πριν εγκαταστήσετε τη βιβλιοθήκη· αυτό διατηρεί το παγκόσμιο Python σας τακτοποιημένο.

---

## Βήμα 1 – Εγκατάσταση WeasyPrint (η μηχανή πίσω από τη μετατροπή)

WeasyPrint είναι μια βιβλιοθήκη pure‑Python που αποδίδει HTML και CSS σε PDF. Διαχειρίζεται τις περισσότερες σύγχρονες λειτουργίες ιστού και σας παρέχει λεπτομερή έλεγχο της φόρτωσης πόρων.

```bash
pip install weasyprint
```

Η εκτέλεση της παραπάνω εντολής κατεβάζει τα `cairocffi`, `tinycss2` και μερικές άλλες εξαρτήσεις. Αν αντιμετωπίσετε σφάλμα σχετικό με `cairo` στα Windows, κατεβάστε τα προ‑συγκροτημένα wheels από την [WeasyPrint website](https://weasyprint.org/docs/install/).

---

## Βήμα 2 – Προετοιμασία ενός μικρού βοηθού για τη διαχείριση πόρων

Όταν φορτώνετε ένα έγγραφο HTML που αναφέρει εξωτερικά φύλλα στυλ ή εικόνες, η βιβλιοθήκη θα ακολουθήσει αυτούς τους συνδέσμους. Σε ορισμένες περιπτώσεις αυτό οδηγεί σε βαθιά ένθετη δομή ή ακόμη και σε άπειρους βρόχους (σκεφτείτε ένα αρχείο CSS που `@import`s τον εαυτό του). Για να διατηρήσουμε την τάξη περιορίζουμε το βάθος της διαχείρισης πόρων.

```python
from weasyprint import HTML, CSS
from pathlib import Path

class ResourceHandlingOptions:
    """Simple container to mimic max depth handling."""
    def __init__(self, max_depth: int = 3):
        self.max_depth = max_depth
        self._current_depth = 0

    def within_limit(self) -> bool:
        return self._current_depth < self.max_depth

    def __enter__(self):
        self._current_depth += 1
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        self._current_depth -= 1
```

Η παραπάνω κλάση δεν απαιτείται από το WeasyPrint, αλλά αντικατοπτρίζει το μοτίβο που είδατε στο αρχικό απόσπασμα και σας παρέχει ένα σημείο προσάρτησης για να σταματήσετε τις ανεξέλεγκτες εισαγωγές. Θα τη δείτε να χρησιμοποιείται στο επόμενο βήμα.

---

## Βήμα 3 – Φόρτωση του εγγράφου HTML χρησιμοποιώντας τις προσαρμοσμένες επιλογές

Τώρα διαβάζουμε πραγματικά το αρχείο HTML. Η κλάση `HTML` δέχεται ένα όρισμα `base_url`, το οποίο ορίζουμε στο φάκελο που περιέχει το αρχείο προέλευσης—αυτό κάνει τις σχετικές συνδέσεις να λειτουργούν χωρίς διακομιστή web.

```python
def load_html(input_path: Path, options: ResourceHandlingOptions) -> HTML:
    """
    Load an HTML file while respecting the max handling depth.
    """
    if not options.within_limit():
        raise RuntimeError("Maximum resource handling depth exceeded.")
    # The `with` block increments depth for the duration of the call.
    with options:
        return HTML(filename=str(input_path), base_url=str(input_path.parent))
```

> **Why this matters:** Αν το HTML σας φορτώνει μια αλυσίδα αρχείων CSS, κάθε `@import` θα προκαλέσει άλλη φόρτωση. Η προστασία βάθους αποτρέπει το script από το να ξεφύγει από τον έλεγχο.

---

## Βήμα 4 – Αποθήκευση του επεξεργασμένου εγγράφου ως PDF

Με το αντικείμενο `HTML` στα χέρια, η δημιουργία PDF είναι μια γραμμή κώδικα. Επιπλέον περνάμε ένα απλό απόσπασμα CSS που επιβάλλει καθαρό μέγεθος σελίδας (A4) και προσθέτει μικρό περιθώριο—αλλάξτε το όπως θέλετε.

```python
def save_as_pdf(html_doc: HTML, output_path: Path) -> None:
    """
    Render the HTML document to a PDF file.
    """
    default_css = CSS(string='''
        @page { size: A4; margin: 1cm }
    ''')
    html_doc.write_pdf(target=str(output_path), stylesheets=[default_css])
```

Η κλήση του `write_pdf` αποστέλλει το PDF στον δίσκο, έτσι έχετε ένα έτοιμο‑για‑κοινοποίηση αρχείο.

---

## Βήμα 5 – Συνδυάστε Όλα Μαζί

Παρακάτω είναι ένα συμπαγές script που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο `convert.py`. Αντικαταστήστε τις διαδρομές placeholder με τους πραγματικούς σας φακέλους.

```python
#!/usr/bin/env python3
"""
HTML to PDF Python script – complete, runnable example.
"""

from pathlib import Path

# Import the helper classes we defined earlier
from __main__ import ResourceHandlingOptions, load_html, save_as_pdf  # noqa: E402

def main():
    # 1️⃣  Define input and output locations
    input_html = Path("YOUR_DIRECTORY/input.html")
    output_pdf = Path("YOUR_DIRECTORY/output.pdf")

    # 2️⃣  Create resource handling options (max depth = 3)
    resource_options = ResourceHandlingOptions(max_depth=3)

    # 3️⃣  Load the HTML document with the custom options
    html_doc = load_html(input_html, resource_options)

    # 4️⃣  Save the processed document as PDF
    save_as_pdf(html_doc, output_pdf)

    print(f"✅ PDF saved to {output_pdf.resolve()}")

if __name__ == "__main__":
    main()
```

**Expected output** – μετά την εκτέλεση του `python convert.py` θα πρέπει να δείτε:

```
✅ PDF saved to /full/path/YOUR_DIRECTORY/output.pdf
```

Ανοίξτε το παραγόμενο αρχείο με οποιονδήποτε προβολέα PDF· θα δείτε την αρχική διάταξη σελίδας, το στυλ CSS και τις εικόνες (εφόσον ήταν προσβάσιμες από το αρχείο HTML).  

Αν παρατηρήσετε ελλιπείς εικόνες, ελέγξτε ξανά ότι τα attributes `src` είναι είτε απόλυτες URLs είτε σχετικές διαδρομές που υπάρχουν κάτω από `YOUR_DIRECTORY`.

---

## Συχνές Ερωτήσεις & Διαχείριση Περιπτώσεων Άκρων

| Question | Answer |
|----------|--------|
| *Τι γίνεται αν το HTML μου αναφέρει εξωτερικές γραμματοσειρές;* | Το WeasyPrint θα κατεβάσει αυτόματα τα αρχεία γραμματοσειρών, αλλά ίσως θέλετε να προσθέσετε σε whitelist τους τομείς για να αποφύγετε μεγάλους χρόνους λήψης. |
| *Μπορώ να μετατρέψω μια συμβολοσειρά HTML αντί για αρχείο;* | Ναι—χρησιμοποιήστε `HTML(string=my_html_string)` και παραλείψτε το `base_url` ή ορίστε το σε έναν προσωρινό φάκελο. |
| *Πώς ελέγχω τα μεταδεδομένα PDF (τίτλος, δημιουργός);* | Περάστε ένα λεξικό `metadata` στο `write_pdf`, π.χ., `html_doc.write_pdf(target='out.pdf', metadata={'Title': 'Report'})`. |
| *Λαμβάνω σφάλμα “cairo‑cffi” σε Linux.* | Εγκαταστήστε το πακέτο συστήματος `libcairo2-dev` (`apt-get install libcairo2-dev` σε Debian/Ubuntu) πριν εγκαταστήσετε το WeasyPrint με pip. |

---

## Σύνοψη

Μόλις **created PDF from HTML** χρησιμοποιώντας μια καθαρή ροή εργασίας Python, καλύψαμε τη μηχανική του **convert HTML to PDF**, και σας δείξαμε πώς να **save HTML as PDF** με αξιόπιστη διαχείριση πόρων. Το script είναι αρκετά μικρό για να το ενσωματώσετε σε CI pipelines, αλλά και αρκετά ευέλικτο για να επεκταθεί με προσαρμοσμένες κεφαλίδες, υποσέλιδα ή υδατογραφήματα.

Επόμενα βήματα που μπορείτε να εξερευνήσετε:

- Χρησιμοποιήστε τη βιβλιοθήκη **html to pdf python** `pdfkit` για μια προσέγγιση βασισμένη στο wkhtmltopdf (καλή για παλαιότερο CSS).  
- Προσθέστε διεπαφή CLI με `argparse` ώστε το script να δέχεται ορίσματα εισόδου/εξόδου.  
- Δημιουργήστε PDFs σε πραγματικό χρόνο μέσα από ένα endpoint Flask ή FastAPI για αναφορές κατά απαίτηση.  

Νιώστε ελεύθεροι να πειραματιστείτε, να σπάσετε πράγματα, και μετά να επιστρέψετε σε αυτόν τον οδηγό για μια γρήγορη ανανέωση. Αν αντιμετωπίσετε προβλήματα, η τεκμηρίωση του WeasyPrint και τα φόρουμ της κοινότητας είναι εξαιρετικοί πόροι.

Καλή προγραμματιστική δουλειά, και απολαύστε τη μετατροπή αυτών των ιστοσελίδων σε κομψά PDFs!

## Τι Θα Μάθετε Στη Σύντομη Μέλλον;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Convert HTML to PDF with Aspose.HTML – Full Manipulation Guide](/html/english/)
- [Convert HTML to PDF in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Create PDF from HTML – C# Step‑by‑Step Guide](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}