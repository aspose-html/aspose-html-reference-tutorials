---
category: general
date: 2026-02-16
description: Μάθετε πώς να εκτελείτε JavaScript σε Java με CompletableFuture, να καθυστερείτε
  το JS και να αξιολογείτε ασύγχρονο κώδικα. Πλήρης οδηγός βήμα‑βήμα για την αξιολόγηση
  ασύγχρονης JavaScript.
draft: false
keywords:
- how to run javascript
- how to use completablefuture
- how to delay js
- how to evaluate async
- evaluate javascript asynchronously
language: el
og_description: Αποκτήστε πλήρη γνώση για το πώς να εκτελείτε JavaScript από Java,
  να καθυστερείτε το JS και να αξιολογείτε ασύγχρονο κώδικα με CompletableFuture σε
  αυτό το ολοκληρωμένο σεμινάριο.
og_title: Πώς να εκτελέσετε JavaScript ασύγχρονα χρησιμοποιώντας το CompletableFuture
tags:
- javascript
- java
- asynchronous
- completablefuture
title: Πώς να τρέξετε JavaScript ασύγχρονα χρησιμοποιώντας το CompletableFuture
url: /el/java/advanced-usage/how-to-run-javascript-asynchronously-using-completablefuture/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε JavaScript Ασύγχρονα Χρησιμοποιώντας CompletableFuture

Ποτέ δεν αναρωτηθήκατε **πώς να εκτελέσετε JavaScript** μέσα σε μια εφαρμογή Java χωρίς να μπλοκάρετε το κύριο νήμα; Ίσως χρειάζεστε να καλέσετε ένα μικρό script που φέρνει δεδομένα, αλλά δεν θέλετε η διεπαφή χρήστη σας να παγώσει. Τα καλά νέα είναι ότι οι σύγχρονες βιβλιοθήκες Java επιτρέπουν την αξιολόγηση του JavaScript **ασύγχρονα**, και μπορείτε ακόμη να εισάγετε καθυστερήσεις όπως θα κάνατε σε έναν περιηγητή. Σε αυτόν τον οδηγό θα σας δείξουμε ένα πλήρες, εκτελέσιμο παράδειγμα που χρησιμοποιεί το `ScriptEngine` του Aspose HTML μαζί με το `CompletableFuture` για **πώς να εκτελέσετε javascript** και να λάβετε το αποτέλεσμα πίσω στη Java.

Θα καλύψουμε επίσης **πώς να χρησιμοποιήσετε CompletableFuture**, **πώς να καθυστερήσετε JS**, και **πώς να αξιολογήσετε async** κώδικα ώστε να μπορείτε να **αξιολογήσετε JavaScript ασύγχρονα** σε οποιοδήποτε έργο Java. Στο τέλος θα έχετε ένα στέρεο πρότυπο που μπορείτε να αντιγράψετε‑επικολλήσετε, να προσαρμόσετε και να ενσωματώσετε σε μεγαλύτερα συστήματα.

---

## Τι Θα Μάθετε

- Ρυθμίστε ένα Java `ScriptEngine` που μπορεί να εκτελεί σύγχρονο JavaScript ES2022.
- Γράψτε μια `async` συνάρτηση που περιλαμβάνει καθυστέρηση (`how to delay js`).
- Καλέστε το `evaluateAsync` και λάβετε ένα `CompletableFuture` (`how to use completablefuture`).
- Ανακτήστε το αποτέλεσμα μόλις η υπόσχεση JavaScript επιλυθεί (`how to evaluate async`).
- Συμβουλές για διαχείριση σφαλμάτων, διαχείριση νημάτων και επέκταση του μοτίβου.

Δεν απαιτούνται εξωτερικά εργαλεία κατασκευής πέρα από το JAR του Aspose HTML for Java, το οποίο μπορείτε να προσθέσετε στο classpath σας. Ας βουτήξουμε.

---

## Βήμα 1: Πώς να Εκτελέσετε JavaScript – Αρχικοποίηση του Μηχανήματος Σκριπτ

Πρώτα απ' όλα. Η βιβλιοθήκη Aspose HTML παρέχει μια κλάση `ScriptEngine` που μπορεί να εκτελεί κώδικα JavaScript. Σκεφτείτε το ως μια μικρή μηχανή Chromium που τρέχει μέσα στη JVM σας.

```java
import com.aspose.html.scripting.*;
import java.util.concurrent.CompletableFuture;

public class JsAsyncDemo {
    public static void main(String[] args) throws Exception {

        // Create a scripting engine that can run JavaScript
        ScriptEngine scriptEngine = new ScriptEngine();
```

> **Γιατί είναι σημαντικό:** Με την δημιουργία ενός αντικειμένου `ScriptEngine` αποκτούμε ένα απομονωμένο περιβάλλον όπου το σύγχρονο JavaScript (συμπεριλαμβανομένου του `async/await`) λειτουργεί αμέσως. Δεν χρειάζεται να εκκινήσετε εξωτερική διεργασία Node.

---

## Βήμα 2: Πώς να Καθυστερήσετε JS – Γράψτε μια Async Συνάρτηση με Χρονόμετρο Βασισμένο σε Υπόσχεση

Το `setTimeout` του JavaScript είναι ο κλασικός τρόπος για να παύσετε την εκτέλεση. Σε σύγχρονο κώδικα το τυλίγουμε σε μια `Promise` ώστε να μπορούμε να το `await`‑αμε. Αυτό ακριβώς θα κάνουμε στο string του script.

```java
        // ES2022 async function that resolves after a short delay
        String asyncScript = """
            async function fetchMessage() {
                const delay = ms => new Promise(r => setTimeout(r, ms));
                await delay(500); // 500 ms pause
                return "Hello from async JS!";
            }
            fetchMessage(); // Return the promise to Java
            """;
```

> **Πώς να καθυστερήσετε js:** Η βοηθητική συνάρτηση `delay` δημιουργεί μια υπόσχεση που λήγει μετά από `ms` χιλιοστά του δευτερολέπτου. Με το `await`‑ing της, η συνάρτηση παύει χωρίς να μπλοκάρει το νήμα Java.

---

## Βήμα 3: Πώς να Αξιολογήσετε Async – Εκτελέστε το Script και Λάβετε ένα CompletableFuture

Αντί της συγχρονισμένης μεθόδου `evaluate`, καλούμε το `evaluateAsync`. Επιστρέφει αμέσως ένα `CompletableFuture<Object>` που θα ολοκληρωθεί όταν η υπόσχεση JavaScript επιλυθεί.

```java
        // Evaluate the script asynchronously – a CompletableFuture is returned
        CompletableFuture<Object> resultFuture = scriptEngine.evaluateAsync(asyncScript);
```

> **Πώς να αξιολογήσετε async:** Το `evaluateAsync` γεφυρώνει το loop γεγονότων του JavaScript με το `CompletableFuture` της Java. Αυτό αποτελεί τον πυρήνα του **evaluate javascript asynchronously**.

---

## Βήμα 4: Πώς να Χρησιμοποιήσετε CompletableFuture – Προσθέστε Callback και Μπλοκάρετε για Demo

Τώρα προσθέτουμε ένα callback με `thenAccept` για να εκτυπώσουμε το αποτέλεσμα, και μπλοκάρουμε το κύριο νήμα αρκετά ώστε το demo να ολοκληρωθεί.

```java
        // When the promise resolves, print the JavaScript result
        resultFuture.thenAccept(result ->
                System.out.println("JS result: " + result));

        // Block the main thread long enough for the demo to finish
        resultFuture.get(); // throws checked exceptions, handled by main's throws clause
    }
}
```

> **Γιατί καλούμε `get()`:** Σε μια πραγματική εφαρμογή πιθανότατα θα συνεχίσετε την επεξεργασία αλλού. Εδώ μπλοκάρουμε για να κρατήσουμε το παράδειγμα αυτό‑συνεπές.

---

## Οπτική Επισκόπηση

![Διάγραμμα που δείχνει πώς να εκτελέσετε JavaScript ασύγχρονα με CompletableFuture](https://example.com/diagram.png "Πώς να Εκτελέσετε JavaScript – Ροή Ασύγχρονης Εκτέλεσης")

*Alt text:* **Διάγραμμα που δείχνει πώς να εκτελέσετε JavaScript ασύγχρονα με CompletableFuture** – η εικόνα απεικονίζει τη ροή από τη Java στη μηχανή script, την async καθυστέρηση, και την ολοκλήρωση του CompletableFuture.

---

## Συνηθισμένα Πιθανά Σφάλματα & Καλές Πρακτικές (Πώς να Αξιολογήσετε Async Ασφαλώς)

| Πιθανό Σφάλμα | Τι Συμβαίνει | Διόρθωση |
|---------------|--------------|----------|
| Ξέχνατε να επιστρέψετε την υπόσχεση | `evaluateAsync` λύνει αμέσως με `undefined` | Βεβαιωθείτε ότι η τελευταία γραμμή του script είναι η υπόσχεση (`fetchMessage();`) |
| Χρήση μπλοκαριστικού `Thread.sleep` στο JS | Μπλοκάρει το event loop της μηχανής, εξουδετερώνει το async | Χρησιμοποιήστε το πρότυπο υπόσχεσης `delay` (όπως φαίνεται) |
| Αγνόηση εξαιρέσεων | Το Future ολοκληρώνεται εξαιρετικά, αλλά δεν το βλέπετε | Προσθέστε `.exceptionally(e -> { e.printStackTrace(); return null; })` |
| Μη κλείσιμο της μηχανής | Διαρροή πόρων σε εφαρμογές μεγάλης διάρκειας | Καλέστε `scriptEngine.dispose()` όταν τελειώσετε |

---

## Επέκταση του Μοτίβου (Πώς να Χρησιμοποιήσετε CompletableFuture σε Πραγματικά Έργα)

Μπορείτε να αλυσίδετε πολλαπλές async κλήσεις JavaScript, να τις συνδυάσετε με άλλα futures, ή ακόμη και να τις τρέξετε σε προσαρμοσμένο `Executor`. Εδώ είναι ένα γρήγορο σκίτσο:

```java
ExecutorService jsPool = Executors.newFixedThreadPool(4);
CompletableFuture<Object> future = scriptEngine.evaluateAsync(asyncScript, jsPool)
    .thenApply(result -> {
        // Post‑process the JS string result
        return ((String) result).toUpperCase();
    })
    .exceptionally(ex -> {
        System.err.println("JS error: " + ex);
        return "fallback";
    });
```

> **Πώς να χρησιμοποιήσετε CompletableFuture:** Με τη μεταβίβαση ενός `Executor` ελέγχετε το thread pool, διατηρώντας το UI ανταποκρινόμενο και αποφεύγοντας την εξάντληση νημάτων.

---

## Αναμενόμενο Αποτέλεσμα

Τρέξτε την κλάση `JsAsyncDemo` και θα δείτε:

```
JS result: Hello from async JS!
```

Η παύση των 500 ms δεν είναι ορατή στην κονσόλα, αλλά μπορείτε να προσθέσετε χρονικές σήμανσεις για να επαληθεύσετε την καθυστέρηση αν το επιθυμείτε.

---

## Ανακεφαλαίωση – Πώς να Εκτελέσετε JavaScript με CompletableFuture

Ξεκινήσαμε με **how to run javascript** μέσα στη Java, γράψαμε μια `async` συνάρτηση που **how to delay js**, την εκτελέσαμε με `evaluateAsync` (**how to evaluate async**) και κατεβάσαμε το αποτέλεσμα χρησιμοποιώντας ένα **how to use completablefuture**. Η ολοκληρωμένη ροή δείχνει **evaluate javascript asynchronously** σε ένα καθαρό, επαναχρησιμοποιήσιμο μοτίβο.

---

## Τι Ακολουθεί;

- **Ενσωμάτωση με HTTP clients:** Φέρτε δεδομένα από ένα REST endpoint μέσα στο async JS και επιστρέψτε τα στη Java.
- **Χρήση πολλαπλών scripts:** Συνδέστε αρκετές κλήσεις `evaluateAsync` για σύνθετους αγωγούς.
- **Αντικατάσταση μηχανών:** Το ίδιο μοτίβο λειτουργεί με Nashorn, GraalVM ή άλλες JavaScript runtime—απλώς αντικαταστήστε το `ScriptEngine`.

Νιώστε ελεύθεροι να πειραματιστείτε με μεγαλύτερες καθυστερήσεις, scripts που ρίχνουν σφάλματα, ή ακόμη και με μονάδες WebAssembly. Ο ουρανός είναι το όριο όταν συνδυάζετε τα primitives σύγχρονης εκτέλεσης της Java με το σύγχρονο JavaScript.

---

### Έχετε Ερωτήσεις;

Αν κάτι δεν είναι σαφές—ίσως αναρωτιέστε πώς να διαχειριστείτε μια απορριφθείσα υπόσχεση ή πώς να περάσετε μεταβλητές από τη Java στο script—αφήστε ένα σχόλιο παρακάτω. Καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}