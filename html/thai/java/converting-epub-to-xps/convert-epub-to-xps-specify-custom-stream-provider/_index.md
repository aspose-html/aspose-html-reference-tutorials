---
date: 2026-03-29
description: เรียนรู้วิธีแปลง EPUB เป็น XPS อย่างง่ายดายด้วย Aspose.HTML สำหรับ Java.
  ปฏิบัติตามคู่มือขั้นตอนต่อขั้นตอนนี้เพื่อกระบวนการแปลงที่ราบรื่น.
linktitle: How to Convert EPUB to XPS with a Custom Stream Provider
second_title: Java HTML Processing with Aspose.HTML
title: วิธีแปลง EPUB เป็น XPS ด้วยผู้ให้บริการสตรีมแบบกำหนดเอง
url: /th/java/converting-epub-to-xps/convert-epub-to-xps-specify-custom-stream-provider/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแปลง EPUB เป็น XPS ด้วยผู้ให้บริการสตรีมแบบกำหนดเอง

ในโลกการเผยแพร่ดิจิทัลในวันนี้ **วิธีแปลง EPUB เป็น XPS** เป็นความต้องการที่พบบ่อย—ไม่ว่าจะต้องการการแสดงผลแบบ fixed‑layout สำหรับการพิมพ์, การเก็บถาวร, หรือการแชร์ระหว่างอุปกรณ์ Windows. Aspose.HTML for Java ทำให้การแปลงนี้ง่ายดาย, และโดยการใช้ผู้ให้บริการสตรีมแบบกำหนดเองในหน่วยความจำ คุณจะทำกระบวนการทั้งหมดอยู่ใน RAM ซึ่งเหมาะอย่างยิ่งสำหรับสภาพแวดล้อมคลาวด์หรือการทำงานที่ต้องการประสิทธิภาพสูง. ด้านล่างนี้คุณจะพบทุกอย่างที่ต้องการเพื่อเริ่มต้น, ตั้งแต่ข้อกำหนดเบื้องต้นจนถึงตัวอย่างที่พร้อมรันเต็มรูปแบบ.

## คำตอบสั้น
- **การแปลงให้ผลลัพธ์อะไร?** เอกสาร XPS ที่คงรูปแบบและฟอนต์ไว้.  
- **ฉันต้องการไลเซนส์หรือไม่?** เวอร์ชันทดลองฟรีใช้ได้สำหรับการทดสอบ; ต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานจริง.  
- **ฉันสามารถรันนี้ในคอนเทนเนอร์ได้หรือไม่?** ได้—ไม่จำเป็นต้องเขียนไฟล์ลงระบบถ้าคุณเก็บทุกอย่างในหน่วยความจำ.  
- **เวอร์ชัน Java ที่รองรับคืออะไร?** Java 8 หรือสูงกว่า.  
- **ผู้ให้บริการสตรีมแบบกำหนดเองจำเป็นหรือไม่?** ไม่จำเป็น, แต่ช่วยให้คุณควบคุมการใช้หน่วยความจำและการจัดการผลลัพธ์ได้เต็มที่.

## วิธีแปลง EPUB เป็น XPS
ก่อนจะลงลึกในโค้ด, มาทำความเข้าใจก่อนว่าการแปลงทำอะไรและทำไมคุณอาจต้องการเก็บทุกอย่างในหน่วยความจำ.

### “แปลง EPUB เป็น XPS” คืออะไร?
การแปลงไฟล์ EPUB เป็น XPS จะเปลี่ยนรูปแบบ e‑book ที่สามารถรีฟลว์ได้ให้เป็นเอกสารแบบ fixed‑layout, ไม่ขึ้นกับอุปกรณ์. XPS (XML Paper Specification) เป็นมาตรฐานของ Microsoft ที่เทียบเคียงกับ PDF, เหมาะสำหรับสถานการณ์ที่ต้องการการแสดงผลที่คงที่และไม่เปลี่ยนแปลงระหว่างแพลตฟอร์ม.

### ทำไมต้องใช้ผู้ให้บริการสตรีมแบบกำหนดเอง?
`MemoryStreamProvider` ที่กำหนดเองทำให้คุณเก็บผลลัพธ์การแปลงไว้ใน RAM แทนการเขียนไฟล์ชั่วคราวลงดิสก์. วิธีนี้:
- ลดภาระ I/O.  
- ปรับปรุงประสิทธิภาพในสถาปัตยกรรม server‑less หรือ micro‑service.  
- ให้ความยืดหยุ่นในการสตรีมผลลัพธ์โดยตรงไปยังไคลเอนต์, ที่เก็บข้อมูลคลาวด์, หรือ API อื่น.

## ข้อกำหนดเบื้องต้น

เพื่อให้ **แปลง EPUB เป็น XPS** สำเร็จ, โปรดตรวจสอบว่าคุณมีข้อกำหนดต่อไปนี้พร้อมใช้งาน:

### 1. ไลบรารี Aspose.HTML for Java  

คุณต้องติดตั้งและกำหนดค่าไลบรารี Aspose.HTML for Java ในสภาพแวดล้อม Java ของคุณ. หากยังไม่ได้ทำ, คุณสามารถดาวน์โหลดไลบรารีได้จาก [ลิงก์ดาวน์โหลด](https://releases.aspose.com/html/java/).

### 2. ไฟล์ EPUB อินพุต  

คุณต้องมีไฟล์ EPUB ที่ต้องการแปลงเป็น XPS พร้อมใช้งาน. ตรวจสอบให้แน่ใจว่าไฟล์นี้พร้อมสำหรับกระบวนการแปลง.

เมื่อคุณเตรียมข้อกำหนดทั้งหมดแล้ว, เราจะเดินผ่านขั้นตอนการแปลงทีละขั้นตอน.

## นำเข้าชุดแพ็กเกจ

ก่อนเริ่ม, อย่าลืมนำเข้าชุดแพ็กเกจที่จำเป็นสำหรับ Aspose.HTML for Java เพื่อใช้ฟังก์ชันต่าง ๆ.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.XpsSaveOptions;
import com.aspose.html.saving.MemoryStreamProvider;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
```

## เปิดไฟล์ EPUB

ขั้นแรก, คุณต้องเปิดไฟล์ EPUB ที่มีอยู่เพื่ออ่าน. ในขั้นตอนนี้เราจะใช้ `FileInputStream` เพื่อเข้าถึงไฟล์ EPUB.

```java
try (FileInputStream fileInputStream = new FileInputStream("path/to/your/input.epub")) {
    // Your code for Step 1
}
```

## สร้าง MemoryStreamProvider

ต่อไป, สร้างอินสแตนซ์ของ `MemoryStreamProvider`. วัตถุนี้จะเก็บผลลัพธ์การแปลงไว้ในหน่วยความจำ.

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
    // Your code for Step 2
}
```

## แปลง EPUB เป็น XPS

ตอนนี้ให้แปลงไฟล์ EPUB เป็น XPS ด้วยเมธอด `Converter.convertEPUB`. `MemoryStreamProvider` จะเป็นสตรีมปลายทาง.

```java
Converter.convertEPUB(
    fileInputStream,
    new XpsSaveOptions(),
    streamProvider.getStream().findFirst().get()
);
```

## รับข้อมูลผลลัพธ์

หลังจากการแปลงเสร็จสิ้น, ดึงสตรีมหน่วยความจำที่บรรจุข้อมูล XPS ออกมา.

```java
InputStream inputStream = streamProvider.getStream().findFirst().get();
```

## บันทึกผลลัพธ์ (ไม่บังคับ)

หากคุณต้องการไฟล์จริง—อาจเพื่อการดีบักหรือการตรวจสอบแบบออฟไลน์—ให้เขียนสตรีมหน่วยความจำลงดิสก์. ในหลายกรณีการผลิตคุณสามารถข้ามขั้นตอนนี้และสตรีมข้อมูลโดยตรงไปยังไคลเอนต์ได้.

```java
try (FileOutputStream fileOutputStream = new FileOutputStream("path/to/your/output.xps")) {
    byte[] buffer = new byte[inputStream.available()];
    inputStream.read(buffer);
    fileOutputStream.write(buffer);
}
```

## โค้ดต้นฉบับเต็ม

ด้านล่างเป็นตัวอย่างเต็มที่พร้อมรัน, รวมทุกส่วนเข้าด้วยกัน. คุณสามารถคัดลอก, วาง, และปรับใช้ในโปรเจกต์ของคุณได้ตามต้องการ.

```java
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of MemoryStreamProvider
            try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
                // Convert EPUB to XPS by using the MemoryStreamProvider
                com.aspose.html.converters.Converter.convertEPUB(
                        fileInputStream,
                        new com.aspose.html.saving.XpsSaveOptions(),
                        streamProvider.lStream
                );
                // Get access to the memory stream that contains the resulted data
                java.io.InputStream inputStream = streamProvider.lStream.stream().findFirst().get();
                // Flush the result data to the output file
                try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("output.xps"))) {
                    byte[] buffer = new byte[inputStream.available()];
                    inputStream.read(buffer);
                    fileOutputStream.write(buffer);
                }
            }
        }
```

## ปัญหาทั่วไปและวิธีแก้

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|----------|
| **`java.lang.OutOfMemoryError`** | ไฟล์ EPUB ขนาดใหญ่เกินขนาด heap เริ่มต้นเมื่อเก็บทั้งหมดในหน่วยความจำ. | เพิ่มขนาด heap ของ JVM (`-Xmx`) หรือประมวลผล EPUB เป็นชิ้นส่วนถ้าเป็นไปได้. |
| **Missing fonts in XPS** | ฟอนต์ที่ไม่ได้ฝังใน EPUB ไม่พร้อมใช้งานบนเครื่องแปลง. | ตรวจสอบให้ฟอนต์ที่จำเป็นติดตั้งบนเซิร์ฟเวอร์หรือฝังฟอนต์ใน EPUB. |
| **`UnsupportedOperationException` from `MemoryStreamProvider`** | ใช้ Aspose.HTML เวอร์ชันเก่า. | อัปเดตเป็นรุ่นล่าสุดของ Aspose.HTML for Java. |

## คำถามที่พบบ่อย

### 1. EPUB คืออะไร?
EPUB, ย่อมาจาก Electronic Publication, เป็นรูปแบบไฟล์ที่ใช้กันอย่างแพร่หลายสำหรับ eBooks. มันออกแบบให้อ่านได้ง่ายบนอุปกรณ์หลากหลาย, เช่น eReader, แท็บเล็ต, และสมาร์ทโฟน.

### 2. XPS คืออะไร?
XPS ย่อมาจาก XML Paper Specification, เป็นรูปแบบเอกสารที่สร้างโดย Microsoft. ใช้สำหรับการแชร์และเก็บเอกสารโดยคงลักษณะการแสดงผลและเลย์เอาต์เดียวกัน.

### 3. ทำไมต้องใช้ Aspose.HTML for Java?
Aspose.HTML for Java เป็นไลบรารีที่ทรงพลัง ช่วยให้งานจัดการเอกสาร, การแปลง, และการเรนเดอร์เป็นเรื่องง่าย. มันให้ฟีเจอร์และการสนับสนุนหลากหลายรูปแบบเอกสาร, ทำให้เป็นเครื่องมือที่มีคุณค่าสำหรับนักพัฒนา.

### 4. ฉันสามารถแปลงรูปแบบเอกสารอื่นด้วย Aspose.HTML for Java ได้หรือไม่?
ได้, Aspose.HTML for Java รองรับการแปลงรูปแบบเอกสารหลายประเภท, รวมถึง HTML, EPUB, XPS, และอื่น ๆ. เป็นเครื่องมือที่หลากหลายสำหรับการจัดการเอกสาร.

### 5. ฉันจะหาแหล่งข้อมูลและการสนับสนุนเพิ่มเติมได้จากที่ไหน?
สำหรับเอกสารและการสนับสนุน, เยี่ยมชม [เอกสาร Aspose.HTML for Java](https://reference.aspose.com/html/java/) และ [ฟอรั่มสนับสนุน](https://forum.aspose.com/).

---

**อัปเดตล่าสุด:** 2026-03-29  
**ทดสอบกับ:** Aspose.HTML for Java 24.12 (latest at time of writing)  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}