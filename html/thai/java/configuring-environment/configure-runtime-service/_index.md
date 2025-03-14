---
title: กำหนดค่าบริการรันไทม์ใน Aspose.HTML สำหรับ Java
linktitle: กำหนดค่าบริการรันไทม์ใน Aspose.HTML สำหรับ Java
second_title: การประมวลผล Java HTML ด้วย Aspose.HTML
description: เรียนรู้วิธีการกำหนดค่า Runtime Service ใน Aspose.HTML สำหรับ Java เพื่อเพิ่มประสิทธิภาพการทำงานของสคริปต์ ป้องกันการวนซ้ำไม่สิ้นสุด และปรับปรุงประสิทธิภาพของแอปพลิเคชัน
weight: 14
url: /th/java/configuring-environment/configure-runtime-service/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# กำหนดค่าบริการรันไทม์ใน Aspose.HTML สำหรับ Java

## การแนะนำ
คุณเคยสงสัยไหมว่าจะทำให้แอปพลิเคชัน Java ของคุณทำงานได้เร็วขึ้นและมีประสิทธิภาพมากขึ้นได้อย่างไร ไม่ว่าคุณจะกำลังสร้างแอปพลิเคชันเว็บที่ซับซ้อนหรือเพียงแค่ปรับแต่งเอกสาร HTML ความเร็วเป็นสิ่งสำคัญ ลองนึกภาพว่าคุณสามารถจำกัดระยะเวลาการทำงานของสคริปต์หรือความเร็วในการเริ่มต้นแอปพลิเคชันของระบบได้ ฟังดูมีประโยชน์มากใช่ไหม นั่นคือจุดที่ Runtime Service ใน Aspose.HTML สำหรับ Java เข้ามาช่วย ในบทช่วยสอนนี้ เราจะเจาะลึกถึงวิธีการกำหนดค่า Runtime Service ใน Aspose.HTML สำหรับ Java เพื่อเพิ่มประสิทธิภาพแอปพลิเคชันของคุณโดยการควบคุมเวลาการทำงานของสคริปต์
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะลงรายละเอียด เรามาตรวจสอบกันก่อนว่าคุณมีทุกสิ่งที่คุณต้องการแล้ว 
1.  Java Development Kit (JDK): ตรวจสอบว่าได้ติดตั้ง JDK ไว้ในระบบของคุณแล้ว คุณสามารถดาวน์โหลดได้จาก[เว็บไซต์ของออราเคิล](https://www.oracle.com/java/technologies/javase-downloads.html).
2.  Aspose.HTML สำหรับ Java Library: ดาวน์โหลดเวอร์ชันล่าสุดจาก[หน้าวางจำหน่าย Aspose](https://releases.aspose.com/html/java/). 
3. สภาพแวดล้อมการพัฒนาแบบบูรณาการ (IDE): คุณจะต้องมี IDE เช่น IntelliJ IDEA, Eclipse หรือ NetBeans เพื่อเขียนและรันโค้ด Java ของคุณ
4. ความรู้พื้นฐานเกี่ยวกับ Java และ HTML: ความคุ้นเคยกับการเขียนโปรแกรม Java และ HTML ขั้นพื้นฐานมีความจำเป็นเพื่อปฏิบัติตามได้อย่างราบรื่น

## แพ็คเกจนำเข้า
ก่อนอื่นเรามาพูดถึงการนำเข้าแพ็กเกจที่จำเป็นกันก่อน หากต้องการทำงานกับ Aspose.HTML สำหรับ Java คุณจะต้องนำเข้าคลาสหลายคลาส การนำเข้าเหล่านี้มีความสำคัญเนื่องจากช่วยให้คุณเข้าถึงฟังก์ชันและบริการต่างๆ ที่ Aspose.HTML จัดเตรียมไว้ได้
```java
import java.io.IOException;
```

## ขั้นตอนที่ 1: สร้างไฟล์ HTML ด้วยโค้ด JavaScript
ก่อนที่เราจะเริ่มกำหนดค่า เราต้องมีไฟล์ HTML เพื่อใช้งาน ในขั้นตอนนี้ คุณจะสร้างไฟล์ HTML พื้นฐานที่รวมสไนปเป็ต JavaScript สคริปต์นี้จะถูกใช้ในภายหลังเพื่อสาธิตวิธีที่ Runtime Service สามารถควบคุมเวลาการทำงานได้
```java
String code = "<h1>Runtime Service</h1>\r\n" +
		"<script> while(true) {} </script>\r\n" +
		"<p>The Runtime Service optimizes your system by helping it start apps and programs faster.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("runtime-service.html")) {
	fileWriter.write(code);
}
```

- เรากำหนดโครงสร้าง HTML ง่าย ๆ ที่มีลูป JavaScript (`while(true) {}`ซึ่งจะทำงานอย่างไม่มีกำหนดเวลาหากไม่มีการควบคุม ถือเป็นตัวอย่างที่ดีเยี่ยมในการแสดงให้เห็นถึงพลังของบริการรันไทม์
-  เราใช้`FileWriter` เพื่อเขียนเนื้อหา HTML นี้ลงในไฟล์ที่ชื่อ`"runtime-service.html"`.
## ขั้นตอนที่ 2: ตั้งค่าวัตถุการกำหนดค่า
 ด้วยไฟล์ HTML ในมือของเรา ขั้นตอนต่อไปคือการตั้งค่า`Configuration` วัตถุ การกำหนดค่านี้จะใช้ในการจัดการบริการรันไทม์และการตั้งค่าอื่น ๆ
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

-  เราสร้างอินสแตนซ์ของ`Configuration`ซึ่งทำหน้าที่เป็นแกนหลักในการตั้งค่าและจัดการบริการต่างๆ เช่น Runtime Service ใน Aspose.HTML สำหรับ Java
## ขั้นตอนที่ 3: กำหนดค่าบริการรันไทม์
นี่คือจุดที่เวทมนตร์เกิดขึ้น! ตอนนี้เราจะกำหนดค่า Runtime Service เพื่อจำกัดระยะเวลาการทำงานของ JavaScript ซึ่งจะป้องกันไม่ให้สคริปต์ในไฟล์ HTML ของเราทำงานอย่างไม่มีกำหนดเวลา
```java
try {
	com.aspose.html.services.IRuntimeService runtimeService = configuration.getService(com.aspose.html.services.IRuntimeService.class);
	runtimeService.setJavaScriptTimeout(com.aspose.html.utils.TimeSpan.fromSeconds(5));
```

-  เรามารับ`IRuntimeService` จาก`Configuration` วัตถุ.
-  โดยใช้`setJavaScriptTimeout`เราจำกัดเวลาการทำงานของ JavaScript ไว้ที่ 5 วินาที หากสคริปต์เกินเวลาที่กำหนด สคริปต์จะหยุดทำงานโดยอัตโนมัติ ซึ่งมีประโยชน์อย่างยิ่งในการหลีกเลี่ยงการวนซ้ำไม่สิ้นสุดหรือสคริปต์ยาวๆ ที่อาจทำให้แอปพลิเคชันของคุณค้างได้
## ขั้นตอนที่ 4: โหลดเอกสาร HTML ด้วยการกำหนดค่า
เมื่อกำหนดค่า Runtime Service เสร็จแล้ว ก็ถึงเวลาโหลดเอกสาร HTML โดยใช้การกำหนดค่านี้ ขั้นตอนนี้จะเชื่อมโยงทุกอย่างเข้าด้วยกัน ทำให้สามารถควบคุมสคริปต์ภายในไฟล์ HTML โดย Runtime Service
```java
	com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("runtime-service.html", configuration);
```

-  เราเริ่มต้นการ`HTMLDocument` วัตถุกับไฟล์ HTML ของเรา (`"runtime-service.html"`) และการกำหนดค่าที่ตั้งค่าไว้ก่อนหน้านี้ เพื่อให้แน่ใจว่าการตั้งค่า Runtime Service จะใช้กับเอกสาร HTML นี้โดยเฉพาะ
## ขั้นตอนที่ 5: แปลง HTML เป็น PNG
เอกสาร HTML จะมีประโยชน์อะไรหากคุณไม่สามารถทำอะไรเจ๋งๆ กับมันได้ ในขั้นตอนนี้ เราจะแปลงเอกสาร HTML ของเราเป็นภาพ PNG โดยใช้ฟีเจอร์การแปลงของ Aspose.HTML
```java
	com.aspose.html.converters.Converter.convertHTML(
		document,
		new com.aspose.html.saving.ImageSaveOptions(),
		"runtime-service_out.png"
	);
```

-  เราใช้`Converter.convertHTML` วิธีการแปลงเอกสาร HTML ของเราเป็นภาพ PNG
- `ImageSaveOptions` ใช้เพื่อระบุรูปแบบเอาต์พุต ในกรณีนี้คือ PNG
- รูปภาพเอาท์พุตจะถูกบันทึกเป็น`"runtime-service_out.png"`.
## ขั้นตอนที่ 6: ทำความสะอาดทรัพยากร
 สุดท้ายนี้ ถือเป็นแนวทางปฏิบัติที่ดีในการล้างทรัพยากรเพื่อหลีกเลี่ยงการรั่วไหลของหน่วยความจำ เราจะกำจัด`document` และ`configuration` วัตถุ
```java
} finally {
	if (document != null) {
		document.dispose();
	}
	if (configuration != null) {
		configuration.dispose();
	}
}
```

-  เราตรวจสอบว่า`document` และ`configuration` วัตถุไม่เป็นค่าว่าง จากนั้นจึงกำจัดทิ้ง วิธีนี้จะช่วยให้มั่นใจว่าทรัพยากรที่จัดสรรทั้งหมดได้รับการปลดปล่อย

## บทสรุป
และแล้วคุณก็รู้แล้ว! คุณเพิ่งเรียนรู้วิธีการกำหนดค่า Runtime Service ใน Aspose.HTML สำหรับ Java เพื่อควบคุมเวลาการทำงานของสคริปต์ ซึ่งเป็นเครื่องมือที่มีประสิทธิภาพสำหรับการเพิ่มประสิทธิภาพแอปพลิเคชันของคุณ โดยเฉพาะอย่างยิ่งเมื่อต้องจัดการกับโค้ด JavaScript ที่ซับซ้อนหรืออาจมีปัญหาได้ หากทำตามขั้นตอนที่ระบุไว้ข้างต้น คุณจะมั่นใจได้ว่าแอปพลิเคชัน Java ของคุณทำงานได้อย่างมีประสิทธิภาพมากขึ้น ช่วยประหยัดเวลาและป้องกันปัญหาที่อาจเกิดขึ้นในภายหลัง โปรดจำไว้ว่ากุญแจสำคัญในการเชี่ยวชาญเครื่องมือใดๆ คือการฝึกฝน ดังนั้นอย่าลังเลที่จะทดลองใช้และปรับแต่งการตั้งค่าให้เหมาะกับความต้องการเฉพาะของคุณ ขอให้สนุกกับการเขียนโค้ด!
## คำถามที่พบบ่อย
### วัตถุประสงค์ของ Runtime Service ใน Aspose.HTML สำหรับ Java คืออะไร  
Runtime Service ช่วยให้คุณควบคุมเวลาการทำงานของสคริปต์ในเอกสาร HTML ของคุณ ช่วยป้องกันการวนซ้ำแบบยาวนานหรือไม่มีที่สิ้นสุดซึ่งอาจทำให้แอปพลิเคชันของคุณหยุดทำงาน
### ฉันจะดาวน์โหลด Aspose.HTML สำหรับ Java ได้อย่างไร?  
 คุณสามารถดาวน์โหลด Aspose.HTML เวอร์ชันล่าสุดสำหรับ Java ได้จาก[หน้าวางจำหน่าย](https://releases.aspose.com/html/java/).
###  จำเป็นต้องทิ้งหรือไม่`document` and `configuration` objects?  
ใช่ การกำจัดวัตถุเหล่านี้เป็นสิ่งจำเป็นในการเพิ่มทรัพยากรและป้องกันการรั่วไหลของหน่วยความจำในแอปพลิเคชันของคุณ
### ฉันสามารถตั้งค่าการหมดเวลาของ JavaScript เป็นค่าอื่นที่ไม่ใช่ 5 วินาทีได้หรือไม่  
 แน่นอน! คุณสามารถตั้งค่าเวลาหมดเวลาเป็นค่าใดก็ได้ที่เหมาะกับความต้องการของคุณโดยแก้ไข`TimeSpan.fromSeconds()` พารามิเตอร์.
### ฉันจะได้รับการสนับสนุนได้ที่ไหนหากพบปัญหาเกี่ยวกับ Aspose.HTML สำหรับ Java?  
 หากต้องการความช่วยเหลือ สามารถเข้าไปเยี่ยมชมได้ที่[ฟอรั่ม Aspose.HTML](https://forum.aspose.com/c/html/29).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
