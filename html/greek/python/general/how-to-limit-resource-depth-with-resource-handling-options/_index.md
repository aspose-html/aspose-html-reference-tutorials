---
category: general
date: 2026-10-25
description: Μάθετε πώς να περιορίζετε το βάθος των πόρων και να εφαρμόζετε τη διαχείριση
  πόρων κατά την αποθήκευση μεγάλων αρχείων HTML χρησιμοποιώντας Python. Ακολουθήστε
  αυτόν τον οδηγό βήμα‑προς‑βήμα για αξιόπιστα αποτελέσματα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- limit resource depth
- apply resource handling
- HTML document processing
- save options Python
- resource handling options
language: el
lastmod: 2026-10-25
og_description: Περιορίστε το βάθος των πόρων και εφαρμόστε διαχείριση πόρων κατά
  την αποθήκευση HTML με Python. Αυτό το σεμινάριο παρουσιάζει τη πλήρη, εκτελέσιμη
  λύση.
og_image_alt: Screenshot illustrating limit resource depth in a Python script
og_title: Περιορίστε το βάθος των πόρων κατά την εφαρμογή διαχείρισης πόρων – Οδηγός
  Python
schemas:
- author: GroupDocs
  dateModified: '2026-10-25'
  description: Learn how to limit resource depth and apply resource handling when
    saving large HTML files using Python. Follow this step‑by‑step guide for reliable
    results.
  headline: How to limit resource depth with resource handling options
  type: TechArticle
- description: Learn how to limit resource depth and apply resource handling when
    saving large HTML files using Python. Follow this step‑by‑step guide for reliable
    results.
  name: How to limit resource depth with resource handling options
  steps:
  - name: '**Dynamic content loaded via JavaScript** – The parser only sees static
      HTML. If your page relies on scripts that inject further resources, those will
      never be counted toward the depth limit. Consider pre‑rendering the page with
      a headless browser before applying the limit.'
    text: '**Dynamic content loaded via JavaScript** – The parser only sees static
      HTML. If your page relies on scripts that inject further resources, those will
      never be counted toward the depth limit. Consider pre‑rendering the page with
      a headless browser before applying the limit.'
  - name: '**Circular references** – Some pages include iframes that point back to
      the same page. The depth counter prevents infinite loops, but you may still
      see partially rendered sections. Adjust `max_handling_depth` or manually exclude
      problematic frames.'
    text: '**Circular references** – Some pages include iframes that point back to
      the same page. The depth counter prevents infinite loops, but you may still
      see partially rendered sections. Adjust `max_handling_depth` or manually exclude
      problematic frames.'
  - name: '**Mixed protocols (http/https)** – If resources use different schemes,
      the library may treat them as separate domains. The depth limit still applies
      across protocols, but network permissions might differ. Ensure your environment
      permits both.'
    text: '**Mixed protocols (http/https)** – If resources use different schemes,
      the library may treat them as separate domains. The depth limit still applies
      across protocols, but network permissions might differ. Ensure your environment
      permits both.'
  type: HowTo
tags:
- Python
- HTML
- File handling
title: Πώς να περιορίσετε το βάθος του πόρου με επιλογές διαχείρισης πόρων
url: /el/python/general/how-to-limit-resource-depth-with-resource-handling-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να περιορίσετε το βάθος των πόρων με επιλογές διαχείρισης πόρων

Εάν χρειάζεται να **περιορίσετε το βάθος των πόρων** κατά την επεξεργασία ενός τεράστιου αρχείου HTML, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε. Στο τέλος του tutorial θα γνωρίζετε επίσης πώς να **εφαρμόσετε τη διαχείριση πόρων** ώστε η λειτουργία αποθήκευσης να σέβεται το όριο βάθους και να αποφεύγει την ατέρμονη επεξεργασία.

Οι μεγάλες σελίδες HTML συχνά ενσωματώνουν πολλούς εξωτερικούς πόρους — εικόνες, scripts, stylesheets και ενσωματωμένα iframes. Χωρίς όριο βάθους, ο parser μπορεί να ακολουθήσει κάθε σύνδεσμο, αυξάνοντας δραματικά τη χρήση μνήμης και το χρόνο επεξεργασίας. Η τεχνική που περιγράφεται εδώ διατηρεί τη λειτουργία γρήγορη και προβλέψιμη.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Εγκατεστημένο Python 3.9+.
* Το `groupdocs-viewer` (ή μια παρόμοια βιβλιοθήκη επεξεργασίας HTML) διαθέσιμο μέσω `pip install groupdocs-viewer`.
* Ένα δείγμα αρχείου HTML (`big_page.html`) τοποθετημένο σε γνωστό φάκελο.
* Δικαιώματα εγγραφής στον φάκελο εξόδου.

Αυτά τα στοιχεία εξασφαλίζουν ότι ο κώδικας θα τρέξει χωρίς πρόσθετη διαμόρφωση.

## Βήμα 1: Φόρτωση του πηγαίου εγγράφου HTML

Το πρώτο βήμα είναι η δημιουργία μιας παρουσίας `HTMLDocument` που δείχνει στο αρχικό αρχείο. Το αντικείμενο αντιπροσωπεύει ολόκληρη τη δομή HTML και σας δίνει πρόσβαση στις επιλογές αποθήκευσης αργότερα.

```python
# Step 1: Load the source HTML document
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

*Γιατί είναι σημαντικό*: Η φόρτωση του αρχείου μία φορά δίνει στη βιβλιοθήκη ένα μοναδικό σημείο εισόδου για όλες τις επόμενες λειτουργίες. Επίσης, επικυρώνει ότι το αρχείο υπάρχει, προκαλώντας σφάλμα νωρίς αν η διαδρομή είναι λανθασμένη.

## Βήμα 2: Δημιουργία επιλογών διαχείρισης πόρων και περιορισμός του βάθους επεξεργασίας

`ResourceHandlingOptions` σας επιτρέπει να ελέγξετε πόσο βαθιά θα διασχίσει η βιβλιοθήκη τους συνδεδεμένους πόρους. Ορίζοντας το `max_handling_depth` σε μικρό αριθμό (π.χ., 5) λέτε στη μηχανή να σταματήσει να ακολουθεί συνδέσμους μετά από πέντε επίπεδα εμφώλευσης.

```python
# Step 2: Create resource handling options and limit the processing depth
resource_opts = ResourceHandlingOptions()
resource_opts.max_handling_depth = 5  # Restricts handling to 5 levels deep
```

*Γιατί είναι σημαντικό*: Με **περιορισμό του βάθους των πόρων**, αποτρέπετε τον parser από το να κατεβάζει κάθε εικόνα, script ή iframe που μπορεί να αναφέρεται έμμεσα. Αυτό μειώνει την κίνηση δικτύου και την πίεση στη μνήμη, ειδικά για σελίδες που ενσωματώνουν περιεχόμενο τρίτων.

## Βήμα 3: Συγκόλληση των επιλογών πόρων στις επιλογές αποθήκευσης

`SaveOptions` συγκεντρώνει όλες τις ρυθμίσεις που επηρεάζουν το αρχείο εξόδου. Αναθέτοντας το `resource_handling_options` **εφαρμόζουμε τη διαχείριση πόρων** στην επερχόμενη λειτουργία αποθήκευσης.

```python
# Step 3: Attach the resource options to the save options
save_opts = SaveOptions()
save_opts.resource_handling_options = resource_opts
```

*Γιατί είναι σημαντικό*: Το αντικείμενο `save_opts` λειτουργεί ως δοχείο για πολλαπλές σημαίες (συμπίεση, μορφή κ.λπ.). Η προσθήκη του `resource_handling_options` εξασφαλίζει ότι το όριο βάθους θα τηρηθεί κατά τη φάση εγγραφής.

## Βήμα 4: Αποθήκευση του εγγράφου με την εφαρμοσμένη περιορισμένη διαχείριση πόρων

Τέλος, καλέστε `doc.save()` με τις ρυθμισμένες `save_opts`. Το αρχείο εξόδου θα περιέχει μόνο τους πόρους που εμπίπτουν στο καθορισμένο βάθος.

```python
# Step 4: Save the document with the limited resource handling applied
doc.save("YOUR_DIRECTORY/big_page_limited.html", save_opts)
```

**Αναμενόμενο αποτέλεσμα**:  
Ένα νέο αρχείο `big_page_limited.html` εμφανίζεται στο `YOUR_DIRECTORY`. Ανοίξτε το σε έναν περιηγητή· θα δείτε την αρχική διάταξη, αλλά οποιοιδήποτε πόροι πέρα από πέντε επίπεδα εμφώλευσης θα λείπουν. Η σελίδα φορτώνει πιο γρήγορα και καταναλώνει πολύ λιγότερη μνήμη.

## Επαλήθευση του αποθηκευμένου HTML

Μετά την αποθήκευση, είναι καλή πρακτική να επιβεβαιώσετε ότι το όριο βάθους τηρήθηκε.

```python
# Verify that the saved file exists and its size is reasonable
import os

output_path = "YOUR_DIRECTORY/big_page_limited.html"
if os.path.isfile(output_path):
    size_kb = os.path.getsize(output_path) / 1024
    print(f"Saved file size: {size_kb:.2f} KB")
else:
    raise FileNotFoundError("The limited HTML file was not created.")
```

Αν το μέγεθος είναι δραματικά μικρότερο από το αρχικό (που μπορεί να είναι εκατοντάδες kilobytes), η ρύθμιση **περιορισμού του βάθους των πόρων** λειτούργησε όπως προβλέπεται.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Συμπτωμα | Αιτία | Διόρθωση |
|----------|-------|----------|
| Δεν υπάρχει αλλαγή στο μέγεθος του αρχείου | `max_handling_depth` παραμένει στην προεπιλογή (απεριόριστο) | Ορίστε ρητά `resource_opts.max_handling_depth` σε τιμή < ∞ |
| Λείπουν εικόνες στη σελίδα | Οι πόροι ήταν πιο βαθιά από το όριο | Αυξήστε το βάθος ή μετακινήστε κρίσιμους πόρους σε πιο ρηχό επίπεδο |
| `PermissionError` κατά την αποθήκευση | Ο φάκελος εξόδου είναι μόνο για ανάγνωση | Επιλέξτε φάκελο με δικαιώματα εγγραφής ή προσαρμόστε τα δικαιώματα του OS |
| Μη αναμενόμενη εξαίρεση `ResourceHandlingException` | Ασυμβατότητα έκδοσης βιβλιοθήκης | Αναβαθμίστε στην τελευταία έκδοση του `groupdocs-viewer` (`pip install --upgrade groupdocs-viewer`) |

**Συμβουλή επαγγελματία**: Ξεκινήστε με βάθος 3 για πολύ μεγάλες σελίδες και αυξήστε το σταδιακά μέχρι η οπτική πιστότητα να ανταποκρίνεται στις απαιτήσεις σας.

## Ακραίες περιπτώσεις που μπορεί να συναντήσετε

1. **Δυναμικό περιεχόμενο που φορτώνεται μέσω JavaScript** – Ο parser βλέπει μόνο το στατικό HTML. Αν η σελίδα σας βασίζεται σε scripts που εισάγουν περαιτέρω πόρους, αυτοί δεν θα ληφθούν υπόψη για το όριο βάθους. Σκεφτείτε προ‑απόδοση της σελίδας με headless browser πριν εφαρμόσετε το όριο.
2. **Κυκλικές αναφορές** – Κάποιες σελίδες περιλαμβάνουν iframes που δείχνουν πίσω στην ίδια σελίδα. Ο μετρητής βάθους αποτρέπει άπειρους βρόχους, αλλά μπορεί να δείτε μερικά τμήματα μερικώς αποδομημένα. Προσαρμόστε το `max_handling_depth` ή εξαιρέστε χειροκίνητα προβληματικά frames.
3. **Μικτοί πρωτόκολλοι (http/https)** – Αν οι πόροι χρησιμοποιούν διαφορετικά σχήματα, η βιβλιοθήκη μπορεί να τους θεωρήσει ως ξεχωριστούς τομείς. Το όριο βάθους ισχύει και μεταξύ πρωτοκόλλων, αλλά τα δικαιώματα δικτύου μπορεί να διαφέρουν. Βεβαιωθείτε ότι το περιβάλλον σας επιτρέπει και τα δύο.

## Επόμενα βήματα: προχωρημένη διαχείριση πόρων

Τώρα που μπορείτε να **περιορίσετε το βάθος των πόρων** και να **εφαρμόσετε τη διαχείριση πόρων**, ίσως θέλετε να εξερευνήσετε:

* **Προσαρμοσμένα φίλτρα** – Χρησιμοποιήστε `resource_opts.resource_filter` για να παραλείψετε συγκεκριμένους τύπους αρχείων (π.χ., μεγάλα βίντεο).
* **Ρυθμίσεις συμπίεσης** – Συνδυάστε `SaveOptions` με `compression_level` για περαιτέρω μείωση του μεγέθους εξόδου.
* **Επεξεργασία παρτίδας** – Επανάληψη σε φάκελο HTML αρχείων, εφαρμόζοντας το ίδιο όριο βάθους σε καθένα.

Αυτές οι επεκτάσεις σας επιτρέπουν να δημιουργήσετε μια πλήρη pipeline βελτιστοποίησης HTML για μεγάλης κλίμακας ροές εργασίας εγγράφων.

## Συμπέρασμα

Μάθατε πώς να **περιορίζετε το βάθος των πόρων** και να **εφαρμόζετε τη διαχείριση πόρων** κατά την αποθήκευση ενός μεγάλου εγγράφου HTML με Python. Με τη διαμόρφωση του `ResourceHandlingOptions` και την προσθήκη του στα `SaveOptions`, αποκτάτε λεπτομερή έλεγχο του αριθμού των εμφωλευμένων πόρων που επεξεργάζονται, οδηγώντας σε ταχύτερες αποθηκεύσεις και μικρότερα αρχεία εξόδου. Πειραματιστείτε με διαφορετικές τιμές βάθους και πρόσθετες `SaveOptions` για να προσαρμόσετε τη συμπεριφορά στις ανάγκες του έργου σας.

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συνδεδεμένα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσετε σε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Set max_handling_depth in Aspose.HTML Python – Complete Guide](/html/english/python/general/how-to-set-max-handling-depth-in-aspose-html-python-complete/)
- [Create resource handling options and load an HTML document in Python](/html/english/python/general/create-resource-handling-options-and-load-an-html-document-i/)
- [How to Save HTML with Controlled Depth – Step‑by‑Step Python Guide](/html/english/python/general/how-to-save-html-with-controlled-depth-step-by-step-python-g/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}