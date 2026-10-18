---
category: general
date: 2026-01-10
description: Δημιουργήστε PNG από HTML σε Java γρήγορα χρησιμοποιώντας το Aspose.HTML.
  Μάθετε πώς να αποδίδετε HTML σε PNG, να ορίζετε το user agent σε Java και να μετατρέπετε
  HTML σε PNG σε Java με ένα πλήρες παράδειγμα.
draft: false
keywords:
- create png from html
- render html to png
- set user agent java
- convert html to png java
language: el
og_description: Δημιουργήστε PNG από HTML σε Java με το Aspose.HTML. Αυτό το σεμινάριο
  σας καθοδηγεί στη μετατροπή HTML σε PNG, στον ορισμό προσαρμοσμένου πράκτορα χρήστη
  και στη μετατροπή HTML σε PNG με Java.
og_title: Δημιουργία PNG από HTML σε Java – Πλήρες Μάθημα Προγραμματισμού
tags:
- Java
- Aspose.HTML
- Image Rendering
title: Δημιουργία PNG από HTML σε Java – Πλήρης Οδηγός Βήμα‑Βήμα
url: /el/java/conversion-html-to-various-image-formats/create-png-from-html-in-java-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία PNG από HTML σε Java – Πλήρης Οδηγός Βήμα‑Βήμα

Έχετε ποτέ χρειαστεί να **create PNG from HTML** σε Java αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι· πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο εμπόδιο όταν προσπαθούν να μετατρέψουν δυναμικά αποσπάσματα ιστού σε στατικές εικόνες.  

Σε αυτό το άρθρο θα βρείτε μια έτοιμη προς εκτέλεση λύση που **renders HTML to PNG**, σας επιτρέπει να **set user agent Java** για δοκιμές σε στυλ κινητών, και καλύπτει όλα όσα χρειάζεστε για **convert HTML to PNG Java** χρησιμοποιώντας τη βιβλιοθήκη Aspose.HTML. Χωρίς εξωτερικές υπηρεσίες, χωρίς κρυφή μαγεία—απλός κώδικας Java που μπορείτε να αντιγράψετε‑επικολλήσετε.

## Τι Καλύπτει Αυτό το Σεμινάριο

Θα περάσουμε από κάθε κομμάτι του παζλ:

* Δημιουργία ενός μικρού HTML payload που περιλαμβάνει ένα media query.  
* Φόρτωση αυτού του markup σε ένα `Aspose.HTML` `Document`.  
* Διαμόρφωση του `RenderingOptions` ώστε η μηχανή να θεωρεί ότι είναι ένα τηλέφωνο (αυτό είναι όπου έρχεται το **set user agent java**).  
* Κατεύθυνση της εξόδου σε αρχείο PNG με `ImageRenderDevice`.  
* Εκτέλεση του render και έλεγχος του αποτελέσματος.

Στο τέλος θα έχετε ένα `sandbox_render.png` στον φάκελο του έργου σας, αποδεικνύοντας ότι μπορείτε να **create PNG from HTML** προγραμματιστικά.  

**Prerequisites** – χρειάζεστε Java 8 ή νεότερη, Maven ή Gradle για να κατεβάσετε την εξάρτηση Aspose.HTML, και μια μέτρια εξοικείωση με τη Java. Τίποτα άλλο.

---

## Βήμα 1: Προετοιμασία του HTML με Media Query

Πρώτα χρειαζόμαστε ένα απλό HTML string που να δείχνει πώς ένα mobile viewport μπορεί να αλλάξει τη διάταξη. Το media query παρακάτω κάνει το φόντο κόκκινο όταν το πλάτος είναι 600 px ή λιγότερο.

```java
// Step 1 – define HTML content
String htmlContent = "<style>@media (max-width:600px){body{background:red}}</style>"
                   + "<body>Test</body>";
```

> **Why this matters:** Όταν αργότερα **set user agent java**, η μηχανή απόδοσης θα θεωρήσει το έγγραφο ως οθόνη μεγέθους iPhone, προκαλώντας την ενεργοποίηση του media query. Αυτή είναι μια συνηθισμένη τεχνική για δοκιμή responsive σχεδίων χωρίς πρόγραμμα περιήγησης.

## Βήμα 2: Φόρτωση του HTML σε ένα Aspose Document

Η κλάση `Document` του Aspose.HTML είναι το σημείο εισόδου σας. Αναλύει το string και δημιουργεί ένα DOM που μπορείτε να χειριστείτε ή να αποδώσετε.

```java
// Step 2 – create the Document object
Document document = new Document(htmlContent);
```

> **Tip:** Εάν έχετε ένα εξωτερικό αρχείο HTML, μπορείτε να περάσετε τη διαδρομή του στον κατασκευαστή `Document` αντί για ένα string.

## Βήμα 3: Διαμόρφωση Rendering Options (Set User Agent Java)

Τώρα λέμε στον renderer ποια “συσκευή” προσομοιώνουμε. Οι βασικές ιδιότητες είναι το πλάτος, το ύψος, το DPI και η κεφαλίδα **user‑agent** που προσποιείται ότι είμαστε iPhone.

```java
// Step 3 – set up rendering options
RenderingOptions renderOptions = new RenderingOptions();
renderOptions.setDeviceWidth(375);      // logical CSS pixels (iPhone 6/7/8 width)
renderOptions.setDeviceHeight(667);    // height in pixels
renderOptions.setDeviceDpi(160);       // typical mobile DPI
renderOptions.setUserAgent(
    "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
    "AppleWebKit/605.1.15 (KHTML, like Gecko) Mobile/15E148");
```

> **Why set a custom user agent?** Ορισμένοι ιστότοποι παρέχουν διαφορετικό markup ανάλογα με τον πελάτη. Με το **setting user agent java** εξασφαλίζετε ότι το ίδιο περιεχόμενο που θα δείτε σε μια πραγματική συσκευή είναι αυτό που αποδίδεται σε PNG. Αυτό είναι ιδιαίτερα χρήσιμο για δοκιμή responsive προτύπων email ή landing pages.

## Βήμα 4: Επιλογή Image Render Device

Η Aspose χρησιμοποιεί την έννοια του “render device” για να αποφασίσει πού πηγαίνει η έξοδος. Εδώ το κατευθύνουμε σε αρχείο PNG.

```java
// Step 4 – create an image render device for PNG output
ImageRenderDevice renderDevice = new ImageRenderDevice(
    "YOUR_DIRECTORY/sandbox_render.png", ImageFormat.Png);
```

> **Pro tip:** Αντικαταστήστε το `YOUR_DIRECTORY` με μια απόλυτη ή σχετική διαδρομή που υπάρχει στον υπολογιστή σας. Η βιβλιοθήκη θα δημιουργήσει το αρχείο αν δεν υπάρχει ήδη.

## Βήμα 5: Απόδοση και Επαλήθευση της Εξόδου

Τέλος, εκτελούμε το render. Αν όλα είναι σωστά συνδεδεμένα, θα δείτε ένα PNG με κόκκινο φόντο (ευχαριστώντας το media query) με όνομα `sandbox_render.png`.

```java
// Step 5 – render the document
document.render(renderDevice, renderOptions);
System.out.println("Rendered with sandbox settings – check sandbox_render.png");
```

Η εκτέλεση του προγράμματος θα πρέπει να εκτυπώσει τη γραμμή επιβεβαίωσης, και το άνοιγμα του PNG θα εμφανίσει ένα ενιαίο κόκκινο φόντο με τη λέξη “Test” κεντραρισμένη—απόδειξη ότι έχετε δημιουργήσει επιτυχώς **create PNG from HTML**.

![Αποτέλεσμα PNG που αποδόθηκε – create png from html](sandbox_render.png "Αποτέλεσμα απόδοσης HTML σε PNG")

---

## Συνηθισμένα Προβλήματα Κατά τη Μετατροπή HTML σε PNG Java

| Σύμπτωμα | Πιθανή Αιτία | Διόρθωση |
|----------|---------------|----------|
| Κενή εικόνα | `DeviceWidth`/`DeviceHeight` ορισμένα σε 0 ή πολύ μικρά | Χρησιμοποιήστε ρεαλιστικές διαστάσεις (π.χ., 375 × 667) |
| Λάθος χρώματα ή διάταξη | Απουσία CSS ή εξωτερικών πόρων | Ενσωματώστε κρίσιμα CSS ή ενεργοποιήστε `loadExternalResources` στο `RenderingOptions` |
| Το αρχείο δεν δημιουργείται | Ο φάκελος εξόδου δεν υπάρχει ή δεν έχει δικαίωμα εγγραφής | Βεβαιωθείτε ότι ο φάκελος υπάρχει και είναι εγγράψιμος |
| Το media query δεν ενεργοποιείται ποτέ | Η συμβολοσειρά user‑agent είναι παρόμοια με επιτραπέζιο | **Set user agent java** σε συμβολοσειρά κινητού όπως φαίνεται παραπάνω |

## Επέκταση του Παραδείγματος: Πολλές Σελίδες και Μορφές

Εάν χρειάζεστε να **render HTML to PNG** για πολλές σελίδες, απλώς κάντε βρόχο πάνω σε μια συλλογή HTML strings, δημιουργώντας ένα νέο `Document` κάθε φορά, ή επαναχρησιμοποιήστε το ίδιο `Document` με διαφορετικά `RenderingOptions`. Μπορείτε επίσης να αλλάξετε το `ImageFormat` σε `Jpeg` ή `Bmp` αν η επόμενη διαδικασία σας προτιμά αυτά.

```java
// Example: render two pages to separate PNG files
String[] pages = {htmlContent, "<body><h1>Second page</h1></body>"};

for (int i = 0; i < pages.length; i++) {
    Document doc = new Document(pages[i]);
    ImageRenderDevice device = new ImageRenderDevice(
        "page_" + (i + 1) + ".png", ImageFormat.Png);
    doc.render(device, renderOptions);
}
```

## Περίληψη

Έχουμε καλύψει όλα όσα χρειάζεστε για **create PNG from HTML** σε Java:

1. Γράψτε το HTML (συμπεριλαμβανομένων των responsive κανόνων).  
2. Φορτώστε το με `Document`.  
3. **Set user agent java** και άλλες μετρήσεις συσκευής μέσω `RenderingOptions`.  
4. Κατευθύνετε ένα `ImageRenderDevice` σε αρχείο PNG.  
5. Καλέστε `document.render()` και επαληθεύστε το αποτέλεσμα.

Με αυτά τα βήματα μπορείτε επίσης να **render HTML to PNG** για email, αναφορές ή οποιαδήποτε εργασία αυτοματοποίησης που απαιτεί μια στατική λήψη του δυναμικού markup.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να μετατρέψετε ολόκληρο φάκελο ιστοσελίδας, ή πειραματιστείτε με έξοδο PDF αντικαθιστώντας το `ImageRenderDevice` με `PdfRenderDevice`. Οι ίδιες αρχές ισχύουν, και το Aspose.HTML API το κάνει αβίαστο.

Αν αντιμετωπίσατε κάποιο πρόβλημα, αφήστε ένα σχόλιο παρακάτω—καλή απόδοση!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}