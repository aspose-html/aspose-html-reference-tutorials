---
category: general
date: 2026-02-10
description: Ορίστε την αναλογία εικονοστοιχείων της συσκευής σε Java χρησιμοποιώντας
  το sandbox του Aspose.HTML. Μάθετε πώς να ορίσετε το πλάτος και το ύψος της οθόνης
  και να λάβετε τον τίτλο της σελίδας σε Java με ένα πλήρες, εκτελέσιμο παράδειγμα.
draft: false
keywords:
- set device pixel ratio
- get page title java
- set screen width height
language: el
og_description: Ορίστε την αναλογία εικονοστοιχείων της συσκευής σε Java με το sandbox
  του Aspose.HTML. Αυτός ο οδηγός σας δείχνει πώς να ορίσετε το πλάτος και το ύψος
  της οθόνης και να λάβετε τον τίτλο της σελίδας σε Java σε λίγα εύκολα βήματα.
og_title: Ορισμός αναλογίας εικονοστοιχείων συσκευής σε Java – Μάθημα Mobile Sandbox
tags:
- Aspose.HTML
- Java
- Mobile Emulation
title: Ορισμός του λόγου εικονοστοιχείων της συσκευής σε Java – Μάθημα Mobile Sandbox
url: /el/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/
---

preserve all code blocks fenced. There are none besides placeholders. So fine.

Check any other markdown like blockquote, lists, tables.

All good.

Now produce final content with Greek translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ορισμός αναλογίας pixel συσκευής σε Java – Εγχειρίδιο Mobile Sandbox

Έχετε χρειαστεί ποτέ να **ορίσετε την αναλογία pixel της συσκευής** ενώ δοκιμάζετε έναν responsive ιστότοπο σε Java; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν η σελίδα φαίνεται τέλεια στην επιφάνεια εργασίας αλλά σπάζει σε τηλέφωνα με υψηλή DPI. Τα καλά νέα; Με το sandbox της Aspose.HTML μπορείτε να προσομοιώσετε ένα iPhone X (ή οποιαδήποτε συσκευή) απευθείας από τον κώδικα Java—χωρίς πρόγραμμα περιήγησης.

Σε αυτόν τον οδηγό θα περάσουμε από το **πώς να ορίσετε το πλάτος και το ύψος της οθόνης**, να διαμορφώσουμε την **αναλογία pixel της συσκευής**, και τελικά το **get page title java** για να επαληθεύσουμε ότι όλα αποδόθηκαν σωστά. Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο και να αρχίσετε αμέσως τη δοκιμή των mobile διατάξεων.

## Προαπαιτούμενα

- Java 8 ή νεότερη (ο κώδικας μεταγλωττίζεται επίσης με JDK 11)  
- Βιβλιοθήκη Aspose.HTML for Java (έκδοση 23.7 ή νεότερη) – μπορείτε να την κατεβάσετε από το Maven Central  
- Ένα IDE ή μια απλή ρύθμιση γραμμής εντολών `javac`  
- Πρόσβαση στο Internet για το demo URL (`https://responsive.example.com`)

Καμία επιπλέον πλατφόρμα, χωρίς Selenium, μόνο καθαρή Java και Aspose.HTML.

---

## Βήμα 1: Ορισμός πλάτους και ύψους οθόνης και αναλογίας pixel συσκευής

Το πρώτο που χρειαζόμαστε είναι ένα αντικείμενο `SandboxOptions` που λέει στο sandbox ποια “συσκευή” προσποιούμαστε ότι είμαστε. Εδώ θα χρησιμοποιήσουμε τις διαστάσεις του iPhone X (375 × 812 CSS pixels) και μια **αναλογία pixel συσκευής** 3.0, η οποία αντικατοπτρίζει την οθόνη retina υψηλής DPI.

```java
// Step 1 – configure the virtual device
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixels width
sandboxOptions.setScreenHeight(812);         // CSS pixels height
sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI factor (set device pixel ratio)
```

> **Γιατί είναι σημαντικό:**  
> Η κλήση `setDevicePixelRatio` κλιμακώνει τα πάντα—από εικόνες μέχρι απόδοση γραμματοσειρών—ώστε η σελίδα να πιστεύει ότι βρίσκεται σε πραγματικό τηλέφωνο. Αν την παραλείψετε, η διάταξη μπορεί να επιστρέψει σε ερωτήματα CSS τύπου desktop, αντιστρέφοντας τον σκοπό της δοκιμής για κινητά.

---

## Βήμα 2: Δημιουργία του αντικειμένου sandbox

Τώρα μετατρέπουμε αυτές τις επιλογές σε ένα ενεργό sandbox. Σκεφτείτε το sandbox ως ένα μικρό, headless πρόγραμμα περιήγησης που σέβεται τις διαστάσεις και την αναλογία pixel που ορίσαμε.

```java
// Step 2 – spin up the sandbox with the options above
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

> **Συμβουλή:** Μπορείτε να επαναχρησιμοποιήσετε το ίδιο αντικείμενο `Sandbox` για πολλαπλές φορτώσεις σελίδων· απλώς αλλάξτε το URL και το sandbox θα διατηρήσει τα ίδια χαρακτηριστικά συσκευής.

---

## Βήμα 3: Φόρτωση της σελίδας μέσα στο sandbox

Με το sandbox έτοιμο, η φόρτωση μιας σελίδας είναι τόσο απλή όσο η δημιουργία ενός `HTMLDocument` και η περάσματος του sandbox ως δεύτερο όρισμα. Αυτό αναγκάζει το έγγραφο να αποδοθεί χρησιμοποιώντας τη εικονική συσκευή που ορίσαμε νωρίτερα.

```java
// Step 3 – fetch the target page using the sandbox
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("https://responsive.example.com"), mobileSandbox);
```

Αν το URL είναι μη προσβάσιμο ή η σελίδα περιέχει σφάλματα, το Aspose.HTML θα ρίξει μια εξαίρεση. Για κώδικα παραγωγής πιθανότατα θα το τυλίξετε σε `try‑catch` και θα καταγράψετε το σφάλμα, αλλά για το tutorial το κρατάμε απλό.

---

## Βήμα 4: Επαλήθευση με get page title java

Ο πιο γρήγορος έλεγχος λογικής είναι η ανάγνωση του τίτλου του εγγράφου. Αν το sandbox εφάρμοσε σωστά την **αναλογία pixel συσκευής**, ο τίτλος θα είναι ταυτόσιος με αυτόν που θα δείτε σε ένα πραγματικό iPhone X.

```java
// Step 4 – retrieve and print the page title (get page title java)
System.out.println("Title under sandbox: " + htmlDoc.getTitle());
```

**Αναμενόμενη έξοδος (παράδειγμα):**

```
Title under sandbox: Responsive Demo – Mobile View
```

Αν δείτε τον τίτλο να εκτυπώνεται, έχετε επιτυχώς **ορίσει την αναλογία pixel συσκευής**, **ορίσει το πλάτος και το ύψος της οθόνης**, και **λάβει τον τίτλο της σελίδας** χρησιμοποιώντας Java.

---

## Πλήρες, Εκτελέσιμο Παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα αρχείο με όνομα `SandboxDemo.java`. Βεβαιωθείτε ότι τα JAR του Aspose.HTML είναι στο classpath (`-cp` flag) πριν το μεταγλωττίσετε.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.net.URL;

/**
 * Demonstrates how to set device pixel ratio, set screen width height,
 * and get page title java using Aspose.HTML sandbox.
 */
public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define device characteristics ----------
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS pixels width
        sandboxOptions.setScreenHeight(812);         // CSS pixels height
        sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI screen factor (set device pixel ratio)

        // ---------- Step 2: Create the sandbox ----------
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // ---------- Step 3: Load a web page inside the sandbox ----------
        HTMLDocument htmlDoc = new HTMLDocument(
                new URL("https://responsive.example.com"), mobileSandbox);

        // ---------- Step 4: Verify the document loaded correctly ----------
        System.out.println("Title under sandbox: " + htmlDoc.getTitle());
    }
}
```

Μεταγλώττιση και εκτέλεση:

```bash
javac -cp "aspose-html-23.7.jar" SandboxDemo.java
java -cp ".:aspose-html-23.7.jar" SandboxDemo
```

Θα πρέπει να δείτε τον τίτλο να εκτυπώνεται στην κονσόλα, επιβεβαιώνοντας ότι η σελίδα αποδόθηκε με την επιθυμητή **αναλογία pixel συσκευής**.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| **Μπορώ να αλλάξω την αναλογία pixel κατά την εκτέλεση;** | Ναι—απλώς δημιουργήστε ένα νέο `SandboxOptions` με διαφορετική τιμή `setDevicePixelRatio` και δημιουργήστε ένα νέο `Sandbox`. Η επαναχρήση του ίδιου sandbox μετά την αλλαγή των επιλογών του δεν υποστηρίζεται. |
| **Τι γίνεται αν χρειαστεί να δοκιμάσω πολλές συσκευές;** | Κάντε βρόχο πάνω σε μια λίστα `SandboxOptions` (π.χ., iPhone 8, Pixel 4) και εκτελέστε την ίδια λογική φόρτωσης‑και‑ανάγνωσης τίτλου για κάθε μία. |
| **Λειτουργεί αυτό με HTTPS ιστοσελίδες που έχουν αυτο‑υπογεγραμμένα πιστοποιητικά;** | Το Aspose.HTML σέβεται το προεπιλεγμένο SSL trust store της Java. Προσθέστε το πιστοποιητικό στο keystore του JVM ή απενεργοποιήστε την επαλήθευση μόνο για δοκιμές (δεν συνιστάται για παραγωγή). |
| **Πώς μπορώ να καταγράψω ένα screenshot αντί για μόνο τον τίτλο;** | Το API του `HTMLDocument` παρέχει μεθόδους `save` που μπορούν να εξάγουν τη σελίδα σε PNG ή JPEG. Χρησιμοποιήστε `htmlDoc.save("output.png", SaveFormat.PNG);` μετά τη φόρτωση. |
| **Είναι το sandbox thread‑safe;** | Κάθε αντικείμενο `Sandbox` είναι απομονωμένο, αλλά θα πρέπει να αποφεύγετε την κοινή χρήση ενός μόνο αντικειμένου μεταξύ πολλαπλών νημάτων χωρίς συγχρονισμό. |

---

## Οπτική Επισκόπηση

![Διάγραμμα που δείχνει την ορισμένη αναλογία pixel συσκευής σε mobile sandbox](https://example.com/images/sandbox-diagram.png "διάγραμμα ορισμένης αναλογίας pixel")

*Η παραπάνω εικονογράφηση απεικονίζει τη ροή από τη διαμόρφωση των `SandboxOptions` (συμπεριλαμβανομένου του **ορισμού πλάτους και ύψους οθόνης** και της **αναλογίας pixel συσκευής**) μέχρι τη φόρτωση ενός URL και την εξαγωγή του τίτλου.*

---

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να ορίσετε την αναλογία pixel συσκευής** σε Java, πώς να **ορίσετε το πλάτος και το ύψος της οθόνης** για ακριβή προσομοίωση κινητών, και πώς να **get page title java** για να επιβεβαιώσετε ότι η απόδοση ολοκληρώθηκε επιτυχώς. Αυτή η συμπαγής ροή εργασίας εξαλείφει την ανάγκη για βαριές browsers κατά τη διάρκεια αυτοματοποιημένων δοκιμών UI και ενσωματώνεται άψογα σε CI pipelines.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να εξάγετε τη σελίδα ως εικόνα, ή πειραματιστείτε με τον εντοπισμό σφαλμάτων CSS media‑query εναλλάσσοντας το `devicePixelRatio` μεταξύ 1.0 και 3.0. Μπορείτε επίσης να εξερευνήσετε τις δυνατότητες μετατροπής PDF του Aspose.HTML για να δημιουργήσετε μια εκτυπώσιμη έκδοση της mobile προβολής.

Καλό κώδικα, και εύχομαι οι mobile διατάξεις σας να είναι πάντα καθαρές—ανεξάρτητα από την πυκνότητα των pixel!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}