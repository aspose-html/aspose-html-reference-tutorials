---
date: 2026-02-10
description: 学习如何使用 Aspose 处理 Java 中的损坏链接，将 HTML 转换为 PNG，并使用 Aspose.HTML for Java
  加载 HTML 文档。
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: 使用 Aspose.HTML 消息处理程序在 Java 中将 HTML 转换为 PNG
url: /zh/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.HTML 消息处理程序在 Java 中将 HTML 转换为 PNG

## 介绍
在本教程中，您将了解 **how to convert HTML to PNG**，并使用 Aspose.HTML for Java 优雅地处理缺失的资源。我们将演示如何创建一个指向不存在图像的微型 HTML 页面，连接一个 **custom message handler** 来 **intercept network requests**，配置 **network service**，加载文档，最后执行 **html to image conversion**。完成后，您将拥有一个可靠的模式，既能 **handle broken links java**，又能生成高质量的 PNG 输出——非常适合报告、缩略图或电子邮件预览。

## 快速回答
- **消息处理程序的作用是什么？** 它拦截网络操作（如图像请求），并让您对诸如 404 等状态码作出响应。  
- **Aspose.HTML 能将 HTML 转换为 PNG 吗？** 是的——`Converter.convertHTML` 在一次调用中完成转换。  
- **我需要为此示例获取许可证吗？** 临时许可证可移除评估限制；生产环境需要永久许可证。  
- **哪个 Java 版本可用？** 任何 JDK 8+（示例在 JDK 11 上运行）。  
- **我可以配置 network service 吗？** 当然可以——使用 `configuration.getService(INetworkService.class)` 添加您的处理程序。  

## 先决条件
在开始之前，请确保您已准备好以下内容：

1. **Java Development Kit (JDK)** – 从 [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html) 下载。  
2. **Aspose.HTML for Java** – 从 [Aspose releases page](https://releases.aspose.com/html/java/) 获取库。  
3. **IDE** – IntelliJ IDEA、Eclipse 或 NetBeans 都可以。  
4. **Basic Java knowledge** – 您应该熟悉类、try‑with‑resources 以及异常处理。  
5. **Temporary License** – 如果您在试用期，请获取 [temporary license](https://purchase.aspose.com/temporary-license/) 以避免水印。  

## 导入包
首先，引入我们需要的 Java I/O 类用于文件处理。其余 Aspose 类将在后面使用全限定名引用，以保持 import 列表简洁。

```java
import java.io.IOException;
```

## 步骤 1：准备 HTML 代码
我们创建一个最小的 HTML 片段，故意引用一个缺失的图像。当引擎尝试获取该资源时，将触发我们的处理程序。

```java
String code = "<img src='missing.jpg'>";
```

## 步骤 2：将 HTML 代码写入文件
接下来，我们将片段持久化为 *document.html*。使用 try‑with‑resources 块可确保 `FileWriter` 正确关闭。

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## 步骤 3：编写自定义消息处理程序
现在我们构建一个 **custom message handler**，检查每个网络请求的 HTTP 状态。如果响应不是 `200`，我们记录一条友好的警告。请注意末尾对 `invoke(context);` 的调用——它将请求转发给链中的下一个处理程序，防止递归。

```java
com.aspose.html.net.MessageHandler handler = new com.aspose.html.net.MessageHandler() {
    @Override
    public void invoke(com.aspose.html.net.INetworkOperationContext context) {
        if (context.getResponse().getStatusCode() != 200) {
            System.out.println(String.format("File '%s' Not Found", context.getRequest().getRequestUri().toString()));
        }
        invoke(context);
    }
};
```

## 步骤 4：配置网络服务
为了让 Aspose.HTML 知道我们的处理程序，我们从 `Configuration` 实例中获取 **network service** 并将处理程序添加到其集合中。这一步是我们 **configure network service** 以实现自定义行为的地方。

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## 步骤 5：加载 HTML 文档
配置就绪后，我们加载 *document.html*。引擎现在使用我们的网络服务，因此缺失的图像请求会被我们刚添加的处理程序拦截。

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Additional operations will go here
} finally {
    if (document != null) {
        document.dispose();
    }
}
```

## 步骤 6：将 HTML 转换为 PNG
以下是 **html to image conversion** 过程的核心。`Converter.convertHTML` 方法接受已加载的 `HTMLDocument`、可选的 `ImageSaveOptions`（您可以在此调整 DPI 或质量）以及输出文件名。

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## 步骤 7：清理资源
良好的 Java 实践要求我们释放所有本机资源。`finally` 块确保即使出现异常，`Configuration` 也会被释放。

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## 为什么使用消息处理程序？
消息处理程序为每个网络请求提供 **fine‑grained control**——无论是图像、CSS、JavaScript 还是字体文件。与其让库静默失败，您可以记录缺失的资源、提供回退内容，甚至重试请求。这使得您的 HTML 处理流水线 **robust**、**production‑ready**，且更易调试。

## 常见问题及解决方案
- **Handler recursion** – 只调用一次 `invoke(context);` 以避免无限循环。  
- **Missing license** – 没有有效许可证，输出的 PNG 将包含水印。  
- **Incorrect file paths** – 加载 `document.html` 时使用绝对路径或正确设置工作目录。  
- **Unsupported resource types** – 确保您想拦截的资源（图像、CSS 等）确实被 HTML 引擎请求。  

## 常见问答

**Q: 我可以链式添加多个消息处理程序吗？**  
A: 是的，您可以向 `network.getMessageHandlers()` 集合添加多个处理程序；它们会按添加顺序执行。

**Q: 处理程序也适用于 CSS 或脚本资源吗？**  
A: 当然——HTML 引擎发出的任何网络请求（图像、CSS、JS、字体）都会经过该处理程序。

**Q: 如何在发送前更改 HTTP 请求？**  
A: 实现一个在调用 `invoke(context)` 之前修改 `context.getRequest()` 的处理程序。

**Q: 是否有办法对特定 URL 抑制警告？**  
A: 在处理程序内部检查 `context.getRequest().getRequestUri()`，并有条件地跳过日志记录。

**Q: 这些 API 需要哪个版本的 Aspose.HTML？**  
A: 该代码适用于 Aspose.HTML for Java 22.10 及更高版本。

## 结论
您现在拥有一个完整的端到端示例，展示 **how to convert HTML to PNG**，并使用 **custom message handler** 来 **intercept network requests** 和 **handle broken links java**。通过配置网络服务、加载文档并调用转换器，您可以在任何 Java 应用中可靠地生成 PNG 缩略图或整页截图。

---

**最后更新：** 2026-02-10  
**测试环境：** Aspose.HTML for Java 24.11  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}