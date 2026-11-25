---
category: general
date: 2026-09-19
description: Μάθετε πώς να αλλάξετε τον τίτλο σε ένα αρχείο HTML με την Python. Αυτός
  ο οδηγός καλύπτει την ανάγνωση του HTML, την ενημέρωση της ετικέτας τίτλου και την
  αποθήκευση του τροποποιημένου HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to change title
- update html title
- read html with python
- load html file python
- save modified html
language: el
lastmod: 2026-09-19
og_description: Πώς να αλλάξετε τον τίτλο σε ένα αρχείο HTML με Python. Ακολουθήστε
  αυτό το πλήρες παράδειγμα για να διαβάσετε το HTML, να ενημερώσετε την ετικέτα title
  και να αποθηκεύσετε το τροποποιημένο έγγραφο.
og_image_alt: Diagram showing how to change title in an HTML file using Python
og_title: Πώς να αλλάξετε τον τίτλο σε ένα αρχείο HTML χρησιμοποιώντας Python – βήμα‑βήμα
  οδηγός
schemas:
- author: Aspose
  dateModified: '2026-09-19'
  description: Learn how to change title in an HTML file with Python. This guide covers
    reading HTML, updating the title tag, and saving the modified HTML.
  headline: How to change title in an HTML file using Python
  type: TechArticle
tags:
- Python
- HTML
- Web scraping
title: Πώς να αλλάξετε τον τίτλο σε ένα αρχείο HTML χρησιμοποιώντας Python
url: /el/python/general/how-to-change-title-in-an-html-file-using-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αλλάξετε τον τίτλο σε ένα αρχείο HTML χρησιμοποιώντας Python

Αν χρειάζεστε **πώς να αλλάξετε τον τίτλο** σε ένα έγγραφο HTML προγραμματιστικά, η Python κάνει τη δουλειά απλή. Σε αυτό το tutorial θα διαβάσετε ένα αρχείο HTML, θα ενημερώσετε το στοιχείο `<title>` και θα αποθηκεύσετε το τροποποιημένο HTML ξανά στο δίσκο — όλα με σαφή, εκτελέσιμο κώδικα.

Η αλλαγή του τίτλου της σελίδας είναι ένα συνηθισμένο βήμα όταν δημιουργείτε στατικές ιστοσελίδες, προσαρμόζετε σελίδες που έχετε «σκάψει», ή αυτοματοποιείτε ενημερώσεις SEO. Στο τέλος αυτού του οδηγού θα ξέρετε πώς να **ενημερώσετε τον τίτλο html**, πώς να **διαβάσετε html με python**, και πώς να **αποθηκεύσετε τροποποιημένο html** με ασφάλεια.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

- Python 3.8 ή νεότερη έκδοση εγκατεστημένη  
- Το πακέτο `beautifulsoup4` (`pip install beautifulsoup4`)  
- Ένα αρχείο HTML που θέλετε να επεξεργαστείτε (το παράδειγμα χρησιμοποιεί το `index.html` σε φάκελο της επιλογής σας)  

Δεν απαιτούνται εξωτερικές υπηρεσίες· όλα εκτελούνται τοπικά.

## Βήμα 1: Φόρτωση του αρχείου HTML με Python  

Το πρώτο καθήκον είναι να **φορτώσετε το αρχείο html με python**‑style. Η χρήση του `BeautifulSoup` σας παρέχει έναν ανεκτικό parser που λειτουργεί ακόμη και με ατελή markup.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Define the directory that holds the original HTML
html_dir = Path("YOUR_DIRECTORY")
original_path = html_dir / "index.html"

# Read the file contents (this is how you **read html with python**)
with original_path.open(encoding="utf-8") as f:
    html_content = f.read()

# Parse the document
soup = BeautifulSoup(html_content, "html.parser")
```

*Γιατί είναι σημαντικό αυτό το βήμα:*  
Το `BeautifulSoup` δημιουργεί μια αναπαράσταση δέντρου, επιτρέποντάς σας να ερωτήσετε και να τροποποιήσετε στοιχεία χωρίς χειροκίνητη διαχείριση συμβολοσειρών. Ο ενσωματωμένος `html.parser` είναι γρήγορος και δεν απαιτεί επιπλέον δυαδικά αρχεία.

## Βήμα 2: Εντοπισμός του στοιχείου `<title>`  

Τα έγγραφα HTML συνήθως περιέχουν ένα μόνο στοιχείο `<title>` μέσα στο `<head>`. Ανακτούμε την πρώτη εμφάνιση, η οποία ικανοποιεί την απαίτηση **ενημέρωσης του τίτλου html**.

```python
# Find the first <title> element; BeautifulSoup returns None if missing
title_tag = soup.find("title")

if title_tag is None:
    # If the document lacks a <title>, create one inside <head>
    head_tag = soup.find("head")
    if head_tag is None:
        # As a safety net, add a <head> element at the top
        head_tag = soup.new_tag("head")
        soup.insert(0, head_tag)
    title_tag = soup.new_tag("title")
    head_tag.append(title_tag)

# Show the current title (useful for debugging)
print("Current title:", title_tag.string)
```

*Γιατί ελέγχουμε το `None`*:  
Κάποια τμήματα HTML μπορεί να μην έχουν τίτλο. Η αυτόματη προσθήκη του αποτρέπει μελλοντικά σφάλματα και διατηρεί το script ανθεκτικό.

## Βήμα 3: Αλλαγή του κειμένου του τίτλου  

Τώρα **ενημερώνουμε τον τίτλο html** αναθέτοντας νέο κείμενο στη συμβολοσειρά του στοιχείου. Αυτό είναι το κεντρικό μέρος της λειτουργίας **πώς να αλλάξετε τον τίτλο**.

```python
new_title = "New Title"

# Replace the existing title text
title_tag.string = new_title

print("Updated title:", title_tag.string)
```

Το χαρακτηριστικό `string` αντιπροσωπεύει τον κόμβο κειμένου μέσα στο `<title>`. Η αντικατάστασή του ενημερώνει το DOM στη μνήμη.

## Βήμα 4: Αποθήκευση του τροποποιημένου HTML  

Τέλος, γράψτε το τροποποιημένο έγγραφο σε νέο αρχείο. Αυτό ολοκληρώνει το βήμα **αποθήκευσης τροποποιημένου html** και αφήνει το αρχικό ανέπαφο.

```python
# Define the output path
modified_path = html_dir / "index_modified.html"

# Write the prettified HTML back to disk
with modified_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())

print(f"Modified HTML saved to {modified_path}")
```

Η μέθοδος `prettify()` μορφοποιεί την έξοδο με εσοχές, καθιστώντας το αρχείο εύκολο στην ανάγνωση μετά την αλλαγή.

### Αναμενόμενη έξοδος

Η εκτέλεση του script σε ένα δείγμα `index.html` που αρχικά περιέχει:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Old Title</title>
</head>
<body>
    <h1>Welcome</h1>
</body>
</html>
```

παράγει έξοδο στην κονσόλα παρόμοια με:

```
Current title: Old Title
Updated title: New Title
Modified HTML saved to YOUR_DIRECTORY/index_modified.html
```

Το αποθηκευμένο `index_modified.html` θα ξεκινά τώρα με:

```html
<!DOCTYPE html>
<html>
 <head>
  <title>
   New Title
  </title>
 </head>
 <body>
  <h1>
   Welcome
  </h1>
 </body>
</html>
```

## Πλήρες script για γρήγορη αντιγραφή‑επικόλληση

Παρακάτω βρίσκεται το ολοκληρωμένο, έτοιμο‑για‑εκτέλεση πρόγραμμα που συνδυάζει και τα τέσσερα βήματα. Αποθηκεύστε το ως `change_title.py` και προσαρμόστε το `YOUR_DIRECTORY` όπως χρειάζεται.

```python
# change_title.py
from pathlib import Path
from bs4 import BeautifulSoup

# ----------------------------------------------------------------------
# Configuration – change these values to match your environment
# ----------------------------------------------------------------------
html_dir = Path("YOUR_DIRECTORY")          # Folder containing index.html
original_file = html_dir / "index.html"
modified_file = html_dir / "index_modified.html"
new_title = "New Title"                    # Desired title text
# ----------------------------------------------------------------------

# 1️⃣ Load the HTML file (read html with python)
with original_file.open(encoding="utf-8") as f:
    html_content = f.read()

soup = BeautifulSoup(html_content, "html.parser")

# 2️⃣ Locate or create the <title> element
title_tag = soup.find("title")
if title_tag is None:
    head_tag = soup.find("head")
    if head_tag is None:
        head_tag = soup.new_tag("head")
        soup.insert(0, head_tag)
    title_tag = soup.new_tag("title")
    head_tag.append(title_tag)

print("Current title:", title_tag.string)

# 3️⃣ Update the title (how to change title)
title_tag.string = new_title
print("Updated title:", title_tag.string)

# 4️⃣ Save the modified HTML (save modified html)
with modified_file.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())

print(f"Modified HTML saved to {modified_file}")
```

Εκτελέστε το script:

```bash
python change_title.py
```

Θα δείτε τα μηνύματα στην κονσόλα και ένα νέο αρχείο `index_modified.html` με τον ενημερωμένο τίτλο.

## Πρόσθετες συμβουλές και ειδικές περιπτώσεις

| Κατάσταση | Τι πρέπει να κάνετε |
|-----------|--------------------|
| **Πολλαπλά στοιχεία `<title>`** | Η `soup.find_all("title")` επιστρέφει λίστα· ενημερώστε το πρώτο στοιχείο ή επαναλάβετε αν χρειάζεται να αλλάξετε όλα. |
| **Προβλήματα κωδικοποίησης** | Ανοίξτε τα αρχεία με `encoding="utf-8-sig"` αν υπάρχει BOM, ή εντοπίστε την κωδικοποίηση με `chardet`. |
| **Μεγάλα αρχεία HTML** | Χρησιμοποιήστε parser `lxml` (`BeautifulSoup(html_content, "lxml")`) για καλύτερη απόδοση. |
| **Διατήρηση αρχικής μορφοποίησης** | Αν πρέπει να κρατήσετε ακριβώς τα κενά, γράψτε `str(soup)` αντί για `prettify()`. |
| **Αυτοματοποίηση σε πολλά αρχεία** | Τυλίξτε τη λογική σε συνάρτηση και κάντε βρόχο πάνω στο `Path.rglob("*.html")`. |

Αυτές οι παραλλαγές διατηρούν τον πυρήνα της λογικής **πώς να αλλάξετε τον τίτλο** ενώ προσαρμόζονται σε πραγματικά έργα.

## Συμπέρασμα

Τώρα ξέρετε πώς να **πώς να αλλάξετε τον τίτλο** σε οποιοδήποτε έγγραφο HTML χρησιμοποιώντας Python. Το tutorial κάλυψε την ανάγνωση HTML, τον εντοπισμό του στοιχείου `<title>`, την ενημέρωση του κειμένου του και την **αποθήκευση τροποποιημένου html** με ασφάλεια. Με το πλήρες script μπορείτε να ενσωματώσετε αυτό το μοτίβο σε στατικούς δημιουργούς ιστοσελίδων, pipelines SEO, ή οποιαδήποτε αυτοματοποίηση που απαιτεί δυναμικές αλλαγές τίτλου.

Στη συνέχεια, εξερευνήστε σχετικά θέματα όπως **διαβάστε html με python** για εξαγωγή meta tags, ή τεχνικές **φόρτωσης αρχείου html με python** για χειρισμό εσφαλμένης markup. Πειραματιστείτε με επεξεργασία σε παρτίδες για να ενημερώσετε τίτλους σε ολόκληρο έναν ιστότοπο — η νέα σας δεξιότητα αποτελεί τη βάση για πολλές εργασίες web‑automation. Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Save HTML with Aspose.Html – Complete C# Guide](/html/english/net/working-with-html-documents/how-to-save-html-with-aspose-html-complete-c-guide/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Render HTML to PNG – Complete Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-render-html-to-png-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}