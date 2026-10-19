---
category: general
date: 2026-05-31
description: Μάθετε πώς να κατεβάζετε εικονίδια με την Python. Θα καλύψουμε επίσης
  πώς να εξάγετε το favicon, να διαβάζετε έγγραφο HTML με Python και να γράφετε δυαδικό
  αρχείο με Python σε ένα ενιαίο σεμινάριο.
draft: false
keywords:
- how to download icons
- how to extract favicon
- write binary file python
- read html document python
- load html python
language: el
og_description: Πώς να κατεβάσετε εικονίδια χρησιμοποιώντας Python, εξηγημένο βήμα‑βήμα.
  Μάθετε να εξάγετε το favicon, να διαβάζετε έγγραφο HTML με Python και να γράφετε
  δυαδικό αρχείο με Python.
og_title: Πώς να κατεβάσετε εικονίδια με Python – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to download icons using Python. We'll also cover how to extract
    favicon, read HTML document Python, and write binary file python in a single tutorial.
  headline: How to Download Icons with Python – Complete Guide
  type: TechArticle
tags:
- python
- web-scraping
- favicon
- file-io
title: Πώς να κατεβάσετε εικονίδια με Python – Πλήρης οδηγός
url: /el/python/general/how-to-download-icons-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Κατεβάσετε Εικονίδια με Python – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να κατεβάσετε εικονίδια** από έναν ιστότοπο χωρίς να κάνετε δεξί κλικ σε κάθε ένα; Δεν είστε ο μόνος. Είτε δημιουργείτε ένα εργαλείο ελέγχου μάρκας είτε απλώς θέλετε ένα τοπικό αντίγραφο κάθε favicon που συναντάτε, η εξοικείωση με αυτήν την εργασία σας εξοικονομεί χρόνο και πληκτρολογήσεις.

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα από το **πώς να κατεβάσετε εικονίδια** από ένα αρχείο HTML χρησιμοποιώντας απλό Python. Θα σας δείξουμε επίσης **πώς να εξάγετε favicon**, θα επιδείξουμε **read html document python**, και θα εξηγήσουμε **write binary file python** ώστε να καταλήξετε με έναν τακτοποιημένο φάκελο .ico αρχείων έτοιμο για οποιοδήποτε έργο.

---

## What You’ll Need

- Python 3.8+ (η τυπική βιβλιοθήκη είναι επαρκής)
- Τοπικό αντίγραφο της σελίδας HTML που θέλετε να σαρώσετε (ή ένα URL που μπορείτε να φέρετε)
- Βασική εξοικείωση με το file I/O στο Python  
- Δεν απαιτούνται εξωτερικά πακέτα, αλλά το `beautifulsoup4` μπορεί να κάνει τα πράγματα πιο ομαλά αν το προτιμάτε (προαιρετικό)

Τα έχετε; Τέλεια—ας βουτήξουμε.

![Παράδειγμα λήψης εικονιδίων](https://example.com/placeholder.png "παράδειγμα λήψης εικονιδίων")

---

## Step 1: Load the HTML Document in Python  

Πρώτα απ' όλα, πρέπει να **load html python** με τρόπο—να διαβάσουμε το αρχείο στη μνήμη ώστε να μπορούμε να εξετάσουμε τις ετικέτες `<link>` του. Ο πιο απλός τρόπος είναι να ανοίξετε το αρχείο με τη ενσωματωμένη συνάρτηση `open` και να το διαβάσετε ως κείμενο.

```python
# Step 1: Load the HTML document
HTML_PATH = "YOUR_DIRECTORY/sample.html"

# Using the built‑in open() to read the file as a string
with open(HTML_PATH, "r", encoding="utf-8") as f:
    html_content = f.read()
```

*Γιατί αυτό το βήμα;*  
Η ανάγνωση του HTML μας δίνει μια ακατέργαστη συμβολοσειρά που μπορούμε να αναλύσουμε. Αν παραλείψετε αυτό και προσπαθήσετε να εργαστείτε απευθείας με μια διαδρομή, ο parser δεν θα έχει τίποτα να εξετάσει.

---

## Step 2: Parse the Document and Find Icon Links  

Τώρα χρειάζεται να **read html document python** με τρόπο. Αν και θα μπορούσατε να χρησιμοποιήσετε regex, ένας μικρός HTML parser κρατά τα πράγματα αξιόπιστα. Το Python περιλαμβάνει το `html.parser` το οποίο μπορούμε να κληρονομήσουμε για τον σκοπό μας.

```python
from html.parser import HTMLParser

class IconLinkParser(HTMLParser):
    """Collects href attributes from <link rel='icon'> tags."""
    def __init__(self):
        super().__init__()
        self.icon_hrefs = []

    def handle_starttag(self, tag, attrs):
        if tag.lower() != "link":
            return
        attrs_dict = dict(attrs)
        # Look for rel="icon" (or rel="shortcut icon")
        rel = attrs_dict.get("rel", "").lower()
        if "icon" in rel:
            href = attrs_dict.get("href")
            if href:
                self.icon_hrefs.append(href)

# Instantiate and feed the HTML content
parser = IconLinkParser()
parser.feed(html_content)

# Now we have a list of all icon URLs
icon_hrefs = parser.icon_hrefs
print(f"Found {len(icon_hrefs)} icon link(s):", icon_hrefs)
```

**Εξήγηση**  
- `handle_starttag` ενεργοποιείται για κάθε ετικέτα έναρξης.  
- Φιλτράρουμε για στοιχεία `<link>` των οποίων το χαρακτηριστικό `rel` περιέχει τη λέξη *icon*. Αυτό καλύπτει τόσο το `rel="icon"` όσο και το παλαιότερο `rel="shortcut icon"`.  
- Οι τιμές `href` αποθηκεύονται στο `icon_hrefs`, έτοιμες για το επόμενο βήμα.

---

## Step 3: Resolve Relative Paths (Optional but Helpful)

Αν το HTML χρησιμοποιεί σχετικές URL, πρέπει να τις μετατρέψουμε σε απόλυτες διαδρομές συστήματος αρχείων. Εδώ η γνώση **load html python** συναντά το `urllib.parse`.

```python
import os
from urllib.parse import urljoin

# Base directory where the HTML file lives
BASE_DIR = os.path.dirname(os.path.abspath(HTML_PATH))

def resolve_path(href):
    # If href already looks like an absolute path, return it unchanged
    if os.path.isabs(href):
        return href
    # Otherwise, join it with the base directory
    return os.path.normpath(os.path.join(BASE_DIR, href))

resolved_icon_paths = [resolve_path(h) for h in icon_hrefs]
print("Resolved paths:", resolved_icon_paths)
```

*Γιατί να ασχοληθούμε;*  
Όταν αργότερα **write binary file python**, χρειάζεστε μια πραγματική διαδρομή αρχείου. Σχετικές URL όπως `images/favicon.ico` διαφορετικά θα προκαλούσαν `FileNotFoundError`.

---

## Step 4: Write Each Icon to a Local Binary File  

Αυτή είναι η ουσία του **how to download icons**. Θα επαναλάβουμε τις επιλυμένες διαδρομές, θα διαβάσουμε κάθε εικονίδιο ως δυαδικά δεδομένα και θα το γράψουμε σε ένα νέο αρχείο σε έναν αφιερωμένο φάκελο `icons/`.

```python
import shutil

OUTPUT_DIR = "YOUR_DIRECTORY/icons"
os.makedirs(OUTPUT_DIR, exist_ok=True)

for index, icon_path in enumerate(resolved_icon_paths):
    # Guard against missing files
    if not os.path.isfile(icon_path):
        print(f"⚠️  Icon file not found: {icon_path}")
        continue

    # Destination filename: icon_0.ico, icon_1.ico, …
    dest_path = os.path.join(OUTPUT_DIR, f"icon_{index}.ico")

    # **write binary file python** – copy the binary data
    with open(icon_path, "rb") as src_file, open(dest_path, "wb") as dst_file:
        shutil.copyfileobj(src_file, dst_file)

    print(f"✅ Saved {dest_path}")
```

**Τι συμβαίνει;**  

- `os.makedirs(..., exist_ok=True)` διασφαλίζει ότι ο φάκελος εξόδου υπάρχει.  
- `shutil.copyfileobj` μεταφέρει τα byte από την πηγή στον προορισμό, που είναι ο πιο αποδοτικός σε μνήμη τρόπο για **write binary file python**.  
- Ονομάζουμε κάθε αρχείο `icon_<index>.ico` για να αποφύγουμε συγκρούσεις.

**Αναμενόμενο αποτέλεσμα**

```
Found 2 icon link(s): ['images/favicon.ico', 'icons/custom.ico']
Resolved paths: ['/path/to/YOUR_DIRECTORY/images/favicon.ico',
                '/path/to/YOUR_DIRECTORY/icons/custom.ico']
✅ Saved YOUR_DIRECTORY/icons/icon_0.ico
✅ Saved YOUR_DIRECTORY/icons/icon_1.ico
```

Μετά το τέλος του script, θα έχετε μια καθαρή συλλογή αρχείων εικονιδίων έτοιμη για οποιαδήποτε επόμενη εργασία.

---

## Step 5: Bonus – Download Icons Directly from a Remote URL  

Αν το HTML σας βρίσκεται στο διαδίκτυο αντί για το τοπικό δίσκο, αντικαταστήστε το τμήμα ανάγνωσης αρχείου με μια μικρή κλήση `requests`. Αυτό δείχνει **how to extract favicon** από οποιαδήποτε ζωντανή σελίδα.

```python
import requests

REMOTE_URL = "https://example.com"

# Grab the HTML
response = requests.get(REMOTE_URL)
response.raise_for_status()
html_content = response.text

# Re‑run the parser (same as before) to get icon URLs
parser = IconLinkParser()
parser.feed(html_content)
icon_hrefs = parser.icon_hrefs

# Download each icon via HTTP
for index, href in enumerate(icon_hrefs):
    # Resolve relative URLs against the page URL
    icon_url = urljoin(REMOTE_URL, href)
    r = requests.get(icon_url, stream=True)
    r.raise_for_status()
    dest_path = os.path.join(OUTPUT_DIR, f"remote_icon_{index}.ico")
    with open(dest_path, "wb") as out_file:
        shutil.copyfileobj(r.raw, out_file)
    print(f"✅ Downloaded {icon_url} → {dest_path}")
```

**Γιατί να το προσθέσουμε;**  
Πολλά πραγματικά έργα χρειάζονται να εξάγουν favicons από ζωντανές τοποθεσίες. Αυτό το απόσπασμα δείχνει ότι μπορείτε να επεκτείνετε την ίδια λογική **how to download icons** στο διαδίκτυο με μόνο μερικές επιπλέον γραμμές.

---

## Common Pitfalls & Pro Tips

- **Missing `rel="icon"`** – Κάποιοι ιστότοποι ενσωματώνουν εικονίδια μέσω ετικετών `<meta>` ή CSS. Αν τα χρειάζεστε, επεκτείνετε τον parser ώστε να ψάχνει για `<meta name="msapplication‑TileImage">` ή URLs CSS `background-image`.
- **Non‑ICO formats** – Τα σύγχρονα favicons συχνά χρησιμοποιούν `.png` ή `.svg`. Ο παραπάνω κώδικας λειτουργεί για οποιαδήποτε δυαδική εικόνα· απλώς προσαρμόστε την επέκταση αρχείου στο `dest_path` αν θέλετε να διατηρήσετε την αρχική μορφή.
- **Permission errors** – Κατά τη γραφή αρχείων, βεβαιωθείτε ότι το script εκτελείται με δικαιώματα εγγραφής στο φάκελο προορισμού. Η χρήση του `os.makedirs(..., exist_ok=True)` αποτρέπει σφάλματα “directory not found”.
- **Large HTML files** – Για τεράστιες σελίδες, σκεφτείτε να διαβάζετε το αρχείο γραμμή‑με‑γραμμή αντί να φορτώνετε ολόκληρη τη συμβολοσειρά στη μνήμη. Ο ενσωματωμένος `HTMLParser` μπορεί να χειριστεί σταδιακές τροφοδοσίες.

---

## Συμπέρασμα

Μόλις μάθατε **how to download icons** από ένα έγγραφο HTML χρησιμοποιώντας καθαρό Python. Με το **reading html document python**, την ανάλυση των ετικετών `<link rel="icon">`, την επίλυση τυχόν σχετικών διαδρομών, και τελικά το **write binary file python** για αποθήκευση κάθε εικονιδίου τοπικά, έχετε τώρα ένα επαναχρησιμοποιήσιμο script που λειτουργεί τόσο για τοπικές όσο και για απομακρυσμένες σελίδες.

Επόμενα βήματα; Δοκιμάστε να επεκτείνετε τον parser ώστε να εντοπίζει Apple touch icons (`rel="apple-touch-icon"`), ή ενσωματώστε το script σε μια μεγαλύτερη αλυσίδα web‑crawling που συλλέγει favicons για εκατοντάδες τομείς. Τα θεμελιώδη που καλύφθηκαν εδώ—ανάλυση HTML, επίλυση διαδρομών και χειρισμός δυαδικών αρχείων—είναι δομικά στοιχεία για πολλές εργασίες αυτοματοποίησης web.

Έχετε ερωτήσεις ή θέλετε να μοιραστείτε μια ενδιαφέρουσα περίπτωση χρήσης; Αφήστε ένα σχόλιο παρακάτω, και καλή αναζήτηση εικονιδίων!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική;

- [Πώς να Επεξεργαστείτε το Δέντρο Εγγράφου HTML στο Aspose.HTML για Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Πώς να Μετατρέψετε HTML σε PDF Java – Χρησιμοποιώντας Aspose.HTML για Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Πώς να Μετατρέψετε HTML σε JPEG Χρησιμοποιώντας Aspose.HTML για Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-jpeg/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}