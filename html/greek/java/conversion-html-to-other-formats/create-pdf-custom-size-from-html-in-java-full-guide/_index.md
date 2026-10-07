---
category: general
date: 2026-01-04
description: Δημιουργήστε προσαρμοσμένο μέγεθος PDF από HTML σε Java χρησιμοποιώντας
  το Aspose.HTML – μάθετε πώς να ορίζετε το μέγεθος της σελίδας και να αυξήσετε το
  DPI ενώ μετατρέπετε HTML σε PDF.
draft: false
keywords:
- create pdf custom size
- convert html to pdf
- html to pdf java
- set pdf page size
- increase pdf dpi
language: el
og_description: Δημιουργήστε PDF προσαρμοσμένου μεγέθους από HTML σε Java με το Aspose.HTML.
  Ορίστε το μέγεθος της σελίδας, αυξήστε το DPI και βελτιώστε τη μετατροπή HTML σε
  PDF.
og_title: Δημιουργία PDF προσαρμοσμένου μεγέθους από HTML σε Java – Πλήρης οδηγός
tags:
- Java
- PDF
- Aspose
- HTML conversion
title: Δημιουργία PDF προσαρμοσμένου μεγέθους από HTML σε Java – Πλήρης Οδηγός
url: /el/java/conversion-html-to-other-formats/create-pdf-custom-size-from-html-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία PDF Προσαρμοσμένου Μεγέθους από HTML σε Java – Πλήρης Οδηγός

Έχετε χρειαστεί ποτέ να **δημιουργήσετε PDF προσαρμοσμένου μεγέθους** από πηγή HTML αλλά δεν ήξερες πώς να ελέγξεις τις διαστάσεις ή την ευκρίνεια των εικόνων; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν η προεπιλεγμένη έξοδος A4 φαίνεται λανθασμένη για τα πρότυπα τιμολογίων ή τα φυλλάδια μάρκετινγκ τους.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα **πλήρες, εκτελέσιμο παράδειγμα** που δείχνει πώς να **μετατρέψετε HTML σε PDF** ορίζοντας ρητά **το μέγεθος της σελίδας PDF** και **αυξάνοντας το DPI του PDF** για πιο καθαρά γραφικά. Στο τέλος θα έχετε μια έτοιμη κλάση Java που μπορείτε να προσαρμόσετε σε οποιοδήποτε έργο χρειάζεται PDF προσαρμοσμένου μεγέθους.

## Τι Θα Χρειαστείτε

- **Java 17** ή νεότερη (ο κώδικας χρησιμοποιεί τη σύγχρονη σύνταξη `var`, αλλά μπορείτε να κάνετε back‑port αν χρειαστεί).  
- Βιβλιοθήκη **Aspose.HTML for Java** – συνιστάται η έκδοση 23.9 ή νεότερη.  
- Ένα αρχείο HTML που θέλετε να μετατρέψετε σε PDF (θα το ονομάσουμε `input.html`).  
- Λίγη εξοικείωση με IDE (IntelliJ IDEA, Eclipse ή VS Code).  

Δεν απαιτούνται άλλες εξαρτήσεις· τα JAR της Aspose περιλαμβάνουν όλα όσα χρειάζεστε.

## Βήμα 1: Προσθήκη του Aspose.HTML στο Έργο Σας

Αν χρησιμοποιείτε Maven, προσθέστε το παρακάτω απόσπασμα στο `pom.xml`. Για Gradle ή απλές ρυθμίσεις μόνο JAR, ισχύουν οι ίδιες συντεταγμένες.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

> **Pro tip:** Η Aspose προσφέρει δωρεάν άδεια αξιολόγησης που μπορείτε να ενσωματώσετε ως αρχείο πόρου. Απλώς τοποθετήστε το `Aspose.HTML.lic` στο φάκελο `src/main/resources` και η βιβλιοθήκη θα το ανιχνεύσει αυτόματα.

## Βήμα 2: Δημιουργία Java Κλάσης για τη Μετατροπή

Παρακάτω βρίσκεται το πλήρες αρχείο πηγαίου κώδικα. Παρατηρήστε πως κάθε γραμμή είναι σχολιασμένη για να εξηγεί **γιατί** το κάνουμε—not just **what** we’re doing.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfConversionOptions;
import com.aspose.html.rendering.PageSize;
import com.aspose.html.rendering.Unit;

/**
 * Demonstrates how to convert an HTML file to a PDF with a custom page size
 * and a higher DPI (dots per inch) for sharper images.
 *
 * Run this class from your IDE or via `java -cp <classpath> ConvertWithOptions`.
 */
public class ConvertWithOptions {
    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1: Prepare conversion options
        // -----------------------------------------------------------------
        PdfConversionOptions conversionOptions = new PdfConversionOptions();

        // Set the page size to A5 (148 mm × 210 mm) – you can change these numbers
        // to any dimensions you need, e.g., a custom flyer size.
        conversionOptions.setPageSize(new PageSize(Unit.MILLIMETERS, 148, 210));

        // Choose a higher resolution: 150 DPI gives noticeably sharper raster images.
        // The default is usually 96 DPI, which can look blurry on printed media.
        conversionOptions.setResolution(150);

        // -----------------------------------------------------------------
        // Step 2: Perform the conversion
        // -----------------------------------------------------------------
        // Replace "YOUR_DIRECTORY" with the actual folder where your files live.
        String inputHtml = "YOUR_DIRECTORY/input.html";
        String outputPdf = "YOUR_DIRECTORY/output.pdf";

        // The static convert method does the heavy lifting.
        Converter.convert(inputHtml, outputPdf, conversionOptions);

        // -----------------------------------------------------------------
        // Step 3: Confirmation
        // -----------------------------------------------------------------
        System.out.println("Custom conversion done. PDF created at: " + outputPdf);
    }
}
```

### Γιατί Έχουν Σημασία Αυτές οι Ρυθμίσεις

- **`setPageSize`** – Από προεπιλογή η Aspose χρησιμοποιεί A4 (210 mm × 297 mm). Η αλλαγή του επιτρέπει την προσαρμογή του περιεχομένου σε φυλλάδιο, απόδειξη ή οποιαδήποτε προσαρμοσμένη μορφή.  
- **`setResolution`** – Το DPI επηρεάζει τη ραστεροποίηση των CSS background images, SVG και ακόμη και την απόδοση κειμένου όταν το PDF προβάλλεται σε οθόνη. Υψηλότερο DPI → μεγαλύτερο αρχείο αλλά πιο καθαρό αποτέλεσμα—ιδανικό για εκτυπώσεις υψηλής ποιότητας.  

## Βήμα 3: Εκτέλεση του Κώδικα και Έλεγχος του Αποτελέσματος

1. Συγκεντρώστε την κλάση:

   ```bash
   javac -cp "path/to/aspose-html.jar" ConvertWithOptions.java
   ```

2. Εκτελέστε την:

   ```bash
   java -cp ".:path/to/aspose-html.jar" ConvertWithOptions
   ```

3. Ανοίξτε το `output.pdf` σε οποιονδήποτε προβολέα PDF. Θα πρέπει να δείτε το HTML αποδομένο σε **σελίδα μεγέθους A5** με εμφανώς πιο καθαρές εικόνες.

> **Τι γίνεται αν χρειάζομαι οριζόντια προσανατολισμό;**  
> Απλώς ανταλλάξτε τις τιμές πλάτους και ύψους κατά τη δημιουργία του `PageSize`, ή χρησιμοποιήστε το βοηθητικό `PageSize.LANDSCAPE` αν προτιμάτε πιο δηλωτική προσέγγιση.

## Βήμα 4: Συνηθισμένες Παραλλαγές & Ακραίες Περιπτώσεις

| Σενάριο | Πώς να προσαρμόσετε τον κώδικα |
|----------|-----------------------|
| **Διάφορες μονάδες (ίντσες, points)** | Αντικαταστήστε το `Unit.MILLIMETERS` με `Unit.INCHES` ή `Unit.POINTS`. |
| **Πολλαπλά αρχεία HTML σε ένα PDF** | Δημιουργήστε ένα αντικείμενο `PdfConversionOptions` μία φορά, έπειτα καλέστε επανειλημμένα το `Converter.convert`, προσθέτοντας κάθε έξοδο στο ίδιο αντικείμενο `PdfDocument`. |
| **Δυναμικό μέγεθος σελίδας ανά έγγραφο** | Υπολογίστε πλάτος/ύψος κατά το χρόνο εκτέλεσης (π.χ. βάσει JSON config) πριν καλέσετε το `setPageSize`. |
| **Εκτέλεση σε web service** | Τυλίξτε τη λογική μετατροπής σε servlet ή Spring controller, ρέξτε τα bytes του PDF πίσω ως `application/pdf`. |
| **Περιβάλλοντα με περιορισμένη μνήμη** | Χρησιμοποιήστε `PdfConversionOptions.setMemoryLimit(...)` για να περιορίσετε τη χρήση heap· η Aspose θα γράψει στο δίσκο αν χρειαστεί. |

## Βήμα 5: Συμβουλές Επίλυσης Προβλημάτων

- **Κενές σελίδες** – Βεβαιωθείτε ότι το HTML σας περιέχει στοιχείο `<body>` και ότι όλα τα εξωτερικά CSS/JS αρχεία είναι προσβάσιμα από τον τρέχοντα κατάλογο εργασίας της JVM.  
- **Απουσία γραμματοσειρών** – Εγκαταστήστε τις απαιτούμενες γραμματοσειρές στον διακομιστή ή ενσωματώστε τις μέσω `PdfConversionOptions.setFontEmbeddingMode(...)`.  
- **Απρόσμενο DPI** – Ελέγξτε ξανά ότι δεν παρακάμπτετε την ανάλυση αργότερα στη διαδικασία (π.χ. μέσω PDF post‑processor).  

## Οπτική Αναφορά

Παρακάτω φαίνεται ένα γρήγορο screenshot του παραγόμενου PDF (A5 portrait). Το alt κείμενο περιέχει σκόπιμα τη βασική λέξη‑κλειδί για σκοπούς SEO.

![Create PDF custom size example](https://example.com/images/create-pdf-custom-size.png "Create PDF custom size example")

## Ανακεφαλαίωση: Τι Καταφέραμε

**Δημιουργήσαμε ένα πρόγραμμα Java που μετατρέπει HTML σε PDF**, ορίζοντας ρητά **προσαρμοσμένο μέγεθος σελίδας** και **αυξάνοντας το DPI** για πιο καθαρό αποτέλεσμα. Η λύση είναι αυτόνομη, χρησιμοποιεί μόνο το Aspose.HTML, και μπορεί να ενσωματωθεί σε οποιοδήποτε Maven‑βασισμένο έργο## Επόμενα Βήματα & Σχετικά Θέματα

- **Batch processing:** Επανάληψη σε φάκελο HTML αρχείων και συγχώνευση σε ένα ενιαίο PDF.  
- **Advanced styling:** Χρήση κανόνων CSS `@page` για έλεγχο περιθωρίων, κεφαλίδων και υποσέλιδων.  
- **Security considerations:** Καθαρισμός HTML που παρέχεται από χρήστη πριν τη μετατροπή για αποφυγή script injection.  

Αν σας ενδιαφέρει πιο προχωρημένος χειρισμός PDF—π.χ. προσθήκη σελιδοδεικτών, κρυπτογράφηση εγγράφου ή σήμανση υδατογραφήματος—εξετάστε τη βιβλιοθήκη **PDF for Java** της Aspose. Συνεργάζεται άψογα με τη ροή μετατροπής HTML που μόλις δημιουργήσαμε.

Καλή προγραμματιστική δουλειά, και τα PDFs σας να είναι πάντα του ακριβούς μεγέθους που χρειάζεστε!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}