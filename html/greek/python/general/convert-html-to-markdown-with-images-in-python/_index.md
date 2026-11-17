---
category: general
date: 2026-11-17
description: Μετατρέψτε το HTML σε markdown με εικόνες σε Python – μάθετε πώς να μετατρέψετε
  γρήγορα το HTML διατηρώντας τις εικόνες ανέπαφες.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- how to convert html
- export html with images
- markdown conversion with images
language: el
lastmod: 2026-11-17
og_description: Μετατρέψτε HTML σε markdown με εικόνες σε Python. Αυτό το σεμινάριο
  δείχνει πώς να μετατρέψετε HTML εξάγοντας τις εικόνες, παρέχοντάς σας μια πλήρη,
  έτοιμη προς εκτέλεση λύση.
og_image_alt: Diagram showing convert html to markdown workflow with image extraction
og_title: Μετατροπή HTML σε markdown με εικόνες σε Python – γρήγορος οδηγός
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Convert HTML to markdown with images in Python – learn how to convert
    HTML quickly while exporting images intact.
  headline: Convert HTML to markdown with images in Python
  type: TechArticle
tags:
- HTML
- Markdown
- Python
- Image extraction
title: Μετατροπή HTML σε markdown με εικόνες σε Python
url: /el/python/general/convert-html-to-markdown-with-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή HTML σε markdown με εικόνες σε Python

Αν χρειάζεστε **convert HTML to markdown** ενώ διατηρείτε τις εικόνες ως ξεχωριστά αρχεία, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε. Θα λάβετε ένα πλήρες, εκτελέσιμο παράδειγμα που διαχειρίζεται εξωτερικούς πόρους, ώστε η έξοδος markdown να αναφέρεται σωστά στις αρχικές εικόνες.

Η εξαγωγή HTML με εικόνες συχνά προκαλεί προβλήματα σε απλούς μετατροπείς, επειδή είτε αφαιρούν τις εικόνες είτε τις ενσωματώνουν ως αλφαριθμητικά base64. Με τη ρύθμιση των επιλογών διαχείρισης πόρων, διατηρείτε τα αρχικά αρχεία εικόνας και παράγετε καθαρό markdown που μπορεί να ελεγχθεί με version‑control ή να επεξεργαστεί αργότερα.

Σε αυτό το tutorial θα:

* Φορτώσετε ένα έγγραφο HTML από το δίσκο.  
* Ρυθμίσετε τον μετατροπέα για **export HTML with images** ως ξεχωριστά αρχεία.  
* Αποθηκεύσετε το αποτέλεσμα ως markdown χρησιμοποιώντας τις επιλογές **markdown conversion with images**.  

Η μόνη προϋπόθεση είναι μια πρόσφατη έκδοση της βιβλιοθήκης Aspose.HTML for Python (ή οποιοδήποτε συμβατό API που παρέχει `HTMLDocument`, `ResourceHandlingOptions`, `MarkdownSaveOptions` και `Converter`). Χρειάζεστε επίσης Python 3.8+ και δικαιώματα εγγραφής στον φάκελο εξόδου.

---

## Προαπαιτούμενα και εγκατάσταση

1. Εγκαταστήστε το πακέτο Aspose.HTML:

   ```bash
   pip install aspose-html
   ```

2. Επαληθεύστε την εγκατάσταση:

   ```python
   import aspose.html as ah
   print(ah.__version__)   # should print the installed version, e.g., 22.9
   ```

> **Pro tip:** Χρησιμοποιήστε ένα εικονικό περιβάλλον για να αποφύγετε συγκρούσεις εκδόσεων με άλλα έργα.

---

## Βήμα 1: Φόρτωση του πηγαίου εγγράφου HTML

Το πρώτο βήμα είναι να δημιουργήσετε ένα αντικείμενο `HTMLDocument` που αντιπροσωπεύει το πηγαίο αρχείο. Αυτό το αντικείμενο αναλύει τη σήμανση και δημιουργεί ένα δέντρο DOM που μπορεί να διασχίσει ο μετατροπέας.

```python
from aspose.html import HTMLDocument

# Load the HTML file you want to convert
html_path = "YOUR_DIRECTORY/sample.html"
html_doc = HTMLDocument(html_path)
```

*Γιατί είναι σημαντικό* – Η φόρτωση του εγγράφου δίνει στη βιβλιοθήκη πλήρη έλεγχο της σήμανσης, επιτρέποντας της να επιλύει σχετικές URL και να εφαρμόζει τη διαχείριση πόρων αργότερα.

---

## Βήμα 2: Διαμόρφωση διαχείρισης εξωτερικών πόρων

Όταν **export HTML with images**, συνήθως θέλετε οι εικόνες να αποθηκεύονται δίπλα στο αρχείο markdown αντί να ενσωματώνονται. Η κλάση `ResourceHandlingOptions` σας επιτρέπει να καθορίσετε αυτή τη συμπεριφορά.

```python
from aspose.html import ResourceHandlingOptions

resource_options = ResourceHandlingOptions()
resource_options.save_external_resources = True   # keep images as separate files
```

Ορίζοντας το `save_external_resources` σε `True` υποδεικνύει στον μετατροπέα να αντιγράψει κάθε εξωτερικό πόρο (εικόνες, CSS, γραμματοσειρές) σε έναν φάκελο δίπλα στην έξοδο markdown. Το αρχείο markdown θα περιέχει σχετικούς συνδέσμους που οδηγούν σε αυτά τα αντίγραφα.

---

## Βήμα 3: Σύνδεση της διαμόρφωσης διαχείρισης πόρων με τις επιλογές markdown

`MarkdownSaveOptions` ελέγχει πώς πραγματοποιείται η μετατροπή σε markdown. Αναθέτοντας την ιδιότητα `resource_handling_options`, ενεργοποιείτε τη λειτουργία **markdown conversion with images**.

```python
from aspose.html import MarkdownSaveOptions

markdown_options = MarkdownSaveOptions()
markdown_options.resource_handling_options = resource_options
```

Αν παραλείψετε αυτό το βήμα, ο μετατροπέας θα αφαιρέσει τις αναφορές εικόνων ή θα τις ενσωματώσει ως data URIs, κάτι που αναιρεί τον σκοπό της εξαγωγής εικόνων.

---

## Βήμα 4: Εκτέλεση της μετατροπής

Τέλος, καλέστε το `Converter.convert` με το πηγαίο έγγραφο, τη διαδρομή προορισμού και τις επιλογές που προετοιμάσατε.

```python
from aspose.html import Converter

output_path = "YOUR_DIRECTORY/sample.md"
Converter.convert(html_doc, output_path, markdown_options)
```

Μετά την ολοκλήρωση της κλήσης, θα βρείτε:

* `sample.md` – την έκδοση markdown του αρχικού HTML.  
* Έναν υπο‑φάκελο με όνομα `sample_files` (ή παρόμοιο) που περιέχει κάθε εικόνα που αναφέρεται στο HTML.

---

## Πλήρες λειτουργικό σενάριο

Συνδυάζοντας όλα τα κομμάτια, έχετε ένα ενιαίο σενάριο που μπορείτε να εκτελέσετε από τη γραμμή εντολών:

```python
# convert_html_to_markdown.py
import os
from aspose.html import HTMLDocument, ResourceHandlingOptions, MarkdownSaveOptions, Converter

def convert_html_to_markdown(html_file: str, markdown_file: str):
    """
    Convert an HTML file to markdown while exporting images as separate files.
    """
    # 1. Load the HTML document
    html_doc = HTMLDocument(html_file)

    # 2. Set up resource handling to keep images external
    res_opts = ResourceHandlingOptions()
    res_opts.save_external_resources = True

    # 3. Attach resource handling to markdown options
    md_opts = MarkdownSaveOptions()
    md_opts.resource_handling_options = res_opts

    # 4. Convert and save
    Converter.convert(html_doc, markdown_file, md_opts)
    print(f"Conversion complete: {markdown_file}")

if __name__ == "__main__":
    # Adjust these paths to your environment
    src_html = os.path.abspath("YOUR_DIRECTORY/sample.html")
    dst_md   = os.path.abspath("YOUR_DIRECTORY/sample.md")

    convert_html_to_markdown(src_html, dst_md)
```

**Αναμενόμενη έξοδος**

```
Conversion complete: /absolute/path/YOUR_DIRECTORY/sample.md
```

Μετά την εκτέλεση, ανοίξτε το `sample.md` σε οποιονδήποτε επεξεργαστή markdown. Οι σύνδεσμοι εικόνων θα εμφανιστούν ως:

```markdown
![Alt text](sample_files/image1.png)
```

Οι ίδιες οι εικόνες βρίσκονται στον φάκελο `sample_files`, έτοιμες για version control ή περαιτέρω επεξεργασία.

---

## Διαχείριση κοινών περιπτώσεων άκρων

| Κατάσταση                              | Συνιστώμενη προσέγγιση |
|----------------------------------------|------------------------|
| **Απουσία αρχών εικόνας**                | Ο μετατροπέας καταγράφει μια προειδοποίηση και αφήνει έναν σπασμένο σύνδεσμο. Επαληθεύστε ότι όλα τα χαρακτηριστικά `<img src>` δείχνουν σε προσβάσιμους πόρους πριν από τη μετατροπή. |
| **Σχετικές URL που δείχνουν εκτός του φακέλου του έργου** | Χρησιμοποιήστε το `ResourceHandlingOptions.base_url` για να παρέχετε μια βασική URL ώστε ο μετατροπέας να μπορεί να επιλύσει τις διαδρομές σωστά. |
| **Μεγάλα αρχεία HTML με πολλές εικόνες**  | Ορίστε το `resource_options.max_resource_size` (αν είναι διαθέσιμο) για να περιορίσετε το μέγεθος των πόρων που αντιγράφονται. |
| **Μη‑PNG/JPEG μορφές εικόνας**        | Η βιβλιοθήκη αντιγράφει αυτόματα την αρχική μορφή. Βεβαιωθείτε ότι ο προορισμός markdown viewer υποστηρίζει τη μορφή (π.χ., SVG). |
| **Σφάλματα δικαιωμάτων εγγραφής**           | Εκτελέστε το σενάριο με τα κατάλληλα δικαιώματα ή επιλέξτε έναν φάκελο εξόδου όπου έχετε δικαιώματα εγγραφής. |

---

## Συμβουλές για ομαλή **markdown conversion with images**

* Διατηρήστε τον φάκελο εξόδου καθαρό: διαγράψτε τον φάκελο `*_files` πριν από κάθε εκτέλεση αν θέλετε ένα νέο σύνολο εικόνων.  
* Χρησιμοποιήστε περιγραφικά `alt` attributes στο αρχικό HTML· γίνονται αυτόματα οι λεζάντες εικόνας στο markdown.  
* Αν χρειάζεστε ενσωμάτωση εικόνων ως base64 (για markdown σε ένα αρχείο), ορίστε `resource_options.save_external_resources = False`. Αυτό είναι το αντίστροφο του **export html with images**, αλλά χρήσιμο για ενσωματώσεις σε email ή τεκμηρίωση.  
* Όταν μετατρέπετε μια δέσμη αρχείων, τυλίξτε το σενάριο σε βρόχο και προσαρμόστε το `resource_options.resource_folder` ώστε να αποφεύγετε συγκρούσεις ονομάτων.

---

## Συχνές ερωτήσεις

**Ε: Λειτουργεί αυτό με τμήματα HTML που δεν έχουν πλήρη ετικέτα `<html>`;**  
Α: Ναι. Το `HTMLDocument` μπορεί να αναλύσει τμήματα· ο μετατροπέας τα αντιμετωπίζει ως

---

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να ενσωματώσετε εικόνες στη μετατροπή HTML σε Markdown χρησιμοποιώντας Python](/html/english/python/general/how-to-embed-images-in-html-to-markdown-conversion-using-pyt/)
- [Μετατροπή HTML σε Markdown – Πλήρης Οδηγός με CSS & Εικόνες](/html/english/python/general/convert-html-to-markdown-complete-guide-with-css-images/)
- [Μετατροπή HTML σε Markdown με Aspose – Πλήρης Οδηγός Python](/html/english/python/general/convert-html-to-markdown-with-aspose-complete-python-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}