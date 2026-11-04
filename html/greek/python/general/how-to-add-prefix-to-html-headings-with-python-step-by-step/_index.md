---
category: general
date: 2026-06-07
description: Πώς να προσθέσετε πρόθεμα σε επικεφαλίδες HTML χρησιμοποιώντας Python.
  Μάθετε πώς να επιλέγετε πολλαπλές επικεφαλίδες, να αλλάζετε τους τίτλους HTML και
  να αποθηκεύετε το τροποποιημένο HTML αποδοτικά.
draft: false
keywords:
- how to add prefix
- select multiple headings
- save modified html
- change html titles
- modify html with python
language: el
og_description: Πώς να προσθέσετε πρόθεμα σε επικεφαλίδες HTML χρησιμοποιώντας Python.
  Αυτό το σεμινάριο δείχνει πώς να επιλέξετε πολλαπλές επικεφαλίδες, να αλλάξετε τους
  τίτλους HTML και να αποθηκεύσετε το τροποποιημένο HTML σε λίγες μόνο γραμμές.
og_title: Πώς να προσθέσετε πρόθεμα σε τίτλους HTML με Python – Σύντομος οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-07'
  description: How to add prefix to HTML headings using Python. Learn to select multiple
    headings, change HTML titles, and save modified HTML efficiently.
  headline: How to Add Prefix to HTML Headings with Python – Step‑by‑Step Guide
  type: TechArticle
- description: How to add prefix to HTML headings using Python. Learn to select multiple
    headings, change HTML titles, and save modified HTML efficiently.
  name: How to Add Prefix to HTML Headings with Python – Step‑by‑Step Guide
  steps:
  - name: Verify the changes in a diff tool.
    text: Verify the changes in a diff tool.
  - name: Roll back instantly if something looks off.
    text: Roll back instantly if something looks off.
  - name: Keep the original untouched for audit purposes.
    text: Keep the original untouched for audit purposes.
  type: HowTo
tags:
- Python
- HTML
- Automation
- Web Scraping
title: Πώς να προσθέσετε πρόθεμα σε επικεφαλίδες HTML με Python – Οδηγός βήμα‑προς‑βήμα
url: /el/python/general/how-to-add-prefix-to-html-headings-with-python-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Προσθέσετε Πρόθεμα σε HTML Επικεφαλίδες με Python – Πλήρης Οδηγός

Το πώς να προσθέσετε πρόθεμα σε HTML επικεφαλίδες χρησιμοποιώντας Python είναι μια συχνή ανάγκη όταν διαχειρίζεστε έναν ιστότοπο που λαμβάνει συχνές ενημερώσεις. Σε αυτόν τον οδηγό θα δούμε πώς να επιλέγουμε πολλαπλές επικεφαλίδες, να αλλάζουμε τους τίτλους HTML και να αποθηκεύουμε το τροποποιημένο HTML—όλα χωρίς να αφήσετε τον επεξεργαστή σας.

Αν έχετε ποτέ αναρωτηθεί αν μπορείτε να αυτοματοποιήσετε το σήμα “σημειωμένο ως ενημερωμένο” σε δεκάδες σελίδες, βρίσκεστε στο σωστό μέρος. Θα αγγίξουμε επίσης πώς να **modify html with python** με τρόπο που κλιμακώνεται, ώστε να μην χρειάζεται να ανοίγετε κάθε αρχείο χειροκίνητα.

## Τι Θα Επιτύχετε

Στο τέλος αυτού του σεμιναρίου θα μπορείτε:

* **Να επιλέγετε πολλαπλές επικεφαλίδες** (`h1`, `h2`, `h3`) σε μία μόνο εκτέλεση.  
* **Να προσθέτετε προσαρμοσμένο πρόθεμα** (π.χ., `[Updated]`) σε κάθε κείμενο επικεφαλίδας.  
* **Να αποθηκεύετε το τροποποιημένο html** ξανά στο δίσκο, διατηρώντας την αρχική δομή αρχείων.  
* Να κατανοείτε τις ανταλλαγές μεταξύ διαφορετικών Python HTML parser και να επιλέγετε αυτόν που ταιριάζει στο έργο σας.

Καμία εξωτερική υπηρεσία, κανένα βαρύ framework—μόνο καθαρό Python και μερικές καλά συντηρημένες βιβλιοθήκες.

---

## Πώς να Προσθέσετε Πρόθεμα στο Κείμενο της Επικεφαλίδας με Python

Παρακάτω υπάρχει ένα ελάχιστο, εκτελέσιμο παράδειγμα που δείχνει την κύρια ιδέα. Χρησιμοποιεί τη βιβλιοθήκη **`lxml`** μαζί με **`cssselect`** για υποστήριξη selector, που αντικατοπτρίζει τη μέθοδο `query_selector_all` που είδατε στο αρχικό απόσπασμα.

```python
# -------------------------------------------------
# Step 0: Install dependencies (run once)
# -------------------------------------------------
# pip install lxml cssselect

# -------------------------------------------------
# Step 1: Load the HTML document
# -------------------------------------------------
from lxml import html

# Replace with your actual file path
input_path = "YOUR_DIRECTORY/article.html"
with open(input_path, "r", encoding="utf-8") as f:
    doc = html.fromstring(f.read())

# -------------------------------------------------
# Step 2: Select multiple headings (h1, h2, h3)
# -------------------------------------------------
# The CSS selector "h1, h2, h3" grabs all three levels.
headings = doc.cssselect("h1, h2, h3")

# -------------------------------------------------
# Step 3: Add the prefix "[Updated] " to each heading
# -------------------------------------------------
prefix = "[Updated] "
for heading in headings:
    # Preserve existing whitespace but prepend our tag
    heading.text = f"{prefix}{heading.text_content().strip()}"

# -------------------------------------------------
# Step 4: Save the modified HTML
# -------------------------------------------------
output_path = "YOUR_DIRECTORY/article_updated.html"
with open(output_path, "w", encoding="utf-8") as f:
    f.write(html.tostring(doc, pretty_print=True, encoding="unicode"))

print(f"✅ Finished! Modified file saved to {output_path}")
```

**Αναμενόμενο αποτέλεσμα** (απόσπασμα του `article_updated.html`):

```html
<h1>[Updated] Introduction to Machine Learning</h1>
<h2>[Updated] Data Pre‑processing Steps</h2>
<h3>[Updated] Feature Engineering Techniques</h3>
```

Παρατηρήστε πώς κάθε επικεφαλίδα τώρα ξεκινά με την ετικέτα `[Updated]`—ακριβώς αυτό που θέλαμε όταν ρωτήσαμε **how to add prefix** στους τίτλους μας.

### Γιατί Λειτουργεί Αυτή η Προσέγγιση

* **`lxml` + `cssselect`** σας δίνει πλήρη δύναμη CSS‑selector, καθιστώντας το βήμα “επιλογή πολλαπλών επικεφαλίδων” μια εντολή μίας γραμμής.  
* Η μέθοδος `text_content()` εξάγει με ασφάλεια το εσωτερικό κείμενο, αποφεύγοντας HTML entities ή παιδικά tags.  
* Η εγγραφή με `pretty_print=True` κρατά το αρχείο αναγνώσιμο από άνθρωπο, κάτι χρήσιμο για diff σε σύστημα ελέγχου εκδόσεων.

---

## Επιλογή Πολλαπλών Επικεφαλίδων με CSS Selectors

Αν προέρχεστε από το JavaScript, η σύνταξη `cssselect` θα σας φαίνεται οικεία. Ο selector `"h1, h2, h3"` είναι μια **λίστα χωρισμένη με κόμμα**, που σημαίνει “πιάσε οποιοδήποτε στοιχείο ταιριάζει *με κάποιο* από αυτά τα τρία”.  

Μπορείτε επίσης να επεκτείνετε το εύρος:

```python
# Grab every heading from h1 through h6
all_headings = doc.cssselect("h1, h2, h3, h4, h5, h6")
```

Ή να το περιορίσετε σε συγκεκριμένο τμήμα:

```python
# Only headings inside the <article> tag
article_headings = doc.cssselect("article h1, article h2, article h3")
```

Αυτές οι μικρές προσαρμογές σας επιτρέπουν να **select multiple headings** με ακρίβεια λέιζερ, κάτι ιδιαίτερα χρήσιμο όταν έχετε έναν τεράστιο ιστότοπο τεκμηρίωσης και θέλετε να ενημερώσετε μόνο ένα υποτμήμα.

---

## Ασφαλής Αποθήκευση Τροποποιημένων Αρχείων HTML

Όταν **save modified html**, θέλετε να αποφύγετε τη διαφθορά του αρχικού αρχείου. Το μοτίβο που φαίνεται παραπάνω γράφει σε νέο αρχείο (`article_updated.html`). Με αυτόν τον τρόπο μπορείτε:

1. Να επαληθεύσετε τις αλλαγές με ένα εργαλείο diff.  
2. Να επαναφέρετε αμέσως αν κάτι φαίνεται λανθασμένο.  
3. Να διατηρήσετε το αρχικό ανέπαφο για σκοπούς ελέγχου.

Αν προτιμάτε επεξεργασία in‑place, απλώς ανταλλάξτε τις διαδρομές:

```python
import shutil
shutil.move(output_path, input_path)  # Overwrites the original
```

Αλλά θυμηθείτε: **πάντα να κάνετε backup** πριν την αντικατάσταση, ειδικά σε παραγωγικούς διακομιστές.

---

## Αλλαγή Τίτλων HTML vs. Επικεφαλίδες

Μπορεί να αναρωτιέστε αν το “changing HTML titles” είναι το ίδιο με το prefixing headings. Στην ορολογία HTML, το tag `<title>` βρίσκεται μέσα στο `<head>` και ελέγχει τον τίτλο της καρτέλας του προγράμματος περιήγησης, ενώ οι επικεφαλίδες (`<h1>…<h3>`) εμφανίζονται στο σώμα της σελίδας.

Αν χρειάζεται να **change html titles** επίσης, η ίδια ροή εργασίας `lxml` ισχύει:

```python
# Change the <title> tag
title_elem = doc.find(".//title")
if title_elem is not None:
    title_elem.text = f"{prefix}{title_elem.text}"
```

Τώρα τόσο ο τίτλος της σελίδας όσο και οι ορατές επικεφαλίδες φέρουν την ίδια σημαία `[Updated]`—τέλειο για SEO ελέγχους όπου θέλετε συνέπεια μεταξύ meta‑data και περιεχομένου στη σελίδα.

---

## Εναλλακτικές Βιβλιοθήκες για modify html with python

Ενώ το `lxml` είναι γρήγορο και πλούσιο σε δυνατότητες, ίσως ήδη χρησιμοποιείτε **BeautifulSoup** (bs4) στο έργο σας. Εδώ είναι η ίδια λογική σε πιο “pythonic” στυλ:

```python
from bs4 import BeautifulSoup

with open(input_path, "r", encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")

for tag in soup.select("h1, h2, h3"):
    tag.string = f"{prefix}{tag.get_text(strip=True)}"

with open(output_path, "w", encoding="utf-8") as f:
    f.write(str(soup.prettify()))
```

Και οι δύο βιβλιοθήκες σας επιτρέπουν να **modify html with python**, οπότε διαλέξτε αυτή που ταιριάζει στο υπάρχον stack σας. Το `BeautifulSoup` διαπρέπει όταν χρειάζεται ανεκτική ανάλυση κατεστραμμένου markup, ενώ το `lxml` προσφέρει ανώτερη ταχύτητα για μεγάλες δόσεις.

---

## Pro Tips & Συνηθισμένα Πιθανά Σφάλματα

* **Η κωδικοποίηση μετρά** – πάντα ανοίγετε αρχεία με `encoding="utf-8"` για να αποφύγετε σφάλματα Unicode σε μη‑ASCII χαρακτήρες.  
* **Αποφύγετε το διπλό πρόθεμα** – αν τρέξετε το script δύο φορές, θα πάρετε `[Updated] [Updated] …`. Προστατέψτε το ελέγχοντας `heading.text.startswith(prefix)`.  
* **Διατηρήστε τα κενά** – η κλήση `strip()` αφαιρεί περιττά κενά, διατηρώντας το αποτέλεσμα τακτοποιημένο.  
* **Επεξεργασία παρτίδας** – τυλίξτε όλη τη ροή σε ένα `for file in pathlib.Path("YOUR_DIRECTORY").glob("*.html"):` loop για να ενημερώσετε ολόκληρο φάκελο με μία εντολή.  

---

## Πλήρες Παράδειγμα Εργασίας: Ενημέρωση Παρτίδας σε Κατάλογο

Παρακάτω είναι ένα συμπαγές script που διατρέχει κάθε αρχείο `.html` σε έναν κατάλογο, προσθέτει πρόθεμα στις επικεφαλίδες, ενημερώνει το `<title>` και γράφει νέο αρχείο με προσθήκη `_updated`.

```python
import pathlib
from lxml import html

prefix = "[Updated] "
source_dir = pathlib.Path("YOUR_DIRECTORY")
output_dir = source_dir / "updated"
output_dir.mkdir(exist_ok=True)

for html_path in source_dir.glob("*.html"):
    # Load
    with open(html_path, "r", encoding="utf-8") as f:
        doc = html.fromstring(f.read())

    # Headings
    for h in doc.cssselect("h1, h2, h3"):
        if not h.text_content().startswith(prefix):
            h.text = f"{prefix}{h.text_content().strip()}"

    # Title
    title_elem = doc.find(".//title")
    if title_elem is not None and not title_elem.text.startswith(prefix):
        title_elem.text = f"{prefix}{title_elem.text}"

    # Save
    out_path = output_dir / f"{html_path.stem}_updated.html"
    with open(out_path, "w", encoding="utf-8") as f:
        f.write(html.tostring(doc, pretty_print=True, encoding="unicode"))

    print(f"✅ Processed {html_path.name} → {out_path.name}")
```

Τρέξτε το μία φορά και κάθε αρχείο HTML στο `YOUR_DIRECTORY` θα πάρει ένα φρέσκο σήμα `[Updated]`—χωρίς χειροκίνητη επεξεργασία.

---

## Συμπέρασμα

Καλύψαμε **how to add prefix** σε HTML επικεφαλίδες χρησιμοποιώντας Python, δείξαμε πώς να **select multiple headings**, εξηγήσαμε πώς να **save modified html** με ασφάλεια, και ακόμη αγγίξαμε το **change html titles** για πλήρη μετασχηματισμό. Εκμεταλλευόμενοι είτε το `lxml` είτε το `BeautifulSoup`, έχετε τώρα ένα ισχυρό κουτί εργαλείων για **modify html with python** σε πραγματικά έργα.

Τι επόμενα βήματα; Δοκιμάστε να προσθέσετε χρονικές σφραγίδες αντί για στατικό tag, ή δημιουργήστε ένα αρχείο changelog που να καταγράφει κάθε αρχείο που επεξεργαστήκατε. Μπορείτε επίσης να ενσωματώσετε αυτό το script σε CI pipeline ώστε κάθε ανάπτυξη να ενημερώνεται αυτόματα.

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}