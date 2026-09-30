---
category: general
date: 2026-08-03
description: Μετατρέψτε HTML σε Markdown χρησιμοποιώντας Python. Μάθετε πώς να εξάγετε
  συνδέσμους από HTML και να εξάγετε παραγράφους από HTML σε μια ενιαία, αποδοτική
  μετατροπή.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- extract paragraphs from html
language: el
lastmod: 2026-08-03
og_description: Μετατρέψτε HTML σε Markdown στην Python με ένα σύντομο παράδειγμα
  που δείχνει πώς να εξάγετε συνδέσμους από HTML και να εξάγετε παραγράφους από HTML
  ενώ αποθηκεύετε το αποτέλεσμα ως αρχείο Markdown.
og_image_alt: Screenshot of Python code converting an HTML file to Markdown with selected
  links and paragraphs
og_title: Μετατροπή HTML σε Markdown με Python – πλήρης οδηγός εξαγωγής
schemas:
- author: GroupDocs
  dateModified: '2026-08-03'
  description: Convert HTML to Markdown using Python. Learn how to extract links from
    HTML and extract paragraphs from HTML in a single, efficient conversion.
  headline: Convert HTML to Markdown Python – extract links & paragraphs
  type: TechArticle
- description: Convert HTML to Markdown using Python. Learn how to extract links from
    HTML and extract paragraphs from HTML in a single, efficient conversion.
  name: Convert HTML to Markdown Python – extract links & paragraphs
  steps:
  - name: Load the HTML document you want to convert
    text: '```python from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions,
      Converter'
  - name: Create a feature set that includes only the elements you need
    text: '```python # Instantiate the feature collection. selected_features = MarkdownSaveOptions.Features()'
  - name: Attach the feature set to the Markdown save options
    text: '```python md_options = MarkdownSaveOptions() md_options.features = selected_features
      ```'
  - name: Perform the conversion and save the result as a Markdown file
    text: '```python output_path = "YOUR_DIRECTORY/links_and_paragraphs.md" Converter.convert_html(html_doc,
      md_options, output_path) print(f"Conversion complete. Markdown saved to {output_path}")
      ```'
  type: HowTo
tags:
- HTML conversion
- Markdown
- Python
title: Μετατροπή HTML σε Markdown Python – εξαγωγή συνδέσμων & παραγράφων
url: /el/python/general/convert-html-to-markdown-python-extract-links-paragraphs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή HTML σε Markdown με Python – εξαγωγή συνδέσμων & παραγράφων

Αν χρειάζεστε **μετατροπή HTML σε Markdown**, αυτό το tutorial σας δείχνει έναν πρακτικό τρόπο να το κάνετε σε Python, εξάγοντας επιλεκτικά **συνδέσμους από HTML** και **παραγράφους από HTML**. Θα δείτε ένα πλήρες, εκτελέσιμο παράδειγμα που αποθηκεύει το φιλτραρισμένο περιεχόμενο ως ένα καθαρό αρχείο Markdown.

Η μετατροπή HTML σε Markdown είναι ένα συνηθισμένο βήμα όταν θέλετε ελαφριά, ελεγχόμενη έκδοση τεκμηρίωσης, περιεχόμενο στατικού ιστότοπου ή απλώς μια αναπαράσταση απλού κειμένου μιας ιστοσελίδας. Στο τέλος αυτού του οδηγού θα έχετε ένα script που:

1. Φορτώνει ένα έγγραφο HTML από το δίσκο.  
2. Διαμορφώνει ένα σύνολο χαρακτηριστικών που διατηρεί μόνο συνδέσμους και στοιχεία παραγράφων.  
3. Εκτελεί τη μετατροπή χρησιμοποιώντας το GroupDocs Conversion SDK for Python.  
4. Γράφει το αποτέλεσμα σε ένα αρχείο `.md`.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

| Απαίτηση | Γιατί είναι σημαντική |
|----------|------------------------|
| Python 3.9+ | Το SDK στοχεύει σε σύγχρονες εκδόσεις του Python. |
| `groupdocs-conversion` package | Παρέχει τις κλάσεις `HTMLDocument`, `MarkdownSaveOptions` και `Converter` που χρησιμοποιούνται στο παράδειγμα. |
| Ένα αρχείο HTML για δοκιμή (π.χ., `sample.html`) | Η πηγή που θα μετατρέψετε. |

Εγκαταστήστε το SDK με pip:

```bash
pip install groupdocs-conversion
```

> **Pro tip:** Χρησιμοποιήστε ένα εικονικό περιβάλλον (`python -m venv .venv`) για να διατηρήσετε τις εξαρτήσεις απομονωμένες.

## Μετατροπή HTML σε Markdown με Python

Ο πυρήνας της μετατροπής βρίσκεται σε μερικά απλά βήματα. Κάθε βήμα εξηγείται παρακάτω, και το πλήρες script εμφανίζεται στο τέλος του άρθρου.

### Βήμα 1: Φορτώστε το έγγραφο HTML που θέλετε να μετατρέψετε

```python
from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, Converter

# Replace YOUR_DIRECTORY with the path that contains your HTML file.
html_path = "YOUR_DIRECTORY/sample.html"
html_doc = HTMLDocument(html_path)
```

*Γιατί αυτό το βήμα;*  
Η `HTMLDocument` αναλύει το αρχείο πηγής και δημιουργεί μια εσωτερική αναπαράσταση DOM που μπορεί να επεξεργαστεί ο μετατροπέας. Χωρίς τη φόρτωση του εγγράφου, το SDK δεν έχει τίποτα για επεξεργασία.

### Βήμα 2: Δημιουργήστε ένα σύνολο χαρακτηριστικών που περιλαμβάνει μόνο τα στοιχεία που χρειάζεστε

```python
# Instantiate the feature collection.
selected_features = MarkdownSaveOptions.Features()

# Keep only hyperlinks.
selected_features.add(MarkdownSaveOptions.Features.LINK)

# Keep only paragraph tags.
selected_features.add(MarkdownSaveOptions.Features.PARAGRAPH)
```

*Γιατί προσθέτουμε αυτά τα χαρακτηριστικά*  
Η `MarkdownSaveOptions.Features` λειτουργεί ως φίλτρο. Προσθέτοντας `LINK` και `PARAGRAPH` λέμε στον μετατροπέα να **εξάγει συνδέσμους από HTML** και **εξάγει παραγράφους από HTML**, αγνοώντας εικόνες, πίνακες, scripts και άλλα στοιχεία που ίσως δεν χρειάζεστε στο τελικό Markdown.

### Βήμα 3: Συνδέστε το σύνολο χαρακτηριστικών με τις επιλογές αποθήκευσης Markdown

```python
md_options = MarkdownSaveOptions()
md_options.features = selected_features
```

*Γιατί αυτό το βήμα;*  
Η `MarkdownSaveOptions` κρατά όλες τις προτιμήσεις μετατροπής. Η ανάθεση του `selected_features` που δημιουργήθηκε προηγουμένως εξασφαλίζει ότι η μετατροπή θα ακολουθήσει τη διαμόρφωση του φίλτρου.

### Βήμα 4: Εκτελέστε τη μετατροπή και αποθηκεύστε το αποτέλεσμα ως αρχείο Markdown

```python
output_path = "YOUR_DIRECTORY/links_and_paragraphs.md"
Converter.convert_html(html_doc, md_options, output_path)
print(f"Conversion complete. Markdown saved to {output_path}")
```

*Γιατί καλούμε το `convert_html`*  
Η `Converter.convert_html` είναι το σημείο εισόδου του SDK για μετατροπές HTML‑σε‑Markdown. Διαβάζει το `HTMLDocument`, εφαρμόζει το `md_options` και γράφει το φιλτραρισμένο αποτέλεσμα στο `output_path`.

#### Αναμενόμενο αποτέλεσμα

Το παραγόμενο `links_and_paragraphs.md` θα περιέχει μόνο τις αναπαραστάσεις Markdown των υπερσυνδέσμων και του κειμένου παραγράφων, για παράδειγμα:

```markdown
[Visit the homepage](https://example.com)

This is the first paragraph of the article, describing the main topic.

Another paragraph with more details.
```

Όλα τα άλλα στοιχεία HTML όπως `<img>`, `<table>` ή `<script>` παραλείπονται, κρατώντας το αρχείο ελαφρύ και εύκολο στην επεξεργασία.

## Εξαγωγή συνδέσμων από HTML (προαιρετική πιο βαθιά ανάλυση)

Αν ο στόχος σας είναι **μόνο η εξαγωγή συνδέσμων από HTML** ενώ απορρίπτετε τα υπόλοιπα, μπορείτε να απλοποιήσετε το σύνολο χαρακτηριστικών:

```python
link_only_features = MarkdownSaveOptions.Features()
link_only_features.add(MarkdownSaveOptions.Features.LINK)

md_options.features = link_only_features
```

Η εκτέλεση της μετατροπής με αυτή τη διαμόρφωση παράγει ένα αρχείο Markdown όπου κάθε σύνδεσμος εμφανίζεται σε ξεχωριστή γραμμή, π.χ.:

```markdown


## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική?

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}