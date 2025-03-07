---
title: นำ CSS ภายในไปใช้ในเอกสาร HTML ด้วย Aspose.HTML สำหรับ Java
linktitle: นำ CSS ภายในไปใช้ในเอกสาร HTML ด้วย Aspose.HTML สำหรับ Java
second_title: การประมวลผล Java HTML ด้วย Aspose.HTML
description: เรียนรู้การนำ CSS ภายในไปใช้ในเอกสาร HTML โดยใช้ Aspose.HTML สำหรับ Java ด้วยบทช่วยสอนทีละขั้นตอนง่ายๆ ของเรา
weight: 16
url: /th/java/editing-html-documents/implement-internal-css-html-documents/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# นำ CSS ภายในไปใช้ในเอกสาร HTML ด้วย Aspose.HTML สำหรับ Java

## การแนะนำ
การสร้างหน้าเว็บที่สวยงามและมีโครงสร้างที่ดีมักจะต้องอาศัยองค์ประกอบสำคัญอย่างหนึ่ง นั่นคือ การจัดรูปแบบ ในการพัฒนาเว็บ CSS (Cascading Style Sheets) เปรียบเสมือนการแต่ง HTML ของคุณ โดยทำให้ทุกอย่างดูน่าสนใจและเป็นระเบียบ วันนี้ เราจะมาเจาะลึกถึงวิธีการผสาน CSS ภายในเอกสาร HTML โดยใช้ Aspose.HTML สำหรับ Java ไม่ว่าคุณจะเป็นมือใหม่หรือผู้พัฒนาที่มีประสบการณ์ บทช่วยสอนนี้จะอธิบายขั้นตอนต่างๆ ในรูปแบบที่เรียบง่ายและน่าสนใจ
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่มต้น เรามาตรวจสอบกันก่อนว่าคุณมีทุกอย่างที่จำเป็นในการปฏิบัติตามบทช่วยสอนนี้แล้ว นี่คือข้อกำหนดเบื้องต้น:
1.  Java Development Kit (JDK): ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง JDK ไว้ในเครื่องของคุณแล้ว คุณสามารถดาวน์โหลดได้จาก[เว็บไซต์ออราเคิล](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html) หรือ[โอเพ่น เจดีเค](https://openjdk.java.net/).
2.  ไลบรารี Aspose.HTML สำหรับ Java: คุณจะต้องมีไลบรารี Aspose.HTML เพื่อจัดการและปรับเปลี่ยนเอกสาร HTML ได้อย่างง่ายดาย คุณสามารถดาวน์โหลดไลบรารีได้จาก[เว็บไซต์อาโพส](https://releases.aspose.com/html/java/).
3. สภาพแวดล้อมการพัฒนาแบบบูรณาการ (IDE): IDE ที่ดี เช่น IntelliJ IDEA หรือ Eclipse สามารถทำให้การเขียนโค้ดราบรื่นยิ่งขึ้น
4. ความรู้พื้นฐานเกี่ยวกับ Java: บทช่วยสอนนี้ถือว่าคุณมีความคุ้นเคยกับการเขียนโปรแกรม Java ในระดับหนึ่ง
5. เวลาและความอดทน: แม้ว่ากระบวนการนี้จะตรงไปตรงมา แต่การดำเนินการทีละขั้นตอนเป็นสิ่งสำคัญ
## แพ็คเกจนำเข้า
ก่อนที่เราจะเริ่มเขียนโค้ด เรามาทำการนำเข้าแพ็คเกจที่จำเป็นเพื่อให้แน่ใจว่าโปรแกรมของเราสามารถเข้าถึงฟีเจอร์ต่างๆ ที่ Aspose.HTML จัดเตรียมไว้ให้
```java
import java.io.IOException;
```
อย่าลืมเพิ่มคำสั่งนำเข้าเหล่านี้ไว้ที่ด้านบนของไฟล์ Java ซึ่งจะทำให้เราสามารถใช้งานคลาสที่จำเป็นสำหรับการสร้างและจัดการเอกสาร HTML และแสดงผลเป็น PDF ได้
ให้เราแบ่งกระบวนการออกเป็นขั้นตอนที่ชัดเจน เพื่อให้คุณปฏิบัติตามได้ง่าย
## ขั้นตอนที่ 1: สร้างอินสแตนซ์ของเอกสาร HTML
ก่อนอื่นเราต้องสร้างอินสแตนซ์ของเอกสาร HTML โดยทำดังนี้:
```java
String content = "<div><p>Internal CSS</p><p>An internal CSS is used to define a style for a single HTML page</p></div>";
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument(content, ".");
```
 ที่นี่เราจะกำหนดโครงสร้าง HTML ง่ายๆ ด้วยสองย่อหน้าภายใน`div` . การ`HTMLDocument` อินสแตนซ์จะเริ่มต้นโครงสร้างนี้ เพื่อเตรียมการปรับเปลี่ยนและกำหนดรูปแบบ
## ขั้นตอนที่ 2: สร้างและเพิ่มองค์ประกอบสไตล์
ต่อไปเราจะสร้างรูปแบบ CSS ภายในของเรา นี่คือจุดเริ่มต้นของมนต์เสน่ห์แห่งการจัดรูปแบบ!
```java
com.aspose.html.dom.Element style = document.createElement("style");
style.setTextContent(".frame1 { margin-top:50px; margin-left:50px; padding:20px; width:360px; height:90px; background-color:#a52a2a; font-family:verdana; color:#FFF5EE;}" +
                      ".frame2 { margin-top:-90px; margin-left:160px; text-align:center; padding:20px; width:360px; height:100px; background-color:#ADD8E6;}");
```
 ในขั้นตอนนี้เราจะสร้าง`<style>` องค์ประกอบและการกำหนดคลาส CSS สองคลาส—`frame1` และ`frame2`แต่ละคลาสจะมีรูปแบบเฉพาะสำหรับขอบ การเติม สีพื้นหลัง และคุณสมบัติของแบบอักษร นี่คือจุดที่ CSS ภายในของเราเริ่มเป็นรูปเป็นร่างขึ้นมา
## ขั้นตอนที่ 3: ผนวกองค์ประกอบสไตล์ลงในส่วนหัวเอกสาร
ตอนนี้เราได้สร้างสไตล์แล้ว เราต้องผนวกสไตล์เหล่านี้ไปที่ส่วนหัวของเอกสาร
```java
com.aspose.html.dom.Element head = document.getElementsByTagName("head").get_Item(0);
head.appendChild(style);
```
 โค้ดตัวอย่างนี้จะระบุตำแหน่ง`head` ของเอกสารและผนวกของเรา`<style>` องค์ประกอบนี้เชื่อมโยงสไตล์ CSS ของเรากับเนื้อหา HTML ด้านล่างนี้
## ขั้นตอนที่ 4: กำหนดคลาส CSS ให้กับองค์ประกอบ HTML
ต่อไปเราจะนำรูปแบบที่เรากำหนดไปใช้กับองค์ประกอบย่อหน้าภายในเอกสารของเรา
```java
com.aspose.html.HTMLElement paragraph = (com.aspose.html.HTMLElement) document.getElementsByTagName("p").get_Item(0);
paragraph.setClassName("frame1");
HTMLElement lastParagraph = (HTMLElement) document.getElementsByTagName("p").get_Item(document.getElementsByTagName("p").getLength() - 1);
lastParagraph.setClassName("frame2");
```
 ที่นี่เราดึงองค์ประกอบย่อหน้าและตั้งชื่อคลาสของพวกมันเป็น`frame1` และ`frame2`ตอนนี้ย่อหน้าของเราจะสืบทอดรูปแบบที่เราเพิ่งกำหนดไว้!
## ขั้นตอนที่ 5: ปรับแต่งคุณสมบัติสไตล์
ให้ปรับปรุงการนำเสนอภาพให้ดียิ่งขึ้นโดยปรับแต่งคุณสมบัติรูปแบบของย่อหน้าของเรา
```java
paragraph.getStyle().setFontSize("250%");
paragraph.getStyle().setTextAlign("center");
lastParagraph.getStyle().setColor("#434343");
lastParagraph.getStyle().setFontSize("150%");
lastParagraph.getStyle().setFontFamily("verdana");
```
ในขั้นตอนนี้ เราจะปรับขนาดและจัดตำแหน่งของตัวอักษรในย่อหน้าแรก รวมถึงปรับสีและตัวอักษรในย่อหน้าที่สอง การปรับแต่งนี้จะเพิ่มเอกลักษณ์และความชัดเจนให้กับเอกสารของคุณ
## ขั้นตอนที่ 6: บันทึกเอกสาร HTML
ตอนนี้เราได้ทำการตั้งค่า CSS ภายในเสร็จแล้วและทำการเปลี่ยนแปลงแล้ว ถึงเวลาบันทึกเอกสารลงในไฟล์
```java
document.save("edit-internal-css.html");
```
 การ`save` วิธีการรักษาเอกสารของเราไว้ในไฟล์ HTML ชื่อ`edit-internal-css.html`คุณสามารถเปิดไฟล์นี้ในเว็บเบราว์เซอร์ใดก็ได้เพื่อดูการเปลี่ยนแปลงของคุณ!
## ขั้นตอนที่ 7: เรนเดอร์เอกสาร HTML เป็น PDF
ขั้นตอนสุดท้ายคือการแปลงเอกสาร HTML ของเราเป็นรูปแบบ PDF ซึ่งมีประโยชน์มากโดยเฉพาะอย่างยิ่งสำหรับการแบ่งปันหรือการพิมพ์เนื้อหาที่คุณแปลงแล้ว
```java
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice("edit-internal-css.pdf");
document.renderTo(device);
```
 ที่นี่เราสร้าง`PdfDevice` อินสแตนซ์ที่ชี้ไปยังไฟล์เอาท์พุตที่เราต้องการ`renderTo` วิธีการนี้จะแปลงเอกสาร HTML เป็น PDF เจ๋งไหมล่ะ?
## บทสรุป
และแล้วคุณก็รู้แล้ว! ตอนนี้คุณรู้วิธีการนำ CSS ภายในไปใช้กับเอกสาร HTML โดยใช้ Aspose.HTML สำหรับ Java แล้ว เมื่อทำตามบทช่วยสอนนี้แล้ว คุณจะไม่เพียงแต่เรียนรู้วิธีจัดรูปแบบ HTML เท่านั้น แต่ยังเรียนรู้วิธีบันทึกและแสดงผลเป็น PDF อีกด้วย ด้วยเครื่องมือเหล่านี้ คุณสามารถทำให้หน้าเว็บของคุณดูมีสไตล์และดูเป็นมืออาชีพได้ ดังนั้นทำไมต้องรอล่ะ? เริ่มลงมือและลองใช้ตัวเลือกการจัดรูปแบบได้เลย!

## คำถามที่พบบ่อย
### ข้อดีของการใช้ CSS ภายในคืออะไร?  
CSS ภายในช่วยให้คุณกำหนดรูปแบบเอกสาร HTML เดียวโดยไม่ส่งผลกระทบต่อเอกสารอื่นๆ ทำให้เหมาะสำหรับการออกแบบที่ไม่ซ้ำใคร
### Aspose.HTML จัดการไฟล์ CSS ภายนอกได้หรือไม่  
ใช่ Aspose.HTML สามารถจัดการไฟล์ CSS ภายนอกได้ และคุณสามารถเชื่อมโยงไฟล์เหล่านั้นได้ในลักษณะเดียวกันกับสไตล์ภายใน
### Aspose.HTML เป็นโอเพ่นซอร์สหรือไม่?  
ไม่ Aspose.HTML เป็นไลบรารีเชิงพาณิชย์ แต่คุณสามารถเริ่มต้นด้วยการทดลองใช้ฟรีเพื่อสำรวจฟีเจอร์ต่างๆ ของมันได้
### ฉันจะติดต่อฝ่ายสนับสนุนได้อย่างไรหากประสบปัญหา?  
 คุณสามารถเยี่ยมชม[ฟอรั่มสนับสนุน Aspose](https://forum.aspose.com/c/html/29) เพื่อขอความช่วยเหลือ
### มีข้อควรพิจารณาเรื่องประสิทธิภาพเมื่อทำการเรนเดอร์ HTML เป็น PDF หรือไม่  
ใช่ เอกสาร HTML ที่ซับซ้อนอาจใช้เวลาในการเรนเดอร์นานกว่า การปรับแต่งเนื้อหาสามารถปรับปรุงประสิทธิภาพได้
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
