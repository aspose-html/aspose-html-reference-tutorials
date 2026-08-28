---
category: general
date: 2026-07-02
description: Μάθετε πώς να φορτώνετε HTML στην Python, να παίρνετε στοιχείο με id
  και να εξάγετε κείμενο από ένα αρχείο. Αυτό το πρακτικό μάθημα δείχνει πώς να διαβάζετε
  αρχεία HTML με το BeautifulSoup.
draft: false
keywords:
- how to load html
- how to get element
- how to extract text
- get element by id
- read html file python
language: el
og_description: Πώς να φορτώσετε HTML σε Python και να εξάγετε κείμενο χρησιμοποιώντας
  το BeautifulSoup. Ακολουθήστε τον οδηγό για να διαβάσετε ένα αρχείο HTML, να λάβετε
  το στοιχείο με το id και να εκτυπώσετε το περιεχόμενό του.
og_title: Πώς να φορτώσετε HTML στην Python – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Learn how to load HTML in Python, get element by id, and extract text
    from a file. This practical tutorial shows reading HTML files with BeautifulSoup.
  headline: How to Load HTML in Python – Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to load HTML in Python, get element by id, and extract text
    from a file. This practical tutorial shows reading HTML files with BeautifulSoup.
  name: How to Load HTML in Python – Step‑by‑Step Guide
  steps:
  - name: What if the HTML is malformed?
    text: BeautifulSoup’s `lxml` parser is forgiving, but for severely broken markup
      you might want to fallback to the built‑in `html.parser`. Swap `"lxml"` with
      `"html.parser"` in the `BeautifulSoup` constructor.
  - name: How to handle multiple elements with the same ID?
    text: HTML spec says IDs should be unique, but reality sometimes disagrees. Use
      `soup.find_all(id="duplicate-id")` to retrieve a list, then iterate over it.
  - name: Need to read from a URL instead of a file?
    text: Replace the file‑reading logic with `requests.get(url).text`. Remember to
      install the `requests` package (`pip install requests`) and handle network errors
      gracefully.
  - name: Want to extract other attributes (e.g., `class` or `href`)?
    text: 'Simply access them like a dictionary: `header[''class'']` or `header[''href'']`.
      If the attribute might be missing, use `.get(''class'')` to avoid `KeyError`.'
  type: HowTo
tags:
- Python
- HTML parsing
- BeautifulSoup
title: Πώς να φορτώσετε HTML στην Python – Οδηγός βήμα‑βήμα
url: /el/python/general/how-to-load-html-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Φορτώσετε HTML σε Python – Πλήρης Οδηγός

Σας έχει τύχει ποτέ να αναρωτιέστε **πώς να φορτώσετε HTML** σε ένα script Python χωρίς να τριβάτε το κεφάλι σας; Δεν είστε μόνοι. Είτε κάνετε scraping σε ένα ειδησεογραφικό site, επεξεργάζεστε μια τοπική αναφορά, είτε απλώς χρειάζεστε να εξάγετε έναν τίτλο από ένα πρότυπο email, η κατάκτηση της τέχνης του φόρτωσης HTML είναι μια απαραίτητη δεξιότητα για κάθε προγραμματιστή.

Σε αυτόν τον οδηγό θα περάσουμε από **πώς να βρούμε ένα στοιχείο** με το ID του, **πώς να εξάγουμε κείμενο**, και τέλος θα εκτυπώσουμε το αποτέλεσμα—όλα ενώ διατηρούμε τον κώδικα καθαρό και Pythonic. Θα καλύψουμε επίσης τις λεπτομέρειες του **διαβάσματος ενός αρχείου HTML σε Python**, ώστε να μπορείτε να αντιγράψετε‑επικολλήσετε μια λειτουργική λύση αμέσως.

> **Συμβουλή:** Το παράδειγμα χρησιμοποιεί τη δημοφιλή βιβλιοθήκη *BeautifulSoup* επειδή είναι ελαφριά, καλά τεκμηριωμένη και λειτουργεί τόσο με απλές όσο και με σύνθετες δομές HTML.

## Τι Θα Χρειαστείτε

- Python 3.9 ή νεότερο (ο κώδικας λειτουργεί επίσης σε 3.10+)
- `beautifulsoup4` και `lxml` εγκατεστημένα (`pip install beautifulsoup4 lxml`)
- Ένα δείγμα αρχείου HTML – θα το ονομάσουμε `sample.html` και θα το τοποθετήσουμε σε φάκελο με όνομα `YOUR_DIRECTORY`

Αυτό είναι όλο. Χωρίς βαρύτατους browsers, χωρίς Selenium, μόνο καθαρό Python.

## Βήμα 1: Πώς να Φορτώσετε HTML – Διαβάστε το Αρχείο στη Μνήμη

Το πρώτο πράγμα που πρέπει να κάνετε είναι **να διαβάσετε το αρχείο HTML** από το δίσκο. Αυτό είναι το θεμέλιο κάθε επόμενου βήματος, οπότε ας το κάνουμε σωστά.

```python
from pathlib import Path

# Define the path to the HTML file
html_path = Path("YOUR_DIRECTORY/sample.html")

# Read the file contents as a string
html_content = html_path.read_text(encoding="utf-8")
```

*Γιατί είναι σημαντικό:* Η χρήση του `Path.read_text` αφαιρεί τις εξαρτήσεις από τα ειδικά line endings του λειτουργικού συστήματος και διαχειρίζεται αυτόματα το UTF‑8, που είναι η κυρίαρχη κωδικοποίηση για σύγχρονες ιστοσελίδες. Αν το αρχείο λείπει, το `Path.read_text` θα ρίξει ένα σαφές `FileNotFoundError`, κάνοντας τον εντοπισμό σφαλμάτων άκοπο.

## Βήμα 2: Αναλύστε το Έγγραφο HTML

Τώρα που έχουμε μια ακατέργαστη συμβολοσειρά, χρειάζεται να **φορτώσουμε το HTML** σε ένα αντικείμενο parser. Το BeautifulSoup μας παρέχει ένα βολικό API για την πλοήγηση στο DOM.

```python
from bs4 import BeautifulSoup

# Create a BeautifulSoup object using the lxml parser (fast and reliable)
soup = BeautifulSoup(html_content, "lxml")
```

*Γιατί lxml;* Ο parser `lxml` είναι σημαντικά πιο γρήγορος από τον ενσωματωμένο parser της Python και διαχειρίζεται πιο ευγενικά εσφαλμένο markup—ιδανικός για πραγματικό HTML που μπορεί να κάνετε scraping.

## Βήμα 3: Βρείτε Στοιχείο με ID – Εντοπίστε την Επικεφαλίδα

Με το έγγραφο αναλυμένο, ας απαντήσουμε στην ερώτηση **πώς να βρούμε ένα στοιχείο** με συγκεκριμένο ID. Στο παράδειγμά μας ψάχνουμε για ένα tag `<h1>` του οποίου το χαρακτηριστικό `id` είναι ίσο με `"main-header"`.

```python
# Retrieve the element with the specific ID
header = soup.find(id="main-header")
```

Αν το στοιχείο δεν βρεθεί, το `header` θα είναι `None`. Είναι καλή πρακτική να το προστατεύετε:

```python
if header is None:
    raise ValueError("Element with id='main-header' not found in the HTML file.")
```

## Βήμα 4: Πώς να Εξάγετε Κείμενο – Αποκτήστε το Εσωτερικό Περιεχόμενο

Τώρα που έχουμε το στοιχείο, η εξαγωγή του κειμενικού του περιεχομένου είναι παιχνιδάκι. Αυτό απαντά στο **πώς να εξάγετε κείμενο** από ένα tag.

```python
# Extract the visible text inside the element
header_text = header.get_text(strip=True)  # strip removes surrounding whitespace
```

Η `get_text` συνενώνει αυτόματα τυχόν ένθετα κείμενα, έτσι δεν χρειάζεται να κάνετε βρόχο στα παιδιά χειροκίνητα. Η σημαία `strip=True` αφαιρεί χαρακτήρες νέας γραμμής και κενά, δίνοντάς σας μια καθαρή συμβολοσειρά.

## Βήμα 5: Εκτυπώστε το Αποτέλεσμα – Επαληθεύστε Ότι Λειτουργεί

Τέλος, ας εμφανίσουμε την τιμή στην κονσόλα. Αυτό αντικατοπτρίζει τη γραμμή `print(header.text_content)` στο αρχικό απόσπασμα.

```python
print(header_text)  # prints: The text inside <h1 id="main-header">
```

Αν εκτελέσετε το script και δείτε τον αναμενόμενο τίτλο, συγχαρητήρια—έχετε επιτυχώς **διαβάσει ένα αρχείο HTML σε Python**, εντοπίσει ένα στοιχείο με ID, και εξάγει το κείμενό του.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση script. Αντιγράψτε το σε ένα αρχείο με όνομα `extract_header.py` και εκτελέστε `python extract_header.py`.

```python
# extract_header.py
from pathlib import Path
from bs4 import BeautifulSoup

def load_html(file_path: str) -> str:
    """Read an HTML file and return its contents as a string."""
    path = Path(file_path)
    if not path.is_file():
        raise FileNotFoundError(f"Unable to locate the file: {file_path}")
    return path.read_text(encoding="utf-8")

def get_element_by_id(soup: BeautifulSoup, element_id: str):
    """Return the first tag with the given id, or raise an informative error."""
    element = soup.find(id=element_id)
    if element is None:
        raise ValueError(f"Element with id='{element_id}' not found.")
    return element

def main():
    # Step 1: Load the HTML document
    html = load_html("YOUR_DIRECTORY/sample.html")
    
    # Step 2: Parse the HTML with BeautifulSoup
    soup = BeautifulSoup(html, "lxml")
    
    # Step 3: Retrieve the element by its ID
    header = get_element_by_id(soup, "main-header")
    
    # Step 4: Extract and print the text content
    print(header.get_text(strip=True))

if __name__ == "__main__":
    main()
```

**Αναμενόμενο αποτέλεσμα** (υποθέτοντας ότι το `sample.html` περιέχει `<h1 id="main-header">Welcome to My Site</h1>`):

```
Welcome to My Site
```

Αυτό είναι—ένα script, χωρίς επιπλέον εξαρτήσεις πέρα από το BeautifulSoup και το lxml.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν το HTML είναι κατεστραμμένο;

Ο parser `lxml` του BeautifulSoup είναι ανεκτικός, αλλά για σοβαρά κατεστραμμένο markup ίσως θέλετε να επιστρέψετε στον ενσωματωμένο `html.parser`. Αντικαταστήστε το `"lxml"` με το `"html.parser"` στον κατασκευαστή `BeautifulSoup`.

### Πώς να διαχειριστείτε πολλαπλά στοιχεία με το ίδιο ID;

Η προδιαγραφή HTML λέει ότι τα IDs πρέπει να είναι μοναδικά, αλλά στην πράξη συμβαίνει διαφορετικά. Χρησιμοποιήστε `soup.find_all(id="duplicate-id")` για να λάβετε μια λίστα, και μετά κάντε επανάληψη πάνω της.

### Χρειάζεστε ανάγνωση από URL αντί για αρχείο;

Αντικαταστήστε τη λογική ανάγνωσης αρχείου με `requests.get(url).text`. Θυμηθείτε να εγκαταστήσετε το πακέτο `requests` (`pip install requests`) και να διαχειρίζεστε τα σφάλματα δικτύου με προσοχή.

### Θέλετε να εξάγετε άλλα χαρακτηριστικά (π.χ., `class` ή `href`);

Απλώς προσπελάστε τα όπως ένα λεξικό: `header['class']` ή `header['href']`. Αν το χαρακτηριστικό μπορεί να λείπει, χρησιμοποιήστε `.get('class')` για να αποφύγετε το `KeyError`.

## Οπτική Σύνοψη

![πώς να φορτώσετε html παράδειγμα](https://example.com/placeholder-image.png "πώς να φορτώσετε html παράδειγμα")

*Κείμενο alt:* πώς να φορτώσετε html παράδειγμα – ένα διάγραμμα που δείχνει τη ροή από την ανάγνωση αρχείου έως την εξαγωγή κειμένου.

## Ανακεφαλαίωση

Καλύψαμε **πώς να φορτώσετε HTML** σε Python, δείξαμε **πώς να βρείτε ένα στοιχείο** με το ID του, και παρουσιάσαμε **πώς να εξάγετε κείμενο** από αυτό το στοιχείο. Ακολουθώντας τα παραπάνω βήματα μπορείτε αξιόπιστα **να διαβάσετε ένα αρχείο HTML σε Python**, να χειριστείτε το DOM, και να εξάγετε ακριβώς ό,τι χρειάζεστε.

## Τι Ακολουθεί;

- **Εξερευνήστε CSS selectors:** Χρησιμοποιήστε `soup.select_one('.my-class')` για πιο ευέλικτα ερωτήματα.
- **Scrape πολλαπλές σελίδες:** Συνδυάστε αυτό το μοτίβο με `requests` και έναν βρόχο για μαζική επεξεργασία ιστοτόπων.
- **Γράψτε πίσω σε HTML:** Το BeautifulSoup σας επιτρέπει επίσης να τροποποιήσετε το δέντρο και να αποθηκεύσετε αλλαγές—χρήσιμο για εργασίες templating.
- **Βελτιστοποίηση απόδοσης:** Για τεράστια αρχεία, σκεφτείτε streaming parsers όπως το `lxml.etree.iterparse`.

Μη διστάσετε να πειραματιστείτε—αλλάξτε το ID, δοκιμάστε διαφορετικά tags, ή ακόμη και μεταβείτε στο `xml.etree.ElementTree` αν δουλεύετε με XHTML. Οι έννοιες παραμένουν οι ίδιες, και τώρα έχετε μια σταθερή βάση για οποιαδήποτε περιπέτεια ανάλυσης HTML.

Καλό κώδικα! Αν αντιμετωπίσετε πρόβλημα ή έχετε ένα ενδιαφέρον use‑case να μοιραστείτε, αφήστε ένα σχόλιο παρακάτω.

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}