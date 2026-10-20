---
category: general
date: 2026-04-23
description: Cách sử dụng querySelectorAll trong Java để lọc các phần tử theo lớp,
  đọc giá trị thuộc tính và duyệt NodeList để trích xuất dữ liệu sản phẩm.
draft: false
keywords:
- how to use queryselectorall
- how to read attribute
- iterate nodelist java
- filter elements by class
- select elements css selector
language: vi
og_description: Cách sử dụng querySelectorAll trong Java để lọc phần tử theo lớp,
  đọc giá trị thuộc tính và lặp qua NodeList để trích xuất dữ liệu sản phẩm.
og_title: Cách sử dụng querySelectorAll trong Java – Lọc theo lớp
tags:
- Java
- HTML parsing
- DOM manipulation
title: Cách sử dụng querySelectorAll trong Java – Lọc theo lớp
url: /vi/java/creating-managing-html-documents/how-to-use-queryselectorall-in-java-filter-by-class/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng querySelectorAll trong Java – Lọc Theo Lớp

Cách sử dụng querySelectorAll trong Java là chìa khóa khi bạn cần lấy các phần tử cụ thể từ một tài liệu HTML. Trong hướng dẫn này, chúng ta sẽ lọc các phần tử theo lớp, đọc giá trị thuộc tính và duyệt một NodeList để lấy giá sản phẩm từ trang danh mục.  

Bạn đã bao giờ nhìn chằm chằm vào một tệp HTML khổng lồ, tự hỏi làm sao lấy chỉ những thẻ “on‑sale” mà không cần viết trình phân tích tùy chỉnh? Đó chính là vấn đề chúng ta sẽ giải quyết ở đây—không cần thư viện bổ sung nào ngoài Aspose.HTML, và chỉ vài bước đơn giản.

Bạn sẽ có một chương trình hoàn chỉnh, có thể chạy được, với các khả năng:

* **Selects elements** using a CSS selector (`select elements css selector`),
* **Filters by class** (`filter elements by class`),
* **Reads a custom attribute** (`how to read attribute`),
* **Iterates the resulting NodeList** (`iterate nodelist java`).

Không cần kinh nghiệm trước với Aspose.HTML—chỉ cần một môi trường Java cơ bản và một tệp HTML để thử nghiệm.

![ví dụ cách sử dụng querySelectorAll trong Java](https://example.com/images/queryselectorall-java.png "cách sử dụng querySelectorAll trong Java")

---

## Những Gì Bạn Cần Chuẩn Bị

| Yêu Cầu | Lý Do Quan Trọng |
|-------------|----------------|
| **Java 17+** | Các tính năng ngôn ngữ hiện đại và quản lý mô-đun tốt hơn. |
| **Aspose.HTML for Java** (phiên bản mới nhất) | Cung cấp lớp `Document` và công cụ chọn CSS. |
| **catalog.html** (HTML mẫu) | Nguồn dữ liệu chúng ta sẽ truy vấn. |
| **IDE hoặc `javac` thuần** | Để biên dịch và chạy bản demo. |

Nếu bạn chưa thêm Aspose.HTML vào dự án, hãy đặt file JAR vào thư mục `libs` và thêm vào classpath:

```bash
javac -cp "libs/*" CssSelectorDemo.java
java -cp ".:libs/*" CssSelectorDemo
```

---

## Bước 1 – Tải Tài Liệu HTML

Trước khi có thể truy vấn bất kỳ thứ gì, bạn cần một đối tượng `Document` đại diện cho tệp HTML. Hãy nghĩ nó như việc tải một bảng tính trước khi bạn có thể đọc bất kỳ ô nào.

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");
```

> **Tại sao điều này quan trọng:** Lớp `Document` phân tích markup thành cây DOM, cho phép công cụ chọn CSS hoạt động. Bỏ qua bước này sẽ chỉ còn lại một chuỗi thuần và không thể sử dụng `querySelectorAll`.

---

## Bước 2 – Chọn Các Phần Tử Bằng CSS Selector

Bây giờ là phần cốt lõi: **cách sử dụng querySelectorAll**. Phương thức chấp nhận bất kỳ selector CSS hợp lệ nào, vì vậy bạn có thể chính xác hoặc rộng rãi tùy ý. Trong trường hợp của chúng ta, chúng ta muốn các thẻ sản phẩm đáp ứng:

* có lớp `product-card`,
* cũng được đánh dấu bằng lớp `sale`,
* và có thuộc tính `data-price`.

```java
        // Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );
```

> **Giải thích:**  
> * `.product-card.sale` → lọc các phần tử chứa **cả** hai lớp.  
> * `[data-price]` → đảm bảo thuộc tính tồn tại, thực tế **lọc phần tử theo lớp** **và** thuộc tính trong một lần gọi.  
> * Kết quả là một `NodeList`, một tập hợp có thứ tự mà bạn có thể duyệt.  

Nếu bạn cần **select elements css selector** cho một mẫu khác, chỉ cần thay đổi chuỗi—không cần viết lại mã.

---

## Bước 3 – Duyệt NodeList Trong Java

`NodeList` hoạt động giống như một mảng, nhưng không triển khai `Iterable`. Vì vậy chúng ta dùng vòng lặp `for` cổ điển—phù hợp cho các trường hợp **iterate nodelist java**.

```java
        // Iterate over the selected elements
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
```

> **Tại sao dùng vòng `for`?**  
> Nó cho phép truy cập trực tiếp vào chỉ mục, hữu ích cho việc ghi log hoặc nhánh điều kiện. Nếu bạn thích vòng `while`, logic vẫn giống nhau—chỉ cần thay đổi cấu trúc vòng lặp.

---

## Bước 4 – Đọc Thuộc Tính `data-price`

Bây giờ chúng ta trả lời **cách đọc attribute** từ một phần tử. Trong DOM API, `getAttribute` trả về chuỗi thô, đúng như trong markup.

```java
            // Read the price value from the data-price attribute
            String priceValue = productElement.getAttribute("data-price");
```

> **Mẹo:** Nếu thuộc tính có thể thiếu, `getAttribute` sẽ trả về `null`. Bạn có thể kiểm tra đơn giản như sau:

```java
            if (priceValue == null) {
                priceValue = "N/A"; // fallback for missing data-price
            }
```

---

## Bước 5 – In Kết Quả

Cuối cùng, chúng ta in mỗi giá lên console. Điều này mô phỏng một kịch bản thực tế, nơi bạn có thể đưa các giá trị vào cơ sở dữ liệu hoặc payload API.

```java
            // Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

### Kết Quả Dự Kiến Trên Console

```
Sale item price: 19.99
Sale item price: 34.50
Sale item price: 12.00
```

Nếu selector không tìm thấy nút nào phù hợp, vòng lặp sẽ không chạy—không có ngoại lệ nào được ném. Đây là một biện pháp an toàn tốt cho **edge cases** khi danh mục có thể rỗng.

---

## Ví Dụ Hoàn Chỉnh

Kết hợp tất cả lại, đây là file hoàn chỉnh bạn có thể sao chép‑dán vào `CssSelectorDemo.java`:

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

Lưu file, biên dịch và chạy—xem các giá xuất hiện liên tục. 🎉

---

## Câu Hỏi Thường Gặp & Mẹo Chuyên Nghiệp

| Câu Hỏi | Trả Lời |
|----------|--------|
| *What if I need to select by tag name too?* | Chỉ cần đặt trước thẻ: `document.querySelectorAll("div.product-card.sale[data-price]")`. |
| *Can I chain multiple attribute filters?* | Chắc chắn. Ví dụ: `[data-price][data-stock]` sẽ giữ lại chỉ những phần tử có **cả** hai thuộc tính. |
| *Is `querySelectorAll` case‑sensitive?* | Có—CSS selectors coi tên lớp và thuộc tính là phân biệt chữ hoa/thường trong HTML5. |
| *How do I handle a huge HTML file?* | Aspose.HTML stream tài liệu, nhưng bạn cũng có thể giới hạn selector vào một subtree (`someElement.querySelectorAll(...)`). |
| *What

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}