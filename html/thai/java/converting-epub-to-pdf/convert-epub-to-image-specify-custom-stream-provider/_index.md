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

## Quick Answers
- **บทเรียนนี้สอนอะไร?** วิธีดึงรูปภาพจาก EPUB และบันทึกเป็นไฟล์ JPEG โดยใช้ custom stream provider.  
- **ต้องใช้ไลบรารีอะไร?** Aspose.HTML for Java.  
- **ต้องการไลเซนส์หรือไม่?** จำเป็นต้องมีไลเซนส์ชั่วคราวหรือเต็มสำหรับการใช้งานในสภาพแวดล้อมการผลิต.  
- **รูปแบบเอาต์พุตที่แสดงคืออะไร?** JPEG (คุณสามารถเปลี่ยนเป็น PNG, BMP ฯลฯ โดยการเปลี่ยน `ImageFormat`).  
- **จำนวนบรรทัดของโค้ด?** มีเพียงห้าบล็อกโค้ดสั้น ๆ – ส่วนอื่นทั้งหมดเป็นคำแนะนำเป็นภาษาอังกฤษธรรมดา.

## How to extract images from EPUB using a custom stream provider?
ก่อนจะลงลึกในโค้ด เรามาเข้าใจว่าทำไม **custom stream provider** จึงมีประโยชน์ การส่งออกการแปลงไปยัง memory stream แทนการใช้ระบบไฟล์จะทำให้คุณควบคุมได้เต็มที่ว่าข้อมูลภาพจะถูกจัดเก็บที่ไหนและอย่างไร – เหมาะอย่างยิ่งสำหรับเว็บเซอร์วิส, ฟังก์ชันคลาวด์, หรือสถานการณ์ใด ๆ ที่ต้องการหลีกเลี่ยงไฟล์ชั่วคราว.

## Prerequisites

1. **Java Development Environment** – ตรวจสอบให้แน่ใจว่า Java ได้รับการติดตั้งอย่างถูกต้องบนระบบของคุณ คุณสามารถดาวน์โหลด Java จากเว็บไซต์ได้.  
2. **Aspose.HTML for Java Library** – คุณต้องรับ Aspose.HTML for Java library คุณสามารถหาได้จาก [here](https://releases.aspose.com/html/java/).  
3. **Aspose.HTML Documentation** – เอกสารสำหรับ Aspose.HTML for Java สามารถหาได้จาก [here](https://reference.aspose.com/html/java/).  
4. **IDE (Integrated Development Environment)** – คุณสามารถเลือก IDE ที่รองรับ Java ใดก็ได้ เช่น Eclipse หรือ IntelliJ IDEA.

## Import Packages
ในส่วนนี้ เราจะชี้แนะขั้นตอนการนำเข้าแพ็กเกจที่จำเป็นเพื่อเริ่มต้นใช้งาน Aspose.HTML for Java.

## Open an Existing EPUB File
ก่อนอื่น คุณต้องเปิดไฟล์ EPUB ที่มีอยู่เพื่ออ่าน นี่คือตัวอย่างวิธีทำ:

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code here
}
```

## Create a MemoryStreamProvider
เพื่อแปลง EPUB เป็นภาพ คุณต้องสร้างอินสแตนซ์ของ `MemoryStreamProvider`:

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
    // Your code here
}
```

## Convert EPUB to Image
ต่อไป เราจะทำการแปลงไฟล์ EPUB เป็นภาพโดยใช้ `MemoryStreamProvider` ขั้นตอนนี้ **แปลง EPUB เป็น JPEG** (คุณสามารถเปลี่ยนรูปแบบเป็น PNG หรือ BMP ได้หากต้องการ).

```java
com.aspose.html.converters.Converter.convertEPUB(
        fileInputStream,
        new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Jpeg),
        streamProvider.lStream
);
```

## Access Memory Streams
คุณสามารถเข้าถึง memory stream ที่บรรจุข้อมูลภาพที่ได้ดังนี้:

```java
int size = streamProvider.lStream.size();
for (int i = 0; i < size; i++) {
    java.io.InputStream inputStream = streamProvider.lStream.get(i);
    // Your code here
}
```

## Flush the Page to Output File
สุดท้าย คุณต้องเขียนแต่ละ image stream ไปยังไฟล์จริง ตัวอย่างนี้บันทึกแต่ละหน้าเป็นไฟล์ JPEG แยกกัน:

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("page_{" + (i + 1) + "}.jpg"))) {
    byte[] buffer = new byte[inputStream.available()];
    inputStream.read(buffer);
    fileOutputStream.write(buffer);
}
```

## Why convert EPUB to JPEG?

- **ความเข้ากันได้ทั่วโลก** – ภาพ JPEG สามารถแสดงบนอุปกรณ์หรือแพลตฟอร์มเกือบทุกประเภท.  
- **การบูรณาการที่ง่าย** – ใช้ภาพที่ดึงออกมาในเว็บเพจ, แอปมือถือ, หรือเอกสารโดยไม่ต้องใช้ EPUB reader.  
- **ประสิทธิภาพ** – การแสดงผลภาพคงที่เร็วกว่าโหลด EPUB ทั้งไฟล์ ซึ่งเหมาะสำหรับภาพย่อหรือพรีวิว.

## Common Pitfalls & Tips

- **การจัดการหน่วยความจำ** – ปิด stream เสมอ (`try‑with‑resources` ถูกใช้ข้างต้น) เพื่อหลีกเลี่ยงการรั่วไหลของหน่วยความจำ.  
- **EPUB ขนาดใหญ่** – สำหรับหนังสือที่มีหลายหน้า พิจารณาประมวลผล stream เป็นชุดเพื่อรักษาการใช้หน่วยความจำให้ต่ำ.  
- **คุณภาพภาพ** – ปรับ `ImageSaveOptions` (เช่น property `Quality`) หากต้องการเอาต์พุตความละเอียดสูงขึ้น.

## Conclusion
ขอแสดงความยินดี! คุณได้เรียนรู้วิธี **ดึงรูปภาพจาก EPUB** ด้วย Aspose.HTML for Java และ custom stream provider อย่างสำเร็จ วิธีการที่ทรงพลังนี้ให้ความยืดหยุ่นในการจัดการข้อมูลภาพตรงตามที่คุณต้องการ ไม่ว่าจะเป็นการบันทึกลงดิสก์, ส่งผ่านเครือข่าย, หรือเก็บในฐานข้อมูล.

## FAQs

### 1. What is Aspose.HTML for Java?
Aspose.HTML for Java คือไลบรารีที่ช่วยให้นักพัฒนา Java ทำงานกับ HTML, EPUB และรูปแบบเว็บอื่น ๆ

### 2. Where can I find the documentation for Aspose.HTML for Java?
คุณสามารถหาเอกสารได้จาก [here](https://reference.aspose.com/html/java/).

### 3. Is there a free trial available?
ใช่ คุณสามารถรับการทดลองใช้ฟรีของ Aspose.HTML for Java [here](https://releases.aspose.com/).

### 4. How can I get a temporary license for Aspose.HTML for Java?
คุณสามารถรับไลเซนส์ชั่วคราวได้จาก [here](https://purchase.aspose.com/temporary-license/).

### 5. Where can I get support for Aspose.HTML for Java?
คุณสามารถหาการสนับสนุนได้ที่ [Aspose forums](https://forum.aspose.com/).

## Additional Frequently Asked Questions

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