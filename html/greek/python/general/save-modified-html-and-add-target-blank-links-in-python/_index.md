---
category: general
date: 2026-11-24
description: Αποθήκευση τροποποιημένου HTML και προσθήκη συνδέσμων με target="_blank"
  σε Python χρησιμοποιώντας το Aspose.HTML. Μάθετε πώς να αλλάζετε το target του href
  για όλες τις ετικέτες <a> και να ανοίγετε όλους τους συνδέσμους σε νέα καρτέλα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save modified html
- add target blank links
- change href target
- open all links newtab
language: el
lastmod: 2026-11-24
og_description: Αποθηκεύστε το τροποποιημένο HTML και προσθέστε συνδέσμους με target
  blank σε Python με το Aspose.HTML. Ακολουθήστε αυτό το βήμα‑βήμα οδηγό για να αλλάξετε
  το target του href και να ανοίξετε όλους τους συνδέσμους σε νέα καρτέλα.
og_image_alt: Screenshot of a Python script that saves modified HTML with target='_blank'
  on every link
og_title: Αποθήκευση τροποποιημένου HTML και προσθήκη συνδέσμων target="_blank" σε
  Python – πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-11-24'
  description: Save modified HTML and add target blank links in Python using Aspose.HTML.
    Learn how to change href target for all <a> tags and open all links newtab.
  headline: Save modified HTML and add target blank links in Python
  type: TechArticle
tags:
- Aspose.HTML
- Python
- HTML manipulation
- Web automation
title: Αποθήκευση τροποποιημένου HTML και προσθήκη συνδέσμων target="_blank" σε Python
url: /el/python/general/save-modified-html-and-add-target-blank-links-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αποθήκευση τροποποιημένου HTML και προσθήκη συνδέσμων target blank σε Python

Αν χρειάζεστε να **αποθηκεύσετε τροποποιημένο HTML** μετά την ενημέρωση κάθε συνδέσμου, αυτός ο οδηγός σας δείχνει πώς να το κάνετε με το Aspose.HTML for Python. Θα μάθετε πώς να **προσθέτετε συνδέσμους target blank**, να αλλάζετε το στόχο του href και να κάνετε όλους τους συνδέσμους να ανοίγουν σε νέα καρτέλα.

Ο οδηγός καλύπτει τα πάντα, από τη φόρτωση ενός αρχείου HTML μέχρι την επαλήθευση ότι οι αλλαγές γράφτηκαν σωστά. Δεν απαιτούνται εξωτερικά εργαλεία εκτός από τη βιβλιοθήκη Aspose.HTML.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Python 3.8 ή νεότερη έκδοση εγκατεστημένη  
* Ένα ενεργό άδεια Aspose.HTML for Python (ή ένα δωρεάν κλειδί αξιολόγησης)  
* Ένα τοπικό αρχείο HTML που θέλετε να τροποποιήσετε (π.χ., `index.html`)  

Μπορείτε να εγκαταστήσετε τη βιβλιοθήκη με pip:

```bash
pip install aspose-html
```

## Βήμα 1: Φόρτωση του εγγράφου HTML

Το πρώτο βήμα είναι να δημιουργήσετε μια παρουσία `HTMLDocument` που δείχνει στο αρχείο προέλευσης. Αυτό το αντικείμενο αντιπροσωπεύει ολόκληρο το δέντρο DOM, επιτρέποντάς σας να ερωτήσετε και να επεξεργαστείτε στοιχεία.

```python
from aspose.html import HTMLDocument

# Load the original HTML file
doc = HTMLDocument("YOUR_DIRECTORY/index.html")
```

*Γιατί είναι σημαντικό*: Η φόρτωση του εγγράφου σας δίνει προγραμματιστική πρόσβαση σε κάθε κόμβο, κάτι που απαιτείται για μαζικές ενημερώσεις όπως η αλλαγή του χαρακτηριστικού `target` σε όλα τα `<a>` tags.

## Βήμα 2: Προσθήκη συνδέσμων target blank σε κάθε άγκυρα

Για να κάνετε κάθε υπερσύνδεσμο να ανοίγει σε νέα καρτέλα, ορίζετε το χαρακτηριστικό `target` σε `_blank`. Η μέθοδος `query_selector_all` επιστρέφει μια ζωντανή συλλογή όλων των στοιχείων `<a>`, ανεξαρτήτως βάθους εμφώλευσης.

```python
# Update all <a> tags to open links in a new tab
for link in doc.query_selector_all("a"):
    link.set_attribute("target", "_blank")
```

**Βασικά σημεία**

* Ο βρόχος αγγίζει κάθε άγκυρα ακριβώς μία φορά, εξασφαλίζοντας ότι η **προσθήκη συνδέσμων target blank** εφαρμόζεται ομοιόμορφα.  
* Αν ένας σύνδεσμος έχει ήδη το χαρακτηριστικό `target`, η κλήση το αντικαθιστά, εξασφαλίζοντας συνεπή συμπεριφορά.  

### Διαχείριση υπαρχουσών τιμών `target` (προαιρετικό)

Αν προτιμάτε να διατηρήσετε τα υπάρχοντα `target` και να ορίσετε `_blank` μόνο όταν λείπει το χαρακτηριστικό, προσθέστε έναν έλεγχο συνθήκης:

```python
for link in doc.query_selector_all("a"):
    if not link.has_attribute("target"):
        link.set_attribute("target", "_blank")
```

## Βήμα 3: Αλλαγή του στόχου href και άνοιγμα όλων των συνδέσμων σε νέα καρτέλα

Μερικές φορές χρειάζεται να ξαναγράψετε το ίδιο το χαρακτηριστικό `href` — ίσως για να προσθέσετε μια βασική διεύθυνση URL ή για να μετατρέψετε σχετικές διαδρομές σε απόλυτες URL. Η ίδια τεχνική διάσχισης του DOM λειτουργεί και για αλλαγές του `href`.

```python
base_url = "https://example.com/"

for link in doc.query_selector_all("a"):
    href = link.get_attribute("href")
    # Skip empty or already absolute URLs
    if href and not href.startswith("http"):
        new_href = base_url + href.lstrip("/")
        link.set_attribute("href", new_href)
    # Ensure the link opens in a new tab
    link.set_attribute("target", "_blank")
```

*Γιατί είναι σημαντικό*: Με την **αλλαγή του στόχου href** και την εξασφάλιση του **άνοιγμα όλων των συνδέσμων σε νέα καρτέλα**, εγγυάστε ότι οι χρήστες κατευθύνονται στη σωστή τοποθεσία και ότι η πλοήγηση γίνεται χωρίς να φύγουν από την τρέχουσα σελίδα.

## Βήμα 4: Αποθήκευση του τροποποιημένου εγγράφου

Αφού ολοκληρωθούν όλες οι τροποποιήσεις, καλέστε `save` για να γράψετε τις αλλαγές σε νέο αρχείο. Αυτό είναι το σημείο όπου η **αποθήκευση τροποποιημένου html** πραγματικά συμβαίνει.

```python
# Save the updated HTML to a new file
doc.save("YOUR_DIRECTORY/index_modified.html")
```

Το παραγόμενο `index_modified.html` περιέχει κάθε `<a>` tag με `target="_blank"` και τυχόν ενημερωμένες τιμές `href`. Μπορείτε να ανοίξετε το αρχείο σε πρόγραμμα περιήγησης για να επαληθεύσετε ότι το κλικ σε οποιονδήποτε σύνδεσμο ανοίγει νέα καρτέλα.

## Βήμα 5: Επαλήθευση του αποτελέσματος (προαιρετικό)

Μια γρήγορη έλεγχος λογικής βοηθά να επιβεβαιώσετε ότι η λειτουργία ολοκληρώθηκε με επιτυχία:

```python
# Reload the saved file to verify changes
verify_doc = HTMLDocument("YOUR_DIRECTORY/index_modified.html")
for link in verify_doc.query_selector_all("a"):
    assert link.get_attribute("target") == "_blank", "Target attribute not set correctly"
print("All links have target='_blank' and the file was saved successfully.")
```

Αν η δήλωση αποτύχει, το script θα ρίξει σφάλμα, υποδεικνύοντας το προβληματικό στοιχείο.

## Συμβουλή επαγγελματία: Επεξεργασία πολλαπλών αρχείων σε παρτίδες

Όταν έχετε έναν φάκελο γεμάτο αρχεία HTML, τυλίξτε τη λογική σε μια συνάρτηση και επαναλάβετε τη διαδικασία για κάθε αρχείο:

```python
import os
from aspose.html import HTMLDocument

def process_file(input_path: str, output_path: str, base_url: str = None):
    doc = HTMLDocument(input_path)
    for link in doc.query_selector_all("a"):
        if base_url:
            href = link.get_attribute("href")
            if href and not href.startswith("http"):
                link.set_attribute("href", base_url + href.lstrip("/"))
        link.set_attribute("target", "_blank")
    doc.save(output_path)

source_dir = "YOUR_DIRECTORY"
for filename in os.listdir(source_dir):
    if filename.endswith(".html"):
        src = os.path.join(source_dir, filename)
        dst = os.path.join(source_dir, f"{os.path.splitext(filename)[0]}_modified.html")
        process_file(src, dst, base_url="https://example.com/")
```

Αυτό το μοτίβο κλιμακώνει τη ροή εργασίας **αποθήκευσης τροποποιημένου html** σε οποιονδήποτε αριθμό σελίδων, διατηρώντας σταθερά την **προσθήκη συνδέσμων target blank** και την **αλλαγή του στόχου href**.

## Αναμενόμενο αποτέλεσμα

Ανοίγοντας το `index_modified.html` σε πρόγραμμα περιήγησης θα πρέπει να εμφανίζεται η ίδια οπτική διάταξη με την αρχική σελίδα, αλλά κάθε υπερσύνδεσμος τώρα περιλαμβάνει:

```html
<a href="https://example.com/about.html" target="_blank">About Us</a>
```

Κάνοντας κλικ στον σύνδεσμο, η προοριστική σελίδα ανοίγει σε νέα καρτέλα του προγράμματος περιήγησης, διατηρώντας τη τρέχουσα σελίδα του χρήστη.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Πρόβλημα | Εξήγηση | Διόρθωση |
|----------|----------|----------|
| Λείπει άδεια Aspose.HTML | Η βιβλιοθήκη ρίχνει σφάλμα άδειας κατά την εκτέλεση. | Αποκτήστε ένα αρχείο άδειας και ορίστε `aspose.html.License().set_license("license_path")` πριν τη φόρτωση του εγγράφου. |
| Σχετικές URL που ξεκινούν με `//` | Αντιμετωπίζονται ως URL σχετικών πρωτοκόλλων και μπορεί να παραμείνουν αμετάβλητες. | Προσθέστε έναν έλεγχο για `href.startswith("//")` και προσθέστε `https:` εάν χρειάζεται. |
| Πολύ μεγάλα αρχεία HTML | Η φόρτωση τεράστιων αρχείων μπορεί να καταναλώσει σημαντική μνήμη. | Χρησιμοποιήστε streaming APIs ή χωρίστε το αρχείο σε μικρότερα τμήματα εάν η μνήμη γίνει περιοριστικός παράγοντας. |

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **αποθηκεύσετε τροποποιημένο HTML** μετά την εφαρμογή των **προσθήκη συνδέσμων target blank**, **αλλαγή στόχου href**, και την εξασφάλιση του **ανοίγματος όλων των συνδέσμων σε νέα καρτέλα** χρησιμοποιώντας το Aspose.HTML for Python. Η πλήρης λύση φορτώνει ένα αρχείο HTML, ενημερώνει κάθε στοιχείο `<a>` και γράφει το αποτέλεσμα σε νέο αρχείο, αντιμετωπίζοντας περιπτώσεις όπως υπάρχοντα χαρακτηριστικά `target` και σχετικές URL.

Στη συνέχεια, μπορείτε να εξερευνήσετε:

* Χρήση CSS selectors για στόχευση μόνο εξωτερικών συνδέσμων (`a[href^="http"]`)  
* Ενσωμάτωση JavaScript που προσθέτει `rel="noopener"` για ασφάλεια κατά το άνοιγμα νέων καρτελών  
* Μετατροπή του τροποποιημένου HTML σε PDF με το Aspose.PDF for Python  

Αισθανθείτε ελεύθεροι να προσαρμόσετε τον κώδικα στη δική σας δομή έργου και να πειραματιστείτε με πρόσθετες επεμβάσεις DOM. Καλή προγραμματιστική εργασία!

## Τι πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να αποθηκεύσετε HTML ως PDF με Aspose.HTML for Python](/html/english/python/general/how-to-save-html-as-pdf-with-aspose-html-for-python/)
- [Πώς να αποθηκεύσετε HTML ως Markdown με Aspose.HTML for Python](/html/english/python/general/how-to-save-html-as-markdown-with-aspose-html-for-python/)
- [Πώς να χρησιμοποιήσετε το Aspose – Μετατροπή HTML σε Markdown και εξαγωγή συνδέσμων](/html/english/python/general/how-to-use-aspose-convert-html-to-markdown-and-extract-links/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}