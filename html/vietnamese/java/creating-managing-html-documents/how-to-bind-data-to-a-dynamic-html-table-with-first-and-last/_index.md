---
category: general
date: 2026-09-07
description: cách ràng buộc dữ liệu trong bảng HTML động – học cách tạo các dòng bảng
  và điền các trường họ và tên một cách hiệu quả
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to bind data
- dynamic html table
- first and last name
- how to generate table
- populate table rows
language: vi
lastmod: 2026-09-07
og_description: cách liên kết dữ liệu trong bảng HTML động. Hướng dẫn này cho thấy
  cách tạo các hàng bảng, hiển thị họ và tên, và điền dữ liệu vào các hàng bảng bằng
  JavaScript.
og_image_alt: Screenshot of a dynamic HTML table populated with first and last names
  after binding data
og_title: Cách liên kết dữ liệu vào bảng HTML động – hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-09-07'
  description: how to bind data in a dynamic HTML table – learn how to generate table
    rows and populate first and last name fields efficiently
  headline: How to bind data to a dynamic HTML table with first and last name columns
  type: TechArticle
tags:
- data binding
- html table
- templating
title: Cách liên kết dữ liệu vào bảng HTML động với các cột họ và tên
url: /vi/java/creating-managing-html-documents/how-to-bind-data-to-a-dynamic-html-table-with-first-and-last/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách ràng buộc dữ liệu vào bảng HTML động với các cột họ và tên

Nếu bạn cần **cách ràng buộc dữ liệu** vào một bảng mà sẽ mở rộng theo từng bản ghi, hướng dẫn này cung cấp giải pháp hoàn chỉnh. Bạn sẽ thấy cách tạo bảng HTML động, điền các hàng bảng, và hiển thị họ và tên của mỗi người mà không phải viết markup lặp lại.

Ví dụ sử dụng cú pháp mẫu nhẹ nhàng hoạt động trong bất kỳ trình duyệt hiện đại nào, nhưng các khái niệm cũng áp dụng cho Handlebars, Mustache, hoặc các engine phía máy chủ. Khi kết thúc tutorial, bạn có thể sao chép mã vào dự án và bắt đầu ràng buộc dữ liệu ngay lập tức.

## Những gì tutorial này đề cập

* Cách cấu trúc nguồn dữ liệu chứa nhiều người  
* Cách tạo mẫu bảng có thể tái sử dụng và lặp lại cho mỗi mục nhập  
* Cách ràng buộc dữ liệu và tạo markup HTML cuối cùng  
* Những lỗi thường gặp khi điền các hàng bảng và cách tránh chúng  

Không cần thư viện bên ngoài, mặc dù cùng một mẫu cũng hoạt động với các framework mẫu phổ biến. Yêu cầu duy nhất là kiến thức cơ bản về HTML và JavaScript.

## Điều kiện tiên quyết

* Trình duyệt hiện đại (Chrome, Edge, Firefox hoặc Safari)  
* Trình soạn thảo cho các tệp HTML/JavaScript  
* Tùy chọn: tệp JSON hoặc đối tượng JavaScript đại diện cho bộ sưu tập người  

## Bước 1: Định nghĩa nguồn dữ liệu

Đầu tiên, tạo một đối tượng JavaScript phản ánh cấu trúc được sử dụng trong mẫu. Mỗi người có họ, tên và một đối tượng địa chỉ.

```html
<script>
  // Data source – an array of person objects
  const data = {
    Persons: {
      Person: [
        {
          FirstName: "Alice",
          LastName: "Johnson",
          Address: {
            Street: "Maple",
            Number: "12A",
            City: "Springfield"
          }
        },
        {
          FirstName: "Bob",
          LastName: "Smith",
          Address: {
            Street: "Oak",
            Number: "34B",
            City: "Riverdale"
          }
        }
        // Add more person objects as needed
      ]
    }
  };
</script>
```

**Tại sao điều này quan trọng:** Cây đối tượng (`Persons.Person`) khớp với vòng lặp `{{#foreach Persons.Person}}` trong mẫu, cho phép engine tự động lặp qua mọi mục nhập.

## Bước 2: Viết mẫu bảng với khối lặp

Mẫu dưới đây sử dụng cú pháp kiểu Mustache đơn giản (`{{#foreach}}`) để lặp lại `<tr>` cho mỗi người. Đặt mẫu trong thẻ `<script type="text/template">` để trình duyệt bỏ qua cho đến khi bạn xử lý nó.

```html
<script type="text/template" id="table-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <!-- Table header -->
  <tr>
    <th>Person</th><th>Address</th>
  </tr>
  <!-- Row populated with each person's data -->
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
</table>
</script>
```

**Tại sao điều này quan trọng:** Chỉ thị `{{#foreach Persons.Person}}` nói cho engine biết lặp lại mọi thứ giữa thẻ mở và thẻ đóng cho mỗi đối tượng người. Bên trong hàng bạn có thể tham chiếu bất kỳ thuộc tính nào (`{{FirstName}}`, `{{LastName}}`, v.v.) để **điền các hàng bảng** một cách động.

## Bước 3: Triển khai hàm render nhỏ

Vì tutorial phải tự chứa, chúng ta sẽ viết một renderer tối thiểu thay thế các placeholder kiểu Mustache bằng giá trị thực. Hàm này duyệt qua đối tượng dữ liệu, mở rộng khối lặp, và chèn HTML cuối cùng vào trang.

```html
<script>
  /**
   * Renders a template that contains a single {{#foreach}} block.
   * This implementation is intentionally simple and works for the
   * specific structure used in this tutorial.
   *
   * @param {string} tmpl   The raw template string.
   * @param {object} ctx    The data context (e.g., the `data` object).
   * @returns {string}      The rendered HTML.
   */
  function renderTemplate(tmpl, ctx) {
    // Extract the foreach expression and the block to repeat
    const foreachRegex = /{{#foreach\s+([^}]+)}}([\s\S]*?){{\/foreach}}/;
    const match = tmpl.match(foreachRegex);
    if (!match) return tmpl; // No foreach found

    const path = match[1].trim(); // e.g., "Persons.Person"
    const block = match[2];       // HTML that repeats

    // Resolve the array from the context (supports dot notation)
    const items = path.split('.').reduce((obj, key) => obj && obj[key], ctx);
    if (!Array.isArray(items)) return tmpl;

    // Render each item
    const renderedBlocks = items.map(item => {
      // Replace each {{property}} with the corresponding value
      return block.replace(/{{([^}]+)}}/g, (_, prop) => {
        const value = prop.trim().split('.').reduce((obj, key) => obj && obj[key], item);
        return value !== undefined ? value : '';
      });
    });

    // Replace the whole foreach section with the concatenated rows
    return tmpl.replace(foreachRegex, renderedBlocks.join(''));
  }

  // When the DOM is ready, render the table
  document.addEventListener('DOMContentLoaded', () => {
    const tmpl = document.getElementById('table-template').innerHTML;
    const html = renderTemplate(tmpl, data);
    document.getElementById('output').innerHTML = html;
  });
</script>
```

**Tại sao điều này quan trọng:** Renderer minh họa **cách tạo bảng** markup một cách lập trình mà không cần kéo toàn bộ thư viện. Nó cũng làm rõ quá trình chuyển đổi từ mẫu sang HTML cuối cùng, giúp bạn dễ dàng áp dụng mã cho các engine mẫu khác sau này.

## Bước 4: Thêm vị trí giữ chỗ cho bảng được tạo

Tạo một `<div>` trống mà script sẽ điền sau khi render.

```html
<div id="output"></div>
```

Khi trang tải, script sẽ thay thế nội dung của `<div>` này bằng bảng đã được điền đầy đủ.

## Bước 5: Kiểm tra kết quả

Mở tệp HTML trong trình duyệt. Bạn sẽ thấy một bảng liệt kê họ và tên đầy đủ cùng địa chỉ của mỗi người:

| Người           | Địa chỉ                         |
|-----------------|---------------------------------|
| Alice Johnson   | Maple 12A, Springfield          |
| Bob Smith       | Oak 34B, Riverdale              |

Nếu bạn thêm nhiều đối tượng hơn vào mảng `data.Persons.Person`, bảng sẽ tự động mở rộng—đáp ứng yêu cầu **điền các hàng bảng**.

## Mẹo chuyên nghiệp: xử lý bộ sưu tập rỗng

Khi mảng dữ liệu trống, renderer hiện tại sẽ xuất ra một tiêu đề bảng rỗng. Để cung cấp trải nghiệm người dùng rõ ràng hơn, hãy thêm một kiểm tra:

```javascript
if (items.length === 0) {
  return '<p>No records found.</p>';
}
```

Thay đổi nhỏ này ngăn không cho bảng trống xuất hiện và cung cấp phản hồi ngay cho người dùng.

## Các biến thể phổ biến và trường hợp góc cạnh

| Tình huống                               | Điều chỉnh                                                                 |
|----------------------------------------|----------------------------------------------------------------------------|
| Sử dụng engine phía máy chủ (ví dụ: Handlebars) | Thay thế `renderTemplate` tùy chỉnh bằng `Handlebars.compile` và truyền cùng một đối tượng dữ liệu. |
| Cần sắp xếp các hàng theo thứ tự alphabet | Sắp xếp `data.Persons.Person` trước khi gọi `renderTemplate`.               |
| Thêm cột số điện thoại                 | Mở rộng `<tr>` bằng `<td>{{Phone}}</td>` và bao gồm `Phone` trong mỗi đối tượng người. |
| Bộ dữ liệu lớn (hàng hàng trăm)        | Render các hàng theo khối hoặc sử dụng cuộn ảo để giữ UI phản hồi nhanh.   |

## Ví dụ hoàn chỉnh hoạt động

Dưới đây là tệp HTML đầy đủ mà bạn có thể sao chép‑dán vào `index.html`. Nó chứa tất cả các phần đã thảo luận ở trên.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How to bind data to a dynamic HTML table</title>
  <style>
    table { border-collapse: collapse; width: 100%; }
    th, td { padding: 8px; text-align: left; }
    th { background-color: #f2f2f2; }
  </style>
</head>
<body>

<h1>Dynamic HTML table bound to JavaScript data</h1>

<!-- Step 2: Table template -->
<script type="text/template" id="table-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <tr>
    <th>Person</th><th>Address</th>
  </tr>
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
</table>
</script>

<!-- Step 1: Data source -->
<script>
  const data = {
    Persons: {
      Person: [
        {
          FirstName: "Alice",
          LastName: "Johnson",
          Address: { Street: "Maple", Number: "12A", City: "Springfield" }
        },
        {
          FirstName: "Bob",
          LastName: "Smith",
          Address: { Street: "Oak", Number: "34B", City: "Riverdale" }
        }
        // Add more entries as needed
      ]
    }
  };
</script>

<!-- Step 4: Output container -->
<div id="output"></div>

<!-- Step 3: Rendering logic -->
<script>
  function renderTemplate(tmpl, ctx) {
    const foreachRegex = /{{#foreach\s+([^}]+)}}([\s\S]*?){{\/foreach}}/;
    const match = tmpl.match(foreachRegex);
    if (!match) return tmpl;
    const path = match[1].trim();
    const block = match[2];
    const items = path.split('.').reduce((obj, key) => obj && obj[key], ctx);
    if (!Array.isArray(items) || items.length === 0) {
      return '<p>No records found.</p>';
    }
    const renderedBlocks = items.map(item => {
      return block.replace(/{{([^}]+)}}/g, (_, prop) => {
        const value = prop.trim().split('.').reduce((obj, key) => obj && obj[key], item);
        return value !== undefined ? value : '';
      });
    });
    return tmpl.replace(foreachRegex, renderedBlocks.join(''));
  }

  document.addEventListener('DOMContentLoaded', () => {
    const tmpl = document.getElementById('table-template').innerHTML;
    const html = renderTemplate(tmpl, data);
    document.getElementById('output').innerHTML = html;
  });
</script>

</body>
</html>
```

**Kết quả mong đợi**

Trang sẽ hiển thị một bảng với hai hàng, mỗi hàng hiển thị họ và tên đầy đủ cùng địa chỉ đã định dạng của một người. Thêm nhiều đối tượng vào mảng `Person` sẽ tự động thêm các hàng mới—chứng minh **cách tạo bảng** từ dữ liệu.

## Kết luận

Bây giờ bạn đã biết **cách ràng buộc dữ liệu** vào một **bảng HTML động**, tạo các hàng cho mỗi bản ghi, và hiển thị giá trị họ và tên cùng địa chỉ.

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Enable JavaScript in Aspose HTML – Load HTML & Get Text](/html/english/java/advanced-usage/how-to-enable-javascript-in-aspose-html-load-html-get-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}