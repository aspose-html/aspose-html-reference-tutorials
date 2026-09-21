---
date: 2026-03-24
description: 'เรียนรู้วิธีตั้งค่าสีพื้นหลังของภาพ, ขนาดหน้ากำหนดเอง, และแปลง EPUB
  เป็นภาพโดยใช้ Aspose.HTML สำหรับ Java. #JavaDevelopment #WebDevelopment #DocumentConversion'
linktitle: Specifying Image Save Options for EPUB to Image Conversion
second_title: Java HTML Processing with Aspose.HTML
title: ตั้งค่าสีพื้นหลังของภาพสำหรับการแปลง EPUB เป็นภาพ
url: /th/java/converting-epub-to-pdf/convert-epub-to-image-specify-image-save-options/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตั้งค่าสีพื้นหลังของภาพสำหรับการแปลง EPUB เป็นภาพ

ในกระบวนการทำงานของเว็บและเอกสารสมัยใหม่ **Aspose.HTML for Java** ให้คุณสามารถแปลงอี‑บุ๊คเช่น EPUB เป็นภาพเรสเตอร์ พร้อมให้คุณควบคุมผลลัพธ์ภาพได้อย่างเต็มที่ โดยการใช้ตัวเลือก **set image background color** ร่วมกับ **custom page size** คุณสามารถสร้างภาพที่ตรงกับส่วนประกอบ UI, การจัดหน้าแบบพิมพ์, หรือข้อกำหนดการประมวลผลต่อเนื่องใด ๆ ได้อย่างสมบูรณ์แบบ ในคู่มือนี้เราจะพาคุณผ่านกระบวนการทั้งหมด—from prerequisites ไปจนถึงการแปลงขั้นสุดท้าย—เพื่อให้คุณ **convert EPUB to image** ได้อย่างมั่นใจ

## คำตอบด่วน
- **“custom page size” มีผลอย่างไร?** จะกำหนดความกว้างและความสูงของภาพที่สร้างขึ้นเป็นพิกเซล  
- **ฉันสามารถแปลง EPUB ไปเป็นรูปแบบใดได้บ้าง?** รูปแบบภาพใด ๆ ที่ `ImageSaveOptions` รองรับ เช่น JPEG, PNG หรือ BMP  
- **ฉันจะตั้งค่าสีพื้นหลังของภาพอย่างไร?** ใช้ `options.setBackgroundColor(Color.getAliceBlue())` (หรือ `Color` ใด ๆ ที่ต้องการ)  
- **ฉันต้องมีไลเซนส์สำหรับการพัฒนาหรือไม่?** เวอร์ชันทดลองฟรีใช้ได้สำหรับการประเมิน; ต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานจริง  
- **ต้องใช้ Java เวอร์ชันใด?** Java 8 หรือสูงกว่า พร้อมไลบรารี Aspose.HTML for Java  

## “set image background color” คืออะไร?
การตั้งค่าสีพื้นหลังของภาพบอกให้เอนจินการเรนเดอร์รู้ว่าจะเติมสีใดบนแคนวาสก่อนที่จะวาดเนื้อหาของหน้า ซึ่งมีประโยชน์เป็นพิเศษเมื่อ EPUB ต้นฉบับมีองค์ประกอบที่โปร่งใสหรือเมื่อคุณต้องการพื้นหลังสีเดียวสำหรับทุกหน้า

## วิธีตั้งค่าสีพื้นหลังของภาพและขนาดหน้ากำหนดเองใน Java?
ต่อไปนี้เป็นขั้นตอนที่คุณต้องทำตาม แต่ละขั้นจะมีคำอธิบายสั้น ๆ ตามด้วยโค้ดตัวอย่างที่ต้องใช้ (โค้ดจะไม่เปลี่ยนแปลงจากบทแนะนำต้นฉบับ)

### Prerequisites
ก่อนเริ่มทำงาน โปรดตรวจสอบว่าคุณมี:

1. **Java Development Environment** – ติดตั้ง JDK 8 หรือใหม่กว่า  
2. **Aspose.HTML for Java** – ดาวน์โหลดไลบรารีจากเว็บไซต์อย่างเป็นทางการ [ที่นี่](https://releases.aspose.com/html/java/)  
3. **Code Editor** – IntelliJ IDEA, Eclipse, VS Code หรือ IDE ใด ๆ ที่คุณชอบ  
4. **Basic Java Knowledge** – ความคุ้นเคยกับไวยากรณ์ Java และการตั้งค่าโปรเจกต์  
5. **Enthusiasm** – พร้อมสำรวจขนาดหน้ากำหนดเองและตัวเลือกการบันทึกภาพอื่น ๆ  

เมื่อคุณพร้อมแล้ว ไปยังขั้นตอนการทำงานต่อไป

## Import Packages

ก่อนอื่นให้ import คลาสที่จำเป็นสำหรับการเรนเดอร์และการแปลง

### Step 1: Import Aspose.HTML Classes

```java
import com.aspose.html.saving.ImageSaveOptions;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.drawing.Page;
import com.aspose.html.drawing.Size;
import com.aspose.html.drawing.Length;
import com.aspose.html.drawing.Color;
import com.aspose.html.converters.Converter;
```

การ import เหล่านี้ทำให้คุณเข้าถึง `ImageSaveOptions`, วัตถุการจัดหน้า, และยูทิลิตี้ `Converter`

## Example Breakdown: Converting EPUB to Image

ต่อไปนี้เป็นการเดินผ่านขั้นตอนอย่างละเอียดของ **วิธีแปลง EPUB** พร้อมกับการใช้ **custom page size** และ **set image background color**  

### Step 2: Open the EPUB File

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
```

`FileInputStream` จะอ่านไฟล์ EPUB ต้นฉบับ แทนที่ `"input.epub"` ด้วยพาธของไฟล์ของคุณเอง

### Step 3: Initialize ImageSaveOptions with Custom Page Size

```java
ImageSaveOptions options = new ImageSaveOptions(ImageFormat.Jpeg);
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
Size size = new Size(Length.fromPixels(3000), Length.fromPixels(1000));
anyPage.setSize(size);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

- **Custom Page Size**: `Size` ถูกสร้างด้วยความกว้าง 3000 px และความสูง 1000 px ปรับค่าตามความต้องการของการจัดหน้า  
- **Set Image Background Color**: `Color.getAliceBlue()` เติมแคนวาสด้วยสีฟ้าอ่อน; คุณสามารถเปลี่ยนเป็น `Color` ใดก็ได้ เช่น `Color.getTransparent()` สำหรับความโปร่งใสของ PNG  

### Step 4: Convert EPUB to Image

```java
Converter.convertEPUB(fileInputStream, options, Resources.output("output.jpg"));
```

เมธอด `convertEPUB` จะทำการแปลงโดยใช้ `options` ที่กำหนด ผลลัพธ์จะถูกบันทึกเป็น `output.jpg`

> **Pro tip:** หากต้องการ **epub to png conversion** ให้สร้าง `ImageSaveOptions` ด้วย `ImageFormat.Png` แทน `ImageFormat.Jpeg`

ยินดีด้วย! คุณได้ **convert epub to image** สำเร็จโดยควบคุมขนาดหน้าและสีพื้นหลังได้ตามต้องการ

## How to set page size (custom page size java) – deeper dive
หากต้องการขนาดหน้าที่แตกต่างกันสำหรับแต่ละ EPUB คุณสามารถคำนวณมิติแบบไดนามิกจาก CSS หรือเมตาดาต้าของเนื้อหาได้ วัตถุ `PageSetup` สามารถนำกลับมาใช้ใหม่ได้หลายการแปลง; เพียงปรับ `Size` ก่อนเรียก `Converter.convertEPUB` ทุกครั้ง

## Common Issues and Solutions

| Issue | Reason | Fix |
|-------|--------|-----|
| ภาพที่ได้ถูกตัด | ขนาดหน้ากำหนดเองเล็กกว่าขนาดเนื้อหา | เพิ่มความกว้าง/ความสูงใน `Size` หรือเปิด `options.setFitToPage(true)` |
| พื้นหลังเป็นสีดำ | ไม่ได้ตั้งค่า Color หรือรูปแบบไม่รองรับ | ตรวจสอบให้แน่ใจว่าได้เรียก `options.setBackgroundColor(...)` ก่อนการแปลง |
| การแปลงล้มเหลวด้วย `NullPointerException` | ไฟล์ `Resources.input` หายไป | ตรวจสอบพาธและยืนยันว่าไฟล์ EPUB มีอยู่จริง |

## Frequently Asked Questions (FAQs)

### 1. ฉันจะหาเอกสาร Aspose.HTML for Java ได้จากที่ไหน?
คุณสามารถเข้าถึงเอกสารได้ [ที่นี่](https://reference.aspose.com/html/java/) ซึ่งให้ข้อมูลและตัวอย่างอย่างครบถ้วนเพื่อช่วยให้คุณเริ่มต้นได้เร็ว

### 2. มีเวอร์ชันทดลองฟรีของ Aspose.HTML for Java หรือไม่?
มีครับ คุณสามารถดาวน์โหลดเวอร์ชันทดลองฟรี [ที่นี่](https://releases.aspose.com/) เพื่อสำรวจความสามารถของไลบรารีก่อนตัดสินใจซื้อ

### 3. ฉันจะขอรับไลเซนส์ชั่วคราวสำหรับ Aspose.HTML for Java ได้อย่างไร?
หากต้องการไลเซนส์ชั่วคราว คุณสามารถขอรับได้ [ที่นี่](https://purchase.aspose.com/temporary-license/)

### 4. Aspose.HTML for Java รองรับการแปลงเอกสารประเภทอื่นได้หรือไม่?
รองรับการแปลงหลายรูปแบบ รวมถึง HTML → PDF, HTML → image และอื่น ๆ อีกมาก

### 5. Aspose.HTML for Java เหมาะกับทั้งผู้เริ่มต้นและนักพัฒนาที่มีประสบการณ์หรือไม่?
แน่นอน! ผู้เริ่มต้นสามารถเริ่มต้นด้วยตัวอย่างง่าย ๆ ส่วนผู้ใช้ระดับสูงสามารถใช้ API เต็มรูปแบบสำหรับเวิร์กโฟลว์ที่ซับซ้อนได้

**Additional Q&A**

**Q: ฉันสามารถแปลงหลายหน้า EPUB เป็นภาพแยกกันได้หรือไม่?**  
A: ได้ ใช้ลูปวนตามดัชนีหน้า ปรับ `options.setPageSetup(pageSetup)` สำหรับแต่ละหน้า แล้วเรียก `Converter.convertEPUB` ซ้ำหลายครั้ง

**Q: ฉันจะเปลี่ยนคุณภาพของภาพ JPEG อย่างไร?**  
A: ตั้งค่า `options.setQuality(90)` (ค่าระหว่าง 0‑100) ก่อนเรียกการแปลง

**Q: ไลบรารีรองรับพื้นหลังโปร่งใสหรือไม่?**  
A: สำหรับการส่งออกเป็น PNG คุณสามารถใช้ `options.setBackgroundColor(Color.getTransparent())`

## Related Topics You Might Explore
- **วิธีแปลง EPUB เป็น PNG** – เปลี่ยนเป็น `ImageFormat.Png` และตั้งค่าพื้นหลังโปร่งใสตามต้องการ  
- **การแปลงหลายไฟล์ EPUB เป็นชุด** – วนลูปผ่านโฟลเดอร์ของ EPUB แล้วใช้ `ImageSaveOptions` ตัวเดียวกันซ้ำได้  
- **การปรับขนาดภาพสำหรับเว็บ** – ใช้ `options.setQuality()` และ `options.setResolution()` เพื่อสมดุลระหว่างคุณภาพภาพและขนาดไฟล์  

## Conclusion

Aspose.HTML for Java ให้คุณควบคุมการแปลง EPUB‑to‑image อย่างละเอียด ด้วยการกำหนด **custom page size**, **set image background color** และตัวเลือก `ImageSaveOptions` อื่น ๆ คุณสามารถสร้างภาพที่ตรงกับความต้องการด้านภาพของโครงการได้อย่างสมบูรณ์ ทดลองใช้รูปแบบ ขนาด และสีพื้นหลังต่าง ๆ และสำรวจความสามารถที่กว้างขวางของ Aspose.HTML for Java ในแอปพลิเคชันของคุณ

มีคำถามหรืออยากขอความช่วยเหลือ? ติดต่อ [Aspose.HTML community](https://forum.aspose.com/) เพื่อรับการสนับสนุน

---

**อัปเดตล่าสุด:** 2026-03-24  
**ทดสอบด้วย:** Aspose.HTML for Java 24.12  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}