---
category: general
date: 2026-10-02
description: เรียนรู้วิธีสร้างเอกสาร SVG ด้วย Python, บันทึก SVG ลงไฟล์, และส่งออกภาพ
  SVG ด้วยสคริปต์สั้น ๆ ที่ครบถ้วน.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG to file
- how to generate SVG
- export SVG image
- SVG Python tutorial
language: th
lastmod: 2026-10-02
og_description: สร้างเอกสาร SVG ด้วย Python และส่งออกภาพ SVG ด้วยบทเรียนปฏิบัตินี้
  ทำตามสคริปต์ บันทึก SVG ไปยังไฟล์ และใช้กราฟิกเวกเตอร์ได้ทันที
og_image_alt: Screenshot of a Python script that creates an SVG document
og_title: สร้างเอกสาร SVG ด้วย Python – คู่มือแบบทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-10-02'
  description: Learn how to create SVG document in Python, save SVG to file, and export
    SVG image with a short, complete script.
  headline: How to create SVG document and export it as an image in Python
  type: TechArticle
tags:
- SVG
- Python
- graphics
title: วิธีสร้างเอกสาร SVG และส่งออกเป็นภาพใน Python
url: /th/python/general/how-to-create-svg-document-and-export-it-as-an-image-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้างเอกสาร SVG และส่งออกเป็นภาพใน Python

หากคุณต้องการ **สร้างเอกสาร SVG** อย่างอัตโนมัติ, บทแนะนำนี้จะแสดงให้คุณเห็นขั้นตอนที่ทำได้ด้วย Python อย่างละเอียด คุณจะได้เห็นสคริปต์เต็มที่สร้างวงกลมง่าย ๆ, บันทึก SVG ลงไฟล์, และสร้างภาพ SVG ที่สามารถฝังได้ทุกที่

การสร้างกราฟิกเวกเตอร์ที่ปรับขนาดได้จากโค้ดช่วยลดความพยายามในการวาดรูปด้วยโปรแกรม GUI ด้วยตนเอง เมื่ออ่านจบคู่มือคุณจะสามารถผสานการสร้าง SVG เข้าไปในกระบวนการแสดงผลข้อมูล, ตัวสร้างรายงานอัตโนมัติ, หรือโครงการใด ๆ ที่ต้องการกราฟิกคมชัดและไม่ขึ้นกับความละเอียด

## ความต้องการเบื้องต้น

ก่อนเริ่มทำงาน, โปรดตรวจสอบว่าคุณมี:

- Python 3.8 หรือใหม่กว่า
- ไลบรารี `svgwrite` (ติดตั้งด้วย `pip install svgwrite`)
- สิทธิ์การเขียนในไดเรกทอรีที่ต้องการบันทึกไฟล์ SVG

ข้อกำหนดเหล่านี้ทำให้ตัวอย่างมีน้ำหนักเบาและเข้ากันได้กับสภาพแวดล้อมส่วนใหญ่

## ขั้นตอนที่ 1: ติดตั้งและนำเข้าไลบรารี SVG

ขั้นตอนแรกคือการเพิ่มไลบรารีของบุคคลที่สามที่ให้ API ที่สะดวกสำหรับการสร้าง SVG

```python
# Install the library (run once in your terminal)
# pip install svgwrite

import svgwrite  # Provides the SVGDocument class and element helpers
```

`svgwrite` ทำหน้าที่เป็นชั้นนามธรรมของโครงสร้าง XML ของไฟล์ SVG, ทำให้คุณโฟกัสที่รูปทรงเรขาคณิตแทนการจัดการ markup ดิบ

## ขั้นตอนที่ 2: สร้างอ็อบเจ็กต์เอกสาร SVG

ตอนนี้คุณสามารถ **สร้างเอกสาร SVG** ได้โดยการสร้างอินสแตนซ์ของ `svgwrite.Drawing`. อ็อบเจ็กต์นี้แทนองค์ประกอบ `<svg>` รากและเก็บรูปทรงทั้งหมดที่ตามมา

```python
# Step 2: Initialize the SVG document
dwg = svgwrite.Drawing(
    filename="circle.svg",     # Desired output file name
    size=("100px", "100px"),   # Width and height of the canvas
    viewBox=("0 0 100 100")    # Coordinate system for drawing
)
```

อาร์กิวเมนต์ `size` กำหนดขนาดพิกเซลที่แสดงผล, ส่วน `viewBox` กำหนดระบบพิกัดที่สอดคล้องกับเรขาคณิตที่คุณจะกำหนดต่อไป

## ขั้นตอนที่ 3: เพิ่มองค์ประกอบวงกลม

วงกลมถูกกำหนดด้วยศูนย์กลาง (`cx`, `cy`) และรัศมี (`r`). ใช้ตัวช่วย `circle` เพื่อแนบแอตทริบิวต์เหล่านี้

```python
# Step 3: Create a <circle> element
circle = dwg.circle(
    center=("50", "50"),   # cx = 50, cy = 50
    r="40",                # radius = 40
    fill="lightcoral",     # Fill color for visual clarity
    stroke="black",        # Outline color
    stroke_width="2"
)

# Append the circle to the SVG root
dwg.add(circle)
```

วงกลมอยู่ตรงกลางของแคนวาสขนาด 100 × 100, มีระยะขอบ 10 พิกเซลในแต่ละด้าน ปรับ `fill` และ `stroke` ให้สอดคล้องกับสไตล์การออกแบบของคุณ

## ขั้นตอนที่ 4: บันทึก SVG ลงไฟล์

เมื่อกราฟิกพร้อม, คุณสามารถ **บันทึก SVG ลงไฟล์** ด้วยเมธอด `save`. วิธีนี้จะเขียน XML ที่สมบูรณ์ซึ่งเบราว์เซอร์และโปรแกรมแก้ไขเวกเตอร์เข้าใจได้

```python
# Step 4: Persist the SVG document
dwg.save()
print("SVG file saved as circle.svg")
```

ไฟล์ `circle.svg` ตอนนี้อยู่ในไดเรกทอรีทำงานปัจจุบัน คุณสามารถเปิดในเว็บเบราว์เซอร์, Inkscape, หรือเครื่องมือใด ๆ ที่รองรับรูปแบบ SVG

## ขั้นตอนที่ 5: ตรวจสอบภาพ SVG ที่ส่งออก

เปิดไฟล์ที่บันทึกไว้ในเบราว์เซอร์เพื่อยืนยันผลลัพธ์ คุณควรเห็นวงกลมที่อยู่กึ่งกลางพร้อมสีที่กำหนด XML ดิบจะมีลักษณะดังนี้:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg width="100px" height="100px" viewBox="0 0 100 100"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40"
          fill="lightcoral" stroke="black" stroke-width="2"/>
</svg>
```

เนื่องจาก SVG เป็นเวกเตอร์, คุณสามารถปรับขนาดภาพได้โดยไม่สูญเสียคุณภาพ, ทำให้เหมาะกับการออกแบบเว็บที่ตอบสนองหรือการพิมพ์ความละเอียดสูง

## เคล็ดลับพิเศษ: ส่งออก SVG เป็น PNG หรือ JPEG

หากต้องการเวอร์ชันเรสเตอร์, ผสานไฟล์ SVG กับเครื่องมือแปลงเช่น **CairoSVG**:

```python
# Optional: Convert SVG to PNG
# pip install cairosvg
import cairosvg

cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

ขั้นตอนนี้แสดงการ **ส่งออกภาพ SVG** ไปเป็นรูปแบบบิตแมป, มีประโยชน์เมื่อระบบ downstream ไม่สามารถเรนเดอร์ SVG ได้โดยตรง

## ความแตกต่างทั่วไปและกรณีขอบ

| Variation | How to handle |
|-----------|---------------|
| Multiple shapes | Call `dwg.add()` for each new element (rect, line, path). |
| Dynamic dimensions | Compute `size` and `viewBox` from data before creating `Drawing`. |
| Text labels | Use `dwg.text("Label", insert=("10", "20"))` and style with `font_size` and `fill`. |
| Re‑using the document | Keep the `Drawing` object in memory and call `save()` whenever you need an updated file. |
| Large files | Stream the output using `dwg.tostring()` and write to a file object manually to avoid memory spikes. |

การจัดการกับสถานการณ์เหล่านี้ช่วยให้สคริปต์ **วิธีสร้าง SVG** ของคุณขยายจากไอคอนง่าย ๆ ไปจนถึงไดอะแกรมซับซ้อน

## สรุปสคริปต์เต็ม

ด้านล่างเป็นตัวอย่างที่ทำงานได้ครบถ้วนซึ่งรวมทุกขั้นตอนและการแปลงแบบเลือกได้:

```python
# Full SVG creation script – create SVG document, save SVG to file, export SVG image
import svgwrite
import cairosvg  # Optional, only needed for PNG conversion

# Initialize the drawing (SVG document)
dwg = svgwrite.Drawing(
    filename="circle.svg",
    size=("100px", "100px"),
    viewBox=("0 0 100 100")
)

# Define a circle element
circle = dwg.circle(
    center=("50", "50"),
    r="40",
    fill="lightcoral",
    stroke="black",
    stroke_width="2"
)

# Add the circle to the document
dwg.add(circle)

# Save the SVG file
dwg.save()
print("SVG file saved as circle.svg")

# Optional: convert SVG to PNG (export SVG image)
cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

การรันสคริปต์นี้จะสร้าง `circle.svg` และหากติดตั้ง `cairosvg` แล้ว จะสร้าง `circle.png` ทั้งสองไฟล์พร้อมใช้ในหน้าเว็บ, รายงาน, หรือการประมวลผลต่อไป

## สรุป

คุณได้เรียนรู้วิธี **สร้างเอกสาร SVG** ด้วย Python, **บันทึก SVG ลงไฟล์**, และ **ส่งออกภาพ SVG** เพื่อการใช้งานที่กว้างขวาง ตัวอย่างครอบคลุมการเรียก API พื้นฐาน, อธิบายเหตุผลของแต่ละขั้นตอน, และเสนอส่วนขยายสำหรับกราฟิกที่ซับซ้อนยิ่งขึ้น

ต่อไป, สำรวจหัวข้อ **SVG Python tutorial** เพิ่มเติม เช่น การวาดเส้นทาง, การใช้กราเดียนต์, และการทำแอนิเมชัน การผสานเทคนิคเหล่านี้จะทำให้คุณสร้างกราฟิกเวกเตอร์เชิงข้อมูลโดยตรงจากแอปพลิเคชัน Python ของคุณ Happy coding!

## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโปรเจกต์ของคุณ

- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}