---
category: general
date: 2026-10-02
description: Μάθετε πώς να δημιουργήσετε ένα έγγραφο SVG με την Python, να αποθηκεύσετε
  το SVG σε αρχείο και να εξάγετε την εικόνα SVG με ένα σύντομο, πλήρες σενάριο.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG to file
- how to generate SVG
- export SVG image
- SVG Python tutorial
language: el
lastmod: 2026-10-02
og_description: Δημιουργήστε έγγραφο SVG στην Python και εξάγετε εικόνα SVG με αυτό
  το πρακτικό σεμινάριο. Ακολουθήστε το σενάριο, αποθηκεύστε το SVG σε αρχείο και
  επαναχρησιμοποιήστε το διανυσματικό γραφικό άμεσα.
og_image_alt: Screenshot of a Python script that creates an SVG document
og_title: Δημιουργία εγγράφου SVG σε Python – βήμα‑βήμα οδηγός
schemas:
- author: Aspose
  dateModified: '2026-10-02'
  description: Learn how to create SVG document in Python, save SVG to file, and export
    SVG image with a short, complete script.
  headline: How to create SVG document and export it as an image in Python
  type: TechArticle
tags:
- SVG
- Python
- graphics
title: Πώς να δημιουργήσετε έγγραφο SVG και να το εξάγετε ως εικόνα σε Python
url: /el/python/general/how-to-create-svg-document-and-export-it-as-an-image-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε έγγραφο SVG και να το εξάγετε ως εικόνα σε Python

Αν χρειάζεστε **να δημιουργήσετε έγγραφο SVG** προγραμματιστικά, αυτό το σεμινάριο σας δείχνει ακριβώς πώς να το κάνετε με Python. Θα δείτε ένα πλήρες σενάριο που δημιουργεί έναν απλό κύκλο, αποθηκεύει το SVG σε αρχείο και παράγει μια εξαγώγιμη εικόνα SVG που μπορείτε να ενσωματώσετε οπουδήποτε.

Η δημιουργία διανυσματικών γραφικών από κώδικα αφαιρεί την ανάγκη χειροκίνητης σχεδίασης σχημάτων σε επεξεργαστή GUI. Στο τέλος αυτού του οδηγού θα μπορείτε να ενσωματώσετε τη δημιουργία SVG σε pipelines οπτικοποίησης δεδομένων, αυτοματοποιημένους δημιουργούς αναφορών ή οποιοδήποτε έργο που απαιτεί καθαρά, ανεξάρτητα από την ανάλυση γραφικά.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

- Python 3.8 ή νεότερη έκδοση εγκατεστημένη
- Τη βιβλιοθήκη `svgwrite` (εγκατάσταση με `pip install svgwrite`)
- Δικαιώματα εγγραφής στον φάκελο όπου θα αποθηκευτεί το SVG

Αυτές οι απαιτήσεις κρατούν το παράδειγμα ελαφρύ και συμβατό με τις περισσότερες περιβάλλοντα.

## Βήμα 1: Εγκατάσταση και εισαγωγή της βιβλιοθήκης SVG

Το πρώτο βήμα είναι η προσθήκη της τρίτης‑πλευράς βιβλιοθήκης που παρέχει ένα βολικό API για τη δημιουργία SVG.

```python
# Install the library (run once in your terminal)
# pip install svgwrite

import svgwrite  # Provides the SVGDocument class and element helpers
```

Η `svgwrite` αφαιρεί την πολυπλοκότητα της XML δομής ενός αρχείου SVG, επιτρέποντάς σας να εστιάσετε στη γεωμετρία αντί για το ακατέργαστο markup.

## Βήμα 2: Δημιουργία αντικειμένου εγγράφου SVG

Τώρα μπορείτε **να δημιουργήσετε έγγραφο SVG** δημιουργώντας ένα στιγμιότυπο του `svgwrite.Drawing`. Αυτό το αντικείμενο αντιπροσωπεύει το ριζικό στοιχείο `<svg>` και περιέχει όλα τα επόμενα σχήματα.

```python
# Step 2: Initialize the SVG document
dwg = svgwrite.Drawing(
    filename="circle.svg",     # Desired output file name
    size=("100px", "100px"),   # Width and height of the canvas
    viewBox=("0 0 100 100")    # Coordinate system for drawing
)
```

Το όρισμα `size` ορίζει τις διαστάσεις σε εικονοστοιχεία που θα αποδοθούν, ενώ το `viewBox` καθορίζει ένα σύστημα συντεταγμένων που ταιριάζει με τη γεωμετρία που θα ορίσετε αργότερα.

## Βήμα 3: Προσθήκη στοιχείου κύκλου

Ένας κύκλος ορίζεται από το κέντρο του (`cx`, `cy`) και την ακτίνα (`r`). Χρησιμοποιήστε τη βοηθητική μέθοδο `circle` για να προσθέσετε αυτά τα χαρακτηριστικά.

```python
# Step 3: Create a <circle> element
circle = dwg.circle(
    center=("50", "50"),   # cx = 50, cy = 50
    r="40",                # radius = 40
    fill="lightcoral",     # Fill color for visual clarity
    stroke="black",        # Outline color
    stroke_width="2"
)

# Append the circle to the SVG root
dwg.add(circle)
```

Ο κύκλος βρίσκεται στο κέντρο του καμβά 100 × 100, αφήνοντας ένα περιθώριο 10 pixel σε κάθε πλευρά. Προσαρμόστε το `fill` και το `stroke` ώστε να ταιριάζουν με τη γλώσσα σχεδίασής σας.

## Βήμα 4: Αποθήκευση του SVG σε αρχείο

Με το γραφικό έτοιμο, μπορείτε **να αποθηκεύσετε το SVG σε αρχείο** χρησιμοποιώντας τη μέθοδο `save`. Αυτό γράφει ένα σωστά δομημένο XML που καταλαβαίνουν οι browsers και οι επεξεργαστές διανυσματικών γραφικών.

```python
# Step 4: Persist the SVG document
dwg.save()
print("SVG file saved as circle.svg")
```

Το αρχείο `circle.svg` βρίσκεται τώρα στον τρέχοντα φάκελο εργασίας. Μπορείτε να το ανοίξετε σε έναν web browser, το Inkscape ή οποιοδήποτε εργαλείο που υποστηρίζει τη μορφή SVG.

## Βήμα 5: Επαλήθευση της εξαγόμενης εικόνας SVG

Ανοίξτε το αποθηκευμένο αρχείο σε έναν browser για να επιβεβαιώσετε το αποτέλεσμα. Θα πρέπει να δείτε έναν κεντρικό κύκλο με τα καθορισμένα χρώματα. Το ακατέργαστο XML είναι ως εξής:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg width="100px" height="100px" viewBox="0 0 100 100"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40"
          fill="lightcoral" stroke="black" stroke-width="2"/>
</svg>
```

Επειδή το SVG είναι διανυσματικό, μπορείτε να κλιμακώσετε την εικόνα χωρίς απώλεια ποιότητας, καθιστώντας το ιδανικό για ανταποκρινόμενα web designs ή εκτυπώσεις υψηλής ανάλυσης.

## Συμβουλή επαγγελματία: Εξαγωγή SVG ως PNG ή JPEG

Αν χρειάζεστε μια ραστερική έκδοση, συνδυάστε το αρχείο SVG με ένα εργαλείο μετατροπής όπως το **CairoSVG**:

```python
# Optional: Convert SVG to PNG
# pip install cairosvg
import cairosvg

cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

Αυτό το βήμα δείχνει **την εξαγωγή εικόνας SVG** σε μορφή bitmap, χρήσιμο όταν τα επόμενα συστήματα δεν μπορούν να αποδώσουν SVG άμεσα.

## Συνηθισμένες παραλλαγές και ειδικές περιπτώσεις

| Παραλλαγή | Πώς να το διαχειριστείτε |
|-----------|--------------------------|
| Πολλαπλά σχήματα | Καλέστε `dwg.add()` για κάθε νέο στοιχείο (rect, line, path). |
| Δυναμικές διαστάσεις | Υπολογίστε `size` και `viewBox` από τα δεδομένα πριν δημιουργήσετε το `Drawing`. |
| Ετικέτες κειμένου | Χρησιμοποιήστε `dwg.text("Label", insert=("10", "20"))` και μορφοποιήστε με `font_size` και `fill`. |
| Επαναχρησιμοποίηση του εγγράφου | Κρατήστε το αντικείμενο `Drawing` στη μνήμη και καλέστε `save()` όποτε χρειάζεστε ενημερωμένο αρχείο. |
| Μεγάλα αρχεία | Ροή εξόδου χρησιμοποιώντας `dwg.tostring()` και γράψτε σε αντικείμενο αρχείου χειροκίνητα για αποφυγή αιχμών μνήμης. |

Η αντιμετώπιση αυτών των σεναρίων εξασφαλίζει ότι το **σενάριο δημιουργίας SVG** σας κλιμακώνεται από απλά εικονίδια έως πολύπλοκα διαγράμματα.

## Πλήρης επανάληψη κώδικα

Παρακάτω βρίσκεται το πλήρες, εκτελέσιμο παράδειγμα που ενσωματώνει όλα τα βήματα και την προαιρετική μετατροπή:

```python
# Full SVG creation script – create SVG document, save SVG to file, export SVG image
import svgwrite
import cairosvg  # Optional, only needed for PNG conversion

# Initialize the drawing (SVG document)
dwg = svgwrite.Drawing(
    filename="circle.svg",
    size=("100px", "100px"),
    viewBox=("0 0 100 100")
)

# Define a circle element
circle = dwg.circle(
    center=("50", "50"),
    r="40",
    fill="lightcoral",
    stroke="black",
    stroke_width="2"
)

# Add the circle to the document
dwg.add(circle)

# Save the SVG file
dwg.save()
print("SVG file saved as circle.svg")

# Optional: convert SVG to PNG (export SVG image)
cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

Η εκτέλεση αυτού του σεναρίου παράγει το `circle.svg` και, αν είναι εγκατεστημένο το `cairosvg`, το `circle.png`. Και τα δύο αρχεία είναι έτοιμα για ενσωμάτωση σε ιστοσελίδες, αναφορές ή περαιτέρω επεξεργασία.

## Συμπέρασμα

Τώρα ξέρετε πώς να **δημιουργήσετε έγγραφο SVG** σε Python, **να αποθηκεύσετε SVG σε αρχείο**, και **να εξάγετε εικόνα SVG** για ευρύτερη χρήση. Το παράδειγμα καλύπτει τις βασικές κλήσεις API, εξηγεί γιατί κάθε βήμα είναι σημαντικό και προσφέρει επεκτάσεις για πιο σύνθετα γραφικά.

Στη συνέχεια, εξερευνήστε επιπλέον θέματα του **SVG Python tutorial** όπως η σχεδίαση μονοπατιών, η εφαρμογή διαβαθμίσεων χρωμάτων και η κίνηση στοιχείων. Η ενσωμάτωση αυτών των τεχνικών θα σας επιτρέψει να δημιουργείτε δυναμικά, δεδομένα‑κινητά διανυσματικά γραφικά απευθείας από τις εφαρμογές σας σε Python. Καλό προγραμματισμό!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω σεμινάρια καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Δημιουργία και διαχείριση εγγράφων SVG στο Aspose.HTML για Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [Αποθήκευση εγγράφου SVG στο Aspose.HTML για Java](/html/english/java/saving-html-documents/save-svg-document/)
- [svg to png java – Μετατροπή SVG σε εικόνα με Aspose.HTML για Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}