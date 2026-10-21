---
category: general
date: 2026-05-31
description: Μάθετε πώς να παίρνετε στοιχείο με βάση το id, να αλλάζετε το χρώμα φόντου
  HTML, να διαβάζετε κείμενο HTML και να ορίζετε χαρακτηριστικό HTML χρησιμοποιώντας
  Python. Βήμα‑βήμα οδηγός.
draft: false
keywords:
- get element by id
- change background colour html
- how to read html text
- how to set html attribute
- manipulate html with python
language: el
og_description: Λάβετε στοιχείο με id, διαβάστε το κείμενο HTML, ορίστε το χαρακτηριστικό
  HTML και αλλάξτε το χρώμα φόντου HTML χρησιμοποιώντας Python σε έναν ενιαίο, εύκολο‑να‑ακολουθήσετε
  οδηγό.
og_title: Ανάκτηση στοιχείου με id στην Python – Πλήρης οδηγός επεξεργασίας HTML
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  headline: Get element by id in Python – Complete HTML Manipulation Guide
  type: TechArticle
- description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  name: Get element by id in Python – Complete HTML Manipulation Guide
  steps:
  - name: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
    text: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
  - name: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
    text: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
  - name: '**Retrieves** the element using **get element by id**.'
    text: '**Retrieves** the element using **get element by id**.'
  - name: '**Prints** the element’s text—showing **how to read HTML text**.'
    text: '**Prints** the element’s text—showing **how to read HTML text**.'
  - name: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
    text: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
  - name: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
    text: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
  - name: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
    text: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
  type: HowTo
tags:
- python
- html
- web‑scraping
title: Λήψη στοιχείου με ID στην Python – Πλήρης Οδηγός Διαχείρισης HTML
url: /el/python/general/get-element-by-id-in-python-complete-html-manipulation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ανάκτηση στοιχείου κατά id σε Python – Πλήρης Οδηγός Χειρισμού HTML

Κάποτε χρειάστηκε να **get element by id** από μια σελίδα HTML ενώ γράφατε ένα γρήγορο script σε Python; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν αρχίζουν να σαρώνουν ιστοτόπους ή να τροποποιούν τοπικές αναφορές. Τα καλά νέα; Με λίγες γραμμές κώδικα μπορείτε να διαβάσετε το κείμενο του στοιχείου, να αλλάξετε το χρώμα του φόντου του και ακόμη να ορίσετε νέα attributes, όλα χωρίς να φύγετε από τον επεξεργαστή σας.

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό παράδειγμα: φόρτωση ενός τοπικού `sample.html`, εξαγωγή του στοιχείου του οποίου το ID είναι `main‑content`, εκτύπωση του εσωτερικού του κειμένου και, τέλος, αλλαγή του χρώματος φόντου σε ανοιχτό γκρι. Στο τέλος θα γνωρίζετε επίσης **how to read HTML text**, **how to set HTML attribute**, και γιατί **manipulate HTML with Python** είναι μια χρήσιμη δεξιότητα σε οποιοδήποτε εργαλείο αυτοματοποίησης.

## Τι Θα Χρειαστείτε

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

- **Python 3.9+** (οποιαδήποτε πρόσφατη έκδοση λειτουργεί)
- Τη βιβλιοθήκη **`lxml`** (ή **BeautifulSoup** αν προτιμάτε) – θα χρησιμοποιήσουμε `lxml.html` επειδή παρέχει ένα καθαρό API τύπου `get_element_by_id`.
- Ένα μικρό αρχείο HTML με όνομα `sample.html` σε φάκελο που ονομάζεται `YOUR_DIRECTORY`. Μπορείτε να αντιγράψετε το παρακάτω απόσπασμα σε αυτό το αρχείο:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Demo Page</title>
</head>
<body>
    <div id="main-content">
        Hello, world! This is the original text.
    </div>
</body>
</html>
```

Αυτό είναι όλο—χωρίς περίπλοκα frameworks, μόνο καθαρός Python και ένα στατικό αρχείο HTML.

## Step 1: Install the Required Library

Αν δεν έχετε εγκαταστήσει ακόμη το `lxml`, ανοίξτε ένα τερματικό και τρέξτε:

```bash
pip install lxml
```

*Pro tip:* Η χρήση εικονικού περιβάλλοντος (virtual environment) διατηρεί τον παγκόσμιο Python σας καθαρό, ειδικά όταν αρχίζετε να διαχειρίζεστε πολλαπλά έργα.

## Step 2: Load the HTML Document

Τώρα θα διαβάσουμε το αρχείο σε ένα αντικείμενο `lxml.html` document. Σκεφτείτε το ως μετατροπή του ακατέργαστου κειμένου σε ένα πλοηγήσιμο δέντρο.

```python
from lxml import html
import pathlib

# Resolve the path to the sample file
html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")

# Parse the file into an HTML document
doc = html.parse(str(html_path)).getroot()
print("Document loaded successfully.")
```

Η εκτέλεση αυτού εκτυπώνει “Document loaded successfully.” Αν το αρχείο δεν βρεθεί, η Python θα ρίξει ένα `FileNotFoundError`—καλό να το πιάσετε νωρίς πριν κυνηγήσετε ένα φανταστικό στοιχείο.

## Step 3: Get element by id

Εδώ είναι η ουσία. Το `lxml` μας παρέχει τη βολική μέθοδο `get_element_by_id` που αντικατοπτρίζει το DOM API που θα χρησιμοποιούσατε σε JavaScript.

```python
# Retrieve the element with the specific ID
elem = doc.get_element_by_id("main-content")

if elem is not None:
    print("Element found!")
else:
    print("No element with that ID.")
```

Όταν το στοιχείο υπάρχει, θα δείτε το “Element found!” να εκτυπώνεται στην κονσόλα. Αυτό είναι το **get element by id** βήμα που τροφοδοτεί τις περισσότερες μεταγενέστερες επεμβάσεις μας.

## Step 4: How to read HTML text

Μόλις έχετε το στοιχείο, η εξαγωγή του ορατού κειμένου είναι παιχνιδάκι. Η μέθοδος `text_content()` επιστρέφει όλα τα περιεχόμενα, χωρίς ετικέτες.

```python
if elem is not None:
    # Show the element's current inner text
    inner_text = elem.text_content()
    print("Inner text:", inner_text)
```

Αναμενόμενη έξοδος:

```
Inner text: Hello, world! This is the original text.
```

Μπορεί να αναρωτιέστε, *τι γίνεται αν το στοιχείο περιέχει ένθετες ετικέτες;* Η `text_content()` λειτουργεί ακόμη—συνενώνει όλους τους απογόνους κόμβους κειμένου, δίνοντάς σας μια καθαρή συμβολοσειρά που μπορείτε να καταγράψετε, αποθηκεύσετε ή να δώσετε σε άλλο αλγόριθμο.

## Step 5: How to set HTML attribute

Η αλλαγή ή προσθήκη attributes είναι εξίσου απλή. Η μέθοδος `set` σας επιτρέπει να ορίσετε οποιοδήποτε όνομα attribute θέλετε.

```python
if elem is not None:
    # Set a custom data attribute
    elem.set("data-modified", "true")
    # Verify it was added
    print("New attribute value:", elem.get("data-modified"))
```

Έξοδος:

```
New attribute value: true
```

Αυτή η γραμμή δείχνει **how to set HTML attribute** εν κινήσει. Μπορείτε να αντικαταστήσετε το `"data-modified"` με `"class"`, `"title"` ή οποιοδήποτε άλλο attribute υποστηρίζει το στοιχείο.

## Step 6: Change background colour HTML

Τώρα για την οπτική βελτίωση. Για να αλλάξετε το χρώμα φόντου, εισάγουμε ένα attribute `style` που παρακάμπτει το προεπιλεγμένο.

```python
if elem is not None:
    # Change the background colour via a style attribute
    elem.set("style", "background:#f0f0f0")
    print("Background style applied.")
```

Μετά την εκτέλεση του script, το `div` στο `sample.html` θα φαίνεται έτσι όταν το ανοίξετε σε έναν φυλλομετρητή:

```html
<div id="main-content" data-modified="true" style="background:#f0f0f0">
    Hello, world! This is the original text.
</div>
```

Αυτή είναι η τεχνική **change background colour html** που μπορείτε να επαναχρησιμοποιήσετε για οποιοδήποτε στοιχείο—απλώς αλλάξτε τον κωδικό χρώματος.

## Step 7: Manipulate HTML with Python – Putting It All Together

Παρακάτω είναι το πλήρες, εκτελέσιμο script που συνδυάζει όλα τα βήματα. Αποθηκεύστε το ως `modify_html.py` και εκτελέστε το από τον ίδιο φάκελο με το `YOUR_DIRECTORY`.

```python
#!/usr/bin/env python3
"""
Complete example: load an HTML file, get element by id,
read its text, set a new attribute, and change its background colour.
"""

from lxml import html
import pathlib
import sys

def main():
    # 1️⃣ Load the document
    html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")
    try:
        doc = html.parse(str(html_path)).getroot()
    except OSError as e:
        sys.exit(f"Failed to read HTML file: {e}")

    # 2️⃣ Get element by id
    elem = doc.get_element_by_id("main-content")
    if elem is None:
        sys.exit("Element with ID 'main-content' not found.")

    # 3️⃣ Read HTML text
    print("🗒️  Inner text:", elem.text_content())

    # 4️⃣ Set a new attribute
    elem.set("data-modified", "true")
    print("✅  data-modified attribute set to:", elem.get("data-modified"))

    # 5️⃣ Change background colour HTML
    elem.set("style", "background:#f0f0f0")
    print("🎨  Background colour changed to #f0f0f0")

    # 6️⃣ Write the modified HTML back to disk
    output_path = pathlib.Path("YOUR_DIRECTORY/sample_modified.html")
    output_path.write_text(html.tostring(doc, pretty_print=True, encoding="unicode"))
    print(f"💾  Modified file saved as {output_path}")

if __name__ == "__main__":
    main()
```

### What the script does, line by line

1. **Imports** `lxml.html` για parsing και `pathlib` για διαδρομές ανεξάρτητες από το OS.  
2. **Loads** `sample.html` και τερματίζει με σαφή σφάλμα αν λείπει το αρχείο.  
3. **Retrieves** το στοιχείο χρησιμοποιώντας **get element by id**.  
4. **Prints** το κείμενο του στοιχείου—δείχνοντας **how to read HTML text**.  
5. **Adds** ένα προσαρμοσμένο attribute, εικονογραφώντας **how to set HTML attribute**.  
6. **Changes** το χρώμα φόντου, ικανοποιώντας την απαίτηση **change background colour html**.  
7. **Writes** το ενημερωμένο markup στο `sample_modified.html`, ώστε να το ανοίξετε σε φυλλομετρητή και να δείτε τις αλλαγές.

Η εκτέλεση του script παράγει έξοδο κονσόλας παρόμοια με:

```
🗒️  Inner text: Hello, world! This is the original text.
✅  data-modified attribute set to: true
🎨  Background colour changed to #f0f0f0
💾  Modified file saved as YOUR_DIRECTORY/sample_modified.html
```

Ανοίξτε το `sample_modified.html` και θα παρατηρήσετε το γκρι φόντο πίσω από το κείμενο—απόδειξη ότι **manipulate HTML with python** λειτουργεί πραγματικά.

## Common Pitfalls & How to Avoid Them

- **Missing ID** – Αν το στοιχείο-στόχος δεν υπάρχει, το `get_element_by_id` επιστρέφει `None`. Πάντα ελέγχετε για `None` πριν προσπελάσετε ιδιότητες· διαφορετικά θα αντιμετωπίσετε `AttributeError`.  
- **Encoding issues** – Όταν διαβάζετε σελίδες μη‑ASCII, περάστε `encoding='utf-8'` στο `html.parse` ή βεβαιωθείτε ότι το αρχείο είναι αποθηκευμένο σε UTF‑8.  
- **Overwriting existing styles** – Η ρύθμιση του attribute `style` αντικαθιστά τυχόν προηγούμενα inline styles. Αν χρειάζεται να διατηρήσετε υπάρχοντες κανόνες, διαβάστε πρώτα την τρέχουσα τιμή `style`, προσθέστε τον νέο κανόνα και γράψτε το ξανά.  
- **File permissions** – Η εγγραφή στον ίδιο φάκελο μπορεί να αποτύχει σε συστήματα μόνο για ανάγνωση. Επιλέξτε διαδρομή εξόδου με δικαιώματα εγγραφής, όπως κάναμε με το `sample_modified.html`.

## Extending the Example

Τώρα που έχετε κατακτήσει τα βασικά, σκεφτείτε τα επόμενα βήματα:

- **Loop over multiple IDs** – Χρησιμοποιήστε μια λίστα IDs και επαναλάβετε με ένα `for` loop για μαζική επεξεργασία τμημάτων μιας σελίδας.  
- **Replace text content** – Καλέστε `elem.text = "New text"` για να αλλάξετε το ορατό κείμενο.  
- **Add child elements** – Use `

## What Should You Learn Next?

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}