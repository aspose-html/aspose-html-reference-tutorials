---
category: general
date: 2026-05-31
description: Δημιουργήστε ένα αντικείμενο ResourceHandlingOptions για να ελέγχετε
  τη φόρτωση πόρων HTML. Μάθετε πώς να περιορίζετε το βάθος των πόρων και να φορτώνετε
  ένα HTMLDocument με προσαρμοσμένες επιλογές.
draft: false
keywords:
- create resourcehandlingoptions instance
- limit resource depth
- HTMLDocument options
- resource loading configuration
- python html parsing
language: el
og_description: Δημιουργήστε ένα αντικείμενο ResourceHandlingOptions για να ελέγχετε
  τη φόρτωση πόρων HTML. Αυτός ο οδηγός δείχνει πώς να ορίσετε το μέγιστο βάθος διαχείρισης
  και να φορτώσετε ένα HTMLDocument με προσαρμοσμένες επιλογές.
og_title: Δημιουργία αντικειμένου ResourceHandlingOptions για τη φόρτωση HTML
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create ResourceHandlingOptions instance to control HTML resource loading.
    Learn how to limit resource depth and load an HTMLDocument with custom options.
  headline: Create ResourceHandlingOptions Instance for HTML Loading
  type: TechArticle
tags:
- Python
- HTML parsing
- Resource handling
title: Δημιουργία Αντικειμένου ResourceHandlingOptions για τη Φόρτωση HTML
url: /el/python/general/create-resourcehandlingoptions-instance-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Παραδείγματος ResourceHandlingOptions για Φόρτωση HTML

Έχετε αναρωτηθεί ποτέ πώς να **δημιουργήσετε ένα παράδειγμα ResourceHandlingOptions** ώστε να μην καταστρέφει ο parser μια τεράστια σελίδα HTML; Δεν είστε οι μόνοι—μεγάλα έγγραφα με ένθετα scripts, frames ή includes μπορούν γρήγορα να μετατρέψουν μια απλή εξαγωγή σε εφιάλτη.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα τις ακριβείς ενέργειες για να δημιουργήσετε ένα αντικείμενο `ResourceHandlingOptions`, να περιορίσετε το επίπεδο ένθεσης και να το περάσετε σε ένα `HTMLDocument`. Στο τέλος θα έχετε ένα καθαρό, επαναχρησιμοποιήσιμο μοτίβο για **διαμόρφωση φόρτωσης πόρων** που λειτουργεί με οποιοδήποτε αρχείο HTML μεγέθους κόσμου.

## Τι Θα Μάθετε

- Γιατί ένα παράδειγμα `ResourceHandlingOptions` είναι σημαντικό όταν αναλύετε τεράστιες σελίδες.  
- Πώς να **περιορίσετε το βάθος των πόρων** ώστε να αποφύγετε την ατέρμονη αναδρομή.  
- Η ακριβής σύνταξη για τη φόρτωση ενός `HTMLDocument` με τις προσαρμοσμένες επιλογές σας.  
- Ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να ενσωματώσετε στο πρότζεκτ σας άμεσα.  

**Προαπαιτούμενα:** Python 3.8+, η βιβλιοθήκη `htmlparser` που παρέχει `HTMLDocument` και `ResourceHandlingOptions`. Δεν απαιτούνται άλλες εξαρτήσεις.

---

## Βήμα 1: Δημιουργία Παραδείγματος ResourceHandlingOptions

Το πρώτο που χρειάζεστε είναι ένα νέο αντικείμενο `ResourceHandlingOptions`. Σκεφτείτε το ως πίνακα ελέγχου για κάθε εξωτερικό πόρο που μπορεί να συναντήσει ο parser—scripts, εικόνες, iframes, ό,τι θέλετε.

```python
# Step 1: Initialize the options object
options = ResourceHandlingOptions()
```

> **Γιατί είναι σημαντικό:** Χωρίς ένα ρητό παράδειγμα, ο parser επιστρέφει στις προεπιλογές του, που συχνά σημαίνει «φόρτωση όλων». Για τεράστιες σελίδες αυτή η προεπιλογή μπορεί να καταναλώσει γιγαμπάιτ μνήμης και να σταματήσει το script σας.

---

## Βήμα 2: Περιορισμός Βάθους Πόρων

Στη συνέχεια, λέμε στις επιλογές πόσο βαθιά είμαστε διατεθειμένοι να πάμε. Ορίζοντας το `max_handling_depth` σε 5, για παράδειγμα, ο parser σταματά μετά από πέντε επίπεδα ένθετων πόρων. Προσαρμόστε τον αριθμό ανάλογα με την περίπτωση χρήσης σας.

```python
# Step 2: Cap the nesting depth (e.g., stop after 5 levels)
options.max_handling_depth = 5
```

> **Συμβουλή:** Αν σας ενδιαφέρει μόνο το περιεχόμενο του πρώτου επιπέδου, ένα βάθος 1 ή 2 είναι συνήθως αρκετό και επιταχύνει δραματικά τη διαδικασία.

---

## Βήμα 3: Φόρτωση του Εγγράφου HTML με τις Επιλογές

Τώρα περνάμε το ρυθμισμένο `options` στο `HTMLDocument`. Ο κατασκευαστής δέχεται τη διαδρομή του αρχείου (ή το URL) και το αντικείμενο επιλογών, δίνοντάς σας λεπτομερή έλεγχο πάνω σε ό,τι φορτώνεται.

```python
# Step 3: Parse the HTML file using the configured options
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", options)
```

> **Τι θα δείτε:** Ο parser θα διαβάσει το `big_page.html`, αλλά οποιοσδήποτε πόρος που θα προκαλούσε το βάθος να ξεπεράσει το 5 θα αγνοηθεί σιωπηλά. Αυτό αποτρέπει την ανεξέλεγκτη αναδρομή και κρατά τη χρήση μνήμης προβλέψιμη.

---

## Βήμα 4: Επαλήθευση του Αποτελέσματος (Προαιρετικό αλλά Χρήσιμο)

Είναι καλή πρακτική να ελέγχετε ότι το έγγραφο φορτώθηκε όπως αναμενόταν. Παρακάτω υπάρχει ένας γρήγορος έλεγχος που εκτυπώνει τον αριθμό των πόρων που διαχειρίστηκαν επιτυχώς.

```python
# Step 4: Quick verification
print(f"Handled resources: {len(doc.resources)}")
print(f"Document title: {doc.title}")
```

**Αναμενόμενη έξοδος** (οι αριθμοί σας θα διαφέρουν ανάλογα με το αρχείο εισόδου):

```
Handled resources: 12
Document title: Example Large Page
```

Αν ο αριθμός είναι πολύ χαμηλότερος από ό,τι περιμένατε, ίσως χρειαστεί να αυξήσετε το `max_handling_depth` ή να προσαρμόσετε άλλες ιδιότητες του `ResourceHandlingOptions`.

---

## Συνηθισμένες Παραλλαγές & Ακραίες Περιπτώσεις

| Κατάσταση | Προσαρμογή |
|-----------|------------|
| **Θέλετε να αγνοήσετε μόνο τις εικόνες** | Ορίστε `options.ignore_images = True`. |
| **Τα scripts προκαλούν time‑outs** | Χρησιμοποιήστε `options.max_script_execution_time = 2` (δευτερόλεπτα). |
| **Ανάλυση απομακρυσμένου URL αντί για αρχείο** | Περνάτε το URL ως συμβολοσειρά στο `HTMLDocument` όπως κάνετε με τη διαδρομή αρχείου. |
| **Θέλετε προσαρμοσμένο logger** | Αναθέστε `options.logger = my_logger` πριν τη φόρτωση. |

Αυτές οι ρυθμίσεις αποτελούν μέρος του **εργαλείου επιλογών HTMLDocument** και σας επιτρέπουν να βελτιστοποιήσετε τη **διαμόρφωση φόρτωσης πόρων** χωρίς να ξαναγράψετε τον parser.

---

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι ένα αυτόνομο script που μπορείτε να τρέξετε αμέσως. Αποθηκεύστε το ως `parse_big_page.py` και εκτελέστε το με `python parse_big_page.py`.

```python
# parse_big_page.py
from htmlparser import HTMLDocument, ResourceHandlingOptions

def main():
    # 1️⃣ Create the options instance
    options = ResourceHandlingOptions()
    
    # 2️⃣ Limit how deep we go into nested resources
    options.max_handling_depth = 5
    
    # Optional: ignore images to speed things up
    # options.ignore_images = True
    
    # 3️⃣ Load the document with our custom options
    doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", options)
    
    # 4️⃣ Verify the load
    print(f"Handled resources: {len(doc.resources)}")
    print(f"Document title: {doc.title}")

if __name__ == "__main__":
    main()
```

Τρέξτε το και θα δείτε τον αριθμό των πόρων και τον τίτλο να εκτυπώνονται, επιβεβαιώνοντας ότι έχετε δημιουργήσει επιτυχώς **resourcehandlingoptions instance** και το έχετε εφαρμόσει.

---

## Συμπέρασμα

Σας δείξαμε πώς να **δημιουργήσετε ένα παράδειγμα ResourceHandlingOptions**, να περιορίσετε το επίπεδο ένθεσης και να το περάσετε σε ένα `HTMLDocument`. Αυτό το μοτίβο προσφέρει αξιόπιστη **διαμόρφωση φόρτωσης πόρων** για οποιοδήποτε μεγάλο αρχείο HTML, διατηρώντας την ανάλυση HTML σε Python γρήγορη και φιλική στη μνήμη.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να αλλάξετε το όριο βάθους, να ενεργοποιήσετε/απενεργοποιήσετε το `ignore_images`, ή να ενσωματώσετε έναν προσαρμοσμένο logger—κάθε προσαρμογή θα σας διδάξει κάτι νέο για τις **επιλογές HTMLDocument** και πώς αλληλεπιδρούν με τη ροή δεδομένων σας.  

Αν βρήκατε αυτόν τον οδηγό χρήσιμο, μοιραστείτε τον, δώστε αστέρι στο repo, ή αφήστε ένα σχόλιο με τις δικές σας συμβουλές. Καλή ανάλυση!

## Τι Θα Μάθετε Στη Σειρά;

- [Create HTML from String in C# – Custom Resource Handler Guide](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Create Stream Provider in .NET with Aspose.HTML](/html/english/net/advanced-features/create-stream-provider/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}