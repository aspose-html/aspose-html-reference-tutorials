---
category: general
date: 2026-11-27
description: Δημιουργήστε έγγραφο SVG και αποθηκεύστε το αρχείο SVG χρησιμοποιώντας
  Python. Μάθετε πώς να εξάγετε το διάνυσμα ως SVG και να δημιουργήσετε γρήγορα μια
  εικόνα SVG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG file
- export vector as SVG
- save SVG image
- how to create SVG
language: el
lastmod: 2026-11-27
og_description: Δημιουργήστε έγγραφο SVG και αποθηκεύστε το αρχείο SVG με Python.
  Αυτός ο οδηγός σας δείχνει πώς να εξάγετε το διανυσματικό ως SVG και να δημιουργήσετε
  μια εικόνα SVG σε λίγα λεπτά.
og_image_alt: Screenshot of a red circle saved as an SVG document
og_title: Δημιουργήστε έγγραφο SVG και αποθηκεύστε το αρχείο SVG χρησιμοποιώντας Python
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  headline: Create SVG document and save SVG file with Python
  type: TechArticle
- description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  name: Create SVG document and save SVG file with Python
  steps:
  - name: Expected output
    text: 'The resulting `circle.svg` contains:'
  - name: Exporting more complex vectors
    text: 'If you need to **export vector as SVG** for multi‑shape illustrations,
      simply repeat the `dwg.add()` pattern with other primitives (`rect`, `line`,
      `path`, etc.). For example:'
  - name: Handling Unicode and text
    text: "SVG supports text elements with full Unicode support. Use `dwg.text(\"Hello,
      \U0001F30D\", insert=(5, 95), fill=\"black\")` to embed multilingual labels."
  - name: Saving to a different location
    text: 'When **save SVG image** to a user‑specified folder, validate the path to
      avoid permission errors:'
  - name: Minifying the output
    text: 'For production pipelines, you might want a smaller file size. Pass `pretty=False`
      to `dwg.tostring()` and write the result manually:'
  type: HowTo
tags:
- SVG
- Python
- Vector graphics
title: Δημιουργία εγγράφου SVG και αποθήκευση αρχείου SVG με Python
url: /el/python/general/create-svg-document-and-save-svg-file-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία εγγράφου SVG και αποθήκευση αρχείου SVG με Python

Αν χρειάζεστε να **create SVG document** από το μηδέν, αυτός ο οδηγός σας καθοδηγεί βήμα‑βήμα στη διαδικασία. Θα δείτε πώς να **save SVG file** στο δίσκο, να εξάγετε το διάνυσμα ως SVG, και να καταλήξετε με μια έτοιμη προς χρήση εικόνα SVG με λίγες μόνο γραμμές κώδικα.

Η δημιουργία κλιμακώσιμων γραφικών προγραμματιστικά είναι χρήσιμη για αναφορές, εικονίδια UI ή οποιαδήποτε κατάσταση όπου θέλετε εικόνες ανεξάρτητες από την ανάλυση. Στο τέλος αυτού του tutorial θα μπορείτε να απαντήσετε «**how to create SVG**;» για απλά σχήματα και να επεκτείνετε το μοτίβο σε πιο σύνθετα διανυσματικά έργα.

## Τι θα χρειαστείτε

- Python 3.8 ή νεότερο  
- Το πακέτο `svgwrite` (εγκαθίσταται μέσω `pip`)  
- Ένας φάκελος με δικαιώματα εγγραφής για το αρχείο εξόδου  

Δεν απαιτούνται εξωτερικοί επεξεργαστές γραφικών· όλα εκτελούνται από τη γραμμή εντολών.

## Step 1: Install the `svgwrite` library

`svgwrite` παρέχει ένα καθαρό, Pythonic API για τη δημιουργία SVG markup. Εγκαταστήστε το μία φορά με:

```bash
pip install svgwrite
```

> **Pro tip:** Χρησιμοποιήστε ένα εικονικό περιβάλλον (`python -m venv .venv`) για να διατηρήσετε τις εξαρτήσεις απομονωμένες.

## Step 2: Create SVG document

Τώρα δημιουργούμε πραγματικά **create SVG document** αντικείμενα. Η κλάση `Drawing` αντιπροσωπεύει το ριζικό στοιχείο `<svg>` και διαχειρίζεται αυτόματα τα namespaces.

```python
import pathlib
import svgwrite

# Define where the file will be saved
output_path = pathlib.Path("output/circle.svg")
output_path.parent.mkdir(parents=True, exist_ok=True)

# Initialize a new SVG document with a 100×100 viewport
dwg = svgwrite.Drawing(
    filename=str(output_path),
    size=("100px", "100px"),
    profile="tiny"  # tiny profile keeps the file lightweight
)
```

Το αντικείμενο `Drawing` είναι το σημείο εισόδου για όλες τις επόμενες λειτουργίες SVG. Καθορίζοντας το `size` ορίζουμε τις διαστάσεις του καμβά, κάτι που επηρεάζει το πώς οι φυλλομετρητές θα αποδώσουν την εικόνα.

## Step 3: Add a red circle element

Η προσθήκη σχημάτων είναι απλή. Η μέθοδος `circle` δημιουργεί ένα στοιχείο `<circle>`· στη συνέχεια το συνδέουμε με τη ρίζα.

```python
# Create a red circle with radius 40 centered at (50, 50)
circle = dwg.circle(
    center=(50, 50),
    r=40,
    fill="red"
)

# Append the circle to the SVG root
dwg.add(circle)
```

Γιατί επιλέγουμε κύκλο: οι κύκλοι είναι διανυσματικά primitives που δείχνουν την κλιμακωσιμότητα χωρίς απώλεια ποιότητας, καθιστώντας την έξοδο ιδανική για δοκιμές **export vector as SVG**.

## Step 4: Save SVG file

Τέλος, γράφουμε το markup στο δίσκο. Αυτό το βήμα ικανοποιεί την απαίτηση **save SVG file** και παράγει ένα αρχείο που μπορείτε να ανοίξετε σε οποιονδήποτε φυλλομετρητή ή διανυσματικό επεξεργαστή.

```python
# Persist the SVG document to the filesystem
dwg.save()
print(f"SVG saved to {output_path.resolve()}")
```

Όταν εκτελέσετε το script, θα δείτε ένα μήνυμα στην κονσόλα που επιβεβαιώνει τη θέση του παραγόμενου αρχείου.

### Expected output

Το παραγόμενο `circle.svg` περιέχει:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg height="100px" version="1.1" width="100px" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" fill="red"/>
</svg>
```

Ανοίγοντας το αρχείο σε φυλλομετρητή εμφανίζεται ένας καθαρός κόκκινος κύκλος, και επειδή είναι διανυσματικό, μπορείτε να κάνετε άπειρο ζουμ χωρίς εικονοστοιχεία.

## Step 5: Common variations and edge cases

### Exporting more complex vectors

Αν χρειάζεστε **export vector as SVG** για εικονογραφήσεις με πολλά σχήματα, απλώς επαναλάβετε το μοτίβο `dwg.add()` με άλλα primitives (`rect`, `line`, `path`, κ.λπ.). Για παράδειγμα:

```python
dwg.add(dwg.rect(insert=(10, 10), size=(30, 30), fill="blue"))
dwg.add(dwg.line(start=(0, 0), end=(100, 100), stroke="black", stroke_width=2))
```

### Handling Unicode and text

Το SVG υποστηρίζει στοιχεία κειμένου με πλήρη υποστήριξη Unicode. Χρησιμοποιήστε `dwg.text("Hello, 🌍", insert=(5, 95), fill="black")` για να ενσωματώσετε πολυγλωσσικές ετικέτες.

### Saving to a different location

Όταν **save SVG image** σε φάκελο που καθορίζεται από τον χρήστη, επικυρώστε τη διαδρομή για να αποφύγετε σφάλματα δικαιωμάτων:

```python
if not output_path.parent.exists():
    raise PermissionError(f"Cannot write to {output_path.parent}")
dwg.save()
```

### Minifying the output

Για παραγωγικές αλυσίδες, ίσως θέλετε μικρότερο μέγεθος αρχείου. Περάστε `pretty=False` στο `dwg.tostring()` και γράψτε το αποτέλεσμα χειροκίνητα:

```python
minified = dwg.tostring(pretty=False)
output_path.write_text(minified)
```

## How to create SVG with alternative libraries (optional)

Ενώ το `svgwrite` είναι ελαφρύ και καθαρό‑Python, υπάρχουν και άλλες βιβλιοθήκες:

- **cairosvg** – μετατρέπει PNG, PDF ή HTML σε SVG.  
- **lxml** – σας επιτρέπει να δημιουργήσετε SVG markup χειροκίνητα χρησιμοποιώντας XML APIs.  

Η επιλογή βιβλιοθήκης εξαρτάται από την πολυπλοκότητα του έργου σας και τις υπάρχουσες εξαρτήσεις.

## Conclusion

Τώρα ξέρετε πώς να **create SVG document**, να προσθέσετε διανυσματικά σχήματα και να **save SVG file** χρησιμοποιώντας Python. Η πλήρης λύση δείχνει τα βήματα για **export vector as SVG**, τη δημιουργία μιας **SVG image**, και απαντά στο συχνό ερώτημα **how to create SVG** προγραμματιστικά.

Από εδώ μπορείτε:

- Να επεκτείνετε το script με βρόχους για αυτόματη δημιουργία γραφημάτων ή εικονιδίων.  
- Να ενσωματώσετε το SVG output σε web εφαρμογές ή email templates.  
- Να εξερευνήσετε animation προσθέτοντας στοιχεία `<animate>` με το `svgwrite`.

Πειραματιστείτε με διαφορετικά σχήματα, χρώματα και διαβαθμίσεις για να αξιοποιήσετε πλήρως τη δύναμη των κλιμακώσιμων διανυσματικών γραφικών στα Python projects σας. Καλή κωδικοποίηση!

## What Should You Learn Next?

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Create SVG Document – Add a Circle and Save as SVG](/html/english/python/general/create-svg-document-add-a-circle-and-save-as-svg/)
- [Create SVG Document in Python – Convert SVG to PNG Guide](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)
- [Load SVG File Python – Complete Guide to Export, Embed & Convert](/html/english/python/general/load-svg-file-python-complete-guide-to-export-embed-convert/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}