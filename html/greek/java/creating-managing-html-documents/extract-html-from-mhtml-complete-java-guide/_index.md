---
category: general
date: 2026-04-19
description: Εξάγετε γρήγορα HTML από MHTML χρησιμοποιώντας Java. Μάθετε πώς να μετατρέπετε
  MHTML σε HTML, να εξάγετε το σώμα του email, να γράφετε συμβολοσειρά σε αρχείο και
  να διαχειρίζεστε τη μετατροπή MHT.
draft: false
keywords:
- extract html from mhtml
- convert mhtml to html
- extract email body
- write string to file
- convert mht to html
language: el
og_description: Εξαγωγή HTML από MHTML σε Java. Αυτός ο οδηγός δείχνει πώς να μετατρέψετε
  το MHTML σε HTML, να εξάγετε το σώμα του email και να γράψετε τη συμβολοσειρά σε
  αρχείο.
og_title: Εξαγωγή HTML από MHTML – Java βήμα‑βήμα
tags:
- Java
- Aspose.HTML
- Email Processing
title: Εξαγωγή HTML από MHTML – Πλήρης Οδηγός Java
url: /el/java/creating-managing-html-documents/extract-html-from-mhtml-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή HTML από MHTML – Πλήρης Οδηγός Java

Έχετε ποτέ χρειαστεί να **εξάγετε HTML από MHTML** αλλά δεν ήξερες από πού να ξεκινήσεις; Ίσως λάβατε ένα αρχειοθετημένο email (`.mht`) και θέλετε το καθαρό σώμα για προεπισκόπηση στο web, ή δημιουργείτε ένα script μετεγκατάστασης που μετατρέπει παλιά αρχεία σε σύγχρονες σελίδες HTML. Σε κάθε περίπτωση, το πρόβλημα είναι το ίδιο: έχετε ένα αρχείο‑αρχείο web και χρειάζεστε το ακατέργαστο HTML markup από αυτό.

Τα καλά νέα; Με λίγες γραμμές Java και τη βιβλιοθήκη Aspose.HTML μπορείτε να **μετατρέψετε MHTML σε HTML**, να εξάγετε το σώμα του email και ακόμη να γράψετε αυτή τη συμβολοσειρά σε αρχείο—όλα χωρίς να φύγετε από το IDE σας. Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία, θα εξηγήσουμε γιατί κάθε βήμα είναι σημαντικό και θα δείξουμε πώς να αντιμετωπίζετε κοινές περιπτώσεις όπως ελλιπείς πόρους ή κωδικοποιήσεις μη‑UTF‑8.

> **Γρήγορη ανακεφαλαίωση:** Στο τέλος αυτού του οδηγού θα μπορείτε να **εξάγετε το σώμα του email**, **μετατρέψετε MHTML σε HTML**, και **γράψετε συμβολοσειρά σε αρχείο** με ένα καθαρό, επαναχρησιμοποιήσιμο snippet που λειτουργεί για οποιοδήποτε `.mht` ή `.mhtml` του πετάξετε.

---

## Τι Θα Χρειαστείτε

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε:

- **Java 17+** (ο κώδικας χρησιμοποιεί το πρότυπο try‑with‑resources, διαθέσιμο από τη Java 7, αλλά η Java 17 είναι η τρέχουσα LTS).
- **Aspose.HTML for Java** JARs στο classpath σας. Μπορείτε να τα κατεβάσετε από το [Aspose website](https://products.aspose.com/html/java/) ή μέσω Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

- Ένα δείγμα αρχείου **`.mht` ή `.mhtml`** που θέλετε να επεξεργαστείτε. Για το demo θα το ονομάσουμε `email.mht` και θα το τοποθετήσουμε στο `YOUR_DIRECTORY`.

Αυτό είναι όλο—χωρίς επιπλέον frameworks, χωρίς βαρύ parsers. Απλώς καθαρή Java και μια καλά τεκμηριωμένη βιβλιοθήκη.

## Βήμα 1 – Άνοιγμα του Αρχείου MHTML ως Stream

Το πρώτο που κάνουμε είναι να ανοίξουμε το αρχειοθετημένο email ως `InputStream`. Η χρήση stream κρατά τη χρήση μνήμης χαμηλή, ειδικά για μεγάλα αρχεία `.mht` που μπορεί να περιέχουν ενσωματωμένες εικόνες ή CSS.

```java
// Step 1: Open the MHTML file as a stream
try (InputStream mhtmlStream = new FileInputStream("YOUR_DIRECTORY/email.mht")) {
    // Subsequent steps go inside this block
}
```

**Γιατί stream;**  
Ένα stream επιτρέπει στο `MhtmlDocument` να διαβάζει δεδομένα «on‑the‑fly», κάτι που σημαίνει ότι δεν θα αντιμετωπίσετε `OutOfMemoryError` ακόμη και αν το αρχείο είναι αρκετά μεγάλου μεγέθους. Επιπλέον, σας δίνει την ευελιξία να διαβάζετε από άλλες πηγές αργότερα (π.χ., `ByteArrayInputStream` από βάση δεδομένων).

## Βήμα 2 – Φόρτωση του Εγγράφου MHTML από το Stream

Τώρα παραδίδουμε το stream στην κλάση `MhtmlDocument` της Aspose. Αυτή η κλάση αναλύει το MIME‑κωδικοποιημένο αρχείο και δημιουργεί μια DOM‑όμοια αναπαράσταση του ενσωματωμένου HTML.

```java
// Step 2: Load the MHTML document from the stream
MhtmlDocument mhtmlDoc = new MhtmlDocument(mhtmlStream);
```

**Πίσω από τη σκηνή:**  
Η Aspose εξάγει κάθε μέρος MIME (HTML, εικόνες, CSS) και τα επανασυνθέτει εσωτερικά. Γι’ αυτό μπορείτε αργότερα να ζητήσετε μόνο το τμήμα HTML χωρίς να ανησυχείτε για τους ενσωματωμένους πόρους.

## Βήμα 3 – Ανάκτηση του Κύριου Περιεχομένου HTML

Με το έγγραφο φορτωμένο, η εξαγωγή του ακατέργαστου HTML είναι μια γραμμή κώδικα. Η μέθοδος `getHtmlContent()` επιστρέφει το σώμα ως `String`, διατηρώντας το αρχικό markup.

```java
// Step 3: Retrieve the main HTML content as a string
String htmlContent = mhtmlDoc.getHtmlContent();
```

**Τι παίρνετε:**  
`htmlContent` περιέχει ολόκληρη τη σελίδα HTML—συμπεριλαμβανομένων των ετικετών `<head>` και `<body>`—ακριβώς όπως εμφανίστηκε όταν αποθηκεύτηκε το email. Αν χρειάζεστε μόνο το ορατό τμήμα, μπορείτε αργότερα να το αναλύσετε με το Jsoup και να αφαιρέσετε το `<head>`.

## Βήμα 4 – Εγγραφή του Εξαγόμενου HTML σε Ξεχωριστό Αρχείο

Η αποθήκευση της συμβολοσειράς σε δίσκο είναι απλή με το API `java.nio.file`. Αυτό το βήμα δείχνει το πρότυπο **write string to file** που λειτουργεί σε οποιαδήποτε πλατφόρμα.

```java
// Step 4: Save the extracted HTML to a separate file
Files.writeString(Path.of("YOUR_DIRECTORY/email_body.html"), htmlContent);
```

**Συμβουλή:**  
Αν χρειάζεστε συγκεκριμένο charset, χρησιμοποιήστε `Files.writeString(Path, CharSequence, Charset)`. Η προεπιλογή είναι UTF‑8, που λειτουργεί για τα περισσότερα σύγχρονα emails.

## Βήμα 5 – Επιβεβαίωση της Εξαγωγής

Ένα γρήγορο `System.out.println` σας επιτρέπει να επαληθεύσετε ότι όλα εκτελέστηκαν χωρίς εξαιρέσεις. Σε παραγωγικό περιβάλλον θα αντικαταστήσετε αυτό το print με κατάλληλο logging.

```java
// Step 5: Indicate successful extraction
System.out.println("HTML extracted.");
```

Όταν τρέξετε το πρόγραμμα, θα πρέπει να δείτε `HTML extracted.` στην κονσόλα, και το αρχείο `email_body.html` θα εμφανιστεί στο `YOUR_DIRECTORY`.

## Πλήρες, Έτοιμο‑για‑Εκτέλεση Παράδειγμα

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι η πλήρης, αυτόνομη κλάση Java. Μπορείτε να την αντιγράψετε‑επικολλήσετε στο IDE σας και να πατήσετε **Run**.

```java
import com.aspose.html.MhtmlDocument;
import java.io.FileInputStream;
import java.io.InputStream;
import java.nio.file.Files;
import java.nio.file.Path;

public class MhtmlToHtmlConverter {

    public static void main(String[] args) {
        // Adjust the path to point to your .mht/.mhtml file
        String sourcePath = "YOUR_DIRECTORY/email.mht";
        String targetPath = "YOUR_DIRECTORY/email_body.html";

        // Try-with-resources ensures the stream is closed automatically
        try (InputStream mhtmlStream = new FileInputStream(sourcePath)) {

            // Load the MHTML document
            MhtmlDocument mhtmlDoc = new MhtmlDocument(mhtmlStream);

            // Extract the HTML content
            String htmlContent = mhtmlDoc.getHtmlContent();

            // Write the HTML string to a new file
            Files.writeString(Path.of(targetPath), htmlContent);

            // Simple confirmation output
            System.out.println("HTML extracted to " + targetPath);
        } catch (Exception e) {
            // In real code you might want to log this instead of printing
            System.err.println("Failed to extract HTML: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Αναμενόμενη Έξοδος

Η εκτέλεση του προγράμματος εκτυπώνει κάτι όπως:

```
HTML extracted to YOUR_DIRECTORY/email_body.html
```

Και το `email_body.html` θα περιέχει την πλήρη πηγή HTML του αρχικού email. Ανοίξτε το σε έναν browser—θα δείτε την ίδια οπτική απόδοση όπως το αρχικό αρχειοθετημένο μήνυμα (εκτός από τυχόν εξωτερικούς πόρους που δεν ήταν ενσωματωμένοι).

## Διαχείριση Συνηθισμένων Edge Cases

### 1. Ελλιπείς Ενσωματωμένοι Πόροι

Μερικές φορές το αρχείο MHTML αναφέρει εξωτερικές εικόνες που δεν αποθηκεύτηκαν μέσα στο αρχείο. Σε αυτές τις περιπτώσεις το `getHtmlContent()` επιστρέφει ακόμα το markup `<img src="...">`, αλλά τα URLs θα δείχνουν στην αρχική τοποθεσία. Αν χρειάζεστε ένα πλήρως αυτόνομο αρχείο HTML, μπορείτε:

- Να χρησιμοποιήσετε `MhtmlDocument.save(Path, SaveFormat.HTML)` για να αφήσετε την Aspose να εξάγει όλους τους πόρους σε φάκελο.
- Ή να επεξεργαστείτε το HTML με μια βιβλιοθήκη όπως **Jsoup** για να αντικαταστήσετε τα απομακρυσμένα URLs με data URIs κωδικοποιημένα σε base64.

### 2. Κωδικοποιήσεις μη‑UTF‑8

Αν το email αποθηκεύτηκε με διαφορετικό charset (π.χ., `windows-1252`), η επιστρεφόμενη συμβολοσειρά μπορεί να περιέχει ακατάλληλους χαρακτήρες. Μπορείτε να επιβάλετε συγκεκριμένο charset κατά την εγγραφή:

```java
Files.writeString(
    Path.of(targetPath),
    htmlContent,
    StandardCharsets.ISO_8859_1
);
```

### 3. Μεγάλα Αρχεία

Για αρχεία μεγαλύτερα από μερικές εκατοντάδες megabytes, σκεφτείτε να κάνετε streaming την έξοδο HTML απευθείας σε `BufferedWriter` αντί να φορτώνετε ολόκληρη τη συμβολοσειρά στη μνήμη. Η Aspose προσφέρει επίσης μια μέθοδο **`save`** που γράφει απευθείας σε αρχείο, παρακάμπτοντας το ενδιάμεσο `String`.

## Pro Tips & Best Practices

- **Ξαναχρησιμοποιήστε το αντικείμενο `MhtmlDocument`** αν χρειαστεί να εξάγετε πολλαπλά τμήματα (π.χ., CSS, εικόνες). Αναλύει το αρχείο μόνο μία φορά.
- **Επικυρώστε το αποτέλεσμα** με έναν HTML validator (W3C validator ή `jsoup.isValid()`) αν σκοπεύετε να τροφοδοτήσετε το HTML σε άλλο σύστημα.
- **Καταγράψτε, μην τυπώνετε** σε παραγωγή. Αντικαταστήστε το `System.out.println` με ένα framework logging όπως το SLF4J για καταγραφή χρονικών σημείων και επιπέδων σοβαρότητας.
- **Έλεγχος εκδόσεων των εξαρτήσεων.** Η Aspose κυκλοφορεί συχνές ενημερώσεις· κλειδώστε την έκδοση στο `pom.xml` σας για να αποφύγετε απρόσμενες αλλαγές που σπάζουν τον κώδικα.

## Συμπέρασμα

Μόλις ολοκληρώσαμε μια πρακτική, end‑to‑end λύση για **εξαγωγή HTML από MHTML** χρησιμοποιώντας Java. Ανοίγοντας το αρχείο ως stream, φορτώνοντάς το με Aspose.HTML, παίρνοντας τη συμβολοσειρά HTML και **γράφοντας τη συμβολοσειρά σε αρχείο**, έχετε τώρα έναν αξιόπιστο τρόπο να **μετατρέψετε MHTML σε HTML**, **εξάγετε το σώμα του email**, και ακόμη **μετατρέψετε MHT σε HTML** για επεξεργασία downstream.

Αισθανθείτε ελεύθεροι να προσαρμόσετε το snippet: αντικαταστήστε το `FileInputStream` με `ByteArrayInputStream` αν τα αρχεία σας ζουν σε βάση δεδομένων, ή ενσωματώστε τον κώδικα σε μεγαλύτερη εργασία batch που επεξεργάζεται δεκάδες emails ταυτόχρονα. Η βασική ιδέα παραμένει η ίδια—αφήστε μια εξειδικευμένη βιβλιοθήκη να κάνει το βαρέως βάρους, μετά χειριστείτε το απλό κείμενο όπως χρειάζεται.

**Επόμενα βήματα** που μπορείτε να εξερευνήσετε:

- Χρησιμοποιήστε το Jsoup για **καθαρισμό του εξαγόμενου HTML** (αφαίρεση tracking pixels, inline CSS, κ.λπ.).
- Αυτοματοποιήστε **μαζική μετατροπή** επαναλαμβάνοντας πάνω σε έναν φάκελο `.mht` αρχείων.
- Συνδυάστε αυτό με **Apache POI** για ενσωμάτωση του καθαρισμένου HTML σε έγγραφα Word ή PDF.

Έχετε ερωτήσεις για κάποιο συγκεκριμένο edge case ή θέλετε να μοιραστείτε πώς επεκτείνετε το script; Αφήστε ένα σχόλιο παρακάτω—καλή κωδικοποίηση!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}