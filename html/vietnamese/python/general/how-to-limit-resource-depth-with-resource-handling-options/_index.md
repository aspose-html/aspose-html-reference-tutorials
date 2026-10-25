---
category: general
date: 2026-10-25
description: Tìm hiểu cách giới hạn độ sâu tài nguyên và áp dụng xử lý tài nguyên
  khi lưu các tệp HTML lớn bằng Python. Hãy làm theo hướng dẫn từng bước này để có
  kết quả đáng tin cậy.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- limit resource depth
- apply resource handling
- HTML document processing
- save options Python
- resource handling options
language: vi
lastmod: 2026-10-25
og_description: Giới hạn độ sâu tài nguyên và áp dụng xử lý tài nguyên khi lưu HTML
  bằng Python. Hướng dẫn này trình bày giải pháp đầy đủ, có thể chạy được.
og_image_alt: Screenshot illustrating limit resource depth in a Python script
og_title: Giới hạn độ sâu tài nguyên khi áp dụng xử lý tài nguyên – Hướng dẫn Python
schemas:
- author: GroupDocs
  dateModified: '2026-10-25'
  description: Learn how to limit resource depth and apply resource handling when
    saving large HTML files using Python. Follow this step‑by‑step guide for reliable
    results.
  headline: How to limit resource depth with resource handling options
  type: TechArticle
- description: Learn how to limit resource depth and apply resource handling when
    saving large HTML files using Python. Follow this step‑by‑step guide for reliable
    results.
  name: How to limit resource depth with resource handling options
  steps:
  - name: '**Dynamic content loaded via JavaScript** – The parser only sees static
      HTML. If your page relies on scripts that inject further resources, those will
      never be counted toward the depth limit. Consider pre‑rendering the page with
      a headless browser before applying the limit.'
    text: '**Dynamic content loaded via JavaScript** – The parser only sees static
      HTML. If your page relies on scripts that inject further resources, those will
      never be counted toward the depth limit. Consider pre‑rendering the page with
      a headless browser before applying the limit.'
  - name: '**Circular references** – Some pages include iframes that point back to
      the same page. The depth counter prevents infinite loops, but you may still
      see partially rendered sections. Adjust `max_handling_depth` or manually exclude
      problematic frames.'
    text: '**Circular references** – Some pages include iframes that point back to
      the same page. The depth counter prevents infinite loops, but you may still
      see partially rendered sections. Adjust `max_handling_depth` or manually exclude
      problematic frames.'
  - name: '**Mixed protocols (http/https)** – If resources use different schemes,
      the library may treat them as separate domains. The depth limit still applies
      across protocols, but network permissions might differ. Ensure your environment
      permits both.'
    text: '**Mixed protocols (http/https)** – If resources use different schemes,
      the library may treat them as separate domains. The depth limit still applies
      across protocols, but network permissions might differ. Ensure your environment
      permits both.'
  type: HowTo
tags:
- Python
- HTML
- File handling
title: Cách giới hạn độ sâu tài nguyên bằng các tùy chọn xử lý tài nguyên
url: /vi/python/general/how-to-limit-resource-depth-with-resource-handling-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách giới hạn độ sâu tài nguyên với các tùy chọn xử lý tài nguyên

Nếu bạn cần **giới hạn độ sâu tài nguyên** khi xử lý một tệp HTML khổng lồ, hướng dẫn này sẽ chỉ cho bạn cách thực hiện chính xác. Khi kết thúc bài học, bạn cũng sẽ biết cách **áp dụng xử lý tài nguyên** để thao tác lưu tôn trọng giới hạn độ sâu và tránh việc xử lý không kiểm soát.

Các trang HTML lớn thường nhúng nhiều tài nguyên bên ngoài — hình ảnh, script, stylesheet và iframe lồng nhau. Nếu không có giới hạn độ sâu, trình phân tích có thể theo mọi liên kết, làm tăng đáng kể việc sử dụng bộ nhớ và thời gian xử lý. Kỹ thuật được mô tả ở đây giúp duy trì tốc độ và tính dự đoán của quá trình.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* Python 3.9+ đã được cài đặt.
* Thư viện `groupdocs-viewer` (hoặc một thư viện xử lý HTML tương tự) có sẵn qua `pip install groupdocs-viewer`.
* Một tệp HTML mẫu (`big_page.html`) nằm trong một thư mục đã biết.
* Quyền ghi vào thư mục đầu ra.

Những mục này đảm bảo mã chạy mà không cần cấu hình bổ sung.

## Bước 1: Tải tài liệu HTML nguồn

Bước đầu tiên là tạo một thể hiện `HTMLDocument` trỏ tới tệp gốc. Đối tượng này đại diện cho toàn bộ cấu trúc HTML và cho phép bạn truy cập các tùy chọn lưu sau này.

```python
# Step 1: Load the source HTML document
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

*Tại sao điều này quan trọng*: Tải tệp một lần duy nhất cung cấp cho thư viện một điểm vào duy nhất cho mọi thao tác tiếp theo. Nó cũng xác thực rằng tệp tồn tại, đưa ra lỗi sớm nếu đường dẫn sai.

## Bước 2: Tạo tùy chọn xử lý tài nguyên và giới hạn độ sâu xử lý

`ResourceHandlingOptions` cho phép bạn kiểm soát độ sâu mà thư viện sẽ duyệt qua các tài nguyên liên kết. Đặt `max_handling_depth` thành một số thấp (ví dụ, 5) sẽ khiến engine dừng theo dõi các liên kết sau năm mức lồng nhau.

```python
# Step 2: Create resource handling options and limit the processing depth
resource_opts = ResourceHandlingOptions()
resource_opts.max_handling_depth = 5  # Restricts handling to 5 levels deep
```

*Tại sao điều này quan trọng*: Bằng cách **giới hạn độ sâu tài nguyên**, bạn ngăn trình phân tích tải xuống mọi hình ảnh, script hoặc iframe có thể được tham chiếu gián tiếp. Điều này giảm lưu lượng mạng và áp lực bộ nhớ, đặc biệt với các trang nhúng nội dung của bên thứ ba.

## Bước 3: Gắn tùy chọn tài nguyên vào tùy chọn lưu

`SaveOptions` tổng hợp tất cả các cài đặt ảnh hưởng đến tệp đầu ra. Bằng cách gán `resource_handling_options` chúng ta **áp dụng xử lý tài nguyên** cho thao tác lưu sắp tới.

```python
# Step 3: Attach the resource options to the save options
save_opts = SaveOptions()
save_opts.resource_handling_options = resource_opts
```

*Tại sao điều này quan trọng*: Đối tượng `save_opts` hoạt động như một container cho nhiều cờ (nén, định dạng, v.v.). Thêm `resource_handling_options` đảm bảo giới hạn độ sâu được tôn trọng trong giai đoạn ghi.

## Bước 4: Lưu tài liệu với xử lý tài nguyên đã được giới hạn

Cuối cùng, gọi `doc.save()` với `save_opts` đã cấu hình. Tệp đầu ra sẽ chỉ chứa các tài nguyên nằm trong độ sâu đã định.

```python
# Step 4: Save the document with the limited resource handling applied
doc.save("YOUR_DIRECTORY/big_page_limited.html", save_opts)
```

**Kết quả mong đợi**:  
Một tệp mới `big_page_limited.html` xuất hiện trong `YOUR_DIRECTORY`. Mở nó trong trình duyệt; bạn sẽ thấy bố cục gốc, nhưng bất kỳ tài nguyên nào vượt quá năm mức lồng nhau sẽ bị loại bỏ. Trang tải nhanh hơn và tiêu thụ ít bộ nhớ hơn nhiều.

## Xác minh HTML đã lưu

Sau khi lưu, tốt nhất là kiểm tra xem giới hạn độ sâu đã được tôn trọng hay chưa.

```python
# Verify that the saved file exists and its size is reasonable
import os

output_path = "YOUR_DIRECTORY/big_page_limited.html"
if os.path.isfile(output_path):
    size_kb = os.path.getsize(output_path) / 1024
    print(f"Saved file size: {size_kb:.2f} KB")
else:
    raise FileNotFoundError("The limited HTML file was not created.")
```

Nếu kích thước tệp giảm đáng kể so với bản gốc (có thể hàng trăm kilobyte), thì cài đặt **giới hạn độ sâu tài nguyên** đã hoạt động như mong muốn.

## Những lỗi thường gặp và cách tránh

| Triệu chứng | Nguyên nhân | Cách khắc phục |
|------------|-------------|----------------|
| Không có thay đổi về kích thước tệp | `max_handling_depth` để mặc định (không giới hạn) | Đặt rõ `resource_opts.max_handling_depth` thành một giá trị < ∞ |
| Hình ảnh bị thiếu trên trang | Các tài nguyên nằm sâu hơn mức giới hạn | Tăng độ sâu hoặc di chuyển các tài nguyên quan trọng lên mức nông hơn |
| `PermissionError` khi lưu | Thư mục đầu ra chỉ đọc | Chọn thư mục có quyền ghi hoặc điều chỉnh quyền hệ điều hành |
| Ngoại lệ bất ngờ `ResourceHandlingException` | Không tương thích phiên bản thư viện | Nâng cấp lên bản `groupdocs-viewer` mới nhất (`pip install --upgrade groupdocs-viewer`) |

**Mẹo chuyên nghiệp**: Bắt đầu với độ sâu 3 cho các trang rất lớn và tăng dần cho đến khi độ chính xác hình ảnh đáp ứng yêu cầu của bạn.

## Các trường hợp đặc biệt bạn có thể gặp

1. **Nội dung động tải qua JavaScript** – Trình phân tích chỉ nhìn thấy HTML tĩnh. Nếu trang của bạn dựa vào script để chèn thêm tài nguyên, những tài nguyên đó sẽ không được tính vào giới hạn độ sâu. Hãy cân nhắc render trước trang bằng trình duyệt không giao diện (headless) trước khi áp dụng giới hạn.
2. **Tham chiếu vòng** – Một số trang bao gồm iframe trỏ lại chính trang đó. Bộ đếm độ sâu ngăn vòng lặp vô hạn, nhưng bạn vẫn có thể thấy một số phần hiển thị không đầy đủ. Điều chỉnh `max_handling_depth` hoặc loại trừ thủ công các frame gây vấn đề.
3. **Giao thức hỗn hợp (http/https)** – Nếu tài nguyên sử dụng các scheme khác nhau, thư viện có thể coi chúng là các domain riêng. Giới hạn độ sâu vẫn áp dụng qua các protocol, nhưng quyền truy cập mạng có thể khác nhau. Đảm bảo môi trường của bạn cho phép cả hai.

## Bước tiếp theo: xử lý tài nguyên nâng cao

Bây giờ bạn đã có thể **giới hạn độ sâu tài nguyên** và **áp dụng xử lý tài nguyên**, có thể muốn khám phá:

* **Bộ lọc tùy chỉnh** – Dùng `resource_opts.resource_filter` để bỏ qua các loại tệp cụ thể (ví dụ, video lớn).
* **Cài đặt nén** – Kết hợp `SaveOptions` với `compression_level` để giảm kích thước đầu ra hơn nữa.
* **Xử lý hàng loạt** – Duyệt qua một thư mục các tệp HTML, áp dụng cùng một giới hạn độ sâu cho mỗi tệp.

Những mở rộng này cho phép bạn xây dựng một pipeline tối ưu hoá HTML hoàn chỉnh cho các quy trình tài liệu quy mô lớn.

## Kết luận

Bạn đã học cách **giới hạn độ sâu tài nguyên** và **áp dụng xử lý tài nguyên** khi lưu một tài liệu HTML lớn bằng Python. Bằng cách cấu hình `ResourceHandlingOptions` và gắn chúng vào `SaveOptions`, bạn có được kiểm soát chi tiết về số lượng tài nguyên lồng nhau được xử lý, dẫn tới việc lưu nhanh hơn và tệp đầu ra nhỏ hơn. Hãy thử nghiệm với các giá trị độ sâu khác nhau và các `SaveOptions` bổ sung để tùy chỉnh hành vi cho nhu cầu dự án của bạn.

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Set max_handling_depth in Aspose.HTML Python – Complete Guide](/html/english/python/general/how-to-set-max-handling-depth-in-aspose-html-python-complete/)
- [Create resource handling options and load an HTML document in Python](/html/english/python/general/create-resource-handling-options-and-load-an-html-document-i/)
- [How to Save HTML with Controlled Depth – Step‑by‑Step Python Guide](/html/english/python/general/how-to-save-html-with-controlled-depth-step-by-step-python-g/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}