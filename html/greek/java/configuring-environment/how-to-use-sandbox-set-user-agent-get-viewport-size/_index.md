---
category: general
date: 2026-04-03
description: Μάθετε πώς να χρησιμοποιείτε το sandbox στο Aspose.HTML Java για να ορίσετε
  τον πράκτορα χρήστη, το μέγεθος και να λαμβάνετε άμεσα το μέγεθος του viewport.
  Περιλαμβάνονται πλήρης κώδικας, επεξηγήσεις και συμβουλές.
draft: false
keywords:
- how to use sandbox
- set user agent
- get viewport size
- how to set size
- how to get viewport
language: el
og_description: Μάθετε πώς να χρησιμοποιείτε το sandbox στο Aspose.HTML Java για να
  ορίσετε τον πράκτορα χρήστη, το μέγεθος και να λάβετε αμέσως το μέγεθος του παραθύρου
  προβολής. Πλήρης οδηγός με κώδικα και βέλτιστες πρακτικές.
og_title: Πώς να χρησιμοποιήσετε το Sandbox – Ορίστε τον User Agent & Λάβετε το μέγεθος
  του Viewport
tags:
- AsposeHTML
- Java
- Sandbox
title: Πώς να χρησιμοποιήσετε το Sandbox – Ορίστε τον πράκτορα χρήστη & Λάβετε το
  μέγεθος της περιοχής προβολής
url: /el/java/configuring-environment/how-to-use-sandbox-set-user-agent-get-viewport-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε το Sandbox – Ορίστε User Agent & Λάβετε το Μέγεθος του Viewport

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε το sandbox** όταν αποδίδετε HTML με Aspose.HTML for Java; Ίσως έχετε συναντήσει δυσκολίες στο να προσομοιώσετε ένα συγκεκριμένο μέγεθος οθόνης ή χρειάζεται να ψεύσετε μια συμβολοσειρά user‑agent ώστε η σελίδα να συμπεριφέρεται σαν να επισκέπτεται ένας κινητός περιηγητής.  

Το καλό νέο είναι ότι το sandbox API σας επιτρέπει ακριβώς αυτό, και μπορείτε επίσης να λάβετε το υπολογισμένο μέγεθος του viewport μετά τη φόρτωση της σελίδας. Σε αυτό το tutorial θα περάσουμε από τη δημιουργία ενός sandbox, τον ορισμό του μεγέθους, τον ορισμό προσαρμοσμένου user agent, τη φόρτωση μιας απομακρυσμένης σελίδας και, τέλος, την ανάγνωση των διαστάσεων του viewport. Στο τέλος θα γνωρίζετε **πώς να ορίσετε το μέγεθος**, **πώς να λάβετε το viewport**, και γιατί αυτά τα βήματα είναι σημαντικά για αξιόπιστη headless απόδοση.

> **Γρήγορο αποτέλεσμα:** θα έχετε μια εκτελέσιμη κλάση Java που εκτυπώνει κάτι όπως `Viewport: 1280×800` σε δευτερόλεπτα.

---

## Τι Θα Χρειαστείτε

- **Aspose.HTML for Java** έκδοση 24.6 ή νεότερη (το API που χρησιμοποιούμε εισήχθη στην 24.5).  
- Ένα Java 17+ development kit (οποιοδήποτε πρόσφατο JDK λειτουργεί).  
- Ένα IDE ή έναν απλό επεξεργαστή κειμένου — δεν απαιτούνται ειδικά πρόσθετα.  
- Πρόσβαση στο Internet αν θέλετε να φορτώσετε μια εξωτερική URL όπως `https://example.com`.

Αυτό είναι όλο. Δεν είναι υποχρεωτικό το Maven/Gradle wizardry· μπορείτε να τοποθετήσετε τα JARs στο classpath χειροκίνητα αν προτιμάτε.  

---

## Πώς να Χρησιμοποιήσετε το Sandbox – Επισκόπηση

Το sandbox απομονώνει τη μηχανή απόδοσης από το λειτουργικό σύστημα, επιτρέποντάς σας να ορίσετε μια εικονική οθόνη (πλάτος, ύψος, DPI) και μια προσαρμοσμένη συμβολοσειρά **user agent**. Σκεφτείτε το ως ένα μικροσκοπικό παράθυρο περιηγητή που ζει εξ ολοκλήρου στη μνήμη. Όταν αργότερα ζητήσετε το `HTMLDocument` για την προεπιλεγμένη προβολή του, η μηχανή θα αναφέρει το **μέγεθος του viewport** που υπολόγισε βάσει των ρυθμίσεων του sandbox.  

Ακολουθεί μια υψηλού επιπέδου ροή:

1. **Δημιουργία** ενός `DocumentSandbox` και ρύθμιση πλάτους, ύψους, DPI και user‑agent.  
2. **Φόρτωση** ενός `HTMLDocument` μέσα σε αυτό το sandbox.  
3. **Ερώτηση** της προεπιλεγμένης προβολής του εγγράφου για το μέγεθος του viewport.  

Ας βουτήξουμε σε κάθε βήμα.

---

## Βήμα 1: Δημιουργία Sandbox και Ορισμός Μεγέθους

Πρώτα, δημιουργούμε ένα sandbox και του λέμε πόσο μεγάλη πρέπει να είναι η εικονική οθόνη. Εδώ απαντάτε στην ερώτηση **πώς να ορίσετε το μέγεθος** για μια headless απόδοση.

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.drawing.Size2D;

/* Step 1 – instantiate the sandbox */
DocumentSandbox sandbox = new DocumentSandbox();

/* Set the virtual screen width & height (in pixels) */
sandbox.setScreenWidth(1280);   // width in pixels
sandbox.setScreenHeight(800);   // height in pixels

/* DPI influences CSS pixel calculations – 96 is the CSS default */
sandbox.setDeviceDpi(96);

/* Optional: give the sandbox a friendly name for debugging */
sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");
```

> **Συμβουλή:** Αν δοκιμάζετε ένα responsive layout, δοκιμάστε ένα στενό πλάτος όπως `360` για να προσομοιώσετε ένα τηλέφωνο, ή ένα ευρύ όπως `1920` για επιτραπέζιο υπολογιστή. Το sandbox σέβεται το DPI που ορίζετε, έτσι μια οθόνη υψηλής πυκνότητας (π.χ., 144 DPI) θα επηρεάσει τα media‑queries που χρησιμοποιούν `device-pixel-ratio`.

---

## Βήμα 2: Ορισμός User Agent για το Sandbox

Γιατί να ασχοληθείτε με έναν προσαρμοσμένο **user agent**; Ορισμένες ιστοσελίδες παρέχουν διαφορετικό markup ή scripts ανάλογα με τον αναφερόμενο περιηγητή. Καλώντας το `setUserAgent` μπορείτε να εξαπατήσετε τη σελίδα ώστε να πιστεύει ότι επισκέπτεται από Chrome, Firefox ή κινητή συσκευή.

```java
/* Step 2 – customize the user‑agent string */
sandbox.setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                     "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                     "Version/15.0 Mobile/15E148 Safari/604.1");
```

Τώρα η σελίδα θα νομίζει ότι αποδίδεται σε iPhone. Αν χρειαστεί να **ορίσετε ξανά το user agent** στην προεπιλογή, απλώς χρησιμοποιήστε ξανά τη συμβολοσειρά “AsposeHTML/24.6 …”.

---

## Βήμα 3: Φόρτωση HTML Εγγράφου Μέσα στο Sandbox

Με το sandbox έτοιμο, μπορούμε να φορτώσουμε οποιοδήποτε URL ή τοπικό αρχείο HTML. Ο κατασκευαστής `HTMLDocument` δέχεται το sandbox ως δεύτερο όρισμα, συνδέοντας τα δύο.

```java
import com.aspose.html.HTMLDocument;

/* Step 3 – load the page using the configured sandbox */
try (HTMLDocument doc = new HTMLDocument("https://example.com", sandbox)) {
    // The document is now rendered inside the sandbox environment.
    // Any JavaScript or CSS will see the size and user‑agent we defined.
```

Το μπλοκ `try‑with‑resources` εξασφαλίζει ότι το έγγραφο θα αποδεσμευτεί σωστά, απελευθερώνοντας τους εγγενείς πόρους που το Aspose.HTML εκχωρεί στο παρασκήνιο.

---

## Βήμα 4: Λήψη Μεγέθους Viewport από το Έγγραφο

Εδώ είναι η στιγμή που περιμένατε: η ανάκτηση του **μεγέθους του viewport** που υπολόγισε η μηχανή απόδοσης. Αυτό απαντά στο **πώς να λάβετε το viewport** μετά την διάταξη της σελίδας.

```java
    /* Step 4 – fetch the viewport dimensions */
    Size2D viewport = doc.getDefaultView().getScreenSize();
    System.out.println("Viewport: " + viewport.getWidth() + "×" + viewport.getHeight());
}
```

Όταν εκτελέσετε το πρόγραμμα, θα πρέπει να δείτε κάτι όπως:

```
Viewport: 1280×800
```

Αν αλλάξατε τις διαστάσεις του sandbox στο Βήμα 1, οι εκτυπωμένοι αριθμοί θα αντικατοπτρίζουν τις νέες τιμές — ιδανικό για αυτοματοποιημένες δοκιμές που επαληθεύουν responsive breakpoints.

---

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται η πλήρης, έτοιμη‑για‑εκτέλεση κλάση που συνδυάζει όλα τα κομμάτια. Αντιγράψτε‑και‑επικολλήστε το σε ένα αρχείο με όνομα `SandboxExample.java`, προσθέστε τα JAR του Aspose.HTML στο classpath, και εκτελέστε `java SandboxExample`.

```java
import com.aspose.html.*;
import com.aspose.html.drawing.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox with a custom screen size and DPI
        DocumentSandbox sandbox = new DocumentSandbox();
        sandbox.setScreenWidth(1280);          // width in pixels
        sandbox.setScreenHeight(800);          // height in pixels
        sandbox.setDeviceDpi(96);              // screen DPI
        sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");

        // Step 2: (Optional) Override the user agent if you need a mobile profile
        sandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
            "Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 3: Load the HTML document inside the configured sandbox
        try (HTMLDocument htmlDocument = new HTMLDocument("https://example.com", sandbox)) {

            // Step 4: Retrieve and display the computed viewport size
            Size2D viewportSize = htmlDocument.getDefaultView().getScreenSize();
            System.out.println("Viewport: " + viewportSize.getWidth() + "×" + viewportSize.getHeight());
        }
    }
}
```

**Αναμενόμενη έξοδος** (υπό τις παραπάνω ρυθμίσεις sandbox):

```
Viewport: 1280×800
```

Αν ορίσετε διαφορετικό πλάτος/ύψος στο sandbox, η έξοδος θα αλλάξει αναλόγως — ακριβώς ό,τι χρειάζεστε όταν δοκιμάζετε responsive σχέδια.

---

## Ακραίες Περιπτώσεις & Συχνές Ερωτήσεις

### Τι γίνεται αν η σελίδα χρησιμοποιεί `window.innerWidth` αντί για CSS media queries;

Το εικονικό μέγεθος οθόνης του sandbox επηρεάζει τόσο τη διάταξη CSS όσο και το `window.innerWidth/innerHeight` της JavaScript. Έτσι, το **πώς να λάβετε το viewport** μέσω JavaScript θα επιστρέψει τους ίδιους αριθμούς που βλέπετε στην κονσόλα Java.

### Μπορώ να τρέξω πολλαπλά sandboxes παράλληλα;

Ναι. Κάθε αντικείμενο `DocumentSandbox` είναι ανεξάρτητο, οπότε μπορείτε να δημιουργήσετε μια ομάδα νημάτων, να δώσετε σε κάθε νήμα το δικό του sandbox με διαφορετικές διαστάσεις και να αποδώσετε δεκάδες σελίδες ταυτόχρονα. Απλώς θυμηθείτε να διατηρήσετε τα JAR thread‑safe (είναι).

### Επηρεάζει η ρύθμιση DPI την κλιμάκωση των εικόνων;

Απολύτως. Ένα υψηλότερο DPI κάνει ένα CSS pixel να αντιστοιχεί σε περισσότερα device pixels, κάτι που μπορεί να κάνει τις εικόνες υψηλής ανάλυσης να φαίνονται πιο οξείς. Αν δοκιμάζετε assets τύπου retina, δοκιμάστε `sandbox.setDeviceDpi(144)`.

### Πώς να διαχειριστώ πιστοποιητικά HTTPS που είναι αυτο‑υπογεγραμμένα

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}