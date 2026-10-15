---
category: general
date: 2026-10-15
description: เรียนรู้วิธีสร้างตัวเลือกการจัดการทรัพยากรและวิธีตั้งค่าความลึกสูงสุดของการจัดการสำหรับการบันทึก
  Markdown ใน Python ตามคู่มือแบบทีละขั้นตอน.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to set max handling depth
language: th
lastmod: 2026-10-15
og_description: สร้างตัวเลือกการจัดการทรัพยากรใน Python เพื่อควบคุมการประมวลผลทรัพยากรแบบซ้อนกัน
  บทเรียนนี้แสดงวิธีตั้งค่าความลึกการจัดการสูงสุดสำหรับการส่งออก Markdown ที่เชื่อถือได้
og_image_alt: Screenshot showing Python code to create resource handling options and
  set max handling depth
og_title: สร้างตัวเลือกการจัดการทรัพยากร – คู่มือ Python
schemas:
- author: Aspose
  dateModified: '2026-10-15'
  description: Learn how to create resource handling options and how to set max handling
    depth for Markdown saving in Python. Follow a step‑by‑step guide.
  headline: How to create resource handling options with Python
  type: TechArticle
tags:
- resource handling
- Markdown
- Python
- options
title: วิธีสร้างตัวเลือกการจัดการทรัพยากรด้วย Python
url: /th/python/general/how-to-create-resource-handling-options-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้างตัวเลือกการจัดการทรัพยากรด้วย Python

หากคุณต้องการ **สร้างตัวเลือกการจัดการทรัพยากร** สำหรับการส่งออกเป็น Markdown คู่มือนี้จะให้วิธีแก้ไขที่ครบถ้วน คุณจะได้เห็นอย่างชัดเจน **วิธีตั้งค่าความลึกสูงสุดของการจัดการ** เพื่อให้ทรัพยากรที่ซ้อนกันหยุดการประมวลผลหลังจากระดับที่ต้องการ

การจัดการทรัพยากรเป็นสิ่งสำคัญเมื่อคุณสร้าง Markdown จากเอกสารที่ซับซ้อนซึ่งมีรูปภาพ, ไฟล์ฝัง, หรือทรัพยากรที่เชื่อมโยงอื่น ๆ การทำซ้ำโดยไม่มีการควบคุมอาจทำให้เกิดปัญหาด้านประสิทธิภาพหรือข้อผิดพลาด out‑of‑memory การกำหนดค่าความลึกของการจัดการช่วยให้กระบวนการคาดเดาได้และมีประสิทธิภาพ

ในบทเรียนนี้คุณจะได้:

* เริ่มต้นสร้างอ็อบเจกต์ `ResourceHandlingOptions`
* กำหนดค่าความลึกสูงสุดของการจัดการ
* แนบตัวเลือกเหล่านั้นไปยังอินสแตนซ์ `MarkdownSaveOptions`
* รันตัวอย่างเต็มที่คุณสามารถคัดลอกไปใช้ในโปรเจกต์ของคุณได้

ไม่จำเป็นต้องใช้ไลบรารีภายนอกใด ๆ นอกเหนือจาก SDK มาตรฐาน และโค้ดทำงานกับเวอร์ชันล่าสุดของแพคเกจ Python ณ เดือนตุลาคม 2026

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน โปรดตรวจสอบว่าคุณมี:

* ติดตั้ง Python 3.9 หรือใหม่กว่า
* SDK ที่ให้บริการ `ResourceHandlingOptions` และ `MarkdownSaveOptions` (เช่น `groupdocs-viewer` หรือแพคเกจที่คล้ายกัน) ติดตั้งด้วยคำสั่ง:

```bash
pip install groupdocs-viewer
```

* ความคุ้นเคยพื้นฐานกับคลาสและแอตทริบิวต์ของอ็อบเจกต์ใน Python

## ขั้นตอนที่ 1: สร้างตัวเลือกการจัดการทรัพยากร

ขั้นตอนแรกคือ **สร้างตัวเลือกการจัดการทรัพยากร** อ็อบเจกต์นี้ทำหน้าที่เป็นคอนเทนเนอร์สำหรับการตั้งค่าที่เกี่ยวข้องกับทรัพยากรทั้งหมด

```python
from groupdocs.viewer import ResourceHandlingOptions, MarkdownSaveOptions

# Step 1: Instantiate the options object
resource_options = ResourceHandlingOptions()
```

`ResourceHandlingOptions` ไม่ได้กำหนดขีดจำกัดใด ๆ โดยค่าเริ่มต้น ซึ่งหมายความว่า viewer จะตามทุกทรัพยากรที่เชื่อมโยงที่พบ การเริ่มต้นอ็อบเจกต์ให้คุณมีพื้นฐานที่สะอาดเพื่อใช้ควบคุมอย่างแม่นยำ

## ขั้นตอนที่ 2: วิธีตั้งค่าความลึกสูงสุดของการจัดการ

ต่อไปคุณจะได้เรียนรู้ **วิธีตั้งค่าความลึกสูงสุดของการจัดการ** คุณสมบัติ `max_handling_depth` กำหนดจำนวนระดับที่ซ้อนกันที่ตัวส่งออกจะประมวลผลก่อนหยุด

```python
# Step 2: Limit the handling depth to five levels
resource_options.max_handling_depth = 5
```

ทำไมต้องจำกัดความลึก? ลองนึกถึงเอกสาร Markdown ที่อ้างอิงไฟล์ Markdown อื่น ซึ่งต่อมามีการอ้างอิงไฟล์ที่สาม และต่อไป หากไม่มีการจำกัดความลึก ตัวส่งออกอาจทำซ้ำอย่างไม่สิ้นสุด ทำให้ใช้หน่วยความจำและ CPU มาก การตั้งค่า `max_handling_depth` เป็น `5` จะบอกให้เครื่องยนต์หยุดหลังจากประมวลผลทรัพยากรซ้อนกันห้าระดับ ซึ่งเป็นค่าเริ่มต้นที่ปลอดภัยสำหรับโปรเจกต์ส่วนใหญ่

### กรณีขอบ: ความลึกไม่จำกัด

หากคุณต้องการให้การทำซ้ำไม่มีขีดจำกัดโดยเจตนา (หายากในสภาพการผลิต) ให้ตั้งค่าเป็น `None`:

```python
resource_options.max_handling_depth = None  # No limit
```

ควรระวังว่าความลึกไม่จำกัดอาจทำให้ประสิทธิภาพลดลงอย่างมากเมื่อทำงานกับต้นไม้เอกสารขนาดใหญ่มาก

## ขั้นตอนที่ 3: แนบตัวเลือกไปยัง MarkdownSaveOptions

หลังจากกำหนดค่าการจัดการทรัพยากรแล้ว คุณต้องแนบตัวเลือกเหล่านั้นไปยังอินสแตนซ์ `MarkdownSaveOptions` ซึ่งจะบอกตัวส่งออกให้ใช้การตั้งค่าเหล่านี้เมื่อบันทึก

```python
# Step 3: Create MarkdownSaveOptions and attach the resource handling config
markdown_options = MarkdownSaveOptions()
markdown_options.resource_handling_options = resource_options
```

`MarkdownSaveOptions` รวมการตั้งค่าที่เกี่ยวข้องกับการส่งออกทั้งหมด โดยการกำหนด `resource_options` ให้กับแอตทริบิวต์ `resource_handling_options` ของมัน คุณจะทำให้แน่ใจว่าขีดจำกัดความลึกถูกบังคับใช้ระหว่างการแปลง

## ขั้นตอนที่ 4: รันการแปลงแบบเต็ม (สาธิตเสริม)

โค้ดส่วนนี้แสดงการแปลงเต็มจากเอกสารตัวอย่างเป็น Markdown โดยใช้ตัวเลือกที่คุณสร้างขึ้น ปรับเส้นทางไฟล์ให้ตรงกับสภาพแวดล้อมของคุณ

```python
from groupdocs.viewer import Viewer

# Path to the source document (e.g., a DOCX with embedded images)
source_path = "sample.docx"
# Path where the Markdown output will be saved
output_path = "output.md"

# Initialize the viewer with the source file
viewer = Viewer(source_path)

# Perform the conversion using the configured options
viewer.save(output_path, markdown_options)

print(f"Conversion complete. Markdown saved to {output_path}")
```

**ผลลัพธ์ที่คาดหวัง**

```
Conversion complete. Markdown saved to output.md
```

หลังจากรันสคริปต์แล้ว เปิดไฟล์ `output.md` คุณจะเห็นว่ารูปภาพและทรัพยากรอื่น ๆ ถูกอ้างอิงถึงระดับห้าระดับลึก; ลิงก์ที่ลึกกว่านั้นจะถูกละเว้น เพื่อป้องกันการทำซ้ำที่ไม่สิ้นสุด

## เคล็ดลับพิเศษ: ตรวจสอบความลึกของการจัดการในระหว่างรันไทม์

หากต้องการยืนยันว่าขีดจำกัดความลึกถูกนำไปใช้ คุณสามารถตรวจสอบ Markdown ที่สร้างขึ้นเพื่อหาการอ้างอิงทรัพยากรที่หายไป หรือเปิดการบันทึกแบบละเอียดใน SDK:

```python
viewer.set_logging(True)  # Enable detailed logs
```

บันทึกจะแสดงข้อความเช่น:

```
[INFO] Resource handling stopped at depth 5 for file 'nested_image.png'
```

## คำถามที่พบบ่อย

**ถ้าเอกสารของฉันมีทรัพยากรซ้อนกันน้อยกว่าห้าระดับจะเป็นอย่างไร?**  
ตัวส่งออกจะประมวลผลทรัพยากรทั้งหมดที่มีอยู่ เนื่องจากขีดจำกัดความลึกสูงกว่าความลึกจริง ไม่มีทรัพยากรใดถูกตัดทอน

**ฉันสามารถตั้งค่าขีดจำกัดที่แตกต่างสำหรับประเภทไฟล์ต่าง ๆ ได้หรือไม่?**  
ได้. สร้างอ็อบเจกต์ `ResourceHandlingOptions` แยกต่างหากสำหรับแต่ละรูปแบบการส่งออกและกำหนดให้กับอินสแตนซ์ `SaveOptions` ที่สอดคล้องกัน

**ขีดจำกัดความลึกมีผลต่อเฉพาะรูปภาพหรือไม่?**  
ไม่. ขีดจำกัดนี้ใช้กับ *ทุก* ทรัพยากรที่ตัวส่งออกสามารถตามได้ รวมถึงไฟล์ฝัง, ไฮเปอร์ลิงก์, และการรวม Markdown ที่ซ้อนกัน

## สรุป

คุณได้เรียนรู้วิธี **สร้างตัวเลือกการจัดการทรัพยากร** และ **ตั้งค่าความลึกสูงสุดของการจัดการ** สำหรับการส่งออก Markdown ที่เชื่อถือได้ใน Python การจำกัดการทำซ้ำช่วยปกป้องแอปพลิเคชันของคุณจากการใช้หน่วยความจำมากเกินไปในขณะที่ยังคงรักษาโครงสร้างเนื้อหาที่จำเป็นไว้

ขั้นตอนต่อไปที่คุณอาจสำรวจ:

* ปรับคุณสมบัติอื่น ๆ ของ `ResourceHandlingOptions` เช่น `extract_images` หรือ `preserve_links`
* ผสานการจัดการทรัพยากรกับแนวทางการตั้งชื่อไฟล์ที่กำหนดเองสำหรับไฟล์ที่สกัดออก
* ทดลองค่าความลึกต่าง ๆ เพื่อค้นหาจุดที่เหมาะสมที่สุดสำหรับชุดเอกสารของคุณ

อย่าลังเลที่จะแก้ไขโค้ดสแนปเพื่อตรงกับเวิร์กโฟลว์ของคุณและแบ่งปันผลการทดลองกับชุมชน ขอให้เขียนโค้ดอย่างสนุกสนาน!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้แบบต่าง ๆ ในโปรเจกต์ของคุณเอง

- [วิธีบันทึก HTML ใน C# – คู่มือฉบับสมบูรณ์โดยใช้ตัวจัดการทรัพยากรแบบกำหนดเอง](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [วิธีบีบอัด HTML ใน C# – บทเรียนตัวจัดการทรัพยากรแบบกำหนดเอง](/html/english/net/html-extensions-and-conversions/how-to-zip-html-in-c-custom-resource-handler-tutorial/)
- [วิธีสร้างตัวจัดการสคีมาที่กำหนดเองด้วย Aspose.HTML สำหรับ Java](/html/english/java/custom-schema-message-handling/custom-schema-message-handler/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}