---
category: general
date: 2026-03-25
description: Πώς να χρησιμοποιήσετε το sandbox για να καταγράψετε στιγμιότυπο οθόνης
  ιστοσελίδας με το Aspose.HTML για Java. Μάθετε πώς να αποθηκεύετε HTML ως PNG, μετατροπή
  HTML σε εικόνα και μετατροπή HTML σε PNG σε λίγα λεπτά.
draft: false
keywords:
- how to use sandbox
- capture webpage screenshot
- save html as png
- html to image conversion
- html to png conversion
language: el
og_description: Πώς να χρησιμοποιήσετε το sandbox για να καταγράψετε στιγμιότυπο οθόνης
  μιας ιστοσελίδας. Αυτό το σεμινάριο δείχνει πώς να αποθηκεύσετε HTML ως PNG, καλύπτοντας
  τη μετατροπή HTML σε εικόνα και τη μετατροπή HTML σε PNG με το Aspose.HTML για Java.
og_title: Πώς να χρησιμοποιήσετε το Sandbox για λήψη στιγμιότυπου οθόνης ιστοσελίδας
tags:
- Aspose.HTML
- Java
- Web Automation
title: Πώς να χρησιμοποιήσετε το Sandbox για τη λήψη στιγμιότυπου οθόνης ιστοσελίδας
url: /el/java/conversion-html-to-various-image-formats/how-to-use-sandbox-to-capture-webpage-screenshot/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε το Sandbox για Λήψη Στιγμιότυπου Ιστοσελίδας

Η χρήση του sandbox για λήψη στιγμιότυπου ιστοσελίδας είναι μια συχνή απαίτηση όταν χρειάζεστε μια τέλεια προεπισκόπηση μιας ανταποκρινόμενης σελίδας. Σε αυτόν τον οδηγό θα σας δείξουμε επίσης πώς να **αποθηκεύσετε HTML ως PNG** χρησιμοποιώντας το Aspose.HTML for Java, καλύπτοντας τα πάντα από *html to image conversion* έως *html to png conversion* σε ένα ενιαίο, επαναλήψιμο παράδειγμα.

Φανταστείτε ότι δοκιμάζετε μια σελίδα προώθησης που φαίνεται διαφορετικά σε τηλέφωνο, tablet και επιτραπέζιο υπολογιστή. Αντί να ανοίξετε τρία προγράμματα περιήγησης, μπορείτε να δημιουργήσετε ένα sandbox, να το κατευθύνετε στη διεύθυνση URL και άμεσα να λάβετε ένα PNG που αντικατοπτρίζει ακριβώς αυτό που θα έδειχνε μια πραγματική συσκευή. Στο τέλος αυτού του tutorial θα έχετε ένα πλήρες, εκτελέσιμο πρόγραμμα Java που κάνει ακριβώς αυτό, μαζί με μια σειρά πρακτικών συμβουλών που μπορείτε να επαναχρησιμοποιήσετε στα δικά σας έργα.

## Τι Θα Χρειαστεί

- **Aspose.HTML for Java** (v23.9 ή νεότερη). Η βιβλιοθήκη είναι διαθέσιμη μέσω Maven Central, οπότε η προσθήκη της εξάρτησης είναι παιχνιδάκι.
- Ένα **JDK 11+** εγκατεστημένο στο σύστημά σας.
- Ένα IDE ή κειμενογράφο της επιλογής σας (IntelliJ IDEA, VS Code, Eclipse… όποιο προτιμάτε).
- Πρόσβαση στο Internet για τη διεύθυνση URL του παραδείγματος (`https://example.com/responsive.html`) ή αντικαταστήστε την με οποιαδήποτε σελίδα θέλετε να στιγμιότυπο.

Δεν απαιτούνται επιπλέον εγγενή binaries ή headless browsers — το sandbox λειτουργεί εξ ολοκλήρου στη μνήμη.

---

## Πώς να Χρησιμοποιήσετε το Sandbox – Βήμα 1: Ορισμός της Εικονικής Συσκευής

Το πρώτο που κάνετε είναι να πείτε στο sandbox ποιο μέγεθος οθόνης θέλετε να προσομοιώσετε. Εδώ ξεχωρίζει η κύρια λέξη‑κλειδί: *how to use sandbox* για συγκεκριμένο viewport.

```java
// Step 1: Create a DeviceInfo that describes the virtual screen
DeviceInfo sandboxDevice = new DeviceInfo();
sandboxDevice.setWidth(800);               // width in pixels
sandboxDevice.setHeight(600);              // height in pixels
sandboxDevice.setDevicePixelRatio(1.0);    // 1 × for standard displays
sandboxDevice.setUserAgent("AsposeHTML/Java Sandbox");
```

**Γιατί είναι σημαντικό:**  
Ο καθορισμός του πλάτους και του ύψους αναγκάζει τη μηχανή διάταξης να αντιμετωπίσει τη σελίδα σαν να εμφανιζόταν σε οθόνη 800×600. Το `devicePixelRatio` επηρεάζει το πώς συμπεριφέρονται τα CSS‑based media queries (`@media (min‑device‑pixel‑ratio: ...)`), εξασφαλίζοντας ότι το στιγμιότυπο ταιριάζει με την πραγματική εμπειρία.

> **Συμβουλή επαγγελματία:** Αν χρειάζεστε στιγμιότυπο υψηλής ανάλυσης (π.χ. Retina displays), αυξήστε το `devicePixelRatio` σε `2.0` και προσαρμόστε ανάλογα το πλάτος/ύψος.

---

## Λήψη Στιγμιότυπου Ιστοσελίδας – Βήμα 2: Φόρτωση της Σελίδας Μέσα στο Sandbox

Τώρα ζητάμε από το Aspose.HTML να κατεβάσει το απομακρυσμένο HTML και να το αποδώσει μέσα στο sandbox που ορίσαμε. Αυτό το βήμα είναι η καρδιά του **capture webpage screenshot**.

```java
// Step 2: Load the remote HTML page using the sandboxed environment
HTMLDocument document = new HTMLDocument(
        "https://example.com/responsive.html",
        new HTMLDocumentLoadOptions(new Sandbox(sandboxDevice)));
```

**Τι συμβαίνει στο παρασκήνιο;**  
Το `HTMLDocumentLoadOptions` λαμβάνει μια παρουσία `Sandbox` που περιέχει το `DeviceInfo` μας. Η βιβλιοθήκη δημιουργεί στη συνέχεια ένα headless rendering context που σέβεται το viewport, το user‑agent string και τυχόν JavaScript που μπορεί να εκτελέσει η σελίδα — *όλα χωρίς να εκκινήσει Chrome ή Firefox*.

Αν η σελίδα-στόχος απαιτεί έλεγχο ταυτότητας, μπορείτε να εισάγετε cookies ή προσαρμοσμένες κεφαλίδες μέσω του `HTMLDocumentLoadOptions`. Αυτό είναι χρήσιμο σε περιπτώσεις εσωτερικών δικτυακών πύλων.

---

## Αποθήκευση HTML ως PNG – Βήμα 3: Μετατροπή του Αποδοθέντος Εγγράφου σε Εικόνα

Με τη σελίδα αποδομένη, το τελευταίο κομμάτι είναι να **αποθηκεύσετε HTML ως PNG**. Αυτό είναι το πραγματικό βήμα *html to png conversion*.

```java
// Step 3: Convert the rendered document to PNG and write it to disk
try (FileOutputStream out = new FileOutputStream("output/responsive_page.png")) {
    Converter.convertDocument(
            document,
            new ConversionOptions(ConversionFormat.PNG),
            out);
}
```

Όταν ο `Converter` ολοκληρωθεί, θα βρείτε ένα αρχείο με όνομα `responsive_page.png` μέσα στο φάκελο `output`. Ανοίξτε το και θα δείτε ακριβώς πώς έδειχνε η σελίδα σε 800×600 pixels — χωρίς UI του προγράμματος περιήγησης, χωρίς scrollbars, μόνο η καθαρή απόδοση.

**Συνηθισμένα προβλήματα:**  
- **Σφάλματα δικαιωμάτων αρχείου:** Βεβαιωθείτε ότι ο φάκελος υπάρχει (`output/` στο παράδειγμα) και ότι η διαδικασία σας μπορεί να γράψει σε αυτόν.  
- **Μεγάλες σελίδες:** Πολύ υψηλές σελίδες μπορεί να παράγουν τεράστια αρχεία PNG· μπορείτε να περιορίσετε το ύψος στο `DeviceInfo` ή να περικόψετε μετά τη μετατροπή.  
- **Δυναμικό περιεχόμενο:** Αν η σελίδα φορτώνει δεδομένα μέσω AJAX μετά τη αρχική φόρτωση, ίσως χρειαστεί να προσθέσετε μια μικρή καθυστέρηση (`Thread.sleep(2000)`) πριν τη μετατροπή, ή να χρησιμοποιήσετε `HTMLDocumentLoadOptions.setWaitForResources(true)`.

---

### html to image conversion – Προηγμένες Επιλογές

Το Aspose.HTML προσφέρει αρκετές ρυθμίσεις για να βελτιώσετε την **html to image conversion**:

| Option | Description | When to use |
|--------|-------------|-------------|
| `ConversionOptions.setQuality(int)` | Ορίζει το επίπεδο συμπίεσης PNG (0‑100). | Μείωση μεγέθους αρχείου για web assets. |
| `ConversionOptions.setBackgroundColor(Color)` | Επιβάλλει χρώμα φόντου (η προεπιλογή είναι διαφανής). | Χρήσιμο όταν η σελίδα έχει διαφανή τμήματα. |
| `ConversionOptions.setPageSize(PageSize)` | Παρακάμπτει το μέγεθος sandbox για την έξοδο εικόνας. | Δημιουργία μικρογραφιών διαφορετικής ανάλυσης. |

Παρακάτω ένα σύντομο απόσπασμα που ορίζει λευκό φόντο και ποιότητα 90 %:

```java
ConversionOptions pngOptions = new ConversionOptions(ConversionFormat.PNG);
pngOptions.setBackgroundColor(java.awt.Color.WHITE);
pngOptions.setQuality(90);

try (FileOutputStream out = new FileOutputStream("output/white_bg_page.png")) {
    Converter.convertDocument(document, pngOptions, out);
}
```

---

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας τα παραπάνω, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα αρχείο `SandboxResponsiveExample.java` και να τρέξετε:

```java
import com.aspose.html.devices.DeviceInfo;
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.ConversionOptions;
import com.aspose.html.converters.ConversionFormat;
import com.aspose.html.render.HTMLDocument;
import com.aspose.html.render.HTMLDocumentLoadOptions;
import com.aspose.html.render.Sandbox;

import java.io.FileOutputStream;

public class SandboxResponsiveExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Define a sandbox with the desired viewport (800×600) and device pixel ratio
        DeviceInfo sandboxDevice = new DeviceInfo();
        sandboxDevice.setWidth(800);
        sandboxDevice.setHeight(600);
        sandboxDevice.setDevicePixelRatio(1.0);
        sandboxDevice.setUserAgent("AsposeHTML/Java Sandbox");

        // Step 2: Load the remote HTML page inside the sandboxed environment
        HTMLDocument document = new HTMLDocument(
                "https://example.com/responsive.html",
                new HTMLDocumentLoadOptions(new Sandbox(sandboxDevice)));

        // Step 3: Convert the document to PNG – the output reflects exactly how the page looks on the defined screen size
        try (FileOutputStream out = new FileOutputStream("output/responsive_page.png")) {
            Converter.convertDocument(
                    document,
                    new ConversionOptions(ConversionFormat.PNG),
                    out);
        }

        System.out.println("Screenshot saved to output/responsive_page.png");
    }
}
```

Η εκτέλεση του προγράμματος εκτυπώνει μια γραμμή επιβεβαίωσης και αποθηκεύει το PNG στον φάκελο `output`. Ανοίξτε το αρχείο και θα δείτε μια πιστή αναπαράσταση της απομακρυσμένης σελίδας στο ακριβές μέγεθος που ορίσατε.

---

## Συχνές Ερωτήσεις

**Q: Λειτουργεί αυτό με τοπικά αρχεία HTML;**  
A: Απόλυτα. Αντικαταστήστε τη διεύθυνση URL με ένα `file://` URI ή περάστε μια διαδρομή `java.io.File` στον κατασκευαστή του `HTMLDocument`.

**Q: Τι γίνεται αν χρειάζομαι PDF αντί για PNG;**  
A: Αντικαταστήστε το `ConversionFormat.PNG` με `ConversionFormat.PDF`. Το υπόλοιπο του κώδικα παραμένει το ίδιο.

**Q: Μπορώ να κάνω λήψη πλήρους σελίδας (scrolling) ως στιγμιότυπο;**  
A: Ορίστε το ύψος του `DeviceInfo` στο scroll height της σελίδας (`document.getDocumentElement().getScrollHeight()`) πριν τη μετατροπή, ή χρησιμοποιήστε `ConversionOptions.setPageSize` για να μεγαλώσετε τον καμβά.

---

## Συμπέρασμα

Τώρα ξέρετε **πώς να χρησιμοποιήσετε το sandbox** για λήψη στιγμιότυπου ιστοσελίδας, αποθήκευση HTML ως PNG και αξιόπιστη μετατροπή html σε εικόνα με το Aspose.HTML for Java. Η προσέγγιση είναι ελαφριά, πλήρως προγραμματιζόμενη και παρακάμπτει το βάρος των παραδοσιακών headless browsers.

Τι έπεται; Δοκιμάστε να αλλάξετε την έξοδο PNG σε PDF, πειραματιστείτε με διαφορετικά device pixel ratios για να μιμηθείτε Retina displays, ή αυτοματοποιήστε την επεξεργασία δεκάδων URLs. Η ίδια τεχνική sandbox μπορεί επίσης να επαναχρησιμοποιηθεί για **html to png conversion** σε CI pipelines, visual regression testing, ή δημιουργία μικρογραφιών για σύστημα διαχείρισης περιεχομένου.

Μη διστάσετε να αφήσετε ένα σχόλιο αν αντιμετωπίσετε δυσκολίες, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}