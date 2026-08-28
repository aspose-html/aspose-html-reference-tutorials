---
category: general
date: 2026-06-10
description: Φορτώστε HTML από URL για να λάβετε γρήγορα τα εικονίδια ιστοτόπων. Μάθετε
  πώς να εξάγετε favicons, να ανακτήσετε τις διευθύνσεις URL των favicons των ιστοτόπων
  και να διαχειριστείτε περιπτώσεις άκρων σε Python.
draft: false
keywords:
- load html from url
- get website icons
- how to extract favicons
- extract favicon urls
- fetch website favicon urls
language: el
og_description: Φορτώστε HTML από URL για να εξάγετε τα favicons και να ανακτήσετε
  τις διευθύνσεις URL των favicons του ιστότοπου. Ένας βήμα‑βήμα οδηγός Python για
  προγραμματιστές.
og_title: Φόρτωση HTML από URL και λήψη εικονιδίων ιστοσελίδας – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Load HTML from URL to get website icons quickly. Learn how to extract
    favicons, fetch website favicon URLs, and handle edge cases in Python.
  headline: Load HTML from URL and Get Website Icons – Complete Guide
  type: TechArticle
tags:
- web scraping
- favicon extraction
- python
- html parsing
title: Φόρτωση HTML από URL και λήψη εικονιδίων ιστοσελίδας – Πλήρης οδηγός
url: /el/python/general/load-html-from-url-and-get-website-icons-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Φόρτωση HTML από URL και Λήψη Εικονιδίων Ιστοσελίδας – Πλήρης Οδηγός

Κάποτε χρειάστηκε να **φορτώσετε HTML από URL** μόνο για να πάρετε το μικρό λογότυπο ενός site; Δεν είστε μόνοι. Είτε χτίζετε έναν διαχειριστή σελιδοδεικτών, έναν πίνακα ελέγχου SEO, είτε ένα προσωπικό χόμπι project, η λήψη εικονιδίων ιστοσελίδας είναι ένα μικρό αλλά απαραίτητο κομμάτι του παζλ.

Σε αυτό το tutorial θα δείξουμε **πώς να εξάγετε favicons** χρησιμοποιώντας απλό Python—χωρίς βαρύ Selenium, χωρίς μαγεία του προγράμματος περιήγησης. Στο τέλος θα μπορείτε να **ανακτήσετε URLs favicons ιστοσελίδων**, να διαχειριστείτε σχετικές διαδρομές, και ακόμη να πάρετε πολλαπλά εικονίδια αν ένα site τα παρέχει. Έτοιμοι; Ας βουτήξουμε.

## Γιατί να Φορτώνουμε HTML από URL;

Η φόρτωση του ακατέργαστου HTML μιας σελίδας σας δίνει άμεση πρόσβαση στις ετικέτες `<link>` που τα προγράμματα περιήγησης χρησιμοποιούν για να εντοπίσουν favicons. Αυτές οι ετικέτες συνήθως φαίνονται έτσι:

```html
<link rel="icon" href="/favicon.ico">
<link rel="apple-touch-icon" href="https://example.com/apple-touch-icon.png">
```

Αν μπορείτε να εξάγετε αυτό το markup, μπορείτε προγραμματιστικά να διαβάσετε το χαρακτηριστικό `href` και να κατεβάσετε την εικόνα μόνοι σας. Είναι πιο γρήγορο από το σκανάρισμα στιγμιότυπων και λειτουργεί για οποιοδήποτε site ακολουθεί τις τυπικές συμβάσεις.

## Βήμα 1 – Φόρτωση του Εγγράφου HTML από URL

Το πρώτο που χρειαζόμαστε είναι ένας τρόπος να φέρουμε τον κώδικα της σελίδας. Η πιο δημοφιλής επιλογή στην Python είναι η βιβλιοθήκη **requests** επειδή είναι απλή, αξιόπιστη, και διαχειρίζεται ανακατευθύνσεις αυτόματα.

```python
import requests

def fetch_html(url: str) -> str:
    """
    Retrieve the raw HTML from the given URL.
    Raises an exception if the request fails.
    """
    response = requests.get(url, timeout=10)
    response.raise_for_status()          # Fail fast on HTTP errors
    return response.text
```

> **Pro tip:** Αν εργάζεστε πίσω από εταιρικό proxy, περάστε `proxies=` στο `requests.get`. Επίσης, ορίζοντας ένα μικρό timeout αποτρέπει το script σας να κολλάει σε νεκρούς ιστότοπους.

Τώρα μπορούμε να καλέσουμε `fetch_html("https://example.com")` και να πάρουμε μια συμβολοσειρά που περιέχει το markup της σελίδας. Αυτό είναι ο πυρήνας του **load HTML from URL**—το υπόλοιπο του pipeline δουλεύει με αυτή τη συμβολοσειρά.

## Βήμα 2 – Λήψη Εικονιδίων Ιστοσελίδας

Μόλις έχουμε το HTML, το επόμενο βήμα είναι να εντοπίσουμε κάθε στοιχείο `<link>` του οποίου το χαρακτηριστικό `rel` αναφέρει “icon”. Το ενσωματωμένο module `html.parser` μπορεί να κάνει τη δουλειά, αλλά η **BeautifulSoup** κάνει τον κώδικα πολύ πιο αναγνώσιμο.

```python
from bs4 import BeautifulSoup
from urllib.parse import urljoin

def extract_icon_links(html: str, base_url: str) -> list[str]:
    """
    Parse the HTML and return a list of absolute URLs pointing to icons.
    Handles relative hrefs by joining them with the page’s base URL.
    """
    soup = BeautifulSoup(html, "html.parser")
    icons = []

    # Look for any <link> tag where rel contains "icon"
    for link in soup.find_all("link", rel=lambda r: r and "icon" in r.lower()):
        href = link.get("href")
        if href:
            # Convert relative URLs to absolute ones
            absolute_url = urljoin(base_url, href)
            icons.append(absolute_url)

    return icons
```

Παρατηρήστε πώς χρησιμοποιούμε το `urljoin` για να μετατρέψουμε το `"/favicon.ico"` σε `"https://example.com/favicon.ico"`—αυτό είναι ένα κοινό edge case όταν **get website icons**. Κάποια sites ακόμη σερβίρουν διαφορετικά εικονίδια για διαφορετικές συσκευές, οπότε μπορεί να καταλήξετε με μια χούφτα URLs. Κανένα πρόβλημα· τα συλλέγουμε όλα.

## Βήμα 3 – Εξαγωγή URLs Favicon και Εμφάνιση τους

Η συναρμολόγηση των κομματιών είναι απλή. Θα φέρουμε το HTML, θα τρέξουμε τον extractor, και θα εκτυπώσουμε τη λίστα που προκύπτει. Το τελικό script είναι το εξής:

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin

def fetch_html(url: str) -> str:
    response = requests.get(url, timeout=10)
    response.raise_for_status()
    return response.text

def extract_icon_links(html: str, base_url: str) -> list[str]:
    soup = BeautifulSoup(html, "html.parser")
    icons = []
    for link in soup.find_all("link", rel=lambda r: r and "icon" in r.lower()):
        href = link.get("href")
        if href:
            icons.append(urljoin(base_url, href))
    return icons

def main():
    target = "https://example.com"
    html = fetch_html(target)
    icon_urls = extract_icon_links(html, target)
    print("Found icon URLs:", icon_urls)

if __name__ == "__main__":
    main()
```

### Αναμενόμενο Αποτέλεσμα

Εκτελώντας το script σε ένα site που παρέχει ένα τυπικό favicon μπορεί να δείτε:

```
Found icon URLs: ['https://example.com/favicon.ico']
```

Αν το site παρέχει πολλαπλά εικονίδια (Apple touch icon, shortcut icon, κ.λπ.), θα δείτε μια μεγαλύτερη λίστα:

```
Found icon URLs: [
    'https://example.com/favicon.ico',
    'https://example.com/apple-touch-icon.png',
    'https://example.com/favicon-32x32.png'
]
```

Αυτή είναι η πλήρης ροή εργασίας **extract favicon urls**—συμπαγής, ελαφριά σε εξαρτήσεις, και έτοιμη να ενσωματωθεί σε οποιοδήποτε project.

## Διαχείριση Συνηθισμένων Προβλημάτων

| Πρόβλημα | Γιατί Συμβαίνει | Γρήγορη Λύση |
|----------|----------------|--------------|
| **Σχετικό `href` χωρίς ετικέτα `<base>`** | Το `urljoin` υποθέτει το URL της σελίδας ως βάση, κάτι που λειτουργεί στις περισσότερες περιπτώσεις. | Αν υπάρχει ετικέτα `<base href="...">`, διαβάστε την πρώτα και περάστε τη ως `base_url`. |
| **Απουσία `rel="icon"`** | Κάποια sites χρησιμοποιούν `rel="shortcut icon"` ή προσαρμοσμένες τιμές. | Επεκτείνετε το lambda: `rel=lambda r: r and ("icon" in r.lower() or "shortcut" in r.lower())`. |
| **Ανακατευθύνσεις σε διαφορετικό domain** | Το favicon μπορεί να βρίσκεται σε CDN. | Το `urljoin` θα λύσει σωστά το νέο domain επειδή χρησιμοποιεί το τελικό URL της αίτησης (`response.url`). |
| **Σπασμένοι σύνδεσμοι (404)** | Το HTML δείχνει σε αρχείο που δεν υπάρχει πια. | Μετά την εξαγωγή των URLs, μπορείτε να ελέγξετε το καθένα με ένα HEAD request πριν τα χρησιμοποιήσετε. |
| **Πολλαπλές ετικέτες `<link>` με το ίδιο εικονίδιο** | Διπλότυπες καταχωρήσεις γεμίζουν τη λίστα. | Χρησιμοποιήστε `set(icon_urls)` για αφαίρεση διπλοτύπων πριν την επιστροφή. |

## Προχωρώντας – Λήψη URLs Favicon Ιστοσελίδων Μαζικά

Αν χρειάζεστε **fetch website favicon URLs** για μια λίστα domain, τυλίξτε τη λογική `main` σε έναν βρόχο:

```python
domains = ["https://example.com", "https://python.org", "https://github.com"]
for site in domains:
    try:
        icons = extract_icon_links(fetch_html(site), site)
        print(site, "->", icons)
    except Exception as e:
        print(site, "error:", e)
```

Αυτό το pattern κλιμακώνεται ωραία, και μπορείτε να προσθέσετε caching (π.χ., με `functools.lru_cache`) για να αποφύγετε την υπερβολική πρόσβαση στο ίδιο site.

## Οπτική Επισκόπηση

![Load HTML from URL diagram](load-html-url.png)

*Alt text: Διάγραμμα φόρτωσης HTML από URL που δείχνει τα βήματα fetch → parse → extract.*

Η παραπάνω εικόνα συνοψίζει τη διαδικασία τριών βημάτων: **load HTML from URL**, **get website icons**, και **extract favicon URLs**. Είναι χρήσιμη όταν πρέπει να εξηγήσετε τη ροή σε έναν συνεργάτη.

## Συμπέρασμα

Διασχίσαμε μια πλήρη, έτοιμη για παραγωγή λύση για το πώς να **load HTML from URL** και **get website icons** χρησιμοποιώντας μόνο τις βιβλιοθήκες requests και BeautifulSoup της Python. Εξάγοντας τα χαρακτηριστικά `href` των ετικετών `<link rel="icon">`, μπορείτε να **extract favicon URLs**, να διαχειριστείτε σχετικές διαδρομές, και ακόμη να ανακτήσετε πολλαπλές μορφές εικονιδίων—όλα σε λίγες δεκάδες γραμμές κώδικα.

Τι ακολουθεί; Δοκιμάστε να κατεβάσετε τα εικονίδια σε τοπικό φάκελο, να δημιουργήσετε ένα CSV αντιστοίχισης domain‑to‑favicon, ή να ενσωματώσετε αυτή τη λογική σε ένα Flask API που σερβίρει favicons κατ’ απαίτηση. Οι δυνατότητες για **fetch website favicon URLs** είναι απεριόριστες, και η βασική τεχνική παραμένει η ίδια.

Έχετε ερωτήσεις για edge cases, ή θέλετε να μοιραστείτε μια έξυπνη τροποποίηση; Αφήστε ένα σχόλιο παρακάτω—καλή αναζήτηση εικονιδίων!

## Τι Θα Μάθετε Στη Στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας projects.

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Load HTML Documents from Stream with Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-stream/)
- [Handle Document Load Events in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/handle-document-load-events/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}