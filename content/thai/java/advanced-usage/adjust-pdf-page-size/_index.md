---
title: ปรับขนาดหน้า PDF ด้วย Aspose.HTML สำหรับ Java
linktitle: การปรับขนาดหน้า PDF
second_title: การประมวลผล Java HTML ด้วย Aspose.HTML
description: เรียนรู้วิธีปรับขนาดหน้า PDF ด้วย Aspose.HTML สำหรับ Java สร้าง PDF คุณภาพสูงจาก HTML ได้อย่างง่ายดาย ควบคุมขนาดหน้าได้อย่างมีประสิทธิภาพ
type: docs
weight: 15
url: /th/java/advanced-usage/adjust-pdf-page-size/
---

ในยุคดิจิทัลปัจจุบัน ความต้องการสร้าง PDF คุณภาพสูงจากเนื้อหา HTML กำลังเพิ่มสูงขึ้น Aspose.HTML สำหรับ Java เป็นไลบรารี Java ที่ทรงพลังซึ่งช่วยให้คุณแปลงเอกสาร HTML เป็นรูปแบบ PDF ได้อย่างง่ายดาย ในบทช่วยสอนนี้ เราจะเน้นไปที่การปรับขนาดหน้าเมื่อแปลง HTML เป็น PDF โดยใช้ Aspose.HTML สำหรับ Java

## ข้อกำหนดเบื้องต้น

ก่อนที่คุณจะเริ่มต้น ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

- สภาพแวดล้อมการพัฒนา Java: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Java Development Kit (JDK) บนระบบของคุณ
-  Aspose.HTML สำหรับ Java: คุณต้องดาวน์โหลดและติดตั้ง Aspose.HTML สำหรับ Java จากเว็บไซต์[ที่นี่](https://releases.aspose.com/html/java/).
- เอกสาร HTML: คุณควรมีเอกสาร HTML พร้อมสำหรับการแปลง ถ้าไม่ ให้สร้างไฟล์หรือใช้ไฟล์ HTML ที่มีอยู่

## แพ็คเกจนำเข้า

ในการเริ่มต้น คุณจะต้องนำเข้าแพ็คเกจที่จำเป็นเพื่อทำงานกับ Aspose.HTML สำหรับ Java ข้อมูลโค้ดต่อไปนี้สาธิตวิธีการทำเช่นนี้:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

ตอนนี้คุณมีข้อกำหนดเบื้องต้นและนำเข้าแพ็คเกจที่จำเป็นแล้ว เรามาแจกแจงขั้นตอนการปรับขนาดหน้า PDF ออกเป็นหลายขั้นตอน:

## ขั้นตอนที่ 1: การอ่านเนื้อหา HTML

ขั้นแรก คุณต้องอ่านเนื้อหา HTML ที่คุณต้องการแปลงเป็น PDF ในตัวอย่างนี้ เราจะอ่าน HTML จากไฟล์ชื่อ "FirstFile.html"

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## ขั้นตอนที่ 2: การเขียนเนื้อหา HTML

ต่อไป คุณจะเขียนเนื้อหา HTML ลงในไฟล์ชื่อ "FirstFileOut.html"

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // เพิ่มสไตล์หรือเนื้อหา HTML ที่กำหนดเองที่นี่
    String style = "<style>\n" +
                   ".st\n" +
                   "{\n" +
                   "color:\n" +
                   "green;\n" +
                   "}\n" +
                   "</style >\n" +
                   "<div id = id1 > Aspose.Html rendering Text in Black Color</div >\n" +
                   "<div id = id2 class='' st '' > Aspose.Html rendering Text in Green Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: blue;' > Aspose.Html rendering Text in Blue Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: red;' ><font face = 'Arial' > Aspose.Html rendering Text in Red\n" +
                   "Color</font ></div >\n";
    fileOutputStream.write(style.getBytes(java.nio.charset.StandardCharsets.UTF_8));
}
```

## ขั้นตอนที่ 3: แสดงผล HTML เป็น PDF

ตอนนี้ คุณจะแสดงเนื้อหา HTML เป็นไฟล์ PDF เราจะกล่าวถึงสองสถานการณ์: สถานการณ์หนึ่งที่ขนาดหน้าไม่ได้ปรับขนาดหน้าให้เข้ากับความกว้างของเนื้อหา และอีกสถานการณ์หนึ่งที่ปรับขนาดหน้า

### ขนาดหน้าไม่ได้ปรับขนาด

ในสถานการณ์สมมตินี้ ขนาดหน้าถูกตั้งค่าเป็นความกว้างและความสูงคงที่ ซึ่งอาจครอบตัดเนื้อหาหากเกินขนาดเหล่านี้

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// สร้างอินสแตนซ์ HTMLDocument จากไฟล์ HTML
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// ตั้งค่าตัวเลือกการเรนเดอร์ PDF
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//แสดงผลเอาต์พุต
pdf_renderer.render(device, html_document);
```

### ขนาดหน้าปรับตามความกว้างของเนื้อหา

ในสถานการณ์สมมตินี้ ขนาดหน้าจะถูกปรับเปลี่ยนตามความกว้างของเนื้อหา

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//แสดงผลเอาต์พุต
pdf_renderer.render(device, html_document);
```

## บทสรุป

ในบทช่วยสอนนี้ เราได้สำรวจวิธีการปรับขนาดหน้า PDF เมื่อแปลง HTML เป็น PDF โดยใช้ Aspose.HTML สำหรับ Java คุณได้เรียนรู้ข้อกำหนดเบื้องต้น นำเข้าแพ็คเกจที่จำเป็น และปฏิบัติตามคำแนะนำทีละขั้นตอนเพื่อให้บรรลุงานนี้ ด้วย Aspose.HTML สำหรับ Java คุณสามารถควบคุมขนาดหน้าของ PDF ที่คุณสร้างขึ้นได้อย่างง่ายดาย เพื่อให้แน่ใจว่าเนื้อหาของคุณจะแสดงตามที่ตั้งใจไว้

 คุณสามารถทดลองใช้ขนาดหน้าและการตั้งค่าต่างๆ เพื่อตอบสนองความต้องการเฉพาะของคุณได้ หากคุณพบปัญหาใดๆ หรือมีคำถามเพิ่มเติม อย่าลังเลที่จะขอความช่วยเหลือจาก[Aspose.HTML สำหรับเอกสารประกอบ Java](https://reference.aspose.com/html/java/) หรือ[กำหนดฟอรั่มการสนับสนุน](https://forum.aspose.com/).

## คำถามที่พบบ่อย

### คำถามที่ 1: Aspose.HTML สำหรับ Java คืออะไร

คำตอบ 1: Aspose.HTML สำหรับ Java เป็นไลบรารี Java ที่ช่วยให้คุณสามารถทำงานกับเอกสาร HTML จัดการ แปลง และเรนเดอร์เป็นรูปแบบต่างๆ รวมถึง PDF

### คำถามที่ 2: ฉันจะปรับขนาดหน้า PDF เมื่อแปลง HTML เป็น PDF ด้วย Aspose.HTML สำหรับ Java ได้อย่างไร

 A2: คุณสามารถปรับขนาดหน้า PDF ได้โดยใช้ไฟล์`PageSetup` คลาสและการตั้งค่า`AdjustToWidestPage` ทรัพย์สินเพื่อ`true` หรือ `เท็จ ขึ้นอยู่กับความต้องการของคุณ

### คำถามที่ 3: ฉันสามารถปรับแต่งสไตล์ของเนื้อหา HTML ก่อนที่จะแปลงเป็น PDF ได้หรือไม่

A3: ได้ คุณสามารถปรับแต่งสไตล์ได้โดยการเพิ่มองค์ประกอบ CSS และ HTML ให้กับเนื้อหา HTML ของคุณก่อนที่จะแปลงเป็น PDF ดังที่แสดงในบทช่วยสอน

### คำถามที่ 4: ฉันจะหาเอกสารสำหรับ Aspose.HTML สำหรับ Java ได้ที่ไหน

 A4: คุณสามารถดูเอกสารประกอบได้[ที่นี่](https://reference.aspose.com/html/java/) สำหรับข้อมูลและตัวอย่างที่ครอบคลุม

### คำถามที่ 5: Aspose.HTML สำหรับ Java มีรุ่นทดลองใช้ฟรีหรือไม่

 A5: ได้ คุณสามารถเข้าถึง Aspose.HTML สำหรับ Java รุ่นทดลองใช้ฟรีได้[ลิงค์นี้](https://releases.aspose.com/).