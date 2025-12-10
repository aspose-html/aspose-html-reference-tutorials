---
date: 2025-12-10
description: เรียนรู้วิธีใช้ Aspose เพื่อจัดการลิงก์ที่เสียใน Java, แปลง HTML เป็น
  PNG และโหลดเอกสาร HTML ด้วย Aspose.HTML สำหรับ Java.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: วิธีใช้ตัวจัดการข้อความ Aspose.HTML ใน Java
url: /th/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ Aspose.HTML Message Handlers ใน Java

## บทนำ
ในบทแนะนำนี้, **how to use aspose** สำหรับการจัดการทรัพยากรที่หายไปใน HTML จะถูกสาธิตแบบขั้นตอนต่อขั้นตอน เราจะสร้างเอกสาร HTML ง่าย ๆ ที่อ้างอิงรูปภาพที่ไม่มีอยู่, แนบตัวจัดการข้อความแบบกำหนดเอง, และแสดงวิธี **load html document java** พร้อมกับจัดการลิงก์ที่เสียอย่างราบรื่น เมื่อเสร็จสิ้น คุณจะได้เห็นวิธี **convert html to png** ด้วย Aspose.HTML ซึ่งจะให้ภาพรวมครบถ้วนของการแปลง HTML เป็นภาพใน Java.

## คำตอบอย่างรวดเร็ว
- **What is the primary purpose of a message handler?** เพื่อดักจับการทำงานของเครือข่ายและตอบสนองต่อรหัสสถานะเช่นทรัพยากรที่หายไป.  
- **Can Aspose.HTML convert HTML to PNG?** ใช่, โดยใช้ `Converter.convertHTML` คุณสามารถทำการแปลง html เป็นภาพได้.  
- **Do I need a license for this example?** ใบอนุญาตชั่วคราวจะลบข้อจำกัดการประเมิน; จำเป็นต้องมีใบอนุญาตถาวรสำหรับการใช้งานจริง.  
- **Which Java version is supported?** รองรับ JDK 8 ขึ้นไป (บทแนะนำนี้ใช้ JDK 11).  
- **Is it possible to handle multiple broken links?** แน่นอน – คุณสามารถเชื่อมต่อหลายตัวจัดการเพื่อจัดการสถานการณ์ต่าง ๆ.

## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะลงลึกในคู่มือขั้นตอนต่อขั้นตอน, ให้แน่ใจว่าคุณมีทุกอย่างที่ต้องการ:
1. Java Development Kit (JDK): ตรวจสอบว่าคุณได้ติดตั้ง JDK บนระบบของคุณแล้ว คุณสามารถดาวน์โหลดได้จาก [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html).
2. Aspose.HTML for Java: คุณต้องติดตั้ง Aspose.HTML for Java คุณสามารถดาวน์โหลดได้จาก [Aspose releases page](https://releases.aspose.com/html/java/).
3. IDE: ใช้สภาพแวดล้อมการพัฒนา Java (IDE) ที่คุณชื่นชอบ เช่น IntelliJ IDEA, Eclipse หรือ NetBeans.
4. Basic Knowledge of Java: ความคุ้นเคยกับการเขียนโปรแกรม Java เป็นสิ่งจำเป็นเพื่อทำตามบทแนะนำนี้ได้อย่างมีประสิทธิภาพ.
5. Temporary License: หากคุณใช้เวอร์ชันทดลองของ Aspose.HTML, พิจารณาได้รับ [temporary license](https://purchase.aspose.com/temporary-license/) เพื่อหลีกเลี่ยงข้อจำกัดใด ๆ ระหว่างการพัฒนา.

## นำเข้าแพ็กเกจ
ก่อนที่เราจะเริ่ม, ให้แน่ใจว่าคุณได้นำเข้าแพ็กเกจที่จำเป็นในโครงการ Java ของคุณ ด้านล่างคือการนำเข้าที่สำคัญที่คุณต้องการ:
```java
import java.io.IOException;
```
การนำเข้าต่าง ๆ นี้จะทำให้คุณเข้าถึงคลาสและเมธอดที่จำเป็นสำหรับการจัดการการทำงานของเครือข่าย, การสร้างเอกสาร HTML, และการทำการแปลง HTML‑to‑PNG.

## ขั้นตอนที่ 1: เตรียมโค้ด HTML
สิ่งแรกที่เราต้องการคือส่วนย่อยของ HTML ง่าย ๆ ที่อ้างอิงไฟล์รูปภาพ เราจะตั้งใจอ้างอิงรูปภาพที่ไม่มีอยู่เพื่อกระตุ้นกลไกการจัดการข้อผิดพลาด.
```java
String code = "<img src='missing.jpg'>";
```
โค้ดนี้สร้างแท็ก `<img>` ที่ชี้ไปที่ `missing.jpg`. เนื่องจากรูปภาพหายไป, บริการเครือข่ายจะคืนรหัสสถานะที่ไม่ใช่ 200, ซึ่งตัวจัดการแบบกำหนดของเราจะจับได้.

## ขั้นตอนที่ 2: เขียนโค้ด HTML ลงไฟล์
ต่อไป, เราต้องบันทึกส่วนย่อยของ HTML เพื่อให้ Aspose.HTML สามารถโหลดเป็นเอกสารได้.
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```
โดยใช้ `FileWriter` เราบันทึก HTML ไปยัง **document.html**. ไฟล์นี้จะเป็นแหล่งสำหรับขั้นตอน **load html document java** ในภายหลัง.

## ขั้นตอนที่ 3: สร้าง Custom Message Handler
ตอนนี้เรามาสร้างตัวจัดการข้อความแบบกำหนดเองที่ตอบสนองเมื่อไม่พบรูปภาพ ตัวจัดการจะตรวจสอบรหัสสถานะ HTTP และพิมพ์ข้อความที่เป็นมิตร.
```java
com.aspose.html.net.MessageHandler handler = new com.aspose.html.net.MessageHandler() {
    @Override
    public void invoke(com.aspose.html.net.INetworkOperationContext context) {
        if (context.getResponse().getStatusCode() != 200) {
            System.out.println(String.format("File '%s' Not Found", context.getRequest().getRequestUri().toString()));
        }
        invoke(context);
    }
};
```
เมธอด `invoke` ตรวจสอบ `context.getResponse().getStatusCode()` หากไม่เป็น **200**, เราจะแสดงคำเตือนที่ชัดเจนว่ามีไฟล์หายไป การเรียก `invoke(context);` สุดท้ายจะส่งการควบคุมไปยังตัวจัดการถัดไปในโซ่.

## ขั้นตอนที่ 4: กำหนดค่า Network Service
เพื่อให้ Aspose.HTML รู้จักตัวจัดการของเรา, เราจดทะเบียนมันกับ network service ผ่านคลาส `Configuration`.
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```
ที่นี่เราสร้างอินสแตนซ์ของ `Configuration`, ดึง `INetworkService`, และเพิ่มตัวจัดการแบบกำหนดของเราเข้าไปในคอลเลกชันของมัน ซึ่งทำให้ตัวจัดการทำงานในทุกคำขอเครือข่าย เช่น การโหลดรูปภาพ.

## ขั้นตอนที่ 5: โหลดเอกสาร HTML
เมื่อการกำหนดค่าเรียบร้อย, เราสามารถโหลดไฟล์ HTML ที่สร้างไว้ก่อนหน้านี้ได้ ขั้นตอนนี้แสดง **load html document java** ขณะรูปภาพที่หายไปกระตุ้นตัวจัดการของเรา.
```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Additional operations will go here
} finally {
    if (document != null) {
        document.dispose();
    }
}
```
คอนสตรัคเตอร์ `HTMLDocument` รับทั้งเส้นทางไฟล์และ `configuration` ที่กำหนดเอง เมื่อเอกสารพาร์สแท็ก `<img>`, network service จะพยายามดึง `missing.jpg`, ได้รับรหัส 404, และตัวจัดการของเราจะแสดงคำเตือน.

## ขั้นตอนที่ 6: แปลง HTML เป็น PNG
เพื่อแสดงความสามารถที่กว้างขวางของ Aspose.HTML, เราจะทำการแปลงเอกสารที่โหลดเป็นภาพ PNG นี่เป็นสถานการณ์คลาสสิกของ **convert html to png**.
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```
`Converter.convertHTML` รับ `HTMLDocument`, `ImageSaveOptions` แบบเลือก (ที่คุณสามารถตั้งค่า DPI, คุณภาพ ฯลฯ), และชื่อไฟล์ผลลัพธ์ ผลลัพธ์คือภาพราสเตอร์ของ HTML ที่เรนเดอร์.

## ขั้นตอนที่ 7: ทำความสะอาดทรัพยากร
การจัดการทรัพยากรอย่างเหมาะสมเป็นสิ่งสำคัญในแอปพลิเคชัน Java ใด ๆ เราทำการปล่อย `Configuration` และ `HTMLDocument` เพื่อหลีกเลี่ยงการรั่วไหลของหน่วยความจำ.
```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```
การห่อการทำความสะอาดในบล็อก `finally` รับประกันว่าจะทำงานแม้ว่าจะเกิดข้อยกเว้นก่อนหน้านั้น.

## ทำไมต้องใช้ Message Handlers?
Message handlers ให้การควบคุมระดับละเอียดต่อการทำงานของเครือข่ายเช่น **handle broken links java** แทนที่จะให้ไลบรารีล้มเหลวโดยไม่มีการแจ้ง, คุณสามารถบันทึก, ลองใหม่, แทนที่ทรัพยากร, หรือให้เนื้อหาสำรอง—ทำให้การประมวลผล HTML ของคุณมีความทนทานและพร้อมสำหรับการผลิต.

## ปัญหาทั่วไปและวิธีแก้
- **Handler recursion** – ตรวจสอบให้แน่ใจว่าคุณเรียก `invoke(context);` เพียงครั้งเดียวเพื่อหลีกเลี่ยงลูปไม่สิ้นสุด.  
- **Missing license** – หากไม่มีใบอนุญาตที่ถูกต้อง, การแปลงอาจสร้างภาพที่มีลายน้ำ.  
- **File path errors** – ใช้เส้นทางแบบเต็มหรือกำหนดไดเรกทอรีทำงานอย่างถูกต้องเมื่อโหลด `document.html`.

## คำถามที่พบบ่อย

**Q:** ฉันสามารถเชื่อมต่อหลายตัวจัดการข้อความได้หรือไม่?  
**A:** ได้, คุณสามารถเพิ่มตัวจัดการหลายตัวลงในคอลเลกชัน `network.getMessageHandlers()`; พวกมันจะทำงานตามลำดับที่เพิ่ม.

**Q:** ตัวจัดการทำงานกับทรัพยากร CSS หรือสคริปต์ด้วยหรือไม่?  
**A:** แน่นอน — คำขอเครือข่ายใด ๆ ที่ทำโดยเอนจิน HTML (รูปภาพ, CSS, JS, ฟอนต์) จะผ่านตัวจัดการนี้.

**Q:** ฉันจะเปลี่ยนคำขอ HTTP ก่อนส่งได้อย่างไร?  
**A:** สร้างตัวจัดการที่แก้ไข `context.getRequest()` ก่อนเรียก `invoke(context)`.

**Q:** มีวิธีปิดการเตือนสำหรับ URL เฉพาะหรือไม่?  
**A:** ภายในตัวจัดการ, ตรวจสอบ `context.getRequest().getRequestUri()` แล้วข้ามการบันทึกตามเงื่อนไขที่กำหนด.

**Q:** เวอร์ชันของ Aspose.HTML ที่ต้องการสำหรับ API เหล่านี้คืออะไร?  
**A:** โค้ดทำงานกับ Aspose.HTML for Java 22.10 ขึ้นไป.

## สรุป
และนี่คือทั้งหมด—คู่มือที่ครอบคลุมเกี่ยวกับ **how to use aspose** message handlers ใน Java เราได้อธิบายการสร้างไฟล์ HTML, การเชื่อมต่อตัวจัดการแบบกำหนดเองกับ **handle broken links java**, การโหลดเอกสาร, และการทำ **convert html to png** ด้วยรูปแบบนี้คุณสามารถจัดการทรัพยากรที่หายไปได้อย่างมั่นใจ, บังคับใช้นโยบายแบบกำหนดเอง, และขยายความสามารถด้านเครือข่ายของ Aspose.HTML ในแอปพลิเคชัน Java ใด ๆ

---

**Last Updated:** 2025-12-10  
**Tested With:** Aspose.HTML for Java 24.11  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}