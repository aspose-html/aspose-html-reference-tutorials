---
category: general
date: 2026-09-07
description: 如何使用 Java 将模板转换为 HTML。学习从模板生成 HTML，启用 foreach 循环，并查看完整的 Java 模板引擎示例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to convert template
- generate html from template
- how to use foreach
- java template engine example
- convert html template
language: zh
lastmod: 2026-09-07
og_description: 如何使用 Java 将模板转换为 HTML。本教程展示了完整的 Java 模板引擎示例，如何从模板生成 HTML，以及如何使用 foreach。
og_image_alt: Screenshot showing the resulting HTML file after template conversion
og_title: 使用 Java 将模板转换为 HTML 的逐步指南
schemas:
- author: Aspose
  dateModified: '2026-09-07'
  description: How to convert template to HTML using Java. Learn to generate HTML
    from a template, enable foreach loops, and see a full java template engine example.
  headline: How to convert template to HTML with a Java template engine
  type: TechArticle
- description: How to convert template to HTML using Java. Learn to generate HTML
    from a template, enable foreach loops, and see a full java template engine example.
  name: How to convert template to HTML with a Java template engine
  steps:
  - name: Reads `template.html` into memory.
    text: Reads `template.html` into memory.
  - name: Substitutes each `{{key}}` with the corresponding value from `data`.
    text: Substitutes each `{{key}}` with the corresponding value from `data`.
  - name: Processes any enabled foreach blocks.
    text: Processes any enabled foreach blocks.
  - name: Writes the transformed content to `resultPath`.
    text: Writes the transformed content to `resultPath`.
  type: HowTo
tags:
- Java
- template engine
- HTML generation
title: 如何使用 Java 模板引擎将模板转换为 HTML
url: /zh/java/creating-managing-html-documents/how-to-convert-template-to-html-with-a-java-template-engine/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Java 模板引擎将模板转换为 HTML

如果您需要 **将模板转换为** 可直接提供的 HTML 页面，本指南提供完整的解决方案。您将看到如何 **从模板生成 HTML**，以及如何使用 **foreach 循环**，并通过一个 **Java 模板引擎示例** 来处理 XML 或 JSON 数据源。

本教程涵盖了在单个 Java 程序中 **转换 html 模板** 文件所需的全部内容。完成后，您将拥有一个可运行的项目，能够读取模板、注入数据并将最终的 HTML 文件写入磁盘。

## 前置条件

在开始之前，请确保您拥有：

* 已安装 JDK 17 或更高版本  
* Maven 或 Gradle 等构建工具（代码仅使用标准 Java 类）  
* 对 Java I/O 以及 XML/JSON 格式有基本了解  

核心步骤不需要外部库，但如果您愿意，也可以将简单的 `Template` 类替换为第三方引擎。

## 第一步：设置文件路径和模板标记

第一步定义模板、数据源和输出文件所在的位置。模板中包含 `{{...}}` 占位符，引擎将在运行时替换它们。

```java
// Step 1: Define paths to the template, data source, and output file
String templatePath = "src/main/resources/template.html";   // contains {{...}} expressions
String dataPath     = "src/main/resources/data.xml";        // can also be a JSON file
String resultPath   = "src/main/resources/result.html";
```

*为什么重要*：硬编码路径可以让您在任何 IDE 中运行程序而无需额外配置。您也可以将这些值作为命令行参数传入，以获得更大的灵活性。

## 第二步：加载数据源（XML 或 JSON）

引擎需要一个数据对象，将占位符名称映射到对应的值。`TemplateData` 类抽象了 XML 和 JSON 的解析过程。

```java
// Step 2: Load the data source (XML or JSON) that will fill the template
TemplateData data = new TemplateData(dataPath);
```

如果 `dataPath` 指向 JSON 文件，`TemplateData` 会自动检测格式并构建相同的键/值映射。这种灵活性在不同环境下 **从模板生成 html** 时非常有用。

## 第三步：启用 foreach 指令以实现循环

许多模板需要对集合中的每个项目重复一段块。启用 foreach 指令后，引擎会处理 `{{#foreach items}} … {{/foreach}}` 块。

```java
// Step 3: Enable the foreach directive to allow loop constructs in the template
TemplateLoadOptions loadOptions = new TemplateLoadOptions();
loadOptions.setEnableForeachDirective(true);
```

**如何使用 foreach**：在 `template.html` 中可以这样写：

```html
<ul>
{{#foreach products}}
  <li>{{name}} – ${{price}}</li>
{{/foreach}}
</ul>
```

当引擎遇到该块时，会为 `TemplateData` 提供的 `products` 集合中的每个条目重复 `<li>` 元素。

## 第四步：转换模板并写入结果

现在，引擎会用实际值替换所有标记，并将最终的 HTML 文件写入磁盘。

```java
// Step 4: Convert the template – replace markers with data values and save the result
Template.convertTemplate(templatePath, data, loadOptions, resultPath);
```

`convertTemplate` 方法执行以下三项操作：

1. 将 `template.html` 读取到内存中。  
2. 用 `data` 中对应的值替换每个 `{{key}}`。  
3. 处理所有已启用的 foreach 块。  
4. 将转换后的内容写入 `resultPath`。

## 第五步：运行程序并验证输出

最后，向用户提示转换已成功完成。

```java
// Step 5: Inform that the conversion has finished
System.out.println("Template conversion completed: " + resultPath);
```

执行 `main` 方法后，您应该在控制台看到类似如下的行：

```
Template conversion completed: src/main/resources/result.html
```

在浏览器中打开 `result.html`。所有占位符都会被替换，foreach 循环也会生成相应的 HTML 片段。

### 预期输出示例

给定一个简单的 `template.html`：

```html
<h1>{{title}}</h1>
<p>{{description}}</p>

<ul>
{{#foreach items}}
  <li>{{name}} – {{quantity}}</li>
{{/foreach}}
</ul>
```

以及一个 XML `data.xml`：

```xml
<root>
  <title>Shopping List</title>
  <description>Items you need to buy</description>
  <items>
    <item><name>Apples</name><quantity>4</quantity></item>
    <item><name>Bread</name><quantity>1</quantity></item>
    <item><name>Milk</name><quantity>2</quantity></item>
  </items>
</root>
```

生成的 `result.html` 将会是：

```html
<h1>Shopping List</h1>
<p>Items you need to buy</p>

<ul>

  <li>Apples – 4</li>

  <li>Bread – 1</li>

  <li>Milk – 2</li>

</ul>
```

## 边缘情况与最佳实践提示

* **缺失占位符** – 引擎会保留未知的 `{{key}}` 标记不变。您可以添加一个验证步骤，扫描模板中剩余的花括号并记录警告。  
* **大数据集** – 对于成千上万的条目，考虑流式读取模板，而不是一次性加载整个文件到内存。当前实现对普通网页已足够。  
* **JSON 与 XML** – 如果切换为 JSON，保持相同的结构：

  ```json
  {
    "title": "Shopping List",
    "description": "Items you need to buy",
    "items": [
      {"name": "Apples", "quantity": 4},
      {"name": "Bread", "quantity": 1},
      {"name": "Milk", "quantity": 2}
    ]
  }
  ```

  `TemplateData` 会自动解析，代码其余部分保持不变。  

* **编码** – 确保模板和数据文件均使用 UTF‑8 编码，以避免字符损坏，尤其是在生成多语言 HTML 时。  

* **安全性** – 不要直接将用户提供的数据注入 HTML 而不进行清理。若数据可能包含标记，请对 HTML 特殊字符进行转义。

## 完整可运行示例

下面是一个自包含的 Java 类，演示了所有步骤的组合。将其保存为 `TemplateConverter.java`，然后在 IDE 或命令行中运行。

```java
import java.io.*;
import java.nio.file.*;
import java.util.*;
import javax.xml.parsers.*;
import org.w3c.dom.*;
import com.fasterxml.jackson.databind.*;
import com.fasterxml.jackson.core.type.TypeReference;

/**
 * Demonstrates how to convert template to HTML using a simple Java template engine.
 */
public class TemplateConverter {

    public static void main(String[] args) throws Exception {
        // Step 1: Define paths
        String templatePath = "src/main/resources/template.html";
        String dataPath     = "src/main/resources/data.xml";
        String resultPath   = "src/main/resources/result.html";

        // Step 2: Load data (XML or JSON)
        TemplateData data = new TemplateData(dataPath);

        // Step 3: Enable foreach loops
        TemplateLoadOptions loadOptions = new TemplateLoadOptions();
        loadOptions.setEnableForeachDirective(true);

        // Step 4: Perform conversion
        Template.convertTemplate(templatePath, data, loadOptions, resultPath);

        // Step 5: Notify user
        System.out.println("Template conversion completed: " + resultPath);
    }
}

/**
 * Holds key/value pairs loaded from XML or JSON.
 */
class TemplateData {
    private final Map<String, Object> map = new HashMap<>();

    public TemplateData(String path) throws Exception {
        if (path.endsWith(".json")) {
            loadJson(path);
        } else if (path.endsWith(".xml")) {
            loadXml(path);
        } else {
            throw new IllegalArgumentException("Unsupported data format: " + path);
        }
    }

    private void loadJson(String path) throws IOException {
        ObjectMapper mapper = new ObjectMapper();
        Map<String, Object> jsonMap = mapper.readValue(
                Files.readAllBytes(Paths.get(path)),
                new TypeReference<Map<String, Object>>() {});
        map.putAll(jsonMap);
    }

    private void loadXml(String path) throws Exception {
        DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
        DocumentBuilder builder = factory.newDocumentBuilder();
        Document doc = builder.parse(new File(path));
        doc.getDocumentElement().normalize();
        traverseNode(doc.getDocumentElement(), "");
    }

    private void traverseNode(Node node, String prefix) {
        NodeList children = node.getChildNodes();
        for (int i = 0; i < children.getLength(); i++) {
            Node child = children.item(i);
            if (child.getNodeType() == Node.ELEMENT_NODE) {
                String key = prefix.isEmpty() ? child.getNodeName() : prefix + "." + child.getNodeName();
                if (child.hasChildNodes() && child.getFirstChild().getNodeType() == Node.ELEMENT_NODE) {
                    // Nested element – recurse
                    traverseNode(child, key);
                } else {
                    map.put(key, child.getTextContent().trim());
                }
            }
        }
    }

    public Object get(String key) {
        return map.get(key);
    }

    public Map<String, Object> getAll() {
        return map;
    }
}

/**
 * Options that control how the template is loaded.
 */
class TemplateLoadOptions {
    private boolean enableForeachDirective = false;

    public void setEnableForeachDirective(boolean enable) {
        this.enableForeachDirective = enable;
    }

    public boolean isForeachEnabled() {
        return enableForeachDirective;
    }
}

/**
 * Core engine that performs placeholder replacement and foreach processing.
 */
class Template {
    public static void convertTemplate(String templatePath,
                                       TemplateData data,
                                       Template


## 接下来应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助您在项目中进一步掌握 API 功能并探索替代实现方式。每个资源均提供完整的可运行代码示例和逐步说明。

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Convert HTML to String using Aspose.HTML for Java](/html/english/java/editing-html-documents/manage-inner-outer-html-properties/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}