---
title: แปลง EPUB เป็นรูปภาพด้วย Aspose.HTML สำหรับ Java
linktitle: การระบุผู้ให้บริการสตรีมแบบกำหนดเองสำหรับการแปลง EPUB เป็นรูปภาพ
second_title: การประมวลผล Java HTML ด้วย Aspose.HTML
description: เรียนรู้วิธีการแปลง EPUB เป็นรูปภาพด้วย Aspose.HTML สำหรับ Java คำแนะนำทีละขั้นตอนสำหรับการแปลงที่ราบรื่น
type: docs
weight: 15
url: /th/java/converting-between-epub-and-image-formats/convert-epub-to-image-specify-custom-stream-provider/
---
หากคุณต้องการแปลงไฟล์ EPUB เป็นไฟล์ภาพใน Java Aspose.HTML สำหรับ Java เป็นเครื่องมือที่มีประสิทธิภาพที่จะช่วยให้กระบวนการนี้ราบรื่นยิ่งขึ้น ในคู่มือทีละขั้นตอนนี้ เราจะแนะนำคุณตลอดกระบวนการทั้งหมด ตั้งแต่การติดตั้งไปจนถึงการแปลงไฟล์ EPUB เป็นไฟล์ภาพ นอกจากนี้ เรายังจะแจ้งข้อกำหนดเบื้องต้นและแนะนำแพ็คเกจที่จำเป็นให้คุณทราบด้วย

## ข้อกำหนดเบื้องต้น

ก่อนที่คุณจะเริ่มการแปลง โปรดตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

- Java Development Kit (JDK): คุณควรติดตั้ง Java SE Development Kit (JDK) ไว้ในระบบของคุณ คุณสามารถดาวน์โหลดได้จาก[ที่นี่](https://www.oracle.com/java/technologies/javase-downloads.html).

-  Aspose.HTML สำหรับ Java: คุณต้องมีไลบรารี Aspose.HTML สำหรับ Java หากคุณยังไม่มี คุณสามารถรับได้[ที่นี่](https://releases.aspose.com/html/java/).

- ไฟล์ EPUB: เตรียมไฟล์ EPUB ที่คุณต้องการแปลงเป็นรูปภาพ

## แพ็คเกจนำเข้า

ในโปรเจ็กต์ Java ของคุณ คุณจะต้องนำเข้าแพ็คเกจที่จำเป็นจาก Aspose.HTML สำหรับ Java อย่าลืมรวมแพ็คเกจเหล่านี้ไว้ในโค้ดของคุณ

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.ImageSaveOptions;
import com.aspose.html.rendering.image.ImageFormat;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
```

## คำแนะนำทีละขั้นตอน

เรามาแบ่งขั้นตอนการแปลงไฟล์ EPUB เป็นรูปภาพโดยใช้ Aspose.HTML สำหรับ Java ออกเป็นหลายขั้นตอนกัน:

### ขั้นตอนที่ 1: เปิดไฟล์ EPUB

 คุณจะเริ่มต้นด้วยการเปิดไฟล์ EPUB ที่มีอยู่เพื่ออ่านโดยใช้`FileInputStream`.

```java
try (FileInputStream fileInputStream = new FileInputStream("input.epub")) {
```

### ขั้นตอนที่ 2: สร้างผู้ให้บริการสตรีมหน่วยความจำ

 ถัดไป ให้สร้างอินสแตนซ์ของ`MemoryStreamProvider` เพื่ออำนวยความสะดวกในการแปลง

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
```

### ขั้นตอนที่ 3: แปลง EPUB เป็นรูปภาพ

 ตอนนี้ถึงเวลาที่จะดำเนินการแปลงไฟล์ EPUB เป็นรูปภาพจริงแล้ว ใช้`Converter.convertEPUB` วิธีการนี้เพื่อจุดประสงค์นี้ โดยระบุรูปแบบเอาต์พุตเป็น JPEG

```java
Converter.convertEPUB(
    fileInputStream,
    new ImageSaveOptions(ImageFormat.Jpeg),
    streamProvider.getStream()
);
```

### ขั้นตอนที่ 4: เข้าถึงข้อมูลผลลัพธ์

หลังจากการแปลง คุณสามารถเข้าถึงสตรีมหน่วยความจำที่มีข้อมูลภาพผลลัพธ์ได้ วนซ้ำผ่านสตรีมเหล่านี้เพื่อประมวลผลภาพ

```java
int size = streamProvider.getStream().size();
for (int i = 0; i < size; i++) {
    InputStream inputStream = streamProvider.getStream().get(i);

    // ล้างเพจไปยังไฟล์เอาท์พุต
    try (FileOutputStream fileOutputStream = new FileOutputStream("page_" + (i + 1) + ".jpg")) {
        byte[] buffer = new byte[inputStream.available()];
        inputStream.read(buffer);
        fileOutputStream.write(buffer);
    }
}
```

เพียงเท่านี้ก็เรียบร้อยแล้ว! คุณได้แปลงไฟล์ EPUB เป็นรูปภาพโดยใช้ Aspose.HTML สำหรับ Java สำเร็จแล้ว

## บทสรุป

Aspose.HTML สำหรับ Java ช่วยให้กระบวนการแปลงไฟล์ EPUB เป็นรูปภาพง่ายขึ้น ด้วยขั้นตอนต่างๆ ที่ระบุไว้ในคู่มือนี้ คุณสามารถดำเนินการนี้ได้อย่างรวดเร็วและมีประสิทธิภาพ โปรดจำไว้ว่าต้องปฏิบัติตามข้อกำหนดเบื้องต้นและนำเข้าแพ็คเกจที่จำเป็นเพื่อให้แน่ใจว่ากระบวนการแปลงจะราบรื่น

## คำถามที่พบบ่อย

### คำถามที่ 1: ฉันสามารถใช้ Aspose.HTML สำหรับ Java ได้ฟรีหรือไม่?

 A1: Aspose.HTML สำหรับ Java เป็นไลบรารีเชิงพาณิชย์ แต่คุณสามารถสำรวจคุณลักษณะของมันได้ด้วย[ทดลองใช้งานฟรี](https://releases.aspose.com/html/java).

### คำถามที่ 2: มีเอกสารใด ๆ สำหรับ Aspose.HTML สำหรับ Java หรือไม่

 A2: ใช่ คุณสามารถค้นหาเอกสารประกอบที่ครอบคลุมได้[ที่นี่](https://reference.aspose.com/html/java/).

### คำถามที่ 3: ฉันจะรับใบอนุญาตชั่วคราวสำหรับ Aspose.HTML สำหรับ Java ได้อย่างไร

 A3: คุณสามารถรับใบอนุญาตชั่วคราวได้[ที่นี่](https://purchase.aspose.com/temporary-license/).

### คำถามที่ 4: ฉันจะได้รับการสนับสนุนสำหรับ Aspose.HTML สำหรับ Java ได้จากที่ไหน

 A4: สำหรับการสนับสนุนและการสนทนาของชุมชน โปรดไปที่[ฟอรั่ม Aspose](https://forum.aspose.com/).

### คำถามที่ 5: ฉันสามารถแปลงไฟล์ EPUB เป็นรูปแบบรูปภาพอื่นได้หรือไม่

 A5: ใช่ คุณสามารถปรับแต่งรูปแบบผลลัพธ์ได้โดยการปรับ`ImageSaveOptions` . เปลี่ยนแปลง`ImageFormat` เป็นรูปแบบที่คุณต้องการ เช่น PNG หรือ GIF