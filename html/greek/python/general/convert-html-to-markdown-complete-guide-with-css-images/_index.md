---
category: general
date: 2026-06-10
description: Μετατρέψτε το HTML σε Markdown με CSS και εικόνες σε ένα ενιαίο script.
  Μάθετε βήμα‑βήμα πώς να διατηρήσετε τα στυλ, τα εξωτερικά στοιχεία και να αποκτήσετε
  καθαρό Markdown.
draft: false
keywords:
- convert html to markdown
- convert html with css
- how to convert html with images
language: el
og_description: Μετατρέψτε το HTML σε Markdown διατηρώντας το CSS και τις εικόνες.
  Αυτός ο οδηγός εμφανίζει τον πλήρη κώδικα, εξηγεί κάθε επιλογή και παρέχει ένα έτοιμο
  προς εκτέλεση παράδειγμα.
og_title: Μετατροπή HTML σε Markdown – Πλήρης οδηγός με CSS & εικόνες
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Convert HTML to Markdown with CSS and images in a single script. Learn
    step‑by‑step how to preserve styles, external assets, and get clean Markdown.
  headline: Convert HTML to Markdown – Complete Guide with CSS & Images
  type: TechArticle
- description: Convert HTML to Markdown with CSS and images in a single script. Learn
    step‑by‑step how to preserve styles, external assets, and get clean Markdown.
  name: Convert HTML to Markdown – Complete Guide with CSS & Images
  steps:
  - name: Expected Result
    text: 'After the script finishes, you should see:'
  - name: What if my HTML uses inline `data:` URIs for images?
    text: The converter treats data URIs as embedded resources and will **not** write
      them to the `resources` folder by default. If you need them extracted, set `res_opts.inline_images
      = False` (or the library’s equivalent) before step 2.
  - name: How do I keep the original CSS file linked in the Markdown?
    text: 'After conversion, add a reference at the top of your Markdown:'
  - name: Can I convert multiple HTML files in one run?
    text: Sure. Wrap the four steps in a `for` loop, change the input and output paths
      each iteration, and reuse the same `options` object. Just make sure each HTML
      file has its own dedicated `resource_folder` to avoid collisions.
  type: HowTo
tags:
- HTML
- Markdown
- Python
title: Μετατροπή HTML σε Markdown – Πλήρης Οδηγός με CSS & Εικόνες
url: /el/python/general/convert-html-to-markdown-complete-guide-with-css-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή HTML σε Markdown – Πλήρης Οδηγός με CSS & Εικόνες

Κάποτε χρειάστηκε να **μετατρέψετε HTML σε Markdown** αλλά ανησυχείτε ότι θα χάσετε το στυλ CSS ή τις ενσωματωμένες εικόνες; Δεν είστε μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν προσπαθούν να μεταφέρουν περιεχόμενο από μια ιστοσελίδα σε ένα ελαφρύ αρχείο Markdown για στατικούς δημιουργούς ιστοτόπων, τεκμηρίωση ή σημειώσεις ελεγχόμενες από έκδοση.

Τα καλά νέα; Με λίγες γραμμές Python και τη σωστή βιβλιοθήκη, μπορείτε να **μετατρέψετε HTML σε Markdown** ενώ αυτόματα αντιγράφετε εξωτερικά στοιχεία, διατηρείτε το CSS και κρατάτε κάθε εικόνα άθικτη. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πρακτικό script copy‑and‑paste που λύνει ακριβώς αυτό το πρόβλημα, και θα εξηγήσουμε γιατί κάθε ρύθμιση είναι σημαντική. Στο τέλος θα μπορείτε να τρέξετε τον μετατροπέα σε οποιοδήποτε αρχείο HTML και να έχετε ένα καθαρό αρχείο `.md` συν ένα φάκελο `resources` γεμάτο με τα αρχικά στοιχεία.

> **Τι θα λάβετε:** ένα πλήρως λειτουργικό παράδειγμα Python, ανάλυση των `resource_handling_options`, συμβουλές για την αντιμετώπιση ειδικών περιπτώσεων, και προτάσεις για επόμενα βήματα όπως η προσαρμογή του CSS ή η διαχείριση ενσωματωμένων data URIs.

## Προαπαιτούμενα

- Python 3.8+ εγκατεστημένο στο σύστημά σας.  
- Το **Aspose.HTML for Python via .NET** (ή οποιαδήποτε παρόμοια βιβλιοθήκη που παρέχει `HTMLDocument`, `MarkdownSaveOptions`, κλπ.). Εγκαταστήστε το με:

```bash
pip install aspose-html
```

- Ένα αρχείο HTML που θέλετε να μετατρέψετε, κατά προτίμηση με εξωτερικά CSS και αναφορές εικόνων, π.χ. `sample_with_images.html`.  
- Δικαιώματα εγγραφής στον φάκελο εξόδου.

Αν χρησιμοποιείτε διαφορετική βιβλιοθήκη, οι έννοιες παραμένουν οι ίδιες – απλώς αντιστοιχίστε τα ονόματα κλάσεων ανάλογα.

## Βήμα 1: Φόρτωση του HTML Document

Το πρώτο που κάνουμε είναι να δημιουργήσουμε ένα αντικείμενο `HTMLDocument` που δείχνει στο αρχείο προέλευσης. Αυτό το αντικείμενο αναλύει το markup, δημιουργεί ένα DOM και προετοιμάζει τα πάντα για μετατροπή.

```python
# Step 1: Load the HTML document
doc = HTMLDocument("YOUR_DIRECTORY/sample_with_images.html")
```

*Γιατί είναι σημαντικό:* Η φόρτωση του εγγράφου δίνει στον μετατροπέα μια σαφή αναπαράσταση της σελίδας, συμπεριλαμβανομένων των συνδέσμων σε εξωτερικά αρχεία CSS και ετικετών εικόνας. Χωρίς αυτό το βήμα, ο μετατροπέας δεν θα ήξερε ποια στοιχεία πρέπει να αντιγραφούν.

## Βήμα 2: Διαμόρφωση Διαχείρισης Πόρων (CSS & Εικόνες)

Στη συνέχεια ρυθμίζουμε το `ResourceHandlingOptions`. Αυτό είναι η καρδιά του τμήματος **convert html with css** και **how to convert html with images** του tutorial. Με την ενεργοποίηση του `save_external_resources` και την καθοδήγηση σε έναν φάκελο, η βιβλιοθήκη θα κατεβάσει αυτόματα κάθε συνδεδεμένο stylesheet, εικόνα και γραμματοσειρά.

```python
# Step 2: Set up resource handling to copy external assets (images, CSS, fonts)
res_opts = ResourceHandlingOptions()
res_opts.save_external_resources = True          # Enable copying of external resources
res_opts.resource_folder = "YOUR_DIRECTORY/resources"
```

*Γιατί είναι σημαντικό:* Αν παραλείψετε αυτή τη ρύθμιση, το παραγόμενο Markdown θα περιέχει σπασμένους συνδέσμους και οποιοδήποτε στυλ ορισμένο σε εξωτερικά αρχεία CSS θα χαθεί. Η ενεργοποίηση του `save_external_resources` εγγυάται ότι όταν ανοίξετε αργότερα το Markdown, οι εικόνες θα εμφανιστούν και το CSS μπορεί να επανασυνδεθεί αν χρειαστεί.

## Βήμα 3: Σύνδεση Επιλογών Πόρων με τις Markdown Save Options

Τώρα ενσωματώνουμε τις επιλογές πόρων στο `MarkdownSaveOptions`. Σκεφτείτε το ως το να λέτε στον μετατροπέα: «Όταν γράψεις το αρχείο `.md`, σεβάσου και τους κανόνες πόρων που ορίσαμε».

```python
# Step 3: Attach the resource options to the Markdown save options
options = MarkdownSaveOptions()
options.resource_handling_options = res_opts
```

*Γιατί είναι σημαντικό:* Το αντικείμενο `MarkdownSaveOptions` περιέχει όλες τις ρυθμίσεις που μπορείτε να προσαρμόσετε για τη διαδικασία μετατροπής – από στυλ επικεφαλίδων μέχρι μορφές συνδέσμων. Συνδέοντας το `resource_handling_options`, διασφαλίζετε ότι ο μετατροπέας θα ακολουθήσει τη συμπεριφορά αντιγραφής πόρων καθ' όλη τη διάρκεια της λειτουργίας.

## Βήμα 4: Εκτέλεση της Μετατροπής

Τέλος, καλούμε τη στατική μέθοδο `convert_html`, περνώντας το έγγραφο, τις επιλογές και τη διαδρομή εξόδου. Η μέθοδος γράφει το αρχείο Markdown και δημιουργεί τον φάκελο `resources` δίπλα του.

```python
# Step 4: Convert the HTML document to Markdown, saving resources alongside the file
Converter.convert_html(doc, options, "YOUR_DIRECTORY/with_resources.md")
```

*Γιατί είναι σημαντικό:* Αυτή η μοναδική γραμμή κάνει το «βαρύ» έργο – αναλύει το HTML, μετατρέπει τις ετικέτες σε σύνταξη Markdown, ξαναγράφει τις URL των εικόνων ώστε να δείχνουν στον νέο φάκελο πόρων, και διατηρεί τυχόν αναφορές CSS που μπορεί να θέλετε να ξαναχρησιμοποιήσετε αργότερα.

### Αναμενόμενο Αποτέλεσμα

Μετά την ολοκλήρωση του script, θα δείτε:

- `with_resources.md` – ένα καθαρό αρχείο Markdown του οποίου οι σύνδεσμοι εικόνας έχουν τη μορφή `![Alt text](resources/image1.png)`.
- `resources/` – φάκελος που περιέχει κάθε εξωτερικό αρχείο CSS, εικόνα και γραμματοσειρά που αναφερόταν στο αρχικό HTML.

Ανοίξτε το αρχείο `.md` σε οποιονδήποτε προβολέα Markdown (VS Code, GitHub, MkDocs) και θα δείτε το περιεχόμενο της αρχικής σελίδας, τις εικόνες να εμφανίζονται, και μπορείτε ακόμη να συνδέσετε το αρχείο CSS χειροκίνητα αν χρειάζεστε στυλιζαρισμένη απόδοση.

---

## Συχνές Ερωτήσεις & Ειδικές Περιπτώσεις

### Τι γίνεται αν το HTML μου χρησιμοποιεί ενσωματωμένα `data:` URIs για εικόνες;

Ο μετατροπέας αντιμετωπίζει τα data URIs ως ενσωματωμένους πόρους και **δεν** θα τα γράψει στον φάκελο `resources` από προεπιλογή. Αν χρειάζεστε την εξαγωγή τους, ορίστε `res_opts.inline_images = False` (ή το ισοδύναμο της βιβλιοθήκης) πριν το βήμα 2.

### Πώς μπορώ να διατηρήσω το αρχικό αρχείο CSS συνδεδεμένο στο Markdown;

Μετά τη μετατροπή, προσθέστε μια αναφορά στην κορυφή του Markdown:

```markdown
<link rel="stylesheet" href="resources/style.css">
```

Επειδή ενεργοποιήσαμε το `save_external_resources`, το αρχείο `style.css` βρίσκεται τώρα στο `resources/`, οπότε ο σύνδεσμος λειτουργεί τοπικά.

### Μπορώ να μετατρέψω πολλά αρχεία HTML σε μία εκτέλεση;

Βεβαίως. Τυλίξτε τα τέσσερα βήματα μέσα σε έναν βρόχο `for`, αλλάξτε τις διαδρομές εισόδου/εξόδου σε κάθε επανάληψη, και επαναχρησιμοποιήστε το ίδιο αντικείμενο `options`. Απλώς βεβαιωθείτε ότι κάθε αρχείο HTML έχει το δικό του φάκελο `resource_folder` για να αποφύγετε συγκρούσεις.

---

## Συμβουλές & Παγίδες

- **Συμβουλή:** Χρησιμοποιήστε ένα σύντομο, μοναδικό όνομα `resource_folder` ανά μετατροπή (π.χ. `resources_page1`) ώστε να αποτρέψετε την αντικατάσταση αρχείων όταν επεξεργάζεστε πολλές σελίδες ταυτόχρονα.
- **Προσοχή για:** Σελίδες HTML που αναφέρονται στο ίδιο αρχείο CSS από διαφορετικούς καταλόγους. Ο μετατροπέας θα αντιγράψει το αρχείο μία φορά ανά φάκελο εξόδου, οπότε μπορεί να καταλήξετε με διπλότυπα. Συγκεντρώστε τα χειροκίνητα μετά τη μετατροπή αν ο χώρος στο δίσκο είναι πρόβλημα.
- **Συμβουλή απόδοσης:** Αν χρειάζεστε μόνο εικόνες και όχι CSS, ορίστε `res_opts.save_css = False`. Αυτό παραλείπει περιττές αντιγραφές αρχείων και επιταχύνει τη διαδικασία.

---

## Συμπέρασμα

Τώρα έχετε ένα πλήρες, έτοιμο‑για‑εκτέλεση script που **convert html to markdown** διατηρώντας το στυλ CSS και όλες τις ενσωματωμένες εικόνες. Με τη διαμόρφωση του `ResourceHandlingOptions` και την ενσωμάτωσή του στα `MarkdownSaveOptions`, η μετατροπή διαχειρίζεται αυτόματα τόσο το **convert html with css** όσο και το **how to convert html with images**.

Δοκιμάστε: αλλάξτε τη μορφή εξόδου (π.χ. `MarkdownSaveOptions` → `PlainTextSaveOptions`), τροποποιήστε τη δομή του φακέλου πόρων, ή ενσωματώστε το script σε μια μεγαλύτερη αλυσίδα δημιουργίας στατικού ιστότοπου. Η βασική ιδέα — η ρητή διαχείριση εξωτερικών πόρων — ισχύει για οποιοδήποτε workflow μετατροπής HTML‑σε‑Markdown.

Έχετε περισσότερες ερωτήσεις; Αφήστε ένα σχόλιο και καλή μετατροπή!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}