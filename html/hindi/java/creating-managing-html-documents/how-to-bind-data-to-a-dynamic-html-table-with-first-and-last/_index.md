---
category: general
date: 2026-09-07
description: डायनेमिक HTML टेबल में डेटा को बाइंड कैसे करें – टेबल की पंक्तियों को
  जेनरेट करना और प्रथम एवं अंतिम नाम फ़ील्ड को कुशलतापूर्वक भरना सीखें.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to bind data
- dynamic html table
- first and last name
- how to generate table
- populate table rows
language: hi
lastmod: 2026-09-07
og_description: डायनामिक HTML टेबल में डेटा को बाइंड करने का तरीका। यह ट्यूटोरियल
  दिखाता है कि टेबल रो कैसे जनरेट करें, पहला और अंतिम नाम कैसे प्रदर्शित करें, और
  जावास्क्रिप्ट के साथ टेबल रो को कैसे भरें।
og_image_alt: Screenshot of a dynamic HTML table populated with first and last names
  after binding data
og_title: डायनेमिक HTML टेबल में डेटा बाइंड करने का चरण-दर-चरण मार्गदर्शक
schemas:
- author: Aspose
  dateModified: '2026-09-07'
  description: how to bind data in a dynamic HTML table – learn how to generate table
    rows and populate first and last name fields efficiently
  headline: How to bind data to a dynamic HTML table with first and last name columns
  type: TechArticle
tags:
- data binding
- html table
- templating
title: पहले और अंतिम नाम वाले कॉलम के साथ एक गतिशील HTML तालिका में डेटा बाइंड कैसे
  करें
url: /hi/java/creating-managing-html-documents/how-to-bind-data-to-a-dynamic-html-table-with-first-and-last/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# डेटा को डायनामिक HTML टेबल में बाइंड कैसे करें जिसमें प्रथम और अंतिम नाम के कॉलम हों

यदि आपको प्रत्येक रिकॉर्ड के साथ बढ़ने वाली टेबल में **डेटा को बाइंड करने** की आवश्यकता है, तो यह गाइड एक पूर्ण समाधान दिखाता है। आप देखेंगे कि कैसे एक डायनामिक HTML टेबल जेनरेट करें, टेबल की पंक्तियों को भरें, और प्रत्येक व्यक्ति का प्रथम और अंतिम नाम बिना दोहरावदार मार्कअप लिखे प्रदर्शित करें।

उदाहरण एक हल्के टेम्प्लेटिंग सिंटैक्स का उपयोग करता है जो किसी भी आधुनिक ब्राउज़र में काम करता है, लेकिन अवधारणाएँ Handlebars, Mustache, या सर्वर‑साइड इंजनों पर भी लागू होती हैं। ट्यूटोरियल के अंत तक आप कोड को अपने प्रोजेक्ट में कॉपी करके तुरंत डेटा बाइंड करना शुरू कर सकते हैं।

## इस ट्यूटोरियल में क्या कवर किया गया है

* कई व्यक्तियों को सम्मिलित करने वाले डेटा स्रोत को कैसे संरचित करें  
* प्रत्येक प्रविष्टि के लिए दोहराने योग्य टेबल टेम्प्लेट कैसे बनाएं  
* डेटा को बाइंड करें और अंतिम HTML मार्कअप जेनरेट करें  
* टेबल पंक्तियों को भरते समय सामान्य समस्याएँ और उन्हें कैसे टालें  

कोई बाहरी लाइब्रेरी आवश्यक नहीं है, हालांकि वही पैटर्न लोकप्रिय टेम्प्लेटिंग फ्रेमवर्क के साथ भी काम करता है। एकमात्र पूर्वापेक्षा बुनियादी HTML और JavaScript ज्ञान है।

## पूर्वापेक्षाएँ

* एक आधुनिक ब्राउज़र (Chrome, Edge, Firefox, या Safari)  
* HTML/JavaScript फ़ाइलों के लिए एक एडिटर  
* वैकल्पिक: एक JSON फ़ाइल या JavaScript ऑब्जेक्ट जो व्यक्तियों के संग्रह को दर्शाता है  

## चरण 1: डेटा स्रोत को परिभाषित करें

पहले, एक JavaScript ऑब्जेक्ट बनाएं जो टेम्प्लेट में उपयोग की गई संरचना को प्रतिबिंबित करता है। प्रत्येक व्यक्ति का प्रथम नाम, अंतिम नाम, और एक पता ऑब्जेक्ट होता है।

```html
<script>
  // Data source – an array of person objects
  const data = {
    Persons: {
      Person: [
        {
          FirstName: "Alice",
          LastName: "Johnson",
          Address: {
            Street: "Maple",
            Number: "12A",
            City: "Springfield"
          }
        },
        {
          FirstName: "Bob",
          LastName: "Smith",
          Address: {
            Street: "Oak",
            Number: "34B",
            City: "Riverdale"
          }
        }
        // Add more person objects as needed
      ]
    }
  };
</script>
```

**यह क्यों महत्वपूर्ण है:** ऑब्जेक्ट पदानुक्रम (`Persons.Person`) टेम्प्लेट में `{{#foreach Persons.Person}}` लूप से मेल खाता है, जिससे इंजन स्वचालित रूप से प्रत्येक प्रविष्टि पर इटररेट कर सकता है।

## चरण 2: दोहराव ब्लॉक के साथ टेबल टेम्प्लेट लिखें

नीचे दिया गया टेम्प्लेट एक सरल Mustache‑स्टाइल सिंटैक्स (`{{#foreach}}`) का उपयोग करता है ताकि प्रत्येक व्यक्ति के लिए `<tr>` दोहराया जा सके। टेम्प्लेट को `<script type="text/template">` टैग के भीतर रखें ताकि ब्राउज़र इसे तब तक अनदेखा करे जब तक आप इसे प्रोसेस न करें।

```html
<script type="text/template" id="table-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <!-- Table header -->
  <tr>
    <th>Person</th><th>Address</th>
  </tr>
  <!-- Row populated with each person's data -->
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
</table>
</script>
```

**यह क्यों महत्वपूर्ण है:** `{{#foreach Persons.Person}}` निर्देश इंजन को बताता है कि प्रत्येक व्यक्ति ऑब्जेक्ट के लिए ओपनिंग और क्लोज़िंग टैग के बीच की सभी सामग्री को दोहराए। पंक्ति के भीतर आप किसी भी प्रॉपर्टी (`{{FirstName}}`, `{{LastName}}`, आदि) को संदर्भित करके **टेबल पंक्तियों को भरें** गतिशील रूप से।

## चरण 3: एक छोटा रेंडरिंग फ़ंक्शन लागू करें

क्योंकि ट्यूटोरियल को स्वयं‑समाहित होना चाहिए, हम एक न्यूनतम रेंडरर लिखेंगे जो Mustache‑स्टाइल प्लेसहोल्डर्स को वास्तविक मानों से बदलता है। फ़ंक्शन डेटा ऑब्जेक्ट को ट्रैवर्स करता है, दोहराव ब्लॉक का विस्तार करता है, और अंतिम HTML को पेज में इंजेक्ट करता है।

```html
<script>
  /**
   * Renders a template that contains a single {{#foreach}} block.
   * This implementation is intentionally simple and works for the
   * specific structure used in this tutorial.
   *
   * @param {string} tmpl   The raw template string.
   * @param {object} ctx    The data context (e.g., the `data` object).
   * @returns {string}      The rendered HTML.
   */
  function renderTemplate(tmpl, ctx) {
    // Extract the foreach expression and the block to repeat
    const foreachRegex = /{{#foreach\s+([^}]+)}}([\s\S]*?){{\/foreach}}/;
    const match = tmpl.match(foreachRegex);
    if (!match) return tmpl; // No foreach found

    const path = match[1].trim(); // e.g., "Persons.Person"
    const block = match[2];       // HTML that repeats

    // Resolve the array from the context (supports dot notation)
    const items = path.split('.').reduce((obj, key) => obj && obj[key], ctx);
    if (!Array.isArray(items)) return tmpl;

    // Render each item
    const renderedBlocks = items.map(item => {
      // Replace each {{property}} with the corresponding value
      return block.replace(/{{([^}]+)}}/g, (_, prop) => {
        const value = prop.trim().split('.').reduce((obj, key) => obj && obj[key], item);
        return value !== undefined ? value : '';
      });
    });

    // Replace the whole foreach section with the concatenated rows
    return tmpl.replace(foreachRegex, renderedBlocks.join(''));
  }

  // When the DOM is ready, render the table
  document.addEventListener('DOMContentLoaded', () => {
    const tmpl = document.getElementById('table-template').innerHTML;
    const html = renderTemplate(tmpl, data);
    document.getElementById('output').innerHTML = html;
  });
</script>
```

**यह क्यों महत्वपूर्ण है:** रेंडरर दर्शाता है कि **टेबल कैसे जेनरेट करें** मार्कअप को प्रोग्रामेटिक रूप से बिना पूरी लाइब्रेरी को शामिल किए। यह टेम्प्लेट से अंतिम HTML में परिवर्तन को स्पष्ट करता है, जिससे आप बाद में कोड को अन्य टेम्प्लेटिंग इंजनों में अनुकूलित कर सकते हैं।

## चरण 4: एक प्लेसहोल्डर जोड़ें जहाँ जेनरेटेड टेबल दिखाई देगा

एक खाली `<div>` बनाएं जिसे स्क्रिप्ट रेंडरिंग के बाद भर देगा।

```html
<div id="output"></div>
```

जब पेज लोड होता है, स्क्रिप्ट इस `<div>` की सामग्री को पूरी तरह से भरे हुए टेबल से बदल देती है।

## चरण 5: परिणाम सत्यापित करें

ब्राउज़र में HTML फ़ाइल खोलें। आपको एक टेबल दिखनी चाहिए जो प्रत्येक व्यक्ति का पूरा नाम और पता सूचीबद्ध करती है:

| व्यक्ति | पता |
|--------|------|
| Alice Johnson | Maple 12A, Springfield |
| Bob Smith | Oak 34B, Riverdale |

यदि आप `data.Persons.Person` एरे में अधिक ऑब्जेक्ट जोड़ते हैं, तो टेबल स्वचालित रूप से बढ़ेगी—जिससे **टेबल पंक्तियों को भरें** की आवश्यकता पूरी होती है।

## प्रो टिप: खाली संग्रह को संभालना

जब डेटा एरे खाली हो, तो रेंडरर वर्तमान में एक खाली टेबल हेडर आउटपुट करता है। उपयोगकर्ता अनुभव को स्पष्ट बनाने के लिए एक गार्ड जोड़ें:

```javascript
if (items.length === 0) {
  return '<p>No records found.</p>';
}
```

यह छोटा परिवर्तन खाली टेबल के दिखने से रोकता है और उपयोगकर्ताओं को तुरंत फीडबैक देता है।

## सामान्य विविधताएँ और किनारे के मामले

| स्थिति | समायोजन |
|--------|----------|
| सर्वर‑साइड इंजन (जैसे Handlebars) का उपयोग करना | कस्टम `renderTemplate` को `Handlebars.compile` से बदलें और वही डेटा ऑब्जेक्ट पास करें। |
| पंक्तियों को वर्णक्रमानुसार क्रमबद्ध करने की आवश्यकता | `renderTemplate` कॉल करने से पहले `data.Persons.Person` को सॉर्ट करें। |
| फ़ोन नंबर के लिए एक कॉलम जोड़ना | `<tr>` को `<td>{{Phone}}</td>` से विस्तारित करें और प्रत्येक व्यक्ति ऑब्जेक्ट में `Phone` शामिल करें। |
| बड़े डेटा सेट (सैकड़ों पंक्तियाँ) | पंक्तियों को भागों में रेंडर करें या UI को रिस्पॉन्सिव रखने के लिए वर्चुअल स्क्रॉलिंग का उपयोग करें। |

## पूर्ण कार्यशील उदाहरण

नीचे वह संपूर्ण HTML फ़ाइल है जिसे आप `index.html` में कॉपी‑पेस्ट कर सकते हैं। इसमें ऊपर चर्चा किए गए सभी हिस्से शामिल हैं।

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How to bind data to a dynamic HTML table</title>
  <style>
    table { border-collapse: collapse; width: 100%; }
    th, td { padding: 8px; text-align: left; }
    th { background-color: #f2f2f2; }
  </style>
</head>
<body>

<h1>Dynamic HTML table bound to JavaScript data</h1>

<!-- Step 2: Table template -->
<script type="text/template" id="table-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <tr>
    <th>Person</th><th>Address</th>
  </tr>
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
</table>
</script>

<!-- Step 1: Data source -->
<script>
  const data = {
    Persons: {
      Person: [
        {
          FirstName: "Alice",
          LastName: "Johnson",
          Address: { Street: "Maple", Number: "12A", City: "Springfield" }
        },
        {
          FirstName: "Bob",
          LastName: "Smith",
          Address: { Street: "Oak", Number: "34B", City: "Riverdale" }
        }
        // Add more entries as needed
      ]
    }
  };
</script>

<!-- Step 4: Output container -->
<div id="output"></div>

<!-- Step 3: Rendering logic -->
<script>
  function renderTemplate(tmpl, ctx) {
    const foreachRegex = /{{#foreach\s+([^}]+)}}([\s\S]*?){{\/foreach}}/;
    const match = tmpl.match(foreachRegex);
    if (!match) return tmpl;
    const path = match[1].trim();
    const block = match[2];
    const items = path.split('.').reduce((obj, key) => obj && obj[key], ctx);
    if (!Array.isArray(items) || items.length === 0) {
      return '<p>No records found.</p>';
    }
    const renderedBlocks = items.map(item => {
      return block.replace(/{{([^}]+)}}/g, (_, prop) => {
        const value = prop.trim().split('.').reduce((obj, key) => obj && obj[key], item);
        return value !== undefined ? value : '';
      });
    });
    return tmpl.replace(foreachRegex, renderedBlocks.join(''));
  }

  document.addEventListener('DOMContentLoaded', () => {
    const tmpl = document.getElementById('table-template').innerHTML;
    const html = renderTemplate(tmpl, data);
    document.getElementById('output').innerHTML = html;
  });
</script>

</body>
</html>
```

**अपेक्षित आउटपुट**

पेज दो पंक्तियों वाला टेबल रेंडर करता है, प्रत्येक में व्यक्ति का पूरा नाम और स्वरूपित पता दिखता है। `Person` एरे में अधिक ऑब्जेक्ट जोड़ने से नई पंक्तियाँ स्वतः जुड़ जाती हैं—जिससे डेटा से **टेबल कैसे जेनरेट करें** तत्व प्रदर्शित होते हैं।

## निष्कर्ष

आप अब जानते हैं **डेटा को बाइंड कैसे करें** एक **डायनामिक HTML टेबल** में, प्रत्येक रिकॉर्ड के लिए पंक्तियों को जेनरेट करें, और प्रथम तथा अंतिम नाम के मानों को पते के साथ प्रदर्शित करें।

## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स निकट संबंधी विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर करने में मदद करेंगे।

- [कैसे जोड़ें CSS – Aspose.HTML for Java में HTML दस्तावेज़ों में इनलाइन CSS](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [कैसे संपादित करें HTML दस्तावेज़ ट्री को Aspose.HTML for Java में](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [कैसे सक्षम करें JavaScript को Aspose HTML में – HTML लोड करें और टेक्स्ट प्राप्त करें](/html/english/java/advanced-usage/how-to-enable-javascript-in-aspose-html-load-html-get-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}