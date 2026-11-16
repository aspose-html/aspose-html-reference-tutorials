---
category: general
date: 2026-07-18
description: Μετατρέψτε το HTML σε EPUB με την Python γρήγορα. Μάθετε πώς να φορτώνετε
  αρχείο HTML στην Python και επίσης να μετατρέπετε το HTML σε MHTML χρησιμοποιώντας
  απλές βιβλιοθήκες.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to epub
- load html file in python
- convert html to mhtml
language: el
lastmod: 2026-07-18
og_description: Μετατρέψτε HTML σε EPUB με Python με ένα σαφές, εκτελέσιμο παράδειγμα.
  Μάθετε επίσης πώς να φορτώσετε αρχείο HTML σε Python και να μετατρέψετε HTML σε
  MHTML σε λίγα λεπτά.
og_image_alt: Diagram showing convert html to epub workflow
og_title: Μετατροπή HTML σε EPUB με Python – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  headline: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  name: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Python 3.9+** – the syntax used here works on any recent version.'
    text: '**Python 3.9+** – the syntax used here works on any recent version.'
  - name: '**pip** – to install third‑party packages.'
    text: '**pip** – to install third‑party packages.'
  - name: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
    text: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
  type: HowTo
tags:
- python
- html
- epub
- mhtml
- file conversion
title: Μετατροπή HTML σε EPUB με Python – Πλήρης Οδηγός Βήμα‑Βήμα
url: /el/python/general/convert-html-to-epub-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή HTML σε EPUB με Python – Πλήρης Οδηγός Βήμα‑βήμα

Έχετε αναρωτηθεί ποτέ πώς να **μετατρέψετε HTML σε EPUB** χωρίς να τσακίζετε τα μαλλιά σας; Δεν είστε ο μόνος—οι προγραμματιστές χρειάζονται συνεχώς να μετατρέπουν ιστοσελίδες σε e‑books για ανάγνωση εκτός σύνδεσης, και η υλοποίηση σε Python είναι εκπληκτικά εύκολη. Σε αυτό το tutorial θα δούμε πώς να φορτώσουμε ένα αρχείο HTML σε Python, να μετατρέψουμε αυτό το HTML σε EPUB, και ακόμη να μετατρέψουμε την ίδια πηγή σε MHTML για αρχεία φιλικά προς το email.

Στο τέλος του οδηγού θα έχετε ένα έτοιμο‑για‑εκτέλεση script που παίρνει ένα μόνο αρχείο `sample.html` και παράγει τόσο `sample.epub` όσο και `sample.mhtml`. Καμία μυστική διαδικασία, μόνο καθαρός κώδικας και εξηγήσεις.

---

![Διάγραμμα ροής μετατροπής](https://example.com/images/convert-html-epub.png "Διάγραμμα που δείχνει τη ροή μετατροπής html σε epub")

## Τι Θα Δημιουργήσετε

- **Φορτώστε ένα αρχείο HTML σε Python** χρησιμοποιώντας τα ενσωματωμένα modules `pathlib` και `io`.  
- **Μετατρέψτε HTML σε EPUB** με τη βιβλιοθήκη `ebooklib`, η οποία διαχειρίζεται για εσάς τη μορφή του container EPUB.  
- **Μετατρέψτε HTML σε MHTML** (γνωστό και ως MHT) χρησιμοποιώντας το πακέτο `email`, δημιουργώντας ένα αρχείο web‑archive ενός μόνο αρχείου που οι browsers μπορούν να ανοίξουν άμεσα.  

Θα καλύψουμε επίσης:

- Απαιτούμενες εξαρτήσεις και πώς να τις εγκαταστήσετε.  
- Διαχείριση σφαλμάτων ώστε το script σας να αποτυγχάνει με χάρη.  
- Πώς να προσαρμόσετε τα μεταδεδομένα όπως τίτλο και συγγραφέα για το αρχείο EPUB.  

Έτοιμοι; Ας βουτήξουμε.

---

## Προαπαιτούμενα

Πριν ξεκινήσουμε τον κώδικα, βεβαιωθείτε ότι έχετε:

1. **Python 3.9+** – η σύνταξη που χρησιμοποιείται εδώ λειτουργεί σε οποιαδήποτε πρόσφατη έκδοση.  
2. **pip** – για την εγκατάσταση τρίτων πακέτων.  
3. Ένα απλό αρχείο HTML, π.χ., `sample.html`, τοποθετημένο σε φάκελο που ελέγχετε.  

Αν τα έχετε ήδη, τέλεια—πηδήξτε στην επόμενη ενότητα.  

> **Συμβουλή:** Διατηρήστε το HTML σας καλά δομημένο (σωστές ενότητες `<head>` και `<body>`). Ενώ το `ebooklib` θα προσπαθήσει να διορθώσει μικρά προβλήματα, μια καθαρή πηγή σας εξοικονομεί προβλήματα αργότερα.

## Βήμα 1 – Εγκατάσταση των Απαιτούμενων Βιβλιοθηκών

Χρειαζόμαστε δύο εξωτερικά πακέτα:

- **ebooklib** – για τη δημιουργία EPUB.  
- **beautifulsoup4** – προαιρετικό, αλλά χρήσιμο για τον καθαρισμό του HTML πριν τη μετατροπή.  

Τρέξτε αυτό στο τερματικό σας:

```bash
pip install ebooklib beautifulsoup4
```

> **Γιατί αυτές οι βιβλιοθήκες;** Το `ebooklib` δημιουργεί τη δομή EPUB βασισμένη σε ZIP για εσάς, διαχειριζόμενο αυτόματα το φάκελο `META‑INF`, το `content.opf` και το `toc.ncx`. Το `beautifulsoup4` μας επιτρέπει να καθαρίσουμε το HTML, διασφαλίζοντας ότι το τελικό e‑book αποδίδει σωστά σε όλους τους αναγνώστες.

## Βήμα 2 – Φόρτωση του Αρχείου HTML σε Python

Η φόρτωση ενός αρχείου HTML είναι απλή, αλλά θα το τυλίξουμε σε μια μικρή βοηθητική συνάρτηση που επιστρέφει ένα αντικείμενο **BeautifulSoup** για επεξεργασία αργότερα.

```python
from pathlib import Path
from bs4 import BeautifulSoup

def load_html(filepath: str) -> BeautifulSoup:
    """
    Load an HTML file from disk and return a BeautifulSoup object.
    Raises FileNotFoundError if the file does not exist.
    """
    path = Path(filepath)
    if not path.is_file():
        raise FileNotFoundError(f"HTML file not found: {filepath}")

    # Read the file using UTF‑8 encoding (most common for web content)
    html_content = path.read_text(encoding="utf-8")
    # Parse with BeautifulSoup for optional cleaning later
    soup = BeautifulSoup(html_content, "html.parser")
    return soup
```

**Επεξήγηση:**  
- `Path` μας παρέχει διαχείριση αρχείων ανεξάρτητη από το λειτουργικό σύστημα.  
- Η χρήση του `read_text` αποφεύγει το χειροκίνητο boilerplate `open`/`close`.  
- Η επιστροφή ενός αντικειμένου `BeautifulSoup` σημαίνει ότι μπορούμε αργότερα να αφαιρέσουμε scripts, να διορθώσουμε κατεστραμμένες ετικέτες ή να ενσωματώσουμε ένα stylesheet πριν **μετατρέψουμε HTML σε EPUB**.

## Βήμα 3 – Μετατροπή HTML σε EPUB

Τώρα που μπορούμε να **φορτώσουμε αρχείο HTML σε Python**, ας το μετατρέψουμε σε ένα καθαρό EPUB. Η παρακάτω συνάρτηση δέχεται ένα αντικείμενο `BeautifulSoup`, μια διαδρομή προορισμού και προαιρετικά μεταδεδομένα.

```python
import uuid
from ebooklib import epub

def html_to_epub(soup: BeautifulSoup,
                 output_path: str,
                 title: str = "Untitled Book",
                 author: str = "Anonymous") -> None:
    """
    Convert a BeautifulSoup HTML document to an EPUB file.
    """
    # Create a new EPUB book instance
    book = epub.EpubBook()

    # Set basic metadata – this is what shows up in e‑reader libraries
    book.set_identifier(str(uuid.uuid4()))
    book.set_title(title)
    book.set_language('en')
    book.add_author(author)

    # Convert the soup back to a string; we could also clean it here
    html_str = str(soup)

    # Create a chapter (EPUB requires at least one)
    chapter = epub.EpubHtml(title=title,
                            file_name='chap_01.xhtml',
                            lang='en')
    chapter.content = html_str
    book.add_item(chapter)

    # Define the spine (reading order) and table of contents
    book.toc = (epub.Link('chap_01.xhtml', title, 'intro'),)
    book.spine = ['nav', chapter]

    # Add default navigation files
    book.add_item(epub.EpubNcx())
    book.add_item(epub.EpubNav())

    # Write the final EPUB file
    epub.write_epub(output_path, book, {})

    print(f"✅ EPUB created at: {output_path}")
```

**Γιατί αυτό λειτουργεί:**  
- `ebooklib.epub.EpubBook` αφαιρεί την πολυπλοκότητα του ZIP container και των απαιτούμενων αρχείων manifest.  
- Δημιουργούμε ένα UUID ως αναγνωριστικό για να αποφύγουμε διπλότυπα IDs αν δημιουργήσετε πολλά βιβλία.  
- Το `spine` λέει στους αναγνώστες τη σειρά των κεφαλαίων· ένα βιβλίο με ένα κεφάλαιο είναι επαρκές για τις περισσότερες απλές πηγές HTML.  

**Εκτέλεση της μετατροπής:**

```python
if __name__ == "__main__":
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_epub(html_doc,
                 "YOUR_DIRECTORY/sample.epub",
                 title="My Sample eBook",
                 author="Jane Developer")
```

Όταν εκτελέσετε το script, θα δείτε ένα πράσινο σημάδι ελέγχου που επιβεβαιώνει τη θέση του αρχείου EPUB.

## Βήμα 4 – Μετατροπή HTML σε MHTML

MHTML (ή MHT) ενώνει το HTML και όλους τους πόρους του (εικόνες, CSS) σε ένα ενιαίο αρχείο MIME. Το πακέτο `email` της Python μπορεί να δημιουργήσει αυτή τη μορφή χωρίς εξωτερικές εξαρτήσεις.

```python
import mimetypes
import base64
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from email.mime.base import MIMEBase
from email import encoders

def html_to_mhtml(soup: BeautifulSoup,
                  output_path: str,
                  base_url: str = "") -> None:
    """
    Convert a BeautifulSoup HTML document to an MHTML file.
    `base_url` is used to resolve relative resource links.
    """
    # Create the multipart/related container required for MHTML
    mhtml = MIMEMultipart('related')
    mhtml['Subject'] = 'Converted MHTML document'
    mhtml['Content-Type'] = 'multipart/related; type="text/html"'

    # Main HTML part
    html_part = MIMEText(str(soup), 'html', 'utf-8')
    html_part.add_header('Content-Location', 'file://index.html')
    mhtml.attach(html_part)

    # Optional: embed images referenced in the HTML
    for img in soup.find_all('img'):
        src = img.get('src')
        if not src:
            continue

        # Resolve absolute path if needed
        img_path = Path(base_url) / src if base_url else Path(src)
        if not img_path.is_file():
            continue  # skip missing files

        # Guess MIME type; default to octet-stream
        mime_type, _ = mimetypes.guess_type(img_path)
        mime_type = mime_type or 'application/octet-stream'

        with img_path.open('rb') as f:
            img_data = f.read()

        img_part = MIMEBase(*mime_type.split('/'))
        img_part.set_payload(img_data)
        encoders.encode_base64(img_part)
        img_part.add_header('Content-Location', f'file://{src}')
        img_part.add_header('Content-Transfer-Encoding', 'base64')
        mhtml.attach(img_part)

    # Write the MHTML file
    with open(output_path, 'wb') as out_file:
        out_file.write(mhtml.as_bytes())

    print(f"✅ MHTML created at: {output_path}")
```

**Κύρια σημεία:**  

- Ο τύπος MIME `multipart/related` ενημερώνει τους browsers ότι το τμήμα HTML και οι πόροι του ανήκουν μαζί.  
- Διατρέχουμε τις ετικέτες `<img>` για να ενσωματώσουμε εικόνες· αν δεν χρειάζεστε εικόνες, μπορείτε να παραλείψετε αυτό το τμήμα.  
- `Content-Location` χρησιμοποιεί ένα URI `file://` ώστε οι browsers να μπορούν να επιλύσουν τους πόρους εσωτερικά.  

**Κλήση της συνάρτησης:**

```python
if __name__ == "__main__":
    # Re‑use the previously loaded soup
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_mhtml(html_doc, "YOUR_DIRECTORY/sample.mhtml", base_url="YOUR_DIRECTORY")
```

Τώρα έχετε τόσο το `sample.epub` όσο και το `sample.mhtml` δίπλα-δίπλα.

## Πλήρες Script – Όλα τα Βήματα σε Ένα Αρχείο

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση script που συνδυάζει όλα. Αποθηκεύστε το ως `convert_html.py` και αντικαταστήστε το `YOUR_DIRECTORY` με τη διαδρομή που περιέχει το `sample.html`.



## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικούς τομείς που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Μετατρέψετε HTML σε MHTML με Aspose.HTML για Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [Πώς να Μετατρέψετε EPUB σε PDF με Java – Χρησιμοποιώντας Aspose.HTML](/html/english/java/converting-epub-to-pdf/convert-epub-to-pdf/)
- [Πώς να Μετατρέψετε EPUB σε Εικόνες με Aspose.HTML για Java](/html/english/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}