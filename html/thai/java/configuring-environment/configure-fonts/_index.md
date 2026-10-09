---
date: 2026-02-04
description: เรียนรู้วิธีใช้ Aspose.HTML เพื่อกำหนดค่าแบบอักษร, ใช้ CSS แบบกำหนดเอง,
  ใช้ใบอนุญาตชั่วคราว, และสร้าง PDF จาก HTML ด้วย Java.
linktitle: Configure Fonts in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: วิธีใช้ Aspose.HTML เพื่อกำหนดฟอนต์สำหรับการแปลง HTML เป็น PDF ด้วย Java
url: /th/java/configuring-environment/configure-fonts/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# กำหนดค่าแบบอักษรสำหรับ HTML‑to‑PDF Java ด้วย Aspose.HTML

## การแนะนำ
บทแนะนำนี้คุณจะได้สัมผัส ** ใช้ Aspose.HTML** เพื่อเป็นแนวทางสำหรับ HTML-to-PDF ใน Java สำหรับเอกสาร HTML อย่างเป็นทางการสำหรับ PDF ของข้อมูลอย่างเป็นทางการอย่างใดอย่างหนึ่ง— รักษาสีแบรนด์, การพิมพ์, และการดำเนินการวางรายงาน, เครื่องแบบ, หรือระบบสร้างเอกสารใด ๆ นวัตกรรมใหม่ ๆ ที่เป็นหลักการสำคัญสำหรับ PDF การพิจารณาคดีทั้งหมดการพิจารณาคดีจนถึง HTML ในองค์กรและ CSS องค์กร

## คำตอบด่วน
- ** คำอธิบายบทแนะนำนี้คืออะไร?** คำอธิบายสำหรับการอ้างอิง HTML‑to‑PDF ใน Java ด้วย Aspose.HTML
- **ไลบรารีใด ๆ ที่เราทานอาหาร?**Aspose.HTML for Java (คลาส `Converter`).
- ** ยืนยันไลเซนส์หรือไม่?** ไลเซนส์ชั่วคราวของ Aspose จะลบข้อจำกัดความเชื่อ; กินไลเซนส์เต็มเลยจริง.
- **ควรวางและตามที่บันทึกไว้ที่ไหน?** ในที่เก็บข้อมูลโดย `FontsLookupFolder` แปลว่า `fonts` อาจจะติดกับโปรเจคของคุณ
- **ฉันสามารถตรวจสอบผลลัพธ์ PDF ได้หรือไม่**ได้—ใช้ `PdfSaveOptions` ในการควบคุมหน้า, ระยะขอบ, คุณสามารถได้

## วิธีใช้ Aspose.HTML สำหรับการกำหนดค่าแบบอักษร
เราจะอธิบายการจัดการและมีความสำคัญอย่างไร, วิธีการใช้ CSS และวิธีการ **ใช้ไลเซนส์ชั่วคราว** สามารถเปิดใช้งานฟังก์ชั่นเต็มในขณะที่ทดสอบประสิทธิภาพ.

## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่ม, กรุณาตรวจสอบคุณอีกครั้ง:

1. **Java Development Kit (JDK) 1.8+** – โค้ดทำงานบน JDK สแกนบาร์โค้ด
2. **Aspose.HTML สำหรับ Java** – ดาวน์โหลด JAR ล่าสุดจาก [เว็บไซต์ Aspose](https://releases.aspose.com/html/java/)
3. **IDE** – IntelliJ IDEA, Eclipse หรือเครื่องมือแก้ไขที่เข้ากันได้กับ Java ซอฟต์แวร์
4. **ความรู้พื้นฐาน Java** – สำหรับคลาสนี้, เมธอด, ส่วนใหญ่เป็นไฟล์ I/O.
5. **ไลเซนส์ Aspose.HTML** – [ไลเซนส์ชั่วคราว](https://purchase.aspose.com/temporary-license/) จะยกเลิกตามปกติตามปกติ

## แพคเกจนำเข้า
ก่อนอื่นให้ทำการนำเข้าคลาสหลักของ Java และ Aspose.HTML ที่คุณต้องการใช้.  

```java
import java.io.IOException;
```

การนำเข้าดังกล่าวทำให้คุณเข้าถึงการจัดการไฟล์และ API ของ Aspose.HTML.

## **html ถึง pdf java** คืออะไร และเหตุใดการกำหนดค่าแบบอักษรจึงมีความสำคัญ
ระบบปฏิบัติการ **html to pdf java** ทำเรนเดอร์เอกสาร HTML เป็นหน้า PDF การเรนเดอร์ตามลำดับการปฏิบัติตามการเรนเดอร์เพราะส่งผลต่อการปฏิบัติตามการวาง, ระยะทางบรรทัด, และประสิทธิภาพของภาพ แสดงให้เห็นประสิทธิภาพที่ Aspose.HTML ประสิทธิภาพการทำงานของประสิทธิภาพ, คุณจะใช้ PDF ใช้งานได้เหมือนกันที่ออกแบบสำหรับการควบคุม, กำจัดการเรียกคืนและการรักษาความปลอดภัยของแบรนด์

## คำแนะนำทีละขั้นตอน

### ขั้นตอนที่ 1: สร้างเนื้อหา HTML
เริ่มต้นโดยสร้างไฟล์ HTML ง่าย ๆ ที่เราจะแปลงเป็น PDF ต่อไป

#### 1.1 เขียนโค้ด HTML
```java
String code = "<h1>FontsSettings property</h1>\r\n" +
    "<p>The FontsSettings property is used for configuration of fonts handling.</p>\r\n";
```

#### 1.2 บันทึก HTML ลงในไฟล์
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("user-agent-fontsetting.html")) {
    fileWriter.write(code);
}
```

`FileWriter` จะเขียนสตริงไปยังไฟล์ `user-agent-fontsetting.html` ในโฟลเดอร์โปรเจคของคุณ หลังจากขั้นตอนนี้คุณจะมีไฟล์ HTML ที่พร้อมสำหรับการประมวลผล.

### ขั้นตอนที่ 2: กำหนดค่าสภาพแวดล้อม Aspose.HTML
ตอนนี้เราจะตั้งค่าอ็อบเจ็กต์ `Configuration` ของ Aspose.HTML ซึ่งช่วยให้เราควบคุมวิธีการแสดงผล HTML ได้

### 2.1 สร้างอินสแตนซ์ Configuration
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

อ็อบเจกต์ `Configuration` เป็นจุดเริ่มต้นสำหรับการปรับแต่งตัวเลือกการเรนเดอร์ เช่น การจัดการแบบอักษรและพฤติกรรมของ user‑agent.

#### 2.2 เข้าถึงบริการ User Agent
```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

`IUserAgentService` จัดการสไตล์ชีต, แบบอักษร, และรายละเอียดการเรนเดอร์อื่น ๆ เราจะใช้มันเพื่อใส่ CSS ที่กำหนดเองและชี้ไปยังโฟลเดอร์แบบอักษรของเรา.

### ขั้นตอนที่ 3: กำหนดค่าสไตล์และฟอนต์เอง
เมื่อเตรียมสภาพแวดล้อมพร้อมแล้ว เราสามารถเพิ่มกฎ CSS และบอก Aspose.HTML ว่าจะหาฟอนต์ได้จากที่ไหน

#### 3.1 ตั้งค่า CSS เอง
```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; }\r\n" +
    "p { color:grey; }\r\n");
```

CSS นี้ทำให้ส่วนหัวเป็นสีบราวน์และย่อหน้าสีเทา คุณสามารถเพิ่มกฎ CSS ที่ถูกต้องใด ๆ ที่นี่—Aspose.HTML รองรับสเปค CSS2.1 เต็มรูปแบบและฟีเจอร์หลายอย่างของ CSS3 *(นี่คือตัวอย่างของ **apply custom css**.)*

#### 3.2 ชี้ไปยังโฟลเดอร์ฟอนต์ที่กำหนดเอง
```java
userAgent.getFontsSettings().setFontsLookupFolder("fonts");
```

วางไฟล์ `.ttf` หรือ `.otf` ที่คุณต้องการใช้ไว้ในโฟลเดอร์ชื่อ `fonts` ที่อยู่ที่รากของโปรเจค Aspose.HTML จะโหลดแบบอักษรเหล่านี้โดยอัตโนมัติระหว่างการเรนเดอร์.

> **เคล็ดลับ:** หากคุณมีหลายฟอนต์แฟมิลี, ให้จัดระเบียบในโฟลเดอร์ย่อยและเพิ่มโฟลเดอร์แม่แต่ละโฟลเดอร์ลงใน `FontsLookupFolder` โดยใช้รายการคั่นด้วยเซมิโคลอน.

### ขั้นตอนที่ 4: โหลดเอกสาร HTML ที่มีการกำหนดค่าแล้ว
Now we load the HTML file we created earlier, applying the custom configuration we just built.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("user-agent-fontsetting.html", configuration);
```

อ็อบเจกต์ `HTMLDocument` ตอนนี้เป็นตัวแทนของ HTML ที่มีสไตล์พร้อมสำหรับการแปลง.

### ขั้นตอนที่ 5: แปลง HTML เป็น PDF
สุดท้ายนี้ เราจะทำการแปลง **aspose html pdf** เพื่อสร้างไฟล์ PDF ที่คงไว้ซึ่งแบบอักษรและสไตล์ที่เรากำหนดเอง

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.PdfSaveOptions(),
    "user-agent-fontsetting_out.pdf"
);
```

อ็อบเจกต์ `PdfSaveOptions` ให้คุณปรับแต่งการตั้งค่าผลลัพธ์ เช่น ขนาดหน้า, การบีบอัด, และเมตาดาต้า สำหรับการแปลงพื้นฐาน ตัวเลือกเริ่มต้นทำงานได้อย่างสมบูรณ์.

### ขั้นตอนที่ 6: ล้างทรัพยากร
การกำจัดทรัพยากรอย่างเหมาะสมจะช่วยป้องกันการรั่วไหลของหน่วยความจำ โดยเฉพาะอย่างยิ่งเมื่อประมวลผลเอกสารจำนวนมากในแอปพลิเคชันที่ทำงานต่อเนื่องเป็นเวลานาน

#### 6.1 กำจัด HTMLDocument
```java
if (document != null) {
    document.dispose();
}
```

#### 6.2 กำจัด Configuration
```java
if (configuration != null) {
    configuration.dispose();
}
```

การเรียกเหล่านี้จะปล่อยทรัพยากรเนทีฟที่ Aspose.HTML จัดสรร.

## ปัญหาและแนวทางแก้ไขทั่วไป
| ปัญหา | วิธีแก้ |
|-------|----------|
| **ไม่แสดง** | มาดู `fonts` ในการอ้างอิงถึงแหล่งที่มาของไฟล์ `.ttf`/`.otf` ที่ถูกต้องเพื่อใช้เส้นทางแบบเต็มหากติดตามอยู่นอกไดรฟ์ของโปรเจค |
| **PDF ดูเป็นสีขาว** | เส้นทางไฟล์ HTML ถูกต้องและไฟล์สามารถอ่านได้ ในส่วนของอ็อบเจกต์ `Configuration` ให้กับคอนสตรัคเตอร์ของ `HTMLDocument` |
| **สำหรับไลเซนส์** | ใช้ไลเซนส์ชั่วคราวหรือเต็มของ Aspose ก่อนที่จะเรียกใช้ API ของ Aspose ใส่ไฟล์ไลเซนส์ใน classpath และโหลดด้วย `License License = new License(); License.setLicense("Aspose.Total.Java.lic");`. |
| **การเรนเดอร์ CSS ได้ที่** | Aspose.HTML รองรับ CSS ได้ทันทีแต่ไม่รองรับสมัยใหม่ทั้งหมด (เช่น CSS Grid) ทำให้สไตล์ง่ายลงเพื่อรองรับคุณสมบัติ CSS รองรับ |

## คำถามที่พบบ่อย

**Q: ฉันสามารถใช้แบบอักษรใดก็ได้กับ Aspose.HTML สำหรับ Java?**  
A: ใช่, แบบอักษร TrueType (`.ttf`) หรือ OpenType (`.otf`) ใด ๆ ที่ระบบปฏิบัติการของคุณรองรับสามารถใช้ได้ เพียงวางไฟล์เหล่านั้นในโฟลเดอร์ที่คุณตั้งค่าไว้ด้วย `FontsLookupFolder`.

**Q: ฉันต้องการไลเซนส์เพื่อใช้ Aspose.HTML สำหรับ Java หรือไม่?**  
A: แม้ว่าคุณจะประเมินไลบรารีโดยไม่มีไลเซนส์ได้, [ไลเซนส์ชั่วคราวของ Aspose](https://purchase.aspose.com/temporary-license/) จะยกเลิกข้อจำกัดการประเมิน. สำหรับการใช้งานจริง, จำเป็นต้องมีไลเซนส์เต็ม.

**Q: ฉันสามารถปรับแต่งผลลัพธ์ PDF ได้อย่างไร?**  
A: ส่งอินสแตนซ์ `PdfSaveOptions` ที่กำหนดค่าแล้วไปยัง `convertHTML`. คุณสามารถตั้งค่าขนาดหน้า, ระยะขอบ, ระดับการบีบอัด, และอื่น ๆ.

**Q: สามารถใช้สไตล์ CSS ที่ซับซ้อนได้หรือไม่?**  
A: ได้, Aspose.HTML รองรับช่วงกว้างของ CSS. ตัวเลือกซับซ้อน, media queries, และ pseudo‑classes ทำงานเช่นเดียวกับในเบราว์เซอร์, แม้ว่าบางคุณลักษณะใหม่ของ CSS3/4 อาจไม่ได้รับการสนับสนุนเต็มที่.

**Q: จะหา ตัวอย่างและเอกสารเพิ่มเติมได้จากที่ไหน?**  
A: เยี่ยมชมหน้า [Aspose.HTML for Java documentation page](https://reference.aspose.com/html/java/) อย่างเป็นทางการเพื่อดูอ้างอิง API รายละเอียดและตัวอย่างโค้ดเพิ่มเติม.

**Q: ไลเซนส์ชั่วคราวของ Aspose มีผลต่อการแปลงอย่างไร?**  
A: ไลเซนส์ชั่วคราวยกเลิกข้อจำกัด 10 หน้าและลายน้ำที่ปรากฏในโหมดประเมิน, ทำให้คุณสามารถทดสอบกระบวนการ **aspose html pdf conversion** ได้อย่างเต็มที่.

---

**อัปเดตล่าสุด:** 2026-02-04  
**ทดสอบกับ:** Aspose.HTML for Java 24.12 (ล่าสุด ณ เวลาที่เขียน)  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}