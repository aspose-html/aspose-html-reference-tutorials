---
category: general
date: 2026-09-07
description: วิธีผูกข้อมูลในตาราง HTML แบบไดนามิก – เรียนรู้วิธีสร้างแถวตารางและเติมข้อมูลชื่อและนามสกุลอย่างมีประสิทธิภาพ
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to bind data
- dynamic html table
- first and last name
- how to generate table
- populate table rows
language: th
lastmod: 2026-09-07
og_description: วิธีผูกข้อมูลในตาราง HTML แบบไดนามิก บทเรียนนี้แสดงวิธีสร้างแถวตาราง
  แสดงชื่อและนามสกุล และเติมข้อมูลในแถวตารางด้วย JavaScript.
og_image_alt: Screenshot of a dynamic HTML table populated with first and last names
  after binding data
og_title: วิธีผูกข้อมูลกับตาราง HTML แบบไดนามิก – คู่มือขั้นตอนโดยละเอียด
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
title: วิธีผูกข้อมูลกับตาราง HTML แบบไดนามิกที่มีคอลัมน์ชื่อจริงและนามสกุล
url: /th/java/creating-managing-html-documents/how-to-bind-data-to-a-dynamic-html-table-with-first-and-last/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีผูกข้อมูลกับตาราง HTML แบบไดนามิกที่มีคอลัมน์ชื่อและนามสกุล

หากคุณต้องการ **how to bind data** ลงในตารางที่ขยายตัวตามแต่ละบันทึก คู่มือนี้จะแสดงวิธีแก้ไขแบบครบถ้วน คุณจะได้เห็นวิธีสร้างตาราง HTML แบบไดนามิก, เติมแถวในตาราง, และแสดงชื่อและนามสกุลของแต่ละบุคคลโดยไม่ต้องเขียนโค้ดซ้ำซ้อน

ตัวอย่างใช้ไวยากรณ์การเทมเพลตแบบเบาที่ทำงานได้ในเบราว์เซอร์สมัยใหม่ใด ๆ แต่แนวคิดสามารถนำไปใช้กับ Handlebars, Mustache หรือเอนจินฝั่งเซิร์ฟเวอร์ได้เช่นกัน เมื่อจบบทเรียนคุณสามารถคัดลอกโค้ดไปยังโปรเจกต์ของคุณและเริ่มผูกข้อมูลได้ทันที

## สิ่งที่บทเรียนนี้ครอบคลุม

* วิธีจัดโครงสร้างแหล่งข้อมูลที่มีหลายบุคคล  
* วิธีสร้างเทมเพลตตารางที่นำกลับมาใช้ใหม่ได้และทำซ้ำสำหรับแต่ละรายการ  
* วิธีผูกข้อมูลและสร้าง HTML markup สุดท้าย  
* ข้อผิดพลาดทั่วไปเมื่อเติมแถวในตารางและวิธีหลีกเลี่ยง  

ไม่จำเป็นต้องใช้ไลบรารีภายนอก แม้ว่าแพทเทิร์นเดียวกันจะทำงานกับเฟรมเวิร์กการเทมเพลตที่นิยมได้เช่นกัน เงื่อนไขเบื้องต้นเพียงแค่ความรู้พื้นฐานของ HTML และ JavaScript

## ข้อกำหนดเบื้องต้น

* เบราว์เซอร์สมัยใหม่ (Chrome, Edge, Firefox หรือ Safari)  
* โปรแกรมแก้ไขไฟล์ HTML/JavaScript  
* ตัวเลือก: ไฟล์ JSON หรืออ็อบเจ็กต์ JavaScript ที่แสดงคอลเลกชันของบุคคล  

## ขั้นตอนที่ 1: กำหนดแหล่งข้อมูล

แรกสุด สร้างอ็อบเจ็กต์ JavaScript ที่สะท้อนโครงสร้างที่ใช้ในเทมเพลต แต่ละบุคคลจะมีชื่อ, นามสกุล, และอ็อบเจ็กต์ address

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

**Why this matters:** โครงสร้างอ็อบเจ็กต์ (`Persons.Person`) ตรงกับลูป `{{#foreach Persons.Person}}` ในเทมเพลต ทำให้เอนจินสามารถวนซ้ำแต่ละรายการโดยอัตโนมัติ

## ขั้นตอนที่ 2: เขียนเทมเพลตตารางพร้อมบล็อกการทำซ้ำ

เทมเพลตด้านล่างใช้ไวยากรณ์แบบ Mustache‑style (`{{#foreach}}`) เพื่อทำซ้ำ `<tr>` สำหรับแต่ละบุคคล วางเทมเพลตภายในแท็ก `<script type="text/template">` เพื่อให้เบราว์เซอร์ละเลยจนกว่าคุณจะประมวลผลมัน

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

**Why this matters:** คำสั่ง `{{#foreach Persons.Person}}` บอกเอนจินให้ทำซ้ำทุกอย่างระหว่างแท็กเปิดและปิดสำหรับแต่ละอ็อบเจ็กต์บุคคล ภายในแถวคุณสามารถอ้างอิงคุณสมบัติใดก็ได้ (`{{FirstName}}`, `{{LastName}}`, เป็นต้น) เพื่อ **populate table rows** อย่างไดนามิก

## ขั้นตอนที่ 3: สร้างฟังก์ชันการเรนเดอร์ขนาดเล็ก

เนื่องจากบทเรียนต้องเป็นอิสระ เราจะเขียนเรนเดอร์เล็ก ๆ ที่แทนที่ตัวแปรแบบ Mustache‑style ด้วยค่าจริง ฟังก์ชันจะเดินผ่านอ็อบเจ็กต์ข้อมูล, ขยายบล็อกการทำซ้ำ, และแทรก HTML สุดท้ายลงในหน้า

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

**Why this matters:** เรนเดอร์แสดง **how to generate table** markup อย่างโปรแกรมเมติกโดยไม่ต้องดึงไลบรารีเต็มรูปแบบ นอกจากนี้ยังทำให้เห็นการแปลงจากเทมเพลตเป็น HTML สุดท้าย ซึ่งช่วยให้คุณปรับโค้ดไปใช้กับเอนจินเทมเพลตอื่น ๆ ในภายหลัง

## ขั้นตอนที่ 4: เพิ่มตัวแทนที่ตารางที่สร้างขึ้นจะปรากฏ

สร้าง `<div>` ว่างที่สคริปต์จะเติมหลังจากการเรนเดอร์

```html
<div id="output"></div>
```

เมื่อหน้าโหลด สคริปต์จะแทนที่เนื้อหาของ `<div>` นี้ด้วยตารางที่เต็มไปด้วยข้อมูล

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์

เปิดไฟล์ HTML ในเบราว์เซอร์ คุณควรเห็นตารางที่แสดงชื่อเต็มและที่อยู่ของแต่ละบุคคล:

| บุคคล          | ที่อยู่                         |
|-----------------|---------------------------------|
| Alice Johnson   | Maple 12A, Springfield          |
| Bob Smith       | Oak 34B, Riverdale              |

หากคุณเพิ่มอ็อบเจ็กต์ลงในอาร์เรย์ `data.Persons.Person` ตารางจะขยายโดยอัตโนมัติ—ตอบสนองความต้องการ **populate table rows**

## เคล็ดลับพิเศษ: การจัดการคอลเลกชันที่ว่างเปล่า

เมื่ออาร์เรย์ข้อมูลว่าง เรนเดอร์จะสร้างหัวตารางเปล่า เพื่อให้ประสบการณ์ผู้ใช้ชัดเจนขึ้น ให้เพิ่มการตรวจสอบ:

```javascript
if (items.length === 0) {
  return '<p>No records found.</p>';
}
```

การเปลี่ยนแปลงเล็ก ๆ นี้จะป้องกันไม่ให้ตารางเปล่าปรากฏและให้ผู้ใช้ได้รับฟีดแบ็กทันที

## ความแตกต่างทั่วไปและกรณีขอบ

| สถานการณ์                               | การปรับแต่ง                                                                 |
|----------------------------------------|----------------------------------------------------------------------------|
| ใช้เอนจินฝั่งเซิร์ฟเวอร์ (เช่น Handlebars) | แทนที่ `renderTemplate` แบบกำหนดเองด้วย `Handlebars.compile` และส่งอ็อบเจ็กต์ข้อมูลเดียวกัน |
| ต้องการจัดเรียงแถวตามลำดับตัวอักษร       | เรียงลำดับ `data.Persons.Person` ก่อนเรียก `renderTemplate`               |
| เพิ่มคอลัมน์สำหรับหมายเลขโทรศัพท์       | ขยาย `<tr>` ด้วย `<td>{{Phone}}</td>` และเพิ่ม `Phone` ในอ็อบเจ็กต์ของแต่ละบุคคล |
| ชุดข้อมูลขนาดใหญ่ (หลายร้อยแถว)     | เรนเดอร์แถวเป็นชิ้นส่วนหรือใช้ virtual scrolling เพื่อให้ UI ตอบสนองได้ดี |

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นไฟล์ HTML ฉบับสมบูรณ์ที่คุณสามารถคัดลอก‑วางลงใน `index.html` ได้ มีส่วนประกอบทั้งหมดที่กล่าวถึงข้างต้น

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

**ผลลัพธ์ที่คาดหวัง**

หน้าจะเรนเดอร์ตารางที่มีสองแถว แต่ละแถวแสดงชื่อเต็มและที่อยู่ที่จัดรูปแบบของบุคคล การเพิ่มอ็อบเจ็กต์ลงในอาร์เรย์ `Person` จะทำให้เพิ่มแถวใหม่โดยอัตโนมัติ—แสดงให้เห็น **how to generate table** จากข้อมูล

## สรุป

คุณตอนนี้รู้แล้วว่า **how to bind data** ไปยัง **dynamic HTML table**, สร้างแถวสำหรับแต่ละบันทึก, และแสดงค่าชื่อและนามสกุลพร้อมที่อยู่

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโปรเจกต์ของคุณ

- [วิธีเพิ่ม CSS – Inline CSS ไปยังเอกสาร HTML ใน Aspose.HTML สำหรับ Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [วิธีแก้ไขโครงสร้างเอกสาร HTML ใน Aspose.HTML สำหรับ Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [วิธีเปิดใช้งาน JavaScript ใน Aspose HTML – โหลด HTML & ดึงข้อความ](/html/english/java/advanced-usage/how-to-enable-javascript-in-aspose-html-load-html-get-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}