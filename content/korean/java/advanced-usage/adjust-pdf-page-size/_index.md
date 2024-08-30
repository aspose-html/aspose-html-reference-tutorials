---
title: Java용 Aspose.HTML로 PDF 페이지 크기 조정
linktitle: PDF 페이지 크기 조정
second_title: Aspose.HTML을 사용한 Java HTML 처리
description: Aspose.HTML for Java로 PDF 페이지 크기를 조정하는 방법을 알아보세요. HTML에서 고품질 PDF를 손쉽게 만드세요. 페이지 크기를 효과적으로 제어하세요.
type: docs
weight: 15
url: /ko/java/advanced-usage/adjust-pdf-page-size/
---

오늘날의 디지털 시대에 HTML 콘텐츠에서 고품질 PDF를 생성해야 할 필요성이 증가하고 있습니다. Aspose.HTML for Java는 HTML 문서를 PDF 형식으로 손쉽게 변환할 수 있는 강력한 Java 라이브러리입니다. 이 튜토리얼에서는 Aspose.HTML for Java를 사용하여 HTML을 PDF로 변환할 때 페이지 크기를 조정하는 데 중점을 둡니다.

## 필수 조건

시작하기 전에 다음 전제 조건이 충족되었는지 확인하세요.

- Java 개발 환경: 시스템에 Java 개발 키트(JDK)가 설치되어 있는지 확인하세요.
-  Java용 Aspose.HTML: 웹사이트에서 Java용 Aspose.HTML을 다운로드하여 설치해야 합니다.[여기](https://releases.aspose.com/html/java/).
- HTML 문서: 변환할 HTML 문서가 준비되어 있어야 합니다. 그렇지 않은 경우, 하나를 만들거나 기존 HTML 파일을 사용합니다.

## 패키지 가져오기

시작하려면 Java용 Aspose.HTML을 사용하는 데 필요한 패키지를 가져와야 합니다. 다음 코드 조각은 이를 수행하는 방법을 보여줍니다.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

이제 필수 구성 요소를 갖추고 필요한 패키지를 가져왔으니 PDF 페이지 크기를 조정하는 과정을 여러 단계로 나누어 보겠습니다.

## 1단계: HTML 콘텐츠 읽기

먼저, PDF로 변환하려는 HTML 콘텐츠를 읽어야 합니다. 이 예에서는 "FirstFile.html"이라는 파일에서 HTML을 읽습니다.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## 2단계: HTML 콘텐츠 작성

다음으로, "FirstFileOut.html"이라는 파일에 HTML 콘텐츠를 작성합니다.

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // 여기에 사용자 정의 HTML 스타일이나 콘텐츠를 추가하세요
    String style = "<style>\n" +
                   ".st\n" +
                   "{\n" +
                   "color:\n" +
                   "green;\n" +
                   "}\n" +
                   "</style >\n" +
                   "<div id = id1 > Aspose.Html rendering Text in Black Color</div >\n" +
                   "<div id = id2 class='' st '' > Aspose.Html rendering Text in Green Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: blue;' > Aspose.Html rendering Text in Blue Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: red;' ><font face = 'Arial' > Aspose.Html rendering Text in Red\n" +
                   "Color</font ></div >\n";
    fileOutputStream.write(style.getBytes(java.nio.charset.StandardCharsets.UTF_8));
}
```

## 3단계: HTML을 PDF로 렌더링

이제 HTML 콘텐츠를 PDF 파일로 렌더링합니다. 두 가지 시나리오를 다루겠습니다. 하나는 페이지 크기가 콘텐츠 너비에 맞춰 조정되지 않은 경우이고, 다른 하나는 페이지 크기가 조정된 경우입니다.

### 페이지 크기가 조정되지 않음

이 시나리오에서는 페이지 크기가 고정된 너비와 높이로 설정되므로 해당 크기를 초과하면 콘텐츠가 잘릴 수 있습니다.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// HTML 파일에서 HTMLDocument 인스턴스를 만듭니다.
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// PDF 렌더링 옵션 설정
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//출력을 렌더링합니다
pdf_renderer.render(device, html_document);
```

### 콘텐츠 너비에 맞게 조정된 페이지 크기

이 시나리오에서는 페이지 크기가 콘텐츠 너비에 따라 조정됩니다.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//출력을 렌더링합니다
pdf_renderer.render(device, html_document);
```

## 결론

이 튜토리얼에서는 Aspose.HTML for Java를 사용하여 HTML을 PDF로 변환할 때 PDF 페이지 크기를 조정하는 방법을 살펴보았습니다. 필수 조건을 알아보고, 필요한 패키지를 가져오고, 단계별 가이드를 따라 이 작업을 수행했습니다. Aspose.HTML for Java를 사용하면 생성된 PDF의 페이지 크기를 쉽게 제어하여 콘텐츠가 의도한 대로 표시되도록 할 수 있습니다.

 귀하의 특정 요구 사항을 충족시키기 위해 다양한 페이지 크기와 설정을 자유롭게 실험해 보세요. 문제가 발생하거나 추가 질문이 있는 경우 주저하지 말고 다음에서 도움을 받으세요.[Java 설명서를 위한 Aspose.HTML](https://reference.aspose.com/html/java/) 또는[Aspose 지원 포럼](https://forum.aspose.com/).

## 자주 묻는 질문

### 질문 1: Java용 Aspose.HTML이란 무엇인가요?

A1: Java용 Aspose.HTML은 HTML 문서를 다루고, 이를 조작하고, 변환하고, PDF를 포함한 다양한 형식으로 렌더링할 수 있는 Java 라이브러리입니다.

### 질문 2: Aspose.HTML for Java를 사용하여 HTML을 PDF로 변환할 때 PDF 페이지 크기를 어떻게 조정할 수 있나요?

 A2: PDF 페이지 크기는 다음을 사용하여 조정할 수 있습니다.`PageSetup` 클래스 및 설정`AdjustToWidestPage` 재산에`true` 또는 요구 사항에 따라 false입니다.

### 질문 3: HTML 콘텐츠를 PDF로 변환하기 전에 스타일을 사용자 지정할 수 있나요?

A3: 네, 튜토리얼에서 보여주는 대로, PDF로 변환하기 전에 HTML 콘텐츠에 CSS와 HTML 요소를 추가하여 스타일을 사용자 정의할 수 있습니다.

### 질문 4: Java용 Aspose.HTML에 대한 문서는 어디에서 찾을 수 있나요?

 A4: 문서를 참고하시면 됩니다.[여기](https://reference.aspose.com/html/java/) 포괄적인 정보와 예를 보려면 여기를 클릭하세요.

### 질문 5: Java용 Aspose.HTML의 무료 평가판이 있나요?

 A5: 예, Java용 Aspose.HTML의 무료 평가판에 액세스할 수 있습니다.[이 링크](https://releases.aspose.com/).