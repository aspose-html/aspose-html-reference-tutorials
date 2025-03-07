---
title: ปรับขนาดหน้า PDF ด้วย Aspose.HTML สำหรับ Java
linktitle: การปรับขนาดหน้า PDF
second_title: การประมวลผล Java HTML ด้วย Aspose.HTML
description: เรียนรู้วิธีการปรับขนาดหน้า PDF ด้วย Aspose.HTML สำหรับ Java สร้าง PDF คุณภาพสูงจาก HTML ได้อย่างง่ายดาย ควบคุมขนาดหน้าได้อย่างมีประสิทธิภาพ
weight: 15
url: /th/java/advanced-usage/adjust-pdf-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ปรับขนาดหน้า PDF ด้วย Aspose.HTML สำหรับ Java


ในยุคดิจิทัลทุกวันนี้ ความต้องการในการสร้าง PDF คุณภาพสูงจากเนื้อหา HTML เพิ่มมากขึ้น Aspose.HTML สำหรับ Java เป็นไลบรารี Java ที่มีประสิทธิภาพที่ช่วยให้คุณแปลงเอกสาร HTML เป็นรูปแบบ PDF ได้อย่างง่ายดาย ในบทช่วยสอนนี้ เราจะเน้นที่การปรับขนาดหน้าเมื่อแปลง HTML เป็น PDF โดยใช้ Aspose.HTML สำหรับ Java

## ข้อกำหนดเบื้องต้น

ก่อนที่คุณจะเริ่มต้น โปรดตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

- สภาพแวดล้อมการพัฒนา Java: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Java Development Kit (JDK) ไว้ในระบบของคุณ
-  Aspose.HTML สำหรับ Java: คุณต้องดาวน์โหลดและติดตั้ง Aspose.HTML สำหรับ Java จากเว็บไซต์[ที่นี่](https://releases.aspose.com/html/java/).
- เอกสาร HTML: คุณควรมีเอกสาร HTML ที่พร้อมสำหรับการแปลง หากไม่มี ให้สร้างขึ้นใหม่หรือใช้ไฟล์ HTML ที่มีอยู่

## แพ็คเกจนำเข้า

ในการเริ่มต้น คุณต้องนำเข้าแพ็คเกจที่จำเป็นเพื่อทำงานกับ Aspose.HTML สำหรับ Java ตัวอย่างโค้ดต่อไปนี้จะสาธิตวิธีการดำเนินการดังกล่าว:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

ตอนนี้คุณมีข้อกำหนดเบื้องต้นและนำเข้าแพ็คเกจที่จำเป็นแล้ว มาแบ่งกระบวนการปรับขนาดหน้า PDF ออกเป็นหลายขั้นตอน:

## ขั้นตอนที่ 1: การอ่านเนื้อหา HTML

ขั้นแรก คุณต้องอ่านเนื้อหา HTML ที่คุณต้องการแปลงเป็น PDF ในตัวอย่างนี้ เราจะอ่าน HTML จากไฟล์ชื่อ "FirstFile.html"

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## ขั้นตอนที่ 2: การเขียนเนื้อหา HTML

จากนั้นคุณจะเขียนเนื้อหา HTML ลงในไฟล์ชื่อ "FirstFileOut.html"

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // เพิ่มรูปแบบหรือเนื้อหา HTML ที่กำหนดเองที่นี่
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

## ขั้นตอนที่ 3: การเรนเดอร์ HTML เป็น PDF

ตอนนี้ คุณจะแสดงเนื้อหา HTML ลงในไฟล์ PDF เราจะกล่าวถึงสถานการณ์สองสถานการณ์: หนึ่งคือ สถานการณ์ที่ขนาดหน้าไม่ได้ปรับให้เข้ากับความกว้างของเนื้อหา และอีกสถานการณ์หนึ่งคือ สถานการณ์ที่ได้รับการปรับ

### ขนาดหน้ากระดาษไม่ได้ปรับ

ในสถานการณ์นี้ ขนาดหน้าจะถูกตั้งค่าเป็นความกว้างและความสูงคงที่ ซึ่งอาจถูกครอบตัดเนื้อหาหากเกินขนาดเหล่านี้

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

//แสดงผลออกมา
pdf_renderer.render(device, html_document);
```

### ขนาดหน้าปรับให้เข้ากับความกว้างของเนื้อหา

ในสถานการณ์นี้ ขนาดหน้าจะได้รับการปรับตามความกว้างของเนื้อหา

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//แสดงผลออกมา
pdf_renderer.render(device, html_document);
```

## บทสรุป

ในบทช่วยสอนนี้ เราได้ศึกษาวิธีการปรับขนาดหน้า PDF เมื่อแปลง HTML เป็น PDF โดยใช้ Aspose.HTML สำหรับ Java คุณได้เรียนรู้ข้อกำหนดเบื้องต้น นำเข้าแพ็คเกจที่จำเป็น และปฏิบัติตามคำแนะนำทีละขั้นตอนเพื่อบรรลุภารกิจนี้ ด้วย Aspose.HTML สำหรับ Java คุณสามารถควบคุมขนาดหน้าของ PDF ที่คุณสร้างขึ้นได้อย่างง่ายดาย เพื่อให้แน่ใจว่าเนื้อหาของคุณจะแสดงตามที่ต้องการ

 อย่าลังเลที่จะทดลองใช้ขนาดและการตั้งค่าหน้ากระดาษที่แตกต่างกันเพื่อให้ตรงตามความต้องการของคุณ หากคุณพบปัญหาหรือมีคำถามเพิ่มเติม โปรดอย่าลังเลที่จะขอความช่วยเหลือจาก[เอกสาร Aspose.HTML สำหรับ Java](https://reference.aspose.com/html/java/) หรือว่า[ฟอรั่มสนับสนุน Aspose](https://forum.aspose.com/).

## คำถามที่พบบ่อย

### คำถามที่ 1: Aspose.HTML สำหรับ Java คืออะไร?

A1: Aspose.HTML สำหรับ Java เป็นไลบรารี Java ที่ช่วยให้คุณทำงานกับเอกสาร HTML จัดการ แปลง และเรนเดอร์เป็นรูปแบบต่างๆ รวมถึง PDF

### คำถามที่ 2: ฉันจะปรับขนาดหน้า PDF เมื่อแปลง HTML เป็น PDF ด้วย Aspose.HTML สำหรับ Java ได้อย่างไร

 A2: คุณสามารถปรับขนาดหน้า PDF ได้โดยใช้`PageSetup` ชั้นเรียนและการตั้งค่า`AdjustToWidestPage` ทรัพย์สินที่จะ`true` หรือ `เท็จ` ขึ้นอยู่กับความต้องการของคุณ

### คำถามที่ 3: ฉันสามารถปรับแต่งรูปแบบของเนื้อหา HTML ก่อนที่จะแปลงเป็น PDF ได้หรือไม่

A3: ใช่ คุณสามารถปรับแต่งรูปแบบได้โดยการเพิ่มองค์ประกอบ CSS และ HTML ลงในเนื้อหา HTML ของคุณก่อนที่จะแปลงเป็น PDF ตามที่สาธิตในบทช่วยสอน

### คำถามที่ 4: ฉันสามารถค้นหาเอกสารสำหรับ Aspose.HTML สำหรับ Java ได้ที่ไหน

 A4: คุณสามารถดูเอกสารประกอบได้[ที่นี่](https://reference.aspose.com/html/java/) เพื่อดูข้อมูลและตัวอย่างที่ครอบคลุม

### คำถามที่ 5: มีรุ่นทดลองใช้งานฟรีสำหรับ Aspose.HTML สำหรับ Java หรือไม่

 A5: ใช่ คุณสามารถเข้าถึงรุ่นทดลองใช้งานฟรีของ Aspose.HTML สำหรับ Java ได้จาก[ลิงค์นี้](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
