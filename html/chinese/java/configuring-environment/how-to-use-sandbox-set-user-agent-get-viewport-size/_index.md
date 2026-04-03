---
category: general
date: 2026-04-03
description: 学习如何在 Aspose.HTML Java 中使用 sandbox 设置用户代理、设定尺寸，并即时获取视口大小。完整代码、说明和技巧均已包含。
draft: false
keywords:
- how to use sandbox
- set user agent
- get viewport size
- how to set size
- how to get viewport
language: zh
og_description: 了解如何在 Aspose.HTML Java 中使用 sandbox 设置用户代理、设置尺寸，并即时获取视口大小。完整指南，附代码和最佳实践。
og_title: 如何使用沙盒 – 设置用户代理并获取视口尺寸
tags:
- AsposeHTML
- Java
- Sandbox
title: 如何使用沙盒 – 设置用户代理并获取视口尺寸
url: /zh/java/configuring-environment/how-to-use-sandbox-set-user-agent-get-viewport-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Sandbox – 设置 User Agent 并获取视口大小

是否曾经想过在使用 Aspose.HTML for Java 渲染 HTML 时 **如何使用 sandbox**？也许你在尝试模拟特定屏幕尺寸时遇到了瓶颈，或者需要伪造一个 user‑agent 字符串，使页面表现得像是从移动浏览器访问一样。  

好消息是 sandbox API 正好可以做到这些，并且在页面加载后还能获取计算得到的视口大小。在本教程中，我们将逐步演示创建 sandbox、设置尺寸、设置自定义 user agent、加载远程页面，最后读取视口尺寸。结束时，你将掌握 **如何设置尺寸**、**如何获取视口**，以及这些步骤为何对可靠的无头渲染至关重要。

> **快速收获：** 您将在几秒钟内拥有一个可运行的 Java 类，打印类似 `Viewport: 1280×800` 的结果。

---

## 您需要的条件

- **Aspose.HTML for Java** version 24.6 或更新（我们使用的 API 在 24.5 中首次引入）。  
- Java 17+ 开发工具包（任何近期的 JDK 都可）。  
- IDE 或简单的文本编辑器——无需特殊插件。  
- 如果想加载外部 URL（如 `https://example.com`），需要网络访问。

就这些。并不强制使用 Maven/Gradle；如果愿意，也可以手动将 JAR 放入 classpath。

---

## 如何使用 Sandbox – 概览

sandbox 将渲染引擎与宿主操作系统隔离，使你能够定义虚拟屏幕（宽度、高度、DPI）以及自定义 **user agent** 字符串。可以把它想象成完全驻留在内存中的微型浏览器窗口。当你随后请求 `HTMLDocument` 的默认视图时，引擎会报告基于 sandbox 设置计算得到的 **视口大小**。  

下面是高级流程：

1. **Create** a `DocumentSandbox` and configure width, height, DPI, and user‑agent.  
2. **Load** an `HTMLDocument` inside that sandbox.  
3. **Query** the document’s default view for the viewport size.  

下面逐步展开每个步骤。

---

## 步骤 1：创建 Sandbox 并设置尺寸

首先，启动一个 sandbox 并告诉它虚拟屏幕的大小。这正是 **如何设置尺寸** 以进行无头渲染的关键。

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.drawing.Size2D;

/* Step 1 – instantiate the sandbox */
DocumentSandbox sandbox = new DocumentSandbox();

/* Set the virtual screen width & height (in pixels) */
sandbox.setScreenWidth(1280);   // width in pixels
sandbox.setScreenHeight(800);   // height in pixels

/* DPI influences CSS pixel calculations – 96 is the CSS default */
sandbox.setDeviceDpi(96);

/* Optional: give the sandbox a friendly name for debugging */
sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");
```

> **Pro tip:** 如果你在测试响应式布局，尝试使用 `360` 的窄宽度来模拟手机，或使用 `1920` 的宽度来模拟桌面。sandbox 会遵循你设置的 DPI，因此高密度屏幕（例如 144 DPI）会影响使用 `device-pixel-ratio` 的媒体查询。

---

## 步骤 2：为 Sandbox 设置 User Agent

为什么要自定义 **user agent**？有些站点会根据报告的浏览器返回不同的标记或脚本。通过调用 `setUserAgent`，你可以让页面误以为是 Chrome、Firefox 或移动设备在访问。

```java
/* Step 2 – customize the user‑agent string */
sandbox.setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                     "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                     "Version/15.0 Mobile/15E148 Safari/604.1");
```

现在页面会认为它正在 iPhone 上渲染。如果需要 **set user agent** 回默认，只需再次使用前面的 “AsposeHTML/24.6 …” 字符串即可。

---

## 步骤 3：在 Sandbox 中加载 HTML 文档

Sandbox 准备好后，我们可以加载任意 URL 或本地 HTML 文件。`HTMLDocument` 构造函数接受 sandbox 作为第二个参数，将两者绑定在一起。

```java
import com.aspose.html.HTMLDocument;

/* Step 3 – load the page using the configured sandbox */
try (HTMLDocument doc = new HTMLDocument("https://example.com", sandbox)) {
    // The document is now rendered inside the sandbox environment.
    // Any JavaScript or CSS will see the size and user‑agent we defined.
```

`try‑with‑resources` 代码块确保文档能够正确释放，释放 Aspose.HTML 在底层分配的本机资源。

---

## 步骤 4：从文档获取视口尺寸

下面就是你一直期待的时刻：检索渲染引擎计算出的 **视口尺寸**。这回答了 **如何获取视口** 在页面布局完成后的问题。

```java
    /* Step 4 – fetch the viewport dimensions */
    Size2D viewport = doc.getDefaultView().getScreenSize();
    System.out.println("Viewport: " + viewport.getWidth() + "×" + viewport.getHeight());
}
```

运行程序后，你应该会看到类似下面的输出：

```
Viewport: 1280×800
```

如果在步骤 1 中更改了 sandbox 的尺寸，打印的数字将反映新的值——这对于验证响应式断点的自动化测试非常理想。

---

## 完整工作示例

下面是完整的、可直接运行的类，整合了所有步骤。将其复制粘贴到名为 `SandboxExample.java` 的文件中，添加 Aspose.HTML JAR 到 classpath，然后执行 `java SandboxExample`。

```java
import com.aspose.html.*;
import com.aspose.html.drawing.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox with a custom screen size and DPI
        DocumentSandbox sandbox = new DocumentSandbox();
        sandbox.setScreenWidth(1280);          // width in pixels
        sandbox.setScreenHeight(800);          // height in pixels
        sandbox.setDeviceDpi(96);              // screen DPI
        sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");

        // Step 2: (Optional) Override the user agent if you need a mobile profile
        sandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
            "Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 3: Load the HTML document inside the configured sandbox
        try (HTMLDocument htmlDocument = new HTMLDocument("https://example.com", sandbox)) {

            // Step 4: Retrieve and display the computed viewport size
            Size2D viewportSize = htmlDocument.getDefaultView().getScreenSize();
            System.out.println("Viewport: " + viewportSize.getWidth() + "×" + viewportSize.getHeight());
        }
    }
}
```

**预期输出**（假设使用上述 sandbox 设置）：

```
Viewport: 1280×800
```

如果在 sandbox 中设置了不同的宽度/高度，输出会相应变化——这正是测试响应式设计时所需要的。

---

## 边缘情况与常见问题

### 如果页面使用 `window.innerWidth` 而不是 CSS 媒体查询怎么办？

sandbox 的虚拟屏幕尺寸会同时影响 CSS 布局和 JavaScript 的 `window.innerWidth/innerHeight`。因此通过 JavaScript 获取的 **视口** 与 Java 控制台中看到的数字相同。

### 我可以并行运行多个 sandbox 吗？

可以。每个 `DocumentSandbox` 实例都是独立的，你可以创建线程池，为每个线程分配不同尺寸的 sandbox 并并发渲染多个页面。只需确保 JAR 本身是线程安全的（它们已经是）。

### DPI 设置会影响图像缩放吗？

当然会。更高的 DPI 会让一个 CSS 像素映射到更多的设备像素，从而使高分辨率图像看起来更清晰。如果在测试 Retina 风格的资源，尝试 `sandbox.setDeviceDpi(144)`。

### 如何处理自签名的 HTTPS 证书？

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}