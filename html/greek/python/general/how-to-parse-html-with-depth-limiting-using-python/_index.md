---
category: general
date: 2026-09-13
description: Μάθετε πώς να αναλύετε HTML και να φορτώνετε έγγραφο HTML περιορίζοντας
  το βάθος για να αποτρέψετε την άπειρη αναδρομή στην Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to parse html
- load html document
- how to limit depth
- prevent infinite recursion
language: el
lastmod: 2026-09-13
og_description: Πώς να αναλύσετε HTML και να φορτώσετε με ασφάλεια ένα έγγραφο HTML.
  Αυτός ο οδηγός δείχνει πώς να περιορίσετε το βάθος και να αποτρέψετε την άπειρη
  επανάληψη.
og_image_alt: Diagram showing HTML parsing flow with depth‑limit control
og_title: Πώς να αναλύσετε HTML με περιορισμό βάθους – Εγχειρίδιο Python
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn how to parse HTML and load HTML document while limiting depth
    to prevent infinite recursion in Python.
  headline: How to parse HTML with depth limiting using Python
  type: TechArticle
- description: Learn how to parse HTML and load HTML document while limiting depth
    to prevent infinite recursion in Python.
  name: How to parse HTML with depth limiting using Python
  steps:
  - name: Create resource handling options
    text: The `ResourceHandlingOptions` object tells the parser when to stop following
      nested resources such as `<iframe>` tags or linked CSS files.
  - name: Load HTML document with the configured options
    text: Now you load the file while supplying the options you just defined. This
      is the **load html document** step that respects the depth limit.
  - name: Parse the document safely
    text: With the document loaded, you can now traverse the DOM. The example below
      extracts all headings (`<h1>`‑`<h3>`) without exceeding the depth limit.
  type: HowTo
tags:
- html parsing
- python
- recursion
- resource handling
title: Πώς να αναλύσετε HTML με περιορισμό βάθους χρησιμοποιώντας Python
url: /el/python/general/how-to-parse-html-with-depth-limiting-using-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αναλύσετε HTML με περιορισμό βάθους χρησιμοποιώντας Python

Αν χρειάζεστε **πώς να αναλύσετε html** από μια μεγάλη αναφορά, το πρώτο βήμα είναι να φορτώσετε το έγγραφο HTML με ένα δίχτυ ασφαλείας που σταματά την βαθιά εμφώλευση. Αυτό το tutorial σας δείχνει πώς να φορτώσετε ένα έγγραφο HTML, να ορίσετε ένα μέγιστο βάθος επεξεργασίας και **να αποτρέψετε την άπειρη αναδρομή** όταν οι πόροι αναφέρονται ο ένας στον άλλο.

Θα δείτε ένα πλήρες, εκτελέσιμο παράδειγμα που χρησιμοποιεί `ResourceHandlingOptions` και `HTMLDocument`. Στο τέλος του οδηγού θα μπορείτε να αναλύετε με ασφάλεια οποιοδήποτε αρχείο HTML χωρίς να εξαντλήσετε τη μνήμη ή να προκαλέσετε υπερχείλιση στοίβας.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Python 3.9 ή νεότερη έκδοση εγκατεστημένη.
* Τη βιβλιοθήκη επεξεργασίας HTML που παρέχει `ResourceHandlingOptions` και `HTMLDocument`. (Για αυτό το tutorial υποθέτουμε ότι η βιβλιοθήκη ονομάζεται `htmlhandler`; εγκαταστήστε την με `pip install htmlhandler`.)
* Βασική κατανόηση της αναδρομής και της δομής του HTML.

Δεν απαιτείται πρόσθετη διαμόρφωση συστήματος.

## Πώς να αναλύσετε HTML με περιορισμό βάθους

Ο πυρήνας της λύσης είναι η δημιουργία ενός αντικειμένου `ResourceHandlingOptions`, η ρύθμιση του `max_handling_depth` και η μεταβίβαση του στο `HTMLDocument`. Τα παρακάτω βήματα σας καθοδηγούν στη διαδικασία.

### Βήμα 1: Δημιουργία επιλογών διαχείρισης πόρων

Το αντικείμενο `ResourceHandlingOptions` ενημερώνει τον parser πότε να σταματήσει την παρακολούθηση ενσωματωμένων πόρων όπως ετικέτες `<iframe>` ή συνδεδεμένα αρχεία CSS.

```python
# Step 1: Create resource handling options
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # Stop after 3 levels of nested resources
```

*Γιατί είναι σημαντικό*: Χωρίς περιορισμό βάθους, ένα κακόβουλο ή κακώς δομημένο έγγραφο θα μπορούσε να ενσωματώνει πόρους που αναφέρονται ατέρμονα ο ένας στον άλλο. Ορίζοντας το `max_handling_depth` σε 3, ο parser σταματά μετά από τρία επίπεδα, κάτι που είναι επαρκές για τα περισσότερα νόμιμα έγγραφα ενώ προστατεύει το runtime.

### Βήμα 2: Φόρτωση εγγράφου HTML με τις ρυθμισμένες επιλογές

Τώρα φορτώνετε το αρχείο παρέχοντας τις επιλογές που μόλις ορίσατε. Αυτό είναι το βήμα **load html document** που σέβεται το όριο βάθους.

```python
# Step 2: Load the HTML document using the configured options
html_doc = HTMLDocument(
    "YOUR_DIRECTORY/big_report.html",
    resource_handling_options=resource_options
)
```

*Γιατί είναι σημαντικό*: Η μεταβίβαση του `resource_handling_options` στο `HTMLDocument` ενσωματώνει το όριο‑βάθους απευθείας στη μηχανή ανάλυσης. Ο parser θα σταματήσει αυτόματα την περιήγηση μόλις φτάσει στο όριο, **αποτρέποντας την άπειρη αναδρομή**.

### Βήμα 3: Ανάλυση του εγγράφου με ασφάλεια

Με το έγγραφο φορτωμένο, μπορείτε τώρα να περιηγηθείτε στο DOM. Το παρακάτω παράδειγμα εξάγει όλους τους τίτλους (`<h1>`‑`<h3>`) χωρίς να υπερβεί το όριο βάθους.

```python
def extract_headings(node, current_depth=0):
    """
    Recursively collect heading text while respecting the max handling depth.
    """
    if current_depth > resource_options.max_handling_depth:
        return []  # Prevent infinite recursion by aborting deeper calls

    headings = []
    if node.tag_name in ("h1", "h2", "h3"):
        headings.append(node.text_content.strip())

    for child in node.children:
        headings.extend(extract_headings(child, current_depth + 1))
    return headings

# Start traversal from the root element
all_headings = extract_headings(html_doc.root)
print("Collected headings:", all_headings)
```

**Αναμενόμενη έξοδος (παράδειγμα)**:

```
Collected headings: ['Executive Summary', 'Methodology', 'Results', 'Conclusion']
```

Η προστασία `if current_depth > resource_options.max_handling_depth` είναι ο μηχανισμός **πώς να περιορίσετε το βάθος** που σταματά περαιτέρω αναδρομή. Αυτό το μοτίβο λειτουργεί για οποιαδήποτε δεδομένα δομημένα σε δέντρο, όχι μόνο για HTML.

## Πώς να φορτώσετε έγγραφο HTML με προσαρμοσμένες επιλογές

Αν χρειάζεται να προσαρμόσετε το βάθος για ένα συγκεκριμένο αρχείο, απλώς αλλάξτε το `max_handling_depth` πριν δημιουργήσετε το `HTMLDocument`.

```python
resource_options.max_handling_depth = 5   # Allow deeper nesting for this file
html_doc = HTMLDocument("another_report.html", resource_handling_options=resource_options)
```

Η αλλαγή του ορίου είναι χρήσιμη όταν γνωρίζετε ότι ένα έγγραφο περιέχει νόμιμη βαθιά εμφώλευση (π.χ., ενσωματωμένοι πίνακες). Ο ίδιος κώδικας εξακολουθεί να **αποτρέπει την άπειρη αναδρομή** επειδή το όριο επιβάλλεται κατά την εκτέλεση.

## Συνηθισμένα λάθη και πώς να τα αποφύγετε

| Παγίδα | Γιατί συμβαίνει | Διόρθωση |
|---------|----------------|-----|
| **Απουσία `resource_handling_options`** | Ο parser ακολουθεί κάθε πόρο, οδηγώντας σε απεριόριστη αναδρομή. | Πάντα να περνάτε το αντικείμενο `ResourceHandlingOptions` κατά την κατασκευή του `HTMLDocument`. |
| **Ορισμός `max_handling_depth` πολύ χαμηλό** | Σημαντικό περιεχόμενο μπορεί να παραλειφθεί επειδή ο parser σταματά νωρίς. | Δοκιμάστε με ένα αντιπροσωπευτικό δείγμα και επιλέξτε βάθος που ισορροπεί ασφάλεια και πληρότητα. |
| **Αναδρομική συνάρτηση χωρίς έλεγχο βάθους** | Προσαρμοσμένες περιηγήσεις μπορούν ακόμα να επαναλαμβάνονται άπειρα ακόμη και αν ο parser σταματά. | Συμπεριλάβετε την ίδια λογική ελέγχου βάθους (`if current_depth > max_depth: return`) σε κάθε βοηθητική αναδρομική συνάρτηση. |
| **Υπόθεση ότι όλοι οι κόμβοι έχουν `children`** | Οι κόμβοι κειμένου μπορεί να μην έχουν χαρακτηριστικό `children`, προκαλώντας σφάλματα attribute. | Προστατέψτε με `hasattr(node, "children")` ή χρησιμοποιήστε μπλοκ try/except. |

Η αντιμετώπιση αυτών των ζητημάτων εξασφαλίζει ότι η λύση **πώς να αναλύσετε html** παραμένει ανθεκτική σε διάφορες εισόδους.

## Πλήρες, εκτελέσιμο παράδειγμα

Ακολουθεί το πλήρες script που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα αρχείο με όνομα `parse_report.py`. Δείχνει ολόκληρη τη ροή εργασίας από τη δημιουργία επιλογών μέχρι την εξαγωγή τίτλων.

```python
# parse_report.py
from htmlhandler import ResourceHandlingOptions, HTMLDocument

def main():
    # ---- Step 1: configure depth limit ----
    resource_options = ResourceHandlingOptions()
    resource_options.max_handling_depth = 3   # adjust as needed

    # ---- Step 2: load the HTML document ----
    html_path = "YOUR_DIRECTORY/big_report.html"
    html_doc = HTMLDocument(html_path, resource_handling_options=resource_options)

    # ---- Step 3: recursive extraction with safety guard ----
    def extract_headings(node, current_depth=0):
        if current_depth > resource_options.max_handling_depth:
            return []  # stop deeper recursion

        headings = []
        if node.tag_name in ("h1", "h2", "h3"):
            headings.append(node.text_content.strip())

        # Safely iterate over children if they exist
        if hasattr(node, "children"):
            for child in node.children:
                headings.extend(extract_headings(child, current_depth + 1))
        return headings

    # Run extraction starting from the document root
    headings = extract_headings(html_doc.root)
    print("Collected headings:", headings)

if __name__ == "__main__":
    main()
```

Εκτελέστε το script:

```bash
python parse_report.py
```

Θα πρέπει να δείτε τη λίστα των τίτλων να εκτυπώνεται στην κονσόλα, επιβεβαιώνοντας ότι ο parser σεβάστηκε το όριο βάθους και **απέτρεψε την άπειρη αναδρομή**.

## Επόμενα βήματα

* **Αναλύστε άλλα στοιχεία** – προσαρμόστε το `extract_headings` για να συλλέξετε πίνακες, συνδέσμους ή εικόνες.
* **Διαχείριση μεγάλων αρχείων** – χρησιμοποιήστε σταδιακή ανάλυση (`HTMLDocument.stream`) όταν εργάζεστε με αναφορές πολλαπλών γιγαμπάιτ.
* **Ενσωμάτωση με asyncio** – τυλίξτε το βήμα φόρτωσης σε ασύγχρονη συνάρτηση αν χρειάζεστε μη‑blocking I/O.

Η εξερεύνηση αυτών των θεμάτων ενισχύει την ικανότητά σας να **φορτώνετε html document** αντικείμενα αποδοτικά διατηρώντας πλήρη έλεγχο του βάθους αναδρομής.

---

Ακολουθώντας αυτόν τον οδηγό ξέρετε πλέον **πώς να αναλύσετε html** με ασφάλεια, πώς να **φορτώνετε html document** με προσαρμοσμένο όριο βάθους, και πώς να **αποτρέψετε την άπειρη αναδρομή** σε οποιαδήποτε αναδρομική περιήγηση. Εφαρμόστε το μοτίβο στα δικά σας έργα και προσαρμόστε τη ρύθμιση βάθους ώστε να ταιριάζει στην πολυπλοκότητα των πηγαίων αρχείων σας. Καλό κώδικα!

## Τι Θα Μάθετε Στη Σειρά Επόμενη;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Parse HTML Java – Load, Query & Count Elements](/html/english/java/creating-managing-html-documents/how-to-parse-html-java-load-query-count-elements/)
- [how to query html in Java – load HTML, CSS selector, and extract headings](/html/english/java/css-html-form-editing/how-to-query-html-in-java-load-html-css-selector-and-extract/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}