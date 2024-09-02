---
title: กำหนดค่าแบบอักษรใน Aspose.HTML สำหรับ Java
linktitle: กำหนดค่าแบบอักษรใน Aspose.HTML สำหรับ Java
second_title: การประมวลผล Java HTML ด้วย Aspose.HTML
description: เรียนรู้วิธีการกำหนดค่าแบบอักษรใน Aspose.HTML สำหรับ Java ด้วยคู่มือทีละขั้นตอนโดยละเอียดนี้ ปรับปรุงการแปลง HTML เป็น PDF ของคุณด้วยแบบอักษรและรูปแบบที่กำหนดเอง
type: docs
weight: 11
url: /th/java/configuring-environment/configure-fonts/
---
## การแนะนำ
เมื่อทำงานกับเอกสาร HTML ใน Java การกำหนดค่าฟอนต์อย่างถูกต้องถือเป็นสิ่งสำคัญสำหรับการสร้างเนื้อหาที่ดึงดูดสายตาและอ่านได้ ไม่ว่าคุณจะกำลังสร้างรายงาน สร้างเว็บเพจ หรือแปลงเอกสาร การกำหนดค่าฟอนต์ให้ถูกต้องก็สามารถสร้างความแตกต่างได้อย่างมาก บทช่วยสอนนี้จะแนะนำคุณเกี่ยวกับขั้นตอนการกำหนดค่าฟอนต์ใน Aspose.HTML สำหรับ Java ตั้งแต่การตั้งค่าสภาพแวดล้อมของคุณไปจนถึงการแปลง HTML เป็น PDF ด้วยฟอนต์ที่กำหนดเอง มาเริ่มกันเลย!

## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่มต้น มีข้อกำหนดเบื้องต้นบางประการที่คุณจะต้องมี:
1. Java Development Kit (JDK): ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง JDK 1.8 ขึ้นไปในระบบของคุณ
2.  Aspose.HTML สำหรับไลบรารี Java: คุณสามารถดาวน์โหลดไลบรารีได้จาก[เว็บไซต์อาโพส](https://releases.aspose.com/html/java/).
3. สภาพแวดล้อมการพัฒนาแบบบูรณาการ (IDE): ใช้ IDE เช่น IntelliJ IDEA หรือ Eclipse เพื่อจัดการโครงการของคุณ
4. ความรู้พื้นฐานเกี่ยวกับการเขียนโปรแกรม Java: ความคุ้นเคยกับ Java จะช่วยให้คุณทำตามบทช่วยสอนได้อย่างมีประสิทธิผลมากขึ้น
5.  ใบอนุญาต Aspose.HTML: แม้ว่าคุณจะใช้ Aspose.HTML ได้โดยไม่ต้องมีใบอนุญาต แต่ใบอนุญาตชั่วคราวหรือใบอนุญาตเต็มรูปแบบจะลบข้อจำกัดในการประเมินใดๆ ออกไป รับใบอนุญาตของคุณ[ใบอนุญาตชั่วคราวที่นี่](https://purchase.aspose.com/temporary-license/).

## แพ็คเกจนำเข้า
ในการเริ่มต้น คุณจะต้องนำเข้าแพ็คเกจที่จำเป็นลงในโปรเจ็กต์ Java ของคุณ แพ็คเกจเหล่านี้มีคลาสและวิธีการที่จำเป็นสำหรับการกำหนดค่าแบบอักษร จัดการเอกสาร HTML และแปลงเป็นรูปแบบอื่น
```java
import java.io.IOException;
```
การนำเข้าเหล่านี้นำฟังก์ชันหลักของ Aspose.HTML สำหรับ Java เข้ามา ช่วยให้คุณสามารถโต้ตอบกับเนื้อหา HTML ผ่านโปรแกรมได้
## ขั้นตอนที่ 1: สร้างเนื้อหา HTML
ขั้นแรก เราต้องสร้างเนื้อหา HTML พื้นฐานที่เราจะปรับแต่งและแปลงเป็น PDF ในภายหลัง เนื้อหานี้จะถูกบันทึกไว้ในไฟล์ HTML
### 1.1 การเขียนโค้ด HTML
 เราจะเริ่มต้นด้วยการกำหนดโค้ด HTML ที่มีส่วนหัวและย่อหน้า โค้ดนี้จะถูกบันทึกไว้ในไฟล์ชื่อ`user-agent-fontsetting.html`.
```java
String code = "<h1>FontsSettings property</h1>\r\n" +
    "<p>The FontsSettings property is used for configuration of fonts handling.</p>\r\n";
```
สตริงนี้ประกอบด้วยเนื้อหา HTML ที่เราต้องการกำหนดรูปแบบ สังเกตว่ามีส่วนหัว (`<h1>`) และย่อหน้า (`<p>`-
### 1.2 การบันทึกเนื้อหา HTML ลงในไฟล์
 ถัดไปคุณจะบันทึกเนื้อหา HTML นี้ลงในไฟล์โดยใช้`FileWriter`.
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("user-agent-fontsetting.html")) {
    fileWriter.write(code);
}
```
 โค้ดตัวอย่างนี้จะเขียนสตริง HTML ลงในไฟล์ชื่อ`user-agent-fontsetting.html` ในไดเร็กทอรีโครงการของคุณ
## ขั้นตอนที่ 2: กำหนดค่าสภาพแวดล้อม Aspose.HTML
เมื่อไฟล์ HTML พร้อมแล้ว ขั้นตอนถัดไปคือการกำหนดค่าสภาพแวดล้อม Aspose.HTML ซึ่งเกี่ยวข้องกับการตั้งค่าการจัดการแบบอักษรและพารามิเตอร์การจัดรูปแบบอื่นๆ
### 2.1 การสร้างอินสแตนซ์ของการกำหนดค่า
 เราเริ่มต้นด้วยการสร้างอินสแตนซ์ของ`Configuration` คลาสที่ช่วยให้เรากำหนดค่าด้านต่างๆ ของการประมวลผลเอกสาร HTML ได้
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```
อินสแตนซ์นี้จะใช้ในการเข้าถึงและแก้ไขการตั้งค่าตัวแทนผู้ใช้ซึ่งควบคุมวิธีการแสดง HTML
### 2.2 การเข้าถึงบริการตัวแทนผู้ใช้
บริการตัวแทนผู้ใช้มีหน้าที่รับผิดชอบในการใช้รูปแบบและจัดการแบบอักษร เราจะดึงบริการนี้จากการกำหนดค่า
```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```
 บรรทัดโค้ดนี้จะดึงข้อมูล`IUserAgentService`ซึ่งเราจะนำมาใช้เพื่อปรับใช้รูปแบบที่กำหนดเองและกำหนดค่าการตั้งค่าฟอนต์
## ขั้นตอนที่ 3: ใช้รูปแบบและแบบอักษรที่กำหนดเอง
ตอนนี้ตั้งค่าสภาพแวดล้อมเรียบร้อยแล้ว ให้เราลองกำหนดรูปแบบที่กำหนดเองและระบุแบบอักษรที่เราต้องการใช้
### 3.1 การตั้งค่ารูปแบบที่กำหนดเอง
เราจะกำหนดรูปแบบที่กำหนดเองสำหรับส่วนหัว (`h1`) และย่อหน้า (`p`) องค์ประกอบในเอกสาร HTML 
```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; }\r\n" +
    "p { color:grey; }\r\n");
```
ที่นี่เราใช้สีน้ำตาล (`#a52a2a`) ไปที่ส่วนหัวและเป็นสีเทา (`grey`กับข้อความในย่อหน้า รูปแบบเหล่านี้จะนำไปใช้กับองค์ประกอบต่างๆ เมื่อดำเนินการประมวลผลเอกสาร
### 3.2 การตั้งค่าโฟลเดอร์แบบอักษรที่กำหนดเอง
เพื่อให้แน่ใจว่าเอกสารของเราใช้แบบอักษรที่ถูกต้อง เราจะตั้งค่าโฟลเดอร์ที่กำหนดเองซึ่งจัดเก็บแบบอักษรของเรา
```java
userAgent.getFontsSettings().setFontsLookupFolder("fonts");
```
 บรรทัดนี้จะแจ้งให้ Aspose.HTML ค้นหาแบบอักษรใน`fonts` ไดเรกทอรี ตรวจสอบให้แน่ใจว่าโฟลเดอร์นี้มีไฟล์ฟอนต์ที่จำเป็น (เช่น`.ttf` หรือ`.otf` ไฟล์)
## ขั้นตอนที่ 4: โหลดเอกสาร HTML ด้วยการกำหนดค่า
เมื่อกำหนดค่าทุกอย่างเรียบร้อยแล้ว ก็ถึงเวลาโหลดเอกสาร HTML โดยใช้การตั้งค่าที่เราปรับแต่งแล้ว

 เราจะเริ่มต้น`HTMLDocument` วัตถุที่มีการกำหนดค่าที่ระบุและเส้นทางไปยังไฟล์ HTML ของเรา
```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("user-agent-fontsetting.html", configuration);
```
 ขั้นตอนนี้จะสร้าง`HTMLDocument` วัตถุที่พร้อมจะถูกประมวลผลโดยใช้รูปแบบและแบบอักษรที่กำหนดเองที่เราได้กำหนดค่าไว้
## ขั้นตอนที่ 5: แปลง HTML เป็น PDF
ขั้นตอนสุดท้ายของบทช่วยสอนนี้คือการแปลงเอกสาร HTML ที่ได้รับการออกแบบให้เป็นไฟล์ PDF

 เราจะใช้`Converter`คลาสที่จะแปลงเอกสาร HTML ของเราเป็นรูปแบบ PDF
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.PdfSaveOptions(),
    "user-agent-fontsetting_out.pdf"
);
```
 โค้ดสั้นๆ นี้จะแปลงเอกสาร HTML เป็นไฟล์ PDF ที่มีชื่อว่า`user-agent-fontsetting_out.pdf` . การ`PdfSaveOptions` พารามิเตอร์ช่วยให้คุณระบุการตั้งค่าต่าง ๆ สำหรับเอาท์พุต PDF
## ขั้นตอนที่ 6: ทำความสะอาดทรัพยากร
หลังจากการแปลงเสร็จสิ้นแล้ว สิ่งสำคัญคือการกำจัดวัตถุเพื่อปลดปล่อยทรัพยากร
### 6.1 การกำจัดเอกสาร
 อย่าลืมกำจัดทิ้ง`HTMLDocument` วัตถุเพื่อหลีกเลี่ยงการรั่วไหลของหน่วยความจำ
```java
if (document != null) {
    document.dispose();
}
```
 ซึ่งจะทำให้มั่นใจได้ว่าทรัพยากรทั้งหมดที่เกี่ยวข้องกับ`HTMLDocument` ได้ถูกปล่อยตัวแล้ว
### 6.2 การกำจัดการกำหนดค่า
 ในทำนองเดียวกัน กำจัดทิ้ง`Configuration` วัตถุเมื่อคุณทำเสร็จแล้ว
```java
if (configuration != null) {
    configuration.dispose();
}
```
ขั้นตอนการล้างข้อมูลครั้งสุดท้ายนี้จะช่วยให้แน่ใจว่าแอปพลิเคชันของคุณทำงานอย่างมีประสิทธิภาพโดยไม่ต้องใช้ทรัพยากรที่ไม่จำเป็น

## บทสรุป
การกำหนดค่าฟอนต์ใน Aspose.HTML สำหรับ Java เป็นกระบวนการที่ตรงไปตรงมาซึ่งสามารถปรับปรุงรูปลักษณ์และความสามารถในการอ่านของเอกสาร HTML ของคุณได้อย่างมาก โดยทำตามขั้นตอนที่ระบุไว้ในคู่มือนี้ คุณสามารถใช้รูปแบบที่กำหนดเอง จัดการฟอนต์ และแปลงเนื้อหา HTML ของคุณเป็นรูปแบบ PDF ได้อย่างง่ายดายด้วยโค้ดเพียงไม่กี่บรรทัด ไม่ว่าคุณจะเป็นนักพัฒนาที่มีประสบการณ์หรือเป็นมือใหม่ใน Java Aspose.HTML ก็มีเครื่องมือที่คุณต้องการเพื่อสร้างเอกสารคุณภาพระดับมืออาชีพได้อย่างง่ายดาย

## คำถามที่พบบ่อย
### ฉันสามารถใช้แบบอักษรใดก็ได้กับ Aspose.HTML สำหรับ Java ได้หรือไม่  
 ใช่ คุณสามารถใช้แบบอักษรใดก็ได้ที่ระบบปฏิบัติการของคุณรองรับ ตรวจสอบให้แน่ใจว่าคุณวางไฟล์แบบอักษรไว้ในไดเรกทอรีที่ระบุโดย`FontsLookupFolder`.
### ฉันต้องมีใบอนุญาตเพื่อใช้ Aspose.HTML สำหรับ Java หรือไม่  
 แม้ว่าคุณจะสามารถใช้ Aspose.HTML ได้โดยไม่ต้องมีใบอนุญาตเพื่อวัตถุประสงค์ในการประเมินผล[ใบอนุญาตชั่วคราว](https://purchase.aspose.com/temporary-license/) หรือแนะนำให้ใช้ใบอนุญาตเต็มรูปแบบสำหรับการใช้ในการผลิตเพื่อหลีกเลี่ยงข้อจำกัด
### ฉันจะปรับแต่งการตั้งค่าเอาท์พุต PDF ได้อย่างไร  
 คุณสามารถปรับแต่งผลลัพธ์ PDF ได้โดยการแก้ไข`PdfSaveOptions`วัตถุที่ถูกส่งต่อไปยัง`convertHTML` วิธี.
### เป็นไปได้ไหมที่จะใช้สไตล์ CSS ที่ซับซ้อนมากขึ้นด้วย Aspose.HTML  
ใช่ Aspose.HTML รองรับรูปแบบ CSS มากมาย คุณสามารถใช้รูปแบบที่ซับซ้อนได้เช่นเดียวกับการใช้งานในสภาพแวดล้อมเว็บทั่วไป
### ฉันสามารถหาตัวอย่างและเอกสารเพิ่มเติมได้ที่ไหน  
 คุณสามารถค้นหาตัวอย่างและเอกสารประกอบโดยละเอียดเพิ่มเติมได้ที่[หน้าเอกสาร Aspose.HTML สำหรับ Java](https://reference.aspose.com/html/java/).