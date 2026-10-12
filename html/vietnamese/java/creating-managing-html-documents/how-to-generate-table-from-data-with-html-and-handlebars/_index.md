---
category: general
date: 2026-10-12
description: Học cách tạo bảng từ dữ liệu và điền dữ liệu vào bảng từ JSON bằng Handlebars.
  Hướng dẫn từng bước để lặp lại các hàng bảng trong các bảng HTML động.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate table from data
- populate table from json
- repeat table rows
- dynamic html table
- dynamic table rows
language: vi
lastmod: 2026-10-12
og_description: Tạo bảng từ dữ liệu và điền dữ liệu vào bảng từ JSON bằng Handlebars.
  Hãy làm theo hướng dẫn này để tạo các bảng HTML động với các hàng lặp lại.
og_image_alt: Screenshot showing generated table from data in a web page
og_title: Tạo bảng từ dữ liệu bằng Handlebars – hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-10-12'
  description: Learn how to generate table from data and populate table from JSON
    using Handlebars. Step‑by‑step guide for repeat table rows in dynamic HTML tables.
  headline: How to generate table from data with HTML and Handlebars
  type: TechArticle
- description: Learn how to generate table from data and populate table from JSON
    using Handlebars. Step‑by‑step guide for repeat table rows in dynamic HTML tables.
  name: How to generate table from data with HTML and Handlebars
  steps:
  - name: 1. Empty data sets
    text: 'If the JSON array is empty, Handlebars will still render the header row
      but no data rows. To display a friendly message, wrap the table in a conditional
      block:'
  - name: 2. Nested loops (e.g., multiple addresses per person)
    text: 'When a person can have several addresses, you can nest another `{{#foreach}}`
      inside the row:'
  - name: 3. Using a real API
    text: 'Replace the static `<script id="people-data">` with a fetch call:'
  - name: 4. Accessibility considerations
    text: '* Add `scope="col"` to `<th>` elements. * Use `<caption>` to describe the
      table purpose. * Ensure sufficient color contrast if you apply custom CSS.'
  type: HowTo
tags:
- HTML
- Handlebars
- JSON
- templating
title: Cách tạo bảng từ dữ liệu bằng HTML và Handlebars
url: /vi/java/creating-managing-html-documents/how-to-generate-table-from-data-with-html-and-handlebars/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo bảng từ dữ liệu bằng HTML và Handlebars

Nếu bạn cần **generate table from data** trong một trang web, hướng dẫn này sẽ chỉ cho bạn cách thực hiện. Bằng cách sử dụng một vòng lặp Handlebars đơn giản, bạn có thể **populate table from JSON**, tạo **repeat table rows**, và có được một **dynamic HTML table** hoàn toàn, cập nhật mỗi khi nguồn dữ liệu thay đổi.

Trong vài phút tới, bạn sẽ thấy một ví dụ đầy đủ, có thể chạy được, hiểu tại sao mỗi phần lại quan trọng, và học cách điều chỉnh mẫu cho các kịch bản phức tạp hơn như cột có điều kiện hoặc đối tượng lồng nhau.

## Những gì bạn sẽ xây dựng

* Đọc một payload JSON chứa danh sách các cá nhân.
* Lặp lại một hàng bảng cho mỗi người (`repeat table rows`).
* Chèn tên, họ và địa chỉ của mỗi người vào các ô tương ứng.
* Hoạt động mà không cần render phía máy chủ – toàn bộ quá trình diễn ra trong trình duyệt.

**Prerequisites**

* Kiến thức cơ bản về HTML và JavaScript.
* Trình duyệt hiện đại (Chrome, Edge, Firefox hoặc Safari).
* Handlebars.js – chúng tôi sẽ tải nó từ CDN, vì vậy không cần công cụ xây dựng.

---

## Bước 1: Chuẩn bị nguồn dữ liệu JSON

Bước đầu tiên là định nghĩa một đối tượng JavaScript mô phỏng JSON bạn sẽ nhận được từ một API. Handlebars làm việc với các đối tượng đơn giản, vì vậy bạn có thể nhúng dữ liệu trực tiếp trong thẻ `<script>` để minh họa.

```html
<script id="people-data" type="application/json">
{
  "Persons": {
    "Person": [
      {
        "FirstName": "Alice",
        "LastName": "Anderson",
        "Address": {
          "Street": "Maple",
          "Number": "123",
          "City": "Springfield"
        }
      },
      {
        "FirstName": "Bob",
        "LastName": "Baker",
        "Address": {
          "Street": "Oak",
          "Number": "456",
          "City": "Rivertown"
        }
      }
    ]
  }
}
</script>
```

**Why this matters** – Bằng cách giữ dữ liệu trong một phần tử `<script>` riêng, bạn có thể dễ dàng thay thế bằng một cuộc gọi AJAX thực tế sau này. Cấu trúc (`Persons.Person`) khớp với đường dẫn được sử dụng trong khối Handlebars `{{#foreach Persons.Person}}`, điều này rất quan trọng cho **populate table from JSON**.

---

## Bước 2: Viết mẫu Handlebars để lặp lại các hàng

Tiếp theo, tạo một khối `<script type="text/x-handlebars-template">` chứa mã HTML của bảng. Handlebars sẽ thay thế các placeholder bằng giá trị thực và lặp lại `<tr>` cho mỗi người.

```html
<script id="table-template" type="text/x-handlebars-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <!-- Header row describing the columns -->
  <tr>
    <th>Person</th>
    <th>Address</th>
  </tr>
  <!-- Data row – this block is repeated for each Person -->
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
</table>
</script>
```

**Giải thích các phần chính**

* `{{#foreach Persons.Person}}` cho Handlebars biết **repeat table rows** cho mỗi mục trong mảng `Persons.Person`.
* Các biểu thức `{{FirstName}} {{LastName}}` và `{{Address.*}}` lấy giá trị từ phần tử hiện tại của mảng.
* Việc bao quanh toàn bộ bảng bằng thuộc tính `data_merge` là tùy chọn; nó có thể hữu ích cho việc xử lý downstream hoặc các selector CSS.

---

## Bước 3: Tải Handlebars và biên dịch mẫu

Chúng tôi sẽ tải Handlebars từ CDN, phân tích JSON, biên dịch mẫu và chèn HTML cuối cùng vào trang.

```html
<script src="https://cdn.jsdelivr.net/npm/handlebars@4.7.7/dist/handlebars.min.js"></script>
<script>
  // Parse the JSON stored in the <script id="people-data">
  const rawData = document.getElementById('people-data').textContent;
  const context = JSON.parse(rawData);

  // Grab the template markup and compile it
  const source = document.getElementById('table-template').innerHTML;
  const template = Handlebars.compile(source);

  // Generate the final HTML by applying the context
  const html = template(context);

  // Insert the generated table into the DOM
  document.getElementById('output').innerHTML = html;
</script>
```

**Why compile at runtime?** – Việc biên dịch mẫu một lần và tái sử dụng nó giúp trang chạy nhanh, đặc biệt khi dữ liệu thay đổi thường xuyên. Mẫu này cũng làm cho việc **populate table from JSON** nhiều lần trở nên đơn giản mà không cần tải lại trang.

---

## Bước 4: Dự trữ một container cho bảng được tạo

Thêm một `<div>` placeholder nơi bảng động sẽ xuất hiện. Điều này giữ cho markup sạch sẽ và tách biệt các mối quan tâm giữa bố cục tĩnh và nội dung được tạo.

```html
<div id="output"></div>
```

Khi script từ Bước 3 chạy, `<div id="output">` sẽ chứa một phần tử `<table>` hoàn chỉnh, sẵn sàng để định dạng hoặc thao tác tiếp theo.

---

## Bước 5: Kiểm tra kết quả và định dạng bảng (tùy chọn)

Mở trang trong trình duyệt và bạn sẽ thấy một bảng giống như hình dưới:

![Ảnh chụp màn hình hiển thị bảng được tạo từ dữ liệu](image.png "Ảnh chụp màn hình hiển thị bảng được tạo từ dữ liệu")

```html
<table border="1" data_merge="true">
  <tr>
    <th>Person</th>
    <th>Address</th>
  </tr>
  <tr>
    <td>Alice Anderson</td>
    <td>Maple 123, Springfield</td>
  </tr>
  <tr>
    <td>Bob Baker</td>
    <td>Oak 456, Rivertown</td>
  </tr>
</table>
```

**Optional styling** – Nếu bạn muốn giao diện sạch sẽ hơn, thêm một vài quy tắc CSS:

```html
<style>
  table { border-collapse: collapse; width: 100%; }
  th, td { padding: 8px; text-align: left; }
  th { background-color: #f2f2f2; }
</style>
```

---

## Xử lý các trường hợp đặc biệt và các biến thể phổ biến

### 1. Bộ dữ liệu trống

Nếu mảng JSON rỗng, Handlebars vẫn sẽ render hàng tiêu đề nhưng không có hàng dữ liệu. Để hiển thị thông báo thân thiện, bao quanh bảng bằng một khối điều kiện:

```handlebars
{{#if Persons.Person.length}}
  {{!-- existing table markup --}}
{{else}}
  <p>No persons found.</p>
{{/if}}
```

### 2. Vòng lặp lồng nhau (ví dụ: nhiều địa chỉ cho mỗi người)

Khi một người có thể có nhiều địa chỉ, bạn có thể lồng một `{{#foreach}}` khác bên trong hàng:

```handlebars
{{#foreach Persons.Person}}
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>
      {{#foreach Address}}
        {{Street}} {{Number}}, {{City}}<br>
      {{/foreach}}
    </td>
  </tr>
{{/foreach}}
```

### 3. Sử dụng API thực

Thay thế `<script id="people-data">` tĩnh bằng một lời gọi fetch:

```javascript
fetch('/api/persons')
  .then(r => r.json())
  .then(context => {
    const html = template(context);
    document.getElementById('output').innerHTML = html;
  });
```

Điều này minh họa kỹ thuật **dynamic table rows** tương tự trong khi lấy dữ liệu trực tiếp.

### 4. Các lưu ý về khả năng truy cập

* Thêm `scope="col"` vào các phần tử `<th>`.
* Sử dụng `<caption>` để mô tả mục đích của bảng.
* Đảm bảo độ tương phản màu đủ nếu bạn áp dụng CSS tùy chỉnh.

---

## Ví dụ đầy đủ, có thể chạy

Sao chép khối sau vào một tệp `index.html` và mở nó trong trình duyệt. Trang sẽ **generate table from data**, **populate table from JSON**, và tự động lặp lại các hàng.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Dynamic table from JSON</title>
  <style>
    table { border-collapse: collapse; width: 100%; }
    th, td { padding: 8px; text-align: left; border: 1px solid #ddd; }
    th { background-color: #f2f2f2; }
  </style>
</head>
<body>

<!-- Step 1: JSON data source -->
<script id="people-data" type="application/json">
{
  "Persons": {
    "Person": [
      {
        "FirstName": "Alice",
        "LastName": "Anderson",
        "Address": {
          "Street": "Maple",
          "Number": "123",
          "City": "Springfield"
        }
      },
      {
        "FirstName": "Bob",
        "LastName": "Baker",
        "Address": {
          "Street": "Oak",
          "Number": "456",
          "City": "Rivertown"
        }
      }
    ]
  }
}
</script>

<!-- Step 2: Handlebars template -->
<script id="table-template" type="text/x-handlebars-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <tr>
    <th scope="col">Person</th>
    <th scope="col">Address</th>
  </tr>
  {{#foreach Persons.Person}}
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
  {{/foreach}}
</table>
</script>

<!-- Step 4: Container for the generated table -->
<div id="output"></div>

<!-- Step 3: Load Handlebars, compile, and render -->
<script src="https://cdn.jsdelivr.net/npm/handlebars@4.7.7/dist/handlebars.min.js"></script>
<script>
  const raw = document.getElementById('people-data').textContent;
  const context = JSON.parse(raw);
  const source = document.getElementById('table-template').innerHTML;
  const template = Handlebars.compile(source);
  document.getElementById('output').innerHTML = template(context);
</script>

</body>
</html>
```

**Kết quả mong đợi**

Một bảng hai hàng (cộng với tiêu đề) hiển thị “Alice Anderson” và “Bob Baker” cùng địa chỉ tương ứng. Trang hoạt động offline, chứng minh rằng bạn có thể **generate table from data** mà không cần thành phần máy chủ nào.

---

## Kết luận

Bây giờ bạn đã biết cách **generate table from data** bằng mẫu Handlebars, **populate table from JSON**, và tạo **repeat table rows** tạo thành một **dynamic HTML table**. Mẫu này có thể mở rộng cho các bộ dữ liệu lớn hơn, cấu trúc lồng nhau và các cuộc gọi API trực tiếp, cung cấp nền tảng vững chắc cho bất kỳ báo cáo phía client hoặc giao diện quản trị nào.

**Các bước tiếp theo**

* Khám phá các helper của Handlebars để định dạng ngày hoặc số.
* Kết hợp cách tiếp cận này với CSS Grid hoặc Flexbox để tạo bố cục bảng đáp ứng.
* Tích hợp các thư viện phân trang hoặc sắp xếp để xử lý các bộ dữ liệu rất lớn.

Bạn có thể thoải mái thử nghiệm với các cấu trúc JSON khác nhau, thêm các cột có điều kiện, hoặc thay Handlebars bằng một engine templating khác—kỹ năng mới của bạn sẽ cho phép xây dựng các giao diện linh hoạt, dựa trên dữ liệu một cách nhanh chóng và đáng tin cậy.

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh, hoạt động với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create HTML Document with Java – Fetch JSON and Generate Content](/html/english/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/)
- [Data Handling and Stream Management in Aspose.HTML for Java](/html/english/java/data-handling-stream-management/)
- [How to Load HTML in Java – Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/how-to-load-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}