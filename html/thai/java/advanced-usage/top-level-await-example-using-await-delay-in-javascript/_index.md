---
category: general
date: 2026-03-26
description: ตัวอย่าง top‑level await แสดงการใช้ await delay ใน JavaScript, คลาสเพิ่มตัวนับ,
  และฟิลด์สาธารณะของคลาสใน JavaScript ในการสาธิตสด.
draft: false
keywords:
- top level await example
- await delay javascript
- increment counter class
- public class fields javascript
- javascript class public field
language: th
og_description: ตัวอย่าง top‑level await ที่สาธิตการใช้ await delay ใน JavaScript,
  คลาสเพิ่มตัวนับ, และฟิลด์สาธารณะของคลาสใน JavaScript อย่างกระชับ.
og_title: ตัวอย่าง top‑level await – การใช้ await delay ใน JavaScript
tags:
- JavaScript
- ES2022
- async‑await
- classes
title: ตัวอย่าง top‑level await – การใช้ await delay ใน JavaScript
url: /th/java/advanced-usage/top-level-await-example-using-await-delay-in-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตัวอย่าง top level await – การใช้ await delay ใน JavaScript

เคยสงสัยไหมว่าจะหยุดการทำงานของโมดูลโดยไม่ต้องห่อทุกอย่างใน async IIFE? นั่นคือสิ่งที่ **top level await example** ทำให้คุณทำได้ ในบทเรียนนี้เราจะเดินผ่านหน้าเว็บขนาดเล็กที่ใช้ `await delay javascript` เพื่อเลื่อนการทำงาน แล้วสร้าง `increment counter class` ที่ใช้ **public class fields javascript** เมื่อจบคุณจะได้สแนปช็อตที่พร้อมคัดลอก‑วางและทำงานในเบราว์เซอร์สมัยใหม่ใดก็ได้

เราจะครอบคลุมทุกอย่างตั้งแต่การกำหนดคลาสด้วยฟิลด์สาธารณะจนถึงการต่อสายช่วยเหลือ delay แบบ promise ไม่ต้องใช้ไลบรารีภายนอก ไม่ต้องขั้นตอน build—แค่ HTML ธรรมดา, `<script type="module">`, และฟีเจอร์ ECMAScript ล่าสุด หากคุณคุ้นเคยกับ async function อยู่แล้ว คุณจะเห็นว่าทำไม top‑level await ถึงรู้สึกเป็นการต่อขยายที่เป็นธรรมชาติ หากคุณใหม่กับไวยากรณ์ **javascript class public field** อย่ากังวล—เราจะอธิบายเหตุผลของแต่ละบรรทัด

## สิ่งที่คุณจะได้เรียนรู้

- วิธีการทำงานของ **top level await example** ภายในสคริปต์โมดูล
- แพทเทิร์นสำหรับ helper `await delay javascript` ที่จำลอง `setTimeout` ด้วย promise
- วิธีเขียน **increment counter class** ที่ใช้ฟิลด์สาธารณะ (`count`) และ static initialization block
- ผลลัพธ์ที่คาดว่าจะเห็นใน console และวิธีตรวจสอบว่า static block ทำงานก่อนส่วนอื่นของสคริปต์
- เคล็ดลับการแก้ปัญหาข้อผิดพลาดทั่วไป เช่น เบราว์เซอร์เก่าที่ไม่รองรับ top‑level await

> **Pro tip:** เบราว์เซอร์สมัยใหม่ (Chrome 106+, Firefox 102+, Edge 106+) รองรับ top‑level await แล้ว หากต้องการสนับสนุนสภาพแวดล้อมเก่า ให้พิจารณา bundle ด้วยเครื่องมืออย่าง Vite หรือ Babel

## ขั้นตอนที่ 1 – กำหนดคลาสด้วยฟิลด์สาธารณะและ static block

ส่วนแรกของเดโมคือคลาสที่เก็บตัวนับเชิงตัวเลข สังเกตบรรทัด `count = 0;`—นี่คือไวยากรณ์ **public class fields javascript** ที่แนะนำใน ES2022 ซึ่งสร้าง property ของอินสแตนซ์โดยไม่ต้อง constructor

```html
<!DOCTYPE html>
<html>
<head>
    <title>ECMAScript 2022 Demo</title>
</head>
<body>
<img src="placeholder.png" alt="top level await example screenshot" title="top level await example">

<script type="module">
    // Step 1: Class definition
    class Counter {
        // Public field holds the current count
        count = 0;

        // Static block runs once when the class is first evaluated
        static {
            console.log('Counter class initialized');
        }

        // Simple method that increments the public field
        increment() {
            this.count++;
        }
    }
```

**ทำไมต้องใช้ static block?** มันทำให้เรารันโลจิกการเริ่มต้นครั้งเดียว (เช่นการล็อก) ทันทีที่โมดูลถูกพาร์ส, *ก่อน* ที่ top‑level await จะทำงาน สิ่งนี้รับประกันว่าข้อความจะปรากฏเป็นอันดับแรกใน console แสดงว่าคลาสถูกประเมินค่าเร็ว

## ขั้นตอนที่ 2 – สร้าง Helper `await delay javascript`

ต่อไปเราต้องการฟังก์ชัน delay แบบ promise ขนาดเล็ก มันเป็นเพียง wrapper รอบ `setTimeout` แต่การคืนค่าเป็น promise ทำให้สามารถ await ได้

```javascript
    // Step 2: Promise‑based delay helper
    const delay = ms => new Promise(resolve => setTimeout(resolve, ms));
```

**กรณีขอบ:** หาก `ms` เป็นค่าลบหรือไม่ใช่ตัวเลข, `setTimeout` จะถือว่าเป็น `0` คุณอาจเพิ่มการตรวจสอบค่าได้ แต่สำหรับเดโมหนึ่งบรรทัดนี้ทำให้โค้ดอ่านง่าย

## ขั้นตอนที่ 3 – ใช้ Top‑Level Await เพื่อหยุดการทำงาน

ตอนนี้มาถึงจุดเด่นของเรา: top‑level await เนื่องจากสคริปต์ของเราคือโมดูล (`type="module"`), เราสามารถวาง `await` ไตรงระดับบนสุดได้ การทำเช่นนี้จะหยุดโมดูลจนกว่า promise จะ resolve, ทำให้เราควบคุมลำดับของ side effect ได้

```javascript
    // Step 3: Top‑level await – delay half a second
    await delay(500);   // Wait 500 ms so the static block logs first
```

**คำถามที่พบบ่อย:** “สามารถใช้ top‑level await ใน `<script>` ธรรมดาได้ไหม?” ไม่ได้—รองรับเฉพาะสคริปต์โมดูลเท่านั้น หากลืมใส่ `type="module"` จะเจอ syntax error

## ขั้นตอนที่ 4 – สร้างอินสแตนซ์ของคลาส, เพิ่มค่า, และบันทึกผลลัพธ์

สุดท้ายเรานำทุกอย่างมารวมกัน: สร้างอินสแตนซ์, เรียก `increment()`, และแสดงผลลัพธ์สุดท้าย นี่คือการแสดง **increment counter class** ทำงานจริง

```javascript
    // Step 4: Work with the Counter instance
    const counterInstance = new Counter();
    counterInstance.increment();               // count becomes 1
    console.log('Final count:', counterInstance.count);
</script>
</body>
</html>
```

### ผลลัพธ์ที่คาดว่าจะเห็นใน Console

```
Counter class initialized
Final count: 1
```

หากคุณเปิดหน้าใน DevTools คุณควรเห็นข้อความจาก static‑block ปรากฏ **ก่อน** ที่ delay จะเสร็จสิ้น ยืนยันว่าคลาสถูกประเมินค่าแรก

## ขั้นตอนที่ 5 – ทำไมต้องใช้ Public Class Fields แทน Constructor?

คุณอาจสงสัยว่าทำไมเราไม่ได้เขียนแบบนี้:

```javascript
class Counter {
    constructor() {
        this.count = 0;
    }
}
```

ทั้งสองวิธีทำงานได้, แต่ **public class fields javascript** ให้ไวยากรณ์ที่สะอาดและเป็น declarative มากกว่า ฟิลด์ถูกกำหนดเพียงครั้งเดียว ไม่ได้อยู่ในทุกการเรียก constructor ซึ่งทำให้อ่านง่ายเมื่อคลาสขยายใหญ่ขึ้น นอกจากนี้ static block ไม่สามารถวางไว้ใน constructor ได้ จึงทำให้การแยกโลจิกการเริ่มต้นเป็นธรรมชาติมากขึ้น

## ขั้นตอนที่ 6 – ปรับตัวอย่างให้เหมาะกับแอปจริง

ใน production คุณมักต้องการมากกว่าตัวนับเดียว นี่คือไอเดียสั้น ๆ:

- **หลายตัวนับ:** เก็บไว้ใน `Map` ที่ใช้ identifier เป็นคีย์
- **สถานะคงที่:** แทนที่ `console.log` ด้วยการเขียนลง `localStorage`
- **การเริ่มต้นแบบ async:** ใช้ static block เพื่อดึง configuration จากเซิร์ฟเวอร์ก่อนสร้างอินสแตนซ์ใด ๆ

รูปแบบทั้งหมดนี้ยังคงได้ประโยชน์จาก top‑level await เพราะคุณสามารถดึงข้อมูลครั้งเดียวเมื่อโมดูลโหลดและรับประกันว่าพร้อมใช้งานสำหรับทุก consumer

## คำถามที่พบบ่อย

**Q: top‑level await ทำให้โมดูลอื่นหยุดทำงานหรือไม่?**  
A: ไม่ โมดูลแต่ละตัวทำงานอิสระ โมดูลที่มี await จะหยุดเท่านั้น โมดูลอื่นยังคงโหลดพร้อมกัน

**Q: ถ้า promise ของ delay ปฏิเสธจะเกิดอะไรขึ้น?**  
A: การปฏิเสธที่ไม่ได้จัดการจะทำให้การประเมินโมดูลหยุดและแสดง error ใน console ให้ใส่ `try…catch` รอบ await หากต้องการ fallback ที่นุ่มนวล

**Q: คีย์เวิร์ด `static` จำเป็นหรือไม่?**  
A: ไม่จำเป็นสำหรับตัวนับเอง, แต่ static block เป็นวิธีที่สะดวกเพื่อแสดงว่าโค้ดทำงาน *ครั้งเดียว* ตอนโหลด—เหมาะสำหรับการล็อกหรือการตรวจจับฟีเจอร์

## สรุป

คุณเพิ่งสร้าง **top level await example** ที่แสดง `await delay javascript`, **increment counter class**, และพลังของ **public class fields javascript** สแนปช็อตที่ทำงานได้เต็มรูปแบบอยู่ด้านบน และผลลัพธ์ใน console ยืนยันว่า static block ทำงานก่อนโค้ดที่ล่าช้า

จากนี้คุณสามารถทดลองกับ flow async ที่ซับซ้อนขึ้น, เปลี่ยน delay ให้เป็นการเรียก API จริง, หรือขยายคลาสด้วยเมธอดเพิ่มเติม จำไว้ว่า JavaScript สมัยใหม่ทำให้โมดูลเป็น async entity ชั้นแรก—ไม่ต้องห่อเพิ่มเติม

ขอให้สนุกกับการโค้ด, และอย่าลืมแชร์เวอร์ชันของคุณในคอมเมนต์ หากบทความนี้เป็นประโยชน์, แชร์ให้เพื่อนร่วมทีมที่ยังต่อสู้กับ async pattern กันอยู่!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}