---
category: general
date: 2026-03-15
description: 'Πώς να δημιουργήσετε sandbox σε Java: μάθετε πώς να ορίσετε το μέγεθος
  της οθόνης, να απενεργοποιήσετε την πρόσβαση στο δίκτυο και να φορτώσετε ένα έγγραφο
  HTML με ασφάλεια.'
draft: false
keywords:
- how to create sandbox
- set screen size
- disable network access
- load html document
- how to render html
language: el
og_description: Πώς να δημιουργήσετε sandbox στη Java και να αποδώσετε με ασφάλεια
  HTML. Οδηγός βήμα‑προς‑βήμα που καλύπτει το μέγεθος της οθόνης, τους περιορισμούς
  δικτύου και τη φόρτωση εγγράφων.
og_title: Πώς να δημιουργήσετε sandbox στη Java – Πλήρης οδηγός
tags:
- Java
- Aspose.HTML
- Security
title: Πώς να δημιουργήσετε sandbox σε Java – Πλήρης οδηγός
url: /el/java/configuring-environment/how-to-create-sandbox-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε Sandbox σε Java – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να δημιουργήσετε sandbox** για την απόδοση μη αξιόπιστου web περιεχομένου σε Java; Δεν είστε μόνοι. Πολλοί προγραμματιστές χρειάζονται ένα ασφαλές «πορτοφόλι» όπου το HTML μπορεί να αποδοθεί χωρίς κίνδυνο για το σύστημα υποδοχής, και το Aspose.HTML Sandbox το κάνει παιχνιδάκι. Σε αυτό το tutorial θα περάσουμε από τον ορισμό του μεγέθους της οθόνης, την απενεργοποίηση της πρόσβασης στο δίκτυο, τη φόρτωση ενός HTML εγγράφου και, τέλος, την απόδοση – όλα μέσα σε ένα περιβάλλον sandbox.

> **Τι θα πάρετε:** ένα πλήρες, εκτελέσιμο παράδειγμα κώδικα, εξηγήσεις για κάθε γραμμή, και πρακτικές συμβουλές που σας προστατεύουν από κοινά λάθη. Δεν χρειάζεται εξωτερική τεκμηρίωση· όλα όσα χρειάζεστε είναι εδώ.

## Τι θα χρειαστείτε

- **Java 8+** (ο κώδικας χρησιμοποιεί τυπική σύνταξη Java, τίποτα εξωτικό)
- **Aspose.HTML for Java** βιβλιοθήκη (έκδοση 23.10 ή νεότερη)
- Ένα IDE ή απλός επεξεργαστής κειμένου – το Visual Studio Code λειτουργεί καλά
- Πρόσβαση στο Internet *μόνο* για τη λήψη της βιβλιοθήκης· το sandbox θα είναι εκτός σύνδεσης

Μόλις έχετε όλα αυτά, είστε έτοιμοι να ξεκινήσετε.

![Διάγραμμα δημιουργίας sandbox](sandbox-diagram.png){alt="Διάγραμμα δημιουργίας sandbox σε Java"}

## Πώς να δημιουργήσετε Sandbox – Επισκόπηση

Το sandbox είναι ουσιαστικά ένα κοντέινερ που περιορίζει τι μπορεί να κάνει η μηχανή HTML. Σκεφτείτε το ως έναν μικροσκοπικό περιηγητή που ζει σε ένα απομονωμένο δωμάτιο: εσείς αποφασίζετε πόσο μεγάλο θα είναι το παράθυρο (`set screen size`), αν θα μπορεί να φτάσει στο web (`disable network access`), και ποιο αρχείο HTML θα ανοίξει (`load html document`). Στο τέλος αυτού του οδηγού θα δείτε ακριβώς πώς ταιριάζουν όλα αυτά τα κομμάτια.

## Βήμα 1: Ορισμός Μεγέθους Οθόνης

Όταν δημιουργείτε το `SandboxConfiguration`, μπορείτε να πείτε στη μηχανή απόδοσης ποιο viewport να προσομοιώσει. Αυτό είναι χρήσιμο αν χρειάζεστε συγκεκριμένη διάταξη για στιγμιότυπα ή μετατροπή σε PDF αργότερα.

```java
// Step 1: Define sandbox constraints – screen size
SandboxConfiguration sandboxConfig = new SandboxConfiguration();
sandboxConfig.setScreenWidth(1024);   // width in pixels
sandboxConfig.setScreenHeight(768);   // height in pixels
```

Ο ορισμός ρεαλιστικού μεγέθους οθόνης εξασφαλίζει ότι τα CSS media queries συμπεριφέρονται όπως αναμένεται. Αν παραλείψετε αυτό το βήμα, η μηχανή προεπιλέγει ένα μικρό viewport 800×600, το οποίο μπορεί να «σπάσει» τις responsive σχεδιάσεις.

**Γιατί είναι σημαντικό:** Πολλοί σύγχρονοι ιστότοποι κρύβουν ή αναδιατάσσουν περιεχόμενο βάσει των διαστάσεων του viewport. Με την ρητή κλήση `set screen size`, εγγυάστε συνεπή απόδοση σε κάθε εκτέλεση.

## Βήμα 2: Απενεργοποίηση Πρόσβασης στο Δίκτυο

Οι προγραμματιστές που βάζουν την ασφάλεια πρώτα αγαπούν να κλειδώνουν οποιαδήποτε εξερχόμενη κίνηση. Το sandbox σας επιτρέπει να το κάνετε αυτό με μία μόνο σημαία.

```java
// Step 2: Turn off network calls – disable network access
sandboxConfig.setEnableNetworkAccess(false);
```

Όταν το `disable network access` είναι true, οποιοδήποτε `<script src="...">`, URL εικόνας ή CSS import που δείχνει σε εξωτερικό host θα αγνοηθεί. Αυτό αποτρέπει κακόβουλα payloads να επικοινωνήσουν με διακομιστή εντολών‑και‑ελέγχου.

> **Pro tip:** Αν αργότερα χρειαστεί να φορτώσετε έναν αξιόπιστο πόρο, μπορείτε προσωρινά να ενεργοποιήσετε την πρόσβαση στο δίκτυο για εκείνη τη συγκεκριμένη κλήση και μετά να την απενεργοποιήσετε ξανά.

## Βήμα 3: Φόρτωση HTML Εγγράφου μέσα στο Sandbox

Τώρα που το sandbox είναι ρυθμισμένο, δημιουργούμε το sandbox instance και του δίνουμε ένα HTML αρχείο. Σε αυτό το παράδειγμα δείχνουμε στο `https://example.com`, αλλά μπορείτε εξίσου καλά να φορτώσετε ένα τοπικό αρχείο με `new HTMLDocument("file:///path/to/file.html", sandbox)`.

```java
// Step 3: Create the sandbox and load the HTML document
Sandbox sandbox = new Sandbox(sandboxConfig);

try (HTMLDocument htmlDoc = new HTMLDocument("https://example.com", sandbox)) {
    // Step 4 will happen inside this block
    System.out.println("Document title: " + htmlDoc.getTitle());
}
```

Παρατηρήστε το **try‑with‑resources** block—εγγυάται ότι το έγγραφο θα αποδεσμευτεί σωστά, απελευθερώνοντας τους εγγενείς πόρους. Η κλήση στο `load html document` συμβαίνει αυτόματα όταν κατασκευάζετε το `HTMLDocument` με το όρισμα sandbox.

**Τι θα δείτε:** Αν τρέξετε το πρόγραμμα, η κονσόλα εκτυπώνει τον τίτλο της σελίδας, π.χ., `Document title: Example Domain`. Αυτό επιβεβαιώνει ότι το HTML αναλύθηκε επιτυχώς μέσα στο sandbox.

## Βήμα 4: Πώς να Αποδώσετε HTML και να Επαληθεύσετε το Αποτέλεσμα

Η απόδοση μπορεί να σημαίνει πολλά: σχεδίαση σε bitmap, δημιουργία PDF, ή απλώς εξαγωγή του DOM. Για αυτό το tutorial θα μείνουμε στην πιο απλή επαλήθευση—την εκτύπωση του τίτλου. Αν χρειάζεστε οπτική απόδοση, το Aspose.HTML προσφέρει το `HTMLRenderer`:

```java
// Optional: render to an image (demonstrates how to render html)
HTMLRenderer renderer = new HTMLRenderer(htmlDoc);
renderer.renderToFile("output.png", ImageFormat.PNG);
System.out.println("Rendered image saved as output.png");
```

Τρέχοντας το πλήρες πρόγραμμα τώρα παίρνετε δύο αποδείξεις ότι το sandbox λειτουργεί:

1. **Έξοδος κονσόλας** με τον τίτλο της σελίδας (αποδεικνύει ότι το `load html document` πέτυχε).
2. **αρχείο output.png** (αποδεικνύει ότι το `how to render html` πραγματικά σχεδίασε κάτι).

## Πλήρες, Εκτελέσιμο Παράδειγμα

Παρακάτω είναι ολόκληρο το πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα αρχείο με όνομα `SandboxDemo.java`. Περιλαμβάνει όλες τις εισαγωγές, τα βήματα ρύθμισης και το προαιρετικό τμήμα απόδοσης.

```java
import com.aspose.html.sandbox.*;
import com.aspose.html.*;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Define sandbox constraints – set screen size
        SandboxConfiguration sandboxConfig = new SandboxConfiguration();
        sandboxConfig.setScreenWidth(1024);
        sandboxConfig.setScreenHeight(768);
        // Step 2: Disable network access for security
        sandboxConfig.setEnableNetworkAccess(false);

        // Step 3: Create the sandbox instance using the configuration
        Sandbox sandbox = new Sandbox(sandboxConfig);

        // Step 4: Load an HTML document inside the sandboxed environment
        try (HTMLDocument htmlDoc = new HTMLDocument("https://example.com", sandbox)) {
            // Verify that the document loaded – print its title
            System.out.println("Document title: " + htmlDoc.getTitle());

            // Optional: render the page to an image (demonstrates how to render html)
            HTMLRenderer renderer = new HTMLRenderer(htmlDoc);
            renderer.renderToFile("output.png", ImageFormat.PNG);
            System.out.println("Rendered image saved as output.png");
        }
    }
}
```

**Αναμενόμενη έξοδος (κονσόλα):**

```
Document title: Example Domain
Rendered image saved as output.png
```

Και θα βρείτε το `output.png` στον φάκελο του έργου σας, δείχνοντας ένα στιγμιότυπο του `example.com` αποδομένο σε 1024×768 pixels.

## Συνηθισμένα Προβλήματα και Pro Tips

| Πρόβλημα | Γιατί συμβαίνει | Πώς να το διορθώσετε |
|----------|----------------|----------------------|
| **Λείπει `sandboxConfig.setEnableNetworkAccess(false)`** | Η μηχανή φορτώνει σιωπηλά εξωτερικά assets, παραβιάζοντας τον σκοπό του sandbox. | Πάντα ορίζετε αυτή τη σημαία, ακόμη και αν νομίζετε ότι η σελίδα είναι αυτόνομη. |
| **Χρήση απομακρυσμένου URL χωρίς πρόσβαση δικτύου** | Το έγγραφο αποτυγχάνει να φορτωθεί επειδή το sandbox μπλοκάρει το αίτημα. | Ενεργοποιήστε προσωρινά την πρόσβαση δικτύου για εκείνη την κλήση ή κατεβάστε το HTML πρώτα και φορτώστε το από δίσκο. |
| **Viewport που δεν ταιριάζει με τα CSS media queries** | Η διάταξη φαίνεται σπασμένη επειδή το προεπιλεγμένο μέγεθος είναι πολύ μικρό. | Χρησιμοποιήστε `setScreenWidth` και `setScreenHeight` ώστε να ταιριάζουν με τη συσκευή-στόχο. |
| **Ξεχάσατε να κλείσετε το `HTMLDocument`** | Διαρροές εγγενούς μνήμης μπορούν να συσσωρευτούν σε υπηρεσίες που τρέχουν πολύ χρόνο. | Χρησιμοποιήστε το try‑with‑resources όπως φαίνεται, ή καλέστε χειροκίνητα `htmlDoc.dispose()`. |

## Επέκταση του Sandbox: Σενάρια Πραγματικού Κόσμου

- **Δημιουργία PDF:** Αντικαταστήστε το `HTMLRenderer` με `HTMLToPDFConverter` για να μετατρέψετε τη φορτωμένη σελίδα σε PDF, διατηρώντας τα όρια του sandbox.
- **Batch Processing:** Επανάληψη πάνω σε λίστα URLs, επαναχρησιμοποιώντας το ίδιο `Sandbox` instance για να αποφύγετε το κόστος δημιουργίας νέου sandbox κάθε φορά.
- **Προσαρμοσμένοι Διαχειριστές Πόρων:** Υλοποιήστε το `IResourceHandler` για να παρέχετε εικόνες ή style sheets στη μνήμη, δίνοντάς σας λεπτομερή έλεγχο στο τι μπορεί να δει το sandbox.

## Ανακεφαλαίωση

Καλύψαμε **πώς να δημιουργήσετε sandbox** σε Java από το μηδέν, επιδείξαμε **set screen size**, σας δείξαμε πώς να **απενεργοποιήσετε την πρόσβαση στο δίκτυο**, περάσαμε από το **load html document**, και ρίξαμε μια γρήγορη ματιά στο **how to render html** σε εικόνα. Το πλήρες παράδειγμα τρέχει αμέσως, και οι εξηγήσεις απαντούν στο «γιατί» πίσω από κάθε σημαία ρύθμισης.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να αντικαταστήσετε το URL με ένα τοπικό HTML αρχείο που περιλαμβάνει ένα μικρό script, και ενεργοποιήστε/απενεργοποιήστε το `disable network access` για να δείτε το script να αγνοείται σιωπηλά. Ή πειραματιστείτε με διαφορετικά μεγέθη viewport για να δείτε τις responsive διατάξεις να αλλάζουν.

Έχετε ερωτήσεις, σενάρια άκρων, ή θέλετε να μοιραστείτε τα δικά σας κόλπα sandbox; Αφήστε ένα σχόλιο παρακάτω—ας συνεχίσουμε τη συζήτηση. Καλή δημιουργία sandbox!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}