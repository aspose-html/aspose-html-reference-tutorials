---
date: 2025-11-29
description: เรียนรู้วิธีแปลง HTML เป็น XPS และปรับขนาดหน้ากระดาษ XPS ด้วย Aspose.HTML
  for Java ควบคุมขนาดผลลัพธ์ได้อย่างง่ายดาย.
language: th
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: แปลง HTML เป็น XPS และปรับขนาดหน้าของ XPS ด้วย Aspose.HTML สำหรับ Java
url: /java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลง HTML เป็น XPS และปรับขนาดหน้า XPS ด้วย Aspose.HTML for Java

ในบทแนะนำนี้คุณจะได้เรียนรู้ **วิธีแปลง HTML เป็น XPS** และปรับขนาดหน้าที่ได้อย่างละเอียดด้วย Aspose.HTML for Java ไม่ว่าคุณจะสร้างรายงานที่พิมพ์ได้ ใบแจ้งหนี้ หรือเอกสารเก็บถาวร การควบคุมมิติของ XPS จะทำให้ผลลัพธ์ออกมาตรงตามที่คุณต้องการ เราจะเดินผ่านทุกขั้นตอน—from การตั้งค่าสภาพแวดล้อมจนถึงการเรนเดอร์ไฟล์ XPS สุดท้าย—เพื่อให้คุณสามารถนำความสามารถนี้ไปใช้ในแอปพลิเคชัน Java ของคุณได้ทันที

## คำตอบสั้น
- **“แปลง HTML เป็น XPS” หมายถึงอะไร?** เป็นการเรนเดอร์เอกสาร HTML ให้เป็นไฟล์ XPS โดยคงรูปแบบและสไตล์ไว้  
- **ต้องมีลิขสิทธิ์หรือไม่?** สามารถใช้รุ่นทดลองฟรีสำหรับการพัฒนา; ต้องมีลิขสิทธิ์เชิงพาณิชย์สำหรับการใช้งานจริง  
- **รองรับเวอร์ชัน Java ใด?** Java 8 หรือสูงกว่า (แนะนำ JDK 11+)  
- **สามารถเปลี่ยนขนาดหน้าได้หรือไม่?** ได้ – Aspose.HTML ให้คุณกำหนดขนาดที่กำหนดเองก่อนการเรนเดอร์  
- **การแปลงใช้เวลานานแค่ไหน?** ปกติภายในไม่กี่วินาทีสำหรับหน้าแบบมาตรฐาน; เอกสารขนาดใหญ่อาจใช้เวลานานขึ้น

## การแปลง HTML เป็น XPS คืออะไร?
การแปลง HTML เป็น XPS หมายถึงการนำไฟล์มาร์กอัปแบบเว็บมาผลิตเป็นเอกสาร XPS (XML Paper Specification) ซึ่งเป็นรูปแบบที่มีการจัดวางคงที่พร้อมพิมพ์ได้คล้ายกับ PDF สิ่งนี้มีประโยชน์เมื่อคุณต้องการเอกสารที่มีความแม่นยำสูงและอิสระจากอุปกรณ์สำหรับการเก็บถาวรหรือการพิมพ์จากแอปพลิเคชัน Java

## ทำไมต้องปรับขนาดหน้า XPS?
การปรับขนาดหน้าจะให้คุณควบคุมมิติทางกายภาพของเอกสารสุดท้าย (เช่น A4, Letter, ป้ายกำหนดเอง) ช่วยป้องกันการสเกลที่ไม่ต้องการ, ทำให้เนื้อหาเข้ากันได้อย่างสมบูรณ์, และสามารถลดขนาดไฟล์โดยกำจัดพื้นที่ว่างที่ไม่จำเป็น

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำตามขั้นตอนต่อไปนี้ให้ตรวจสอบว่าคุณมีสิ่งต่อไปนี้พร้อมใช้งาน:

1. **สภาพแวดล้อมการพัฒนา Java** – ติดตั้ง Java Development Kit (JDK) บนระบบของคุณ  
2. **Aspose.HTML for Java Library** – ดาวน์โหลดและเพิ่มไลบรารี Aspose.HTML for Java ลงในโปรเจกต์ของคุณ คุณสามารถหาไลบรารีได้จาก [ที่นี่](https://releases.aspose.com/html/java/)  
3. **ไฟล์ HTML อินพุต** – เตรียมไฟล์ HTML ที่ต้องการเรนเดอร์และปรับขนาดหน้า XPS คุณสามารถใช้ไฟล์ HTML ของคุณเองสำหรับบทแนะนำนี้

## นำเข้าแพ็กเกจ

ก่อนอื่นให้นำเข้าคลาสที่จำเป็น แพ็กเกจเหล่านี้ให้คุณเข้าถึงการจัดการเอกสาร, การเรนเดอร์, และคุณสมบัติการตั้งค่าหน้า

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## ขั้นตอนที่ 1: ตั้งค่าชื่อไฟล์อินพุต

อ่านไฟล์ HTML ต้นฉบับโดยใช้ `FileInputStream` สตรีมนี้จะส่ง HTML ดิบเข้าสู่เอนจิน Aspose.HTML

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

## ขั้นตอนที่ 2: สร้าง HTML Document และตั้งค่าสไตล์

สร้างอินสแตนซ์ `HTMLDocument` ที่แทนเนื้อหาที่คุณจะเรนเดอร์ ในตัวอย่างนี้เรายังแทรกบล็อก CSS เล็ก ๆ เพื่อสาธิตการสไตล์—คุณสามารถเปลี่ยนเป็นมาร์กอัปของคุณเองได้

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
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n" +
               "\n";

// ...
```

## ขั้นตอนที่ 3: สร้าง XPS Rendering Options

สร้างอ็อบเจกต์ `XpsRenderingOptions` เพื่อเก็บการตั้งค่าทั้งหมดที่มีผลต่อการแปลงจาก HTML ไปยัง XPS

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

## ขั้นตอนที่ 4: ปรับขนาดหน้า

กำหนดขนาดหน้าที่กำหนดเอง (กว้าง × สูงเป็นจุด) และบอกเรนเดอร์ให้ขยายอัตโนมัติเพื่อให้พอดีกับหน้าที่กว้างที่สุดหรือไม่ การตั้งค่า `adjustToWidestPage` เป็น `false` จะคงมิติที่คุณระบุไว้

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

## ขั้นตอนที่ 5: เรนเดอร์ผลลัพธ์

สุดท้าย สร้าง `XpsDevice` ด้วยตัวเลือกที่กำหนดแล้วและเรนเดอร์เอกสาร HTML ผลลัพธ์คือไฟล์ XPS ที่สมบูรณ์พร้อมขนาดหน้าที่กำหนดเองของคุณ

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## ปัญหาที่พบบ่อยและวิธีแก้

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|----------|
| **XPS ผลลัพธ์เป็นไฟล์เปล่า** | สตรีมอินพุตไม่ได้ปิดหรือ `HTMLDocument` ชี้ไปที่ไฟล์ผิด | ตรวจสอบให้แน่ใจว่า `FileInputStream` ถูกห่อด้วย `try‑with‑resources` อย่างถูกต้องและเส้นทางไฟล์แม่นยำ |
| **ขนาดหน้าไม่ถูกนำไปใช้** | `adjustToWidestPage` ยังตั้งเป็น `true` | ตั้งค่า `pageSetup.setAdjustToWidestPage(false);` ตามที่แสดงในขั้นตอน 4 |
| **CSS ไม่รองรับ** | Aspose.HTML รองรับเพียงส่วนย่อยของ CSS | ใช้การจัดวางพื้นฐาน, ฟอนต์, สี; หลีกเลี่ยงตัวเลือกขั้นสูงหรือ CSS Grid |
| **LicenseException** | รันโดยไม่มีลิขสิทธิ์ที่ถูกต้องในสภาพการผลิต | ใส่ลิขสิทธิ์ชั่วคราวหรือที่ซื้อไว้ก่อนการเรนเดอร์ (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`) |

## คำถามที่พบบ่อย

**ถาม: Aspose.HTML for Java คืออะไร?**  
ตอบ: Aspose.HTML for Java เป็นไลบรารี Java ที่ช่วยให้นักพัฒนาสามารถจัดการและแปลงเอกสาร HTML ไปยังรูปแบบต่าง ๆ เช่น XPS, PDF, และภาพ

**ถาม: จะดาวน์โหลด Aspose.HTML for Java ได้จากที่ไหน?**  
ตอบ: คุณสามารถดาวน์โหลดไลบรารี Aspose.HTML for Java ได้จาก [ลิงก์นี้](https://releases.aspose.com/html/java/)

**ถาม: มีรุ่นทดลองฟรีสำหรับ Aspose.HTML for Java หรือไม่?**  
ตอบ: มี, คุณสามารถรับรุ่นทดลองฟรีได้จาก [ที่นี่](https://releases.aspose.com/)

**ถาม: จะขอรับลิขสิทธิ์ชั่วคราวสำหรับ Aspose.HTML for Java ได้อย่างไร?**  
ตอบ: เพื่อขอรับลิขสิทธิ์ชั่วคราวสำหรับ Aspose.HTML for Java, เยี่ยมชม [หน้านี้](https://purchase.aspose.com/temporary-license/)

**ถาม: มีการสนับสนุนสำหรับ Aspose.HTML for Java หรือไม่?**  
ตอบ: มี, คุณสามารถขอความช่วยเหลือจากชุมชน Aspose ได้ที่ [Aspose Forum](https://forum.aspose.com/)

**ถาม: สามารถแปลง HTML เป็น XPS บนเซิร์ฟเวอร์แบบ headless ได้หรือไม่?**  
ตอบ: แน่นอน, Aspose.HTML ทำงานในสภาพแวดล้อมที่ไม่มี GUI; เพียงแค่ตรวจสอบให้ Java runtime ถูกตั้งค่าอย่างเหมาะสม

**ถาม: ไลบรารีรองรับการตั้งค่าขอบกระดาษแบบกำหนดเองหรือไม่?**  
ตอบ: รองรับ, ใช้ `PageSetup.setMarginTop()`, `setMarginBottom()` ฯลฯ ก่อนกำหนด `PageSetup` ให้กับตัวเลือกการเรนเดอร์

## สรุป

เราได้เดินผ่านกระบวนการทั้งหมดของ **การแปลง HTML เป็น XPS** และการปรับขนาดหน้าโดยใช้ Aspose.HTML for Java ด้วยการทำตามขั้นตอนเหล่านี้ คุณจะสามารถสร้างเอกสาร XPS ที่พร้อมพิมพ์และตรงกับความต้องการการจัดวางของคุณได้อย่างแม่นยำ อย่าลังเลที่จะทดลองกับขนาดหน้าต่าง ๆ, สไตล์ต่าง ๆ, หรือแม้กระทั่งเพิ่มส่วนหัวและส่วนท้ายเพื่อให้เหมาะกับโครงการของคุณ

หากมีคำถามหรือจำเป็นต้องการความช่วยเหลือเพิ่มเติม, สำรวจ [เอกสาร Aspose.HTML for Java](https://reference.aspose.com/html/java/) หรือเข้าร่วมการสนทนาที่ [Aspose Forum](https://forum.aspose.com/)

---

**อัปเดตล่าสุด:** 2025-11-29  
**ทดสอบกับ:** Aspose.HTML for Java 24.11 (ล่าสุด ณ เวลาที่เขียน)  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}