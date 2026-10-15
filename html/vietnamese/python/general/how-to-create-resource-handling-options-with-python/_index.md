---
category: general
date: 2026-10-15
description: Tìm hiểu cách tạo các tùy chọn xử lý tài nguyên và cách đặt độ sâu xử
  lý tối đa cho việc lưu Markdown trong Python. Thực hiện theo hướng dẫn từng bước.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to set max handling depth
language: vi
lastmod: 2026-10-15
og_description: Tạo các tùy chọn xử lý tài nguyên trong Python để kiểm soát việc xử
  lý tài nguyên lồng nhau. Hướng dẫn này cho thấy cách thiết lập độ sâu xử lý tối
  đa để xuất Markdown một cách đáng tin cậy.
og_image_alt: Screenshot showing Python code to create resource handling options and
  set max handling depth
og_title: Tạo các tùy chọn xử lý tài nguyên – Hướng dẫn Python
schemas:
- author: Aspose
  dateModified: '2026-10-15'
  description: Learn how to create resource handling options and how to set max handling
    depth for Markdown saving in Python. Follow a step‑by‑step guide.
  headline: How to create resource handling options with Python
  type: TechArticle
tags:
- resource handling
- Markdown
- Python
- options
title: Cách tạo các tùy chọn xử lý tài nguyên bằng Python
url: /vi/python/general/how-to-create-resource-handling-options-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo tùy chọn xử lý tài nguyên với Python

Nếu bạn cần **tạo tùy chọn xử lý tài nguyên** cho việc xuất Markdown, hướng dẫn này cung cấp giải pháp hoàn chỉnh. Bạn sẽ thấy **cách đặt độ sâu xử lý tối đa** để các tài nguyên lồng nhau dừng xử lý sau mức mong muốn.

Xử lý tài nguyên là điều cần thiết khi bạn tạo Markdown từ các tài liệu phức tạp chứa hình ảnh, tệp nhúng hoặc các tài sản liên kết khác. Đệ quy không kiểm soát có thể gây ra vấn đề hiệu năng hoặc lỗi hết bộ nhớ. Bằng cách cấu hình độ sâu xử lý, bạn giữ cho quá trình dự đoán được và hiệu quả.

Trong tutorial này, bạn sẽ:

* Khởi tạo một đối tượng `ResourceHandlingOptions`.
* Cấu hình độ sâu xử lý tối đa.
* Gắn các tùy chọn vào một thể hiện `MarkdownSaveOptions`.
* Chạy một ví dụ đầy đủ mà bạn có thể sao chép vào dự án của mình.

Không cần thư viện bên ngoài nào ngoài SDK chuẩn, và mã hoạt động với phiên bản mới nhất của gói Python tính đến tháng 10 2026.

## Prerequisites

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* Python 3.9 hoặc mới hơn đã được cài đặt.
* SDK cung cấp `ResourceHandlingOptions` và `MarkdownSaveOptions` (ví dụ, `groupdocs-viewer` hoặc một gói tương tự). Cài đặt bằng lệnh:

```bash
pip install groupdocs-viewer
```

* Kiến thức cơ bản về lớp và thuộc tính đối tượng trong Python.

## Step 1: Create resource handling options

Bước đầu tiên là **tạo tùy chọn xử lý tài nguyên**. Đối tượng này hoạt động như một container cho tất cả các cài đặt liên quan đến tài nguyên.

```python
from groupdocs.viewer import ResourceHandlingOptions, MarkdownSaveOptions

# Step 1: Instantiate the options object
resource_options = ResourceHandlingOptions()
```

`ResourceHandlingOptions` không áp dụng bất kỳ giới hạn nào theo mặc định, có nghĩa là viewer sẽ theo dõi mọi tài nguyên liên kết mà nó gặp. Khởi tạo đối tượng cung cấp cho bạn một nền tảng sạch để áp dụng các kiểm soát chính xác.

## Step 2: How to set max handling depth

Bây giờ bạn sẽ học **cách đặt độ sâu xử lý tối đa**. Thuộc tính `max_handling_depth` xác định số mức lồng nhau mà exporter sẽ xử lý trước khi dừng.

```python
# Step 2: Limit the handling depth to five levels
resource_options.max_handling_depth = 5
```

Tại sao phải giới hạn độ sâu? Hãy tưởng tượng một tài liệu Markdown tham chiếu tới một tệp Markdown khác, tệp này lại tham chiếu tới tệp thứ ba, và cứ tiếp tục như vậy. Nếu không có giới hạn độ sâu, exporter có thể đệ quy vô hạn, tiêu tốn bộ nhớ và CPU. Đặt `max_handling_depth` thành `5` sẽ yêu cầu engine dừng sau năm tài nguyên lồng nhau, đây là giá trị mặc định an toàn cho hầu hết các dự án.

### Edge case: unlimited depth

Nếu bạn muốn đệ quy không giới hạn (hiếm khi dùng trong môi trường production), hãy đặt giá trị thành `None`:

```python
resource_options.max_handling_depth = None  # No limit
```

Lưu ý rằng độ sâu không giới hạn có thể gây suy giảm hiệu năng trên các cây tài liệu rất lớn.

## Step 3: Attach the options to MarkdownSaveOptions

Sau khi cấu hình xử lý tài nguyên, bạn phải gắn các tùy chọn vào một thể hiện `MarkdownSaveOptions`. Điều này cho exporter biết sẽ sử dụng các cài đặt khi lưu.

```python
# Step 3: Create MarkdownSaveOptions and attach the resource handling config
markdown_options = MarkdownSaveOptions()
markdown_options.resource_handling_options = resource_options
```

`MarkdownSaveOptions` tổng hợp tất cả các cài đặt liên quan đến xuất. Bằng cách gán `resource_options` cho thuộc tính `resource_handling_options` của nó, bạn đảm bảo rằng giới hạn độ sâu được thực thi trong quá trình chuyển đổi.

## Step 4: Run a complete conversion (optional demo)

Đoạn mã dưới đây minh họa một quá trình chuyển đổi đầy đủ từ một tài liệu mẫu sang Markdown sử dụng các tùy chọn bạn vừa tạo. Điều chỉnh các đường dẫn tệp cho phù hợp với môi trường của bạn.

```python
from groupdocs.viewer import Viewer

# Path to the source document (e.g., a DOCX with embedded images)
source_path = "sample.docx"
# Path where the Markdown output will be saved
output_path = "output.md"

# Initialize the viewer with the source file
viewer = Viewer(source_path)

# Perform the conversion using the configured options
viewer.save(output_path, markdown_options)

print(f"Conversion complete. Markdown saved to {output_path}")
```

**Expected output**

```
Conversion complete. Markdown saved to output.md
```

Sau khi chạy script, mở `output.md`. Bạn sẽ thấy các hình ảnh và tài nguyên khác được tham chiếu tới tối đa năm mức lồng nhau; bất kỳ liên kết nào sâu hơn sẽ bị bỏ qua, ngăn ngừa đệ quy không kiểm soát.

## Pro tip: verify the handling depth at runtime

Nếu bạn cần xác nhận rằng giới hạn độ sâu đã được áp dụng, có thể kiểm tra Markdown đã tạo để tìm các tham chiếu tài nguyên bị thiếu hoặc bật chế độ ghi log chi tiết trong SDK:

```python
viewer.set_logging(True)  # Enable detailed logs
```

Log sẽ hiển thị các thông báo như:

```
[INFO] Resource handling stopped at depth 5 for file 'nested_image.png'
```

## Common questions

**What if my document has fewer than five nested resources?**  
Exporter sẽ xử lý tất cả các tài nguyên có sẵn vì giới hạn độ sâu cao hơn độ sâu thực tế. Không có tài nguyên nào bị cắt ngắn.

**Can I set a different limit for different file types?**  
Có. Tạo các đối tượng `ResourceHandlingOptions` riêng cho mỗi định dạng xuất và gán chúng vào thể hiện `SaveOptions` tương ứng.

**Does the depth limit affect only images?**  
Không. Giới hạn áp dụng cho *tất cả* tài nguyên mà exporter có thể theo dõi, bao gồm tệp nhúng, siêu liên kết và các include Markdown lồng nhau.

## Conclusion

Bây giờ bạn đã biết cách **tạo tùy chọn xử lý tài nguyên** và **đặt độ sâu xử lý tối đa** cho các xuất Markdown đáng tin cậy trong Python. Bằng cách giới hạn đệ quy, bạn bảo vệ ứng dụng khỏi việc tiêu tốn quá mức bộ nhớ đồng thời vẫn giữ được cấu trúc nội dung cần thiết.

Các bước tiếp theo bạn có thể khám phá:

* Điều chỉnh các thuộc tính khác của `ResourceHandlingOptions` như `extract_images` hoặc `preserve_links`.
* Kết hợp xử lý tài nguyên với quy tắc đặt tên tùy chỉnh cho các tệp đã trích xuất.
* Thử nghiệm các giá trị độ sâu khác nhau để tìm mức tối ưu cho bộ tài liệu của bạn.

Hãy tự do điều chỉnh các đoạn mã cho quy trình làm việc của mình và chia sẻ kết quả với cộng đồng. Chúc bạn lập trình vui vẻ!

## What Should You Learn Next?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Zip HTML in C# – Custom Resource Handler Tutorial](/html/english/net/html-extensions-and-conversions/how-to-zip-html-in-c-custom-resource-handler-tutorial/)
- [How to create custom schema handler with Aspose.HTML for Java](/html/english/java/custom-schema-message-handling/custom-schema-message-handler/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}