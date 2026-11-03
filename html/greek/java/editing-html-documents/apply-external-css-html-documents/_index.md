---
date: 2026-06-24
description: Μάθετε πώς να δημιουργήσετε PDF από HTML και να προσθέσετε CSS σε έγγραφα
  HTML χρησιμοποιώντας το Aspose.HTML για Java – append style to head, set CSS class,
  and render to PDF.
keywords:
- create pdf from html
- append style to head
- set css class java
- inject css java
- add css html java
- convert html pdf java
linktitle: Δημιουργία PDF από HTML και Προσθήκη CSS με Aspose.HTML
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Learn how to create PDF from HTML and add CSS to HTML documents using
    Aspose.HTML for Java – append style to head, set CSS class, and render to PDF.
  headline: Create PDF from HTML and Add CSS with Aspose.HTML for Java
  type: TechArticle
- description: Learn how to create PDF from HTML and add CSS to HTML documents using
    Aspose.HTML for Java – append style to head, set CSS class, and render to PDF.
  name: Create PDF from HTML and Add CSS with Aspose.HTML for Java
  steps:
  - name: Create HTML document in Java
    text: The `HTMLDocument` class is Aspose.HTML's core object that represents an
      HTML file in memory. First off, we need to create our HTML document. We’ll start
      by defining the content with a simple HTML structure. Here, we defined a basic
      HTML structure, including a `<div>` with two paragraphs. The `HTMLD
  - name: Create a Style Element
    text: A `<style>` element is an HTML tag that holds CSS rules directly inside
      the document. Next, we will create a `style` element to hold our CSS rules.
      Using the `createElement` method of `HTMLDocument`, we create a new `<style>`
      element and set its content to include our CSS definitions for two classes
  - name: Append style to head
    text: Appending a style element to the `<head>` makes the browser (or Aspose renderer)
      apply the CSS to the whole page. Now that we have our CSS in place, we need
      to **append style to head** so the browser (or Aspose renderer) can apply it.
      We retrieve the head of the document and append our newly created
  - name: Set CSS class in Java
    text: 'The `setClassName` method assigns a CSS class name to an HTML element,
      linking it to the style rules defined earlier. Next, we’ll apply the previously
      defined CSS classes to our paragraph elements. Here, we access the first and
      last paragraph elements in the document and assign them the CSS classes '
  - name: Set Additional Style Properties
    text: The `setStyleProperty` method lets you modify individual CSS properties
      on an element after it has been created. To enhance the appearance further,
      we’ll set additional style properties for our paragraphs. In this step, we're
      fine‑tuning our styles. The first paragraph's font size is increased and c
  - name: Save the HTML Document
    text: The `save` method writes the current state of the `HTMLDocument` object
      to a file on disk. Once we have our styles applied, it’s time to save the HTML
      document. Here, we utilize the `save` method of the `HTMLDocument` class to
      write the modified HTML content to a file, thus preserving our styles and
  - name: Render HTML to PDF
    text: The `PdfDevice` class is Aspose.HTML’s rendering engine that converts an
      HTML document into a PDF file. Finally, let’s **render HTML to PDF** so you
      can share the styled document in a universally accessible format. Using the
      `PdfDevice` class, we set up the rendering of our HTML document into a PDF.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a powerful library that allows developers to work
      with HTML documents in Java applications, providing a vast range of features,
      from HTML manipulation to rendering.
    question: What is Aspose.HTML for Java?
  - answer: No, once you’ve downloaded the necessary library files, you can use Aspose.HTML
      offline.
    question: Do I need an Internet connection to use Aspose.HTML?
  - answer: Yes, you can create multiple `<link>` elements and append them to the
      document's head for various CSS files.
    question: Can I apply multiple CSS files to an HTML document?
  - answer: Yes! Internal CSS is defined within an HTML document, while external CSS
      resides in a separate file and is linked to the document.
    question: Is there a difference between internal and external CSS?
  - answer: You can access community support through the [Aspose forum](https://forum.aspose.com/c/html/29)
      for any questions or issues you may encounter.
    question: How can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: Δημιουργία PDF από HTML και Προσθήκη CSS με Aspose.HTML για Java
url: /el/java/editing-html-documents/apply-external-css-html-documents/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία PDF από HTML και Προσθήκη CSS με Aspose.HTML για Java

## Εισαγωγή
Σε αυτό το tutorial θα ανακαλύψετε πώς να **create PDF from HTML** ενώ προσθέτετε στυλ CSS χρησιμοποιώντας το Aspose.HTML για Java. Είτε χρειάζεστε να δημιουργήσετε μια μορφοποιημένη αναφορά PDF, ένα πρότυπο email, ή ένα έγγραφο που επεξεργάζεται μαζικά, τα παρακάτω βήματα σας δίνουν πλήρη έλεγχο της διαδικασίας HTML‑to‑PDF. Θα περάσουμε από τη δημιουργία ενός εγγράφου HTML, την έγχυση CSS, την προσθήκη ενός στοιχείου style στο head, τον ορισμό κλάσεων CSS στη Java, και τελικά τη μετατροπή του αποτελέσματος σε αρχείο PDF — όλα χωρίς να αφήσετε το περιβάλλον Java.

## Γρήγορες Απαντήσεις
- **Τι κάνει το Aspose.HTML for Java;** Σας επιτρέπει να δημιουργείτε, επεξεργάζεστε και αποδίδετε έγγραφα HTML απευθείας από κώδικα Java, υποστηρίζοντας αρχεία άνω των 50 MB και 100 σελίδες ανά δευτερόλεπτο σε τυπικούς διακομιστές.  
- **Μπορώ να εφαρμόσω εξωτερικό CSS;** Ναι – μπορείτε να προσθέσετε στυλ στο head, να συνδέσετε εξωτερικά αρχεία ή να ενσωματώσετε αλφαριθμητικά CSS.  
- **Χρειάζομαι σύνδεση στο διαδίκτυο;** Όχι, όλα εκτελούνται τοπικά μετά τη λήψη της βιβλιοθήκης.  
- **Ποιοι μορφές εξόδου υποστηρίζονται;** Το HTML μπορεί να αποδοθεί σε PDF, PNG, JPEG ή να διατηρηθεί ως HTML.  
- **Απαιτείται άδεια για παραγωγή;** Απαιτείται εμπορική άδεια για χρήση σε παραγωγή· διατίθεται δωρεάν δοκιμή.

## Τι είναι η «προσθήκη CSS σε HTML»;
Η προσθήκη CSS σε HTML σημαίνει την επισύναψη κανόνων στυλ—inline, internal ή external—σε ένα έγγραφο HTML ώστε τα προγράμματα περιήγησης να γνωρίζουν πώς να εμφανίζουν τα στοιχεία (χρώματα, γραμματοσειρές, διάταξη κ.λπ.). Με το Aspose.HTML για Java μπορείτε να ενσωματώσετε προγραμματιστικά αυτά τα στυλ χωρίς να ανοίξετε πρόγραμμα περιήγησης.

## Γιατί να χρησιμοποιήσετε το Aspose.HTML για Java για την προσθήκη CSS;
Το Aspose.HTML για Java παρέχει **full‑stack control** στην επεξεργασία HTML. Μπορεί να διαχειριστεί έγγραφα έως **500 MB** και να αποδώσει **πάνω από 200 σελίδες ανά δευτερόλεπτο** σε τυπική CPU 2.5 GHz, εξαλείφοντας την ανάγκη για τρίτα προγράμματα περιήγησης. Η βιβλιοθήκη λειτουργεί εντελώς offline, καθιστώντας την ιδανική για υπηρεσίες backend, και περιλαμβάνει ενσωματωμένο PDF renderer ώστε να μπορείτε να **convert HTML to PDF** με μία κλήση API.

## Προαπαιτούμενα
Πριν βυθιστείτε στον κώδικα, βεβαιωθείτε ότι έχετε τα παρακάτω:

### 1. Java Development Kit (JDK)
Βεβαιωθείτε ότι έχετε εγκατεστημένο το JDK στο σύστημά σας. Μπορείτε να κατεβάσετε την πιο πρόσφατη έκδοση από [Oracle’s Java website](https://www.oracle.com/java/technologies/javase-downloads.html).

### 2. Aspose.HTML for Java
Θα χρειαστεί να έχετε εγκατεστημένο το Aspose.HTML για Java. Αν δεν το έχετε κάνει ακόμη, μεταβείτε στη [Aspose downloads page](https://releases.aspose.com/html/java/) και κατεβάστε τη βιβλιοθήκη.

### 3. Ένα IDE ή Επεξεργαστής Κειμένου
Επιλέξτε ένα Integrated Development Environment (IDE) όπως IntelliJ IDEA, Eclipse ή ακόμη και έναν απλό επεξεργαστή κειμένου για να γράψετε τον κώδικα Java.

### 4. Βασικές Γνώσεις Java και CSS
Η εξοικείωση με τον προγραμματισμό Java και τα βασικά του CSS θα σας βοηθήσει να ακολουθήσετε πιο άνετα.

## Εισαγωγή Πακέτων
Αφού έχετε ρυθμίσει τα πάντα, το επόμενο βήμα είναι η εισαγωγή των απαραίτητων πακέτων στο έργο Java σας. Αυτό χρειάζεστε:

```java
import com.aspose.html.HTMLDocument;
```

Αυτές οι εισαγωγές θα σας επιτρέψουν να χειρίζεστε έγγραφα HTML και να τα αποδίδετε σε διαφορετικές μορφές, όπως PDF.

Θα χωρίσουμε το tutorial μας σε διαχειρίσιμα βήματα. Κάθε βήμα θα σας καθοδηγήσει στη διαδικασία **add CSS to HTML** χρησιμοποιώντας το Aspose.HTML για Java.

## Πώς να δημιουργήσετε PDF από HTML χρησιμοποιώντας το Aspose.HTML για Java;
Φορτώστε το περιεχόμενο HTML με `new HTMLDocument(htmlString)` (ή από αρχείο) και στη συνέχεια καλέστε `document.save("output.pdf", new PdfSaveOptions())`. Το Aspose.HTML αναλύει το markup, εφαρμόζει τυχόν ενσωματωμένο CSS και αποδίδει το αποτέλεσμα σε PDF με μία ενέργεια. Αυτή η προσέγγιση εξαλείφει την ανάγκη για εξωτερική μηχανή προγράμματος περιήγησης και εγγυάται συνεπή διάταξη σε όλα τα περιβάλλοντα.

### Βήμα 1: Δημιουργία εγγράφου HTML στη Java
Η κλάση `HTMLDocument` είναι το βασικό αντικείμενο του Aspose.HTML που αντιπροσωπεύει ένα αρχείο HTML στη μνήμη.  
Πρώτα απ' όλα, πρέπει να δημιουργήσουμε το HTML έγγραφό μας. Θα ξεκινήσουμε ορίζοντας το περιεχόμενο με μια απλή δομή HTML.

```java
String content = "<div><p>Internal CSS</p><p>An internal CSS is used to define a style for a single HTML page</p></div>";
HTMLDocument document = new HTMLDocument(content, ".");
```

Εδώ, ορίσαμε μια βασική δομή HTML, συμπεριλαμβανομένου ενός `<div>` με δύο παραγράφους. Η κλάση `HTMLDocument` χρησιμοποιείται για τη δημιουργία μιας αναπαράστασης του HTML περιεχομένου μας.

### Βήμα 2: Δημιουργία στοιχείου Style
Ένα στοιχείο `<style>` είναι μια ετικέτα HTML που περιέχει κανόνες CSS απευθείας μέσα στο έγγραφο.  
Στη συνέχεια, θα δημιουργήσουμε ένα στοιχείο `style` για να περιέχει τους κανόνες CSS μας.

```java
Element style = document.createElement("style");
style.setTextContent(".frame1 { margin-top:50px; margin-left:50px; padding:20px; width:360px; height:90px; background-color:#a52a2a; font-family:verdana; color:#FFF5EE;} \n" +
        ".frame2 { margin-top:-90px; margin-left:160px; text-align:center; padding:20px; width:360px; height:100px; background-color:#ADD8E6;}");
```

Χρησιμοποιώντας τη μέθοδο `createElement` του `HTMLDocument`, δημιουργούμε ένα νέο στοιχείο `<style>` και ορίζουμε το περιεχόμενό του ώστε να περιλαμβάνει τους ορισμούς CSS για δύο κλάσεις: `frame1` και `frame2`. Αυτές οι κλάσεις ορίζουν περιθώρια, padding, διαστάσεις, χρώματα φόντου, γραμματοσειρές και χρώματα κειμένου.

### Βήμα 3: Προσθήκη style στο head
Η προσθήκη ενός στοιχείου style στο `<head>` κάνει το πρόγραμμα περιήγησης (ή το Aspose renderer) να εφαρμόσει το CSS σε ολόκληρη τη σελίδα.  
Τώρα που έχουμε το CSS μας, πρέπει να **append style to head** ώστε το πρόγραμμα περιήγησης (ή το Aspose renderer) να το εφαρμόσει.

```java
Element head = document.getElementsByTagName("head").get_Item(0);
head.appendChild(style);
```

Ανακτούμε το head του εγγράφου και προσθέτουμε το νεοδημιουργημένο στοιχείο `style`. Αυτή η ενέργεια ενσωματώνει αποτελεσματικά το CSS στο έγγραφο HTML, επιτρέποντας του να μορφοποιήσει το HTML περιεχόμενό μας.

### Βήμα 4: Ορισμός κλάσης CSS στη Java
Η μέθοδος `setClassName` αναθέτει ένα όνομα κλάσης CSS σε ένα στοιχείο HTML, συνδέοντάς το με τους κανόνες στυλ που ορίστηκαν προηγουμένως.  
Στη συνέχεια, θα εφαρμόσουμε τις προηγουμένως ορισμένες κλάσεις CSS στα στοιχεία παραγράφου μας.

```java
HTMLElement paragraph = (HTMLElement) document.getElementsByTagName("p").get_Item(0);
paragraph.setClassName("frame1");
HTMLElement lastParagraph = (HTMLElement) document.getElementsByTagName("p").get_Item(document.getElementsByTagName("p").getLength() - 1);
lastParagraph.setClassName("frame2");
```

Εδώ, προσπελαύνουμε τα πρώτα και τελευταία στοιχεία παραγράφου στο έγγραφο και τους αναθέτουμε τις κλάσεις CSS που δημιουργήσαμε. Αυτή η ανάθεση εξασφαλίζει ότι θα ακολουθήσουν τα στυλ που ορίσαμε στο CSS.

### Βήμα 5: Ορισμός πρόσθετων ιδιοτήτων στυλ
Η μέθοδος `setStyleProperty` σας επιτρέπει να τροποποιήσετε μεμονωμένες ιδιότητες CSS σε ένα στοιχείο μετά τη δημιουργία του.  
Για να βελτιώσουμε περαιτέρω την εμφάνιση, θα ορίσουμε πρόσθετες ιδιότητες στυλ για τις παραγράφους μας.

```java
paragraph.getStyle().setFontSize("250%");
paragraph.getStyle().setTextAlign("center");
lastParagraph.getStyle().setColor("#434343");
lastParagraph.getStyle().setFontSize("150%");
lastParagraph.getStyle().setFontFamily("verdana");
```

Σε αυτό το βήμα, κάνουμε λεπτομερή ρύθμιση των στυλ μας. Το μέγεθος γραμματοσειράς της πρώτης παραγράφου αυξάνεται και κεντράρεται, ενώ το χρώμα, το μέγεθος γραμματοσειράς και η γραμματοσειρά της τελευταίας παραγράφου ορίζονται. Αυτή η βελτίωση είναι κρίσιμη για την αναγνωσιμότητα και την αισθητική.

### Βήμα 6: Αποθήκευση του εγγράφου HTML
Η μέθοδος `save` γράφει την τρέχουσα κατάσταση του αντικειμένου `HTMLDocument` σε αρχείο στο δίσκο.  
Μόλις εφαρμόσουμε τα στυλ, ήρθε η ώρα να αποθηκεύσουμε το έγγραφο HTML.

```java
document.save("edit-internal-css.html");
```

Εδώ, χρησιμοποιούμε τη μέθοδο `save` της κλάσης `HTMLDocument` για να γράψουμε το τροποποιημένο περιεχόμενο HTML σε αρχείο, διατηρώντας έτσι τα στυλ και τις αλλαγές μας.

### Βήμα 7: Απόδοση HTML σε PDF
Η κλάση `PdfDevice` είναι η μηχανή απόδοσης του Aspose.HTML που μετατρέπει ένα έγγραφο HTML σε αρχείο PDF.  
Τέλος, ας **render HTML to PDF** ώστε να μπορείτε να μοιραστείτε το μορφοποιημένο έγγραφο σε μια καθολικά προσβάσιμη μορφή.

```java
PdfDevice device = new PdfDevice("edit-internal-css.pdf");
document.renderTo(device);
```

## Συνηθισμένες Περιπτώσεις Χρήσης
- **Αυτοματοποιημένη δημιουργία αναφορών** – δημιουργήστε μορφοποιημένες αναφορές HTML και μετατρέψτε τις σε PDF για διανομή.  
- **Πρότυπα email** – δημιουργήστε email HTML με συνεπή branding, έπειτα αποδώστε τα σε PDF για αρχειοθέτηση.  
- **Μαζική επεξεργασία** – εφαρμόστε το ίδιο CSS σε δεκάδες αρχεία HTML σε εργασία διακομιστή, έπειτα μετατρέψτε το καθένα σε PDF με μία κλήση API.

## Επίλυση Προβλημάτων & Συμβουλές
- **Απουσία στοιχείου head** – Αν το `getElementsByTagName("head")` επιστρέφει null, βεβαιωθείτε ότι η συμβολοσειρά HTML περιλαμβάνει ετικέτα `<head>`.  
- **CSS δεν εφαρμόζεται** – Επαληθεύστε ότι τα ονόματα κλάσεων στο `setClassName` ταιριάζουν ακριβώς με αυτά που ορίζονται στο μπλοκ `<style>`.  
- **Προβλήματα απόδοσης PDF** – Βεβαιωθείτε ότι η άδεια Aspose.HTML έχει εφαρμοστεί σωστά· διαφορετικά, το αποτέλεσμα μπορεί να έχει υδατογράφημα.  
- **Μεγάλα αρχεία HTML** – Για αρχεία μεγαλύτερα από 200 MB, εξετάστε τη χρήση `HTMLDocument.load(..., LoadOptions)` με streaming για αποφυγή πίεσης μνήμης.  
- **Συμβουλή απόδοσης** – Η επαναχρησιμοποίηση ενός μόνο αντικειμένου `HTMLDocument` για πολλαπλές λειτουργίες απόδοσης μπορεί να μειώσει το κόστος δημιουργίας αντικειμένων έως και 30 %.

## Συχνές Ερωτήσεις

**Q: Τι είναι το Aspose.HTML για Java;**  
A: Το Aspose.HTML για Java είναι μια ισχυρή βιβλιοθήκη που επιτρέπει στους προγραμματιστές να εργάζονται με έγγραφα HTML σε εφαρμογές Java, παρέχοντας ένα ευρύ φάσμα λειτουργιών, από τη διαχείριση HTML μέχρι την απόδοση.

**Q: Χρειάζομαι σύνδεση στο Internet για να χρησιμοποιήσω το Aspose.HTML;**  
A: Όχι, μόλις κατεβάσετε τα απαραίτητα αρχεία βιβλιοθήκης, μπορείτε να χρησιμοποιήσετε το Aspose.HTML offline.

**Q: Μπορώ να εφαρμόσω πολλαπλά αρχεία CSS σε ένα έγγραφο HTML;**  
A: Ναι, μπορείτε να δημιουργήσετε πολλαπλά στοιχεία `<link>` και να τα προσθέσετε στο head του εγγράφου για διάφορα αρχεία CSS.

**Q: Υπάρχει διαφορά μεταξύ internal και external CSS;**  
A: Ναι! Το internal CSS ορίζεται μέσα σε ένα έγγραφο HTML, ενώ το external CSS βρίσκεται σε ξεχωριστό αρχείο και συνδέεται με το έγγραφο.

**Q: Πώς μπορώ να λάβω υποστήριξη για το Aspose.HTML για Java;**  
A: Μπορείτε να έχετε πρόσβαση σε υποστήριξη κοινότητας μέσω του [Aspose forum](https://forum.aspose.com/c/html/29) για τυχόν ερωτήσεις ή προβλήματα που μπορεί να αντιμετωπίσετε.

---

**Τελευταία ενημέρωση:** 2026-06-24  
**Δοκιμάστηκε με:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Συγγραφέας:** Aspose

## Σχετικά Μαθήματα

- [Δημιουργία PDF από HTML – Ορισμός Φύλλου Στυλ Χρήστη στο Aspose.HTML για Java](/html/java/configuring-environment/set-user-style-sheet/)
- [Πώς να Προσθέσετε CSS – Inline CSS σε Έγγραφα HTML στο Aspose.HTML για Java](/html/java/editing-html-documents/add-inline-css-html-documents/)
- [Πώς να Επεξεργαστείτε CSS – Προχωρημένη Εξωτερική Επεξεργασία CSS με Aspose.HTML για Java](/html/java/editing-html-documents/advanced-external-css-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< blocks/products/products-backtop-button >}}
{{< /blocks/products/pf/main-wrap-class >}}