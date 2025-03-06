---
title: การระบุตัวเลือกการบันทึก XPS สำหรับ EPUB เป็น XPS
linktitle: การระบุตัวเลือกการบันทึก XPS สำหรับ EPUB เป็น XPS
second_title: การประมวลผล Java HTML ด้วย Aspose.HTML
description: เรียนรู้วิธีใช้ Aspose.HTML สำหรับ Java เพื่อระบุตัวเลือกการบันทึก XPS สำหรับ EPUB เป็น XPS ในบทช่วยสอนทีละขั้นตอนนี้ แปลงไฟล์ EPUB ได้อย่างราบรื่น
weight: 12
url: /th/java/converting-epub-to-xps/convert-epub-to-xps-specify-xps-save-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การระบุตัวเลือกการบันทึก XPS สำหรับ EPUB เป็น XPS

ในโลกของการพัฒนาเว็บ ความสามารถในการแปลงไฟล์ EPUB เป็นรูปแบบ XPS ถือเป็นเครื่องมือที่มีประโยชน์ Aspose.HTML สำหรับ Java เป็นไลบรารีที่มีประสิทธิภาพซึ่งให้ความสามารถในการแปลงไฟล์นี้ได้อย่างง่ายดาย ในบทช่วยสอนที่ครอบคลุมนี้ เราจะแนะนำคุณตลอดกระบวนการระบุตัวเลือกการบันทึก XPS สำหรับ EPUB เป็น XPS โดยใช้ Aspose.HTML สำหรับ Java

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเจาะลึกในบทช่วยสอน มีข้อกำหนดเบื้องต้นบางประการที่คุณต้องมี:

1. สภาพแวดล้อมการพัฒนา Java: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Java Development Kit (JDK) ไว้ในระบบของคุณ

2.  Aspose.HTML สำหรับไลบรารี Java: ดาวน์โหลดและติดตั้ง Aspose.HTML สำหรับ Java จาก[ลิงค์ดาวน์โหลด](https://releases.aspose.com/html/java/).

3. ไฟล์ EPUB: คุณจะต้องมีไฟล์ EPUB ที่คุณต้องการแปลงเป็น XPS

ตอนนี้เรามีข้อกำหนดเบื้องต้นแล้ว เรามาดูขั้นตอนที่จำเป็นในการระบุตัวเลือกการบันทึก XPS สำหรับ EPUB เป็น XPS กัน

## แพ็คเกจนำเข้า

ขั้นแรก คุณต้องนำเข้าแพ็คเกจที่จำเป็นเพื่อทำงานกับ Aspose.HTML สำหรับ Java คุณสามารถทำได้โดยเพิ่มโค้ดต่อไปนี้ที่จุดเริ่มต้นของไฟล์ Java:

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

เริ่มต้นด้วยการเปิดไฟล์ EPUB ที่มีอยู่เพื่ออ่าน คุณสามารถใช้โค้ดสั้นๆ ดังต่อไปนี้:

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    //โค้ดของคุณสำหรับการจัดการไฟล์ EPUB อยู่ที่นี่
}
```

## สร้างตัวเลือกการบันทึก XPS

ขั้นตอนต่อไป ให้สร้างอินสแตนซ์ของ XpsSaveOptions ด้วยขนาดหน้าและสีพื้นหลังแบบกำหนดเอง ซึ่งทำได้โดยกำหนดค่า PageSetup และตัวเลือกต่างๆ ต่อไปนี้คือวิธีดำเนินการ:

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

 สุดท้ายคุณต้องโทรหา`convertEPUB` วิธีการแปลง EPUB เป็น XPS นี่คือโค้ดสำหรับขั้นตอนดังกล่าว:

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

เมื่อทำตามขั้นตอนเหล่านี้แล้ว คุณสามารถระบุตัวเลือกการบันทึก XPS สำหรับการแปลง EPUB เป็น XPS ได้อย่างง่ายดายโดยใช้ Aspose.HTML สำหรับ Java บทช่วยสอนนี้มีคำแนะนำที่ครอบคลุมแก่คุณ และหากทำตามขั้นตอนเหล่านี้ คุณจะสามารถทำงานกับไฟล์ EPUB และแปลงเป็นรูปแบบ XPS ได้อย่างราบรื่น

## บทสรุป

ในบทช่วยสอนนี้ เราจะแนะนำคุณเกี่ยวกับขั้นตอนในการระบุตัวเลือกการบันทึก XPS สำหรับการแปลง EPUB เป็น XPS โดยใช้ Aspose.HTML สำหรับ Java ด้วยข้อกำหนดเบื้องต้นที่ถูกต้องและคำแนะนำทีละขั้นตอน คุณสามารถใช้ประโยชน์จากพลังของไลบรารีนี้สำหรับโครงการพัฒนาเว็บของคุณได้อย่างมีประสิทธิภาพ

## คำถามที่พบบ่อย

### 1. Aspose.HTML สำหรับ Java คืออะไร?
Aspose.HTML สำหรับ Java เป็นไลบรารีอันทรงพลังสำหรับการทำงานกับไฟล์ HTML และ EPUB ช่วยให้นักพัฒนาสามารถดำเนินการต่างๆ ได้มากมาย รวมถึงการแปลงเป็นรูปแบบต่างๆ

### 2. ฉันสามารถใช้ Aspose.HTML สำหรับ Java ในโครงการเชิงพาณิชย์ของฉันได้หรือไม่
 ใช่ คุณสามารถใช้ Aspose.HTML สำหรับ Java ในโครงการเชิงพาณิชย์ได้ สำหรับรายละเอียดเกี่ยวกับการอนุญาตใช้งาน คุณสามารถเยี่ยมชมได้ที่[หน้าการซื้อ](https://purchase.aspose.com/buy).

### 3. มีรุ่นทดลองใช้งานฟรีสำหรับ Aspose.HTML สำหรับ Java หรือไม่
 ใช่ คุณสามารถสำรวจห้องสมุดได้ด้วยการทดลองใช้ฟรี ดาวน์โหลดได้จาก[ที่นี่](https://releases.aspose.com/).

### 4. ฉันจะได้รับการสนับสนุนหรือถามคำถามเกี่ยวกับ Aspose.HTML สำหรับ Java ได้ที่ไหน
 คุณสามารถเยี่ยมชมฟอรัม Aspose เพื่อรับการสนับสนุนและการสนทนาได้ที่[https://forum.aspose.com/](https://forum.aspose.com/).

### 5. ข้อกำหนดของระบบสำหรับ Aspose.HTML สำหรับ Java คืออะไร
Aspose.HTML สำหรับ Java ต้องใช้ Java Development Kit (JDK) และระบบปฏิบัติการที่เข้ากันได้ ตรวจสอบให้แน่ใจว่าคุณปฏิบัติตามข้อกำหนดเบื้องต้นตามที่กล่าวไว้ในบทช่วยสอนนี้
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
