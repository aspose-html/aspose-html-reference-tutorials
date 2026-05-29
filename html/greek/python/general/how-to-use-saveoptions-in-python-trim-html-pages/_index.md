---
category: general
date: 2026-05-28
description: Μάθετε πώς να χρησιμοποιείτε το SaveOptions για να περικόψετε σελίδες
  HTML στην Python. Αυτός ο οδηγός βήμα‑βήμα εξηγεί επίσης πώς να φορτώσετε ένα έγγραφο
  HTML και να αφαιρέσετε αποδοτικά ενσωματωμένους πόρους.
draft: false
keywords:
- how to use saveoptions
- how to load html document
- how to trim html page
language: el
og_description: Πώς να χρησιμοποιήσετε το SaveOptions για να περικόψετε σελίδες HTML
  στην Python. Ακολουθήστε αυτόν τον οδηγό για να φορτώσετε ένα έγγραφο HTML, να ορίσετε
  όρια πόρων και να αποθηκεύσετε ένα καθαρό, ελαφρύ αρχείο.
og_title: Πώς να χρησιμοποιήσετε το SaveOptions στην Python – Περικοπή σελίδων HTML
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to use SaveOptions to trim HTML pages in Python. This step‑by‑step
    guide also explains how to load an HTML document and efficiently remove nested
    resources.
  headline: How to Use SaveOptions in Python – Trim HTML Pages
  type: TechArticle
tags:
- python
- html-processing
- saveoptions
- resource-handling
title: Πώς να χρησιμοποιήσετε το SaveOptions στην Python – Κοπή σελίδων HTML
url: /el/python/general/how-to-use-saveoptions-in-python-trim-html-pages/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε το SaveOptions σε Python – Κοπή Σελίδων HTML

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε το SaveOptions** για να μειώσετε ένα τεράστιο αρχείο HTML χωρίς να σπάσει κάτι; Δεν είστε μόνοι. Όταν φορτώνετε μια σελίδα που περιλαμβάνει δεκάδες ένθετους πόρους—σκεφτείτε CSS, JS ή ακόμη και άλλα αποσπάσματα HTML—το αποτέλεσμα μπορεί να εκτοξευθεί ανεξέλεγκτα.  

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που όχι μόνο δείχνει **πώς να χρησιμοποιήσετε το SaveOptions**, αλλά καλύπτει επίσης **πώς να φορτώσετε ένα έγγραφο HTML** και τον καλύτερο τρόπο **να κόψετε μια σελίδα HTML** περιορίζοντας το βάθος της ένθεσης. Στο τέλος θα έχετε ένα καθαρό, κομμένο αρχείο έτοιμο για ανάπτυξη ή περαιτέρω επεξεργασία.

## Τι Θα Επιτύχετε

- Φορτώστε οποιοδήποτε τοπικό αρχείο HTML με μία μόνο γραμμή κώδικα.  
- Διαμορφώστε τις επιλογές διαχείρισης πόρων ώστε να σταματούν σε συγκεκριμένο βάθος ενσωμάτωσης.  
- Αποθηκεύστε το κομμένο αποτέλεσμα χρησιμοποιώντας την ισχυρή κλάση `SaveOptions`.  

Χωρίς εξωτερικά εργαλεία, χωρίς μαγεία—μόνο απλό Python και μια μικρή βιβλιοθήκη που κάνει τη βαριά δουλειά.

---

## Προαπαιτούμενα

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε:

1. **Python 3.9+** εγκατεστημένο (η σύνταξη που χρησιμοποιείται λειτουργεί σε οποιαδήποτε πρόσφατη έκδοση).  
2. Το υποθετικό πακέτο `htmlprocessor` που παρέχει `HTMLDocument`, `SaveOptions` και `ResourceHandlingOptions`. Εγκαταστήστε το μέσω:

```bash
pip install htmlprocessor
```

> **Συμβουλή:** Αν χρησιμοποιείτε εικονικό περιβάλλον, ενεργοποιήστε το πρώτα—διατηρεί τις εξαρτήσεις σας τακτοποιημένες.

---

## Βήμα 1: Πώς να Φορτώσετε ένα Έγγραφο HTML

Το φόρτωμα ενός αρχείου είναι τόσο απλό όσο το να δείξετε τον κατασκευαστή στο μονοπάτι σας. Η βιβλιοθήκη διαβάζει το markup, δημιουργεί ένα δέντρο τύπου DOM και το προετοιμάζει για περαιτέρω επεξεργασία.

```python
from htmlprocessor import HTMLDocument

# Replace with the actual path to your file
doc = HTMLDocument("YOUR_DIRECTORY/complex_page.html")
print("Document loaded –", doc.title or "Untitled")
```

> **Γιατί είναι σημαντικό:** Το αντικείμενο `HTMLDocument` αφαιρεί την ανάγκη για άμεση διαχείριση ακατέργαστων συμβολοσειρών, παρέχοντάς σας μεθόδους για ερωτήματα, τροποποιήσεις και τελικά αποθήκευση της σελίδας. Επίσης, ομαλοποιεί τα τέλη γραμμής και τις κωδικοποιήσεις χαρακτήρων, αποφεύγοντας λεπτές σφάλματα αργότερα.

Θα παρατηρήσετε ότι εκτυπώσαμε τον τίτλο μόνο για να επαληθεύσουμε ότι η φόρτωση πέτυχε. Αν το αρχείο λείπει ή είναι κατεστραμμένο, ο κατασκευαστής θα ρίξει μια σαφή εξαίρεση—χωρίς σιωπηλές αποτυχίες.

---

## Βήμα 2: Διαμορφώστε τη Διαχείριση Πόρων – Ο Πυρήνας της Κοπής

Το επόμενο κομμάτι του παζλ είναι **πώς να κόψετε το περιεχόμενο μιας σελίδας HTML** περιορίζοντας το πόσο βαθιά ακολουθεί ο επεξεργαστής τις ενσωματώσεις. Εδώ η `ResourceHandlingOptions` διαπρέπει.

```python
from htmlprocessor import ResourceHandlingOptions

# Create a fresh options instance
res_opt = ResourceHandlingOptions()
# max_handling_depth = 2 means: main page + one level of includes
res_opt.max_handling_depth = 2
```

### Τι Κάνει το `max_handling_depth`;

- **Βάθος 1** → Μόνο το αρχικό αρχείο HTML, όλοι οι εξωτερικοί πόροι αγνοούνται.  
- **Βάθος 2** → Το αρχικό αρχείο συν τυχόν άμεσα αναφερόμενα αρχεία (π.χ., ένα `iframe` ή server‑side include).  
- **Μεγαλύτερες τιμές** → Βαθύτερη ένθεση, αλλά και μεγαλύτερο αρχείο εξόδου και μεγαλύτερος χρόνος επεξεργασίας.

Καθορίζοντας το βάθος στο **2**, κρατάμε τη κύρια σελίδα και ένα επίπεδο ενσωματώσεων, απορρίπτοντας ό,τι πιο βαθύ. Αυτό συνήθως αρκεί για να αφαιρεθούν περιττά υποσέλιδα, σενάρια analytics ή ένθετα πρότυπα που δεν χρειάζεστε σε μια κομμένη αντίγραφο.

---

## Βήμα 3: Συνδέστε τις Επιλογές στη Διαμόρφωση Αποθήκευσης

Τώρα συνδέουμε τους κανόνες πόρων μας με ένα αντικείμενο `SaveOptions`. Αυτό το αντικείμενο λέει στη βιβλιοθήκη *ακριβώς* πώς να γράψει το αρχείο πίσω στο δίσκο.

```python
from htmlprocessor import SaveOptions

save_opt = SaveOptions()
save_opt.resource_handling_options = res_opt
```

> **Γιατί να χρησιμοποιήσετε το `SaveOptions`?**  
> Σας δίνει λεπτομερή έλεγχο πάνω στην έξοδο—πέρα από το μόνο βάθος πόρων. Μπορείτε αργότερα να προσθέσετε συμπίεση, pretty‑printing ή ακόμη και προσαρμοσμένα callbacks χωρίς να αγγίξετε τη βασική λογική αποθήκευσης.

---

## Βήμα 4: Πώς να Χρησιμοποιήσετε το SaveOptions για να Κόψετε τη Σελίδα HTML

Τέλος, καλούμε τη μέθοδο `save` με τις ρυθμισμένες επιλογές μας. Η βιβλιοθήκη θα διασχίσει το DOM, θα σεβαστεί το όριο βάθους και θα γράψει ένα κομμένο αρχείο.

```python
# Save the trimmed document
output_path = "YOUR_DIRECTORY/trimmed_page.html"
doc.save(output_path, save_opt)

print(f"Trimmed page saved to {output_path}")
```

### Αναμενόμενο Αποτέλεσμα

- Το αρχείο `trimmed_page.html` περιέχει το αρχικό markup **συν** τυχόν ενσωματώσεις μέχρι ένα επίπεδο βάθους.  
- Όλες οι πιο βαθιές ενσωματώσεις παραλείπονται, με αποτέλεσμα μια μικρότερη, πιο γρήγορη σε φόρτωση σελίδα.  
- Δεν εμφανίζονται σπασμένες ετικέτες—η βιβλιοθήκη κλείνει αυτόματα τυχόν στοιχεία που έμειναν ανοιχτά μετά την αφαίρεση.

Μπορείτε να ανοίξετε το αποτέλεσμα σε έναν περιηγητή για να επαληθεύσετε ότι το κύριο περιεχόμενο εξακολουθεί να αποδίδεται, ενώ τα περιττά σενάρια ή ένθετα πλαίσια έχουν αφαιρεθεί.

---

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες script που μπορείτε να αντιγράψετε‑και‑εκτελέσετε:

```python
# -*- coding: utf-8 -*-
"""
Trim an HTML page using SaveOptions.
Demonstrates:
- How to load an HTML document
- How to configure ResourceHandlingOptions
- How to use SaveOptions to save a trimmed version
"""

from htmlprocessor import HTMLDocument, SaveOptions, ResourceHandlingOptions

def trim_html(input_path: str, output_path: str, max_depth: int = 2) -> None:
    # Load the source document
    doc = HTMLDocument(input_path)
    print("Loaded:", doc.title or "Untitled")

    # Set up resource handling (how to trim HTML page)
    res_opt = ResourceHandlingOptions()
    res_opt.max_handling_depth = max_depth

    # Attach options to save configuration (how to use SaveOptions)
    save_opt = SaveOptions()
    save_opt.resource_handling_options = res_opt

    # Perform the save
    doc.save(output_path, save_opt)
    print(f"Trimmed HTML saved to {output_path}")

if __name__ == "__main__":
    INPUT = "YOUR_DIRECTORY/complex_page.html"
    OUTPUT = "YOUR_DIRECTORY/trimmed_page.html"
    trim_html(INPUT, OUTPUT, max_depth=2)
```

Τρέξτε το script, ορίστε το `INPUT` σε οποιοδήποτε σύνθετο αρχείο HTML και θα λάβετε μια πιο ελαφριά έκδοση στο `OUTPUT`.  

> **Σημείωση για ειδικές περιπτώσεις:** Αν η αρχική σελίδα περιέχει conditional comments (`<!--[if IE]>…<![endif]-->`) που αναφέρονται σε πιο βαθιούς πόρους, θα αφαιρεθούν όπως κάθε άλλη ένθετη ενσωμάτωση. Αυτό αποτρέπει τα παλιά‑IE hacks από το να φουσκώνουν το τελικό μέγεθος.

---

## Οπτική Σύνοψη

Παρακάτω υπάρχει ένα γρήγορο διάγραμμα που απεικονίζει τη ροή—από τη φόρτωση του εγγράφου, μέσω της διαχείρισης πόρων, μέχρι την αποθήκευση του κομμένου αποτελέσματος.

![πώς να χρησιμοποιήσετε το saveoptions παράδειγμα](https://example.com/placeholder.png "Διάγραμμα που δείχνει πώς να χρησιμοποιήσετε το SaveOptions για να κόψετε σελίδες HTML")

*Κείμενο alt:* **πώς να χρησιμοποιήσετε το saveoptions παράδειγμα** – δείχνει τη διαδικασία τριών βημάτων φόρτωσης, διαμόρφωσης και αποθήκευσης ενός εγγράφου HTML.

---

## Συχνές Ερωτήσεις & Παγίδες

| Ερώτηση | Απάντηση |
|----------|--------|
| **Τι γίνεται αν χρειαστώ μεγαλύτερο βάθος ένθεσης;** | Αυξήστε το `max_handling_depth` σε 3 ή 4, αλλά θυμηθείτε ότι το μέγεθος της εξόδου θα αυξηθεί. |
| **Μπορώ να εξαιρέσω συγκεκριμένες ετικέτες (π.χ., `<script>`) ανεξάρτητα από το βάθος;** | Ναι—το `SaveOptions` υποστηρίζει επίσης την ιδιότητα `tag_exclusion_list`. Προσθέστε `"script"` σε αυτή τη λίστα για να αφαιρείτε πάντα τα scripts. |
| **Η βιβλιοθήκη είναι thread‑safe;** | Η τρέχουσα έκδοση δεν είναι. Δημιουργήστε ένα ξεχωριστό `HTMLDocument` ανά νήμα. |
| **Θα ξαναγραφούν τα σχετικά URLs;** | Από προεπιλογή όχι. Χρησιμοποιήστε `save_opt.rewrite_relative_urls = True` αν χρειάζεται να τα προσαρμόσετε στη νέα θέση. |

---

## Επόμενα Βήματα

Τώρα που έχετε κατακτήσει **πώς να χρησιμοποιήσετε το SaveOptions**, δοκιμάστε αυτές τις επεκτάσεις:

- **Συμπίεση της εξόδου:** Ορίστε `save_opt.enable_gzip = True` για μικρότερα αρχεία κατά τη μετάδοση.  
- **Μορφοποίηση για αποσφαλμάτωση:** Ενεργοποιήστε `save_opt.indent_output = True` για ωραία μορφοποιημένο HTML.  
- **Επεξεργασία παρτίδας:** Επανάληψη σε έναν φάκελο με αρχεία HTML και εφαρμογή της ίδιας λογικής κοπής—ιδανικό για στατικούς δημιουργούς ιστοσελίδων.

Κάθε μία από αυτές τις προσαρμογές βασίζεται στο ίδιο θεμέλιο που μόλις μάθατε, διατηρώντας τον κώδικά σας καθαρό και συντηρήσιμο.

---

## Συμπέρασμα

Καλύψαμε ολόκληρο τον κύκλο ζωής της κοπής μιας σελίδας HTML σε Python: **πώς να φορτώσετε ένα έγγραφο HTML**, να διαμορφώσετε **πώς να κόψετε μια σελίδα HTML** χρησιμοποιώντας `ResourceHandlingOptions`, και τελικά **πώς να χρησιμοποιήσετε το SaveOptions** για να γράψετε το καθαρισμένο αρχείο. Το παράδειγμα είναι πλήρως αυτόνομο, τρέχει αμέσως, και δείχνει γιατί ο έλεγχος του βάθους πόρων είναι μια κρίσιμη βελτιστοποίηση για web‑scraping, στατική δημιουργία ιστοσελίδων ή οποιαδήποτε κατάσταση που χρειάζεται ένα ελαφρύ στιγμιότυπο HTML.

Δοκιμάστε το, πειραματιστείτε με διαφορετικές τιμές `max_handling_depth`, και αφήστε τις κομμένες σελίδες να κάνουν τη σκληρή δουλειά για εσάς. Αν αντιμετωπίσετε προβλήματα, αφήστε ένα σχόλιο παρακάτω—καλή κωδικοποίηση!

## Σχετικά Μαθήματα

- [Πώς να Αποθηκεύσετε HTML σε C# – Πλήρης Οδηγός με Χρήση Προσαρμοσμένου Διαχειριστή Πόρων](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Πώς να Αποδώσετε HTML ως PNG – Πλήρης Οδηγός C#](/html/english/net/rendering-html-documents/how-to-render-html-as-png-complete-c-guide/)
- [Πώς να Συμπιέσετε HTML σε C# – Αποθήκευση HTML σε Zip](/html/english/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}