---
category: general
date: 2026-04-26
description: Μάθετε πώς να διαβάζετε CSS με το sandbox Aspose HTML, να προσομοιώνετε
  οθόνη κινητού, να ορίζετε την αναλογία pixel της συσκευής, να λαμβάνετε το στυλ
  του στοιχείου και να δοκιμάζετε ερωτήματα μέσων σε Java.
draft: false
keywords:
- how to read css
- simulate mobile screen
- get element style
- set device pixel ratio
- how to test media queries
language: el
og_description: Πώς να διαβάσετε CSS σε Java χρησιμοποιώντας το sandbox Aspose HTML.
  Προσομοιώστε μια οθόνη κινητού, ορίστε την αναλογία εικονοστοιχείων της συσκευής,
  λάβετε το στυλ του στοιχείου και δοκιμάστε τα media queries.
og_title: Πώς να διαβάσετε CSS σε Java – Προσομοίωση κινητών & Δοκιμή ερωτημάτων μέσων
tags:
- Aspose.HTML
- Java
- CSS testing
title: Πώς να διαβάσετε CSS σε Java – Προσομοίωση οθόνης κινητού & Δοκιμή ερωτημάτων
  μέσων
url: /el/java/css-html-form-editing/how-to-read-css-in-java-simulate-mobile-screen-test-media-qu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να διαβάσετε CSS σε Java – Προσομοίωση κινητής οθόνης & Δοκιμή Media Queries

Έχετε αναρωτηθεί ποτέ **πώς να διαβάσετε CSS** από ένα ζωντανό έγγραφο HTML ενώ προσποιείστε ότι βρίσκεστε σε ένα τηλέφωνο; Ίσως τροποποιείτε ένα ανταποκρινόμενο hero banner και χρειάζεται να επαληθεύσετε το χρώμα φόντου που παράγει ένα media query. Σε αυτό το tutorial θα σας δείξουμε μια πλήρη, εκτελέσιμη λύση που σας επιτρέπει να **προσομοιώσετε μια κινητή οθόνη**, **ορίσετε το device pixel ratio**, **λάβετε το στυλ του στοιχείου**, και **δοκιμάσετε media queries**—όλα με το Aspose HTML for Java.

Θα αποκτήσετε ένα αυτόνομο πρόγραμμα που ανοίγει ένα αρχείο HTML μέσα σε sandbox, διαβάζει την υπολογισμένη τιμή CSS ενός στοιχείου και την εκτυπώνει στην κονσόλα. Χωρίς εξωτερικά προγράμματα περιήγησης, χωρίς χειροκίνητη επιθεώρηση—απλώς καθαρός κώδικας Java που κάνει το δύσκολο για εσάς.

## Τι θα μάθετε

- Πώς να διαμορφώσετε ένα sandbox ώστε να μιμείται ένα mobile viewport πλάτους 375 px.  
- Τα βήματα που απαιτούνται για τη φόρτωση ενός αρχείου HTML και την ερώτηση ενός στοιχείου DOM.  
- Πώς να ανακτήσετε το υπολογισμένο `background-color` (ή οποιαδήποτε άλλη ιδιότητα CSS) μετά την ενεργοποίηση των media queries.  
- Συμβουλές για την αντιμετώπιση κοινών προβλημάτων όταν **δοκιμάζετε media queries** προγραμματιστικά.  

**Prerequisites** – Χρειάζεστε Java 8 ή νεότερη, ένα IDE (IntelliJ IDEA, Eclipse ή VS Code) και τη βιβλιοθήκη Aspose HTML for Java στο classpath σας. Αυτό είναι όλο· δεν απαιτούνται επιπλέον προγράμματα περιήγησης ή headless drivers.

---

## Βήμα 1: Ρύθμιση του Sandbox για Προσομοίωση Κινητής Οθόνης

Το πρώτο που κάνουμε είναι να δημιουργήσουμε ένα `SandboxConfiguration` που προσποιείται ότι βλέπουμε ένα τηλέφωνο. Αυτό είναι ο πυρήνας του **πώς να διαβάσετε CSS** σε ένα ελεγχόμενο περιβάλλον.

```java
import com.aspose.html.sandbox.*;
import com.aspose.html.*;

public class SandboxTutorial {
    public static void main(String[] args) throws Exception {

        // Create a sandbox configuration that mimics a 375 px wide mobile screen
        SandboxConfiguration sandboxConfig = new SandboxConfiguration();
        sandboxConfig.setScreenSize(new ScreenSize(375, 667)); // width × height in CSS pixels
        sandboxConfig.setDevicePixelRatio(2.0);                // simulate a high‑DPI device

        // Open the sandbox using the configuration
        try (Sandbox sandbox = new Sandbox(sandboxConfig)) {
            // Remaining steps go here …
        }
    }
}
```

**Γιατί αυτό είναι σημαντικό:** Με την επιβολή του μεγέθους οθόνης και του device pixel ratio, η μηχανή του προγράμματος περιήγησης μέσα στο sandbox αξιολογεί τα media queries ακριβώς όπως θα έκανε ένα πραγματικό τηλέφωνο. Αν παραλείψετε αυτό το βήμα, θα λαμβάνετε πάντα CSS σε στυλ desktop, κάτι που αναιρεί τον σκοπό του **testing media queries**.

## Βήμα 2: Φόρτωση του HTML Εγγράφου σας μέσα στο Sandbox

Τώρα που το sandbox είναι έτοιμο, πρέπει να του δώσουμε το HTML που θέλουμε να εξετάσουμε. Τοποθετήστε ένα αρχείο με όνομα `responsive.html` δίπλα στο φάκελο πηγαίου κώδικα, ή προσαρμόστε τη διαδρομή ανάλογα.

```java
// Load the HTML document inside the sandbox
Document htmlDoc = sandbox.openDocument("YOUR_DIRECTORY/responsive.html");
```

**Συμβουλή:** Κρατήστε το δοκιμαστικό HTML σας ελάχιστο—μόνο το στοιχείο που σας ενδιαφέρει συν το σχετικό CSS. Αυτό επιταχύνει τη φόρτωση και κάνει το debugging πιο εύκολο.

## Βήμα 3: Επιλογή του Στόχου Στοιχείου (Λήψη Στυλ Στοιχείου)

Με το έγγραφο φορτωμένο, μπορούμε να ερωτήσουμε οποιονδήποτε κόμβο DOM. Σε αυτό το παράδειγμα στοχεύουμε σε ένα στοιχείο με το ID `hero`. Η μέθοδος `querySelector` λειτουργεί ακριβώς όπως το εγγενές API του προγράμματος περιήγησης.

```java
// Select the target element whose style is affected by media queries
Element targetElement = htmlDoc.querySelector("#hero");
```

Αν ο selector επιστρέψει `null`, ελέγξτε ξανά ότι το ID υπάρχει στο HTML σας. Ένα κοινό λάθος είναι να ξεχάσετε το πρόθεμα `#` όταν χρησιμοποιείτε selector ID.

## Βήμα 4: Ανάγνωση της Υπολογισμένης Ιδιότητας CSS (Πώς να διαβάσετε CSS)

Τώρα έρχεται η καρδιά του **πώς να διαβάσετε CSS**: ζητάμε από το στοιχείο το υπολογισμένο του στυλ, το οποίο ήδη λαμβάνει υπόψη τους κανόνες cascade και τα ενεργά media queries.

```java
// Read the computed background color after the media query is applied
String backgroundColor = targetElement.getComputedStyle().getBackgroundColor();
```

Μπορείτε να αντικαταστήσετε το `getBackgroundColor()` με οποιαδήποτε άλλη μέθοδο ιδιότητας CSS (`getFontSize()`, `getMarginTop()`, κ.λπ.). Το αντικείμενο `ComputedStyle` αντικατοπτρίζει τις τιμές που θα δείτε στα εργαλεία προγραμματιστή του προγράμματος περιήγησης.

## Βήμα 5: Έξοδος του Αποτελέσματος – Επαλήθευση της Λογικής των Media Queries

Τέλος, εκτυπώνουμε την τιμή στην κονσόλα. Αυτό είναι ένας γρήγορος έλεγχος λογικής που επιβεβαιώνει αν το media query λειτούργησε όπως αναμενόταν.

```java
// Output the computed style value
System.out.println("Computed background: " + backgroundColor);
```

Όταν εκτελέσετε το πρόγραμμα, θα πρέπει να δείτε κάτι όπως:

```
Computed background: rgb(255, 0, 0)
```

Αν η έξοδος ταιριάζει με το χρώμα που ορίζεται στο mobile‑specific media query, συγχαρητήρια—έχετε επιτυχώς **tested media queries** προγραμματιστικά!

## Πλήρες, Εκτελέσιμο Παράδειγμα

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι η πλήρης κλάση Java που μπορείτε να αντιγράψετε‑επικολλήσετε στο πρότζεκτ σας:

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.sandbox.*;

public class SandboxTutorial {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox configuration that mimics a 375 px wide mobile screen
        SandboxConfiguration sandboxConfig = new SandboxConfiguration();
        sandboxConfig.setScreenSize(new ScreenSize(375, 667));
        sandboxConfig.setDevicePixelRatio(2.0);

        // Step 2: Open a sandbox using the configuration
        try (Sandbox sandbox = new Sandbox(sandboxConfig)) {

            // Step 3: Load the HTML document inside the sandbox
            Document htmlDoc = sandbox.openDocument("YOUR_DIRECTORY/responsive.html");

            // Step 4: Select the target element whose style is affected by media queries
            Element targetElement = htmlDoc.querySelector("#hero");

            // Step 5: Read the computed background color after the media query is applied
            String backgroundColor = targetElement.getComputedStyle().getBackgroundColor();

            // Step 6: Output the computed style value
            System.out.println("Computed background: " + backgroundColor);
        }
    }
}
```

Αποθηκεύστε το αρχείο ως `SandboxTutorial.java`, αντικαταστήστε το `YOUR_DIRECTORY` με τη διαδρομή προς το HTML σας, μεταγλωττίστε με `javac` και τρέξτε με `java`. Η κονσόλα θα εμφανίσει το υπολογισμένο χρώμα φόντου, επιβεβαιώνοντας ότι η ρύθμιση **simulate mobile screen** λειτούργησε.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν το στοιχείο έχει πολλαπλές κλάσεις που επηρεάζουν το στυλ του;

Το υπολογισμένο στυλ ήδη συγχωνεύει όλους τους εφαρμόσιμους κανόνες, οπότε δεν χρειάζεται να επιλύσετε χειροκίνητα την ειδικότητα. Απλώς καλέστε `getComputedStyle()` στο στοιχείο που επιλέξατε.

### Μπορώ να δοκιμάσω άλλες ιδιότητες media (π.χ., orientation);

Απολύτως. Προσαρμόστε το `ScreenSize` ή προσθέστε `sandboxConfig.setOrientation(ScreenOrientation.LANDSCAPE);` (αν το API το υποστηρίζει). Το sandbox θα αξιολογήσει τότε τους κανόνες `@media (orientation: landscape)` αναλόγως.

### Πώς μπορώ να αλλάξω το device pixel ratio εν κινήσει;

Δημιουργήστε ένα νέο `SandboxConfiguration` με διαφορετική τιμή `setDevicePixelRatio()` και ανοίξτε ξανά το sandbox. Αυτό είναι χρήσιμο για δοκιμή Retina vs. non‑Retina οθονών.

### Τι γίνεται αν το CSS μου χρησιμοποιεί μονάδες `rem`;

`rem` υπολογίζεται από το μέγεθος γραμματοσειράς του ριζικού στοιχείου, το οποίο επίσης επηρεάζεται από τις ρυθμίσεις του viewport του sandbox. Βεβαιωθείτε ότι το βασικό `html { font-size: … }` είναι ορισμένο στο δοκιμαστικό HTML.

## Οπτική Αναφορά

![πώς να διαβάσετε css σε προσομοίωση sandbox](https://example.com/images/css-read-sandbox.png "πώς να διαβάσετε css σε προσομοίωση sandbox")

*Το στιγμιότυπο οθόνης δείχνει την έξοδο της κονσόλας μετά την εκτέλεση του κώδικα του tutorial.*

## Συμπέρασμα

Τώρα έχετε μια στέρεη, ολοκληρωμένη συνταγή για **πώς να διαβάσετε CSS** από ένα έγγραφο HTML ενώ **προσομοιώνετε μια κινητή οθόνη**, **ορίζετε το device pixel ratio**, και **δοκιμάζετε media queries** προγραμματιστικά. Χρησιμοποιώντας το sandbox του Aspose HTML αποφεύγετε ασταθή δοκιμές που εξαρτώνται από το πρόγραμμα περιήγησης και αποκτάτε καθοριστικά αποτελέσματα που μπορείτε να ενσωματώσετε σε CI pipelines.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να εξάγετε άλλες υπολογισμένες ιδιότητες (μέγεθος γραμματοσειράς, περιθώριο κ.λπ.), να επαναλάβετε πάνω σε μια λίστα selectors, ή να ενσωματώσετε αυτή τη λογική σε μια σειρά δοκιμών JUnit. Το ίδιο μοτίβο λειτουργεί για οποιοδήποτε responsive component που χρειάζεται να επικυρώσετε.

Καλό κώδικα, και εύχομαι τα media queries σας να λειτουργούν πάντα όπως προορίζεται!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}