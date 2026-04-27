---
category: general
date: 2026-04-26
description: Μετατρέψτε HTML σε PDF σε Java με το Aspose.HTML – μάθετε πώς να ορίσετε
  το μέγεθος σελίδας PDF, να προσθέσετε περιθώρια PDF και να εξάγετε HTML ως PDF σε
  λίγες γραμμές.
draft: false
keywords:
- convert html to pdf
- set pdf page size
- add pdf margins
- export html as pdf
- how to set margins
language: el
og_description: Μετατρέψτε HTML σε PDF σε Java με το Aspose.HTML. Αυτός ο οδηγός σας
  δείχνει πώς να ορίσετε το μέγεθος της σελίδας PDF, να προσθέσετε περιθώρια PDF και
  να εξάγετε γρήγορα το HTML ως PDF.
og_title: Μετατροπή HTML σε PDF σε Java – Ορισμός Μεγέθους Σελίδας & Περιθωρίων
tags:
- Java
- Aspose.HTML
- PDF conversion
title: Μετατροπή HTML σε PDF σε Java – Ορισμός μεγέθους σελίδας & περιθωρίων
url: /el/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-set-page-size-margins/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή HTML σε PDF σε Java – Ορισμός Μεγέθους Σελίδας & Περιθωρίων

Χρειάζεστε **μετατροπή HTML σε PDF σε Java**; Αντιμετωπίζετε δυσκολίες με **ορισμό μεγέθους σελίδας PDF** ή **προσθήκη περιθωρίων PDF**; Δεν είστε μόνοι. Σε πολλά έργα το τελικό PDF πρέπει να ταιριάζει με την εταιρική ταυτότητα, και αυτό σημαίνει ακριβείς διαστάσεις σελίδας και τακτοποιημένα περιθώρια.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που **εξάγει html ως pdf** χρησιμοποιώντας τη βιβλιοθήκη Aspose.HTML. Στο τέλος θα ξέρετε *πώς να ορίσετε περιθώρια* και γιατί η συμμόρφωση PDF‑A‑1b μπορεί να είναι σωτήρας για αρχειοθέτηση. Χωρίς ασαφείς αναφορές—μόνο ο κώδικας που μπορείτε να αντιγράψετε‑και‑επικολλήσετε και να τρέξετε.

## Τι Θα Χρειαστεί

- **Java 17** (ή οποιοδήποτε πρόσφατο JDK) – το API λειτουργεί με Java 8+ αλλά οι νεότερες εκδόσεις προσφέρουν καλύτερη απόδοση.  
- **Aspose.HTML for Java** JARs – μπορείτε να τα κατεβάσετε από το Maven Central repository ή από τον ιστότοπο της Aspose.  
- Ένα απλό αρχείο **input.html** που θέλετε να μετατρέψετε σε PDF.  
- Λίγος χώρος στο δίσκο για το αρχείο εξόδου (το PDF θα είναι μερικές εκατοντάδες kilobytes).  

Αυτό είναι όλο. Χωρίς επιπλέον frameworks, χωρίς εξωτερικές υπηρεσίες. Αν έχετε αυτά τα στοιχεία, μπορούμε να ξεκινήσουμε.

## Μετατροπή HTML σε PDF – Στοιχειώδη Επισκόπηση Βήμα‑βήμα

Παρακάτω είναι η υψηλού επιπέδου ροή που θα ακολουθήσουμε:

1. **Καθορίστε την πηγή HTML** – τοπικό αρχείο, απομακρυσμένο URL ή ένα `InputStream`.  
2. **Διαμορφώστε τις επιλογές αποθήκευσης PDF** – ορίστε μέγεθος σελίδας, περιθώρια και συμμόρφωση PDF‑A.  
3. **Εκτελέστε τη μετατροπή** – αφήστε το Aspose να κάνει το σκληρό έργο.  

Κάθε ένα από αυτά τα βήματα αναλύεται σε δική του ενότητα, ώστε να μπορείτε να επιλέξετε μόνο τα τμήματα που χρειάζεστε.

## Βήμα 1: Καθορίστε την Πηγή HTML

Το πρώτο πράγμα που χρειάζεται ο μετατροπέας είναι μια αναφορά στο HTML που θέλετε να μετατρέψετε σε PDF. Το Aspose.HTML είναι ευέλικτο: μπορείτε να του δώσετε μια διαδρομή, ένα URL ή ακόμη και ένα stream αν το HTML σας βρίσκεται στη μνήμη.

```java
// Step 1 – Define where the HTML comes from
String htmlPath = "YOUR_DIRECTORY/input.html"; // replace with your actual file
```

> **Γιατί είναι σημαντικό:** Η χρήση ενός απλού string κρατά το παράδειγμα απλό, αλλά σε πραγματικές συνθήκες μπορεί να αντλήσετε το HTML από μια web υπηρεσία ή μια βάση δεδομένων. Το API δέχεται επίσης `java.net.URL` ή `java.io.InputStream`, κάτι που είναι χρήσιμο όταν δεν θέλετε να γράψετε ένα προσωρινό αρχείο.

## Βήμα 2: Ορισμός Μεγέθους Σελίδας PDF

Τα περισσότερα PDFs έχουν προεπιλεγμένο μέγεθος **Letter**, το οποίο μπορεί να φαίνεται περίεργο αν το κοινό σας αναμένει **A4**. Η αλλαγή του μεγέθους σελίδας γίνεται με μία γραμμή κώδικα μέσω του `PdfSaveOptions`.

```java
// Step 2 – Create PDF options and set the page size to A4
PdfSaveOptions pdfOptions = new PdfSaveOptions();
pdfOptions.setPageSize(PdfPageSize.A4); // this is the “set pdf page size” step
```

> **Pro tip:** Αν χρειάζεστε προσαρμοσμένο μέγεθος (π.χ. μορφή απόδειξης), το Aspose σας επιτρέπει να περάσετε ένα αντικείμενο `SizeF` με ακριβές πλάτος και ύψος σε points.

## Βήμα 3: Προσθήκη Περιθωρίων PDF

Τα περιθώρια αποτρέπουν το περιεχόμενο να αγγίζει την άκρη της σελίδας. Μετρώνται σε points (1 mm ≈ 2.8346 pt), αλλά το Aspose προσφέρει μια βολική κλάση `Margin` που δέχεται χιλιοστά απευθείας.

```java
// Step 3 – Define 20 mm margins on all sides (how to set margins)
pdfOptions.setMargins(new Margin(20, 20, 20, 20));
```

> **Γιατί σας ενδιαφέρει:** Χωρίς περιθώρια, οι κεφαλίδες μπορεί να κοπούν κατά την εκτύπωση και τα υποσέλιδα να εξαφανιστούν στην μη‑εκτυπώσιμη περιοχή του εκτυπωτή. Συνεπή περιθώρια κάνουν επίσης το PDF να φαίνεται επαγγελματικό.

## Βήμα 4: Ενεργοποίηση Συμμόρφωσης PDF‑A‑1b (Προαιρετικό αλλά Συνιστώμενο)

Αν αρχειοθετείτε έγγραφα για νομικούς ή κανονιστικούς λόγους, το PDF‑A‑1b διασφαλίζει ότι το αρχείο είναι αυτόνομο και ανθεκτικό στο χρόνο.

```java
// Step 4 – Make the PDF archival‑ready
pdfOptions.setPdfACompliance(PdfACompliance.PdfA1b);
```

> **Σύντομη σημείωση:** Η συμμόρφωση PDF‑A μπορεί να αυξήσει λίγο το μέγεθος του αρχείου επειδή οι γραμματοσειρές ενσωματώνονται. Είναι ένα μικρό κόστος για τη μακροπρόθεσμη αναγνωσιμότητα.

## Βήμα 5: Εκτέλεση της Μετατροπής

Τώρα που όλα είναι διαμορφωμένα, η πραγματική μετατροπή είναι μια ενιαία στατική κλήση. Το Aspose διαχειρίζεται τη μηχανή απόδοσης, CSS, JavaScript (αν είναι ενεργοποιημένο) και την ενσωμάτωση εικόνων στο παρασκήνιο.

```java
// Step 5 – Convert the HTML to PDF using the configured options
Converter.convertHtmlToPdf(htmlPath, "YOUR_DIRECTORY/output.pdf", pdfOptions);
```

Αυτό είναι ολόκληρο το πρόγραμμα! Συγκεντρώστε όλα τα αποσπάσματα μαζί και θα έχετε μια εκτελέσιμη κλάση.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι το πλήρες πρόγραμμα Java που μπορείτε να αντιγράψετε στο `ConvertHtmlToPdfCustom.java`. Αντικαταστήστε τις διαδρομές placeholder με πραγματικές τοποθεσίες στο σύστημά σας.

```java
import com.aspose.html.*;
import com.aspose.html.converters.*;
import com.aspose.html.saving.*;

public class ConvertHtmlToPdfCustom {
    public static void main(String[] args) throws Exception {

        // Step 1: Specify the source HTML file (local file, URL, or stream)
        String htmlPath = "YOUR_DIRECTORY/input.html";

        // Step 2: Configure PDF output options
        //   • A4 page size
        //   • 20 mm margins on all sides
        //   • PDF‑A‑1b compliance for archival
        PdfSaveOptions pdfOptions = new PdfSaveOptions();
        pdfOptions.setPageSize(PdfPageSize.A4);
        pdfOptions.setMargins(new Margin(20, 20, 20, 20));
        pdfOptions.setPdfACompliance(PdfACompliance.PdfA1b);

        // Step 3: Convert the HTML to PDF using the configured options
        Converter.convertHtmlToPdf(htmlPath, "YOUR_DIRECTORY/output.pdf", pdfOptions);
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Η εκτέλεση του προγράμματος δημιουργεί το `output.pdf` που:

- Είναι **A4** (210 mm × 297 mm).  
- Έχει **20 mm** περιθώρια στα αριστερά, δεξιά, πάνω και κάτω.  
- Είναι **PDF‑A‑1b** συμμορφωμένο, δηλαδή όλες οι γραμματοσειρές είναι ενσωματωμένες και το αρχείο είναι αυτόνομο.  
- Αναπαράγει πιστά τη διάταξη του `input.html` (εικόνες, πίνακες και στυλ CSS διατηρούνται).

Μπορείτε να ανοίξετε το PDF σε οποιονδήποτε προβολέα (Adobe Acrobat, Foxit ή ακόμη και Chrome) και θα δείτε μια καθαρή σελίδα με άνετο λευκό περιθώριο γύρω από το περιεχόμενο.

![προεπισκόπηση εξόδου μετατροπής html σε pdf](/images/convert-html-to-pdf.png)

*Σχήμα: Μια γρήγορη ματιά στο παραγόμενο PDF μετά τη μετατροπή.*

## Συχνές Ερωτήσεις και Ακραίες Περιπτώσεις

### Τι γίνεται αν το HTML μου περιέχει εξωτερικό CSS ή εικόνες;

Το Aspose.HTML ακολουθεί τους ίδιους κανόνες με τους browsers. Εφόσον τα URLs είναι προσβάσιμα (απόλυτα ή σχετικά με το φάκελο του HTML αρχείου), ο μετατροπέας θα τα κατεβάσει. Αν τρέχετε τον κώδικα σε διακομιστή χωρίς πρόσβαση στο internet, σκεφτείτε την ενσωμάτωση πόρων ως **data‑URI** strings ή την προφόρτωση τους σε ένα `MemoryStream`.

### Πώς να μετατρέψω ένα **URL** αντί για αρχείο;

Απλώς αντικαταστήστε το string `htmlPath` με ένα URL:

```java
String htmlPath = "https://example.com/report.html";
```

Η ίδια υπερφόρτωση `Converter.convertHtmlToPdf` θα κατεβάσει και θα αποδώσει τη σελίδα.

### Μπορώ να αλλάξω τις μονάδες των περιθωρίων σε ίντσες ή points;

Ναι. Ο κατασκευαστής `Margin` δέχεται επίσης `float left, float top, float right, float bottom` σε **points**. Αν προτιμάτε ίντσες, πολλαπλασιάστε με 72 (1 inch = 72 pt). Για παράδειγμα, περιθώρια 0.5 in θα ήταν `new Margin(36, 36, 36, 36)`.

### Τι γίνεται αν χρειάζομαι **διαφορετικό προσανατολισμό σελίδας** (landscape);

Ορίστε την ιδιότητα `PageOrientation` πριν καλέσετε το `setPageSize`:

```java
pdfOptions.setPageOrientation(PageOrientation.Landscape);
pdfOptions.setPageSize(PdfPageSize.A4);
```

### Υπάρχει τρόπος να **προσθέσω αυτόματα κεφαλίδα/υποσέλιδο**;

Το Aspose.HTML σας επιτρέπει να ενσωματώσετε αποσπάσματα HTML που λειτουργούν ως κεφαλίδες ή υποσέλιδα μέσω της κλάσης `PdfPageTemplate`. Δημιουργείτε ένα μικρό HTML τμήμα με το επιθυμητό κείμενο, έπειτα το αναθέτετε στο `pdfOptions.getPageTemplate().setHeaderHtml(...)` (ή `.setFooterHtml(...)`). Είναι ένα ευρύ θέμα, αλλά το κύριο συμπέρασμα είναι: μπορείτε να αντιμετωπίσετε κεφαλίδες/υποσέλιδα ως κανονικό HTML.

## Συμβουλές για Κώδικα Έτοιμο για Παραγωγή

- **License the library** – the free

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}