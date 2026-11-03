---
category: general
date: 2026-07-02
description: Δημιουργήστε γρήγορα έγγραφο SVG με Python. Μάθετε πώς να αποθηκεύετε
  αρχείο SVG, να δημιουργείτε μια βασική εικόνα SVG και να εξάγετε SVG από κώδικα
  σε λίγες μόνο γραμμές.
draft: false
keywords:
- create svg document
- save svg file
- how to generate svg
- export svg from code
- create basic svg image
language: el
og_description: Δημιουργήστε εύκολα έγγραφο SVG. Αυτός ο οδηγός δείχνει πώς να δημιουργήσετε
  SVG, να αποθηκεύσετε αρχείο SVG και να εξάγετε SVG από κώδικα με ένα καθαρό παράδειγμα
  Python.
og_title: Δημιουργία εγγράφου SVG – Γρήγορο μάθημα Python
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Create SVG document quickly with Python. Learn to save SVG file, generate
    a basic SVG image, and export SVG from code in just a few lines.
  headline: Create SVG Document – Step‑by‑Step Guide for Beginners
  type: TechArticle
- description: Create SVG document quickly with Python. Learn to save SVG file, generate
    a basic SVG image, and export SVG from code in just a few lines.
  name: Create SVG Document – Step‑by‑Step Guide for Beginners
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: How can I add text or other shapes?
    text: Just call `svg.create_element("text", {...})` or `svg.create_element("circle",
      {...})` and append them just like the rectangle. The same **how to generate
      SVG** logic applies.
  - name: What if I need to **export SVG from code** with a transparent background?
    text: Remove any `fill` attribute from the root `<svg>` element or set `fill="none"`
      on shapes that should be transparent. The XML stays valid; browsers will render
      the transparency automatically.
  - name: Can I **save SVG file** with pretty‑printed formatting?
    text: '`ElementTree` writes compact XML by default. For a human‑readable version,
      you can use `xml.dom.minidom` to re‑format:'
  - name: What about performance for large SVGs?
    text: When generating thousands of elements, consider building a list of `ET.Element`
      objects first and then extending the root in one go. This reduces the number
      of tree mutations and speeds up the **save SVG file** operation.
  type: HowTo
tags:
- SVG
- Python
- Graphics
- File I/O
title: Δημιουργία εγγράφου SVG – Οδηγός βήμα‑προς‑βήμα για αρχαρίους
url: /el/python/general/create-svg-document-step-by-step-guide-for-beginners/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Εγγράφου SVG – Οδηγός Βήμα‑βήμα για Αρχάριους

Έχετε αναρωτηθεί ποτέ πώς να **create SVG document** χωρίς να ανοίξετε έναν επεξεργαστή γραφικών; Δεν είστε ο μόνος. Είτε χρειάζεστε ένα μικρό εικονίδιο για μια ιστοσελίδα είτε ένα δυναμικό διάγραμμα που δημιουργείται επί τόπου, η δυνατότητα **create SVG document** προγραμματιστικά εξοικονομεί χρόνο και διατηρεί όλα υπό έλεγχο εκδόσεων.

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που σας δείχνει ακριβώς πώς να **create SVG document**, **save SVG file**, και ακόμη να απαντήσουμε στην επίμονη ερώτηση «**how to generate SVG**» που εμφανίζεται όταν αυτοματοποιείτε γραφικά. Στο τέλος θα έχετε ένα κόκκινο τετράγωνο αποθηκευμένο στο δίσκο, και θα ξέρετε πώς να **export SVG from code** για οποιοδήποτε μελλοντικό έργο.

## Τι Θα Χρειαστείτε

* Python 3.9 ή νεότερο (η τυπική βιβλιοθήκη κάνει όλη τη βαριά δουλειά)
* Ένας επεξεργαστής κειμένου ή IDE που σας αρέσει—VS Code, PyCharm, ή ακόμη και Notepad αρκεί
* Δικαίωμα εγγραφής σε φάκελο όπου θα **save SVG file** (θα χρησιμοποιήσουμε έναν φάκελο `output/`)

Δεν απαιτούνται εξωτερικά πακέτα, έτσι η ρύθμιση διαρκεί κυριολεκτικά λίγα λεπτά.

## Βήμα 1: Ρύθμιση των Βοηθητικών Συναρτήσεων SVG (Create the Document)

Πρώτα απ' όλα: χρειαζόμαστε έναν μικρό βοηθό που δημιουργεί τη δομή XML πίσω από ένα SVG. Σκεφτείτε το ως τον καμβά στον οποίο θα **create basic SVG image** στοιχεία αργότερα.

```python
import pathlib
import xml.etree.ElementTree as ET

# ----------------------------------------------------------------------
# Helper class that mimics a minimal SVG library.
# ----------------------------------------------------------------------
class SVGDocument:
    """Simple wrapper to generate an SVG document using ElementTree."""
    
    SVG_NS = "http://www.w3.org/2000/svg"
    def __init__(self, width: int = 200, height: int = 200):
        # Register the SVG namespace so the output looks clean
        ET.register_namespace("", self.SVG_NS)
        self.root = ET.Element(
            "svg",
            attrib={
                "xmlns": self.SVG_NS,
                "width": str(width),
                "height": str(height),
                "version": "1.1"
            }
        )
    
    def create_element(self, tag: str, attributes: dict) -> ET.Element:
        """Create an SVG element with the given attributes."""
        return ET.Element(tag, attrib=attributes)
    
    def append_child(self, element: ET.Element):
        """Append a child element to the root <svg> node."""
        self.root.append(element)
    
    def save(self, file_path: str):
        """Write the SVG XML to a file, creating directories as needed."""
        path = pathlib.Path(file_path)
        path.parent.mkdir(parents=True, exist_ok=True)
        tree = ET.ElementTree(self.root)
        tree.write(str(path), encoding="utf-8", xml_declaration=True)
```

**Γιατί αυτό το βήμα είναι σημαντικό:** Η κλάση `SVGDocument` αφαιρεί την πολύπλοκη διαχείριση XML. Με την περιτύλιξη της σε μια κλάση κρατάμε τον υπόλοιπο κώδικα καθαρό, κάτι που αποτελεί βέλτιστη πρακτική όταν **export SVG from code** σε μεγαλύτερες εφαρμογές.

## Βήμα 2: Προσθήκη Ορθογωνίου – Ο Πυρήνας ενός Παραδείγματος **Create Basic SVG Image**

Τώρα που έχουμε ένα αντικείμενο εγγράφου, ας προσθέσουμε ένα κόκκινο τετράγωνο. Αυτό είναι η καρδιά του τμήματος **create basic SVG image** του tutorial.

```python
# ----------------------------------------------------------------------
# Step 2: Build the SVG content
# ----------------------------------------------------------------------
svg = SVGDocument(width=120, height=120)   # canvas size a little larger than the square

# Define rectangle attributes: 100x100 size, red fill, positioned at (10,10)
rect_attrs = {
    "x": "10",
    "y": "10",
    "width": "100",
    "height": "100",
    "fill": "red"
}

# Create the <rect> element and attach it to the SVG root
rect_element = svg.create_element("rect", rect_attrs)
svg.append_child(rect_element)
```

**Explanation:**  
* Οι συντεταγμένες `x` και `y` του ορθογωνίου του δίνουν ένα περιθώριο 10 pixel ώστε να μην ακουμπάει στην άκρη.  
* Η χρήση λεξικού για τα attributes κάνει τον κώδικα πιο αναγνώσιμο και αντικατοπτρίζει πώς θα **save SVG file** attributes σε οποιαδήποτε μορφή βασισμένη σε XML.  
* Αν ποτέ χρειαστείτε **how to generate SVG** σχήματα διαφορετικά από ορθογώνια, απλώς αλλάξτε το tag σε `"circle"` ή `"path"` και προσαρμόστε το λεξικό attributes ανάλογα.

## Βήμα 3: Αποθήκευση του SVG – Τέλος **Save SVG File** στο Δίσκο

Έχουμε δημιουργήσει το έγγραφο στη μνήμη· τώρα θα το γράψουμε στο δίσκο. Αυτή είναι η στιγμή που το αφηρημένο **create SVG document** γίνεται ένα απτό αρχείο που μπορείτε να ανοίξετε σε έναν περιηγητή.

```python
# ----------------------------------------------------------------------
# Step 3: Persist the SVG to the filesystem
# ----------------------------------------------------------------------
output_path = "output/square.svg"
svg.save(output_path)

print(f"✅ SVG saved! Open {output_path} in any browser to see the red square.")
```

**Τι θα δείτε:** Το άνοιγμα του `output/square.svg` σε Chrome, Firefox ή οποιονδήποτε προβολέα που υποστηρίζει SVG θα εμφανίσει ένα απλό κόκκινο τετράγωνο με λεπτό λευκό περίγραμμα (το φόντο του καμβά SVG). Αυτό είναι η απόδειξη ότι έχουμε **exported SVG from code** επιτυχώς.

## Πλήρες Script – Λύση σε Ένα Αρχείο

Παρακάτω βρίσκεται ολόκληρο το script, έτοιμο για αντιγραφή‑επικόλληση στο `create_svg.py`. Η εκτέλεση του `python create_svg.py` θα δημιουργήσει το αρχείο που περιγράφηκε παραπάνω.

```python
import pathlib
import xml.etree.ElementTree as ET

class SVGDocument:
    """Simple wrapper to generate an SVG document using ElementTree."""
    SVG_NS = "http://www.w3.org/2000/svg"
    def __init__(self, width: int = 200, height: int = 200):
        ET.register_namespace("", self.SVG_NS)
        self.root = ET.Element(
            "svg",
            attrib={
                "xmlns": self.SVG_NS,
                "width": str(width),
                "height": str(height),
                "version": "1.1"
            }
        )
    def create_element(self, tag: str, attributes: dict) -> ET.Element:
        return ET.Element(tag, attrib=attributes)
    def append_child(self, element: ET.Element):
        self.root.append(element)
    def save(self, file_path: str):
        path = pathlib.Path(file_path)
        path.parent.mkdir(parents=True, exist_ok=True)
        tree = ET.ElementTree(self.root)
        tree.write(str(path), encoding="utf-8", xml_declaration=True)

# -------------------- Build the SVG --------------------
svg = SVGDocument(width=120, height=120)

rect_attrs = {
    "x": "10",
    "y": "10",
    "width": "100",
    "height": "100",
    "fill": "red"
}
svg.append_child(svg.create_element("rect", rect_attrs))

# -------------------- Save the file --------------------
output_path = "output/square.svg"
svg.save(output_path)

print(f"✅ SVG saved! Open {output_path} in any browser to see the red square.")
```

### Αναμενόμενη Έξοδος

Η εκτέλεση του script εκτυπώνει:

```
✅ SVG saved! Open output/square.svg in any browser to see the red square.
```

Και το παραγόμενο `square.svg` φαίνεται ως εξής (απλοποιημένη προβολή):

```xml
<?xml version='1.0' encoding='utf-8'?>
<svg xmlns="http://www.w3.org/2000/svg" width="120" height="120" version="1.1">
  <rect x="10" y="10" width="100" height="100" fill="red" />
</svg>
```

Το άνοιγμα του αρχείου αποδίδει ένα καθαρό κόκκινο τετράγωνο—ακριβώς αυτό που θέλαμε να **create basic SVG image**.

## Επέκταση του Παραδείγματος – Απαντήσεις σε Συχνές Ερωτήσεις

### Πώς μπορώ να προσθέσω κείμενο ή άλλα σχήματα;

Απλώς καλέστε `svg.create_element("text", {...})` ή `svg.create_element("circle", {...})` και προσθέστε τα όπως το ορθογώνιο. Η ίδια λογική **how to generate SVG** ισχύει.

### Τι γίνεται αν χρειαστεί να **export SVG from code** με διαφανές φόντο;

Αφαιρέστε οποιοδήποτε attribute `fill` από το ριζικό στοιχείο `<svg>` ή ορίστε `fill="none"` στα σχήματα που πρέπει να είναι διαφανή. Το XML παραμένει έγκυρο· οι περιηγητές θα αποδώσουν τη διαφάνεια αυτόματα.

### Μπορώ να **save SVG file** με μορφοποίηση pretty‑printed;

`ElementTree` γράφει συμπαγές XML από προεπιλογή. Για μια εκδοχή αναγνώσιμη από άνθρωπο, μπορείτε να χρησιμοποιήσετε `xml.dom.minidom` για επαναμορφοποίηση:

```python
import xml.dom.minidom as minidom

def pretty_save(svg_doc, path):
    rough_string = ET.tostring(svg_doc.root, 'utf-8')
    reparsed = minidom.parseString(rough_string)
    with open(path, 'w', encoding='utf-8') as f:
        f.write(reparsed.toprettyxml(indent="  "))
```

Αντικαταστήστε το `svg.save(output_path)` με `pretty_save(svg, output_path)`.

### Τι γίνεται με την απόδοση για μεγάλα SVG;

Κατά τη δημιουργία χιλιάδων στοιχείων, σκεφτείτε να δημιουργήσετε πρώτα μια λίστα από αντικείμενα `ET.Element` και στη συνέχεια να επεκτείνετε τη ρίζα σε ένα βήμα. Αυτό μειώνει τον αριθμό των μεταβολών του δέντρου και επιταχύνει τη λειτουργία **save SVG file**.

## Pro Συμβουλές & Πιθανά Σφάλματα

* **Pro tip:** Πάντα χρησιμοποιείτε απόλυτες διαδρομές (ή `pathlib.Path`) όταν **saving SVG file**· οι σχετικές διαδρομές μπορεί να σπάσουν όταν το script σας εκτελείται από διαφορετικό φάκελο εργασίας.  
* **Watch out for:** Ξεχάσιμο της καταχώρισης του namespace SVG. Χωρίς `ET.register_namespace("", SVGDocument.SVG_NS)`, η έξοδος θα περιέχει ένα περιττό πρόθεμα `ns0` που μερικοί περιηγητές ερμηνεύουν λανθασμένα.  
* **Typical mistake:** Ανάμειξη ακέραιων και συμβολοσειρών στα attribute values. Το XML αναμένει συμβολοσειρές, έτσι μετατρέπουμε τα πάντα με `str()`—η βοηθητική κλάση το κάνει για εσάς, αλλά αν το παρακάμψετε, μπορεί να προκύψει `TypeError`.  

## Συμπέρασμα

Μόλις περάσαμε από ένα πλήρες, end‑to‑end παράδειγμα που δείχνει πώς να **create SVG document**, **save SVG file**, και να απαντήσουμε

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}