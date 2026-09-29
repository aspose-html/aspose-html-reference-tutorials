---
category: general
date: 2026-09-29
description: Μετατρέψτε HTML σε markdown με Python ενώ εξάγετε συνδέσμους από το HTML
  και τις παραγράφους. Μάθετε πώς να αποθηκεύετε το HTML ως markdown με λεπτομερή
  έλεγχο.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- save html as markdown
- extract paragraphs from html
- convert html to markdown python
language: el
lastmod: 2026-09-29
og_description: Μετατρέψτε το HTML σε markdown με Python και Aspose.HTML. Αυτός ο
  οδηγός δείχνει πώς να εξάγετε συνδέσμους από HTML, να εξάγετε παραγράφους και να
  αποθηκεύσετε το HTML ως markdown.
og_image_alt: Screenshot of Python code converting an HTML file to a partial Markdown
  file
og_title: Μετατροπή HTML σε Markdown με Python – εξαγωγή συνδέσμων & παραγράφων
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: convert HTML to markdown in Python while extracting links from HTML
    and paragraphs. Learn to save HTML as markdown with fine‑grained control.
  headline: How to convert HTML to Markdown in Python and extract links and paragraphs
  type: TechArticle
tags:
- Python
- Aspose.HTML
- Markdown conversion
title: Πώς να μετατρέψετε το HTML σε Markdown με Python και να εξάγετε συνδέσμους
  και παραγράφους
url: /el/python/general/how-to-convert-html-to-markdown-in-python-and-extract-links/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να μετατρέψετε HTML σε Markdown σε Python και να εξάγετε συνδέσμους και παραγράφους

Αν χρειάζεστε **convert HTML to markdown** σε Python, αυτό το tutorial σας παρουσιάζει μια έτοιμη προς εκτέλεση λύση. Είτε δημιουργείτε έναν static‑site generator είτε συλλέγετε τεκμηρίωση, θα μάθετε πώς να εξάγετε συνδέσμους από HTML, να εξάγετε παραγράφους από HTML, και να αποθηκεύετε HTML ως markdown με ακριβή έλεγχο της εξόδου.

Θα ολοκληρώσετε τον οδηγό με ένα πλήρες script που διαβάζει ένα αρχείο HTML, επιλέγει μόνο τα στοιχεία που σας ενδιαφέρουν, και γράφει ένα αρχείο Markdown που περιέχει μόνο αυτά τα στοιχεία. Δεν απαιτούνται εξωτερικά εργαλεία CLI—όλα εκτελούνται από καθαρό Python χρησιμοποιώντας τη βιβλιοθήκη Aspose.HTML.

## Προαπαιτούμενα

* Εγκατεστημένο Python 3.8 ή νεότερο.
* Ένα ενεργό license του Aspose.HTML for Python (η δωρεάν δοκιμή λειτουργεί για αξιολόγηση).
* `pip install aspose-html` για την εγκατάσταση του SDK.
* Ένα δείγμα αρχείου HTML (`sample.html`) που βρίσκεται σε φάκελο που μπορείτε να αναφέρετε.

Αν δεν έχετε εγκαταστήσει ακόμη το SDK, εκτελέστε:

```bash
pip install aspose-html
```

## Βήμα 1: Φορτώστε το έγγραφο HTML που θέλετε να μετατρέψετε

Η πρώτη ενέργεια είναι να δημιουργήσετε ένα αντικείμενο `HTMLDocument` που αντιπροσωπεύει το αρχείο προέλευσης. Ο κατασκευαστής δέχεται διαδρομή αρχείου ή ροή, ώστε να μπορείτε να το δείξετε σε οποιαδήποτε τοπική ή απομακρυσμένη πηγή HTML.

```python
from aspose.html import HTMLDocument, MarkdownSaveOptions, MarkdownFeatures, Converter

# Load the HTML file you want to convert
html_path = "YOUR_DIRECTORY/sample.html"
html_doc = HTMLDocument(html_path)
```

**Γιατί είναι σημαντικό:** `HTMLDocument` αναλύει το markup σε ένα δέντρο DOM, παρέχοντάς σας προγραμματιστική πρόσβαση σε κάθε στοιχείο. Αυτό το βήμα είναι υποχρεωτικό επειδή ο μετατροπέας λειτουργεί σε αντικείμενο εγγράφου, όχι σε ακατέργαστο κείμενο.

## Βήμα 2: Διαμορφώστε ποια στοιχεία HTML πρέπει να μετατραπούν σε Markdown

Το Aspose.HTML σας επιτρέπει να ρυθμίσετε λεπτομερώς τη μετατροπή μέσω του `MarkdownSaveOptions`. Ορίζοντας τη σημαία `features` αποφασίζετε ποια τμήματα της πηγής θα εξαχθούν ως Markdown. Σε αυτό το tutorial ενεργοποιούμε μόνο **links** και **paragraphs**, που ικανοποιούν τις δευτερεύουσες λέξεις-κλειδιά *extract links from html* και *extract paragraphs from html*.

```python
# Create Markdown save options
md_opts = MarkdownSaveOptions()

# Enable only links and paragraphs; all other elements are ignored
md_opts.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS
```

**Γιατί είναι σημαντικό:** Αν παραλείψετε αυτή τη διαμόρφωση, ο μετατροπέας θα μετατρέψει ολόκληρη τη σελίδα, συμπεριλαμβανομένων εικόνων, πινάκων και scripts. Περιορίζοντας το σύνολο των χαρακτηριστικών διατηρείτε την έξοδο μικρή και εστιασμένη, κάτι ιδανικό για pipelines εξαγωγής περιεχομένου.

## Βήμα 3: Εκτελέστε τη μετατροπή και αποθηκεύστε το αποτέλεσμα

Με το έγγραφο φορτωμένο και τις επιλογές ορισμένες, καλέστε το `Converter.convert_html`. Η μέθοδος γράφει το αρχείο Markdown απευθείας στο δίσκο.

```python
# Destination path for the generated Markdown file
md_path = "YOUR_DIRECTORY/partial.md"

# Convert the HTML document to Markdown using the configured options
Converter.convert_html(html_doc, md_opts, md_path)

print(f"Markdown saved to {md_path}")
```

**Τι θα δείτε:** Αν το `sample.html` περιέχει μια παράγραφο και έναν σύνδεσμο, το `partial.md` θα περιέχει κάτι όπως:

```markdown
This is a sample paragraph extracted from the HTML file.

[Visit Aspose](https://www.aspose.com)
```

Όλα τα άλλα στοιχεία (εικόνες, πίνακες, scripts) παραλείπονται επειδή ενεργοποιήσαμε μόνο `LINKS` και `PARAGRAPHS`.

## Πλήρες script – έτοιμο για αντιγραφή και εκτέλεση

Παρακάτω βρίσκεται το πλήρες, εκτελέσιμο πρόγραμμα που συνδυάζει τα τρία βήματα. Αντικαταστήστε το `YOUR_DIRECTORY` με την απόλυτη ή σχετική διαδρομή που περιέχει το `sample.html`.

```python
# convert_html_to_markdown.py
from aspose.html import HTMLDocument, MarkdownSaveOptions, MarkdownFeatures, Converter

def convert_html_to_markdown(
    source_html: str,
    target_md: str,
    include_links: bool = True,
    include_paragraphs: bool = True,
) -> None:
    """
    Convert an HTML file to a Markdown file, optionally extracting only links
    and/or paragraphs.

    Args:
        source_html: Path to the input HTML file.
        target_md:   Path where the Markdown output should be written.
        include_links:      When True, <a> elements become Markdown links.
        include_paragraphs: When True, <p> elements become plain text paragraphs.
    """
    # Load the HTML document
    html_doc = HTMLDocument(source_html)

    # Prepare save options
    md_opts = MarkdownSaveOptions()
    features = 0
    if include_links:
        features |= MarkdownFeatures.LINKS
    if include_paragraphs:
        features |= MarkdownFeatures.PARAGRAPHS
    md_opts.features = features

    # Convert and save
    Converter.convert_html(html_doc, md_opts, target_md)
    print(f"Conversion complete: {target_md}")

if __name__ == "__main__":
    # Example usage
    convert_html_to_markdown(
        source_html="YOUR_DIRECTORY/sample.html",
        target_md="YOUR_DIRECTORY/partial.md",
        include_links=True,
        include_paragraphs=True,
    )
```

### Εκτέλεση του script

```bash
python convert_html_to_markdown.py
```

Θα πρέπει να δείτε το μήνυμα επιβεβαίωσης και να βρείτε το `partial.md` στον ίδιο φάκελο.

## Διαχείριση περιπτώσεων άκρων και κοινών παραλλαγών

| Situation | Recommended tweak | Reason |
|-----------|-------------------|--------|
| **Χρειάζεστε επίσης επικεφαλίδες** | Προσθέστε `MarkdownFeatures.HEADINGS` στη σημαία `features`. | Οι επικεφαλίδες είναι χρήσιμες για τη δημιουργία πίνακα περιεχομένων. |
| **Πρέπει να διατηρηθούν οι εικόνες** | Συμπεριλάβετε `MarkdownFeatures.IMAGES`. | Ο μετατροπέας θα ενσωματώσει συνδέσμους εικόνας χρησιμοποιώντας τη σύνταξη `![]()`. |
| **Τα μεγάλα αρχεία HTML προκαλούν πίεση μνήμης** | Χρησιμοποιήστε `HTMLDocument.from_stream` με μια bufferized ροή, και στη συνέχεια μετατρέψτε σε κομμάτια. | Η ροή μειώνει τη μέγιστη χρήση μνήμης. |
| **Θέλετε να διατηρήσετε τα ενσωματωμένα στυλ** | Ορίστε `md_opts.inline_styles = True`. | Αυτό διατηρεί το CSS ως ενσωματωμένο HTML μέσα στο Markdown, χρήσιμο για πρότυπα email. |
| **Οι χαρακτήρες Unicode είναι κατεστραμμένοι** | Βεβαιωθείτε ότι το αρχείο προέλευσης είναι αποθηκευμένο ως UTF‑8 και περάστε `encoding='utf-8'` κατά τη δημιουργία του `HTMLDocument`. | Η σωστή κωδικοποίηση αποτρέπει τη διαστρέβλωση χαρακτήρων. |

## Pro συμβουλές για αξιόπιστες μετατροπές

* **Επικυρώστε πρώτα το HTML** – εσφαλμένο markup μπορεί να οδηγήσει σε ελλιπή στοιχεία. Χρησιμοποιήστε `html_doc.validate()` αν υποψιάζεστε προβλήματα.
* **Καταγράψτε τα χαρακτηριστικά που ενεργοποιείτε** – η εκτύπωση του `md_opts.features` πριν από τη μετατροπή βοηθά στον εντοπισμό του γιατί λείπει κάποιο στοιχείο.
* **Δοκιμάστε με ένα ελάχιστο απόσπασμα HTML** – ένα αρχείο που περιέχει μόνο ένα `<p>` και ένα `<a>` σας επιτρέπει να επαληθεύσετε γρήγορα τη λογική των σημαιών.
* **Κλείδωμα έκδοσης** – οι εκδόσεις του Aspose.HTML είναι συμβατές προς τα πίσω, αλλά καθορίστε την έκδοση του SDK στο `requirements.txt` για να αποφύγετε απρόσμενες αλλαγές που σπάζουν.

## Συμπέρασμα

Τώρα ξέρετε πώς να **convert HTML to markdown** σε Python ενώ εξάγετε ακριβώς **links from HTML** και **paragraphs from HTML**. Διαμορφώνοντας το `MarkdownSaveOptions`, μπορείτε επίσης να **save HTML as markdown** με οποιονδήποτε συνδυασμό στοιχείων χρειάζεστε, κάνοντας τη διαδικασία ευέλικτη για web‑scraping, pipelines τεκμηρίωσης ή static‑site generation.

Τα επόμενα βήματα που μπορείτε να εξερευνήσετε περιλαμβάνουν:

* Προσθήκη `MarkdownFeatures.HEADINGS` και `MarkdownFeatures.IMAGES` για παραγωγή πιο πλούσιου Markdown.
* Ενσωμάτωση του script σε μια ροή εργασίας CI/CD που δημιουργεί αυτόματα τεκμηρίωση από πηγές HTML.
* Συνδυασμός της εξόδου με έναν static‑site generator όπως το MkDocs ή το Hugo για μια πλήρως αυτοματοποιημένη pipeline δημοσίευσης.

Μη διστάσετε να πειραματιστείτε με διαφορετικές σημαίες `MarkdownFeatures` και να μοιραστείτε τα αποτελέσματά σας. Καλό κώδικα!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Μετατροπή HTML σε Markdown στο Aspose.HTML για Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Μετατροπή HTML σε Markdown σε .NET με Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Μετατροπή markdown σε html – Οδηγός Java με έξοδο PDF](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html-java-guide-with-pdf-output/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}