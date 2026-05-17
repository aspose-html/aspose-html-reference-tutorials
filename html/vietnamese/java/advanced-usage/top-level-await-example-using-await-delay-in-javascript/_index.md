---
category: general
date: 2026-03-26
description: Ví dụ top-level await hiển thị await delay trong JavaScript, lớp tăng
  bộ đếm và các trường công khai của lớp trong JavaScript trong một bản demo trực
  tiếp.
draft: false
keywords:
- top level await example
- await delay javascript
- increment counter class
- public class fields javascript
- javascript class public field
language: vi
og_description: Ví dụ top-level await minh họa await delay trong JavaScript, lớp tăng
  bộ đếm và các trường công khai của lớp trong JavaScript trong một hướng dẫn ngắn
  gọn.
og_title: Ví dụ về top-level await – Sử dụng await delay trong JavaScript
tags:
- JavaScript
- ES2022
- async‑await
- classes
title: Ví dụ về top-level await – Sử dụng await delay trong JavaScript
url: /vi/java/advanced-usage/top-level-await-example-using-await-delay-in-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ví dụ top level await – Sử dụng await delay trong JavaScript

Bạn đã bao giờ tự hỏi làm sao tạm dừng việc thực thi module mà không cần bọc mọi thứ trong một async IIFE? Đó chính là những gì một **ví dụ top level await** cho phép bạn làm. Trong hướng dẫn này chúng ta sẽ đi qua một trang web nhỏ sử dụng `await delay javascript` để hoãn công việc, sau đó tạo một `increment counter class` tận dụng **public class fields javascript**. Khi kết thúc, bạn sẽ có một đoạn mã hoàn chỉnh, có thể sao chép‑dán và chạy trên bất kỳ trình duyệt hiện đại nào.

Chúng ta sẽ bao phủ mọi thứ từ việc định nghĩa một lớp với trường công khai đến việc kết nối một helper delay dựa trên promise. Không có thư viện bên ngoài, không có bước build—chỉ HTML thuần, một `<script type="module">`, và các tính năng ECMAScript mới nhất. Nếu bạn đã quen với các hàm async, bạn sẽ thấy tại sao top‑level await cảm giác như một mở rộng tự nhiên. Nếu bạn mới với cú pháp **javascript class public field**, đừng lo—chúng tôi sẽ giải thích lý do đằng sau mỗi dòng.

## Những gì bạn sẽ học

- Cách một **ví dụ top level await** hoạt động bên trong một module script.
- Mẫu cho một helper `await delay javascript` mô phỏng `setTimeout` bằng promises.
- Cách viết một **increment counter class** sử dụng trường công khai (`count`) và một static initialization block.
- Đầu ra console dự kiến và cách xác minh rằng static block được thực thi trước phần còn lại của script.
- Mẹo khắc phục các vấn đề thường gặp, chẳng hạn như các trình duyệt cũ không hỗ trợ top‑level await.

> **Mẹo chuyên nghiệp:** Các trình duyệt hiện đại (Chrome 106+, Firefox 102+, Edge 106+) đã hỗ trợ top‑level await. Nếu bạn cần hỗ trợ môi trường cũ hơn, hãy cân nhắc bundle bằng công cụ như Vite hoặc Babel.

## Bước 1 – Định nghĩa một lớp với trường công khai và một static block

Phần đầu tiên của demo là một lớp lưu trữ một bộ đếm số. Hãy chú ý dòng `count = 0;`—đây là cú pháp **public class fields javascript** được giới thiệu trong ES2022. Nó tạo một thuộc tính instance mà không cần constructor.

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

**Tại sao lại dùng static block?** Nó cho phép chúng ta chạy một đoạn khởi tạo một lần (như logging) ngay khi module được phân tích, *trước* khi bất kỳ top‑level await nào chạy. Điều này đảm bảo thông điệp xuất hiện đầu tiên trong console, chứng minh lớp đã được đánh giá sớm.

## Bước 2 – Tạo một helper `await delay javascript`

Tiếp theo chúng ta cần một hàm delay dựa trên promise nhỏ gọn. Nó thực chất là một wrapper quanh `setTimeout`, nhưng trả về một promise để có thể await được.

```javascript
    // Step 2: Promise‑based delay helper
    const delay = ms => new Promise(resolve => setTimeout(resolve, ms));
```

**Trường hợp đặc biệt:** Nếu `ms` là số âm hoặc không phải là số, `setTimeout` sẽ coi nó là `0`. Bạn có thể thêm validation, nhưng trong demo một dòng ngắn gọn giữ cho mã dễ đọc hơn.

## Bước 3 – Sử dụng Top‑Level Await để tạm dừng thực thi

Bây giờ là phần nổi bật: top‑level await. Vì script của chúng ta là một module (`type="module"`), chúng ta có thể đặt `await` trực tiếp ở phạm vi trên cùng. Điều này tạm dừng module cho đến khi promise được giải quyết, cho phép chúng ta kiểm soát thứ tự các side effect.

```javascript
    // Step 3: Top‑level await – delay half a second
    await delay(500);   // Wait 500 ms so the static block logs first
```

**Câu hỏi thường gặp:** “Có thể dùng top‑level await trong thẻ `<script>` bình thường không?” Không—chỉ các module script mới hỗ trợ. Nếu bạn quên `type="module"`, sẽ nhận được lỗi cú pháp.

## Bước 4 – Tạo thể hiện của lớp, tăng giá trị, và ghi log kết quả

Cuối cùng chúng ta ghép mọi thứ lại: tạo một instance, gọi `increment()`, và xuất ra giá trị đếm cuối cùng. Điều này minh họa **increment counter class** đang hoạt động.

```javascript
    // Step 4: Work with the Counter instance
    const counterInstance = new Counter();
    counterInstance.increment();               // count becomes 1
    console.log('Final count:', counterInstance.count);
</script>
</body>
</html>
```

### Đầu ra Console Dự kiến

```
Counter class initialized
Final count: 1
```

Nếu bạn mở trang trong DevTools, bạn sẽ thấy thông điệp static‑block xuất hiện **trước** khi delay kết thúc, xác nhận rằng lớp đã được đánh giá trước.

## Bước 5 – Tại sao dùng Public Class Fields thay vì Constructor?

Bạn có thể tự hỏi tại sao chúng ta không viết:

```javascript
class Counter {
    constructor() {
        this.count = 0;
    }
}
```

Cả hai cách đều hoạt động, nhưng **public class fields javascript** cho bạn một cú pháp sạch hơn, khai báo một cách rõ ràng. Trường được định nghĩa một lần, không nằm trong mỗi lần gọi constructor, điều này dễ đọc hơn khi lớp trở nên phức tạp. Thêm nữa, static block không thể đặt bên trong constructor, vì vậy việc tách logic khởi tạo trở nên tự nhiên hơn.

## Bước 6 – Điều chỉnh ví dụ cho các ứng dụng thực tế

Trong môi trường production, bạn thường cần hơn một bộ đếm duy nhất. Dưới đây là một vài ý tưởng nhanh:

- **Nhiều bộ đếm:** Lưu chúng trong một `Map` với key là định danh.
- **Trạng thái persist:** Thay `console.log` bằng việc ghi vào `localStorage`.
- **Khởi tạo async:** Dùng static block để fetch cấu hình từ server trước khi tạo bất kỳ instance nào.

Tất cả các mẫu này vẫn hưởng lợi từ top‑level await, vì bạn có thể fetch dữ liệu một lần khi module được tải và đảm bảo nó sẵn sàng cho mọi consumer.

## Câu hỏi thường gặp

**Hỏi: Top‑level await có chặn các module khác không?**  
Đáp: Không. Mỗi module chạy độc lập. Chỉ module chứa await bị tạm dừng; các module khác vẫn tiếp tục tải song song.

**Hỏi: Nếu promise delay bị reject thì sao?**  
Đáp: Một rejection không được xử lý sẽ làm abort quá trình đánh giá module và hiện ra lỗi trong console. Hãy bọc await trong `try…catch` nếu bạn cần fallback mềm mại.

**Hỏi: Từ khóa `static` có bắt buộc không?**  
Đáp: Không đối với bộ đếm tự thân, nhưng static block là cách tiện lợi để minh họa rằng code chạy *một lần* khi load—rất hữu ích cho logging hoặc detection tính năng.

## Kết luận

Bạn vừa xây dựng một **ví dụ top level await** thể hiện `await delay javascript`, một **increment counter class**, và sức mạnh của **public class fields javascript**. Đoạn mã hoàn chỉnh, có thể chạy ngay ở trên đã được cung cấp, và đầu ra console chứng minh static block được thực thi trước code delay.  

Từ đây, bạn có thể thử nghiệm các luồng async phức tạp hơn, thay thế delay bằng một cuộc gọi API thực, hoặc mở rộng lớp với các phương thức bổ sung. Hãy nhớ, JavaScript hiện đại cho phép bạn xem các module như những thực thể async cấp cao—không cần wrapper thêm.

Chúc bạn coding vui vẻ, và đừng ngại chia sẻ các biến thể của bạn trong phần bình luận. Nếu bạn thấy hướng dẫn này hữu ích, hãy chia sẻ với đồng nghiệp đang vật lộn với các mẫu async!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}