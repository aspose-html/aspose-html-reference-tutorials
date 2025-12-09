---
date: 2025-12-05
description: เรียนรู้วิธีสร้างไฟล์ HTML, จัดการทรัพยากรเครือข่าย, และแปลง HTML เป็น
  PNG ด้วย Aspose.HTML สำหรับ Java พร้อมการจัดการข้อผิดพลาดแบบกำหนดเอง.
linktitle: Set Up Network Service in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: สร้างไฟล์ HTML และตั้งค่าบริการเครือข่าย (Aspose.HTML Java)
url: /th/java/configuring-environment/setup-network-service/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้างไฟล์ HTML & ตั้งค่า Network Service (Aspose.HTML Java)

## บทนำ
หากคุณต้องการ **create html file** ที่ดึงรูปภาพจากเว็บแล้วแปลงหน้านั้นเป็นรูปภาพ คุณมาถูกที่แล้ว ในบทเรียนนี้เราจะอธิบายทุกขั้นตอนที่จำเป็นในการกำหนดค่า Aspose.HTML สำหรับ Java, **manage network resources**, จัดการทรัพยากรที่หายไปด้วยตัวจัดการข้อผิดพลาดแบบกำหนดเอง, **convert html to png**, และสุดท้าย **clean up resources** เพื่อให้แอปพลิเคชันของคุณทำงานได้อย่างดี ไม่ว่าคุณจะสร้างเครื่องมือรายงาน, ตัวสร้างภาพย่ออัตโนมัติ, หรือแค่ทดลองแปลง HTML‑to‑image รูปแบบที่แสดงที่นี่จะช่วยประหยัดเวลาและลดปัญหา

## คำตอบอย่างรวดเร็ว
- **What is the first step?** สร้างไฟล์ HTML ที่อ้างอิงรูปภาพที่โฮสต์บนเครือข่าย.  
- **Which class configures networking?** `com.aspose.html.Configuration`.  
- **How do I capture load errors?** เพิ่ม `MessageHandler` แบบกำหนดเองไปยัง `INetworkService`.  
- **What output format does this example produce?** ภาพ PNG (`output.png`).  
- **Do I need to release objects?** ใช่ – เรียก `dispose()` ทั้งบนเอกสารและการกำหนดค่า.

## ข้อกำหนดเบื้องต้น
ก่อนจะดำดิ่งเข้าสู่การตั้งค่าจริง ให้เราตรวจสอบว่าคุณมีทุกอย่างที่จำเป็นเพื่อเริ่มต้นแล้ว:
- **Java Development Kit (JDK)** 1.8 หรือใหม่กว่า.  
- **Aspose.HTML for Java** library – ดาวน์โหลดเวอร์ชันล่าสุดจาก [official release page](https://releases.aspose.com/html/java/).  
- **IDE** ที่คุณเลือก (IntelliJ IDEA, Eclipse, NetBeans ฯลฯ).  
- ความคุ้นเคยพื้นฐานกับไวยากรณ์ Java และการตั้งค่าโครงการ Maven/Gradle.

## นำเข้าแพ็กเกจ
ขั้นตอนแรกคุณต้องนำเข้าแพ็กเกจที่จำเป็นเข้าสู่โครงการ Java ของคุณ แพ็กเกจเหล่านี้จะทำให้คุณสามารถใช้ฟังก์ชันต่าง ๆ ของ Aspose.HTML for Java ได้

```java
import java.io.IOException;
```

การนำเข้าเหล่านี้เป็นโครงสร้างหลักของฟังก์ชันที่เราจะพูดถึง ดังนั้นตรวจสอบให้แน่ใจว่าตั้งไว้ที่ส่วนต้นของไฟล์ Java ของคุณ

## ขั้นตอนที่ 1: สร้างไฟล์ HTML พร้อมรูปภาพที่พึ่งพาเครือข่าย
เพื่อ **create html file** ที่อ้างอิงทรัพยากรภายนอก ให้เขียนโค้ดสั้น ๆ ที่แทรกแท็ก `<img>` จำนวนไม่กี่ตัวชี้ไปยังรูปภาพที่เปิดให้สาธารณะ

```java
String code = "<img src=\"https://docs.aspose.com/svg/net/drawing-basics/filters-and-gradients/park.jpg\" >\r\n" +
        "<img src=\"https://docs.aspose.com/html/net/missing1.jpg\" >\r\n" +
        "<img src=\"https://docs.aspose.com/html/net/missing2.jpg\" >\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

ไฟล์ HTML นี้เป็นจุดเริ่มต้นของ network service; รูปภาพจะถูกดึงผ่าน HTTP เมื่อเอกสารถูกโหลด

## ขั้นตอนที่ 2: เริ่มต้นอ็อบเจ็กต์ Configuration
ตอนนี้เรามาสร้าง **configuration** ที่จะเก็บการตั้งค่า network‑service ของเรา

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

อ็อบเจ็กต์ `Configuration` คือที่คุณจะระบุว่าต้องการให้ Aspose.HTML จัดการการจราจรเครือข่าย การบันทึก และการจัดการข้อผิดพลาดอย่างไร

## ขั้นตอนที่ 3: เพิ่มตัวจัดการข้อความข้อผิดพลาดแบบกำหนดเอง
`MessageHandler` แบบกำหนดเองช่วยให้คุณมองเห็นปัญหาเช่นรูปภาพหายหรือการหมดเวลา

```java
com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
com.aspose.html.net.MessageHandler logHandler = new LogMessageHandler();
network.getMessageHandlers().addItem(logHandler);
```

โดยการแนบ `LogMessageHandler` คำเตือนหรือข้อผิดพลาดที่เกี่ยวข้องกับเครือข่ายทั้งหมดจะถูกบันทึก ทำให้การดีบักเป็นเรื่องง่าย

## ขั้นตอนที่ 4: โหลดเอกสาร HTML ด้วย Configuration
เมื่อ network service พร้อมแล้ว ให้โหลดไฟล์ HTML ที่เราสร้างไว้ก่อนหน้านี้

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
```

เมื่อเอกสารถูกโหลด Aspose.HTML จะใช้การกำหนดค่าเครือข่ายแบบกำหนดเองและเรียกตัวจัดการข้อความของเราสำหรับปัญหาใด ๆ

## ขั้นตอนที่ 5: แปลง HTML เป็น PNG
ตอนนี้เราจะ **convert html to png** โดยแปลงหน้าที่โหลดแล้ว (รวมถึงรูปภาพที่ดึงสำเร็จ) เป็นภาพเรสเตอร์

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

ผลลัพธ์คือไฟล์ PNG เดียว (`output.png`) ที่คุณสามารถฝังในที่อื่นหรือให้บริการแก่ผู้ใช้

## ขั้นตอนที่ 6: ทำความสะอาดทรัพยากร
การจัดการทรัพยากรอย่างเหมาะสมเป็นสิ่งสำคัญ หลังจากการแปลงให้ปล่อยอ็อบเจ็กต์เพื่อ **clean up resources** และหลีกเลี่ยงการรั่วไหลของหน่วยความจำ

```java
if (document != null) {
    document.dispose();
}
if (configuration != null) {
    configuration.dispose();
}
```

คิดว่ามันเหมือนการล้างจานหลังมื้ออาหาร—การปล่อยทรัพยากรค้างไว้สามารถทำให้เกิดปัญหาประสิทธิภาพในภายหลัง

## ปัญหาที่พบบ่อยและวิธีแก้
| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|----------|
| Images fail to load | การหมดเวลาเครือข่ายหรือ URL ผิด | ตรวจสอบ URL, เพิ่มเวลา timeout ผ่านการตั้งค่า `NetworkService`, หรือเพิ่มตรรกะสำรองใน `LogMessageHandler`. |
| PNG is blank | เอกสารไม่ได้โหลดเต็มก่อนการแปลง | ตรวจสอบให้แน่ใจว่า `HTMLDocument` ถูกสร้างด้วย configuration ที่รวมตัวจัดการแบบกำหนดเอง; สามารถเรียก `document.waitForLoad()` หากใช้การโหลดแบบ async. |
| Out‑of‑memory error | HTML ขนาดใหญ่มากหรือมีรูปภาพความละเอียดสูงจำนวนมาก | ใช้ `ImageSaveOptions.setMaxWidth/MaxHeight` เพื่อลดขนาดผลลัพธ์, หรือทำการ dispose อ็อบเจ็กต์กลางโดยเร็ว. |

## คำถามที่พบบ่อย

**Q: จุดประสงค์หลักของการตั้งค่า network service ใน Aspose.HTML for Java คืออะไร?**  
A: มันทำให้คุณ **manage network resources** เช่นรูปภาพระยะไกล, สคริปต์, หรือสไตล์ชีต, และให้คุณควบคุมการจัดการข้อผิดพลาดและการบันทึก  

**Q: ฉันสามารถใช้การตั้งค่านี้เพื่อสร้างรูปแบบภาพอื่น ๆ (เช่น JPEG, BMP) ได้หรือไม่?**  
A: ได้—เพียงเปลี่ยนคุณสมบัติ format ของ `ImageSaveOptions` ไปเป็นประเภทผลลัพธ์ที่ต้องการ  

**Q: ตัวจัดการ `MessageHandler` แบบกำหนดเองแตกต่างจาก logger เริ่มต้นอย่างไร?**  
A: ตัวจัดการแบบกำหนดเองทำให้คุณส่งข้อความไปยังเฟรมเวิร์กการบันทึกของคุณเอง, กรองคำเตือนเฉพาะ, หรือเรียกแจ้งเตือน, ในขณะที่ logger เริ่มต้นจะเขียนเฉพาะไปยังคอนโซล  

**Q: จำเป็นต้องเรียก `dispose()` ทั้งบนเอกสารและการกำหนดค่าหรือไม่?**  
A: แน่นอน การ dispose จะปล่อยทรัพยากรพื้นฐานและ **cleans up resources** ที่ไลบรารีถือไว้ภายใน  

**Q: ฉันจะหา ตัวอย่างเพิ่มเติมของการแปลง HTML เป็นภาพใน Java ได้จากที่ไหน?**  
A: ตรวจสอบเอกสาร Aspose.HTML for Java และหน้าตัวอย่างอย่างเป็นทางการบน GitHub สำหรับกรณีการใช้งานเพิ่มเติม เช่น การแปลงเป็น PDF, การเรนเดอร์ SVG, และการประมวลผลแบบแบตช์  

---

**Last Updated:** 2025-12-05  
**Tested With:** Aspose.HTML for Java 24.12 (latest)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}