---
category: general
date: 2026-08-22
description: Πώς να εξάγετε συνδέσμους από HTML και να τους μετατρέψετε σε αρχείο
  markdown, συμπεριλαμβανομένων παραγράφων. Οδηγός βήμα‑προς‑βήμα για τη μετατροπή
  HTML σε markdown.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export links
- convert html to markdown
- how to convert html
- how to extract paragraphs
- html to markdown file
language: el
lastmod: 2026-08-22
og_description: Πώς να εξάγετε συνδέσμους από ένα έγγραφο HTML και να το μετατρέψετε
  σε αρχείο markdown, συμπεριλαμβανομένων των παραγράφων. Ακολουθήστε αυτό το πλήρες
  σεμινάριο για αξιόπιστη μετατροπή από HTML σε markdown.
og_image_alt: How to export links while converting HTML to Markdown
og_title: Πώς να εξάγετε συνδέσμους κατά τη μετατροπή HTML σε Markdown – βήμα‑βήμα
  οδηγός
schemas:
- author: GroupDocs
  dateModified: '2026-08-22'
  description: How to export links from HTML and convert it to a markdown file, including
    paragraphs. Step‑by‑step guide for HTML to markdown conversion.
  headline: How to export links while converting HTML to Markdown
  type: TechArticle
tags:
- HTML conversion
- Markdown
- Python
title: Πώς να εξάγετε συνδέσμους κατά τη μετατροπή HTML σε Markdown
url: /el/python/general/how-to-export-links-while-converting-html-to-markdown/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εξάγετε συνδέσμους κατά τη μετατροπή HTML σε Markdown

Αν χρειάζεστε **how to export links** από μια σελίδα HTML και θέλετε να μετατρέψετε το αποτέλεσμα σε ένα καθαρό **html to markdown file**, αυτός ο οδηγός σας δείχνει τα ακριβή βήματα. Θα ανακαλύψετε επίσης **how to extract paragraphs** ώστε η έξοδος markdown να περιέχει το κύριο περιεχόμενο που σας ενδιαφέρει. Στο τέλος του οδηγού μπορείτε να απαντήσετε στην ερώτηση “**how to convert html** to markdown” με ένα έτοιμο‑για‑εκτέλεση script.

Η εξαγωγή συνδέσμων και η εξαγωγή παραγράφων είναι κοινές εργασίες όταν μεταφέρετε περιεχόμενο ιστού σε στατικές τοποθεσίες, πύλες τεκμηρίωσης ή back‑ends headless CMS. Η παρακάτω προσέγγιση λειτουργεί με το GroupDocs Conversion SDK for Python, αλλά οι έννοιες ισχύουν για οποιαδήποτε βιβλιοθήκη που σας επιτρέπει να διαμορφώσετε τις δυνατότητες εξαγωγής.

---

## Τι θα χρειαστείτε

- Python 3.9 ή νεότερη  
- Πακέτο `groupdocs-conversion` (εγκατάσταση με `pip install groupdocs-conversion`)  
- Ένα αρχείο HTML που θέλετε να επεξεργαστείτε (π.χ., `input.html`)  
- Βασική εξοικείωση με scripting Python  

---

## Πώς να εξάγετε συνδέσμους με τη μετατροπή HTML σε Markdown

Το πρώτο σημαντικό βήμα είναι η διαμόρφωση της μετατροπής ώστε μόνο τα επιθυμητά χαρακτηριστικά—σύνδεσμοι και παράγραφοι—να γραφτούν στο **html to markdown file**. Το SDK σας επιτρέπει να ορίσετε μια bitmask τιμών `MarkdownFeature`; συνδυάζουμε τα `LINKS` και `PARAGRAPHS` για να διατηρήσουμε την έξοδο εστιασμένη.

```python
# Import the required classes from the GroupDocs Conversion SDK
from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeature, Converter

# Step 1: Load the source HTML document
html_doc = HTMLDocument("YOUR_DIRECTORY/input.html")

# Step 2: Create Markdown save options and select the features to export
markdown_options = MarkdownSaveOptions()
# Export only links and paragraphs from the HTML
markdown_options.features = MarkdownFeature.LINKS | MarkdownFeature.PARAGRAPHS

# Step 3: Convert the HTML to Markdown using the configured options
output_path = "YOUR_DIRECTORY/links_and_paragraphs.md"
Converter.convert(html_doc, markdown_options, output_path)

print(f"Conversion complete. Markdown saved to {output_path}")
```

### Γιατί λειτουργεί αυτό

- **`HTMLDocument`** αναλύει το αρχικό αρχείο και δημιουργεί ένα DOM που μπορεί να περιηγηθεί ο μετατροπέας.  
- **`MarkdownSaveOptions`** σας δίνει λεπτομερή έλεγχο πάνω σε ό,τι γράφει το SDK. Ορίζοντας το `features` σε `LINKS | PARAGRAPHS` λέει στη μηχανή να αγνοήσει εικόνες, πίνακες ή scripts, μειώνοντας τον θόρυβο στο τελικό **html to markdown file**.  
- **`Converter.convert`** εκτελεί το βαριά έργο. Σεβεται τη μάσκα χαρακτηριστικών, εξάγει ετικέτες αγκύρωσης (`<a>`) και ετικέτες παραγράφου (`<p>`), και τις γράφει χρησιμοποιώντας τη στάνταρ σύνταξη Markdown.

---

## Πώς να μετατρέψετε HTML σε Markdown με πλήρες περιεχόμενο (προαιρετικό)

Αν αργότερα αποφασίσετε ότι χρειάζεστε ολόκληρη τη σελίδα—όχι μόνο συνδέσμους και παραγράφους—απλώς προσαρμόστε τη μάσκα χαρακτηριστικών:

```python
# Export everything the SDK supports (links, paragraphs, images, tables, etc.)
markdown_options.features = MarkdownFeature.ALL
```

Η εκτέλεση της ίδιας μετατροπής τώρα παράγει ένα πλήρες **html to markdown file** που αντικατοπτρίζει την αρχική διάταξη. Αυτό δείχνει **how to convert html** με ευέλικτο τρόπο: ελέγχετε την έξοδο εναλλάσσοντας τις σημαίες χαρακτηριστικών.

---

## Πώς να εξάγετε μόνο παραγράφους

Μερικές φορές σας ενδιαφέρει μόνο το κείμενο ενός άρθρου, όχι οι υπερσυνδέσεις. Μπορείτε να απομονώσετε τις παραγράφους ορίζοντας τη μάσκα μόνο σε `PARAGRAPHS`:

```python
markdown_options.features = MarkdownFeature.PARAGRAPHS
output_path = "YOUR_DIRECTORY/only_paragraphs.md"
Converter.convert(html_doc, markdown_options, output_path)
```

Το παραγόμενο markdown θα περιέχει καθαρό, περιτυλιγμένο κείμενο χωρίς καμία σήμανση συνδέσμου. Αυτό το απόσπασμα απαντά στην ερώτηση **how to extract paragraphs** από πηγή HTML.

---

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| Κενό αρχείο εξόδου | Το πηγαίο HTML δεν περιέχει ετικέτες `<a>` ή `<p>` που ταιριάζουν με τα επιλεγμένα χαρακτηριστικά. | Επαληθεύστε τη δομή του HTML ή διευρύνετε τη μάσκα χαρακτηριστικών (π.χ., συμπεριλάβετε `HEADINGS`). |
| Προβλήματα κωδικοποίησης | Το HTML χρησιμοποιεί charset που δεν είναι UTF‑8 και το SDK το διαβάζει λανθασμένα. | Περνάτε μια ρητή κωδικοποίηση στο `HTMLDocument`, π.χ., `HTMLDocument(path, encoding="iso-8859-1")`. |
| Αντικατάσταση υπάρχοντος markdown | Η εκτέλεση του script πολλές φορές αντικαθιστά το προηγούμενο αρχείο. | Προσθέστε χρονική σήμανση στο όνομα του αρχείου εξόδου ή ελέγξτε `os.path.exists` πριν τη γραφή. |

**Pro tip:** Όταν επεξεργάζεστε πολλά αρχεία σε έναν φάκελο, τυλίξτε τη λογική μετατροπής σε βρόχο και καταγράψτε κάθε αποτέλεσμα. Αυτό σας παρέχει ένα σαφές audit trail και διευκολύνει την επανεκκίνηση μετά από αποτυχία.

---

## Πλήρες script που μπορείτε να αντιγράψετε‑επικολλήσετε

Παρακάτω υπάρχει ένα αυτόνομο αρχείο Python (`convert_links_paragraphs.py`) που μπορείτε να εκτελέσετε άμεσα. Περιλαμβάνει ανάλυση ορισμάτων ώστε να μπορείτε να καθορίσετε διαδρομές εισόδου και εξόδου χωρίς να επεξεργαστείτε τον κώδικα.

```python
#!/usr/bin/env python3
"""
convert_links_paragraphs.py

A complete example that shows how to export links and extract paragraphs
when converting HTML to a markdown file using GroupDocs Conversion SDK.
"""

import argparse
import os
from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeature, Converter

def convert_html_to_md(input_html: str, output_md: str, features: int) -> None:
    """Perform the conversion with the given feature mask."""
    if not os.path.isfile(input_html):
        raise FileNotFoundError(f"Input file not found: {input_html}")

    # Load the HTML document
    html_doc = HTMLDocument(input_html)

    # Configure markdown options
    md_options = MarkdownSaveOptions()
    md_options.features = features

    # Run the conversion
    Converter.convert(html_doc, md_options, output_md)
    print(f"✅ Conversion finished – markdown saved to: {output_md}")

def main() -> None:
    parser = argparse.ArgumentParser(
        description="How to export links while converting HTML to Markdown."
    )
    parser.add_argument("input", help="Path to the source HTML file.")
    parser.add_argument(
        "output",
        help="Path for the resulting markdown file (e.g., links_and_paragraphs.md).",
    )
    parser.add_argument(
        "--links",
        action="store_true",
        help="Include links in the markdown output.",
    )
    parser.add_argument(
        "--paragraphs",
        action="store_true",
        help="Include paragraphs in the markdown output.",
    )
    args = parser.parse_args()

    # Build the feature mask based on user flags
    selected_features = 0
    if args.links:
        selected_features |= MarkdownFeature.LINKS
    if args.paragraphs:
        selected_features |= MarkdownFeature.PARAGRAPHS

    # Default to both links and paragraphs if no flag is provided
    if selected_features == 0:
        selected_features = MarkdownFeature.LINKS | MarkdownFeature.PARAGRAPHS

    try:
        convert_html_to_md(args.input, args.output, selected_features)
    except Exception as exc:
        print(f"❌ Conversion failed: {exc}")

if __name__ == "__main__":
    main()
```

**Πώς να εκτελέσετε**

```bash
python convert_links_paragraphs.py YOUR_DIRECTORY/input.html YOUR_DIRECTORY/links_and_paragraphs.md --links --paragraphs
```

Η παραπάνω εντολή δείχνει **how to export links** και **how to extract paragraphs** σε μία κλήση. Παραλείψτε το `--links` ή το `--paragraphs` για να προσαρμόσετε την έξοδο στις ανάγκες σας.

---

## Επαλήθευση – πώς φαίνεται η έξοδος

Δεδομένου του παρακάτω απλού HTML (`input.html`):

```html
<!DOCTYPE html>
<html>
<head><title>Sample page</title></head>
<body>
  <p>Welcome to the tutorial.</p>
  <p>Visit <a href="https://example.com">our site</a> for more info.</p>
</body>
</html>
```

Η εκτέλεση του script με και τις δύο σημαίες παράγει το `links_and_paragraphs.md`:

```markdown
Welcome to the tutorial.

Visit [our site](https://example.com) for more info.
```

Βλέπετε ότι μόνο οι δύο παράγραφοι και ο υπερσύνδεσμος είναι παρόντες—ακριβώς αυτό που ζητήσατε όταν ψάχνατε **how to export links** ενώ εκτελούσατε **convert html to markdown**.

---

## Επόμενα βήματα και συναφή θέματα

- **How to convert html to markdown** με εικόνες: προσθέστε `MarkdownFeature.IMAGES` στη μάσκα.  
- **How to extract paragraphs** και έπειτα post‑process  

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Set Offset When Converting HTML to Markdown in Java](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)
- [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)
- [Convert HTML to Markdown – Complete C# Guide](/html/english/java/conversion-html-to-other-formats/convert-html-to-markdown-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}