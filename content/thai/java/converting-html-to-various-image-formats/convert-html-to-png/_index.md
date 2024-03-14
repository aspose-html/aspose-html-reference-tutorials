---
title: การแปลง HTML เป็น PNG ด้วย Aspose.HTML สำหรับ Java
linktitle: แปลง HTML เป็น PNG
second_title: การประมวลผล Java HTML ด้วย Aspose.HTML
description: แปลง HTML เป็น PNG ด้วย Aspose.HTML สำหรับ Java ปฏิบัติตามคำแนะนำทีละขั้นตอนของเราเพื่อการแปลง HTML เป็น PNG อย่างง่ายดาย เริ่มต้นวันนี้!
type: docs
weight: 13
url: /th/java/converting-html-to-various-image-formats/convert-html-to-png/
---

ในโลกของการพัฒนาเว็บ ความสามารถในการแปลงเนื้อหา HTML เป็นรูปแบบอื่นมักเป็นงานที่สำคัญ ข้อกำหนดทั่วไปประการหนึ่งคือการแปลง HTML ให้เป็นรูปแบบรูปภาพ เช่น PNG Aspose.HTML สำหรับ Java มอบโซลูชันอันทรงพลังเพื่อให้งานนี้สำเร็จลุล่วงได้อย่างง่ายดาย ในบทช่วยสอนทีละขั้นตอนนี้ เราจะแนะนำคุณตลอดกระบวนการแปลง HTML เป็น PNG โดยใช้ Aspose.HTML สำหรับ Java

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่มกระบวนการแปลงจริง ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

- สภาพแวดล้อมการพัฒนา Java: ตรวจสอบให้แน่ใจว่าคุณได้ตั้งค่าสภาพแวดล้อมการพัฒนา Java บนระบบของคุณ

-  Aspose.HTML สำหรับ Java: คุณควรติดตั้งไลบรารี Aspose.HTML สำหรับ Java คุณสามารถดาวน์โหลดได้จาก[Aspose.HTML สำหรับเอกสารประกอบ Java](https://reference.aspose.com/html/java/).

- เนื้อหา HTML: เตรียมเนื้อหา HTML ที่คุณต้องการแปลงเป็นรูปภาพ PNG

- ความรู้พื้นฐานของ Java: คุณควรมีความเข้าใจพื้นฐานเกี่ยวกับการเขียนโปรแกรม Java

## แพ็คเกจนำเข้า

ในโปรเจ็กต์ Java ของคุณ คุณต้องนำเข้าแพ็คเกจที่จำเป็นจาก Aspose.HTML สำหรับ Java เพื่อทำการแปลง HTML เป็น PNG ต่อไปนี้คือวิธีการนำเข้าแพ็คเกจที่จำเป็น:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.saving.ImageSaveOptions;
import com.aspose.html.converters.Converter;
import com.aspose.html.rendering.image.ImageFormat;
```

## เตรียมเนื้อหา HTML

ในการเริ่มต้น คุณควรเตรียมเนื้อหา HTML ที่คุณต้องการแปลงเป็นรูปภาพ PNG คุณสามารถใช้โค้ด HTML ใดก็ได้ตามความต้องการของคุณ

```java
String htmlCode = "<span>Hello</span> <span>World!!</span>";
```

คุณสามารถบันทึกโค้ด HTML นี้ลงในไฟล์เพื่อการประมวลผลต่อไปได้ ในตัวอย่างนี้ เรากำลังบันทึกลงในไฟล์ชื่อ "document.html"

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(htmlCode);
}
```

## เริ่มต้นเอกสาร HTML

ถัดไป คุณต้องเริ่มต้นเอกสาร HTML จากไฟล์ HTML ที่คุณสร้างในขั้นตอนก่อนหน้า

```java
HTMLDocument document = new HTMLDocument("document.html");
```

## แปลง HTML เป็น PNG

ตอนนี้ได้เวลาตั้งค่าตัวเลือกการแปลงและทำการแปลง HTML เป็น PNG

```java
ImageSaveOptions options = new ImageSaveOptions(ImageFormat.Png);
Converter.convertHTML(document, options, "output.png");
```

## ทำความสะอาด

อย่าลืมปล่อยทรัพยากรใด ๆ และล้างข้อมูลหลังจากการแปลงเสร็จสิ้น

```java
if (document != null) {
    document.dispose();
}
```

ยินดีด้วย! คุณได้แปลง HTML เป็น PNG โดยใช้ Aspose.HTML สำหรับ Java สำเร็จแล้ว ตอนนี้คุณสามารถใช้รูปภาพ PNG ที่สร้างขึ้นได้ตามต้องการในโครงการของคุณ

## บทสรุป

ในบทช่วยสอนนี้ เราได้สาธิตวิธีใช้ Aspose.HTML สำหรับ Java เพื่อแปลง HTML เป็น PNG ด้วยขั้นตอนและข้อมูลโค้ดที่ให้มา คุณจะสามารถรวมฟังก์ชันการทำงานนี้เข้ากับแอปพลิเคชัน Java ของคุณได้อย่างง่ายดาย

## คำถามที่พบบ่อย

### ฉันจะหาเอกสารประกอบสำหรับ Aspose.HTML สำหรับ Java ได้ที่ไหน
    คุณสามารถค้นหาเอกสารได้ที่[Aspose.HTML สำหรับเอกสาร Java](https://reference.aspose.com/html/java/).

### ฉันจะดาวน์โหลด Aspose.HTML สำหรับ Java ได้อย่างไร
    คุณสามารถดาวน์โหลดได้จากเว็บไซต์:[ดาวน์โหลด Aspose.HTML สำหรับ Java](https://releases.aspose.com/html/java/).

### มีการทดลองใช้ฟรีสำหรับ Aspose.HTML สำหรับ Java หรือไม่
    ใช่ คุณสามารถทดลองใช้ฟรีได้จาก[Aspose.HTML ทดลองใช้ฟรี](https://releases.aspose.com/).

### ฉันจะขอรับใบอนุญาตชั่วคราวสำหรับ Aspose.HTML สำหรับ Java ได้อย่างไร
    คุณสามารถขอใบอนุญาตชั่วคราวได้จาก[Aspose.HTML ใบอนุญาตชั่วคราว](https://purchase.aspose.com/temporary-license/).

### ฉันจะรับการสนับสนุนจากชุมชนและถามคำถามเกี่ยวกับ Aspose.HTML สำหรับ Java ได้ที่ไหน
    คุณสามารถเข้าร่วมการสนทนาของชุมชนได้ที่[ฟอรั่มสนับสนุน Aspose.HTML](https://forum.aspose.com/).