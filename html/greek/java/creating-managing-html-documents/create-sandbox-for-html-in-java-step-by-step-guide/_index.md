---
category: general
date: 2026-04-12
description: Μάθετε πώς να αποκλείετε το HTML στη Java δημιουργώντας ένα sandbox,
  ανοίγοντας ένα αρχείο HTML με ασφάλεια και ανακτώντας τον τίτλο της σελίδας. Παράδειγμα
  κώδικα βήμα‑προς‑βήμα.
draft: false
keywords:
- how to block html
- open html file sandbox
- retrieve html title java
og_description: Μάθετε πώς να αποκλείετε το HTML σε Java χρησιμοποιώντας το sandbox
  του Aspose.HTML, να ανοίγετε αρχεία HTML με ασφάλεια και να εξάγετε τον τίτλο.
og_title: Πώς να αποκλείσετε το HTML στη Java – Πλήρης οδηγός
tags:
- Java
- Aspose.HTML
- Sandbox
- HTML Processing
title: Πώς να αποκλείσετε το HTML στην Java – Δημιουργήστε sandbox και ανακτήστε τον
  τίτλο
url: /el/java/creating-managing-html-documents/create-sandbox-for-html-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αποκλείσετε το HTML στη Java – Πλήρες Εγχειρίδιο

Αν έχετε χρειαστεί ποτέ **πώς να αποκλείσετε το HTML** κατά την επεξεργασία σελίδων τρίτων σε μια εφαρμογή Java, γνωρίζετε τον πόνο από ανεπιθύμητες κλήσεις δικτύου και εκτέλεση σεναρίων. Σε αυτό το εγχειρίδιο θα σας δείξουμε ακριβώς πώς να δημιουργήσετε ένα sandbox, **ανοίγοντας αρχείο HTML σε sandbox** με ασφάλεια, και **να ανακτήσετε τον τίτλο HTML Java** χωρίς να επιτρέψετε σε εξωτερικούς πόρους να διαρρεύσουν. Τα βήματα είναι σύντομα, ο κώδικας είναι έτοιμος‑για‑εκτέλεση, και θα καταλάβετε γιατί κάθε ρύθμιση είναι σημαντική.

## Γρήγορες Απαντήσεις
- **Πώς μπορώ να αποκλείσω το HTML από τη φόρτωση εξωτερικών πόρων;** Ορίστε `setEnableNetworkAccess(false)` στο `SandboxOptions`.  
- **Ποια βιβλιοθήκη διαχειρίζεται το sandboxing στη Java;** Το Aspose.HTML for Java παρέχει ενσωματωμένη κλάση `Sandbox`.  
- **Χρειάζομαι Maven για να χρησιμοποιήσω αυτόν τον κώδικα;** Όχι, απλώς προσθέστε το JAR του Aspose.HTML στο classpath σας.  
- **Μπορώ ακόμη να εκτελέσω JavaScript μέσα στο sandbox;** Ναι, αλλά πρέπει να το ενεργοποιήσετε ρητά και να διαχειριστείτε τις δικαιοδοσίες δικτύου.  
- **Ποιο είναι το αποτέλεσμα μετά την εκτέλεση της επίδειξης;** Δύο γραμμές: ένα μήνυμα επιτυχίας και ο τίτλος της σελίδας που εξήχθη από την ετικέτα `<title>`.

## Τι Θα Αποκομίσετε

Θα καλύψουμε τα πάντα, από τη ρύθμιση των επιλογών sandbox μέχρι την εκτύπωση του τίτλου του εγγράφου. Στο τέλος θα γνωρίζετε:

* Γιατί ένα sandbox είναι απαραίτητο όταν επεξεργάζεστε HTML τρίτων.  
* Πώς να ρυθμίσετε τις διαστάσεις της οθόνης και να απενεργοποιήσετε την πρόσβαση δικτύου.  
* Τον ακριβή κώδικα Java που ανοίγει ένα αρχείο HTML μέσα στο sandbox.  
* Πώς να διαβάσετε την ετικέτα τίτλου με ασφάλεια, ακόμη και αν η σελίδα προσπαθεί να φορτώσει εξωτερικά σενάρια.

**Προαπαιτούμενα;** Απλώς ένα πρόσφατο JDK (8 ή νεότερο) και η βιβλιοθήκη Aspose.HTML for Java στο classpath σας. Δεν απαιτείται Maven, αλλά αν το χρησιμοποιείτε απλώς προσθέστε την εξάρτηση Aspose και είστε έτοιμοι.

## Πώς να αποκλείσετε το HTML στη Java; – Διαμόρφωση του Περιβάλλοντος Sandbox

Πριν μπορέσουμε να φορτώσουμε οποιοδήποτε έγγραφο, χρειαζόμαστε ένα sandbox που να μιμείται ένα παράθυρο περιήγησης αλλά να αρνείται την επικοινωνία με τον έξω κόσμο. Σκεφτείτε το ως έναν περιφραγμένο κήπο όπου το παιδί (το HTML σας) μπορεί να παίξει, αλλά η πύλη είναι κλειδωμένη.

```java
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;

// Step 1: Define sandbox options – screen size and network policy
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(1280);               // width in pixels
sandboxOptions.setScreenHeight(800);               // height in pixels
sandboxOptions.setEnableNetworkAccess(false);      // blocks all remote resources

// Pro tip: you can also set a custom user‑agent string here if needed.
```

**Γιατί είναι σημαντικό:**  
Ορίζοντας `setEnableNetworkAccess(false)` εξασφαλίζετε ότι οποιοδήποτε `<script src="…">`, `<img src="…">` ή εισαγωγή CSS δεν θα φτάσει στο διαδίκτυο. Αυτό αποτελεί τον πυρήνα του **πώς να αποκλείσετε το HTML**—παίρνετε απομόνωση χωρίς να θυσιάζετε την πιστότητα της απόδοσης.

## Άνοιγμα αρχείου HTML σε sandbox – Φόρτωση του εγγράφου με ασφάλεια

Τώρα που το sandbox είναι έτοιμο, μπορούμε να τοποθετήσουμε το αρχείο HTML μέσα του. Η μέθοδος `Sandbox.open()` επιστρέφει ένα `HTMLDocument` που ζει εξ ολοκλήρου μέσα στο περιφραγμένο περιβάλλον.

```java
import com.aspose.html.HTMLDocument;

try (Sandbox sandbox = new Sandbox(sandboxOptions)) {
    // Step 2: Open the HTML file inside the sandbox
    // Replace YOUR_DIRECTORY/complex.html with the actual path to your file.
    HTMLDocument htmlDoc = sandbox.open("YOUR_DIRECTORY/complex.html");

    // At this point the document is parsed, but no network calls were made.
    System.out.println("Document loaded successfully inside sandbox.");
}
catch (Exception e) {
    // Handle errors such as file not found or parsing issues.
    System.err.println("Failed to open HTML file sandbox: " + e.getMessage());
}
```

**Συχνή ερώτηση:** *Τι γίνεται αν το αρχείο δεν υπάρχει;*  
Το μπλοκ `try‑with‑resources` κλείνει αυτόματα το sandbox, και η ενότητα `catch` θα σας δώσει ένα σαφές μήνυμα σφάλματος. Μπορείτε επίσης να προεπαληθεύσετε τη διαδρομή με `Files.exists()` αν προτιμάτε.

## Ανάκτηση τίτλου HTML Java – Εξαγωγή της ετικέτας `<title>`

Με το έγγραφο φορτωμένο με ασφάλεια, η λήψη του τίτλου της σελίδας είναι παιχνιδάκι. Η μέθοδος `HTMLDocument.getTitle()` διαβάζει το στοιχείο `<title>` από το DOM, χωρίς να λαμβάνει υπόψη τους εξωτερικούς πόρους που έχουν αποκλειστεί.

```java
// Continuing inside the try block from Step 2
String pageTitle = htmlDoc.getTitle();
System.out.println("Title inside sandbox: " + pageTitle);
```

**Αναμενόμενο αποτέλεσμα** (υποθέτοντας ότι το αρχείο HTML περιέχει `<title>My Complex Page</title>`):

```
Document loaded successfully inside sandbox.
Title inside sandbox: My Complex Page
```

Αν το HTML δεν περιέχει ετικέτα `<title>`, το `getTitle()` επιστρέφει απλώς μια κενή συμβολοσειρά—δεν ρίχνεται εξαίρεση. Αυτό κάνει το **retrieve HTML title Java** μια ασφαλή λειτουργία ακόμη και σε κατεστραμμένες σελίδες.

## Πλήρες, Εκτελέσιμο Παράδειγμα

Συνδυάζοντας τα παραπάνω, εδώ είναι μια αυτόνομη κλάση Java που μπορείτε να μεταγλωττίσετε και να τρέξετε αμέσως. Θυμηθείτε να αντικαταστήσετε το `YOUR_DIRECTORY/complex.html` με την πραγματική διαδρομή του αρχείου δοκιμής σας.

```java
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.HTMLDocument;

public class SandboxDemo {
    public static main(String[] args) {
        // 1️⃣ Configure sandbox options
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(1280);
        sandboxOptions.setScreenHeight(800);
        sandboxOptions.setEnableNetworkAccess(false); // blocks remote resources

        // 2️⃣ Create sandbox and open HTML file
        try (Sandbox sandbox = new Sandbox(sandboxOptions)) {
            HTMLDocument htmlDoc = sandbox.open("YOUR_DIRECTORY/complex.html");

            // 3️⃣ Retrieve and display the title
            String title = htmlDoc.getTitle();
            System.out.println("Title inside sandbox: " + title);
        } catch (Exception e) {
            System.err.println("Error during sandbox operation: " + e.getMessage());
        }
    }
}
```

**Εκτέλεση της επίδειξης:**  

```bash
javac -cp "path/to/aspose-html.jar" SandboxDemo.java
java -cp ".:path/to/aspose-html.jar" SandboxDemo
```

Θα πρέπει να δείτε το αποτέλεσμα δύο γραμμών που εμφανίστηκε νωρίτερα, επιβεβαιώνοντας ότι έχετε δημιουργήσει **sandbox for HTML**, **ανοίξει αρχείο HTML σε sandbox**, και **ανακτήσει τον τίτλο HTML Java** με επιτυχία.

## Συμβουλές, Ακραίες Περιπτώσεις και Καλές Πρακτικές

* **Πολλές σελίδες;** Αν χρειάζεται να επεξεργαστείτε πολλά αρχεία HTML, επαναχρησιμοποιήστε την ίδια παρουσία `Sandbox`—απλώς καλέστε `open()` επανειλημμένα. Το sandbox παραμένει απομονωμένο για κάθε κλήση.  
* **Δυναμικό περιεχόμενο;** Για σελίδες που εξαρτώνται από JavaScript για τον καθορισμό του τίτλου, θα πρέπει να ενεργοποιήσετε την εκτέλεση σεναρίων (`sandboxOptions.setEnableScript(true)`). Θυμηθείτε ότι η ενεργοποίηση των σεναρίων ανοίγει επίσης την πόρτα για κλήσεις δικτύου, οπότε ίσως θελήσετε να προσθέσετε λευκή λίστα συγκεκριμένων domain αντί να απενεργοποιήσετε πλήρως την πρόσβαση δικτύου.  
* **Μεγάλα αρχεία;** Το sandbox κρατά ολόκληρο το DOM στη μνήμη. Για τεράστια έγγραφα, σκεφτείτε τη ροή του αρχείου και την εξαγωγή του `<title>` με έναν ελαφρύ parser πριν το φορτώσετε στο sandbox.  
* **Καταγραφή:** Το Aspose.HTML μπορεί να εκδώσει λεπτομερή logs μέσω `System.setProperty("aspose.html.logging", "true")`. Χρήσιμο όταν προσπαθείτε να εντοπίσετε γιατί ένας συγκεκριμένος πόρος αποκλείστηκε.

## Συχνές Ερωτήσεις

**Ε: Μπορώ να αποκλείσω όλους τους εξωτερικούς πόρους ενώ επιτρέπω τα ενσωματωμένα σενάρια;**  
Α: Ναι. Διατηρήστε `setEnableNetworkAccess(false)` και ορίστε `setEnableScript(true)` για να επιτρέψετε ενσωματωμένο JavaScript αλλά να αποτρέψετε οποιεσδήποτε δικτυακές κλήσεις.

**Ε: Τι συμβαίνει αν το HTML προσπαθήσει να φορτώσει ένα αρχείο CSS από το διαδίκτυο;**  
Α: Η αίτηση αποκλείεται από το sandbox και το CSS αγνοείται, αφήνοντας τη διάταξη του εγγράφου να βασίζεται στα διαθέσιμα στυλ.

**Ε: Είναι το sandbox thread‑safe;**  
Α: Μία μόνο παρουσία `Sandbox` δεν είναι thread‑safe. Δημιουργήστε ξεχωριστό sandbox ανά νήμα ή συγχρονίστε την πρόσβαση αν χρειάζεστε ταυτόχρονη επεξεργασία.

**Ε: Χρειάζομαι άδεια για το Aspose.HTML στην ανάπτυξη;**  
Α: Μια δωρεάν άδεια αξιολόγησης λειτουργεί για ανάπτυξη και δοκιμές. Απαιτείται εμπορική άδεια για παραγωγικές εγκαταστάσεις.

**Ε: Πώς μπορώ να συλλάβω σφάλματα που προκύπτουν κατά την ανάλυση;**  
Α: Τυλίξτε την κλήση `sandbox.open()` σε μπλοκ `try‑catch` όπως φαίνεται· το μήνυμα της εξαίρεσης θα περιέχει λεπτομέρειες ανάλυσης.

---

**Τελευταία ενημέρωση:** 2026-04-12  
**Δοκιμάστηκε με:** Aspose.HTML for Java 24.11  
**Συγγραφέας:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}