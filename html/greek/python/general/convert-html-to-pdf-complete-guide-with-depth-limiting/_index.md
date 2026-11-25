---
category: general
date: 2026-05-25
description: Μετατρέψτε γρήγορα HTML σε PDF και μάθετε πώς να περιορίζετε το βάθος
  κατά την αποθήκευση μιας ιστοσελίδας ως PDF χρησιμοποιώντας Python. Περιλαμβάνει
  κώδικα βήμα‑προς‑βήμα.
draft: false
keywords:
- convert html to pdf
- save webpage as pdf
- download html as pdf
- how to limit depth
- set depth limit
language: el
og_description: Μετατρέψτε HTML σε PDF και μάθετε πώς να ορίσετε όριο βάθους κατά
  την αποθήκευση μιας ιστοσελίδας ως PDF. Πλήρες παράδειγμα Python και βέλτιστες πρακτικές.
og_title: Μετατροπή HTML σε PDF – Βήμα‑βήμα με Έλεγχο Βάθους
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Convert HTML to PDF quickly and learn how to limit depth when saving
    a webpage as PDF using Python. Includes step‑by‑step code.
  headline: Convert HTML to PDF – Complete Guide with Depth Limiting
  type: TechArticle
- description: Convert HTML to PDF quickly and learn how to limit depth when saving
    a webpage as PDF using Python. Includes step‑by‑step code.
  name: Convert HTML to PDF – Complete Guide with Depth Limiting
  steps:
  - name: '## Convert HTML to PDF with Depth Control'
    text: The core of the solution lives in four concise steps. Let’s break each one
      down, explain **why** it’s needed, and show the exact code you’ll paste into
      `convert_html_to_pdf.py`.
  - name: '## Save Webpage as PDF – Verifying the Result'
    text: After the script finishes, check `YOUR_DIRECTORY/output.pdf`. You should
      see the page rendered correctly, with images and styles that fell within the
      five‑level depth you set. If the PDF looks missing a stylesheet or an image,
      increase `max_handling_depth` by one and re‑run.
  - name: '### When to Adjust the Depth Limit'
    text: '| Situation | Recommended `max_handling_depth` | |-----------|-----------------------------------|
      | Simple blog post with a few images | 2–3 | | Complex web app with nested iframes
      | 6–8 | | Documentation site that uses CSS imports | 4–5 | | Unknown third‑party
      site | Start low (2) and increase gra'
  - name: '### Handling Authentication‑Protected Pages'
    text: 'If the target page requires a login, you’ll need to fetch the HTML yourself
      (using `requests` with a session) and feed the raw string to `HTMLDocument`:'
  - name: '### Setting a Custom Base URL'
    text: 'When you pass raw HTML, you may need to tell the converter where to resolve
      relative links:'
  - name: '### Common Pitfalls'
    text: '- **Forgot to attach `resource_options`** – the converter silently ignores
      your depth setting. - **Using an invalid output folder** – you’ll get a `PermissionError`.
      Make sure the directory exists and is writable. - **Mixing HTTP and HTTPS resources**
      – some converters block insecure content by defa'
  type: HowTo
tags:
- Python
- PDF conversion
- Web scraping
title: Μετατροπή HTML σε PDF – Πλήρης Οδηγός με Περιορισμό Βάθους
url: /el/python/general/convert-html-to-pdf-complete-guide-with-depth-limiting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή HTML σε PDF – Πλήρης Οδηγός με Περιορισμό Βάθους

Έχετε ποτέ χρειαστεί να **μετατρέψετε HTML σε PDF** αλλά ανησυχείτε για το ότι άπειροι συνδεδεμένοι πόροι θα αυξήσουν το μέγεθος του αρχείου σας; Δεν είστε μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν προσπαθούν να **αποθηκεύσουν μια ιστοσελίδα ως PDF** και ξαφνικά καταλήγουν με ένα τεράστιο έγγραφο γεμάτο εξωτερικά CSS, JavaScript και εικόνες που δεν έπρεπε καν να είναι εκεί.

Το θέμα είναι: μπορείτε να ελέγξετε ακριβώς πόσο βαθιά θα σαρώνει η μηχανή μετατροπής ορίζοντας ένα όριο βάθους. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα καθαρό, εκτελέσιμο παράδειγμα Python που δείχνει πώς να **κατεβάσετε HTML ως PDF** ενώ **περιορίζετε το βάθος** για να διατηρείτε τα πράγματα τακτικά. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση script, θα καταλάβετε γιατί το βάθος είναι σημαντικό και θα γνωρίζετε μερικές επαγγελματικές συμβουλές για να αποφύγετε κοινά προβλήματα.

---

## Τι Θα Χρειαστείτε

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε:

| Προαπαιτούμενο | Γιατί είναι σημαντικό |
|----------------|------------------------|
| Python 3.9 ή νεότερο | Η βιβλιοθήκη μετατροπής που θα χρησιμοποιήσουμε υποστηρίζει μόνο πρόσφατες εκδόσεις. |
| `aspose-pdf` package (or any similar API) | Παρέχει `HTMLDocument`, `ResourceHandlingOptions`, `SaveOptions` και `Converter`. |
| Πρόσβαση στο διαδίκτυο (για λήψη της πηγής) | Το script λαμβάνει το ζωντανό HTML από ένα URL. |
| Δικαίωμα εγγραφής σε φάκελο εξόδου | Το PDF θα γραφτεί στο `YOUR_DIRECTORY`. |

Η εγκατάσταση είναι μια μόνο γραμμή:

```bash
pip install aspose-pdf
```

*(Αν προτιμάτε διαφορετική βιβλιοθήκη, οι έννοιες παραμένουν ίδιες – απλώς αντικαταστήστε τα ονόματα κλάσεων.)*

---

## Υλοποίηση Βήμα‑βήμα

### ## Μετατροπή HTML σε PDF με Έλεγχο Βάθους

Ο πυρήνας της λύσης βρίσκεται σε τέσσερα σύντομα βήματα. Ας τα αναλύσουμε, εξηγήσουμε **γιατί** είναι απαραίτητα και δείξουμε τον ακριβή κώδικα που θα επικολλήσετε στο `convert_html_to_pdf.py`.

#### 1️⃣ Φόρτωση του HTML Document

Ξεκινάμε δημιουργώντας ένα αντικείμενο `HTMLDocument` που δείχνει στη σελίδα που θέλετε να μετατρέψετε. Σκεφτείτε το σαν να δίνετε στον μετατροπέα έναν φρέσκο καμβά που περιέχει ήδη το markup.

```python
from aspose.pdf import HTMLDocument

# Step 1: Load the HTML document you want to convert
doc = HTMLDocument("https://example.com/very-large-page.html")
```

*Γιατί αυτό είναι σημαντικό*: Χωρίς τη φόρτωση της πηγής, ο μετατροπέας δεν έχει τίποτα να επεξεργαστεί. Το URL μπορεί να είναι οποιαδήποτε δημόσια σελίδα ή τοπική διαδρομή αρχείου αν έχετε ήδη αποθηκεύσει το HTML.

#### 2️⃣ Ορισμός του Ορίου Βάθους

Το βάθος καθορίζει πόσα «επίπεδα» συνδεδεμένων πόρων (CSS, εικόνες, iframes κ.λπ.) θα ακολουθήσει η μηχανή. Ορίζοντας `max_handling_depth = 5` σημαίνει ότι ο μετατροπέας θα κυνηγάει συνδέσμους μέχρι πέντε άλματα, μετά θα σταματήσει. Αυτό αποτρέπει ανεξέλεγκτες λήψεις.

```python
from aspose.pdf import ResourceHandlingOptions

# Step 2: Define how deep the engine should follow linked resources
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 5   # stop after 5 levels of links
```

*Γιατί αυτό είναι σημαντικό*: Μεγάλες ιστοσελίδες συχνά ενσωματώνουν πόρους μέσα σε άλλους πόρους (π.χ., ένα CSS που εισάγει άλλο CSS). Χωρίς όριο, μπορεί να καταλήξετε να κατεβάζετε ολόκληρο το διαδίκτυο.

#### 3️⃣ Σύνδεση των Επιλογών με τη Διαμόρφωση Αποθήκευσης

`SaveOptions` συγκεντρώνει όλες τις προτιμήσεις μετατροπής, συμπεριλαμβανομένων των ρυθμίσεων βάθους που μόλις δημιουργήσαμε. Είναι σαν μια κάρτα συνταγής που λέει στον μετατροπέα ακριβώς πώς θέλετε να «ψήνετε» το PDF.

```python
from aspose.pdf import SaveOptions

# Step 3: Attach the resource handling options to the save configuration
save_options = SaveOptions()
save_options.resource_handling_options = resource_options
```

*Γιατί αυτό είναι σημαντικό*: Αν παραλείψετε αυτό το βήμα, ο μετατροπέας θα επιστρέψει στις προεπιλεγμένες ρυθμίσεις βάθους (συνήθως απεριόριστο), καταστρέφοντας τον σκοπό του **πώς να περιορίσετε το βάθος**.

#### 4️⃣ Εκτέλεση της Μετατροπής

Τέλος, καλούμε το `Converter.convert`, περνώντας το έγγραφο, τη διαδρομή εξόδου και τις `save_options`. Η μηχανή σέβεται το όριο βάθους και γράφει ένα καθαρό PDF.

```python
from aspose.pdf import Converter

# Step 4: Convert the document to PDF while respecting the depth limit
Converter.convert(doc, "YOUR_DIRECTORY/output.pdf", save_options)
```

*Γιατί αυτό είναι σημαντικό*: Αυτή η μοναδική γραμμή κάνει το σκληρό έργο – αναλύει το HTML, φέρνει τους επιτρεπόμενους πόρους και αποδίδει τα πάντα σε ένα αρχείο PDF.

---

### ## Αποθήκευση Ιστοσελίδας ως PDF – Επαλήθευση του Αποτελέσματος

Αφού το script ολοκληρωθεί, ελέγξτε το `YOUR_DIRECTORY/output.pdf`. Θα πρέπει να δείτε τη σελίδα σωστά αποδομένη, με εικόνες και στυλ που εμπίπτουν στο πέντε‑επίπεδο βάθος που ορίσατε. Αν το PDF λείπει κάποιο stylesheet ή εικόνα, αυξήστε το `max_handling_depth` κατά ένα και ξανατρέξτε.

**Pro tip:** Ανοίξτε το PDF σε προβολέα που μπορεί να εμφανίσει layers (π.χ., Adobe Acrobat) για να δείτε αν κρυφά στοιχεία έχουν αφαιρεθεί. Αυτό σας βοηθά να ρυθμίσετε ακριβώς το βάθος χωρίς υπερβολική λήψη.

---

## Προχωρημένα Θέματα & Ακραίες Περιπτώσεις

### ### Πότε να Προσαρμόσετε το Όριο Βάθους

| Κατάσταση | Συνιστώμενο `max_handling_depth` |
|-----------|-----------------------------------|
| Απλό blog post με λίγες εικόνες | 2–3 |
| Πολύπλοκη web εφαρμογή με ενσωματωμένα iframes | 6–8 |
| Ιστοσελίδα τεκμηρίωσης που χρησιμοποιεί εισαγωγές CSS | 4–5 |
| Αγνώστου τρίτου site | Ξεκινήστε χαμηλά (2) και αυξήστε σταδιακά |

Ο ορισμός του ορίου πολύ χαμηλά μπορεί να κόψει κρίσιμο CSS, αφήνοντας το PDF απλό. Πολύ υψηλό, και σπαταλάτε εύρος ζώνης και μνήμη.

### ### Διαχείριση Σελίδων με Προστασία Επαλήθευσης

Αν η στόχευση σελίδα απαιτεί σύνδεση, θα πρέπει να κατεβάσετε το HTML μόνοι σας (χρησιμοποιώντας `requests` με session) και να το περάσετε ως ακατέργαστη συμβολοσειρά στο `HTMLDocument`:

```python
import requests
from aspose.pdf import HTMLDocument

session = requests.Session()
session.post("https://example.com/login", data={"user":"me","pass":"secret"})
html = session.get("https://example.com/secure-page.html").text

doc = HTMLDocument(html)  # Pass raw HTML instead of a URL
```

Τώρα η λογική του ορίου βάθους εξακολουθεί να ισχύει επειδή ο μετατροπέας θα επιλύσει τους σχετικούς συνδέσμους βάσει του base URL που παρέχετε.

### ### Ορισμός Προσαρμοσμένου Base URL

Όταν περνάτε ακατέργαστο HTML, ίσως χρειαστεί να πείτε στον μετατροπέα πού να επιλύει τους σχετικούς συνδέσμους:

```python
doc.base_url = "https://example.com/"
```

Αυτή η μικρή γραμμή εξασφαλίζει ότι το όριο βάθους λειτουργεί σωστά για πόρους όπως `/assets/style.css`.

### ### Συνηθισμένα Πίπτα

- **Ξεχάσατε να συνδέσετε το `resource_options`** – ο μετατροπέας αγνοεί σιωπηλά τη ρύθμιση του βάθους.  
- **Χρήση μη έγκυρου φακέλου εξόδου** – θα λάβετε `PermissionError`. Βεβαιωθείτε ότι ο φάκελος υπάρχει και είναι εγγράψιμος.  
- **Ανάμειξη πόρων HTTP και HTTPS** – ορισμένοι μετατροπείς αποκλείουν το μη ασφαλές περιεχόμενο από προεπιλογή· ενεργοποιήστε τη διαχείριση mixed‑content αν χρειάζεται.  

---

## Πλήρες Λειτουργικό Script

Παρακάτω είναι το πλήρες, έτοιμο‑για‑αντιγραφή script που ενσωματώνει όλες τις παραπάνω συμβουλές. Αποθηκεύστε το ως `convert_html_to_pdf.py` και τρέξτε το με `python convert_html_to_pdf.py`.

```python
# convert_html_to_pdf.py
# Complete example: convert HTML to PDF while setting a depth limit

import os
from aspose.pdf import HTMLDocument, ResourceHandlingOptions, SaveOptions, Converter

# ----------------------------------------------------------------------
# Configuration section – adjust these values for your environment
# ----------------------------------------------------------------------
SOURCE_URL = "https://example.com/very-large-page.html"
OUTPUT_DIR = "YOUR_DIRECTORY"
OUTPUT_FILE = os.path.join(OUTPUT_DIR, "output.pdf")
MAX_DEPTH = 5                     # set depth limit (how to limit depth)

# Ensure the output directory exists
os.makedirs(OUTPUT_DIR, exist_ok=True)

# ----------------------------------------------------------------------
# Step 1: Load the HTML document
# ----------------------------------------------------------------------
doc = HTMLDocument(SOURCE_URL)

# ----------------------------------------------------------------------
# Step 2: Define depth handling options
# ----------------------------------------------------------------------
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = MAX_DEPTH  # set depth limit

# ----------------------------------------------------------------------
# Step 3: Attach options to save configuration
# ----------------------------------------------------------------------
save_options = SaveOptions()
save_options.resource_handling_options = resource_options

# ----------------------------------------------------------------------
# Step 4: Perform the conversion
# ----------------------------------------------------------------------
Converter.convert(doc, OUTPUT_FILE, save_options)

print(f"✅ Conversion complete! PDF saved to: {OUTPUT_FILE}")
```

**Αναμενόμενη έξοδος** όταν εκτελείτε το script:

```
✅ Conversion complete! PDF saved to: YOUR_DIRECTORY/output.pdf
```

Ανοίξτε το παραγόμενο PDF – θα πρέπει να δείτε τη σελίδα αποδομένη με όλους τους πόρους που εμπίπτουν στο πέντε‑επίπεδο βάθος που ορίσατε.

---

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για να **μετατρέψετε HTML σε PDF** ενώ **ορίζετε όριο βάθους**. Από την εγκατάσταση της βιβλιοθήκης, τη διαμόρφωση του `ResourceHandlingOptions`, μέχρι τη διαχείριση επαλήθευσης και προσαρμοσμένων base URLs, το tutorial σας παρέχει μια σταθερή, παραγωγική βάση.

Θυμηθείτε:

- Χρησιμοποιήστε το `max_handling_depth` για **πώς να περιορίσετε το βάθος** και να διατηρήσετε τα PDF ελαφριά.  
- Προσαρμόστε το βάθος ανάλογα με την πολυπλοκότητα της πηγής.  
- Δοκιμάστε το αποτέλεσμα, μετά ρυθμίστε μέχρι να βρείτε την ιδανική ισορροπία μεταξύ πιστότητας και μεγέθους αρχείου.  

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε **να αποθηκεύσετε ένα πολυ‑σελίδες άρθρο ως PDF**, πειραματιστείτε με τιμές `set depth limit`, ή εξερευνήστε την προσθήκη κεφαλίδων/υποσέλιδων με αντικείμενα `PdfPage`. Ο κόσμος της **download html as pdf** αυτοματοποίησης είναι τεράστιος, και τώρα έχετε τα σωστά εργαλεία για να τον περιηγηθείτε.

Αν αντιμετωπίσετε δυσκολίες, αφήστε ένα σχόλιο παρακάτω – θα χαρώ να βοηθήσω. Καλό coding και απολαύστε τα καθαρά PDF!

## Σχετικά Μαθήματα

- [Μετατροπή HTML σε PDF με Aspose.HTML – Πλήρης Οδηγός Χειρισμού](/html/english/)
- [Πώς να Μετατρέψετε HTML σε PDF Java – Χρησιμοποιώντας Aspose.HTML για Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Μετατροπή HTML σε PDF σε .NET με Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}