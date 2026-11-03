---
category: general
date: 2026-07-02
description: Μάθετε πώς να αποθηκεύσετε μια ιστοσελίδα ως mhtml χρησιμοποιώντας το
  Aspire HTML for Java. Αυτός ο οδηγός καλύπτει τις επιλογές αποθήκευσης MHTML, την
  ενσωμάτωση πόρων και τον πλήρη κώδικα Java.
draft: false
keywords:
- save webpage as mhtml
- aspose html for java
- mhtml save options
- embed resources in mhtml
- htmldocument java
language: el
og_description: Αποθηκεύστε τη σελίδα ως mhtml γρήγορα με το Aspose HTML for Java.
  Ακολουθήστε αυτόν τον οδηγό για πλήρη κώδικα, επιλογές και αντιμετώπιση προβλημάτων.
og_title: Αποθήκευση ιστοσελίδας ως mhtml – Πλήρης Εκμάθηση Java
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Learn how to save webpage as mhtml using Aspise HTML for Java. This
    guide covers MHTML save options, embedding resources, and full Java code.
  headline: save webpage as mhtml with Aspose HTML for Java – Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to save webpage as mhtml using Aspise HTML for Java. This
    guide covers MHTML save options, embedding resources, and full Java code.
  name: save webpage as mhtml with Aspose HTML for Java – Step‑by‑Step Guide
  steps:
  - name: Maven Dependency (Primary Way)
    text: If you’re using Maven, pop this snippet into your `pom.xml`. It pulls the
      latest stable version from Maven Central.
  - name: Manual JAR Setup (Alternative)
    text: 'Download the `aspose-html-23.10.jar` from the Aspose website, then add
      it to your classpath:'
  - name: Optional Tweaks
    text: '- **`setDocumentTitle("My Snapshot")`** – gives the MHTML a friendly title.
      - **`setEncoding(Encoding.UTF_8)`** – forces UTF‑8, handy for non‑ASCII sites.
      - **`setCompressResources(true)`** – reduces size by compressing embedded binaries.'
  - name: Edge Cases
    text: '- **HTTPS sites with self‑signed certificates** – Aspose respects Java’s
      default SSL settings. If you encounter `SSLHandshakeException`, import the certificate
      into the JVM keystore or disable verification (not recommended for production).
      - **Dynamic pages relying on JavaScript** – Aspose renders t'
  type: HowTo
tags:
- Java
- Aspose
- Web Conversion
title: Αποθήκευση ιστοσελίδας ως mhtml με το Aspose HTML για Java – Οδηγός βήμα‑προς‑βήμα
url: /el/java/saving-html-documents/save-webpage-as-mhtml-with-aspose-html-for-java-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# αποθήκευση ιστοσελίδας ως mhtml – Πλήρης Java Tutorial

Κάποτε χρειάστηκε να **αποθηκεύσετε μια ιστοσελίδα ως mhtml** αλλά δεν ήξερες ποια βιβλιοθήκη θα κάνει τη σκληρή δουλειά; Δεν είσαι μόνος. Πολλοί προγραμματιστές συναντούν εμπόδιο όταν θέλουν ένα στιγμιότυπο ενός ζωντανού ιστότοπου σε ένα μόνο αρχείο—ιδιαίτερα όταν χρειάζονται όλες τις εικόνες, τα CSS και τα scripts ενσωματωμένα.

Το θέμα είναι: το Aspose HTML for Java κάνει αυτό το έργο παιχνιδάκι. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από τη ρύθμιση της βιβλιοθήκης μέχρι τη ρύθμιση των **επιλογών αποθήκευσης MHTML** ώστε το αποτέλεσμα να μοιάζει ακριβώς με την αρχική σελίδα. Στο τέλος, θα έχεις ένα έτοιμο πρόγραμμα Java που αποθηκεύει οποιοδήποτε URL ως αρχείο MHTML, με ενσωματωμένους πόρους.

## Τι Θα Μάθεις

- Πώς να προσθέσεις το **Aspose HTML for Java** στο πρότζεκτ σου (Maven ή χειροκίνητο JAR).
- Τον σωστό τρόπο δημιουργίας ενός `HTMLDocument` από απομακρυσμένο URL.
- Πώς να ρυθμίσεις τις **επιλογές αποθήκευσης MHTML** για ενσωμάτωση εικόνων, στυλ και scripts.
- Ένα πλήρες, εκτελέσιμο δείγμα κώδικα που μπορείς να αντιγράψεις‑επικολλήσεις και να τρέξεις.
- Συνηθισμένα προβλήματα (όπως χρονικά όρια δικτύου ή έλλειψη αδειών) και πώς να τα αποφύγεις.

Χωρίς περιττές πληροφορίες, μόνο τα πρακτικά βήματα που μπορείς να εφαρμόσεις σήμερα.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιώσου ότι έχεις:

- Java 17 (ή οποιοδήποτε πρόσφατο JDK) εγκατεστημένο και `JAVA_HOME` ορισμένο.
- Ένα εργαλείο κατασκευής της επιλογής σου—το Maven χρησιμοποιείται στα παραδείγματα, αλλά μπορείς επίσης να προσθέσεις τα JAR χειροκίνητα.
- Ενεργή σύνδεση στο διαδίκτυο για το demo URL (`https://example.com`), ή αντικατέστησέ το με οποιονδήποτε ιστότοπο που διαχειρίζεσαι.
- Άδεια για το Aspose HTML for Java. Αν κάνεις μόνο πειραματισμούς, η δωρεάν αξιολόγηση λειτουργεί, αλλά θυμήσου να ορίσεις την άδεια για να αποφύγεις υδατογραφήματα.

Τα έχεις όλα; Τέλεια—ας ξεκινήσουμε.

## Βήμα 1: Προσθήκη Aspose HTML for Java στο Πρότζεκτ Σου

### Maven Dependency (Κύρια Μέθοδος)

Αν χρησιμοποιείς Maven, πρόσθεσε αυτό το απόσπασμα στο `pom.xml`. Θα κατεβάσει την πιο πρόσφατη σταθερή έκδοση από το Maven Central.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- check for newer releases -->
</dependency>
```

> **Pro tip:** Κράτησε σταθερό τον αριθμό έκδοσης για να αποφύγεις απρόσμενες αλλαγές όταν κυκλοφορήσει νέα έκδοση.

### Manual JAR Setup (Εναλλακτική)

Κατέβασε το `aspose-html-23.10.jar` από την ιστοσελίδα της Aspose, έπειτα πρόσθεσέ το στο classpath σου:

```bash
javac -cp ".;path/to/aspose-html-23.10.jar" SaveAsMhtml.java
java  -cp ".;path/to/aspose-html-23.10.jar" SaveAsMhtml
```

Με οποιονδήποτε τρόπο, τώρα έχεις **aspose html for java** έτοιμο.

## Βήμα 2: Φόρτωση της Ιστοσελίδας σε ένα `HTMLDocument`

Η κλάση `HTMLDocument` είναι το σημείο εισόδου για οποιαδήποτε επεξεργασία HTML. Δώσε της ένα URL, και το Aspose κάνει τη σκληρή δουλειά—ανακτά το markup, κατεβάζει τους συνδεδεμένους πόρους και δημιουργεί ένα DOM με το οποίο μπορείς να δουλέψεις.

```java
import com.aspose.html.*;

public class SaveAsMhtml {
    public static void main(String[] args) throws Exception {
        // Step 2: Load the web page into an HTMLDocument
        HTMLDocument doc = new HTMLDocument("https://example.com");
```

Γιατί να χρησιμοποιήσεις `HTMLDocument` αντί για έναν ακατέργαστο HTTP client; Επειδή η κλάση αυτόματα λύνει σχετικές διευθύνσεις, διαχειρίζεται redirects και σέβεται την κωδικοποίηση χαρακτήρων της σελίδας—λεπτομέρειες που αλλιώς θα έπρεπε να κωδικοποιήσεις εσύ.

## Βήμα 3: Ρύθμιση `MhtmlSaveOptions` και Ενσωμάτωση Πόρων

Από προεπιλογή, το Aspose δημιουργεί ένα αρχείο MHTML που αναφέρεται σε εξωτερικά assets. Για να **αποθηκεύσεις την ιστοσελίδα ως mhtml** σε ένα ενιαίο, φορητό αρχείο, πρέπει να ενσωματώσεις αυτούς τους πόρους.

```java
        // Step 3: Create MHTML save options and embed external resources
        com.aspose.html.saving.MhtmlSaveOptions mhtmlOpts = new com.aspose.html.saving.MhtmlSaveOptions();
        mhtmlOpts.setEmbedResources(true); // embed images, CSS, JS
```

Η κλήση `setEmbedResources(true)` λέει στη βιβλιοθήκη να ενσωματώνει τα πάντα—οι εικόνες γίνονται base64 strings, το CSS τοποθετείται απευθείας μέσα στο σώμα του MHTML και τα scripts διατηρούνται. Αν παραλείψεις αυτή τη γραμμή, το αποτέλεσμα θα είναι ακόμα αρχείο MHTML, αλλά θα περιέχει εξωτερικές αναφορές που θα σπάζουν όταν μετακινήσεις το αρχείο.

### Προαιρετικές Ρυθμίσεις

- **`setDocumentTitle("My Snapshot")`** – δίνει στο MHTML έναν φιλικό τίτλο.
- **`setEncoding(Encoding.UTF_8)`** – εξαναγκάζει UTF‑8, χρήσιμο για μη‑ASCII ιστοσελίδες.
- **`setCompressResources(true)`** – μειώνει το μέγεθος συμπιέζοντας τα ενσωματωμένα δυαδικά δεδομένα.

Πειραματίσου ελεύθερα· οι επιλογές είναι καλά τεκμηριωμένες στο Aspose API.

## Βήμα 4: Αποθήκευση του Εγγράφου ως Αρχείο MHTML

Τώρα που όλα είναι ρυθμισμένα, η αποθήκευση της σελίδας γίνεται με μία μόνο γραμμή κώδικα.

```java
        // Step 4: Save the document as an MHTML file
        doc.save("output/example.mhtml", mhtmlOpts);
        System.out.println("Webpage saved successfully as MHTML!");
    }
}
```

Τρέχοντας το πρόγραμμα θα κατεβάσει το `https://example.com`, θα ενσωματώσει όλα τα assets του και θα δημιουργήσει ένα αρχείο `example.mhtml` στο φάκελο `output`. Άνοιξέ το σε Chrome, Edge ή Internet Explorer (τα προγράμματα περιήγησης που ακόμα υποστηρίζουν MHTML) για να δεις ένα ακριβές αντίγραφο της ζωντανής σελίδας.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι η πλήρης, αυτόνομη κλάση Java. Αντέγραψέ την στο `SaveAsMhtml.java`, προσαρμόζοντας το μονοπάτι εξόδου αν θέλεις, και τρέξε την.

```java
import com.aspose.html.*;
import com.aspose.html.saving.*;

public class SaveAsMhtml {
    public static void main(String[] args) throws Exception {
        // Load the target web page
        HTMLDocument doc = new HTMLDocument("https://example.com");

        // Configure MHTML options – embed everything for a single‑file result
        MhtmlSaveOptions mhtmlOpts = new MhtmlSaveOptions();
        mhtmlOpts.setEmbedResources(true);
        // Optional: give the file a friendly title and enforce UTF‑8
        mhtmlOpts.setDocumentTitle("Example.com Snapshot");
        mhtmlOpts.setEncoding(java.nio.charset.StandardCharsets.UTF_8);
        mhtmlOpts.setCompressResources(true);

        // Save as MHTML
        String outputPath = "output/example.mhtml";
        doc.save(outputPath, mhtmlOpts);
        System.out.println("Webpage saved successfully as MHTML at: " + outputPath);
    }
}
```

**Αναμενόμενη έξοδος** (console):

```
Webpage saved successfully as MHTML at: output/example.mhtml
```

Άνοιξε το `example.mhtml` με έναν περιηγητή που υποστηρίζει MHTML, και θα δεις το `example.com` να αποδίδεται ακριβώς όπως εμφανιζόταν online—εικόνες, στυλ και scripts όλα ακεραιά.

## Συνηθισμένα Προβλήματα & Πώς να Τα Διορθώσεις

| Συμπτωμα | Πιθανή Αιτία | Διόρθωση |
|----------|--------------|----------|
| **Το αρχείο είναι κενό ή περιέχει μόνο HTML markup** | `setEmbedResources(false)` ή παραλήφθηκε | Βεβαιώσου ότι καλείται `mhtmlOpts.setEmbedResources(true)`. |
| **Λείπουν εικόνες** | Χρονικό όριο δικτύου κατά τη λήψη πόρων | Αυξήστε το προεπιλεγμένο timeout με `doc.getSettings().setNetworkTimeout(30000);` (30 δευτερόλεπτα). |
| **`java.lang.NoClassDefFoundError`** | JAR δεν βρίσκεται στο classpath | Επαλήθευσε ότι το Aspose JAR περιλαμβάνεται στην παράμετρο `-cp` ή ως εξάρτηση Maven. |
| **Το MHTML ανοίγει ως απλό κείμενο** | Χρήση περιηγητή που δεν υποστηρίζει MHTML (π.χ. Firefox) | Άνοιξε με Chrome, Edge ή Internet Explorer, ή μετονομασία σε `.mht`. |
| **Προειδοποίηση άδειας** | Λειτουργία αξιολόγησης χωρίς άδεια | Κατέγραψε την άδειά σου με `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` πριν δημιουργήσεις το `HTMLDocument`. |

### Ακραίες Περιπτώσεις

- **HTTPS ιστότοποι με αυτο‑υπογεγραμμένα πιστοποιητικά** – Το Aspose ακολουθεί τις προεπιλεγμένες ρυθμίσεις SSL της Java. Αν αντιμετωπίσεις `SSLHandshakeException`, εισήγαγε το πιστοποιητικό στο keystore της JVM ή απενεργοποίησε την επαλήθευση (δεν συνιστάται για παραγωγή).
- **Δυναμικές σελίδες που εξαρτώνται από JavaScript** – Το Aspose αποδίδει μόνο το στατικό HTML· δεν εκτελεί client‑side scripts. Για σελίδες που βασίζονται έντονα στο JS, σκέψου ένα headless browser (π.χ. Selenium) πριν τη μετατροπή.

## Γιατί να Επιλέξεις Aspose HTML for Java;

Μπορεί να αναρωτιέσαι, “Γιατί όχι απλώς ένας απλός μετατροπέας HTML‑σε‑MHTML?” Η απάντηση κρύβεται στην αξιοπιστία και τον έλεγχο. Το Aspose σου προσφέρει:

- **Λεπτομερείς επιλογές** (`MhtmlSaveOptions`) για ενσωμάτωση, συμπίεση και κωδικοποίηση.
- **Συνεπή λειτουργία σε πολλαπλές πλατφόρμες**—ο ίδιος κώδικας τρέχει σε Windows, macOS και Linux.
- **Ισχυρή διαχείριση σφαλμάτων**—επαναπροσπάθειες δικτύου, ήπια πτώση και λεπτομερείς εξαιρέσεις.

Με λίγα λόγια, είναι η **συνιστώμενη προσέγγιση** για επιχειρησιακό αρχειοθέτηση ιστοσελίδων.

## Επόμενα Βήματα

Τώρα που μπορείς να **αποθηκεύσεις μια ιστοσελίδα ως mhtml**, σκέψου τις παρακάτω ιδέες:

- **Batch processing** – βρόχος πάνω σε λίστα URLs και δημιουργία zip με αρχεία MHTML.
- **Προγραμματισμένη αρχειοθέτηση** – συνδύασε με `java.util.Timer` ή cron job για καθημερινά snapshots.
- **Ενσωμάτωση με βάση δεδομένων** – αποθήκευσε τα bytes του MHTML ως BLOB για αναζητήσιμα αρχεία.
- **Μετατροπή σε άλλες μορφές** – το Aspose υποστηρίζει επίσης εξαγωγές σε PDF, DOCX και PNG από `HTMLDocument`.

Κάθε ένα από αυτά τα θέματα συνδέεται με τις δευτερεύουσες λέξεις‑κλειδιά όπως **aspose html for java** και **htmldocument java**, οπότε θα βρεις άφθονο υλικό για περαιτέρω εξερεύνηση.

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεσαι για να **αποθηκεύσεις μια ιστοσελίδα ως mhtml** χρησιμοποιώντας το Aspose HTML for Java: εγκατάσταση της βιβλιοθήκης, φόρτωση απομακρυσμένης σελίδας, ρύθμιση των **επιλογών αποθήκευσης MHTML** για ενσωμάτωση πόρων, και τελικά αποθήκευση του αποτελέσματος στο δίσκο. Με το πλήρες δείγμα κώδικα και τον οδηγό αντιμετώπισης προβλημάτων, μπορείς να αρχίσεις να αρχειοθετείς περιεχόμενο web αμέσως—χωρίς εξωτερικά εργαλεία.

Δοκίμασέ το, πειραματίσου με τις επιλογές, και πες μας πώς λειτουργεί στην περίπτωσή σου. Καλό coding!

![save webpage as mhtml example](images/save-webpage-as-mhtml.png "Εικονογράφηση ενός αποθηκευμένου αρχείου MHTML ανοιγμένου σε περιηγητή")


## Τι Πρέπει Να Μάθεις Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσεις επιπλέον δυνατότητες του API και να εξερευνήσεις εναλλακτικές προσεγγίσεις στα δικά σου έργα.

- [Save HTML to MHTML in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-to-mhtml/)
- [How to Convert HTML to MHTML with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [Save HTML Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}