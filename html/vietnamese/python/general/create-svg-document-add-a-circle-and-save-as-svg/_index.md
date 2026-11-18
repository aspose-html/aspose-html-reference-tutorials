---
category: general
date: 2026-07-31
description: Học cách tạo tài liệu SVG, thêm một vòng tròn và lưu tệp SVG nhanh chóng.
  Xuất đồ họa dưới dạng SVG chỉ với vài dòng mã Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg document
- save svg file
- export graphic as svg
- add circle to svg
language: vi
lastmod: 2026-07-31
og_description: Tạo tài liệu SVG, thêm một vòng tròn và lưu tệp SVG trong vài giây.
  Hướng dẫn này cho bạn cách xuất đồ họa dưới dạng SVG với mã rõ ràng, có thể chạy
  được.
og_image_alt: Screenshot of a red circle inside an SVG file named circle.svg
og_title: Tạo tài liệu SVG – Thêm một vòng tròn và lưu dưới dạng SVG
schemas:
- author: Aspose
  dateModified: '2026-07-31'
  description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  headline: Create SVG Document – Add a Circle and Save as SVG
  type: TechArticle
- description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  name: Create SVG Document – Add a Circle and Save as SVG
  steps:
  - name: Pro tip
    text: If you plan to generate many files in a loop, give each `Drawing` a unique
      name or use `io.BytesIO` to keep everything in memory until you’re ready to
      write.
  - name: Edge case – Transparent background
    text: 'If you need a transparent background (the default for SVG), you can skip
      setting a `fill` on the root. For a white background, add:'
  - name: 'Bonus: Export graphic as SVG programmatically'
    text: 'If you need the SVG content as a string—for example, to embed it in an
      HTML email—you can call `dwg.tostring()` instead of `save()`:'
  type: HowTo
- questions:
  - answer: Swap `dwg.circle` for `dwg.rect`, `dwg.ellipse`, or even a custom `<path>`
      string. The API is consistent across shapes.
    question: What if I want a different shape?
  - answer: Absolutely. The file you just created can be referenced with `<img src="circle.svg"
      alt="Red circle">` or inlined with `<svg>` tags.
    question: Can I embed the SVG directly in HTML?
  - answer: You could, but libraries like `svgwrite` handle namespace quirks and make
      the code far more maintainable—especially when you start adding gradients or
      animations.
    question: Why not write raw XML?
  type: FAQPage
tags:
- svg
- python
- vector-graphics
- programming-tutorial
title: Tạo tài liệu SVG – Thêm một vòng tròn và lưu dưới dạng SVG
url: /vi/python/general/create-svg-document-add-a-circle-and-save-as-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Tài liệu SVG – Thêm Hình Tròn và Lưu dưới dạng SVG

Bạn đã bao giờ cần **create SVG document** từ mã nhưng không chắc bắt đầu từ đâu? Bạn không phải là người duy nhất; nhiều nhà phát triển gặp khó khăn này khi lần đầu tiên làm việc với đồ họa vector. Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ nhỏ, tự chứa, cho bạn thấy cách **add circle to SVG**, sau đó **save SVG file** để bạn có thể **export graphic as SVG** để sử dụng trên web hoặc trong các công cụ thiết kế.

Chúng ta sẽ giữ mọi thứ nhẹ nhàng: chỉ vài dòng Python, một thư viện trợ giúp SVG phổ biến, và một chút giải thích. Khi kết thúc, bạn sẽ có một tệp `circle.svg` sẵn sàng sử dụng trong thư mục của mình, và bạn sẽ hiểu tại sao mỗi bước quan trọng — không có các lối tắt mơ hồ “xem tài liệu”.

## Những gì bạn cần

- Python 3.8+ (bất kỳ phiên bản gần đây nào cũng hoạt động)
- Gói `svgwrite` – cài đặt bằng `pip install svgwrite`
- Trình soạn thảo văn bản hoặc IDE (VS Code, PyCharm, hoặc thậm chí Notepad cũng được)
- Quyền ghi vào thư mục nơi bạn muốn lưu tệp

Chỉ vậy. Không có phụ thuộc nặng, không có dịch vụ bên ngoài.

## Bước 1: Thiết lập Tài liệu SVG

Tạo một tài liệu SVG đơn giản như việc khởi tạo một đối tượng `Drawing` từ `svgwrite`. Hãy nghĩ đối tượng này như một canvas trống nơi mọi hình dạng tồn tại.

```python
import svgwrite

# Step 1: Create a new SVG document (canvas) 800×800 pixels
dwg = svgwrite.Drawing(filename="circle.svg", size=("200px", "200px"))
```

> **Tại sao điều này quan trọng:** Lớp `Drawing` xử lý toàn bộ phần đầu XML cho bạn — không gian tên, tiêu đề và phần tử gốc `<svg>`. Bằng cách chỉ định tên tệp ngay từ đầu, chúng ta đã biết tệp sẽ được lưu ở đâu, điều này làm cho bước **save svg file** sau này trở nên đơn giản.

### Mẹo chuyên nghiệp
Nếu bạn dự định tạo nhiều tệp trong một vòng lặp, hãy đặt cho mỗi `Drawing` một tên duy nhất hoặc sử dụng `io.BytesIO` để giữ mọi thứ trong bộ nhớ cho đến khi bạn sẵn sàng ghi.

## Bước 2: Thêm Hình Tròn vào SVG

Bây giờ tài liệu đã tồn tại, chúng ta hãy **add circle to SVG**. Phương thức `add()` chấp nhận bất kỳ đối tượng hình dạng nào; một `Circle` là lựa chọn hoàn hảo cho một chấm đỏ đơn giản ở trung tâm.

```python
# Step 2: Add a red circle element to the SVG root
center = (100, 100)          # x, y coordinates (half of 200px canvas)
radius = 80                  # radius in pixels
circle = dwg.circle(center=center, r=radius, fill='red')
dwg.add(circle)
```

> **Tại sao chúng ta sử dụng các biến `center` và `radius`:** Việc mã hoá cứng các số làm cho mã khó đọc và bảo trì. Bằng cách đặt tên cho các giá trị, chúng ta làm rõ ý định — hình tròn này nằm ngay chính giữa canvas 200 × 200 và đủ lớn để dễ nhận thấy.

### Trường hợp đặc biệt – Nền trong suốt
Nếu bạn cần nền trong suốt (mặc định cho SVG), bạn có thể bỏ qua việc đặt `fill` trên phần tử gốc. Đối với nền trắng, hãy thêm:

```python
dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))
```

Đặt đoạn này trước khi thêm hình tròn để hình chữ nhật nằm phía dưới.

## Bước 3: Lưu Tệp SVG

Với hình dạng đã có, bước cuối cùng là **save SVG file**. Phương thức `save()` ghi XML ra đĩa, và vì chúng ta đã đặt tên tệp cho `Drawing`, một lần gọi là đủ.

```python
# Step 3: Save the SVG document to a file
dwg.save()
print("✅ circle.svg has been created in the current directory.")
```

> **Đi gì phía sau?** `svgwrite` tuần tự hoá cây phần tử thành một chuỗi, thêm khai báo XML, và ghi nó bằng mã hoá UTF‑8. Nếu thư mục đích không tồn tại, Python sẽ ném ra `FileNotFoundError`; hãy chắc chắn đường dẫn hợp lệ hoặc tạo nó bằng `os.makedirs()`.

### Thêm: Xuất đồ họa dưới dạng SVG bằng chương trình
Nếu bạn cần nội dung SVG dưới dạng chuỗi — ví dụ, để nhúng vào email HTML — bạn có thể gọi `dwg.tostring()` thay vì `save()`:

```python
svg_content = dwg.tostring()
# Now you can send svg_content over a network, store it in a DB, etc.
```

## Ví dụ Hoạt động Đầy đủ

Kết hợp tất cả lại, đây là một script hoàn chỉnh, sẵn sàng chạy:

```python
import svgwrite
import os

def create_svg_with_circle(output_path: str):
    """
    Creates an SVG file containing a single red circle.
    Parameters
    ----------
    output_path: str
        Full path where the SVG file will be saved.
    """
    # Ensure the directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Initialise the SVG document (800×800 canvas)
    dwg = svgwrite.Drawing(filename=output_path, size=("200px", "200px"))

    # Optional: add a white background rectangle
    dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))

    # Add a red circle in the centre
    center = (100, 100)
    radius = 80
    circle = dwg.circle(center=center, r=radius, fill='red')
    dwg.add(circle)

    # Save the file – this is the key step to **save svg file**
    dwg.save()
    print(f"✅ SVG saved to {output_path}")

if __name__ == "__main__":
    # Change this path to wherever you want the file
    output_file = os.path.join(os.getcwd(), "circle.svg")
    create_svg_with_circle(output_file)
```

**Kết quả mong đợi:** Sau khi chạy script, bạn sẽ thấy một tệp `circle.svg` trong cùng thư mục. Mở nó trong trình duyệt hoặc bất kỳ trình chỉnh sửa vector nào sẽ hiển thị một vòng tròn đỏ nằm ở trung tâm của một hình vuông trắng — chính xác như chúng ta đã lập trình.

## Câu hỏi Thường gặp & Những Lưu ý

- **Nếu tôi muốn một hình dạng khác?** Thay `dwg.circle` bằng `dwg.rect`, `dwg.ellipse`, hoặc thậm chí một chuỗi `<path>` tùy chỉnh. API nhất quán giữa các hình dạng.
- **Tôi có thể nhúng SVG trực tiếp trong HTML không?** Chắc chắn. Tệp bạn vừa tạo có thể được tham chiếu bằng `<img src="circle.svg" alt="Red circle">` hoặc nhúng trực tiếp bằng thẻ `<svg>`.
- **Tại sao không viết XML thô?** Bạn có thể, nhưng các thư viện như `svgwrite` xử lý các quirks của namespace và làm cho mã dễ bảo trì hơn rất nhiều — đặc biệt khi bạn bắt đầu thêm gradient hoặc hoạt ảnh.

## Kết luận

Bây giờ bạn đã biết cách **create SVG document**, **add circle to SVG**, và **save SVG file** để bạn có thể **export graphic as SVG** chỉ với một vài dòng Python. Mô hình này có thể mở rộng: thay thế hình tròn bằng bất kỳ hình vector nào, lặp qua dữ liệu để tạo biểu đồ, hoặc xử lý hàng loạt tài sản cho hệ thống thiết kế.

Bước tiếp theo? Hãy thử thêm nhãn văn bản, thử nghiệm gradient, hoặc tạo một bộ sưu tập biểu tượng trong một script duy nhất. Nếu bạn muốn khám phá các tính năng nâng cao hơn, hãy xem tài liệu `svgwrite` về nhóm (`<g>`), biến đổi và hỗ trợ hoạt ảnh.

Chúc lập trình vui vẻ, và hy vọng các vector của bạn luôn sắc nét!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}