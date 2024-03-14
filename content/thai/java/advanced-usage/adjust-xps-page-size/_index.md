---
title: ปรับขนาดหน้า XPS ด้วย Aspose.HTML สำหรับ Java
linktitle: การปรับขนาดหน้า XPS
second_title: การประมวลผล Java HTML ด้วย Aspose.HTML
description: เรียนรู้วิธีปรับขนาดหน้า XPS ด้วย Aspose.HTML สำหรับ Java ควบคุมขนาดเอาต์พุตของเอกสาร XPS ของคุณได้อย่างง่ายดาย
type: docs
weight: 16
url: /th/java/advanced-usage/adjust-xps-page-size/
---

ในบทช่วยสอนนี้ เราจะแนะนำคุณตลอดขั้นตอนการปรับขนาดหน้า XPS โดยใช้ Aspose.HTML สำหรับ Java ไลบรารีอันทรงพลังนี้ช่วยให้คุณสามารถจัดการเอกสาร HTML และเรนเดอร์เป็นรูปแบบต่าง ๆ รวมถึง XPS การปรับขนาดหน้าถือเป็นสิ่งสำคัญเมื่อคุณต้องการควบคุมขนาดเอาต์พุตของเอกสาร XPS

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่มต้น ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

1. สภาพแวดล้อมการพัฒนา Java: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Java Development Kit (JDK) บนระบบของคุณ

2.  Aspose.HTML สำหรับไลบรารี Java: คุณต้องดาวน์โหลดและรวม Aspose.HTML สำหรับไลบรารี Java ในโปรเจ็กต์ Java ของคุณ คุณสามารถค้นหาห้องสมุด[ที่นี่](https://releases.aspose.com/html/java/).

3. อินพุตไฟล์ HTML: เตรียมไฟล์ HTML ที่คุณต้องการแสดงผลและปรับขนาดหน้า XPS คุณสามารถใช้ไฟล์ HTML ของคุณเองสำหรับบทช่วยสอนนี้

## แพ็คเกจนำเข้า

ขั้นแรก คุณต้องนำเข้าแพ็คเกจที่จำเป็นเพื่อทำงานกับ Aspose.HTML สำหรับ Java รวมแพ็คเกจเหล่านี้ไว้ที่จุดเริ่มต้นของคลาส Java ของคุณ:

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## ขั้นตอนที่ 1: ตั้งชื่อไฟล์อินพุต

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

 ในขั้นตอนนี้ เราจะอ่านไฟล์อินพุต HTML ของคุณโดยใช้ไฟล์`FileInputStream`.

## ขั้นตอนที่ 2: สร้างเอกสาร HTML และตั้งค่าสไตล์

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n";

// ...
```

 ขั้นตอนนี้เกี่ยวข้องกับการสร้าง`HTMLDocument` และเพิ่มสไตล์เข้าไปด้วย

## ขั้นตอนที่ 3: สร้างตัวเลือกการแสดงผล XPS

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

ที่นี่ เราสร้างตัวเลือกการเรนเดอร์ XPS เพื่อกำหนดค่ากระบวนการเรนเดอร์

## ขั้นตอนที่ 4: ปรับขนาดหน้า

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

ขั้นตอนนี้เกี่ยวข้องกับการตั้งค่าขนาดหน้าและระบุว่าจะปรับเป็นหน้าที่กว้างที่สุดหรือไม่

## ขั้นตอนที่ 5: แสดงผลเอาต์พุต

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

ในขั้นตอนสุดท้าย เราเรนเดอร์เอาต์พุต XPS โดยใช้ตัวเลือกที่กำหนดค่าไว้

## บทสรุป

ในบทช่วยสอนนี้ เราได้แสดงวิธีปรับขนาดหน้า XPS โดยใช้ Aspose.HTML สำหรับ Java คุณสามารถควบคุมขนาดเอาต์พุตของเอกสาร XPS ของคุณได้ เพื่อให้มั่นใจว่าตรงตามข้อกำหนดเฉพาะของคุณ ด้วยโค้ดและขั้นตอนที่ให้มา คุณสามารถปรับใช้คุณลักษณะนี้ในแอปพลิเคชัน Java ของคุณได้อย่างง่ายดาย

 หากคุณมีคำถามหรือต้องการความช่วยเหลือเพิ่มเติม โปรดไปที่[Aspose.HTML สำหรับเอกสารประกอบ Java](https://reference.aspose.com/html/java/) หรือขอความช่วยเหลือได้ที่[ตั้งฟอรั่ม](https://forum.aspose.com/).

## คำถามที่พบบ่อย

### คำถามที่ 1: Aspose.HTML สำหรับ Java คืออะไร

คำตอบ 1: Aspose.HTML สำหรับ Java เป็นไลบรารี Java ที่ช่วยให้นักพัฒนาจัดการและแปลงเอกสาร HTML เป็นรูปแบบต่างๆ เช่น XPS, PDF และรูปภาพ

### คำถามที่ 2: ฉันจะดาวน์โหลด Aspose.HTML สำหรับ Java ได้ที่ไหน

 A2: คุณสามารถดาวน์โหลดไลบรารี Aspose.HTML สำหรับ Java ได้จาก[ลิงค์นี้](https://releases.aspose.com/html/java/).

### คำถามที่ 3: Aspose.HTML สำหรับ Java มีรุ่นทดลองใช้ฟรีหรือไม่

 ตอบ 3: ได้ คุณสามารถทดลองใช้ Aspose.HTML สำหรับ Java ฟรีได้จาก[ที่นี่](https://releases.aspose.com/).

### คำถามที่ 4: ฉันจะขอรับใบอนุญาตชั่วคราวสำหรับ Aspose.HTML สำหรับ Java ได้อย่างไร

 A4: หากต้องการรับใบอนุญาตชั่วคราวสำหรับ Aspose.HTML สำหรับ Java โปรดไปที่[หน้านี้](https://purchase.aspose.com/temporary-license/).

### คำถามที่ 5: ฉันสามารถรับการสนับสนุนสำหรับ Aspose.HTML สำหรับ Java ได้หรือไม่

 A5: ได้ คุณสามารถขอความช่วยเหลือและการสนับสนุนจากชุมชน Aspose ได้ที่[ตั้งฟอรั่ม](https://forum.aspose.com/).