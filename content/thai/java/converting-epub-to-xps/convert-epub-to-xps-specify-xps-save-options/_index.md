---
title: การระบุตัวเลือกการบันทึก XPS สำหรับ EPUB ถึง XPS
linktitle: การระบุตัวเลือกการบันทึก XPS สำหรับ EPUB ถึง XPS
second_title: การประมวลผล Java HTML ด้วย Aspose.HTML
description: เรียนรู้วิธีใช้ Aspose.HTML สำหรับ Java เพื่อระบุตัวเลือกการบันทึก XPS สำหรับ EPUB เป็น XPS ในบทช่วยสอนทีละขั้นตอนนี้ แปลงไฟล์ EPUB ได้อย่างราบรื่น
type: docs
weight: 12
url: /th/java/converting-epub-to-xps/convert-epub-to-xps-specify-xps-save-options/
---
ในโลกของการพัฒนาเว็บ ความสามารถในการแปลงไฟล์ EPUB เป็นรูปแบบ XPS ถือเป็นเครื่องมืออันทรงคุณค่า Aspose.HTML สำหรับ Java เป็นไลบรารีที่มีประสิทธิภาพซึ่งนำเสนอความสามารถในการแปลงนี้ได้อย่างง่ายดาย ในบทช่วยสอนที่ครอบคลุมนี้ เราจะแนะนำคุณตลอดกระบวนการระบุตัวเลือกการบันทึก XPS สำหรับ EPUB ถึง XPS โดยใช้ Aspose.HTML สำหรับ Java

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเจาะลึกบทช่วยสอน มีข้อกำหนดเบื้องต้นบางประการที่คุณต้องมี:

1. สภาพแวดล้อมการพัฒนา Java: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Java Development Kit (JDK) บนระบบของคุณ

2.  Aspose.HTML สำหรับ Java Library: ดาวน์โหลดและติดตั้ง Aspose.HTML สำหรับ Java จากไฟล์[ลิ้งค์ดาวน์โหลด](https://releases.aspose.com/html/java/).

3. ไฟล์ EPUB: คุณจะต้องมีไฟล์ EPUB ที่คุณต้องการแปลงเป็น XPS

ตอนนี้เรามีข้อกำหนดเบื้องต้นแล้ว มาดูขั้นตอนที่จำเป็นเพื่อระบุตัวเลือกการบันทึก XPS สำหรับ EPUB เป็น XPS กัน

## แพ็คเกจนำเข้า

ขั้นแรก คุณต้องนำเข้าแพ็คเกจที่จำเป็นเพื่อทำงานกับ Aspose.HTML สำหรับ Java คุณสามารถทำได้โดยเพิ่มโค้ดต่อไปนี้ที่จุดเริ่มต้นของไฟล์ Java ของคุณ:

```java
import java.io.FileInputStream;
import com.aspose.html.saving.XpsSaveOptions;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.drawing.Page;
import com.aspose.html.drawing.Size;
import com.aspose.html.drawing.Length;
import com.aspose.html.drawing.Color;
import com.aspose.html.converters.Converter;
import com.aspose.html.system.io.resources.Resources;
```

## เปิดไฟล์ EPUB

เริ่มต้นด้วยการเปิดไฟล์ EPUB ที่มีอยู่เพื่ออ่าน คุณสามารถใช้ข้อมูลโค้ดต่อไปนี้:

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    //รหัสของคุณสำหรับการจัดการไฟล์ EPUB อยู่ที่นี่
}
```

## สร้างตัวเลือกการบันทึก XPS

จากนั้น สร้างอินสแตนซ์ของ XpsSaveOptions ด้วยขนาดหน้าและสีพื้นหลังที่กำหนดเอง ทำได้โดยการกำหนดค่า PageSetup และตัวเลือก นี่คือวิธีที่คุณสามารถบรรลุเป้าหมายนี้:

```java
XpsSaveOptions options = new XpsSaveOptions();
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
anyPage.setSize(new Size(Length.fromPixels(3000), Length.fromPixels(1000)));
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

## แปลง EPUB เป็น XPS

 สุดท้ายคุณต้องโทรไปที่`convertEPUB` วิธีการแปลง EPUB เป็น XPS นี่คือรหัสสำหรับสิ่งนั้น:

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

ด้วยขั้นตอนเหล่านี้ คุณสามารถระบุตัวเลือกการบันทึก XPS สำหรับการแปลง EPUB เป็น XPS โดยใช้ Aspose.HTML สำหรับ Java ได้อย่างง่ายดาย บทช่วยสอนนี้มีคำแนะนำที่ครอบคลุมให้คุณ และเมื่อทำตามขั้นตอนเหล่านี้ คุณจะสามารถทำงานกับไฟล์ EPUB และแปลงเป็นรูปแบบ XPS ได้อย่างราบรื่น

## บทสรุป

ในบทช่วยสอนนี้ เราได้แนะนำคุณตลอดกระบวนการระบุตัวเลือกการบันทึก XPS สำหรับการแปลง EPUB เป็น XPS โดยใช้ Aspose.HTML สำหรับ Java ด้วยข้อกำหนดเบื้องต้นที่เหมาะสมและคำแนะนำทีละขั้นตอน คุณจะสามารถควบคุมพลังของไลบรารีนี้สำหรับโครงการพัฒนาเว็บของคุณได้อย่างมีประสิทธิภาพ

## คำถามที่พบบ่อย

### 1. Aspose.HTML สำหรับ Java คืออะไร
Aspose.HTML สำหรับ Java เป็นไลบรารีที่มีประสิทธิภาพสำหรับการทำงานกับไฟล์ HTML และ EPUB ช่วยให้นักพัฒนาสามารถดำเนินการต่างๆ รวมถึงการแปลงเป็นรูปแบบต่างๆ

### 2. ฉันสามารถใช้ Aspose.HTML สำหรับ Java ในโครงการเชิงพาณิชย์ของฉันได้หรือไม่
 ได้ คุณสามารถใช้ Aspose.HTML สำหรับ Java ในโครงการเชิงพาณิชย์ได้ สำหรับรายละเอียดใบอนุญาต คุณสามารถเยี่ยมชมได้ที่[หน้าซื้อ](https://purchase.aspose.com/buy).

### 3. Aspose.HTML สำหรับ Java มีให้ทดลองใช้ฟรีหรือไม่
 ใช่ คุณสามารถสำรวจห้องสมุดด้วยการทดลองใช้ฟรี ดาวน์โหลดได้จาก[ที่นี่](https://releases.aspose.com/).

### 4. ฉันจะรับการสนับสนุนหรือถามคำถามเกี่ยวกับ Aspose.HTML สำหรับ Java ได้ที่ไหน
 คุณสามารถเยี่ยมชมฟอรัม Aspose เพื่อรับการสนับสนุนและการสนทนาได้ที่[https://forum.aspose.com/](https://forum.aspose.com/).

### 5. ข้อกำหนดของระบบสำหรับ Aspose.HTML สำหรับ Java คืออะไร
Aspose.HTML สำหรับ Java ต้องใช้ Java Development Kit (JDK) และระบบปฏิบัติการที่เข้ากันได้ ตรวจสอบให้แน่ใจว่าคุณมีคุณสมบัติตรงตามข้อกำหนดเบื้องต้นตามที่กล่าวไว้ในบทช่วยสอนนี้