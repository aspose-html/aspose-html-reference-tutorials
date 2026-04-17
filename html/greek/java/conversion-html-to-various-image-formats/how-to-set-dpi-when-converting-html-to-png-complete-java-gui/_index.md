---
category: general
date: 2026-03-14
description: Μάθετε πώς να ορίζετε το DPI κατά τη μετατροπή HTML σε PNG με το Aspose.HTML.
  Περιλαμβάνει εξαγωγή HTML ως PNG, αποθήκευση HTML ως PNG και αντικατάσταση διαφανούς
  φόντου.
draft: false
keywords:
- how to set dpi
- convert html to png
- export html as png
- save html as png
- replace transparent background
language: el
og_description: Πώς να ορίσετε το DPI κατά τη μετατροπή HTML σε PNG χρησιμοποιώντας
  το Aspose.HTML. Οδηγός βήμα‑βήμα για εξαγωγή HTML ως PNG, αποθήκευση HTML ως PNG
  και αντικατάσταση διαφανούς φόντου.
og_title: Πώς να ορίσετε DPI κατά τη μετατροπή HTML σε PNG – Java Tutorial
tags:
- Java
- Aspose.HTML
- Image Export
title: Πώς να ορίσετε DPI κατά τη μετατροπή HTML σε PNG – Πλήρης οδηγός Java
url: /el/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-html-to-png-complete-java-gui/
---

construct final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ορίσετε DPI κατά τη μετατροπή HTML σε PNG – Πλήρης Οδηγός Java

Έχετε αναρωτηθεί ποτέ **πώς να ορίσετε DPI** για μια εικόνα που δημιουργείται από HTML; Ίσως ετοιμάζετε μια εκτυπώσιμη αναφορά και το προεπιλεγμένο 96 DPI φαίνεται θολό στο χαρτί. Τα καλά νέα είναι ότι δεν χρειάζεται να ψάχνετε για σπάνιες βιβλιοθήκες—το Aspose.HTML κάνει τη βαριά δουλειά, και μπορείτε να ελέγξετε την ανάλυση με λίγες μόνο γραμμές κώδικα. Σε αυτό το tutorial θα σας δείξουμε επίσης πώς να **μετατρέψετε HTML σε PNG**, **εξάγετε HTML ως PNG**, και ακόμη **αντικαταστήσετε το διαφανές φόντο** με ένα στερεό χρώμα.

Θα περάσουμε από όλα όσα χρειάζεστε: την απαιτούμενη εξάρτηση Maven, μια πλήρως εκτελέσιμη κλάση Java, και συμβουλές για κοινά προβλήματα. Στο τέλος θα έχετε ένα καθαρό PNG 300 DPI έτοιμο για εκτύπωση υψηλής ποιότητας ή ενσωμάτωση σε PDF.

## Προαπαιτούμενα

- Java 17 (ή οποιοδήποτε πρόσφατο JDK)  
- Maven ή Gradle εργαλείο κατασκευής  
- Aspose.HTML for Java (μπορείτε να λάβετε δωρεάν δοκιμή από την ιστοσελίδα της Aspose)  
- Ένα αρχείο HTML που θέλετε να μετατρέψετε σε εικόνα (οποιοδήποτε έγκυρο HTML λειτουργεί)

> **Συμβουλή:** Αν χρησιμοποιείτε IDE όπως το IntelliJ IDEA, ενεργοποιήστε το “Show whitespaces” – βοηθά να εντοπίσετε τυχαία κενά που θα μπορούσαν να σπάσουν τις διαδρομές αρχείων.

## Βήμα 1: Προσθήκη εξάρτησης Aspose.HTML

Πρώτα, πείτε στο Maven πού να κατεβάσει τη βιβλιοθήκη. Επικολλήστε το παρακάτω απόσπασμα στο `pom.xml` μέσα στο `<dependencies>`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

Αν προτιμάτε Gradle, το ισοδύναμο είναι:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

> **Γιατί είναι σημαντικό:** Χωρίς τη σωστή έκδοση θα λάβετε σφάλματα κατά τη μεταγλώττιση όπως `cannot find class com.aspose.html.Conversion`. Η βιβλιοθήκη περιλαμβάνει όλα όσα χρειάζεστε για απόδοση HTML, διαχείριση DPI, και αποθήκευση εικόνας.

## Βήμα 2: Προετοιμασία του πηγαίου HTML και των διαδρομών προορισμού

Μπορείτε να τοποθετήσετε το αρχείο HTML οπουδήποτε στο δίσκο, αλλά κρατήστε τη διαδρομή απλή για να αποφύγετε προβλήματα διαφυγής. Για αυτό το παράδειγμα θα υποθέσουμε έναν φάκελο που ονομάζεται `reports` μέσα στη ρίζα του έργου:

```java
String htmlPath = "reports/report.html";   // source HTML
String pngPath  = "reports/report.png";    // output PNG
```

> **Ακραία περίπτωση:** Στα Windows, χρησιμοποιήστε μπροστιές κάθετες (`/`) ή διπλές ανάστροφες (`\\`). Ο συνδυασμός τους μπορεί να προκαλέσει `FileNotFoundException`.

## Βήμα 3: Διαμόρφωση επιλογών αποθήκευσης PNG και ορισμός DPI

Αυτό είναι η καρδιά του **πώς να ορίσετε DPI**. Η κλάση `PngSaveOptions` εκθέτει τις μεθόδους `setDpiX` και `setDpiY`. Μπορείτε επίσης να επιλέξετε χρώμα φόντου για **αντικατάσταση του διαφανούς φόντου**—χρήσιμο όταν το HTML περιέχει ημιδιαφανή στοιχεία.

```java
// Create PNG save options
PngSaveOptions pngOptions = new PngSaveOptions();

// Set horizontal and vertical DPI – 300 is a common print resolution
pngOptions.setDpiX(300);
pngOptions.setDpiY(300);

// Replace any transparency with solid white (you could pick any Color)
pngOptions.setBackgroundColor(Color.getWhite());
```

> **Γιατί 300 DPI;** Οι περισσότερες εκτυπωτές απαιτούν τουλάχιστον 300 DPI για καθαρό αποτέλεσμα. Οι χαμηλότερες τιμές φαίνονται εντάξει στις οθόνες αλλά θα εμφανιστούν θολές όταν εκτυπωθούν.

## Βήμα 4: Εκτέλεση της μετατροπής

Τώρα καλούμε τη στατική μέθοδο `Conversion.convert`. Διαβάζει το HTML, το αποδίδει στην ζητούμενη DPI, και γράφει το αρχείο PNG.

```java
Conversion.convert(htmlPath, pngPath, pngOptions);
System.out.println("PNG created with 300 DPI at: " + pngPath);
```

Αν όλα πάνε καλά, θα δείτε το μήνυμα στην κονσόλα που επιβεβαιώνει τη θέση του αρχείου.

## Βήμα 5: Επαλήθευση του Αποτελέσματος (Προαιρετικό αλλά Συνιστάται)

Ανοίξτε το παραγόμενο PNG σε προβολέα εικόνας που εμφανίζει DPI—Windows Photo Viewer, macOS Preview, ή ακόμη `identify` από το ImageMagick:

```bash
identify -format "%x x %y DPI\n" reports/report.png
```

Θα πρέπει να δείτε `300 x 300 DPI`. Αν οι αριθμοί είναι διαφορετικοί, ελέγξτε ξανά ότι κάλεσατε `setDpiX/Y` **πριν** τη μετατροπή.

## Πλήρες, Έτοιμο‑για‑Εκτέλεση Παράδειγμα

Παρακάτω είναι η πλήρης κλάση Java που συνδυάζει όλα τα κομμάτια. Αντιγράψτε‑επικολλήστε την σε ένα αρχείο με όνομα `HtmlToPngCustom.java` μέσα στο `src/main/java/com/example`.

```java
package com.example;

import com.aspose.html.Conversion;
import com.aspose.html.saving.PngSaveOptions;
import com.aspose.html.drawing.Color;

/**
 * Demonstrates how to set DPI while converting HTML to PNG using Aspose.HTML.
 * The example also shows how to export HTML as PNG, save HTML as PNG, and
 * replace transparent background with white.
 */
public class HtmlToPngCustom {
    public static void main(String[] args) throws Exception {

        // Step 1: Source HTML and destination PNG paths
        String htmlPath = "reports/report.html";
        String pngPath  = "reports/report.png";

        // Step 2: Create PNG options and configure high‑resolution output
        PngSaveOptions pngOptions = new PngSaveOptions();
        pngOptions.setDpiX(300);                         // Horizontal DPI
        pngOptions.setDpiY(300);                         // Vertical DPI
        pngOptions.setBackgroundColor(Color.getWhite()); // Replace transparency with white

        // Step 3: Convert the HTML document to a PNG image using the defined options
        Conversion.convert(htmlPath, pngPath, pngOptions);

        // Step 4: Confirm that the image has been created
        System.out.println("PNG created with 300 DPI at: " + pngPath);
    }
}
```

Η εκτέλεση αυτού του προγράμματος θα δημιουργήσει το `reports/report.png` στα 300 DPI, με τυχόν διαφανείς περιοχές να μετατρέπονται σε λευκό.

## Συχνές Ερωτήσεις & Προβλήματα

### 1. *Μπορώ να χρησιμοποιήσω διαφορετική τιμή DPI;*  
Απολύτως. Απλώς αντικαταστήστε το `300` με `150`, `600`, ή ό,τι απαιτεί η ροή εργασίας σας. Λάβετε υπόψη ότι υψηλότερο DPI αυξάνει την κατανάλωση μνήμης και τον χρόνο επεξεργασίας.

### 2. *Τι γίνεται αν το HTML μου αναφέρεται σε εξωτερικά CSS ή εικόνες;*  
Το Aspose.HTML επιλύει σχετικές URL βάσει της τοποθεσίας του αρχείου HTML. Βεβαιωθείτε ότι όλα τα assets είναι προσβάσιμα, ή ενσωματώστε τα με data URIs για να διατηρήσετε τη μετατροπή αυτόνομη.

### 3. *Πώς αλλάζω το χρώμα φόντου;*  
Αντικαταστήστε το `Color.getWhite()` με οποιαδήποτε άλλη στατική μέθοδο (`Color.getBlack()`, `Color.getRed()`) ή δημιουργήστε ένα προσαρμοσμένο χρώμα RGB: `new Color(255, 215, 0)` για χρυσό.

### 4. *Είναι πάντα το αποτέλεσμα PNG;*  
Μπορείτε να εξάγετε σε JPEG, BMP ή TIFF χρησιμοποιώντας την αντίστοιχη κλάση `*SaveOptions` (`JpegSaveOptions`, `BmpSaveOptions`, κλπ.). Το μοτίβο ορισμού DPI παραμένει το ίδιο.

## Συμβουλές για Παραγωγική Χρήση

- **Επεξεργασία παρτίδας:** Τοποθετήστε τη λογική μετατροπής μέσα σε βρόχο και δώστε του μια λίστα αρχείων HTML. Θυμηθείτε να επαναχρησιμοποιήσετε την ίδια παρουσία `PngSaveOptions` για να μειώσετε τη δημιουργία αντικειμένων.
- **Διαχείριση μνήμης:** Για πολύ μεγάλες σελίδες, σκεφτείτε να αυξήσετε τη μνήμη heap της JVM (`-Xmx2g`) ώστε να αποφύγετε `OutOfMemoryError`.
- **Ασφάλεια νήματος:** Η `Conversion.convert` είναι thread‑safe, έτσι μπορείτε να παραλληλοποιήσετε τις μετατροπές με `ExecutorService` για μεγαλύτερη απόδοση.

## Συμπέρασμα

Τώρα ξέρετε **πώς να ορίσετε DPI** όταν **μετατρέπετε HTML σε PNG**, πώς να **εξάγετε HTML ως PNG**, και πώς να **αντικαταστήσετε το διαφανές φόντο** με ένα στερεό χρώμα χρησιμοποιώντας το Aspose.HTML for Java. Το πλήρες, εκτελέσιμο παράδειγμα παραπάνω θα λειτουργήσει αμέσως—απλώς τοποθετήστε το αρχείο HTML σας στον φάκελο `reports` και εκτελέστε την κλάση.

Στη συνέχεια, ίσως θέλετε να εξερευνήσετε **την αποθήκευση HTML ως PNG** με διαφορετικές μορφές εικόνας, ή να ενσωματώσετε αυτή τη διαδικασία σε μια υπηρεσία web που δημιουργεί PDF κατ' απαίτηση. Σε κάθε περίπτωση, τα δομικά στοιχεία είναι τα ίδια: διαμορφώστε τις επιλογές αποθήκευσης, ορίστε το DPI, και αφήστε το Aspose να χειριστεί την απόδοση.

Καλό προγραμματισμό, και εύχομαι τα PNG σας να είναι πάντα καθαρά!

![Diagram showing DPI conversion flow – how to set DPI when converting HTML to PNG](/images/dpi-conversion-diagram.png){: .img-responsive alt="Διάγραμμα που δείχνει τη ροή μετατροπής DPI – πώς να ορίσετε DPI κατά τη μετατροπή HTML σε PNG"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}