---
category: general
date: 2026-06-16
description: Cách sử dụng CSS để tải tệp HTML và đếm liên kết trong Java. Học cách
  đếm các phần tử HTML và đánh giá XPath trong Java qua một ví dụ duy nhất, rõ ràng.
draft: false
keywords:
- how to use css
- load html file
- how to count links
- count html elements
- evaluate xpath java
language: vi
og_description: Cách sử dụng CSS trong Java để tải tệp HTML, đếm liên kết và đánh
  giá các biểu thức XPath—tất cả trong một hướng dẫn thực tế.
og_title: Cách sử dụng CSS trong Java – Tải HTML, Đếm liên kết và Đánh giá XPath
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to use CSS to load HTML file and count links in Java. Learn to
    count html elements and evaluate xpath java in a single, clear example.
  headline: How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath
  type: TechArticle
- description: How to use CSS to load HTML file and count links in Java. Learn to
    count html elements and evaluate xpath java in a single, clear example.
  name: How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath
  steps:
  - name: What if the HTML file is malformed?
    text: Both the CSS and XPath engines are tolerant of minor markup errors (missing
      closing tags, unquoted attributes). However, severe malformations may cause
      the parser to abort. In production, wrap the loading step in a try‑catch block
      and log the exception.
  - name: Can I combine CSS and XPath in a single expression?
    text: Not directly; each engine has its own syntax. The typical pattern is to
      use the one that expresses the condition most naturally (CSS for structural
      queries, XPath for attribute functions) and then merge the results in Java if
      needed.
  - name: How do I count elements across multiple files?
    text: 'Just place the loading logic inside a loop:'
  - name: Does this work with Java 8?
    text: Yes—provided you use a library version that targets Java 8 or higher. The
      code shown does not rely on newer language features.
  type: HowTo
tags:
- Java
- HTML parsing
- CSS selectors
- XPath
title: Cách sử dụng CSS trong Java – Tải HTML, Đếm liên kết và Đánh giá XPath
url: /vi/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng CSS trong Java – Tải HTML, Đếm Liên Kết & Đánh Giá XPath

Bạn đã bao giờ tự hỏi **cách sử dụng CSS** selector khi xử lý một tệp HTML trong Java chưa? Có thể bạn đang xây dựng một web‑crawler, một scraper, hoặc chỉ cần kiểm tra một trang tĩnh. Tin tốt là gì? Bạn không cần phải viết một parser tùy chỉnh từ đầu—các thư viện hiện đại cho phép bạn kết hợp selector CSS4 với biểu thức XPath 3.1 trong một quy trình gọn gàng.

Trong hướng dẫn này, chúng ta sẽ đi qua **cách tải một tệp HTML**, áp dụng selector CSS để đếm các liên kết trong thanh điều hướng, và sau đó **đánh giá XPath** để đếm các phần tử ảnh cụ thể. Khi kết thúc, bạn sẽ có một chương trình hoàn chỉnh, có thể chạy được, in ra số lượng node khớp, và bạn sẽ hiểu tại sao mỗi phần lại quan trọng.

## Yêu Cầu Trước

- Java 17 (hoặc bất kỳ JDK hiện đại nào) đã được cài đặt trên máy của bạn  
- Maven hoặc Gradle để quản lý phụ thuộc (chúng tôi sẽ dùng Maven trong ví dụ)  
- Một đoạn HTML nhỏ được lưu dưới tên `input.html` trong một thư mục bạn kiểm soát  

Không cần công cụ nào khác—chỉ cần một trình soạn thảo văn bản và một terminal.

## Nội Dung Hướng Dẫn

- **Tải một tệp HTML** vào cấu trúc giống DOM bằng lớp *HTMLDocument*  
- Áp dụng **selector CSS4** (`nav a[data-role]`) để tìm các liên kết điều hướng  
- Thực thi **biểu thức XPath 3.1** để tìm các thẻ `<img>` có `src` kết thúc bằng `.png` và cũng có thuộc tính `alt`  
- **Đếm** kết quả của cả hai truy vấn và in chúng ra console  
- Mã nguồn đầy đủ, giải thích “tại sao”, và một cái nhìn nhanh vào các trường hợp biên có thể xảy ra  

Hãy bắt đầu ngay.

---

## Bước 1 – Cách Tải Tệp HTML với HTMLDocument

Trước khi bạn có thể truy vấn bất cứ thứ gì, tài liệu HTML phải được phân tích thành một mô hình có thể duyệt được. Lớp `HTMLDocument` từ thư viện **jsoup‑plus** (hoặc bất kỳ parser HTML‑aware nào tương tự) làm đúng điều này.

```java
import com.example.html.HTMLDocument;
import com.example.html.NodeList;

public class CssXPathDemo {
    public static void main(String[] args) throws Exception {
        // Load the HTML document from the file system
        HTMLDocument doc = new HTMLDocument("YOUR_DIRECTORY/input.html");
        // From here on we can query the DOM using CSS or XPath
```

*Lý do quan trọng:*  
Tải tệp một lần và giữ tham chiếu (`doc`) tránh việc I/O lặp lại, điều này có thể trở thành nút thắt hiệu năng khi xử lý một lượng lớn trang.

---

## Bước 2 – Cách Sử Dụng CSS Để Đếm Liên Kết Trong `<nav>`

Bây giờ tài liệu đã ở trong bộ nhớ, chúng ta có thể dùng selector CSS4 để lấy mọi phần tử `<a>` nằm trong một `<nav>` và cũng có thuộc tính `data‑role`. Đây là mẫu phổ biến cho các menu điều hướng sử dụng thuộc tính dữ liệu làm hook cho JavaScript.

```java
        // Use a CSS4 selector to find every <a> inside a <nav> that has a data‑role attribute
        NodeList navLinks = doc.querySelectorAll("nav a[data-role]");
```

*Giải thích:*  
- `nav a[data-role]` có nghĩa là “bất kỳ phần tử `<a>` nào có thuộc tính `data‑role` và là con cháu của một phần tử `<nav>`.”  
- Selector này tương thích **CSS4**, nghĩa là bạn cũng có thể dùng các pseudo‑class như `:not()` hoặc `:has()` nếu trường hợp sử dụng của bạn mở rộng.

> **Mẹo chuyên nghiệp:** Nếu bạn chỉ cần các phần tử con trực tiếp, thay dấu cách bằng `>` (`nav > a[data-role]`). Điều này giảm không gian tìm kiếm và có thể tăng tốc cho các tài liệu lớn.

---

## Bước 3 – Đánh Giá XPath trong Java Để Đếm Các Phần Tử `<img>` Cụ Thể

XPath tỏa sáng khi bạn cần lọc dựa trên thuộc tính mà CSS không thực hiện được một cách trực quan. Ở đây chúng ta sẽ tìm mọi `<img>` có `src` kết thúc bằng `.png` **và** cũng có thuộc tính `alt`—rất hữu ích cho các cuộc kiểm tra khả năng truy cập.

```java
        // Use an XPath 3.1 expression to locate all <img> elements whose src ends with .png and have an alt attribute
        NodeList pngImages = doc.evaluate("//img[ends-with(@src, '.png') and @alt]");
```

*Lý do dùng XPath?*  
- Hàm `ends-with()` là một phần của XPath 3.1, cho phép khớp hậu tố mà không cần regex.  
- Kết hợp nhiều predicate (`and @alt`) đảm bảo bạn chỉ đếm những ảnh vừa có nguồn đúng vừa được mô tả.

Nếu thư viện của bạn chỉ hỗ trợ XPath 1.0, bạn sẽ phải dùng `contains(@src, '.png')` rồi lọc bằng Java—cách tiếp cận kém chính xác hơn.

---

## Bước 4 – Cách Đếm Các Phần Tử HTML và In Kết Quả

Cuối cùng, chúng ta lấy độ dài của cả hai đối tượng `NodeList` và xuất chúng ra. Đây là phần **cách đếm liên kết** của bài toán, nhưng nó hoạt động với bất kỳ tập hợp node nào.

```java
        // Output the number of matches for each query
        System.out.println("Nav links: " + navLinks.getLength());
        System.out.println("PNG images with alt: " + pngImages.getLength());
    }
}
```

**Kết quả console dự kiến** (giả sử HTML mẫu có 3 liên kết khớp và 2 ảnh khớp):

```
Nav links: 3
PNG images with alt: 2
```

Nếu số đếm bằng 0, hãy kiểm tra lại cú pháp selector hoặc xác nhận rằng `input.html` thực sự chứa các phần tử mong muốn.

---

## Ví Dụ Hoàn Chỉnh

Dưới đây là chương trình đầy đủ, tự chứa, bạn có thể sao chép‑dán vào một tệp tên `CssXPathDemo.java`. Nó bao gồm các import cần thiết, một đoạn `pom.xml` đơn giản cho Maven, và một mẫu HTML tối thiểu để thử nghiệm.

```java
/* CssXPathDemo.java */
import com.example.html.HTMLDocument;
import com.example.html.NodeList;

public class CssXPathDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the HTML document
        HTMLDocument doc = new HTMLDocument("input.html");

        // Step 2: CSS selector – count navigation links with data-role
        NodeList navLinks = doc.querySelectorAll("nav a[data-role]");

        // Step 3: XPath expression – count PNG images that have alt text
        NodeList pngImages = doc.evaluate("//img[ends-with(@src, '.png') and @alt]");

        // Step 4: Print the results
        System.out.println("Nav links: " + navLinks.getLength());
        System.out.println("PNG images with alt: " + pngImages.getLength());
    }
}
```

**Đoạn trích Maven `pom.xml`** (thêm phụ thuộc này để kéo thư viện parser hỗ trợ cả CSS4 và XPath 3.1):

```xml
<dependencies>
    <dependency>
        <groupId>com.example</groupId>
        <artifactId>html-parser-plus</artifactId>
        <version>2.3.1</version>
    </dependency>
</dependencies>
```

**Mẫu `input.html`** (đặt nó trong cùng thư mục với tệp Java):

```html
<!DOCTYPE html>
<html lang="en">
<head><title>Test Page</title></head>
<body>
<nav>
    <a href="/home" data-role="main">Home</a>
    <a href="/about" data-role="secondary">About</a>
    <a href="/contact">Contact</a>
</nav>
<img src="logo.png" alt="Company Logo">
<img src="banner.jpg">
<img src="icon.png" alt="Icon">
</body>
</html>
```

Chạy `mvn compile exec:java -Dexec.mainClass=CssXPathDemo` sẽ cho ra các số đếm như đã mô tả ở trên.

---

## Trường Hợp Biên & Câu Hỏi Thường Gặp

### HTML bị hỏng thì sao?

Cả engine CSS và XPath đều chịu được các lỗi markup nhỏ (thiếu thẻ đóng, thuộc tính không có dấu ngoặc). Tuy nhiên, những lỗi nghiêm trọng có thể làm parser dừng lại. Trong môi trường production, hãy bao bọc bước tải trong khối try‑catch và ghi log ngoại lệ.

### Có thể kết hợp CSS và XPath trong một biểu thức duy nhất không?

Không trực tiếp; mỗi engine có cú pháp riêng. Mô hình thường dùng là chọn engine phù hợp nhất cho điều kiện (CSS cho truy vấn cấu trúc, XPath cho hàm thuộc tính) rồi hợp nhất kết quả trong Java nếu cần.

### Làm sao để đếm phần tử trên nhiều tệp?

Chỉ cần đặt logic tải vào trong một vòng lặp:

```java
for (Path p : Files.newDirectoryStream(Paths.get("html_folder"), "*.html")) {
    HTMLDocument doc = new HTMLDocument(p.toString());
    // repeat the queries...
}
```

### Có hoạt động với Java 8 không?

Có—miễn là bạn dùng phiên bản thư viện hỗ trợ Java 8 trở lên. Đoạn mã ở trên không dựa vào các tính năng ngôn ngữ mới hơn.

---

## Kết Luận

Chúng ta đã chứng minh **cách sử dụng CSS** selector kết hợp với **đánh giá xpath java** để **tải một tệp HTML**, **đếm liên kết**, và **đếm các phần tử HTML** đáp ứng tiêu chí cụ thể. Những điểm chính cần nhớ là:

- Tải tài liệu một lần bằng `HTMLDocument`.  
- Tận dụng CSS4 cho các truy vấn cấu trúc đơn giản (`nav a[data-role]`).  
- Sử dụng XPath 3.1 cho các hàm thuộc tính mạnh mẽ (`ends-with(@src, '.png')`).  
- Lấy độ dài `NodeList` để có số đếm chính xác.  

Từ đây, bạn có thể mở rộng script: thêm nhiều selector, ghi kết quả vào CSV, hoặc tích hợp vào pipeline crawling lớn hơn. Sự kết hợp giữa CSS và XPath mang lại sự linh hoạt để giải quyết hầu hết các thách thức thu thập dữ liệu HTML.

Bạn đã sẵn sàng thử nghiệm? Hãy thay selector CSS bằng `section article[data-id]` hoặc thay đổi XPath để nhắm tới thẻ `<video>` có codec cụ thể. Không giới hạn gì cả.

Nếu bạn thấy hướng dẫn này hữu ích, hãy chia sẻ, star repository, hoặc để lại bình luận với các trường hợp sử dụng của bạn. Chúc lập trình vui vẻ!

![ví dụ cách sử dụng css diagram](https://example.com/diagram.png "ví dụ cách sử dụng css diagram")

---


## Bạn Nên Học Gì Tiếp Theo?


Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên đều có mã nguồn đầy đủ, ví dụ làm việc thực tế và giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách Thêm CSS – CSS Nội Tuyến vào Tài Liệu HTML trong Aspose.HTML cho Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [Cách Chỉnh Sửa CSS - Chỉnh Sửa CSS Ngoại Viên Nâng Cao với Aspose.HTML cho Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)
- [Cách Chỉnh Sửa Cây Tài Liệu HTML trong Aspose.HTML cho Java](/html/english/java/editing-html-documents/edit-html-document-tree/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}