---
category: general
date: 2026-09-19
description: Πώς να ενεργοποιήσετε λειτουργίες κατά τη μετατροπή HTML σε Markdown
  χρησιμοποιώντας Python. Μάθετε πώς να μετατρέψετε ένα έγγραφο HTML και να αποθηκεύσετε
  το HTML ως Markdown με ακριβή έλεγχο των λειτουργιών.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable features
- convert html to markdown
- how to convert html
- convert html document
- save html as markdown
language: el
lastmod: 2026-09-19
og_description: Πώς να ενεργοποιήσετε λειτουργίες κατά τη μετατροπή HTML σε Markdown.
  Αυτός ο οδηγός σας δείχνει βήμα‑βήμα πώς να μετατρέψετε ένα έγγραφο HTML και να
  αποθηκεύσετε το HTML ως Markdown με λεπτομερή έλεγχο.
og_image_alt: Screenshot of Python code that enables features for HTML‑to‑Markdown
  conversion
og_title: Πώς να ενεργοποιήσετε λειτουργίες κατά τη μετατροπή του HTML σε Markdown
schemas:
- author: GroupDocs
  dateModified: '2026-09-19'
  description: How to enable features while converting HTML to Markdown using Python.
    Learn to convert HTML document and save HTML as Markdown with precise feature
    control.
  headline: How to enable features while converting HTML to Markdown
  type: TechArticle
tags:
- HTML conversion
- Markdown
- Python
title: Πώς να ενεργοποιήσετε λειτουργίες κατά τη μετατροπή του HTML σε Markdown
url: /el/python/general/how-to-enable-features-while-converting-html-to-markdown/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ενεργοποιήσετε λειτουργίες κατά τη μετατροπή HTML σε Markdown

Αν χρειάζεστε **πώς να ενεργοποιήσετε λειτουργίες** κατά τη διάρκεια μιας μετατροπής, αυτός ο οδηγός σας παρέχει μια πλήρη, εκτελέσιμη λύση. Θα δείτε ακριβώς πώς να μετατρέψετε HTML σε Markdown, να ελέγξετε ποιες λειτουργίες του Markdown παράγονται, και να αποθηκεύσετε το HTML ως Markdown σε μία μόνο εκτέλεση.

Το παράδειγμα χρησιμοποιεί το δημοφιλές **GroupDocs.Conversion** Python SDK, αλλά οι έννοιες ισχύουν για οποιαδήποτε βιβλιοθήκη που σας επιτρέπει να διαμορφώσετε σύνολα λειτουργιών. Στο τέλος αυτού του οδηγού μπορείτε να μετατρέψετε ένα έγγραφο HTML, να διατηρήσετε μόνο συνδέσμους και παραγράφους, και να αποφύγετε ανεπιθύμητους πίνακες, εικόνες ή μπλοκ κώδικα.

## Τι θα επιτύχετε

* **πώς να ενεργοποιήσετε λειτουργίες** στις επιλογές αποθήκευσης Markdown  
* μια σαφής ροή εργασίας **μετατροπής html σε markdown**  
* η δυνατότητα **πώς να μετατρέψετε html** με επιλεκτική έξοδο  
* ένα έτοιμο‑για‑εκτέλεση script που **μετατρέπει έγγραφο html** και **αποθηκεύει html ως markdown**  

### Προαπαιτούμενα

* Python 3.8+ εγκατεστημένο  
* πακέτο `groupdocs-conversion` (εγκατάσταση με `pip install groupdocs-conversion`)  
* Ένα δείγμα αρχείου HTML (`sample.html`) σε γνωστό φάκελο  

---

## Πώς να ενεργοποιήσετε λειτουργίες στη μετατροπή Markdown

Το πρώτο βήμα είναι να δημιουργήσετε ένα αντικείμενο `MarkdownSaveOptions` και να πείτε στον μετατροπέα ποια στοιχεία θέλετε να διατηρήσετε. Σε αυτόν τον οδηγό ενεργοποιούμε μόνο **links** και **paragraphs**.

```python
# Import the required classes from the GroupDocs.Conversion SDK
from groupdocs.conversion import Converter, HTMLDocument, MarkdownSaveOptions

# Step 1: Load the source HTML document
html_doc = HTMLDocument("YOUR_DIRECTORY/sample.html")

# Step 2: Create Markdown save options
markdown_options = MarkdownSaveOptions()

# Step 3: Enable only the desired features (links and paragraphs)
markdown_options.features = ["Link", "Paragraph"]

# Step 4: Convert the HTML document to Markdown using the configured options
Converter.convert_html(html_doc, "YOUR_DIRECTORY/sample.md", markdown_options)
```

**Γιατί λειτουργεί αυτό:**  
* `HTMLDocument` τυλίγει το αρχείο προέλευσης ώστε ο μετατροπέας να μπορεί να το διαβάσει.  
* `MarkdownSaveOptions` περιέχει όλες τις ρυθμίσεις μετατροπής· η λίστα `features` είναι η κύρια ιδιότητα που **πώς να ενεργοποιήσετε λειτουργίες**.  
* Αναθέτοντας `["Link", "Paragraph"]` λέτε στη μηχανή να παράγει μόνο συνδέσμους Markdown (`[text](url)`) και απλές παραγράφους, απορρίπτοντας εικόνες, πίνακες και άλλα στοιχεία.  
* `Converter.convert_html` εκτελεί την πραγματική λειτουργία **convert html to markdown** και γράφει το αποτέλεσμα στο `sample.md`.

---

## Πώς να μετατρέψετε έγγραφο HTML με προσαρμοσμένες επιλογές

Αν αργότερα χρειαστεί να προσθέσετε περισσότερες σημαίες λειτουργιών—όπως `"Header"` ή `"Bold"`—απλώς επεκτείνετε τη λίστα:

```python
# Enable links, paragraphs, headers, and bold text
markdown_options.features = ["Link", "Paragraph", "Header", "Bold"]
```

Η ίδια κλήση στο `Converter.convert_html` θα συμπεριλάβει τώρα αυτά τα επιπλέον στοιχεία. Αυτό το μοτίβο σας επιτρέπει να **πώς να μετατρέψετε html** με έναν πολύ παραμετροποιήσιμο τρόπο χωρίς να γράψετε προσαρμοσμένους αναλυτές.

---

## Πώς να αποθηκεύσετε HTML ως Markdown σε συγκεκριμένο φάκελο

Η μέθοδος `convert_html` δέχεται απόλυτη ή σχετική διαδρομή εξόδου. Για να **αποθηκεύσετε html ως markdown** σε έναν υπο‑φάκελο που ονομάζεται `output`, προσαρμόστε το τρίτο όρισμα:

```python
output_path = "YOUR_DIRECTORY/output/sample.md"
Converter.convert_html(html_doc, output_path, markdown_options)
```

Η εκτέλεση του script δημιουργεί το φάκελο `output` (αν δεν υπάρχει) και γράφει το αρχείο Markdown εκεί. Αυτή η προσέγγιση διατηρεί το πηγαίο HTML και το παραγόμενο Markdown οργανωμένα.

---

## Πλήρες script που μπορείτε να αντιγράψετε‑και‑επικολλήσετε

Παρακάτω βρίσκεται ολόκληρο το πρόγραμμα, έτοιμο για εκτέλεση. Αντικαταστήστε το `YOUR_DIRECTORY` με τη διαδρομή που περιέχει το `sample.html`.

```python
# -*- coding: utf-8 -*-
"""
How to enable features while converting HTML to Markdown

This script demonstrates:
* loading an HTML document,
* configuring MarkdownSaveOptions to keep only links and paragraphs,
* converting the HTML to Markdown,
* and saving the result to a .md file.
"""

from pathlib import Path
from groupdocs.conversion import Converter, HTMLDocument, MarkdownSaveOptions

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
BASE_DIR = Path("YOUR_DIRECTORY")                # <— change this
HTML_FILE = BASE_DIR / "sample.html"
OUTPUT_MD = BASE_DIR / "sample.md"               # <— change if you want a different name

# ----------------------------------------------------------------------
# Step 1: Load the source HTML document
# ----------------------------------------------------------------------
html_doc = HTMLDocument(str(HTML_FILE))

# ----------------------------------------------------------------------
# Step 2: Create and configure Markdown save options
# ----------------------------------------------------------------------
markdown_options = MarkdownSaveOptions()
# Enable only the desired features (links and paragraphs)
markdown_options.features = ["Link", "Paragraph"]

# ----------------------------------------------------------------------
# Step 3: Perform the conversion and write the Markdown file
# ----------------------------------------------------------------------
Converter.convert_html(html_doc, str(OUTPUT_MD), markdown_options)

print(f"Conversion complete. Markdown saved to: {OUTPUT_MD}")
```

**Αναμενόμενη έξοδος** (εκτυπώνεται στην κονσόλα):

```
Conversion complete. Markdown saved to: /path/to/YOUR_DIRECTORY/sample.md
```

Ανοίξτε το `sample.md` και θα δείτε μόνο συνδέσμους Markdown και απλές παραγράφους, για παράδειγμα:

```markdown
This is a paragraph with a [link](https://example.com) inside.
Another paragraph follows without any images or tables.
```

Όλα τα άλλα στοιχεία HTML έχουν παραλειφθεί επειδή η **πώς να ενεργοποιήσετε λειτουργίες** περιορίσθηκε η έξοδος στους δύο επιλεγμένους τύπους.

---

## Συχνές ερωτήσεις και ειδικές περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| *Τι γίνεται αν το αρχείο HTML δεν περιέχει συνδέσμους;* | Ο μετατροπέας εξακολουθεί να γράφει τις παραγράφους· η έξοδος θα περιέχει απλό κείμενο χωρίς σύνταξη συνδέσμου. |
| *Μπορώ να απενεργοποιήσω όλες τις λειτουργίες;* | Ορίζοντας `markdown_options.features = []` παράγει ένα κενό αρχείο Markdown. Χρησιμοποιήστε το μόνο για δοκιμές. |
| *Πώς διαχειρίζεται το SDK το μη έγκυρο HTML;* | Ο parser προσπαθεί να καθαρίσει το κακοδιατυπωμένο markup πριν εφαρμόσει το φίλτρο λειτουργιών. Τα σφάλματα καταγράφονται αλλά δεν διακόπτουν τη μετατροπή. |
| *Είναι δυνατόν να διατηρηθούν οι εικόνες ενώ απορρίπτονται οι πίνακες;* | Ναι. Ορίστε `markdown_options.features = ["Link", "Paragraph", "Image"]`. Η λίστα λειτουργιών είναι προσθετική, όχι αποκλειστική. |
| *Τι γίνεται αν χρειαστεί να μετατρέψετε πολλά αρχεία σε έναν φάκελο;* | Τυλίξτε τη λογική μετατροπής σε βρόχο που επαναλαμβάνει πάνω από `Path.glob("*.html")`. Η ίδια **πώς να ενεργοποιήσετε λειτουργίες** διαμόρφωση μπορεί να επαναχρησιμοποιηθεί για κάθε αρχείο. |

**Συμβουλή:** Όταν επεξεργάζεστε μεγάλες παρτίδες, δημιουργήστε το `MarkdownSaveOptions` μία φορά και επαναχρησιμοποιήστε το. Αυτό μειώνει το κόστος δημιουργίας αντικειμένων και διατηρεί την **convert html to markdown** γραμμή εργασίας γρήγορη.

---

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να ενεργοποιήσετε λειτουργίες** όταν **μετατρέπετε html σε markdown**, πώς να **πώς να μετατρέψετε html** με επιλεκτική έξοδο, και πώς να **μετατρέψετε έγγραφο html** και **αποθηκεύετε html ως markdown** χρησιμοποιώντας ένα σύντομο script Python. Με τη διαμόρφωση του `MarkdownSaveOptions.features`, αποκτάτε πλήρη έλεγχο των στοιχείων Markdown που εμφανίζονται στο τελικό αρχείο.

### Επόμενα βήματα

* Εξερευνήστε πρόσθετες σημαίες λειτουργιών όπως `"Header"`, `"Bold"` και `"Italic"` για να εμπλουτίσετε την έξοδο Markdown.  
* Συνδυάστε αυτό το script με έναν παρακολουθητή αρχείων (π.χ., `watchdog`) για να μετατρέπετε αυτόματα νέα αρχεία HTML καθώς εμφανίζονται.  
* Ανασκοπήστε την [GroupDocs.Conversion Python SDK documentation](https://github.com/groupdocs-conversion/GroupDocs.Conversion-Examples) για προχωρημένα σενάρια όπως μετατροπές PDF‑to‑Markdown ή DOCX‑to‑HTML.

Νιώστε ελεύθεροι να πειραματιστείτε με διαφορετικά σύνολα λειτουργιών και να μοιραστείτε τα ευρήματά σας με την κοινότητα. Καλή μετατροπή!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες λειτουργίες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Μετατροπή HTML σε Markdown στο Aspose.HTML για Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Markdown σε HTML Java - Μετατροπή με Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)
- [Πώς να Ενεργοποιήσετε JavaScript στο Aspose HTML – Φόρτωση HTML & Λήψη Κειμένου](/html/english/java/advanced-usage/how-to-enable-javascript-in-aspose-html-load-html-get-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}