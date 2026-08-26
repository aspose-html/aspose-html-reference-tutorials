---
category: general
date: 2026-08-25
description: เรียนรู้วิธีสร้างเอกสาร HTML, เลือกองค์ประกอบ CSS, แก้ไขข้อความ HTML
  และบันทึกไฟล์ HTML ด้วยสคริปต์ Python ง่าย ๆ
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create html document
- select element css
- modify html text
- save html file
- how to edit html
language: th
lastmod: 2026-08-25
og_description: สร้างเอกสาร HTML, เลือก CSS ขององค์ประกอบ, แก้ไขข้อความ HTML และบันทึกไฟล์
  HTML ด้วยไม่กี่บรรทัดของ Python. ทำตามบทเรียนฉบับเต็มนี้.
og_image_alt: Screenshot of a Python script that creates and updates an HTML file
og_title: สร้างเอกสาร HTML และแก้ไขเนื้อหาด้วย Python – คู่มือขั้นตอนโดยละเอียด
schemas:
- author: Aspose
  dateModified: '2026-08-25'
  description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  headline: How to create html document and edit its content in Python
  type: TechArticle
- description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  name: How to create html document and edit its content in Python
  steps:
  - name: Full script for quick copy‑paste
    text: '```python # ------------------------------------------------- # File: edit_html.py
      # ------------------------------------------------- # Purpose: Demonstrate how
      to create html document, # select an element with CSS, modify its text, # and
      save the result to a file. # -------------------------------'
  - name: Selecting multiple elements
    text: If you need to **select element css** selectors that match several tags
      (e.g., `"div.note"`), use `doc.select("div.note")` which returns a list. Iterate
      over the list to apply changes to each element.
  - name: Preserving existing attributes
    text: 'When you replace the text, BeautifulSoup retains any attributes on the
      tag. For example:'
  - name: Handling missing elements gracefully
    text: In production scripts, you often encounter malformed HTML. Wrap the selection
      in a conditional or try‑except block, as shown in Step 4, to avoid crashes.
  - name: Writing to a specific directory
    text: 'Replace `output_path` with an absolute or relative path:'
  type: HowTo
tags:
- Python
- HTML manipulation
- CSS selectors
- File I/O
title: วิธีสร้างเอกสาร HTML และแก้ไขเนื้อหาใน Python
url: /th/python/general/how-to-create-html-document-and-edit-its-content-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้างเอกสาร html และแก้ไขเนื้อหาใน Python

หากคุณต้องการ **create html document** ตั้งแต่ต้นและเปลี่ยนแปลงองค์ประกอบของมันโดยโปรแกรมมิ่ง คู่มือนี้จะแสดงให้คุณเห็นอย่างชัดเจน คุณจะได้เห็นสคริปต์สั้น ๆ ที่สามารถรันได้ซึ่งสร้างไฟล์ เลือกย่อหน้าด้วย CSS selector ปรับข้อความ และเขียนผลลัพธ์กลับไปยังดิสก์

การทำงานกับ HTML ใน Python เป็นเรื่องทั่วไปเมื่อสร้างรายงาน, แม่แบบอีเมล, หรือเนื้อหาเว็บไซต์แบบสถิต  เมื่อจบบทเรียนนี้คุณจะสามารถ **select element css**, **modify html text**, และ **save html file** ได้โดยไม่ต้องออกจาก IDE ที่คุณคุ้นเคย

## ข้อกำหนดเบื้องต้น

* ติดตั้ง Python 3.9 หรือใหม่กว่า
* แพคเกจ `beautifulsoup4` และ `lxml` (ติดตั้งด้วย `pip install beautifulsoup4 lxml`).
* สิทธิ์การเขียนในไดเรกทอรีที่คุณวางแผนจะเก็บไฟล์ผลลัพธ์

ไม่ต้องการเครื่องมือเพิ่มเติม; ไลบรารีมาตรฐานจัดการ I/O ของไฟล์ได้

## ขั้นตอนที่ 1: ติดตั้งไลบรารีที่จำเป็น

```bash
pip install beautifulsoup4 lxml
```

`beautifulsoup4` มี API ที่สะดวกสำหรับการแยกวิเคราะห์และจัดการ HTML, ส่วน `lxml` ให้ตัวพาร์เซอร์ที่เร็วและเข้าใจ CSS selectors

## ขั้นตอนที่ 2: สร้างเอกสาร HTML เริ่มต้น

```python
from bs4 import BeautifulSoup

# Define the initial markup as a string
initial_html = "<p>Old</p>"

# Parse the markup into a BeautifulSoup object
doc = BeautifulSoup(initial_html, "lxml")
```

คอนสตรัคเตอร์ `BeautifulSoup` สร้างอ็อบเจกต์ **create html document** ในหน่วยความจำ การใช้พาร์เซอร์ `"lxml"` รับประกันการสนับสนุน CSS selector อย่างเต็มรูปแบบ

## ขั้นตอนที่ 3: เลือกองค์ประกอบย่อหน้าด้วย CSS selector

```python
# Use the CSS selector "p" to locate the first <p> element
para = doc.select_one("p")
```

เมธอด `select_one` ทำงานตามตรรกะ **select element css**, คืนค่าแท็กแรกที่ตรงกัน หาก selector ไม่ตรงกับอะไรเลย `para` จะเป็น `None` ดังนั้นควรตรวจสอบอย่างระมัดระวังในโค้ดการผลิต

## ขั้นตอนที่ 4: แก้ไขข้อความของย่อหน้า

```python
if para is not None:
    # Replace the existing text with new content
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")
```

การกำหนดค่าให้ `para.string` ทำการ **modify html text**  BeautifulSoup จะอัปเดตโครงสร้าง DOM ด้านล่าง, ดังนั้นการเปลี่ยนแปลงจะปรากฏเมื่อเอกสารถูกแปลงเป็นข้อความ

## ขั้นตอนที่ 5: บันทึก HTML ที่อัปเดตลงไฟล์

```python
output_path = "updated.html"

# Write the prettified HTML to disk
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())
print(f"HTML file saved to {output_path}")
```

การเรียก `open` ร่วมกับ `write` ทำหน้าที่ **save html file**  การใช้ `prettify()` จะให้ผลลัพธ์ที่จัดย่อหน้าอย่างสวยงาม ซึ่งเป็นประโยชน์ในการดีบัก

### สคริปต์เต็มสำหรับคัดลอก‑วางอย่างรวดเร็ว

```python
# -------------------------------------------------
# File: edit_html.py
# -------------------------------------------------
# Purpose: Demonstrate how to create html document,
#          select an element with CSS, modify its text,
#          and save the result to a file.
# -------------------------------------------------

from bs4 import BeautifulSoup

# 1️⃣ Create an HTML document with initial content
initial_html = "<p>Old</p>"
doc = BeautifulSoup(initial_html, "lxml")

# 2️⃣ Locate the paragraph element using a CSS selector
para = doc.select_one("p")

# 3️⃣ Update the text inside the paragraph
if para is not None:
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")

# 4️⃣ Save the modified document to a file
output_path = "updated.html"
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())

print(f"HTML file saved to {output_path}")
# -------------------------------------------------
```

การรัน `python edit_html.py` จะสร้างไฟล์ `updated.html` ที่มีเนื้อหา:

```html
<p>
 New
</p>
```

## ความแปรผันทั่วไปและกรณีขอบ

### การเลือกหลายองค์ประกอบ

หากคุณต้องการ **select element css** ที่ตรงกับหลายแท็ก (เช่น `"div.note"`), ใช้ `doc.select("div.note")` ซึ่งจะคืนรายการ ให้วนลูปผ่านรายการเพื่อปรับเปลี่ยนแต่ละองค์ประกอบ

```python
for note in doc.select("div.note"):
    note.string = "Updated note"
```

### การคงคุณลักษณะเดิม

เมื่อคุณแทนที่ข้อความ, BeautifulSoup จะคงคุณลักษณะใด ๆ ของแท็กไว้ ตัวอย่างเช่น:

```python
initial_html = '<p class="intro">Old</p>'
doc = BeautifulSoup(initial_html, "lxml")
para = doc.select_one("p.intro")
para.string = "New"
# Result: <p class="intro">New</p>
```

### การจัดการกับองค์ประกอบที่หายไปอย่างราบรื่น

ในสคริปต์การผลิต, คุณมักเจอ HTML ที่ผิดรูปแบบ การห่อหุ้มการเลือกด้วยเงื่อนไขหรือบล็อก try‑except ตามที่แสดงในขั้นตอน 4 จะช่วยหลีกเลี่ยงการหยุดทำงาน

### การเขียนไปยังไดเรกทอรีเฉพาะ

แทนที่ `output_path` ด้วยพาธแบบ absolute หรือ relative:

```python
output_path = r"C:\Temp\updated.html"   # Windows
# or
output_path = "/home/user/updated.html"  # Linux/macOS
```

ตรวจสอบให้แน่ใจว่าไดเรกทอรีมีอยู่; หากไม่, Python จะโยน `FileNotFoundError`

## เคล็ดลับระดับมืออาชีพ

* **Performance** – สำหรับไฟล์ HTML ขนาดใหญ่ ควรใช้ `lxml.etree` โดยตรง; BeautifulSoup จะเพิ่มชั้นนามธรรมบางส่วนที่สะดวกแต่ช้ากว่าเล็กน้อย
* **Encoding** – เปิดไฟล์เสมอด้วย `encoding="utf-8"` เพื่อคงอักขระที่ไม่ใช่ ASCII
* **Testing** – หลังการแก้ไข, คุณสามารถตรวจสอบผลลัพธ์ด้วย `assert "New" in open(output_path).read()` ในการทดสอบหน่วย

## สรุป

ตอนนี้คุณรู้วิธี **create html document**, ใช้การค้นหา **select element css** เพื่อหาน็อด, **modify html text**, และสุดท้าย **save html file** ด้วย Python รูปแบบนี้สามารถขยายไปสู่การแปลงที่ซับซ้อนยิ่งขึ้น เช่น การอัปเดตเป็นกลุ่ม, การเปลี่ยนแปลงคุณลักษณะ, หรือการสร้างเทมเพลต

ต่อไป, สำรวจหัวข้อที่เกี่ยวข้องเช่น **how to edit html** ด้วย XPath, การสร้างหน้า HTML เต็มรูปแบบด้วย Jinja2, หรือการทำอัตโนมัติการประมวลผลหลายไฟล์แต่ละไฟล์ สิ่งเหล่านี้ต่อยอดจากขั้นตอนหลักที่แสดงในที่นี้และขยายเครื่องมือของคุณสำหรับการจัดการ HTML ด้วยโปรแกรม

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโครงการของคุณ

- [สร้างเอกสาร HTML ด้วย Aspose.HTML – คู่มือขั้นตอนโดยละเอียด](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)
- [วิธีแก้ไขโครงสร้างเอกสาร HTML ใน Aspose.HTML สำหรับ Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [บันทึกเอกสาร HTML ใน Aspose.HTML สำหรับ Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}