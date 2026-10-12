---
category: general
date: 2026-10-12
description: डेटा से टेबल बनाना और Handlebars का उपयोग करके JSON से टेबल को भरना सीखें।
  डायनेमिक HTML टेबल में पंक्तियों को दोहराने के लिए चरण‑दर‑चरण गाइड।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate table from data
- populate table from json
- repeat table rows
- dynamic html table
- dynamic table rows
language: hi
lastmod: 2026-10-12
og_description: डेटा से टेबल बनाएं और Handlebars का उपयोग करके JSON से टेबल को भरें।
  दोहराए जाने वाले टेबल पंक्तियों के साथ डायनेमिक HTML टेबल बनाने के लिए इस ट्यूटोरियल
  का पालन करें।
og_image_alt: Screenshot showing generated table from data in a web page
og_title: हैंडलबार्स के साथ डेटा से तालिका बनाएं – पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-12'
  description: Learn how to generate table from data and populate table from JSON
    using Handlebars. Step‑by‑step guide for repeat table rows in dynamic HTML tables.
  headline: How to generate table from data with HTML and Handlebars
  type: TechArticle
- description: Learn how to generate table from data and populate table from JSON
    using Handlebars. Step‑by‑step guide for repeat table rows in dynamic HTML tables.
  name: How to generate table from data with HTML and Handlebars
  steps:
  - name: 1. Empty data sets
    text: 'If the JSON array is empty, Handlebars will still render the header row
      but no data rows. To display a friendly message, wrap the table in a conditional
      block:'
  - name: 2. Nested loops (e.g., multiple addresses per person)
    text: 'When a person can have several addresses, you can nest another `{{#foreach}}`
      inside the row:'
  - name: 3. Using a real API
    text: 'Replace the static `<script id="people-data">` with a fetch call:'
  - name: 4. Accessibility considerations
    text: '* Add `scope="col"` to `<th>` elements. * Use `<caption>` to describe the
      table purpose. * Ensure sufficient color contrast if you apply custom CSS.'
  type: HowTo
tags:
- HTML
- Handlebars
- JSON
- templating
title: HTML और Handlebars के साथ डेटा से तालिका कैसे बनाएं
url: /hi/java/creating-managing-html-documents/how-to-generate-table-from-data-with-html-and-handlebars/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# डेटा से HTML और Handlebars के साथ टेबल कैसे जनरेट करें

यदि आपको वेब पेज में **डेटा से टेबल जनरेट** करनी है, तो यह ट्यूटोरियल आपको ठीक-ठीक दिखाता है। एक सरल Handlebars लूप का उपयोग करके आप **JSON से टेबल भर** सकते हैं, **टेबल की पंक्तियों को दोहराएँ**, और एक पूरी **डायनामिक HTML टेबल** प्राप्त कर सकते हैं जो स्रोत बदलने पर अपडेट होती रहती है।

अगले कुछ मिनटों में आप एक पूर्ण, चलाने योग्य उदाहरण देखेंगे, समझेंगे कि प्रत्येक भाग क्यों महत्वपूर्ण है, और सीखेंगे कि इस पैटर्न को अधिक जटिल परिस्थितियों जैसे कि शर्तीय कॉलम या नेस्टेड ऑब्जेक्ट्स के लिए कैसे अनुकूलित किया जाए।

## आप क्या बनाएँगे

* एक JSON पेलोड पढ़ता है जिसमें व्यक्तियों की सूची होती है।
* प्रत्येक व्यक्ति के लिए एक टेबल पंक्ति दोहराता है (`repeat table rows`)।
* प्रत्येक व्यक्ति का पहला नाम, अंतिम नाम, और पता उपयुक्त सेल में डालता है।
* कोई सर्वर‑साइड रेंडरिंग नहीं – पूरी प्रक्रिया ब्राउज़र में होती है।

**आवश्यकताएँ**

* HTML और JavaScript का बुनियादी ज्ञान।
* एक आधुनिक ब्राउज़र (Chrome, Edge, Firefox, या Safari)।
* Handlebars.js – हम इसे CDN से लोड करेंगे, इसलिए कोई बिल्ड टूल्स आवश्यक नहीं हैं।

---

## चरण 1: JSON डेटा स्रोत तैयार करें

पहला कदम एक JavaScript ऑब्जेक्ट को परिभाषित करना है जो API से मिलने वाले JSON की नकल करता है। Handlebars साधारण ऑब्जेक्ट्स के साथ काम करता है, इसलिए आप डेटा को सीधे एक `<script>` टैग में एम्बेड कर सकते हैं प्रदर्शन के उद्देश्य से।

```html
<script id="people-data" type="application/json">
{
  "Persons": {
    "Person": [
      {
        "FirstName": "Alice",
        "LastName": "Anderson",
        "Address": {
          "Street": "Maple",
          "Number": "123",
          "City": "Springfield"
        }
      },
      {
        "FirstName": "Bob",
        "LastName": "Baker",
        "Address": {
          "Street": "Oak",
          "Number": "456",
          "City": "Rivertown"
        }
      }
    ]
  }
}
</script>
```

**यह क्यों महत्वपूर्ण है** – डेटा को एक अलग `<script>` एलिमेंट में रखकर आप बाद में इसे वास्तविक AJAX कॉल से आसानी से बदल सकते हैं। संरचना (`Persons.Person`) Handlebars `{{#foreach Persons.Person}}` ब्लॉक में उपयोग किए गए पाथ से मेल खाती है, जो **JSON से टेबल भर**ने के लिए आवश्यक है।

---

## चरण 2: Handlebars टेम्पलेट लिखें जो पंक्तियों को दोहराता है

अगला, एक `<script type="text/x-handlebars-template">` ब्लॉक बनाएँ जिसमें टेबल मार्कअप हो। Handlebars प्लेसहोल्डर्स को वास्तविक मानों से बदल देगा और प्रत्येक व्यक्ति के लिए `<tr>` को दोहराएगा।

```html
<script id="table-template" type="text/x-handlebars-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <!-- Header row describing the columns -->
  <tr>
    <th>Person</th>
    <th>Address</th>
  </tr>
  <!-- Data row – this block is repeated for each Person -->
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
</table>
</script>
```

**मुख्य भागों की व्याख्या**

* `{{#foreach Persons.Person}}` Handlebars को बताता है कि `Persons.Person` एरे के प्रत्येक एंट्री के लिए **टेबल पंक्तियों को दोहराएँ**।
* `{{FirstName}} {{LastName}}` और `{{Address.*}}` अभिव्यक्तियाँ वर्तमान एरे तत्व से मान निकालती हैं।
* पूरी टेबल को `data_merge` एट्रिब्यूट में लपेटना वैकल्पिक है; यह डाउनस्ट्रीम प्रोसेसिंग या CSS सेलेक्टर्स के लिए उपयोगी हो सकता है।

---

## चरण 3: Handlebars लोड करें और टेम्पलेट को कंपाइल करें

हम Handlebars को CDN से लाएँगे, JSON को पार्स करेंगे, टेम्पलेट को कंपाइल करेंगे, और अंतिम HTML को पेज में इन्जेक्ट करेंगे।

```html
<script src="https://cdn.jsdelivr.net/npm/handlebars@4.7.7/dist/handlebars.min.js"></script>
<script>
  // Parse the JSON stored in the <script id="people-data">
  const rawData = document.getElementById('people-data').textContent;
  const context = JSON.parse(rawData);

  // Grab the template markup and compile it
  const source = document.getElementById('table-template').innerHTML;
  const template = Handlebars.compile(source);

  // Generate the final HTML by applying the context
  const html = template(context);

  // Insert the generated table into the DOM
  document.getElementById('output').innerHTML = html;
</script>
```

**रनटाइम पर कंपाइल क्यों करें?** – टेम्पलेट को एक बार कंपाइल करके पुनः उपयोग करने से पेज तेज़ रहता है, विशेषकर जब डेटा बार‑बार बदलता है। यह पैटर्न कई बार **JSON से टेबल भर**ने को पेज रीलोड किए बिना आसान बनाता है।

---

## चरण 4: जनरेटेड टेबल के लिए कंटेनर आरक्षित करें

एक प्लेसहोल्डर `<div>` जोड़ें जहाँ डायनामिक टेबल दिखाई देगा। इससे मार्कअप साफ़ रहता है और स्थैतिक लेआउट व जनरेटेड कंटेंट के बीच की ज़िम्मेदारियों को अलग किया जाता है।

```html
<div id="output"></div>
```

जब चरण 3 की स्क्रिप्ट चलती है, तो `<div id="output">` में एक पूरी तरह से बनी हुई `<table>` एलिमेंट होगी, जो स्टाइलिंग या आगे की हेरफेर के लिए तैयार होगी।

---

## चरण 5: आउटपुट सत्यापित करें और टेबल को स्टाइल करें (वैकल्पिक)

ब्राउज़र में पेज खोलें और आपको नीचे दिखाए गए जैसा टेबल दिखना चाहिए:

![डेटा से जनरेटेड टेबल का स्क्रीनशॉट](image.png "डेटा से जनरेटेड टेबल का स्क्रीनशॉट")

```html
<table border="1" data_merge="true">
  <tr>
    <th>Person</th>
    <th>Address</th>
  </tr>
  <tr>
    <td>Alice Anderson</td>
    <td>Maple 123, Springfield</td>
  </tr>
  <tr>
    <td>Bob Baker</td>
    <td>Oak 456, Rivertown</td>
  </tr>
</table>
```

**वैकल्पिक स्टाइलिंग** – यदि आप साफ़ लुक चाहते हैं, तो कुछ CSS नियम जोड़ें:

```html
<style>
  table { border-collapse: collapse; width: 100%; }
  th, td { padding: 8px; text-align: left; }
  th { background-color: #f2f2f2; }
</style>
```

---

## किनारे के मामलों और सामान्य विविधताओं को संभालना

### 1. खाली डेटा सेट

यदि JSON एरे खाली है, तो Handlebars अभी भी हेडर रो रेंडर करेगा लेकिन डेटा रो नहीं। एक मित्रवत संदेश दिखाने के लिए, टेबल को एक कंडीशनल ब्लॉक में लपेटें:

```handlebars
{{#if Persons.Person.length}}
  {{!-- existing table markup --}}
{{else}}
  <p>No persons found.</p>
{{/if}}
```

### 2. नेस्टेड लूप्स (उदा., प्रत्येक व्यक्ति के कई पते)

जब किसी व्यक्ति के पास कई पते हो सकते हैं, तो आप पंक्ति के अंदर एक और `{{#foreach}}` नेस्ट कर सकते हैं:

```handlebars
{{#foreach Persons.Person}}
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>
      {{#foreach Address}}
        {{Street}} {{Number}}, {{City}}<br>
      {{/foreach}}
    </td>
  </tr>
{{/foreach}}
```

### 3. वास्तविक API का उपयोग

स्थिर `<script id="people-data">` को एक fetch कॉल से बदलें:

```javascript
fetch('/api/persons')
  .then(r => r.json())
  .then(context => {
    const html = template(context);
    document.getElementById('output').innerHTML = html;
  });
```

यह लाइव डेटा खींचते हुए वही **डायनामिक टेबल रो** तकनीक दर्शाता है।

### 4. एक्सेसिबिलिटी विचार

* `<th>` एलिमेंट्स में `scope="col"` जोड़ें।
* टेबल के उद्देश्य को वर्णित करने के लिए `<caption>` का उपयोग करें।
* यदि आप कस्टम CSS लागू करते हैं तो पर्याप्त रंग कंट्रास्ट सुनिश्चित करें।

---

## पूर्ण, चलाने योग्य उदाहरण

निम्नलिखित ब्लॉक को एक `index.html` फ़ाइल में कॉपी करें और ब्राउज़र में खोलें। पेज **डेटा से टेबल जनरेट** करेगा, **JSON से टेबल भर**ेगा, और पंक्तियों को स्वचालित रूप से दोहराएगा।

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Dynamic table from JSON</title>
  <style>
    table { border-collapse: collapse; width: 100%; }
    th, td { padding: 8px; text-align: left; border: 1px solid #ddd; }
    th { background-color: #f2f2f2; }
  </style>
</head>
<body>

<!-- Step 1: JSON data source -->
<script id="people-data" type="application/json">
{
  "Persons": {
    "Person": [
      {
        "FirstName": "Alice",
        "LastName": "Anderson",
        "Address": {
          "Street": "Maple",
          "Number": "123",
          "City": "Springfield"
        }
      },
      {
        "FirstName": "Bob",
        "LastName": "Baker",
        "Address": {
          "Street": "Oak",
          "Number": "456",
          "City": "Rivertown"
        }
      }
    ]
  }
}
</script>

<!-- Step 2: Handlebars template -->
<script id="table-template" type="text/x-handlebars-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <tr>
    <th scope="col">Person</th>
    <th scope="col">Address</th>
  </tr>
  {{#foreach Persons.Person}}
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
  {{/foreach}}
</table>
</script>

<!-- Step 4: Container for the generated table -->
<div id="output"></div>

<!-- Step 3: Load Handlebars, compile, and render -->
<script src="https://cdn.jsdelivr.net/npm/handlebars@4.7.7/dist/handlebars.min.js"></script>
<script>
  const raw = document.getElementById('people-data').textContent;
  const context = JSON.parse(raw);
  const source = document.getElementById('table-template').innerHTML;
  const template = Handlebars.compile(source);
  document.getElementById('output').innerHTML = template(context);
</script>

</body>
</html>
```

**अपेक्षित परिणाम**

एक दो‑पंक्तियों वाली टेबल (हेडर सहित) जिसमें “Alice Anderson” और “Bob Baker” उनके संबंधित पते के साथ दिखाए गए हैं। पेज ऑफ़लाइन काम करता है, यह सिद्ध करता है कि आप **डेटा से टेबल जनरेट** कर सकते हैं बिना किसी सर्वर कंपोनेंट के।

---

## निष्कर्ष

अब आप जानते हैं कि Handlebars टेम्पलेट का उपयोग करके **डेटा से टेबल जनरेट** कैसे करें, **JSON से टेबल भर**ें, और **टेबल पंक्तियों को दोहराएँ** जिससे एक **डायनामिक HTML टेबल** बनती है। यह पैटर्न बड़े डेटा सेट, नेस्टेड स्ट्रक्चर, और लाइव API कॉल्स तक स्केल करता है, जिससे आपको किसी भी क्लाइंट‑साइड रिपोर्टिंग या एडमिन UI के लिए एक मजबूत आधार मिलता है।

**आगे के कदम**

* तारीख या नंबर फॉर्मेट करने के लिए Handlebars हेल्पर्स का अन्वेषण करें।
* रिस्पॉन्सिव टेबल लेआउट्स के लिए इस दृष्टिकोण को CSS Grid या Flexbox के साथ मिलाएँ।
* बहुत बड़े डेटा सेट को संभालने के लिए पेजिनेशन या सॉर्टिंग लाइब्रेरीज़ को इंटीग्रेट करें।

विभिन्न JSON संरचनाओं के साथ प्रयोग करने, शर्तीय कॉलम जोड़ने, या Handlebars को किसी अन्य टेम्पलेटिंग इंजन से बदलने में संकोच न करें—आपके नए कौशल आपको लचीले, डेटा‑ड्रिवन इंटरफ़ेस जल्दी और भरोसेमंद तरीके से बनाने में सक्षम करेंगे।

## अगला आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑बद्ध व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच को एक्सप्लोर करने में मदद करती हैं।

- [जावा के साथ HTML डॉक्यूमेंट बनाएं – JSON फ़ेच करें और कंटेंट जनरेट करें](/html/english/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/)
- [Aspose.HTML for Java में डेटा हैंडलिंग और स्ट्रीम मैनेजमेंट](/html/english/java/data-handling-stream-management/)
- [जावा में HTML लोड करने का तरीका – स्टेप‑बाय‑स्टेप गाइड](/html/english/java/creating-managing-html-documents/how-to-load-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}