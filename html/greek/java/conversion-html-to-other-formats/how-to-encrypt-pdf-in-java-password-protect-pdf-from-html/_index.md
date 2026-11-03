---
category: general
date: 2026-03-18
description: Μάθετε πώς να κρυπτογραφήσετε PDF και να προστατεύσετε με κωδικό πρόσβασης
  αρχεία PDF κατά τη μετατροπή HTML σε PDF σε Java χρησιμοποιώντας το Aspose.HTML.
  Συμπεριλαμβάνεται πλήρες, εκτελέσιμο παράδειγμα.
draft: false
keywords:
- how to encrypt pdf
- password protect pdf
- convert html to pdf
- html to pdf java
- create encrypted pdf
language: el
og_description: 'Πώς να κρυπτογραφήσετε PDF βήμα‑βήμα: προστασία PDF με κωδικό πρόσβασης
  κατά τη μετατροπή HTML σε PDF με το Aspose.HTML για Java.'
og_title: Πώς να κρυπτογραφήσετε PDF σε Java – Προστασία PDF με κωδικό πρόσβασης από
  HTML
tags:
- PDF
- Java
- Aspose
title: Πώς να κρυπτογραφήσετε PDF σε Java – Προστασία PDF με κωδικό πρόσβασης από
  HTML
url: /el/java/conversion-html-to-other-formats/how-to-encrypt-pdf-in-java-password-protect-pdf-from-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κρυπτογραφήσετε PDF σε Java – Προστασία PDF με κωδικό από HTML

Έχετε αναρωτηθεί ποτέ **πώς να κρυπτογραφήσετε PDF** αρχεία απευθείας από τον κώδικα Java; Ίσως δημιουργείτε μια διαδικτυακή πύλη που επιτρέπει στους χρήστες να κατεβάζουν αναφορές, αλλά χρειάζεται να διασφαλίσετε ότι αυτά τα έγγραφα παραμένουν ασφαλή από ανεπιθύμητες ματιές. Τα καλά νέα; Με το Aspose.HTML for Java μπορείτε **να προστατεύσετε PDF με κωδικό** ενώ μετατρέπετε σελίδες HTML σε PDF — χωρίς επιπλέον εργαλεία, χωρίς χειροκίνητα βήματα.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: από τη ρύθμιση της εξάρτησης Maven μέχρι τη διαμόρφωση των επιλογών κρυπτογράφησης, τη μετατροπή ενός αρχείου HTML και, τέλος, την επαλήθευση ότι το PDF είναι πραγματικά κλειδωμένο. Στο τέλος θα έχετε ένα αυτόνομο, έτοιμο για παραγωγή snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Java.

## Τι Θα Μάθετε

- Πώς να **μετατρέψετε HTML σε PDF** χρησιμοποιώντας τη βιβλιοθήκη Aspose.HTML.  
- Τα ακριβή API calls που απαιτούνται για **δημιουργία κρυπτογραφημένου PDF**.  
- Πότε να επιλέξετε προστασία με κωδικό χρήστη vs. κωδικό ιδιοκτήτη.  
- Συνηθισμένα προβλήματα, όπως σημαίες αδειών που δεν συμπεριφέρονται όπως αναμένεται.  
- Έναν γρήγορο τρόπο δοκιμής του αποτελέσματος χωρίς να φύγετε από το IDE.

Δεν απαιτείται προγενέστερη εμπειρία με το Aspose — μόνο ένα περιβάλλον Java 8+ και ένα αρχείο HTML που θέλετε να προστατέψετε.

## Προαπαιτούμενα

| Απαίτηση | Λόγος |
|-------------|--------|
| Java 8 ή νεότερο | Το Aspose.HTML στοχεύει σε Java 8+. |
| Maven ή Gradle (θα χρησιμοποιήσουμε Maven) | Απλοποιεί τη διαχείριση εξαρτήσεων. |
| Ένα αρχείο HTML (`secure.html`) | Το πηγαίο έγγραφο που θέλετε να κρυπτογραφήσετε. |
| Άδεια Aspose.HTML for Java (προαιρετικό) | Η δωρεάν αξιολόγηση λειτουργεί, αλλά μια άδεια αφαιρεί το υδατογράφημα αξιολόγησης. |

Αν έχετε ήδη όλα αυτά, υπέροχα — μπορείτε να προχωρήσετε στο πρώτο βήμα.

---

## Πώς να Κρυπτογραφήσετε PDF με Aspose.HTML (Primary Keyword)

Παρακάτω υπάρχει ένα **πλήρες, εκτελέσιμο πρόγραμμα** που δείχνει κάθε βήμα. Αντιγράψτε‑και‑επικολλήστε το σε μια κλάση με όνομα `PdfEncryptionTutorial` και τρέξτε το.

```java
// PdfEncryptionTutorial.java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfSaveOptions;
import com.aspose.html.saving.PdfEncryption;
import com.aspose.html.saving.PdfPermissions;

/**
 * Demonstrates how to encrypt PDF while converting HTML to PDF in Java.
 */
public class PdfEncryptionTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Initialize PDF save options – this object holds all PDF‑specific settings.
        PdfSaveOptions pdfOptions = new PdfSaveOptions();

        // 2️⃣ Configure encryption: user password, owner password, and allowed actions.
        pdfOptions.setEncryption(
                new PdfEncryption()
                        .setUserPassword("user123")               // password required to open the file
                        .setOwnerPassword("owner456")             // password that grants full control
                        .setPermissions(PdfPermissions.PRINT |   // allow printing
                                         PdfPermissions.COPY));   // allow copying text/images
        // 3️⃣ Perform the conversion from HTML to an encrypted PDF.
        Converter.convertDocument(
                "YOUR_DIRECTORY/secure.html",   // source HTML
                "YOUR_DIRECTORY/secure.pdf",    // destination PDF
                pdfOptions);                    // options we just configured

        // 4️⃣ Let the developer know the job is done.
        System.out.println("Encrypted PDF generated.");
    }
}
```

### Γιατί Λειτουργεί Αυτό

- **`PdfSaveOptions`** λειτουργεί σαν εργαλειοθήκη για όλα τα θέματα PDF — μέγεθος σελίδας, συμπίεση και, κρίσιμα για εμάς, κρυπτογράφηση.  
- **`PdfEncryption`** σας επιτρέπει να ορίσετε δύο κωδικούς: έναν *κωδικό χρήστη* που πρέπει να εισαχθεί για το άνοιγμα του αρχείου, και έναν *κωδικό ιδιοκτήτη* που ελέγχει τι μπορεί να κάνει ο χρήστης (π.χ. εκτύπωση, αντιγραφή). Αυτό το μοντέλο διπλού κωδικού αντικατοπτρίζει αυτό που ο Adobe Acrobat ονομάζει “permissions”.  
- **`PdfPermissions`** είναι ένα bitmask· συνδυάζουμε τις σημαίες με τον τελεστή `|` για να ενεργοποιήσουμε πολλαπλές ενέργειες. Στο παράδειγμα επιτρέπουμε στον θεατή να εκτυπώνει και να αντιγράφει, αλλά θα μπορούσατε να αφαιρέσετε τη σημαία `PRINT` για να απαγορεύσετε εντελώς την εκτύπωση.

---

## Βήμα 1: Ρυθμίστε το Έργο Σας (Secondary Keyword – convert html to pdf)

Αν χρησιμοποιείτε Maven, προσθέστε την παρακάτω εξάρτηση στο `pom.xml`. Προσαρμόστε την έκδοση στην πιο πρόσφατη κυκλοφορία (ως Μάρτιος 2026 είναι **23.11**).

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.11</version>
</dependency>
```

> **Pro tip:** Αν σκοπεύετε να τρέξετε τον κώδικα σε CI server, αποθηκεύστε το αρχείο άδειας (`Aspose.Total.Java.lic`) σε ασφαλή τοποθεσία και φορτώστε το κατά το runtime. Αυτό αποτρέπει το υδατογράφημα αξιολόγησης να εμφανιστεί στα PDFs σας.

---

## Βήμα 2: Αρχικοποιήστε τις Επιλογές Αποθήκευσης PDF (Secondary Keyword – html to pdf java)

Πριν μπορέσετε να κρυπτογραφήσετε οτιδήποτε, χρειάζεστε μια παρουσία `PdfSaveOptions`. Σκεφτείτε το σαν το *πάνελ ρυθμίσεων* που βλέπετε σε έναν επιτραπέζιο δημιουργό PDF.

```java
PdfSaveOptions pdfOptions = new PdfSaveOptions();
// You can also tweak image quality, compression, etc., here if needed.
```

> **Γιατί να το κάνετε;** Η προ-ρύθμιση των επιλογών κρατάει την αλυσίδα μετατροπής σας καθαρή και κάνει εύκολο το προσθήκη επιπλέον λειτουργιών αργότερα (όπως ενσωμάτωση γραμματοσειρών ή ρύθμιση συμμόρφωσης PDF/A).

---

## Βήμα 3: Εφαρμόστε τις Ρυθμίσεις Κρυπτογράφησης (Secondary Keyword – password protect pdf)

Τώρα έρχεται η καρδιά του tutorial: η διαμόρφωση της κρυπτογράφησης. Το API είναι σκόπιμα fluent, ώστε να μπορείτε να αλυσίδετε κλήσεις για μεγαλύτερη αναγνωσιμότητα.

```java
pdfOptions.setEncryption(
        new PdfEncryption()
                .setUserPassword("user123")
                .setOwnerPassword("owner456")
                .setPermissions(PdfPermissions.PRINT | PdfPermissions.COPY));
```

### Κατανόηση των Δικαιωμάτων

| Σημαία | Τι Επιτρέπει | Τυπική Χρήση |
|------|----------------|------------------|
| `PdfPermissions.PRINT` | Εκτύπωση του εγγράφου | Επιχειρηματικές αναφορές που χρειάζονται φυσική διανομή. |
| `PdfPermissions.COPY` | Αντιγραφή κειμένου ή εικόνων | Όταν θέλετε οι χρήστες να μπορούν να παραθέσουν μια παράγραφο. |
| `PdfPermissions.MODIFY` | Επεξεργασία του PDF | Σπάνια χορηγείται για ασφαλή έγγραφα. |
| `PdfPermissions.ANNOTATE` | Προσθήκη σχολίων/σχόλια | Χρήσιμο για κύκλους ανασκόπησης. |

Αν παραλείψετε μια σημαία, η αντίστοιχη ενέργεια αποκλείεται. Ο κωδικός ιδιοκτήτη μπορεί αργότερα να παρακάμψει αυτούς τους περιορισμούς, οπότε φυλάξτε τον ασφαλή.

---

## Βήμα 4: Μετατροπή HTML σε Κρυπτογραφημένο PDF (Secondary Keyword – convert html to pdf)

Η πραγματική μετατροπή είναι μια γραμμή κώδικα χάρη στο `Converter.convertDocument`. Διαβάζει το πηγαίο HTML, εφαρμόζει τις `PdfSaveOptions` (συμπεριλαμβανομένης της κρυπτογράφησης) και γράφει το αποτέλεσμα.

```java
Converter.convertDocument(
        "YOUR_DIRECTORY/secure.html",
        "YOUR_DIRECTORY/secure.pdf",
        pdfOptions);
```

> **Τι γίνεται αν το HTML περιέχει εξωτερικούς πόρους;** Το Aspose.HTML ακολουθεί σχετικές διαδρομές, οπότε βεβαιωθείτε ότι οι εικόνες, τα CSS και οι γραμματοσειρές είναι είτε ενσωματωμένα είτε προσβάσιμα από το σύστημα αρχείων.

### Οπτική Επισκόπηση

![διάγραμμα πώς να κρυπτογραφήσετε PDF](https://example.com/images/pdf-encryption.png "διάγραμμα πώς να κρυπτογραφήσετε PDF")

*Το διάγραμμα απεικονίζει τη ροή: HTML → Converter → PdfSaveOptions (με κρυπτογράφηση) → Κρυπτογραφημένο PDF.*

---

## Βήμα 5: Επαληθεύστε το Κρυπτογραφημένο PDF (Secondary Keyword – create encrypted pdf)

Τρέξτε το πρόγραμμα, μετά ανοίξτε το `secure.pdf` σε οποιονδήποτε προβολέα PDF (Adobe Reader, Foxit, κλπ.). Θα σας ζητηθεί ο **κωδικός χρήστη** (`user123`). Αφού τον εισάγετε:

- Δοκιμάστε να εκτυπώσετε το έγγραφο — λειτουργεί επειδή επιτρέψαμε το `PRINT`.  
- Προσπαθήστε να αντιγράψετε κείμενο — λειτουργεί επειδή επιτρέψαμε το `COPY`.  
- Ανοίξτε την καρτέλα *Properties → Security* — θα δείτε τον κωδικό ιδιοκτήτη (`owner456`) (μασκαρισμένο) και τις άδειες που ορίσατε.

Αν κάποια από αυτές τις ενέργειες είναι μπλοκαρισμένη, ελέγξτε ξανά το bitmask `PdfPermissions`.

---

## Συχνά Πάγια & Πώς να τα Αποφύγετε

1. **Λάθος πεζά‑κεφαλαία στον κωδικό** — Οι κωδικοί είναι case‑sensitive. Ένα περιττό κενό θα σας κλειδώσει έξω.  
2. **Απουσία αδειών** — Η παράλειψη του OR (`|`) μεταξύ σημαίων αφήνει μόνο την τελευταία σημαία ενεργή.  
3. **Σχετικές διαδρομές** — Η χρήση του `"secure.html"` χωρίς πλήρη διαδρομή λειτουργεί μόνο αν το τρέχον directory ταιριάζει. Χρησιμοποιήστε `Paths.get(...).toAbsolutePath()` για μεγαλύτερη σταθερότητα.  
4. **Υδατογράφημα αξιολόγησης** — Η εκτέλεση χωρίς άδεια προσθέτει τη σημείωση “Created with Aspose.Total for Java” σε κάθε σελίδα. Εγκαταστήστε την άδεια νωρίς στο `main` αν έχετε.

```java
// Example of loading a license (optional)
com.aspose.html.License license = new com.aspose.html.License();
license.setLicense("Aspose.Total.Java.lic");
```

---

## Ανακεφαλαίωση: Τι Καταφέραμε

Ξεκινήσαμε με το ερώτημα **πώς να κρυπτογραφήσετε PDF** ενώ μετατρέπουμε HTML σε PDF σε Java. Με τη διαμόρφωση των `PdfSaveOptions` και `PdfEncryption`, παράγουμε ένα **PDF προστατευμένο με κωδικό** που σέβεται τις άδειες που ορίσαμε. Το πλήρες παράδειγμα κώδικα είναι έτοιμο για αντιγραφή‑επικόλληση, και η προσέγγιση λειτουργεί για οποιαδήποτε πηγή HTML — είτε πρόκειται για στατική αναφορά είτε για δυναμικά παραγόμενο τιμολόγιο.

---

## Επόμενα Βήματα (Secondary Keywords in Action)

- **Δοκιμάστε άλλους συνδυασμούς αδειών**: απενεργοποιήστε την εκτύπωση για εξαιρετικά εμπιστευτικά έγγραφα.  
- **Επεξεργασία παρτίδας πολλαπλών αρχείων HTML**: τυλίξτε τη μετατροπή σε βρόχο και δημιουργήστε ένα zip κρυπτογραφημένων PDFs.  
- **Συνδυάστε με ψηφιακές υπογραφές**: μετά την κρυπτογράφηση, χρησιμοποιήστε το Aspose.PDF για να προσθέσετε κρυπτογραφική υπογραφή για μη‑αποδοχή.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}