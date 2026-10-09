---
category: general
date: 2026-10-09
description: Μάθετε πώς να ενσωματώνετε εικόνες κατά τη μετατροπή HTML σε Markdown
  με Python χρησιμοποιώντας το Aspose.HTML. Περιλαμβάνει ενσωμάτωση εικόνων ως Base64
  και markdown με ενσωματωμένες εικόνες.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed images
- convert html to markdown
- html to markdown python
- embed images as base64
- markdown with embedded images
language: el
lastmod: 2026-10-09
og_description: Πώς να ενσωματώσετε εικόνες κατά τη μετατροπή HTML σε Markdown με
  Python. Αυτός ο οδηγός δείχνει πώς να ενσωματώνετε εικόνες ως Base64 και παράγει
  markdown με ενσωματωμένες εικόνες.
og_image_alt: Screenshot of a Markdown file that contains embedded images generated
  by a Python HTML‑to‑Markdown conversion
og_title: Πώς να ενσωματώσετε εικόνες κατά τη μετατροπή HTML σε Markdown με Python
schemas:
- author: Aspose
  dateModified: '2026-10-09'
  description: Learn how to embed images while converting HTML to Markdown in Python
    using Aspose.HTML. Includes embed images as Base64 and markdown with embedded
    images.
  headline: How to embed images when converting HTML to Markdown in Python
  type: TechArticle
- description: Learn how to embed images while converting HTML to Markdown in Python
    using Aspose.HTML. Includes embed images as Base64 and markdown with embedded
    images.
  name: How to embed images when converting HTML to Markdown in Python
  steps:
  - name: '**Resize images before conversion** – Use Pillow (`pip install pillow`)
      to shrink images to a reasonable resolution (e.g., 800 px width) before embedding.'
    text: '**Resize images before conversion** – Use Pillow (`pip install pillow`)
      to shrink images to a reasonable resolution (e.g., 800 px width) before embedding.'
  - name: '**Limit embedding to specific formats** – If you only need PNGs embedded,
      adjust `resource_opts` to filter by MIME type:'
    text: '**Limit embedding to specific formats** – If you only need PNGs embedded,
      adjust `resource_opts` to filter by MIME type:'
  - name: Import Aspose.HTML classes and create `MarkdownSaveOptions`.
    text: Import Aspose.HTML classes and create `MarkdownSaveOptions`.
  - name: Set `ResourceHandlingOptions.embed_resources` and `embed_images_as_base64`
      to `True`.
    text: Set `ResourceHandlingOptions.embed_resources` and `embed_images_as_base64`
      to `True`.
  - name: Attach those options to the markdown save settings.
    text: Attach those options to the markdown save settings.
  - name: Call `Converter.convert` with the source HTML and destination Markdown paths.
    text: Call `Converter.convert` with the source HTML and destination Markdown paths.
  type: HowTo
tags:
- Python
- Aspose.HTML
- Markdown conversion
- Image embedding
title: Πώς να ενσωματώσετε εικόνες κατά τη μετατροπή HTML σε Markdown με Python
url: /el/python/general/how-to-embed-images-when-converting-html-to-markdown-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ενσωματώσετε εικόνες κατά τη μετατροπή HTML σε Markdown με Python

Αν χρειάζεστε **πώς να ενσωματώσετε εικόνες** κατά τη μετατροπή HTML‑σε‑Markdown, αυτός ο οδηγός σας παρέχει μια πλήρη, έτοιμη προς εκτέλεση λύση. Χρησιμοποιώντας το Aspose.HTML για Python μπορείτε να ενσωματώσετε εικόνες ως συμβολοσειρές Base‑64, ώστε το παραγόμενο αρχείο Markdown να περιέχει τις εικόνες ενσωματωμένες. Αυτό εξαλείφει τα σπασμένα links και κάνει το έγγραφο φορητό.

Εκτός από την ενσωμάτωση εικόνων, το tutorial δείχνει πώς να **μετατρέψετε HTML σε Markdown** με έναν Pythonic τρόπο, καλύπτοντας τη ροή εργασίας *html to markdown python*, τη ρύθμιση **embed images as Base64**, και την παραγωγή **markdown with embedded images** που λειτουργεί σε οποιονδήποτε προβολέα Markdown.

Στο τέλος αυτού του άρθρου θα έχετε ένα ενιαίο script που:

* Διαβάζει ένα αρχείο HTML από το δίσκο.  
* Ενσωματώνει κάθε αναφερόμενη εικόνα απευθείας στην έξοδο Markdown ως URI δεδομένων Base‑64.  
* Αποθηκεύει το τελικό αρχείο Markdown έτοιμο για διανομή ή έλεγχο εκδόσεων.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Python 3.8 ή νεότερη έκδοση εγκατεστημένη.  
* Ένα έγκυρο license του Aspose.HTML για Python (η δωρεάν δοκιμή λειτουργεί για αξιολόγηση).  
* `pip install aspose-html` εκτελεσμένο στο εικονικό σας περιβάλλον.  
* Ένα αρχείο HTML (`input.html`) που αναφέρει τοπικές ή απομακρυσμένες εικόνες.

Αν λείπει κάποιο από τα παραπάνω, εγκαταστήστε το τώρα για να αποφύγετε σφάλματα χρόνου εκτέλεσης.

## Βήμα 1: Ρύθμιση του περιβάλλοντος Aspose.HTML

Πρώτα, εισάγετε τις κλάσεις που χρειάζεστε και δημιουργήστε ένα αντικείμενο `MarkdownSaveOptions`. Το αντικείμενο `MarkdownSaveOptions` περιέχει τις ρυθμίσεις μετατροπής, συμπεριλαμβανομένων των επιλογών διαχείρισης πόρων που θα διαμορφώσουμε αργότερα.

```python
# Step 1: Import required Aspose.HTML classes
from aspose.html import Converter, ResourceHandlingOptions, MarkdownSaveOptions

# Initialize Markdown save options (you can customize other settings here)
markdown_opts = MarkdownSaveOptions()
```

**Γιατί είναι σημαντικό αυτό το βήμα:**  
Ο `Converter` εκτελεί το βαρέως τύπου έργο, ενώ το `MarkdownSaveOptions` λέει στον μετατροπέα ακριβώς πώς να αντιμετωπίσει πόρους όπως εικόνες, scripts και stylesheets. Χωρίς την αρχικοποίηση του `markdown_opts`, δεν μπορείτε να συνδέσετε τη διαμόρφωση διαχείρισης πόρων που ενεργοποιεί την ενσωμάτωση εικόνων.

## Βήμα 2: Διαμόρφωση διαχείρισης πόρων για ενσωμάτωση εικόνων ως Base64

Το Aspose.HTML παρέχει `ResourceHandlingOptions`. Ορίζοντας `embed_resources = True` λέτε στον μετατροπέα να αντικαταστήσει τις εξωτερικές αναφορές εικόνων με URI δεδομένων Base‑64.

```python
# Step 2: Create and configure resource handling options
resource_opts = ResourceHandlingOptions()
resource_opts.embed_resources = True          # Embed images directly in the output
resource_opts.embed_images_as_base64 = True   # Explicitly request Base64 encoding for images

# Attach the resource options to the markdown save options
markdown_opts.resource_handling_options = resource_opts
```

**Γιατί είναι σημαντικό αυτό το βήμα:**  
Όταν το `embed_resources` είναι `True`, ο μετατροπέας σαρώει το HTML για ετικέτες `<img>`, κατεβάζει κάθε εικόνα, την κωδικοποιεί και ενσωματώνει ένα URI της μορφής `data:image/...;base64,` στο Markdown. Αυτό παράγει **markdown with embedded images**, ιδανικό για τεκμηρίωση που πρέπει να μεταφέρεται μαζί με το αρχείο πηγής (π.χ. σε αποθετήριο Git).

## Βήμα 3: Εκτέλεση της μετατροπής από HTML σε Markdown

Τώρα μπορείτε να καλέσετε το `Converter.convert`, περνώντας τη διαδρομή του πηγαίου HTML, τη διαδρομή του προορισμού Markdown και το διαμορφωμένο `markdown_opts`.

```python
# Step 3: Define source and destination paths
html_path = "YOUR_DIRECTORY/input.html"
markdown_path = "YOUR_DIRECTORY/with_images.md"

# Step 4: Convert HTML to Markdown, embedding images
Converter.convert(html_path, markdown_path, markdown_opts)
```

**Γιατί είναι σημαντικό αυτό το βήμα:**  
Το `Converter.convert` διαβάζει το HTML, επεξεργάζεται όλους τους πόρους σύμφωνα με τις επιλογές που ορίσατε, και γράφει ένα αρχείο Markdown που περιέχει το ίδιο οπτικό περιεχόμενο — εικόνες συμπεριλαμβανομένες — χωρίς εξωτερικές εξαρτήσεις.

## Βήμα 4: Επαλήθευση του παραγόμενου Markdown

Ανοίξτε το `with_images.md` σε οποιονδήποτε προβολέα Markdown (VS Code, GitHub, Typora κ.λπ.). Θα πρέπει να δείτε τις εικόνες να εμφανίζονται ακριβώς όπως εμφανίζονταν στο αρχικό HTML. Οι σύνδεσμοι εικόνων θα έχουν την εξής μορφή:

```markdown
![Alt text](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA...)
```

Αν ο προβολέας εμφανίζει σπασμένες εικόνες, ελέγξτε ξανά ότι:

* Το αρχικό HTML αναφερόταν σε εικόνες που είναι προσβάσιμες (τα τοπικά αρχεία υπάρχουν, τα απομακρυσμένα URLs είναι προσβάσιμα).  
* Η σημαία `embed_images_as_base64` είναι ορισμένη σε `True`.  

## Βήμα 5: Διαχείριση μεγάλων εικόνων και ζητήματα απόδοσης

Η ενσωμάτωση πολύ μεγάλων εικόνων μπορεί να αυξήσει δραματικά το μέγεθος του αρχείου Markdown. Εδώ είναι δύο πρακτικές συμβουλές:

1. **Αλλάξτε το μέγεθος των εικόνων πριν τη μετατροπή** – Χρησιμοποιήστε το Pillow (`pip install pillow`) για να μειώσετε τις εικόνες σε λογική ανάλυση (π.χ. πλάτος 800 px) πριν τις ενσωματώσετε.  
2. **Περιορίστε την ενσωμάτωση σε συγκεκριμένες μορφές** – Αν χρειάζεστε ενσωματωμένα μόνο PNG, προσαρμόστε το `resource_opts` ώστε να φιλτράρει κατά MIME type:

```python
resource_opts.allowed_image_formats = ["png"]  # Only embed PNG images
```

Αυτές οι προσαρμογές διατηρούν το Markdown ελαφρύ, ενώ παρέχουν την φορητότητα που χρειάζεστε.

## Συνηθισμένα προβλήματα και πώς να τα επιλύσετε

| Πρόβλημα | Αιτία | Διόρθωση |
|----------|-------|----------|
| Οι εικόνες εμφανίζονται ως σπασμένοι σύνδεσμοι | `embed_resources` παραμένει `False` | Βεβαιωθείτε ότι `resource_opts.embed_resources = True`. |
| Το αρχείο Markdown είναι > 10 MB | Πολύ μεγάλες εικόνες υψηλής ανάλυσης | Μειώστε το μέγεθος των εικόνων ή ενσωματώστε μόνο τις απαραίτητες. |
| Απομακρυσμένες εικόνες δεν ενσωματώνονται | Χρονικό όριο δικτύου ή μπλοκαρισμένο URL | Ελέγξτε τη σύνδεση στο internet ή κατεβάστε τις εικόνες τοπικά πριν τη μετατροπή. |
| Απρόσμενοι χαρακτήρες στη συμβολοσειρά Base64 | Το δυαδικό αρχείο δεν διαβάστηκε σωστά | Βεβαιωθείτε ότι τα αρχεία εικόνας δεν είναι κατεστραμμένα και έχουν σωστά δικαιώματα πρόσβασης. |

## Επέκταση της λύσης: Μετατροπή πολλαπλών αρχείων HTML σε παρτίδα

Αν χρειάζεστε επεξεργασία φακέλου με HTML αρχεία, τυλίξτε τη λογική μετατροπής σε βρόχο:

```python
import os

input_dir = "YOUR_DIRECTORY/html_files"
output_dir = "YOUR_DIRECTORY/markdown_output"

for filename in os.listdir(input_dir):
    if filename.lower().endswith(".html"):
        src_path = os.path.join(input_dir, filename)
        dst_path = os.path.join(output_dir, os.path.splitext(filename)[0] + ".md")
        Converter.convert(src_path, dst_path, markdown_opts)
        print(f"Converted {filename} → {os.path.basename(dst_path)}")
```

Αυτό το απόσπασμα δείχνει **convert html to markdown** σε κλίμακα, διατηρώντας τη συμπεριφορά **embed images as base64** για κάθε αρχείο.

## Ανακεφαλαίωση

Τώρα γνωρίζετε **πώς να ενσωματώσετε εικόνες** όταν **μετατρέπετε HTML σε Markdown** χρησιμοποιώντας Python. Τα βασικά βήματα είναι:

1. Εισάγετε τις κλάσεις Aspose.HTML και δημιουργήστε `MarkdownSaveOptions`.  
2. Ορίστε `ResourceHandlingOptions.embed_resources` και `embed_images_as_base64` σε `True`.  
3. Συνδέστε αυτές τις επιλογές στις ρυθμίσεις αποθήκευσης markdown.  
4. Καλέστε `Converter.convert` με τις διαδρομές του πηγαίου HTML και του προορισμού Markdown.  

Το αποτέλεσμα είναι **markdown with embedded images** που μπορεί να μοιραστεί χωρίς ανησυχία για ελλιπή assets.

## Επόμενα βήματα

* Εξερευνήστε άλλες επιλογές του `ResourceHandlingOptions` όπως `embed_stylesheets` αν χρειάζεστε ενσωματωμένο CSS.  
* Συνδυάστε αυτή τη ροή εργασίας με έναν static site generator (π.χ. MkDocs) για να δημιουργήσετε pipelines τεκμηρίωσης.  
* Πειραματιστείτε με διαφορετικές μορφές εικόνων και επίπεδα συμπίεσης για να βρείτε την ισορροπία μεταξύ ποιότητας και μεγέθους αρχείου.

Αισθανθείτε ελεύθεροι να προσαρμόσετε το script στις δικές σας απαιτήσεις έργου, και καλή προγραμματιστική δουλειά!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Set Offset When Converting HTML to Markdown in Java](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)
- [Convert markdown to html – Java guide with PDF output](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html-java-guide-with-pdf-output/)
- [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}