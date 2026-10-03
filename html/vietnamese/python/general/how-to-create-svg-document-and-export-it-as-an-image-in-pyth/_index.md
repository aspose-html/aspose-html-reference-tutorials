---
category: general
date: 2026-10-02
description: Tìm hiểu cách tạo tài liệu SVG trong Python, lưu SVG vào tệp và xuất
  hình ảnh SVG bằng một đoạn mã ngắn, đầy đủ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG to file
- how to generate SVG
- export SVG image
- SVG Python tutorial
language: vi
lastmod: 2026-10-02
og_description: Tạo tài liệu SVG trong Python và xuất hình ảnh SVG với hướng dẫn thực
  tế này. Theo dõi kịch bản, lưu SVG vào tệp và sử dụng lại đồ họa vector ngay lập
  tức.
og_image_alt: Screenshot of a Python script that creates an SVG document
og_title: Tạo tài liệu SVG trong Python – hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-10-02'
  description: Learn how to create SVG document in Python, save SVG to file, and export
    SVG image with a short, complete script.
  headline: How to create SVG document and export it as an image in Python
  type: TechArticle
tags:
- SVG
- Python
- graphics
title: Cách tạo tài liệu SVG và xuất nó dưới dạng hình ảnh trong Python
url: /vi/python/general/how-to-create-svg-document-and-export-it-as-an-image-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo tài liệu SVG và xuất nó thành hình ảnh trong Python

Nếu bạn cần **create SVG document** một cách lập trình, hướng dẫn này sẽ chỉ cho bạn cách thực hiện bằng Python. Bạn sẽ thấy một script hoàn chỉnh tạo một vòng tròn đơn giản, lưu SVG vào tệp và tạo ra một hình ảnh SVG có thể xuất ra để nhúng ở bất kỳ đâu.

Việc tạo đồ họa vector có thể mở rộng từ mã nguồn loại bỏ công việc vẽ thủ công trong trình chỉnh sửa GUI. Khi kết thúc hướng dẫn này, bạn có thể tích hợp việc tạo SVG vào các pipeline trực quan hoá dữ liệu, trình tạo báo cáo tự động, hoặc bất kỳ dự án nào cần đồ họa sắc nét, độc lập độ phân giải.

## Yêu cầu trước

- Python 3.8 hoặc mới hơn đã được cài đặt
- Thư viện `svgwrite` (cài đặt bằng `pip install svgwrite`)
- Quyền ghi vào thư mục nơi SVG sẽ được lưu

Các yêu cầu này giúp ví dụ nhẹ và tương thích với hầu hết các môi trường.

## Bước 1: Cài đặt và import thư viện SVG

Bước đầu tiên là thêm thư viện bên thứ ba cung cấp API tiện lợi cho việc tạo SVG.

```python
# Install the library (run once in your terminal)
# pip install svgwrite

import svgwrite  # Provides the SVGDocument class and element helpers
```

`svgwrite` trừu tượng hoá cấu trúc XML của tệp SVG, cho phép bạn tập trung vào hình học thay vì markup thô.

## Bước 2: Tạo đối tượng tài liệu SVG

Bây giờ bạn có thể **create SVG document** bằng cách khởi tạo `svgwrite.Drawing`. Đối tượng này đại diện cho phần tử gốc `<svg>` và chứa tất cả các hình dạng tiếp theo.

```python
# Step 2: Initialize the SVG document
dwg = svgwrite.Drawing(
    filename="circle.svg",     # Desired output file name
    size=("100px", "100px"),   # Width and height of the canvas
    viewBox=("0 0 100 100")    # Coordinate system for drawing
)
```

Tham số `size` xác định kích thước pixel khi render, trong khi `viewBox` thiết lập hệ tọa độ phù hợp với hình học bạn sẽ định nghĩa sau.

## Bước 3: Thêm phần tử vòng tròn

Một vòng tròn được định nghĩa bởi tâm (`cx`, `cy`) và bán kính (`r`). Sử dụng hàm trợ giúp `circle` để gán các thuộc tính này.

```python
# Step 3: Create a <circle> element
circle = dwg.circle(
    center=("50", "50"),   # cx = 50, cy = 50
    r="40",                # radius = 40
    fill="lightcoral",     # Fill color for visual clarity
    stroke="black",        # Outline color
    stroke_width="2"
)

# Append the circle to the SVG root
dwg.add(circle)
```

Vòng tròn nằm ở giữa canvas 100 × 100, để lại lề 10 pixel ở mỗi phía. Điều chỉnh `fill` và `stroke` để phù hợp với ngôn ngữ thiết kế của bạn.

## Bước 4: Lưu SVG vào tệp

Sau khi đồ họa được lắp ráp, bạn có thể **save SVG to file** bằng phương thức `save`. Điều này ghi ra XML chuẩn mà trình duyệt và trình chỉnh sửa vector hiểu.

```python
# Step 4: Persist the SVG document
dwg.save()
print("SVG file saved as circle.svg")
```

Tệp `circle.svg` hiện đã nằm trong thư mục làm việc hiện tại. Bạn có thể mở nó trong trình duyệt web, Inkscape, hoặc bất kỳ công cụ nào hỗ trợ định dạng SVG.

## Bước 5: Xác minh hình ảnh SVG đã xuất

Mở tệp đã lưu trong trình duyệt để xác nhận kết quả. Bạn sẽ thấy một vòng tròn ở trung tâm với các màu đã chỉ định. XML thô trông như sau:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg width="100px" height="100px" viewBox="0 0 100 100"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40"
          fill="lightcoral" stroke="black" stroke-width="2"/>
</svg>
```

Vì SVG dựa trên vector, bạn có thể phóng to hình ảnh mà không mất chất lượng, làm cho nó lý tưởng cho thiết kế web đáp ứng hoặc in ấn độ phân giải cao.

## Mẹo chuyên nghiệp: Xuất SVG thành PNG hoặc JPEG

Nếu bạn cần phiên bản raster, kết hợp tệp SVG với công cụ chuyển đổi như **CairoSVG**:

```python
# Optional: Convert SVG to PNG
# pip install cairosvg
import cairosvg

cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

Bước này minh họa **export SVG image** sang định dạng bitmap, hữu ích khi các hệ thống downstream không thể render SVG trực tiếp.

## Các biến thể phổ biến và trường hợp đặc biệt

| Variation | How to handle |
|-----------|---------------|
| Nhiều hình dạng | Gọi `dwg.add()` cho mỗi phần tử mới (rect, line, path). |
| Kích thước động | Tính toán `size` và `viewBox` từ dữ liệu trước khi tạo `Drawing`. |
| Nhãn văn bản | Sử dụng `dwg.text("Label", insert=("10", "20"))` và định dạng bằng `font_size` và `fill`. |
| Tái sử dụng tài liệu | Giữ đối tượng `Drawing` trong bộ nhớ và gọi `save()` mỗi khi bạn cần một tệp cập nhật. |
| Tệp lớn | Phát luồng đầu ra bằng `dwg.tostring()` và ghi vào đối tượng tệp một cách thủ công để tránh tăng đột biến bộ nhớ. |

Việc xử lý các kịch bản này đảm bảo script **how to generate SVG** của bạn mở rộng từ các biểu tượng đơn giản đến các sơ đồ phức tạp.

## Tóm tắt toàn bộ script

Dưới đây là ví dụ đầy đủ, có thể chạy được, bao gồm tất cả các bước và chuyển đổi tùy chọn:

```python
# Full SVG creation script – create SVG document, save SVG to file, export SVG image
import svgwrite
import cairosvg  # Optional, only needed for PNG conversion

# Initialize the drawing (SVG document)
dwg = svgwrite.Drawing(
    filename="circle.svg",
    size=("100px", "100px"),
    viewBox=("0 0 100 100")
)

# Define a circle element
circle = dwg.circle(
    center=("50", "50"),
    r="40",
    fill="lightcoral",
    stroke="black",
    stroke_width="2"
)

# Add the circle to the document
dwg.add(circle)

# Save the SVG file
dwg.save()
print("SVG file saved as circle.svg")

# Optional: convert SVG to PNG (export SVG image)
cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

## Kết luận

Bây giờ bạn đã biết cách **create SVG document** trong Python, **save SVG to file**, và **export SVG image** để sử dụng rộng rãi hơn. Ví dụ này bao gồm các lời gọi API thiết yếu, giải thích lý do mỗi bước quan trọng, và cung cấp các mở rộng cho đồ họa phức tạp hơn.

Tiếp theo, khám phá các chủ đề **SVG Python tutorial** bổ sung như vẽ đường dẫn, áp dụng gradient, và tạo hoạt ảnh cho các phần tử. Kết hợp những kỹ thuật này sẽ cho phép bạn tạo đồ họa vector động, dựa trên dữ liệu trực tiếp từ các ứng dụng Python của mình. Chúc lập trình vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}