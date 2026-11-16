---
category: general
date: 2026-05-31
description: เรียนรู้วิธีดึงองค์ประกอบด้วย id, เปลี่ยนสีพื้นหลังของ HTML, อ่านข้อความ
  HTML และตั้งค่าแอตทริบิวต์ของ HTML ด้วย Python. คู่มือทีละขั้นตอน.
draft: false
keywords:
- get element by id
- change background colour html
- how to read html text
- how to set html attribute
- manipulate html with python
language: th
og_description: ดึงองค์ประกอบตาม id, อ่านข้อความ HTML, ตั้งค่าแอตทริบิวต์ HTML และเปลี่ยนสีพื้นหลังของ
  HTML ด้วย Python ในคู่มือที่ง่ายต่อการทำตามขั้นตอนเดียว.
og_title: ดึงองค์ประกอบโดย id ใน Python – บทเรียนการจัดการ HTML อย่างเต็มรูปแบบ
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  headline: Get element by id in Python – Complete HTML Manipulation Guide
  type: TechArticle
- description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  name: Get element by id in Python – Complete HTML Manipulation Guide
  steps:
  - name: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
    text: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
  - name: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
    text: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
  - name: '**Retrieves** the element using **get element by id**.'
    text: '**Retrieves** the element using **get element by id**.'
  - name: '**Prints** the element’s text—showing **how to read HTML text**.'
    text: '**Prints** the element’s text—showing **how to read HTML text**.'
  - name: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
    text: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
  - name: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
    text: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
  - name: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
    text: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
  type: HowTo
tags:
- python
- html
- web‑scraping
title: ดึงองค์ประกอบตาม id ใน Python – คู่มือการจัดการ HTML อย่างครบถ้วน
url: /th/python/general/get-element-by-id-in-python-complete-html-manipulation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงองค์ประกอบโดย id ใน Python – คู่มือการจัดการ HTML อย่างสมบูรณ์

เคยต้อง **get element by id** จากหน้า HTML ขณะเขียนสคริปต์ Python อย่างรวดเร็วหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาส่วนใหญ่เจออุปสรรคเดียวกันเมื่อต้องครอว์ลเว็บไซต์หรือปรับแต่งรายงานในเครื่อง ข่าวดีคือ ด้วยไม่กี่บรรทัดของโค้ดคุณสามารถอ่านข้อความขององค์ประกอบ เปลี่ยนสีพื้นหลัง และแม้กระทั่งตั้งค่าแอตทริบิวต์ใหม่ได้ทั้งหมดโดยไม่ต้องออกจากโปรแกรมแก้ไขของคุณ

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างจริง: โหลดไฟล์ `sample.html` ที่อยู่ในเครื่อง ดึงองค์ประกอบที่มี ID เป็น `main‑content` พิมพ์ข้อความภายในของมัน และสุดท้ายสลับสีพื้นหลังเป็นสีเทาอ่อน เมื่อจบคุณจะรู้ **how to read HTML text**, **how to set HTML attribute**, และทำไม **manipulate HTML with Python** จึงเป็นทักษะที่มีประโยชน์ในกล่องเครื่องมืออัตโนมัติของคุณ

## สิ่งที่คุณต้องมี

ก่อนที่เราจะลงลึก ตรวจสอบให้แน่ใจว่าคุณมี:

- **Python 3.9+** (เวอร์ชันล่าสุดใดก็ได้)
- ไลบรารี **`lxml`** (หรือ **BeautifulSoup** หากคุณชอบ) – เราจะใช้ `lxml.html` เพราะให้ API แบบ `get_element_by_id` ที่สะอาดตา
- ไฟล์ HTML ขนาดเล็กชื่อ `sample.html` อยู่ในโฟลเดอร์ชื่อ `YOUR_DIRECTORY` คุณสามารถคัดลอกโค้ดตัวอย่างด้านล่างไปวางในไฟล์นั้นได้:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Demo Page</title>
</head>
<body>
    <div id="main-content">
        Hello, world! This is the original text.
    </div>
</body>
</html>
```

เท่านี้—ไม่มีเฟรมเวิร์กซับซ้อน เพียง Python ธรรมดาและไฟล์ HTML คงที่

## ขั้นตอนที่ 1: ติดตั้งไลบรารีที่จำเป็น

หากคุณยังไม่ได้ติดตั้ง `lxml` ให้เปิดเทอร์มินัลแล้วรัน:

```bash
pip install lxml
```

*เคล็ดลับ:* การใช้ virtual environment จะช่วยให้ Python ของคุณเป็นระเบียบโดยไม่กระทบกับโปรเจกต์อื่น ๆ

## ขั้นตอนที่ 2: โหลดเอกสาร HTML

ต่อไปเราจะอ่านไฟล์เข้าเป็นอ็อบเจกต์ `lxml.html` คิดว่าเป็นการแปลงข้อความดิบให้เป็นต้นไม้ที่สามารถนำทางได้

```python
from lxml import html
import pathlib

# Resolve the path to the sample file
html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")

# Parse the file into an HTML document
doc = html.parse(str(html_path)).getroot()
print("Document loaded successfully.")
```

เมื่อรันแล้วจะพิมพ์ “Document loaded successfully.” หากไฟล์ไม่พบ Python จะโยน `FileNotFoundError`—ควรจับข้อผิดพลาดนี้ตั้งแต่ต้นเพื่อหลีกเลี่ยงการตามหาองค์ประกอบที่ไม่มีอยู่

## ขั้นตอนที่ 3: Get element by id

นี่คือหัวใจของเรื่อง `lxml` มีเมธอด `get_element_by_id` ที่ทำงานคล้ายกับ DOM API ใน JavaScript

```python
# Retrieve the element with the specific ID
elem = doc.get_element_by_id("main-content")

if elem is not None:
    print("Element found!")
else:
    print("No element with that ID.")
```

เมื่อพบองค์ประกอบ คุณจะเห็น “Element found!” แสดงบนคอนโซล นี่คือขั้นตอน **get element by id** ที่เป็นฐานของการจัดการต่อ ๆ ไป

## ขั้นตอนที่ 4: How to read HTML text

เมื่อคุณได้องค์ประกอบแล้ว การดึงข้อความที่มองเห็นได้เป็นเรื่องง่าย เมธอด `text_content()` จะคืนค่าทุกอย่างภายในโดยลบแท็กออก

```python
if elem is not None:
    # Show the element's current inner text
    inner_text = elem.text_content()
    print("Inner text:", inner_text)
```

ผลลัพธ์ที่คาดหวัง:

```
Inner text: Hello, world! This is the original text.
```

คุณอาจสงสัยว่า *ถ้าองค์ประกอบมีแท็กซ้อนอยู่ล่ะ?* `text_content()` ยังคงทำงาน—มันจะต่อข้อความของโหนดลูกทั้งหมดให้เป็นสตริงสะอาดที่คุณสามารถบันทึกหรือส่งต่อให้อัลกอริทึมอื่นได้

## ขั้นตอนที่ 5: How to set HTML attribute

การเปลี่ยนหรือเพิ่มแอตทริบิวต์ก็ง่ายเช่นกัน เมธอด `set` ให้คุณกำหนดชื่อแอตทริบิวต์ใดก็ได้ที่ต้องการ

```python
if elem is not None:
    # Set a custom data attribute
    elem.set("data-modified", "true")
    # Verify it was added
    print("New attribute value:", elem.get("data-modified"))
```

ผลลัพธ์:

```
New attribute value: true
```

บรรทัดนี้แสดง **how to set HTML attribute** แบบทันที คุณสามารถเปลี่ยน `"data-modified"` เป็น `"class"` , `"title"` หรือแอตทริบิวต์อื่น ๆ ที่องค์ประกอบรองรับ

## ขั้นตอนที่ 6: Change background colour HTML

ต่อไปเป็นการปรับเปลี่ยนภาพลักษณ์ เพื่อเปลี่ยนสีพื้นหลัง เราจะใส่แอตทริบิวต์ `style` ที่เขียนทับค่าเริ่มต้น

```python
if elem is not None:
    # Change the background colour via a style attribute
    elem.set("style", "background:#f0f0f0")
    print("Background style applied.")
```

หลังจากรันสคริปต์ `div` ใน `sample.html` จะมีลักษณะดังนี้เมื่อเปิดในเบราว์เซอร์:

```html
<div id="main-content" data-modified="true" style="background:#f0f0f0">
    Hello, world! This is the original text.
</div>
```

นี่คือเทคนิค **change background colour html** ที่คุณสามารถนำไปใช้กับองค์ประกอบใดก็ได้—แค่เปลี่ยนรหัสสี

## ขั้นตอนที่ 7: Manipulate HTML with Python – รวมทุกอย่างไว้ด้วยกัน

ด้านล่างเป็นสคริปต์เต็มที่สามารถรันได้ ซึ่งรวมทุกขั้นตอนเข้าด้วยกัน บันทึกเป็น `modify_html.py` แล้วเรียกใช้จากโฟลเดอร์เดียวกับ `YOUR_DIRECTORY`

```python
#!/usr/bin/env python3
"""
Complete example: load an HTML file, get element by id,
read its text, set a new attribute, and change its background colour.
"""

from lxml import html
import pathlib
import sys

def main():
    # 1️⃣ Load the document
    html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")
    try:
        doc = html.parse(str(html_path)).getroot()
    except OSError as e:
        sys.exit(f"Failed to read HTML file: {e}")

    # 2️⃣ Get element by id
    elem = doc.get_element_by_id("main-content")
    if elem is None:
        sys.exit("Element with ID 'main-content' not found.")

    # 3️⃣ Read HTML text
    print("🗒️  Inner text:", elem.text_content())

    # 4️⃣ Set a new attribute
    elem.set("data-modified", "true")
    print("✅  data-modified attribute set to:", elem.get("data-modified"))

    # 5️⃣ Change background colour HTML
    elem.set("style", "background:#f0f0f0")
    print("🎨  Background colour changed to #f0f0f0")

    # 6️⃣ Write the modified HTML back to disk
    output_path = pathlib.Path("YOUR_DIRECTORY/sample_modified.html")
    output_path.write_text(html.tostring(doc, pretty_print=True, encoding="unicode"))
    print(f"💾  Modified file saved as {output_path}")

if __name__ == "__main__":
    main()
```

### สิ่งที่สคริปต์ทำ ทีละบรรทัด

1. **Imports** `lxml.html` สำหรับการพาร์สและ `pathlib` สำหรับเส้นทางที่เป็น OS‑independent  
2. **Loads** `sample.html` และหยุดพร้อมข้อความชัดเจนหากไฟล์หายไป  
3. **Retrieves** องค์ประกอบด้วย **get element by id**  
4. **Prints** ข้อความขององค์ประกอบ—แสดง **how to read HTML text**  
5. **Adds** แอตทริบิวต์แบบกำหนดเอง แสดง **how to set HTML attribute**  
6. **Changes** สีพื้นหลัง เพื่อทำตามความต้องการ **change background colour html**  
7. **Writes** markup ที่อัปเดตลงใน `sample_modified.html` เพื่อให้คุณเปิดในเบราว์เซอร์และเห็นการเปลี่ยนแปลง

เมื่อรันสคริปต์จะได้ผลลัพธ์บนคอนโซลคล้ายกับ:

```
🗒️  Inner text: Hello, world! This is the original text.
✅  data-modified attribute set to: true
🎨  Background colour changed to #f0f0f0
💾  Modified file saved as YOUR_DIRECTORY/sample_modified.html
```

เปิด `sample_modified.html` แล้วคุณจะเห็นพื้นหลังสีเทาอยู่หลังข้อความ—พิสูจน์ว่า **manipulate HTML with python** ทำงานจริง

## ข้อผิดพลาดทั่วไป & วิธีหลีกเลี่ยง

- **Missing ID** – หากไม่มีองค์ประกอบเป้าหมาย `get_element_by_id` จะคืนค่า `None` ตรวจสอบให้แน่ใจว่าตรวจสอบ `None` ก่อนเข้าถึงคุณสมบัติ มิฉะนั้นจะเกิด `AttributeError`  
- **Encoding issues** – เมื่ออ่านหน้าไม่ใช่ ASCII ให้ใส่ `encoding='utf-8'` ใน `html.parse` หรือให้ไฟล์ของคุณบันทึกเป็น UTF‑8  
- **Overwriting existing styles** – การตั้งค่าแอตทริบิวต์ `style` จะทับสไตล์อินไลน์เดิม หากต้องการเก็บกฎเดิมไว้ ให้อ่านค่า `style` ปัจจุบันก่อน เพิ่มกฎใหม่ แล้วเขียนกลับไป  
- **File permissions** – การเขียนกลับไปยังโฟลเดอร์เดียวกันอาจล้มเหลวบนระบบที่อ่าน‑อย่าง‑เดียว ให้เลือกเส้นทางที่เขียนได้ เช่น `sample_modified.html` ที่เราใช้ในตัวอย่าง

## ขยายตัวอย่างต่อ

เมื่อคุณเชี่ยวชาญพื้นฐานแล้ว ลองทำตามขั้นตอนต่อไปนี้:

- **Loop over multiple IDs** – ใช้ลิสต์ของ ID แล้ววน `for` เพื่อประมวลผลหลายส่วนของหน้าในครั้งเดียว  
- **Replace text content** – ใช้ `elem.text = "New text"` เพื่อเปลี่ยนข้อความที่มองเห็นได้  
- **Add child elements** – ใช้  

## คุณควรเรียนรู้อะไรต่อไป?

- [วิธีแก้ไข HTML ด้วย Aspose.HTML สำหรับ Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [วิธี Query HTML ใน Java – คู่มือฉบับสมบูรณ์](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [วิธีแปลง HTML เป็น PDF ด้วย Java – ใช้ Aspose.HTML สำหรับ Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}