---
category: general
date: 2026-11-27
description: สร้างเอกสาร SVG และบันทึกไฟล์ SVG ด้วย Python เรียนรู้การส่งออกเวกเตอร์เป็น
  SVG และสร้างภาพ SVG อย่างรวดเร็ว
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG file
- export vector as SVG
- save SVG image
- how to create SVG
language: th
lastmod: 2026-11-27
og_description: สร้างเอกสาร SVG และบันทึกไฟล์ SVG ด้วย Python คู่มือนี้จะแสดงวิธีส่งออกเวกเตอร์เป็น
  SVG และสร้างภาพ SVG ในไม่กี่นาที
og_image_alt: Screenshot of a red circle saved as an SVG document
og_title: สร้างเอกสาร SVG และบันทึกไฟล์ SVG ด้วย Python
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  headline: Create SVG document and save SVG file with Python
  type: TechArticle
- description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  name: Create SVG document and save SVG file with Python
  steps:
  - name: Expected output
    text: 'The resulting `circle.svg` contains:'
  - name: Exporting more complex vectors
    text: 'If you need to **export vector as SVG** for multi‑shape illustrations,
      simply repeat the `dwg.add()` pattern with other primitives (`rect`, `line`,
      `path`, etc.). For example:'
  - name: Handling Unicode and text
    text: "SVG supports text elements with full Unicode support. Use `dwg.text(\"Hello,
      \U0001F30D\", insert=(5, 95), fill=\"black\")` to embed multilingual labels."
  - name: Saving to a different location
    text: 'When **save SVG image** to a user‑specified folder, validate the path to
      avoid permission errors:'
  - name: Minifying the output
    text: 'For production pipelines, you might want a smaller file size. Pass `pretty=False`
      to `dwg.tostring()` and write the result manually:'
  type: HowTo
tags:
- SVG
- Python
- Vector graphics
title: สร้างเอกสาร SVG และบันทึกไฟล์ SVG ด้วย Python
url: /th/python/general/create-svg-document-and-save-svg-file-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้างเอกสาร SVG และบันทึกไฟล์ SVG ด้วย Python

หากคุณต้องการ **สร้างเอกสาร SVG** ตั้งแต่ต้น คู่มือนี้จะพาคุณผ่านกระบวนการทั้งหมด คุณจะได้เห็นวิธี **บันทึกไฟล์ SVG** ลงดิสก์, ส่งออกเวกเตอร์เป็น SVG, และได้ภาพ SVG ที่พร้อมใช้งานในไม่กี่บรรทัดของโค้ด

การสร้างกราฟิกขนาดยืดหยุ่นโดยอัตโนมัติเป็นประโยชน์สำหรับรายงาน, ไอคอน UI, หรือสถานการณ์ใด ๆ ที่คุณต้องการภาพที่ไม่ขึ้นกับความละเอียด เมื่อจบบทเรียนนี้คุณจะสามารถตอบคำถาม “**วิธีสร้าง SVG**?” สำหรับรูปทรงง่าย ๆ และต่อยอดเป็นงานศิลปะเวกเตอร์ที่ซับซ้อนได้

## สิ่งที่คุณต้องมี

- Python 3.8 หรือใหม่กว่า  
- แพ็กเกจ `svgwrite` (ติดตั้งได้ผ่าน `pip`)  
- โฟลเดอร์ที่สามารถเขียนไฟล์ได้สำหรับไฟล์ผลลัพธ์  

ไม่จำเป็นต้องใช้โปรแกรมแก้ไขกราฟิกภายนอก; ทุกอย่างทำงานจากบรรทัดคำสั่ง

## ขั้นตอนที่ 1: ติดตั้งไลบรารี `svgwrite`

`svgwrite` ให้ API ที่สะอาดและเป็นสไตล์ Python สำหรับสร้าง markup ของ SVG ติดตั้งครั้งเดียวด้วยคำสั่ง:

```bash
pip install svgwrite
```

> **เคล็ดลับ:** ใช้ virtual environment (`python -m venv .venv`) เพื่อแยกการพึ่งพาออกจากโปรเจกต์อื่น

## ขั้นตอนที่ 2: สร้างเอกสาร SVG

ตอนนี้เราจะ **สร้างเอกสาร SVG** จริง ๆ คลาส `Drawing` แทนองค์ประกอบราก `<svg>` และจัดการ namespace ให้โดยอัตโนมัติ

```python
import pathlib
import svgwrite

# Define where the file will be saved
output_path = pathlib.Path("output/circle.svg")
output_path.parent.mkdir(parents=True, exist_ok=True)

# Initialize a new SVG document with a 100×100 viewport
dwg = svgwrite.Drawing(
    filename=str(output_path),
    size=("100px", "100px"),
    profile="tiny"  # tiny profile keeps the file lightweight
)
```

อินสแตนซ์ `Drawing` คือจุดเริ่มต้นสำหรับการทำงานกับ SVG ทั้งหมดต่อไป โดยการระบุ `size` เรากำหนดขนาดของแคนวาส ซึ่งมีผลต่อการแสดงผลของเบราว์เซอร์

## ขั้นตอนที่ 3: เพิ่มองค์ประกอบวงกลมสีแดง

การเพิ่มรูปทรงทำได้ง่าย ๆ เมธอด `circle` สร้างองค์ประกอบ `<circle>` แล้วเราจึงแนบมันเข้ากับราก

```python
# Create a red circle with radius 40 centered at (50, 50)
circle = dwg.circle(
    center=(50, 50),
    r=40,
    fill="red"
)

# Append the circle to the SVG root
dwg.add(circle)
```

เหตุผลที่เราเลือกวงกลม: วงกลมเป็น primitive ของเวกเตอร์ที่แสดงความสามารถในการยืดขยายโดยไม่มีการสูญเสียคุณภาพ ทำให้ผลลัพธ์เหมาะสำหรับการทดสอบกระบวนการ **export vector as SVG**

## ขั้นตอนที่ 4: บันทึกไฟล์ SVG

สุดท้ายให้เขียน markup ลงดิสก์ ขั้นตอนนี้ทำให้ **บันทึกไฟล์ SVG** เสร็จสมบูรณ์และสร้างไฟล์ที่คุณสามารถเปิดในเบราว์เซอร์หรือโปรแกรมแก้ไขเวกเตอร์ใดก็ได้

```python
# Persist the SVG document to the filesystem
dwg.save()
print(f"SVG saved to {output_path.resolve()}")
```

เมื่อคุณรันสคริปต์ จะเห็นข้อความในคอนโซลยืนยันตำแหน่งของไฟล์ที่สร้างขึ้น

### ผลลัพธ์ที่คาดหวัง

ไฟล์ `circle.svg` ที่ได้จะมีเนื้อหา:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg height="100px" version="1.1" width="100px" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" fill="red"/>
</svg>
```

เปิดไฟล์ในเบราว์เซอร์จะแสดงวงกลมสีแดงที่คมชัด และเนื่องจากเป็นเวกเตอร์ คุณสามารถซูมเข้าได้ไม่จำกัดโดยไม่มีการพิกเซล

## ขั้นตอนที่ 5: ตัวแปรทั่วไปและกรณีขอบ

### ส่งออกเวกเตอร์ที่ซับซ้อนกว่า

หากต้องการ **export vector as SVG** สำหรับภาพประกอบหลายรูปทรง เพียงทำซ้ำรูปแบบ `dwg.add()` กับ primitive อื่น ๆ (`rect`, `line`, `path` เป็นต้น) ตัวอย่างเช่น:

```python
dwg.add(dwg.rect(insert=(10, 10), size=(30, 30), fill="blue"))
dwg.add(dwg.line(start=(0, 0), end=(100, 100), stroke="black", stroke_width=2))
```

### จัดการ Unicode และข้อความ

SVG รองรับองค์ประกอบข้อความพร้อมการสนับสนุน Unicode เต็มรูปแบบ ใช้ `dwg.text("Hello, 🌍", insert=(5, 95), fill="black")` เพื่อฝังป้ายหลายภาษา

### บันทึกไปยังตำแหน่งอื่น

เมื่อ **save SVG image** ไปยังโฟลเดอร์ที่ผู้ใช้ระบุ ให้ตรวจสอบพาธเพื่อหลีกเลี่ยงข้อผิดพลาดเรื่องสิทธิ์:

```python
if not output_path.parent.exists():
    raise PermissionError(f"Cannot write to {output_path.parent}")
dwg.save()
```

### ลดขนาดไฟล์ผลลัพธ์

สำหรับ pipeline การผลิต คุณอาจต้องการไฟล์ขนาดเล็กลง ส่งค่า `pretty=False` ให้กับ `dwg.tostring()` แล้วเขียนผลลัพธ์ด้วยตนเอง:

```python
minified = dwg.tostring(pretty=False)
output_path.write_text(minified)
```

## วิธีสร้าง SVG ด้วยไลบรารีทางเลือก (ไม่บังคับ)

แม้ `svgwrite` จะเบาและเป็น Python ล้วน ๆ แต่ก็มี ecosystem อื่น ๆ:

- **cairosvg** – แปลง PNG, PDF หรือ HTML เป็น SVG  
- **lxml** – ให้คุณสร้าง markup ของ SVG ด้วย API ของ XML  

การเลือกไลบรารีขึ้นอยู่กับความซับซ้อนของโปรเจกต์และการพึ่งพาที่มีอยู่แล้ว

## สรุป

คุณได้เรียนรู้วิธี **สร้างเอกสาร SVG**, เพิ่มรูปทรงเวกเตอร์, และ **บันทึกไฟล์ SVG** ด้วย Python โซลูชันเต็มรูปแบบนี้แสดงขั้นตอนการ **export vector as SVG**, สร้าง **SVG image**, และตอบคำถามทั่วไป **วิธีสร้าง SVG** ด้วยโปรแกรม

ต่อจากนี้คุณสามารถ:

- ขยายสคริปต์ด้วยลูปเพื่อสร้างแผนภูมิหรือไอคอนโดยอัตโนมัติ  
- ผสานผลลัพธ์ SVG เข้าในเว็บแอปหรือเทมเพลตอีเมล  
- ทดลองแอนิเมชันโดยเพิ่มองค์ประกอบ `<animate>` ด้วย `svgwrite`

ลองเล่นกับรูปทรง, สี, และไล่ระดับสีต่าง ๆ เพื่อใช้ศักยภาพของกราฟิกเวกเตอร์ที่ปรับขนาดได้ในโปรเจกต์ Python ของคุณ ขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีโค้ดตัวอย่างทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโปรเจกต์ของคุณเอง

- [Create SVG Document – Add a Circle and Save as SVG](/html/english/python/general/create-svg-document-add-a-circle-and-save-as-svg/)
- [Create SVG Document in Python – Convert SVG to PNG Guide](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)
- [Load SVG File Python – Complete Guide to Export, Embed & Convert](/html/english/python/general/load-svg-file-python-complete-guide-to-export-embed-convert/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}