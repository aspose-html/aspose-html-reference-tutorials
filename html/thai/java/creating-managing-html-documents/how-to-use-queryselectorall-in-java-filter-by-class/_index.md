---
category: general
date: 2026-04-23
description: วิธีใช้ querySelectorAll ใน Java เพื่อกรององค์ประกอบตามคลาส, อ่านค่าคุณลักษณะ,
  และวนลูป NodeList เพื่อดึงข้อมูลผลิตภัณฑ์.
draft: false
keywords:
- how to use queryselectorall
- how to read attribute
- iterate nodelist java
- filter elements by class
- select elements css selector
language: th
og_description: วิธีใช้ querySelectorAll ใน Java เพื่อกรององค์ประกอบตามคลาส, อ่านค่าคุณลักษณะ,
  และวนรอบ NodeList เพื่อดึงข้อมูลผลิตภัณฑ์
og_title: วิธีใช้ querySelectorAll ใน Java – กรองด้วยคลาส
tags:
- Java
- HTML parsing
- DOM manipulation
title: วิธีใช้ querySelectorAll ใน Java – กรองด้วยคลาส
url: /th/java/creating-managing-html-documents/how-to-use-queryselectorall-in-java-filter-by-class/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ querySelectorAll ใน Java – กรองตามคลาส

การใช้ querySelectorAll ใน Java เป็นกุญแจสำคัญเมื่อคุณต้องการดึงองค์ประกอบเฉพาะจากเอกสาร HTML ในบทเรียนนี้เราจะกรององค์ประกอบตามคลาส อ่านค่าแอตทริบิวต์ และวนลูป NodeList เพื่อดึงราคาผลิตภัณฑ์จากหน้ารายการสินค้า  

เคยเจอว่าต้องมองไฟล์ HTML ขนาดใหญ่และสงสัยว่าจะดึงการ์ด “on‑sale” เท่านั้นโดยไม่ต้องเขียนพาร์เซอร์แบบกำหนดเองหรือไม่? นั่นคือปัญหาที่เราจะแก้ไขที่นี่—โดยไม่ต้องใช้ไลบรารีเพิ่มเติมนอกจาก Aspose.HTML และขั้นตอนที่ง่ายไม่กี่ขั้นตอน  

คุณจะได้โปรแกรมที่สมบูรณ์และสามารถรันได้ที่มี:

* **เลือกองค์ประกอบ** ด้วย CSS selector (`select elements css selector`),
* **กรองตามคลาส** (`filter elements by class`),
* **อ่านแอตทริบิวต์ที่กำหนดเอง** (`how to read attribute`),
* **วนลูป NodeList ที่ได้** (`iterate nodelist java`).

ไม่จำเป็นต้องมีประสบการณ์กับ Aspose.HTML มาก่อน—เพียงการตั้งค่า Java พื้นฐานและไฟล์ HTML สำหรับทดสอบ  

![how to use querySelectorAll in Java example](https://example.com/images/queryselectorall-java.png "how to use querySelectorAll in Java")

---

## สิ่งที่คุณต้องการ

| ความต้องการ | ทำไมจึงสำคัญ |
|-------------|----------------|
| **Java 17+** | คุณสมบัติภาษาใหม่และการจัดการโมดูลที่ดีกว่า. |
| **Aspose.HTML for Java** (เวอร์ชันล่าสุด) | ให้คลาส `Document` และเอนจิน CSS‑selector. |
| **catalog.html** (HTML ตัวอย่าง) | แหล่งข้อมูลที่เราจะทำการ query. |
| **IDE หรือ `javac` ธรรมดา** | เพื่อคอมไพล์และรันเดโม. |

ถ้าคุณยังไม่ได้เพิ่ม Aspose.HTML ไปยังโปรเจคของคุณ ให้วางไฟล์ JAR ลงในโฟลเดอร์ `libs` ของคุณและเพิ่มเข้าไปใน classpath:

```bash
javac -cp "libs/*" CssSelectorDemo.java
java -cp ".:libs/*" CssSelectorDemo
```

---

## ขั้นตอนที่ 1 – โหลดเอกสาร HTML

ก่อนที่คุณจะ query อะไรก็ตาม คุณต้องมีอ็อบเจ็กต์ `Document` ที่แทนไฟล์ HTML คิดว่าเหมือนกับการโหลดสเปรดชีตก่อนที่คุณจะอ่านเซลล์ใด ๆ  

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");
```

> **ทำไมจึงสำคัญ:** คลาส `Document` จะทำการพาร์สมาร์คอัปเป็นต้นไม้ DOM ทำให้เอนจิน CSS‑selector ทำงานได้ การข้ามขั้นตอนนี้จะทำให้คุณเหลือเพียงสตริงธรรมดาและไม่มีวิธีใช้ `querySelectorAll`.

---

## ขั้นตอนที่ 2 – เลือกองค์ประกอบด้วย CSS Selector

ตอนนี้เป็นส่วนสำคัญของเรื่อง: **วิธีใช้ querySelectorAll** เมธอดรับ CSS selector ที่ถูกต้องใด ๆ ดังนั้นคุณสามารถกำหนดให้แม่นยำหรือกว้างตามต้องการ สำหรับสถานการณ์ของเราต้องการการ์ดสินค้าที่:

* มีคลาส `product-card`,
* มีคลาส `sale` ด้วย,
* และมีแอตทริบิวต์ `data-price`.

```java
        // Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );
```

> **คำอธิบาย:**  
> > * `.product-card.sale` → กรององค์ประกอบที่มี **ทั้งสอง** คลาส.  
> > * `[data-price]` → ตรวจสอบว่าแอตทริบิวต์มีอยู่ ทำให้ **กรององค์ประกอบตามคลาส** **และ** แอตทริบิวต์ในหนึ่งการเรียก.  
> > * ผลลัพธ์คือ `NodeList` ซึ่งเป็นคอลเลกชันที่เรียงลำดับและคุณสามารถวนลูปได้.

หากคุณต้องการ **select elements css selector** สำหรับรูปแบบอื่น เพียงเปลี่ยนสตริง—ไม่ต้องเขียนโค้ดใหม่

---

## ขั้นตอนที่ 3 – วนลูป NodeList ใน Java

`NodeList` ทำงานคล้ายอาเรย์ แต่ไม่ได้ implement `Iterable` นั่นคือเหตุผลที่เราใช้ `for` loop แบบคลาสสิก—เหมาะสำหรับสถานการณ์ **iterate nodelist java**  

```java
        // Iterate over the selected elements
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
```

> **ทำไมต้องใช้ `for` loop?**  
> > มันให้คุณเข้าถึงดัชนีโดยตรง ซึ่งอาจเป็นประโยชน์สำหรับการบันทึกหรือการแยกสาขาเงื่อนไข หากคุณชอบ `while` loop โลจิกก็ยังคงเหมือนเดิม—เพียงเปลี่ยนโครงสร้างลูป

---

## ขั้นตอนที่ 4 – อ่านแอตทริบิวต์ `data-price`

ตอนนี้เราตอบ **วิธีอ่านแอตทริบิวต์** จากองค์ประกอบแล้ว ใน DOM API, `getAttribute` จะคืนสตริงดิบตามที่ปรากฏในมาร์คอัป  

```java
            // Read the price value from the data-price attribute
            String priceValue = productElement.getAttribute("data-price");
```

> **เคล็ดลับ:** หากแอตทริบิวต์อาจหายไป `getAttribute` จะคืนค่า `null`. คุณสามารถป้องกันได้ด้วยการตรวจสอบง่าย ๆ:  

```java
            if (priceValue == null) {
                priceValue = "N/A"; // fallback for missing data-price
            }
```

---

## ขั้นตอนที่ 5 – แสดงผลลัพธ์

สุดท้ายแต่ไม่ท้ายสุด เราจะแสดงราคาทุกค่าออกที่คอนโซล ซึ่งสอดคล้องกับสถานการณ์จริงที่คุณอาจส่งค่าลงฐานข้อมูลหรือเป็น payload ของ API  

```java
            // Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

### ผลลัพธ์ที่คาดหวังในคอนโซล

```
Sale item price: 19.99
Sale item price: 34.50
Sale item price: 12.00
```

หาก selector ไม่พบโหนดที่ตรงกัน ลูปจะไม่ทำงานเลย—ไม่มีข้อยกเว้นถูกโยน นี่เป็นการป้องกันที่ดีสำหรับ **edge cases** ที่แคตาล็อกอาจว่างเปล่า

---

## ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือไฟล์เต็มที่คุณสามารถคัดลอก‑วางลงใน `CssSelectorDemo.java`:

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");

        // Step 2: Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );

        // Step 3 & 4: Iterate over the selected elements and read the price attribute
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
            String priceValue = productElement.getAttribute("data-price");
            if (priceValue == null) {
                priceValue = "N/A"; // fallback if attribute is missing
            }

            // Step 5: Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

บันทึกไฟล์ คอมไพล์ และรัน—ดูราคาที่ไหลออกมา 🎉

---

## คำถามทั่วไป & เคล็ดลับระดับมืออาชีพ

| คำถาม | คำตอบ |
|----------|--------|
| *ถ้าฉันต้องการเลือกตามชื่อแท็กด้วยล่ะ?* | เพียงใส่แท็กไว้หน้าสำหรับ: `document.querySelectorAll("div.product-card.sale[data-price]")`. |
| *ฉันสามารถเชื่อมต่อหลายตัวกรองแอตทริบิวต์ได้หรือไม่?* | ได้เลย ตัวอย่าง: `[data-price][data-stock]` จะเก็บเฉพาะองค์ประกอบที่มี **ทั้งสอง** แอตทริบิวต์. |
| *`querySelectorAll` แยกแยะตัวพิมพ์ใหญ่‑เล็กหรือไม่?* | ใช่—CSS selector จะพิจารณาชื่อคลาสและแอตทริบิวต์เป็น case‑sensitive ใน HTML5. |
| *ฉันจะจัดการไฟล์ HTML ขนาดใหญ่ได้อย่างไร?* | Aspose.HTML สตรีมเอกสาร แต่คุณยังสามารถจำกัด selector ไปยัง subtree (`someElement.querySelectorAll(...)`). |
| *What

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}