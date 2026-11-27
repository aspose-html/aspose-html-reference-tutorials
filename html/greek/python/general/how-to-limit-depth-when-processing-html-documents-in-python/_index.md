---
category: general
date: 2026-11-27
description: Πώς να περιορίσετε το βάθος κατά την επεξεργασία HTML χρησιμοποιώντας
  Python. Ακολουθήστε αυτό το παράδειγμα φόρτωσης εγγράφου HTML με επιλογές διαχείρισης
  πόρων.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to limit depth
- load html document
- html processing example
language: el
lastmod: 2026-11-27
og_description: Πώς να περιορίσετε το βάθος κατά την επεξεργασία HTML στην Python.
  Μάθετε πώς να φορτώνετε έγγραφο HTML και να διαμορφώνετε τη διαχείριση πόρων για
  αποδοτικά αποτελέσματα.
og_image_alt: Illustration of how to limit depth in HTML processing using Python
og_title: Πώς να περιορίσετε το βάθος κατά την επεξεργασία HTML σε Python
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: How to limit depth during HTML processing using Python. Follow this
    load html document example with resource handling options.
  headline: How to limit depth when processing HTML documents in Python
  type: TechArticle
tags:
- HTML processing
- resource handling
- Python
title: Πώς να περιορίσετε το βάθος κατά την επεξεργασία εγγράφων HTML με Python
url: /el/python/general/how-to-limit-depth-when-processing-html-documents-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να περιορίσετε το βάθος κατά την επεξεργασία εγγράφων HTML σε Python

Αν χρειάζεστε **how to limit depth** ενώ διαχειρίζεστε αρχεία HTML, αυτός ο οδηγός σας παρουσιάζει μια πλήρη, έτοιμη προς εκτέλεση λύση. Θα δείτε μια πρακτική ροή εργασίας **load html document** και ένα σαφές **html processing example** που επιδεικνύει τη διαμόρφωση resource‑handling.

Η επεξεργασία μεγάλων δέντρων HTML μπορεί γρήγορα να καταναλώσει μνήμη ή CPU εάν κάθε ένθετο στοιχείο διασχίζεται. Με τον περιορισμό του βάθους επεξεργασίας, προστατεύετε την εφαρμογή σας από ανεξέλεγκτη αναδρομή και διατηρείτε την απόδοση προβλέψιμη.

## Τι καλύπτει ο οδηγός

* Πώς να **load html document** με μια βιβλιοθήκη συμβατή με Python.  
* Πώς να δημιουργήσετε και να συνδέσετε ένα αντικείμενο `ResourceHandlingOptions`.  
* Πώς να ορίσετε το `max_handling_depth` για να σταματήσετε την επεξεργασία μετά από συγκεκριμένο αριθμό επιπέδων ένθεσης.  
* Πώς να αποθηκεύσετε το μετασχηματισμένο αρχείο χρησιμοποιώντας τις ρυθμισμένες επιλογές.  

Στο τέλος αυτού του άρθρου θα έχετε ένα λειτουργικό script που περιορίζει το βάθος, αποφεύγει την υπερβολική χρήση πόρων και παράγει ένα καθαρό αρχείο HTML εξόδου.

![How to limit depth in HTML processing using Python](image.png)

## Προαπαιτούμενα

| Requirement | Reason |
|-------------|--------|
| Python 3.8+ | Απαιτείται για τις υποδείξεις τύπων της βιβλιοθήκης και τη σύγχρονη σύνταξη. |
| `groupdocs-viewer` (or a similar HTML handling package) installed via `pip install groupdocs-viewer` | Παρέχει `HTMLDocument`, `ResourceHandlingOptions` και `SaveOptions`. |
| Basic familiarity with Python functions and object‑oriented code | Σας επιτρέπει να προσαρμόσετε το παράδειγμα στο δικό σας έργο. |

> **Pro tip:** Εάν χρησιμοποιείτε εικονικό περιβάλλον, ενεργοποιήστε το πριν εγκαταστήσετε το πακέτο για να διατηρήσετε τις εξαρτήσεις απομονωμένες.

## Βήμα 1: Φόρτωση του εγγράφου HTML

Η πρώτη ενέργεια είναι η ανάγνωση του αρχείου πηγής σε ένα αντικείμενο `HTMLDocument`. Αυτό το αντικείμενο αντιπροσωπεύει ολόκληρο το δέντρο σήμανσης και σας παρέχει μεθόδους για περαιτέρω επεξεργασία.

```python
from groupdocs.viewer import HTMLDocument, ResourceHandlingOptions, SaveOptions

# Step 1 – load the source HTML document
html_doc = HTMLDocument("YOUR_DIRECTORY/input.html")
```

*Γιατί είναι σημαντικό*: Η φόρτωση του εγγράφου δημιουργεί μια αναπαράσταση στη μνήμη που η βιβλιοθήκη μπορεί να διασχίσει. Χωρίς αυτό το βήμα δεν μπορείτε να εφαρμόσετε κανόνες resource‑handling.

## Βήμα 2: Δημιουργία επιλογών resource‑handling

`ResourceHandlingOptions` σας επιτρέπει να ρυθμίσετε λεπτομερώς πώς επεξεργάζονται οι εξωτερικοί πόροι (εικόνες, scripts, styles). Για περιορισμό βάθους, η ιδιότητα `max_handling_depth` είναι το κλειδί.

```python
# Step 2 – create a resource handling configuration
resource_options = ResourceHandlingOptions()
```

Τώρα έχετε ένα κενό αντικείμενο διαμόρφωσης που μπορείτε να γεμίσετε με τα επιθυμητά όρια.

## Βήμα 3: Περιορισμός του βάθους της ένθετης επεξεργασίας πόρων

Ορίστε το `max_handling_depth` στον αριθμό των επιπέδων ένθεσης που είστε διατεθειμένοι να διαχειριστείτε. Σε αυτό το παράδειγμα σταματάμε μετά από τρία επίπεδα, κάτι που συχνά είναι αρκετό για τυπικές ιστοσελίδες ενώ αποτρέπει τις βαθιά‑ένθετες δομές από το να υπερφορτώνουν το σύστημα.

```python
# Step 3 – limit processing depth (e.g., stop after 3 levels)
resource_options.max_handling_depth = 3
```

*Γιατί πρέπει να περιορίσετε το βάθος*: Το βαθιά ένθετο HTML (σκεφτείτε μεγάλους πίνακες μέσα σε πίνακες ή δέντρα επαναλαμβανόμενων στοιχείων) μπορεί να προκαλέσει υπερπλήρωση στοίβας ή τεράστιες αυξήσεις μνήμης. Το όριο βάθους λέει στη μηχανή να αγνοεί οτιδήποτε πέρα από το καθορισμένο επίπεδο, εφαρμόζοντας πρακτικά **how to limit depth**.

## Βήμα 4: Σύνδεση της διαμόρφωσης με τις επιλογές αποθήκευσης

`SaveOptions` συγκεντρώνει όλες τις ρυθμίσεις που θέλετε ο συγγραφέας να τηρήσει κατά την εξαγωγή του εγγράφου. Αναθέτοντας την ιδιότητα `resource_handling_options`, εξασφαλίζετε ότι το όριο βάθους θα τηρηθεί κατά τη λειτουργία αποθήκευσης.

```python
# Step 4 – prepare save options and attach the resource handling configuration
save_options = SaveOptions()
save_options.resource_handling_options = resource_options
```

Εάν χρειάζεστε πρόσθετες ρυθμίσεις (όπως κωδικοποίηση ή pretty‑print), μπορούν να προστεθούν στην ίδια παρουσία `save_options`.

## Βήμα 5: Αποθήκευση του επεξεργασμένου εγγράφου

Τέλος, καλέστε τη μέθοδο `save` με τη διαδρομή εξόδου και τις ρυθμισμένες `save_options`. Η βιβλιοθήκη θα διασχίσει το δέντρο HTML, θα τηρήσει το όριο βάθους και θα γράψει τη δημιουργημένη σήμανση στο αρχείο προορισμού.

```python
# Step 5 – save the processed document with the configured options
html_doc.save("YOUR_DIRECTORY/output.html", save_options)
```

### Αναμενόμενο αποτέλεσμα

* Το αρχείο `output.html` περιέχει το αρχικό περιεχόμενο μέχρι τρία επίπεδα ένθεσης.  
* Οποιαδήποτε πιο βαθιά στοιχεία παραλείπονται, αφήνοντας μια ελαφριά έκδοση της σελίδας.  
* Δεν εμφανίζονται σφάλματα ακόμη και αν η πηγή περιέχει εκατοντάδες ένθετες ετικέτες.

Μπορείτε να επαληθεύσετε το αποτέλεσμα ανοίγοντας το `output.html` σε έναν περιηγητή ή εκτυπώνοντας ένα απόσπασμα:

```python
with open("YOUR_DIRECTORY/output.html", "r", encoding="utf-8") as f:
    print(f.read()[:500])   # show the first 500 characters
```

## Συχνές ερωτήσεις και ειδικές περιπτώσεις

| Question | Answer |
|----------|--------|
| **Τι γίνεται αν χρειάζομαι μεγαλύτερο όριο;** | Αλλάξτε το `resource_options.max_handling_depth` σε μεγαλύτερο ακέραιο, π.χ., `5`. |
| **Θα αφαιρεθούν οι εικόνες πέρα από το όριο;** | Ναι. Οποιοσδήποτε πόρος βρίσκεται σε κόμβο πιο βαθύ από το όριο αγνοείται, συμπεριλαμβανομένων των εικόνων, των scripts και των ενσωματωμένων στυλ. |
| **Μπορώ να απενεργοποιήσω εντελώς τον περιορισμό βάθους;** | Ορίστε το `max_handling_depth` σε `0` ή `None` (ανάλογα με την έκδοση της βιβλιοθήκης) για να επεξεργαστείτε ολόκληρο το δέντρο. |
| **Πώς αλληλεπιδρά αυτό με τις εισαγωγές CSS;** | Τα αρχεία CSS θεωρούνται πόροι· εάν συνδέονται από κόμβο πιο βαθύ από το όριο, δεν θα ληφθούν. |
| **Εφαρμόζεται το όριο ανά τύπο πόρου;** | Το όριο βάθους είναι παγκόσμιο για ολόκληρο το δέντρο του εγγράφου· δεν διακρίνει μεταξύ εικόνων, scripts ή άλλων κόμβων. |

## Πλήρες λειτουργικό script

Συνδυάζοντας όλα τα βήματα δημιουργείται ένα ενιαίο, αυτόνομο script που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα αρχείο `.py` και να το εκτελέσετε αμέσως:

```python
from groupdocs.viewer import HTMLDocument, ResourceHandlingOptions, SaveOptions

def limit_html_depth(input_path: str, output_path: str, max_depth: int = 3) -> None:
    """
    Loads an HTML file, limits the processing depth, and saves the result.

    Args:
        input_path: Path to the source HTML file.
        output_path: Destination path for the processed HTML.
        max_depth: Maximum nesting level to process (default is 3).
    """
    # Load the source document
    html_doc = HTMLDocument(input_path)

    # Configure depth limiting
    resource_options = ResourceHandlingOptions()
    resource_options.max_handling_depth = max_depth

    # Attach configuration to save options
    save_options = SaveOptions()
    save_options.resource_handling_options = resource_options

    # Save the transformed document
    html_doc.save(output_path, save_options)

if __name__ == "__main__":
    # Example usage – adjust paths as needed
    limit_html_depth(
        input_path="YOUR_DIRECTORY/input.html",
        output_path="YOUR_DIRECTORY/output.html",
        max_depth=3
    )
```

Η εκτέλεση αυτού του script παράγει το ίδιο `output.html` που περιγράφηκε νωρίτερα. Μη διστάσετε να προσαρμόσετε το `max_depth` ή να επεκτείνετε τη λειτουργία με πρόσθετες παραμέτρους (π.χ., προσαρμοσμένη κωδικοποίηση).

## Επόμενα βήματα και συναφή θέματα

* **Advanced resource handling** – εξερευνήστε τις ιδιότητες του `ResourceHandlingOptions` όπως

## Τι θα πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Set max_handling_depth in Aspose.HTML Python – Complete Guide](/html/english/python/general/how-to-set-max-handling-depth-in-aspose-html-python-complete/)
- [Create resource handling options and load an HTML document in Python](/html/english/python/general/create-resource-handling-options-and-load-an-html-document-i/)
- [How to configure HTML resource handling in Python and load an HTML document](/html/english/python/general/how-to-configure-html-resource-handling-in-python-and-load-a/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}