---
category: general
date: 2026-07-21
description: Δημιουργήστε επιλογές διαχείρισης πόρων στην Python και μάθετε πώς να
  ορίζετε το μέγιστο βάθος διαχείρισης για την ανάλυση HTML. Ακολουθήστε αυτό το βήμα‑βήμα
  οδηγό για αξιόπιστη διαχείριση πόρων.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to set max handling depth
language: el
lastmod: 2026-07-21
og_description: Δημιουργήστε επιλογές διαχείρισης πόρων σε Python και δείτε αμέσως
  πώς να ορίσετε το μέγιστο βάθος διαχείρισης για ασφαλή φόρτωση εγγράφων HTML. Κατακτήστε
  την τεχνική σε λίγα λεπτά.
og_image_alt: Screenshot of Python code that creates resource handling options with
  max handling depth set
og_title: Δημιουργία επιλογών διαχείρισης πόρων σε Python – Πλήρης οδηγός βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  headline: Create Resource handling options in Python – Full Guide
  type: TechArticle
- description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  name: Create Resource handling options in Python – Full Guide
  steps:
  - name: Circular References
    text: 'Some legacy sites embed an iframe that points back to the original page,
      creating a loop. With `max_handling_depth` set, the loop is automatically broken
      after the third iteration. However, you might still see a warning in the logs.
      To silence noisy logs, adjust the logger level:'
  - name: Missing Resources
    text: 'If a nested resource fails to load (404 or network timeout), the parser
      throws an exception by default. Wrap the loading call in a `try/except` block
      to keep your application alive:'
  - name: Adjusting Depth Dynamically
    text: 'Sometimes you need different depths for different parts of your pipeline.
      Because `resource_options` is a mutable object, you can change `max_handling_depth`
      on the fly:'
  type: HowTo
tags:
- Python
- HTML parsing
- resource management
title: Δημιουργία επιλογών διαχείρισης πόρων σε Python – Πλήρης οδηγός
url: /el/python/general/create-resource-handling-options-in-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία επιλογών διαχείρισης πόρων σε Python – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ πώς να **create resource handling options** για μια τεράστια σελίδα HTML χωρίς να εξαντλήσετε τη μνήμη σας; Δεν είστε ο μόνος. Όταν τροφοδοτείτε ένα τεράστιο έγγραφο σε έναν parser, οι ένθετοι πόροι όπως frames, iframes ή συνδεδεμένα CSS μπορούν γρήγορα να βγουν εκτός ελέγχου.  

Τα καλά νέα; Μπορείτε να πείτε στον parser να σταματήσει μετά από έναν ορισμένο αριθμό επιπέδων ένθεσης. Σε αυτό το tutorial θα σας δείξουμε **how to set max handling depth** και να διατηρήσετε την εφαρμογή σας ανταποκρινόμενη. Έτοιμοι; Ας βουτήξουμε.

## Τι θα μάθετε

- Γιατί ο περιορισμός του βάθους ένθεσης είναι σημαντικός για την απόδοση και την ασφάλεια.  
- Ο ακριβής κώδικας που χρειάζεστε για **create resource handling options** χρησιμοποιώντας την κλάση `ResourceHandlingOptions`.  
- Πώς να ρυθμίσετε το `max_handling_depth` ώστε ο parser να σταματά μετά από τρία επίπεδα.  
- Συμβουλές για τη διαχείριση edge cases, όπως έγγραφα με κυκλικές αναφορές ή ελλιπείς πόρους.  

Δεν απαιτείται προηγούμενη εμπειρία με τη βιβλιοθήκη — μόνο μια λειτουργική εγκατάσταση Python 3 και μια βασική κατανόηση του file I/O.

## Προαπαιτούμενα

- Python 3.8+ (η βιβλιοθήκη λειτουργεί σε όλες τις πρόσφατες εκδόσεις).  
- Το πακέτο `htmlparser` που παρέχει `HTMLDocument` και `ResourceHandlingOptions`.  
- Ένα δείγμα αρχείου HTML (`big_page.html`) τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε.  

Αν δεν έχετε εγκαταστήσει ακόμη το πακέτο, εκτελέστε:

```bash
pip install htmlparser
```

Τώρα που η προετοιμασία έχει ολοκληρωθεί, ας προχωρήσουμε στο κυρίως θέμα.

## Δημιουργία επιλογών διαχείρισης πόρων – Βήμα 1

Πρώτα απ' όλα: χρειάζεστε μια παρουσία του `ResourceHandlingOptions`. Σκεφτείτε το ως ένα κουτί εργαλείων όπου μπορείτε να ορίσετε τα όρια και τις πολιτικές που πρέπει να τηρεί ο parser.

```python
# Step 1: Create resource handling options and limit nesting depth
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # Stop after three levels of nested resources
```

**Γιατί είναι σημαντικό:**  
Όταν ο parser συναντά ένα `<iframe>` μέσα σε άλλο `<iframe>`, συνήθως ακολουθεί την αλυσίδα επ' άπειρον. Περιορίζοντας το βάθος στο `3`, αποτρέπετε την ανεξέλεγκτη αναδρομή που θα μπορούσε αλλιώς να εξαντλήσει τη RAM ή να προκαλέσει υπερχείλιση στοίβας.  

> **Συμβουλή επαγγελματία:**  
> Αν κάνετε parsing ακατάλληλου περιεχομένου (π.χ., HTML που ανέβασε χρήστης), σκεφτείτε να μειώσετε το βάθος σε `1` ή `2` για να περιορίσετε πιθανές επιθέσεις.

## Φόρτωση του εγγράφου HTML – Βήμα 2

Με το αντικείμενο επιλογών έτοιμο, περάστε το στο `HTMLDocument`. Ο κατασκευαστής θα σεβαστεί το `max_handling_depth` που μόλις ορίσατε.

```python
# Step 2: Load the HTML document using the configured options
html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
```

**Τι συμβαίνει στο παρασκήνιο;**  
`HTMLDocument` διαβάζει το αρχείο, δημιουργεί ένα δέντρο DOM, και στη συνέχεια διασχίζει κάθε εξωτερικό πόρο (stylesheets, scripts, images). Κάθε φορά που συναντά έναν ένθετο πόρο, ελέγχει το `resource_options.max_handling_depth`. Αν το όριο έχει φτάσει, ο parser καταγράφει μια προειδοποίηση και παραλείπει περαιτέρω ένθεση.  

Αυτό σημαίνει ότι λαμβάνετε ένα πλήρως χρησιμοποιήσιμο DOM για τα πρώτα τρία επίπεδα, και το υπόλοιπο αγνοείται με ασφάλεια.

## Επαλήθευση της διαμόρφωσης – Βήμα 3

Πάντα είναι καλή ιδέα να επιβεβαιώσετε ότι οι ρυθμίσεις σας έλαβαν ισχύ. Το αντικείμενο `resource_options` εκθέτει την τρέχουσα κατάσταση του, ώστε να μπορείτε να το εκτυπώσετε ή να το ελέγξετε σε ένα τεστ.

```python
# Step 3: Verify that the max handling depth is set correctly
assert resource_options.max_handling_depth == 3, "Depth limit not applied!"

print(f"Resource handling options configured: max depth = {resource_options.max_handling_depth}")
```

Αν η επαλήθευση περάσει, μπορείτε να είστε σίγουροι ότι ο parser θα τηρήσει το όριο καθ' όλη τη διάρκεια της εκτέλεσης.

## Διαχείριση ακραίων περιπτώσεων

### Κυκλικές Αναφορές

Ορισμένες παλαιές ιστοσελίδες ενσωματώνουν ένα iframe που δείχνει πίσω στην αρχική σελίδα, δημιουργώντας βρόχο. Με το `max_handling_depth` ορισμένο, ο βρόχος σπάζει αυτόματα μετά την τρίτη επανάληψη. Ωστόσο, μπορεί ακόμη να δείτε μια προειδοποίηση στα logs. Για να σιγήσετε τα θορυβώδη logs, προσαρμόστε το επίπεδο του logger:

```python
import logging
logging.getLogger("htmlparser").setLevel(logging.ERROR)
```

### Ελλιπείς Πόροι

Αν ένας ένθετος πόρος αποτύχει να φορτωθεί (404 ή timeout δικτύου), ο parser ρίχνει μια εξαίρεση από προεπιλογή. Τυλίξτε την κλήση φόρτωσης σε ένα μπλοκ `try/except` για να διατηρήσετε την εφαρμογή σας ζωντανή:

```python
try:
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
except Exception as e:
    print(f"Failed to load a nested resource: {e}")
    # Fallback: load the document without additional resources
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

### Δυναμική Προσαρμογή Βάθους

Μερικές φορές χρειάζεστε διαφορετικά βάθη για διαφορετικά μέρη του pipeline σας. Επειδή το `resource_options` είναι μεταβλητό αντικείμενο, μπορείτε να αλλάξετε το `max_handling_depth` εν κινήσει:

```python
resource_options.max_handling_depth = 5   # Temporarily allow deeper nesting
html_doc_deep = HTMLDocument("deep_page.html", resource_options)

resource_options.max_handling_depth = 2   # Tighten for a lightweight preview
html_doc_preview = HTMLDocument("preview.html", resource_options)
```

Απλώς θυμηθείτε να επαναφέρετε την τιμή πριν ξαναχρησιμοποιήσετε την ίδια παρουσία επιλογών σε άλλο νήμα.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι ένα πλήρες script που μπορείτε να αντιγράψετε‑επικολλήσετε, να προσαρμόσετε τις διαδρομές αρχείων και να το εκτελέσετε αμέσως.

```python
import logging
from htmlparser import HTMLDocument, ResourceHandlingOptions

# Optional: Reduce noisy output
logging.getLogger("htmlparser").setLevel(logging.ERROR)

def load_document(path: str, max_depth: int = 3):
    """
    Load an HTML document with a controlled resource handling depth.
    Returns the HTMLDocument instance.
    """
    opts = ResourceHandlingOptions()
    opts.max_handling_depth = max_depth    # How to set max handling depth
    try:
        doc = HTMLDocument(path, opts)
        print(f"Loaded '{path}' with max depth {max_depth}.")
        return doc
    except Exception as exc:
        print(f"Error loading '{path}': {exc}")
        # Fallback to a simple load without resource handling
        return HTMLDocument(path)

if __name__ == "__main__":
    # Example 1: Standard depth
    doc1 = load_document("YOUR_DIRECTORY/big_page.html", max_depth=3)

    # Example 2: Deeper inspection for debugging
    doc2 = load_document("YOUR_DIRECTORY/complex_page.html", max_depth=5)

    # Example 3: Very shallow preview (e.g., thumbnail generation)
    doc3 = load_document("YOUR_DIRECTORY/preview_page.html", max_depth=1)
```

**Αναμενόμενο αποτέλεσμα (όταν τα αρχεία υπάρχουν και είναι σωστά διαμορφωμένα):**

```
Loaded 'YOUR_DIRECTORY/big_page.html' with max depth 3.
Loaded 'YOUR_DIRECTORY/complex_page.html' with max depth 5.
Loaded 'YOUR_DIRECTORY/preview_page.html' with max depth 1.
```

Αν ένα αρχείο δεν μπορεί να διαβαστεί, θα δείτε ένα μήνυμα σφάλματος αντί για κατάρρευση.

![Δημιουργία επιλογών διαχείρισης πόρων σε Python](/images/resource-options.png){alt="Δημιουργία επιλογών διαχείρισης πόρων σε Python"}

## Σύνοψη – Γιατί αυτή η προσέγγιση είναι εξαιρετική

- **Ασφάλεια πρώτα:** Ο περιορισμός του βάθους ένθεσης αποτρέπει την ανεξέλεγκτη αναδρομή και την υπερφόρτωση μνήμης.  
- **Ευελιξία:** Μπορείτε να αλλάξετε το `max_handling_depth` σε χρόνο εκτέλεσης ώστε να ταιριάζει σε διαφορετικά σενάρια.  
- **Απλότητα:** Μερικές γραμμές κώδικα σας επιτρέπουν να **create resource handling options** και να τις εφαρμόσετε αμέσως.  

Συνοψίζοντας, έχετε τώρα ένα ισχυρό μοτίβο για τον έλεγχο του πόσο βαθιά ο parser σας ακολουθεί εξωτερικούς πόρους.

## Τι θα ακολουθήσει;

- Εξερευνήστε περαιτέρω την κλάση `ResourceHandlingOptions` — υπάρχουν σημαίες για caching, διαχείριση timeout και φιλτράρισμα MIME‑type.  
- Συνδυάστε τον περιορισμό βάθους με μια προσαρμοσμένη συμβολοσειρά `UserAgent` για να αποφύγετε το μπλοκάρισμα από επιθετικούς διακομιστές.  
- Αν εργάζεστε με ασύγχρονο I/O, ρίξτε μια ματιά στην παραλλαγή `aiohtmlparser` που σέβεται τις ίδιες επιλογές αλλά λειτουργεί με `asyncio`.  

Μη διστάσετε να πειραματιστείτε: δοκιμάστε να ορίσετε το βάθος σε `0` και παρακολουθήστε τον parser να αγνοεί κάθε εξωτερική αναφορά. Είναι μια χρήσιμη συντόμευση όταν χρειάζεστε μόνο το ακατέργαστο HTML markup.

Έχετε ερωτήσεις ή μια δύσκολη σελίδα που σας προκαλεί προβλήματα; Αφήστε ένα σχόλιο παρακάτω και θα χαρώ να σας βοηθήσω να ρυθμίσετε ακριβώς τις ρυθμίσεις. Καλή ανάλυση!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Δημιουργία HTML από String σε C# – Οδηγός Προσαρμοσμένου Διαχειριστή Πόρων](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Πώς να αποθηκεύσετε HTML σε C# – Πλήρης Οδηγός με Χρήση Προσαρμοσμένου Διαχειριστή Πόρων](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Δημιουργία sandbox για HTML σε Java – Οδηγός βήμα‑βήμα](/html/english/java/creating-managing-html-documents/create-sandbox-for-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}