---
category: general
date: 2026-03-18
description: πώς να ενσωματώσετε εικόνες κατά τη μετατροπή HTML σε PDF χρησιμοποιώντας
  το Aspose HTML για Java. Ακολουθήστε αυτό το βήμα‑βήμα οδηγό για να μετατρέψετε
  HTML σε PDF με έναν προσαρμοσμένο διαχειριστή πόρων.
draft: false
keywords:
- how to embed images
- convert html to pdf
- aspose html to pdf
- java html to pdf
- custom resource handler
language: el
og_description: πώς να ενσωματώσετε εικόνες κατά τη μετατροπή HTML σε PDF με το Aspose
  HTML for Java. Μάθετε την τεχνική του προσαρμοσμένου διαχειριστή πόρων σε αυτόν
  τον σύντομο οδηγό.
og_title: πώς να ενσωματώσετε εικόνες σε HTML σε PDF – οδηγός Aspose Java
tags:
- Aspose
- Java
- PDF conversion
title: Πώς να ενσωματώσετε εικόνες από HTML σε PDF με το Aspose – οδηγός Java
url: /el/java/conversion-html-to-other-formats/how-to-embed-images-in-html-to-pdf-with-aspose-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ενσωματώσετε εικόνες σε HTML → PDF με το Aspose – Οδηγός Java

Έχετε αναρωτηθεί **πώς να ενσωματώσετε εικόνες** όταν μετατρέπετε HTML σε PDF σε Java; Δεν είστε οι μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν πρόβλημα όταν το HTML τους αναφέρεται σε εικόνες που βρίσκονται μέσα στο JAR ή σε ιδιωτικό διακομιστή, και η μετατροπή καταλήγει με κενά placeholders. Τα καλά νέα; Το Aspose HTML for Java σας επιτρέπει να προσθέσετε έναν **προσαρμοσμένο διαχειριστή πόρων** ώστε κάθε εικόνα, CSS ή script να λυθεί ακριβώς όπως χρειάζεστε.

Σε αυτό το tutorial θα περάσουμε από τη διαδικασία από την ρύθμιση των επιλογών φόρτωσης μέχρι την παραγωγή ενός επαγγελματικού PDF που περιλαμβάνει τις ενσωματωμένες εικόνες. Στο τέλος θα μπορείτε να **μετατρέψετε HTML σε PDF** με το Aspose, να ενσωματώσετε εικόνες απευθείας από το classpath, και να καταλάβετε πώς λειτουργεί ο **προσαρμοσμένος διαχειριστής πόρων** στο παρασκήνιο. Χωρίς εξωτερικές υπηρεσίες, χωρίς ελλείποντα γραφικά.

> **Τι θα χρειαστείτε**  
> * Java 17 (ή οποιοδήποτε πρόσφατο JDK)  
> * Βιβλιοθήκη Aspose HTML for Java (v23.12 ή νεότερη)  
> * Ένα απλό αρχείο HTML που αναφέρει μια εικόνα (π.χ., `logo.png`)  
> * Το αρχείο εικόνας τοποθετημένο στο `src/main/resources/myresources/`  

Ας ξεκινήσουμε.

---

## Βήμα 1: Ρυθμίστε το Maven/Gradle project με το Aspose HTML

Πρώτα απ' όλα—προσθέστε την εξάρτηση Aspose HTML. Αν χρησιμοποιείτε Maven, τοποθετήστε το παρακάτω στο `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

Οι χρήστες του Gradle μπορούν να προσθέσουν:

```groovy
implementation 'com.aspose:aspose-html:23.12'
```

> **Pro tip:** Πάντα τραβήξτε την τελευταία σταθερή έκδοση· οι νεότερες κυκλοφορίες περιλαμβάνουν διορθώσεις σφαλμάτων για τη φόρτωση πόρων.

---

## Βήμα 2: Προετοιμάστε το HTML και την ενσωματωμένη εικόνα

Δημιουργήστε έναν φάκελο `src/main/resources/myresources/` και τοποθετήστε εκεί το `logo.png`. Στη συνέχεια δημιουργήστε ένα μικρό αρχείο HTML (π.χ., `page-with-assets.html`) που δείχνει σε αυτήν την εικόνα:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Sample Page</title>
</head>
<body>
    <h1>Welcome!</h1>
    <p>This page shows how to embed images.</p>
    <img src="logo.png" alt="Company logo">
</body>
</html>
```

Παρατηρήστε το `src="logo.png"` – θα αντιστοιχίσουμε αυτό το URL στην εικόνα μέσα στο JAR.

---

## Βήμα 3: Δημιουργήστε έναν **προσαρμοσμένο διαχειριστή πόρων** για την εξυπηρέτηση των ενσωματωμένων assets

Το Aspose HTML χρησιμοποιεί το `HtmlLoadOptions` για να ελέγξει πώς φορτώνονται εξωτερικοί πόροι. Παρέχοντας μια υλοποίηση `ResourceHandler`, μπορείτε να παρεμβείτε σε κάθε αίτηση URL. Ο παρακάτω διαχειριστής ελέγχει αν το ζητούμενο URL τελειώνει σε `logo.png` και, αν ναι, επιστρέφει ένα `InputStream` από το classpath. Για όλα τα άλλα επιστρέφουμε τον προεπιλεγμένο φορτωτή δικτύου.

```java
import com.aspose.html.*;
import com.aspose.html.loading.*;

import java.io.InputStream;

public class CustomResourceHandler {
    public static void main(String[] args) throws Exception {

        // 1️⃣  Create load options that will hold our handler
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();

        // 2️⃣  Register the handler – this is where the magic happens
        loadOptions.setResourceHandler(new ResourceHandler() {
            @Override
            public InputStream getResource(String url) {
                // If the URL points to our bundled logo, serve it from the JAR
                if (url.endsWith("logo.png")) {
                    // The image lives under /myresources/ inside the JAR
                    return getClass().getResourceAsStream("/myresources/logo.png");
                }
                // Anything else: let Aspose use its built‑in network loader
                return null;
            }
        });

        // 3️⃣  Convert the HTML to PDF using the custom loader
        Converter.convertDocument(
                "src/main/resources/page-with-assets.html",   // input HTML
                "output/page.pdf",                            // output PDF
                new PdfSaveOptions(),
                loadOptions);

        System.out.println("Conversion completed – images embedded!");
    }
}
```

### Γιατί ένας προσαρμοσμένος διαχειριστής;

* **Έλεγχος** – Εσείς αποφασίζετε ακριβώς από πού προέρχεται κάθε asset (classpath, βάση δεδομένων, κρυπτογραφημένη αποθήκευση).  
* **Ασφάλεια** – Δεν γίνονται τυχαίες εξωτερικές κλήσεις HTTP σε μη αξιόπιστους τομείς.  
* **Φορητότητα** – Το παραγόμενο JAR είναι αυτόνομο· μετακινήστε το σε άλλο διακομιστή και οι εικόνες παραμένουν.

---

## Βήμα 4: Εκτελέστε τη μετατροπή και επαληθεύστε το αποτέλεσμα

Συγκεντρώστε και τρέξτε την κλάση:

```bash
mvn clean compile exec:java -Dexec.mainClass=CustomResourceHandler
```

Αν όλα είναι σωστά συνδεδεμένα, θα δείτε το μήνυμα `Conversion completed – images embedded!` στην κονσόλα, και το `output/page.pdf` θα περιέχει την εικόνα λογότυπου ακριβώς εκεί που τοποθετήθηκε η ετικέτα `<img>`.

### Αναμενόμενη προβολή PDF

Ανοίξτε το PDF· θα πρέπει να δείτε:

* Τον τίτλο **«Welcome!»**  
* Την παράγραφο **«This page shows how to embed images.»**  
* Το **logo.png** να εμφανίζεται κάτω από το κείμενο.

Αν η εικόνα λείπει, ελέγξτε ξανά τη διαδρομή πόρου (`/myresources/logo.png`) και βεβαιωθείτε ότι το αρχείο περιλαμβάνεται στο τελικό JAR (εκτελέστε `jar tf target/your‑app.jar | grep logo.png`).

---

## Βήμα 5: Διαχείριση πολλαπλών assets και ειδικές περιπτώσεις

### Πολλαπλές εικόνες

Αν έχετε πολλές εικόνες, επεκτείνετε το `if` block ή χρησιμοποιήστε ένα `Map<String, String>` που αντιστοιχεί URLs σε θέσεις classpath:

```java
Map<String, String> assetMap = Map.of(
        "logo.png", "/myresources/logo.png",
        "banner.jpg", "/myresources/banner.jpg"
);
```

Στη συνέχεια μέσα στη μέθοδο `getResource`:

```java
String path = assetMap.get(url.substring(url.lastIndexOf('/') + 1));
return path != null ? getClass().getResourceAsStream(path) : null;
```

### Ελλιπείς πόροι

Επιστρέφοντας `null` λέτε στο Aspose να επανέλθει στον προεπιλεγμένο φορτωτή του. Αν θέλετε **ευγενική εναλλακτική** (π.χ., μια placeholder εικόνα), επιστρέψτε ένα stream σε μια προεπιλεγμένη εικόνα αντί για `null`.

### Μεγάλα αρχεία

Για πολύ μεγάλα assets (υψηλής ανάλυσης φωτογραφίες), σκεφτείτε να ρέετε τα δεδομένα σε τμήματα ή να χρησιμοποιήσετε προσωρινό αρχείο ώστε να μην φορτώνετε ολόκληρη την εικόνα στη μνήμη.

---

## Βήμα 6: Συμβουλές για μια ομαλή εμπειρία **aspose html to pdf**

* **Ορίστε base URL** – Αν το HTML σας χρησιμοποιεί σχετικές διαδρομές, καλέστε `loadOptions.setBaseUrl("file:///absolute/path/")` ώστε η μηχανή να τις επιλύει σωστά.  
* **Ενεργοποιήστε caching** – `loadOptions.setCacheEnabled(true)` επιταχύνει επαναλαμβανόμενες μετατροπές των ίδιων assets.  
* **Ασφάλεια νήματος** – Η παρουσίαση `ResourceHandler` μπορεί να μοιραστεί μεταξύ νημάτων, αλλά βεβαιωθείτε ότι τυχόν κατάσταση που διατηρείτε είναι μόνο για ανάγνωση ή σωστά συγχρονισμένη.  
* **Καταγραφή** – Ενεργοποιήστε τη διάγνωση του Aspose (`System.setProperty("aspose.html.logging", "true")`) για να δείτε ποιοι πόροι ζητούνται· αυτό βοηθά στον εντοπισμό ελλιπών εικόνων.

---

## Βήμα 7: Πλήρες, εκτελέσιμο παράδειγμα (όλα σε ένα αρχείο)

Παρακάτω βρίσκεται ο πλήρης κώδικας που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε ένα μόνο `CustomResourceHandler.java`. Περιλαμβάνει τις εισαγωγές, τον διαχειριστή, και την κλήση μετατροπής—όλα έτοιμα για μεταγλώττιση.

```java
import com.aspose.html.*;
import com.aspose.html.loading.*;

import java.io.InputStream;
import java.util.Map;

public class CustomResourceHandler {
    public static void main(String[] args) throws Exception {

        // ------------------------------------------------------------
        // 1️⃣  Configure load options with a custom resource handler
        // ------------------------------------------------------------
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();

        // Map of URL file names to classpath resource locations
        Map<String, String> assetMap = Map.of(
                "logo.png", "/myresources/logo.png",
                "banner.jpg", "/myresources/banner.jpg"
        );

        loadOptions.setResourceHandler(new ResourceHandler() {
            @Override
            public InputStream getResource(String url) {
                // Extract the file name from the URL
                String fileName = url.substring(url.lastIndexOf('/') + 1);
                String classpath = assetMap.get(fileName);
                if (classpath != null) {
                    // Return the image stream from inside the JAR
                    return getClass().getResourceAsStream(classpath);
                }
                // No mapping – let Aspose handle it (network, file system, etc.)
                return null;
            }
        });

        // ------------------------------------------------------------
        // 2️⃣  Perform the conversion – HTML → PDF
        // ------------------------------------------------------------
        Converter.convertDocument(
                "src/main/resources/page-with-assets.html", // input HTML
                "output/page.pdf",                          // output PDF
                new PdfSaveOptions(),                       // default PDF options
                loadOptions                                 // our custom loader
        );

        System.out.println("Conversion completed – images embedded!");
    }
}
```

Τρέξτε το, ανοίξτε το `output/page.pdf`, και θα δείτε τις ενσωματωμένες εικόνες ακριβώς εκεί που τις περιμένατε.

---

## Συμπέρασμα

Μόλις καλύψαμε **πώς να ενσωματώσετε εικόνες** κατά τη διάρκεια μιας λειτουργίας **convert html to pdf** χρησιμοποιώντας το Aspose HTML for Java. Εκμεταλλευόμενοι έναν **προσαρμοσμένο διαχειριστή πόρων**, αποκτάτε πλήρη έλεγχο στην επίλυση των assets, καθιστώντας τη δημιουργία PDF αξιόπιστη, ασφαλή και πλήρως φορητή.  

Αν νιώθετε άνετα με αυτή τη ρύθμιση, τα επόμενα λογικά βήματα είναι:

* Πειραματιστείτε με επιλογές **aspose html to pdf** (π.χ., μέγεθος σελίδας, συμπίεση).  
* Αντικαταστήστε την πηγή εικόνας με ένα **BLOB βάσης δεδομένων** για να κρατήσετε τα assets εκτός του συστήματος αρχείων.  
* Συνδυάστε αυτήν την τεχνική με **java html to pdf** επεξεργασία παρτίδας για μεγάλα σύνολα εγγράφων.  

Καλή προγραμματιστική δουλειά, και ας είναι τα PDF σας πάντα όπως τα σχεδιάσατε!

---  

![πώς να ενσωματώσετε εικόνες παράδειγμα](placeholder.png "πώς να ενσωματώσετε εικόνες σε μετατροπή PDF")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}