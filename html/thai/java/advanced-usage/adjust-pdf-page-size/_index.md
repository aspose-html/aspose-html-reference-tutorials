---
date: 2025-12-01
description: เรียนรู้วิธีปรับขนาดหน้าของ PDF, แปลง HTML เป็น PDF และสร้าง PDF จาก
  HTML ด้วย Aspose.HTML for Java ควบคุมขนาดหน้าได้อย่างง่ายดาย
linktitle: Adjusting PDF Page Size
second_title: Java HTML Processing with Aspose.HTML
title: ปรับขนาดหน้ากระดาษ PDF ด้วย Aspose.HTML สำหรับ Java
url: /th/java/advanced-usage/adjust-pdf-page-size/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ปรับขนาดหน้า PDF ด้วย Aspose.HTML for Java

การสร้าง PDF จาก HTML เป็นความต้องการทั่วไปสำหรับรายงาน ใบแจ้งหนี้ และอี‑บุ๊ค เมื่อคุณ **ปรับขนาดหน้า PDF** คุณจะทำให้เอกสารสุดท้ายตรงกับเลย์เอาต์ที่คุณออกแบบใน HTML ในบทเรียนนี้คุณจะได้เรียนรู้วิธีแปลง HTML เป็น PDF ตั้งค่าขนาดที่กำหนดเอง และควบคุมว่าหน้าจะขยายอัตโนมัติเพื่อรองรับเนื้อหาที่กว้างที่สุด เราจะเดินผ่านตัวอย่างเต็มรูปแบบแบบทำมือโดยใช้ Aspose.HTML for Java

## คำตอบสั้น
- **“ปรับขนาดหน้า PDF” หมายถึงอะไร?** มันให้คุณกำหนดความกว้างและความสูงของแต่ละหน้าของ PDF หรือให้ตัวแปลงอัตโนมัติพอดีกับองค์ประกอบที่กว้างที่สุด  
- **ใช้ไลบรารีอะไร?** Aspose.HTML for Java (เวอร์ชันล่าสุด)  
- **ต้องมีลิขสิทธิ์หรือไม่?** ทดลองใช้ฟรีสำหรับการพัฒนา; ต้องมีลิขสิทธิ์เชิงพาณิชย์สำหรับการใช้งานจริง  
- **สามารถเปลี่ยนขนาดได้โดยโปรแกรมหรือไม่?** ได้ – ใช้ `PageSetup` และคุณสมบัติ `AdjustToWidestPage`  
- **รองรับ Java 8+ หรือไม่?** แน่นอน – API ทำงานกับ JDK 8 หรือใหม่กว่าใด ๆ  

## “ปรับขนาดหน้า PDF” คืออะไร?
การปรับขนาดหน้า PDF หมายถึงการกำหนดมิติของแต่ละหน้าที่ตัวแปลง HTML สร้างขึ้น คุณสามารถตั้งค่าขนาดคงที่ (เช่น A4, Letter) หรือให้ตัวแปลงคำนวณความกว้างที่เหมาะสมตามเนื้อหา ซึ่งช่วยให้คุณควบคุมเลย์เอาต์ การแบ่งหน้า และความแม่นยำของการแสดงผลได้อย่างละเอียด

## ทำไมต้องปรับขนาดหน้า PDF เมื่อแปลง HTML เป็น PDF?
- **รักษาเจตนาการออกแบบ:** ป้องกันไม่ให้เนื้อหาถูกตัดหรือยืดออก  
- **เพิ่มประสิทธิภาพการพิมพ์:** ตรงกับขนาดกระดาษที่กระบวนการต่อไปต้องการ  
- **ปรับปรุงความอ่านง่าย:** หลีกเลี่ยงพื้นที่ว่างมากเกินไปหรือข้อความแออัด  
- **เอกสารแบบไดนามิก:** รองรับตารางหรือรูปภาพกว้างโดยอัตโนมัติโดยไม่ต้องคำนวณด้วยตนเอง  

## ข้อกำหนดเบื้องต้น
ก่อนเริ่มทำงาน ให้ตรวจสอบว่าคุณมี:

- **Java Development Kit (JDK) 8 หรือสูงกว่า** ติดตั้งบนเครื่องของคุณ  
- **Aspose.HTML for Java** – ดาวน์โหลด JAR ล่าสุดจาก [official release page](https://releases.aspose.com/html/java/)  
- **ไฟล์ HTML** ที่ต้องการแปลง (เราจะใช้ `FirstFile.html` ในตัวอย่าง)  

## นำเข้าแพ็กเกจ
ก่อนอื่นให้นำเข้าคลาสที่จำเป็น โค้ดบล็อกด้านล่างไม่ได้เปลี่ยนแปลงจากบทเรียนต้นฉบับ

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

## ขั้นตอนที่ 1: อ่านเนื้อหา HTML
เราอ่านไฟล์ HTML ต้นฉบับด้วย `FileInputStream` ขั้นตอนนี้เตรียมมาร์กอัปดิบสำหรับการจัดการต่อไป

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## ขั้นตอนที่ 2: เขียน (และอาจเพิ่ม) HTML
ที่นี่เราคัดลอก HTML ดั้งเดิมไปยังไฟล์ใหม่และแทรกสไตล์อินไลน์บางส่วนเพื่อสาธิตว่าการจัดรูปแบบส่งผลต่อผลลัพธ์ PDF อย่างไร คุณสามารถเปลี่ยน CSS ตัวอย่างนี้เป็นของคุณเองได้ตามต้องการ

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Add custom HTML styles or content here
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

## ขั้นตอนที่ 3: แปลง HTML เป็น PDF – สองสถานการณ์
ต่อไปเราจะดูวิธี **สร้าง PDF จาก HTML** ด้วยสองกลยุทธ์ขนาดหน้าแตกต่างกัน

### 3.1 ขนาดหน้าที่ไม่ได้ปรับตามความกว้างของเนื้อหา
ในกรณีนี้เรากำหนดขนาดหน้าเป็น 100 × 100 points หากมีองค์ประกอบใดเกินขอบเขตนั้น จะถูกตัดออก

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Create an HTMLDocument instance from the HTML file
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Set PDF rendering options
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

### 3.2 ขนาดหน้าที่ปรับตามความกว้างของเนื้อหา
ที่นี่เราเปิดใช้งาน `AdjustToWidestPage` ทำให้ตัวแปลงขยายความกว้างของหน้าอัตโนมัติเพื่อรองรับองค์ประกอบที่กว้างที่สุด ขณะที่ความสูงคงที่

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

## วิธีตั้งค่าขนาด PDF (วิธีเปลี่ยนขนาดหน้า PDF) ในโค้ด
อ็อบเจ็กต์ `PageSetup` คือกุญแจสำคัญ:

- `setAnyPage(Page page)`: กำหนดความกว้าง × ความสูงพื้นฐาน  
- `setAdjustToWidestPage(boolean)`: สลับการขยายอัตโนมัติ  

โดยการปรับคุณสมบัติเหล่านี้สองอย่าง คุณสามารถ **ตั้งค่าขนาด PDF** สำหรับสถานการณ์ใด ๆ ไม่ว่าจะเป็นหน้า A4 คงที่หรือความกว้างไดนามิกที่ตามเลย์เอาต์ HTML ของคุณ

## ปัญหาทั่วไปและเคล็ดลับ
| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|---------|
| เนื้อหาถูกตัดออก | ขนาดคงที่เล็กเกินไป | เพิ่มค่าของ `Size` หรือเปิดใช้งาน `AdjustToWidestPage` |
| ตัวอักษรดูเบลอ | DPI เริ่มต้นของการเรนเดอร์ต่ำ | ใช้ `PdfRenderingOptions.setResolution(int dpi)` เพื่อเพิ่มคุณภาพ |
| สไตล์หายไป | CSS ภายนอกไม่ถูกโหลด | ฝัง CSS อินไลน์หรือใช้ `HTMLDocument.setBaseUrl()` ชี้ไปยังโฟลเดอร์สไตล์ชีต |
| ไฟล์ HTML ขนาดใหญ่ทำให้ OutOfMemoryError | ตัวแปลงโหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ | ประมวลผลเอกสารเป็นชิ้นส่วนหรือเพิ่ม heap ของ JVM (`-Xmx`) |

## คำถามที่พบบ่อย

**Q: Aspose.HTML for Java คืออะไร?**  
A: เป็นไลบรารี Java ที่ช่วยให้คุณสร้าง แก้ไข และเรนเดอร์เอกสาร HTML รวมถึงการแปลงเป็น PDF, PNG และรูปแบบอื่น ๆ  

**Q: จะปรับขนาดหน้า PDF อย่างไรเมื่อแปลง HTML เป็น PDF ด้วย Aspose.HTML for Java?**  
A: ใช้คลาส `PageSetup` แล้วตั้งค่า `AdjustToWidestPage` เป็น `true` (ขนาดอัตโนมัติ) หรือ `false` (ขนาดคงที่) จากนั้นกำหนด `Size` ที่ต้องการผ่าน `new Page(new Size(width, height))`  

**Q: สามารถปรับแต่งสไตล์ของเนื้อหา HTML ก่อนแปลงเป็น PDF ได้หรือไม่?**  
A: ได้ – คุณสามารถแทรก CSS, แก้ไข DOM, หรือใช้สไตล์ชีตภายนอก บทเรียนนี้แสดงการแทรก CSS อินไลน์เป็นตัวอย่าง  

**Q: จะหาเอกสารอ้างอิงของ Aspose.HTML for Java ได้จากที่ไหน?**  
A: เอกสารฉบับเต็มมีให้ที่ [here](https://reference.aspose.com/html/java/)  

**Q: มีรุ่นทดลองฟรีสำหรับ Aspose.HTML for Java หรือไม่?**  
A: มีแน่นอน – ดาวน์โหลดรุ่นทดลองจาก [release page](https://releases.aspose.com/html/java/)  

## สรุป
คุณได้เรียนรู้วิธี **ปรับขนาดหน้า PDF**, **แปลง HTML เป็น PDF**, และ **ตั้งค่าขนาด PDF ที่กำหนดเอง** ด้วย Aspose.HTML for Java ทดลองปรับขนาดหน้า, การตั้งค่า DPI, และการปรับ CSS เพื่อให้ได้ผลลัพธ์ที่สมบูรณ์แบบสำหรับกรณีการใช้งานของคุณ หากเจออุปสรรคใด ๆ ให้ดูเอกสารอย่างเป็นทางการหรือฟอรั่มสนับสนุนของ Aspose

---

**อัปเดตล่าสุด:** 2025-12-01  
**ทดสอบกับ:** Aspose.HTML for Java 24.12 (latest)  
**ผู้เขียน:** Aspose  
**แหล่งข้อมูลที่เกี่ยวข้อง:** [API Reference](https://reference.aspose.com/html/java/) | [Download Free Trial](https://releases.aspose.com/html/java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}