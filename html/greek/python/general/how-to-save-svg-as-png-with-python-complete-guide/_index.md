---
category: general
date: 2026-09-29
description: Πώς να αποθηκεύσετε SVG χρησιμοποιώντας Python και να εξάγετε SVG σε
  PNG. Μάθετε να μετατρέπετε SVG σε PNG με προσαρμοσμένες επιλογές σε λίγα λεπτά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save svg
- convert svg to png
- save svg as png
- export svg to png
- vector svg to png
language: el
lastmod: 2026-09-29
og_description: Πώς να αποθηκεύσετε SVG χρησιμοποιώντας Python και να εξάγετε SVG
  σε PNG. Ακολουθήστε αυτόν τον οδηγό για να μετατρέψετε SVG σε PNG με πλήρη έλεγχο
  των επιλογών.
og_image_alt: Screenshot of Python code converting a vector SVG file to a PNG image
og_title: Πώς να αποθηκεύσετε SVG ως PNG με Python – βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: How to save SVG using Python and export SVG to PNG. Learn to convert
    SVG to PNG with fine‑tuned options in minutes.
  headline: How to save SVG as PNG with Python – complete guide
  type: TechArticle
- description: How to save SVG using Python and export SVG to PNG. Learn to convert
    SVG to PNG with fine‑tuned options in minutes.
  name: How to save SVG as PNG with Python – complete guide
  steps:
  - name: Load the SVG document
    text: '```python from aspose.svg import SVGDocument'
  - name: (Optional) Create image‑save options
    text: '```python from aspose.svg import ImageSaveOptions'
  - name: Save the SVG as PNG
    text: '```python # Export the SVG to a PNG file using the options defined above
      svg_doc.save("YOUR_DIRECTORY/vector.png", options) ```'
  - name: Full script
    text: 'Putting the pieces together yields a complete, runnable program:'
  - name: Missing file or invalid path
    text: 'If `src_path` does not exist, `SVGDocument` raises a `FileNotFoundError`.
      Wrap the call in a `try/except` block to provide a friendly error message:'
  - name: Preserving aspect ratio
    text: When only one dimension (width **or** height) is set, the library automatically
      scales the other dimension to maintain the original aspect ratio. If you set
      both dimensions, the image may stretch. Choose the approach that matches your
      UI requirements.
  - name: Transparent backgrounds
    text: 'If the original SVG relies on transparency (e.g., icons), you can keep
      the PNG transparent by omitting `background_color`:'
  type: HowTo
tags:
- Python
- SVG
- Image conversion
title: Πώς να αποθηκεύσετε SVG ως PNG με Python – πλήρης οδηγός
url: /el/python/general/how-to-save-svg-as-png-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αποθηκεύσετε SVG ως PNG με Python – πλήρης οδηγός

Αν χρειάζεστε **πώς να αποθηκεύσετε SVG** ως εικόνα raster, αυτό το tutorial σας παρουσιάζει μια έτοιμη προς εκτέλεση λύση. Θα μάθετε πώς να φορτώσετε ένα διανυσματικό αρχείο SVG, προαιρετικά να προσαρμόσετε τις ρυθμίσεις αποθήκευσης εικόνας, και να εξάγετε το αποτέλεσμα σε PNG με μόνο τρεις γραμμές κώδικα.

Η αποθήκευση αρχείων SVG ως PNG είναι συνηθισμένη όταν θέλετε να ενσωματώσετε γραφικά σε ιστοσελίδες, να δημιουργήσετε μικρογραφίες ή να τροφοδοτήσετε εικόνες raster σε pipelines μηχανικής μάθησης. Η προσέγγιση που περιγράφεται εδώ λειτουργεί σε Windows, macOS και Linux χωρίς πρόσθετες εγγενείς εξαρτήσεις.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Python 3.9 ή νεότερη έκδοση εγκατεστημένη
* Το πακέτο `aspose.svg` (το επίσημο Aspose SVG για Python μέσω .NET). Εγκαταστήστε το με:

```bash
pip install aspose-svg
```

* Ένα έγκυρο αρχείο SVG στον δίσκο (π.χ., `vector.svg`)

Αυτές οι απαιτήσεις διατηρούν το παράδειγμα αυτόνομο και αποφεύγουν εξωτερικά εργαλεία όπως το CairoSVG.

## Πώς να αποθηκεύσετε SVG με Python

Ο πυρήνας της διαδικασίας είναι τρία βήματα: φόρτωση, ρύθμιση και αποθήκευση. Οι παρακάτω ενότητες εξηγούν κάθε βήμα.

### Βήμα 1: Φόρτωση του εγγράφου SVG

```python
from aspose.svg import SVGDocument

# Load the SVG file from the local filesystem
svg_doc = SVGDocument("YOUR_DIRECTORY/vector.svg")
```

`SVGDocument` αναλύει το XML του SVG και δημιουργεί μια αναπαράσταση στη μνήμη. Η φόρτωση του αρχείου πρώτα είναι υποχρεωτική· διαφορετικά η λειτουργία αποθήκευσης δεν έχει δεδομένα προέλευσης.

### Βήμα 2: (Προαιρετικό) Δημιουργία επιλογών αποθήκευσης εικόνας

```python
from aspose.svg import ImageSaveOptions

# Create default options; you can tweak width, height, and background
options = ImageSaveOptions()
options.width = 800          # Desired output width in pixels
options.height = 600         # Desired output height in pixels
options.background_color = "#FFFFFF"  # Force a white background for transparent SVGs
```

`ImageSaveOptions` σας επιτρέπει να ρυθμίσετε λεπτομερώς την έξοδο PNG. Η προσαρμογή του πλάτους και του ύψους διατηρεί τον λόγο διαστάσεων εκτός αν ορίσετε και τα δύο ρητά. Η ρύθμιση χρώματος φόντου είναι χρήσιμη όταν το αρχικό SVG περιέχει διαφάνεια αλλά χρειάζεστε ένα αδιαφανές PNG.

### Βήμα 3: Αποθήκευση του SVG ως PNG

```python
# Export the SVG to a PNG file using the options defined above
svg_doc.save("YOUR_DIRECTORY/vector.png", options)
```

Η μέθοδος `save` γράφει ένα αρχείο PNG στη διαδρομή προορισμού. Αν παραλείψετε το όρισμα `options`, η βιβλιοθήκη χρησιμοποιεί προεπιλεγμένες διαστάσεις που προέρχονται από το viewBox του SVG.

### Πλήρες σενάριο

Συνδυάζοντας τα παραπάνω παίρνουμε ένα πλήρες, εκτελέσιμο πρόγραμμα:

```python
# -*- coding: utf-8 -*-
"""
How to save SVG as PNG with Python.
This script loads an SVG file, applies optional image‑save settings,
and exports the result to PNG.
"""

from aspose.svg import SVGDocument, ImageSaveOptions

def convert_svg_to_png(
    src_path: str,
    dst_path: str,
    width: int = 800,
    height: int = 600,
    background: str = "#FFFFFF"
) -> None:
    """Convert an SVG file to PNG with custom dimensions and background."""
    # Load the SVG document
    svg_doc = SVGDocument(src_path)

    # Prepare save options
    options = ImageSaveOptions()
    options.width = width
    options.height = height
    options.background_color = background

    # Save as PNG
    svg_doc.save(dst_path, options)


if __name__ == "__main__":
    # Example usage
    convert_svg_to_png(
        src_path="YOUR_DIRECTORY/vector.svg",
        dst_path="YOUR_DIRECTORY/vector.png",
        width=1024,
        height=768,
        background="#FFFFFF"
    )
    print("SVG successfully saved as PNG.")
```

Η εκτέλεση του σεναρίου εμφανίζει **«SVG successfully saved as PNG.»** και δημιουργεί το `vector.png` στον ίδιο φάκελο.

## Μετατροπή SVG σε PNG – αντιμετώπιση κοινών προβλημάτων

### Απουσία αρχείου ή μη έγκυρη διαδρομή

Αν το `src_path` δεν υπάρχει, το `SVGDocument` εγείρει ένα `FileNotFoundError`. Τυλίξτε την κλήση σε ένα μπλοκ `try/except` για να παρέχετε ένα φιλικό μήνυμα σφάλματος:

```python
try:
    svg_doc = SVGDocument(src_path)
except FileNotFoundError:
    raise SystemExit(f"File not found: {src_path}")
```

### Διατήρηση λόγου διαστάσεων

Όταν ορίζεται μόνο μία διάσταση (πλάτος **ή** ύψος), η βιβλιοθήκη κλιμακώνει αυτόματα την άλλη διάσταση ώστε να διατηρηθεί ο αρχικός λόγος διαστάσεων. Αν ορίσετε και τις δύο διαστάσεις, η εικόνα μπορεί να τεντωθεί. Επιλέξτε την προσέγγιση που ταιριάζει στις απαιτήσεις του UI σας.

### Διαφανά φόντα

Αν το αρχικό SVG βασίζεται σε διαφάνεια (π.χ., εικονίδια), μπορείτε να διατηρήσετε το PNG διαφανές παραλείποντας το `background_color`:

```python
options.background_color = None   # PNG will retain transparency
```

Αυτή η παραλλαγή είναι χρήσιμη όταν το PNG θα τοποθετηθεί πάνω σε άλλα γραφικά.

## Εξαγωγή SVG σε PNG – συμβουλές απόδοσης

* **Reuse `ImageSaveOptions`** όταν μετατρέπετε πολλά αρχεία σε batch. Η δημιουργία νέου αντικειμένου επιλογών για κάθε αρχείο προσθέτει αμελητέο κόστος, αλλά η επαναχρησιμοποίηση αποφεύγει επαναλαμβανόμενη κατανομή μνήμης.
* **Batch processing**: Επανάληψη σε έναν φάκελο με αρχεία SVG και κλήση της `convert_svg_to_png` για κάθε ένα. Η βιβλιοθήκη επεξεργάζεται κάθε αρχείο ανεξάρτητα, οπότε μπορείτε να παραλληλοποιήσετε τον βρόχο με `concurrent.futures.ThreadPoolExecutor` για ταχύτερη μετατροπή σε πολυπύρηνες μηχανές.

```python
import os
from concurrent.futures import ThreadPoolExecutor

svg_folder = "YOUR_DIRECTORY"
png_folder = "YOUR_DIRECTORY/pngs"
os.makedirs(png_folder, exist_ok=True)

def batch_convert(file_name):
    src = os.path.join(svg_folder, file_name)
    dst = os.path.join(png_folder, file_name.replace('.svg', '.png'))
    convert_svg_to_png(src, dst)

with ThreadPoolExecutor(max_workers=8) as executor:
    executor.map(batch_convert, [f for f in os.listdir(svg_folder) if f.endswith('.svg')])
```

## Αποθήκευση SVG ως PNG – επαλήθευση

Μετά τη μετατροπή, μπορείτε να επαληθεύσετε το αποτέλεσμα προγραμματιστικά:

```python
from PIL import Image

with Image.open("YOUR_DIRECTORY/vector.png") as img:
    print(f"PNG size: {img.size}, mode: {img.mode}")
```

Τυπική έξοδος:

```
PNG size: (1024, 768), mode: RGBA
```

Η `mode` `RGBA` επιβεβαιώνει ότι η εικόνα περιέχει κανάλι άλφα (διαφάνεια). Αν ορίσετε χρώμα φόντου, η λειτουργία θα είναι `RGB`.

## Συμπέρασμα

Τώρα ξέρετε **πώς να αποθηκεύσετε SVG** ως PNG χρησιμοποιώντας Python, **πώς να μετατρέψετε SVG σε PNG**, και **πώς να εξάγετε SVG σε PNG** με προσαρμοσμένες διαστάσεις και διαχείριση φόντου. Το πλήρες σενάριο δείχνει όλη τη ροή εργασίας, από τη φόρτωση ενός διανυσματικού αρχείου SVG μέχρι την παραγωγή μιας raster εικόνας PNG.

Στη συνέχεια, εξερευνήστε συναφή θέματα όπως **αποθήκευση SVG ως PNG** σε λειτουργία batch, χρήση εναλλακτικών βιβλιοθηκών όπως **CairoSVG**, ή δημιουργία πολυ-σελίδων PDF από πηγές SVG. Πειραματιστείτε με διαφορετικές ρυθμίσεις `ImageSaveOptions` για να βελτιστοποιήσετε την ποιότητα, το DPI και τη συμπίεση ανάλογα με τη δική σας περίπτωση χρήσης.

## Τι πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [svg to png java – Μετατροπή SVG σε εικόνα με Aspose.HTML για Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Απόδοση εγγράφου SVG ως PNG σε .NET με Aspose.HTML](/html/hindi/net/rendering-html-documents/render-svg-doc-as-png/)
- [Πώς να ορίσετε DPI κατά τη μετατροπή SVG σε PNG με Java](/html/english/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-with-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}