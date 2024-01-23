---
title: การระบุตัวเลือกการบันทึก PDF สำหรับ EPUB เป็น PDF
linktitle: การระบุตัวเลือกการบันทึก PDF สำหรับ EPUB เป็น PDF
second_title: การประมวลผล Java HTML ด้วย Aspose.HTML
description: เรียนรู้วิธีแปลง EPUB เป็น PDF ใน Java โดยใช้ Aspose.HTML ซึ่งเป็นไลบรารีการจัดการ HTML อันทรงพลัง
type: docs
weight: 12
url: /th/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
---

## การแนะนำ

Aspose.HTML สำหรับ Java เป็นเครื่องมืออันทรงพลังสำหรับการทำงานกับเอกสาร HTML และ EPUB ในคำแนะนำทีละขั้นตอนนี้ เราจะแนะนำคุณตลอดขั้นตอนการแปลงไฟล์ EPUB เป็น PDF โดยใช้ Aspose.HTML สำหรับ Java ไม่ว่าคุณจะเป็นนักพัฒนาที่มีประสบการณ์หรือเพิ่งเริ่มต้น บทช่วยสอนนี้จะช่วยให้คุณมีความรู้และทักษะที่จำเป็นในการดำเนินงานนี้อย่างมีประสิทธิภาพ

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่มต้น ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

- สภาพแวดล้อมการพัฒนา Java: คุณต้องมีการตั้งค่าสภาพแวดล้อมการพัฒนา Java บนระบบของคุณ

-  Aspose.HTML สำหรับ Java: ดาวน์โหลดและติดตั้ง Aspose.HTML สำหรับไลบรารี Java คุณสามารถค้นหาห้องสมุดและเอกสารที่เกี่ยวข้องได้ที่[เว็บไซต์](https://releases.aspose.com/html/java/).

- ไฟล์ EPUB: คุณจะต้องมีไฟล์ EPUB ที่คุณต้องการแปลงเป็น PDF

ตอนนี้ เรามาเจาะลึกคำแนะนำทีละขั้นตอนสำหรับการแปลง EPUB เป็น PDF โดยใช้ Aspose.HTML สำหรับ Java

## ขั้นตอนที่ 1: เปิดไฟล์ EPUB

 ในการเริ่มต้น ให้เปิดไฟล์ EPUB ที่มีอยู่เพื่ออ่าน คุณสามารถใช้ก`FileInputStream` เพื่อให้บรรลุเป้าหมายนี้ นี่คือรหัสสำหรับขั้นตอนนี้:

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // รหัสของคุณสำหรับขั้นตอนต่อไปจะอยู่ที่นี่
}
```

## ขั้นตอนที่ 2: กำหนดตัวเลือกการบันทึก PDF

 สร้างอินสแตนซ์ของ`PdfSaveOptions` ด้วยขนาดหน้าและสีพื้นหลังที่กำหนดเอง คุณสามารถกำหนดค่าการตั้งค่าเพจได้ตามความต้องการของคุณ ต่อไปนี้คือวิธีที่คุณสามารถทำได้:

```java
com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
anyPage.setSize(new com.aspose.html.drawing.Size(
    com.aspose.html.drawing.Length.fromPixels(3000),
    com.aspose.html.drawing.Length.fromPixels(1000))
);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
```

## ขั้นตอนที่ 3: แปลง EPUB เป็น PDF

 ตอนนี้โทรไปที่`ConvertEPUB` วิธีแปลงไฟล์ EPUB เป็น PDF ระบุอินพุตสตรีม ตัวเลือกการบันทึก PDF และตำแหน่งเอาต์พุต ต่อไปนี้เป็นวิธีดำเนินการ:

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

ยินดีด้วย! คุณได้แปลงไฟล์ EPUB เป็น PDF โดยใช้ Aspose.HTML สำหรับ Java สำเร็จแล้ว ตอนนี้คุณสามารถเข้าถึงไฟล์ PDF ที่แปลงแล้วได้ที่ตำแหน่งเอาต์พุตที่ระบุ

## กรอกซอร์สโค้ดให้สมบูรณ์
```java
Specifying PDF Save Options for EPUB to PDF
        // เปิดไฟล์ EPUB ที่มีอยู่เพื่ออ่าน
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // สร้างอินสแตนซ์ของ PdfSaveOptions ด้วยขนาดหน้าที่กำหนดเองและสีพื้นหลัง
            com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
            com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
            com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
            anyPage.setSize(new com.aspose.html.drawing.Size(
                    com.aspose.html.drawing.Length.fromPixels(3000),
                    com.aspose.html.drawing.Length.fromPixels(1000))
            );
            pageSetup.setAnyPage(anyPage);
            options.setPageSetup(pageSetup);
            options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
            // เรียกใช้เมธอด ConvertEPUB เพื่อแปลง EPUB เป็น PDF
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```


## บทสรุป

ในบทช่วยสอนนี้ เราได้เรียนรู้วิธีใช้ Aspose.HTML สำหรับ Java เพื่อแปลงไฟล์ EPUB เป็นรูปแบบ PDF ไลบรารีอเนกประสงค์นี้มอบเครื่องมืออันทรงพลังให้กับนักพัฒนาสำหรับการจัดการเอกสาร ด้วยการทำตามขั้นตอนที่ระบุไว้ในคู่มือนี้ คุณสามารถรวมการแปลง EPUB เป็น PDF เข้ากับแอปพลิเคชัน Java ของคุณได้อย่างราบรื่น

## คำถามที่พบบ่อย (FAQ)

### Aspose.HTML สำหรับ Java เป็นไลบรารีฟรีหรือไม่
 Aspose.HTML สำหรับ Java เป็นไลบรารีเชิงพาณิชย์ แต่คุณสามารถรับเวอร์ชันทดลองใช้ฟรีได้จากไลบรารีเหล่านี้[เว็บไซต์](https://releases.aspose.com/).

### EPUB รูปแบบใดบ้างที่รองรับการแปลง
Aspose.HTML สำหรับ Java รองรับการแปลงรูปแบบ EPUB ต่างๆ เพื่อให้มั่นใจว่าสามารถเข้ากันได้กับเอกสาร EPUB ส่วนใหญ่

### ฉันสามารถปรับแต่งเอาต์พุต PDF เพิ่มเติมได้หรือไม่
 ใช่ คุณสามารถปรับแต่งเอาต์พุต PDF ได้โดยการปรับการตั้งค่าหน้า สีพื้นหลัง และการตั้งค่าอื่นๆ ใน`PdfSaveOptions`.

### มีข้อจำกัดใดๆ สำหรับ Aspose.HTML สำหรับ Java เวอร์ชันทดลองหรือไม่
เวอร์ชันทดลองใช้งานอาจมีข้อจำกัดบางประการ ดังนั้นจึงแนะนำให้ตรวจสอบรายละเอียดจากเอกสารประกอบ

### ฉันจะรับการสนับสนุน Aspose.HTML สำหรับ Java ได้ที่ไหน
คุณสามารถค้นหาคำตอบสำหรับคำถามของคุณและขอรับการสนับสนุนได้ที่[ฟอรั่ม Aspose.HTML](https://forum.aspose.com/).
