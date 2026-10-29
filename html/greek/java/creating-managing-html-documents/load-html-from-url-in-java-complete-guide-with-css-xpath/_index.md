---
category: general
date: 2026-07-02
description: Φορτώστε HTML από URL χρησιμοποιώντας το Aspose.HTML για Java, στη συνέχεια
  επιλέξτε στοιχεία με χαρακτηριστικό, εξάγετε συνδέσμους λήψης και μετρήστε κόμβους
  XPath σε λίγα εύκολα βήματα.
draft: false
keywords:
- load html from url
- select elements with attribute
- extract download links
- search html with css
- count xpath nodes
language: el
og_description: Φορτώστε HTML από URL σε Java, στη συνέχεια χρησιμοποιήστε CSS selectors
  και XPath για να επιλέξετε στοιχεία με χαρακτηριστικό, να εξάγετε συνδέσμους λήψης
  και να μετρήσετε τους κόμβους XPath.
og_title: Φόρτωση HTML από URL σε Java – Πλήρης οδηγός CSS & XPath
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Load HTML from URL using Aspose.HTML for Java, then select elements
    with attribute, extract download links, and count XPath nodes in a few easy steps.
  headline: Load HTML from URL in Java – Complete Guide with CSS & XPath
  type: TechArticle
- description: Load HTML from URL using Aspose.HTML for Java, then select elements
    with attribute, extract download links, and count XPath nodes in a few easy steps.
  name: Load HTML from URL in Java – Complete Guide with CSS & XPath
  steps:
  - name: Maven
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-html</artifactId>
      <version>23.10</version> <!-- Check for the latest version --> </dependency>
      ```'
  - name: Gradle
    text: '```gradle implementation ''com.aspose:aspose-html:23.10'' ```'
  - name: What the selector means
    text: '| Part | Meaning | |------|---------| | `a` | any `<a>` element | | `[href*=''download'']`
      | attribute `href` that **contains** the substring `download` (`*=` is the “contains”
      operator) |'
  - name: Expected console output (may vary by site)
    text: '``` Document loaded from https://example.com'
  type: HowTo
tags:
- Java
- Aspose.HTML
- Web Scraping
title: Φόρτωση HTML από URL σε Java – Πλήρης Οδηγός με CSS & XPath
url: /el/java/creating-managing-html-documents/load-html-from-url-in-java-complete-guide-with-css-xpath/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Φόρτωση HTML από URL σε Java – Πλήρης Οδηγός με CSS & XPath

Έχετε χρειαστεί ποτέ να **φορτώσετε HTML από URL** σε μια εφαρμογή Java και να εξάγετε συγκεκριμένους συνδέσμους χωρίς να γράψετε έναν πλήρη web‑crawler; Δεν είστε μόνοι. Είτε δημιουργείτε έναν διαχειριστή λήψεων, έναν συγκεντρωτή περιεχομένου, είτε απλώς είστε περίεργοι για τις σελίδες που επισκέπτεστε, η δυνατότητα ανάκτησης μιας σελίδας, **αναζήτησης HTML με CSS**, και στη συνέχεια **καταμέτρησης κόμβων XPath** είναι μια χρήσιμη δεξιότητα.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: από τη λήψη μιας απομακρυσμένης σελίδας στη μνήμη, μέχρι τη χρήση ενός CSS selector για **επιλογή στοιχείων με χαρακτηριστικό**, την εξαγωγή αυτών των **συνδέσμων λήψης**, και τέλος την επαλήθευση του ίδιου αποτελέσματος με ένα ερώτημα XPath. Χωρίς εξωτερικές υπηρεσίες, μόνο καθαρή Java και η βιβλιοθήκη Aspose.HTML for Java.

> **Προαπαιτούμενα** – Θα χρειαστείτε εγκατεστημένη Java 8+, Maven ή Gradle για διαχείριση εξαρτήσεων, και βασική κατανόηση του HTML και της σύνταξης Java. Αν είστε νέοι στην Aspose.HTML, μην ανησυχείτε· θα καλύψουμε τη ρύθμιση βήμα‑βήμα.

## Τι Θα Δημιουργήσετε

Στο τέλος αυτού του οδηγού θα έχετε μια εκτελέσιμη κλάση Java που:

1. **Φορτώνει HTML από ένα URL** (π.χ., `https://example.com`).
2. **Αναζητά το DOM με έναν CSS selector** για να βρει κάθε ετικέτα `<a>` της οποίας το `href` περιέχει το “download”.
3. **Εξάγει και εκτυπώνει κάθε σύνδεσμο λήψης**.
4. **Εκτελεί ένα ισοδύναμο ερώτημα XPath** και εκτυπώνει πόσοι κόμβοι βρέθηκαν.

Θα δείτε επίσης ένα μικρό διάγραμμα που οπτικοποιεί τη ροή—για τυχόν οπτικούς μαθητές.

![Διάγραμμα που δείχνει τη ροή της φόρτωσης HTML από URL, την επιλογή στοιχείων, την εξαγωγή συνδέσμων και την καταμέτρηση κόμβων XPath](load-html-from-url-diagram.png)

## Βήμα 1: Προσθέστε το Aspose.HTML for Java στο Έργο σας

Πρώτα απ' όλα. Το Aspose.HTML είναι εμπορική βιβλιοθήκη, αλλά προσφέρει δωρεάν δοκιμή που λειτουργεί τέλεια για εκπαιδευτικούς σκοπούς.

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

### Gradle

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

> **Συμβουλή:** Αν αντιμετωπίσετε αργότερα ένα `NoClassDefFoundError`, ελέγξτε ξανά ότι το αρχείο `aspose-html` jar βρίσκεται στο classpath εκτέλεσης.

## Βήμα 2: Φόρτωση HTML από URL και Αρχικοποίηση του Εγγράφου

Τώρα που η βιβλιοθήκη είναι διαθέσιμη, μπορούμε πραγματικά να **φορτώσουμε HTML από URL**. Η κλάση `HTMLDocument` δέχεται ένα string URL και αναλαμβάνει το αίτημα HTTP, τις ανακατευθύνσεις και την ανίχνευση του συνόλου χαρακτήρων για εσάς.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;

public class HtmlDownloader {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Define the target page
        String pageUrl = "https://example.com";

        // Step 2.2: Load the page into an HTMLDocument object
        HTMLDocument document = new HTMLDocument(pageUrl);

        System.out.println("Document loaded successfully.");
        // From here on we can query the DOM.
    }
}
```

**Γιατί αυτό λειτουργεί:** Η `HTMLDocument` δημιουργεί εσωτερικά ένα `HttpWebRequest`, ακολουθεί τις ανακατευθύνσεις και δημιουργεί ένα δέντρο DOM που συμπεριφέρεται όπως το `document` ενός προγράμματος περιήγησης. Αυτό σημαίνει ότι μπορούμε να χρησιμοποιήσουμε αμέσως και CSS selectors και XPath.

## Βήμα 3: Αναζήτηση HTML με CSS – Επιλογή Στοιχείων με Χαρακτηριστικό

Ο πιο αναγνώσιμος τρόπος για τον εντοπισμό στοιχείων είναι με έναν CSS selector. Στην περίπτωσή μας θέλουμε κάθε `<a>` του οποίου το χαρακτηριστικό `href` περιέχει τη λέξη “download”. Η σύνταξη selector `a[href*='download']` κάνει ακριβώς αυτό.

```java
// Step 3: Find all anchor elements whose href contains "download"
NodeList downloadLinks = document.selectElements("a[href*='download']");

// Quick sanity check – how many did we find?
System.out.println("CSS found " + downloadLinks.getLength() + " nodes.");
```

### Τι σημαίνει ο selector

| Μέρος | Σημασία |
|------|---------|
| `a` | οποιοδήποτε στοιχείο `<a>` |
| `[href*='download']` | χαρακτηριστικό `href` που **περιέχει** την υπο‑ακολουθία `download` (`*=` είναι ο τελεστής “contains”) |

> **Ακρόατο σενάριο:** Αν η σελίδα χρησιμοποιεί σχετικές διευθύνσεις URL (π.χ., `href="/files/download.zip"`), το Aspose.HTML θα τις διατηρήσει όπως είναι. Μπορεί να χρειαστεί να τις επιλύσετε σε σχέση με το βασικό URL αργότερα.

## Βήμα 4: Εξαγωγή Συνδέσμων Λήψης

Τώρα που έχουμε ένα `NodeList`, η εξαγωγή των πραγματικών URL είναι απλή. Θα μετατρέψουμε κάθε κόμβο σε `Element` και θα διαβάσουμε το χαρακτηριστικό `href` του.

```java
System.out.println("\n--- Extracted Download Links ---");
for (int i = 0; i < downloadLinks.getLength(); i++) {
    Element anchor = (Element) downloadLinks.item(i);
    String href = anchor.getAttribute("href");
    // Resolve relative URLs to absolute ones (optional but handy)
    String absoluteHref = document.getBaseUrl().resolve(href).toString();
    System.out.println(absoluteHref);
}
```

**Αποτέλεσμα που θα δείτε** (δείγμα εξόδου):

```
CSS found 3 nodes.

--- Extracted Download Links ---
https://example.com/files/report-download.pdf
https://example.com/downloads/setup.exe
https://cdn.example.com/assets/manual-download.docx
```

Αν χρειάζεστε μόνο την ακατέργαστη τιμή του χαρακτηριστικού, παραλείψτε την κλήση `resolve`. Το βήμα επίλυσης είναι χρήσιμο όταν αργότερα τροφοδοτείτε αυτά τα URL σε έναν downloader.

## Βήμα 5: Αναζήτηση HTML με XPath – Καταμέτρηση Κόμβων XPath

Μερικές φορές προτιμάτε το XPath—ιδιαίτερα όταν χρειάζεστε πιο σύνθετα ιεραρχικά ερωτήματα. Η ισοδύναμη έκφραση XPath για τον CSS selector μας είναι:

```xpath
//a[contains(@href,'download')]
```

Ας το εκτελέσουμε και ας δούμε πόσοι κόμβοι θα ληφθούν.

```java
// Step 5: Perform the same search using XPath
NodeList xpathNodes = document.selectNodes("//a[contains(@href,'download')]");

// Output the count
System.out.println("\nXPath found " + xpathNodes.getLength() + " nodes.");
```

Η έξοδος πρέπει να ταιριάζει με την καταμέτρηση CSS, επιβεβαιώνοντας ότι και οι δύο προσεγγίσεις είναι ισοδύναμες:

```
XPath found 3 nodes.
```

> **Γιατί και τα δύο;** Η χρήση και των δύο selectors στον ίδιο κώδικα σας δίνει ευελιξία. Το CSS είναι σύντομο για απλούς ελέγχους χαρακτηριστικών, ενώ το XPath ξεχωρίζει όταν χρειάζεται να περιηγηθείτε πάνω/κάτω στο δέντρο ή να συνδυάσετε πολλαπλές συνθήκες.

## Βήμα 6: Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα, εδώ είναι η πλήρης κλάση που μπορείτε να αντιγράψετε‑επικολλήσετε στο IDE σας και να τρέξετε αμέσως.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;

public class QueryExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the HTML document from a web page
        String url = "https://example.com";
        HTMLDocument document = new HTMLDocument(url);
        System.out.println("Document loaded from " + url);

        // 2️⃣ Search HTML with CSS – select elements with attribute
        NodeList cssMatches = document.selectElements("a[href*='download']");
        System.out.println("\nCSS found " + cssMatches.getLength() + " nodes.");

        // 3️⃣ Extract download links
        System.out.println("\n--- Extracted Download Links ---");
        for (int i = 0; i < cssMatches.getLength(); i++) {
            Element anchor = (Element) cssMatches.item(i);
            String href = anchor.getAttribute("href");
            // Resolve relative URLs (optional)
            String absolute = document.getBaseUrl().resolve(href).toString();
            System.out.println(absolute);
        }

        // 4️⃣ Search HTML with XPath – count xpath nodes
        NodeList xpathMatches = document.selectNodes("//a[contains(@href,'download')]");
        System.out.println("\nXPath found " + xpathMatches.getLength() + " nodes.");
    }
}
```

### Αναμενόμενη έξοδος κονσόλας (μπορεί να διαφέρει ανά ιστότοπο)

```
Document loaded from https://example.com

CSS found 3 nodes.

--- Extracted Download Links ---
https://example.com/files/report-download.pdf
https://example.com/downloads/setup.exe
https://cdn.example.com/assets/manual-download.docx

XPath found 3 nodes.
```

Εκτελέστε το πρόγραμμα, και θα δείτε αμέσως όλους τους συνδέσμους που περιέχουν “download”. Αλλάξτε τον selector ή το XPath string ώστε να ταιριάζει στα δικά σας κριτήρια—ίσως `a[href$='.pdf']` μόνο για PDF, ή `//div[@class='product']//a` για σελίδες προϊόντων.

## Συνηθισμένα Πιθανά Προβλήματα & Πώς να τα Αποφύγετε

| Πρόβλημα | Σύμπτωμα | Διόρθωση |
|----------|----------|----------|
| **Σφάλματα πιστοποιητικού HTTPS** | `javax.net.ssl.SSLHandshakeException` | Προσθέστε έναν trust manager ή χρησιμοποιήστε ένα URL με έγκυρο πιστοποιητικό. Για γρήγορη δοκιμή, μπορείτε να απενεργοποιήσετε την επικύρωση πιστοποιητικού, αλλά ποτέ σε παραγωγή. |
| **Βρόχοι ανακατεύθυνσης** | Το πρόγραμμα κολλάει ή πετάει `Too many redirects` | Ορίστε ένα λογικό όριο ανακατεύθυνσης (`document.setRedirectLimit(5)`) ή ελέγξτε το URL προορισμού χειροκίνητα. |
| **Σχετικά URLs** | Οι εξαγόμενοι σύνδεσμοι ξεκινούν με `/` αντί για πλήρη domain | Χρησιμοποιήστε `document.getBaseUrl().resolve(relative)` όπως φαίνεται στο παράδειγμα. |
| **Μεγάλες σελίδες** | Υψηλή χρήση μνήμης | Ροή (stream) της απάντησης ή χρήση υπερφορτώσεων `HTMLDocument` που περιορίζουν το μέγεθος του DOM. |
| **Λείπει άδεια Aspose** | Η εκτέλεση πετάει `LicenseException` μετά τη λήξη της δοκιμής | Αγοράστε άδεια ή συνεχίστε να χρησιμοποιείτε τη δοκιμή για μη‑εμπορικά πειράματα. |

## Επόμενα Βήματα & Σχετικά Θέματα

- Κατεβάστε τα αρχεία – συνδυάστε τα εξαγόμενα URLs με το `HttpURLConnection` της Java ή το Apache HttpClient για να κατεβάσετε πραγματικά τους πόρους.
- Παράλληλη επεξεργασία – χρησιμοποιήστε `CompletableFuture` για να κατεβάζετε πολλά αρχεία ταυτόχρονα.
- Προχωρημένοι CSS selectors – δοκιμάστε `a[href$='.zip']` για επεκτάσεις αρχείων, ή `div[data-id]` για επιλογή στοιχείων με προσαρμοσμένα attributes.
- Συναρτήσεις XPath – εξερευνήστε `starts-with()`, `ends-with()` και λογικούς τελεστές (`and`, `or`) για πιο λεπτομερή ερωτήματα.
- Καθαρισμός HTML – αν σκοπεύετε να εμφανίσετε το ληφθέν HTML, σκεφτείτε τη χρήση βιβλιοθήκης όπως το Jsoup για καθαρισμό.

## Συμπέρασμα

Μόλις δείξαμε πώς να **φορτώσετε HTML από URL** σε Java, στη συνέχεια **αναζητήσετε HTML με CSS** για **επιλογή στοιχείων με χαρακτηριστικό**, **εξάγετε συνδέσμους λήψης**, και τέλος **μετρήσετε κόμβους XPath** για να επαληθεύσετε το αποτέλεσμα. Η προσέγγιση είναι σύντομη, βασίζεται σε μία μόνο βιβλιοθήκη και λειτουργεί τόσο για απλές εργασίες scraping όσο και για πιο σύνθετες αναλύσεις DOM.  

Μη διστάσετε να προσαρμόσετε τους selectors

## Τι Θα Μάθετε Στη Σύντομη Μελλοντική;

Τα παρακάτω tutorials καλύπτουν στενά σχετικά θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Φόρτωση Εγγράφων HTML από Ροή με Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-stream/)
- [Φόρτωση Εγγράφων HTML από Αρχείο στο Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Διαχείριση Συμβάντων Φόρτωσης Εγγράφου στο Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/handle-document-load-events/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}