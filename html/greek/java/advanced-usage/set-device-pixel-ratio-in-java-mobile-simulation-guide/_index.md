---
category: general
date: 2026-04-05
description: Μάθετε πώς να ορίσετε το λόγο εικονοστοιχείων της συσκευής (device pixel
  ratio) σε Java χρησιμοποιώντας το sandbox του Aspose.HTML, να ορίσετε προσαρμοσμένο
  user agent, να προσομοιώσετε κινητή συσκευή, να λάβετε το υπολογισμένο στυλ σε Java
  και να ανακτήσετε το φόντο του στοιχείου.
draft: false
keywords:
- set device pixel ratio
- set custom user agent
- simulate mobile device
- get computed style java
- retrieve element background
language: el
og_description: Ορίστε την αναλογία pixel της συσκευής σε Java με το sandbox του Aspose.HTML,
  ορίστε προσαρμοσμένο user agent, προσομοιώστε κινητή συσκευή, λάβετε το υπολογισμένο
  στυλ σε Java και ανακτήστε το φόντο του στοιχείου.
og_title: Ορισμός αναλογίας εικονοστοιχείων συσκευής σε Java – Οδηγός προσομοίωσης
  κινητών
tags:
- Aspose.HTML
- Java
- Web testing
title: Ορισμός αναλογίας pixel συσκευής σε Java – Οδηγός προσομοίωσης κινητών
url: /el/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-simulation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# set device pixel ratio in Java – Οδηγός προσομοίωσης κινητής

Ever needed to **set device pixel ratio** in Java to see how a page looks on a retina‑ready phone? You're not the only one. With Aspose.HTML you can spin up a sandbox, **set custom user agent**, and even **retrieve element background** colors—all without leaving your IDE.

Έχετε χρειαστεί ποτέ να **set device pixel ratio** σε Java για να δείτε πώς φαίνεται μια σελίδα σε ένα τηλέφωνο με οθόνη retina; Δεν είστε ο μόνος. Με το Aspose.HTML μπορείτε να δημιουργήσετε ένα sandbox, **set custom user agent**, και ακόμη **retrieve element background** χρώματα—όλα χωρίς να αφήσετε το IDE σας.

In this tutorial we’ll walk through creating a sandbox that **simulate mobile device** behavior, adjusting the pixel density, pulling the computed CSS, and printing the header’s background. By the end you’ll have a complete, runnable example that works with any responsive site. No external tools, just plain Java and the Aspose.HTML library.

Σε αυτό το tutorial θα περάσουμε από τη δημιουργία ενός sandbox που **simulate mobile device** συμπεριφορά, ρυθμίζοντας την πυκνότητα εικονοστοιχείων, εξάγοντας το υπολογισμένο CSS, και εκτυπώνοντας το φόντο της κεφαλίδας. Στο τέλος θα έχετε ένα πλήρες, εκτελέσιμο παράδειγμα που λειτουργεί με οποιονδήποτε responsive ιστότοπο. Χωρίς εξωτερικά εργαλεία, μόνο απλή Java και η βιβλιοθήκη Aspose.HTML.

## Προαπαιτούμενα

- Java 17 ή νεότερη (ο κώδικας μεταγλωττίζεται με παλαιότερες εκδόσεις αλλά συνιστάται η 17).
- Aspose.HTML for Java 23.4 ή νεότερη – μπορείτε να κατεβάσετε το JAR από το Maven Central.
- Μία βασική κατανόηση του HTML και CSS (δεν απαιτείται τίποτα περίπλοκο).
- Πρόσβαση στο Internet για τη σελίδα demo (`https://example.com/responsive.html`).

> **Pro tip:** Εάν βρίσκεστε πίσω από εταιρικό proxy, ορίστε τις ιδιότητες proxy του JVM πριν εκτελέσετε το demo.

## Step 1: Πώς να **set device pixel ratio** σε ένα sandbox

Το πρώτο πράγμα που κάνετε είναι να δημιουργήσετε μια παρουσία `Sandbox` και να της δηλώσετε το λογικό μέγεθος viewport της συσκευής που θέλετε να μιμηθείτε. Στη συνέχεια, χρησιμοποιείτε το `setDevicePixelRatio` για να ενημερώσετε τη μηχανή απόδοσης ότι κάθε εικονοστοιχείο CSS αντιστοιχεί σε δύο φυσικά εικονοστοιχεία—όπως ένα iPhone 6/7/8.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // Create a sandbox that pretends to be a mobile phone
        Sandbox mobileSandbox = new Sandbox();

        // Define the logical screen size (width × height in CSS pixels)
        mobileSandbox.setViewportSize(new Size(375, 667)); // iPhone 6/7/8 dimensions

        // 👇 This is where we **set device pixel ratio** to 2.0
        mobileSandbox.setDevicePixelRatio(2.0);

        // Continue with the rest of the steps…
```

Γιατί είναι σημαντικό; Τα προγράμματα περιήγησης χρησιμοποιούν την device pixel ratio για να αποφασίσουν πόσο καθαρές εμφανίζονται οι εικόνες και πώς ενεργοποιούνται τα media queries όπως `@media (min-device-pixel-ratio: 2)`. Συμφωνώντας με την αναλογία, λαμβάνετε μια ακριβή αναπαράσταση της σελίδας σε οθόνες υψηλής πυκνότητας.

## Step 2: **set custom user agent** για ρεαλιστικές κεφαλίδες αιτήματος

Οι ιστοσελίδες συχνά παρέχουν διαφορετικό markup βάσει της συμβολοσειράς `User‑Agent`. Για να κάνει το sandbox σας να πιστεύει πραγματικά ότι είναι ένα iPhone, πρέπει να **set custom user agent**. Αυτό αποτρέπει την ανακατεύθυνση σε έκδοση desktop ή τη λήψη γενικής εναλλακτικής.

```java
        // Set a realistic iPhone user‑agent string
        mobileSandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0 Mobile/15E148 Safari/604.1"
        );
```

Παρατηρήστε τη διακοπή γραμμής και τη συνένωση συμβολοσειρών—διατηρεί το μήκος της γραμμής αναγνώσιμο. Αν παραλείψετε αυτό το βήμα, ο διακομιστής μπορεί να νομίζει ότι είστε ένα desktop Chrome και να σερβίρει εντελώς διαφορετική διάταξη, κάτι που αναιρεί τον σκοπό του testing **simulate mobile device**.

## Step 3: Φορτώστε τη σελίδα και **simulate mobile device** συμπεριφορά

Τώρα που το sandbox είναι διαμορφωμένο, μπορείτε να φορτώσετε οποιοδήποτε responsive URL. Το sandbox θα εφαρμόσει αυτόματα το μέγεθος viewport, την pixel ratio και το user‑agent που μόλις ορίσατε, προσομοιώνοντας αποτελεσματικά τις συνθήκες **simulate mobile device**.

```java
        // Load the responsive HTML document inside the configured sandbox
        try (HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com/responsive.html", mobileSandbox)) {

            // From here on we work with the DOM just like a normal browser
```

Εάν η στόχευση σελίδα χρησιμοποιεί lazy‑loading εικόνες ή JavaScript που εξαρτάται από το `window.innerWidth`, όλα θα συμπεριφέρονται ακριβώς όπως σε ένα πραγματικό iPhone. Αυτό είναι ιδιαίτερα χρήσιμο για CI pipelines όπου χρειάζεστε καθοριστικά screenshots ή επαλήθευση CSS.

## Step 4: Πώς να **get computed style java** για ένα στοιχείο

Μόλις φορτωθεί το έγγραφο, μπορείτε να ερωτήσετε οποιοδήποτε στοιχείο και να ζητήσετε από τη μηχανή τις *computed* τιμές CSS. Στη Java η μέθοδος είναι `getComputedStyle()`. Αυτό είναι η καρδιά της χρήσης **get computed style java**.

```java
            // Locate the <header> element we want to inspect
            HTMLElement headerElement = htmlDoc.getElementsByTagName("header").item(0);

            // Retrieve the computed CSS style for that element
            CSSStyleDeclaration computedStyle = headerElement.getComputedStyle();

            // Now we can read any property—background‑color, font‑size, etc.
```

Γιατί να μην διαβάσετε απλώς το inline style; Επειδή πολλές ιστοσελίδες ορίζουν χρώματα μέσω εξωτερικών φύλλων στυλ ή media queries. Το `getComputedStyle` επιλύει όλα μετά την κατάρρευση, δίνοντάς σας την τελική τιμή που θα αποδώσει πραγματικά το πρόγραμμα περιήγησης.

## Step 5: **retrieve element background** και εκτύπωση του αποτελέσματος

Τέλος, εξάγουμε το χρώμα φόντου και το εμφανίζουμε. Αυτό δείχνει το **retrieve element background** σε μια καθαρή, μονογραμμή δήλωση.

```java
            // Output the background color that the browser would render
            System.out.println("Header background: " + computedStyle.getBackgroundColor());
        }
    }
}
```

Όταν εκτελέσετε το πρόγραμμα, θα πρέπει να δείτε κάτι όπως:

```
Header background: rgb(255, 255, 255)
```

Εάν η σελίδα χρησιμοποιεί σκοτεινή κεφαλίδα για κινητά, η έξοδος θα το αντικατοπτρίζει—ακριβώς ό,τι θα δείτε σε μια συσκευή με την ίδια **set device pixel ratio**.

## Οπτική επισκόπηση

![Διάγραμμα που δείχνει πώς το set device pixel ratio, το custom user agent, και το viewport συνδυάζονται μέσα στο Aspose.HTML sandbox για να προσομοιώσουν μια κινητή συσκευή](https://example.com/images/sandbox-diagram.png)

*Το alt κείμενο της εικόνας περιέχει τη βασική λέξη-κλειδί, βοηθώντας τόσο τους crawlers αναζήτησης όσο και τους αναγνώστες οθόνης.*

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

- **Missing viewport size** – Εάν παραλείψετε το `setViewportSize`, το sandbox προεπιλογή είναι ένα viewport μεγέθους desktop, και τα media queries σας δεν θα ενεργοποιηθούν.
- **Wrong pixel ratio** – Η χρήση του `1.0` αναιρεί τον σκοπό· τα περισσότερα σύγχρονα τηλέφωνα χρησιμοποιούν `2.0` ή `3.0`. Ελέγξτε τις προδιαγραφές της συσκευής αν χρειάζεστε ακριβή αντιστοιχία.
- **User‑Agent mismatches** – Κάποιες ιστοσελίδες ελέγχουν για `iPhone` *και* την έκδοση `OS`. Μείνετε σε μια πλήρη συμβολοσειρά όπως φαίνεται στο Step 2.
- **Resource loading errors** – Βεβαιωθείτε ότι το sandbox έχει πρόσβαση στο internet· διαφορετικά τα εξωτερικά CSS/JS δεν θα φορτωθούν, και το `getComputedStyle` μπορεί να επιστρέψει προεπιλογές.

## Επέκταση του παραδείγματος

Τώρα που μπορείτε να **set device pixel ratio**, **set custom user agent**, **simulate mobile device**, **get computed style java**, και **retrieve element background**, μπορεί να αναρωτιέστε τι άλλο μπορείτε να κάνετε.

- **Take screenshots** – Το Aspose.HTML μπορεί να αποδώσει το sandbox σε PNG ή JPEG, ιδανικό για visual regression testing.
- **Run JavaScript** – Το sandbox υποστηρίζει εκτέλεση script, ώστε να μπορείτε να δοκιμάσετε δυναμικές αλλαγές UI.
- **Iterate over breakpoints** – Επανάληψη σε διάφορα πλάτη viewport και pixel ratios για να επαληθεύσετε ένα responsive design σε όλο το φάσμα.

## Συμπέρασμα

Μόλις μάθατε πώς να **set device pixel ratio** σε Java, να διαμορφώσετε ένα **custom user agent**, να **simulate mobile device** συνθήκες, να **get computed style java**, και να **retrieve element background** χρησιμοποιώντας το sandbox API του Aspose.HTML. Το πλήρες απόσπασμα κώδικα παραπάνω είναι έτοιμο να επικολληθεί σε οποιοδήποτε Java project, να μεταγλωττιστεί και να εκτελεστεί.

Μη διστάσετε να προσαρμόσετε τις διαστάσεις του viewport, να δοκιμάσετε διαφορετικό URL, ή να πειραματιστείτε με άλλες ιδιότητες CSS όπως `font-size` ή `margin`. Το ίδιο μοτίβο λειτουργεί για οποιοδήποτε στοιχείο χρειάζεται να ελέγξετε, καθιστώντας αυτήν την προσέγγιση ένα ευέλικτο εργαλείο στο κουτί εργαλείων web‑testing σας.

Αν βρήκατε αυτόν τον οδηγό χρήσιμο, σκεφτείτε να τον μοιραστείτε με συναδέλφους ή να δώσετε αστέρι στο αποθετήριο Aspose.HTML στο GitHub. Καλή προγραμματιστική, και εύχομαι τα pixel‑perfect τεστ σας πάντα να περνούν!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}