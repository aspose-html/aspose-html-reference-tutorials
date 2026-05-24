---
category: general
date: 2026-02-16
description: Cách tải HTML trong Java, đặt DPI thiết bị, xác định kích thước màn hình
  ảo và đọc màu nền đã tính toán của bất kỳ phần tử nào.
draft: false
keywords:
- how to load html
- read background color
- set device dpi
- set virtual screen size
- get computed background color
language: vi
og_description: Cách tải HTML trong Java, thiết lập DPI thiết bị, định nghĩa kích
  thước màn hình ảo và đọc màu nền đã tính toán của bất kỳ phần tử nào.
og_title: Cách tải HTML, đặt DPI thiết bị và đọc màu nền
tags:
- Aspose.HTML
- Java
title: Cách tải HTML, thiết lập DPI thiết bị và đọc màu nền
url: /vi/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/
---

markdown.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tải HTML, đặt DPI thiết bị & đọc màu nền

Bạn đã bao giờ tự hỏi **cách tải html** trong một ứng dụng Java và sau đó kiểm tra các kiểu của trang chưa? Bạn không phải là người duy nhất—các nhà phát triển thường cần render một trang web ngoài màn hình, lấy các giá trị CSS cuối cùng, và sử dụng chúng cho việc chuyển đổi PDF, chụp màn hình, hoặc thậm chí các bài kiểm tra tự động.  

Trong hướng dẫn này, chúng tôi sẽ đi qua từng bước: tải một tệp HTML, **đặt DPI thiết bị**, xác định **kích thước màn hình ảo**, và cuối cùng **đọc màu nền** từ phần tử `<body>`. Khi kết thúc, bạn sẽ có một đoạn mã có thể chạy được hoàn toàn, in ra **màu nền đã tính toán**—không có gì bí ẩn, chỉ là Java thuần.

## Những gì bạn cần

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* Java 17 hoặc mới hơn (mã hoạt động với bất kỳ JDK hiện đại nào).  
* Aspose.HTML for Java 23.9 hoặc mới hơn—tải JAR từ trang Aspose hoặc thêm qua Maven.  
* Một tệp HTML đơn giản (ví dụ, `responsive.html`) định nghĩa màu nền trong CSS.

Chỉ vậy thôi—không cần framework bổ sung, không cần driver trình duyệt. Sẵn sàng? Hãy bắt đầu.

![Sơ đồ minh họa cách tải html](/images/load-html-diagram.png){alt="Sơ đồ minh họa cách tải html"}

## Bước 1: Cách tải HTML và cấu hình tùy chọn render

Điều đầu tiên bạn làm là tạo một đối tượng `HtmlLoadOptions`. Đối tượng này cho Aspose.HTML biết **cách tải html**—bao gồm kích thước màn hình ảo và DPI bạn muốn mô phỏng.

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create load options and define the virtual screen size and DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        // setVirtualScreenSize – width × height in CSS pixels
        loadOptions.setScreenSize(new Size(1280, 800));
        // setDeviceDpi – typical desktop DPI (96 is the default for most monitors)
        loadOptions.setDeviceDpi(96);
```

**Tại sao điều này quan trọng:**  
Đặt kích thước màn hình ảo đảm bảo các media query như `@media (max-width: 600px)` hoạt động như thể trang được render trên một màn hình thực. DPI ảnh hưởng đến cách các đơn vị CSS `px` được ánh xạ tới pixel vật lý—rất quan trọng khi bạn sau này tạo hình ảnh hoặc PDF.

## Bước 2: Tải tệp HTML bằng các tùy chọn đã cấu hình

Bây giờ chúng ta thực sự tải tệp. Lưu ý chúng ta truyền cùng một `loadOptions` vừa cấu hình.

```java
        // 2️⃣ Load the HTML file with the options we just set.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);
```

Nếu tệp không được tìm thấy, Aspose sẽ ném ra một `FileNotFoundException` rõ ràng. Trong môi trường production, bạn có thể muốn bọc nó trong try‑catch và sử dụng một chuỗi HTML mặc định.

## Bước 3: Đặt kích thước màn hình ảo và DPI thiết bị (một cách rõ ràng)

Mặc dù chúng ta đã gọi `setScreenSize` và `setDeviceDpi` ở trên, nhưng cần nhấn mạnh rằng **đặt kích thước màn hình ảo** và **đặt DPI thiết bị** có thể được điều chỉnh bất kỳ lúc nào trước khi render. Ví dụ, bạn có thể tăng DPI cho ảnh chụp màn hình độ phân giải cao:

```java
        // 3️⃣ Adjust DPI for a high‑resolution render (optional).
        loadOptions.setDeviceDpi(300);   // 300 DPI is common for print‑ready images
        // 4️⃣ Change screen size for a mobile layout test.
        loadOptions.setScreenSize(new Size(375, 667)); // iPhone X viewport
```

Hãy nhớ tải lại tài liệu nếu bạn thay đổi các thiết lập này sau lần tải đầu tiên—Aspose coi chúng là bất biến sau khi `Document` được tạo.

## Bước 4: Đọc màu nền và lấy màu nền đã tính toán

Với tài liệu trong bộ nhớ, bạn có thể truy vấn kiểu đã tính toán của bất kỳ phần tử nào. Ở đây chúng ta tập trung vào thẻ `<body>`, nhưng cách tiếp cận này cũng áp dụng cho `<div>`, `<p>`, hoặc thậm chí các pseudo‑element.

```java
        // 5️⃣ Retrieve the <body> element.
        Element bodyElement = document.getBody();

        // 6️⃣ Output the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

**Bạn sẽ thấy:** Nếu `responsive.html` chứa `body { background: #ff5722; }`, console sẽ in ra một thứ gì đó như:

```
Computed background color: rgba(255,87,34,1)
```

Đó là kết quả **lấy màu nền đã tính toán**—Aspose giải quyết tất cả các quy tắc cascade CSS, media queries, và thậm chí các khai báo `!important` trước khi trả về giá trị cuối cùng.

## Ví dụ hoàn chỉnh hoạt động

Kết hợp tất cả lại, đây là chương trình đầy đủ, sẵn sàng sao chép và dán:

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create load options – virtual screen size + DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        loadOptions.setScreenSize(new Size(1280, 800)); // set virtual screen size
        loadOptions.setDeviceDpi(96);                  // set device DPI (default desktop)

        // Optional: tweak for high‑resolution or mobile rendering.
        // loadOptions.setDeviceDpi(300);
        // loadOptions.setScreenSize(new Size(375, 667));

        // Step 2: Load the HTML document with the options.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);

        // Step 3: Grab the <body> element.
        Element bodyElement = document.getBody();

        // Step 4: Print the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

### Kết quả mong đợi

```
Computed background color: rgba(255,255,255,1)
```

*(Các giá trị RGBA cụ thể phụ thuộc vào CSS trong tệp HTML của bạn.)*

## Những cạm bẫy thường gặp & Mẹo chuyên nghiệp

* **Thiếu thiết lập DPI?** Aspose mặc định là 96 DPI, có thể làm mờ ảnh chụp màn hình độ phân giải cao. Luôn đặt DPI một cách rõ ràng nếu bạn cần đầu ra sắc nét.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}