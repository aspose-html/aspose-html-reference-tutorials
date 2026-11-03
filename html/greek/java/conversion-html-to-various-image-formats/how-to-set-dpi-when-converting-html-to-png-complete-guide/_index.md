---
category: general
date: 2026-01-03
description: Μάθετε πώς να ορίζετε το DPI κατά τη μετατροπή HTML σε PNG χρησιμοποιώντας
  το Aspose.HTML σε Java. Περιλαμβάνει συμβουλές για εξαγωγή HTML ως PNG και απόδοση
  HTML σε εικόνα.
draft: false
keywords:
- how to set dpi
- convert html to png
- export html as png
- render html to image
- save html as png
language: el
og_description: Μάθετε πώς να ορίζετε το DPI για τη μετατροπή HTML σε PNG. Αυτός ο
  οδηγός σας δείχνει πώς να μετατρέψετε HTML σε PNG, να εξάγετε HTML ως PNG και να
  αποδίδετε HTML σε εικόνα αποδοτικά.
og_title: Πώς να ορίσετε DPI κατά τη μετατροπή HTML σε PNG – Πλήρης οδηγός
tags:
- Aspose.HTML
- Java
- Image Processing
title: Πώς να ορίσετε DPI κατά τη μετατροπή HTML σε PNG – Πλήρης οδηγός
url: /el/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-html-to-png-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Ορίσετε DPI Κατά τη Μετατροπή HTML σε PNG – Πλήρης Οδηγός

Αν ψάχνετε για **πώς να ορίσετε DPI** κατά τη μετατροπή HTML σε PNG, βρίσκεστε στο σωστό μέρος. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια λύση Java που όχι μόνο σας δείχνει **πώς να ορίσετε DPI**, αλλά επίσης επιδεικνύει πώς να **μετατρέψετε HTML σε PNG**, **εξάγετε HTML ως PNG**, και **αποδώσετε HTML σε εικόνα** με το Aspose.HTML.

Έχετε προσπαθήσει ποτέ να εκτυπώσετε μια ιστοσελίδα και το αποτέλεσμα να φαίνεται θολό επειδή η ανάλυση είναι λανθασμένη; Αυτό συνήθως είναι πρόβλημα DPI. Μέχρι το τέλος αυτού του οδηγού θα καταλάβετε γιατί το DPI είναι σημαντικό, πώς να το ελέγξετε προγραμματιστικά, και πώς να αποκτήσετε ένα καθαρό PNG κάθε φορά. Χωρίς εξωτερικά εργαλεία, μόνο απλός κώδικας Java που μπορείτε να ενσωματώσετε στο πρότζεκτ σας σήμερα.

## Τι Θα Χρειαστείτε

- **Java 8+** (ο κώδικας λειτουργεί με οποιοδήποτε πρόσφατο JDK)
- **Aspose.HTML for Java** βιβλιοθήκη (η δωρεάν δοκιμή λειτουργεί για δοκιμές)
- Ένα **αρχείο HTML εισόδου** που θέλετε να αποδώσετε (π.χ., `input.html`)
- Λίγη περιέργεια για την ανάλυση εικόνας

Αυτό είναι όλο—χωρίς μαγικά Maven, χωρίς επιπλέον gems επεξεργασίας εικόνας. Αν έχετε ήδη το Aspose.HTML JAR στο classpath, είστε έτοιμοι να ξεκινήσετε.

## Βήμα 1: Φόρτωση του Εγγράφου HTML – Μετατροπή HTML σε PNG

Το πρώτο πράγμα που κάνετε όταν θέλετε να **μετατρέψετε HTML σε PNG** είναι να φορτώσετε το αρχείο πηγής σε ένα `HTMLDocument`. Σκεφτείτε το έγγραφο ως μια εικονική σελίδα περιηγητή που το Aspose θα ζωγραφίσει αργότερα σε bitmap.

```java
import com.aspose.html.HTMLDocument;

public class ExportHtmlToPng {

    public static void main(String[] args) throws Exception {
        // Step 1: Load the HTML document you want to render
        // Replace "YOUR_DIRECTORY/input.html" with the actual path to your file
        HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

> **Συμβουλή:** Αν το HTML σας αναφέρεται σε εξωτερικά CSS ή εικόνες, βεβαιωθείτε ότι οι διαδρομές είναι απόλυτες ή σχετικές με τον φάκελο που περνάτε. Διαφορετικά η μηχανή απόδοσης δεν θα τις βρει και το PNG θα χάσει το στυλ.

## Βήμα 2: Διαμόρφωση Επιλογών Εξαγωγής Εικόνας – Πώς να Ορίσετε DPI

Τώρα έρχεται η ουσία: **πώς να ορίσετε DPI** για την εικόνα εξόδου. Το DPI (dots per inch) ελέγχει πόσα pixel συμπιέζονται σε κάθε ίντσα του τελικού PNG. Ένα υψηλότερο DPI προσφέρει πιο οξεία εικόνα, ειδικά όταν την εκτυπώνετε ή την ενσωματώνετε σε έγγραφο υψηλής ανάλυσης.

```java
import com.aspose.html.rendering.ImageSaveOptions;
import com.aspose.html.rendering.ImageFormat;

// Step 2: Configure image export options (format, size, DPI)
ImageSaveOptions imageSaveOptions = new ImageSaveOptions();
imageSaveOptions.setFormat(ImageFormat.Png);   // Export as PNG
imageSaveOptions.setWidth(1920);               // Desired pixel width
imageSaveOptions.setHeight(1080);              // Desired pixel height
imageSaveOptions.setDpiX(300);                 // Horizontal DPI – this is how we set DPI
imageSaveOptions.setDpiY(300);                 // Vertical DPI – same for vertical axis
```

Γιατί ορίζουμε και τα `DpiX` και `DpiY`; Οι περισσότερες οθόνες χρησιμοποιούν τετράγωνα pixel, οπότε η ισότητα τους διατηρεί την αναλογία διαστάσεων. Αν χρειαστεί ποτέ να έχετε μη τετράγωνο πλέγμα pixel (σπάνιο, αλλά δυνατό για ορισμένους σαρωτές), μπορείτε να τα ρυθμίσετε ξεχωριστά.

> **Γιατί το DPI είναι σημαντικό:** Ένα PNG 1920 × 1080 σε 72 DPI φαίνεται εντάξει σε οθόνη, αλλά αν το εκτυπώσετε σε φωτογραφικό χαρτί 4 × 6 ίντσες η εικόνα θα εμφανιστεί pixelated. Ανεβάζοντας το DPI στα 300 κάθε ίντσα θα περιέχει 300 pixel, δίνοντάς σας καθαρή εκτύπωση.

## Βήμα 3: Αποθήκευση της Αποδοθείσας Σελίδας – Εξαγωγή HTML ως PNG

Με το έγγραφο φορτωμένο και το DPI ορισμένο, το τελευταίο βήμα είναι να **εξάγετε HTML ως PNG**. Η μέθοδος `save` κάνει όλη τη βαριά δουλειά: αποδίδει το DOM, εφαρμόζει CSS, ραστεροποιεί τη διάταξη, και γράφει το αρχείο PNG στο δίσκο.

```java
        // Step 3: Save the rendered page as a PNG image
        // Replace "YOUR_DIRECTORY/output.png" with the desired output path
        htmlDoc.save("YOUR_DIRECTORY/output.png", imageSaveOptions);
    }
}
```

Η εκτέλεση του προγράμματος δημιουργεί το `output.png` στον φάκελο που καθορίσατε. Ανοίξτε το με οποιονδήποτε προβολέα εικόνων—θα πρέπει να δείτε μια κρυστάλλινη αναπαράσταση της σελίδας HTML, αποδομένη στο DPI που ορίσατε προηγουμένως.

## Βήμα 4: Επαλήθευση του Αποτελέσματος – Απόδοση HTML σε Εικόνα

Μερικές φορές είναι χρήσιμο να ελέγξετε ξανά ότι η εικόνα πραγματικά περιέχει τα μεταδεδομένα DPI που ζητήσατε. Οι περισσότεροι επεξεργαστές εικόνας (π.χ., Photoshop, GIMP) εμφανίζουν το DPI στις ιδιότητες της εικόνας. Μπορείτε επίσης να το ελέγξετε προγραμματιστικά:

```java
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;

public class VerifyDpi {
    public static void main(String[] args) throws Exception {
        BufferedImage img = ImageIO.read(new File("YOUR_DIRECTORY/output.png"));
        // Most Java APIs don’t expose DPI directly, but you can infer it
        // by comparing pixel dimensions to the expected physical size.
        System.out.println("Width (px): " + img.getWidth());
        System.out.println("Height (px): " + img.getHeight());
    }
}
```

Αν γνωρίζετε ότι η εικόνα είναι 1920 × 1080 px και θέλατε 300 DPI, το φυσικό μέγεθος θα πρέπει να είναι περίπου 6.4 × 3.6 ίντσες (1920 / 300 ≈ 6.4). Αυτός ο έλεγχος σιγουριάζει ότι το βήμα **render HTML to image** τήρησε το DPI που ορίσατε.

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Θολό αποτέλεσμα** | Το DPI παραμένει στο προεπιλεγμένο 72 DPI ενώ οι διαστάσεις είναι μεγάλες. | Καλέστε ρητά `setDpiX` και `setDpiY` όπως φαίνεται στο Βήμα 2. |
| **Λείπει CSS** | Σχετικές διαδρομές στο HTML δείχνουν έξω από το `YOUR_DIRECTORY`. | Χρησιμοποιήστε απόλυτες URL ή αντιγράψτε τα assets στον ίδιο φάκελο. |
| **Σφάλματα μνήμης** | Η απόδοση μιας τεράστιας σελίδας σε υψηλό DPI καταναλώνει πολύ RAM. | Μειώστε `width`/`height` ή αυξήστε το heap της JVM (`-Xmx2g`). |
| **Λάθος χρωματικό προφίλ** | Το PNG αποθηκεύεται χωρίς ετικέτα sRGB και μπορεί να φαίνεται λανθασμένο σε ορισμένες οθόνες. | Το Aspose.HTML ενσωματώνει αυτόματα sRGB· διαφορετικά επεξεργαστείτε με εργαλείο. |

## Προχωρημένες Επιλογές – Περαιτέρω Βελτιστοποίηση Απόδοσης HTML σε Εικόνα

Αν χρειάζεστε περισσότερο έλεγχο από το βασικό DPI, το Aspose.HTML προσφέρει επιπλέον ρυθμίσεις:

```java
// Enable anti‑aliasing for smoother text
imageSaveOptions.setAntiAliasing(true);

// Set background color (transparent PNG by default)
imageSaveOptions.setBackgroundColor(java.awt.Color.WHITE);
```

Μπορείτε επίσης να αποδώσετε σε άλλες μορφές (JPEG, BMP) αλλάζοντας το `setFormat`. Η ίδια λογική DPI ισχύει, οπότε η γνώση **πώς να ορίσετε DPI** μεταφέρεται και σε αυτές τις μορφές.

## Πλήρες Παράδειγμα – Όλα τα Βήματα σε Ένα Αρχείο

Παρακάτω είναι η πλήρης, έτοιμη‑για‑εκτέλεση κλάση Java που ενσωματώνει όλα όσα συζητήσαμε. Απλώς αντικαταστήστε τις διαδρομές placeholder και τρέξτε την από το IDE ή τη γραμμή εντολών.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.ImageSaveOptions;
import com.aspose.html.rendering.ImageFormat;

public class ExportHtmlToPng {

    public static void main(String[] args) throws Exception {
        // Load the source HTML file
        HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/input.html");

        // Configure export options – this is where we set DPI
        ImageSaveOptions options = new ImageSaveOptions();
        options.setFormat(ImageFormat.Png);
        options.setWidth(1920);
        options.setHeight(1080);
        options.setDpiX(300);   // Horizontal DPI
        options.setDpiY(300);   // Vertical DPI
        options.setAntiAliasing(true);               // Optional: smoother rendering
        options.setBackgroundColor(java.awt.Color.WHITE); // Optional: solid background

        // Save the rendered image
        htmlDoc.save("YOUR_DIRECTORY/output.png", options);

        System.out.println("HTML successfully rendered to PNG with 300 DPI.");
    }
}
```

Τρέξτε το, ανοίξτε το `output.png`, και θα δείτε ένα υψηλής ανάλυσης στιγμιότυπο της σελίδας HTML—ακριβώς αυτό που θέλατε όταν ρωτήσατε **πώς να ορίσετε DPI** για εξαγωγή PNG.

![παράδειγμα ρύθμισης DPI](image.png)

*Κείμενο alt εικόνας: παράδειγμα ρύθμισης DPI – δείχνει ένα αποδομένο PNG στα 300 DPI.*

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για να μάθετε **πώς να ορίσετε DPI** όταν **μετατρέπετε HTML σε PNG** χρησιμοποιώντας το Aspose.HTML σε Java. Μάθατε πώς να φορτώσετε ένα έγγραφο HTML, να διαμορφώσετε το `ImageSaveOptions` με το επιθυμητό DPI, **να εξάγετε HTML ως PNG**, και να επαληθεύσετε ότι η αποδοθείσα εικόνα τηρεί την ανάλυση που καθορίσατε. Καθ' όλη τη διάρκεια, αγγίξαμε σχετικές θεματικές όπως **render HTML to image**, **save HTML as PNG**, και κοινά εμπόδια που μπορούν να πιάσουν ακόμη και έμπειρους προγραμματιστές.

Δοκιμάστε: αλλάξτε πλάτη, ύψη ή τιμές DPI· μεταβείτε σε JPEG για μικρότερα αρχεία· ή συνδυάστε πολλαπλές σελίδες για δημιουργία PDF slideshow. Οι έννοιες παραμένουν ίδιες—ελέγξτε το DPI, και ελέγχετε την ποιότητα.

Έχετε ερωτήσεις για ειδικές περιπτώσεις, όπως απόδοση σελίδων με βαριά JavaScript ή ενσωμάτωση γραμματοσειρών; Αφήστε ένα σχόλιο παρακάτω και θα εμβαθύνουμε μαζί. Καλή προγραμματιστική δουλειά και απολαύστε εκείνα τα καθαρά PNG!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}