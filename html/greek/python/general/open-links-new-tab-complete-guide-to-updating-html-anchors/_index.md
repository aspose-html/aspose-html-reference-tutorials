---
category: general
date: 2026-07-05
description: Άνοιγμα συνδέσμων σε νέα καρτέλα με Python – μάθετε πώς να προσθέσετε
  target="_blank", να αλλάξετε τον προορισμό του συνδέσμου, να χρησιμοποιήσετε επιλογέα
  attribute contains και να αποθηκεύσετε το τροποποιημένο HTML χωρίς κόπο.
draft: false
keywords:
- open links new tab
- add target blank
- change link target
- attribute contains selector
- save modified html
language: el
og_description: Άνοιγμα συνδέσμων σε νέα καρτέλα γρήγορα. Αυτό το σεμινάριο δείχνει
  πώς να προσθέσετε target='_blank', να αλλάξετε τον προορισμό του συνδέσμου και να
  αποθηκεύσετε το τροποποιημένο HTML με Python.
og_title: Άνοιγμα Συνδέσμων σε Νέα Καρτέλα – Οδηγός Ενημέρωσης HTML βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  headline: Open Links New Tab – Complete Guide to Updating HTML Anchors
  type: TechArticle
- description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  name: Open Links New Tab – Complete Guide to Updating HTML Anchors
  steps:
  - name: Expected Result
    text: 'Suppose `links.html` originally contained:'
  - name: What if a link already has a `rel` attribute?
    text: 'Our loop overwrites it with `"noopener"`. If you need to preserve existing
      values (e.g., `"nofollow"`), concatenate instead:'
  - name: How to handle multiple domains?
    text: 'Just expand the selector list:'
  - name: Does `prettify()` change the original HTML structure?
    text: It re‑indents but doesn’t alter tag order or attribute values. If you must
      keep the exact original whitespace, replace `prettify()` with `str(soup)` as
      mentioned earlier.
  type: HowTo
tags:
- HTML manipulation
- Python
- web automation
title: Άνοιγμα συνδέσμων σε νέα καρτέλα – Πλήρης οδηγός για την ενημέρωση των HTML
  άγκυρων
url: /el/python/general/open-links-new-tab-complete-guide-to-updating-html-anchors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Άνοιγμα Συνδέσμων σε Νέα Καρτέλα – Πλήρης Οδηγός για την Ενημέρωση των Άγκυρων HTML

Ποτέ χρειάστηκε να **ανοίξετε συνδέσμους σε νέα καρτέλα** σε μια στατική σελίδα HTML αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είσαι μόνος. Πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν καθαρίζουν παλιές ιστοσελίδες ή προσθέτουν βελτιώσεις προσβασιμότητας. Σε αυτό το tutorial θα περάσουμε από μια πρακτική λύση που **προσθέτει target blank**, **αλλάζει το στόχο του συνδέσμου**, και αποθηκεύει με ασφάλεια **το τροποποιημένο html**—όλα με λίγες γραμμές Python.

Θα καλύψουμε επίσης πώς να χρησιμοποιήσετε έναν **attribute contains selector** ώστε να επηρεάσετε μόνο τις άγκυρες που πραγματικά σας ενδιαφέρουν (για παράδειγμα, κάθε σύνδεσμος που οδηγεί στο *example.com*). Στο τέλος, θα έχετε ένα επαναχρησιμοποιήσιμο script που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο, μικρό ή μεγάλο.

## Τι Θα Μάθετε

- Φόρτωση ενός αρχείου HTML σε ένα αντικείμενο εγγράφου που μπορεί να τροποποιηθεί.  
- Επιλογή στοιχείων `<a>` των οποίων το χαρακτηριστικό `href` περιέχει ένα συγκεκριμένο υποσυμβολοσειρά.  
- **Προσθήκη target blank** και ορισμός του χαρακτηριστικού `rel="noopener"` για βελτιωμένη ασφάλεια.  
- **Αποθήκευση τροποποιημένου html** πίσω στο δίσκο χωρίς να χάσετε τη μορφοποίηση.  

Καμία εξωτερική εξάρτηση πέρα από τη βιβλιοθήκη της Python και το **beautifulsoup4** (μια μικρή εγκατάσταση). Αν ήδη χρησιμοποιείτε διαφορετικό parser, οι έννοιες μεταφράζονται άμεσα.

---

## Προαπαιτούμενα

- Python 3.8+ εγκατεστημένο στο σύστημά σας.  
- Βασική εξοικείωση με HTML και Python.  
- Πακέτο `beautifulsoup4` (`pip install beautifulsoup4`).  

Αυτό είναι όλο—δεν απαιτούνται βαριές πλατφόρμες.

---

## Βήμα 1: Φόρτωση του Εγγράφου HTML

Πρώτα απ' όλα: πρέπει να διαβάσουμε το αρχείο προέλευσης και να το περάσουμε στο BeautifulSoup. Σκεφτείτε το ως το άνοιγμα ενός κεννού καμβά όπου μπορείτε να προσθέσετε νέα χαρακτηριστικά.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Path to the original HTML file
html_path = Path("YOUR_DIRECTORY/links.html")

# Read the file content
with html_path.open(encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")
```

> **Γιατί είναι σημαντικό:** Η χρήση του `Path` κρατά τον κώδικα ανεξάρτητο από το λειτουργικό σύστημα, και το `html.parser` είναι ενσωματωμένο, οπότε δεν χρειάζεστε επιπλέον parsers για απλές εργασίες.

---

## Βήμα 2: Χρήση Attribute Contains Selector για να Βρείτε τα Σωστά Links

Θέλουμε να επηρεάσουμε μόνο τις άγκυρες που οδηγούν στο *example.com*. Ο CSS selector `a[href*='example.com']` κάνει ακριβώς αυτό—`*=` σημαίνει “περιέχει”. Η μέθοδος `select` του BeautifulSoup καταλαβαίνει αυτή τη σύνταξη.

```python
# Find all <a> tags whose href contains 'example.com'
selector = "a[href*='example.com']"
anchor_elements = soup.select(selector)
```

> **Pro tip:** Αν χρειάζεστε αναζήτηση χωρίς διάκριση πεζών‑κεφαλαίων, χρησιμοποιήστε έναν μικρό βρόχο που ελέγχει `if 'example.com' in a.get('href', '').lower()`.

Τώρα το `anchor_elements` περιέχει κάθε σύνδεσμο που μας ενδιαφέρει, έτοιμο για την επόμενη μετατροπή.

---

## Βήμα 3: Αλλαγή Στόχου Συνδέσμου – Προσθήκη Target Blank και Ασφάλιση του Συνδέσμου

Το άνοιγμα ενός συνδέσμου σε νέα καρτέλα είναι τόσο απλό όσο το `target="_blank"`. Ωστόσο, οι σύγχρονοι browsers συνιστούν επίσης την προσθήκη `rel="noopener"` (ή `noreferrer`) για να αποτρέψουν τη νέα σελίδα από το να έχει πρόσβαση στο αρχικό παράθυρο μέσω `window.opener`. Αυτή η μικρή βελτίωση ασφαλείας μπορεί να σταματήσει επιθέσεις phishing.

```python
for anchor in anchor_elements:
    # Open in a new tab
    anchor['target'] = "_blank"          # add target blank
    # Harden security
    anchor['rel'] = "noopener"           # prevent access to the opener page
```

> **Γιατί χρησιμοποιούμε άμεση ανάθεση λεξικού:** Δημιουργεί αυτόματα το χαρακτηριστικό αν λείπει, και το αντικαθιστά αν υπάρχει ήδη—ιδανικό για μια λειτουργία **αλλαγής στόχου συνδέσμου**.

---

## Βήμα 4: Αποθήκευση Τροποποιημένου HTML Πίσω στο Δίσκο

Το τελευταίο βήμα είναι η εγγραφή του ενημερωμένου markup σε νέο αρχείο. Κρατώντας το αρχικό ανέγγιχτο, μπορείτε να επαναφέρετε την κατάσταση αν κάτι πάει στραβά.

```python
# Destination path for the updated HTML
output_path = Path("YOUR_DIRECTORY/links-updated.html")

# Write the prettified HTML (preserves indentation)
with output_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())
```

> **Τι κάνει το `prettify()`:** Μορφοποιεί το HTML με ωραία εσοχή, κάνοντας το αποθηκευμένο αρχείο πιο ευανάγνωστο και εύκολο στη σύγκριση (diff). Αν προτιμάτε το αρχικό whitespace, αντικαταστήστε το `prettify()` με `str(soup)`.

---

## Πλήρες Script – Λύση Ένα‑Κλικ

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση script. Αποθηκεύστε το ως `update_links.py` και τρέξτε `python update_links.py` από το τερματικό σας.

```python
#!/usr/bin/env python3
"""
Open Links New Tab – script that adds target blank,
sets rel="noopener", and saves modified html.
"""

from pathlib import Path
from bs4 import BeautifulSoup

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Load the HTML document
    # ------------------------------------------------------------------
    html_path = Path("YOUR_DIRECTORY/links.html")
    with html_path.open(encoding="utf-8") as f:
        soup = BeautifulSoup(f, "html.parser")

    # ------------------------------------------------------------------
    # 2️⃣ Select anchors with an attribute contains selector
    # ------------------------------------------------------------------
    selector = "a[href*='example.com']"
    anchors = soup.select(selector)

    # ------------------------------------------------------------------
    # 3️⃣ Change link target – add target blank & secure the link
    # ------------------------------------------------------------------
    for a in anchors:
        a['target'] = "_blank"          # add target blank
        a['rel'] = "noopener"           # prevent opener access

    # ------------------------------------------------------------------
    # 4️⃣ Save modified html to a new file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/links-updated.html")
    with output_path.open("w", encoding="utf-8") as f:
        f.write(soup.prettify())

    print(f"✅ Updated {len(anchors)} link(s) and saved to {output_path}")

if __name__ == "__main__":
    main()
```

### Αναμενόμενο Αποτέλεσμα

Ας υποθέσουμε ότι το `links.html` περιείχε αρχικά:

```html
<a href="https://example.com/page1">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Μετά την εκτέλεση του script, το `links-updated.html` θα φαίνεται ως εξής:

```html
<a href="https://example.com/page1" target="_blank" rel="noopener">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Μόνο ο σύνδεσμος προς *example.com* έλαβε τα χαρακτηριστικά **add target blank**, δείχνοντας ότι ο **attribute contains selector** μας λειτούργησε ακριβώς όπως αναμενόταν.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν ένας σύνδεσμος έχει ήδη χαρακτηριστικό `rel`;

Ο βρόχος μας το αντικαθιστά με `"noopener"`. Αν χρειάζεται να διατηρήσετε υπάρχουσες τιμές (π.χ., `"nofollow"`), συνδυάστε τις:

```python
existing = a.get('rel', '')
a['rel'] = f"{existing} noopener".strip()
```

### Πώς να διαχειριστείτε πολλαπλούς τομείς;

Απλώς επεκτείνετε τη λίστα selectors:

```python
domains = ["example.com", "sample.org"]
selector = ",".join([f"a[href*='{d}']" for d in domains])
anchors = soup.select(selector)
```

### Το `prettify()` αλλάζει τη δομή του αρχικού HTML;

Αναδιατάσσει μόνο την εσοχή, χωρίς να αλλάξει τη σειρά των ετικετών ή τις τιμές των χαρακτηριστικών. Αν πρέπει να διατηρήσετε ακριβώς το αρχικό whitespace, αντικαταστήστε το `prettify()` με `str(soup)` όπως αναφέρθηκε παραπάνω.

---

## Pro Tips για Σκριπτά Έτοιμα για Παραγωγή

- **Δημιουργία αντιγράφου πριν την αντικατάσταση:** Προσθέστε βήμα αντιγραφής (`shutil.copy`) για να κρατήσετε το αρχικό αρχείο ασφαλές.  
- **Καταγραφή αντί για print:** Χρησιμοποιήστε το module `logging` για έργα που κλιμακώνουν.  
- **Επεξεργασία παρτίδας:** Περάστε έναν φάκελο με `Path.rglob("*.html")` για να ενημερώσετε πολλά αρχεία σε μία εκτέλεση.  

Αυτές οι βελτιώσεις μετατρέπουν ένα απλό script **open links new tab** σε ένα ισχυρό εργαλείο για οποιοδήποτε workflow συντήρησης ιστοσελίδων.

---

## Συμπέρασμα

Τώρα έχετε μια σταθερή, επαναχρησιμοποιήσιμη μέθοδο για **open links new tab** σε οποιαδήποτε συλλογή στατικών HTML. Χρησιμοποιώντας έναν **attribute contains selector**, μπορείτε να **change link target** ακριβώς όπου χρειάζεται, **add target blank**, και **save modified html** χωρίς να χάσετε τη μορφοποίηση. 

Δοκιμάστε το σε μια δοκιμαστική σελίδα, έπειτα κλιμακώστε το σε ολόκληρο τον ιστότοπό σας. Χρειάζεται να προσαρμόσετε τον selector για PDFs, εικόνες ή άλλους τομείς; Απλώς αλλάξτε τη συμβολοσειρά CSS—τα υπόλοιπα παραμένουν ίδια.

Αφήστε ένα σχόλιο αν αντιμετωπίσετε δυσκολίες, ή μοιραστείτε πώς επεκτείνατε το script για τα δικά σας έργα. Καλό κώδικα, και να ανοίγουν όλες οι άγκυρες ακριβώς εκεί που θέλετε!

## Τι Θα Μάθετε Στη Σειρά Επόμενη;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}