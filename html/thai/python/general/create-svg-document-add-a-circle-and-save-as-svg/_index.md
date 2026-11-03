---
category: general
date: 2026-07-31
description: เรียนรู้วิธีสร้างเอกสาร SVG, เพิ่มวงกลม, และบันทึกไฟล์ SVG อย่างรวดเร็ว
  ส่งออกกราฟิกเป็น SVG ด้วยโค้ด Python เพียงไม่กี่บรรทัด
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg document
- save svg file
- export graphic as svg
- add circle to svg
language: th
lastmod: 2026-07-31
og_description: สร้างเอกสาร SVG, เพิ่มวงกลม, และบันทึกไฟล์ SVG ภายในไม่กี่วินาที คู่มือนี้จะแสดงวิธีส่งออกกราฟิกเป็น
  SVG ด้วยโค้ดที่ชัดเจนและสามารถรันได้
og_image_alt: Screenshot of a red circle inside an SVG file named circle.svg
og_title: สร้างเอกสาร SVG – เพิ่มวงกลมและบันทึกเป็น SVG
schemas:
- author: Aspose
  dateModified: '2026-07-31'
  description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  headline: Create SVG Document – Add a Circle and Save as SVG
  type: TechArticle
- description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  name: Create SVG Document – Add a Circle and Save as SVG
  steps:
  - name: Pro tip
    text: If you plan to generate many files in a loop, give each `Drawing` a unique
      name or use `io.BytesIO` to keep everything in memory until you’re ready to
      write.
  - name: Edge case – Transparent background
    text: 'If you need a transparent background (the default for SVG), you can skip
      setting a `fill` on the root. For a white background, add:'
  - name: 'Bonus: Export graphic as SVG programmatically'
    text: 'If you need the SVG content as a string—for example, to embed it in an
      HTML email—you can call `dwg.tostring()` instead of `save()`:'
  type: HowTo
- questions:
  - answer: Swap `dwg.circle` for `dwg.rect`, `dwg.ellipse`, or even a custom `<path>`
      string. The API is consistent across shapes.
    question: What if I want a different shape?
  - answer: Absolutely. The file you just created can be referenced with `<img src="circle.svg"
      alt="Red circle">` or inlined with `<svg>` tags.
    question: Can I embed the SVG directly in HTML?
  - answer: You could, but libraries like `svgwrite` handle namespace quirks and make
      the code far more maintainable—especially when you start adding gradients or
      animations.
    question: Why not write raw XML?
  type: FAQPage
tags:
- svg
- python
- vector-graphics
- programming-tutorial
title: สร้างเอกสาร SVG – เพิ่มวงกลมและบันทึกเป็น SVG
url: /th/python/general/create-svg-document-add-a-circle-and-save-as-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้างเอกสาร SVG – เพิ่มวงกลมและบันทึกเป็น SVG

เคยต้อง **สร้างเอกสาร SVG** จากโค้ดแต่ไม่รู้จะเริ่มจากตรงไหนหรือไม่? คุณไม่ได้เป็นคนเดียว; นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อลองทำงานกับกราฟิกเวกเตอร์เป็นครั้งแรก ในบทเรียนนี้เราจะเดินผ่านตัวอย่างขนาดเล็กที่ทำงานได้เองซึ่งจะแสดงวิธี **เพิ่มวงกลมลงใน SVG**, แล้ว **บันทึกไฟล์ SVG** เพื่อที่คุณจะ **ส่งออกกราฟิกเป็น SVG** สำหรับใช้บนเว็บหรือในเครื่องมือออกแบบ

เราจะทำให้มันเบา ๆ: เพียงไม่กี่บรรทัดของ Python, ไลบรารีช่วยเหลือ SVG ที่เป็นที่นิยม, และคำอธิบายสั้น ๆ เมื่อเสร็จคุณจะมีไฟล์ `circle.svg` พร้อมใช้งานในโฟลเดอร์ของคุณ และคุณจะเข้าใจว่าทำไมแต่ละขั้นตอนถึงสำคัญ—ไม่มีการอ้างอิง “ดูเอกสาร” ที่คลุมเครือ

## สิ่งที่คุณต้องเตรียม

- Python 3.8+ (เวอร์ชันล่าสุดใดก็ได้)
- แพคเกจ `svgwrite` – ติดตั้งด้วย `pip install svgwrite`
- โปรแกรมแก้ไขข้อความหรือ IDE (VS Code, PyCharm, หรือแม้แต่ Notepad ก็ใช้ได้)
- สิทธิ์การเขียนในไดเรกทอรีที่คุณต้องการบันทึกไฟล์

เท่านี้เอง ไม่มีการพึ่งพาไลบรารีหนัก ๆ หรือบริการภายนอก

## ขั้นตอนที่ 1: ตั้งค่าเอกสาร SVG

การสร้างเอกสาร SVG ทำได้ง่ายเพียงการสร้างอ็อบเจกต์ `Drawing` จาก `svgwrite` คิดว่าอ็อบเจกต์นี้เป็นผืนผ้าใบเปล่าที่ทุกรูปทรงจะอาศัยอยู่

```python
import svgwrite

# Step 1: Create a new SVG document (canvas) 800×800 pixels
dwg = svgwrite.Drawing(filename="circle.svg", size=("200px", "200px"))
```

> **ทำไมขั้นตอนนี้สำคัญ:** คลาส `Drawing` จัดการส่วนหัว XML ทั้งหมดให้คุณ—namespaces, headers, และอิลิเมนต์ราก `<svg>` โดยการระบุชื่อไฟล์ล่วงหน้า เรารู้แล้วว่าไฟล์จะถูกบันทึกที่ไหน ทำให้ขั้นตอน **บันทึกไฟล์ SVG** ต่อไปเป็นเรื่องง่าย

### เคล็ดลับพิเศษ
หากคุณวางแผนจะสร้างไฟล์หลายไฟล์ในลูป ให้ตั้งชื่อ `Drawing` ให้เป็นเอกลักษณ์หรือใช้ `io.BytesIO` เพื่อเก็บทั้งหมดในหน่วยความจำจนกว่าจะพร้อมเขียน

## ขั้นตอนที่ 2: เพิ่มวงกลมลงใน SVG

เมื่อเอกสารพร้อมแล้ว เรามา **เพิ่มวงกลมลงใน SVG** กัน `add()` เมธอดรับอ็อบเจกต์รูปทรงใดก็ได้; `Circle` เหมาะสำหรับจุดสีแดงง่าย ๆ ที่ศูนย์กลาง

```python
# Step 2: Add a red circle element to the SVG root
center = (100, 100)          # x, y coordinates (half of 200px canvas)
radius = 80                  # radius in pixels
circle = dwg.circle(center=center, r=radius, fill='red')
dwg.add(circle)
```

> **ทำไมเราถึงใช้ตัวแปร `center` และ `radius`:** การกำหนดค่าตัวเลขโดยตรงทำให้โค้ดอ่านและบำรุงรักษายาก การตั้งชื่อค่าช่วยให้เจตนาชัดเจน—วงกลมนี้อยู่ตรงกลางของผืนผ้า 200 × 200 และใหญ่พอที่จะมองเห็นได้

### กรณีขอบ – พื้นหลังโปร่งใส
หากต้องการพื้นหลังโปร่งใส (ค่าเริ่มต้นของ SVG) คุณสามารถข้ามการตั้งค่า `fill` ที่รูทได้ หากต้องการพื้นหลังสีขาว ให้เพิ่ม:

```python
dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))
```

วางโค้ดนี้ก่อนเพิ่มวงกลมเพื่อให้สี่เหลี่ยมอยู่ด้านล่าง

## ขั้นตอนที่ 3: บันทึกไฟล์ SVG

เมื่อรูปทรงพร้อม ขั้นตอนสุดท้ายคือ **บันทึกไฟล์ SVG** เมธอด `save()` จะเขียน XML ลงดิสก์ และเพราะเราได้ตั้งชื่อไฟล์ให้ `Drawing` ไว้แล้ว การเรียกครั้งเดียวก็ทำงานเสร็จ

```python
# Step 3: Save the SVG document to a file
dwg.save()
print("✅ circle.svg has been created in the current directory.")
```

> **เกิดอะไรขึ้นเบื้องหลัง?** `svgwrite` ทำการแปลงต้นไม้ของอิลิเมนต์เป็นสตริง, เพิ่มประกาศ XML, แล้วเขียนไฟล์ด้วยการเข้ารหัส UTF‑8 หากไดเรกทอรีเป้าหมายไม่มีอยู่ Python จะโยน `FileNotFoundError`; ตรวจสอบว่าเส้นทางถูกต้องหรือสร้างด้วย `os.makedirs()`

### โบนัส: ส่งออกกราฟิกเป็น SVG ผ่านโปรแกรม

หากต้องการเนื้อหา SVG เป็นสตริง—เช่น เพื่อนำไปฝังในอีเมล HTML—คุณสามารถเรียก `dwg.tostring()` แทน `save()` ได้:

```python
svg_content = dwg.tostring()
# Now you can send svg_content over a network, store it in a DB, etc.
```

## ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือสคริปต์ที่พร้อมรันทั้งหมด:

```python
import svgwrite
import os

def create_svg_with_circle(output_path: str):
    """
    Creates an SVG file containing a single red circle.
    Parameters
    ----------
    output_path: str
        Full path where the SVG file will be saved.
    """
    # Ensure the directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Initialise the SVG document (800×800 canvas)
    dwg = svgwrite.Drawing(filename=output_path, size=("200px", "200px"))

    # Optional: add a white background rectangle
    dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))

    # Add a red circle in the centre
    center = (100, 100)
    radius = 80
    circle = dwg.circle(center=center, r=radius, fill='red')
    dwg.add(circle)

    # Save the file – this is the key step to **save svg file**
    dwg.save()
    print(f"✅ SVG saved to {output_path}")

if __name__ == "__main__":
    # Change this path to wherever you want the file
    output_file = os.path.join(os.getcwd(), "circle.svg")
    create_svg_with_circle(output_file)
```

**ผลลัพธ์ที่คาดหวัง:** หลังจากรันสคริปต์ คุณจะเห็นไฟล์ `circle.svg` อยู่ในโฟลเดอร์เดียวกัน การเปิดไฟล์ในเบราว์เซอร์หรือโปรแกรมแก้ไขเวกเตอร์จะแสดงวงกลมสีแดงอยู่กึ่งกลางสี่เหลี่ยมสีขาว—ตรงกับที่เราเขียนโค้ดไว้

## คำถามที่พบบ่อยและข้อควรระวัง

- **อยากใช้รูปทรงอื่น?** แทนที่ `dwg.circle` ด้วย `dwg.rect`, `dwg.ellipse` หรือแม้แต่สตริง `<path>` ที่กำหนดเอง API มีความสอดคล้องกันในทุกรูปทรง
- **สามารถฝัง SVG ลงใน HTML ได้โดยตรงหรือไม่?** แน่นอน ไฟล์ที่คุณสร้างสามารถอ้างอิงด้วย `<img src="circle.svg" alt="Red circle">` หรือฝังโดยตรงด้วยแท็ก `<svg>`
- **ทำไมไม่เขียน XML ดิบ?** คุณทำได้, แต่ไลบรารีอย่าง `svgwrite` จัดการเรื่อง namespace และทำให้โค้ดดูแลรักษาง่ายกว่า—โดยเฉพาะเมื่อเริ่มเพิ่มกราเดียนต์หรือแอนิเมชัน

## สรุป

ตอนนี้คุณรู้วิธี **สร้างเอกสาร SVG**, **เพิ่มวงกลมลงใน SVG**, และ **บันทึกไฟล์ SVG** เพื่อที่คุณจะ **ส่งออกกราฟิกเป็น SVG** ด้วยเพียงไม่กี่บรรทัดของ Python รูปแบบนี้สามารถขยายได้: แทนที่วงกลมด้วยรูปเวกเตอร์ใดก็ได้, วนลูปข้อมูลเพื่อสร้างแผนภูมิ, หรือประมวลผลไฟล์หลาย ๆ ไฟล์สำหรับระบบออกแบบ

ขั้นตอนต่อไป? ลองเพิ่มข้อความอธิบาย, ทดลองกราเดียนต์, หรือสร้างแกลเลอรีไอคอนทั้งหมดในสคริปต์เดียว หากสนใจฟีเจอร์ขั้นสูงเพิ่มเติม ให้ดูเอกสาร `svgwrite` เกี่ยวกับกลุ่ม (`<g>`), การแปลง, และการสนับสนุนแอนิเมชัน

ขอให้สนุกกับการเขียนโค้ด, และขอให้เวกเตอร์ของคุณคมชัดเสมอ!

## สิ่งที่คุณควรเรียนต่อ

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้ในโปรเจกต์ของคุณเอง

- [บันทึกเอกสาร SVG ใน Aspose.HTML สำหรับ Java](/html/english/java/saving-html-documents/save-svg-document/)
- [สร้างและจัดการเอกสาร SVG ใน Aspose.HTML สำหรับ Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – แปลง SVG เป็นภาพด้วย Aspose.HTML สำหรับ Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}