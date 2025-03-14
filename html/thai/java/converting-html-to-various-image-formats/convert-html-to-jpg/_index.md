---
title: การแปลง HTML เป็น JPG ด้วย Aspose.HTML สำหรับ Java
linktitle: การแปลง HTML เป็น JPG
second_title: การประมวลผล Java HTML ด้วย Aspose.HTML
description: เรียนรู้วิธีแปลง HTML เป็น JPG โดยใช้ Aspose.HTML สำหรับ Java ปฏิบัติตามคำแนะนำทีละขั้นตอนของเราเพื่อการแปลง HTML เป็น JPG ได้อย่างราบรื่น
weight: 12
url: /th/java/converting-html-to-various-image-formats/convert-html-to-jpg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การแปลง HTML เป็น JPG ด้วย Aspose.HTML สำหรับ Java


ในยุคดิจิทัล การแปลงเนื้อหา HTML เป็นรูปแบบต่างๆ ถือเป็นความต้องการทั่วไป Aspose.HTML สำหรับ Java เป็นไลบรารีที่มีประสิทธิภาพซึ่งช่วยลดความซับซ้อนของกระบวนการแปลง HTML เป็น JPG ในคู่มือที่ครอบคลุมนี้ เราจะพาคุณผ่านกระบวนการทีละขั้นตอน คุณจะได้เรียนรู้เกี่ยวกับข้อกำหนดเบื้องต้น วิธีนำเข้าแพ็คเกจ และแบ่งตัวอย่างแต่ละตัวอย่างออกเป็นหลายขั้นตอนเพื่อให้เชี่ยวชาญการแปลง HTML เป็น JPG ด้วย Aspose.HTML สำหรับ Java

## ข้อกำหนดเบื้องต้น

ก่อนที่คุณจะเริ่มต้น โปรดตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

1. สภาพแวดล้อมการพัฒนา Java: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Java ไว้ในระบบของคุณแล้ว คุณสามารถดาวน์โหลดและติดตั้งได้จากเว็บไซต์ Java

2.  Aspose.HTML สำหรับไลบรารี Java: คุณต้องติดตั้งไลบรารี Aspose.HTML สำหรับ Java หากคุณยังไม่ได้ติดตั้ง คุณสามารถดาวน์โหลดได้จาก[ที่นี่](https://releases.aspose.com/html/java/).

## แพ็คเกจนำเข้า

ในการเริ่มต้น คุณต้องนำเข้าแพ็กเกจ Aspose.HTML ที่จำเป็นลงในโปรเจ็กต์ Java ของคุณ คุณสามารถทำได้โดยใช้โค้ดต่อไปนี้:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.saving.ImageSaveOptions;
import com.aspose.html.rendering.image.ImageFormat;
import com.aspose.html.converters.Converter;
import java.io.FileWriter;
```

ตอนนี้เรามาแบ่งกระบวนการแปลง HTML เป็น JPG ออกเป็นหลายขั้นตอน:

## เตรียมโค้ด HTML

ขั้นแรก เตรียมโค้ด HTML ที่คุณต้องการแปลงเป็นภาพ JPG คุณสามารถทำได้โดยสร้างไฟล์ HTML หรือสตริงที่มีโค้ด HTML

```java
String code = "<span>Hello</span> <span>World!!</span>";
try (FileWriter fileWriter = new FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## เริ่มต้นเอกสาร HTML

ขั้นตอนต่อไป คุณต้องเริ่มต้นเอกสาร HTML จากไฟล์ HTML ที่คุณเพิ่งสร้างขึ้น โดยใช้ไลบรารี Aspose.HTML

```java
HTMLDocument document = new HTMLDocument("document.html");
```

## กำหนดค่า ImageSaveOptions

 ตอนนี้กำหนดค่า`ImageSaveOptions` เพื่อระบุรูปแบบที่คุณต้องการบันทึกภาพ ในกรณีนี้ เราจะแปลงเป็น JPEG

```java
ImageSaveOptions options = new ImageSaveOptions(ImageFormat.Jpeg);
```

## แปลง HTML เป็น JPG

ขั้นตอนสุดท้ายคือการแปลงเอกสาร HTML เป็นภาพ JPG โดยใช้ตัวเลือกที่ระบุ

```java
Converter.convertHTML(document, options, "output.jpg");
```

## การทำความสะอาด

อย่าลืมปล่อยทรัพยากรเมื่อคุณแปลงเสร็จแล้ว

```java
if (document != null) {
    document.dispose();
}
```

ขอแสดงความยินดี! คุณได้แปลง HTML เป็น JPG โดยใช้ Aspose.HTML สำหรับ Java สำเร็จแล้ว

## บทสรุป

Aspose.HTML สำหรับ Java ทำให้กระบวนการแปลง HTML เป็น JPG ง่ายขึ้น ทำให้เป็นเครื่องมือที่จำเป็นสำหรับนักพัฒนา ด้วยคำแนะนำทีละขั้นตอนนี้ คุณจะได้เรียนรู้วิธีการเตรียม HTML เริ่มต้นเอกสาร กำหนดค่าตัวเลือก และดำเนินการแปลง ตอนนี้คุณสามารถผสานรวมฟีเจอร์นี้เข้ากับแอปพลิเคชัน Java ของคุณได้อย่างง่ายดาย

 หากคุณมีคำถามเพิ่มเติมหรือต้องการความช่วยเหลือ โปรดเยี่ยมชม[เอกสาร Aspose.HTML สำหรับ Java](https://reference.aspose.com/html/java/) หรือติดต่อได้ที่[ฟอรั่มสนับสนุน Aspose](https://forum.aspose.com/).

## คำถามที่พบบ่อย

### Aspose.HTML สำหรับ Java คืออะไร?
Aspose.HTML สำหรับ Java เป็นไลบรารี Java ที่ช่วยให้นักพัฒนาสามารถทำงานกับเอกสาร HTML และดำเนินการต่างๆ รวมถึงการแปลง HTML เป็น JPG

### ฉันสามารถดาวน์โหลด Aspose.HTML สำหรับ Java ได้ที่ไหน
 คุณสามารถดาวน์โหลด Aspose.HTML สำหรับ Java ได้จากหน้าเผยแพร่[ที่นี่](https://releases.aspose.com/html/java/).

### มีการทดลองใช้ฟรีหรือไม่?
 ใช่ คุณสามารถรับรุ่นทดลองใช้ Aspose.HTML สำหรับ Java ได้ฟรีจาก[ที่นี่](https://releases.aspose.com/).

### ฉันต้องมีใบอนุญาตสำหรับการใช้งานเชิงพาณิชย์หรือไม่?
 ใช่ สำหรับการใช้งานเชิงพาณิชย์ คุณสามารถซื้อใบอนุญาตได้จาก[ลิงค์นี้](https://purchase.aspose.com/buy).

### ฉันจะได้รับใบอนุญาตชั่วคราวได้อย่างไร?
หากคุณต้องการใบอนุญาตชั่วคราว คุณสามารถขอได้จาก[ลิงค์นี้](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
