---
category: general
date: 2026-03-15
description: Πώς να ορίσετε DPI για PNG υψηλής ανάλυσης κατά τη μετατροπή HTML σε
  PNG χρησιμοποιώντας το Aspose.HTML. Μάθετε πώς να μετατρέπετε HTML σε PNG γρήγορα
  και αξιόπιστα.
draft: false
keywords:
- how to set dpi
- convert html to png
- how to convert html
- how to generate png
- export html as png
language: el
og_description: Πώς να ορίσετε το DPI για PNG υψηλής ανάλυσης κατά τη μετατροπή HTML
  σε PNG. Ακολουθήστε αυτόν τον οδηγό βήμα‑προς‑βήμα για να εξάγετε HTML ως PNG με
  το Aspose.HTML.
og_title: Πώς να ορίσετε DPI κατά τη μετατροπή HTML σε PNG – Οδηγός Java
tags:
- Aspose.HTML
- Java
- Image Conversion
title: Πώς να ορίσετε DPI κατά τη μετατροπή HTML σε PNG – Οδηγός Java
url: /el/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-html-to-png-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ορίσετε DPI κατά τη μετατροπή HTML σε PNG – Οδηγός Java

Η ρύθμιση DPI είναι συχνά το χαμένο κομμάτι όταν χρειάζεστε ένα εξαιρετικά καθαρό PNG από μια σελίδα HTML. Αντιμετωπίζετε δυσκολία να πάρετε μια θολή λήψη οθόνης; Η απάντηση είναι συνήθως τόσο απλή όσο η προσαρμογή των ρυθμίσεων DPI πριν την εξαγωγή. Σε αυτόν τον οδηγό θα μάθετε **πώς να ορίσετε DPI**, **να μετατρέψετε HTML σε PNG**, και ακόμη θα εξερευνήσετε μερικές παραλλαγές όπως **πώς να δημιουργήσετε αρχεία PNG** για αναφορές ή τεκμηρίωση.  

Θα περάσουμε από όλα όσα χρειάζεστε: την απαιτούμενη εξάρτηση Maven, μια πλήρη, εκτελέσιμη κλάση Java, και τη λογική πίσω από κάθε γραμμή κώδικα. Στο τέλος θα μπορείτε να **εξάγετε HTML ως PNG** με κρυστάλλινη ανάλυση, είτε χτίζετε μια υπηρεσία μικρογραφιών είτε μια γραμμή επεξεργασίας παρτίδας.

## Προαπαιτούμενα

- Java 8 ή νεότερη εγκατεστημένη (το API λειτουργεί επίσης με Java 11+)  
- Maven ή Gradle για λήψη της βιβλιοθήκης Aspose.HTML for Java  
- Ένα τοπικό αρχείο HTML που θέλετε να μετατρέψετε σε εικόνα (π.χ., `diagram.html`)  

Δεν απαιτούνται πρόσθετες εγγενείς βιβλιοθήκες· το Aspose.HTML διαχειρίζεται τα πάντα εσωτερικά.

---

## Βήμα 1: Προσθήκη εξάρτησης Aspose.HTML

Πρώτα, ενημερώστε το Maven (ή Gradle) από πού να κατεβάσει το JAR του Aspose.HTML. Αυτή η βιβλιοθήκη παρέχει την κλάση `Converter` που θα χρησιμοποιήσουμε αργότερα.

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.11</version> <!-- latest as of March 2026 -->
</dependency>
```

Αν προτιμάτε Gradle, η ισοδύναμη γραμμή είναι:

```gradle
implementation 'com.aspose:aspose-html:24.11'
```

> **Συμβουλή:** Παρακολουθείτε τον αριθμό έκδοσης· οι νεότερες εκδόσεις συχνά προσθέτουν βελτιώσεις απόδοσης για απόδοση υψηλού DPI.

---

## Βήμα 2: Δημιουργία σκελετού κλάσης Java

Τώρα ας δημιουργήσουμε μια καθαρή, αυτόνομη κλάση με όνομα `HtmlToPng`. Αυτή θα περιέχει τη λογική μετατροπής μας.

```java
import com.aspose.html.converters.*;
import com.aspose.html.converters.image.*;

public class HtmlToPng {
    public static void main(String[] args) throws Exception {
        // We'll fill this in next
    }
}
```

Σε αυτό το σημείο το αρχείο μεταγλωττίζεται, αλλά δεν κάνει τίποτα ακόμη. Το επόμενο βήμα είναι όπου συμβαίνει η μαγεία του **πώς να ορίσετε DPI**.

---

## Βήμα 3: Διαμόρφωση ImageConversionOptions (Ο πυρήνας του πώς να ορίσετε DPI)

Το αντικείμενο `ImageConversionOptions` σας επιτρέπει να καθορίσετε την επιθυμητή ανάλυση. Από προεπιλογή, το Aspose.HTML χρησιμοποιεί 96 DPI, που είναι εντάξει για εικόνες μεγέθους οθόνης αλλά όχι για PNG έτοιμα για εκτύπωση. Ορίζοντας και τα `DpiX` και `DpiY` στα 300 DPI παράγει έξοδο υψηλής ποιότητας.

```java
// Step 3: Create image conversion options and configure DPI for high‑resolution output
ImageConversionOptions conversionOptions = new ImageConversionOptions();
conversionOptions.setDpiX(300);   // Horizontal DPI
conversionOptions.setDpiY(300);   // Vertical DPI
```

Γιατί 300 DPI; Είναι το de‑facto πρότυπο για εκτυπώσιμα γραφικά. Αν χρειάζεστε κάτι ακόμη πιο οξύ (π.χ., 600 DPI για επαγγελματική εκτύπωση), απλώς αλλάξτε τους αριθμούς· το Aspose.HTML θα διαχειριστεί την κλιμάκωση για εσάς.

---

## Βήμα 4: Εκτέλεση της μετατροπής – Πώς να μετατρέψετε HTML σε PNG

Με τις επιλογές έτοιμες, η πραγματική μετατροπή είναι μια εντολή μίας γραμμής. Απλώς περνάτε τη διαδρομή του πηγαίου HTML, τη διαδρομή του προορισμού PNG, και το `conversionOptions` που μόλις δημιουργήσαμε.

```java
// Step 4: Convert the HTML file to a PNG image using the configured options
Converter.convert(
        "YOUR_DIRECTORY/diagram.html",   // source HTML
        "YOUR_DIRECTORY/diagram.png",    // output PNG
        conversionOptions                // DPI‑aware options
);
```

Αυτό είναι! Όταν το πρόγραμμα ολοκληρωθεί, θα βρείτε το `diagram.png` δίπλα στο αρχείο HTML, αποδομένο σε 300 DPI.  

> **Συχνή ερώτηση:** *Τι γίνεται αν το HTML μου αναφέρει εξωτερικά CSS ή εικόνες;*  
> Το Aspose.HTML ακολουθεί σχετικές διαδρομές, οπότε εφόσον οι πόροι βρίσκονται στην ίδια ιεραρχία φακέλων, θα φορτωθούν αυτόματα. Αν χρειάζεται να φορτώσετε από το διαδίκτυο, βεβαιωθείτε ότι η μηχανή έχει πρόσβαση στο internet.

---

## Βήμα 5: Πλήρες λειτουργικό παράδειγμα

Συνδυάζοντας όλα, εδώ είναι η πλήρης, έτοιμη προς εκτέλεση κλάση. Αντικαταστήστε το `YOUR_DIRECTORY` με τον πραγματικό φάκελο στο μηχάνημά σας.

```java
import com.aspose.html.converters.*;
import com.aspose.html.converters.image.*;

public class HtmlToPng {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create conversion options and set DPI – this is the heart of how to set DPI
        ImageConversionOptions conversionOptions = new ImageConversionOptions();
        conversionOptions.setDpiX(300);
        conversionOptions.setDpiY(300);

        // 2️⃣ Convert the HTML file to PNG – the simplest way to convert HTML to PNG with Aspose.HTML
        Converter.convert(
                "C:/projects/sample/diagram.html",   // source file
                "C:/projects/sample/diagram.png",    // output file
                conversionOptions                     // DPI settings
        );

        System.out.println("✅ Conversion complete! PNG saved at C:/projects/sample/diagram.png");
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Η εκτέλεση του προγράμματος θα πρέπει να παράγει ένα PNG που:

- Ταιριάζει ακριβώς με τη οπτική διάταξη του `diagram.html`  
- Έχει ανάλυση 300 DPI (μπορείτε να το επαληθεύσετε σε οποιονδήποτε προβολέα εικόνας στις ιδιότητές του)  
- Είναι κατάλληλο για εκτύπωση, PDF ή οποιοδήποτε σενάριο όπου **πώς να δημιουργήσετε PNG** έχει σημασία  

Αν ανοίξετε το PNG σε έναν επεξεργαστή και μεγεθύνετε στο 100 %, θα δείτε καθαρό κείμενο και οξείς γραμμές—χωρίς εικονοστοιχεία.

---

## Βήμα 6: Παραλλαγές & Ακραίες Περιπτώσεις

### 6.1 Διαφορετικές τιμές DPI

Αν χρειάζεστε μικρογραφία αντί για εικόνα έτοιμη για εκτύπωση, μειώστε το DPI:

```java
conversionOptions.setDpiX(72);
conversionOptions.setDpiY(72);
```

### 6.2 Αλλαγή μορφής εικόνας

Το Aspose.HTML μπορεί επίσης να εξάγει JPEG, BMP ή TIFF. Απλώς αλλάξτε την επέκταση αρχείου στην κλήση `convert`:

```java
Converter.convert("diagram.html", "diagram.tiff", conversionOptions);
```

### 6.3 Μετατροπή πολλαπλών αρχείων σε βρόχο

Όταν έχετε μια παρτίδα HTML αναφορών:

```java
String[] files = {"report1.html", "report2.html", "report3.html"};
for (String html : files) {
    String png = html.replace(".html", ".png");
    Converter.convert(html, png, conversionOptions);
}
```

### 6.4 Διαχείριση μεγάλων εγγράφων

Για πολύ μεγάλες σελίδες HTML, μπορεί να αντιμετωπίσετε περιορισμούς μνήμης. Σε αυτήν την περίπτωση, ενεργοποιήστε τη ροή:

```java
conversionOptions.setRenderOnDemand(true);
```

Αυτό λέει στο Aspose.HTML να αποδίδει τμήματα σελίδας κατά απαίτηση, μειώνοντας το αποτύπωμα μνήμης.

---

## Συχνές Ερωτήσεις

**Ε: Λειτουργεί αυτό σε Linux/macOS;**  
Α: Απόλυτα. Η βιβλιοθήκη είναι καθαρή Java, οπότε οποιοδήποτε OS με συμβατό JRE θα το εκτελέσει.

**Ε: Τι γίνεται αν το HTML μου περιέχει JavaScript;**  
Α: Το Aspose.HTML εκτελεί τα περισσότερα client‑side scripts κατά τη διάρκεια της απόδοσης, αλλά ορισμένα προηγμένα API προγράμματος περιήγησης (όπως το WebGL) δεν υποστηρίζονται. Για τυπικά διαγράμματα ή δυναμικούς πίνακες, είστε εντάξει.

**Ε: Μπορώ να ορίσω προσαρμοσμένο χρώμα φόντου;**  
Α: Ναι—προσθέστε `conversionOptions.setBackgroundColor(Color.WHITE);` πριν από τη μετατροπή.

---

## Συμπέρασμα

Τώρα ξέρετε **πώς να ορίσετε DPI** όταν **μετατρέπετε HTML σε PNG**, και έχετε δει αρκετούς τρόπους **πώς να δημιουργήσετε PNG** αρχεία για διαφορετικές περιπτώσεις χρήσης. Το παραπάνω απόσπασμα είναι μια πλήρης, εκτελέσιμη λύση που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Java.  

Από εδώ μπορείτε να εξερευνήσετε **εξαγωγή HTML ως PNG** για αυτοματοποιημένη δημιουργία αναφορών, ή να συνδυάσετε αυτό με μια βιβλιοθήκη PDF για ενσωμάτωση εικόνων υψηλής ανάλυσης απευθείας σε έγγραφα. Ο ουρανός είναι το όριο—απλώς θυμηθείτε να προσαρμόσετε το DPI ώστε να ταιριάζει με το μέσο εξόδου.  

Αν βρήκατε αυτόν τον οδηγό χρήσιμο, δώστε του αστέρι στο GitHub, μοιραστείτε τον με συναδέλφους, ή δοκιμάστε να τροποποιήσετε τις τιμές DPI για να δείτε πώς επηρεάζουν την ποιότητα εκτύπωσης. Καλό προγραμματισμό!  

![how to set dpi example](example.png){alt="παράδειγμα ρύθμισης dpi"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}