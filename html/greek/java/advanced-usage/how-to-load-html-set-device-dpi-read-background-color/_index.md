---
category: general
date: 2026-02-16
description: Πώς να φορτώσετε HTML σε Java, να ορίσετε το DPI της συσκευής, να καθορίσετε
  ένα εικονικό μέγεθος οθόνης και να διαβάσετε το υπολογισμένο χρώμα φόντου οποιουδήποτε
  στοιχείου.
draft: false
keywords:
- how to load html
- read background color
- set device dpi
- set virtual screen size
- get computed background color
language: el
og_description: Πώς να φορτώσετε HTML σε Java, να ορίσετε το DPI της συσκευής, να
  ορίσετε ένα εικονικό μέγεθος οθόνης και να διαβάσετε το υπολογισμένο χρώμα φόντου
  οποιουδήποτε στοιχείου.
og_title: Πώς να φορτώσετε HTML, να ορίσετε το DPI της συσκευής και να διαβάσετε το
  χρώμα φόντου
tags:
- Aspose.HTML
- Java
title: Πώς να φορτώσετε HTML, να ορίσετε το DPI της συσκευής & να διαβάσετε το χρώμα
  φόντου
url: /el/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Φορτώσετε HTML, Ορίσετε DPI Συσκευής & Διαβάσετε το Χρώμα Φόντου

Έχετε αναρωτηθεί **πώς να φορτώσετε html** σε μια εφαρμογή Java και μετά να εξετάσετε τα στυλ της σελίδας; Δεν είστε μόνοι—οι προγραμματιστές συχνά χρειάζονται να αποδώσουν μια ιστοσελίδα εκτός οθόνης, να πάρουν τις τελικές τιμές CSS και να τις χρησιμοποιήσουν για μετατροπή σε PDF, στιγμιότυπα οθόνης ή ακόμη και αυτοματοποιημένες δοκιμές.  

Σε αυτόν τον οδηγό θα περάσουμε ακριβώς από αυτό: θα φορτώσουμε ένα αρχείο HTML, **ορίσουμε DPI συσκευής**, θα ορίσουμε **εικονικό μέγεθος οθόνης**, και τέλος **θα διαβάσουμε το χρώμα φόντου** από το στοιχείο `<body>`. Στο τέλος θα έχετε ένα πλήρως εκτελέσιμο απόσπασμα που εκτυπώνει το **υπολογισμένο χρώμα φόντου**—χωρίς μυστήριο, μόνο καθαρή Java.

## Τι Θα Χρειαστείτε

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

* Java 17 ή νεότερη (ο κώδικας λειτουργεί με οποιοδήποτε πρόσφατο JDK).  
* Aspose.HTML for Java 23.9 ή νεότερη — κατεβάστε το JAR από τον ιστότοπο της Aspose ή προσθέστε το μέσω Maven.  
* Ένα απλό αρχείο HTML (π.χ., `responsive.html`) που ορίζει χρώμα φόντου στο CSS.

Αυτό είναι όλο—χωρίς επιπλέον frameworks, χωρίς οδηγούς προγράμματος περιήγησης. Έτοιμοι; Ας ξεκινήσουμε.

![Diagram illustrating how to load html and extract computed styles](/images/load-html-diagram.png){alt="Diagram illustrating how to load html"}

## Βήμα 1: Πώς να Φορτώσετε HTML και να Διαμορφώσετε τις Επιλογές Απόδοσης

Το πρώτο πράγμα που κάνετε είναι να δημιουργήσετε ένα αντικείμενο `HtmlLoadOptions`. Αυτό το αντικείμενο λέει στην Aspose.HTML **πώς να φορτώσει html** — συμπεριλαμβανομένων των διαστάσεων της εικονικής οθόνης και του DPI που θέλετε να προσομοιώσετε.

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create load options and define the virtual screen size and DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        // setVirtualScreenSize – width × height in CSS pixels
        loadOptions.setScreenSize(new Size(1280, 800));
        // setDeviceDpi – typical desktop DPI (96 is the default for most monitors)
        loadOptions.setDeviceDpi(96);
```

**Γιατί αυτό είναι σημαντικό:**  
Ο καθορισμός ενός εικονικού μεγέθους οθόνης εξασφαλίζει ότι τα media queries όπως `@media (max-width: 600px)` συμπεριφέρονται σαν η σελίδα να αποδίδεται σε πραγματική οθόνη. Το DPI επηρεάζει το πώς οι μονάδες CSS `px` αντιστοιχίζονται σε φυσικά pixel — κρίσιμο όταν αργότερα δημιουργείτε εικόνες ή PDF.

## Βήμα 2: Φορτώστε το Αρχείο HTML Χρησιμοποιώντας τις Διαμορφωμένες Επιλογές

Τώρα φορτώνουμε πραγματικά το αρχείο. Παρατηρήστε ότι περνάμε τις ίδιες `loadOptions` που μόλις διαμορφώσαμε.

```java
        // 2️⃣ Load the HTML file with the options we just set.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);
```

Αν το αρχείο δεν βρεθεί, η Aspose ρίχνει μια σαφή `FileNotFoundException`. Σε παραγωγή ίσως θέλετε να το τυλίξετε σε try‑catch και να επιστρέψετε μια προεπιλεγμένη συμβολοσειρά HTML.

## Βήμα 3: Ορίστε το Εικονικό Μέγεθος Οθόνης και το DPI Συσκευής (Ρητά)

Ακόμη και αν έχουμε ήδη καλέσει `setScreenSize` και `setDeviceDpi` παραπάνω, αξίζει να τονιστεί ότι το **set virtual screen size** και το **set device dpi** μπορούν να προσαρμοστούν οποιαδήποτε στιγμή πριν από την απόδοση. Για παράδειγμα, μπορείτε να αυξήσετε το DPI για εικόνες υψηλής ανάλυσης:

```java
        // 3️⃣ Adjust DPI for a high‑resolution render (optional).
        loadOptions.setDeviceDpi(300);   // 300 DPI is common for print‑ready images
        // 4️⃣ Change screen size for a mobile layout test.
        loadOptions.setScreenSize(new Size(375, 667)); // iPhone X viewport
```

Θυμηθείτε να επαναφορτώσετε το έγγραφο αν αλλάξετε αυτές τις ρυθμίσεις μετά το πρώτο φόρτωμα — η Aspose τις θεωρεί αμετάβλητες μόλις δημιουργηθεί το `Document`.

## Βήμα 4: Διαβάστε το Χρώμα Φόντου και Λάβετε το Υπολογισμένο Χρώμα Φόντου

Με το έγγραφο στη μνήμη, μπορείτε να ερωτήσετε το υπολογισμένο στυλ οποιουδήποτε στοιχείου. Εδώ εστιάζουμε στην ετικέτα `<body>`, αλλά η ίδια προσέγγιση λειτουργεί για `<div>`, `<p>` ή ακόμη και ψευδο‑στοιχεία.

```java
        // 5️⃣ Retrieve the <body> element.
        Element bodyElement = document.getBody();

        // 6️⃣ Output the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

**Τι θα δείτε:** Αν το `responsive.html` περιέχει `body { background: #ff5722; }`, η κονσόλα εκτυπώνει κάτι όπως:

```
Computed background color: rgba(255,87,34,1)
```

Αυτό είναι το αποτέλεσμα του **get computed background color** — η Aspose επιλύει όλους τους κανόνες καταρράκτη CSS, τα media queries και ακόμη και τις δηλώσεις `!important` πριν επιστρέψει την τελική τιμή.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα, εδώ είναι το πλήρες, έτοιμο για αντιγραφή πρόγραμμα:

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create load options – virtual screen size + DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        loadOptions.setScreenSize(new Size(1280, 800)); // set virtual screen size
        loadOptions.setDeviceDpi(96);                  // set device DPI (default desktop)

        // Optional: tweak for high‑resolution or mobile rendering.
        // loadOptions.setDeviceDpi(300);
        // loadOptions.setScreenSize(new Size(375, 667));

        // Step 2: Load the HTML document with the options.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);

        // Step 3: Grab the <body> element.
        Element bodyElement = document.getBody();

        // Step 4: Print the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

### Αναμενόμενη Έξοδος

```
Computed background color: rgba(255,255,255,1)
```

*(Οι ακριβείς τιμές RGBA εξαρτώνται από το CSS στο αρχείο HTML σας.)*

## Συνηθισμένα Παράπτωμα & Επαγγελματικές Συμβουλές

* **Λείπει η ρύθμιση DPI;** Η Aspose προεπιλογή είναι 96 DPI, που μπορεί να θολώσει τις εικόνες υψηλής ανάλυσης. Ορίστε το ρητά πάντα αν χρειάζεστε καθαρό αποτέλεσμα.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}