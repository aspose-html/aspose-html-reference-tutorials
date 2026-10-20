---
category: general
date: 2026-06-26
description: Μάθετε πώς να λαμβάνετε το favicon φορτώνοντας HTML από URL και εξάγοντας
  το href από ετικέτες link. Βήμα‑βήμα κώδικας Python για γρήγορη λήψη εικονιδίων
  ιστοσελίδων.
draft: false
keywords:
- how to get favicon
- load html from url
- get website icons
- extract href from link
- how to extract favicons
language: el
og_description: 'Πώς να λάβετε το favicon γρήγορα: φορτώστε το HTML από το URL, βρείτε
  το link rel=''icon'' και εξάγετε το href από τις ετικέτες link χρησιμοποιώντας Python.'
og_title: Πώς να αποκτήσετε Favicon – Εγχειρίδιο Python
schemas:
- author: Aspose
  dateModified: '2026-06-26'
  description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  headline: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  type: TechArticle
- description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  name: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  steps:
  - name: What if the site uses a `<meta>` tag instead of `<link>`?
    text: Some older pages embed the icon URL in a `<meta name="msapplication‑TileImage">`.
      You can extend `find_icon_links` to also search for those meta tags and treat
      them the same way.
  - name: How do I handle relative URLs that start with `//`?
    text: '`urljoin` automatically resolves protocol‑relative URLs (`//example.com/favicon.ico`)
      based on the scheme of the base URL, so you don’t need extra logic.'
  - name: Can I retrieve multiple sizes (e.g., 32×32, 180×180) automatically?
    text: Yes—just drop the `filter_ico_urls` step. The script will return every icon
      URL it discovers, including PNGs of various dimensions. You can then sort or
      select based on the filename pattern.
  - name: Does this work on sites that block bots?
    text: 'If a site returns a 403 or requires a custom User‑Agent, tweak the `requests.get`
      call:'
  type: HowTo
tags:
- Python
- Web Scraping
- HTML Parsing
title: Πώς να αποκτήσετε το Favicon – Πλήρης οδηγός Python για την εξαγωγή εικονιδίων
  ιστοτόπων
url: /el/python/general/how-to-get-favicon-complete-python-guide-for-extracting-site/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Λάβετε Favicon – Πλήρης Οδηγός Python για την Εξαγωγή Εικονιδίων Ιστοσελίδας

Έχετε αναρωτηθεί ποτέ **πώς να λάβετε favicon** από οποιοδήποτε ιστότοπο χωρίς να ψάχνετε χειροκίνητα στον κώδικα της σελίδας; Δεν είστε μόνοι—προγραμματιστές, ειδικοί SEO και ακόμη και σχεδιαστές συχνά χρειάζονται το μικρό εικονίδιο που αντιπροσωπεύει έναν ιστότοπο. Σε αυτό το tutorial θα σας δείξουμε έναν καθαρό, Python‑κεντρικό τρόπο για να φορτώσετε HTML από ένα URL, να εντοπίσετε τις ετικέτες `<link rel="icon">` και να εξάγετε τα URLs των εικονιδίων. Στο τέλος, θα γνωρίζετε ακριβώς **πώς να λάβετε favicon** για οποιονδήποτε τομέα, και θα έχετε ένα επαναχρησιμοποιήσιμο script έτοιμο για τα έργα σας.

Θα καλύψουμε τα πάντα, από την ανάκτηση του HTML μέχρι τη διαχείριση ειδικών περιπτώσεων όπως σχετικές διευθύνσεις URL και πολλαπλές μορφές εικονιδίων. Δεν απαιτούνται εξωτερικές υπηρεσίες—μόνο η τυπική βιβλιοθήκη `requests` και ένας ελαφρύς HTML parser. Έτοιμοι να ξεκινήσετε; Ας βουτήξουμε.

## Προαπαιτούμενα

- Εγκατεστημένο Python 3.8+ (ο κώδικας λειτουργεί επίσης σε 3.10)  
- Βασική εξοικείωση με `requests` και list comprehensions  
- Πρόσβαση στο διαδίκτυο για τον στόχο ιστότοπο  

Αν έχετε ήδη αυτά, υπέροχα—πηδήξτε στο πρώτο βήμα. Διαφορετικά, εγκαταστήστε την μοναδική εξάρτηση που χρειαζόμαστε:

```bash
pip install requests beautifulsoup4
```

> **Pro tip:** `beautifulsoup4` είναι ένας δοκιμασμένος parser που κάνει το “load html from url” παιχνιδάκι.

## Βήμα 1: Φόρτωση HTML από URL με Python  

Το πρώτο πράγμα που πρέπει να κάνετε όταν μαθαίνετε **πώς να λάβετε favicon** είναι να ανακτήσετε την πηγή της σελίδας. Αυτό είναι το τμήμα “load html from url” της διαδικασίας.

```python
import requests
from bs4 import BeautifulSoup

def fetch_html(url: str) -> str:
    """Download the raw HTML of *url* and return it as text."""
    response = requests.get(url, timeout=10)
    response.raise_for_status()   # will raise if the request failed
    return response.text
```

Γιατί να χρησιμοποιήσετε `requests`; Διαχειρίζεται αυτόματα ανακατευθύνσεις, επαλήθευση HTTPS και χρονικά όρια, κάτι που σημαίνει λιγότερες εκπλήξεις όταν αργότερα προσπαθήσετε να **λάβετε εικονίδια ιστοτόπου**.

## Βήμα 2: Ανάλυση του Εγγράφου και Εύρεση Συνδέσμων Εικονιδίων  

Τώρα που έχουμε το HTML, πρέπει να εντοπίσουμε όλα τα στοιχεία `<link>` των οποίων το χαρακτηριστικό `rel` υποδεικνύει εικονίδιο. Αυτό είναι η καρδιά του **πώς να λάβετε favicon**.

```python
def find_icon_links(html: str) -> list[BeautifulSoup]:
    """Return a list of <link> tags that declare an icon."""
    soup = BeautifulSoup(html, "html.parser")
    # Look for rel="icon" or rel="shortcut icon"
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]
```

Παρατηρήστε ότι ελέγχουμε τόσο `icon` όσο και `shortcut icon` επειδή παλαιότεροι ιστότοποι εξακολουθούν να χρησιμοποιούν το δεύτερο. Αυτή η μικρή λεπτομέρεια συχνά προκαλεί σύγχυση όταν κάποιος ψάχνει “how to extract favicons”.

## Βήμα 3: Εξαγωγή href από τα Στοιχεία Link  

Με τις σχετικές ετικέτες στα χέρια, το επόμενο λογικό βήμα—**εξαγωγή href από link**—είναι απλό.

```python
from urllib.parse import urljoin

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    """Convert each <link> tag’s href into a full absolute URL."""
    urls = []
    for tag in link_tags:
        href = tag.get("href")
        if href:
            # Resolve relative URLs against the base page
            full_url = urljoin(base_url, href)
            urls.append(full_url)
    return urls
```

Η χρήση του `urljoin` εγγυάται ότι ακόμη και αν ένας ιστότοπος παρέχει σχετική διαδρομή όπως `/favicon.ico`, θα καταλήξετε με μια σωστή απόλυτη διεύθυνση URL—κρίσιμο για ένα αξιόπιστο script **πώς να λάβετε favicon**.

## Βήμα 4: Προαιρετικό – Επικύρωση και Φιλτράρισμα URLs Εικονιδίων  

Μερικές φορές μια σελίδα καταχωρεί πολλά εικονίδια (Apple touch icons, PNG διαφόρων μεγεθών κ.λπ.). Αν σας ενδιαφέρει μόνο το κλασικό αρχείο `.ico`, φιλτράρετε αναλόγως. Αυτό το βήμα δείχνει **πώς να εξάγετε favicons** συγκεκριμένου τύπου.

```python
def filter_ico_urls(urls: list[str]) -> list[str]:
    """Keep only URLs that end with .ico (case‑insensitive)."""
    return [u for u in urls if u.lower().endswith(".ico")]
```

Αισθανθείτε ελεύθεροι να τροποποιήσετε το φίλτρο: αντικαταστήστε `".ico"` με `".png"` ή ελέγξτε για `rel="apple-touch-icon"` αν χρειάζεστε εικονίδια υψηλής ανάλυσης.

## Βήμα 5: Λήψη των Αρχείων Εικονιδίων (Αν Θέλετε το Πραγματικό Εικόνα)  

Η εξαγωγή των URLs είναι το μισό της μάχης· η λήψη σας δίνει ένα αρχείο που μπορείτε να εμφανίσετε ή να αποθηκεύσετε. Εδώ είναι ένας γρήγορος βοηθός:

```python
import os

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    """Save each icon to *folder*, creating it if necessary."""
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")
```

Η εκτέλεση αυτού μετά τα προηγούμενα βήματα σας δίνει ένα τοπικό αντίγραφο κάθε εντοπισμένου favicon, ιδανικό για caching ή ανάλυση εκτός σύνδεσης.

## Βήμα 6: Συνδυάζοντας Όλα – Πλήρες Παράδειγμα Εργασίας  

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση script που δείχνει **πώς να λάβετε favicon** από οποιονδήποτε ιστότοπο. Αντιγράψτε‑επικολλήστε, αλλάξτε το `target_url`, και παρακολουθήστε το αποτέλεσμα.

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin
import os

def fetch_html(url: str) -> str:
    response = requests.get(url, timeout=10)
    response.raise_for_status()
    return response.text

def find_icon_links(html: str) -> list[BeautifulSoup]:
    soup = BeautifulSoup(html, "html.parser")
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    return [urljoin(base_url, tag.get("href")) for tag in link_tags if tag.get("href")]

def filter_ico_urls(urls: list[str]) -> list[str]:
    return [u for u in urls if u.lower().endswith(".ico")]

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")

def get_favicons(target_url: str) -> None:
    print(f"Fetching HTML from {target_url} …")
    html = fetch_html(target_url)

    print("Finding <link> tags that declare icons …")
    icon_tags = find_icon_links(html)

    print(f"Extracting href attributes – {len(icon_tags)} candidates found.")
    raw_urls = extract_icon_urls(target_url, icon_tags)

    # Optional filtering – keep only .ico files
    ico_urls = filter_ico_urls(raw_urls)
    print(f"Filtered to {len(ico_urls)} .ico URLs:", ico_urls)

    if ico_urls:
        download_icons(ico_urls)
    else:
        print("No .ico favicons detected; here are all discovered URLs:")
        print(raw_urls)

# Example usage – replace with any site you want to test
if __name__ == "__main__":
    target_url = "https://www.python.org"
    get_favicons(target_url)
```

**Αναμενόμενο αποτέλεσμα (κομμένο για συντομία):**

```
Fetching HTML from https://www.python.org …
Finding <link> tags that declare icons …
Extracting href attributes – 3 candidates found.
Filtered to 1 .ico URLs: ['https://www.python.org/static/favicon.ico']
Saved favicons/favicon.ico
```

Αν ο ιστότοπος παρέχει μόνο PNG ή Apple touch icons, το script θα εμφανίσει αυτές τις διευθύνσεις URL, δείχνοντάς σας ακριβώς **πώς να λάβετε favicon** σε κάθε σενάριο.

## Συχνές Ερωτήσεις & Ειδικές Περιπτώσεις  

### Τι γίνεται αν ο ιστότοπος χρησιμοποιεί ετικέτα `<meta>` αντί για `<link>`;  
Ορισμένες παλαιότερες σελίδες ενσωματώνουν τη διεύθυνση του εικονιδίου σε μια ετικέτα `<meta name="msapplication‑TileImage">`. Μπορείτε να επεκτείνετε τη `find_icon_links` ώστε να ψάχνει και αυτές τις meta ετικέτες και να τις αντιμετωπίζει με τον ίδιο τρόπο.

### Πώς να διαχειριστώ σχετικές διευθύνσεις URL που ξεκινούν με `//`;  
Το `urljoin` επιλύει αυτόματα τις διευθύνσεις URL σχετικές με το πρωτόκολλο (`//example.com/favicon.ico`) βάσει του σχήματος της βασικής διεύθυνσης, οπότε δεν χρειάζεται επιπλέον λογική.

### Μπορώ να ανακτήσω αυτόματα πολλαπλά μεγέθη (π.χ., 32×32, 180×180);  
Ναι—απλώς παραλείψτε το βήμα `filter_ico_urls`. Το script θα επιστρέψει κάθε URL εικονιδίου που εντοπίζει, συμπεριλαμβανομένων PNG διαφόρων διαστάσεων. Μπορείτε στη συνέχεια να ταξινομήσετε ή να επιλέξετε βάσει του προτύπου ονόματος αρχείου.

### Λειτουργεί αυτό σε ιστότοπους που μπλοκάρουν bots;  
Αν ένας ιστότοπος επιστρέφει 403 ή απαιτεί προσαρμοσμένο User‑Agent, τροποποιήστε την κλήση `requests.get`:

```python
headers = {"User-Agent": "Mozilla/5.0 (compatible; FaviconBot/1.0)"}
response = requests.get(url, headers=headers, timeout=10)
```

Αυτή η μικρή αλλαγή συχνά λύνει το “πώς να λάβετε favicon” σε πιο αυστηρούς τομείς.

## Οπτική Επισκόπηση  

![Διάγραμμα που δείχνει τη ροή του πώς να λάβετε favicon από έναν ιστότοπο – φόρτωση HTML, ανάλυση ετικετών link, εξαγωγή href, προαιρετική λήψη](how-to-get-favicon-diagram.png "how to get favicon flow diagram")

*Το alt κείμενο της εικόνας περιέχει τη βασική λέξη‑κλειδί, ικανοποιώντας το SEO για εικόνες.*

## Συμπέρασμα  

Διασχίσαμε βήμα‑βήμα το **πώς να λάβετε favicon**: φόρτωση HTML από ένα URL,

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Αποθηκεύσετε HTML σε C# – Πλήρης Οδηγός Χρησιμοποιώντας έναν Προσαρμοσμένο Διαχειριστή Πόρων](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Πώς να Επεξεργαστείτε HTML Χρησιμοποιώντας Aspose.HTML για Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Πώς να Μετατρέψετε HTML σε PDF με Java – Χρησιμοποιώντας Aspose.HTML για Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}