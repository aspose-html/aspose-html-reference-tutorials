---
category: general
date: 2026-08-03
description: Πώς να ενσωματώσετε εικόνες κατά τη μετατροπή HTML σε Markdown με Python.
  Μάθετε πώς να αποθηκεύετε HTML ως Markdown και να ενσωματώνετε εικόνες ως Base64
  σε ένα ενιαίο script.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed images
- convert html to markdown
- how to convert html
- save html as markdown
- embed images as base64
language: el
lastmod: 2026-08-03
og_description: Πώς να ενσωματώσετε εικόνες κατά τη μετατροπή HTML σε Markdown με
  Python. Αυτός ο οδηγός σας δείχνει πώς να αποθηκεύσετε το HTML ως Markdown και να
  ενσωματώσετε εικόνες ως Base64 αποδοτικά.
og_image_alt: Screenshot showing how to embed images in HTML to Markdown conversion
  using Python
og_title: Πώς να ενσωματώσετε εικόνες στη μετατροπή HTML‑σε‑Markdown (Python)
schemas:
- author: Aspose
  dateModified: '2026-08-03'
  description: How to embed images while converting HTML to Markdown with Python.
    Learn to save HTML as Markdown and embed images as Base64 in a single script.
  headline: How to embed images in HTML to Markdown conversion using Python
  type: TechArticle
- description: How to embed images while converting HTML to Markdown with Python.
    Learn to save HTML as Markdown and embed images as Base64 in a single script.
  name: How to embed images in HTML to Markdown conversion using Python
  steps:
  - name: Load the source HTML document
    text: '```python from aspose.html import HTMLDocument'
  - name: Configure resource handling to embed images as Base64
    text: '```python from aspose.html import ResourceHandlingOptions'
  - name: Attach the resource options to the Markdown save options
    text: '```python from aspose.html import MarkdownSaveOptions'
  - name: Convert the HTML to Markdown and save the file
    text: '```python from aspose.html import Converter'
  - name: Expected output
    text: 'Open `embedded_images.md` in any Markdown viewer. You should see something
      like:'
  - name: Tips for reliable conversion
    text: '* **Validate the source HTML** – malformed tags can lead to unexpected
      Markdown. Use `HTMLDocument.validate()` if you suspect issues. * **Set `markdown_opts.escape_uri
      = False`** if you want to keep original URLs for images that are not embedded.
      * **Control line breaks** with `markdown_opts.force_n'
  type: HowTo
tags:
- Python
- Aspose.HTML
- Markdown
- Base64
- HTML conversion
title: Πώς να ενσωματώσετε εικόνες στη μετατροπή από HTML σε Markdown χρησιμοποιώντας
  Python
url: /el/python/general/how-to-embed-images-in-html-to-markdown-conversion-using-pyt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ενσωματώσετε εικόνες στη μετατροπή HTML σε Markdown χρησιμοποιώντας Python

Αν χρειάζεστε **πώς να ενσωματώσετε εικόνες** κατά τη μετατροπή ενός αρχείου HTML σε Markdown, αυτό το tutorial σας παρέχει μια πλήρη, έτοιμη‑για‑εκτέλεση λύση. Χρησιμοποιώντας το Aspose.HTML για Python μπορείτε να μετατρέψετε HTML σε Markdown, να ενσωματώσετε κάθε εικόνα ως συμβολοσειρά Base64 και να αποθηκεύσετε το αποτέλεσμα με μία μόνο κλήση.

Η ενσωμάτωση εικόνων ως Base64 εξαλείφει τις εξωτερικές εξαρτήσεις αρχείων, κάτι που είναι ιδιαίτερα χρήσιμο όταν θέλετε να διανείμετε ένα αυτόνομο έγγραφο Markdown ή να το αποθηκεύσετε σε μια βάση δεδομένων. Τα παρακάτω βήματα καλύπτουν επίσης **convert html to markdown**, **save html as markdown**, και **embed images as base64**—όλα χωρίς να αφήσετε το περιβάλλον Python.

> **Προαπαιτούμενα**  
> • Python 3.8+ εγκατεστημένο  
> • Πακέτο `aspose.html` (`pip install aspose-html`)  
> • Τοπικό αρχείο HTML (`sample.html`) που περιέχει τουλάχιστον μία ετικέτα `<img>`  

Στο τέλος αυτού του οδηγού θα μπορείτε να εκτελέσετε ένα script που παράγει το `embedded_images.md`, ένα αρχείο Markdown με κάθε εικόνα ήδη ενσωματωμένη ως Base64 data URI.

![How to embed images in HTML to Markdown conversion using Python](https://example.com/placeholder-image.png){.align-center width=600 alt="Στιγμιότυπο που δείχνει πώς να ενσωματώσετε εικόνες στη μετατροπή HTML σε Markdown χρησιμοποιώντας Python"}

## Πώς να ενσωματώσετε εικόνες στη μετατροπή HTML σε Markdown

Ο πυρήνας της διαδικασίας είναι η διαμόρφωση του **ResourceHandlingOptions** ώστε το Aspose.HTML να γνωρίζει ότι πρέπει να ενσωματώνει τις εικόνες αντί να τις αντιγράφει ως ξεχωριστά αρχεία. Τα παρακάτω τμήματα χωρίζουν τη ροή εργασίας σε σαφή, λογικά βήματα.

### Βήμα 1: Φόρτωση του πηγαίου εγγράφου HTML

```python
from aspose.html import HTMLDocument

# Replace YOUR_DIRECTORY with the folder that holds your HTML file
html_path = "YOUR_DIRECTORY/sample.html"
html_doc = HTMLDocument(html_path)
```

*Γιατί είναι σημαντικό αυτό το βήμα:* Το `HTMLDocument` αναλύει το HTML markup και δημιουργεί ένα DOM με το οποίο μπορεί να εργαστεί το Aspose.HTML. Χωρίς τη φόρτωση του εγγράφου, ο μετατροπέας δεν έχει τίποτα προς επεξεργασία.

### Βήμα 2: Διαμόρφωση διαχείρισης πόρων για ενσωμάτωση εικόνων ως Base64

```python
from aspose.html import ResourceHandlingOptions

resource_opts = ResourceHandlingOptions()
# Setting embed_images to True tells the converter to replace <img src="...">
# with a data URI that contains the image encoded in Base64.
resource_opts.embed_images = True
```

*Γιατί είναι σημαντικό:* Από προεπιλογή, ο μετατροπέας αντιγράφει τα αρχεία εικόνας δίπλα στο αρχείο Markdown. Η ενεργοποίηση του `embed_images` εγγυάται ότι κάθε εικόνα γίνεται ένα αυτόνομο data URI, ικανοποιώντας την απαίτηση **embed images as base64**.

### Βήμα 3: Συμπλήρωση των επιλογών πόρων στις επιλογές αποθήκευσης Markdown

```python
from aspose.html import MarkdownSaveOptions

markdown_opts = MarkdownSaveOptions()
markdown_opts.resource_handling_options = resource_opts
```

*Γιατί είναι σημαντικό:* Το `MarkdownSaveOptions` συγκεντρώνει όλες τις ρυθμίσεις μετατροπής. Η σύνδεση του `resource_handling_options` εξασφαλίζει ότι ο κανόνας ενσωμάτωσης εικόνας εφαρμόζεται κατά το βήμα **convert html**.

### Βήμα 4: Μετατροπή του HTML σε Markdown και αποθήκευση του αρχείου

```python
from aspose.html import Converter

output_path = "YOUR_DIRECTORY/embedded_images.md"
Converter.convert_html(html_doc, markdown_opts, output_path)
print(f"Markdown file created at: {output_path}")
```

*Γιατί είναι σημαντικό:* Το `Converter.convert_html` εκτελεί το βαρέως τύπου έργο—αναλύει το DOM, μετατρέπει τις ετικέτες HTML σε σύνταξη Markdown και γράφει το τελικό αρχείο. Επειδή έχουμε προσθέσει τις επιλογές πόρων, κάθε ετικέτα `<img>` μετατρέπεται σε καταχώρηση `![alt text](data:image/...;base64,...)`.

### Αναμενόμενο αποτέλεσμα

Ανοίξτε το `embedded_images.md` σε οποιονδήποτε προβολέα Markdown. Θα πρέπει να δείτε κάτι όπως:

```markdown
# Sample Document

Here is an image embedded directly in the file:

![Sample Image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA...)
```

Η μακριά συμβολοσειρά μετά το `base64,` είναι τα κωδικοποιημένα δεδομένα της εικόνας. Δεν απαιτούνται εξωτερικά αρχεία εικόνας.

## Μετατροπή HTML σε Markdown με Aspose.HTML

Το Aspose.HTML υποστηρίζει ένα ευρύ φάσμα λειτουργιών HTML, συμπεριλαμβανομένων πινάκων, λιστών και μπλοκ κώδικα. Όταν **convert html to markdown**, η βιβλιοθήκη αντιστοιχίζει κάθε στοιχείο HTML στο αντίστοιχο του σε Markdown:

| HTML element | Markdown output |
|--------------|-----------------|
| `<h1>`       | `# Heading`     |
| `<ul>` / `<li>` | `- List item` |
| `<pre><code>` | ```` ```code``` ```` |
| `<img>`      | `![alt](url)`   (ή data URI όταν `embed_images=True`) |

Επειδή η μετατροπή εκτελείται στην πλευρά του διακομιστή, δεν χρειάζεστε πρόσθετο JavaScript ή υπηρεσίες τρίτων. Η διαδικασία είναι ντετερμινιστική και λειτουργεί το ίδιο σε Windows, macOS και Linux.

### Συμβουλές για αξιόπιστη μετατροπή

* **Επικυρώστε το πηγαίο HTML** – εσφαλμένες ετικέτες μπορούν να οδηγήσουν σε απρόσμενο Markdown. Χρησιμοποιήστε `HTMLDocument.validate()` αν υποπτεύεστε προβλήματα.  
* **Ορίστε `markdown_opts.escape_uri = False`** αν θέλετε να διατηρήσετε τις αρχικές URL για εικόνες που δεν ενσωματώνονται.  
* **Έλεγχος αλλαγών γραμμής** με `markdown_opts.force_new_line = True` όταν χρειάζεστε αυστηρή διαχείριση line‑breaks.

## Αποθήκευση HTML ως Markdown με προσαρμοσμένες επιλογές

Αν χρειάζεστε μόνο **save html as markdown** χωρίς ενσωμάτωση εικόνων, ορίστε απλώς `resource_opts.embed_images = False`. Το υπόλοιπο του κώδικα παραμένει αμετάβλητο:

```python
resource_opts.embed_images = False  # Images will be saved as regular URLs
```

Αυτή η ευελιξία σας επιτρέπει να επαναχρησιμοποιήσετε το ίδιο script για διαφορετικά σενάρια ανάπτυξης—αυτόνομο Markdown για τεκμηρίωση ή ελαφρύ Markdown με εξωτερικά assets για δημοσίευση στο web.

## Ενσωμάτωση εικόνων ως Base64 χρησιμοποιώντας ResourceHandlingOptions

Η ενσωμάτωση εικόνων ως Base64 αυξάνει το μέγεθος του αρχείου (περίπου 33 % μεγαλύτερο από το αρχικό δυαδικό), αλλά εγγυάται φορητότητα. Σκεφτείτε τις ακόλουθες περιπτώσεις:

| Situation | Recommendation |
|-----------|----------------|
| Large PNGs (>1 MB) | Συμπιέστε ή αλλάξτε το μέγεθος πριν την ενσωμάτωση ώστε το αρχείο Markdown να παραμένει διαχειρίσιμο. |
| SVG images | Είναι ήδη XML· μπορείτε να ενσωματώσετε το ακατέργαστο SVG markup ή να το κωδικοποιήσετε σε Base64—και τα δύο λειτουργούν. |
| Remote images (`http://…`) | Το Aspose.HTML θα κατεβάσει την εικόνα, θα την ενσωματώσει και θα την αποθηκεύσει στην κρυφή μνήμη κατά τη μετατροπή. Βεβαιωθείτε ότι υπάρχει πρόσβαση στο δίκτυο. |

**Pro tip:** Αν χρειάζεστε να ενσωματώσετε μόνο ένα υποσύνολο των εικόνων, φιλτράρετε τις με βάση την επέκταση αρχείου ή το μέγεθος πριν ορίσετε `embed_images = True`. Μπορείτε να το κάνετε προσαρμόζοντας το `resource_opts.image_filter` (διαθέσιμο σε νεότερες εκδόσεις του Aspose.HTML).

## Πλήρες script που μπορείτε να αντιγράψετε‑και‑επικολλήσετε

```python
# embed_html_to_markdown.py
# -------------------------------------------------
# Complete example: convert HTML to Markdown and embed images as Base64.
# -------------------------------------------------
from aspose.html import HTMLDocument, ResourceHandlingOptions, MarkdownSaveOptions, Converter

# 1️⃣ Load HTML
html_path = "YOUR_DIRECTORY/sample.html"
html_doc = HTMLDocument(html_path)

# 2️⃣ Configure resource handling (embed images)
resource_opts = ResourceHandlingOptions()
resource_opts.embed_images = True  # Change to False to keep external image files

# 3️⃣ Attach options to MarkdownSaveOptions
markdown_opts = MarkdownSaveOptions()
markdown_opts.resource_handling_options = resource_opts

# 4️⃣ Convert and save
output_path = "YOUR_DIRECTORY/embedded_images.md"
Converter.convert_html(html_doc, markdown_opts, output_path)

print(f"✅ Markdown with embedded images saved to: {output_path}")
```

Εκτελέστε το script:

```bash
python embed_html_to_markdown.py
```

Θα δείτε το μήνυμα επιβεβαίωσης και το παραγόμενο `embedded_images.md` θα περιέχει όλες τις εικόνες ως Base64 data URIs.

## Συμπέρασμα

Τώρα ξέρετε **πώς να ενσωματώσετε εικόνες** όταν **convert html to markdown** χρησιμοποιώντας το Aspose.HTML για Python. Το tutorial κάλυψε τη φόρτωση ενός εγγράφου HTML, τη διαμόρφωση του `ResourceHandlingOptions` για **embed images as base64**, τη σύνδεση αυτών των επιλογών στο `MarkdownSaveOptions` και, τέλος, την κλήση του `Converter.convert_html` για **save html as markdown**.

Από εδώ μπορείτε:

* Να απενεργοποιήσετε την ενσωμάτωση εικόνων για να διατηρήσετε εξωτερικά assets (`embed_images = False`).  
* Να πειραματιστείτε με πρόσθετες `MarkdownSaveOptions` όπως `force_new_line` ή `escape_uri`.  
* Να συνδυάσετε αυτό το script με μια παρτίδα διαδικασιών για αυτόματη μετατροπή πολλαπλών αρχείων HTML.

Νιώστε ελεύθεροι να προσαρμόσετε τον κώδικα για άλλες γλώσσες που υποστηρίζονται από το Aspose.HTML (C#, Java κ.λπ.) ή να τον ενσωματώσετε σε μια CI pipeline που δημιουργεί τεκμηρίωση από πηγές HTML. Καλή μετατροπή!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Save HTML as GIF with Aspose.HTML for Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-gif/)
- [How to Convert HTML to JPEG Using Aspose.HTML for Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-jpeg/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}