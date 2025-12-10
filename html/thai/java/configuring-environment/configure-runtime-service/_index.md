---
date: 2025-12-10
description: เรียนรู้วิธีตั้งค่า timeout ใน Aspose.HTML สำหรับ Java, กำหนดค่า Runtime
  Service เพื่อแปลง HTML เป็น PNG, ป้องกันลูปไม่สิ้นสุด, และเพิ่มประสิทธิภาพ
linktitle: Configure Runtime Service in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: วิธีตั้งค่า Timeout ใน Aspose.HTML สำหรับบริการรันไทม์ Java
url: /th/java/configuring-environment/configure-runtime-service/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีตั้งค่า Timeout ใน Aspose.HTML สำหรับ Java Runtime Service

## บทนำ
หากคุณกำลังมองหา **วิธีตั้งค่า timeout** สำหรับสคริปต์เมื่อทำงานกับ Aspose.HTML สำหรับ Java คุณมาถูกที่แล้ว การควบคุมการทำงานของสคริปต์ไม่เพียงแต่ป้องกันลูปไม่สิ้นสุด แต่ยังช่วยให้คุณ **แปลง html เป็น png** ได้เร็วขึ้นและทำให้แอปพลิเคชันของคุณตอบสนองได้ดี ในบทแนะนำนี้เราจะอธิบายขั้นตอนที่แน่นอนเพื่อกำหนดค่า Runtime Service, จำกัดการทำงานของสคริปต์, และในที่สุดสร้างภาพ PNG จาก HTML โดยไม่ทำให้โปรแกรมค้าง

## คำตอบอย่างรวดเร็ว
- **Runtime Service ทำอะไร?** มันช่วยให้คุณควบคุมเวลาการทำงานของสคริปต์และจัดการทรัพยากรขณะประมวลผล HTML.  
- **วิธีตั้งค่า timeout สำหรับ JavaScript?** ใช้ `runtimeService.setJavaScriptTimeout(TimeSpan.fromSeconds(...))`.  
- **ฉันสามารถป้องกันลูปไม่สิ้นสุดได้หรือไม่?** ได้ – timeout จะหยุดลูปที่เกินขีดจำกัดที่กำหนด.  
- **การแปลง HTML‑to‑PNG จะได้รับผลกระทบหรือไม่?** ไม่, การแปลงจะดำเนินต่อเมื่อสคริปต์เสร็จหรือถูกยกเลิกโดย timeout.  
- **ต้องการเวอร์ชันของ Aspose.HTML ใด?** เวอร์ชันล่าสุดจากหน้าดาวน์โหลดของ Aspose.

## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะลงลึกในรายละเอียด โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้:

1. **Java Development Kit (JDK)** – ติดตั้งจาก [Oracle's website](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java Library** – ดาวน์โหลดเวอร์ชันล่าสุดจาก [Aspose releases page](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse หรือ NetBeans จะใช้งานได้ดี.  
4. **Basic Java & HTML knowledge** – จำเป็นสำหรับการทำตามตัวอย่างโค้ด.

## นำเข้าแพ็กเกจ
ก่อนอื่น ให้นำเข้าคลาสที่คุณต้องการใช้ การนำเข้า `java.io.IOException` จำเป็นสำหรับการจัดการไฟล์.

```java
import java.io.IOException;
```

## ขั้นตอนที่ 1: สร้างไฟล์ HTML พร้อมโค้ด JavaScript
เราจะเริ่มด้วยการสร้างไฟล์ HTML ง่าย ๆ ที่มีลูป JavaScript ลูปนี้จะทำงานตลอดไปหากเราไม่ได้กำหนด timeout ทำให้เป็นตัวอย่างที่สมบูรณ์แบบสำหรับ Runtime Service.

```java
String code = "<h1>Runtime Service</h1>\r\n" +
        "<script> while(true) {} </script>\r\n" +
        "<p>The Runtime Service optimizes your system by helping it start apps and programs faster.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("runtime-service.html")) {
    fileWriter.write(code);
}
```

- สคริปต์ `while(true) {}` แสดงถึงลูปที่อาจเป็นลูปไม่สิ้นสุด.  
- `FileWriter` เขียนเนื้อหา HTML ไปยัง **runtime-service.html**.

## ขั้นตอนที่ 2: ตั้งค่าอ็อบเจ็กต์ Configuration
ต่อไป สร้างอินสแตนซ์ของ `Configuration` อ็อบเจ็กต์นี้เป็นโครงสร้างหลักสำหรับบริการทั้งหมดของ Aspose.HTML รวมถึง Runtime Service.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## ขั้นตอนที่ 3: กำหนดค่า Runtime Service
นี่คือจุดที่เราจริง ๆ **ตั้งค่า timeout** โดยการดึง `IRuntimeService` จาก configuration เราสามารถกำหนดขีดจำกัดการทำงานของ JavaScript ได้.

```java
try {
    com.aspose.html.services.IRuntimeService runtimeService = configuration.getService(com.aspose.html.services.IRuntimeService.class);
    runtimeService.setJavaScriptTimeout(com.aspose.html.utils.TimeSpan.fromSeconds(5));
```

- `setJavaScriptTimeout` จำกัดการทำงานของสคริปต์ที่ **5 วินาที** ทำให้ **ป้องกันลูปไม่สิ้นสุด**.  
- สิ่งนี้ยัง **จำกัดการทำงานของสคริปต์** สำหรับโค้ดฝั่งไคลเอนต์ที่หนัก.

## ขั้นตอนที่ 4: โหลดเอกสาร HTML ด้วย Configuration
ตอนนี้โหลดไฟล์ HTML โดยใช้ configuration ที่มีกฎ timeout ของเรา.

```java
    com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("runtime-service.html", configuration);
```

- เอกสารจะเคารพ timeout ที่กำหนดไว้ก่อนหน้า ดังนั้นลูปที่ไม่มีที่สิ้นสุดจะถูกหยุดหลังจาก 5 วินาที.

## ขั้นตอนที่ 5: แปลง HTML เป็น PNG
เมื่อโหลดเอกสารอย่างปลอดภัยแล้ว เราสามารถ **แปลง html เป็น png** ได้ การแปลงจะเกิดขึ้นเฉพาะหลังจากสคริปต์เสร็จหรือถูกยกเลิกโดย timeout.

```java
    com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.ImageSaveOptions(),
        "runtime-service_out.png"
    );
```

- `ImageSaveOptions` บอก Aspose.HTML ให้บันทึกเป็นภาพ PNG.  
- ไฟล์ที่ได้, **runtime-service_out.png**, แสดง HTML ที่เรนเดอร์แล้วโดยไม่ค้าง.

## ขั้นตอนที่ 6: ทำความสะอาดทรัพยากร
สุดท้าย ให้ทำการ dispose อ็อบเจ็กต์เพื่อปลดปล่อยหน่วยความจำและหลีกเลี่ยงการรั่วไหล.

```java
} finally {
    if (document != null) {
        document.dispose();
    }
    if (configuration != null) {
        configuration.dispose();
    }
}
```

- การทำ disposal อย่างเหมาะสมเป็นสิ่งสำคัญสำหรับแอปพลิเคชันที่ทำงานเป็นเวลานาน.

## สรุป
คุณเพิ่งเรียนรู้ **วิธีตั้งค่า timeout** สำหรับการทำงานของ JavaScript ใน Aspose.HTML สำหรับ Java, วิธี **ป้องกันลูปไม่สิ้นสุด**, และวิธี **แปลง html เป็น png** อย่างปลอดภัย ด้วยการกำหนดค่า Runtime Service คุณจะได้การควบคุมพฤติกรรมของสคริปต์อย่างละเอียด ซึ่งทำให้เวลาเริ่มต้นเร็วขึ้นและการแปลงมีความน่าเชื่อถือมากขึ้น ทดลองใช้ค่า timeout ต่าง ๆ ให้เหมาะกับงานของคุณ แล้วคุณจะเห็นการเพิ่มประสิทธิภาพที่ชัดเจน.

## คำถามที่พบบ่อย

**Q: จุดประสงค์ของ Runtime Service ใน Aspose.HTML สำหรับ Java คืออะไร?**  
A: มันช่วยให้คุณควบคุมเวลาการทำงานของสคริปต์, ช่วย **ป้องกันลูปไม่สิ้นสุด** และทำให้การแปลงตอบสนองได้ดี  

**Q: ฉันจะดาวน์โหลด Aspose.HTML สำหรับ Java ได้อย่างไร?**  
A: ดาวน์โหลดเวอร์ชันล่าสุดจาก [releases page](https://releases.aspose.com/html/java/).  

**Q: จำเป็นต้องทำการ dispose อ็อบเจ็กต์ `document` และ `configuration` หรือไม่?**  
A: ใช่, การทำ dispose จะปล่อยทรัพยากรเนทีฟและป้องกันการรั่วไหลของหน่วยความจำ.  

**Q: ฉันสามารถตั้งค่า JavaScript timeout เป็นค่าที่ไม่ใช่ 5 วินาทีได้หรือไม่?**  
A: แน่นอน – เปลี่ยนค่าอาร์กิวเมนต์ของ `TimeSpan.fromSeconds()` ให้เป็นขีดจำกัดที่เหมาะกับสถานการณ์ของคุณ.  

**Q: ฉันจะหาความช่วยเหลือได้จากที่ไหนหากเจอปัญหา?**  
A: เยี่ยมชม [Aspose.HTML forum](https://forum.aspose.com/c/html/29) เพื่อรับความช่วยเหลือจากชุมชนและทีมงาน.  

---

**อัปเดตล่าสุด:** 2025-12-10  
**ทดสอบกับ:** Aspose.HTML for Java 24.11 (latest)  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}