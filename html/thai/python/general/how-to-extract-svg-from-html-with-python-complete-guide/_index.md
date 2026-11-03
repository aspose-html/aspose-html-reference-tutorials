---
category: general
date: 2026-05-31
description: เรียนรู้วิธีดึง SVG จาก HTML ด้วย Python การสอนแบบขั้นตอนนี้แสดงวิธีอ่านเอกสาร
  HTML, บันทึกไฟล์ SVG และบันทึก SVG แบบอินไลน์อย่างมีประสิทธิภาพ.
draft: false
keywords:
- how to extract svg
- read html document
- save svg files
- save inline svg
- extract svg from html
language: th
og_description: วิธีดึง SVG จาก HTML ด้วย Python ทำตามบทเรียนนี้เพื่ออ่านเอกสาร HTML
  บันทึกไฟล์ SVG และจัดการกับ SVG แบบอินไลน์ได้อย่างง่ายดาย
og_title: วิธีดึง SVG จาก HTML ด้วย Python – คู่มือเต็ม
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  headline: How to extract SVG from HTML with Python – Complete Guide
  type: TechArticle
- description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  name: How to extract SVG from HTML with Python – Complete Guide
  steps:
  - name: Reads an HTML file.
    text: Reads an HTML file.
  - name: Collects inline <svg> markup.
    text: Collects inline <svg> markup.
  - name: Finds external SVG references (<img> and <object> tags).
    text: Finds external SVG references (<img> and <object> tags).
  - name: Saves each SVG to a separate .svg file.
    text: Saves each SVG to a separate .svg file.
  type: HowTo
tags:
- Python
- SVG
- HTML parsing
- Aspose
title: วิธีดึง SVG จาก HTML ด้วย Python – คู่มือฉบับสมบูรณ์
url: /th/python/general/how-to-extract-svg-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีดึง SVG จาก HTML ด้วย Python – คู่มือฉบับสมบูรณ์

เคยสงสัย **วิธีดึง SVG** จากหน้า HTML ที่รกๆ โดยไม่ต้องบิดหัวไหม? คุณไม่ได้อยู่คนเดียว ไม่ว่าคุณจะกำลังสร้างเว็บ‑สครัปเปอร์, pipeline ด้านดีไซน์, หรือแค่ต้องการส่งออกไอคอนเป็นชุด, การรู้ **วิธีดึง SVG** เป็นเทคนิคที่ช่วยประหยัดเวลาและลดความยุ่งยาก

ในบทเรียนนี้เราจะสาธิต **วิธีดึง SVG** อย่างละเอียดโดยใช้ไลบรารี Aspose.HTML สำหรับ Python เราจะอ่านไฟล์ HTML, ดึงเอา markup `<svg>` ทั้งแบบ inline **และ** การอ้างอิง SVG ภายนอก, แล้ว **บันทึกไฟล์ SVG** ลงดิสก์—ทั้งหมดในสคริปต์ที่เรียบง่ายและนำกลับมาใช้ใหม่ได้ หลังจากจบคุณจะได้โซลูชันที่พร้อมรันและปรับใช้กับโปรเจกต์ของคุณ

> **เคล็ดลับ:** หากคุณแค่ต้องการดูกระบวนการอย่างเร็ว `BeautifulSoup` ก็ทำได้เช่นกัน, แต่ Aspose.HTML ให้ DOM เต็มรูปแบบ ทำให้การดึงทั้ง SVG แบบ inline และแบบลิงก์เป็นเรื่องง่ายดาย

## สิ่งที่คุณต้องมี

ก่อนที่เราจะลงมือทำ, ตรวจสอบให้แน่ใจว่าคุณมี:

* Python 3.8+ (โค้ดใช้ f‑strings, ดังนั้น 3.6+ เป็นขั้นต่ำที่ต้องมี)
* `pip install aspose-html` – ไลบรารีเชิงพาณิชย์ที่ใช้สำหรับการพาร์ส HTML
* โฟลเดอร์ที่มีไฟล์ `input.html` ซึ่งบรรจุ SVG ที่คุณต้องการดึงออก
* สิทธิ์การเขียนในไดเรกทอรีผลลัพธ์ (เราจะเรียกมันว่า `YOUR_DIRECTORY`)

แค่นั้นเอง—ไม่มีไบนารีเพิ่มเติม, ไม่มีเบราว์เซอร์แบบ headless. ง่ายใช่ไหม?

## ขั้นตอนที่ 1: อ่านเอกสาร HTML ด้วย Aspose.HTML

สิ่งแรกที่ต้องทำคือ **อ่านเอกสาร HTML** เพื่อให้คุณสามารถเดินทางในโครงสร้าง DOM ได้ Aspose.HTML จะให้คุณได้อ็อบเจ็กต์ `HTMLDocument` ที่ทำงานคล้ายกับ `document` ของเบราว์เซอร์

```python
from aspose.html import HTMLDocument

# Load the HTML file – replace YOUR_DIRECTORY with the actual path
doc = HTMLDocument("YOUR_DIRECTORY/input.html")
```

*ทำไมจึงสำคัญ:* การโหลด HTML เข้า DOM ที่ถูกต้องช่วยหลีกเลี่ยงปัญหาการพาร์สด้วย regex, และคุณจะได้เมธอดอย่าง `get_elements_by_tag_name` และ `query_selector_all` มาให้โดยอัตโนมัติ

## ขั้นตอนที่ 2: รวบรวมทุกองค์ประกอบ `<svg>` แบบ inline

SVG แบบ inline คือบล็อก `<svg>…</svg>` ที่อยู่ภายใน HTML โดยตรง เพื่อ **บันทึก SVG แบบ inline** เราแค่ต้องการเอา outer HTML ของมัน

```python
svg_contents = []  # We'll collect both markup and file paths here

# Find every <svg> element in the document
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)   # Store the raw markup
```

สังเกตว่าเรากำลังต่อ markup ดิบโดยตรงเข้าไปใน `svg_contents` หลังจากนี้เราจะตัดสินใจว่าแต่ละรายการเป็น markup หรือเป็นเส้นทางไฟล์

## ขั้นตอนที่ 3: ค้นหาการอ้างอิง SVG ภายนอก (แท็ก img และ object)

หลายหน้าเว็บลิงก์ไฟล์ SVG ภายนอกผ่าน `<img src="icon.svg">` หรือ `<object data="logo.svg">` เพื่อ **ดึง SVG จาก HTML** เราต้องจับ URL เหล่านั้นด้วย

```python
# CSS selector: img or object whose src/data ends with .svg (case‑insensitive)
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    # For <img> we read the src attribute, for <object> the data attribute
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:                                   # Guard against missing attribute
        svg_contents.append(src)
```

*แจ้งเตือนกรณีขอบ:* หาก URL ของ SVG เป็น relative, คุณควรเชื่อมต่อกับ base path ของไฟล์ HTML สำหรับความกระชับเราจะสมมติว่า HTML อยู่เคียงข้างไฟล์ SVG

## ขั้นตอนที่ 4: เขียนแต่ละ SVG ลงไฟล์แยกกัน

ตอนนี้เรามีรายการผสมของสตริง markup และเส้นทางไฟล์แล้ว, เราจะวนลูปและ **บันทึกไฟล์ SVG** สคริปต์จะตรวจจับอัตโนมัติว่าเป็น markup แบบ inline หรือเป็นการอ้างอิงไฟล์ที่มีอยู่

```python
import os
import shutil

for index, content in enumerate(svg_contents):
    output_path = f"YOUR_DIRECTORY/svg_{index}.svg"

    # Trim leading whitespace and check if it looks like markup
    if content.lstrip().startswith("<svg"):
        # Inline SVG – write the markup directly
        with open(output_path, "w", encoding="utf-8") as file:
            file.write(content)
        print(f"Saved inline SVG to {output_path}")
    else:
        # External reference – copy the source file's contents
        src_path = os.path.abspath(content)  # Resolve relative paths
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, output_path)
            print(f"Copied external SVG from {src_path} to {output_path}")
        else:
            print(f"⚠️  Warning: referenced SVG not found: {src_path}")
```

**สิ่งที่คุณจะเห็น:** หลังสคริปต์ทำงานเสร็จ, `YOUR_DIRECTORY` จะมีไฟล์ชื่อ `svg_0.svg`, `svg_1.svg`, … แต่ละไฟล์จะบรรจุ markup inline ดั้งเดิมหรือสำเนาของ SVG ภายนอก

### ผลลัพธ์ที่คาดหวัง

```
Saved inline SVG to YOUR_DIRECTORY/svg_0.svg
Saved inline SVG to YOUR_DIRECTORY/svg_1.svg
Copied external SVG from /path/to/logo.svg to YOUR_DIRECTORY/svg_2.svg
...
```

หากไฟล์ที่อ้างอิงไม่พบ, สคริปต์จะแสดงคำเตือนแต่จะดำเนินต่อ—ดังนั้นลิงก์ที่เสียหนึ่งลิงก์จะไม่ทำให้การดึงทั้งหมดหยุดชะงัก

## การจัดการกับปัญหาที่พบบ่อย

| ปัญหา | สาเหตุ | วิธีแก้เร็ว |
|---------|----------------|-----------|
| **URL แบบ relative ขัดข้อง** | แอตทริบิวต์ `src` อาจเป็น `"../assets/icon.svg"` | ใช้ `os.path.join(os.path.dirname(html_path), src)` เพื่อแก้ไข |
| **ชื่อไฟล์ซ้ำ** | มี SVG สองไฟล์ที่ใช้ชื่อเดียวกันทำให้ไฟล์ถูกเขียนทับ | ใส่แฮชของเนื้อหาในชื่อไฟล์ (`hashlib.md5(content.encode()).hexdigest()[:8]`) |
| **SVG แบบ inline ขนาดใหญ่ทำให้เมมโมรีพุ่ง** | เก็บ markup ทั้งหมดในลิสต์ก่อนเขียน | สตรีมแต่ละองค์ประกอบโดยตรงไปไฟล์แทนการบัฟเฟอร์ |
| **ภาพที่ไม่ใช่ SVG ล่วงผ่าน** | บาง `<img>` มีนามสกุล `.svg?version=1` | ตัด query string ก่อนตรวจสอบนามสกุล (`src.split('?')[0]`) |

## สคริปต์เต็มที่คุณสามารถคัดลอก‑วางได้

ด้านล่างเป็นโปรแกรมที่พร้อมรันทั้งหมด บันทึกเป็น `extract_svg.py`, ปรับ `YOUR_DIRECTORY` ตามต้องการ, แล้วรันด้วย `python extract_svg.py`

```python
"""
extract_svg.py – How to extract SVG from HTML using Aspose.HTML for Python

This script:
1. Reads an HTML file.
2. Collects inline <svg> markup.
3. Finds external SVG references (<img> and <object> tags).
4. Saves each SVG to a separate .svg file.

Author: Your Name
Date: 2026-05-31
"""

import os
import shutil
from aspose.html import HTMLDocument

# ----------------------------------------------------------------------
# Configuration – change these paths to suit your environment
# ----------------------------------------------------------------------
HTML_PATH = "YOUR_DIRECTORY/input.html"          # Path to source HTML
OUTPUT_DIR = "YOUR_DIRECTORY"                    # Where SVGs will be written

# Ensure output directory exists
os.makedirs(OUTPUT_DIR, exist_ok=True)

# ----------------------------------------------------------------------
# Step 1: Load the HTML document (read html document)
# ----------------------------------------------------------------------
doc = HTMLDocument(HTML_PATH)

# ----------------------------------------------------------------------
# Step 2: Collect inline <svg> elements (save inline svg)
# ----------------------------------------------------------------------
svg_contents = []
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)

# ----------------------------------------------------------------------
# Step 3: Collect external SVG references (extract svg from html)
# ----------------------------------------------------------------------
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:
        # Resolve relative paths relative to the HTML file location
        src_path = os.path.join(os.path.dirname(HTML_PATH), src)
        svg_contents.append(src_path)

# ----------------------------------------------------------------------
# Step 4: Save each gathered SVG (save svg files)
# ----------------------------------------------------------------------
for idx, content in enumerate(svg_contents):
    out_path = os.path.join(OUTPUT_DIR, f"svg_{idx}.svg")

    # Detect inline markup vs file path
    if isinstance(content, str) and content.lstrip().startswith("<svg"):
        # Inline SVG – write directly
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(content)
        print(f"[✓] Inline SVG saved → {out_path}")
    else:
        # External file – copy its contents
        src_path = os.path.abspath(content)
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, out_path)
            print(f"[✓] External SVG copied → {out_path}")
        else:
            print(f"[⚠] Missing SVG file: {src_path}")

print("\n✅ Extraction complete. Check the", OUTPUT_DIR, "folder for your SVGs.")
```

## สรุป – วิธีดึง SVG อย่างสั้นๆ

* **อ่านเอกสาร HTML** ด้วย `HTMLDocument`
* **รวบรวม `<svg>` แบบ inline** ผ่าน `get_elements_by_tag_name`
* **ค้นหา SVG ภายนอก** ด้วย CSS selector ที่ลงท้ายด้วย `.svg`
* **บันทึกแต่ละส่วน** — เขียน markup ลงไฟล์โดยตรงหรือคัดลอกไฟล์ที่อ้างอิง
* **จัดการกรณีขอบ** เช่น เส้นทาง relative, ชื่อไฟล์ซ้ำ, ไฟล์หาย

นี่คือคำตอบทั้งหมดสำหรับ **วิธีดึง SVG** จากหน้า HTML, รวมอยู่ในสคริปต์เดียวที่ง่ายต่อการปรับแต่ง

## ต่อไปคุณจะทำอะไรได้บ้าง?

เมื่อคุณดึง **SVG** ได้อย่างมั่นใจแล้ว, ลองไอเดียต่อไปนี้:

* **ประมวลผลเป็นชุด:** วนลูปผ่านโฟลเดอร์ของไฟล์ HTML เพื่อสร้างไลบรารีไอคอน
* **เพิ่มประสิทธิภาพ:** รัน SVG ที่บันทึกไว้ผ่าน SVGO (optimizer ของ Node.js) เพื่อลดขนาดไฟล์
* **แปลงรูปแบบ:** ใช้ `cairosvg` หรือ `svglib` เพื่อแปลง SVG เป็น PNG สำหรับเบราว์เซอร์รุ่นเก่า
* **ดึงเมตาดาต้า:** พาร์สแท็ก `<title>` หรือ `<desc>` ภายในแต่ละ SVG เพื่อใช้เป็นป้ายกำกับที่ค้นหาได้

หัวข้อเหล่านี้เชื่อมโยงกับคีย์เวิร์ดรองของเรา—**read HTML document**, **save svg files**, **save inline svg**, **extract svg from html**—จึงมีเนื้อหาให้คุณสำรวจต่อไปอีกมาก

---

*Happy hacking! หากเจออุปสรรคใด, แสดงความคิดเห็นด้านล่างหรือทักมาที่ GitHub. โลกของ SVG กว้างใหญ่, แต่ด้วยเครื่องมือที่ถูกต้อง การดึงมันก็เป็นเรื่องง่ายเหมือนตัดเค้ก.*

## คุณควรเรียนรู้อะไรต่อไป?

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [Rendre un document SVG au format PNG dans .NET avec Aspose.HTML](/html/french/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}