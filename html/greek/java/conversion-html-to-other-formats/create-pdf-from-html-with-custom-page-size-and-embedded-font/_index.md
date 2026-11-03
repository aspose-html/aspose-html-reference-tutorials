---
category: general
date: 2026-03-05
description: Δημιουργήστε PDF από HTML γρήγορα χρησιμοποιώντας το Aspose.HTML – ορίστε
  προσαρμοσμένο μέγεθος σελίδας PDF, ενσωματώστε γραμματοσειρές και μάθετε πώς να
  μετατρέψετε HTML σε PDF με πλήρη κώδικα.
draft: false
keywords:
- create pdf from html
- convert html to pdf
- html to pdf conversion
- custom pdf page size
- embed fonts pdf
language: el
og_description: Δημιουργήστε PDF από HTML με το Aspose.HTML. Αυτός ο οδηγός δείχνει
  πώς να ορίσετε προσαρμοσμένο μέγεθος σελίδας PDF, να ενσωματώσετε γραμματοσειρές
  στο PDF και να πραγματοποιήσετε μετατροπή από HTML σε PDF.
og_title: Δημιουργία PDF από HTML – Προσαρμοσμένο μέγεθος σελίδας & ενσωματωμένες
  γραμματοσειρές
tags:
- Java
- PDF
- Aspose.HTML
title: Δημιουργία PDF από HTML με προσαρμοσμένο μέγεθος σελίδας και ενσωματωμένες
  γραμματοσειρές
url: /el/java/conversion-html-to-other-formats/create-pdf-from-html-with-custom-page-size-and-embedded-font/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία PDF από HTML με Προσαρμοσμένο Μέγεθος Σελίδας και Ενσωματωμένες Γραμματοσειρές

Έχετε ποτέ χρειαστεί να **create PDF from HTML** αλλά νιώσατε κολλημένοι στο στάδιο του styling; Δεν είστε μόνοι. Είτε μετατρέπετε μια σελίδα προώθησης μάρκετινγκ σε ένα εκτυπώσιμο φυλλάδιο είτε αρχειοθετείτε τιμολόγια που δημιουργούνται σε μια web εφαρμογή, πιθανότατα θέλετε ένα PDF που ταιριάζει ακριβώς στις διαστάσεις της μάρκας σας και διατηρεί κάθε γραμματοσειρά καθαρή.  

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει πώς να **convert HTML to PDF** χρησιμοποιώντας το Aspose.HTML for Java, να ορίσετε ένα **custom PDF page size**, και να ενεργοποιήσετε το **embed fonts PDF** ώστε το αποτέλεσμα να φαίνεται ταυτόσημο σε οποιονδήποτε υπολογιστή. Στο τέλος θα έχετε μια μοναδική κλάση Java που μπορείτε να ενσωματώσετε στο πρόγραμμά σας και να αρχίσετε να δημιουργείτε PDFs αμέσως.

## Τι Θα Μάθετε

* Πώς να προσθέσετε τη βιβλιοθήκη Aspose.HTML σε ένα έργο Maven ή Gradle.  
* Πώς να διαμορφώσετε το **PdfConversionOptions** για ένα **custom pdf page size** (8.5 × 11 ίντσες σε αυτήν την περίπτωση).  
* Πώς να ενεργοποιήσετε το **embed fonts pdf** ώστε το κείμενο να αποδίδεται σωστά ακόμη και όταν το σύστημα-στόχος δεν διαθέτει τις αρχικές γραμματοσειρές.  
* Πώς να εκτελέσετε τη **HTML to PDF conversion** και να διαβάσετε τον αριθμό σελίδων που προκύπτει.  

Χωρίς περιττά, μόνο μια πρακτική, end‑to‑end λύση που μπορείτε να αντιγράψετε‑και‑επικολλήσετε.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

* Java 17 ή νεότερη εγκατεστημένη (το API λειτουργεί με Java 8+, αλλά τα νεότερα JDK παρέχουν καλύτερη απόδοση).  
* Ένα εργαλείο κατασκευής – Maven ή Gradle – για να κατεβάσετε το Aspose.HTML JAR από το αποθετήριο Maven Central.  
* Ένα αρχείο HTML (`sample.html`) που θέλετε να μετατρέψετε σε PDF.  
* Μια μικρή περιέργεια για τη διάταξη σελίδων PDF – θα το καλύψουμε στον κώδικα.  

> **Pro tip:** Εάν δεν έχετε διαθέσιμο αρχείο HTML, δημιουργήστε απλώς ένα απλό με ένα `<h1>` και μια παράγραφο· η μετατροπή λειτουργεί με τον ίδιο τρόπο.

## Βήμα 1: Προσθήκη του Aspose.HTML στο Έργο σας (Convert HTML to PDF)

Αν χρησιμοποιείτε **Maven**, προσθέστε την ακόλουθη εξάρτηση στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- latest at time of writing -->
</dependency>
```

Για **Gradle**, προσθέστε αυτή τη γραμμή στο `build.gradle`:

```gradle
implementation 'com.aspose:aspose-html:23.12'
```

Αυτή η μοναδική γραμμή σας παρέχει όλα όσα χρειάζεστε για **html to pdf conversion** – το `Converter`, τις κλάσεις επιλογών και τις βοηθητικές λειτουργίες σχεδίασης.

## Βήμα 2: Διαμόρφωση Προσαρμοσμένου Μεγέθους Σελίδας PDF (Custom PDF Page Size)

Τώρα που η βιβλιοθήκη βρίσκεται στο classpath, μπορούμε να αρχίσουμε να διαμορφώνουμε το αποτέλεσμα. Το αντικείμενο `PdfConversionOptions` σας επιτρέπει να ορίσετε διαστάσεις σελίδας, περιθώρια και αν οι γραμματοσειρές πρέπει να ενσωματωθούν. Ακολουθεί ο κώδικας που ορίζει ένα **custom pdf page size** 8.5 × 11 ίντσες με περιθώρια μισού ίντσου σε όλες τις πλευρές:

```java
// Step 2: Create PDF conversion options and configure page size, margins, and font embedding
PdfConversionOptions pdfOptions = new PdfConversionOptions();

// Set a custom PDF page size – 8.5 × 11 inches (Letter)
pdfOptions.setPageSize(new SizeF(Unit.inch(8.5), Unit.inch(11)));

// Margins are also expressed in inches; here we use 0.5 in on each side
pdfOptions.setMargins(0.5, 0.5, 0.5, 0.5); // left, top, right, bottom

// Enable font embedding so the PDF looks the same everywhere
pdfOptions.setEmbedFonts(true);
```

Παρατηρήστε την κλήση στο `setEmbedFonts(true)`. Αυτό είναι το σήμα που λέει στο Aspose.HTML να **embed fonts PDF** αρχεία, εξαλείφοντας το πρόβλημα «missing font» που μερικές φορές εμφανίζεται όταν ανοίγετε PDFs σε διαφορετικό υπολογιστή.

## Βήμα 3: Εκτέλεση της HTML to PDF Conversion

Με τις επιλογές έτοιμες, η πραγματική μετατροπή είναι μια γραμμή κώδικα. Σημειώνουμε το `Converter` στο αρχείο HTML προέλευσης και στο αρχείο PDF προορισμού, και του δίνουμε τις επιλογές που μόλις δημιουργήσαμε:

```java
// Step 3: Convert the HTML file to PDF using the configured options
String htmlPath = "YOUR_DIRECTORY/sample.html";
String pdfPath  = "YOUR_DIRECTORY/custom.pdf";

PdfConversionResult conversionResult = Converter.convertHTML(htmlPath, pdfPath, pdfOptions);
```

Αν όλα πάνε ομαλά, το `conversionResult` θα περιέχει μεταδεδομένα για το παραγόμενο PDF, όπως ο αριθμός των σελίδων.

## Βήμα 4: Επαλήθευση του Αποτελέσματος – Έλεγχος Αριθμού Σελίδων

Πάντα είναι καλό να επιβεβαιώσετε ότι η μετατροπή πέτυχε. Το `PdfConversionResult` σας παρέχει έναν γρήγορο τρόπο για να διαβάσετε τον αριθμό σελίδων:

```java
// Step 4: Output the number of pages in the generated PDF
System.out.println("Custom PDF created, pages: " + conversionResult.getPageCount());
```

Η εκτέλεση του προγράμματος θα πρέπει να εκτυπώσει κάτι όπως:

```
Custom PDF created, pages: 1
```

Αυτή η γραμμή σας λέει ότι η **html to pdf conversion** παρήγαγε ένα PDF μιας σελίδας, ταιριάζοντας με το **custom pdf page size** που ορίσατε. Εάν το αρχικό HTML είναι μεγαλύτερο, θα δείτε αυτόματα μεγαλύτερο αριθμό σελίδων.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω βρίσκεται η πλήρης κλάση Java που μπορείτε να αντιγράψετε σε ένα αρχείο με όνομα `ConvertHtmlToPdfWithOptions.java`. Αντικαταστήστε το `YOUR_DIRECTORY` με το πραγματικό φάκελο όπου βρίσκεται το `sample.html`.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.pdf.PdfConversionOptions;
import com.aspose.html.converters.pdf.PdfConversionResult;
import com.aspose.html.drawing.SizeF;
import com.aspose.html.drawing.Unit;

public class ConvertHtmlToPdfWithOptions {
    public static void main(String[] args) throws Exception {

        // Step 1: Create PDF conversion options and configure page size, margins, and font embedding
        PdfConversionOptions pdfOptions = new PdfConversionOptions();
        pdfOptions.setPageSize(new SizeF(Unit.inch(8.5), Unit.inch(11)));
        pdfOptions.setMargins(0.5, 0.5, 0.5, 0.5);   // left, top, right, bottom (in inches)
        pdfOptions.setEmbedFonts(true);            // embed fonts PDF for consistent rendering

        // Step 2: Convert the HTML file to PDF using the configured options
        String htmlPath = "YOUR_DIRECTORY/sample.html";
        String pdfPath  = "YOUR_DIRECTORY/custom.pdf";
        PdfConversionResult conversionResult = Converter.convertHTML(htmlPath, pdfPath, pdfOptions);

        // Step 3: Output the number of pages in the generated PDF
        System.out.println("Custom PDF created, pages: " + conversionResult.getPageCount());
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Αφού μεταγλωττίσετε (`javac ConvertHtmlToPdfWithOptions.java`) και εκτελέσετε την κλάση (`java ConvertHtmlToPdfWithOptions`), θα βρείτε το `custom.pdf` στον ίδιο φάκελο. Ανοίξτε το με οποιονδήποτε προβολέα PDF· θα πρέπει να δείτε το αρχικό σας HTML αποδομένο σε ένα **custom pdf page size** με όλες τις γραμματοσειρές σωστά ενσωματωμένες. Χωρίς προειδοποιήσεις missing‑glyph, χωρίς αλλαγές διάταξης.

![Παράδειγμα δημιουργίας PDF από HTML που εμφανίζει την προεπισκόπηση του παραγόμενου PDF](/images/create-pdf-from-html-preview.png "δημιουργία pdf από html προεπισκόπηση")

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

**Τι γίνεται αν το HTML μου αναφέρεται σε εξωτερικά CSS ή εικόνες;**  
Το Aspose.HTML ακολουθεί τους ίδιους κανόνες με ένα πρόγραμμα περιήγησης. Εφόσον οι διαδρομές είναι απόλυτες ή σχετικές με τη θέση του αρχείου HTML, ο μετατροπέας θα τις φορτώσει. Για απομακρυσμένα URLs, βεβαιωθείτε ότι η μηχανή που εκτελεί τη μετατροπή έχει πρόσβαση στο διαδίκτυο.

**Μπορώ να αλλάξω τον προσανατολισμό της σελίδας σε landscape;**  
Απόλυτα. Απλώς ανταλλάξτε τις τιμές πλάτους και ύψους όταν καλέσετε το `setPageSize`:

```java
pdfOptions.setPageSize(new SizeF(Unit.inch(11), Unit.inch(8.5)));
```

**Χρειάζομαι άδεια για το Aspose.HTML για παραγωγική χρήση;**  
Η βιβλιοθήκη λειτουργεί σε λειτουργία αξιολόγησης, αλλά προσθέτει υδατογράφημα στο PDF. Για εμπορικά έργα θα χρειαστείτε ένα έγκυρο αρχείο άδειας — απλώς φορτώστε το στην αρχή του προγράμματός σας με `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`.

**Τι γίνεται με τις γραμματοσειρές Unicode;**  
Εάν το HTML σας περιέχει μη‑λατινικούς χαρακτήρες, βεβαιωθείτε ότι οι γραμματοσειρές που ενσωματώνετε υποστηρίζουν αυτά τα σημεία κώδικα. Η ρύθμιση `setEmbedFonts(true)` θα ενσωματώσει ολόκληρο το αρχείο γραμματοσειράς, έτσι το PDF θα αποδίδει σωστά το Unicode σε οποιαδήποτε συσκευή.

## Συμπέρασμα

Τώρα γνωρίζετε ακριβώς πώς να **create PDF from HTML** ελέγχοντας το **custom pdf page size** και διασφαλίζοντας ότι το τελικό έγγραφο **embed fonts PDF** για άψογη απόδοση σε όλες τις πλατφόρμες. Το παράδειγμα καλύπτει ολόκληρη τη διαδικασία **html to pdf conversion** — από τη ρύθμιση των εξαρτήσεων, τη διαμόρφωση των επιλογών, μέχρι την επαλήθευση του αποτελέσματος.

Θέλετε να προχωρήσετε περαιτέρω; Δοκιμάστε να πειραματιστείτε με:

* **Multiple page sizes** σε ένα έγγραφο (διαφορετικές επιλογές ανά μετατροπή).  
* **Header/footer templates** χρησιμοποιώντας το `PdfPageSettings` του Aspose.HTML.  
* **Security features** όπως προστασία με κωδικό (`PdfEncryptionOptions`).  

Κάθε ένα από αυτά βασίζεται στην ίδια θεμελιώδη βάση που μόλις παρουσιάσαμε, έτσι θα είστε έτοιμοι να τα αντιμετωπίσετε χωρίς προβλήματα.

Καλό κώδικα, και απολαύστε τη μετατροπή των ιστοσελίδων σας σε τέλεια μορφοποιημένα PDFs!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}