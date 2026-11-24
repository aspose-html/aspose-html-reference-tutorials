---
category: general
date: 2026-11-24
description: Μετατρέψτε HTML σε Markdown στην Python χρησιμοποιώντας επιλογές τύπου
  GitLab και εξάγετε συνδέσμους εύκολα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- gitlab flavored markdown
- save html as markdown
- html to markdown conversion
- extract links to markdown
language: el
lastmod: 2026-11-24
og_description: Μετατρέψτε HTML σε Markdown στην Python χρησιμοποιώντας επιλογές τύπου
  GitLab, αποθηκεύστε το HTML ως markdown και εξάγετε συνδέσμους σε markdown με ένα
  πλήρες παράδειγμα.
og_image_alt: Screenshot of a Python script converting HTML to GitLab‑flavored Markdown
og_title: Μετατροπή HTML σε Markdown με έξοδο στυλ GitLab – Οδηγός Python
schemas:
- author: Aspose
  dateModified: '2026-11-24'
  description: Convert HTML to Markdown in Python using GitLab‑flavored options and
    extract links easily.
  headline: How to convert HTML to Markdown with GitLab‑flavored output in Python
  type: TechArticle
tags:
- HTML
- Markdown
- Python
- Conversion
- GitLab
title: Πώς να μετατρέψετε το HTML σε Markdown με έξοδο τύπου GitLab σε Python
url: /el/python/general/how-to-convert-html-to-markdown-with-gitlab-flavored-output/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να μετατρέψετε HTML σε Markdown με μορφοποίηση τύπου GitLab σε Python

Αν χρειάζεστε **μετατροπή HTML σε Markdown**, αυτός ο οδηγός παρουσιάζει μια πλήρη, έτοιμη προς εκτέλεση λύση. Θα δείτε πώς να αποθηκεύσετε html ως markdown χρησιμοποιώντας μορφοποίηση τύπου GitLab και πώς να εξάγετε συνδέσμους σε markdown χωρίς να αφήσετε τον κώδικα.

Η προσέγγιση λειτουργεί με τη βιβλιοθήκη Aspose.HTML for Python, η οποία παρέχει ένα API μετατροπής μίας γραμμής και λεπτομερή έλεγχο της γεύσης του Markdown. Στο τέλος του tutorial θα έχετε ένα script που παράγει καθαρά αρχεία GitLab‑flavored markdown και μια λίστα εξαγόμενων συνδέσμων.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Python 3.8 ή νεότερη έκδοση εγκατεστημένη.
* Πρόσβαση στο `pip` για εγκατάσταση πακέτων.
* Τοπικό αρχείο HTML (π.χ., `article.html`) που θέλετε να μετατρέψετε.
* Βασική εξοικείωση με την εκτέλεση Python scripts από τη γραμμή εντολών.

Δεν απαιτούνται πρόσθετα εργαλεία· η βιβλιοθήκη διαχειρίζεται την ανάλυση, τη μετατροπή και την εξαγωγή συνδέσμων εσωτερικά.

## Εγκατάσταση της βιβλιοθήκης Aspose.HTML for Python

Το API μετατροπής βρίσκεται στο πακέτο `aspose.html`. Εγκαταστήστε το με `pip`:

```bash
pip install aspose-html
```

Το πακέτο περιλαμβάνει τις κλάσεις `HTMLDocument`, `MarkdownSaveOptions` και `Converter` που χρησιμοποιούνται αργότερα στο script. Η εγκατάσταση ολοκληρώνεται σε δευτερόλεπτα και δεν απαιτεί ξεχωριστό runtime.

## Φόρτωση του εγγράφου HTML

Η δημιουργία ενός αντικειμένου `HTMLDocument` φορτώνει το αρχείο προέλευσης στη μνήμη. Ο κατασκευαστής δέχεται διαδρομή αρχείου ή URL.

```python
from aspose.html import HTMLDocument

# Load the HTML file you want to convert.
doc = HTMLDocument("YOUR_DIRECTORY/article.html")
```

Η παρουσία `doc` αντιπροσωπεύει τώρα το πλήρες δέντρο DOM, επιτρέποντας στον μετατροπέα να διαβάσει κάθε στοιχείο, συμπεριλαμβανομένων των συνδέσμων και των ετικετών παραγράφου.

## Διαμόρφωση επιλογών GitLab‑flavored Markdown

Το GitLab‑flavored markdown διαφέρει από το τυπικό CommonMark στον τρόπο που αντιμετωπίζει συνδέσμους και παραγράφους. Η κλάση `MarkdownSaveOptions` σας επιτρέπει να καθορίσετε τον formatter και το σύνολο χαρακτηριστικών που χρειάζεστε.

```python
from aspose.html import MarkdownSaveOptions

# Configure options for GitLab‑flavored output.
#   formatter="GIT"  -> GitLab markdown
#   features=["Link", "Paragraph"] -> keep only links and paragraphs.
opts = MarkdownSaveOptions(formatter="GIT", features=["Link", "Paragraph"])
```

Ορίζοντας `features` σε `["Link", "Paragraph"]` εξασφαλίζει ότι η μετατροπή εστιάζει στην εξαγωγή συνδέσμων διατηρώντας τη δομή των παραγράφων, κάτι ιδανικό για τεκμηρίωση ή δημιουργία changelog.

## Εκτέλεση της μετατροπής και αποθήκευση ως Markdown

Με το έγγραφο φορτωμένο και τις επιλογές διαμορφωμένες, καλέστε τη στατική μέθοδο `Converter.convert`. Αυτή γράφει το αποτέλεσμα απευθείας στο αρχείο προορισμού.

```python
from aspose.html import Converter

# Perform the conversion and write the markdown file.
Converter.convert(doc, "YOUR_DIRECTORY/article.md", opts)
```

Μετά την εκτέλεση, το `article.md` περιέχει GitLab‑flavored markdown που αντικατοπτρίζει τους συνδέσμους και τις παραγράφους του αρχικού HTML.

## Επαλήθευση του αποτελέσματος και εξαγωγή συνδέσμων σε markdown

Ανοίξτε το παραγόμενο αρχείο για να επιβεβαιώσετε τη μετατροπή. Θα πρέπει να δείτε τη σύνταξη συνδέσμου (`[text](url)`) και τις διακοπές παραγράφων που ταιριάζουν με την πηγή.

```python
# Quick verification: read and print the first 10 lines.
with open("YOUR_DIRECTORY/article.md", "r", encoding="utf-8") as f:
    for i, line in enumerate(f):
        if i >= 10:
            break
        print(line.rstrip())
```

Αν χρειάζεστε τη ακατέργαστη λίστα URL για περαιτέρω επεξεργασία, μπορείτε να την εξάγετε από το `HTMLDocument` πριν από τη μετατροπή:

```python
# Extract all anchor href attributes.
links = [a.get_attribute("href") for a in doc.get_elements_by_tag_name("a")]
print("Extracted links:", links)
```

Αυτό το βήμα δείχνει **extract links to markdown** χρησιμοποιώντας το ίδιο DOM που έχετε ήδη, αποφεύγοντας δεύτερη ανάλυση.

## Πλήρες script

Συνδυάζοντας όλα τα παραπάνω προκύπτει ένα ενιαίο, αυτόνομο script που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο:

```python
# convert_html_to_gitlab_md.py
from aspose.html import HTMLDocument, MarkdownSaveOptions, Converter

def convert_html_to_markdown(src_path: str, dst_path: str) -> list:
    """
    Convert an HTML file to GitLab‑flavored Markdown and return a list of extracted links.

    Args:
        src_path: Path to the source HTML file.
        dst_path: Path where the Markdown file will be saved.

    Returns:
        A list of URLs found in the HTML document.
    """
    # Load the HTML document.
    doc = HTMLDocument(src_path)

    # Configure GitLab‑flavored Markdown options (links and paragraphs only).
    opts = MarkdownSaveOptions(formatter="GIT", features=["Link", "Paragraph"])

    # Convert and save as Markdown.
    Converter.convert(doc, dst_path, opts)

    # Extract links for additional processing.
    links = [a.get_attribute("href") for a in doc.get_elements_by_tag_name("a")]
    return links

if __name__ == "__main__":
    source = "YOUR_DIRECTORY/article.html"
    target = "YOUR_DIRECTORY/article.md"
    extracted_links = convert_html_to_markdown(source, target)

    print(f"Conversion complete. Markdown saved to {target}")
    print("Extracted links:", extracted_links)
```

Εκτέλεση του script:

```bash
python convert_html_to_gitlab_md.py
```

παράγει το `article.md` με GitLab‑flavored markdown και εκτυπώνει τη λίστα των εξαγόμενων URL.

## Συνηθισμένες παραλλαγές και edge cases

| Σενάριο                              | Προσαρμογή                                                                 |
|--------------------------------------|-----------------------------------------------------------------------------|
| **Πλήρες HTML (εικόνες, πίνακες, κ.λπ.)** | Προσθέστε `"Image"` ή `"Table"` στα `features` για να διατηρήσετε αυτά τα στοιχεία. |
| **Διαφορετική γεύση Markdown**        | Αλλάξτε `formatter="GIT"` σε `"COMMONMARK"` ή `"GFM"` για άλλες πλατφόρμες. |
| **Μεγάλα αρχεία (> 50 MB)**             | Χρησιμοποιήστε streaming APIs (`HTMLDocument.open`) για να αποφύγετε τη φόρτωση ολόκληρου του αρχείου. |
| **Χαρακτήρες Unicode**                | Βεβαιωθείτε ότι το αρχείο προέλευσης είναι κωδικοποιημένο σε UTF‑8· η βιβλιοθήκη διατηρεί την κωδικοποίηση. |

Αυτές οι παραλλαγές σας επιτρέπουν να επαναχρησιμοποιήσετε το ίδιο μοτίβο για **save html as markdown** σε πολλές περιπτώσεις.

## Pro tips

* **Επαναχρησιμοποίηση επιλογών:** Δημιουργήστε ένα μόνο αντικείμενο `MarkdownSaveOptions` και περάστε το αν μετατρέπετε πολλά αρχεία σε μια παρτίδα.
* **Επικύρωση συνδέσμων:** Μετά την εξαγωγή, εκτελέστε έναν απλό έλεγχο `requests.head(url)` για να εντοπίσετε σπασμένους συνδέσμους.
* **Κλείδωμα έκδοσης:** Καθορίστε την έκδοση του Aspose.HTML (`aspose-html==23.10`) για να αποφύγετε απρόσμενες αλλαγές στο API.

## Συμπέρασμα

Τώρα ξέρετε πώς να **μετατρέψετε HTML σε markdown** χρησιμοποιώντας έναν formatter τύπου GitLab, να **save html as markdown**, και να **extract links to markdown** με ένα σύντομο Python script. Η λύση λειτουργεί αμέσως, αντιμετωπίζει τυπικές edge cases και μπορεί να επεκταθεί για άλλες γεύσεις Markdown ή πρόσθετα χαρακτηριστικά HTML.

### Επόμενα βήματα

* Εξερευνήστε τη λίστα `features` για να συμπεριλάβετε εικόνες, πίνακες ή μπλοκ κώδικα.
* Ενσωματώστε αυτό το script σε pipeline CI για αυτόματη δημιουργία τεκμηρίωσης από πηγές HTML.
* Συνδυάστε τους εξαγόμενους συνδέσμους με υπηρεσία ελέγχου συνδέσμων για να διατηρήσετε υγιείς αναφορές.

Αισθανθείτε ελεύθεροι να προσαρμόσετε το script στις δικές σας ροές εργασίας και να μοιραστείτε τα αποτελέσματά σας με την κοινότητα!

## What Should You Learn Next?

Οι παρακάτω οδηγίες καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Μετατροπή HTML σε Markdown Python – εξαγωγή συνδέσμων & παραγράφων](/html/english/python/general/convert-html-to-markdown-python-extract-links-paragraphs/)
- [Πώς να μετατρέψετε HTML σε Markdown με μορφοποίηση τύπου GitLab σε Python](/html/english/python/general/how-to-convert-html-to-markdown-with-gitlab-flavored-markdow/)
- [convert html to markdown python – αποθήκευση αρχείου markdown με python](/html/english/python/general/convert-html-to-markdown-python-save-markdown-file-with-pyth/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}