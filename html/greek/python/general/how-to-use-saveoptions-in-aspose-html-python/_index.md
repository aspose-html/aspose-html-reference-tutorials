---
category: general
date: 2026-07-27
description: Πώς να χρησιμοποιήσετε το SaveOptions στο Aspose.HTML (Python) για να
  μετατρέψετε μια μεγάλη σελίδα HTML και να εφαρμόσετε αποδοτική διαχείριση πόρων.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use SaveOptions
- convert large html page
- apply resource handling
- Aspose.HTML Python
- HTML resource handling
language: el
lastmod: 2026-07-27
og_description: Η χρήση του SaveOptions στο Aspose.HTML (Python) σας επιτρέπει να
  μετατρέψετε μεγάλες σελίδες HTML, εφαρμόζοντας διαχείριση πόρων για καθαρά και γρήγορα
  αποτελέσματα.
og_image_alt: Screenshot illustrating how to use SaveOptions in Aspose.HTML for Python
og_title: Πώς να χρησιμοποιήσετε το SaveOptions στο Aspose.HTML – Οδηγός Python
schemas:
- author: Aspose
  dateModified: '2026-07-27'
  description: How to use SaveOptions in Aspose.HTML (Python) to convert large HTML
    page and apply resource handling efficiently.
  headline: How to Use SaveOptions in Aspose.HTML (Python)
  type: TechArticle
- questions:
  - answer: Aspose.HTML follows redirects but won’t send credentials automatically.
      You can pre‑download those assets or use a custom `WebRequest` handler (beyond
      this guide’s scope).
    question: What if the page references resources over HTTPS that require authentication?
  - answer: Yes—set `resource_options.max_handling_depth = 0`. This skips external
      files but leaves any `<style>` blocks intact.
    question: Can I preserve inline CSS while stripping external files?
  - answer: After saving, you can run a secondary pass with Pillow to downscale images,
      or let Aspose.HTML’s built‑in image compression options handle it (use `save_options.image_quality`).
    question: What about very large images that still bloat the output?
  - answer: The limit is global across all resource types (images, scripts, styles).
      If you need granular control, you’d have to filter resources manually after
      loading the document.
    question: Is the depth limit applied per‑resource type?
  type: FAQPage
tags:
- Aspose.HTML
- Python
- HTML processing
title: Πώς να χρησιμοποιήσετε το SaveOptions στο Aspose.HTML (Python)
url: /el/python/general/how-to-use-saveoptions-in-aspose-html-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε το SaveOptions στο Aspose.HTML (Python)

Η χρήση του SaveOptions στο Aspose.HTML για Python είναι κάτι που πολλοί προγραμματιστές ρωτούν όταν εργάζονται με τεράστια αρχεία HTML. Αν χρειάζεστε **μετατροπή μεγάλης σελίδας HTML** διατηρώντας αυστηρό έλεγχο στην **εφαρμογή διαχείρισης πόρων**, βρίσκεστε στο σωστό σημείο.  

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό σενάριο: λήψη μιας βαριάς σελίδας HTML, περιορισμός του βάθους με το οποίο αντλούνται ενσωματωμένοι πόροι, και τελικά αποθήκευση (ή μετατροπή) του αποτελέσματος με απόλυτο έλεγχο. Χωρίς ασαφείς αναφορές, μόνο ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο πρότζεκτ σας σήμερα.

> **Συμβουλή:** Το `SaveOptions` του Aspose.HTML λειτουργεί όχι μόνο για αποθήκευση πίσω σε HTML, αλλά και για μετατροπή σε PDF, PNG ή ακόμη και DOCX. Το ίδιο μοτίβο που καλύπτουμε παρακάτω ισχύει για όλες αυτές τις μορφές.

---

## Τι Θα Χρειαστείτε

- **Python 3.8+** (ο κώδικας χρησιμοποιεί type hints αλλά εκτελείται σε οποιαδήποτε πρόσφατη έκδοση)  
- **Aspose.HTML for Python via .NET** – εγκαταστήστε το με `pip install aspose-html`  
- Ένα **μεγάλο αρχείο HTML** που θέλετε να μειώσετε ή να μετασχηματίσετε (το παράδειγμα χρησιμοποιεί το `big_page.html`)  
- Μια μέτρια ποσότητα χώρου στο δίσκο για το αρχείο εξόδου  

Αυτό είναι όλο—χωρίς επιπλέον βιβλιοθήκες, χωρίς βαριά εργαλεία κατασκευής.

---

## Πώς να Χρησιμοποιήσετε το SaveOptions με Επιλογές Διαχείρισης Πόρων

Αυτή είναι η ουσία του ζητήματος. Θα δημιουργήσουμε ένα αντικείμενο `SaveOptions`, θα προσθέσουμε ένα αντικείμενο `ResourceHandlingOptions` που λέει στο Aspose.HTML πόσο βαθιά πρέπει να ακολουθεί συνδεδεμένα στοιχεία, και τέλος θα περάσουμε τα πάντα στη μέθοδο `save` του εγγράφου.

```python
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

# Load the source HTML document
input_path = "YOUR_DIRECTORY/big_page.html"
doc = HTMLDocument(input_path)

# Define how deep nested resources should be processed (limit to 3 levels)
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # <-- controls depth of resource fetching

# Attach the resource handling configuration to the save options
save_options = SaveOptions()
save_options.resource_handling_options = resource_options

# Save the processed document (or convert to another format if desired)
output_path = "YOUR_DIRECTORY/big_page_processed.html"
doc.save(output_path, save_options)
```

**Γιατί λειτουργεί αυτό:**  
- Το `HTMLDocument` φορτώνει το αρχικό αρχείο, αναλύοντας κάθε `<img>`, `<link>`, `<script>` κ.λπ.  
- Η ιδιότητα `ResourceHandlingOptions.max_handling_depth` λέει στη μηχανή να σταματήσει να ακολουθεί πόρους μετά από τρία επίπεδα εμφώλευσης—ιδανικό για αποφυγή άπειρων βρόχων σε σελίδες που ενσωματώνουν άλλες σελίδες.  
- Το `SaveOptions` είναι το δοχείο που μεταφέρει τόσο τη μορφή εξόδου (HTML από προεπιλογή) όσο και τους κανόνες διαχείρισης πόρων.  
- Τέλος, το `doc.save` γράφει το νέο αρχείο, εφαρμόζοντας τους κανόνες που μόλις ορίσαμε.

Όταν εκτελέσετε το script, θα δείτε ένα νέο αρχείο στο `big_page_processed.html`. Ανοίξτε το σε πρόγραμμα περιήγησης· θα παρατηρήσετε ότι όλες οι εικόνες, τα στυλ και τα scripts μέχρι τρία επίπεδα βάθους είναι ακόμη παρόντα, ενώ οι πιο βαθιές αναφορές έχουν αφαιρεθεί. Αυτό μειώνει δραστικά το μέγεθος του αρχείου χωρίς να σπάσει η βασική διάταξη της σελίδας—ακριβώς ό,τι χρειάζεστε όταν **μετατρέπετε μεγάλη σελίδα HTML** για χρήση εκτός σύνδεσης ή αποστολή μέσω email.

---

## Αποδοτική Μετατροπή Μεγάλης Σελίδας HTML

Αν ο στόχος σας είναι η *μετατροπή μεγάλης σελίδας HTML* σε μια πιο ελαφριά έκδοση, το παραπάνω απόσπασμα κάνει ήδη το μεγαλύτερο μέρος της δουλειάς. Ωστόσο, ίσως θέλετε να αλλάξετε τελείως τη μορφή εξόδου. Το Aspose.HTML το κάνει με μία γραμμή:

```python
# Convert to PDF instead of HTML
pdf_save_options = SaveOptions()
pdf_save_options.resource_handling_options = resource_options
pdf_save_options.format = "PDF"   # specify desired format

doc.save("YOUR_DIRECTORY/big_page.pdf", pdf_save_options)
```

Απλώς αντικαταστήστε την ιδιότητα `format` με `"PNG"`, `"JPEG"` ή `"DOCX"` και έχετε μια πλήρη γραμμή μετατροπής. Οι ίδιες **εφαρμογή διαχείρισης πόρων** παραμένουν αμετάβλητες, έτσι το παραγόμενο PDF δεν θα ενσωματώνει κάθε εξωτερικό αρχείο CSS από τον αρχικό ιστότοπο—μόνο εκείνα που βρίσκονται εντός του τριών‑επίπεδου βάθους που ορίσατε.

---

## Εφαρμογή Διαχείρισης Πόρων σε Ενσωματωμένους Πόρους

Ας εμβαθύνουμε λίγο περισσότερο στην **εφαρμογή διαχείρισης πόρων** αποτελεσματικά. Υποθέστε ότι το HTML σας περιέχει ένα stylesheet που με τη σειρά του εισάγει άλλα stylesheets, το καθένα τραβώντας εικόνες. Χωρίς όριο βάθους, το Aspose.HTML θα μπορούσε να ακολουθεί την αλυσίδα ατέρμονα, φουσκώνοντας τη μνήμη και τη χρήση CPU.

```python
# Example: limit to 1 level for aggressive trimming
resource_options.max_handling_depth = 1
save_options.resource_handling_options = resource_options
doc.save("trimmed_page.html", save_options)
```

- **Βάθος 0** – Δεν ανακτώνται εξωτερικοί πόροι· παίρνετε ένα κενό σκελετό HTML.  
- **Βάθος 1** – Συμπεριλαμβάνονται μόνο πόροι πρώτου επιπέδου (άμεσες ετικέτες `<img>`, άμεσα CSS αρχεία).  
- **Βάθος 2+** – Σεβασμός σε πιο βαθιά εμφώλευση, χρήσιμο για σύνθετους ιστότοπους όπου τα στυλ εξαρτώνται από άλλα στυλ.

Επιλέξτε το βάθος που ταιριάζει στο σενάριο **μετατροπής μεγάλης σελίδας HTML** σας. Για ενημερωτικά δελτία email, το βάθος 1 είναι συχνά αρκετό. Για τοπικό αρχείο, το βάθος 3 (όπως στο κύριο παράδειγμα) προσφέρει καλή ισορροπία.

---

## Πλήρες Παράδειγμα Εργασίας – Από την Αρχή μέχρι το Τέλος

Παρακάτω υπάρχει ένα αυτόνομο script που μπορείτε να αποθηκεύσετε σε ένα αρχείο με όνομα `process_html.py`. Περιλαμβάνει διαχείριση σφαλμάτων, καταγραφή (logging) και έναν μικρό βοηθό που εκτυπώνει τη μείωση μεγέθους που πετύχατε.

```python
import os
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

def process_html(
    src_path: str,
    dst_path: str,
    depth: int = 3,
    fmt: str = "HTML"
) -> None:
    """
    Loads an HTML file, applies resource handling, and saves it in the requested format.
    Returns nothing; prints size statistics for quick verification.
    """
    if not os.path.isfile(src_path):
        raise FileNotFoundError(f"Source file not found: {src_path}")

    # Load document
    doc = HTMLDocument(src_path)

    # Set up resource handling
    res_opts = ResourceHandlingOptions()
    res_opts.max_handling_depth = depth

    # Configure save options (including format)
    save_opts = SaveOptions()
    save_opts.resource_handling_options = res_opts
    save_opts.format = fmt.upper()   # Aspose expects upper‑case format strings

    # Perform save / conversion
    doc.save(dst_path, save_opts)

    # Report size change
    original = os.path.getsize(src_path)
    final = os.path.getsize(dst_path)
    reduction = (original - final) / original * 100
    print(f"Saved {fmt.lower()} to '{dst_path}'. Size reduced by {reduction:.2f}%.")

# -------------------------------------------------------------------------
# Example usage
if __name__ == "__main__":
    input_file = "YOUR_DIRECTORY/big_page.html"
    output_file = "YOUR_DIRECTORY/big_page_processed.html"

    process_html(
        src_path=input_file,
        dst_path=output_file,
        depth=3,          # apply resource handling up to three levels
        fmt="HTML"       # change to "PDF" or "PNG" to convert format
    )
```

**Αναμενόμενη έξοδος (κονσόλα):**

```
Saved html to 'YOUR_DIRECTORY/big_page_processed.html'. Size reduced by 42.57%.
```

Ανοίξτε το επεξεργασμένο αρχείο· θα δείτε μια πιο ελαφριά σελίδα που εξακολουθεί να μοιάζει με την αρχική. Αν αλλάξετε το `fmt` σε `"PDF"`, η κονσόλα θα αναφέρει το μέγεθος του αρχείου PDF και μπορείτε να το ανοίξετε σε οποιονδήποτε PDF viewer.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

- **Τι γίνεται αν η σελίδα αναφέρει πόρους μέσω HTTPS που απαιτούν πιστοποίηση;**  
  Το Aspose.HTML ακολουθεί ανακατευθύνσεις αλλά δεν στέλνει διαπιστευτήρια αυτόματα. Μπορείτε να προ‑κατεβάσετε αυτά τα στοιχεία ή να χρησιμοποιήσετε έναν προσαρμοσμένο `WebRequest` handler (πέρα από το εύρος αυτού του οδηγού).

- **Μπορώ να διατηρήσω το ενσωματωμένο CSS ενώ αφαιρώ τα εξωτερικά αρχεία;**  
  Ναι—ορίστε `resource_options.max_handling_depth = 0`. Αυτό παραλείπει τα εξωτερικά αρχεία αλλά αφήνει άθικτα τυχόν `<style>` blocks.

- **Τι γίνεται με πολύ μεγάλες εικόνες που εξακολουθούν να αυξάνουν το μέγεθος του εξόδου;**  
  Μετά την αποθήκευση, μπορείτε να εκτελέσετε ένα δευτερεύον πέρασμα με το Pillow για να μειώσετε την ανάλυση των εικόνων, ή να αφήσετε τις ενσωματωμένες επιλογές συμπίεσης εικόνας του Aspose.HTML (χρησιμοποιήστε `save_options.image_quality`).

- **Εφαρμόζεται το όριο βάθους ανά τύπο πόρου;**  
  Το όριο είναι καθολικό για όλους τους τύπους πόρων (εικόνες, scripts, styles). Αν χρειάζεστε πιο λεπτομερή έλεγχο, θα πρέπει να φιλτράρετε τους πόρους χειροκίνητα μετά τη φόρτωση του εγγράφου.

---

## Συμπέρασμα

Τώρα έχετε μια σταθερή κατανόηση του **πώς να χρησιμοποιήσετε το SaveOptions** στο Aspose.HTML


## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [How to Convert HTML to MHTML with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}