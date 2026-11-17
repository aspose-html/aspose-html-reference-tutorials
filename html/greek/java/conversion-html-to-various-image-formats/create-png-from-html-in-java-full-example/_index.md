---
category: general
date: 2026-06-07
description: Δημιουργήστε PNG από HTML σε Java χρησιμοποιώντας το Aspose.HTML. Μάθετε
  πώς να αποδίδετε HTML σε PNG, να ορίζετε το user agent στη Java και να ρυθμίζετε
  την αναλογία εικονοστοιχείων της συσκευής σε λίγα μόνο βήματα.
draft: false
keywords:
- create png from html
- render html to png
- set user agent java
- convert html to png
- set device pixel ratio
language: el
og_description: Δημιουργήστε PNG από HTML σε Java με το Aspose.HTML. Αυτό το σεμινάριο
  δείχνει πώς να αποδίδετε HTML σε PNG, να ορίσετε τον πράκτορα χρήστη Java και να
  ρυθμίσετε την αναλογία εικονοστοιχείων της συσκευής.
og_title: Δημιουργία PNG από HTML σε Java – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-07'
  description: Create PNG from HTML in Java using Aspose.HTML. Learn to render HTML
    to PNG, set user agent Java, and adjust device pixel ratio in just a few steps.
  headline: Create PNG from HTML in Java – Full Example
  type: TechArticle
- description: Create PNG from HTML in Java using Aspose.HTML. Learn to render HTML
    to PNG, set user agent Java, and adjust device pixel ratio in just a few steps.
  name: Create PNG from HTML in Java – Full Example
  steps:
  - name: Setting the Viewport Width
    text: '```java renderingSandbox.setDeviceWidth(375); // 375 px width – typical
      iPhone size ```'
  - name: Adjusting the Device Pixel Ratio
    text: '```java renderingSandbox.setDevicePixelRatio(2.0); // 2× pixel density
      for retina displays ```'
  - name: Providing a Custom User‑Agent (set user agent java)
    text: '```java renderingSandbox.setUserAgent( "Mozilla/5.0 (iPhone; CPU iPhone
      OS 14_0 like Mac OS X) " + "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0
      Mobile/15E148 Safari/604.1" ); ```'
  - name: Expected Output
    text: 'Open the PNG in any image viewer and you should see:'
  type: HowTo
tags:
- Java
- Aspose.HTML
- Image Conversion
title: Δημιουργία PNG από HTML σε Java – Πλήρες Παράδειγμα
url: /el/java/conversion-html-to-various-image-formats/create-png-from-html-in-java-full-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία PNG από HTML σε Java – Πλήρες Παράδειγμα

Έχετε ποτέ σκεφτεί πώς να **δημιουργήσετε PNG από HTML** απευθείας μέσα σε μια εφαρμογή Java; Ίσως χρειάζεστε μια μικρογραφία για προεπισκόπηση email, ή θέλετε να δημιουργήσετε κάρτες κοινωνικών μέσων εν κινήσει. Σε κάθε περίπτωση, η **απόδοση HTML σε PNG** χωρίς άνοιγμα προγράμματος περιήγησης είναι ένα χρήσιμο κόλπο που εξοικονομεί χρόνο και πόρους.

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από μια πρακτική, ολοκληρωμένη λύση που χρησιμοποιεί το Aspose.HTML for Java. Θα δείτε πώς να **ορίσετε το user agent Java**, να ρυθμίσετε το **device pixel ratio**, και τελικά να **μετατρέψετε HTML σε PNG** με λίγες μόνο γραμμές κώδικα. Χωρίς εξωτερικές υπηρεσίες, χωρίς headless Chrome—απλός κώδικας Java που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο.

## Τι Θα Μάθετε

- Πώς να φορτώσετε μια σελίδα HTML που περιέχει media queries.
- Πώς να δημιουργήσετε ένα sandbox απόδοσης που μιμείται μια κινητή συσκευή.
- Πώς να **ορίσετε το device pixel ratio** και μια προσαρμοσμένη συμβολοσειρά user‑agent.
- Πώς να **αποδώσετε HTML σε PNG** και να αποθηκεύσετε το αποτέλεσμα στο δίσκο.
- Συμβουλές για την αντιμετώπιση κοινών προβλημάτων (ελλιπείς γραμματοσειρές, πόροι cross‑origin κ.λπ.).

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

- Java 17 ή νεότερη (το API λειτουργεί με Java 8+, αλλά οι νεότερες εκδόσεις προσφέρουν καλύτερη απόδοση).
- Βιβλιοθήκη Aspose.HTML for Java (μπορείτε να τη λάβετε από το Maven Central).
- Ένα IDE ή εργαλείο κατασκευής της επιλογής σας (IntelliJ IDEA, Maven, Gradle—ό,τι προτιμάτε).

Έτοιμοι; Ας βάλουμε τα χέρια στη δουλειά.

## Βήμα 1: Ρύθμιση του Έργου και Προσθήκη του Aspose.HTML

Πρώτα, προσθέστε την εξάρτηση Aspose.HTML στο `pom.xml` εάν χρησιμοποιείτε Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- check for the latest version -->
</dependency>
```

Ή, για Gradle:

```gradle
implementation 'com.aspose:aspose-html:23.9'
```

Μόλις η βιβλιοθήκη είναι στο classpath, είστε έτοιμοι να **δημιουργήσετε PNG από HTML**.

## Βήμα 2: Φόρτωση του Εγγράφου HTML (το σημείο εκκίνησης για τη μετατροπή)

Το πρώτο που χρειαζόμαστε είναι μια παρουσία `HTMLDocument` που δείχνει στο πηγαίο HTML. Μπορεί να είναι τοπικό αρχείο, URL ή ακόμη και μια συμβολοσειρά που περιέχει ακατέργαστο markup.

```java
// Step 2: Load the HTML document that contains media queries
HTMLDocument htmlDoc = new HTMLDocument("https://YOUR_DOMAIN/responsive.html");
```

> **Γιατί είναι σημαντικό:** Η φόρτωση του εγγράφου μέσω Aspose.HTML μας δίνει πλήρη έλεγχο της αλυσίδας απόδοσης, επιτρέποντάς μας αργότερα να ενσωματώσουμε ένα sandbox με προσαρμοσμένες ρυθμίσεις συσκευής.

## Βήμα 3: Δημιουργία Sandbox Απόδοσης για Προσομοίωση Κινητής Συσκευής

Ένα sandbox είναι ουσιαστικά ένα εικονικό περιβάλλον προγράμματος περιήγησης. Με τη διαμόρφωσή του, μπορούμε να **ορίσουμε το device pixel ratio** και άλλες παραμέτρους που επηρεάζουν τη συμπεριφορά των CSS media queries.

```java
// Step 3: Create a rendering sandbox that simulates a mobile device
RenderingSandbox renderingSandbox = new RenderingSandbox();
```

### Ορισμός Πλάτους Viewport

```java
renderingSandbox.setDeviceWidth(375); // 375 px width – typical iPhone size
```

### Ρύθμιση του Device Pixel Ratio

```java
renderingSandbox.setDevicePixelRatio(2.0); // 2× pixel density for retina displays
```

### Παροχή Προσαρμοσμένου User‑Agent (set user agent java)

```java
renderingSandbox.setUserAgent(
    "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
    "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0 Mobile/15E148 Safari/604.1"
);
```

> **Συμβουλή επαγγελματία:** Η αντιστοίχιση μιας πραγματικής συμβολοσειράς user‑agent μιας συσκευής εξασφαλίζει ότι οποιοδήποτε JavaScript ή CSS που ελέγχει το `navigator.userAgent` συμπεριφέρεται ακριβώς όπως στη συσκευή αυτή.

## Βήμα 4: Σύνδεση του Sandbox με το Έγγραφο

Τώρα συνδέουμε το sandbox με το έγγραφο HTML ώστε όλες οι επόμενες αποδόσεις να σέβονται τις ρυθμίσεις κινητής που μόλις ορίσαμε.

```java
// Step 4: Apply the sandbox to the document so it renders with the mobile settings
htmlDoc.setSandbox(renderingSandbox);
```

Αν παραλείψετε αυτό το βήμα, θα χρησιμοποιηθεί το προεπιλεγμένο desktop viewport και τα media queries για κινητά δεν θα ενεργοποιηθούν—σημαίνει ότι το PNG εξόδου δεν θα μοιάζει με οθόνη τηλεφώνου.

## Βήμα 5: Επιλογή Επιλογών Αποθήκευσης Εικόνας (convert html to png)

Το Aspose.HTML υποστηρίζει πολλές μορφές εικόνας. Για ένα καθαρό PNG, δημιουργούμε μια παρουσία `ImageSaveOptions` με `SaveFormat.PNG`.

```java
// Step 5: Prepare image save options for PNG output
ImageSaveOptions imageOptions = new ImageSaveOptions(SaveFormat.PNG);
```

Μπορείτε επίσης να ρυθμίσετε DPI, χρώμα φόντου ή επίπεδο συμπίεσης μέσω του αντικειμένου `imageOptions` εάν χρειάζεστε ένα στοιχείο υψηλότερης ανάλυσης.

## Βήμα 6: Απόδοση και Αποθήκευση – το τελικό βήμα **convert html to png**

Η τελευταία γραμμή εκτελεί τη βαριά δουλειά: αποδίδει τη σελίδα μέσα στο sandbox και γράφει το bitmap στο δίσκο.

```java
// Step 6: Render the page and save it as an image that reflects the mobile viewport
htmlDoc.save("YOUR_DIRECTORY/mobile-view.png", imageOptions);
```

Όταν το πρόγραμμα ολοκληρωθεί, θα βρείτε ένα αρχείο `mobile‑view.png` που φαίνεται ακριβώς όπως η σελίδα σε iPhone πλάτους 375 px με πυκνότητα 2× pixel.

### Αναμενόμενο Αποτέλεσμα

Ανοίξτε το PNG σε οποιονδήποτε προβολέα εικόνων και θα πρέπει να δείτε:

- Κείμενο με μέγεθος σύμφωνα με τα mobile CSS breakpoints.
- Εικόνες κλιμακωμένες για οθόνη υψηλής πυκνότητας (ευχαριστώντας την κλήση **set device pixel ratio**).
- Οποιαδήποτε ανταποκρινόμενη πλοήγηση να έχει συμπτυστεί στην κινητή της εκδοχή.

Εάν το αποτέλεσμα φαίνεται λανθασμένο, ελέγξτε ξανά το URL, βεβαιωθείτε ότι όλοι οι εξωτερικοί πόροι είναι προσβάσιμοι και επαληθεύστε ότι οι ρυθμίσεις του sandbox ταιριάζουν με τη στοχευόμενη συσκευή.

## Συνηθισμένα Προβλήματα & Πώς να Τα Διορθώσετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Ελλιπείς γραμματοσειρές** | Το sandbox δεν έχει πρόσβαση στις γραμματοσειρές του συστήματος που χρησιμοποιεί η σελίδα. | Εγκαταστήστε τις απαιτούμενες γραμματοσειρές στον διακομιστή ή ενσωματώστε web‑fonts μέσω `@font-face`. |
| **Αποκλεισμένες εικόνες cross‑origin** | Το Aspose.HTML σέβεται τις πολιτικές CORS. | Φιλοξενήστε τις εικόνες στον ίδιο τομέα ή ενεργοποιήστε τις κεφαλίδες CORS στον διακομιστή προέλευσης. |
| **JavaScript δεν εκτελείται** | Από προεπιλογή, το Aspose.HTML απενεργοποιεί την εκτέλεση script για ασφάλεια. | Καλέστε `renderingSandbox.setEnableJavaScript(true)` εάν χρειάζεστε αλλαγές διάταξης που προκαλούνται από script (χρησιμοποιήστε με προσοχή). |
| **Ασαφές αποτέλεσμα σε οθόνες retina** | Το DPI προεπιλογή είναι 96. | Ορίστε `imageOptions.setDpiX(300); imageOptions.setDpiY(300);` για υψηλότερη ανάλυση. |

## Πλήρες Παράδειγμα Εργασίας (Όλα τα Βήματα σε Ένα Σημείο)

Παρακάτω είναι η πλήρης, έτοιμη για εκτέλεση κλάση Java. Αντικαταστήστε τα `YOUR_DOMAIN` και `YOUR_DIRECTORY` με πραγματικές τιμές.

```java
import com.aspose.html.*;
import com.aspose.html.saving.*;
import com.aspose.html.rendering.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the HTML document that contains media queries
        HTMLDocument htmlDoc = new HTMLDocument("https://YOUR_DOMAIN/responsive.html");

        // Step 2: Create a rendering sandbox that simulates a mobile device
        RenderingSandbox renderingSandbox = new RenderingSandbox();

        // Step 3: Configure the sandbox (viewport width, pixel ratio, and user‑agent)
        renderingSandbox.setDeviceWidth(375);                     // 375 px width
        renderingSandbox.setDevicePixelRatio(2.0);               // 2× pixel density
        renderingSandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0 Mobile/15E148 Safari/604.1");

        // Step 4: Apply the sandbox to the document so it renders with the mobile settings
        htmlDoc.setSandbox(renderingSandbox);

        // Step 5: Prepare image save options for PNG output
        ImageSaveOptions imageOptions = new ImageSaveOptions(SaveFormat.PNG);

        // Step 6: Render the page and save it as an image that reflects the mobile viewport
        htmlDoc.save("YOUR_DIRECTORY/mobile-view.png", imageOptions);
    }
}
```

Εκτελέστε το πρόγραμμα (`mvn exec:java` ή τη ρύθμιση εκτέλεσης του IDE) και θα έχετε μια **create PNG from HTML** ροή εργασίας που λειτουργεί εντελώς εκτός σύνδεσης.

## Συμπέρασμα

Μόλις καλύψαμε όλα όσα χρειάζεστε για να **δημιουργήσετε PNG από HTML** σε Java—φόρτωση του εγγράφου, διαμόρφωση sandbox, **setting user agent java**, ρύθμιση του **device pixel ratio**, και τελικά **render html to png**. Ο κώδικας είναι σύντομος, οι εξαρτήσεις ελάχιστες, και το αποτέλεσμα είναι ένα PNG ιδανικού μεγέθους που αντικατοπτρίζει μια πραγματική κινητή συσκευή.

Τι ακολουθεί; Δοκιμάστε να αντικαταστήσετε τη μορφή PNG με JPEG εάν χρειάζεστε μικρότερα αρχεία, πειραματιστείτε με διαφορετικά πλάτη viewport για δημιουργία μικρογραφιών για tablets, ή ενσωματώστε αυτό το απόσπασμα σε ένα endpoint Spring Boot που επιστρέφει την εικόνα κατόπιν αιτήματος. Οι δυνατότητες είναι ατελείωτες, και τώρα έχετε μια σταθερή βάση για να χτίσετε.

Έχετε ερωτήσεις ή αντιμετωπίσατε κάποιο περίεργο edge case; Αφήστε ένα σχόλιο παρακάτω και ας το αντιμετωπίσουμε μαζί. Καλό κώδικα!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Convert HTML to PNG with Aspose.HTML for Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-png/)
- [Convert HTML to PNG with Aspose.HTML Message Handlers in Java](/html/english/java/configuring-environment/use-message-handlers/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}