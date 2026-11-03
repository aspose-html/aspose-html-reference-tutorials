---
date: 2026-08-17
description: Μάθετε πώς να ορίσετε DPI κατά τη μετατροπή EPUB σε BMP και να προσαρμόσετε
  την ανάλυση εικόνας χρησιμοποιώντας το Aspose.HTML for Java σε έναν οδηγό βήμα‑βήμα.
keywords:
- how to set dpi
- convert epub to bmp
- convert ebook to bmp
lastmod: 2026-08-17
linktitle: Μετατροπή EPUB σε BMP
og_description: Μάθετε πώς να ορίσετε DPI κατά τη μετατροπή EPUB σε BMP με το Aspose.HTML
  for Java. Αυτός ο οδηγός παρουσιάζει κώδικα βήμα‑βήμα, προσαρμογή DPI και συμβουλές
  αντιμετώπισης προβλημάτων.
og_image_alt: Developer guide showing Java code converting EPUB to BMP with custom
  DPI
og_title: Πώς να ορίσετε DPI κατά τη μετατροπή EPUB σε BMP αποδοτικά χρησιμοποιώντας
  το Aspose.HTML for Java
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Learn how to set DPI while converting EPUB to BMP and customize image
    resolution using Aspose.HTML for Java in a step‑by‑step guide.
  headline: How to set DPI when converting EPUB to BMP efficiently using Aspose.HTML
    for Java
  type: TechArticle
- description: Learn how to set DPI while converting EPUB to BMP and customize image
    resolution using Aspose.HTML for Java in a step‑by‑step guide.
  name: How to set DPI when converting EPUB to BMP efficiently using Aspose.HTML for
    Java
  steps:
  - name: open the epub file
    text: First, load the EPUB document into a `Document` object so the library can
      read its structure and assets. `Document` represents an EPUB or HTML document
      loaded into memory, providing access to its pages and resources. Replace `"path/to/your/input.epub"`
      with the actual file path of your EPUB.
  - name: initialize image save options
    text: Create an `ImageSaveOptions` instance and specify BMP as the target format.
      `ImageSaveOptions` configures how the output image is saved, including format,
      resolution, and quality settings. This ensures the conversion output will be
      a BMP file.
  - name: convert epub to bmp
    text: Invoke the static `Converter.convertEPUB` method, passing the source document,
      the output path, and the configured options. `Converter.convertEPUB` performs
      the rendering of the EPUB to an image using the supplied options. Replace `"path/to/your/output.bmp"`
      with the desired destination path. And th
  type: HowTo
- questions:
  - answer: Converting an EPUB document to a BMP image and setting custom DPI with
      Aspose.HTML for Java.
    question: What does this tutorial cover?
  - answer: About 10‑15 minutes for a basic conversion.
    question: How long does the implementation take?
  - answer: Java JDK, Aspose.HTML for Java library, and an EPUB file.
    question: What are the prerequisites?
  - answer: A free trial works for testing; a commercial license is required for production.
    question: Do I need a license?
  - answer: Yes—replace `ImageFormat.Bmp` with PNG, JPEG, etc.
    question: Can I target other image formats?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
tags:
- convert epub to bmp
- Aspose.HTML
- Java image processing
title: Πώς να ορίσετε DPI κατά τη μετατροπή EPUB σε BMP αποδοτικά χρησιμοποιώντας
  το Aspose.HTML for Java
url: /el/java/converting-between-epub-and-image-formats/convert-epub-to-bmp/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ορίσετε DPI κατά τη μετατροπή EPUB σε BMP αποδοτικά χρησιμοποιώντας το Aspose.HTML για Java

## Εισαγωγή

Εάν χρειάζεται να **μετατρέψετε epub σε bmp** και επίσης να ελέγξετε την ανάλυση της εικόνας, αυτό το tutorial σας δείχνει ακριβώς **πώς να ορίσετε DPI** κατά τη μετατροπή με το Aspose.HTML για Java. Θα έχετε έναν σαφή, βήμα‑βήμα οδηγό που λειτουργεί για οποιοδήποτε EPUB ή άλλο φορμά ebook, επιτρέποντάς σας να παράγετε υψηλής ποιότητας bitmap αρχεία έτοιμα για εκτύπωση ή αρχειοθέτηση.

## Γρήγορες απαντήσεις
- **Τι καλύπτει αυτό το tutorial;** Μετατροπή ενός εγγράφου EPUB σε εικόνα BMP και ορισμός προσαρμοσμένου DPI με το Aspose.HTML για Java.  
- **Πόσο χρόνο διαρκεί η υλοποίηση;** Περίπου 10‑15 λεπτά για μια βασική μετατροπή.  
- **Ποιες είναι οι προαπαιτήσεις;** Java JDK, βιβλιοθήκη Aspose.HTML για Java, και ένα αρχείο EPUB.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για δοκιμές· απαιτείται εμπορική άδεια για παραγωγή.  
- **Μπορώ να στοχεύσω άλλα φορμά εικόνας;** Ναι—αντικαταστήστε το `ImageFormat.Bmp` με PNG, JPEG κ.λπ.

## Τι είναι η “μετατροπή epub σε bmp”;
Η μετατροπή ενός αρχείου EPUB σε BMP σημαίνει την απόδοση κάθε σελίδας του ηλεκτρονικού βιβλίου ως raster εικόνα σε φορμά BMP. Αυτό είναι χρήσιμο όταν χρειάζεστε μια σταθερή ανάλυση για εκτύπωση, αρχειοθέτηση ή ενσωμάτωση σε συστήματα που δέχονται μόνο bitmap εικόνες.

## Γιατί να χρησιμοποιήσετε το Aspose.HTML για Java;
Το Aspose.HTML για Java παρέχει ένα ολοκληρωμένο σύνολο λειτουργιών που απλοποιούν την απόδοση EPUB και τη μετατροπή εικόνας. Διαχειρίζεται την ανάλυση, τη διάταξη και τη rasterization εσωτερικά, παρέχοντας υψηλής ποιότητας αποτελέσματα με ελάχιστο κώδικα και χωρίς εξωτερικές εξαρτήσεις.

- **Χωρίς εξωτερικές εξαρτήσεις** – η βιβλιοθήκη διαχειρίζεται την ανάλυση EPUB και την απόδοση εικόνας εσωτερικά.  
- **Υψηλή πιστότητα** – διατηρεί τη διάταξη, τις γραμματοσειρές και τα διανυσματικά γραφικά κατά τη rasterization.  
- **Βελτιστοποιημένη απόδοση** – κατάλληλη για μαζική επεξεργασία μεγάλων συλλογών EPUB.  

## Προαπαιτήσεις

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε τις παρακάτω προαπαιτήσεις:

1. **Περιβάλλον ανάπτυξης Java** – εγκατεστημένο και ρυθμισμένο JDK 8 ή νεότερο.  
2. **Aspose.HTML για Java** – πρέπει να έχετε το Aspose.HTML για Java έτοιμο προς χρήση. Εάν δεν το έχετε ήδη, μπορείτε να το κατεβάσετε από τη [download it from the Aspose.HTML for Java releases page](https://releases.aspose.com/html/java/).  
3. **Αρχείο EPUB** – ένα έγκυρο EPUB που θέλετε να μετατρέψετε.  
4. **Βασικές γνώσεις Java** – χρήσιμες για την κατανόηση του παραδείγματος κώδικα.

Τώρα που έχετε τις προαπαιτήσεις έτοιμες, ας εισάγουμε τα απαιτούμενα πακέτα.

## Εισαγωγή πακέτων

Ο χώρος ονομάτων `com.aspose.html` περιέχει όλες τις κλάσεις που χρειάζεστε για την απόδοση EPUB και την αποθήκευση εικόνας.

Η κλάση `ImageSaveOptions` ορίζει πώς μορφοποιείται και αποδίδεται η έξοδος εικόνας.  

```java
import com.aspose.html.saving.ImageSaveOptions;
import com.aspose.html.rendering.image.ImageFormat;
import com.aspose.html.converters.Converter;
```

## Μετατροπή EPUB σε BMP – βήμα προς βήμα μετατροπή

### Βήμα 1: άνοιγμα του αρχείου epub

Πρώτα, φορτώστε το έγγραφο EPUB σε ένα αντικείμενο `Document` ώστε η βιβλιοθήκη να μπορεί να διαβάσει τη δομή και τα περιουσιακά στοιχεία του.  
`Document` αντιπροσωπεύει ένα έγγραφο EPUB ή HTML που έχει φορτωθεί στη μνήμη, παρέχοντας πρόσβαση στις σελίδες και τους πόρους του.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("path/to/your/input.epub")) {
```

Αντικαταστήστε το `"path/to/your/input.epub"` με το πραγματικό μονοπάτι του αρχείου EPUB σας.

### Βήμα 2: αρχικοποίηση επιλογών αποθήκευσης εικόνας

Δημιουργήστε μια παρουσία `ImageSaveOptions` και ορίστε το BMP ως μορφή προορισμού.  
`ImageSaveOptions` διαμορφώνει πώς αποθηκεύεται η έξοδος εικόνας, συμπεριλαμβανομένης της μορφής, της ανάλυσης και των ρυθμίσεων ποιότητας.

```java
ImageSaveOptions options = new ImageSaveOptions(ImageFormat.Bmp);
```

Αυτό εξασφαλίζει ότι η έξοδος της μετατροπής θα είναι αρχείο BMP.

#### Προσαρμογή DPI BMP (πώς να ορίσετε DPI)

Για **ορισμό DPI**, καλέστε `options.setResolution(300);` (ή οποιαδήποτε τιμή χρειάζεστε).  
`setResolution` ορίζει το DPI (dots per inch) της εικόνας για το παραγόμενο bitmap, ελέγχοντας το εκτυπωμένο μέγεθος και την ευκρίνεια.

### Βήμα 3: μετατροπή epub σε bmp

Κληθείτε τη στατική μέθοδο `Converter.convertEPUB`, περνώντας το πηγαίο έγγραφο, το μονοπάτι εξόδου και τις διαμορφωμένες επιλογές.  
`Converter.convertEPUB` εκτελεί την απόδοση του EPUB σε εικόνα χρησιμοποιώντας τις παρεχόμενες επιλογές.

```java
Converter.convertEPUB(fileInputStream, options, "path/to/your/output.bmp");
```

Αντικαταστήστε το `"path/to/your/output.bmp"` με το επιθυμητό μονοπάτι προορισμού.

Και αυτό είναι! Έχετε **μετατρέψει επιτυχώς epub σε bmp** ενώ ελέγχετε το DPI χρησιμοποιώντας το Aspose.HTML για Java.

## Πώς να ορίσετε DPI για τη μετατροπή EPUB σε BMP

Φορτώστε το EPUB, διαμορφώστε το `ImageSaveOptions` με `setResolution`, και καλέστε το `Converter.convertEPUB`. Αυτό το τρι‑βήμα μοτίβο σας επιτρέπει να ορίσετε το ακριβές DPI (π.χ., 300) πριν από τη rasterization, εξασφαλίζοντας ότι το παραγόμενο bitmap ταιριάζει στις απαιτήσεις ανάλυσης. Ο ορισμός DPI διασφαλίζει ότι το bitmap έχει τη σωστή πυκνότητα εικονοστοιχείων για εκτύπωση ή λεπτομερή προβολή, αντιστοιχώντας στο προοριζόμενο φυσικό μέγεθος.

## Συχνά προβλήματα και λύσεις

| Πρόβλημα | Γιατί συμβαίνει | Πώς να διορθώσετε |
|----------|----------------|-------------------|
| **File not found** | Λανθασμένο μονοπάτι ή έλλειψη δικαιωμάτων. | Επαληθεύστε το μονοπάτι και εξασφαλίστε πρόσβαση ανάγνωσης. |
| **Unsupported EPUB features** | Πολύπλοκα EPUB με ενσωματωμένες γραμματοσειρές ή σενάρια. | Χρησιμοποιήστε τις υπερφορτωμένες μεθόδους `Converter` που δέχονται επιλογές απόδοσης, ή απλοποιήστε το EPUB. |
| **Out of memory for large files** | Ολόκληρο το EPUB φορτώνεται στη μνήμη. | Αυξήστε το heap της JVM (`-Xmx`) ή επεξεργαστείτε το EPUB σελίδα‑με‑σελίδα. |
| **DPI not applied** | Η ανάλυση του `ImageSaveOptions` δεν έχει οριστεί πριν τη μετατροπή. | Καλέστε `options.setResolution(yourDpi);` πριν το `convertEPUB`. |

## Συχνές ερωτήσεις

**Q1: Είναι το Aspose.HTML για Java δωρεάν;**  
A: Το Aspose.HTML για Java προσφέρει δωρεάν δοκιμή· απαιτείται εμπορική άδεια για παραγωγικές εγκαταστάσεις. Μπορείτε να αποκτήσετε προσωρινή άδεια από το Aspose [obtain a temporary license from Aspose](https://purchase.aspose.com/temporary-license/).

**Q2: Μπορώ να μετατρέψω EPUB σε άλλες μορφές εικόνας;**  
A: Ναι—απλώς αντικαταστήστε το `ImageFormat.Bmp` με PNG, JPEG, TIFF ή οποιαδήποτε από τις 50+ υποστηριζόμενες μορφές.

**Q3: Χρειάζομαι προχωρημένες προγραμματιστικές δεξιότητες;**  
A: Βασικές γνώσεις Java αρκούν· το API είναι σχεδιασμένο ώστε να είναι απλό και καλά τεκμηριωμένο.

**Q4: Πού μπορώ να λάβω βοήθεια ή υποστήριξη;**  
A: Επισκεφθείτε το φόρουμ της κοινότητας Aspose.HTML [Aspose.HTML community forum](https://forum.aspose.com/) για βοήθεια από μηχανικούς της Aspose και την κοινότητα χρηστών.

**Q5: Υπάρχει όριο μεγέθους για τα αρχεία EPUB;**  
A: Το Aspose.HTML διαχειρίζεται μεγάλα EPUB αποδοτικά· δεν υπάρχει σκληρό όριο μεγέθους, αλλά εξαιρετικά μεγάλα αρχεία μπορεί να απαιτούν αυξημένο heap της JVM.

**Q6: Πώς να μετατρέψω κάθε σελίδα ενός EPUB σε ξεχωριστά αρχεία BMP;**  
A: Επαναλάβετε τη διαδικασία για κάθε σελίδα χρησιμοποιώντας την υπερφορτωμένη μέθοδο `Converter` που δέχεται δείκτη σελίδας, και ορίστε μοναδικό μονοπάτι εξόδου για κάθε επανάληψη.

**Q7: Μπορώ να προσαρμόσω την ποιότητα ή το DPI του παραγόμενου BMP;**  
A: Ναι—ορίστε ιδιότητες όπως `options.setResolution(dpi)` και `options.setQuality(quality)` πριν καλέσετε το `convertEPUB`.

## Συμπέρασμα

Ο ορισμός DPI κατά τη μετατροπή **epub σε bmp** είναι απλός με το Aspose.HTML για Java. Αυτός ο οδηγός κάλυψε τη ρύθμιση του περιβάλλοντος, την εξήγηση του κώδικα, την προσαρμογή DPI και συμβουλές αντιμετώπισης προβλημάτων. Εξερευνήστε την πλήρη τεκμηρίωση του Aspose.HTML [Aspose.HTML Java API reference](https://reference.aspose.com/html/java/) για προχωρημένα σενάρια όπως μαζική επεξεργασία, προσαρμοσμένες επιλογές απόδοσης και μετατροπή άλλων φορμά ebook.

---

**Τελευταία ενημέρωση:** 2026-08-17  
**Δοκιμή με:** Aspose.HTML για Java (τελευταία έκδοση)  
**Συγγραφέας:** Aspose

## Σχετικά Tutorials

- [Convert EPUB to Image Using Aspose.HTML for Java – Set Custom Page Size](/html/java/converting-between-epub-and-image-formats/convert-epub-to-image-specify-image-save-options/)
- [Aspose HTML Convert EPUB to PNG in Java – Step‑By‑Step Guide](/html/java/converting-between-epub-and-image-formats/convert-epub-to-png/)
- [How to Convert EPUB to TIFF Image with Aspose.HTML for Java](/html/java/converting-between-epub-and-image-formats/convert-epub-to-tiff/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}