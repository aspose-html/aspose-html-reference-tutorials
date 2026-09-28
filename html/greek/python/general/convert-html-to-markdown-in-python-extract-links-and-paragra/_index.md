---
category: general
date: 2026-09-26
description: Μετατρέψτε το HTML σε Markdown με Python, εξάγοντας συνδέσμους από το
  HTML και αποθηκεύοντας το HTML ως Markdown. Μάθετε πώς να μετατρέπετε το HTML βήμα‑βήμα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- save html as markdown
- how to convert html
- extract paragraphs from html
language: el
lastmod: 2026-09-26
og_description: Μετατρέψτε το HTML σε Markdown με Python, εξάγοντας συνδέσμους από
  το HTML και αποθηκεύοντας το HTML ως Markdown. Ακολουθήστε αυτόν τον πλήρη οδηγό.
og_image_alt: Screenshot of Python code converting HTML to Markdown and showing extracted
  links
og_title: Μετατροπή HTML σε Markdown με Python – εξαγωγή συνδέσμων και παραγράφων
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Convert HTML to Markdown with Python, extracting links from HTML and
    saving HTML as Markdown. Learn how to convert HTML step‑by‑step.
  headline: Convert HTML to Markdown in Python – extract links and paragraphs easily
  type: TechArticle
- description: Convert HTML to Markdown with Python, extracting links from HTML and
    saving HTML as Markdown. Learn how to convert HTML step‑by‑step.
  name: Convert HTML to Markdown in Python – extract links and paragraphs easily
  steps:
  - name: Expected output
    text: 'Running the script generates a file similar to the following (the exact
      content depends on the source HTML):'
  - name: 1. Extract only links
    text: '```python md_options.features = MarkdownFeatures.LINKS # No paragraphs
      ```'
  - name: 2. Extract only paragraphs
    text: '```python md_options.features = MarkdownFeatures.PARAGRAPHS # No links
      ```'
  type: HowTo
- questions:
  - answer: Yes. `HTMLDocument` accepts any well‑formed fragment; the converter treats
      the fragment as the document body.
    question: Does this work with HTML fragments (no `<html>` root tag)?
  - answer: 'Add `MarkdownFeatures.IMAGES` to the `features` flag: ```python md_options.features
      = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS | MarkdownFeatures.IMAGES
      ```'
    question: Can I keep images as Markdown image syntax?
  - answer: 'Wrap `convert_html_to_markdown` in a loop that walks the directory with
      `os.listdir` or `pathlib.Path.rglob("*.html")`. --- ## Conclusion You now know
      how to **convert HTML to Markdown** in Python while selectively **extracting
      links from HTML** and **extracting paragraphs from HTML**. The script de'
    question: How do I convert many files in a directory?
  type: FAQPage
tags:
- html
- markdown
- python
- data‑extraction
title: Μετατροπή HTML σε Markdown με Python – εξαγωγή συνδέσμων και παραγράφων εύκολα
url: /el/python/general/convert-html-to-markdown-in-python-extract-links-and-paragra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή HTML σε Markdown με Python – εξαγωγή συνδέσμων και παραγράφων εύκολα

Αν χρειάζεστε **convert HTML to Markdown** κρατώντας μόνο τα χρήσιμα μέρη, αυτός ο οδηγός σας δείχνει πώς να το κάνετε με λίγες γραμμές κώδικα Python. Είτε κάνετε scraping σε blog posts, είτε αρχειοθετείτε τεκμηρίωση, είτε καθαρίζετε το σώμα email, θα μάθετε έναν αξιόπιστο τρόπο να εξάγετε συνδέσμους από HTML και να αποθηκεύσετε HTML ως Markdown.

Το tutorial καλύπτει τα πάντα, από την εγκατάσταση του απαιτούμενου πακέτου μέχρι τη διαχείριση edge cases όπως κενές ετικέτες `<a>` ή ένθετες παραγράφους. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση script που **converts HTML to Markdown**, εξάγει συνδέσμους από HTML, και ακόμη εξάγει παραγράφους από HTML όταν τις χρειάζεστε.

---

## Προαπαιτήσεις

* Εγκατεστημένο Python 3.8 ή νεότερο  
* Πρόσβαση στο πακέτο Python `groupdocs-conversion` (η βιβλιοθήκη που παρέχει `HTMLDocument`, `MarkdownSaveOptions` και `Converter`)  
* Ένα τοπικό αρχείο HTML που θέλετε να επεξεργαστείτε (π.χ., `article.html`)

Μπορείτε να εγκαταστήσετε τη βιβλιοθήκη με pip:

```bash
pip install groupdocs-conversion
```

> **Συμβουλή:** Χρησιμοποιήστε ένα εικονικό περιβάλλον (`python -m venv venv`) για να διατηρήσετε τις εξαρτήσεις απομονωμένες.

---

## Βήμα 1: Φόρτωση του πηγαίου εγγράφου HTML

Η πρώτη ενέργεια είναι η δημιουργία ενός αντικειμένου `HTMLDocument` που δείχνει στο πηγαίο αρχείο σας. Αυτό το αντικείμενο αφαιρεί την ακατέργαστη HTML και δίνει στον μετατροπέα ένα καθαρό σημείο εισόδου.

```python
from groupdocs.conversion import HTMLDocument

# Load the HTML file you want to transform
html_doc = HTMLDocument("YOUR_DIRECTORY/article.html")
```

*Γιατί είναι σημαντικό:* Η φόρτωση του εγγράφου με αυτόν τον τρόπο επιτρέπει στη βιβλιοθήκη να αναλύσει το DOM μία φορά, ώστε οι επόμενες λειτουργίες (όπως η εξαγωγή συνδέσμων ή παραγράφων) να είναι γρήγορες και αποδοτικές σε μνήμη.

---

## Βήμα 2: Δημιουργία επιλογών αποθήκευσης Markdown και επιλογή των χαρακτηριστικών που χρειάζεστε

`MarkdownSaveOptions` σας επιτρέπει να αποφασίσετε ποια στοιχεία HTML θα παραμείνουν μετά τη μετατροπή. Η σημαία `features` χρησιμοποιεί bitwise OR για να συνδυάσει τις επιλογές.

```python
from groupdocs.conversion import MarkdownSaveOptions, MarkdownFeatures

# Keep only links and paragraphs in the resulting Markdown
md_options = MarkdownSaveOptions()
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS
```

*Γιατί είναι σημαντικό:* Καθορίζοντας `LINKS` και `PARAGRAPHS` εσείς **extract links from HTML** και **extract paragraphs from HTML** ενώ απορρίπτετε όλα τα άλλα (styles, scripts, images). Αν αργότερα χρειάζεστε μόνο συνδέσμους, αντικαταστήστε το `MarkdownFeatures.PARAGRAPHS` με `0` (ή παραλείψτε το).

---

## Βήμα 3: Μετατροπή του HTML σε Markdown χρησιμοποιώντας τις ρυθμισμένες επιλογές

Τώρα καλέστε τη στατική μέθοδο `convert_html`, περνώντας το πηγαίο έγγραφο, τη διαδρομή προορισμού και τις επιλογές που μόλις δημιουργήσατε.

```python
from groupdocs.conversion import Converter

# Perform the conversion and write the Markdown file
Converter.convert_html(html_doc, "YOUR_DIRECTORY/article_links.md", md_options)
```

*Γιατί είναι σημαντικό:* Η μετατροπή εκτελείται σε μία μόνο διέλευση, εφαρμόζοντας το φίλτρο χαρακτηριστικών που ορίσατε. Το παραγόμενο αρχείο (`article_links.md`) περιέχει μόνο συνδέσμους και παραγράφους μορφοποιημένα σε Markdown, που είναι ακριβώς αυτό που χρειάζεστε όταν θέλετε να **save HTML as Markdown** για επεξεργασία σε επόμενα βήματα.

---

## Πλήρες script – όλα μαζί

Παρακάτω είναι ένα πλήρες, εκτελέσιμο script που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα αρχείο με όνομα `html_to_md.py`. Προσαρμόστε τις διαδρομές ώστε να ταιριάζουν με το περιβάλλον σας.

```python
# html_to_md.py
# -------------------------------------------------
# Convert HTML to Markdown, keeping only links and paragraphs.
# -------------------------------------------------

from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeatures, Converter

def convert_html_to_markdown(source_path: str, target_path: str) -> None:
    """
    Convert an HTML file to Markdown, extracting only links and paragraphs.

    Args:
        source_path: Path to the source HTML file.
        target_path: Path where the Markdown file will be saved.
    """
    # Load the HTML document
    html_doc = HTMLDocument(source_path)

    # Configure conversion to keep links and paragraphs
    md_options = MarkdownSaveOptions()
    md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS

    # Run the conversion
    Converter.convert_html(html_doc, target_path, md_options)
    print(f"✅ Conversion complete – Markdown saved to: {target_path}")

if __name__ == "__main__":
    # Example usage – replace with your actual file locations
    src = "YOUR_DIRECTORY/article.html"
    dst = "YOUR_DIRECTORY/article_links.md"
    convert_html_to_markdown(src, dst)
```

### Αναμενόμενη έξοδος

Η εκτέλεση του script δημιουργεί ένα αρχείο παρόμοιο με το παρακάτω (το ακριβές περιεχόμενο εξαρτάται από το πηγαίο HTML):

```markdown
[OpenAI](https://openai.com)

This is the first paragraph of the article.

[GitHub](https://github.com)

Another paragraph that explains the next topic.
```

Μόνο το κείμενο των συνδέσμων και το κείμενο των παραγράφων εμφανίζονται· όλα τα άλλα στοιχεία HTML αφαιρούνται.

---

## Εξαγωγή μόνο συνδέσμων ή μόνο παραγράφων (προχωρημένες παραλλαγές)

Μερικές φορές χρειάζεστε **how to convert HTML** σε ένα αρχείο Markdown που περιέχει μόνο έναν τύπο στοιχείου.

### 1. Εξαγωγή μόνο συνδέσμων

```python
md_options.features = MarkdownFeatures.LINKS   # No paragraphs
```

### 2. Εξαγωγή μόνο παραγράφων

```python
md_options.features = MarkdownFeatures.PARAGRAPHS   # No links
```

Και οι δύο παραλλαγές επαναχρησιμοποιούν την ίδια κλήση `convert_html`, ώστε να μην χρειάζεται να γράψετε ξεχωριστή λογική μετατροπής.

---

## Διαχείριση edge cases

| Κατάσταση | Προτεινόμενη διόρθωση |
|-----------|-----------------------|
| Το αρχείο HTML περιέχει κενές ετικέτες `<a>` | Ο μετατροπέας παραλείπει αυτόματα κενά συνδέσμους. Αν δείτε ανεπιθύμητες καταχωρήσεις `[]()`, ορίστε `md_options.removeEmptyLinks = True`. |
| Ένθετες παράγραφοι (`<p>` μέσα σε `<div>`) | Η βιβλιοθήκη επίπεδωσε τις ένθετες παραγράφους, διατηρώντας τη σειρά του κειμένου. Δεν απαιτείται επιπλέον κώδικας. |
| Μη‑ASCII χαρακτήρες στους τίτλους των συνδέσμων | Βεβαιωθείτε ότι το αρχείο Python είναι αποθηκευμένο με κωδικοποίηση UTF‑8 και ανοίξτε το αρχείο εξόδου με `encoding="utf-8"` αν το διαβάσετε αργότερα. |
| Πολύ μεγάλα αρχεία HTML (≥ 50 MB) | Επεξεργαστείτε το αρχείο σε τμήματα χρησιμοποιώντας `HTMLDocument(stream=io.BytesIO(...))` για να αποφύγετε τη φόρτωση ολόκληρου του αρχείου στη μνήμη. |

---

## Συχνές ερωτήσεις

**Q: Λειτουργεί αυτό με αποσπάσματα HTML (χωρίς ετικέτα ρίζας `<html>`);**  
A: Ναι. `HTMLDocument` δέχεται οποιοδήποτε σωστά μορφοποιημένο απόσπασμα· ο μετατροπέας το αντιμετωπίζει ως σώμα του εγγράφου.

**Q: Μπορώ να διατηρήσω τις εικόνες ως σύνταξη εικόνας Markdown;**  
A: Προσθέστε `MarkdownFeatures.IMAGES` στη σημαία `features`:  
```python
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS | MarkdownFeatures.IMAGES
```

**Q: Πώς μπορώ να μετατρέψω πολλά αρχεία σε έναν φάκελο;**  
A: Τυλίξτε το `convert_html_to_markdown` σε βρόχο που διασχίζει το φάκελο με `os.listdir` ή `pathlib.Path.rglob("*.html")`.

---

## Συμπέρασμα

Τώρα ξέρετε πώς να **convert HTML to Markdown** με Python ενώ εξάγετε επιλεκτικά **extract links from HTML** και **extract paragraphs from HTML**. Το script δείχνει την τυπική προσέγγιση—φόρτωση του εγγράφου, ρύθμιση του `MarkdownSaveOptions` και εκτέλεση του `Converter.convert_html`. Με λίγες προσαρμογές μπορείτε επίσης να **save HTML as Markdown** που περιέχει μόνο συνδέσμους, μόνο παραγράφους ή μια πλήρη πιστή αναπαράσταση.

Στη συνέχεια, μπορείτε να εξερευνήσετε:

* Προσθήκη `MarkdownFeatures.HEADINGS` για διατήρηση των τίτλων ενοτήτων.  
* Χρήση του παραγόμενου Markdown ως είσοδο για στατικούς δημιουργούς ιστοσελίδων όπως MkDocs ή Hugo.  
* Αυτοματοποίηση μαζικών μετατροπών για ολόκληρο αποθετήριο τεκμηρίωσης.

Καλή μετατροπή!

## Τι Θα Μάθετε Στη Σειρά Επόμενη;

Τα παρακάτω tutorials καλύπτουν στενά σχετικό θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Μετατροπή HTML σε Markdown σε .NET με Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Μετατροπή HTML σε Markdown σε Aspose.HTML για Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Πώς να ορίσετε offset κατά τη μετατροπή HTML σε Markdown σε Java](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}