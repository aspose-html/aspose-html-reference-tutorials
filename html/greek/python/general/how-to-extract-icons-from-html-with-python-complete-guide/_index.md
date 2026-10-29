---
category: general
date: 2026-07-02
description: Πώς να εξάγετε εικονίδια από ένα αρχείο HTML χρησιμοποιώντας Python.
  Μάθετε πώς να διαβάζετε αρχείο HTML με Python, να αναλύετε το έγγραφο HTML και να
  εξάγετε το χαρακτηριστικό href για να λάβετε τις διευθύνσεις URL των favicon.
draft: false
keywords:
- how to extract icons
- read html file python
- parse html document
- extract href attribute
- extract favicon urls
language: el
og_description: Πώς να εξάγετε εικονίδια από μια σελίδα HTML χρησιμοποιώντας Python.
  Αυτό το σεμινάριο σας δείχνει πώς να διαβάσετε αρχείο HTML με Python, να αναλύσετε
  το έγγραφο και να εξάγετε τις URL των favicon.
og_title: Πώς να εξάγετε εικονίδια από HTML – Οδηγός Python
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: How to extract icons from an HTML file using Python. Learn to read
    HTML file python, parse HTML document, and extract href attribute to get favicon
    URLs.
  headline: How to Extract Icons from HTML with Python – Complete Guide
  type: TechArticle
- questions:
  - answer: Some sites embed icons via `<meta itemprop="image">`. Extend `is_icon_link`
      to also check for `meta` with `itemprop="image"` and pull its `content` attribute.
    question: What if the HTML uses `<meta>` tags for icons?
  - answer: Yes—just feed each URL into `requests.get(url, stream=True)` and write
      the content to a file. Remember to handle relative URLs with `urljoin`.
    question: Can I fetch the icons automatically?
  - answer: 'Absolutely. Replace the file‑reading step with `requests.get(page_url).text`
      and pass the HTML string to BeautifulSoup. Just be mindful of robots.txt and
      rate limits. --- ## Wrap‑Up We’ve covered **how to extract icons** from any
      static HTML using Python, from reading the file to printing out each f'
    question: Does this work on remote pages?
  type: FAQPage
tags:
- python
- html-parsing
- web‑scraping
- favicon
title: Πώς να εξάγετε εικονίδια από HTML με Python – Πλήρης οδηγός
url: /el/python/general/how-to-extract-icons-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εξάγετε εικονίδια από HTML με Python – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να εξάγετε εικονίδια** από μια ιστοσελίδα χωρίς να ανοίξετε έναν περιηγητή; Ίσως δημιουργείτε έναν κατάλογο ιστότοπων, ένα εργαλείο ελέγχου SEO, ή απλώς είστε περίεργοι για τα μικρά favicons που εμφανίζονται στις καρτέλες. Τα καλά νέα είναι ότι μπορείτε να το κάνετε με λίγες γραμμές Python—χωρίς Selenium, χωρίς headless Chrome, μόνο ένα αρχείο HTML απλού κειμένου.

Σε αυτό το tutorial θα περάσουμε από την ανάγνωση ενός αρχείου HTML με Python, την ανάλυση του εγγράφου HTML, και τελικά **την εξαγωγή του χαρακτηριστικού href** από τις ετικέτες `<link rel="icon">` για να πάρουμε τα URLs των favicon. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο κομμάτι κώδικα που λειτουργεί σε οποιοδήποτε στατικό HTML τουρίσετε, και θα δείτε επίσης πώς να διαχειριστείτε περιπτώσεις όπως σχετικές διαδρομές ή πολλαπλές δηλώσεις εικονιδίων.

## Τι Θα Μάθετε

- Φορτώστε ένα τοπικό αρχείο HTML με Python (read html file python)  
- Χρησιμοποιήστε έναν ελαφρύ parser για **να αναλύσετε το έγγραφο html** με ασφάλεια  
- Εντοπίστε στοιχεία `<link>` που δηλώνουν ένα εικονίδιο  
- **Εξάγετε το χαρακτηριστικό href** και μετατρέψτε τα σε απόλυτα URLs  
- Συλλέξτε και εκτυπώστε όλα τα ανακαλυφθέντα **favicon URLs**  

Δεν απαιτούνται εξωτερικές υπηρεσίες—μόνο η τυπική βιβλιοθήκη και το δημοφιλές πακέτο **BeautifulSoup**.

![Screenshot showing Python script extracting icons – how to extract icons](https://example.com/images/extract-icons-python.png "how to extract icons")
*Κείμενο alt εικόνας: "πώς να εξάγετε εικονίδια χρησιμοποιώντας ένα script Python"*

## Προαπαιτούμενα

- Python 3.8+ εγκατεστημένο  
- `beautifulsoup4` βιβλιοθήκη (`pip install beautifulsoup4`)  
- Ένα τοπικό αρχείο HTML που θέλετε να σαρώσετε (π.χ., `sample.html`)  

Αν τα έχετε ήδη, ας ξεκινήσουμε.

## Βήμα 1: Ανάγνωση Αρχείου HTML με Python – Φόρτωση του Εγγράφου

Πρώτα απ' όλα: πρέπει να ανοίξουμε το αρχείο και να περάσουμε το περιεχόμενό του σε έναν parser. Χρησιμοποιώντας `with open(..., "r", encoding="utf‑8")` εξασφαλίζει ότι το αρχείο κλείνει αυτόματα, και η κωδικοποίηση UTF‑8 διαχειρίζεται τις περισσότερες σύγχρονες σελίδες.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Step 1: Load the HTML document from disk
html_path = Path("sample.html")          # adjust the path as needed
html_content = html_path.read_text(encoding="utf-8")
```

**Γιατί είναι σημαντικό:** Το άνοιγμα του αρχείου με τη σωστή κωδικοποίηση αποτρέπει μυστηριώδους χαρακτήρες `�` που θα μπορούσαν να σπάσουν τον parser αργότερα. Η χρήση του `Path` από τη τυπική βιβλιοθήκη κάνει επίσης τον κώδικα διαλειτουργικό.

## Βήμα 2: Ανάλυση Εγγράφου HTML – Εύρεση Όλων των Συνδέσμων Εικονιδίων

Τώρα δίνουμε το ακατέργαστο HTML στο **BeautifulSoup**, το οποίο δημιουργεί ένα πλοηγήσιμο δέντρο. Θα ψάξουμε για κάθε ετικέτα `<link>` της οποίας το χαρακτηριστικό `rel` περιέχει τη λέξη `icon`. Σημειώστε ότι το `rel` μπορεί να είναι λίστα χωρισμένη με κενά (`rel="shortcut icon"`), οπότε χρειαζόμαστε έναν ευέλικτο έλεγχο.

```python
# Step 2: Parse the HTML and locate <link> tags that declare an icon
soup = BeautifulSoup(html_content, "html.parser")

def is_icon_link(tag):
    """Return True if a <link> tag declares an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    # BeautifulSoup may return a list or a string; handle both
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

icon_links = [tag for tag in soup.find_all(is_icon_link)]
```

**Γιατί αυτό το βήμα είναι κρίσιμο:** Ένα αφελές `soup.find_all("link", rel="icon")` θα χάσει παραλλαγές όπως `rel="shortcut icon"` ή `rel="apple-touch-icon"`. Η βοηθητική μας συνάρτηση `is_icon_link` καλύπτει αυτές τις περιπτώσεις, καθιστώντας την εξαγωγή αξιόπιστη.

## Βήμα 3: Εξαγωγή Χαρακτηριστικού href – Ανάκτηση των URLs

Με τις σχετικές ετικέτες συλλεγμένες, τώρα εξάγουμε το χαρακτηριστικό `href` από καθεμία. Κάποιες σελίδες μπορεί να παραλείπουν το `href` (σπάνια, αλλά δυνατόν), οπότε προστατεύουμε από `None`. Επιπλέον, τα favicons συχνά δηλώνονται με σχετικές URLs, οπότε θα τα επιλύσουμε σε σχέση με τη βασική URL της σελίδας αν τη γνωρίζετε. Για ένα τοπικό αρχείο θα κρατήσουμε τη διαδρομή όπως είναι.

```python
# Step 3: Grab the href attribute from each icon link
icon_urls = []
for tag in icon_links:
    href = tag.get("href")
    if href:
        icon_urls.append(href.strip())
```

**Γιατί αφαιρούμε τα κενά:** Οι δημιουργοί HTML μερικές φορές προσθέτουν κατά λάθος κενά γύρω από τα URLs, κάτι που θα σπάσει ένα επόμενο αίτημα. Η αφαίρεση εξασφαλίζει καθαρές συμβολοσειρές.

## Βήμα 4: Εξαγωγή URLs Favicon – Εμφάνιση των Αποτελεσμάτων

Τέλος, εκτυπώνουμε (ή επιστρέφουμε) τη λίστα των ανακαλυφθέντων URLs. Σε ένα πραγματικό script μπορεί να τα γράψετε σε CSV, να κατεβάσετε τα εικονίδια, ή να τα περάσετε σε άλλη υπηρεσία. Εδώ είναι ένας απλός βρόχος που δείχνει το αποτέλεσμα στην κονσόλα.

```python
# Step 4: Display each discovered favicon URL
if not icon_urls:
    print("No icon links found in the document.")
else:
    for url in icon_urls:
        print("Favicon URL:", url)
```

### Διαχείριση Περιπτώσεων Άκρων

- **Πολλαπλές τιμές rel:** Ο έλεγχος `is_icon_link` μας ήδη εντοπίζει `rel="shortcut icon"` και `rel="apple-touch-icon"`.  
- **Σχετικές διαδρομές:** Αν αργότερα χρειαστείτε απόλυτα URLs, χρησιμοποιήστε `urllib.parse.urljoin(base_url, href)`.  
- **Απουσία href:** Η προστασία `if href:` παραλείπει εσφαλμένες ετικέτες, αποφεύγοντας σφάλματα `NoneType`.  
- **Διπλότυπες καταχωρήσεις:** Μπορείτε να χρησιμοποιήσετε `icon_urls = list(dict.fromkeys(icon_urls))` για απομάκρυνση διπλότυπων.

---

## Πλήρες Script – Ολοκληρωμένη Λύση

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες, έτοιμο‑να‑τρέξει πρόγραμμα. Αποθηκεύστε το ως `extract_icons.py` και ορίστε το `html_path` σε οποιοδήποτε αρχείο θέλετε.

```python
#!/usr/bin/env python3
"""
How to extract icons from an HTML file using Python.

This script:
- Reads an HTML file (read html file python)
- Parses the HTML document (parse html document)
- Finds <link> tags with rel containing "icon"
- Extracts the href attribute (extract href attribute)
- Prints each favicon URL (extract favicon urls)
"""

from pathlib import Path
from bs4 import BeautifulSoup

def is_icon_link(tag):
    """Detect <link> tags that declare an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

def extract_favicon_urls(html_path: Path):
    """Return a list of favicon URLs found in the given HTML file."""
    html_content = html_path.read_text(encoding="utf-8")
    soup = BeautifulSoup(html_content, "html.parser")
    icon_links = [t for t in soup.find_all(is_icon_link)]

    urls = []
    for tag in icon_links:
        href = tag.get("href")
        if href:
            urls.append(href.strip())
    # Remove duplicates while preserving order
    return list(dict.fromkeys(urls))

if __name__ == "__main__":
    # Adjust the path to point to your HTML file
    html_file = Path("sample.html")
    favicon_urls = extract_favicon_urls(html_file)

    if not favicon_urls:
        print("No icon links found in the document.")
    else:
        for url in favicon_urls:
            print("Favicon URL:", url)
```

**Αναμενόμενο αποτέλεσμα** (υπόθεση ότι το `sample.html` περιέχει δύο εικονίδια):

```
Favicon URL: /images/favicon.ico
Favicon URL: https://example.com/assets/apple-touch-icon.png
```

Τρέξτε το με `python extract_icons.py` και θα δείτε τα URLs να εκτυπώνονται στην κονσόλα.

---

## Συχνές Ερωτήσεις

**Ε: Τι γίνεται αν το HTML χρησιμοποιεί ετικέτες `<meta>` για εικονίδια;**  
Α: Κάποιες ιστοσελίδες ενσωματώνουν εικονίδια μέσω `<meta itemprop="image">`. Επεκτείνετε το `is_icon_link` ώστε να ελέγχει επίσης για `meta` με `itemprop="image"` και να εξάγει το χαρακτηριστικό `content`.

**Ε: Μπορώ να κατεβάσω τα εικονίδια αυτόματα;**  
Α: Ναι—απλώς περάστε κάθε URL στο `requests.get(url, stream=True)` και γράψτε το περιεχόμενο σε αρχείο. Θυμηθείτε να διαχειριστείτε τις σχετικές URLs με `urljoin`.

**Ε: Λειτουργεί αυτό σε απομακρυσμένες σελίδες;**  
Α: Απόλυτα. Αντικαταστήστε το βήμα ανάγνωσης αρχείου με `requests.get(page_url).text` και περάστε τη συμβολοσειρά HTML στο BeautifulSoup. Να προσέχετε το robots.txt και τα όρια ταχύτητας.

---

## Συμπέρασμα

Καλύψαμε **πώς να εξάγετε εικονίδια** από οποιοδήποτε στατικό HTML χρησιμοποιώντας Python, από την ανάγνωση του αρχείου μέχρι την εκτύπωση κάθε URL favicon. Οι βασικές ιδέες—ανάγνωση αρχείου, ανάλυση εγγράφου, εντοπισμός των σωστών ετικετών, και εξαγωγή του χαρακτηριστικού `href`—είναι επαναχρησιμοποιήσιμα μοτίβα που θα συναντήσετε σε πολλές εργασίες web‑scraping.

Επόμενα βήματα; Δοκιμάστε να επεκτείνετε το script για:

- Επίλυση σχετικών URLs σε σχέση με τη βασική URL της σελίδας  
- Κατέβασμα κάθε εικονιδίου και αποθήκευση τοπικά  
- Υποστήριξη επιπλέον μορφών εικονιδίων (`rel="mask-icon"` για Safari)  

Νιώστε ελεύθεροι να πειραματιστείτε, και αν αντιμετωπίσετε προβλήματα, αφήστε ένα σχόλιο παρακάτω. Καλή ανάλυση!

## Τι Θα Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση στα δικά σας projects.

- [Πώς να Αναζητήσετε HTML σε Java – Πλήρης Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Πώς να Επεξεργαστείτε το Δέντρο Εγγράφου HTML στο Aspose.HTML για Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Αποθήκευση Εγγράφου HTML σε Αρχείο στο Aspose.HTML για Java](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}