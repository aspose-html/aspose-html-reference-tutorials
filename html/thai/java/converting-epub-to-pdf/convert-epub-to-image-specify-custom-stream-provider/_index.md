---
date: 2026-01-02
description: เรียนรู้วิธีดึงรูปภาพจาก EPUB ด้วย Aspose.HTML สำหรับ Java และแปลง EPUB
  เป็นไฟล์รูปภาพด้วยคู่มือขั้นตอนนี้
linktitle: Specifying Custom Stream Provider for EPUB to Image Conversion
second_title: Java HTML Processing with Aspose.HTML
title: ดึงรูปภาพจาก EPUB – การระบุผู้ให้บริการสตรีมแบบกำหนดเอง
url: /th/java/converting-epub-to-pdf/convert-epub-to-image-specify-custom-stream-provider/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงรูปภาพจาก EPUB – กำหนด Custom Stream Provider สำหรับการแปลง EPUB เป็นรูปภาพ

## คำตอบด่วน
- **บทเรียนนี้สอนอะไร?** วิธีดึงรูปภาพจาก EPUB และบันทึกเป็นไฟล์ JPEG สำหรับผู้ให้บริการสตรีมแบบกำหนดเอง
- **ต้องใช้ไลบรารีอะไร?** Aspose.HTML for Java
- **ต้องการไลเซนส์หรือไม่?** ต้องการไลเซนส์ชั่วคราวหรือเต็มรูปแบบสำหรับการผลิต
- ** รูปแบบนี้เพิ่มมากขึ้นคืออะไร?** JPEG ( คุณสามารถใช้ PNG, BMP และอื่นๆ โดยอาศัย `ImageFormat`)
- **จำนวนบรรทัดของโค้ด?**มีเพียงห้าบล็อกโค้ดสั้น – ส่วนอื่นๆ ทั้งหมดเป็นคำแนะนำเป็นภาษาอังกฤษธรรมดาๆ.

## จะดึงภาพจาก EPUB โดยใช้ผู้ให้บริการสตรีมแบบกำหนดเองได้อย่างไร
เหตุการณ์ลงลึกในโค้ดมักจะเข้าใจว่าทำไม **ผู้ให้บริการสตรีมแบบกำหนดเอง** เอกสารที่มีความสำคัญต่อเซิร์ฟเวอร์, ฟังก์ชั่นเซิร์ฟเวอร์, หรือสถานการณ์ใดๆ ที่ต้องการจะควบคุมไฟล์ชั่วคราว

## ข้อกำหนดเบื้องต้น

1. **Java Development Environment** – การควบคุม Java สามารถดูได้จากการดาวน์โหลดบนระบบของคุณ ดาวน์โหลด Java จากเว็บไซต์ได้
2. **Aspose.HTML for Java Library** – เอกสารรับ Aspose.HTML for Java Library คุณไม่จำเป็นต้องทำอะไรเลย [ที่นี่](https://releases.aspose.com/html/java/)
3. **Aspose.HTML Documentation** – เอกสารสำหรับ Aspose.HTML for Java สามารถหาได้จาก [ที่นี่](https://reference.aspose.com/html/java/)
4. **IDE (Integrated Development Environment)** – ไฟล์ IDE รองรับ Java เวลส์ เช่น Eclipse หรือ IntelliJ IDEA

## แพคเกจนำเข้า
นี่คือคำแนะนำเบื้องต้นในการนำเข้าระบบปฏิบัติการเพื่อเริ่มต้นการใช้งาน Aspose.HTML สำหรับ Java

## เปิดไฟล์ EPUB ที่มีอยู่
ก่อนอื่น คุณต้องเปิดไฟล์ EPUB ที่มีอยู่เพื่ออ่าน นี่คือตัวอย่างวิธีทำ:

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code here
}
```

## สร้าง MemoryStreamProvider
เพื่อแปลง EPUB เป็นภาพ คุณต้องสร้างอินสแตนซ์ของ `MemoryStreamProvider`:

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
    // Your code here
}
```

## แปลง EPUB เป็นรูปภาพ
ต่อไป เราจะทำการแปลงไฟล์ EPUB เป็นภาพโดยใช้ `MemoryStreamProvider` ขั้นตอนนี้ **แปลง EPUB เป็น JPEG** (คุณสามารถเปลี่ยนรูปแบบเป็น PNG หรือ BMP ได้หากต้องการ).

```java
com.aspose.html.converters.Converter.convertEPUB(
        fileInputStream,
        new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Jpeg),
        streamProvider.lStream
);
```

## เข้าถึง Memory Streams
คุณสามารถเข้าถึง memory stream ที่บรรจุข้อมูลภาพที่ได้ดังนี้:

```java
int size = streamProvider.lStream.size();
for (int i = 0; i < size; i++) {
    java.io.InputStream inputStream = streamProvider.lStream.get(i);
    // Your code here
}
```

## บันทึกหน้าลงในไฟล์เอาต์พุต
สุดท้าย คุณต้องเขียนแต่ละ image stream ไปยังไฟล์จริง ตัวอย่างนี้บันทึกแต่ละหน้าเป็นไฟล์ JPEG แยกกัน:

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("page_{" + (i + 1) + "}.jpg"))) {
    byte[] buffer = new byte[inputStream.available()];
    inputStream.read(buffer);
    fileOutputStream.write(buffer);
}
```

## ทำไมต้องแปลง EPUB เป็น JPEG

- ** บันทึกทั่วโลก** – ภาพ JPEG แสดงหรือแพลตฟอร์มที่รองรับประเภทต่างๆ
- **การวิธีการที่ง่าย** – ใช้สำหรับการดึงออกมาในเว็บเพจ, คุณสามารถใช้มือถือ, หรือเอกสารโดยไม่ต้องใช้โปรแกรมอ่าน EPUB
- **นักแสดง** – ตรวจสอบภาพในช่วงเวลาที่โหลด EPUB ทั้งไฟล์ที่เหมาะสำหรับภาพขนาดย่อหรือพรีวิว

## ข้อผิดพลาดและเคล็ดลับทั่วไป

- **การจัดการคำอธิบาย** – ปิดสตรีมเสมอ (`try‑with‑resources` บันทึกการควบคุม) ในการควบคุมของคืนนี้
- **EPUB ขนาดใหญ่** – สำหรับหนังสือที่มีหลายหน้าพิจารณาว่าสตรีมเป็นชุดที่ต้องใช้เหตุผลให้ต่ำ
- **คุณภาพภาพ** – โบสถ์ `ImageSaveOptions` (เช่นคุณสมบัติ `คุณภาพ`) อีกครั้งหนึ่งที่ความละเอียดสูงขึ้น

## บทสรุป
บทความ! พบกับ **ดึงรูปภาพจาก EPUB** ด้วย Aspose.HTML สำหรับ Java และผู้ให้บริการสตรีมแบบกำหนดเองเช่นความสำเร็จวิธีที่นี้ให้คุณสมบัติของภาพข้อมูลโดยตรงที่ต้องใช้ลงไปในนั้น, ส่งผ่านเครือข่าย, หรือเก็บในทางเทคนิค

## คำถามที่พบบ่อยเพิ่มเติม

**Q: ฉันจะแปลง EPUB เป็น PNG แทน JPEG อย่างไร?**  
A: เปลี่ยน `ImageFormat` ใน `ImageSaveOptions` เป็น `ImageFormat.Png` และปรับนามสกุลไฟล์ให้สอดคล้อง.

**Q: ฉันสามารถดึงเฉพาะหน้าที่ต้องการจาก EPUB ได้หรือไม่?**  
A: ได้ โดยการวนลูปผ่านคอลเลกชัน `lStream` และเลือกดัชนีที่ต้องการก่อนบันทึกเป็นไฟล์.

**Q: สามารถทำการแปลงนี้ในฟังก์ชันคลาวด์โดยไม่เขียนลงดิสก์ได้หรือไม่?**  
A: แน่นอน เนื่องจากผลลัพธ์การแปลงถูกเก็บใน memory stream คุณสามารถส่งคืน byte array จากฟังก์ชันคลาวด์โดยตรง.

**Q: Aspose.HTML รองรับไฟล์ EPUB ที่มี DRM หรือไม่?**  
A: ไลบรารีสามารถเปิด EPUB ที่ไม่ได้เข้ารหัสได้ สำหรับไฟล์ที่มี DRM คุณต้องลบการป้องกันก่อนทำการแปลง.

**Q: ต้องใช้เวอร์ชันของ Aspose.HTML ใดสำหรับฟีเจอร์นี้?**  
A: คลาส `MemoryStreamProvider` มีให้ใช้ตั้งแต่ Aspose.HTML 22.9 ขึ้นไป.

---

**อัปเดตล่าสุด:** 2026-01-02  
**ทดสอบด้วย:** Aspose.HTML for Java 23.10  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}