---
category: general
date: 2026-05-06
description: Απόδοση HTML σε PNG σε Java χρησιμοποιώντας το Aspose.HTML, προσθήκη
  token τύπου bearer και προσαρμοσμένων κεφαλίδων για τη φόρτωση προστατευμένων σελίδων.
  Μάθετε πώς να αποθηκεύετε HTML ως PNG γρήγορα.
draft: false
keywords:
- render html to png
- save html as png
- add bearer token
- how to pass header
- use custom headers
language: el
og_description: Μετατροπή HTML σε PNG σε Java με το Aspose.HTML, προσθήκη bearer token
  και προσαρμοσμένων κεφαλίδων για τη φόρτωση προστατευμένων σελίδων, και αποθήκευση
  του HTML ως PNG.
og_title: Μετατροπή HTML σε PNG σε Java – Προσθήκη Bearer Token & Προσαρμοσμένων κεφαλίδων
tags:
- Java
- Aspose.HTML
- Image Rendering
- HTTP Authentication
title: Απόδοση HTML σε PNG σε Java – Προσθήκη Bearer Token & Προσαρμοσμένων κεφαλίδων
url: /el/java/conversion-html-to-various-image-formats/render-html-to-png-in-java-add-bearer-token-custom-headers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Απόδοση HTML σε PNG σε Java – Πλήρης Οδηγός

Έχετε ποτέ χρειαστεί να **αποδώσετε HTML σε PNG** σε Java ενώ αντιμετωπίζετε ένα ασφαλισμένο endpoint; Με το Aspose.HTML μπορείτε να φορτώσετε μια προστατευμένη σελίδα, **να προσθέσετε ένα bearer token**, και **να αποθηκεύσετε το HTML ως PNG**—όλα σε λίγες γραμμές.  

Σε αυτό το tutorial θα περάσουμε από κάθε βήμα: από την προετοιμασία προσαρμοσμένων headers μέχρι τη μετατροπή του φορτωμένου εγγράφου σε ένα καθαρό αρχείο PNG. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση πρόγραμμα που μπορεί να αποδώσει οποιαδήποτε αυθεντικοποιημένη σελίδα HTML σε εικόνα στο δίσκο.

## Τι Θα Μάθετε

* Πώς να **προσθέσετε bearer token** σε ένα HTTP αίτημα χρησιμοποιώντας ένα `Map` από headers.  
* Η ακριβής σύνταξη για **πώς να περάσετε τιμές header** στο `HTMLDocument`.  
* Ο πιο απλός τρόπος για **να αποθηκεύσετε HTML ως PNG** με το `Converter` του Aspose.HTML.  
* Συμβουλές για την αντιμετώπιση κοινών προβλημάτων (π.χ., σφάλματα πιστοποιητικού, ελλιπείς πόροι).  

Καμία εξωτερική εργαλειοθήκη, καμία μαγεία—απλώς καθαρή Java, λίγες εισαγωγές, και η βιβλιοθήκη Aspose.HTML (έκδοση 23.10 ή νεότερη).  

### Προαπαιτούμενα

* Java 8 ή νεότερη εγκατεστημένη.  
* Aspose.HTML for Java JAR στο classpath σας.  
* Ένα έγκυρο bearer token για τον στόχο (μπορείτε να το αποκτήσετε μέσω OAuth2, κλειδιού API, κ.λπ.).  

Αν είστε άνετοι με τη βασική σύνταξη της Java, είστε έτοιμοι να ξεκινήσετε.  

## Απόδοση HTML σε PNG – Επισκόπηση

Η βασική ιδέα είναι απλή: δημιουργήστε ένα `HTMLDocument` που ξέρει πώς να φέρει τη σελίδα **με προσαρμοσμένα headers**, έπειτα δώστε αυτό το έγγραφο στο `Converter.convertHtmlToPng`. Ο μετατροπέας κάνει όλη τη βαριά δουλειά—διάταξη, CSS, εικόνες, γραμματοσειρές—ώστε να καταλήξετε με ένα pixel‑perfect στιγμιότυπο.

```java
import com.aspose.html.*;
import java.util.*;

public class AuthenticatedLoad {
    public static void main(String[] args) throws Exception {

        // Step 1: Prepare the HTTP headers with the bearer token
        Map<String, String> authHeaders = new HashMap<>();
        authHeaders.put("Authorization", "Bearer my-secure-token");

        // Step 2: Load the protected HTML page using the custom headers
        String protectedUrl = "https://secure.example.com/report.html";
        HTMLDocument document = new HTMLDocument(protectedUrl, authHeaders);

        // Step 3: Render the loaded page to a PNG file to verify the result
        String outputImagePath = "YOUR_DIRECTORY/secure.png";
        Converter.convertHtmlToPng(document, outputImagePath);

        System.out.println("Page rendered and saved to: " + outputImagePath);
    }
}
```

Αυτό το απόσπασμα κώδικα είναι η πλήρης λύση, αλλά ας εξηγήσουμε γιατί κάθε γραμμή είναι σημαντική.

## Προσθήκη Bearer Token σε HTTP Αίτηση

Όταν ένας ιστότοπος προστατεύει τους πόρους του, αναμένει ένα header `Authorization` της μορφής `Bearer <token>`. Τοποθετώντας αυτό το header σε ένα `Map<String,String>` και περνώντας το χάρτη στον κατασκευαστή του `HTMLDocument`, το Aspose.HTML αυτόματα ενσωματώνει το header σε κάθε αίτημα που κάνει (HTML, CSS, εικόνες, κλήσεις AJAX).

```java
Map<String, String> authHeaders = new HashMap<>();
authHeaders.put("Authorization", "Bearer my-secure-token");
```

**Γιατί να χρησιμοποιήσετε έναν χάρτη;**  
* Είναι τύπου‑ασφαλές και σας επιτρέπει να προσθέσετε *οποιονδήποτε* αριθμό προσαρμοσμένων headers—τέλειο για APIs που χρειάζονται `X‑API‑KEY` ή `Accept-Language`.  
* Ο χάρτης επαναχρησιμοποιείται για όλα τα επόμενα αιτήματα πόρων, εξασφαλίζοντας συνεπή αυθεντικοποίηση.

> **Pro tip:** Αν το token σας λήγει μετά από σύντομο διάστημα, ανανεώστε το πριν δημιουργήσετε το `HTMLDocument`. Διαφορετικά θα λάβετε σφάλμα 401 και το PNG θα είναι κενό.

## Πώς να Περνάτε Header Χρησιμοποιώντας Προσαρμοσμένα Headers

Το overload του `HTMLDocument` του Aspose.HTML που δέχεται ένα `Map` είναι ο πιο καθαρός τρόπος για **να χρησιμοποιήσετε προσαρμοσμένα headers**. Θα μπορούσατε επίσης να χρησιμοποιήσετε το `HttpClient` χειροκίνητα, αλλά αυτό προσθέτει περιττή πολυπλοκότητα.

```java
HTMLDocument document = new HTMLDocument(protectedUrl, authHeaders);
```

Στο παρασκήνιο, η βιβλιοθήκη δημιουργεί ένα εσωτερικό `HttpWebRequest` και αντιγράφει κάθε καταχώρηση από το `authHeaders`. Αυτό σημαίνει ότι μπορείτε επίσης να περάσετε headers όπως:

```java
authHeaders.put("User-Agent", "MyApp/1.0");
authHeaders.put("Accept-Language", "en-US");
```

Αν χρειαστεί να **προσθέσετε bearer token** υπό όρους (π.χ., μόνο για ορισμένους τομείς), απλώς ελέγξτε το URL πριν γεμίσετε το χάρτη.

## Αποθήκευση HTML ως Αρχείο PNG

Το τελικό βήμα είναι όπου συμβαίνει η μαγεία: η μετατροπή του πλήρως φορτωμένου DOM σε μια raster εικόνα. Το `Converter.convertHtmlToPng` διαχειρίζεται αυτόματα τη διάταξη, το DPI και το βάθος χρώματος.

```java
String outputImagePath = "YOUR_DIRECTORY/secure.png";
Converter.convertHtmlToPng(document, outputImagePath);
```

Μπορείτε να ρυθμίσετε την ποιότητα εξόδου παρέχοντας ένα `PngDevice` με προσαρμοσμένες ρυθμίσεις, αλλά η προεπιλογή λειτουργεί για τις περισσότερες περιπτώσεις.

**Αναμενόμενο αποτέλεσμα:** ένα αρχείο PNG που βρίσκεται στο `YOUR_DIRECTORY/secure.png` και φαίνεται ακριβώς όπως η σελίδα που θα δείτε σε έναν περιηγητή (χωρίς διαδραστικό JavaScript).

## Επαλήθευση της Αποδοθείσας Εικόνας

Αφού το πρόγραμμα ολοκληρωθεί, ανοίξτε το PNG με οποιονδήποτε προβολέα εικόνων. Αν η σελίδα εμφανίζει οθόνη σύνδεσης ή μήνυμα σφάλματος 401, ελέγξτε ξανά:

1. Το bearer token είναι ακόμα έγκυρο.  
2. Η ορθογραφία του header `Authorization` είναι σωστή (`Bearer` + διάστημα).  
3. Το URL προορισμού είναι προσβάσιμο από το μηχάνημά σας (τείχος προστασίας, VPN, κ.λπ.).  

Αν όλα ευθυγραμμιστούν, θα δείτε την προστατευμένη αναφορά αποδομένη pixel‑perfect.

![Αποτέλεσμα απόδοσης προστατευμένης σελίδας αποθηκευμένης ως PNG](render_html_to_png.png)

*Κείμενο εναλλακτικής περιγραφής: Στιγμιότυπο οθόνης που δείχνει μια αποδοθείσα σελίδα HTML αποθηκευμένη ως PNG μετά την προσθήκη bearer token και προσαρμοσμένων headers.*

## Ακραίες Περιπτώσεις & Συνηθισμένα Πιθανά Σφάλματα

| Situation | What to Check | Suggested Fix |
|-----------|---------------|---------------|
| **Self‑signed SSL certificate** | `SSLHandshakeException` | Προσθέστε ένα προσαρμοσμένο `TrustManager` ή εκκινήστε τη Java με `-Djavax.net.ssl.trustStore` που δείχνει στο πιστοποιητικό. |
| **Large page (over 10 MB)** | Memory blow‑up | Αυξήστε τη μνήμη heap της JVM (`-Xmx2g`) ή αποδώστε μόνο ένα συγκεκριμένο στοιχείο χρησιμοποιώντας `document.getElementById`. |
| **Dynamic content loaded via AJAX** | Content missing in PNG | Χρησιμοποιήστε `document.waitForLoad()` πριν τη μετατροπή, ή ενεργοποιήστε `HtmlLoadOptions.setEnableJavaScript(true)`. |
| **Missing fonts** | Text displayed with fallback font | Εγκαταστήστε τις απαιτούμενες γραμματοσειρές στον κεντρικό υπολογιστή ή ενσωματώστε τις μέσω CSS `@font-face`. |

Η αντιμετώπιση αυτών των θεμάτων νωρίς σας εξοικονομεί ώρες εντοπισμού σφαλμάτων αργότερα.

## Συμπέρασμα: Απόδοση HTML σε PNG με Σιγουριά

Καλύψαμε ολόκληρη τη ροή εργασίας για **απόδοση HTML σε PNG** σε Java, από **προσθήκη bearer token** μέχρι **χρήση προσαρμοσμένων headers**, και τέλος **αποθήκευση HTML ως PNG**. Το πλήρες, εκτελέσιμο παράδειγμα βρίσκεται στην αρχή αυτού του οδηγού, ώστε να μπορείτε να το αντιγράψετε‑επικολλήσετε και να το προσαρμόσετε αμέσως.

### Τι Ακολουθεί;

* Πειραματιστείτε με διαφορετικές μορφές εικόνας (`convertHtmlToJpeg`, `convertHtmlToBmp`).  
* Προσπαθήστε να αποδώσετε μόνο ένα συγκεκριμένο στοιχείο DOM φορτώνοντας τη σελίδα, επιλέγοντας το στοιχείο, και περνώντας το σε ένα `PngDevice`.  
* Συνδυάστε αυτήν την τεχνική με έναν χρονοπρογραμματιστή για να δημιουργείτε αυτόματα καθημερινά στιγμιότυπα αναφορών.

Νιώστε ελεύθεροι να τροποποιήσετε το χάρτη headers, να αντικαταστήσετε τον πάροχο token, ή να ενσωματώσετε τον κώδικα σε μια μεγαλύτερη μικροϋπηρεσία. Οι δυνατότητες είναι πρακτικά ατελείωτες, και το βασικό μοτίβο—**χρησιμοποιήστε προσαρμοσμένα headers, φορτώστε το έγγραφο, μετατρέψτε σε PNG**—παραμένει το ίδιο.

Καλή προγραμματιστική, και οι στιγμιότυπες οθόνης σας να είναι πάντα κρυστάλλινα καθαρές!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}