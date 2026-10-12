---
category: general
date: 2026-10-12
description: Μετατρέψτε το HTML σε markdown γρήγορα και μάθετε πώς να ενσωματώνετε
  εικόνες στο markdown. Αυτός ο οδηγός εξηγεί τη μετατροπή HTML σε markdown με Python,
  παρέχοντας πλήρες κώδικα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- how to embed images in markdown
- html to markdown conversion python
- how to convert html page to markdown
language: el
lastmod: 2026-10-12
og_description: Μετατρέψτε το HTML σε markdown και ενσωματώστε εικόνες στο markdown
  χρησιμοποιώντας Python. Ακολουθήστε αυτό το πλήρες σεμινάριο για αξιόπιστη μετατροπή
  HTML σε markdown με Python.
og_image_alt: Screenshot showing a Python script that converts an HTML file to a markdown
  file with base64‑encoded images
og_title: Μετατροπή HTML σε markdown με ενσωματωμένες εικόνες σε Python – οδηγός βήμα‑βήμα
schemas:
- author: GroupDocs
  dateModified: '2026-10-12'
  description: convert HTML to markdown quickly and learn how to embed images in markdown.
    This guide walks through html to markdown conversion python with full code.
  headline: How to convert HTML to markdown with embedded images using Python
  type: TechArticle
tags:
- markdown
- html
- python
- document conversion
title: Πώς να μετατρέψετε το HTML σε markdown με ενσωματωμένες εικόνες χρησιμοποιώντας
  Python
url: /el/python/general/how-to-convert-html-to-markdown-with-embedded-images-using-p/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να μετατρέψετε HTML σε markdown με ενσωματωμένες εικόνες χρησιμοποιώντας Python

Αν χρειάζεστε **μετατροπή HTML σε markdown** ενώ διατηρείτε κάθε εικόνα, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε. Ρυθμίζοντας τη μηχανή μετατροπής ώστε να ενσωματώνει τις εικόνες ως Base64, λαμβάνετε ένα ενιαίο, αυτόνομο αρχείο `.md` που λειτουργεί παντού—από τα README του GitHub έως τους στατικούς δημιουργούς ιστοσελίδων.

Θα μάθετε επίσης **πώς να ενσωματώνετε εικόνες σε markdown**, γιατί οι ενσωματωμένες επιλογές διαχείρισης πόρων είναι η πιο αξιόπιστη επιλογή, και πώς να εκτελέσετε μια **html to markdown conversion python** με μόνο λίγες γραμμές κώδικα.

## Τι θα πετύχετε

- Μετατρέψτε οποιαδήποτε τοπική σελίδα HTML σε ένα καθαρό έγγραφο Markdown.  
- Ενσωματώστε κάθε εικόνα απευθείας στο αρχείο Markdown ως συμβολοσειρά Base64, εξαλείφοντας τα σπασμένα links.  
- Εκτελέστε τη διαδικασία σε οποιαδήποτε πλατφόρμα που υποστηρίζει Python 3.9+ και τη βιβλιοθήκη GroupDocs Conversion.

## Προαπαιτούμενα

| Απαίτηση | Λόγος |
|------------|--------|
| Python 3.9 or newer | Απαιτείται από το GroupDocs Conversion SDK. |
| `groupdocs-conversion` package | Παρέχει `Converter`, `HTMLDocument`, `MarkdownSaveOptions` και `ResourceHandlingOptions`. |
| Ένα υπάρχον αρχείο HTML (π.χ., `page.html`) | Η πηγή που θέλετε να μετατρέψετε. |
| Δικαίωμα εγγραφής στον φάκελο εξόδου | Για την αποθήκευση του παραγόμενου αρχείου `.md`. |

Install the SDK with pip:

```bash
pip install groupdocs-conversion
```

> **Pro tip:** Χρησιμοποιήστε ένα εικονικό περιβάλλον (`python -m venv .venv`) για να διατηρήσετε τις εξαρτήσεις απομονωμένες.

## Βήμα 1: Διαμορφώστε τη διαχείριση πόρων ώστε να ενσωματώνετε εικόνες σε markdown

Όταν η μηχανή μετατροπής συναντά μια ετικέτα `<img>`, μπορεί είτε να αντιγράψει την εικόνα σε ξεχωριστό φάκελο είτε να την ενσωματώσει απευθείας. Η ενσωμάτωση παράγει ένα data URI κωδικοποιημένο σε Base64, που είναι ακριβώς αυτό που απαιτεί το **how to embed images in markdown**.

```python
from groupdocs.conversion import ResourceHandlingOptions

# Create a resource handling configuration
resource_options = ResourceHandlingOptions()
# Enable embedding of images as Base64 data URIs
resource_options.embed_images = True   # Embeds images directly in the Markdown file
```

**Γιατί είναι σημαντικό:**  
Η ενσωμάτωση εγγυάται ότι το αρχείο Markdown παραμένει φορητό. Εάν μοιραστείτε το αρχείο `.md` χωρίς τον συνοδευτικό φάκελο εικόνων, οι εικόνες θα εμφανίζονται σωστά σε οποιαδήποτε πλατφόρμα που υποστηρίζει data URIs (GitHub, GitLab, προεπισκόπηση VS Code, κ.λπ.).

## Βήμα 2: Ρυθμίστε τις επιλογές αποθήκευσης Markdown χρησιμοποιώντας τη διαμόρφωση πόρων

Η κλάση `MarkdownSaveOptions` σας επιτρέπει να περάσετε τις `resource_options` που δημιουργήθηκαν παραπάνω. Επίσης, σας επιτρέπει να ρυθμίσετε λεπτομερώς τα τέλη γραμμής, τα στυλ επικεφαλίδων και άλλα, αλλά στις περισσότερες περιπτώσεις οι προεπιλογές λειτουργούν καλά.

```python
from groupdocs.conversion import MarkdownSaveOptions

# Attach the resource handling to the markdown save options
markdown_options = MarkdownSaveOptions(resource_handling_options=resource_options)
```

**Τι συμβαίνει στο παρασκήνιο:**  
Κατά τη μετατροπή, η μηχανή σαρώει το DOM του HTML, μετατρέπει κάθε στοιχείο στην αντίστοιχη μορφή Markdown, και αντικαθιστά το `<img src="...">` με `![alt text](data:image/...;base64,...)`. Η σημαία `resource_options.embed_images` ενεργοποιεί αυτή τη συμπεριφορά.

## Βήμα 3: Μετατρέψτε το έγγραφο HTML σε markdown και αποθηκεύστε το αποτέλεσμα

Τώρα συνδέετε όλα μαζί: φορτώνετε το πηγαίο HTML, εφαρμόζετε τις επιλογές αποθήκευσης και γράφετε το αρχείο εξόδου.

```python
from groupdocs.conversion import Converter, HTMLDocument

# Path to the source HTML file
source_path = "YOUR_DIRECTORY/page.html"
# Desired output path for the markdown file
output_path = "YOUR_DIRECTORY/page.md"

# Perform the conversion
Converter.convert_html(
    HTMLDocument(source_path),
    markdown_options,
    output_path
)

print(f"✅ Conversion complete! Markdown saved to: {output_path}")
```

**Αναμενόμενο αποτέλεσμα:**  

- `page.md` περιέχει κείμενο Markdown, επικεφαλίδες, λίστες και **embedded images** ως συμβολοσειρές Base64.  
- Ανοίγοντας το `page.md` σε έναν προβολέα Markdown εμφανίζει την αρχική διάταξη HTML, συμπεριλαμβανομένων όλων των εικόνων, χωρίς εξωτερικά περιουσιακά στοιχεία.

### Πλήρες σενάριο για γρήγορη αντιγραφή‑επικόλληση

```python
# convert_html_to_markdown.py
from groupdocs.conversion import (
    Converter,
    HTMLDocument,
    MarkdownSaveOptions,
    ResourceHandlingOptions,
)

def convert_html_to_markdown(src_html: str, dst_md: str) -> None:
    """Convert an HTML file to markdown with images embedded as Base64."""
    # 1️⃣ Embed images
    resource_opts = ResourceHandlingOptions()
    resource_opts.embed_images = True

    # 2️⃣ Prepare markdown options
    md_opts = MarkdownSaveOptions(resource_handling_options=resource_opts)

    # 3️⃣ Run conversion
    Converter.convert_html(
        HTMLDocument(src_html),
        md_opts,
        dst_md
    )
    print(f"✅ Markdown file created at: {dst_md}")

if __name__ == "__main__":
    # Adjust these paths to your environment
    convert_html_to_markdown(
        src_html="YOUR_DIRECTORY/page.html",
        dst_md="YOUR_DIRECTORY/page.md"
    )
```

Εκτελέστε το σενάριο:

```bash
python convert_html_to_markdown.py
```

## Διαχείριση κοινών περιπτώσεων άκρων

| Κατάσταση | Λύση |
|-----------|------|
| **Μεγάλες εικόνες προκαλούν τεράστια αρχεία markdown** | Περιορίστε το μέγεθος της εικόνας πριν την ενσωμάτωση, μειώνοντάς τη στο HTML ή χρησιμοποιώντας μια βιβλιοθήκη βελτιστοποίησης εικόνων (π.χ., Pillow) πριν τη μετατροπή. |
| **Σχετικές διευθύνσεις URL εικόνων δείχνουν εκτός του έργου** | Βεβαιωθείτε ότι οι αναφορές HTML είναι προσβάσιμες, ή αντιγράψτε αυτές τις εικόνες στον ίδιο φάκελο πριν τη μετατροπή. |
| **Χρειάζεστε ξεχωριστά αρχεία εικόνας αντί για ενσωμάτωση** | Ορίστε `resource_options.embed_images = False` και δώστε μια διαδρομή `resource_folder` όπου θα αποθηκευτούν οι εικόνες. |
| **Η μετατροπή αποτυγχάνει σε κακοσχηματισμένο HTML** | Προεπεξεργαστείτε το HTML με `BeautifulSoup` (`html5lib` parser) για να καθαρίσετε τα σπασμένα tags πριν το δώσετε στον μετατροπέα. |

## Επαλήθευση του αποτελέσματος

Ανοίξτε το παραγόμενο `page.md` σε οποιονδήποτε προβολέα Markdown:

```bash
code YOUR_DIRECTORY/page.md   # VS Code preview
```

Θα πρέπει να δείτε τις αρχικές επικεφαλίδες, παραγράφους και εικόνες να εμφανίζονται σωστά. Εάν μια εικόνα εμφανίζεται ως σπασμένος σύνδεσμος, ελέγξτε ξανά ότι το `embed_images` είναι ορισμένο σε `True` και ότι το πηγαίο HTML περιέχει έγκυρες ετικέτες `<img>`.

## Επόμενα βήματα και σχετικά θέματα

- **Export to other formats** – Η ίδια κλάση `Converter` μπορεί να παράγει PDF, DOCX ή απλό κείμενο. Αντικαταστήστε το `MarkdownSaveOptions` με `PdfSaveOptions` ή `DocxSaveOptions`.  
- **Batch processing** – Επανάληψη πάνω σε έναν φάκελο αρχείων HTML για να παραχθεί μια συλλογή εγγράφων Markdown.  
- **Custom image handling** – Υλοποιήστε μια callback μέσω `ResourceHandlingOptions` για να αποθηκεύσετε τις εικόνες σε CDN και να αντικαταστήσετε το data URI με ένα URL CDN.  
- **Advanced markdown features** – Ενεργοποιήστε το GitHub‑flavored markdown (πίνακες, λίστες εργασιών) προσαρμόζοντας τις ιδιότητες `markdown_options`.

Με την εξειδίκευση στην **html to markdown conversion python**, έχετε τώρα μια επαναλαμβανόμενη, έτοιμη για παραγωγή ροή εργασίας που εγγυάται ότι οι εικόνες παραμένουν μαζί με το περιεχόμενο. Μη διστάσετε να πειραματιστείτε με τις παραπάνω επιλογές και να προσαρμόσετε το σενάριο στις δικές σας διαδικασίες περιεχομένου.

---

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να εξοικειωθείτε με πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Μετατροπή HTML σε Markdown σε .NET με Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Μετατροπή HTML σε Markdown σε Aspose.HTML για Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Δημιουργία PDF από Markdown χρησιμοποιώντας Aspose HTML Converter (Java)](/html/english/java/conversion-html-to-other-formats/create-pdf-from-markdown-using-aspose-html-converter-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}