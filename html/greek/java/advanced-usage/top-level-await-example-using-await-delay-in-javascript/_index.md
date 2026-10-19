---
category: general
date: 2026-03-26
description: Παράδειγμα top‑level await που δείχνει await delay JavaScript, κλάση
  αύξησης μετρητή και δημόσια πεδία κλάσης JavaScript σε ζωντανή επίδειξη.
draft: false
keywords:
- top level await example
- await delay javascript
- increment counter class
- public class fields javascript
- javascript class public field
language: el
og_description: Παράδειγμα top‑level await που επιδεικνύει την καθυστέρηση await σε
  JavaScript, κλάση αύξησης μετρητή και δημόσια πεδία κλάσης σε JavaScript σε ένα
  σύντομο οδηγό.
og_title: Παράδειγμα top-level await – Χρήση await delay στη JavaScript
tags:
- JavaScript
- ES2022
- async‑await
- classes
title: Παράδειγμα top‑level await – Χρήση await delay στη JavaScript
url: /el/java/advanced-usage/top-level-await-example-using-await-delay-in-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# top level await example – Using await delay in JavaScript

Έχετε αναρωτηθεί ποτέ πώς να διακόψετε την εκτέλεση ενός module χωρίς να τυλίξετε τα πάντα σε ένα async IIFE; Αυτό ακριβώς κάνει ένα **top level await example**. Σε αυτό το tutorial θα περάσουμε από μια μικρή ιστοσελίδα που χρησιμοποιεί `await delay javascript` για να αναβάλει εργασία, και στη συνέχεια δημιουργεί μια `increment counter class` που αξιοποιεί **public class fields javascript**. Στο τέλος θα έχετε ένα πλήρες, αντιγράψτε‑και‑επικολλήστε snippet που τρέχει σε οποιονδήποτε σύγχρονο περιηγητή.

Θα καλύψουμε τα πάντα, από τον ορισμό μιας κλάσης με public field μέχρι τη σύνδεση ενός απλού helper καθυστέρησης βασισμένου σε promises. Χωρίς εξωτερικές βιβλιοθήκες, χωρίς βήμα build—μόνο απλό HTML, ένα `<script type="module">`, και τα πιο πρόσφατα χαρακτηριστικά του ECMAScript. Αν είστε ήδη άνετοι με async functions, θα δείτε γιατί το top‑level await φαίνεται σαν φυσική επέκταση. Αν είστε νέοι στη **javascript class public field** σύνταξη, μην ανησυχείτε—εξηγούμε το «γιατί» πίσω από κάθε γραμμή.

## What You’ll Learn

- Πώς λειτουργεί ένα **top level await example** μέσα σε ένα module script.
- Το pattern για έναν `await delay javascript` helper που μιμείται το `setTimeout` με promises.
- Πώς να γράψετε μια **increment counter class** που χρησιμοποιεί ένα public field (`count`) και ένα static initialization block.
- Το αναμενόμενο console output και πώς να επαληθεύσετε ότι το static block εκτελείται πριν από το υπόλοιπο script.
- Συμβουλές για την αντιμετώπιση κοινών προβλημάτων, όπως παλαιότεροι περιηγητές που δεν υποστηρίζουν top‑level await.

> **Pro tip:** Modern browsers (Chrome 106+, Firefox 102+, Edge 106+) already support top‑level await. If you need to support older environments, consider bundling with a tool like Vite or Babel.

## Step 1 – Define a Class with a Public Field and a Static Block

Το πρώτο κομμάτι της επίδειξής μας είναι μια κλάση που αποθηκεύει έναν αριθμητικό μετρητή. Παρατηρήστε τη γραμμή `count = 0;`—αυτή είναι η **public class fields javascript** σύνταξη που εισήχθη στο ES2022. Δημιουργεί μια ιδιότητα του instance χωρίς constructor.

```html
<!DOCTYPE html>
<html>
<head>
    <title>ECMAScript 2022 Demo</title>
</head>
<body>
<img src="placeholder.png" alt="top level await example screenshot" title="top level await example">

<script type="module">
    // Step 1: Class definition
    class Counter {
        // Public field holds the current count
        count = 0;

        // Static block runs once when the class is first evaluated
        static {
            console.log('Counter class initialized');
        }

        // Simple method that increments the public field
        increment() {
            this.count++;
        }
    }
```

**Why a static block?** It lets us run one‑off initialization logic (like logging) the moment the module is parsed, *before* any top‑level await runs. This guarantees the message appears first in the console, proving that the class was evaluated early.

## Step 2 – Create an `await delay javascript` Helper

Στη συνέχεια χρειαζόμαστε μια μικρή συνάρτηση delay βασισμένη σε promise. Είναι ουσιαστικά ένας wrapper γύρω από το `setTimeout`, αλλά επιστρέφει ένα promise ώστε να μπορεί να χρησιμοποιηθεί με await.

```javascript
    // Step 2: Promise‑based delay helper
    const delay = ms => new Promise(resolve => setTimeout(resolve, ms));
```

**Edge case:** If `ms` is negative or not a number, `setTimeout` treats it as `0`. You could add validation, but for a demo the one‑liner keeps things readable.

## Step 3 – Use Top‑Level Await to Pause Execution

Τώρα έρχεται το αστέρι της παράστασης: top‑level await. Επειδή το script μας είναι module (`type="module"`), μπορούμε να τοποθετήσουμε `await` απευθείας στο top scope. Αυτό παγώνει το module μέχρι να λυθεί το promise, επιτρέποντάς μας να ελέγξουμε τη σειρά των side effects.

```javascript
    // Step 3: Top‑level await – delay half a second
    await delay(500);   // Wait 500 ms so the static block logs first
```

**Common question:** “Can I use top‑level await in a normal `<script>` tag?” No—only module scripts support it. If you forget `type="module"`, you’ll get a syntax error.

## Step 4 – Instantiate the Class, Increment, and Log the Result

Τέλος, συνδυάζουμε τα πάντα: δημιουργούμε ένα instance, καλούμε `increment()`, και εμφανίζουμε το τελικό count. Αυτό δείχνει την **increment counter class** σε δράση.

```javascript
    // Step 4: Work with the Counter instance
    const counterInstance = new Counter();
    counterInstance.increment();               // count becomes 1
    console.log('Final count:', counterInstance.count);
</script>
</body>
</html>
```

### Expected Console Output

```
Counter class initialized
Final count: 1
```

Αν ανοίξετε τη σελίδα στα DevTools, θα πρέπει να δείτε το μήνυμα του static‑block να εμφανίζεται **πριν** ολοκληρωθεί η καθυστέρηση, επιβεβαιώνοντας ότι η κλάση αξιολογήθηκε πρώτα.

## Step 5 – Why Use Public Class Fields Instead of a Constructor?

Μπορεί να αναρωτιέστε γιατί δεν γράψαμε:

```javascript
class Counter {
    constructor() {
        this.count = 0;
    }
}
```

Both approaches work, but **public class fields javascript** give you a cleaner, more declarative syntax. The field is defined once, not inside every constructor call, which can be easier to read when the class grows larger. Additionally, static blocks can’t be placed inside a constructor, so separating initialization logic becomes more natural.

## Step 6 – Adapting the Example for Real‑World Apps

Σε παραγωγή συχνά χρειάζεστε περισσότερους από έναν μετρητή. Εδώ είναι μερικές γρήγορες ιδέες:

- **Multiple counters:** Store them in a `Map` keyed by identifier.
- **Persisted state:** Replace `console.log` with `localStorage` writes.
- **Async initialization:** Use the static block to fetch configuration from a server before any instances are created.

All of these patterns still benefit from top‑level await, because you can fetch data once at module load time and guarantee it’s ready for every consumer.

## Frequently Asked Questions

**Q: Does top‑level await block other modules?**  
A: No. Each module runs independently. Only the module that contains the await is paused; other modules continue loading in parallel.

**Q: What if the delay promise rejects?**  
A: An unhandled rejection will abort the module evaluation and surface as an error in the console. Wrap the await in a `try…catch` if you need graceful fallback.

**Q: Is the `static` keyword required?**  
A: Not for the counter itself, but the static block is a handy way to demonstrate that code runs *once* at load time—great for logging or feature‑detection.

## Conclusion

You’ve just built a **top level await example** that showcases `await delay javascript`, an **increment counter class**, and the power of **public class fields javascript**. The complete, runnable snippet lives above, and the console output proves that the static block fires before the delayed code runs.  

From here you can experiment with more complex async flows, swap the delay for a real API call, or expand the class with additional methods. Remember, modern JavaScript lets you treat modules as first‑class async entities—no extra wrappers needed.

Happy coding, and feel free to drop your variations in the comments. If you found this guide useful, share it with a teammate who’s still wrestling with async patterns!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}