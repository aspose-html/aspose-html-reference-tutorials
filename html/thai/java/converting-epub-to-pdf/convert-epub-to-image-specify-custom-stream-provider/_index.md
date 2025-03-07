---
title: การระบุผู้ให้บริการสตรีมแบบกำหนดเองสำหรับการแปลง EPUB เป็นรูปภาพ
linktitle: การระบุผู้ให้บริการสตรีมแบบกำหนดเองสำหรับการแปลง EPUB เป็นรูปภาพ
second_title: การประมวลผล Java HTML ด้วย Aspose.HTML
description: เรียนรู้วิธีใช้ Aspose.HTML สำหรับ Java เพื่อแปลงไฟล์ EPUB เป็นรูปภาพด้วยคู่มือทีละขั้นตอนนี้
weight: 15
url: /th/java/converting-epub-to-pdf/convert-epub-to-image-specify-custom-stream-provider/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การระบุผู้ให้บริการสตรีมแบบกำหนดเองสำหรับการแปลง EPUB เป็นรูปภาพ


คุณพร้อมที่จะใช้ประโยชน์จากพลังของ Aspose.HTML สำหรับ Java แล้วหรือยัง? คู่มือฉบับสมบูรณ์นี้จะแนะนำคุณทีละขั้นตอน ไม่ว่าคุณจะเป็นนักพัฒนาที่มีประสบการณ์หรือเพิ่งเริ่มต้น เราก็ช่วยคุณได้ 

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเจาะลึกการใช้ Aspose.HTML สำหรับ Java มีบางสิ่งบางอย่างที่คุณต้องมี:

1. สภาพแวดล้อมการพัฒนา Java: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Java อย่างถูกต้องบนระบบของคุณ คุณสามารถดาวน์โหลด Java ได้จากเว็บไซต์

2.  Aspose.HTML สำหรับไลบรารี Java: คุณจะต้องได้รับไลบรารี Aspose.HTML สำหรับ Java คุณสามารถค้นหาได้[ที่นี่](https://releases.aspose.com/html/java/).

3.  เอกสารประกอบ Aspose.HTML: สามารถพบเอกสารประกอบสำหรับ Aspose.HTML สำหรับ Java ได้[ที่นี่](https://reference.aspose.com/html/java/).

4. IDE (Integrated Development Environment): คุณสามารถเลือก IDE ที่เข้ากันได้กับ Java เช่น Eclipse หรือ IntelliJ IDEA

## แพ็คเกจนำเข้า

ในส่วนนี้ เราจะแนะนำคุณเกี่ยวกับขั้นตอนการนำเข้าแพ็คเกจที่จำเป็นเพื่อเริ่มต้นใช้งาน Aspose.HTML สำหรับ Java

## เปิดไฟล์ EPUB ที่มีอยู่

ขั้นแรก คุณต้องเปิดไฟล์ EPUB ที่มีอยู่เพื่ออ่าน โดยคุณสามารถทำได้ดังนี้:

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // รหัสของคุณที่นี่
}
```

## สร้าง MemoryStreamProvider

หากต้องการแปลง EPUB เป็นรูปภาพ คุณจะต้องสร้างอินสแตนซ์ของ MemoryStreamProvider:

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
    // รหัสของคุณที่นี่
}
```

## แปลง EPUB เป็นรูปภาพ

ตอนนี้เรามาแปลงไฟล์ EPUB เป็นรูปภาพโดยใช้ MemoryStreamProvider กัน:

```java
com.aspose.html.converters.Converter.convertEPUB(
        fileInputStream,
        new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Jpeg),
        streamProvider.lStream
);
```

## การเข้าถึงสตรีมหน่วยความจำ

คุณสามารถเข้าถึงสตรีมหน่วยความจำที่ประกอบด้วยข้อมูลผลลัพธ์ได้:

```java
int size = streamProvider.lStream.size();
for (int i = 0; i < size; i++) {
    java.io.InputStream inputStream = streamProvider.lStream.get(i);
    // รหัสของคุณที่นี่
}
```

## ล้างเพจไปยังไฟล์เอาต์พุต

สุดท้ายคุณต้องล้างเพจไปยังไฟล์เอาท์พุต:

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("page_{" + (i + 1) + "}.jpg"))) {
    byte[] buffer = new byte[inputStream.available()];
    inputStream.read(buffer);
    fileOutputStream.write(buffer);
}
```

## บทสรุป

ขอแสดงความยินดี! คุณได้เรียนรู้วิธีใช้ Aspose.HTML สำหรับ Java เพื่อแปลงไฟล์ EPUB เป็นรูปภาพสำเร็จแล้ว ไลบรารีอันทรงพลังนี้จะเปิดโลกแห่งความเป็นไปได้ให้กับแอปพลิเคชัน Java ของคุณ

## คำถามที่พบบ่อย

### 1. Aspose.HTML สำหรับ Java คืออะไร?

Aspose.HTML สำหรับ Java เป็นไลบรารีที่ช่วยให้ผู้พัฒนา Java สามารถทำงานกับ HTML, EPUB และรูปแบบอื่นๆ ที่เกี่ยวข้องกับเว็บได้

### 2. ฉันสามารถหาเอกสารสำหรับ Aspose.HTML สำหรับ Java ได้ที่ไหน

 คุณสามารถค้นหาเอกสารประกอบได้[ที่นี่](https://reference.aspose.com/html/java/).

### 3. มีการทดลองใช้ฟรีหรือไม่?

 ใช่ คุณสามารถรับ Aspose.HTML สำหรับ Java รุ่นทดลองใช้งานฟรีได้[ที่นี่](https://releases.aspose.com/).

### 4. ฉันจะได้รับใบอนุญาตชั่วคราวสำหรับ Aspose.HTML สำหรับ Java ได้อย่างไร

 คุณสามารถขอใบอนุญาตชั่วคราวได้[ที่นี่](https://purchase.aspose.com/temporary-license/).

### 5. ฉันจะได้รับการสนับสนุนสำหรับ Aspose.HTML สำหรับ Java ได้จากที่ไหน

 คุณสามารถหาการสนับสนุนได้ที่[ฟอรั่ม Aspose](https://forum.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
