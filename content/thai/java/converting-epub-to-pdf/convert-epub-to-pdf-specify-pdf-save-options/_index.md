---
title: การระบุตัวเลือกการบันทึก PDF สำหรับ EPUB เป็น PDF
linktitle: การระบุตัวเลือกการบันทึก PDF สำหรับ EPUB เป็น PDF
second_title: การประมวลผล Java HTML ด้วย Aspose.HTML
description: เรียนรู้วิธีการแปลง EPUB เป็น PDF ใน Java โดยใช้ Aspose.HTML ซึ่งเป็นไลบรารีการจัดการ HTML ที่ทรงพลัง
type: docs
weight: 12
url: /th/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
---

## การแนะนำ

Aspose.HTML สำหรับ Java เป็นเครื่องมืออันทรงพลังสำหรับการทำงานกับเอกสาร HTML และ EPUB ในคู่มือทีละขั้นตอนนี้ เราจะแนะนำคุณเกี่ยวกับกระบวนการแปลงไฟล์ EPUB เป็น PDF โดยใช้ Aspose.HTML สำหรับ Java ไม่ว่าคุณจะเป็นนักพัฒนาที่มีประสบการณ์หรือเพิ่งเริ่มต้น บทช่วยสอนนี้จะมอบความรู้และทักษะที่จำเป็นแก่คุณในการทำงานนี้อย่างมีประสิทธิภาพ

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่มต้น ให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

- สภาพแวดล้อมการพัฒนา Java: คุณต้องมีการตั้งค่าสภาพแวดล้อมการพัฒนา Java บนระบบของคุณ

-  Aspose.HTML สำหรับ Java: ดาวน์โหลดและติดตั้งไลบรารี Aspose.HTML สำหรับ Java คุณสามารถค้นหาไลบรารีและเอกสารที่เกี่ยวข้องได้ที่[เว็บไซต์](https://releases.aspose.com/html/java/).

- ไฟล์ EPUB: คุณจะต้องมีไฟล์ EPUB ที่คุณต้องการแปลงเป็น PDF

ตอนนี้ เรามาดูคำแนะนำทีละขั้นตอนในการแปลง EPUB เป็น PDF โดยใช้ Aspose.HTML สำหรับ Java กัน

## ขั้นตอนที่ 1: เปิดไฟล์ EPUB

 ในการเริ่มต้น ให้เปิดไฟล์ EPUB ที่มีอยู่เพื่ออ่าน คุณสามารถใช้`FileInputStream` เพื่อให้บรรลุสิ่งนี้ นี่คือโค้ดสำหรับขั้นตอนนี้:

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // โค้ดของคุณสำหรับขั้นตอนต่อไปจะอยู่ที่นี่
}
```

## ขั้นตอนที่ 2: กำหนดตัวเลือกการบันทึก PDF

 สร้างอินสแตนซ์ของ`PdfSaveOptions` ด้วยขนาดหน้าและสีพื้นหลังที่กำหนดเอง คุณสามารถกำหนดค่าการตั้งค่าหน้าได้ตามความต้องการของคุณ โดยทำได้ดังนี้:

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

 ตอนนี้โทรหา`ConvertEPUB` วิธีการแปลงไฟล์ EPUB เป็น PDF ระบุสตรีมอินพุต ตัวเลือกการบันทึก PDF และตำแหน่งเอาต์พุต ทำได้ดังนี้:

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

ขอแสดงความยินดี! คุณได้แปลงไฟล์ EPUB เป็น PDF โดยใช้ Aspose.HTML สำหรับ Java สำเร็จแล้ว ขณะนี้คุณสามารถเข้าถึงไฟล์ PDF ที่แปลงแล้วได้ที่ตำแหน่งเอาต์พุตที่ระบุ

## ซอร์สโค้ดที่สมบูรณ์
```java
Specifying PDF Save Options for EPUB to PDF
        // เปิดไฟล์ EPUB ที่มีอยู่เพื่อการอ่าน
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // สร้างอินสแตนซ์ของ PdfSaveOptions ด้วยขนาดหน้าแบบกำหนดเองและสีพื้นหลัง
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

ในบทช่วยสอนนี้ เราได้เรียนรู้วิธีใช้ Aspose.HTML สำหรับ Java เพื่อแปลงไฟล์ EPUB เป็นรูปแบบ PDF ไลบรารีอเนกประสงค์นี้มอบเครื่องมืออันทรงพลังสำหรับการจัดการเอกสารให้กับนักพัฒนา หากปฏิบัติตามขั้นตอนที่ระบุไว้ในคู่มือนี้ คุณจะสามารถผสานการแปลง EPUB เป็น PDF เข้ากับแอปพลิเคชัน Java ได้อย่างราบรื่น

## คำถามที่พบบ่อย (FAQs)

### Aspose.HTML สำหรับ Java เป็นไลบรารีฟรีหรือไม่?
 Aspose.HTML สำหรับ Java เป็นไลบรารีเชิงพาณิชย์ แต่คุณสามารถรับเวอร์ชันทดลองใช้งานฟรีได้จาก[เว็บไซต์](https://releases.aspose.com/).

### รูปแบบ EPUB ใดบ้างที่รองรับการแปลง?
Aspose.HTML สำหรับ Java รองรับการแปลงรูปแบบ EPUB ต่างๆ เพื่อให้เข้ากันได้กับเอกสาร EPUB ส่วนใหญ่

### ฉันสามารถปรับแต่งเอาท์พุต PDF เพิ่มเติมได้หรือไม่
 ใช่ คุณสามารถปรับแต่งผลลัพธ์ PDF ได้โดยการปรับการตั้งค่าหน้า สีพื้นหลัง และการตั้งค่าอื่นๆ ใน`PdfSaveOptions`.

### มีข้อจำกัดใด ๆ กับเวอร์ชันทดลองใช้ของ Aspose.HTML สำหรับ Java หรือไม่
เวอร์ชันทดลองใช้อาจมีข้อจำกัดบางประการ ดังนั้นขอแนะนำให้ตรวจสอบเอกสารประกอบเพื่อดูรายละเอียด

### ฉันจะได้รับการสนับสนุนสำหรับ Aspose.HTML สำหรับ Java ได้จากที่ไหน
คุณสามารถค้นหาคำตอบสำหรับคำถามของคุณและขอรับการสนับสนุนได้ที่[ฟอรั่ม Aspose.HTML](https://forum.aspose.com/).
