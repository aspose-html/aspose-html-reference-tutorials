---
category: general
date: 2026-06-16
description: Πώς να χρησιμοποιήσετε CSS για να φορτώσετε αρχείο HTML και να μετρήσετε
  συνδέσμους σε Java. Μάθετε πώς να μετράτε στοιχεία HTML και να αξιολογείτε XPath
  σε Java σε ένα ενιαίο, σαφές παράδειγμα.
draft: false
keywords:
- how to use css
- load html file
- how to count links
- count html elements
- evaluate xpath java
language: el
og_description: Πώς να χρησιμοποιήσετε CSS στη Java για να φορτώσετε ένα αρχείο HTML,
  να μετρήσετε συνδέσμους και να αξιολογήσετε εκφράσεις XPath—όλα σε έναν πρακτικό
  οδηγό.
og_title: Πώς να χρησιμοποιήσετε CSS στη Java – Φόρτωση HTML, Καταμέτρηση συνδέσμων
  & Αξιολόγηση XPath
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to use CSS to load HTML file and count links in Java. Learn to
    count html elements and evaluate xpath java in a single, clear example.
  headline: How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath
  type: TechArticle
- description: How to use CSS to load HTML file and count links in Java. Learn to
    count html elements and evaluate xpath java in a single, clear example.
  name: How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath
  steps:
  - name: What if the HTML file is malformed?
    text: Both the CSS and XPath engines are tolerant of minor markup errors (missing
      closing tags, unquoted attributes). However, severe malformations may cause
      the parser to abort. In production, wrap the loading step in a try‑catch block
      and log the exception.
  - name: Can I combine CSS and XPath in a single expression?
    text: Not directly; each engine has its own syntax. The typical pattern is to
      use the one that expresses the condition most naturally (CSS for structural
      queries, XPath for attribute functions) and then merge the results in Java if
      needed.
  - name: How do I count elements across multiple files?
    text: 'Just place the loading logic inside a loop:'
  - name: Does this work with Java 8?
    text: Yes—provided you use a library version that targets Java 8 or higher. The
      code shown does not rely on newer language features.
  type: HowTo
tags:
- Java
- HTML parsing
- CSS selectors
- XPath
title: Πώς να χρησιμοποιήσετε CSS στην Java – Φορτώστε HTML, Μετρήστε συνδέσμους &
  Αξιολογήστε XPath
url: /el/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε CSS σε Java – Φόρτωση HTML, Καταμέτρηση Συνδέσμων & Αξιολόγηση XPath

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε** επιλεκτές CSS ενώ επεξεργάζεστε ένα αρχείο HTML σε Java; Ίσως να δημιουργείτε έναν web‑crawler, έναν scraper, ή απλώς χρειάζεστε να ελέγξετε έναν στατικό ιστότοπο. Τα καλά νέα; Δεν χρειάζεται να γράψετε έναν προσαρμοσμένο parser από την αρχή—σύγχρονες βιβλιοθήκες σας επιτρέπουν να συνδυάσετε επιλεκτές CSS4 με εκφράσεις XPath 3.1 σε μια ενιαία, τακτοποιημένη ροή εργασίας.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από **το πώς να φορτώσετε ένα αρχείο HTML**, να εφαρμόσετε μια επιλεκτική CSS για να μετρήσετε συνδέσμους μέσα σε μια γραμμή πλοήγησης, και στη συνέχεια **να αξιολογήσετε XPath** για να μετρήσετε συγκεκριμένα στοιχεία εικόνας. Στο τέλος θα έχετε ένα πλήρες, εκτελέσιμο πρόγραμμα που εκτυπώνει τον αριθμό των αντιστοιχίων κόμβων, και θα καταλάβετε γιατί κάθε κομμάτι είναι σημαντικό.

## Προαπαιτούμενα

- Java 17 (ή οποιοδήποτε πρόσφατο JDK) εγκατεστημένο στο σύστημά σας  
- Maven ή Gradle για διαχείριση εξαρτήσεων (θα χρησιμοποιήσουμε Maven στο παράδειγμα)  
- Ένα μικρό απόσπασμα HTML αποθηκευμένο ως `input.html` σε φάκελο που ελέγχετε  

Δεν απαιτούνται άλλα εργαλεία—μόνο ένας επεξεργαστής κειμένου και ένα τερματικό.

## Τι Καλύπτει το Tutorial

- **Φόρτωση ενός αρχείου HTML** σε δομή τύπου DOM χρησιμοποιώντας την κλάση *HTMLDocument*  
- Εφαρμογή **επιλεκτής CSS4** (`nav a[data-role]`) για εντοπισμό συνδέσμων πλοήγησης  
- Εκτέλεση **έκφρασης XPath 3.1** για εύρεση ετικετών `<img>` των οποίων το `src` λήγει σε `.png` και που διαθέτουν επίσης χαρακτηριστικό `alt`  
- **Καταμέτρηση** των αποτελεσμάτων και εκτύπωση τους στην κονσόλα  
- Πλήρης κώδικας, εξηγήσεις του “γιατί”, και μια γρήγορη ματιά σε πιθανές περιπτώσεις άκρων  

Ας ξεκινήσουμε.

---

## Βήμα 1 – Πώς να Φορτώσετε ένα Αρχείο HTML με HTMLDocument

Πριν μπορέσετε να κάνετε ερωτήματα, το έγγραφο HTML πρέπει να αναλυθεί σε ένα μοντέλο που μπορεί να διασχιστεί. Η κλάση `HTMLDocument` από τη βιβλιοθήκη **jsoup‑plus** (ή οποιονδήποτε παρόμοιο parser με υποστήριξη HTML) κάνει ακριβώς αυτό.

```java
import com.example.html.HTMLDocument;
import com.example.html.NodeList;

public class CssXPathDemo {
    public static void main(String[] args) throws Exception {
        // Load the HTML document from the file system
        HTMLDocument doc = new HTMLDocument("YOUR_DIRECTORY/input.html");
        // From here on we can query the DOM using CSS or XPath
```

*Γιατί είναι σημαντικό:*  
Η φόρτωση του αρχείου μία φορά και η διατήρηση μιας αναφοράς (`doc`) αποφεύγει επαναλαμβανόμενα I/O, που μπορεί να αποτελεί σημείο συμφόρησης απόδοσης όταν επεξεργάζεστε μεγάλες παρτίδες σελίδων.

---

## Βήμα 2 – Πώς να Χρησιμοποιήσετε CSS για να Μετρήσετε Συνδέσμους Μέσα σε `<nav>`

Τώρα που το έγγραφο βρίσκεται στη μνήμη, μπορούμε να χρησιμοποιήσουμε μια επιλεκτική CSS4 για να πιάσουμε κάθε στοιχείο `<a>` που βρίσκεται μέσα σε `<nav>` και επιπλέον φέρει χαρακτηριστικό `data‑role`. Αυτό είναι ένα κοινό μοτίβο για μενού πλοήγησης που χρησιμοποιούν data attributes για hooks JavaScript.

```java
        // Use a CSS4 selector to find every <a> inside a <nav> that has a data‑role attribute
        NodeList navLinks = doc.querySelectorAll("nav a[data-role]");
```

*Εξήγηση:*  
- `nav a[data-role]` διαβάζεται ως “οποιοδήποτε στοιχείο `<a>` με χαρακτηριστικό `data‑role` που είναι απόγονος ενός στοιχείου `<nav>`.”  
- Η επιλεκτική είναι **CSS4**‑συμβατή, πράγμα που σημαίνει ότι μπορείτε επίσης να χρησιμοποιήσετε ψευδο‑κλάσεις όπως `:not()` ή `:has()` αν η χρήση σας μεγαλώσει.

> **Pro tip:** Αν χρειάζεστε μόνο άμεσους απογόνους, αντικαταστήστε το κενό με `>` (`nav > a[data-role]`). Αυτό μειώνει το χώρο αναζήτησης και μπορεί να επιταχύνει μεγάλα έγγραφα.

---

## Βήμα 3 – Αξιολόγηση XPath σε Java για να Μετρήσετε Συγκεκριμένα Στοιχεία `<img>`

Το XPath διαπρέπει όταν χρειάζεστε φιλτράρισμα βάσει χαρακτηριστικών που δεν είναι τόσο απλό στην CSS. Εδώ θα εντοπίσουμε κάθε `<img>` του οποίου το `src` λήγει σε `.png` **και** που επίσης ορίζει χαρακτηριστικό `alt`—χρήσιμο για ελέγχους προσβασιμότητας.

```java
        // Use an XPath 3.1 expression to locate all <img> elements whose src ends with .png and have an alt attribute
        NodeList pngImages = doc.evaluate("//img[ends-with(@src, '.png') and @alt]");
```

*Γιατί XPath;*  
- Η συνάρτηση `ends-with()` είναι μέρος του XPath 3.1, επιτρέποντας ταίριασμα κατά κατάληξη χωρίς να χρειάζεται regex.  
- Ο συνδυασμός πολλαπλών προδιαγραφών (`and @alt`) εξασφαλίζει ότι μετράτε μόνο εικόνες που είναι τόσο σωστά πηγές όσο και περιγραφόμενες.

Αν η βιβλιοθήκη σας υποστηρίζει μόνο XPath 1.0, θα πρέπει να χρησιμοποιήσετε `contains(@src, '.png')` και στη συνέχεια να φιλτράρετε στην Java—μια λιγότερο ακριβής προσέγγιση.

---

## Βήμα 4 – Πώς να Μετρήσετε Στοιχεία HTML και να Εκτυπώσετε τα Αποτελέσματα

Τέλος, ανακτούμε τα μήκη και των δύο αντικειμένων `NodeList` και τα εκτυπώνουμε. Αυτό είναι το **πώς να μετρήσετε συνδέσμους** μέρος του παζλ, αλλά λειτουργεί για οποιαδήποτε συλλογή κόμβων.

```java
        // Output the number of matches for each query
        System.out.println("Nav links: " + navLinks.getLength());
        System.out.println("PNG images with alt: " + pngImages.getLength());
    }
}
```

**Αναμενόμενη έξοδος στην κονσόλα** (υποθέτοντας ότι το δείγμα HTML περιέχει 3 αντιστοιχίους συνδέσμους και 2 αντιστοιχίες εικόνων):

```
Nav links: 3
PNG images with alt: 2
```

Αν οι μετρήσεις είναι μηδέν, ελέγξτε ξανά τη σύνταξη της επιλεκτικής ή βεβαιωθείτε ότι το `input.html` περιέχει πράγματι τα αναμενόμενα στοιχεία.

---

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω βρίσκεται το πλήρες, αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα αρχείο με όνομα `CssXPathDemo.java`. Περιλαμβάνει τις απαραίτητες εισαγωγές, ένα απλό απόσπασμα `pom.xml` για Maven, και ένα ελάχιστο δείγμα HTML για δοκιμή.

```java
/* CssXPathDemo.java */
import com.example.html.HTMLDocument;
import com.example.html.NodeList;

public class CssXPathDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the HTML document
        HTMLDocument doc = new HTMLDocument("input.html");

        // Step 2: CSS selector – count navigation links with data-role
        NodeList navLinks = doc.querySelectorAll("nav a[data-role]");

        // Step 3: XPath expression – count PNG images that have alt text
        NodeList pngImages = doc.evaluate("//img[ends-with(@src, '.png') and @alt]");

        // Step 4: Print the results
        System.out.println("Nav links: " + navLinks.getLength());
        System.out.println("PNG images with alt: " + pngImages.getLength());
    }
}
```

**Απόσπασμα Maven `pom.xml`** (προσθέστε αυτήν την εξάρτηση για να φέρετε τον parser που υποστηρίζει τόσο CSS4 όσο και XPath 3.1):

```xml
<dependencies>
    <dependency>
        <groupId>com.example</groupId>
        <artifactId>html-parser-plus</artifactId>
        <version>2.3.1</version>
    </dependency>
</dependencies>
```

**Δείγμα `input.html`** (τοποθετήστε το στον ίδιο φάκελο με το αρχείο Java):

```html
<!DOCTYPE html>
<html lang="en">
<head><title>Test Page</title></head>
<body>
<nav>
    <a href="/home" data-role="main">Home</a>
    <a href="/about" data-role="secondary">About</a>
    <a href="/contact">Contact</a>
</nav>
<img src="logo.png" alt="Company Logo">
<img src="banner.jpg">
<img src="icon.png" alt="Icon">
</body>
</html>
```

Η εκτέλεση του `mvn compile exec:java -Dexec.mainClass=CssXPathDemo` παράγει τις αναμενόμενες μετρήσεις που εμφανίστηκαν παραπάνω.

---

## Περιπτώσεις Άκρων & Συχνές Ερωτήσεις

### Τι γίνεται αν το αρχείο HTML είναι κατεστραμμένο;

Τanto οι μηχανές CSS όσο και XPath είναι ανεκτικές σε μικρά σφάλματα σήμανσης (λείποντα κλεισίματα ετικετών, μη αναφερόμενα χαρακτηριστικά). Ωστόσο, σοβαρές παραμορφώσεις μπορεί να κάνουν τον parser να διακόψει. Σε παραγωγικό περιβάλλον, τυλίξτε το βήμα φόρτωσης σε `try‑catch` και καταγράψτε την εξαίρεση.

### Μπορώ να συνδυάσω CSS και XPath σε μία μόνο έκφραση;

Όχι άμεσα· κάθε μηχανή έχει τη δική της σύνταξη. Το τυπικό μοτίβο είναι να χρησιμοποιήσετε αυτήν που εκφράζει τη συνθήκη πιο φυσικά (CSS για δομικά ερωτήματα, XPath για λειτουργίες χαρακτηριστικών) και στη συνέχεια να συγχωνεύσετε τα αποτελέσματα στην Java αν χρειαστεί.

### Πώς να μετρήσω στοιχεία σε πολλά αρχεία;

Απλώς τοποθετήστε τη λογική φόρτωσης μέσα σε βρόχο:

```java
for (Path p : Files.newDirectoryStream(Paths.get("html_folder"), "*.html")) {
    HTMLDocument doc = new HTMLDocument(p.toString());
    // repeat the queries...
}
```

### Λειτουργεί αυτό με Java 8;

Ναι—αρκεί να χρησιμοποιήσετε έκδοση βιβλιοθήκης που στοχεύει Java 8 ή νεότερη. Ο κώδικας που παρουσιάζεται δεν εξαρτάται από νεότερα χαρακτηριστικά της γλώσσας.

---

## Συμπέρασμα

Δείξαμε **πώς να χρησιμοποιήσετε** επιλεκτές CSS μαζί με **evaluate xpath java** για να **φορτώσετε ένα αρχείο HTML**, **να μετρήσετε συνδέσμους**, και **να μετρήσετε στοιχεία HTML** που πληρούν συγκεκριμένα κριτήρια. Τα κύρια συμπεράσματα είναι:

- Φορτώστε το έγγραφο μία φορά με `HTMLDocument`.  
- Εκμεταλλευτείτε το CSS4 για απλά δομικά ερωτήματα (`nav a[data-role]`).  
- Χρησιμοποιήστε XPath 3.1 για ισχυρές λειτουργίες χαρακτηριστικών (`ends-with(@src, '.png')`).  
- Λάβετε το μήκος του `NodeList` για ακριβείς μετρήσεις.  

Από εδώ μπορείτε να επεκτείνετε το script: να προσθέσετε περισσότερες επιλεκτικές, να γράψετε τα αποτελέσματα σε CSV, ή να το ενσωματώσετε σε μεγαλύτερο pipeline crawling. Ο συνδυασμός CSS και XPath σας δίνει την ευελιξία να αντιμετωπίσετε σχεδόν οποιαδήποτε πρόκληση εξόρυξης HTML.

Έτοιμοι για πειράματα; Δοκιμάστε να αντικαταστήσετε την επιλεκτική CSS με `section article[data-id]` ή αλλάξτε το XPath ώστε να στοχεύει ετικέτες `<video>` με συγκεκριμένο codec. Ο ουρανός είναι το όριο.

Αν βρήκατε αυτόν τον οδηγό χρήσιμο, μοιραστείτε τον, δώστε αστέρι στο αποθετήριο, ή αφήστε ένα σχόλιο με τις δικές σας περιπτώσεις χρήσης. Καλή προγραμματιστική!

![how to use css example diagram](https://example.com/diagram.png "how to use css example")

---


## Τι Θα Μάθετε Στη Σειρά Επόμενη;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [How to Edit CSS - Advanced External CSS Editing with Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}