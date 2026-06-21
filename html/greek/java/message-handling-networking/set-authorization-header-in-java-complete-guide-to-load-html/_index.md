---
category: general
date: 2026-03-25
description: Ορίστε την κεφαλίδα εξουσιοδότησης και φορτώστε HTML από URL με το Aspose.HTML
  σε Java. Μάθετε πώς να ορίζετε την κεφαλίδα accept, να διαμορφώνετε προσαρμοσμένες
  κεφαλίδες και να προσθέτετε κεφαλίδες HTTP με στυλ Java.
draft: false
keywords:
- set authorization header
- load html from url
- set accept header
- configure custom headers
- add http headers java
language: el
og_description: Ορίστε το header εξουσιοδότησης γρήγορα και με ασφάλεια. Αυτός ο οδηγός
  δείχνει πώς να φορτώσετε HTML από URL, να ορίσετε το header αποδοχής, να διαμορφώσετε
  προσαρμοσμένα headers και να προσθέσετε HTTP headers με Java.
og_title: Ορισμός κεφαλίδας εξουσιοδότησης σε Java – Φόρτωση HTML από URL
tags:
- Java
- HTTP
- Aspose.HTML
- Web Scraping
title: Ορισμός κεφαλίδας εξουσιοδότησης σε Java – Πλήρης οδηγός για τη φόρτωση HTML
  από URL
url: /el/java/message-handling-networking/set-authorization-header-in-java-complete-guide-to-load-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ορισμός Κεφαλίδας Authorization – Φόρτωση HTML από URL με Aspose.HTML

Έχετε ποτέ χρειαστεί να **set authorization header** όταν ανακτάτε μια προστατευμένη ιστοσελίδα σε Java; Ίσως να ανακτάτε μια αναφορά από ένα εσωτερικό API, ή να κάνετε scraping σε έναν πίνακα ελέγχου που μόνο το token της υπηρεσίας σας μπορεί να ξεκλειδώσει. Τα καλά νέα είναι ότι δεν χρειάζεται να συνθέσετε χαμηλού επιπέδου κώδικα `HttpURLConnection`. Με το Aspose.HTML μπορείτε να συνδέσετε προσαρμοσμένες HTTP κεφαλίδες—*συμπεριλαμβανομένης* της πολύ σημαντικής κεφαλίδας `Authorization`—απευθείας στον φορτωτή εγγράφου.

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό παράδειγμα που **sets the authorization header**, **sets the accept header**, και **configure custom headers** ώστε να μπορείτε να **load HTML from URL** με ασφάλεια. Στο τέλος θα έχετε μια έτοιμη προς εκτέλεση κλάση Java που εκτυπώνει τον τίτλο της σελίδας, και θα καταλάβετε πώς να **add HTTP headers Java** style για τυχόν μελλοντικές κλήσεις.

## Τι Θα Χρειαστείτε

- Java 17 ή νεότερη (ο κώδικας λειτουργεί σε οποιοδήποτε πρόσφατο JDK)
- Βιβλιοθήκη Aspose.HTML for Java (διαθέσιμη μέσω Maven Central)
- Ένα έγκυρο bearer token ή οποιοδήποτε άλλο διαπιστευτήριο που χρειάζεται να στείλετε
- Ένα IDE ή απλό επεξεργαστή κειμένου + γραμμή εντολών

Αυτό είναι όλο—δεν απαιτούνται επιπλέον βιβλιοθήκες HTTP client. Αν έχετε ήδη Maven, απλώς προσθέστε την εξάρτηση Aspose.HTML και είστε έτοιμοι.

## Βήμα 1: Εγκατάσταση Εξάρτησης Aspose.HTML

Πρώτα, βεβαιωθείτε ότι το JAR του Aspose.HTML βρίσκεται στο classpath σας. Σε ένα έργο Maven, προσθέστε:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Αν προτιμάτε Gradle:

```groovy
implementation 'com.aspose:aspose-html:23.9'
```

> **Pro tip:** Κρατήστε τον αριθμό έκδοσης ενημερωμένο· οι νεότερες εκδόσεις φέρνουν βελτιώσεις απόδοσης και καλύτερη υποστήριξη TLS.

## Βήμα 2: Δημιουργία Χάρτη Προσαρμοσμένων Κεφαλίδων

Για να **set authorization header** και **set accept header**, χρειάζεστε ένα `Map<String, String>` που περιέχει κάθε όνομα κεφαλίδας και την τιμή της. Αυτός ο χάρτης θα παραδοθεί στον φορτωτή αργότερα.

```java
// Step 2: Define the custom HTTP headers required by the remote page
Map<String, String> customHeaders = new HashMap<>();
customHeaders.put("Authorization", "Bearer abcdef123456"); // <-- set authorization header
customHeaders.put("Accept", "text/html");                // <-- set accept header
```

Εδώ προσθέτουμε ρητά **add HTTP headers Java** style, χρησιμοποιώντας το γνωστό `HashMap`. Μπορείτε να προσθέσετε όσες κεφαλίδες χρειάζεται το API—`User-Agent`, `Cookie`, κ.λπ.—καλώντας ξανά τη μέθοδο `put`.

## Βήμα 3: Συγκόλληση Κεφαλίδων στις Επιλογές Φόρτωσης HTML

Το Aspose.HTML εκθέτει το `HTMLDocumentLoadOptions`. Καλώντας τη μέθοδο `setCustomHeaders` λέμε στη βιβλιοθήκη να συμπεριλάβει τον χάρτη μας σε κάθε αίτημα.

```java
// Step 3: Attach the headers to the HTML load options
HTMLDocumentLoadOptions loadOptions = new HTMLDocumentLoadOptions();
loadOptions.setCustomHeaders(customHeaders); // configure custom headers
```

Το αντικείμενο `loadOptions` τώρα μεταφέρει την εντολή **configure custom headers**. Όταν το έγγραφο ανακτηθεί, το Aspose.HTML προσθέτει αυτόματα τις γραμμές `Authorization` και `Accept` στο HTTP αίτημα.

## Βήμα 4: Φόρτωση της Προστατευμένης Σελίδας

Τώρα πραγματικά **load HTML from URL**. Ο κατασκευαστής του `HTMLDocument` δέχεται το URL προορισμού και το `loadOptions` που μόλις προετοιμάσαμε.

```java
// Step 4: Load the secured HTML page using the configured options
try (HTMLDocument document = new HTMLDocument(
        "https://api.example.com/secured-page.html", loadOptions)) {

    // Step 5: Use the loaded document – here we simply print its title
    System.out.println("Page title: " + document.getTitle());
}
```

Επειδή τυλίξαμε το `HTMLDocument` σε ένα μπλοκ try‑with‑resources, το έγγραφο κλείνει αυτόματα, ελευθερώνοντας τις δικτυακές υποδοχές και τη μνήμη. Η κλήση θα πετύχει μόνο εάν η τιμή **set authorization header** είναι έγκυρη· διαφορετικά θα λάβετε σφάλμα 401.

### Αναμενόμενη Έξοδος

```
Page title: Secure Dashboard
```

Αν δείτε τον τίτλο να εκτυπώνεται, έχετε επιτυχώς **set authorization header**, **set accept header**, και **load HTML from URL** σε μια καθαρή ροή.

## Βήμα 5: Διαχείριση Ακραίων Περιστατικών και Συνηθισμένων Παγίδων

### 5.1 Ληγμένα Tokens

Τα tokens συχνά λήγουν μετά από μια ώρα. Αν λάβετε `401 Unauthorized`, ανανεώστε το token πρώτα, έπειτα ξαναδημιουργήστε τον χάρτη `customHeaders`. Μια γρήγορη βοηθητική μέθοδος μπορεί να κεντρικοποιήσει αυτή τη λογική:

```java
private static Map<String, String> buildHeaders(String token) {
    Map<String, String> map = new HashMap<>();
    map.put("Authorization", "Bearer " + token);
    map.put("Accept", "text/html");
    return map;
}
```

### 5.2 Ανακατευθύνσεις και Cookies

Το Aspose.HTML ακολουθεί τις ανακατευθύνσεις εξ ορισμού, αλλά τα cookies δεν διατηρούνται μεταξύ των ανακατευθύνσεων εκτός αν τα ενεργοποιήσετε ρητά:

```java
loadOptions.setEnableCookies(true);
```

### 5.3 Αποσφαλμάτωση Αιτημάτων

Αν η σελίδα εξακολουθεί να μην φορτώνει, ενεργοποιήστε την καταγραφή αιτημάτων:

```java
loadOptions.setEnableNetworkLogging(true);
loadOptions.setNetworkLogFile("network.log");
```

Εξετάστε το `network.log` για να επαληθεύσετε ότι η κεφαλίδα `Authorization` είναι παρούσα.

## Βήμα 6: Πλήρες Παράδειγμα Λειτουργίας

Ακολουθεί η πλήρης, έτοιμη προς εκτέλεση κλάση Java. Επικολλήστε την στο IDE σας, αντικαταστήστε το placeholder token και το URL, και πατήστε **Run**.

```java
import com.aspose.html.*;
import java.util.*;

public class UrlWithHeaders {
    public static void main(String[] args) throws Exception {

        // Step 2: Define the custom HTTP headers required by the remote page
        Map<String, String> customHeaders = new HashMap<>();
        customHeaders.put("Authorization", "Bearer abcdef123456"); // set authorization header
        customHeaders.put("Accept", "text/html");                // set accept header

        // Step 3: Attach the headers to the HTML load options
        HTMLDocumentLoadOptions loadOptions = new HTMLDocumentLoadOptions();
        loadOptions.setCustomHeaders(customHeaders); // configure custom headers

        // Optional: enable cookie handling and network logging for debugging
        loadOptions.setEnableCookies(true);
        loadOptions.setEnableNetworkLogging(true);
        loadOptions.setNetworkLogFile("network.log");

        // Step 4: Load the secured HTML page using the configured options
        try (HTMLDocument document = new HTMLDocument(
                "https://api.example.com/secured-page.html", loadOptions)) {

            // Step 5: Use the loaded document – here we simply print its title
            System.out.println("Page title: " + document.getTitle());
        }
    }
}
```

> **Note:** Ο παραπάνω κώδικας **adds HTTP headers Java**‑style, φορτώνει τη σελίδα και εκτυπώνει τον τίτλο. Δεν απαιτούνται πρόσθετες βιβλιοθήκες, καμία χειροκίνητη διαχείριση υποδοχών.

## Οπτική Επισκόπηση

![Διάγραμμα που δείχνει πώς να ορίσετε την κεφαλίδα authorization σε Java χρησιμοποιώντας το Aspose.HTML](/images/set-authorization-header-java.png)

Η εικονογράφηση επισημαίνει τη ροή: *Header Map → Load Options → HTMLDocument → Page Title*.

## Συχνές Ερωτήσεις

- **Μπορώ να χρησιμοποιήσω διαφορετικό σχήμα αυθεντικοποίησης;**  
  Απόλυτα. Απλώς αντικαταστήστε την τιμή της κεφαλίδας—π.χ., `customHeaders.put("Authorization", "Basic " + base64Creds);`.

- **Τι γίνεται αν το API επιστρέφει JSON αντί για HTML;**  
  Το Aspose.HTML αναμένει HTML, οπότε για JSON θα χρησιμοποιούσατε έναν απλό `HttpClient`. Το μοτίβο **add http headers java** παραμένει το ίδιο, ωστόσο.

- **Είναι αυτή η προσέγγιση thread‑safe;**  
  Η παρουσία `HTMLDocumentLoadOptions` δεν μοιράζεται μεταξύ νήματος. Δημιουργήστε ένα νέο αντικείμενο επιλογών ανά αίτημα για ασφάλεια.

## Συμπέρασμα

Τώρα ξέρετε πώς να **set authorization header**, **set accept header**, και **configure custom headers** ώστε να μπορείτε να **load HTML from URL** με το Aspose.HTML σε Java. Το πλήρες παράδειγμα δείχνει ολόκληρη τη διαδικασία—από τη δημιουργία ενός χάρτη κεφαλίδων μέχρι την εκτύπωση του τίτλου της σελίδας—καλύπτοντας ταυτόχρονα ακραίες περιπτώσεις όπως η λήξη του token και η διαχείριση cookies.

Στη συνέχεια, ίσως θελήσετε να **add HTTP headers Java** για αιτήματα POST, να αναλύσετε το ανακτημένο DOM, ή να ενσωματώσετε αυτό το απόσπασμα σε ένα μεγαλύτερο πλαίσιο web‑scraping. Ό,τι και να επιλέξετε, το μοτίβο παραμένει το ίδιο: δημιουργήστε έναν χάρτη κεφαλίδων, συνδέστε τον μέσω `HTMLDocumentLoadOptions`, και αφήστε το Aspose.HTML να κάνει το σκληρό έργο.

Καλό κώδικα, και εύχομαι οι κλήσεις HTTP σας να επιστρέφουν πάντα τα δεδομένα που χρειάζεστε!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}