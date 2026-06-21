---
category: general
date: 2026-03-28
description: Εξαγωγή τίτλου από HTML χρησιμοποιώντας το Aspose HTML για Java. Μάθετε
  πώς να εκτελείτε HTML σε sandbox, να φορτώνετε έγγραφο HTML σε Java και να ρυθμίζετε
  το χρονικό όριο του script σε λεπτά.
draft: false
keywords:
- extract title from html
- run html in sandbox
- load html document java
- configure script timeout
language: el
og_description: Εξαγωγή τίτλου από HTML χρησιμοποιώντας το Aspose HTML για Java. Αυτός
  ο οδηγός δείχνει πώς να εκτελέσετε HTML σε sandbox, να φορτώσετε έγγραφο HTML σε
  Java και να ρυθμίσετε το χρονικό όριο του script.
og_title: Εξαγωγή Τίτλου από HTML σε Java – Πλήρης Οδηγός Sandbox
tags:
- Java
- Aspose.HTML
- Web Scraping
title: Εξαγωγή τίτλου από HTML σε Java – Πλήρης Οδηγός Sandbox
url: /el/java/configuring-environment/extract-title-from-html-in-java-complete-sandbox-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή τίτλου από HTML σε Java – Πλήρης Οδηγός Sandbox

Κάποτε χρειάστηκε να **εξάγετε τίτλο από HTML** αλλά δεν ήσασταν σίγουροι πώς να εκτελέσετε τη σελίδα με ασφάλεια;  
Ίσως δοκιμάσατε να φορτώσετε ένα απομακρυσμένο αρχείο και να λάβατε `NullPointerException` επειδή το script δεν ολοκληρώθηκε.

Σε αυτό το tutorial θα σας δείξουμε έναν αδιάβλητο τρόπο για **εξαγωγή τίτλου από HTML** χρησιμοποιώντας το Aspose HTML for Java, κρατώντας το script μέσα σε sandbox, ρυθμίζοντας χρόνο λήξης script, και φορτώνοντας το έγγραφο HTML σε Java. Στο τέλος θα έχετε ένα έτοιμο κομμάτι κώδικα, μια σαφή εξήγηση κάθε ρύθμισης, και συμβουλές για την αντιμετώπιση ειδικών περιπτώσεων.

> **Τι θα μάθετε**
> - Πώς να **τρέξετε HTML σε sandbox** με προσαρμοσμένο μέγεθος οθόνης.  
> - Τα ακριβή βήματα για **φόρτωση HTML εγγράφου Java** χρησιμοποιώντας το Aspose HTML.  
> - Πώς να **ρυθμίσετε χρόνο λήξης script** ώστε τα ανεξέλεγκτα scripts να μην κρεμάσουν την εφαρμογή σας.  
> - Πώς να διαβάσετε το παραγόμενο `<title>` tag μετά το τέλος του script (ή το timeout).

---

![Εξαγωγή τίτλου από HTML sandbox](image-placeholder.png "Εξαγωγή τίτλου από HTML χρησιμοποιώντας sandbox Java")

## Επισκόπηση: Γιατί είναι Σημαντικό το Sandbox Όταν Εξάγετε Τίτλο από HTML

Σκεφτείτε το sandbox ως ένα μικρό, περιφραγμένο παιδικό πάρκο για τη σελίδα HTML.  
Αν η σελίδα περιέχει JavaScript που προσπαθεί να κατεβάσει εξωτερικούς πόρους, να ανοίξει νέα παράθυρα ή να μπει σε άπειρο βρόχο, το sandbox το σταματά αμέσως.  
Αυτό το δίχτυ ασφαλείας είναι ιδιαίτερα πολύτιμο όταν το μόνο που σας ενδιαφέρει είναι το στοιχείο `<title>` — δεν χρειάζεται να εκθέσετε ολόκληρο το JVM σε πιθανό κακόβουλο κώδικα.

Παρακάτω βρίσκεται το πλήρες, εκτελέσιμο παράδειγμα. Μπορείτε να το αντιγράψετε‑και‑επικολλήσετε σε ένα νέο Maven project με την εξάρτηση Aspose HTML for Java.

```java
import com.aspose.html.dom.Document;
import com.aspose.html.environment.Sandbox;
import com.aspose.html.environment.SandboxOptions;
import com.aspose.html.environment.ScriptExecutionOptions;

public class ExtractTitleDemo {
    public static void main(String[] args) {
        // 1️⃣ Configure sandbox display size (optional but helpful for layout‑dependent scripts)
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(800);
        sandboxOptions.setScreenHeight(600);

        // 2️⃣ Set a maximum script execution time – 2 seconds in this case
        ScriptExecutionOptions scriptOptions = new ScriptExecutionOptions();
        scriptOptions.setTimeout(2000); // milliseconds

        // 3️⃣ Create the sandbox, load the HTML file, and let the script run
        try (Sandbox sandbox = new Sandbox(sandboxOptions, scriptOptions);
             Document document = sandbox.openDocument("YOUR_DIRECTORY/scripted.html")) {

            // 4️⃣ The script has already run (or timed‑out). Grab the title.
            System.out.println("Title after script: " + document.getTitle());
        } catch (Exception e) {
            System.err.println("Failed to extract title: " + e.getMessage());
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα (όταν το script ολοκληρωθεί εντός 2 δευτερολέπτων):**

```
Title after script: My Awesome Page
```

Αν το script υπερβεί το όριο, το sandbox το ακυρώνει και εσείς λαμβάνετε ό,τι τίτλο υπήρχε πριν το timeout.

---

## Βήμα 1 – Ρύθμιση Χρόνου Λήξης Script (και γιατί είναι σημαντικό)

Όταν **ρυθμίζετε χρόνο λήξης script**, λέτε στο sandbox πόσο χρόνο μπορεί να τρέξει ένα script πριν αναγκαστικά σταματήσει.  
Ένα όριο 2 δευτερολέπτων είναι καλή αρχή· είναι αρκετό για τα περισσότερα scripts που τροποποιούν το DOM, αλλά αρκετά μικρό ώστε η υπηρεσία σας να παραμένει ανταποκρινόμενη.

```java
ScriptExecutionOptions scriptOptions = new ScriptExecutionOptions();
scriptOptions.setTimeout(2000); // 2000 ms = 2 seconds
```

> **Pro tip:** Αν παρατηρήσετε ότι έγκυρες σελίδες κόβονται, αυξήστε το timeout στα 5000 ms.  
> Αντίστροφα, αν επεξεργάζεστε μη αξιόπιστο περιεχόμενο, κρατήστε το χαμηλό για να αποφύγετε επιθέσεις άρνησης υπηρεσίας.

---

## Βήμα 2 – Φόρτωση HTML Εγγράφου Java (χρησιμοποιώντας Aspose HTML)

Η γραμμή `sandbox.openDocument("YOUR_DIRECTORY/scripted.html")` κάνει το βαριά έργο για το βήμα **φόρτωση HTML εγγράφου Java**.  
Το Aspose HTML αναλαμβάνει την ανάλυση, την εκτέλεση ενσωματωμένων scripts, και τη δημιουργία ενός DOM που μπορείτε να ερωτήσετε.

```java
Document document = sandbox.openDocument("YOUR_DIRECTORY/scripted.html");
```

Βεβαιωθείτε ότι η διαδρομή δείχνει σε πραγματικό αρχείο στον διακομιστή ή χρησιμοποιήστε ένα αντικείμενο `File`/`URL` αν προτιμάτε πιο δυναμική προσέγγιση.  
Το sandbox θα σεβαστεί αυτόματα τις διαστάσεις οθόνης που ορίσατε νωρίτερα, κάτι που μπορεί να επηρεάσει scripts που ελέγχουν το `window.innerWidth`.

---

## Βήμα 3 – Εκτέλεση HTML σε Sandbox: Αφήστε τη Μηχανή να Δουλέψει

Δεν χρειάζεται να καλέσετε κάποια επιπλέον μέθοδο “run” — το sandbox εκτελεί τη σελίδα αμέσως μόλις την ανοίξετε.  
Αυτή είναι η μαγεία του **run HTML in sandbox**: η μηχανή αναλύει το markup, πυροδοτεί το `DOMContentLoaded`, και εκτελεί τυχόν `<script>` tags — όλα μέσα σε απομονωμένο περιβάλλον.

Αν η σελίδα περιλαμβάνει `setTimeout` ή βρόχους μεγάλης διάρκειας, το timeout που ρυθμίσατε στο Βήμα 1 θα παρέμβει.  
Δεν απαιτείται επιπλέον κώδικας — απλώς καθίστε και αφήστε το sandbox να το διαχειριστεί.

---

## Βήμα 4 – Ανάκτηση του Τίτλου μετά την Εκτέλεση του Script

Αφού το sandbox ολοκληρωθεί (ή ακυρωθεί), μπορείτε να πάρετε τον τίτλο απευθείας από το DOM:

```java
String title = document.getTitle();
System.out.println("Title after script: " + title);
```

Ακόμη και αν το αρχικό HTML είχε κενό `<title>` και ένα script το έθεσε αργότερα, θα δείτε την τελική τιμή — ακριβώς αυτό που χρειάζεστε όταν **εξάγετε τίτλο από HTML**.

---

## Bonus: Χειρισμός Timeouts και Σφαλμάτων με Ευγένεια

Μια υλοποίηση για πραγματικό κόσμο πρέπει να προβλέπει δύο κοινά προβλήματα:

1. **Timeouts** – Το script δεν ολοκληρώθηκε έγκαιρα.  
   *Λύση:* Πιάστε την εξαίρεση timeout (το Aspose ρίχνει μια συγκεκριμένη υποκλάση) και επιστρέψτε τον αρχικό τίτλο ή ένα placeholder.

2. **Malformed HTML** – Το αρχείο δεν μπορεί να αναλυθεί.  
   *Λύση:* Τυλίξτε τη δημιουργία του sandbox σε block `try‑with‑resources` (όπως φαίνεται) και καταγράψτε το σφάλμα για μετέπειτα ανάλυση.

```java
catch (com.aspose.html.environment.ScriptTimeoutException toe) {
    System.err.println("Script timed out – using original title.");
    System.out.println("Title after script: " + document.getTitle());
}
```

---

## Συχνές Ερωτήσεις & Ειδικές Περιπτώσεις

**Τι γίνεται αν η σελίδα χρησιμοποιεί εξωτερικά scripts;**  
Το sandbox μπλοκάρει τα δίκτυα αιτήματα από προεπιλογή, οπότε αυτά τα scripts απλώς δεν θα τρέξουν. Αν *πραγματικά* τα χρειάζεστε, ενεργοποιήστε έναν προσαρμοσμένο `NetworkHandler` — αλλά αυτό αντιβαίνει στον σκοπό ενός ασφαλούς sandbox.

**Μπορώ να αλλάξω το viewport μετά τη δημιουργία του sandbox;**  
Όχι. Το `SandboxOptions` πρέπει να οριστεί πριν δημιουργηθεί το sandbox. Δημιουργήστε νέο sandbox αν χρειάζεστε διαφορετικό μέγεθος.

**Διατηρείται η κεφαλαιοποίηση του τίτλου;**  
Ναι. Το Aspose HTML επιστρέφει την ακριβή συμβολοσειρά που αποθηκεύεται στο στοιχείο `<title>` μετά την εκτέλεση του script, διατηρώντας κεφαλαία/μικρά και κενά.

---

## Ανακεφαλαίωση: Εξαγωγή Τίτλου από HTML με Πλήρη Έλεγχο

Διασχίσαμε μια ολοκληρωμένη, αυτόνομη λύση για **εξαγωγή τίτλου από HTML** ενώ:

- **Τρέχουμε HTML σε sandbox** για απομόνωση των scripts.  
- **Φορτώνουμε HTML έγγραφο Java** μέσω του `openDocument` του Aspose HTML.  
- **Ρυθμίζουμε χρόνο λήξης script** για αποφυγή ανεξέλεγκτου κώδικα.  
- Ανακτούμε τον τελικό τίτλο με ασφάλεια.

Πειραματιστείτε — αλλάξτε τις διαστάσεις οθόνης, αυξήστε το timeout, ή δείξτε το sandbox σε απομακρυσμένο URL (να θυμάστε ότι το sandbox θα συνεχίσει να μπλοκάρει τα δίκτυα αιτήματα εκτός αν το επιτρέψετε ρητά).

---

### Τι Ακολουθεί;

- **Ανάλυση άλλων meta tags** (π.χ. `description`, `og:title`) χρησιμοποιώντας το ίδιο αντικείμενο `Document`.  
- **Μαζική επεξεργασία πολλαπλών αρχείων** με βρόχο πάνω σε φάκελο και επαναχρησιμοποίηση των ρυθμίσεων sandbox.  
- **Ενσωμάτωση με web service** για να προσφέρετε ένα “title‑extraction API” σε downstream εφαρμογές.

Αν συναντήσετε δυσκολίες, αφήστε ένα σχόλιο ή ελέγξτε την τεκμηρίωση του Aspose HTML for Java — υπάρχουν πολλά παραδείγματα για handling frames, SVG, και άλλα.

Καλό κώδικα, και οι τίτλοι σας να είναι πάντα ακριβείς!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}