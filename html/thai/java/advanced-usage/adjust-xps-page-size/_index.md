---
title: ปรับขนาดหน้า XPS ด้วย Aspose.HTML สำหรับ Java
linktitle: การปรับขนาดหน้า XPS
second_title: การประมวลผล Java HTML ด้วย Aspose.HTML
description: เรียนรู้วิธีการปรับขนาดหน้า XPS ด้วย Aspose.HTML สำหรับ Java ควบคุมขนาดเอาต์พุตของเอกสาร XPS ของคุณได้อย่างง่ายดาย
type: docs
weight: 16
url: /th/java/advanced-usage/adjust-xps-page-size/
---

ในบทช่วยสอนนี้ เราจะแนะนำคุณเกี่ยวกับกระบวนการปรับขนาดหน้า XPS โดยใช้ Aspose.HTML สำหรับ Java ไลบรารีอันทรงพลังนี้ช่วยให้คุณสามารถจัดการเอกสาร HTML และแสดงผลเป็นรูปแบบต่างๆ รวมถึง XPS การปรับขนาดหน้าเป็นสิ่งสำคัญเมื่อคุณจำเป็นต้องควบคุมขนาดเอาต์พุตของเอกสาร XPS

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่ม โปรดตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

1. สภาพแวดล้อมการพัฒนา Java: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Java Development Kit (JDK) ไว้ในระบบของคุณ

2.  Aspose.HTML สำหรับไลบรารี Java: คุณต้องดาวน์โหลดและรวมไลบรารี Aspose.HTML สำหรับ Java ไว้ในโปรเจ็กต์ Java ของคุณ คุณสามารถค้นหาไลบรารีได้[ที่นี่](https://releases.aspose.com/html/java/).

3. อินพุตไฟล์ HTML: เตรียมไฟล์ HTML ที่คุณต้องการเรนเดอร์และปรับขนาดหน้า XPS คุณสามารถใช้ไฟล์ HTML ของคุณเองสำหรับบทช่วยสอนนี้

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
    // -
}
```

 ในขั้นตอนนี้ เราจะอ่านไฟล์อินพุต HTML ของคุณโดยใช้`FileInputStream`.

## ขั้นตอนที่ 2: สร้างเอกสาร HTML และตั้งค่ารูปแบบ

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

// -
```

 ขั้นตอนนี้เกี่ยวข้องกับการสร้าง`HTMLDocument` และเพิ่มสไตล์ให้กับมัน

## ขั้นตอนที่ 3: สร้างตัวเลือกการเรนเดอร์ XPS

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

ขั้นตอนนี้เกี่ยวข้องกับการตั้งค่าขนาดหน้าและระบุว่าจะปรับให้เหมาะกับหน้าที่กว้างที่สุดหรือไม่

## ขั้นตอนที่ 5: แสดงผล

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

ในขั้นตอนสุดท้าย เราจะเรนเดอร์เอาท์พุต XPS โดยใช้ตัวเลือกที่กำหนดค่าไว้

## บทสรุป

ในบทช่วยสอนนี้ เราจะแสดงให้คุณเห็นถึงวิธีการปรับขนาดหน้า XPS โดยใช้ Aspose.HTML สำหรับ Java คุณสามารถควบคุมขนาดเอาต์พุตของเอกสาร XPS ของคุณ เพื่อให้แน่ใจว่าเอกสารเหล่านั้นตรงตามข้อกำหนดเฉพาะของคุณ ด้วยโค้ดและขั้นตอนที่ให้มา คุณสามารถนำฟีเจอร์นี้ไปใช้กับแอปพลิเคชัน Java ของคุณได้อย่างง่ายดาย

 หากคุณมีคำถามหรือต้องการความช่วยเหลือเพิ่มเติม โปรดเยี่ยมชม[เอกสาร Aspose.HTML สำหรับ Java](https://reference.aspose.com/html/java/) หรือขอความช่วยเหลือได้ที่[ฟอรั่ม Aspose](https://forum.aspose.com/).

## คำถามที่พบบ่อย

### คำถามที่ 1: Aspose.HTML สำหรับ Java คืออะไร?

A1: Aspose.HTML สำหรับ Java เป็นไลบรารี Java ที่ช่วยให้นักพัฒนาสามารถจัดการและแปลงเอกสาร HTML เป็นรูปแบบต่างๆ เช่น XPS, PDF และรูปภาพ

### คำถามที่ 2: ฉันสามารถดาวน์โหลด Aspose.HTML สำหรับ Java ได้ที่ไหน

 A2: คุณสามารถดาวน์โหลดไลบรารี Aspose.HTML สำหรับ Java ได้จาก[ลิงค์นี้](https://releases.aspose.com/html/java/).

### คำถามที่ 3: มีรุ่นทดลองใช้งานฟรีสำหรับ Aspose.HTML สำหรับ Java หรือไม่

 A3: ใช่ คุณสามารถรับรุ่นทดลองใช้งาน Aspose.HTML สำหรับ Java ได้ฟรีจาก[ที่นี่](https://releases.aspose.com/).

### คำถามที่ 4: ฉันจะรับใบอนุญาตชั่วคราวสำหรับ Aspose.HTML สำหรับ Java ได้อย่างไร

 A4: หากต้องการรับใบอนุญาตชั่วคราวสำหรับ Aspose.HTML สำหรับ Java โปรดไปที่[หน้านี้](https://purchase.aspose.com/temporary-license/).

### คำถามที่ 5: ฉันสามารถรับการสนับสนุนสำหรับ Aspose.HTML สำหรับ Java ได้หรือไม่

 A5: ใช่ คุณสามารถขอความช่วยเหลือและการสนับสนุนจากชุมชน Aspose ได้ที่[ฟอรั่ม Aspose](https://forum.aspose.com/).