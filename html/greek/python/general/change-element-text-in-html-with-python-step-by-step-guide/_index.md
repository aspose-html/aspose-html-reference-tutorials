---
category: general
date: 2026-09-23
description: Αλλάξτε το κείμενο ενός στοιχείου σε αρχείο HTML χρησιμοποιώντας Python.
  Μάθετε πώς να φορτώνετε αρχείο HTML, να επεξεργάζεστε την ετικέτα <title> και να
  ενημερώνετε τον τίτλο του HTML αποδοτικά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change element text
- how to change title
- edit title tag
- load html file
- update html title
language: el
lastmod: 2026-09-23
og_description: Αλλάξτε το κείμενο ενός στοιχείου σε ένα έγγραφο HTML χρησιμοποιώντας
  Python. Αυτό το σεμινάριο δείχνει πώς να φορτώσετε ένα αρχείο HTML, να επεξεργαστείτε
  την ετικέτα τίτλου και να ενημερώσετε τον τίτλο του HTML με λίγες μόνο γραμμές κώδικα.
og_image_alt: Screenshot showing change element text in HTML using Python code
og_title: Αλλαγή κειμένου στοιχείου σε HTML με Python – γρήγορος οδηγός
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Change element text in an HTML file using Python. Learn how to load
    HTML file, edit title tag, and update HTML title efficiently.
  headline: Change element text in HTML with Python – step‑by‑step guide
  type: TechArticle
- description: Change element text in an HTML file using Python. Learn how to load
    HTML file, edit title tag, and update HTML title efficiently.
  name: Change element text in HTML with Python – step‑by‑step guide
  steps:
  - name: 'Edge case: Multiple `<title>` tags'
    text: 'HTML standards allow only one `<title>` element, but malformed files sometimes
      contain more. If you need to handle that situation, iterate over all matches:'
  - name: Editing other elements (e.g., `<h1>`)
    text: 'If you need to **change element text** for a heading instead of the title,
      adjust the XPath:'
  - name: Preserving existing whitespace
    text: 'When the original HTML uses indentation inside tags, `pretty_print` may
      reformat it. To keep the original formatting, omit `pretty_print`:'
  - name: Working with Unicode characters
    text: '`lxml` handles Unicode automatically. Ensure the source file is saved with
      UTF‑8 encoding; otherwise, specify the correct encoding when opening the file.'
  type: HowTo
tags:
- Python
- HTML manipulation
- Web scraping
title: Αλλαγή κειμένου στοιχείου σε HTML με Python – βήμα‑βήμα οδηγός
url: /el/python/general/change-element-text-in-html-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αλλαγή κειμένου στοιχείου σε HTML με Python – βήμα‑βήμα οδηγός

Αν χρειάζεστε να **αλλάξετε το κείμενο ενός στοιχείου** σε ένα έγγραφο HTML, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε με Python. Είτε διορθώνετε μια παλιά ετικέτα `<title>` είτε ενημερώνετε οποιοδήποτε άλλο στοιχείο, θα μάθετε να **φορτώνετε αρχείο HTML**, να τροποποιείτε το κείμενο και να **ενημερώνετε τον τίτλο HTML** (ή οποιοδήποτε στοιχείο) με ασφάλεια.

Η αλλαγή του τίτλου μιας ιστοσελίδας είναι μια συνηθισμένη εργασία όταν καθαρίζετε δεδομένα που έχουν συλλεχθεί, δημιουργείτε στατικές σελίδες ή αυτοματοποιείτε ενημερώσεις SEO. Σε αυτό το tutorial θα:

* Φορτώσετε ένα αρχείο HTML από το δίσκο.
* Εντοπίσετε το στοιχείο `<title>` και **επεξεργαστείτε την ετικέτα τίτλου**.
* Αποθηκεύσετε το τροποποιημένο έγγραφο, ενημερώνοντας αποτελεσματικά **τον τίτλο HTML**.

Όλος ο απαιτούμενος κώδικας περιλαμβάνεται, και κάθε βήμα εξηγεί **γιατί** η ενέργεια είναι σημαντική, όχι μόνο **τι** πρέπει να πληκτρολογήσετε.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Εγκατεστημένο Python 3.9 ή νεότερο.
* Τη βιβλιοθήκη `lxml` (`pip install lxml`).  
  Η `lxml` παρέχει γρήγορη, συμβατή με πρότυπα ανάλυση και διαχείριση HTML.
* Έναν φάκελο που περιέχει το αρχείο HTML που θέλετε να επεξεργαστείτε (αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή).

## Βήμα 1: Φορτώστε το αρχείο HTML

Το πρώτο βήμα είναι να **φορτώσετε το αρχείο HTML** σε ένα δέντρο DOM (Document Object Model) ώστε η Python να μπορεί να εργαστεί με αυτό. Η χρήση του `lxml.html` σας παρέχει υποστήριξη XPath και αξιόπιστη διαχείριση στοιχείων.

```python
from pathlib import Path
from lxml import html

# Path to the source HTML document
source_path = Path("YOUR_DIRECTORY/page.html")

# Parse the file into an HTML tree
doc = html.parse(str(source_path))
```

**Γιατί είναι σημαντικό:**  
Η ανάλυση δημιουργεί μια δομημένη αναπαράσταση της σελίδας, επιτρέποντάς σας να ερωτάτε στοιχεία άμεσα. Χωρίς τη φόρτωση του αρχείου, δεν μπορείτε με ασφάλεια να **αλλάξετε το κείμενο ενός στοιχείου**, επειδή θα δουλεύατε με ακατέργαστες συμβολοσειρές, κάτι που είναι επιρρεπές σε σφάλματα.

## Βήμα 2: Εντοπίστε το στοιχείο `<title>` και **αλλάξτε το κείμενο του στοιχείου**

Τώρα που το έγγραφο έχει φορτωθεί, μπορείτε να **επεξεργαστείτε την ετικέτα τίτλου**. Η έκφραση XPath `".//title"` βρίσκει το πρώτο στοιχείο `<title>` στην ιεραρχία του εγγράφου.

```python
# Find the <title> element (the first occurrence)
title_elem = doc.find(".//title")

# Guard against missing <title>
if title_elem is None:
    raise ValueError("The document does not contain a <title> element.")

# Change the text inside the <title> tag
title_elem.text = "New Title"
```

**Γιατί είναι σημαντικό:**  
Η άμεση εκχώρηση στο `title_elem.text` **αλλάζει το κείμενο του στοιχείου** χωρίς να τροποποιεί το περιβάλλον markup. Αυτή η προσέγγιση διατηρεί τα κενά, τα σχόλια και άλλα ετικέτες, εξασφαλίζοντας ότι η έξοδος παραμένει έγκυρο HTML.

### Ακραία περίπτωση: Πολλαπλές ετικέτες `<title>`

Τα πρότυπα HTML επιτρέπουν μόνο ένα στοιχείο `<title>`, αλλά εσφαλμένα αρχεία μερικές φορές περιέχουν περισσότερα. Εάν χρειάζεται να διαχειριστείτε αυτήν την κατάσταση, επαναλάβετε πάνω σε όλες τις αντιστοιχίες:

```python
for t in doc.findall(".//title"):
    t.text = "New Title"
```

## Βήμα 3: Αποθηκεύστε το τροποποιημένο έγγραφο – **ενημερώστε τον τίτλο HTML**

Μετά την τροποποίηση, γράψτε το δέντρο ξανά στο δίσκο. Η χρήση του `pretty_print=True` διατηρεί το αρχείο αναγνώσιμο.

```python
# Destination path for the updated file
output_path = Path("YOUR_DIRECTORY/updated.html")

# Write the updated HTML back to a file
doc.write(str(output_path), encoding="utf-8", pretty_print=True)
print(f"HTML saved to {output_path}")
```

**Γιατί είναι σημαντικό:**  
Η αποθήκευση δημιουργεί ένα νέο αρχείο που αντανακλά τη λειτουργία **αλλαγής κειμένου στοιχείου**. Εάν χρειάζεται να αντικαταστήσετε το αρχικό αρχείο, απλώς χρησιμοποιήστε την ίδια διαδρομή για το `output_path`.

## Πλήρες σενάριο σε ένα μπλοκ

Συνδυάζοντας όλα μαζί, εδώ είναι ένα αυτόνομο σενάριο που **φορτώνει αρχείο HTML**, **αλλάζει το κείμενο του στοιχείου** και **ενημερώνει τον τίτλο HTML**:

```python
"""Change element text in an HTML document – update the <title> tag."""

from pathlib import Path
from lxml import html

def change_title(source: str, new_title: str, destination: str) -> None:
    """Load an HTML file, edit its title, and save the result."""
    # Load the HTML document
    doc = html.parse(source)

    # Locate the <title> element
    title_elem = doc.find(".//title")
    if title_elem is None:
        raise ValueError("No <title> element found in the document.")

    # Change element text
    title_elem.text = new_title

    # Save the updated document
    doc.write(destination, encoding="utf-8", pretty_print=True)

if __name__ == "__main__":
    src = "YOUR_DIRECTORY/page.html"
    dst = "YOUR_DIRECTORY/updated.html"
    change_title(src, "New Title", dst)
    print(f"Updated title saved to {dst}")
```

Η εκτέλεση αυτού του σεναρίου παράγει ένα αρχείο `updated.html` του οποίου το `<title>` τώρα εμφανίζει **New Title**.

## Συνηθισμένες παραλλαγές της τεχνικής

### Επεξεργασία άλλων στοιχείων (π.χ., `<h1>`)

Εάν χρειάζεται να **αλλάξετε το κείμενο ενός στοιχείου** για μια επικεφαλίδα αντί για τον τίτλο, προσαρμόστε το XPath:

```python
heading = doc.find(".//h1")
if heading is not None:
    heading.text = "Updated Heading"
```

### Διατήρηση του υπάρχοντος whitespace

Όταν το αρχικό HTML χρησιμοποιεί εσοχές μέσα στις ετικέτες, το `pretty_print` μπορεί να το επαναμορφοποιήσει. Για να διατηρήσετε την αρχική μορφοποίηση, παραλείψτε το `pretty_print`:

```python
doc.write(destination, encoding="utf-8")
```

### Εργασία με χαρακτήρες Unicode

Η `lxml` διαχειρίζεται αυτόματα το Unicode. Βεβαιωθείτε ότι το αρχείο προέλευσης είναι αποθηκευμένο με κωδικοποίηση UTF‑8· διαφορετικά, καθορίστε τη σωστή κωδικοποίηση όταν ανοίγετε το αρχείο.

## Συμβουλές και παγίδες

* **Συμβουλή:** Χρησιμοποιήστε `doc.xpath("//title/text()")` αν χρειάζεστε μόνο το κείμενο χωρίς να τροποποιήσετε το στοιχείο.
* **Προσοχή:** Αρχεία HTML που περιέχουν ένα `<title>` μέσα σε `<svg>` ή άλλο μη‑HTML namespace. Σε τέτοιες περιπτώσεις, βελτιώστε το XPath ώστε να στοχεύει στην ενότητα `<head>`: `doc.find(".//head/title")`.
* **Συμβουλή απόδοσης:** Για επεξεργασία παρτίδας χιλιάδων αρχείων, επαναχρησιμοποιήστε το ίδιο αντικείμενο parser για να μειώσετε το κόστος.

## Συμπέρασμα

Τώρα ξέρετε πώς να **αλλάξετε το κείμενο ενός στοιχείου** σε ένα έγγραφο HTML χρησιμοποιώντας Python, συγκεκριμένα πώς να **φορτώνετε αρχείο HTML**, **επεξεργάζεστε την ετικέτα τίτλου**, και **ενημερώνετε τον τίτλο HTML**. Το πλήρες παράδειγμα δείχνει μια αξιόπιστη, βασισμένη σε βιβλιοθήκη προσέγγιση που λειτουργεί τόσο για καλά δομημένο όσο και για ελαφρώς εσφαλμένο HTML.

Από εδώ μπορείτε:

* Εφαρμόσετε το ίδιο μοτίβο σε άλλες ετικέτες (`<h2>`, `<meta>`, κλπ.).
* Συνδυάσετε αυτό το σενάριο με μια αλυσίδα web‑scraping για να καθαρίσετε μεγάλες συλλογές σελίδων.
* Εξερευνήσετε το πιο πλούσιο API της `lxml` για διαχείριση χαρακτηριστικών, CSS selectors και σειριοποίηση HTML.

Καλή προγραμματιστική δουλειά, και μη διστάσετε να πειραματιστείτε με διαφορετικά στοιχεία για να κυριαρχήσετε στη διαχείριση HTML με Python!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Φόρτωση εγγράφων HTML από αρχείο στο Aspose.HTML για Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Πώς να επεξεργαστείτε το δέντρο εγγράφου HTML στο Aspose.HTML για Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Πώς να αναλύσετε HTML Java – Φόρτωση, Ερώτημα & Καταμέτρηση Στοιχείων](/html/english/java/creating-managing-html-documents/how-to-parse-html-java-load-query-count-elements/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}