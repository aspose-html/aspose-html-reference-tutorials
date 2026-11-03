---
category: general
date: 2026-08-12
description: Μάθετε τη δεσμεύση δεδομένων πίνακα HTML σε λίγα λεπτά. Αυτός ο οδηγός
  δείχνει πώς να συγχωνεύσετε δεδομένα, να επαναλάβετε μια συλλογή και να εμφανίσετε
  το πρώτο όνομα σε έναν δυναμικό πίνακα HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- html table data binding
- how to merge data
- loop through collection
- show first name
- dynamic html table
language: el
lastmod: 2026-08-12
og_description: Η δέσμευση δεδομένων σε πίνακα HTML σας επιτρέπει να συγχωνεύετε δεδομένα
  και να επαναλαμβάνετε τη συλλογή για να εμφανίζετε το όνομα και άλλα πεδία. Ακολουθήστε
  αυτόν τον πλήρη οδηγό για να δημιουργήσετε έναν δυναμικό πίνακα HTML.
og_image_alt: Screenshot of a dynamic HTML table created with html table data binding
og_title: Δεσμεύση δεδομένων πίνακα HTML – δημιουργήστε έναν δυναμικό πίνακα HTML
  βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Learn html table data binding in minutes. This guide shows how to merge
    data, loop through collection, and show first name in a dynamic HTML table.
  headline: html table data binding tutorial – create a dynamic HTML table
  type: TechArticle
- description: Learn html table data binding in minutes. This guide shows how to merge
    data, loop through collection, and show first name in a dynamic HTML table.
  name: html table data binding tutorial – create a dynamic HTML table
  steps:
  - name: Sample JSON payload
    text: '```json { "Persons": { "Person": [ { "FirstName": "Alice", "LastName":
      "Smith", "Address": { "Street": "Maple Ave", "Number": "12", "City": "Springfield"
      } }, { "FirstName": "Bob", "LastName": "Johnson", "Address": { "Street": "Oak
      Street", "Number": "45B", "City": "Rivertown" } } ] } } ```'
  - name: Empty collections
    text: 'If the `Person` array is empty, the table will render only the header row.
      To display a friendly message, add a conditional block after the header:'
  - name: Escaping special characters
    text: When names or addresses contain characters like `<` or `&`, most templating
      engines escape them automatically. If your engine does not, wrap the values
      with an escape helper, e.g., `{{escape FirstName}}`.
  - name: Custom styling
    text: 'You can add CSS classes to the table for better visual presentation without
      affecting the data binding logic:'
  type: HowTo
- questions:
  - answer: Yes. Libraries like Handlebars.js or Mustache.js run in the browser and
      respect the same `{{#foreach}}` syntax. Load the library, compile the template,
      and pass the JSON object to render the table.
    question: Can I use this approach with plain JavaScript instead of a server‑side
      engine?
  - answer: Fetch the data with `fetch()` or `axios`, then call the template’s render
      function inside the promise’s `.then()` handler. The table updates once the
      data arrives.
    question: What if my data source is an API that returns data asynchronously?
  - answer: 'Pagination is a separate concern. Render only the slice of the collection
      you want to show, then re‑render the table when the user navigates to another
      page. ## Conclusion You now have a complete guide to **html table data binding**
      that shows **how to merge data**, **loop through collection**, and '
    question: Does this method support pagination?
  type: FAQPage
tags:
- HTML
- data-binding
- templating
title: Μάθημα σύνδεσης δεδομένων πίνακα HTML – δημιουργία δυναμικού πίνακα HTML
url: /el/java/creating-managing-html-documents/html-table-data-binding-tutorial-create-a-dynamic-html-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# html table data binding – πλήρης οδηγός προγραμματισμού

Αν χρειάζεστε **html table data binding** για να μετατρέψετε μια λίστα JSON σε έναν ζωντανό πίνακα HTML, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε. Θα μάθετε να συγχωνεύετε δεδομένα, να επαναλαμβάνετε μια συλλογή και **show first name** μαζί με άλλα πεδία χωρίς να γράφετε επαναλαμβανόμενο markup.

Οι δυναμικοί πίνακες είναι συνηθισμένοι σε πίνακες ελέγχου, admin panels και εργαλεία αναφοράς. Στο τέλος αυτού του tutorial μπορείτε να δημιουργήσετε έναν **dynamic html table** από οποιαδήποτε συλλογή αντικειμένων, χρησιμοποιώντας μόνο μια απλή σύνταξη templating.

## Prerequisites

- Βασικές γνώσεις HTML.
- Μηχανή templating που υποστηρίζει βρόχους `{{#foreach}}` (π.χ., Handlebars, Mustache ή μια προσαρμοσμένη server‑side μηχανή).
- Ένα JSON payload που περιέχει έναν πίνακα `Persons.Person` με `FirstName`, `LastName` και ένα αντικείμενο `Address`.

## Overview of the solution

Θα:

1. **Create a table** που θα λαμβάνει συγχωνευμένα δεδομένα.
2. **Define the header row** μία φορά.
3. **Loop through the collection** και αποδώστε μια γραμμή για κάθε άτομο.
4. **Show first name**, το επώνυμο και τα πεδία διεύθυνσης μέσα στον ίδιο πίνακα.

Το τελικό markup είναι ένας πλήρως λειτουργικός **dynamic html table** που ενημερώνεται αυτόματα όταν αλλάζουν τα υποκείμενα δεδομένα.

![html table data binding example](/images/html-table-data-binding.png "html table data binding example")

## Step 1: Ρυθμίστε το σκελετό του πίνακα HTML (html table data binding)

Το εξωτερικό στοιχείο `<table>` λαμβάνει τα συγχωνευμένα δεδομένα μέσω του χαρακτηριστικού `data_merge`. Το χαρακτηριστικό λέει στη μηχανή templating να επαναλάβει τις γραμμές μέσα στον πίνακα για κάθε στοιχείο της συλλογής.

```html
<table border="1" data_merge="{{#foreach Persons.Person}}">
    <!-- Header row and data rows will be inserted here -->
</table>
```

*Why this matters*: Με την προσθήκη του χαρακτηριστικού `data_merge` στο στοιχείο `<table>`, αποφεύγετε την αντιγραφή του markup `<tr>` για κάθε άτομο. Η μηχανή συγχωνεύει τα δεδομένα αυτόματα, που αποτελεί τον πυρήνα του **html table data binding**.

## Step 2: Προσθέστε μια στατική γραμμή κεφαλίδας (dynamic html table)

Οι κεφαλίδες είναι στατικές—εμφανίζονται μία φορά ανεξάρτητα από το πόσες εγγραφές υπάρχουν. Τοποθετήστε τις απευθείας μέσα στον πίνακα πριν ο βρόχος αποδώσει οποιεσδήποτε γραμμές.

```html
<tr>
    <th>Person</th>
    <th>Address</th>
</tr>
```

Η γραμμή κεφαλίδας ορίζει τους τίτλους των στηλών για τον **dynamic html table**. Κρατώντας την εκτός του βρόχου εξασφαλίζετε ότι δεν επαναλαμβάνεται για κάθε εγγραφή.

## Step 3: Αποδώστε μια γραμμή για κάθε άτομο (loop through collection)

Μέσα στο ίδιο στοιχείο `<table>`, προσθέστε μια γραμμή που χρησιμοποιεί τα placeholders του templating. Η μηχανή θα επαναλάβει αυτό το `<tr>` για κάθε καταχώρηση στο `Persons.Person`.

```html
<tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
</tr>
```

*Key points*:

- `{{FirstName}}` και `{{LastName}}` εξάγουν τις τιμές **show first name** και επώνυμου από το τρέχον στοιχείο.
- `{{Address.Street}}`, `{{Address.Number}}` και `{{Address.City}}` δείχνουν πώς να προσπελάσετε ένθετα αντικείμενα.
- Επειδή η γραμμή βρίσκεται μέσα στο μπλοκ `{{#foreach}}` που ορίζεται στο `<table>`, η μηχανή templating **how to merge data** αυτόματα.

## Full working example

Ακολουθεί το πλήρες απόσπασμα HTML που μπορείτε να επικολλήσετε σε οποιαδήποτε σελίδα υποστηρίζει την ίδια σύνταξη templating.

```html
<table border="1" data_merge="{{#foreach Persons.Person}}">
    <!-- Header row – appears once -->
    <tr>
        <th>Person</th>
        <th>Address</th>
    </tr>

    <!-- Data row – repeated for each person -->
    <tr>
        <td>{{FirstName}} {{LastName}}</td>
        <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
    </tr>
</table>
```

### Παράδειγμα JSON payload

```json
{
  "Persons": {
    "Person": [
      {
        "FirstName": "Alice",
        "LastName": "Smith",
        "Address": {
          "Street": "Maple Ave",
          "Number": "12",
          "City": "Springfield"
        }
      },
      {
        "FirstName": "Bob",
        "LastName": "Johnson",
        "Address": {
          "Street": "Oak Street",
          "Number": "45B",
          "City": "Rivertown"
        }
      }
    ]
  }
}
```

Όταν η μηχανή template επεξεργάζεται το HTML με το παραπάνω JSON, το παραγόμενο αποτέλεσμα φαίνεται ως εξής:

| Person          | Address                         |
|-----------------|---------------------------------|
| Alice Smith     | Maple Ave 12, Springfield       |
| Bob Johnson     | Oak Street 45B, Rivertown       |

*Why it works*: Η μηχανή διαβάζει `data_merge="{{#foreach Persons.Person}}"`, επαναλαμβάνει κάθε αντικείμενο στον πίνακα `Person` και αντικαθιστά τα placeholders με τις αντίστοιχες τιμές. Αυτό είναι η ουσία του **html table data binding** σε συνδυασμό με **how to merge data**.

## Step 4: Διαχείριση ειδικών περιπτώσεων (advanced html table data binding)

### Κενές συλλογές

Αν ο πίνακας `Person` είναι κενός, ο πίνακας θα αποδώσει μόνο τη γραμμή κεφαλίδας. Για να εμφανίσετε ένα φιλικό μήνυμα, προσθέστε ένα conditional block μετά την κεφαλίδα:

```html
{{#if Persons.Person.length}}
    <!-- rows are generated automatically -->
{{else}}
    <tr>
        <td colspan="2">No records found.</td>
    </tr>
{{/if}}
```

### Απόδραση ειδικών χαρακτήρων

Όταν ονόματα ή διευθύνσεις περιέχουν χαρακτήρες όπως `<` ή `&`, οι περισσότερες μηχανές templating τα αποδυναμώνουν αυτόματα. Αν η μηχανή σας δεν το κάνει, τυλίξτε τις τιμές με έναν βοηθό escape, π.χ., `{{escape FirstName}}`.

### Προσαρμοσμένο στυλ

Μπορείτε να προσθέσετε κλάσεις CSS στον πίνακα για καλύτερη οπτική παρουσίαση χωρίς να επηρεάσετε τη λογική του data binding:

```html
<table class="responsive-table" border="1" data_merge="{{#foreach Persons.Person}}">
    ...
</table>
```

## Pro tip: Επαναχρησιμοποίηση του ίδιου πίνακα για πολλαπλές συλλογές

Αν χρειάζεται να εμφανίσετε τόσο `Employees` όσο και `Customers` σε ξεχωριστούς πίνακες στην ίδια σελίδα, δώστε σε κάθε πίνακα το δικό του χαρακτηριστικό `data_merge`:

```html
<table data_merge="{{#foreach Employees.Employee}}">
    <!-- employee rows -->
</table>

<table data_merge="{{#foreach Customers.Customer}}">
    <!-- customer rows -->
</table>
```

Αυτό δείχνει την ευελιξία του **html table data binding** για οποιαδήποτε συλλογή.

## Συχνές ερωτήσεις

**Q: Μπορώ να χρησιμοποιήσω αυτήν την προσέγγιση με καθαρό JavaScript αντί για μια server‑side μηχανή;**  
A: Ναι. Βιβλιοθήκες όπως Handlebars.js ή Mustache.js εκτελούνται στον περιηγητή και σέβονται την ίδια σύνταξη `{{#foreach}}`. Φορτώστε τη βιβλιοθήκη, συντάξτε το template και περάστε το αντικείμενο JSON για να αποδώσετε τον πίνακα.

**Q: Τι γίνεται αν η πηγή δεδομένων μου είναι ένα API που επιστρέφει δεδομένα ασύγχρονα;**  
A: Φέρετε τα δεδομένα με `fetch()` ή `axios`, μετά καλέστε τη συνάρτηση render του template μέσα στον χειριστή `.then()` της υπόσχεσης. Ο πίνακας ενημερώνεται μόλις φτάσουν τα δεδομένα.

**Q: Υποστηρίζει αυτή η μέθοδος σελιδοποίηση;**  
A: Η σελιδοποίηση είναι ξεχωριστό ζήτημα. Αποδώστε μόνο το τμήμα της συλλογής που θέλετε να δείξετε, μετά ξανααποδώστε τον πίνακα όταν ο χρήστης μεταβεί σε άλλη σελίδα.

## Συμπέρασμα

Τώρα έχετε έναν πλήρη οδηγό για το **html table data binding** που δείχνει **how to merge data**, **loop through collection**, και **show first name** μαζί με άλλα πεδία σε έναν **dynamic html table**. Προσθέτοντας το χαρακτηριστικό `data_merge` στο στοιχείο `<table>` και χρησιμοποιώντας απλά placeholders, αφαιρείτε το επαναλαμβανόμενο markup και διατηρείτε το UI σας συγχρονισμένο με τα υποκείμενα δεδομένα.

Στη συνέχεια, εξετάστε:

- **Dynamic html table** styling με CSS Grid ή Flexbox.
- Σελιδοποίηση και ταξινόμηση στην πλευρά του client χρησιμοποιώντας βιβλιοθήκες όπως DataTables.
- Ενημερώσεις σε πραγματικό χρόνο με WebSockets ή Server‑Sent Events.

Μη διστάσετε να προσαρμόσετε το μοτίβο σε άλλες δομές δεδομένων, να πειραματιστείτε με επιπλέον στήλες ή να ενσωματώσετε τον πίνακα σε μια μεγαλύτερη εφαρμογή μονής σελίδας. Καλή κωδικοποίηση!

## Τι θα πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Συγχώνευση HTML με Json σε .NET με Aspose.HTML](/html/english/net/html-document-manipulation/merge-html-with-json/)
- [Συγχώνευση HTML με XML σε .NET με Aspose.HTML](/html/english/net/html-document-manipulation/merge-html-with-xml/)
- [Πώς να επεξεργαστείτε το δέντρο εγγράφου HTML στο Aspose.HTML για Java](/html/english/java/editing-html-documents/edit-html-document-tree/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}