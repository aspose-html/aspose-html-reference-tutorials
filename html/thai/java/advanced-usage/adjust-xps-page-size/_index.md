---
date: 2026-03-18
description: เรียนรู้วิธีแปลง HTML เป็น XPS และปรับขนาดหน้ากระดาษ XPS ด้วย Aspose.HTML
  สำหรับ Java ควบคุมขนาดผลลัพธ์ได้อย่างง่ายดาย.
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: แปลง HTML เป็น XPS และปรับขนาดหน้าของ XPS ด้วย Aspose.HTML สำหรับ Java
url: /th/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลง HTML เป็น XPS และปรับขนาดหน้า XPS ด้วย Aspose.HTML สำหรับ Java

ในบทแนะนำนี้คุณจะได้ค้นพบ **วิธีแปลง HTML เป็น XPS** และปรับขนาดหน้าที่ได้อย่างละเอียดโดยใช้ Aspose.HTML สำหรับ Java ไม่ว่าคุณจะสร้างรายงานที่พิมพ์ได้ ใบแจ้งหนี้ หรือเอกสารเก็บถาวร การควบคุมขนาดของ XPS จะทำให้ผลลัพธ์ออกมาตรงตามที่คุณคาดหวัง เราจะเดินผ่านทุกขั้นตอน—ตั้งแต่การตั้งค่าสภาพแวดล้อมจนถึงการเรนเดอร์ไฟล์ XPS สุดท้าย—เพื่อให้คุณสามารถรวมความสามารถนี้เข้าไปในแอปพลิเคชัน Java ของคุณได้ทันที

## คำตอบด่วน
- **What does “convert HTML to XPS” mean?** มันทำการเรนเดอร์เอกสาร HTML เป็นไฟล์ XPS โดยคงรูปแบบและสไตล์ไว้  
- **Do I need a license?** การทดลองใช้ฟรีใช้ได้สำหรับการพัฒนา; จำเป็นต้องมีลิขสิทธิ์เชิงพาณิชย์สำหรับการใช้งานจริง.  
- **Which Java version is supported?** Java 8 หรือสูงกว่า (แนะนำ JDK 11+)  
- **Can I change page size?** ใช่ – Aspose.HTML ให้คุณระบุขนาดที่กำหนดเองก่อนการเรนเดอร์  
- **How long does the conversion take?** ปกติใช้เวลาน้อยกว่าวินาทีสำหรับหน้าแบบมาตรฐาน; เอกสารที่ใหญ่กว่าอาจใช้เวลานานขึ้น  

## การแปลง HTML เป็น XPS คืออะไร?
การแปลง HTML เป็น XPS หมายถึงการนำไฟล์มาร์กอัปที่ออกแบบสำหรับเว็บมาผลิตเป็นเอกสาร XPS (XML Paper Specification) — รูปแบบที่มีการจัดวางคงที่พร้อมพิมพ์ที่คล้ายกับ PDF สิ่งนี้มีประโยชน์เมื่อคุณต้องการเอกสารที่มีความแม่นยำสูงและไม่ขึ้นกับอุปกรณ์สำหรับการเก็บถาวรหรือการพิมพ์จากแอปพลิเคชัน Java

## ทำไมต้องปรับขนาดหน้าของ XPS?
การปรับขนาดหน้าจะให้คุณควบคุมมิติทางกายภาพของเอกสารสุดท้าย (เช่น A4, Letter, ป้ายกำหนดเอง) มันช่วยป้องกันการย่อขยายที่ไม่ต้องการ, ทำให้เนื้อหาเข้ากันได้อย่างสมบูรณ์, และสามารถลดขนาดไฟล์โดยการกำจัดพื้นที่ว่างที่ไม่จำเป็น

## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่ม, โปรดตรวจสอบว่าคุณมีข้อกำหนดต่อไปนี้พร้อมใช้งาน:

1. **Java Development Environment** – Java Development Kit (JDK) ที่ติดตั้งบนระบบของคุณ.  
2. **Aspose.HTML for Java Library** – ดาวน์โหลดและรวมไลบรารี Aspose.HTML for Java เข้าในโปรเจกต์ของคุณ คุณสามารถหาไลบรารีได้จาก [here](https://releases.aspose.com/html/java/).  
3. **Input HTML File** – เตรียมไฟล์ HTML ที่คุณต้องการเรนเดอร์และปรับขนาดหน้า XPS สำหรับไฟล์นั้น คุณสามารถใช้ไฟล์ HTML ของคุณเองสำหรับบทแนะนำนี้.

## นำเข้าแพ็กเกจ
ก่อนอื่น, นำเข้าคลาสที่คุณต้องการ แพ็กเกจเหล่านี้ให้คุณเข้าถึงการจัดการเอกสาร, การเรนเดอร์, และคุณสมบัติการตั้งค่าหน้า.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## คู่มือขั้นตอนต่อขั้นตอน
ด้านล่างเป็นขั้นตอนสั้น ๆ ที่จัดเป็นลำดับเลขที่สะท้อนขั้นตอนเดิมพร้อมเพิ่มบริบทเพิ่มเติมเพื่อความชัดเจน.

### ขั้นตอนที่ 1: ตั้งชื่อไฟล์อินพุต
อ่านไฟล์ HTML ต้นฉบับโดยใช้ `FileInputStream`. สตรีมนี้จะส่งข้อมูล HTML ดิบเข้าสู่เอ็นจิ้น Aspose.HTML.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

### ขั้นตอนที่ 2: สร้าง HTML Document และตั้งค่า Styles
สร้างอินสแตนซ์ `HTMLDocument` ที่เป็นตัวแทนของเนื้อหาที่คุณจะเรนเดอร์ ในตัวอย่างนี้เรายังแทรกบล็อก CSS เล็ก ๆ เพื่อสาธิตการจัดสไตล์—คุณสามารถแทนที่ด้วยมาร์กอัปของคุณเองได้ตามต้องการ.

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

### ขั้นตอนที่ 3: สร้าง XPS Rendering Options
สร้างอินสแตนซ์ `XpsRenderingOptions` เพื่อเก็บการตั้งค่าทั้งหมดที่มีผลต่อการแปลงจาก HTML เป็น XPS.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

### ขั้นตอนที่ 4: ปรับขนาดหน้า  
**How to set XPS page size** – กำหนดขนาดหน้าที่กำหนดเอง (ความกว้าง × ความสูงเป็นหน่วย points) และบอก renderer ว่าควรขยายอัตโนมัติเพื่อให้ครอบคลุมหน้าที่กว้างที่สุดหรือไม่ การตั้งค่า `adjustToWidestPage` เป็น `false` จะคงขนาดที่คุณระบุไว้โดยตรง.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

### ขั้นตอนที่ 5: เรนเดอร์ผลลัพธ์
สุดท้าย, สร้าง `XpsDevice` ด้วยตัวเลือกที่กำหนดและเรนเดอร์เอกสาร HTML ผลลัพธ์คือไฟล์ XPS ที่สมบูรณ์พร้อมขนาดหน้าที่กำหนดเองที่คุณตั้งค่า.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## ปัญหาทั่วไปและวิธีแก้

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|--------|
| **Blank XPS output** | สตรีมอินพุตไม่ได้ปิดหรือ `HTMLDocument` ชี้ไปยังไฟล์ที่ผิด. | ตรวจสอบให้แน่ใจว่า `FileInputStream` ถูกห่อหุ้มอย่างถูกต้องในบล็อก try‑with‑resources และเส้นทางไฟล์ถูกต้อง. |
| **Page size not applied** | `adjustToWidestPage` ถูกตั้งเป็น `true`. | ตั้งค่า `pageSetup.setAdjustToWidestPage(false);` ตามที่แสดงในขั้นตอน 4. |
| **Unsupported CSS** | Aspose.HTML รองรับเพียงส่วนย่อยของ CSS. | ใช้การจัดวางพื้นฐาน, ฟอนต์, และสี; หลีกเลี่ยงตัวเลือกขั้นสูงหรือ CSS Grid. |
| **LicenseException** | ทำงานโดยไม่มีลิขสิทธิ์ที่ถูกต้องในสภาพการผลิต. | ใช้ลิขสิทธิ์ชั่วคราวหรือที่ซื้อไว้ก่อนการเรนเดอร์ (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## คำถามที่พบบ่อย

**Q: What is Aspose.HTML for Java?**  
A: Aspose.HTML for Java คือไลบรารี Java ที่ช่วยให้นักพัฒนาสามารถจัดการและแปลงเอกสาร HTML ไปยังรูปแบบต่าง ๆ เช่น XPS, PDF, และรูปภาพ.

**Q: Where can I download Aspose.HTML for Java?**  
A: คุณสามารถดาวน์โหลดไลบรารี Aspose.HTML for Java ได้จาก [this link](https://releases.aspose.com/html/java/).

**Q: Is there a free trial available for Aspose.HTML for Java?**  
A: มี, คุณสามารถรับการทดลองใช้ฟรีของ Aspose.HTML for Java ได้จาก [here](https://releases.aspose.com/).

**Q: How can I obtain a temporary license for Aspose.HTML for Java?**  
A: เพื่อรับลิขสิทธิ์ชั่วคราวสำหรับ Aspose.HTML for Java, เยี่ยมชม [this page](https://purchase.aspose.com/temporary-license/).

**Q: Can I get support for Aspose.HTML for Java?**  
A: ได้, คุณสามารถขอความช่วยเหลือและสนับสนุนจากชุมชน Aspose ที่ [Aspose Forum](https://forum.aspose.com/).

**Q: Can I convert HTML to XPS on a headless server?**  
A: แน่นอน. Aspose.HTML ทำงานในสภาพแวดล้อมที่ไม่มี GUI; เพียงตรวจสอบให้แน่ใจว่า Java runtime ถูกกำหนดค่าอย่างเหมาะสม.

**Q: Does the library support custom page margins?**  
A: ใช่. ใช้ `PageSetup.setMarginTop()`, `setMarginBottom()`, เป็นต้น ก่อนที่จะกำหนด `PageSetup` ให้กับตัวเลือกการเรนเดอร์.

## สรุป
เราได้เดินผ่านกระบวนการทั้งหมดของ **การแปลง HTML เป็น XPS** และการปรับขนาดหน้าโดยใช้ Aspose.HTML for Java ด้วยการทำตามขั้นตอนเหล่านี้คุณสามารถสร้างเอกสาร XPS พร้อมพิมพ์ที่ตรงกับข้อกำหนดการจัดวางของคุณได้อย่างแม่นยำ อย่าลังเลที่จะทดลองกับขนาดหน้าต่าง ๆ, สไตล์, หรือแม้แต่เพิ่มส่วนหัวและส่วนท้ายเพื่อให้เหมาะกับความต้องการของโครงการของคุณ.

หากคุณมีคำถามหรือจำเป็นต้องการความช่วยเหลือเพิ่มเติม, สำรวจ [Aspose.HTML for Java documentation](https://reference.aspose.com/html/java/) หรือเข้าร่วมการสนทนาที่ [Aspose Forum](https://forum.aspose.com/).

---

**อัปเดตล่าสุด:** 2026-03-18  
**ทดสอบด้วย:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}