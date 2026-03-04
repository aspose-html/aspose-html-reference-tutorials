---
category: general
date: 2026-03-04
description: Ορίστε την αναλογία εικονοστοιχείων της συσκευής σε Java για να αποδώσετε
  μια κινητή προβολή του HTML σας. Μάθετε πώς να μετατρέψετε το HTML σε κινητό, να
  δοκιμάσετε το προσαρμοστικό HTML και να αποθηκεύσετε εύκολα το αποδομένο αρχείο
  HTML.
draft: false
keywords:
- set device pixel ratio
- convert html to mobile
- test responsive html
- save rendered html file
- render html file java
language: el
og_description: Ορίστε την αναλογία εικονοστοιχείων της συσκευής σε Java για να αποδώσετε
  μια κινητή προβολή του HTML σας. Αυτός ο οδηγός δείχνει πώς να μετατρέψετε το HTML
  σε κινητό, να δοκιμάσετε το ανταποκρινόμενο HTML και να αποθηκεύσετε το αρχείο HTML
  που αποδόθηκε.
og_title: Ορισμός Αναλογίας Pixel Συσκευής σε Java – Μετατροπή HTML σε Κινητό
tags:
- Aspose.HTML
- Java
- Responsive Design
title: Ορισμός Αναλογίας Pixel Συσκευής σε Java – Μετατροπή HTML σε Κινητό
url: /el/java/conversion-html-to-other-formats/set-device-pixel-ratio-in-java-convert-html-to-mobile/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ορισμός Αναλογίας Pixel Συσκευής σε Java – Μετατροπή HTML σε Κινητό

Έχετε αναρωτηθεί ποτέ πώς να **ορίσετε την αναλογία pixel της συσκευής** σε Java ώστε το HTML σας να φαίνεται όπως θα ήταν σε ένα τηλέφωνο; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν δυσκολίες όταν προσπαθούν να **μετατρέψουν HTML σε κινητό** χωρίς πραγματική συσκευή, και καταλήγουν να μαντεύουν αν η διάταξή τους λειτουργεί πραγματικά.  

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που **ορίζει την αναλογία pixel της συσκευής**, φορτώνει μια ανταποκρινόμενη σελίδα, **αποδίδει αρχείο HTML σε στυλ Java**, και τελικά **αποθηκεύει το αποδοθέν αρχείο HTML** για μετέπειτα έλεγχο. Στο τέλος θα μπορείτε να **δοκιμάζετε ανταποκρινόμενο HTML** τοπικά, χωρίς ανάγκη εξομοιωτή.

## Τι Θα Χρειαστεί

- **Java 17** ή νεότερη (το API λειτουργεί με οποιοδήποτε πρόσφατο JDK).  
- Βιβλιοθήκη **Aspose.HTML for Java** – συνιστάται η έκδοση 22.12 ή νεότερη.  
- Μια απλή ανταποκρινόμενη σελίδα HTML (π.χ., `responsive.html`).  
- Ένα IDE ή ένας απλός επεξεργαστής κειμένου και ένα τερματικό – ό,τι προτιμάτε.

Αυτό είναι όλο. Χωρίς επιπλέον εργαλεία κατασκευής, χωρίς Docker containers, μόνο απλή Java και ένα μόνο JAR.

---

## Βήμα 1: Δημιουργία Sandbox που **Ορίζει Αναλογία Pixel Συσκευής**

Η καρδιά της λύσης είναι το `DocumentSandbox`. Με τη ρύθμιση των διαστάσεων της οθόνης του και της **αναλογίας pixel της συσκευής**, μιμείται μια οθόνη υψηλής πυκνότητας (π.χ. iPhone 6/7/8).  

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class MobileSandbox {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox that simulates a mobile device screen
        DocumentSandbox mobileSandbox = new DocumentSandbox();
        mobileSandbox.setScreenWidth(375);          // width in CSS pixels
        mobileSandbox.setScreenHeight(667);         // height in CSS pixels
        mobileSandbox.setDevicePixelRatio(2.0);     // high‑density display

        // The sandbox now **sets device pixel ratio** to 2.0, which tells the renderer
        // to treat each CSS pixel as two physical pixels – exactly what modern phones do.
```

**Γιατί είναι σημαντικό:**  
Αν παραλείψετε την κλήση `setDevicePixelRatio`, η αποδοθείσα έξοδος θα φαίνεται θολή σε οθόνες retina, και τα media queries που εξαρτώνται από `devicePixelRatio` δεν θα ενεργοποιηθούν ποτέ. Με το ρητό **ορισμό της αναλογίας pixel της συσκευής**, εξασφαλίζετε ότι η διάταξη συμπεριφέρεται ακριβώς όπως θα έκανε σε πραγματική συσκευή.

## Βήμα 2: Φορτώστε τη Σελίδα Σας και **Μετατρέψτε HTML σε Κινητό**

Τώρα κατευθύνουμε το sandbox στο HTML που θέλετε να εξετάσετε. Η ίδια κλάση `Document` που θα χρησιμοποιούσατε για απόδοση σε επιτραπέζιο υπολογιστή λειτουργεί εδώ, αλλά περνάμε το sandbox ως δεύτερο όρισμα.

```java
        // 2️⃣ Load the responsive HTML document inside the sandbox
        // This is where we **convert HTML to mobile** by feeding it the mobileSandbox.
        Document htmlDocument = new Document("YOUR_DIRECTORY/responsive.html", mobileSandbox);
```

**Τι συμβαίνει στο παρασκήνιο;**  
Το Aspose.HTML διαβάζει το αρχείο, εφαρμόζει τις ρυθμίσεις του viewport του sandbox, και επανυπολογίζει τις μονάδες CSS βάσει της **αναλογίας pixel της συσκευής** που ορίσατε νωρίτερα. Αυτό σημαίνει ότι οποιοσδήποτε κανόνας `@media (min-device-pixel-ratio: 2)` θα τηρηθεί, επιτρέποντάς σας να **δοκιμάζετε ανταποκρινόμενο HTML** χωρίς φυσική συσκευή.

## Βήμα 3: **Απόδοση Αρχείου HTML σε Στυλ Java** και **Αποθήκευση Αποδοθέντος Αρχείου HTML**

Τέλος, ζητάμε από το `Document` να γράψει το επεξεργασμένο markup. Η έξοδος είναι ένα κανονικό αρχείο `.html` που αντικατοπτρίζει πώς φαίνεται η σελίδα στη προσομοιωμένη συσκευή.

```java
        // 3️⃣ Render and save the mobile view of the document
        // The save call creates a new HTML file that you can open in any browser.
        htmlDocument.save("YOUR_DIRECTORY/mobile_view.html");
    }
}
```

Ανοίξτε το `mobile_view.html` στο Chrome, πατήστε **Ctrl + Shift + I**, και ενεργοποιήστε τη γραμμή εργαλείων συσκευής – θα δείτε την ίδια διάταξη που μόλις αποδώσατε. Με άλλα λόγια, έχετε επιτυχώς **αποδώσει αρχείο html σε java** και **αποθηκεύσει το αποδοθέν αρχείο html** για μετέπειτα QA.

## Πλήρες, Εκτελέσιμο Παράδειγμα

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο `MobileSandbox.java`. Θυμηθείτε να αντικαταστήσετε το `YOUR_DIRECTORY` με την πραγματική διαδρομή φακέλου όπου βρίσκεται το `responsive.html`.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class MobileSandbox {
    public static void main(String[] args) throws Exception {

        // Step 1 – create a sandbox that simulates a mobile device screen
        DocumentSandbox mobileSandbox = new DocumentSandbox();
        mobileSandbox.setScreenWidth(375);          // width in CSS pixels (iPhone 6/7/8)
        mobileSandbox.setScreenHeight(667);         // height in CSS pixels
        mobileSandbox.setDevicePixelRatio(2.0);     // ★ set device pixel ratio ★

        // Step 2 – load the responsive HTML document inside the sandbox
        // This effectively **convert html to mobile** for testing.
        Document htmlDocument = new Document("YOUR_DIRECTORY/responsive.html", mobileSandbox);

        // Step 3 – render and **save rendered html file** for inspection
        htmlDocument.save("YOUR_DIRECTORY/mobile_view.html");

        // Optional: print a friendly confirmation
        System.out.println("Mobile view saved to mobile_view.html – you can now open it in any browser.");
    }
}
```

### Αναμενόμενο Αποτέλεσμα

- Το `mobile_view.html` περιέχει το ακριβές markup που θα χρησιμοποιούσε ο περιηγητής σε οθόνη πυκνότητας 2×.  
- Όλα τα media queries που εξαρτώνται από `device-pixel-ratio` ενεργοποιούνται σωστά.  
- Μπορείτε να ανοίξετε το αρχείο σε οποιονδήποτε επιτραπέζιο περιηγητή και να δείτε ακόμη τη διάταξη για κινητά, κάτι που είναι ιδανικό για **δοκιμή ανταποκρινόμενου HTML** σε CI pipelines.

---

## Συμβουλές & Ακραίες Περιπτώσεις

| Situation | What to Do | Why |
|-----------|------------|-----|
| **Διαφορετικά μεγέθη οθόνης** | Ρυθμίστε `setScreenWidth` / `setScreenHeight` ώστε να ταιριάζουν με τη συσκευή-στόχο (π.χ., 414 × 896 για iPhone XR). | Εγγυάται ότι η διάταξή σας λειτουργεί σε πολλαπλά σημεία διακοπής. |
| **Δοκιμή σε οριζόντια λειτουργία** | Ανταλλάξτε τις τιμές πλάτους και ύψους, μετά αποθηκεύστε ξανά. | Η οριζόντια λειτουργία συχνά ενεργοποιεί διαφορετικούς κανόνες CSS. |
| **Εικόνες υψηλής ανάλυσης** | Διατηρήστε το `setDevicePixelRatio` στο 3.0 για συσκευές όπως το iPhone X. | Αναγκάζει τον αποδοτικό να επιλέξει πόρους `@2x` ή `@3x` εάν χρησιμοποιείτε `srcset`. |
| **Δυναμικό περιεχόμενο (JS)** | Χρησιμοποιήστε `htmlDocument.renderToBitmap(...)` αντί για `save` εάν χρειάζεστε ένα raster στιγμιότυπο. | Ορισμένα scripts εκτελούνται μόνο όταν το DOM έχει αποδοθεί πλήρως. |
| **Ενσωμάτωση CI/CD** | Τυλίξτε τον κώδικα σε ένα Maven plugin ή Gradle task, και εκτελέστε το ως μέρος της κατασκευής σας. | Αυτοματοποιεί τη **δοκιμή ανταποκρινόμενου HTML** σε κάθε αίτημα έλξης. |

## Συχνές Ερωτήσεις

**Ε: Μπορώ να χρησιμοποιήσω αυτήν την προσέγγιση με απομακρυσμένο URL αντί για τοπικό αρχείο;**  
Α: Απόλυτα. Απλώς περάστε το URL string στον κατασκευαστή `Document` – το sandbox θα εξακολουθεί να εφαρμόζει την **αναλογία pixel της συσκευής** που ορίσατε.

**Ε: Λειτουργεί αυτό σε headless servers;**  
Α: Ναι. Το Aspose.HTML είναι μια καθαρά‑Java βιβλιοθήκη· δεν απαιτείται γραφικό περιβάλλον, καθιστώντας το ιδανικό για CI pipelines.

**Ε: Τι γίνεται αν η σελίδα μου χρησιμοποιεί γραμματοσειρές που δεν είναι εγκατεστημένες στον server;**  
Α: Συμπεριλάβετε συνδέσμους web‑font στο HTML σας ή ενσωματώστε τις γραμματοσειρές χρησιμοποιώντας `@font-face`. Ο αποδοτικός θα τις κατεβάσει όπως θα έκανε ένας κανονικός περιηγητής.

## Συμπέρασμα

Τώρα έχετε μια αξιόπιστη ροή εργασίας **ορισμού αναλογίας pixel συσκευής** που σας επιτρέπει να **μετατρέψετε HTML σε κινητό**.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}