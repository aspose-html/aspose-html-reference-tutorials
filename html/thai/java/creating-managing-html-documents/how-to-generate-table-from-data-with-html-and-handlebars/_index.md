---
category: general
date: 2026-10-12
description: เรียนรู้วิธีสร้างตารางจากข้อมูลและเติมข้อมูลตารางจาก JSON ด้วย Handlebars
  คู่มือแบบทีละขั้นตอนสำหรับการทำซ้ำแถวตารางในตาราง HTML แบบไดนามิก
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate table from data
- populate table from json
- repeat table rows
- dynamic html table
- dynamic table rows
language: th
lastmod: 2026-10-12
og_description: สร้างตารางจากข้อมูลและเติมข้อมูลตารางจาก JSON ด้วย Handlebars ทำตามบทเรียนนี้เพื่อสร้างตาราง
  HTML แบบไดนามิกที่มีแถวซ้ำ.
og_image_alt: Screenshot showing generated table from data in a web page
og_title: สร้างตารางจากข้อมูลด้วย Handlebars – คู่มือฉบับสมบูรณ์
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
title: วิธีสร้างตารางจากข้อมูลด้วย HTML และ Handlebars
url: /th/java/creating-managing-html-documents/how-to-generate-table-from-data-with-html-and-handlebars/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้างตารางจากข้อมูลด้วย HTML และ Handlebars

หากคุณต้องการ **สร้างตารางจากข้อมูล** ในหน้าเว็บ นี้เป็นบทแนะนำที่จะแสดงให้คุณเห็นอย่างชัดเจน ด้วยการใช้ลูปง่าย ๆ ของ Handlebars คุณสามารถ **เติมข้อมูลตารางจาก JSON**, สร้าง **แถวตารางซ้ำ** และได้ **ตาราง HTML แบบไดนามิก** ที่อัปเดตทุกครั้งที่แหล่งข้อมูลเปลี่ยนแปลง

ในไม่กี่นาทีต่อไป คุณจะได้เห็นตัวอย่างที่ทำงานได้เต็มรูปแบบ เข้าใจว่าทำไมแต่ละส่วนจึงสำคัญ และเรียนรู้วิธีปรับใช้รูปแบบนี้สำหรับสถานการณ์ที่ซับซ้อนมากขึ้น เช่น คอลัมน์ตามเงื่อนไขหรืออ็อบเจ็กต์ซ้อนกัน

## สิ่งที่คุณจะสร้าง

เราจะสร้างตาราง HTML ที่:

* อ่าน payload JSON ที่มีรายการของบุคคล
* ทำซ้ำแถวตารางสำหรับแต่ละบุคคล (`repeat table rows`)
* ใส่ชื่อจริง, นามสกุล และที่อยู่ของแต่ละบุคคลลงในเซลล์ที่เหมาะสม
* ทำงานโดยไม่ต้องใช้การเรนเดอร์ฝั่งเซิร์ฟเวอร์ – ทั้งหมดเกิดขึ้นในเบราว์เซอร์

**ข้อกำหนดเบื้องต้น**

* ความรู้พื้นฐานเกี่ยวกับ HTML และ JavaScript
* เบราว์เซอร์สมัยใหม่ (Chrome, Edge, Firefox หรือ Safari)
* Handlebars.js – เราจะโหลดจาก CDN ดังนั้นไม่ต้องใช้เครื่องมือสร้างใด ๆ

---

## ขั้นตอนที่ 1: เตรียมแหล่งข้อมูล JSON

ขั้นตอนแรกคือการกำหนดอ็อบเจ็กต์ JavaScript ที่จำลอง JSON ที่คุณจะได้รับจาก API Handlebars ทำงานกับอ็อบเจ็กต์ธรรมดา ดังนั้นคุณสามารถฝังข้อมูลไว้ในแท็ก `<script>` เพื่อการสาธิตได้โดยตรง

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

**ทำไมส่วนนี้สำคัญ** – การเก็บข้อมูลไว้ในองค์ประกอบ `<script>` แยกต่างหากทำให้คุณสามารถสลับเป็นการเรียก AJAX จริงได้ในภายหลัง โครงสร้าง (`Persons.Person`) ตรงกับเส้นทางที่ใช้ในบล็อก Handlebars `{{#foreach Persons.Person}}` ซึ่งจำเป็นสำหรับ **เติมข้อมูลตารางจาก JSON**

---

## ขั้นตอนที่ 2: เขียนเทมเพลต Handlebars ที่ทำซ้ำแถว

ต่อไป สร้างบล็อก `<script type="text/x-handlebars-template">` ที่บรรจุมาร์กอัปของตาราง Handlebars จะเปลี่ยนตำแหน่งตัวแปรเป็นค่าจริงและทำซ้ำ `<tr>` สำหรับแต่ละบุคคล

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

**คำอธิบายส่วนสำคัญ**

* `{{#foreach Persons.Person}}` บอก Handlebars ให้ **ทำซ้ำแถวตาราง** สำหรับทุกรายการในอาร์เรย์ `Persons.Person`
* นิพจน์ `{{FirstName}} {{LastName}}` และ `{{Address.*}}` ดึงค่าจากอิลิเมนต์ปัจจุบันของอาร์เรย์
* การห่อหุ้มตารางทั้งหมดด้วยแอตทริบิวต์ `data_merge` เป็นตัวเลือก; สามารถใช้สำหรับการประมวลผลต่อเนื่องหรือเลือกด้วย CSS

---

## ขั้นตอนที่ 3: โหลด Handlebars และคอมไพล์เทมเพลต

เราจะดึง Handlebars จาก CDN, แปลง JSON, คอมไพล์เทมเพลต, แล้วแทรก HTML สุดท้ายลงในหน้า

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

**ทำไมต้องคอมไพล์ในเวลาเรียกใช้?** – การคอมไพล์เทมเพลตครั้งเดียวแล้วนำกลับมาใช้ซ้ำทำให้หน้าโหลดเร็วขึ้น โดยเฉพาะเมื่อข้อมูลเปลี่ยนบ่อย รูปแบบนี้ยังทำให้การ **เติมข้อมูลตารางจาก JSON** หลายครั้งเป็นเรื่องง่ายโดยไม่ต้องรีโหลดหน้า

---

## ขั้นตอนที่ 4: จองคอนเทนเนอร์สำหรับตารางที่สร้างขึ้น

เพิ่ม `<div>` ตัวแทนที่ซึ่งตารางไดนามิกจะปรากฏ นี่ช่วยให้มาร์กอัปสะอาดและแยกความรับผิดชอบระหว่างเลย์เอาต์คงที่และเนื้อหาที่สร้างขึ้น

```html
<div id="output"></div>
```

เมื่อสคริปต์จากขั้นตอน 3 ทำงาน `<div id="output">` จะมีองค์ประกอบ `<table>` ที่สมบูรณ์พร้อมสำหรับการสไตล์หรือการจัดการต่อไป

---

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์และสไตล์ตาราง (ไม่บังคับ)

เปิดหน้าในเบราว์เซอร์และคุณควรเห็นตารางคล้ายกับด้านล่าง:

![ภาพหน้าจอแสดงตารางที่สร้างจากข้อมูล](image.png "ภาพหน้าจอแสดงตารางที่สร้างจากข้อมูล")

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

**สไตล์เสริม** – หากต้องการรูปลักษณ์ที่เรียบง่าย สามารถเพิ่มกฎ CSS เล็กน้อยได้ดังนี้:

```html
<style>
  table { border-collapse: collapse; width: 100%; }
  th, td { padding: 8px; text-align: left; }
  th { background-color: #f2f2f2; }
</style>
```

---

## การจัดการกรณีขอบและรูปแบบที่พบบ่อย

### 1. ชุดข้อมูลว่าง

หากอาร์เรย์ JSON ว่าง Handlebars จะยังคงเรนเดอร์แถวหัวตารางแต่ไม่มีแถวข้อมูล เพื่อแสดงข้อความเป็นมิตร ให้ห่อหุ้มตารางด้วยบล็อกเงื่อนไข:

```handlebars
{{#if Persons.Person.length}}
  {{!-- existing table markup --}}
{{else}}
  <p>No persons found.</p>
{{/if}}
```

### 2. ลูปซ้อนกัน (เช่น ที่อยู่หลายรายการต่อบุคคล)

เมื่อบุคคลมีหลายที่อยู่ คุณสามารถซ้อน `{{#foreach}}` อีกอันหนึ่งภายในแถวได้:

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

### 3. ใช้ API จริง

แทนที่ `<script id="people-data">` แบบคงที่ด้วยการเรียก fetch:

```javascript
fetch('/api/persons')
  .then(r => r.json())
  .then(context => {
    const html = template(context);
    document.getElementById('output').innerHTML = html;
  });
```

นี่แสดงเทคนิค **dynamic table rows** เดียวกันขณะดึงข้อมูลแบบเรียลไทม์

### 4. พิจารณาด้านการเข้าถึง

* เพิ่ม `scope="col"` ให้กับองค์ประกอบ `<th>`
* ใช้ `<caption>` เพื่ออธิบายวัตถุประสงค์ของตาราง
* ตรวจสอบให้แน่ใจว่าคอนทราสต์สีเพียงพอหากคุณเพิ่ม CSS กำหนดเอง

---

## ตัวอย่างเต็มที่ทำงานได้

คัดลอกบล็อกต่อไปนี้ลงในไฟล์ `index.html` แล้วเปิดในเบราว์เซอร์ หน้าเว็บจะ **สร้างตารางจากข้อมูล**, **เติมข้อมูลตารางจาก JSON**, และทำซ้ำแถวโดยอัตโนมัติ

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

**ผลลัพธ์ที่คาดหวัง**

ตารางสองแถว (บวกหัวตาราง) แสดง “Alice Anderson” และ “Bob Baker” พร้อมที่อยู่ของแต่ละคน หน้าเว็บทำงานแบบออฟไลน์ แสดงว่าคุณสามารถ **สร้างตารางจากข้อมูล** ได้โดยไม่ต้องมีส่วนเซิร์ฟเวอร์

---

## สรุป

คุณได้เรียนรู้วิธี **สร้างตารางจากข้อมูล** ด้วยเทมเพลต Handlebars, **เติมข้อมูลตารางจาก JSON**, และสร้าง **แถวตารางซ้ำ** ที่ทำให้เป็น **ตาราง HTML แบบไดนามิก** รูปแบบนี้สามารถขยายได้กับชุดข้อมูลขนาดใหญ่ โครงสร้างซ้อนกัน และการเรียก API แบบเรียลไทม์ ให้คุณมีพื้นฐานที่แข็งแกร่งสำหรับการทำรายงานหรือ UI ฝั่งคลไอเอนต์ใด ๆ

**ขั้นตอนต่อไป**

* สำรวจ Handlebars helpers สำหรับการจัดรูปแบบวันที่หรือจำนวน
* ผสานวิธีนี้กับ CSS Grid หรือ Flexbox เพื่อทำเลย์เอาต์ตารางแบบตอบสนอง
* ผสานการแบ่งหน้า หรือไลบรารีการจัดเรียงเพื่อจัดการชุดข้อมูลขนาดใหญ่มาก

อย่ากลัวที่จะทดลองกับโครงสร้าง JSON ต่าง ๆ, เพิ่มคอลัมน์ตามเงื่อนไข, หรือเปลี่ยน Handlebars เป็นเอนจินเทมเพลตอื่น — ทักษะใหม่ของคุณจะทำให้คุณสร้างอินเทอร์เฟซที่ขับเคลื่อนด้วยข้อมูลได้อย่างรวดเร็วและเชื่อถือได้


## สิ่งที่คุณควรเรียนต่อไป


บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโครงการของคุณเอง

- [Create HTML Document with Java – Fetch JSON and Generate Content](/html/english/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/)
- [Data Handling and Stream Management in Aspose.HTML for Java](/html/english/java/data-handling-stream-management/)
- [How to Load HTML in Java – Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/how-to-load-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}