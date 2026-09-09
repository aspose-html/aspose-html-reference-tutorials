---
category: general
date: 2026-01-07
description: Ορίστε το μέγεθος της σελίδας PDF κατά τη μετατροπή HTML σε PDF με Java.
  Μάθετε ένα πλήρες παράδειγμα μετατροπής HTML σε PDF σε Java, δημιουργήστε PDF από
  HTML και διαχειριστείτε τα περιθώρια.
draft: false
keywords:
- set pdf page size
- html to pdf java
- generate pdf from html
- html file to pdf
- html to pdf example
language: el
og_description: Ορίστε το μέγεθος σελίδας PDF κατά τη μετατροπή HTML σε PDF σε Java.
  Ακολουθήστε αυτό το βήμα‑βήμα παράδειγμα html σε pdf και μάθετε πώς να δημιουργήσετε
  pdf από html.
og_title: Ορισμός μεγέθους σελίδας PDF σε Java – Πλήρης οδηγός HTML σε PDF
tags:
- Java
- PDF conversion
- Aspose.HTML
title: Ορισμός μεγέθους σελίδας PDF σε Java – Πλήρης οδηγός HTML σε PDF
url: /el/java/conversion-html-to-other-formats/set-pdf-page-size-in-java-complete-html-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ορισμός Μεγέθους Σελίδας PDF σε Java – Πλήρης Οδηγός HTML σε PDF

Έχετε χρειαστεί ποτέ να **ορίσετε το μέγεθος σελίδας PDF** όταν μετατρέπετε ένα αρχείο HTML σε PDF χρησιμοποιώντας Java; Δεν είστε οι μόνοι. Οι περισσότεροι προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα: οι προεπιλεγμένες διαστάσεις σελίδας δεν ταιριάζουν με τη διάταξη που σχεδίασαν στο πρόγραμμα περιήγησης, και το αποτέλεσμα φαίνεται συμπιεσμένο ή υπερέκτεινο.

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα ένα παράδειγμα **full html to pdf java** που όχι μόνο *ορίζει το μέγεθος σελίδας PDF* αλλά και δείχνει πώς να **δημιουργήσετε pdf από html**, να ρυθμίσετε τα περιθώρια και ακόμη να ενεργοποιήσετε τη συμμόρφωση PDF‑A‑1b. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση πρόγραμμα που μετατρέπει το `input.html` σε `output.pdf` ακριβώς όπως το περιμένετε.

## Τι Θα Χρειαστεί

- **Java Development Kit (JDK) 8 ή νεότερο** – θα κάνουμε compile με `javac`.
- **Aspose.HTML for Java** library (ο κώδικας χρησιμοποιεί την έκδοση 23.10, αλλά οποιαδήποτε πρόσφατη έκδοση λειτουργεί).
- Ένα απλό **HTML file** που θέλετε να μετατρέψετε σε PDF (θα το ονομάσουμε `input.html`).
- Ένα IDE ή απλός επεξεργαστής κειμένου – συνήθως κωδικοποιώ στο IntelliJ, αλλά το Eclipse ή το VS Code είναι εντάξει.

> Συμβουλή επαγγελματία: Η Aspose προσφέρει δωρεάν άδεια αξιολόγησης 30 ημερών· απλώς τοποθετήστε τα JAR στο classpath του έργου σας και είστε έτοιμοι.

## Βήμα 1: Προσθήκη Aspose.HTML στο Έργο σας

Αν χρησιμοποιείτε Maven, επικολλήστε αυτήν την εξάρτηση στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

Για Gradle, προσθέστε:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

Ή, αν προτιμάτε τη χειροκίνητη μέθοδο, κατεβάστε το JAR από την ιστοσελίδα της Aspose και τοποθετήστε το στο φάκελο `libs/`, στη συνέχεια προσθέστε το στο classpath κατά τη μεταγλώττιση:

```bash
javac -cp "libs/*" AdvancedConvert.java
```

## Βήμα 2: Φόρτωση του Πηγαίου HTML Εγγράφου

Πρώτα δημιουργούμε μια παρουσία `HtmlDocument` που δείχνει στο αρχείο που θέλουμε να μετατρέψουμε. Ο κατασκευαστής δέχεται διαδρομή ή URL, ώστε να του δώσετε ό,τι μπορεί να διαβάσει η βιβλιοθήκη.

```java
import com.aspose.html.HtmlDocument;

// ...

// Load the HTML file from the local file system
HtmlDocument htmlDoc = new HtmlDocument("YOUR_DIRECTORY/input.html");
```

> Γιατί είναι σημαντικό: Η προηφόρτωση του εγγράφου παρέχει στον μετατροπέα ένα πλήρες δέντρο DOM, που είναι απαραίτητο για ακριβείς υπολογισμούς διάταξης—ιδιαίτερα όταν αργότερα **ορίσετε το μέγεθος σελίδας pdf**.

## Βήμα 3: Διαμόρφωση Επιλογών Μετατροπής PDF (Ορισμός Μεγέθους Σελίδας PDF)

Τώρα έρχεται η καρδιά του tutorial: η διαμόρφωση του `PdfConversionOptions`. Αυτό το αντικείμενο σας επιτρέπει να ορίσετε το μέγεθος σελίδας, τα περιθώρια και ακόμη τη συμμόρφωση PDF/A. Παρακάτω χρησιμοποιούμε το προκαθορισμένο `PdfPageSize.A4`, αλλά μπορείτε να επιλέξετε οποιαδήποτε τιμή του enum (`Letter`, `Legal`, `A3`, κλπ.) ή να δημιουργήσετε προσαρμοσμένο μέγεθος.

```java
import com.aspose.html.converters.PdfConversionOptions;
import com.aspose.html.render.PdfA;
import com.aspose.html.render.PdfPageSize;

// ...

PdfConversionOptions conversionOptions = new PdfConversionOptions();

// Set the desired PDF page size – this is where we *set pdf page size* for the output
conversionOptions.setPageSize(PdfPageSize.A4);          // A4 is 210 × 297 mm
conversionOptions.setMarginTop(10);                    // Top margin in points (≈0.35 mm)
conversionOptions.setMarginBottom(10);                 // Bottom margin in points
conversionOptions.setPdfA(PdfA.Standard.PdfA1b);       // Optional: enforce PDF‑A‑1b compliance
```

### Προσαρμοσμένο Μέγεθος Σελίδας (Bonus)

Αν τα τυπικά μεγέθη δεν ταιριάζουν στο σχέδιό σας, μπορείτε να δημιουργήσετε ένα `PdfPageSize` χειροκίνητα:

```java
import com.aspose.html.render.PdfPageSize;

// Width = 8.5 inches, Height = 11 inches (Letter size) in points (1 inch = 72 points)
PdfPageSize customSize = new PdfPageSize(8.5 * 72, 11 * 72);
conversionOptions.setPageSize(customSize);
```

> Ακραία περίπτωση: Όταν το HTML σας περιέχει στοιχεία που εκτείνονται πιο πλατιά από την επιλεγμένη σελίδα, ο μετατροπέας θα τα κλιμακώσει αυτόματα. Ωστόσο, ο ορισμός κατάλληλου μεγέθους σελίδας εκ των προτέρων αποφεύγει απροσδόκητη κλιμάκωση.

## Βήμα 4: Εκτέλεση της Μετατροπής

Με το έγγραφο φορτωμένο και τις επιλογές διαμορφωμένες, η πραγματική μετατροπή είναι μια γραμμή κώδικα. Η μέθοδος `Converter.convert` γράφει το PDF στη διαδρομή που καθορίζετε.

```java
import com.aspose.html.converters.Converter;

// ...

Converter.convert(htmlDoc, "YOUR_DIRECTORY/output.pdf", conversionOptions);
System.out.println("Conversion complete! PDF saved as output.pdf");
```

Αν εκτελέσετε το πρόγραμμα τώρα, θα δείτε το `output.pdf` στον φάκελο προορισμού, μορφοποιημένο στο **μέγεθος σελίδας A4** (ή όποιο μέγεθος επιλέξατε).

## Βήμα 5: Επαλήθευση του Αποτελέσματος – Γρήγορη Λίστα Ελέγχου

1. **Ανοίξτε το PDF** σε έναν προβολέα (Adobe Reader, Foxit κλπ.). Συμφωνεί κάθε σελίδα με τις διαστάσεις που ορίσατε;
2. **Ελέγξτε τα περιθώρια** – το πάνω και το κάτω πρέπει να είναι ακριβώς 10 points όπως ορίσαμε.
3. **Συμμόρφωση PDF/A** – αν ανοίξετε τις ιδιότητες του αρχείου, θα δείτε το “PDF/A‑1b” καταχωρημένο στην ενότητα “PDF version”.
4. **Ακρίβεια περιεχομένου** – συγκρίνετε το παραγόμενο PDF με το αρχικό HTML σε έναν φυλλομετρητή. Το κείμενο, οι εικόνες και το CSS πρέπει να είναι πανομοιότυπα.

Αν κάτι φαίνεται λανθασμένο, επιστρέψτε στο **Βήμα 3** και προσαρμόστε το μέγεθος σελίδας ή τα περιθώρια. Μικρές ρυθμίσεις συχνά λύνουν τις περισσότερες ιδιαιτερότητες διάταξης.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω βρίσκεται η πλήρης, έτοιμη‑για‑εκτέλεση κλάση Java. Απλώς αντικαταστήστε το `YOUR_DIRECTORY` με την απόλυτη διαδρομή όπου βρίσκεται το `input.html` σας.

```java
// AdvancedConvert.java
import com.aspose.html.HtmlDocument;
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfConversionOptions;
import com.aspose.html.render.PdfA;
import com.aspose.html.render.PdfPageSize;

public class AdvancedConvert {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the source HTML document
        HtmlDocument htmlDoc = new HtmlDocument("YOUR_DIRECTORY/input.html");

        // Step 2: Create PDF conversion options and configure page settings
        PdfConversionOptions conversionOptions = new PdfConversionOptions();
        conversionOptions.setPageSize(PdfPageSize.A4);          // Use A4 paper size
        conversionOptions.setMarginTop(10);                    // Top margin (points)
        conversionOptions.setMarginBottom(10);                 // Bottom margin (points)
        conversionOptions.setPdfA(PdfA.Standard.PdfA1b);       // Enable PDF‑A‑1b compliance

        // Step 3: Convert the HTML document to PDF using the configured options
        Converter.convert(htmlDoc, "YOUR_DIRECTORY/output.pdf", conversionOptions);

        System.out.println("PDF successfully generated with the set page size!");
    }
}
```

### Αναμενόμενη Έξοδος

Η εκτέλεση του προγράμματος εκτυπώνει:

```
PDF successfully generated with the set page size!
```

Και δημιουργεί το `output.pdf` του οποίου οι διαστάσεις σελίδας είναι **210 mm × 297 mm** (A4) με περιθώρια 10 points στην κορυφή/κάτω.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### “Μπορώ να ορίσω προσανατολισμό τοπίου (landscape);”

Ναι. Χρησιμοποιήστε το enum `PdfPageSize` για μεγέθη τοπίου (`A4_Landscape`, `Letter_Landscape`, κλπ.):

```java
conversionOptions.setPageSize(PdfPageSize.A4_Landscape);
```

### “Τι γίνεται αν το HTML μου χρησιμοποιεί εξωτερικό CSS ή εικόνες;”

Βεβαιωθείτε ότι οι διαδρομές είναι απόλυτες ή ότι το αρχείο HTML βρίσκεται στον ίδιο φάκελο με τα περιουσιακά στοιχεία. Ο μετατροπέας επιλύει σχετικές URL σε σχέση με τη θέση του αρχείου HTML.

### “Υπάρχει τρόπος να μετατρέψω πολλά αρχεία HTML ταυτόχρονα;”

Τυλίξτε τη λογική μετατροπής μέσα σε βρόχο:

```java
String[] files = {"file1.html", "file2.html"};
for (String f : files) {
    HtmlDocument doc = new HtmlDocument("YOUR_DIRECTORY/" + f);
    Converter.convert(doc, "YOUR_DIRECTORY/" + f.replace(".html", ".pdf"), conversionOptions);
}
```

### “Χρειάζομαι άδεια για παραγωγή;”

Μια άδεια αφαιρεί το υδατογράφημα αξιολόγησης και ξεκλειδώνει πλήρη απόδοση. Εγγραφείτε στην Aspose, κατεβάστε το αρχείο άδειας και φορτώστε το κατά την εκκίνηση της εφαρμογής:

```java
import com.aspose.html.License;
License license = new License();
license.setLicense("Aspose.Total.Java.lic");
```

## Συμπέρασμα

Μόλις καλύψαμε μια **complete html to pdf java** ροή εργασίας που σας επιτρέπει να **ορίσετε το μέγεθος σελίδας pdf** με ακρίβεια, να ελέγχετε τα περιθώρια και ακόμη να παράγετε αρχεία συμβατά με PDF‑A‑1b. Το παραπάνω απόσπασμα αποτελεί μια στιβαρή βάση για οποιοδήποτε έργο Java που χρειάζεται να **δημιουργήσει pdf από html**—είτε δημιουργείτε τιμολόγια, αναφορές ή e‑books.

Επόμενα βήματα; Δοκιμάστε να αλλάξετε το μέγεθος σελίδας σε `Letter`, πειραματιστείτε με προσαρμοσμένες διαστάσεις, ή προσθέστε κεφαλίδα/υποσέλιδο χρησιμοποιώντας το `PdfPageEditor` της Aspose. Μπορείτε επίσης να εξερευνήσετε τη μετατροπή ολόκληρου φακέλου αρχείων HTML, μετατρέποντας έναν στατικό ιστότοπο σε φορητό εγχειρίδιο PDF.

Έχετε περισσότερες ερωτήσεις σχετικά με τη μετατροπή **html file to pdf**, ή θέλετε να δείτε πώς να ενσωματώσετε γραμματοσειρές; Αφήστε ένα σχόλιο και ας συνεχίσουμε τη συζήτηση. Καλή κωδικοποίηση!

![Διάγραμμα που δείχνει τη ροή μετατροπής με ορισμένο μέγεθος σελίδας pdf](/images/set-pdf-page-size.png "παράδειγμα ορισμού μεγέθους σελίδας pdf")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}