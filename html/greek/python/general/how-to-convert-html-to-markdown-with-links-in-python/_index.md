---
category: general
date: 2026-10-18
description: Μετατρέψτε το HTML σε Markdown με Python και μάθετε πώς να ενσωματώνετε
  συνδέσμους και παραγράφους για καθαρά αρχεία markdown.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- how to include links
- save html as markdown
- how to convert html
- include links markdown
language: el
lastmod: 2026-10-18
og_description: Μετατρέψτε το HTML σε Markdown με Python και δείτε πώς να συμπεριλάβετε
  συνδέσμους και παραγράφους για ένα καλά δομημένο αρχείο markdown.
og_image_alt: Screenshot of converted HTML to Markdown output showing links
og_title: Μετατροπή HTML σε Markdown με συνδέσμους – Οδηγός Python
schemas:
- author: Aspose
  dateModified: '2026-10-18'
  description: Convert HTML to Markdown in Python and learn how to include links and
    paragraphs for clean markdown files.
  headline: How to convert HTML to Markdown with links in Python
  type: TechArticle
- description: Convert HTML to Markdown in Python and learn how to include links and
    paragraphs for clean markdown files.
  name: How to convert HTML to Markdown with links in Python
  steps:
  - name: Expected output
    text: 'Assuming `sample.html` contains:'
  - name: Images
    text: 'Images are not covered by `MarkdownFeature.LINK`. If you also need to **include
      links markdown** for images, enable the `IMAGE` feature:'
  - name: Tables and code blocks
    text: The default conversion already maps `<table>` and `<pre>` tags to markdown
      tables and fenced code blocks. If you want tighter control, explore `MarkdownFeature.TABLE`
      and `MarkdownFeature.CODE_BLOCK`.
  - name: Encoding
    text: 'Make sure the source HTML is UTF‑8 encoded; otherwise you might see garbled
      characters in the markdown file. You can enforce UTF‑8 when reading the file:'
  type: HowTo
tags:
- HTML
- Markdown
- Python
title: Πώς να μετατρέψετε το HTML σε Markdown με συνδέσμους σε Python
url: /el/python/general/how-to-convert-html-to-markdown-with-links-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να μετατρέψετε HTML σε Markdown με συνδέσμους σε Python

Αν χρειάζεστε να **μετατρέψετε HTML σε Markdown** γρήγορα, αυτός ο οδηγός σας δείχνει τα ακριβή βήματα για να το κάνετε ενώ διατηρείτε τους υπερσυνδέσμους και τη δομή των παραγράφων. Θα ανακαλύψετε επίσης **πώς να συμπεριλάβετε συνδέσμους** ώστε το παραγόμενο markdown να διαβάζεται φυσικά.  

Στις επόμενες ενότητες θα καλύψουμε τα πάντα, από την εγκατάσταση της βιβλιοθήκης μέχρι τη διαχείριση ειδικών περιπτώσεων όπως οι σχετικές URL. Στο τέλος του tutorial θα μπορείτε να **αποθηκεύσετε HTML ως Markdown** με μόνο μερικές γραμμές κώδικα.

## Προαπαιτούμενα

* Εγκατεστημένο Python 3.8 ή νεότερο.
* Πρόσβαση στο πακέτο `aspose.html` (το παράδειγμα χρησιμοποιεί Aspose.HTML για Python, αλλά οποιαδήποτε βιβλιοθήκη που προσφέρει `HTMLDocument`, `MarkdownSaveOptions` και `Converter` θα λειτουργήσει παρόμοια).
* Ένα δείγμα αρχείου HTML (`sample.html`) που θέλετε να μετατρέψετε.

Μπορείτε να εγκαταστήσετε το πακέτο Aspose.HTML με pip:

```bash
pip install aspose-html
```

> **Συμβουλή:** Χρησιμοποιήστε ένα εικονικό περιβάλλον (`python -m venv venv`) για να διατηρήσετε τις εξαρτήσεις απομονωμένες.

## Βήμα 1: Φόρτωση του εγγράφου HTML

Η πρώτη ενέργεια είναι η ανάγνωση του πηγαίου αρχείου HTML σε ένα αντικείμενο `HTMLDocument`. Αυτό το αντικείμενο αντιπροσωπεύει το δέντρο DOM και δίνει στον μετατροπέα πλήρη πρόσβαση στο περιεχόμενο της σελίδας.

```python
from aspose.html import HTMLDocument

# Load the HTML document from the file system
doc = HTMLDocument("YOUR_DIRECTORY/sample.html")
```

*Γιατί είναι σημαντικό:* Η φόρτωση του εγγράφου εξασφαλίζει ότι όλα τα στοιχεία—τίτλοι, πίνακες, εικόνες και ιδιαίτερα σύνδεσμοι—αναλύονται σωστά πριν από τη μετατροπή.

## Βήμα 2: Διαμόρφωση επιλογών αποθήκευσης markdown για να συμπεριλάβετε συνδέσμους και παραγράφους

Από προεπιλογή, ορισμένοι μετατροπείς μπορεί να αφαιρούν τους υπερσυνδέσμους ή να συμπτύσσουν τις ετικέτες παραγράφων. Για να **συμπεριλάβετε συνδέσμους** στην έξοδο markdown, πρέπει να ενεργοποιήσετε τις κατάλληλες δυνατότητες.

```python
from aspose.html import MarkdownSaveOptions, MarkdownFeature

# Create save options and enable link and paragraph features
opt = MarkdownSaveOptions()
opt.features = MarkdownFeature.LINK | MarkdownFeature.PARAGRAPH
```

*Εξήγηση:*  
* `MarkdownFeature.LINK` λέει στον μετατροπέα να διατηρεί τις ετικέτες `<a>` ως σύνταξη markdown `[text](url)`.  
* `MarkdownFeature.PARAGRAPH` διατηρεί τα στοιχεία `<p>` ως ξεχωριστές γραμμές, αποτρέποντας τη συγκόλληση προτάσεων.

## Βήμα 3: Μετατροπή του εγγράφου HTML σε αρχείο Markdown

Τώρα καλέστε τη στατική μέθοδο `Converter.convert`, περνώντας το φορτωμένο έγγραφο, τη διαδρομή του αρχείου προορισμού και τις διαμορφωμένες επιλογές.

```python
from aspose.html import Converter

# Perform the conversion and write the markdown file
Converter.convert(doc, "YOUR_DIRECTORY/partial.md", opt)
```

Μετά την εκτέλεση αυτής της γραμμής, το `partial.md` περιέχει μια αναπαράσταση markdown του `sample.html` με όλους τους συνδέσμους αμετάβλητους.

## Πλήρες εκτελέσιμο παράδειγμα

Συνδυάζοντας τα τρία βήματα δημιουργείται ένα σύντομο script που μπορείτε να εκτελέσετε άμεσα:

```python
# convert_html_to_markdown.py
from aspose.html import HTMLDocument, MarkdownSaveOptions, MarkdownFeature, Converter

def convert_html_to_md(source_path: str, target_path: str) -> None:
    """
    Convert an HTML file to Markdown while preserving links and paragraphs.
    """
    # 1️⃣ Load the HTML document
    doc = HTMLDocument(source_path)

    # 2️⃣ Set conversion options (include links and paragraphs)
    opt = MarkdownSaveOptions()
    opt.features = MarkdownFeature.LINK | MarkdownFeature.PARAGRAPH

    # 3️⃣ Execute the conversion
    Converter.convert(doc, target_path, opt)

if __name__ == "__main__":
    # Example usage
    convert_html_to_md(
        source_path="YOUR_DIRECTORY/sample.html",
        target_path="YOUR_DIRECTORY/partial.md"
    )
```

### Αναμενόμενο αποτέλεσμα

Υποθέτοντας ότι το `sample.html` περιέχει:

```html
<p>Visit the <a href="https://example.com">example site</a> for more info.</p>
```

Το παραγόμενο `partial.md` θα μοιάζει με:

```markdown
Visit the [example site](https://example.com) for more info.
```

Παρατηρήστε πώς ο σύνδεσμος μετατράπηκε σωστά και η παράγραφος παραμένει σε ξεχωριστή γραμμή.

## Πώς να μετατρέψετε HTML διαχειριζόμενοι σχετικούς συνδέσμους

Αν το HTML σας χρησιμοποιεί σχετικές URL (π.χ., `<a href="/about">About</a>`), ο μετατροπέας θα τις διατηρήσει όπως είναι. Για να παραγάγετε απόλυτες URL στο markdown, μπορείτε να επεξεργαστείτε το αρχείο μετά τη μετατροπή:

```python
import pathlib

def make_links_absolute(md_path: str, base_url: str) -> None:
    md_file = pathlib.Path(md_path)
    content = md_file.read_text(encoding="utf-8")
    # Replace markdown link patterns with absolute URLs
    updated = re.sub(r'\[([^\]]+)\]\((/[^)]+)\)', fr'[\1]({base_url}\2)', content)
    md_file.write_text(updated, encoding="utf-8")
```

Εκτελέστε `make_links_absolute("YOUR_DIRECTORY/partial.md", "https://example.com")` μετά τη μετατροπή για να διασφαλίσετε ότι όλοι οι σύνδεσμοι δείχνουν στο σωστό domain.

## Αποθήκευση HTML ως Markdown – επιπλέον παραμέτρους

### Εικόνες

Οι εικόνες δεν καλύπτονται από το `MarkdownFeature.LINK`. Αν χρειάζεστε επίσης **να συμπεριλάβετε markdown συνδέσμους** για εικόνες, ενεργοποιήστε τη δυνατότητα `IMAGE`:

```python
opt.features |= MarkdownFeature.IMAGE
```

### Πίνακες και μπλοκ κώδικα

Η προεπιλεγμένη μετατροπή ήδη αντιστοιχίζει τις ετικέτες `<table>` και `<pre>` σε πίνακες markdown και σε μπλοκ κώδικα με φράγκο. Αν θέλετε πιο ακριβή έλεγχο, εξερευνήστε τα `MarkdownFeature.TABLE` και `MarkdownFeature.CODE_BLOCK`.

### Κωδικοποίηση

Βεβαιωθείτε ότι το πηγαίο HTML είναι κωδικοποιημένο σε UTF‑8· διαφορετικά μπορεί να εμφανιστούν ακατάληπτοι χαρακτήρες στο αρχείο markdown. Μπορείτε να εξαναγκάσετε UTF‑8 κατά την ανάγνωση του αρχείου:

```python
doc = HTMLDocument(open(source_path, "r", encoding="utf-8").read())
```

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Σύμπτωμα | Πιθανή αιτία | Διόρθωση |
|---------|--------------|-----|
| Οι σύνδεσμοι εξαφανίζονται | `MarkdownFeature.LINK` not set | Add `opt.features = MarkdownFeature.LINK` |
| Οι παράγραφοι συγχωνεύονται | `MarkdownFeature.PARAGRAPH` missing | Include `| MarkdownFeature.PARAGRAPH` |
| Οι εικόνες εμφανίζονται ως απλό κείμενο | `MarkdownFeature.IMAGE` not enabled | Use `opt.features |= MarkdownFeature.IMAGE` |
| Οι σχετικές URL σπάζουν σε επόμενα εργαλεία | No post‑processing | Run `make_links_absolute` after conversion |

## Δοκιμή της μετατροπής

Μπορείτε γρήγορα να επαληθεύσετε ότι η μετατροπή πέτυχε διαβάζοντας το παραγόμενο αρχείο markdown:

```python
with open("YOUR_DIRECTORY/partial.md", "r", encoding="utf-8") as f:
    print(f.read())
```

Αν η έξοδος περιέχει σύνταξη markdown συνδέσμου (`[text](url)`) και ξεχωριστές παραγράφους, έχετε επιτυχώς **αποθηκεύσει html ως markdown**.

## Συμπέρασμα

Αυτό το tutorial έδειξε πώς να **μετατρέψετε HTML σε Markdown** σε Python ενώ εξειδικεύετε **πώς να συμπεριλάβετε συνδέσμους** και να διατηρήσετε τις διακοπές παραγράφων. Με τη διαμόρφωση του `MarkdownSaveOptions` αποκτάτε λεπτομερή έλεγχο της εξόδου, καθιστώντας εύκολο το **αποθήκευση html ως markdown** για τεκμηρίωση, στατικούς δημιουργούς ιστοσελίδων ή pipelines περιεχομένου.

Επόμενα βήματα που μπορείτε να εξερευνήσετε:

* **Πώς να συμπεριλάβετε markdown συνδέσμους** σε παραγόμενους πίνακες.
* Μετατροπή πολλαπλών αρχείων HTML σε σενάριο batch.
* Ενσωμάτωση της μετατροπής σε διαδικασία δημιουργίας στατικού ιστότοπου (π.χ., με MkDocs ή Jekyll).

Μη διστάσετε να πειραματιστείτε με τις επιλογές, να τις συνδυάσετε με σενάρια post‑processing και να προσαρμόσετε τη ροή εργασίας στις ανάγκες του έργου σας. Καλή δημιουργία markdown!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να χρησιμοποιήσετε το Aspose – Μετατροπή HTML σε Markdown και εξαγωγή συνδέσμων](/html/english/python/general/how-to-use-aspose-convert-html-to-markdown-and-extract-links/)
- [Πώς να εξάγετε συνδέσμους: Μετατροπή HTML σε Markdown με Aspose.Words](/html/english/python/general/how-to-export-links-convert-html-to-markdown-with-aspose-wor/)
- [Μετατροπή HTML σε Markdown με Aspose – Πλήρης οδηγός Python](/html/english/python/general/convert-html-to-markdown-with-aspose-complete-python-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}