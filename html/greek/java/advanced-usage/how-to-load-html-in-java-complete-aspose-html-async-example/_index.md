---
category: general
date: 2026-04-02
description: Πώς να φορτώσετε HTML σε Java χρησιμοποιώντας το Aspose.HTML, με προαιρετική
  αλυσίδωση JavaScript, await υπόσχεση JavaScript και παράδειγμα επίλυσης υπόσχεσης.
  Εκτελέστε εύκολα μια ασύγχρονη συνάρτηση.
draft: false
keywords:
- how to load html
- optional chaining javascript
- await promise javascript
- promise resolve example
- run async function
language: el
og_description: Πώς να φορτώσετε HTML σε Java με το Aspose.HTML. Μάθετε προαιρετική
  αλυσίδωση (optional chaining) στη JavaScript, await promise στη JavaScript και ένα
  παράδειγμα resolve promise ενώ εκτελείτε ασύγχρονη λειτουργία.
og_title: Πώς να φορτώσετε HTML σε Java – Οδηγός Async του Aspose.HTML
tags:
- Java
- Aspose.HTML
- JavaScript
- Async Programming
title: Πώς να φορτώσετε HTML σε Java – Πλήρες παράδειγμα ασύγχρονης Aspose.HTML
url: /el/java/advanced-usage/how-to-load-html-in-java-complete-aspose-html-async-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να φορτώσετε HTML σε Java – Πλήρες Παράδειγμα Async με Aspose.HTML

Έχετε αναρωτηθεί ποτέ **πώς να φορτώσετε HTML** σε ένα πρόγραμμα Java χωρίς να εκκινήσετε έναν πλήρη περιηγητή; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν πρέπει να αξιολογήσουν ένα μικρό script—π.χ., μια async λειτουργία που φέρνει δεδομένα—μέσα σε ένα headless περιβάλλον. Τα καλά νέα; Με το Aspose.HTML μπορείτε να δημιουργήσετε ένα `HTMLDocument`, να του δώσετε μια συμβολοσειρά και να αφήσετε το ενσωματωμένο JavaScript να εκτελεστεί μέχρι το τέλος.  

Σε αυτόν τον οδηγό θα περάσουμε βήμα-βήμα από ένα πραγματικό απόσπασμα κώδικα που δείχνει **optional chaining JavaScript**, **await promise JavaScript** και ένα **promise resolve example**. Στο τέλος θα ξέρετε ακριβώς πώς να εκτελέσετε μια async λειτουργία, να καταγράψετε το αποτέλεσμα και να το εκτυπώσετε—όλα από καθαρή Java. Χωρίς εξωτερικούς browsers, χωρίς Selenium, μόνο απλός κώδικας που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Maven ή Gradle.

## Prerequisites

- Java 17 (ή οποιαδήποτε πρόσφατη LTS έκδοση)  
- Aspose.HTML for Java 23.2 ή νεότερη – μπορείτε να την αποκτήσετε από το Maven Central  
- Βασική εξοικείωση με promises του JavaScript και τη σύνταξη async/await  

Αν έχετε όλα αυτά, είμαστε έτοιμοι να ξεκινήσουμε.

![Διάγραμμα που δείχνει πώς φορτώνεται το HTML σε ένα HTMLDocument και το async script εκτελείται μέσα](/images/how-to-load-html-diagram.png "διάγραμμα φόρτωσης html")

## Step 1: Set Up the Project and Import Aspose.HTML

Πρώτα απ’ όλα, προσθέστε την εξάρτηση Aspose.HTML στο αρχείο κατασκευής σας. Για Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.2</version>
</dependency>
```

Ή για Gradle:

```gradle
implementation 'com.aspose:aspose-html:23.2'
```

Οι δηλώσεις εισαγωγής που θα χρειαστείτε στον κώδικα Java είναι:

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;
```

> **Pro tip:** Κρατήστε τις εξαρτήσεις σας ενημερωμένες. Οι νέες εκδόσεις συχνά φέρνουν βελτιώσεις απόδοσης για την εκτέλεση async script.

## Step 2: Create an `HTMLDocument` to Host the Page

Τώρα δημιουργούμε ένα νέο `HTMLDocument`. Σκεφτείτε το ως μια ελαφριά καρτέλα browser που ζει εξ ολοκλήρου στη μνήμη.

```java
try (HTMLDocument document = new HTMLDocument()) {
    // The document will be automatically closed at the end of the block.
}
```

Η χρήση ενός μπλοκ `try‑with‑resources` εγγυάται ότι οι εγγενείς πόροι απελευθερώνονται, αποτρέποντας διαρροές μνήμης—κάτι που είναι εύκολο να παραβλεφθεί όταν δοκιμάζετε μόνο αποσπάσματα κώδικα.

## Step 3: Write the HTML with an Async Script

Εδώ έρχεται το τμήμα **run async function**. Ενσωματώνουμε ένα μικρό script που:

1. **awaits** ένα resolved promise (`await Promise.resolve(...)`) – κλασικό μοτίβο **await promise JavaScript**.  
2. Χρησιμοποιεί **optional chaining JavaScript** (`data?.user?.name`) για ασφαλή πρόσβαση σε ένθετες ιδιότητες.  
3. Επιστρέφει `'unknown'` μέσω του nullish coalescing operator (`??`).  

Η πλήρης συμβολοσειρά HTML είναι η εξής:

```java
String htmlContent = "<!DOCTYPE html><html><head>"
        + "<script>"
        + "async function load() {"
        + "  const data = await Promise.resolve({user:{name:'Alice'}});"
        + "  document.body.textContent = data?.user?.name ?? 'unknown';"
        + "}"
        + "load();"
        + "</script>"
        + "</head><body></body></html>";
```

> **Why this matters:**  
> - **`await promise`** μας επιτρέπει να παύσουμε την εκτέλεση μέχρι να ολοκληρωθεί το promise, προσομοιώνοντας πραγματικές κλήσεις API.  
> - **`optional chaining`** αποτρέπει `TypeError` όταν λείπει μια ιδιότητα, ένα δίχτυ ασφαλείας που θα εκτιμήσετε σε παραγωγικό κώδικα.  
> - Το **`promise resolve example`** δείχνει ένα καθορισμένο αποτέλεσμα, κάνοντας το tutorial επαναλήψιμο.

## Step 4: Load the HTML String into the Document

Με το HTML έτοιμο, το παραδίδουμε στο Aspose.HTML:

```java
document.loadHtml(htmlContent);
```

Σε αυτό το σημείο το έγγραφο αναλύει το markup, δημιουργεί ένα DOM και προετοιμάζει τη μηχανή JavaScript για εκτέλεση.

## Step 5: Give the Async Script Time to Finish

Το κύριο νήμα της Java δεν περιμένει αυτόματα το event loop του script. Σε μια πλήρη εφαρμογή θα συνδεόσασταν στο γεγονός `ScriptExecutionCompleted` του Aspose, αλλά για μια γρήγορη επίδειξη αρκεί ένα απλό sleep:

```java
Thread.sleep(500); // Give the async script a moment to finish.
```

> **Watch out:** Η χρήση του `Thread.sleep` είναι αποδεκτή για demos, αλλά σε παραγωγή θα πρέπει να συγχρονίζεστε με τη μηχανή script ή να χρησιμοποιήσετε ένα `Future` για να αποφύγετε περιττή καθυστέρηση.

## Step 6: Retrieve the Result from the Document Body

Τέλος, διαβάζουμε τι έγραψε το script στο `<body>` και το εκτυπώνουμε:

```java
System.out.println("Body text after script: " + document.getBody().getTextContent());
```

Όταν τρέξετε το πρόγραμμα, θα δείτε:

```
Body text after script: Alice
```

Αν αλλάξετε το JSON payload σε `{}` ή παραλείψετε το πεδίο `user`, η έξοδος θα γίνει `unknown`—ακριβώς όπως ορίζει η έκφραση optional chaining.

## Full, Ready‑to‑Run Example

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι η πλήρης κλάση που μπορείτε να αντιγράψετε‑επικολλήσετε στο IDE σας:

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class JsAsyncDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an HTMLDocument instance that will host the page.
        try (HTMLDocument document = new HTMLDocument()) {

            // Step 2: Define a simple HTML page containing an async script.
            // The script resolves a promise and uses optional chaining to
            // safely read a nested property, falling back to "unknown".
            String htmlContent = "<!DOCTYPE html><html><head>"
                    + "<script>"
                    + "async function load() {"
                    + "  const data = await Promise.resolve({user:{name:'Alice'}});"
                    + "  document.body.textContent = data?.user?.name ?? 'unknown';"
                    + "}"
                    + "load();"
                    + "</script>"
                    + "</head><body></body></html>";

            // Step 3: Load the HTML string into the document.
            document.loadHtml(htmlContent);

            // Step 4: Give the asynchronous script a moment to finish.
            // (In a real application you would use proper synchronization.)
            Thread.sleep(500);

            // Step 5: Retrieve and display the text that the script wrote to the body.
            System.out.println("Body text after script: " + document.getBody().getTextContent());
        }
    }
}
```

### Expected Output

```
Body text after script: Alice
```

Αν αντικαταστήσετε το JSON με `{}` η κονσόλα θα εμφανίσει:

```
Body text after script: unknown
```

Αυτή η μικρή αλλαγή δείχνει τη δύναμη του **optional chaining JavaScript** σε συνδυασμό με ένα **promise resolve example**.

## Common Questions & Edge Cases

### What if the script takes longer than 500 ms?

Η τιμή του `Thread.sleep` είναι αυθαίρετη. Για promises που εξαρτώνται από δίκτυο θα θέλετε μεγαλύτερη αναμονή ή, καλύτερα, να συνδεθείτε στα callbacks ολοκλήρωσης script του Aspose:

```java
document.getWindow().setOnload(() -> {
    // This runs after all scripts have finished.
});
```

### Can I load HTML from a file instead of a string?

Απολύτως. Χρησιμοποιήστε `document.load("path/to/file.html");` ή `document.load(new java.io.FileInputStream(...))`. Η ίδια διαχείριση async ισχύει.

### Does Aspose.HTML support ES2022 features like `?.` and `??`?

Ναι. Η ενσωματωμένη μηχανή V8 (ή η ενσωματωμένη μηχανή Chromium στις νεότερες εκδόσεις) καταλαβαίνει τη σύγχρονη σύνταξη αμέσως. Απλώς βεβαιωθείτε ότι χρησιμοποιείτε πρόσφατη έκδοση του Aspose.HTML.

### How do I capture console.log output from the script?

Μπορείτε να ανακατευθύνετε την κονσόλα JavaScript στην Java προσθέτοντας μια προσαρμοσμένη υλοποίηση `Console`:

```java
document.getWindow().setConsole(new Console() {
    @Override public void log(Object... args) {
        System.out.println("[JS] " + java.util.Arrays.toString(args));
    }
});
```

Τώρα κάθε `console.log` μέσα στο HTML σας θα εμφανίζεται στην κονσόλα Java—χρήσιμο για εντοπισμό σφαλμάτων σε σύνθετες async ροές.

## Wrap‑Up

Καλύψαμε **πώς να φορτώσετε HTML** σε Java με Aspose.HTML, παρουσιάσαμε ένα σενάριο **run async function**, και εξετάσαμε **optional chaining JavaScript**, **await promise JavaScript**, και ένα **promise resolve example**—όλα σε ένα ενιαίο, αυτόνομο πρόγραμμα.  

Τώρα έχετε μια σταθερή βάση για να ενσωματώσετε μικρές ιστοσελίδες, να αξιολογήσετε λογική client‑side, ή ακόμη και να δημιουργήσετε pipelines server‑side rendering χωρίς βαρύ browser. Τα επόμενα βήματα μπορεί να περιλαμβάνουν:

- Φόρτωση εξωτερικών script μέσω `<script src="...">` και διαχείριση CORS.  
- Χρήση της μετατροπής PDF του Aspose.HTML για να συλλάβετε το αποδοθέν αποτέλεσμα.  
- Ενσωμάτωση πραγματικών κλήσεων HTTP μέσα στη async λειτουργία (fetch API) και επεξεργασία των αποτελεσμάτων.

Δοκιμάστε αυτές τις ιδέες και θα δείτε πόσο ευέλικτη είναι η προσέγγιση. Έχετε κάποιο δικό σας twist; Αφήστε ένα σχόλιο παρακάτω—μας αρέσει να ακούμε πώς οι προγραμματιστές σπρώχνουν τα όρια.

Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}