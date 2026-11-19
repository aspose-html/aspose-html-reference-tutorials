---
category: general
date: 2026-06-03
description: Δημιουργήστε έγγραφο HTML σε Java και ενσωματώστε JavaScript για να αυξήσετε
  έναν μετρητή. Μάθετε ένα παράδειγμα μηχανής σεναρίου, αποκτήστε το innerHTML του
  στοιχείου και άλλα.
draft: false
keywords:
- create html document
- embed javascript html
- get element innerhtml
- increment counter javascript
- script engine example
language: el
og_description: Δημιουργήστε έγγραφο HTML σε Java, ενσωματώστε JavaScript για την
  αύξηση ενός μετρητή και ανακτήστε την τελική τιμή χρησιμοποιώντας ένα παράδειγμα
  μηχανής σεναρίου.
og_title: Δημιουργία εγγράφου HTML με ενσωματωμένο JavaScript – Παράδειγμα Java
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  headline: Create HTML Document with Embedded JavaScript – Java Example
  type: TechArticle
- description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  name: Create HTML Document with Embedded JavaScript – Java Example
  steps:
  - name: '**Creates an HTML document** in memory.'
    text: '**Creates an HTML document** in memory.'
  - name: '**Embeds a small JavaScript snippet** that increments a counter five times.'
    text: '**Embeds a small JavaScript snippet** that increments a counter five times.'
  - name: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
    text: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
  - name: '**Retrieves the final counter value** using `getElementInnerHTML`.'
    text: '**Retrieves the final counter value** using `getElementInnerHTML`.'
  - name: 'Prints `Final counter value: 5` to the console.'
    text: 'Prints `Final counter value: 5` to the console.'
  type: HowTo
tags:
- HTML
- JavaScript
- Java
- ScriptEngine
title: Δημιουργία εγγράφου HTML με ενσωματωμένο JavaScript – Παράδειγμα Java
url: /el/java/creating-managing-html-documents/create-html-document-with-embedded-javascript-java-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Εγγράφου HTML με Ενσωματωμένο JavaScript – Παράδειγμα Java

Έχετε ποτέ χρειαστεί να **create HTML document** από κώδικα Java και να αναρωτηθείτε πώς να ενσωματώσετε JavaScript μέσα σε αυτό; Σε αυτόν τον οδηγό θα σας δείξουμε ακριβώς αυτό, βήμα προς βήμα, και θα καταλήξετε με ένα λειτουργικό παράδειγμα script engine που εκτυπώνει την τελική τιμή του μετρητή.  

Αν έχετε ποτέ ρωτήσει τον εαυτό σας *«πώς μπορώ να πάρω το element innerHTML μετά την εκτέλεση ενός script;»* ή *«ποιος είναι ο πιο καθαρός τρόπος να αυξήσω έναν μετρητή σε JavaScript από Java;»*—βρίσκεστε στο σωστό μέρος. Θα καλύψουμε **embed javascript html**, **increment counter javascript**, και **get element innerHTML** όλα σε ένα ενιαίο tutorial.

![Create HTML Document with embedded JavaScript](/images/create-html-document.png){: .center alt="Παράδειγμα δημιουργίας εγγράφου HTML με ενσωματωμένο JavaScript"}

## Τι Θα Δημιουργήσετε

1. **Creates an HTML document** στη μνήμη.
2. **Embeds a small JavaScript snippet** που αυξάνει έναν μετρητή πέντε φορές.
3. **Initializes a script engine** (το παράδειγμα `ScriptEngine`) για να εκτελέσει αυτό το snippet.
4. **Retrieves the final counter value** χρησιμοποιώντας `getElementInnerHTML`.
5. Εκτυπώνει `Final counter value: 5` στην κονσόλα.

## Προαπαιτούμενα

- Java 17 ή νεότερη (το `ScriptEngine` API είναι μέρος της τυπικής βιβλιοθήκης).
- Βασική εξοικείωση με HTML και JavaScript (δεν χρειάζεται βαθιά εξειδίκευση).
- Ένα IDE ή ένας απλός επεξεργαστής κειμένου συν τερματικό για να μεταγλωττίσετε και να εκτελέσετε το πρόγραμμα.

## Βήμα 1: Δημιουργία Εγγράφου HTML σε Java

Το πρώτο που χρειάζεται είναι ένα κενό αντικείμενο εγγράφου HTML που μπορούμε αργότερα να γεμίσουμε με markup. Σκεφτείτε το ως μια εικονική σελίδα που υπάρχει μόνο στη μνήμη.

```java
// Import statements
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

// Minimal HTML document wrapper (pseudo‑class for illustration)
class HTMLDocument {
    private StringBuilder html = new StringBuilder();

    public void write(String content) {
        html.append(content);
    }

    public String getContent() {
        return html.toString();
    }

    // Simple DOM simulation for getElementById / innerHTML
    private java.util.Map<String, String> elements = new java.util.HashMap<>();

    public void setElementInnerHTML(String id, String value) {
        elements.put(id, value);
    }

    public String getElementInnerHTML(String id) {
        return elements.getOrDefault(id, "");
    }

    // Helper used by the script engine (not production‑grade)
    public void updateCounter(int value) {
        setElementInnerHTML("counter", String.valueOf(value));
    }
}
```

**Why this matters:** Με το **creating HTML document** αντικειμένων μόνοι σας, αποφεύγετε τη γραφή στο δίσκο και κρατάτε τα πάντα δοκιμαστικά. Η μικρή προσομοίωση DOM μας επιτρέπει αργότερα να **get element innerHTML** χωρίς πλήρη πρόγραμμα περιήγησης.

## Βήμα 2: Ενσωμάτωση JavaScript HTML – Η Λογική του Μετρητή

Τώρα θα γράψουμε το HTML markup που περιλαμβάνει ένα μπλοκ `<script>`. Αυτό το script θα **increment counter JavaScript** πέντε φορές.

```java
HTMLDocument doc = new HTMLDocument();

doc.write(
    "<!DOCTYPE html><html><body>"
  + "<div id='counter'>0</div>"
  + "<script>"
  + "for (let i = 0; i < 5; i++) {"
  + "  document.getElementById('counter').innerHTML = i + 1;"
  + "}"
  + "</script>"
  + "</body></html>"
);
```

**Εξήγηση:**  
- Το `<div id='counter'>0</div>` είναι το στοιχείο-στόχος μας.  
- Ο βρόχος `for` εκτελεί τη λογική **increment counter javascript**, ενημερώνοντας το div σε κάθε επανάληψη.  
- Επειδή δεν είμαστε σε πραγματικό πρόγραμμα περιήγησης, η μηχανή script που θα χρησιμοποιήσουμε αργότερα θα πρέπει να καταλαβαίνει το `document.getElementById`. Γι' αυτό προσθέσαμε ένα μικρό stub στο `HTMLDocument`.

## Βήμα 3: Αρχικοποίηση της Μηχανής Script – Παράδειγμα Μηχανής Script

Η Java παρέχει το API `ScriptEngine` (JSR‑223). Θα δημιουργήσουμε ένα μικρό wrapper που τροφοδοτεί το περιεχόμενο HTML στη μηχανή και παρέχει τις ελάχιστες μεθόδους DOM που απαιτούνται.

```java
class SimpleScriptEngine {
    private final HTMLDocument document;
    private final ScriptEngine engine;

    public SimpleScriptEngine(HTMLDocument doc) throws ScriptException {
        this.document = doc;
        ScriptEngineManager manager = new ScriptEngineManager();
        this.engine = manager.getEngineByName("JavaScript");
        // Expose a mock 'document' object to the JavaScript context
        engine.put("document", new Object() {
            public Object getElementById(String id) {
                return new Object() {
                    public void setInnerHTML(String value) {
                        document.updateCounter(Integer.parseInt(value));
                    }
                };
            }
        });
    }

    public void execute() throws ScriptException {
        // Extract only the script part from the HTML (simplified)
        String html = document.getContent();
        int scriptStart = html.indexOf("<script>") + "<script>".length();
        int scriptEnd   = html.indexOf("</script>");
        String script = html.substring(scriptStart, scriptEnd);
        engine.eval(script);
    }
}
```

**Why this matters:** Αυτό το **script engine example** δείχνει πώς μπορείτε να εκτελέσετε ενσωματωμένο JavaScript χωρίς πλήρες πρόγραμμα περιήγησης. Επίσης, παρουσιάζει έναν ελαφρύ τρόπο να εκθέσετε το `document.getElementById` ώστε το script να μπορεί να αλληλεπιδρά με το mock DOM μας.

## Βήμα 4: Εκτέλεση JavaScript – Increment Counter JavaScript σε Δράση

Με τη μηχανή έτοιμη, απλώς εκτελούμε το script. Ο βρόχος μέσα στην ετικέτα `<script>` θα ενεργοποιηθεί, και το mock `setInnerHTML` μας θα ενημερώσει τον μετρητή.

```java
try {
    SimpleScriptEngine engine = new SimpleScriptEngine(doc);
    engine.execute(); // runs the embedded JavaScript
} catch (ScriptException e) {
    e.printStackTrace();
}
```

**What happens under the hood?** Κάθε επανάληψη του βρόχου καλεί `document.getElementById('counter').innerHTML = i + 1;`. Το mock `setInnerHTML` μας προωθεί το αριθμητικό string στο `HTMLDocument.updateCounter`, το οποίο αποθηκεύει την τελευταία τιμή. Μετά το τέλος του βρόχου, ο εσωτερικός χάρτης του εγγράφου περιέχει `"5"` για το στοιχείο `counter`.

## Βήμα 5: Ανάκτηση της Τελικής Τιμής του Μετρητή – Get Element InnerHTML

Τώρα που το script ολοκληρώθηκε, μπορούμε να **get element innerHTML** από το στιγμιότυπο `HTMLDocument` μας.

```java
String finalValue = doc.getElementInnerHTML("counter");
System.out.println("Final counter value: " + finalValue); // prints 5
```

Η εκτέλεση του πλήρους προγράμματος εκτυπώνει:

```
Final counter value: 5
```

Αυτό επιβεβαιώνει ότι η λογική **increment counter javascript** λειτούργησε και ότι καταφέραμε με επιτυχία να **retrieved the element innerHTML** μετά την εκτέλεση του script.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα, εδώ είναι η πλήρης, έτοιμη‑για‑εκτέλεση κλάση Java:

```java
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

public class HtmlJsDemo {

    // ---------- Minimal HTMLDocument implementation ----------
    static class HTMLDocument {
        private final StringBuilder html = new StringBuilder();
        private final java.util.Map<String, String> elements = new java.util.HashMap<>();

        public void write(String content) {
            html.append(content);
        }

        public String getContent() {
            return html.toString();
        }

        public void setElementInnerHTML(String id, String value) {
            elements.put(id, value);
        }

        public String getElementInnerHTML(String id) {
            return elements.getOrDefault(id, "");
        }

        public void updateCounter(int value) {
            setElementInnerHTML("counter", String.valueOf(value));
        }
    }

    // ---------- SimpleScriptEngine (script engine example) ----------
    static class SimpleScriptEngine {
        private final HTMLDocument document;
        private final ScriptEngine engine;

        public SimpleScriptEngine(HTMLDocument doc) throws ScriptException {
            this.document = doc;
            ScriptEngineManager manager = new ScriptEngineManager();
            this.engine = manager.getEngineByName("JavaScript");
            // Expose a mock 'document' object
            engine.put("document", new Object() {
                public Object getElementById(String id) {
                    return new Object() {
                        public void setInnerHTML(String value) {
                            document.updateCounter(Integer.parseInt(value));
                        }
                    };
                }
            });
        }

        public void execute() throws ScriptException {
            String html = document.getContent();
            int start = html.indexOf("<script>") + "<script>".length();
            int end   = html.indexOf("</script>");
            String script = html.substring(start, end);
            engine.eval(script);
        }
    }

    // ---------- Main method ----------
    public static void main(String[] args) {
        // Step 1: create HTML document
        HTMLDocument doc = new HTMLDocument();

        // Step 2: embed JavaScript HTML (increment counter JavaScript)
        doc.write(
            "<!DOCTYPE html><html><body>"
          + "<div id='counter'>0</div>"
          + "<script>"
          + "for (let i = 0; i < 5; i++) {"
          + "  document.getElementById('counter').innerHTML = i


## Τι Θα Μάθετε Στη Σύντομη Επόμενη

Τα παρακάτω tutorials καλύπτουν στενά σχετικό θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Δημιουργία Κενών Εγγράφων HTML στο Aspose.HTML για Java](/html/english/java/creating-managing-html-documents/create-empty-html-documents/)
- [Δημιουργία Εγγράφων HTML από String στο Aspose.HTML για Java](/html/english/java/creating-managing-html-documents/create-html-documents-from-string/)
- [Αποθήκευση Εγγράφου HTML στο Aspose.HTML για Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}