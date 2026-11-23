---
category: general
date: 2026-03-14
description: Μάθετε πώς να ορίσετε το device pixel ratio σε Java και να αποθηκεύσετε
  μια ιστοσελίδα ως PNG χρησιμοποιώντας το Aspose.HTML – ένας πλήρης οδηγός μετατροπής
  HTML σε PNG.
draft: false
keywords:
- set device pixel ratio
- save webpage as png
- how to render png
- html to png conversion
- java html to image
language: el
og_description: Μάθετε πώς να ορίσετε το λόγο εικονοστοιχείων συσκευής σε Java και
  να αποθηκεύσετε μια ιστοσελίδα ως PNG με το Aspose.HTML, καλύπτοντας τη μετατροπή
  από HTML σε PNG βήμα προς βήμα.
og_title: Ορισμός αναλογίας εικονοστοιχείων συσκευής σε Java – Απόδοση HTML σε PNG
tags:
- java
- aspose-html
- image-rendering
title: Ορισμός του λόγου εικονοστοιχείων της συσκευής σε Java – Απόδοση HTML σε PNG
url: /el/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-render-html-to-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ορισμός device pixel ratio σε Java – Render HTML σε PNG

Έχετε ποτέ χρειαστεί να **ορίσετε device pixel ratio** ενώ δημιουργείτε ένα στιγμιότυπο οθόνης μιας ιστοσελίδας σε Java; Ίσως να δημιουργείτε μια υπηρεσία προεπισκόπησης για κινητές συσκευές, ή απλώς θέλετε μια καθαρή μικρογραφία που να φαίνεται σωστά σε οθόνη Retina. Ό,τι και να είναι, βρίσκεστε στο σωστό μέρος. Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία **html to png conversion**, και θα δείτε ακριβώς πώς να **save webpage as png** χρησιμοποιώντας τη βιβλιοθήκη Aspose.HTML.

Θα καλύψουμε τα πάντα, από τη διαμόρφωση ενός sandbox που προσομοιώνει το viewport ενός iPhone, μέχρι τη φόρτωση μιας απομακρυσμένης HTML σελίδας, και τέλος τη γραφή του αποτελέσματος στο δίσκο. Στο τέλος θα γνωρίζετε **how to render png** αρχεία προγραμματιστικά, και θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε Java project που χρειάζεται δυνατότητες **java html to image**.

## Τι Θα Χρειαστείτε

- **Java Development Kit (JDK) 8 ή νεότερο** – η βιβλιοθήκη λειτουργεί με οποιοδήποτε πρόσφατο JDK.
- **Aspose.HTML for Java** – μπορείτε να κατεβάσετε το τελευταίο JAR από το αποθετήριο Aspose Maven ή να κατεβάσετε το zip από την επίσημη ιστοσελίδα.
- Ένα **IDE** (IntelliJ IDEA, Eclipse, ή ακόμη και VS Code) – οτιδήποτε σας επιτρέπει να μεταγλωττίσετε και να εκτελέσετε Java.
- Σύνδεση στο διαδίκτυο αν σκοπεύετε να φορτώσετε μια ζωντανή URL (το παράδειγμα χρησιμοποιεί `https://example.com/mobile.html`).

Αυτό είναι όλο. Δεν απαιτούνται επιπλέον εργαλεία κατασκευής ή εγγενή δυαδικά αρχεία.

## Βήμα 1: Διαμόρφωση του Sandbox και ορισμός device pixel ratio

Η πρώτη ενέργεια που πρέπει να κάνετε είναι να δημιουργήσετε ένα **Sandbox** που προσποιείται ότι είναι μια κινητή συσκευή. Εδώ είναι που πραγματικά **ορίζετε device pixel ratio** ώστε να ταιριάζει με μια οθόνη υψηλής πυκνότητας (π.χ., η 2× retina οθόνη του iPhone).

```java
import com.aspose.html.rendering.SandboxOptions;

// Create sandbox options
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixel width of iPhone 6/7/8
sandboxOptions.setScreenHeight(667);         // CSS pixel height
sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
sandboxOptions.setUserAgent(
    "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
    "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0 Mobile/15E148 Safari/604.1");

// Build the sandbox
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

**Γιατί είναι σημαντικό:** Το `devicePixelRatio` λέει στη μηχανή απόδοσης πόσα φυσικά pixel αντιστοιχούν σε ένα CSS pixel. Χωρίς να το ορίσετε, η εικόνα εξόδου θα φαίνεται θολή σε οθόνες υψηλής DPI. Ορίζοντάς το ρητά, εξασφαλίζετε ότι το παραγόμενο PNG έχει την κατάλληλη λεπτομέρεια.

> **Συμβουλή:** Αν στοχεύετε σε συσκευές Android, μπορείτε να χρησιμοποιήσετε `3.0` για συσκευές με κλιμάκωση 3×. Προσαρμόστε το πλάτος/ύψος αναλόγως.

## Βήμα 2: Φόρτωση της HTML σελίδας για μετατροπή html σε png

Τώρα που το sandbox είναι έτοιμο, μπορούμε να φορτώσουμε τη σελίδα που θέλουμε να καταγράψουμε. Η κλάση `HTMLDocument` του Aspose.HTML δέχεται μια URL και ένα αντικείμενο sandbox, έτσι ώστε η σελίδα να αποδίδεται ακριβώς όπως θα έκανε στη προσομοιωμένη συσκευή.

```java
import com.aspose.html.HTMLDocument;

// Load the remote page inside the sandbox
HTMLDocument document = new HTMLDocument(
    "https://example.com/mobile.html", // Replace with your own URL
    mobileSandbox);
```

**Τι συμβαίνει στο παρασκήνιο;** Η βιβλιοθήκη φέρνει το HTML, αναλύει το CSS, εκτελεί τυχόν JavaScript (αν είναι ενεργοποιημένο), και διατάσσει τη σελίδα χρησιμοποιώντας τις διαστάσεις του viewport που ορίσατε νωρίτερα. Αυτό το βήμα είναι ο πυρήνας της μετατροπής **java html to image** επειδή σας παρέχει ένα πλήρως αποδομένο DOM έτοιμο για rasterization.

> **Ακραία περίπτωση:** Αν η σελίδα εξαρτάται από εξωτερικές γραμματοσειρές, βεβαιωθείτε ότι είναι προσβάσιμες από το μηχάνημα που εκτελεί τον κώδικα. Διαφορετικά το κείμενο μπορεί να επιστρέψει σε προεπιλεγμένη γραμματοσειρά, αλλάζοντας το οπτικό αποτέλεσμα.

## Βήμα 3: Αποθήκευση της ιστοσελίδας ως PNG – πώς να render png με Aspose.HTML

Με το έγγραφο αποδομένο, το τελευταίο κομμάτι είναι να γράψετε πραγματικά ένα αρχείο PNG στο δίσκο. Η κλάση `PngSaveOptions` σας επιτρέπει να ρυθμίσετε το επίπεδο συμπίεσης και άλλες ρυθμίσεις ειδικές για PNG, αλλά οι προεπιλογές λειτουργούν τέλεια για τις περισσότερες περιπτώσεις.

```java
import com.aspose.html.saving.PngSaveOptions;

// Define PNG options (optional)
PngSaveOptions pngOptions = new PngSaveOptions();
// You could adjust pngOptions.setCompressionLevel(9); for maximum compression

// Save the rendered page as a PNG image
document.save("output/mobile_view.png", pngOptions);

System.out.println("Mobile view rendered and saved as PNG.");
```

Όταν εκτελέσετε το πρόγραμμα, θα έχετε το `mobile_view.png` στον φάκελο `output`. Ανοίξτε το, και θα δείτε ένα ακριβές στιγμιότυπο της απομακρυσμένης σελίδας, αποδομένο στην υψηλής πυκνότητας ανάλυση που καθορίσατε μέσω του **set device pixel ratio**.

### Γρήγορη επαλήθευση

```text
$ java -jar MobileRenderTutorial.jar
Mobile view rendered and saved as PNG.
$ ls output
mobile_view.png
```

Ανοίξτε την εικόνα με οποιονδήποτε προβολέα· το κείμενο πρέπει να είναι καθαρό, τα εικονίδια ευκρινή, και η διάταξη ίδια με αυτή που θα δείτε σε πραγματικό iPhone.

## Προαιρετικό: Προσαρμογή του Pipeline Απόδοσης

### Αλλαγή του DPI δυναμικά

Αν χρειάζεται να δημιουργήσετε εικόνες για πολλαπλές πυκνότητες οθόνης, τυλίξτε τη δημιουργία του sandbox σε μια μέθοδο:

```java
private static Sandbox createSandbox(double dpr) {
    SandboxOptions opts = new SandboxOptions();
    opts.setScreenWidth(375);
    opts.setScreenHeight(667);
    opts.setDevicePixelRatio(dpr); // Pass 1.0, 2.0, 3.0, etc.
    opts.setUserAgent("...");
    return new Sandbox(opts);
}
```

Στη συνέχεια καλέστε `createSandbox(3.0)` για μια συσκευή 3×. Αυτή η ευελιξία είναι χρήσιμη όταν δημιουργείτε μια υπηρεσία που επιστρέφει μικρογραφίες για iPhone, iPad και Android tablets ταυτόχρονα.

### Απόδοση χωρίς JavaScript

Αν η σελίδα που καταγράφετε περιέχει βαριά scripts που δεν χρειάζεστε, μπορείτε να απενεργοποιήσετε το JavaScript για μια ταχύτερη **html to png conversion**:

```java
sandboxOptions.setJavaScriptEnabled(false);
```

Η απενεργοποίηση των scripts μπορεί να μειώσει τον χρόνο απόδοσης στο μισό, αλλά να έχετε υπόψη ότι κάποιο δυναμικό περιεχόμενο μπορεί να εξαφανιστεί.

## Συνηθισμένα Πιθανά Προβλήματα και Πώς να τα Αποφύγετε

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|-------|----------------|-----|
| **Θολή έξοδος** | `devicePixelRatio` έμεινε στην προεπιλογή (1.0) | Ορίστε ρητά **device pixel ratio** σε 2.0 ή υψηλότερο |
| **Λείπουν γραμματοσειρές** | Απομακρυσμένες γραμματοσειρές μπλοκαρισμένες από το firewall | Βεβαιωθείτε ότι το μηχάνημα έχει πρόσβαση στο διαδίκτυο ή ενσωματώστε τις γραμματοσειρές τοπικά |
| **Σφάλματα έλλειψης μνήμης** | Απόδοση πολύ μεγάλων σελίδων σε υψηλό DPI | Περιορίστε το μέγεθος του viewport ή μειώστε το `devicePixelRatio` |
| **Λανθασμένη URL** | Χρήση σχετικής διαδρομής χωρίς βασική URL | Παρέχετε πλήρη απόλυτη URL ή ορίστε `document.setBaseUrl()` |

Η αντιμετώπιση αυτών νωρίς σας εξοικονομεί απογοητευτικές συνεδρίες εντοπισμού σφαλμάτων αργότερα.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα Java. Αντιγράψτε‑και‑επικολλήστε το σε ένα αρχείο με όνομα `MobileRenderTutorial.java`, προσθέστε το JAR του Aspose.HTML στο classpath σας, και εκτελέστε το.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.Sandbox;
import com.aspose.html.rendering.SandboxOptions;
import com.aspose.html.saving.PngSaveOptions;

public class MobileRenderTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox that mimics a mobile device viewport
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS pixel width
        sandboxOptions.setScreenHeight(667);         // CSS pixel height
        sandboxOptions.setDevicePixelRatio(2.0);     // High‑density screen (set device pixel ratio)
        sandboxOptions.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0 Mobile/15E148 Safari/604.1");

        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // Step 2: Load the HTML page inside the sandbox
        HTMLDocument document = new HTMLDocument(
            "https://example.com/mobile.html", // Replace with your own URL
            mobileSandbox);

        // Step 3: Render the page to a PNG image
        PngSaveOptions pngOptions = new PngSaveOptions();
        document.save("output/mobile_view.png", pngOptions);

        System.out.println("Mobile view rendered.");
    }
}
```

> **Αποτέλεσμα:** Το πρόγραμμα δημιουργεί το `output/mobile_view.png`, ένα στιγμιότυπο υψηλής ανάλυσης που σέβεται το **set device pixel ratio** που ορίσατε.

## Οπτική Επιβεβαίωση

<img src="output/mobile_view.png" alt="παράδειγμα screenshot ορισμού device pixel ratio" width="400"/>

Η παραπάνω εικόνα (placeholder) δείχνει το τελικό PNG μετά τη διαδικασία απόδοσης. Παρατηρήστε το καθαρό κείμενο και τα σωστά κλιμακωμένα στοιχεία UI—ακριβώς αυτό που περιμένετε όταν **ορίζετε device pixel ratio** σωστά.

## Συμπέρασμα

Τώρα έχετε μια σταθερή κατανόηση του πώς να **set device pixel ratio** σε Java, να εκτελέσετε μια **html to png conversion**, και να **save webpage as png** χρησιμοποιώντας το Aspose.HTML. Αυτό καλύπτει τη βασική ροή εργασίας “πώς να render png” και σας παρέχει ένα επαναχρησιμοποιήσιμο πρότυπο για οποιαδήποτε εργασία **java html to image** μπορεί να συναντήσετε.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να αλλάξετε το URL με μια δυναμική σελίδα, πειραματιστείτε με διαφορετικές τιμές `devicePixelRatio`, ή ενσωματώστε αυτό το snippet σε ένα endpoint Spring Boot που επιστρέφει PNG κατά απαίτηση. Ο ουρανός είναι το όριο, και με τα θεμέλια σταθερά, θα βρείτε εύκολο να επεκτείνετε αυτή τη λύση.

Καλό κώδικα, και μη διστάσετε να αφήσετε ένα σχόλιο

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}