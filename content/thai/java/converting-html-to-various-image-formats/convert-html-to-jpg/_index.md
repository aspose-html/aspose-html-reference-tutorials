---
title: การแปลง HTML เป็น JPG ด้วย Aspose.HTML สำหรับ Java
linktitle: การแปลง HTML เป็น JPG
second_title: การประมวลผล Java HTML ด้วย Aspose.HTML
description: เรียนรู้วิธีแปลง HTML เป็น JPG โดยใช้ Aspose.HTML สำหรับ Java ปฏิบัติตามคำแนะนำทีละขั้นตอนของเราเพื่อการแปลง HTML เป็น JPG ได้อย่างราบรื่น
type: docs
weight: 12
url: /th/java/converting-html-to-various-image-formats/convert-html-to-jpg/
---

ในยุคดิจิทัล การแปลงเนื้อหา HTML เป็นรูปแบบต่างๆ เป็นสิ่งจำเป็นทั่วไป Aspose.HTML สำหรับ Java เป็นไลบรารีที่มีประสิทธิภาพซึ่งช่วยให้กระบวนการแปลง HTML เป็น JPG ง่ายขึ้น ในคู่มือที่ครอบคลุมนี้ เราจะแนะนำคุณตลอดกระบวนการทีละขั้นตอน คุณจะได้เรียนรู้เกี่ยวกับข้อกำหนดเบื้องต้น วิธีนำเข้าแพ็คเกจ และแบ่งแต่ละตัวอย่างออกเป็นหลายขั้นตอนเพื่อเชี่ยวชาญการแปลง HTML เป็น JPG ด้วย Aspose.HTML สำหรับ Java

## ข้อกำหนดเบื้องต้น

ก่อนที่คุณจะเริ่มต้น ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

1. สภาพแวดล้อมการพัฒนา Java: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Java บนระบบของคุณ คุณสามารถดาวน์โหลดและติดตั้งได้จากเว็บไซต์ Java

2.  Aspose.HTML สำหรับไลบรารี Java: คุณต้องติดตั้ง Aspose.HTML สำหรับไลบรารี Java หากคุณยังไม่ได้ดำเนินการ คุณสามารถดาวน์โหลดได้จาก[ที่นี่](https://releases.aspose.com/html/java/).

## แพ็คเกจนำเข้า

ในการเริ่มต้น คุณต้องนำเข้าแพ็คเกจ Aspose.HTML ที่จำเป็นลงในโปรเจ็กต์ Java ของคุณ คุณสามารถทำได้โดยใช้รหัสต่อไปนี้:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.saving.ImageSaveOptions;
import com.aspose.html.rendering.image.ImageFormat;
import com.aspose.html.converters.Converter;
import java.io.FileWriter;
```

ตอนนี้ เรามาแบ่งกระบวนการแปลง HTML เป็น JPG ออกเป็นหลายขั้นตอน:

## เตรียมโค้ด HTML

ขั้นแรก เตรียมโค้ด HTML ที่คุณต้องการแปลงเป็นรูปภาพ JPG คุณสามารถทำได้โดยสร้างไฟล์ HTML หรือสตริงที่มีโค้ด HTML

```java
String code = "<span>Hello</span> <span>World!!</span>";
try (FileWriter fileWriter = new FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## เริ่มต้นเอกสาร HTML

ถัดไป คุณต้องเริ่มต้นเอกสาร HTML จากไฟล์ HTML ที่คุณเพิ่งสร้างขึ้น ซึ่งทำได้โดยใช้ไลบรารี Aspose.HTML

```java
HTMLDocument document = new HTMLDocument("document.html");
```

## กำหนดค่า ImageSaveOptions

 ตอนนี้กำหนดค่า`ImageSaveOptions` เพื่อระบุรูปแบบที่คุณต้องการบันทึกรูปภาพ ในกรณีนี้ เรากำลังแปลงเป็น JPEG

```java
ImageSaveOptions options = new ImageSaveOptions(ImageFormat.Jpeg);
```

## แปลง HTML เป็น JPG

ขั้นตอนสุดท้ายคือการแปลงเอกสาร HTML เป็นรูปภาพ JPG โดยใช้ตัวเลือกที่ระบุ

```java
Converter.convertHTML(document, options, "output.jpg");
```

## ทำความสะอาด

อย่าลืมปล่อยทรัพยากรเมื่อคุณแปลงเสร็จแล้ว

```java
if (document != null) {
    document.dispose();
}
```

ยินดีด้วย! คุณได้แปลง HTML เป็น JPG โดยใช้ Aspose.HTML สำหรับ Java สำเร็จแล้ว

## บทสรุป

Aspose.HTML สำหรับ Java ทำให้กระบวนการแปลง HTML เป็น JPG ง่ายขึ้น ทำให้เป็นเครื่องมือที่จำเป็นสำหรับนักพัฒนา ด้วยคำแนะนำทีละขั้นตอนนี้ คุณจะได้เรียนรู้วิธีเตรียม HTML เริ่มต้นเอกสาร กำหนดค่าตัวเลือก และดำเนินการแปลง ตอนนี้คุณสามารถรวมคุณสมบัตินี้เข้ากับแอปพลิเคชัน Java ของคุณได้อย่างง่ายดาย

 หากคุณมีคำถามเพิ่มเติมหรือต้องการความช่วยเหลือ โปรดไปที่[Aspose.HTML สำหรับเอกสารประกอบ Java](https://reference.aspose.com/html/java/) หรือติดต่อได้ที่[กำหนดฟอรั่มการสนับสนุน](https://forum.aspose.com/).

## คำถามที่พบบ่อย

### Aspose.HTML สำหรับ Java คืออะไร
Aspose.HTML สำหรับ Java เป็นไลบรารี Java ที่ช่วยให้นักพัฒนาสามารถทำงานกับเอกสาร HTML และดำเนินการต่างๆ รวมถึงการแปลง HTML เป็น JPG

### ฉันจะดาวน์โหลด Aspose.HTML สำหรับ Java ได้ที่ไหน
 คุณสามารถดาวน์โหลด Aspose.HTML สำหรับ Java ได้จากหน้าเผยแพร่[ที่นี่](https://releases.aspose.com/html/java/).

### มีการทดลองใช้ฟรีหรือไม่?
 ใช่ คุณสามารถทดลองใช้ Aspose.HTML สำหรับ Java ฟรีได้จาก[ที่นี่](https://releases.aspose.com/).

### ฉันจำเป็นต้องมีใบอนุญาตสำหรับการใช้งานเชิงพาณิชย์หรือไม่?
 ใช่ สำหรับการใช้งานเชิงพาณิชย์ คุณสามารถซื้อใบอนุญาตได้จาก[ลิงค์นี้](https://purchase.aspose.com/buy).

### ฉันจะรับใบอนุญาตชั่วคราวได้อย่างไร
หากคุณต้องการใบอนุญาตชั่วคราว คุณสามารถขอรับได้จาก[ลิงค์นี้](https://purchase.aspose.com/temporary-license/).