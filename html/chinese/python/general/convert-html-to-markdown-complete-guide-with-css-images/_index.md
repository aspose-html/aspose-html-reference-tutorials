---
category: general
date: 2026-06-10
description: 使用单个脚本将 HTML 转换为 Markdown，保留 CSS 和图像。一步步学习如何保留样式、外部资源，并生成干净的 Markdown。
draft: false
keywords:
- convert html to markdown
- convert html with css
- how to convert html with images
language: zh
og_description: 将 HTML 转换为 Markdown，同时保留 CSS 和图像。本指南展示完整代码，解释每个选项，并提供可直接运行的示例。
og_title: 将HTML转换为Markdown – 完整教程，包含CSS和图片
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Convert HTML to Markdown with CSS and images in a single script. Learn
    step‑by‑step how to preserve styles, external assets, and get clean Markdown.
  headline: Convert HTML to Markdown – Complete Guide with CSS & Images
  type: TechArticle
- description: Convert HTML to Markdown with CSS and images in a single script. Learn
    step‑by‑step how to preserve styles, external assets, and get clean Markdown.
  name: Convert HTML to Markdown – Complete Guide with CSS & Images
  steps:
  - name: Expected Result
    text: 'After the script finishes, you should see:'
  - name: What if my HTML uses inline `data:` URIs for images?
    text: The converter treats data URIs as embedded resources and will **not** write
      them to the `resources` folder by default. If you need them extracted, set `res_opts.inline_images
      = False` (or the library’s equivalent) before step 2.
  - name: How do I keep the original CSS file linked in the Markdown?
    text: 'After conversion, add a reference at the top of your Markdown:'
  - name: Can I convert multiple HTML files in one run?
    text: Sure. Wrap the four steps in a `for` loop, change the input and output paths
      each iteration, and reuse the same `options` object. Just make sure each HTML
      file has its own dedicated `resource_folder` to avoid collisions.
  type: HowTo
tags:
- HTML
- Markdown
- Python
title: 将HTML转换为Markdown – 包含CSS和图片的完整指南
url: /zh/python/general/convert-html-to-markdown-complete-guide-with-css-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将 HTML 转换为 Markdown – 包含 CSS 与图片的完整指南

是否曾经需要**将 HTML 转换为 Markdown**，但又担心会失去 CSS 样式或嵌入的图片？你并不是唯一遇到这种情况的人。许多开发者在尝试将网页内容迁移到用于静态站点生成器、文档或版本控制笔记的轻量级 Markdown 文件时，都会遇到这个难题。

好消息是？只需几行 Python 代码和合适的库，你就可以**将 HTML 转换为 Markdown**，同时自动复制外部资源，保留 CSS，并完整保留每张图片。在本教程中，我们将逐步演示一个实用的复制粘贴脚本，完美解决上述问题，并解释每个设置的意义。完成后，你将能够对任意 HTML 文件运行转换器，得到一个干净的 `.md` 文件以及一个包含原始资源的 `resources` 文件夹。

> **你将获得：** 一个完整可运行的 Python 示例，`resource_handling_options` 的详细拆解，处理边缘情况的技巧，以及后续步骤的建议（如微调 CSS 或处理内联 data URI）。

## 前置条件

- 在机器上安装了 Python 3.8+。  
- **Aspose.HTML for Python via .NET**（或任何提供 `HTMLDocument`、`MarkdownSaveOptions` 等的类似库）。使用以下方式安装：

```bash
pip install aspose-html
```

- 需要转换的 HTML 文件，最好包含外部 CSS 和图片引用，例如 `sample_with_images.html`。  
- 对输出目录拥有写入权限。

如果你使用的是其他库，概念保持不变——只需相应映射类名即可。

## 步骤 1：加载 HTML 文档

我们首先创建指向源文件的 `HTMLDocument` 对象。该对象会解析标记，构建 DOM，并为转换做好准备。

```python
# Step 1: Load the HTML document
doc = HTMLDocument("YOUR_DIRECTORY/sample_with_images.html")
```

*Why this matters:* 加载文档为转换器提供了页面的具体表示，包括指向外部 CSS 文件和图片标签的链接。如果没有这一步，转换器将不知道需要复制哪些资源。

## 步骤 2：配置资源处理（CSS 与图片）

接下来我们设置 `ResourceHandlingOptions`。这正是本教程中 **convert html with css** 与 **how to convert html with images** 部分的核心。通过切换 `save_external_resources` 并指定文件夹，库会自动下载每个链接的样式表、图片和字体。

```python
# Step 2: Set up resource handling to copy external assets (images, CSS, fonts)
res_opts = ResourceHandlingOptions()
res_opts.save_external_resources = True          # Enable copying of external resources
res_opts.resource_folder = "YOUR_DIRECTORY/resources"
```

*Why this matters:* 如果跳过此配置，生成的 Markdown 将出现失效链接，外部 CSS 文件中的任何样式也会丢失。启用 `save_external_resources` 可确保稍后打开 Markdown 时图片能够显示，且 CSS 如有需要可以重新附加。

## 步骤 3：将资源选项附加到 Markdown 保存选项

现在我们将资源选项绑定到 `MarkdownSaveOptions`。可以把它理解为告诉转换器：“在写入 `.md` 文件时，也遵循我们刚才定义的资源规则。”

```python
# Step 3: Attach the resource options to the Markdown save options
options = MarkdownSaveOptions()
options.resource_handling_options = res_opts
```

*Why this matters:* `MarkdownSaveOptions` 对象包含了转换过程中的所有可调参数——从标题样式到链接格式。通过插入 `resource_handling_options`，确保转换器在整个操作期间遵守资源复制行为。

## 步骤 4：运行转换

最后，调用静态的 `convert_html` 方法，传入文档、选项以及期望的输出路径。该方法会写入 Markdown 文件并在旁边创建 `resources` 文件夹。

```python
# Step 4: Convert the HTML document to Markdown, saving resources alongside the file
Converter.convert_html(doc, options, "YOUR_DIRECTORY/with_resources.md")
```

*Why this matters:* 这一行代码完成了繁重的工作——解析 HTML、将标签转换为 Markdown 语法、重写图片 URL 指向新创建的资源文件夹，并保留任何可能稍后复用的 CSS 引用。

### 预期结果

脚本执行完毕后，你应该看到：

- `with_resources.md` – 一个干净的 Markdown 文件，图片链接形如 `![Alt text](resources/image1.png)`。
- `resources/` – 一个文件夹，包含原始 HTML 所引用的所有外部 CSS 文件、图片和字体。

在任意 Markdown 查看器（VS Code、GitHub、MkDocs）中打开 `.md` 文件，你将看到原页面的内容、显示的图片，甚至可以手动链接 CSS 文件以获得带样式的渲染。

---

## 常见问题与边缘情况

### 如果我的 HTML 对图片使用了内联 `data:` URI 会怎样？

转换器将 data URI 视为嵌入式资源，默认**不会**写入 `resources` 文件夹。如果需要提取它们，请在第 2 步之前设置 `res_opts.inline_images = False`（或库的等效属性）。

### 如何在 Markdown 中保持原始 CSS 文件的链接？

转换完成后，在 Markdown 顶部添加引用：

```markdown
<link rel="stylesheet" href="resources/style.css">
```

由于我们启用了 `save_external_resources`，`style.css` 现在位于 `resources/` 中，链接即可在本地正常工作。

### 能否一次性转换多个 HTML 文件？

可以。将四个步骤包装在 `for` 循环中，每次迭代更改输入输出路径，并复用同一个 `options` 对象。只需确保每个 HTML 文件都有各自独立的 `resource_folder`，以避免冲突。

---

## 专业技巧与常见陷阱

- **Pro tip:** 为每次转换使用简短且唯一的 `resource_folder` 名称（例如 `resources_page1`），以防在批量处理多页时文件相互覆盖。
- **Watch out for:** 不同目录下引用同一 CSS 文件的 HTML 页面。转换器会在每个输出文件夹中复制一次该文件，可能导致重复副本。如磁盘空间紧张，可在转换后手动合并。
- **Performance hint:** 如果只需要图片而不需要 CSS，设置 `res_opts.save_css = False`。这会跳过不必要的文件复制，加快处理速度。

---

## 结论

现在你拥有一个完整、可直接运行的脚本，能够**convert html to markdown**，同时保留 CSS 样式和所有嵌入图片。通过配置 `ResourceHandlingOptions` 并将其插入 `MarkdownSaveOptions`，转换过程会自动处理 **convert html with css** 与 **how to convert html with images**。

欢迎随意实验：更换输出格式（例如 `MarkdownSaveOptions` → `PlainTextSaveOptions`），调整资源文件夹结构，或将脚本集成到更大的静态站点生成流水线中。显式管理外部资产的核心思路适用于任何 HTML‑to‑Markdown 工作流。

还有其他问题吗？留下评论吧，祝转换愉快！

## 接下来你应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在此基础上进一步掌握 API 功能并探索替代实现方式，每篇都提供完整可运行的代码示例和逐步解释。

- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}