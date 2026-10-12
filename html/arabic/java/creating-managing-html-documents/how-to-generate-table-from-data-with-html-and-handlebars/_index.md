---
category: general
date: 2026-10-12
description: تعلم كيفية إنشاء جدول من البيانات وتعبئته من JSON باستخدام Handlebars.
  دليل خطوة بخطوة لتكرار صفوف الجدول في جداول HTML الديناميكية.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate table from data
- populate table from json
- repeat table rows
- dynamic html table
- dynamic table rows
language: ar
lastmod: 2026-10-12
og_description: إنشاء جدول من البيانات وتعبئة الجدول من JSON باستخدام Handlebars.
  اتبع هذا الدرس لإنشاء جداول HTML ديناميكية مع تكرار صفوف الجدول.
og_image_alt: Screenshot showing generated table from data in a web page
og_title: إنشاء جدول من البيانات باستخدام Handlebars – دليل كامل
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
title: كيفية إنشاء جدول من البيانات باستخدام HTML و Handlebars
url: /ar/java/creating-managing-html-documents/how-to-generate-table-from-data-with-html-and-handlebars/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء جدول من البيانات باستخدام HTML و Handlebars

إذا كنت بحاجة إلى **إنشاء جدول من البيانات** في صفحة ويب، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك. باستخدام حلقة Handlebars بسيطة يمكنك **ملء الجدول من JSON**، وإنشاء **تكرار صفوف الجدول**، والحصول على **جدول HTML ديناميكي** بالكامل يتحدث كلما تغير المصدر.

في الدقائق القليلة القادمة ستشاهد مثالًا كاملاً قابلاً للتنفيذ، وتفهم لماذا كل جزء مهم، وتتعلم كيفية تكييف النمط لسيناريوهات أكثر تعقيدًا مثل الأعمدة الشرطية أو الكائنات المتداخلة.

## ما ستبنيه

سننشئ جدول HTML يقوم بـ:

* قراءة حمولة JSON تحتوي على قائمة من الأشخاص.
* تكرار صف جدول لكل شخص (`repeat table rows`).
* إدراج الاسم الأول، الاسم الأخير، والعنوان لكل شخص في الخلايا المناسبة.
* العمل دون أي تصيير من جانب الخادم – العملية بالكامل تتم في المتصفح.

**المتطلبات المسبقة**

* معرفة أساسية بـ HTML و JavaScript.
* متصفح حديث (Chrome أو Edge أو Firefox أو Safari).
* Handlebars.js – سنحمّله من CDN، لذا لا تحتاج إلى أدوات بناء.

---

## الخطوة 1: إعداد مصدر بيانات JSON

الخطوة الأولى هي تعريف كائن JavaScript يحاكي الـ JSON الذي ستحصل عليه من API. Handlebars يعمل مع كائنات عادية، لذا يمكنك تضمين البيانات مباشرة داخل وسم `<script>` لأغراض العرض.

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

**لماذا هذا مهم** – بالحفاظ على البيانات في عنصر `<script>` منفصل يمكنك استبداله بسهولة باستدعاء AJAX حقيقي لاحقًا. البنية (`Persons.Person`) تتطابق مع المسار المستخدم في كتلة Handlebars `{{#foreach Persons.Person}}`، وهو أمر أساسي لـ **ملء الجدول من JSON**.

---

## الخطوة 2: كتابة قالب Handlebars الذي يكرر الصفوف

بعد ذلك، أنشئ كتلة `<script type="text/x-handlebars-template">` تحتوي على ترميز الجدول. Handlebars سيستبدل العناصر النائبة بالقيم الفعلية ويكرر `<tr>` لكل شخص.

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

**شرح الأجزاء الرئيسية**

* `{{#foreach Persons.Person}}` يخبر Handlebars **بتكرار صفوف الجدول** لكل عنصر في مصفوفة `Persons.Person`.
* تعبيرات `{{FirstName}} {{LastName}}` و `{{Address.*}}` تستخرج القيم من العنصر الحالي في المصفوفة.
* تغليف الجدول بالكامل بصفة `data_merge` اختياري؛ قد يكون مفيدًا للمعالجة اللاحقة أو لتحديد عناصر CSS.

---

## الخطوة 3: تحميل Handlebars وتجميع القالب

سنحمّل Handlebars من CDN، نُحلل الـ JSON، نجمع القالب، ونُدرج الـ HTML النهائي في الصفحة.

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

**لماذا نجمع القالب في وقت التشغيل؟** – تجميع القالب مرة واحدة وإعادة استخدامه يحافظ على سرعة الصفحة، خاصةً عندما تتغيّر البيانات بشكل متكرر. هذا النمط يجعل من السهل **ملء الجدول من JSON** عدة مرات دون إعادة تحميل الصفحة.

---

## الخطوة 4: حجز حاوية للجدول المُولد

أضف عنصر `<div>` كعنصر نائب حيث سيظهر الجدول الديناميكي. هذا يحافظ على نظافة الترميز ويفصل بين التخطيط الثابت والمحتوى المُولد.

```html
<div id="output"></div>
```

عند تشغيل السكربت من الخطوة 3، سيحتوي `<div id="output">` على عنصر `<table>` مكتمل، جاهز للتنسيق أو المعالجة الإضافية.

---

## الخطوة 5: التحقق من النتيجة وتنسيق الجدول (اختياري)

افتح الصفحة في متصفح وسترى جدولًا مشابهًا للذي أدناه:

![لقطة شاشة تُظهر الجدول المُولد من البيانات](image.png "لقطة شاشة تُظهر الجدول المُولد من البيانات")

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

**تنسيق اختياري** – إذا رغبت في مظهر أنظف، أضف بعض قواعد CSS:

```html
<style>
  table { border-collapse: collapse; width: 100%; }
  th, td { padding: 8px; text-align: left; }
  th { background-color: #f2f2f2; }
</style>
```

---

## معالجة الحالات الحدية والاختلافات الشائعة

### 1. مجموعات البيانات الفارغة

إذا كانت مصفوفة JSON فارغة، سيظل Handlebars يُظهر صف العنوان دون صفوف بيانات. لعرض رسالة ودية، غلف الجدول بكتلة شرطية:

```handlebars
{{#if Persons.Person.length}}
  {{!-- existing table markup --}}
{{else}}
  <p>No persons found.</p>
{{/if}}
```

### 2. الحلقات المتداخلة (مثال: عناوين متعددة لكل شخص)

عندما يمكن للشخص أن يمتلك عدة عناوين، يمكنك تضمين `{{#foreach}}` آخر داخل الصف:

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

### 3. استخدام API حقيقي

استبدل `<script id="people-data">` باستدعاء fetch:

```javascript
fetch('/api/persons')
  .then(r => r.json())
  .then(context => {
    const html = template(context);
    document.getElementById('output').innerHTML = html;
  });
```

هذا يُظهر نفس تقنية **صفوف الجدول الديناميكية** أثناء جلب البيانات الحية.

### 4. اعتبارات الوصول

* أضف `scope="col"` إلى عناصر `<th>`.
* استخدم `<caption>` لوصف هدف الجدول.
* تأكد من وجود تباين ألوان كافٍ إذا طبقت CSS مخصصًا.

---

## مثال كامل قابل للتنفيذ

انسخ الكتلة التالية إلى ملف `index.html` وافتحه في متصفح. ستقوم الصفحة **بإنشاء جدول من البيانات**، **بملء الجدول من JSON**، وتكرار الصفوف تلقائيًا.

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

**النتيجة المتوقعة**

جدول من صفين (بالإضافة إلى العنوان) يُظهر “Alice Anderson” و “Bob Baker” مع عناوينهما الخاصة. تعمل الصفحة دون اتصال، مما يثبت أنه يمكنك **إنشاء جدول من البيانات** دون أي مكوّن خادم.

---

## الخلاصة

أنت الآن تعرف كيف **تنشئ جدولًا من البيانات** باستخدام قالب Handlebars، **تملأ الجدول من JSON**، وتُنشئ **صفوف جدول متكررة** تُكوّن **جدول HTML ديناميكي**. النمط قابل للتوسيع لمجموعات بيانات أكبر، هياكل متداخلة، واستدعاءات API حية، مما يمنحك أساسًا قويًا لأي تقارير أو واجهات إدارية على جانب العميل.

**الخطوات التالية**

* استكشف مساعدي Handlebars لتنسيق التواريخ أو الأرقام.
* اجمع هذا النهج مع CSS Grid أو Flexbox لتصاميم جداول متجاوبة.
* دمج مكتبات التصفية أو الفرز للتعامل مع مجموعات بيانات ضخمة.

لا تتردد في تجربة أشكال JSON مختلفة، إضافة أعمدة شرطية، أو استبدال Handlebars بمحرك قوالب آخر—مهاراتك الجديدة ستمكنك من بناء واجهات مرنة مدفوعة بالبيانات بسرعة وموثوقية.

## ما يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء مستند HTML باستخدام Java – جلب JSON وإنشاء محتوى](/html/english/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/)
- [معالجة البيانات وإدارة التدفقات في Aspose.HTML للـ Java](/html/english/java/data-handling-stream-management/)
- [كيفية تحميل HTML في Java – دليل خطوة بخطوة](/html/english/java/creating-managing-html-documents/how-to-load-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}