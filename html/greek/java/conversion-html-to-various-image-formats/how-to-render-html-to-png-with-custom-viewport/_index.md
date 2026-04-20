---
category: general
date: 2026-02-11
description: Πώς να αποδίδετε γρήγορα HTML χρησιμοποιώντας το Aspose.HTML για Java.
  Μάθετε πώς να μετατρέπετε HTML σε PNG, να ορίζετε το μέγεθος του viewport, να αποκλείετε
  απομακρυσμένες γραμματοσειρές και να αποθηκεύετε HTML ως PNG σε λίγα μόνο βήματα.
draft: false
keywords:
- how to render html
- convert html to png
- set viewport size
- save html as png
- block remote fonts
language: el
og_description: Πώς να αποδίδετε το HTML αποτελεσματικά – αυτός ο οδηγός σας δείχνει
  πώς να μετατρέψετε το HTML σε PNG, να ορίσετε το μέγεθος του viewport, να αποκλείσετε
  απομακρυσμένες γραμματοσειρές και να αποθηκεύσετε το HTML ως PNG χρησιμοποιώντας
  το Aspose.HTML για Java.
og_title: Πώς να αποδώσετε HTML σε PNG με προσαρμοσμένο viewport
tags:
- Java
- Aspose.HTML
- Image conversion
- Web rendering
title: Πώς να αποδώσετε HTML σε PNG με προσαρμοσμένο παράθυρο προβολής
url: /el/java/conversion-html-to-various-image-formats/how-to-render-html-to-png-with-custom-viewport/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αποδώσετε html σε PNG με προσαρμοσμένο viewport

Έχετε αναρωτηθεί ποτέ **πώς να αποδώσετε html** και να αποκτήσετε ένα pixel‑perfect PNG για σχεδίαση mobile‑first; Δεν είστε οι μόνοι. Είτε δημιουργείτε αυτοματοποιημένες δοκιμές οπτικής παλινδρόμησης, είτε παράγετε μικρογραφίες για ένα CMS, είτε απλώς χρειάζεστε μια γρήγορη λήψη στιγμιότυπου μιας ανταποκρινόμενης σελίδας, η δυνατότητα **μετατροπής html σε png** επί τόπου είναι πραγματικός ενισχυτής παραγωγικότητας.

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα τη διαδικασία απόδοσης html με το Aspose.HTML for Java, καλύπτοντας τα πάντα από **ορισμό μεγέθους viewport** μέχρι **αποκλεισμό απομακρυσμένων γραμματοσειρών**, ώστε να καταλήξετε με μια καθαρή, ντετερμινιστική εικόνα. Στο τέλος θα ξέρετε ακριβώς πώς να **αποθηκεύσετε html ως png** και γιατί κάθε ρύθμιση είναι σημαντική.

## Τι θα χρειαστείτε

- Java 17 ή νεότερη (ο κώδικας μπορεί να μεταγλωττιστεί και με παλαιότερες εκδόσεις, αλλά η 17 είναι η ιδανική)
- Aspose.HTML for Java 23.5 (ή η πιο πρόσφατη έκδοση τη στιγμή της ανάγνωσης)
- Ένα απλό IDE ή `javac` από τη γραμμή εντολών
- Πρόσβαση στο Internet μόνο για τη αρχική λήψη της βιβλιοθήκης· το sandbox θα **αποκλείσει απομακρυσμένες γραμματοσειρές** για αναπαραγωγικότητα

Δεν απαιτούνται άλλα εργαλεία τρίτων—όλα τρέχουν σε καθαρή Java.

## Πώς να αποδώσετε html – Βήμα 1: Φόρτωση του εγγράφου HTML

Πρώτα απ’ όλα: πρέπει να πείτε στο Aspose.HTML ποια σελίδα θέλετε να καταγράψετε. Η κλάση `HTMLDocument` μπορεί να φορτώσει μια απομακρυσμένη URL ή ένα τοπικό αρχείο. Η χρήση ζωντανής URL κάνει το παράδειγμα πιο ρεαλιστικό, αλλά μπορείτε επίσης να δείξετε στο `file:///C:/path/to/file.html`.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the responsive HTML page you want to render
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com/responsive.html");
```

**Γιατί είναι σημαντικό:** Η φόρτωση του εγγράφου είναι το θεμέλιο κάθε ροής **πώς να αποδώσετε html**. Αν η URL είναι μη προσβάσιμη, το Aspose.HTML θα ρίξει μια σαφή εξαίρεση, επιτρέποντάς σας να διαχειριστείτε τα προβλήματα δικτύου νωρίς.

## Ορισμός μεγέθους viewport για sandbox τύπου κινητού

Μια ανταποκρινόμενη σελίδα συχνά φαίνεται διαφορετικά σε τηλέφωνο σε σχέση με υπολογιστή. Για να μιμηθούμε μια μικρή συσκευή, δημιουργούμε ένα `DocumentSandbox` και ορίζουμε ρητά **το μέγεθος viewport**. Οι αριθμοί παρακάτω αντιπροσωπεύουν μια τυπική προβολή πορτραίτου iPhone 6/7/8.

```java
        // Step 2: Create a sandbox that mimics a small mobile device
        DocumentSandbox mobileSandbox = new DocumentSandbox();
        mobileSandbox.setViewportWidth(375);          // typical phone width in CSS pixels
        mobileSandbox.setViewportHeight(667);         // typical phone height in CSS pixels
        mobileSandbox.setDevicePixelRatio(2.0);       // high‑density screen
```

**Γιατί πρέπει να το κάνετε:** Χωρίς τον ορισμό του viewport, το Aspose.HTML προεπιλέγει μεγάλο μέγεθος επιφάνειας εργασίας, κάτι που μπορεί να προκαλέσει αλλαγές διάταξης. Ελέγχοντας το πλάτος, το ύψος και το pixel ratio εξασφαλίζετε ότι η παραγόμενη εικόνα ταιριάζει με αυτό που θα έβλεπε ένας πραγματικός χρήστης.

## Αποκλεισμός απομακρυσμένων γραμματοσειρών και εξωτερικών πόρων

Οι απομακρυσμένες γραμματοσειρές και εικόνες μπορεί να διαφέρουν από αίτηση σε αίτηση, οδηγώντας σε ασταθή στιγμιότυπα. Το sandbox μας επιτρέπει να **αποκλείσουμε απομακρυσμένες γραμματοσειρές** (και οποιουσδήποτε άλλους εξωτερικούς πόρους) ώστε η απόδοση να είναι ντετερμινιστική.

```java
        // Optional but highly recommended for repeatable results
        mobileSandbox.setEnableExternalResources(false); // block remote fonts/images for a clean view
```

**Συμβουλή επαγγελματία:** Αν *πρέπει* να χρησιμοποιήσετε εξωτερικές εικόνες (π.χ. φωτογραφία προϊόντος), ορίστε αυτή τη σημαία σε `true` και σκεφτείτε τη χρήση τοπικού CDN για αποφυγή καθυστέρησης δικτύου.

## Σύνδεση του sandbox με το έγγραφο HTML

Τώρα συνδέουμε το sandbox με το έγγραφο. Αυτό λέει στον renderer να τηρεί τους περιορισμούς viewport και τις πολιτικές πόρων που ορίσαμε.

```java
        // Step 3: Attach the sandbox to the HTML document
        htmlDoc.setSandbox(mobileSandbox);
```

## Μετατροπή html σε png και αποθήκευση της εικόνας

Με όλα ρυθμισμένα, η πραγματική μετατροπή είναι μια μόνο γραμμή. Η `Converter.convertHTML` παίρνει το έγγραφο, μια διαδρομή εξόδου και `ImageSaveOptions` που καθορίζουν PNG ως μορφή.

```java
        // Step 4: Render the sandboxed document to an image file
        Converter.convertHTML(
                htmlDoc,
                "YOUR_DIRECTORY/mobileView.png",
                new ImageSaveOptions(SaveFormat.PNG));
```

**Γιατί PNG;** Το PNG διατηρεί την απώλεια‑απώλειας ποιότητα, κάτι που είναι ιδανικό για δοκιμές UI όπου απαιτούνται pixel‑perfect συγκρίσεις. Αν χρειάζεστε μικρότερο αρχείο, αλλάξτε σε `SaveFormat.JPEG` και προσαρμόστε τη ρύθμιση ποιότητας.

## Επαλήθευση του αποτελέσματος – τι να περιμένετε

Όταν το πρόγραμμα ολοκληρωθεί, θα δείτε ένα μήνυμα στην κονσόλα και ένα αρχείο PNG στη διαδρομή που δώσατε.

```java
        // Step 5: Indicate that rendering has finished
        System.out.println("Rendered with custom sandbox.");
    }
}
```

Ανοίξτε το `mobileView.png` σε οποιονδήποτε προβολέα εικόνων. Θα πρέπει να δείτε τη responsive σελίδα αποδομένη ακριβώς όπως θα εμφανιζόταν σε οθόνη 375 × 667 CSS‑pixel, χωρίς εξωτερικές γραμματοσειρές. Αν συγκρίνετε αυτό με ένα στιγμιότυπο επιφάνειας εργασίας, οι διαφορές διάταξης γίνονται αμέσως εμφανείς.

![How to render html result screenshot](mobileView.png "How to render html result")

*Κείμενο alt εικόνας: “Στιγμιότυπο αποτελέσματος απόδοσης html” – δείχνει το τελικό PNG μετά τη μετατροπή.*

## Ακραίες περιπτώσεις και κοινές παραλλαγές

| Κατάσταση | Τι να αλλάξετε | Λόγος |
|-----------|----------------|--------|
| Χρειάζεται **διαφορετική συσκευή** (π.χ. tablet) | Προσαρμόστε `setViewportWidth`/`Height` και `setDevicePixelRatio` | Συμφωνεί με τις διαστάσεις CSS pixel της στόχευσης |
| Θέλετε **να συμπεριλάβετε εξωτερικό CSS** αλλά να αποκλείσετε τις γραμματοσειρές | Διατηρήστε `setEnableExternalResources(true)` και προσθέστε `mobileSandbox.setEnableRemoteFonts(false)` (αν υποστηρίζεται από το API) | Διασφαλίζει την πιστότητα στυλ ενώ αποφεύγει τη μεταβλητότητα γραμματοσειρών |
| Απόδοση **μεγάλων σελίδων** (υψηλότερων από το viewport) | Ορίστε `setViewportHeight` σε μεγαλύτερη τιμή ή χρησιμοποιήστε `DocumentSandbox.setScrollHeight` αν είναι διαθέσιμο | Αποτρέπει το κόψιμο περιεχομένου πέρα από το αρχικό viewport |
| Χρειάζεται **αποθήκευση ως JPEG** για συνημμένα email | Αντικαταστήστε `SaveFormat.PNG` με `SaveFormat.JPEG` και προαιρετικά περάστε `new JpegSaveOptions(85)` | Μειώνει το μέγεθος αρχείου με κόστος μικρής απώλειας ποιότητας |

## Συχνές ερωτήσεις

**Λειτουργεί αυτό σε headless servers;**  
Ναι. Το Aspose.HTML είναι καθαρά βιβλιοθήκη Java και δεν εξαρτάται από γραφικό περιβάλλον, καθιστώντας το ιδανικό για CI pipelines.

**Τι γίνεται αν η στόχευση σελίδα απαιτεί έλεγχο ταυτότητας;**  
Μπορείτε να περάσετε μια προ‑φορτωμένη συμβολοσειρά HTML στο `HTMLDocument` αντί για URL, ή να χρησιμοποιήσετε `HttpClient` για λήψη της σελίδας με cookies και στη συνέχεια να περάσετε το περιεχόμενο.

**Μπορώ να αποδώσω πολλές σελίδες σε βρόχο;**  
Απόλυτα. Απλώς δημιουργήστε ένα νέο `HTMLDocument` για κάθε URL, επαναχρησιμοποιήστε το ίδιο `DocumentSandbox` αν το viewport παραμένει σταθερό, και καλέστε `Converter.convertHTML` μέσα στο βρόχο σας.

## Συμπεράσματα

Καλύψαμε **πώς να αποδώσετε html** σε αρχείο PNG χρησιμοποιώντας το Aspose.HTML for Java, δείξαμε πώς να **ορίσετε το μέγεθος viewport**, παρουσιάσαμε τον ασφαλέστερο τρόπο **αποκλεισμού απομακρυσμένων γραμματοσειρών**, και περάσαμε από τον ακριβή κώδικα που χρειάζεστε για **μετατροπή html σε png** και **αποθήκευση html ως png** στο δίσκο. Με αυτή τη γνώση μπορείτε να αυτοματοποιήσετε οπτικές δοκιμές, να δημιουργήσετε μικρογραφίες ή να αρχειοθετήσετε ιστοσελίδες με pixel‑perfect πιστότητα.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να αποδώσετε PDF αντί για PNG, ή πειραματιστείτε με CSS media queries για λήψη τόσο πορτραίτου όσο και τοπίου. Οι ίδιες μηχανισμοί sandbox ισχύουν, οπότε είστε ήδη έτοιμοι για μια ολόκληρη σειρά εργασιών δημιουργίας εικόνων.

Αν αντιμετωπίσετε πρόβλημα, ελέγξτε ξανά ότι χρησιμοποιείτε τις πιο πρόσφατες JAR του Aspose.HTML και ότι η Java runtime σας ταιριάζει με τις απαιτήσεις της βιβλιοθήκης. Καλή απόδοση!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}