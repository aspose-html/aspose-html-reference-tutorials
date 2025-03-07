---
title: Apply External CSS to HTML Documents in Aspose.HTML for Java
linktitle: Apply External CSS to HTML Documents in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
description: Discover how to apply external CSS to HTML documents using Aspose.HTML for Java! Follow this step-by-step guide for a complete tutorial.
weight: 12
url: /java/editing-html-documents/apply-external-css-html-documents/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Apply External CSS to HTML Documents in Aspose.HTML for Java

## Introduction
When working with HTML documents, applying styles can make all the difference in presentation and user experience. If you’re diving into Java and want to learn how to apply external CSS styles to your HTML documents using the Aspose.HTML library, you’re in the right place! This guide aims to illuminate the process step-by-step, making it easy even for those who might be new to Java or CSS.
## Prerequisites
Before diving into the code, there are a few things you’ll need to have in place:
### 1. Java Development Kit (JDK)
Ensure that you have JDK installed on your machine. You can download the latest version from [Oracle’s Java website](https://www.oracle.com/java/technologies/javase-downloads.html).
### 2. Aspose.HTML for Java
You’ll need to have Aspose.HTML for Java set up. If you haven’t done this yet, head over to the [Aspose downloads page](https://releases.aspose.com/html/java/) and grab the library.
### 3. An IDE or Text Editor
Choose an Integrated Development Environment (IDE) like IntelliJ IDEA, Eclipse, or even a simple text editor to write your Java code.
### 4. Basic Knowledge of Java
Familiarity with Java programming and CSS basics will certainly help you follow along more comfortably.
## Import Packages
Once you have everything set up, the next step is to import the necessary packages in your Java project. Here’s what you need:
```java
import com.aspose.html.HTMLDocument;
```
These imports will allow you to manipulate HTML documents and render them into different formats, such as PDF.

We’ll break down our tutorial into manageable steps. Each step will guide you through the process of applying external CSS styles to an HTML document using Aspose.HTML for Java.
## Step 1: Create an HTML Document
First off, we need to create our HTML document. We’ll start by defining the content with a simple HTML structure.
```java
String content = "<div><p>Internal CSS</p><p>An internal CSS is used to define a style for a single HTML page</p></div>";
HTMLDocument document = new HTMLDocument(content, ".");
```

Here, we defined a basic HTML structure, including a `<div>` with two paragraphs. The `HTMLDocument` class is used to create a document representation of our HTML content.
## Step 2: Create a Style Element
Next, we will create a `style` element to hold our CSS rules.
```java
Element style = document.createElement("style");
style.setTextContent(".frame1 { margin-top:50px; margin-left:50px; padding:20px; width:360px; height:90px; background-color:#a52a2a; font-family:verdana; color:#FFF5EE;} \n" +
        ".frame2 { margin-top:-90px; margin-left:160px; text-align:center; padding:20px; width:360px; height:100px; background-color:#ADD8E6;}");
```

Using the `createElement` method of `HTMLDocument`, we create a new `<style>` element and set its content to include our CSS definitions for two classes: `frame1` and `frame2`. These classes define margins, padding, dimensions, background colors, font families, and text colors.
## Step 3: Append the Style to the Document Header
Now that we have our CSS in place, we need to append our style element to the document's head.
```java
Element head = document.getElementsByTagName("head").get_Item(0);
head.appendChild(style);
```

We retrieve the head of the document and append our newly created `style` element. This action effectively integrates our CSS into the HTML document, allowing it to style our HTML content.
## Step 4: Apply Classes to HTML Elements
Next, we’ll apply the previously defined CSS classes to our paragraph elements.
```java
HTMLElement paragraph = (HTMLElement) document.getElementsByTagName("p").get_Item(0);
paragraph.setClassName("frame1");
HTMLElement lastParagraph = (HTMLElement) document.getElementsByTagName("p").get_Item(document.getElementsByTagName("p").getLength() - 1);
lastParagraph.setClassName("frame2");
```

Here, we access the first and last paragraph elements in the document and assign them the CSS classes we created. This assignment ensures that they adhere to the styles defined in our CSS.
## Step 5: Set Additional Style Properties
To enhance the appearance further, we’ll set additional style properties for our paragraphs.
```java
paragraph.getStyle().setFontSize("250%");
paragraph.getStyle().setTextAlign("center");
lastParagraph.getStyle().setColor("#434343");
lastParagraph.getStyle().setFontSize("150%");
lastParagraph.getStyle().setFontFamily("verdana");
```

In this step, we're fine-tuning our styles. The first paragraph's font size is increased and centered, while the last paragraph's color, font size, and font family are defined. This refinement is crucial for readability and aesthetic appeal.
## Step 6: Save the HTML Document
Once we have our styles applied, it’s time to save the HTML document.
```java
document.save("edit-internal-css.html");
```

Here, we utilize the `save` method of the `HTMLDocument` class to write the modified HTML content to a file, thus preserving our styles and changes.
## Step 7: Render the Document to PDF
Finally, let’s render the document to a PDF format for output.
```java
PdfDevice device = new PdfDevice("edit-internal-css.pdf");
document.renderTo(device);
```

Using the `PdfDevice` class, we set up the rendering of our HTML document into a PDF. This step is key when you want to share the styled document in a universally accessible format.
## Conclusion
And there you have it—applying external CSS to HTML documents using Aspose.HTML for Java is both straightforward and rewarding! With just a few lines of code, you can turn plain text into visually appealing and professionally styled documents. So, whether you’re designing for personal use, creating reports, or developing web content, understanding how to manipulate HTML and CSS in Java is a powerful skill to have in your toolkit.
## FAQ's
### What is Aspose.HTML for Java?
Aspose.HTML for Java is a powerful library that allows developers to work with HTML documents in Java applications, providing a vast range of features, from HTML manipulation to rendering.
### Do I need an Internet connection to use Aspose.HTML?
No, once you’ve downloaded the necessary library files, you can use Aspose.HTML offline.
### Can I apply multiple CSS files to an HTML document?
Yes, you can create multiple `<link>` elements and append them to the document's head for various CSS files.
### Is there a difference between internal and external CSS?
Yes! Internal CSS is defined within an HTML document, while external CSS is placed in a separate file and linked to the document.
### How can I get support for Aspose.HTML for Java?
You can access community support through the [Aspose forum](https://forum.aspose.com/c/html/29) for any questions or issues you may encounter.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
