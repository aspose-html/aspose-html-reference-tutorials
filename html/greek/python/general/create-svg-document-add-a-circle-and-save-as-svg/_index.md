---
category: general
date: 2026-07-31
description: Μάθετε πώς να δημιουργήσετε ένα έγγραφο SVG, να προσθέσετε έναν κύκλο
  και να αποθηκεύσετε γρήγορα το αρχείο SVG. Εξάγετε το γραφικό ως SVG με λίγες γραμμές
  κώδικα Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg document
- save svg file
- export graphic as svg
- add circle to svg
language: el
lastmod: 2026-07-31
og_description: Δημιουργήστε έγγραφο SVG, προσθέστε έναν κύκλο και αποθηκεύστε το
  αρχείο SVG σε δευτερόλεπτα. Αυτός ο οδηγός σας δείχνει πώς να εξάγετε το γραφικό
  ως SVG με σαφή, εκτελέσιμο κώδικα.
og_image_alt: Screenshot of a red circle inside an SVG file named circle.svg
og_title: Δημιουργία εγγράφου SVG – Προσθήκη κύκλου και αποθήκευση ως SVG
schemas:
- author: Aspose
  dateModified: '2026-07-31'
  description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  headline: Create SVG Document – Add a Circle and Save as SVG
  type: TechArticle
- description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  name: Create SVG Document – Add a Circle and Save as SVG
  steps:
  - name: Pro tip
    text: If you plan to generate many files in a loop, give each `Drawing` a unique
      name or use `io.BytesIO` to keep everything in memory until you’re ready to
      write.
  - name: Edge case – Transparent background
    text: 'If you need a transparent background (the default for SVG), you can skip
      setting a `fill` on the root. For a white background, add:'
  - name: 'Bonus: Export graphic as SVG programmatically'
    text: 'If you need the SVG content as a string—for example, to embed it in an
      HTML email—you can call `dwg.tostring()` instead of `save()`:'
  type: HowTo
- questions:
  - answer: Swap `dwg.circle` for `dwg.rect`, `dwg.ellipse`, or even a custom `<path>`
      string. The API is consistent across shapes.
    question: What if I want a different shape?
  - answer: Absolutely. The file you just created can be referenced with `<img src="circle.svg"
      alt="Red circle">` or inlined with `<svg>` tags.
    question: Can I embed the SVG directly in HTML?
  - answer: You could, but libraries like `svgwrite` handle namespace quirks and make
      the code far more maintainable—especially when you start adding gradients or
      animations.
    question: Why not write raw XML?
  type: FAQPage
tags:
- svg
- python
- vector-graphics
- programming-tutorial
title: Δημιουργία εγγράφου SVG – Προσθήκη κύκλου και αποθήκευση ως SVG
url: /el/python/general/create-svg-document-add-a-circle-and-save-as-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Εγγράφου SVG – Προσθήκη Κύκλου και Αποθήκευση ως SVG

Έχετε ποτέ χρειαστεί να **create SVG document** από κώδικα αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι· πολλοί προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν πειραματίζονται για πρώτη φορά με διανυσματικά γραφικά. Σε αυτό το tutorial θα περάσουμε από ένα μικρό, αυτόνομο παράδειγμα που δείχνει πώς να **add circle to SVG**, μετά να **save SVG file** ώστε να μπορείτε να **export graphic as SVG** για χρήση στο web ή σε εργαλεία σχεδίασης.

Θα κρατήσουμε τα πράγματα ελαφριά: μόνο μερικές γραμμές Python, μια δημοφιλής βιβλιοθήκη βοηθού SVG, και μια δόση εξήγησης. Στο τέλος θα έχετε ένα έτοιμο προς χρήση `circle.svg` στον φάκελό σας, και θα καταλάβετε γιατί κάθε βήμα είναι σημαντικό—χωρίς ασαφείς συντομεύσεις “δείτε τα docs”.

## Τι Θα Χρειαστεί

- Python 3.8+ (οποιαδήποτε πρόσφατη έκδοση λειτουργεί)
- Το πακέτο `svgwrite` – εγκαταστήστε το με `pip install svgwrite`
- Ένας επεξεργαστής κειμένου ή IDE (VS Code, PyCharm, ή ακόμη και Notepad)
- Δικαίωμα εγγραφής στον κατάλογο όπου θέλετε να αποθηκευτεί το αρχείο

Αυτό είναι όλο. Χωρίς βαρύ εξαρτήματα, χωρίς εξωτερικές υπηρεσίες.

## Βήμα 1: Ρύθμιση του Εγγράφου SVG

Η δημιουργία ενός εγγράφου SVG είναι τόσο απλή όσο η δημιουργία ενός αντικειμένου `Drawing` από το `svgwrite`. Σκεφτείτε αυτό το αντικείμενο ως το κενό καμβά όπου ζει κάθε σχήμα.

```python
import svgwrite

# Step 1: Create a new SVG document (canvas) 800×800 pixels
dwg = svgwrite.Drawing(filename="circle.svg", size=("200px", "200px"))
```

> **Γιατί είναι σημαντικό:** Η κλάση `Drawing` διαχειρίζεται όλο το XML boilerplate για εσάς—χωρικά ονόματα, κεφαλίδες και το ριζικό στοιχείο `<svg>`. Καθορίζοντας ένα όνομα αρχείου εκ των προτέρων, ξέρουμε ήδη πού θα καταλήξει το αρχείο, κάτι που κάνει το επόμενο βήμα **save svg file** τετριμμένο.

### Συμβουλή Pro
Αν σκοπεύετε να δημιουργήσετε πολλά αρχεία σε βρόχο, δώστε σε κάθε `Drawing` ένα μοναδικό όνομα ή χρησιμοποιήστε `io.BytesIO` για να κρατήσετε όλα στη μνήμη μέχρι να είστε έτοιμοι να γράψετε.

## Βήμα 2: Προσθήκη Κύκλου στο SVG

Τώρα που υπάρχει το έγγραφο, ας **add circle to SVG**. Η μέθοδος `add()` δέχεται οποιοδήποτε αντικείμενο σχήματος· ένα `Circle` είναι τέλειο για μια απλή κόκκινη κουκκίδα στο κέντρο.

```python
# Step 2: Add a red circle element to the SVG root
center = (100, 100)          # x, y coordinates (half of 200px canvas)
radius = 80                  # radius in pixels
circle = dwg.circle(center=center, r=radius, fill='red')
dwg.add(circle)
```

> **Γιατί χρησιμοποιούμε τις μεταβλητές `center` και `radius`:** Η σκληρή κωδικοποίηση αριθμών κάνει τον κώδικα πιο δύσκολο στην ανάγνωση και συντήρηση. Ονομάζοντας τις τιμές, διευκρινίζουμε την πρόθεση—αυτός ο κύκλος βρίσκεται ακριβώς στο κέντρο ενός καμβά 200 × 200 και είναι αρκετά μεγάλος για να παρατηρηθεί.

### Ακραία περίπτωση – Διαφανές φόντο
Αν χρειάζεστε διαφανές φόντο (η προεπιλογή για SVG), μπορείτε να παραλείψετε τον ορισμό `fill` στο ριζικό στοιχείο. Για λευκό φόντο, προσθέστε:

```python
dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))
```

Τοποθετήστε το αυτό πριν προσθέσετε τον κύκλο ώστε το ορθογώνιο να βρίσκεται κάτω.

## Βήμα 3: Αποθήκευση του Αρχείου SVG

Με το σχήμα στη θέση του, η τελική ενέργεια είναι να **save SVG file**. Η μέθοδος `save()` γράφει το XML στο δίσκο, και επειδή ήδη δώσαμε στο `Drawing` ένα όνομα αρχείου, μια κλήση αρκεί.

```python
# Step 3: Save the SVG document to a file
dwg.save()
print("✅ circle.svg has been created in the current directory.")
```

> **Τι συμβαίνει στο παρασκήνιο;** Το `svgwrite` σειριοποιεί το δέντρο στοιχείων σε μια συμβολοσειρά, προσθέτει τη δήλωση XML, και το γράφει χρησιμοποιώντας κωδικοποίηση UTF‑8. Αν ο προορισμός δεν υπάρχει, η Python θα εγείρει `FileNotFoundError`; βεβαιωθείτε ότι η διαδρομή είναι έγκυρη ή δημιουργήστε τη με `os.makedirs()`.

### Bonus: Εξαγωγή γραφικού ως SVG προγραμματιστικά
Αν χρειάζεστε το περιεχόμενο SVG ως συμβολοσειρά—π.χ., για ενσωμάτωση σε HTML email—μπορείτε να καλέσετε `dwg.tostring()` αντί για `save()`:

```python
svg_content = dwg.tostring()
# Now you can send svg_content over a network, store it in a DB, etc.
```

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας τα όλα, εδώ είναι ένα πλήρες, έτοιμο‑για‑εκτέλεση script:

```python
import svgwrite
import os

def create_svg_with_circle(output_path: str):
    """
    Creates an SVG file containing a single red circle.
    Parameters
    ----------
    output_path: str
        Full path where the SVG file will be saved.
    """
    # Ensure the directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Initialise the SVG document (800×800 canvas)
    dwg = svgwrite.Drawing(filename=output_path, size=("200px", "200px"))

    # Optional: add a white background rectangle
    dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))

    # Add a red circle in the centre
    center = (100, 100)
    radius = 80
    circle = dwg.circle(center=center, r=radius, fill='red')
    dwg.add(circle)

    # Save the file – this is the key step to **save svg file**
    dwg.save()
    print(f"✅ SVG saved to {output_path}")

if __name__ == "__main__":
    # Change this path to wherever you want the file
    output_file = os.path.join(os.getcwd(), "circle.svg")
    create_svg_with_circle(output_file)
```

**Αναμενόμενο αποτέλεσμα:** Μετά την εκτέλεση του script, θα δείτε ένα αρχείο `circle.svg` στον ίδιο φάκελο. Ανοίγοντας το σε πρόγραμμα περιήγησης ή σε οποιονδήποτε επεξεργαστή διανυσματικών γραφικών εμφανίζεται ένας κόκκινος κύκλος κεντραρισμένος σε λευκό τετράγωνο—ακριβώς αυτό που προγραμματίσαμε.

## Συχνές Ερωτήσεις & Παγίδες

- **Τι γίνεται αν θέλω διαφορετικό σχήμα;** Αντικαταστήστε το `dwg.circle` με `dwg.rect`, `dwg.ellipse`, ή ακόμη και μια προσαρμοσμένη συμβολοσειρά `<path>`. Το API είναι συνεπές μεταξύ των σχημάτων.
- **Μπορώ να ενσωματώσω το SVG απευθείας σε HTML;** Απόλυτα. Το αρχείο που μόλις δημιουργήσατε μπορεί να αναφερθεί με `<img src="circle.svg" alt="Red circle">` ή ενσωματωμένο με ετικέτες `<svg>`.
- **Γιατί να μην γράψουμε ακατέργαστο XML;** Θα μπορούσατε, αλλά βιβλιοθήκες όπως το `svgwrite` διαχειρίζονται τις ιδιαιτερότητες των namespaces και κάνουν τον κώδικα πολύ πιο συντηρήσιμο—ειδικά όταν αρχίζετε να προσθέτετε διαβαθμίσεις ή κινούμενα σχέδια.

## Συμπέρασμα

Τώρα ξέρετε πώς να **create SVG document**, **add circle to SVG**, και **save SVG file** ώστε να μπορείτε να **export graphic as SVG** με μόνο λίγες γραμμές Python. Το μοτίβο κλιμακώνεται: αντικαταστήστε τον κύκλο με οποιοδήποτε διανυσματικό σχήμα, κάντε βρόχο πάνω σε δεδομένα για να δημιουργήσετε διαγράμματα, ή επεξεργαστείτε μαζικά πόρους για ένα σύστημα σχεδίασης.

Επόμενα βήματα; Δοκιμάστε να προσθέσετε ετικέτες κειμένου, να πειραματιστείτε με διαβαθμίσεις, ή να δημιουργήσετε μια ολόκληρη γκαλερί εικονιδίων σε ένα μόνο script. Αν είστε περίεργοι για πιο προχωρημένα χαρακτηριστικά, ρίξτε μια ματιά στην τεκμηρίωση του `svgwrite` για ομάδες (`<g>`), μετασχηματισμούς, και υποστήριξη animation.

Καλό κώδικα, και τα διανύσματά σας να παραμένουν πάντα καθαρά!

## Τι Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Αποθήκευση Εγγράφου SVG στο Aspose.HTML για Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Δημιουργία και Διαχείριση Εγγράφων SVG στο Aspose.HTML για Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg σε png java – Μετατροπή SVG σε Εικόνα με Aspose.HTML για Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}