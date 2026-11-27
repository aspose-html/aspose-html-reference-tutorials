---
category: general
date: 2026-11-27
description: Tạo tài liệu SVG và lưu tệp SVG bằng Python. Học cách xuất vector dưới
  dạng SVG và nhanh chóng tạo hình ảnh SVG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG file
- export vector as SVG
- save SVG image
- how to create SVG
language: vi
lastmod: 2026-11-27
og_description: Tạo tài liệu SVG và lưu tệp SVG bằng Python. Hướng dẫn này cho bạn
  cách xuất vector dưới dạng SVG và tạo hình ảnh SVG trong vài phút.
og_image_alt: Screenshot of a red circle saved as an SVG document
og_title: Tạo tài liệu SVG và lưu tệp SVG bằng Python
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  headline: Create SVG document and save SVG file with Python
  type: TechArticle
- description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  name: Create SVG document and save SVG file with Python
  steps:
  - name: Expected output
    text: 'The resulting `circle.svg` contains:'
  - name: Exporting more complex vectors
    text: 'If you need to **export vector as SVG** for multi‑shape illustrations,
      simply repeat the `dwg.add()` pattern with other primitives (`rect`, `line`,
      `path`, etc.). For example:'
  - name: Handling Unicode and text
    text: "SVG supports text elements with full Unicode support. Use `dwg.text(\"Hello,
      \U0001F30D\", insert=(5, 95), fill=\"black\")` to embed multilingual labels."
  - name: Saving to a different location
    text: 'When **save SVG image** to a user‑specified folder, validate the path to
      avoid permission errors:'
  - name: Minifying the output
    text: 'For production pipelines, you might want a smaller file size. Pass `pretty=False`
      to `dwg.tostring()` and write the result manually:'
  type: HowTo
tags:
- SVG
- Python
- Vector graphics
title: Tạo tài liệu SVG và lưu tệp SVG bằng Python
url: /vi/python/general/create-svg-document-and-save-svg-file-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo tài liệu SVG và lưu tệp SVG bằng Python

Nếu bạn cần **create SVG document** từ đầu, hướng dẫn này sẽ dẫn bạn qua toàn bộ quy trình. Bạn sẽ thấy cách **save SVG file** lên đĩa, xuất vector dưới dạng SVG, và có được một hình ảnh SVG sẵn sàng sử dụng chỉ trong vài dòng mã.

Việc tạo đồ họa có thể mở rộng một cách lập trình hữu ích cho báo cáo, biểu tượng UI, hoặc bất kỳ tình huống nào bạn muốn có hình ảnh không phụ thuộc vào độ phân giải. Khi kết thúc tutorial này, bạn sẽ có thể trả lời câu hỏi “**how to create SVG**?” cho các hình dạng đơn giản và mở rộng mẫu này cho các tác phẩm vector phức tạp hơn.

## Những gì bạn cần

- Python 3.8 trở lên  
- Gói `svgwrite` (có thể cài đặt qua `pip`)  
- Thư mục có quyền ghi cho tệp đầu ra  

Không cần bất kỳ trình chỉnh sửa đồ họa bên ngoài nào; mọi thứ chạy từ dòng lệnh.

## Bước 1: Cài đặt thư viện `svgwrite`

`svgwrite` cung cấp một API sạch, Pythonic để xây dựng markup SVG. Cài đặt một lần bằng cách:

```bash
pip install svgwrite
```

> **Mẹo chuyên nghiệp:** Sử dụng môi trường ảo (`python -m venv .venv`) để giữ các phụ thuộc được cô lập.

## Bước 2: Tạo tài liệu SVG

Bây giờ chúng ta thực sự **create SVG document** các đối tượng. Lớp `Drawing` đại diện cho phần tử gốc `<svg>` và tự động xử lý các namespace.

```python
import pathlib
import svgwrite

# Define where the file will be saved
output_path = pathlib.Path("output/circle.svg")
output_path.parent.mkdir(parents=True, exist_ok=True)

# Initialize a new SVG document with a 100×100 viewport
dwg = svgwrite.Drawing(
    filename=str(output_path),
    size=("100px", "100px"),
    profile="tiny"  # tiny profile keeps the file lightweight
)
```

Đối tượng `Drawing` là điểm khởi đầu cho mọi thao tác SVG tiếp theo. Bằng cách chỉ định `size` chúng ta đặt kích thước canvas, ảnh hưởng đến cách trình duyệt hiển thị hình ảnh.

## Bước 3: Thêm một phần tử vòng tròn màu đỏ

Thêm các hình dạng rất đơn giản. Phương thức `circle` tạo một phần tử `<circle>`; sau đó chúng ta gắn nó vào gốc.

```python
# Create a red circle with radius 40 centered at (50, 50)
circle = dwg.circle(
    center=(50, 50),
    r=40,
    fill="red"
)

# Append the circle to the SVG root
dwg.add(circle)
```

Lý do chúng ta chọn vòng tròn: các vòng tròn là primitive vector thể hiện khả năng mở rộng mà không mất chất lượng, làm cho kết quả phù hợp để thử nghiệm quy trình **export vector as SVG**.

## Bước 4: Lưu tệp SVG

Cuối cùng, ghi markup ra đĩa. Bước này đáp ứng yêu cầu **save SVG file** và tạo ra một tệp bạn có thể mở trong bất kỳ trình duyệt hoặc trình chỉnh sửa vector nào.

```python
# Persist the SVG document to the filesystem
dwg.save()
print(f"SVG saved to {output_path.resolve()}")
```

Khi bạn chạy script, sẽ có thông báo trên console xác nhận vị trí của tệp đã tạo.

### Kết quả mong đợi

Tệp `circle.svg` tạo ra chứa:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg height="100px" version="1.1" width="100px" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" fill="red"/>
</svg>
```

Mở tệp trong trình duyệt sẽ hiển thị một vòng tròn đỏ sắc nét, và vì nó dựa trên vector nên bạn có thể phóng to vô hạn mà không bị pixel hoá.

## Bước 5: Các biến thể phổ biến và trường hợp đặc biệt

### Xuất các vector phức tạp hơn

Nếu bạn cần **export vector as SVG** cho các minh hoạ đa hình, chỉ cần lặp lại mẫu `dwg.add()` với các primitive khác (`rect`, `line`, `path`, v.v.). Ví dụ:

```python
dwg.add(dwg.rect(insert=(10, 10), size=(30, 30), fill="blue"))
dwg.add(dwg.line(start=(0, 0), end=(100, 100), stroke="black", stroke_width=2))
```

### Xử lý Unicode và văn bản

SVG hỗ trợ các phần tử text với đầy đủ hỗ trợ Unicode. Dùng `dwg.text("Hello, 🌍", insert=(5, 95), fill="black")` để nhúng nhãn đa ngôn ngữ.

### Lưu vào vị trí khác

Khi **save SVG image** vào thư mục do người dùng chỉ định, hãy xác thực đường dẫn để tránh lỗi quyền truy cập:

```python
if not output_path.parent.exists():
    raise PermissionError(f"Cannot write to {output_path.parent}")
dwg.save()
```

### Thu nhỏ đầu ra

Đối với các pipeline sản xuất, bạn có thể muốn giảm kích thước tệp. Truyền `pretty=False` vào `dwg.tostring()` và ghi kết quả thủ công:

```python
minified = dwg.tostring(pretty=False)
output_path.write_text(minified)
```

## Cách tạo SVG bằng các thư viện thay thế (tùy chọn)

Mặc dù `svgwrite` nhẹ và thuần Python, vẫn có các hệ sinh thái khác:

- **cairosvg** – chuyển đổi PNG, PDF hoặc HTML sang SVG.  
- **lxml** – cho phép bạn xây dựng markup SVG thủ công bằng các API XML.  

Lựa chọn thư viện phụ thuộc vào độ phức tạp của dự án và các phụ thuộc hiện có.

## Kết luận

Bây giờ bạn đã biết cách **create SVG document**, thêm các hình dạng vector, và **save SVG file** bằng Python. Giải pháp hoàn chỉnh minh họa các bước **export vector as SVG**, tạo **SVG image**, và trả lời câu hỏi thường gặp **how to create SVG** một cách lập trình.

Từ đây bạn có thể:

- Mở rộng script với vòng lặp để tự động tạo biểu đồ hoặc biểu tượng.  
- Tích hợp đầu ra SVG vào các ứng dụng web hoặc mẫu email.  
- Khám phá hoạt ảnh bằng cách thêm các phần tử `<animate>` với `svgwrite`.

Thử nghiệm với các hình dạng, màu sắc và gradient khác nhau để khai thác tối đa sức mạnh của đồ họa vector có thể mở rộng trong các dự án Python của bạn. Chúc bạn lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create SVG Document – Add a Circle and Save as SVG](/html/english/python/general/create-svg-document-add-a-circle-and-save-as-svg/)
- [Create SVG Document in Python – Convert SVG to PNG Guide](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)
- [Load SVG File Python – Complete Guide to Export, Embed & Convert](/html/english/python/general/load-svg-file-python-complete-guide-to-export-embed-convert/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}