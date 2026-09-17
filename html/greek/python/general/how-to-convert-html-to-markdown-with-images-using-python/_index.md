---
category: general
date: 2026-09-16
description: Μάθετε πώς να μετατρέπετε γρήγορα το HTML σε markdown, να εξάγετε το
  HTML ως markdown και να διατηρείτε τις εικόνες ανέπαφες με ένα απλό script Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- export html as markdown
- save html page as markdown
- how to convert html to markdown
- markdown conversion with images
language: el
lastmod: 2026-09-16
og_description: Μετατρέψτε HTML σε markdown και διατηρήστε τις εικόνες. Αυτό το σεμινάριο
  σας δείχνει πώς να εξάγετε HTML ως markdown χρησιμοποιώντας ένα σύντομο σενάριο
  Python.
og_image_alt: convert html to markdown script output showing markdown file with images
og_title: Μετατροπή HTML σε markdown με εικόνες – βήμα‑βήμα οδηγός Python
schemas:
- author: GroupDocs
  dateModified: '2026-09-16'
  description: Learn to convert HTML to markdown quickly, export HTML as markdown
    and keep images intact with a simple Python script.
  headline: How to convert HTML to markdown with images using Python
  type: TechArticle
- description: Learn to convert HTML to markdown quickly, export HTML as markdown
    and keep images intact with a simple Python script.
  name: How to convert HTML to markdown with images using Python
  steps:
  - name: '**Validate the source HTML** – malformed markup can cause missing elements
      in the markdown output. Use tools like `html5lib` or browser dev tools to clean
      up the HTML first.'
    text: '**Validate the source HTML** – malformed markup can cause missing elements
      in the markdown output. Use tools like `html5lib` or browser dev tools to clean
      up the HTML first.'
  - name: '**Keep the output folder writable** – the script needs permission to create
      the resource sub‑folder.'
    text: '**Keep the output folder writable** – the script needs permission to create
      the resource sub‑folder.'
  - name: '**Version‑control the markdown** – once generated, commit the `.md` files
      to your repository; the accompanying resource folder should be added to `.gitignore`
      if you don’t need version history for binary assets.'
    text: '**Version‑control the markdown** – once generated, commit the `.md` files
      to your repository; the accompanying resource folder should be added to `.gitignore`
      if you don’t need version history for binary assets.'
  - name: '**Test the markdown rendering** – open the resulting file in a markdown
      viewer (e.g., VS Code, Typora) to ensure images display as expected.'
    text: '**Test the markdown rendering** – open the resulting file in a markdown
      viewer (e.g., VS Code, Typora) to ensure images display as expected.'
  type: HowTo
tags:
- HTML
- Markdown
- Python
- Document conversion
title: Πώς να μετατρέψετε το HTML σε markdown με εικόνες χρησιμοποιώντας Python
url: /el/python/general/how-to-convert-html-to-markdown-with-images-using-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να μετατρέψετε HTML σε markdown με εικόνες χρησιμοποιώντας Python

Αν χρειάζεστε **μετατροπή HTML σε markdown** και θέλετε να διατηρήσετε όλες τις συνδεδεμένες εικόνες, αυτός ο οδηγός σας παρέχει μια πλήρη, έτοιμη προς εκτέλεση λύση. Είτε μεταφέρετε ένα blog, εξάγετε τεκμηρίωση, είτε δημιουργείτε έναν στατικό γεννήτρια ιστοσελίδων, τα παρακάτω βήματα σας επιτρέπουν να **εξάγετε HTML ως markdown** σε λίγα δευτερόλεπτα.

Θα μάθετε πώς να **αποθηκεύσετε μια σελίδα HTML ως markdown**, να χειρίζεστε αυτόματα την αντιγραφή πόρων και να αποφεύγετε κοινά προβλήματα όπως σπασμένοι σύνδεσμοι εικόνων. Ο οδηγός υποθέτει ότι έχετε βασικές γνώσεις Python και μια πρόσφατη έκδοση της βιβλιοθήκης μετατροπής εγκατεστημένη.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Python 3.8+ εγκατεστημένο (ο κώδικας λειτουργεί σε Windows, macOS και Linux)
* Το πακέτο `groupdocs-conversion` (ή συμβατό) που παρέχει `HTMLDocument`, `MarkdownSaveOptions`, `ResourceHandlingOptions` και `Converter`. Εγκαταστήστε το με:

```bash
pip install groupdocs-conversion
```

* Ένα αρχείο HTML που θέλετε να μετατρέψετε, π.χ. `page.html`, τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε ως `YOUR_DIRECTORY`.

> **Pro tip:** Κρατήστε το HTML και το φάκελο προορισμού markdown μαζί· το script θα αντιγράψει τις εικόνες σε έναν υπο‑φάκελο δίπλα στο αρχείο markdown.

## Βήμα 1: Φορτώστε το έγγραφο HTML που θέλετε να μετατρέψετε

Η πρώτη λειτουργία δημιουργεί ένα αντικείμενο `HTMLDocument` που αντιπροσωπεύει το αρχείο προέλευσης. Αυτό το αντικείμενο δίνει στον μετατροπέα πρόσβαση στο DOM, τα στυλ και τους συνδεδεμένους πόρους.

```python
from groupdocs.conversion import HTMLDocument

# Load the HTML file you wish to convert
doc = HTMLDocument("YOUR_DIRECTORY/page.html")
```

*Γιατί είναι σημαντικό*: Η φόρτωση του εγγράφου το απομονώνει από το σύστημα αρχείων, επιτρέποντας στον μετατροπέα να δουλέψει με μια καθαρή, εν ενθύμιστη αναπαράσταση. Αν η διαδρομή του αρχείου είναι λανθασμένη, ο κατασκευαστής ρίχνει ένα σαφές `FileNotFoundError`, το οποίο μπορείτε να πιάσετε για καλύτερο χειρισμό σφαλμάτων.

## Βήμα 2: Δημιουργήστε επιλογές αποθήκευσης Markdown

`MarkdownSaveOptions` σας επιτρέπει να ρυθμίσετε λεπτομερώς πώς θα παραχθεί το markdown. Για τις περισσότερες περιπτώσεις οι προεπιλογές είναι επαρκείς, αλλά πρέπει να ενεργοποιήσετε τη διαχείριση πόρων για να διατηρήσετε τις εικόνες.

```python
from groupdocs.conversion import MarkdownSaveOptions

# Prepare options for the markdown output
opt = MarkdownSaveOptions()
```

*Γιατί είναι σημαντικό*: Το αντικείμενο επιλογών είναι το σημείο όπου ελέγχετε πράγματα όπως τα τέλη γραμμής, τα επίπεδα επικεφαλίδων και η διαχείριση εικόνων. Χωρίς τη δημιουργία του, θα βασίζεστε στις προεπιλογές της βιβλιοθήκης, οι οποίες μπορεί να παραλείψουν εικόνες.

## Βήμα 3: Διαμορφώστε τη διαχείριση πόρων ώστε να αντιγράψετε όλους τους συνδεδεμένους πόρους

Εικόνες, αρχεία CSS και άλλα περιουσιακά στοιχεία που αναφέρονται στο HTML πρέπει να αποθηκευτούν δίπλα στο αρχείο markdown. Ορίζοντας `copy_resources` σε `True` λέτε στον μετατροπέα να αντιγράψει αυτά τα αρχεία σε φάκελο δίπλα στην έξοδο markdown.

```python
from groupdocs.conversion import ResourceHandlingOptions

# Enable copying of linked resources (images, CSS, etc.)
opt.resource_handling_options = ResourceHandlingOptions()
opt.resource_handling_options.copy_resources = True
```

*Γιατί είναι σημαντικό*: Αν παραλείψετε αυτό το βήμα, το παραγόμενο markdown θα περιέχει URLs εικόνων που δείχνουν στην αρχική θέση, κάτι που συχνά σπάει όταν το markdown μετακινείται. Η ενεργοποίηση της αντιγραφής πόρων εξασφαλίζει μια **μετατροπή markdown με εικόνες** που λειτουργεί εκτός σύνδεσης.

## Βήμα 4: Μετατρέψτε το έγγραφο HTML σε Markdown χρησιμοποιώντας τις διαμορφωμένες επιλογές

Τέλος, καλέστε τη μέθοδο `Converter.convert`, περνώντας το πηγαίο έγγραφο, τη διαδρομή προορισμού και τις επιλογές που προετοιμάσατε.

```python
from groupdocs.conversion import Converter

# Perform the conversion
Converter.convert(doc, "YOUR_DIRECTORY/page.md", opt)
```

Όταν το script ολοκληρωθεί, θα βρείτε το `page.md` στον ίδιο φάκελο, και έναν υπο‑φάκελο με όνομα `page_files` (ή παρόμοιο) που περιέχει κάθε εικόνα και stylesheet που αναφερόταν στο αρχικό HTML.

### Αναμενόμενη έξοδος

Ανοίξτε το `page.md` σε οποιονδήποτε επεξεργαστή κειμένου. Θα πρέπει να δείτε σύνταξη markdown για επικεφαλίδες, παραγράφους, λίστες και συνδέσμους εικόνων που μοιάζουν με αυτό:

```markdown
# Sample Title

Here is a paragraph from the original HTML.

![Alt text](page_files/image1.png)
```

Όλες οι εικόνες είναι τώρα αποθηκευμένες τοπικά, καθιστώντας το αρχείο markdown φορητό.

## Πλήρες, εκτελέσιμο script

Παρακάτω βρίσκεται το πλήρες script που συνδυάζει όλα τα τέσσερα βήματα. Αποθηκεύστε το ως `convert_html_to_md.py` και τρέξτε το με `python convert_html_to_md.py`.

```python
# convert_html_to_md.py
# This script converts an HTML file to markdown and copies all linked resources.
# It demonstrates a reliable "convert html to markdown" workflow with images.

from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, ResourceHandlingOptions, Converter

# ------------------------------------------------------------
# Configuration – adjust these paths for your environment
# ------------------------------------------------------------
INPUT_HTML = "YOUR_DIRECTORY/page.html"   # Path to the source HTML file
OUTPUT_MD = "YOUR_DIRECTORY/page.md"      # Desired markdown output path

def main():
    # Step 1: Load the HTML document
    doc = HTMLDocument(INPUT_HTML)

    # Step 2: Create markdown save options
    opt = MarkdownSaveOptions()

    # Step 3: Enable resource copying so images stay linked
    opt.resource_handling_options = ResourceHandlingOptions()
    opt.resource_handling_options.copy_resources = True

    # Step 4: Execute the conversion
    Converter.convert(doc, OUTPUT_MD, opt)

    print(f"Conversion complete! Markdown saved to: {OUTPUT_MD}")

if __name__ == "__main__":
    main()
```

Τρέξτε το script, και η κονσόλα θα επιβεβαιώσει τη μετατροπή:

```
Conversion complete! Markdown saved to: YOUR_DIRECTORY/page.md
```

## Διαχείριση ειδικών περιπτώσεων και συχνές ερωτήσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| **Τι γίνεται αν το HTML περιέχει εξωτερικές εικόνες (π.χ. `https://example.com/img.png`);** | Ο μετατροπέας κατεβάζει αυτές τις εικόνες στον φάκελο πόρων, εφόσον το URL είναι προσβάσιμο. Αν ο διακομιστής μπλοκάρει το αίτημα, ο σύνδεσμος εικόνας θα παραμείνει αμετάβλητος· μπορείτε να κατεβάσετε χειροκίνητα το αρχείο και να το τοποθετήσετε στον φάκελο πόρων. |
| **Μπορώ να προσαρμόσω το όνομα του φακέλου εικόνων;** | Ναι. Ορίστε `opt.resource_handling_options.resource_folder_name = "my_images"` πριν από τη μετατροπή. |
| **Πώς μετατρέπω πολλαπλά αρχεία HTML σε παρτίδα;** | Τυλίξτε τη λογική μετατροπής σε βρόχο που διατρέχει μια λίστα διαδρομών αρχείων. Επαναχρησιμοποιήστε το ίδιο αντικείμενο `MarkdownSaveOptions` για αποδοτικότητα. |
| **Υπάρχει τρόπος να αφαιρέσω τα CSS στυλ;** | Ορίστε `opt.resource_handling_options.copy_css = False`. Αυτό αφαιρεί τα συνδεδεμένα αρχεία CSS ενώ διατηρεί το περιεχόμενο markdown. |
| **Θα μετατραπούν σωστά οι πίνακες;** | Η βιβλιοθήκη μετατρέπει τους HTML πίνακες σε σύνταξη πίνακα markdown. Πολύπλοκοι ενσωματωμένοι πίνακες μπορεί να χρειαστούν χειροκίνητη προσαρμογή. |

## Καλές πρακτικές για αξιόπιστο **export html as markdown**

1. **Επικυρώστε το HTML προέλευσης** – κακόμορφη σήμανση μπορεί να προκαλέσει ελλιπή στοιχεία στην έξοδο markdown. Χρησιμοποιήστε εργαλεία όπως `html5lib` ή τα dev tools του προγράμματος περιήγησης για να καθαρίσετε το HTML πρώτα.  
2. **Βεβαιωθείτε ότι ο φάκελος εξόδου είναι εγγράψιμος** – το script χρειάζεται δικαιώματα για να δημιουργήσει τον υπο‑φάκελο πόρων.  
3. **Έλεγχος έκδοσης του markdown** – μόλις δημιουργηθούν, κάντε commit τα `.md` αρχεία στο αποθετήριό σας· ο συνοδευτικός φάκελος πόρων θα πρέπει να προστεθεί στο `.gitignore` αν δεν χρειάζεστε ιστορικό για τα δυαδικά αρχεία.  
4. **Δοκιμάστε την απόδοση του markdown** – ανοίξτε το παραγόμενο αρχείο σε έναν προβολέα markdown (π.χ. VS Code, Typora) για να βεβαιωθείτε ότι οι εικόνες εμφανίζονται όπως αναμένεται.

## Συμπέρασμα

Τώρα διαθέτετε μια σταθερή, έτοιμη για παραγωγή μέθοδο **μετατροπής HTML σε markdown** διατηρώντας τις εικόνες, η οποία ικανοποιεί την ανάγκη **αποθήκευσης σελίδας HTML ως markdown** και **εξαγωγής HTML ως markdown** σε ένα ενιαίο, αυτοματοποιημένο βήμα. Με τη διαμόρφωση του `ResourceHandlingOptions`, το script εγγυάται μια καθαρή **μετατροπή markdown με εικόνες** που λειτουργεί σε όλες τις πλατφόρμες.

Στη συνέχεια, εξετάστε σχετικές θεματικές όπως **πώς να μετατρέψετε HTML σε markdown** για μεγάλα σύνολα τεκμηρίωσης, ενσωμάτωση του script σε CI pipeline, ή επέκταση για υποστήριξη άλλων μορφών εξόδου όπως PDF ή DOCX. Καλή μετατροπή!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Μετατροπή HTML σε Markdown με Aspose.HTML για Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Μετατροπή HTML σε Markdown με .NET και Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Markdown σε HTML Java - Μετατροπή με Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}