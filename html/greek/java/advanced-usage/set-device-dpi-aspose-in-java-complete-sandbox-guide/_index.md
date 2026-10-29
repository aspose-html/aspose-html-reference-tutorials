---
category: general
date: 2026-06-16
description: Μάθετε πώς να ορίσετε το DPI της συσκευής στο Aspose και να καθορίσετε
  το πλάτος και το ύψος του viewport κατά την απόδοση HTML με το Aspose.HTML sandbox
  σε Java. Περιλαμβάνεται κώδικας βήμα‑βήμα.
draft: false
keywords:
- set device dpi aspose
- set viewport width height
language: el
og_description: Ανακαλύψτε πώς να ορίσετε το DPI της συσκευής με το Aspose και να
  ρυθμίσετε το πλάτος και το ύψος του viewport χρησιμοποιώντας το Aspose.HTML sandbox
  για Java. Πλήρης κώδικας και εξήγηση.
og_title: Ορισμός DPI συσκευής Aspose σε Java – Πλήρης Οδηγός Sandbox
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to set device dpi aspose and set viewport width height when
    rendering HTML with Aspose.HTML sandbox in Java. Step‑by‑step code included.
  headline: set device dpi aspose in Java – Complete Sandbox Guide
  type: TechArticle
- description: Learn how to set device dpi aspose and set viewport width height when
    rendering HTML with Aspose.HTML sandbox in Java. Step‑by‑step code included.
  name: set device dpi aspose in Java – Complete Sandbox Guide
  steps:
  - name: Configure sandbox options (including DPI and viewport size).
    text: Configure sandbox options (including DPI and viewport size).
  - name: Instantiate a `DocumentSandbox` with those options.
    text: Instantiate a `DocumentSandbox` with those options.
  - name: Load an external HTML page inside the sandbox.
    text: Load an external HTML page inside the sandbox.
  - name: Perform a simple DOM operation—printing the page title.
    text: Perform a simple DOM operation—printing the page title.
  type: HowTo
tags:
- Aspose.HTML
- Java
- HTML rendering
- Sandbox
title: Ορισμός DPI συσκευής Aspose σε Java – Πλήρης Οδηγός Sandbox
url: /el/java/advanced-usage/set-device-dpi-aspose-in-java-complete-sandbox-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ορισμός dpi συσκευής aspose – Java Sandbox Tutorial

Έχετε αναρωτηθεί ποτέ πώς να **ορίσετε το dpi της συσκευής aspose** κατά την απόδοση μιας ιστοσελίδας σε Java; Δεν είστε οι μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν χρειάζεται η αποδοθείσα σελίδα να φαίνεται ακριβώς όπως θα έδειχνε σε πραγματική οθόνη—ιδιαίτερα όταν το DPI επηρεάζει τους υπολογισμούς διάταξης.  

Σε αυτόν τον οδηγό θα σας καθοδηγήσουμε βήμα‑βήμα μέσα από ένα πρακτικό παράδειγμα που όχι μόνο **ορίζει το dpi της συσκευής aspose**, αλλά δείχνει επίσης πώς να **ορίσετε το πλάτος και το ύψος του viewport** ώστε η σελίδα να συμπεριφέρεται όπως σε παράθυρο περιηγητή 1280 × 800 pixel. Στο τέλος θα έχετε ένα εκτελέσιμο απόσπασμα, μια σαφή εξήγηση κάθε βήματος και συμβουλές για την αποφυγή κοινών παγίδων.

## Τι Καλύπτει Αυτό το Tutorial

Θα ξεκινήσουμε με τις προαπαιτούμενες ρυθμίσεις, μετά θα προχωρήσουμε σε τέσσερα σύντομα βήματα:

1. Διαμόρφωση επιλογών sandbox (συμπεριλαμβανομένου DPI και μεγέθους viewport).  
2. Δημιουργία ενός `DocumentSandbox` με αυτές τις επιλογές.  
3. Φόρτωση εξωτερικής HTML σελίδας μέσα στο sandbox.  
4. Εκτέλεση μιας απλής λειτουργίας DOM—εκτύπωση του τίτλου της σελίδας.

Θα δείτε γιατί κάθε στοιχείο είναι σημαντικό, πώς να προσαρμόσετε τις ρυθμίσεις για διαφορετικές συσκευές και πώς θα πρέπει να φαίνεται η έξοδος. Δεν χρειάζεται εξωτερική τεκμηρίωση· όλα όσα χρειάζεστε είναι εδώ.

## Προαπαιτούμενα

- Java 8 ή νεότερη (η βιβλιοθήκη Aspose.HTML for Java υποστηρίζει JDK 8+).  
- Aspose.HTML for Java JARs προστεμένα στο classpath του έργου σας.  
- Ένα IDE ή εργαλείο κατασκευής (Maven/Gradle) για να μεταγλωττίσετε και να εκτελέσετε τον κώδικα.  
- Πρόσβαση στο Internet αν σκοπεύετε να φορτώσετε μια ζωντανή διεύθυνση όπως `https://example.com`.

Αν έχετε όλα τα παραπάνω, ας ξεκινήσουμε.

## Βήμα 1: Ορισμός DPI Συσκευής aspose – Καθορισμός Sandbox Options

Το πρώτο που πρέπει να κάνετε είναι να πείτε στο sandbox ποια «οθόνη» προσποιείστε. Εδώ έρχεται η **ορισμός dpi συσκευής aspose**. Το DPI (dots per inch) επηρεάζει τον τρόπο ερμηνείας των μονάδων CSS `px`, κάτι που μπορεί να αλλάξει τα μεγέθη γραμματοσειρών, την κλιμάκωση εικόνων και τα media queries.

```java
// Step 1: Create sandbox options and configure DPI and viewport.
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setDeviceDpi(96);               // set device dpi aspose
sandboxOptions.setViewportWidth(1280);         // set viewport width height
sandboxOptions.setViewportHeight(800);         // set viewport width height
```

> **Γιατί είναι σημαντικό:**  
> *Η κλήση `setDeviceDpi` λέει στο Aspose.HTML να θεωρεί ένα CSS pixel ως 1/96 ίντσας, προσομοιώνοντας τα περισσότερα desktop monitors. Αν παραλείψετε αυτό, η διάταξη μπορεί να εμφανιστεί πολύ μικρή ή πολύ μεγάλη σε οθόνες υψηλού DPI.*

## Βήμα 2: Δημιουργία του Sandbox με τις Διαμορφωμένες Επιλογές

Τώρα που οι επιλογές είναι έτοιμες, χρειάζεστε μια παρουσία sandbox που τις σέβεται. Σκεφτείτε το sandbox ως έναν μικρό, απομονωμένο κινητήρα περιηγητή που δεν θα αγγίξει το σύστημα αρχείων σας.

```java
// Step 2: Initialise the DocumentSandbox using the options above.
DocumentSandbox documentSandbox = new DocumentSandbox(sandboxOptions);
```

> **Pro tip:**  
> Η επαναχρησιμοποίηση του ίδιου `DocumentSandbox` για πολλές σελίδες εξοικονομεί μνήμη, αλλά θυμηθείτε να επαναρυθμίσετε τις επιλογές αν χρειαστεί διαφορετικό DPI ή viewport αργότερα.

## Βήμα 3: Φόρτωση HTML Εγγράφου Μέσα στο Sandbox

Με το sandbox στη θέση του, η φόρτωση μιας σελίδας είναι απλή. Ο κατασκευαστής του `HTMLDocument` δέχεται τη διεύθυνση URL και το sandbox που μόλις δημιουργήσατε.

```java
// Step 3: Load a remote HTML page using the sandbox.
HTMLDocument htmlDoc = new HTMLDocument("https://example.com", documentSandbox);
```

> **Edge case:**  
> Αν ο στόχος ιστότοπος μπλοκάρει αυτοματοποιημένα αιτήματα, μπορεί να λάβετε σφάλμα 403. Σε αυτήν την περίπτωση, είτε κατεβάστε το HTML τοπικά και φορτώστε το από διαδρομή αρχείου, είτε ορίστε μια προσαρμοσμένη συμβολοσειρά user‑agent μέσω `sandboxOptions`.

## Βήμα 4: Εκτέλεση Κανονικών Λειτουργιών DOM – Εκτύπωση Τίτλου Σελίδας

Σε αυτό το σημείο η σελίδα έχει αποδοθεί πλήρως μέσα στο sandbox, οπότε οποιοδήποτε ερώτημα DOM λειτουργεί ακριβώς όπως σε πλήρη περιηγητή. Ας το κρατήσουμε απλό και ας πάρουμε τον τίτλο.

```java
// Step 4: Access the DOM – print the page title.
System.out.println("Title: " + htmlDoc.getTitle());
```

**Αναμενόμενη έξοδος**

```
Title: Example Domain
```

Αν δείτε κάτι διαφορετικό, ελέγξτε ξανά ότι η URL είναι προσβάσιμη και ότι δεν αλλάξατε κατά λάθος τις τιμές DPI ή viewport.

## Γιατί η Ρύθμιση Viewport Width Height Είναι Καίρια

Μπορεί να αναρωτιέστε, “Γιατί **ορίζουμε το πλάτος και το ύψος του viewport**;” Η απάντηση κρύβεται στο responsive design. Τα media queries όπως `@media (max-width: 600px)` αντιδρούν στις διαστάσεις του viewport, όχι στο φυσικό μέγεθος της οθόνης. Ορίζοντας `1280` × `800`, εξασφαλίζετε ότι η σελίδα αποδίδει τη «desktop» διάταξη, ακόμη και αν τρέχετε τον κώδικα σε headless server χωρίς οθόνη.

```java
sandboxOptions.setViewportWidth(1280);   // set viewport width height
sandboxOptions.setViewportHeight(800);   // set viewport width height
```

Αλλάζοντας αυτούς τους αριθμούς μπορείτε να προσομοιώσετε tablets, smartphones ή ακόμη και ultra‑wide monitors χωρίς να βγείτε από το IDE σας.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται η πλήρης, έτοιμη για εκτέλεση κλάση Java που ενώνει όλα τα παραπάνω. Αντιγράψτε‑και‑επικολλήστε το σε ένα αρχείο με όνομα `SandboxExample.java`, προσθέστε τα Aspose.HTML JARs στο classpath και τρέξτε `javac SandboxExample.java && java SandboxExample`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.sandbox.SandboxOptions;

public class SandboxExample {
    public static void main(String[] args) {
        // Step 1: Define sandbox options – set device DPI and viewport.
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setDeviceDpi(96);               // set device dpi aspose
        sandboxOptions.setViewportWidth(1280);         // set viewport width height
        sandboxOptions.setViewportHeight(800);         // set viewport width height

        // Step 2: Create a DocumentSandbox using the defined options.
        DocumentSandbox documentSandbox = new DocumentSandbox(sandboxOptions);

        // Step 3: Load an HTML document inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com", documentSandbox);

        // Step 4: Perform normal DOM operations – print the page title.
        System.out.println("Title: " + htmlDoc.getTitle());
    }
}
```

> **Γρήγορη επαλήθευση:**  
> Εκτελέστε το πρόγραμμα. Αν δείτε `Title: Example Domain`, όλα είναι σωστά συνδεδεμένα. Αν όχι, ελέγξτε την κονσόλα για εξαιρέσεις—τα περισσότερα προβλήματα προέρχονται από ελλιπή JARs ή περιορισμούς δικτύου.

## Συνηθισμένες Παγίδες & Πώς να τις Αποφύγετε

| Συμπτωμα | Πιθανή Αιτία | Διόρθωση |
|---|---|---|
| `NullPointerException` στο `htmlDoc.getTitle()` | Το sandbox δεν μπόρεσε να φορτώσει τη σελίδα | Επαληθεύστε τη URL, προσθέστε try‑catch γύρω από τον κατασκευαστή `HTMLDocument`, ή ενεργοποιήστε logging μέσω `sandboxOptions.setLogLevel(...)`. |
| Η διάταξη φαίνεται ζουμμένη | DPI δεν έχει οριστεί σωστά | Βεβαιωθείτε ότι `sandboxOptions.setDeviceDpi(96)` (ή το επιθυμητό DPI). |
| Τα media queries δεν ενεργοποιούνται ποτέ | Λείπουν διαστάσεις viewport | Ελέγξτε ότι κάλεσατε και `setViewportWidth` **και** `setViewportHeight`. |
| Σφάλμα out‑of‑memory σε μεγάλες σελίδες | Επαναχρησιμοποίηση ενός sandbox για πολλές βαριές σελίδες | Δημιουργήστε νέο `DocumentSandbox` ανά σελίδα ή καλέστε `documentSandbox.dispose()` μετά τη χρήση. |

## Επέκταση του Παραδείγματος

Τώρα που ξέρετε πώς να **ορίσετε το dpi της συσκευής aspose** και **να ορίσετε το πλάτος και το ύψος του viewport**, μπορείτε να πειραματιστείτε περαιτέρω:

- **Καταγραφή screenshot** της αποδοθείσας σελίδας με `htmlDoc.renderToBitmap(...)`.  
- **Ένθεση προσαρμοσμένου CSS** πριν την απόδοση για δοκιμή θεμάτων dark‑mode.  
- **Εκτέλεση JavaScript** μέσα στο sandbox με `htmlDoc.getWindow().eval(...)`.  

Όλες αυτές οι ενέργειες σέβονται το DPI και το viewport που διαμορφώσατε, προσφέροντας ένα αξιόπιστο περιβάλλον δοκιμών για responsive διατάξεις.

## Συμπέρασμα

Διασχίσαμε μια σύντομη, ολοκληρωμένη λύση που δείχνει πώς να **ορίσετε το dpi της συσκευής aspose** και **να ορίσετε το πλάτος και το ύψος του viewport** χρησιμοποιώντας το sandbox του Aspose.HTML σε Java. Τώρα έχετε μια σταθερή βάση για την απόδοση σελίδων ακριβώς όπως θα εμφανίζονταν σε οποιαδήποτε συσκευή, όλα μέσα σε ασφαλές, απομονωμένο περιβάλλον.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να αποδώσετε μια σελίδα που χρησιμοποιεί CSS grid layout, ή φορτώστε ένα απομακρυσμένο stylesheet και δείτε πώς το DPI επηρεάζει την απόδοση των γραμματοσειρών. Το sandbox σας δίνει την ελευθερία να πειραματιστείτε χωρίς να επηρεάσετε το σύστημα υποδοχής.

Αν αντιμετωπίσετε δυσκολίες, αφήστε ένα σχόλιο παρακάτω ή ελέγξτε την τεκμηρίωση Aspose.HTML for Java—αν και όλα όσα χρειάζεστε είναι ήδη εδώ. Καλή κωδικοποίηση!  

![set device dpi aspose sandbox diagram](https://example.com/images/set-device-dpi-aspose.png "Diagram showing DPI and viewport configuration in Aspose.HTML sandbox")


## Τι Πρέπει να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Create PDF from HTML using Aspose.HTML for Java – Sandbox](/html/english/java/configuring-environment/implement-sandboxing/)
- [Create PDF from HTML – Set User Style Sheet in Aspose.HTML for Java](/html/english/java/configuring-environment/set-user-style-sheet/)
- [How to Set Charset in Aspose.HTML for Java](/html/english/java/configuring-environment/set-character-set/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}