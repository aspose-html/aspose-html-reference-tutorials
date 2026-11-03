---
category: general
date: 2026-04-11
description: Απόδοση HTML σε PNG σε Java γρήγορα προσομοιώνοντας μια κινητή συσκευή.
  Μάθετε πώς να ορίσετε το μέγεθος του viewport, να ορίσετε το user agent και να μετατρέψετε
  το HTML σε εικόνα με το Aspose.HTML.
draft: false
keywords:
- render html to png
- convert html to image
- emulate mobile device
- set viewport size
- set user agent
language: el
og_description: Απόδοση HTML σε PNG σε Java χρησιμοποιώντας το Aspose.HTML. Αυτός
  ο οδηγός δείχνει πώς να ορίσετε το μέγεθος του viewport, να ορίσετε το user agent
  και να μετατρέψετε το HTML σε εικόνα για δοκιμές σε κινητά.
og_title: Απόδοση HTML σε PNG σε Java – Εξομοίωση κινητής συσκευής
tags:
- Aspose.HTML
- Java
- HTML to Image
title: Απόδοση HTML σε PNG σε Java – Εξομοίωση κινητής συσκευής
url: /el/java/conversion-html-to-various-image-formats/render-html-to-png-in-java-emulate-mobile-device/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Απόδοση HTML σε PNG σε Java – Προσομοίωση Κινητής Συσκευής

Έχετε ποτέ χρειαστεί να **αποδώσετε HTML σε PNG** αλλά δεν ήξερες πώς να πετύχεις μια αληθινή εμφάνιση κινητής συσκευής; Δεν είστε ο μόνος. Σε πολλές δοκιμαστικές αλυσίδες πρέπει να δημιουργούμε στιγμιότυπο μιας σελίδας ακριβώς όπως θα εμφανιζόταν σε ένα τηλέφωνο, και η προγραμματιστική εκτέλεση εξοικονομεί ώρες χειροκίνητης δουλειάς.  

Σε αυτό το tutorial θα δείτε ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που **convert html to image** ενώ **emulate mobile device**, ρυθμίζει το **set viewport size**, και **set user agent** χρησιμοποιώντας το Aspose.HTML for Java. Χωρίς ελλείψεις, μόνο καθαρός κώδικας που μπορείτε να ενσωματώσετε στο πρόγραμμά σας σήμερα.

## Τι Θα Μάθετε

- Πώς να δημιουργήσετε ένα sandbox που μιμείται την οθόνη ενός iPhone.
- Γιατί η ρύθμιση του μεγέθους του viewport και της συμβολοσειράς user‑agent είναι σημαντική για ακριβή απόδοση.
- Οι ακριβείς κλάσεις και μέθοδοι Java που απαιτούνται για **render html to png**.
- Συμβουλές για τη διαχείριση ειδικών περιπτώσεων όπως ελλιπή αρχεία ή οθόνες υψηλής ανάλυσης (high‑DPI).
- Πώς φαίνεται το παραγόμενο PNG, ώστε να ξέρετε πότε έχετε επιτύχει.

### Προαπαιτούμενα

- Εγκατεστημένο Java 8 ή νεότερο.
- Maven ή Gradle για λήψη της βιβλιοθήκης Aspose.HTML for Java (η έκδοση 23.10 είναι η τρέχουσα από τον Απρίλιο 2026).
- Ένα απλό αρχείο HTML (`responsive.html`) που περιέχει responsive CSS (μπορείτε να αντιγράψετε οποιαδήποτε σελίδα θέλετε να δοκιμάσετε).

Αν τα έχετε αυτά, ας βουτήξουμε.

![Παράδειγμα Απόδοσης HTML σε PNG](render-html-to-png.png "Στιγμιότυπο της κινητής προβολής που δημιουργήθηκε από την απόδοση html σε png")

## Επισκόπηση Βήμα‑προς‑Βήμα – Απόδοση HTML σε PNG

Παρακάτω βρίσκεται το πλήρες αρχείο πηγαίου κώδικα που θα μεταγλωττίσετε. Περιέχει τα πάντα — από τις εισαγωγές μέχρι τη μέθοδο `main` — ώστε να μπορείτε να το αντιγράψετε‑και‑επικολλήσετε απευθείας στο IDE σας.

```java
// File: SandboxRendering.java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxRendering {
    public static void main(String[] args) throws Exception {

        // -------------------------------------------------
        // Step 1: Emulate a mobile device
        // -------------------------------------------------
        HtmlSandbox sandbox = new HtmlSandbox();
        // set viewport size – typical iPhone dimensions
        sandbox.setViewportWidth(375);   // width in CSS pixels
        sandbox.setViewportHeight(667);  // height in CSS pixels
        // high‑DPI screens need a device pixel ratio > 1
        sandbox.setDevicePixelRatio(2.0);
        // set user agent so the page thinks it's Safari on iOS
        sandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.0 Mobile/15E148 Safari/604.1");

        // -------------------------------------------------
        // Step 2: Load the HTML document inside the sandbox
        // -------------------------------------------------
        // Replace YOUR_DIRECTORY with the absolute or relative path to your HTML file
        HTMLDocument doc = new HTMLDocument("YOUR_DIRECTORY/responsive.html", sandbox);

        // -------------------------------------------------
        // Step 3: Define image conversion options
        // -------------------------------------------------
        ImageConversionOptions opts = new ImageConversionOptions();
        // match the viewport so the output image isn’t stretched
        opts.setWidth(375);
        opts.setHeight(667);
        // optional: set background color if your page has transparency
        // opts.setBackgroundColor(Color.WHITE);

        // -------------------------------------------------
        // Step 4: Render and save the PNG
        // -------------------------------------------------
        // The result is a PNG file that shows the mobile view.
        Converter.convert(doc, opts, "YOUR_DIRECTORY/mobile-view.png");

        System.out.println("✅ Rendering complete – check mobile-view.png");
    }
}
```

### Γιατί Λειτουργεί Αυτό

- **HtmlSandbox** απομονώνει το περιβάλλον απόδοσης, διασφαλίζοντας ότι η σελίδα δεν θα φορτώσει τα cookies ή τους αποθηκευμένους πόρους της επιφάνειας εργασίας σας.  
- **setViewportWidth/Height** λέει στη μηχανή τις λογικές διαστάσεις CSS, που είναι ο πυρήνας του **set viewport size**. Χωρίς αυτό, η σελίδα θα αποδοθεί στο προεπιλεγμένο μέγεθος επιφάνειας εργασίας.  
- **setDevicePixelRatio** κάνει την εικόνα καθαρή σε οθόνες τύπου Retina — σκεφτείτε το σαν να λέτε στον περιηγητή “προσομοίστε κάθε pixel CSS ως δύο φυσικά pixel”.  
- **setUserAgent** είναι το τελικό κομμάτι του παζλ **emulate mobile device**· πολλά responsive sites κρύβουν ή αναδιατάσσουν στοιχεία βάσει της συμβολοσειράς user‑agent.  

Μαζί, σας παρέχουν ένα πιστό στιγμιότυπο κινητής συσκευής που μπορείτε να **convert html to image** χωρίς καμία χειροκίνητη αλλαγή μεγέθους.

## Βήμα 1 – Προσομοίωση Κινητής Συσκευής

Όταν θέλετε να **emulate mobile device** συμπεριφορά, δύο πράγματα είναι τα πιο σημαντικά: οι διαστάσεις του viewport και η συμβολοσειρά user‑agent. Ο παραπάνω κώδικας χρησιμοποιεί μέγεθος τύπου iPhone 11 (375 × 667 CSS pixels) και user agent Safari‑on‑iOS. Αν χρειάζεστε δοκιμή Android, απλώς αντικαταστήστε τη συμβολοσειρά με ένα Chrome Android UA και προσαρμόστε τις διαστάσεις ανάλογα.

> **Pro tip:** Για Android tablets, αυξήστε το πλάτος σε 600‑800 CSS pixels και αυξήστε το device pixel ratio σε 1.5.

## Βήμα 2 – Φόρτωση HTML Εγγράφου με Sandbox

Ο κατασκευαστής `HTMLDocument` παίρνει τη διαδρομή του αρχείου HTML και το sandbox που διαμορφώσαμε. Εδώ ξεκινά πραγματικά η διαδικασία **convert html to image**. Αν το αρχείο δεν βρεθεί, το Aspose ρίχνει ένα `FileNotFoundException`. Για να κάνετε τον κώδικά σας πιο ανθεκτικό, μπορείτε να τυλίξετε την κλήση σε ένα μπλοκ try‑catch και να καταγράψετε ένα φιλικό μήνυμα.

```java
try {
    HTMLDocument doc = new HTMLDocument("YOUR_DIRECTORY/responsive.html", sandbox);
} catch (FileNotFoundException e) {
    System.err.println("❌ HTML file not found – check the path!");
    return;
}
```

## Βήμα 3 – Διαμόρφωση Επιλογών Μετατροπής Εικόνας

`ImageConversionOptions` σας επιτρέπει να ελέγξετε το τελικό μέγεθος PNG. Η αντιστοίχιση του **set viewport size** εδώ αποτρέπει παραμόρφωση. Μπορείτε επίσης να αλλάξετε τη μορφή εξόδου αντικαθιστώντας το `ImageConversionOptions` με `PdfConversionOptions` (αν χρειαστείτε ποτέ PDF αντί για PNG).

> **Το ήξερες;** Το Aspose.HTML υποστηρίζει JPEG, BMP, GIF, και ακόμη και WebP έτοιμο. Απλώς αλλάξτε την επέκταση του αρχείου στην κλήση `convert`.

## Βήμα 4 – Δημιουργία του Αρχείου PNG

Η μονογραμμή `Converter.convert(doc, opts, "output.png")` κάνει όλη τη βαριά δουλειά. Πίσω από τις σκηνές η βιβλιοθήκη αναλύει CSS, αποδίδει τη διάταξη, ραστεριάζει το αποτέλεσμα και γράφει το PNG. Όταν η μέθοδος επιστρέψει, έχετε ένα αρχείο που μπορείτε να ανοίξετε σε οποιονδήποτε προβολέα εικόνων.

**Αναμενόμενο αποτέλεσμα:** ένα PNG 375 × 667 που φαίνεται ακριβώς όπως η σελίδα σε iPhone. Στοιχεία που κρύβονταν στην επιφάνεια εργασίας (όπως τα hamburger μενού) θα πρέπει τώρα να είναι ορατά.

### Επαλήθευση του Αποτελέσματος

Ανοίξτε το `mobile-view.png` στον αγαπημένο σας επεξεργαστή εικόνων. Αν δείτε την πλοήγηση να έχει συμπτυχθεί σε εικονίδιο burger και τις γραμματοσειρές να είναι προσαρμοσμένες για τηλέφωνο, έχετε πετύχει. Αν όχι, ελέγξτε ξανά τη συμβολοσειρά **set user agent** — ορισμένες ιστοσελίδες βασίζονται σε επιπλέον κεφαλίδες όπως `Accept-Language`.

## Διαχείριση Συνηθισμένων Περιπτώσεων Άκρων

| Κατάσταση | Τι Να Κάνετε |
|-----------|------------|
| **HTML file contains external resources (CSS, JS) that are blocked** | Προσθέστε `sandbox.setAllowInternetAccess(true);` ώστε το sandbox να κατεβάσει τους πόρους. |
| **You need a higher‑resolution screenshot** | Αυξήστε το `sandbox.setDevicePixelRatio(3.0);` και προσαρμόστε το `opts.setWidth/Height` αναλογικά. |
| **Page uses lazy‑loaded images** | Μετά τη δημιουργία του `HTMLDocument`, καλέστε `doc.waitForComplete();` για να δώσετε στη σελίδα χρόνο να φορτώσει όλα τα στοιχεία. |
| **You want a transparent background** | Ορίστε `opts.setBackgroundColor(null);` – το PNG θα διατηρήσει το κανάλι άλφα. |

## Συνοπτικό Παράδειγμα Πλήρους Λειτουργίας

Ακολουθεί ολόκληρο το πρόγραμμα ξανά, αυτή τη φορά με τις προαιρετικές βελτιώσεις ανθεκτικότητας ενσωματωμένες:

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxRendering {
    public static void main(String[] args) throws Exception {

        // Emulate a mobile device
        HtmlSandbox sandbox = new HtmlSandbox();
        sandbox.setViewportWidth(375);
        sandbox.setViewportHeight(667);
        sandbox

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}