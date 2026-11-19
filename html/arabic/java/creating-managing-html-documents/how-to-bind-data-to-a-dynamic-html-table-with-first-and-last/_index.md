---
category: general
date: 2026-09-07
description: كيفية ربط البيانات في جدول HTML ديناميكي – تعلم كيفية إنشاء صفوف الجدول
  وتعبئة حقول الاسم الأول والاسم الأخير بكفاءة
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to bind data
- dynamic html table
- first and last name
- how to generate table
- populate table rows
language: ar
lastmod: 2026-09-07
og_description: كيفية ربط البيانات في جدول HTML ديناميكي. يوضح هذا الدرس كيفية إنشاء
  صفوف الجدول، وعرض الاسم الأول والاسم الأخير، وتعبئة صفوف الجدول باستخدام JavaScript.
og_image_alt: Screenshot of a dynamic HTML table populated with first and last names
  after binding data
og_title: كيفية ربط البيانات بجدول HTML ديناميكي – دليل خطوة بخطوة
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
title: كيفية ربط البيانات بجدول HTML ديناميكي يحتوي على أعمدة الاسم الأول والاسم الأخير
url: /ar/java/creating-managing-html-documents/how-to-bind-data-to-a-dynamic-html-table-with-first-and-last/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية ربط البيانات بجدول HTML ديناميكي يحتوي على عمودي الاسم الأول والاسم الأخير

إذا كنت بحاجة إلى **how to bind data** داخل جدول يتوسع مع كل سجل، يوضح هذا الدليل حلاً كاملاً. ستتعرف على كيفية إنشاء جدول HTML ديناميكي، تعبئة صفوف الجدول، وعرض الاسم الأول والاسم الأخير لكل شخص دون كتابة علامات مكررة.

المثال يستخدم صيغة قوالب خفيفة تعمل في أي متصفح حديث، لكن المفاهيم تنطبق على Handlebars أو Mustache أو محركات الخادم. بنهاية الدرس يمكنك نسخ الشيفرة إلى مشروعك والبدء في ربط البيانات فورًا.

## ما يغطيه هذا الدرس

* كيفية هيكلة مصدر بيانات يحتوي على عدة أشخاص  
* كيفية إنشاء قالب جدول قابل لإعادة الاستخدام يتكرر لكل إدخال  
* كيفية ربط البيانات وتوليد العلامات النهائية للـ HTML  
* الأخطاء الشائعة عند تعبئة صفوف الجدول وكيفية تجنبها  

لا توجد مكتبات خارجية مطلوبة، رغم أن النمط نفسه يعمل مع أطر القوالب الشهيرة. المتطلب الوحيد هو معرفة أساسية بـ HTML وJavaScript.

## المتطلبات المسبقة

* متصفح حديث (Chrome أو Edge أو Firefox أو Safari)  
* محرر لملفات HTML/JavaScript  
* اختياري: ملف JSON أو كائن JavaScript يمثل مجموعة الأشخاص  

## الخطوة 1: تعريف مصدر البيانات

أولاً، أنشئ كائن JavaScript يعكس البنية المستخدمة في القالب. كل شخص يمتلك اسمًا أولًا، اسمًا آخر، وكائن عنوان.

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

**لماذا هذا مهم:** تسلسل الكائن (`Persons.Person`) يتطابق مع حلقة `{{#foreach Persons.Person}}` في القالب، مما يسمح للمحرك بالتكرار عبر كل إدخال تلقائيًا.

## الخطوة 2: كتابة قالب الجدول مع كتلة التكرار

القالب أدناه يستخدم صيغة بسيطة على نمط Mustache (`{{#foreach}}`) لتكرار `<tr>` لكل شخص. ضع القالب داخل وسم `<script type="text/template">` حتى يتجاهله المتصفح حتى تقوم بمعالجته.

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

**لماذا هذا مهم:** توجيه `{{#foreach Persons.Person}}` يخبر المحرك بتكرار كل ما بين وسم الفتح والإغلاق لكل كائن شخص. داخل الصف يمكنك الإشارة إلى أي خاصية (`{{FirstName}}`، `{{LastName}}`، إلخ) لـ **populate table rows** بشكل ديناميكي.

## الخطوة 3: تنفيذ دالة تصيير صغيرة

نظرًا لأن الدرس يجب أن يكون ذاتيًا، سنكتب مصممًا بسيطًا يستبدل العناصر النائبة على نمط Mustache بالقيم الفعلية. تقوم الدالة بزيارة كائن البيانات، توسيع كتلة التكرار، وإدخال الـ HTML النهائي في الصفحة.

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

**لماذا هذا مهم:** يوضح المصمم **how to generate table** برمجيًا دون الحاجة إلى مكتبة كاملة. كما يوضح التحول من القالب إلى الـ HTML النهائي، مما يساعدك على تعديل الشيفرة لتتناسب مع محركات قوالب أخرى لاحقًا.

## الخطوة 4: إضافة عنصر نائب حيث سيظهر الجدول المُولد

أنشئ `<div>` فارغًا سيملأه السكربت بعد عملية التصيير.

```html
<div id="output"></div>
```

عند تحميل الصفحة، يستبدل السكربت محتويات هذا `<div>` بالجدول المكتمل.

## الخطوة 5: التحقق من النتيجة

افتح ملف HTML في المتصفح. يجب أن ترى جدولًا يسرد الاسم الكامل لكل شخص وعنوانه:

| الشخص | العنوان |
|-------|----------|
| Alice Johnson   | Maple 12A, Springfield          |
| Bob Smith       | Oak 34B, Riverdale              |

إذا أضفت المزيد من الكائنات إلى مصفوفة `data.Persons.Person`، سينمو الجدول تلقائيًا—محققًا متطلب **populate table rows**.

## نصيحة احترافية: التعامل مع المجموعات الفارغة

عندما تكون مصفوفة البيانات فارغة، ينتج المصمم حاليًا رأس جدول فارغ. لتوفير تجربة مستخدم أوضح، أضف شرطًا وقائيًا:

```javascript
if (items.length === 0) {
  return '<p>No records found.</p>';
}
```

هذا التغيير الصغير يمنع ظهور جدول فارغ ويعطي المستخدمين ملاحظات فورية.

## الاختلافات الشائعة وحالات الحافة

| الحالة                               | التعديل                                                                 |
|--------------------------------------|--------------------------------------------------------------------------|
| استخدام محرك من جانب الخادم (مثل Handlebars) | استبدل الدالة المخصصة `renderTemplate` بـ `Handlebars.compile` ومرّر نفس كائن البيانات. |
| الحاجة إلى فرز الصفوف أبجديًا       | قم بفرز `data.Persons.Person` قبل استدعاء `renderTemplate`.               |
| إضافة عمود لرقم الهاتف               | قم بتمديد `<tr>` بإضافة `<td>{{Phone}}</td>` وتضمين `Phone` في كل كائن شخص. |
| مجموعات بيانات كبيرة (مئات الصفوف)   | قم بتجسيد الصفوف على دفعات أو استخدم التمرير الافتراضي للحفاظ على استجابة واجهة المستخدم. |

## مثال كامل يعمل

فيما يلي ملف HTML كامل يمكنك نسخه ولصقه في `index.html`. يحتوي على جميع الأجزاء التي نوقشت أعلاه.

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

**الناتج المتوقع**

الصفحة تعرض جدولًا بصفين، كل منهما يُظهر الاسم الكامل والعنوان المنسق لشخص. إضافة المزيد من الكائنات إلى مصفوفة `Person` يضيف صفوفًا جديدة تلقائيًا—مظهرًا **how to generate table** من البيانات.

## الخلاصة

أنت الآن تعرف **how to bind data** إلى **جدول HTML ديناميكي**، توليد صفوف لكل سجل، وعرض قيم الاسم الأول والاسم الأخير جنبًا إلى جنب مع العنوان.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية إضافة CSS – CSS مضمّن إلى مستندات HTML في Aspose.HTML للـ Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [كيفية تحرير شجرة مستند HTML في Aspose.HTML للـ Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [كيفية تمكين JavaScript في Aspose HTML – تحميل HTML والحصول على النص](/html/english/java/advanced-usage/how-to-enable-javascript-in-aspose-html-load-html-get-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}