---
category: general
date: 2026-03-29
description: Πώς να χρησιμοποιήσετε το sandbox για ασφαλή μετατροπή HTML σε PDF σε
  Java – ορίστε τον user agent, το μέγεθος οθόνης και το DPI για τέλεια αποτελέσματα.
draft: false
keywords:
- how to use sandbox
- convert html to pdf
- generate pdf from html
- set user agent
- html to pdf java
language: el
og_description: Πώς να χρησιμοποιήσετε το sandbox για να μετατρέψετε HTML σε PDF σε
  Java. Μάθετε πώς να ορίσετε τον πράκτορα χρήστη, το μέγεθος της οθόνης και το DPI
  για αξιόπιστη έξοδο PDF.
og_title: Πώς να χρησιμοποιήσετε το Sandbox – Οδηγός HTML‑σε‑PDF για Java
tags:
- Aspose.HTML
- Java
- PDF generation
title: Πώς να χρησιμοποιήσετε το Sandbox για τη μετατροπή HTML σε PDF σε Java
url: /el/java/conversion-html-to-other-formats/how-to-use-sandbox-for-html-to-pdf-conversion-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε το Sandbox για Μετατροπή HTML‑σε‑PDF σε Java

Έχετε αναρωτηθεί **πώς να χρησιμοποιήσετε sandbox** όταν μετατρέπετε ιστοσελίδες σε αρχεία PDF; Δεν είστε οι μόνοι—πολλοί προγραμματιστές Java συναντούν προβλήματα όταν οι κανόνες CSS @media αγνοούν τις διαστάσεις που έχετε ορίσει, ή όταν ένας απομακρυσμένος ιστότοπος μπλοκάρει το προεπιλεγμένο user‑agent. Τα καλά νέα; Ένα sandbox σας παρέχει ένα ελεγχόμενο περιβάλλον όπου καθορίζετε το μέγεθος της οθόνης, το DPI και ακόμη και τη ζώνη ώρας, εξασφαλίζοντας ότι το παραγόμενο PDF φαίνεται ακριβώς όπως το περιμένετε.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα τη διαδικασία **πώς να χρησιμοποιήσετε sandbox** με το Aspose.HTML, από τη ρύθμιση των διαστάσεων της οθόνης μέχρι τον ορισμό προσαρμοσμένου user‑agent, και τέλος τη μετατροπή ενός αρχείου HTML σε PDF. Στο τέλος θα μπορείτε να **μετατρέψετε HTML σε PDF** αξιόπιστα, **να δημιουργήσετε PDF από HTML** με οποιεσδήποτε ρυθμίσεις θέλετε, και θα ξέρετε πώς να **ορίσετε user agent** strings που απαιτούν ορισμένες υπηρεσίες web. Χωρίς εξωτερικά εργαλεία, μόνο ένα αυτόνομο πρόγραμμα Java.

> **Τι θα πάρετε:** ένα έτοιμο‑για‑εκτέλεση αρχείο `SandboxTutorial.java`, εξήγηση κάθε γραμμής, και συμβουλές για κοινά προβλήματα (όπως ελλιπείς γραμματοσειρές ή ασυμφωνίες ζώνης ώρας). Ας βουτήξουμε.

---

## Προαπαιτούμενα

- **Java 17** ή νεότερη εγκατεστημένη (ο κώδικας χρησιμοποιεί try‑with‑resources, που είναι διαθέσιμο από τη Java 7, αλλά συνιστούμε την τελευταία LTS).
- **Aspose.HTML for Java** βιβλιοθήκη (έκδοση 23.10 ή νεότερη). Προσθέστε την εξάρτηση Maven ή κατεβάστε το JAR από την ιστοσελίδα της Aspose.
- Ένα απλό αρχείο HTML (`input.html`) που θέλετε να μετατρέψετε σε PDF. Μπορεί να περιέχει CSS, εικόνες ή JavaScript—το Aspose.HTML τα διαχειρίζεται όλα.
- Ένα IDE ή έναν επεξεργαστή κειμένου· στα στιγμιότυπα θα χρησιμοποιήσουμε το Visual Studio Code, αλλά οποιοδήποτε IDE Java λειτουργεί.

> **Pro tip:** Αν χρησιμοποιείτε Maven, προσθέστε το ακόλουθο στο `pom.xml` σας:
> ```xml
> <dependency>
>     <groupId>com.aspose</groupId>
>     <artifactId>aspose-html</artifactId>
>     <version>23.10</version>
> </dependency>
> ```

---

## Πώς να Χρησιμοποιήσετε Sandbox – Ρύθμιση του Περιβάλλοντος

Το πρώτο πράγμα που πρέπει να γνωρίζετε για το **πώς να χρησιμοποιήσετε sandbox** είναι ότι δεν είναι ένα μαγικό μαύρο κουτί· είναι μια ελαφριά περιτύλιξη γύρω από μια ξεχωριστή διεργασία που σέβεται τις επιλογές που της δίνετε. Σκεφτείτε το ως έναν μικρό‑browser που τρέχει σε κλουβί, ακολουθώντας τους κανόνες σας.

```java
// Step 1: Import required Aspose.HTML classes
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.converters.Converter;
```

> **Γιατί αυτές οι εισαγωγές;** Η `DocumentSandbox` δημιουργεί το απομονωμένο περιβάλλον, η `SandboxOptions` σας επιτρέπει να ρυθμίσετε το μέγεθος της οθόνης, DPI, user‑agent κλπ., και η `Converter` κάνει το βαρέως τύπου έργο της μετατροπής HTML σε PDF.

### Ρύθμιση Μεγέθους Οθόνης, DPI και Ζώνης Ώρας

```java
// Step 2: Define sandbox configuration (screen size, DPI, user‑agent, time zone)
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(1280);               // width in pixels
sandboxOptions.setScreenHeight(720);               // height in pixels
sandboxOptions.setDevicePixelRatio(2.0);           // high‑DPI (retina) scaling
sandboxOptions.setUserAgent("AsposeHTML/1.0 (CI)"); // custom user‑agent string
sandboxOptions.setTimeZone("UTC");                // forces UTC for consistent timestamps
```

- **Πλάτος/ύψος οθόνης** επηρεάζει τα CSS media queries όπως `@media (max-width: 600px)`. Αν παραλείψετε αυτή τη ρύθμιση, το sandbox χρησιμοποιεί προεπιλογή 1024 × 768, κάτι που μπορεί να ενεργοποιήσει μια κινητή διάταξη που δεν περιμένατε.
- **Device pixel ratio** επηρεάζει το πώς rasterize‑γονται εικόνες και διανυσματικά γραφικά. Ορίζοντάς το σε `2.0` παίρνετε καθαρά, retina‑ready PDFs.
- **User‑agent** είναι κρίσιμο όταν ο στόχος εξυπηρετεί διαφορετικό markup σε διαφορετικούς browsers. Με **set user agent** σε μια συμβολοσειρά που μιμείται πραγματικό browser, αποφεύγετε την εξυπηρέτηση μιας “no‑script” έκδοσης.
- **Ζώνη ώρας** έχει σημασία για JavaScript που σχετίζεται με ημερομηνίες. Η χρήση UTC εξασφαλίζει επαναλήψιμα αποτελέσματα μεταξύ προγραμματιστών και CI pipelines.

---

## Μετατροπή HTML σε PDF Μέσα σε Sandbox

Τώρα που το sandbox είναι ρυθμισμένο, ας δούμε **πώς να χρησιμοποιήσετε sandbox** για να **μετατρέψετε HTML σε PDF**. Η μετατροπή πρέπει να γίνει *μέσα* στο sandbox· διαφορετικά οι κανόνες CSS `@media` θα διαβάσουν τις διαστάσεις του κεντρικού μηχανήματος, σπάζοντας τη διάταξη.

```java
// Step 3: Create a sandbox instance with the configured options
try (DocumentSandbox sandbox = new DocumentSandbox(sandboxOptions)) {

    // Step 4: Run the conversion inside the sandbox so CSS @media rules use the defined dimensions
    sandbox.run(() -> {
        // Convert input.html to sandboxed.pdf using the options defined above
        Converter.convert("YOUR_DIRECTORY/input.html", "YOUR_DIRECTORY/sandboxed.pdf");
    });
}
```

> **Τι συμβαίνει εδώ;**  
> 1. Η `DocumentSandbox` εκκινεί μια ξεχωριστή διεργασία με τις επιλογές που ορίσαμε.  
> 2. Η `sandbox.run` λαμβάνει ένα lambda (το μπλοκ κώδικα) που εκτελείται *μέσα* σε αυτή τη διεργασία.  
> 3. Η `Converter.convert` διαβάζει το `input.html`, το αποδίδει χρησιμοποιώντας την εικονική οθόνη του sandbox, και γράφει το `sandboxed.pdf`.

Αν τρέξετε το πρόγραμμα τώρα, θα πρέπει να δείτε ένα αρχείο `sandboxed.pdf` δίπλα στο πηγαίο HTML. Ανοίξτε το—ταιριάζει η διάταξη με αυτή που βλέπετε σε κανονικό browser στα 1280 × 720; Αν ναι, έχετε κατακτήσει το **πώς να χρησιμοποιήσετε sandbox** για δημιουργία PDF.

---

## Δημιουργία PDF από HTML με Προσαρμοσμένο User Agent

Μερικές φορές ο ιστότοπος που μετατρέπετε μπλοκάρει άγνωστους browsers. Εδώ έρχεται η **set user agent** σε δράση. Ας τροποποιήσουμε το παράδειγμα ώστε να μιμείται το Chrome στα Windows:

```java
sandboxOptions.setUserAgent(
    "Mozilla/5.0 (Windows NT 10.0; Win64; x64) " +
    "AppleWebKit/537.36 (KHTML, like Gecko) " +
    "Chrome/124.0.0.0 Safari/537.36"
);
```

Τρέξτε ξανά το πρόγραμμα και συγκρίνετε το PDF με αυτό που δημιουργήθηκε χρησιμοποιώντας το γενικό user‑agent του AsposeHTML. Θα παρατηρήσετε διαφορές σε γραμματοσειρές, εικονίδια ή ακόμη και κρυφά στοιχεία που εμφανίζονται μόνο για Chrome. Αυτό δείχνει **πώς να χρησιμοποιήσετε sandbox** για να ελέγξετε το header του αιτήματος, ένα ζωτικό κόλπο για αξιόπιστες **html to pdf java** pipelines.

---

## Συνηθισμένες Ακραίες Περιπτώσεις & Πώς να τις Αντιμετωπίσετε

| Κατάσταση | Γιατί Συμβαίνει | Διόρθωση (χρησιμοποιώντας πώς να χρησιμοποιήσετε sandbox) |
|-----------|----------------|--------------------------------|
| Απουσία web fonts | Το sandbox δεν έχει πρόσβαση στο φάκελο γραμματοσειρών του OS. | Προσθέστε `sandboxOptions.setFontFolder("/path/to/fonts")` ή ενσωματώστε γραμματοσειρές στο CSS με `@font-face`. |
| Σφάλματα JavaScript | Το sandbox τρέχει με περιορισμένο JavaScript engine. | Χρησιμοποιήστε `sandboxOptions.setJavaScriptEnabled(true)` (προεπιλογή) και βεβαιωθείτε ότι χρησιμοποιείτε Aspose.HTML 23.10+ που υποστηρίζει σύγχρονο JS. |
| Μεγάλες εικόνες προκαλούν αυξήσεις μνήμης | Υψηλό DPI + μεγάλες εικόνες → τεράστιοι raster buffers. | Μειώστε το `DevicePixelRatio` σε `1.0` ή προ‑κλιμακώστε τις εικόνες στο HTML. |
| Περιεχόμενο εξαρτημένο από ζώνη ώρας εμφανίζεται λανθασμένα | Το JavaScript `new Date()` χρησιμοποιεί τη ζώνη ώρας του κεντρικού μηχανήματος. | Ορίζοντας `sandboxOptions.setTimeZone("UTC")` εξαναγκάζει σταθερή ζώνη ώρας σε όλες τις builds. |

> **Συμβουλή:** Πάντα να δοκιμάζετε με μια εργασία CI που τρέχει το sandbox σε headless mode. Αν η εργασία αποτύχει, τα logs θα δείξουν ποια επιλογή προκάλεσε το πρόβλημα, κάνοντας το debugging πιο εύκολο.

---

## Πλήρες Παράδειγμα (Έτοιμο για Αντιγραφή)

Παρακάτω βρίσκεται το πλήρες `SandboxTutorial.java`. Αντικαταστήστε το `YOUR_DIRECTORY` με την απόλυτη διαδρομή του φακέλου του έργου σας.

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.converters.Converter;

public class SandboxTutorial {
    public static void main(String[] args) throws Exception {

        // Step 2: Define sandbox configuration (screen size, DPI, user‑agent, time zone)
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(1280);
        sandboxOptions.setScreenHeight(720);
        sandboxOptions.setDevicePixelRatio(2.0);
        sandboxOptions.setUserAgent("AsposeHTML/1.0 (CI)");
        sandboxOptions.setTimeZone("UTC");

        // OPTIONAL: Mimic Chrome if the site blocks generic agents
        // sandboxOptions.setUserAgent(
        //     "Mozilla/5.0 (Windows NT 10.0; Win64; x64) " +
        //     "AppleWebKit/537.36 (KHTML, like Gecko) " +
        //     "Chrome/124.0.0.0 Safari/537.36"
        // );

        // Step 3: Create a sandbox instance with the configured options
        try (DocumentSandbox sandbox = new DocumentSandbox(sandboxOptions)) {

            // Step 4: Run the conversion inside the sandbox so CSS @media rules use the defined dimensions
            sandbox.run(() -> {
                // Convert HTML to PDF
                Converter.convert("YOUR_DIRECTORY/input.html", "YOUR_DIRECTORY/sandboxed.pdf");
            });
        }

        System.out.println("PDF generated successfully at YOUR_DIRECTORY/sandboxed.pdf");
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Μετά την εκτέλεση `java SandboxTutorial`, θα δείτε το μήνυμα στην κονσόλα *«PDF generated successfully at …»* και ένα αρχείο με όνομα `sandboxed.pdf`. Ανοίξτε το· η σελίδα θα πρέπει να σέβεται τη διάταξη 1280 × 720, την υψηλή κλιμάκωση DPI, και οποιαδήποτε λογική προσαρμοσμένου user‑agent έχετε ενσωματώσει.

---

## Οπτική Επισκόπηση

![Diagram illustrating how to use sandbox for HTML‑to‑PDF conversion](https://example.com/placeholder.png "how to use sandbox diagram")

*Η εικόνα δείχνει τη ροή: Java code → SandboxOptions → DocumentSandbox → Converter → PDF.*

---

## Ανακεφαλαίωση – Τι Καλύψαμε

- **Πώς να χρησιμοποιήσετε sandbox** για απομόνωση της απόδοσης, εξασφαλίζοντας ότι τα CSS media queries βλέπουν τις διαστάσεις που καθορίζετε.  
- **Μετατροπή HTML σε PDF** με ασφάλεια, χωρίς παρενέργειες από το λειτουργικό σύστημα του κεντρικού μηχανήματος.  
- **Δημιουργία PDF από HTML** με προσαρμοσμένη **set user agent** string για ιστοτόπους που περιορίζουν το περιεχόμενο.  
- Αντιμετώπιση ακραίων περιπτώσεων όπως ελλιπείς γραμματοσειρές, Java

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}