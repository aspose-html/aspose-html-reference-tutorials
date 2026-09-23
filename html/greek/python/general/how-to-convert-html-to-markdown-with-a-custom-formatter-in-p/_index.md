---
category: general
date: 2026-09-23
description: Μάθετε πώς να μετατρέπετε HTML σε Markdown και να εξάγετε HTML ως Markdown
  χρησιμοποιώντας τον μορφοποιητή με γεύση GitLab. Οδηγός βήμα‑βήμα με πλήρη κώδικα
  Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- export html as markdown
- set markdown formatter
- how to convert html
- convert html document
language: el
lastmod: 2026-09-23
og_description: Μετατρέψτε το HTML σε Markdown και εξάγετε το HTML ως Markdown χρησιμοποιώντας
  τον μορφοποιητή με γεύση GitLab. Ακολουθήστε αυτό το πλήρες σεμινάριο για ένα έτοιμο
  προς εκτέλεση script Python.
og_image_alt: Terminal window showing a Python script that converts an HTML file to
  a Markdown file
og_title: Μετατροπή HTML σε Markdown με Python – πλήρης οδηγός με προσαρμοσμένο μορφοποιητή
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Learn how to convert HTML to Markdown and export HTML as Markdown using
    the GitLab‑flavored formatter. Step‑by‑step guide with full Python code.
  headline: How to convert HTML to Markdown with a custom formatter in Python
  type: TechArticle
tags:
- HTML
- Markdown
- Python
- Conversion
title: Πώς να μετατρέψετε το HTML σε Markdown με προσαρμοσμένο μορφοποιητή στην Python
url: /el/python/general/how-to-convert-html-to-markdown-with-a-custom-formatter-in-p/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να μετατρέψετε HTML σε Markdown με προσαρμοσμένο μορφοποιητή σε Python

Αν χρειάζεστε **μετατροπή HTML σε Markdown**, αυτό το tutorial σας δείχνει τα ακριβή βήματα για να το κάνετε προγραμματιστικά. Θα δείτε πώς να **εξάγετε HTML ως Markdown**, να ρυθμίσετε τον επιθυμητό μορφοποιητή και να εκτελέσετε τη μετατροπή με μία μόνο κλήση Python.

Θα χρησιμοποιήσουμε το API στυλ `aspose-words-cloud` που παρέχει `HTMLDocument`, `MarkdownSaveOptions` και `Converter`. Στο τέλος του οδηγού θα έχετε ένα επαναχρησιμοποιήσιμο script που μπορεί να επεξεργαστεί οποιοδήποτε αρχείο HTML και να παράγει ένα αρχείο Markdown που ταιριάζει με την προεπιλογή τύπου GitLab.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Python 3.9 ή νεότερο εγκατεστημένο  
* Το πακέτο `aspose-words-cloud` (ή ισοδύναμο) που παρέχει `HTMLDocument`, `MarkdownSaveOptions` και `Converter`. Εγκαταστήστε το με:

```bash
pip install aspose-words-cloud
```

* Έναν φάκελο που περιέχει το πηγαίο αρχείο HTML που θέλετε να μετατρέψετε (π.χ., `sample.html`).

## Βήμα 1: Φόρτωση του πηγαίου εγγράφου HTML

Η πρώτη ενέργεια είναι η ανάγνωση του αρχείου HTML σε ένα αντικείμενο `HTMLDocument`. Αυτό το αντικείμενο αφαιρεί την πολυπλοκότητα του DOM και προετοιμάζει το περιεχόμενο για μετατροπή.

```python
# Step 1: Load the source HTML document
html_doc = HTMLDocument("YOUR_DIRECTORY/sample.html")
```

*Γιατί αυτό το βήμα είναι σημαντικό* – Η φόρτωση του αρχείου δημιουργεί μια αναπαράσταση στη μνήμη που ο μετατροπέας μπορεί να διασχίσει αποδοτικά. Η παράλειψη αυτού του βήματος θα ανάγκαζε τον μετατροπέα να διαβάζει το αρχείο επανειλημμένα, κάτι που μειώνει την απόδοση.

## Βήμα 2: Ορισμός του μορφοποιητή markdown

Διαφορετικές πλατφόρμες ερμηνεύουν το Markdown ελαφρώς διαφορετικά. Η βιβλιοθήκη σας επιτρέπει να επιλέξετε έναν προεπιλεγμένο μορφοποιητή· η προεπιλογή τύπου GitLab επιλέγεται ορίζοντας το `MarkdownSaveOptions.formatter` σε `GIT`. Αυτό ικανοποιεί την απαίτηση **set markdown formatter**.

```python
# Step 2: Configure Markdown save options to use the GitLab‑flavored preset
md_options = MarkdownSaveOptions()
md_options.formatter = MarkdownSaveOptions.Formatter.GIT   # GIT = GitLab flavor (default for standard)
```

*Γιατί μπορεί να θέλετε προσαρμοσμένο μορφοποιητή* – Ορισμένες υπηρεσίες (GitHub, GitLab, Bitbucket) αναμένουν λεπτές παραλλαγές σύνταξης. Ορίζοντας ρητά τον μορφοποιητή, εξασφαλίζετε ότι οι επικεφαλίδες, οι πίνακες και οι κώδικες θα αποδοθούν σωστά στην πλατφόρμα-στόχο.

## Βήμα 3: Μετατροπή του HTML σε Markdown και αποθήκευση του αρχείου

Τώρα καλέστε τη στατική μέθοδο `Converter.convert_html`. Δέχεται το φορτωμένο έγγραφο, τις ρυθμισμένες επιλογές και τη διαδρομή προορισμού.

```python
# Step 3: Convert the HTML to Markdown and save the output file
Converter.convert_html(html_doc, md_options, "YOUR_DIRECTORY/sample.md")
```

Όταν ολοκληρωθεί η κλήση, το `sample.md` περιέχει την αναπαράσταση Markdown του αρχικού HTML. Μπορείτε να ανοίξετε το αρχείο σε οποιονδήποτε επεξεργαστή για να επαληθεύσετε το αποτέλεσμα.

### Αναμενόμενη έξοδος

Υποθέτοντας ότι το `sample.html` περιέχει μια απλή παράγραφο και μια επικεφαλίδα, το παραγόμενο `sample.md` θα μοιάζει με:

```markdown
# Sample Heading

This is a paragraph extracted from the original HTML file.
```

Αν το πηγαίο HTML περιλαμβάνει πίνακες, λίστες ή μπλοκ κώδικα, ο μορφοποιητής θα τα μετατρέψει σε ισοδύναμα Markdown συμβατά με το GitLab.

## Πώς να μετατρέψετε έγγραφα HTML μαζικά

Συχνά χρειάζεται να **μετατρέψετε αρχεία html** σε παρτίδα. Συσκευάστε τα τρία βήματα σε μια συνάρτηση και επαναλάβετε πάνω σε έναν φάκελο:

```python
import os

def convert_html_to_md(src_path: str, dst_path: str, formatter=MarkdownSaveOptions.Formatter.GIT):
    """Convert a single HTML file to Markdown using the chosen formatter."""
    html_doc = HTMLDocument(src_path)

    md_options = MarkdownSaveOptions()
    md_options.formatter = formatter

    Converter.convert_html(html_doc, md_options, dst_path)

# Batch conversion example
source_dir = "YOUR_DIRECTORY/html_files"
target_dir = "YOUR_DIRECTORY/md_output"
os.makedirs(target_dir, exist_ok=True)

for filename in os.listdir(source_dir):
    if filename.lower().endswith(".html"):
        src_file = os.path.join(source_dir, filename)
        dst_file = os.path.join(target_dir, os.path.splitext(filename)[0] + ".md")
        convert_html_to_md(src_file, dst_file)
        print(f"Converted {filename} → {os.path.basename(dst_file)}")
```

*Συμβουλή*: Χρησιμοποιήστε `formatter=MarkdownSaveOptions.Formatter.GIT` για GitLab, `MarkdownSaveOptions.Formatter.GFM` για GitHub ή `MarkdownSaveOptions.Formatter.DEFAULT` για γενική έξοδο. Αυτό δείχνει την ευελιξία του **set markdown formatter** για διαφορετικές ροές εργασίας.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| Οι εικόνες λείπουν στο αρχείο Markdown | Ο μετατροπέας δεν ενσωματώνει τα δεδομένα της εικόνας· αντιγράφει μόνο το χαρακτηριστικό `src`. | Βεβαιωθείτε ότι τα URLs των εικόνων είναι απόλυτα ή αντιγράψτε τα αρχεία εικόνας στον ίδιο φάκελο με την έξοδο Markdown. |
| Η στοίχιση του πίνακα είναι λανθασμένη | Διαφορετικοί μορφοποιητές διαχειρίζονται τη στοίχιση των στηλών διαφορετικά. | Επιλέξτε τον μορφοποιητή που ταιριάζει στην πλατφόρμα-στόχο ή προσαρμόστε χειροκίνητα τον παραγόμενο πίνακα. |
| Οι χαρακτήρες Unicode γίνονται ακατάληπτοι | Το πηγαίο HTML χρησιμοποιεί διαφορετική κωδικοποίηση από UTF‑8. | Ανοίξτε το αρχείο HTML με τη σωστή κωδικοποίηση πριν δημιουργήσετε το `HTMLDocument`. |

## Επαλήθευση της μετατροπής

Αφού εκτελέσετε το script, ανοίξτε το παραγόμενο αρχείο `.md` σε έναν προβολέα Markdown (π.χ., VS Code, GitLab UI). Ελέγξτε ότι οι επικεφαλίδες, οι λίστες και τα μπλοκ κώδικα εμφανίζονται όπως αναμένεται. Αν παρατηρήσετε διαφορές, επανεξετάστε το **set markdown formatter** για να επιλέξετε μια πιο κατάλληλη προεπιλογή.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **μετατρέψετε HTML σε Markdown**, **εξάγετε HTML ως Markdown**, και **ορίσετε τον μορφοποιητή markdown** ώστε να ταιριάζει με τη γεύση του GitLab. Η πλήρης λύση—φόρτωση του HTML, ρύθμιση του μορφοποιητή και κλήση του μετατροπέα—καλύπτει τις πιο κοινές περιπτώσεις χρήσης και μπορεί να επεκταθεί για μαζική επεξεργασία ή προσαρμοσμένες ανάγκες μορφοποίησης.

Μη διστάσετε να πειραματιστείτε με άλλες επιλογές μορφοποιητή (`GFM`, `DEFAULT`) ή να ενσωματώσετε αυτό το script σε μια CI/CD pipeline που δημιουργεί αυτόματα τεκμηρίωση από πηγές HTML. Καλή μετατροπή!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική;

Τα παρακάτω tutorials καλύπτουν στενά σχετικούς τομείς που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Μετατροπή HTML σε Markdown με Aspose.HTML για Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Μετατροπή HTML σε Markdown σε .NET με Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Markdown σε HTML Java - Μετατροπή με Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}