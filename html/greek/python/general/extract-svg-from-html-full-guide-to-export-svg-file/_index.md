---
category: general
date: 2026-06-04
description: Εξάγετε το SVG από το HTML και εξαγάγετε το αρχείο SVG με προσαρμοσμένες
  επιλογές αποθήκευσης SVG, διατηρώντας το εξωτερικό CSS αμετάβλητο. Ακολουθήστε αυτό
  το βήμα‑βήμα οδηγό.
draft: false
keywords:
- extract svg from html
- export svg file
- svg save options
- svg external css
- inline svg markup
language: el
og_description: Εξάγετε SVG από HTML γρήγορα. Αυτό το σεμινάριο δείχνει πώς να εξάγετε
  αρχείο SVG χρησιμοποιώντας τις επιλογές αποθήκευσης SVG, διατηρώντας το εξωτερικό
  CSS.
og_title: Εξαγωγή SVG από HTML – Οδηγός Εξαγωγής Αρχείου SVG
schemas:
- author: Aspose
  dateModified: '2026-06-04'
  description: Extract SVG from HTML and export SVG file with custom SVG save options,
    keeping external CSS intact. Follow this step‑by‑step tutorial.
  headline: Extract SVG from HTML – Full Guide to Export SVG File
  type: TechArticle
tags:
- SVG
- HTML
- Export
- Scripting
title: Εξαγωγή SVG από HTML – Πλήρης οδηγός για την εξαγωγή αρχείου SVG
url: /el/python/general/extract-svg-from-html-full-guide-to-export-svg-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή SVG από HTML – Πλήρης Οδηγός για Εξαγωγή Αρχείου SVG

Έχετε χρειαστεί ποτέ να **extract svg from html** αλλά δεν ήσασταν σίγουροι ποιες κλήσεις API σας δίνουν ένα καθαρό, αυτόνομο αρχείο; Δεν είστε μόνοι. Σε πολλά έργα web‑automation το SVG βρίσκεται κρυμμένο μέσα σε μια σελίδα, και η εξαγωγή του διατηρώντας το αρχικό στυλ είναι λίγο δύσκολη.  

Σε αυτόν τον οδηγό θα σας καθοδηγήσουμε βήμα‑βήμα σε μια πλήρη λύση που όχι μόνο **extracts the SVG** αλλά και δείχνει πώς να **export svg file** με ακριβείς **svg save options**, διασφαλίζοντας ότι το **svg external css** παραμένει εξωτερικό και το **inline svg markup** παραμένει αμετάβλητο.

## Τι Θα Μάθετε

- Πώς να φορτώσετε ένα HTML έγγραφο από το δίσκο.  
- Πώς να εντοπίσετε το πρώτο στοιχείο `<svg>` (ή όποιο χρειάζεστε).  
- Πώς να δημιουργήσετε ένα `SVGDocument` από το **inline svg markup**.  
- Ποιες **svg save options** απενεργοποιούν την ενσωμάτωση CSS ώστε τα στυλ να παραμένουν σε εξωτερικά αρχεία.  
- Τα ακριβή βήματα για **export svg file** στον επιθυμητό φάκελο.  
- Συμβουλές για διαχείριση πολλαπλών SVG, διατήρηση IDs και αντιμετώπιση κοινών προβλημάτων.

Δεν απαιτούνται βαριές εξαρτήσεις, μόνο τα ενσωματωμένα αντικείμενα scripting που παρέχει το Adobe InDesign (ή οποιοδήποτε περιβάλλον που παρέχει `HTMLDocument`, `SVGDocument` και `SVGSaveOptions`). Πάρτε έναν επεξεργαστή κειμένου, αντιγράψτε τον κώδικα και είστε έτοιμοι.

![Extract SVG from HTML workflow](extract-svg-workflow.png){alt="Διαδικασία εξαγωγής SVG από HTML"}

## Προαπαιτούμενα

- Adobe InDesign (ή ένας συμβατός κεντρικός ExtendScript) έκδοση 2022 ή νεότερη.  
- Βασική εξοικείωση με τη σύνταξη JavaScript/ExtendScript.  
- Ένα αρχείο HTML που περιέχει τουλάχιστον ένα στοιχείο `<svg>` που θέλετε να εξάγετε.

Αν πληροίτε αυτά τα τρία σημεία, μπορείτε να παραλείψετε το τμήμα “setup” και να περάσετε κατευθείαν στον κώδικα.

---

## Εξαγωγή SVG από HTML – Βήμα 1: Φόρτωση του HTML Εγγράφου

Πρώτα απ’ όλα: χρειάζεστε μια αναφορά στη σελίδα HTML που φιλοξενεί το SVG. Ο κατασκευαστής `HTMLDocument` δέχεται μια διαδρομή αρχείου και αναλύει το markup για εσάς.

```javascript
// Step 1: Load the HTML document
var htmlPath = File("YOUR_DIRECTORY/page.html"); // adjust the path
var htmlDoc = new HTMLDocument(htmlPath);
```

> **Why this matters:** Η φόρτωση του εγγράφου σας παρέχει ένα μοντέλο αντικειμένων παρόμοιο με DOM, ώστε να μπορείτε να ερωτήσετε στοιχεία όπως θα κάνατε σε έναν περιηγητή. Χωρίς αυτό, θα έπρεπε να χρησιμοποιήσετε ασταθείς αναζητήσεις συμβολοσειρών.

---

## Εξαγωγή SVG από HTML – Βήμα 2: Εντοπισμός του Πρώτου Στοιχείου `<svg>`

Τώρα που το DOM είναι έτοιμο, ας πάρουμε τον πρώτο κόμβο SVG. Αν χρειάζεστε κάποιον διαφορετικό, απλώς αλλάξτε το δείκτη ή χρησιμοποιήστε έναν πιο συγκεκριμένο selector.

```javascript
// Step 2: Locate the first <svg> element
var svgElements = htmlDoc.getElementsByTagName("svg");
if (svgElements.length === 0) {
    throw new Error("No <svg> elements found in the HTML file.");
}
var svgElement = svgElements[0]; // you could loop through all if needed
```

> **Pro tip:** Το `svgElements` είναι μια συλλογή τύπου array‑like, οπότε μπορείτε να το επαναλάβετε για **export multiple svg files** σε μια μεταγενέστερη επανάληψη.

## Inline SVG Markup – Βήμα 3: Δημιουργία ενός SVGDocument

Η ιδιότητα `outerHTML` επιστρέφει το πλήρες markup του στοιχείου `<svg>`, συμπεριλαμβανομένων τυχόν inline χαρακτηριστικών. Η μεταφορά αυτής της συμβολοσειράς στο `SVGDocument` σας δίνει ένα πλήρως διαμορφωμένο αντικείμενο SVG που μπορείτε να επεξεργαστείτε ή να αποθηκεύσετε.

```javascript
// Step 3: Create an SVGDocument from the extracted markup
var svgMarkup = svgElement.outerHTML; // this is the inline svg markup
var svgDoc = new SVGDocument(svgMarkup);
```

> **Why we use `outerHTML`:** Καταγράφει το στοιχείο *και* τα παιδιά του, διατηρώντας διαβαθμίσεις, φίλτρα και τυχόν ενσωματωμένα μπλοκ `<style>` που μπορεί να αποτελούν μέρος του **inline svg markup**.

## SVG Save Options – Βήμα 4: Διαμόρφωση Ρυθμίσεων Εξαγωγής

Από προεπιλογή, το InDesign ενσωματώνει CSS απευθείας στο SVG, κάτι που μπορεί να φουσκώσει το αρχείο και να διακόψει τις εξωτερικές αλυσίδες στυλ. Για να διατηρήσετε το φύλλο στυλ ξεχωριστό, ενεργοποιήστε/απενεργοποιήστε τη σημαία `embedCSS`.

```javascript
// Step 4: Configure SVG save options (disable CSS embedding)
var svgOptions = new SVGSaveOptions();
svgOptions.embedCSS = false;      // ensures svg external css stays external
svgOptions.embedImages = false;   // optional: keep images as links
svgOptions.fontType = SVGFontType.OUTLINE; // optional: outline fonts
```

> **What “svg external css” means:** Όταν το `embedCSS` είναι `false`, οποιεσδήποτε ετικέτες `<style>` αφαιρούνται και το SVG αναφέρεται σε ξεχωριστό αρχείο CSS (αν υπάρχει). Αυτό είναι ιδανικό για ροές εργασίας που βασίζονται σε κοινό stylesheet για πολλά SVG assets.

## Εξαγωγή Αρχείου SVG – Βήμα 5: Αποθήκευση του Εξαγόμενου SVG

Τέλος, γράψτε το SVG στο δίσκο. Η μέθοδος `save` σέβεται τις επιλογές που ορίσαμε παραπάνω, παράγοντας ένα καθαρό αρχείο έτοιμο για το web ή για περαιτέρω επεξεργασία.

```javascript
// Step 5: Save the extracted SVG to a separate file
var outputPath = File("YOUR_DIRECTORY/extracted.svg");
svgDoc.save(outputPath, svgOptions);
```

**Expected result:** Ένα αρχείο με όνομα `extracted.svg` εμφανίζεται στο `YOUR_DIRECTORY`. Ανοίξτε το σε έναν περιηγητή – θα πρέπει να δείτε το γραφικό να αποδίδεται ακριβώς όπως εμφανιζόταν στο αρχικό HTML, αλλά με όλα τα CSS τώρα φορτωμένα από εξωτερικές πηγές.

## Διαχείριση Πολλαπλών SVG (Προαιρετικό)

Αν η σελίδα HTML σας περιέχει πολλά SVG, τυλίξτε τη λογική εντοπισμού‑και‑αποθήκευσης μέσα σε ένα βρόχο:

```javascript
for (var i = 0; i < svgElements.length; i++) {
    var element = svgElements[i];
    var doc = new SVGDocument(element.outerHTML);
    var outFile = File("YOUR_DIRECTORY/svg_" + i + ".svg");
    doc.save(outFile, svgOptions);
}
```

Αυτή η μικρή τροποποίηση σας επιτρέπει να **export svg file** μαζικά χωρίς να ξαναγράψετε κώδικα.

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Το SVG εμφανίζεται κενό στον περιηγητή | Το CSS ενσωματώθηκε και στη συνέχεια αφαιρέθηκε, χάνοντας τους κανόνες στυλ | Βεβαιωθείτε ότι `svgOptions.embedCSS = false` μόνο όταν έχετε έτοιμο εξωτερικό stylesheet. |
| Το κείμενο φαίνεται τριγωνικό | Οι γραμματοσειρές δεν είχαν περιγραφεί | Ορίστε `svgOptions.fontType = SVGFontType.OUTLINE`. |
| Οι εικόνες λείπουν | Το `embedImages` έμεινε true ενώ οι εικόνες είναι εξωτερικές | Αλλάξτε `svgOptions.embedImages = false` και κρατήστε τα αρχεία εικόνας δίπλα στο SVG. |
| Συγκρούσεις IDs όταν συγχωνεύονται πολλαπλά SVG | Κάθε SVG διατήρησε τα αρχικά του IDs | Μετα-επεξεργαστείτε με ένα απλό script μετονομασίας ή χρησιμοποιήστε την επιλογή “unique IDs” του InDesign αν είναι διαθέσιμη. |

## Πλήρες Script – Έτοιμο για Αντιγραφή‑Επικόλληση

Παρακάτω βρίσκεται ολόκληρο το script, έτοιμο να τοποθετηθεί σε ένα παράθυρο ExtendScript Toolkit και να εκτελεστεί. Αντικαταστήστε το `YOUR_DIRECTORY` με το φάκελο που περιέχει το αρχείο HTML σας.



## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Αποθήκευση Εγγράφου SVG στο Aspose.HTML για Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Πώς να Μετατρέψετε SVG σε XPS με το Aspose.HTML για Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [Δημιουργία PDF από SVG με Aspose.HTML για Java](/html/hindi/java/conversion-html-to-other-formats/convert-svg-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}