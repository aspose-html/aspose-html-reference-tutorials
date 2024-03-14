---
title: Java용 Aspose.HTML을 사용하여 XPS 페이지 크기 조정
linktitle: XPS 페이지 크기 조정
second_title: Aspose.HTML을 사용한 Java HTML 처리
description: Java용 Aspose.HTML을 사용하여 XPS 페이지 크기를 조정하는 방법을 알아보세요. XPS 문서의 출력 크기를 쉽게 제어하세요.
type: docs
weight: 16
url: /ko/java/advanced-usage/adjust-xps-page-size/
---

이 튜토리얼에서는 Java용 Aspose.HTML을 사용하여 XPS 페이지 크기를 조정하는 과정을 안내합니다. 이 강력한 라이브러리를 사용하면 HTML 문서를 조작하고 XPS를 포함한 다양한 형식으로 렌더링할 수 있습니다. XPS 문서의 출력 크기를 제어해야 하는 경우 페이지 크기를 조정하는 것이 필수적입니다.

## 전제 조건

시작하기 전에 다음 전제 조건이 충족되었는지 확인하세요.

1. Java 개발 환경: 시스템에 JDK(Java Development Kit)가 설치되어 있는지 확인하십시오.

2.  Java 라이브러리용 Aspose.HTML: Java 프로젝트에 Java용 Aspose.HTML 라이브러리를 다운로드하여 포함해야 합니다. 도서관을 찾으실 수 있습니다[여기](https://releases.aspose.com/html/java/).

3. HTML 파일 입력: XPS 페이지 크기를 렌더링하고 조정할 HTML 파일을 준비합니다. 이 튜토리얼에서는 자신만의 HTML 파일을 사용할 수 있습니다.

## 패키지 가져오기

먼저, Aspose.HTML for Java를 사용하려면 필요한 패키지를 가져와야 합니다. Java 클래스 시작 부분에 다음 패키지를 포함합니다.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## 1단계: 입력 파일 이름 설정

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

 이 단계에서는 다음을 사용하여 HTML 입력 파일을 읽습니다.`FileInputStream`.

## 2단계: HTML 문서 만들기 및 스타일 설정

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n";

// ...
```

 이 단계에는`HTMLDocument` 스타일을 추가하는 것입니다.

## 3단계: XPS 렌더링 옵션 생성

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

여기서는 XPS 렌더링 옵션을 만들어 렌더링 프로세스를 구성합니다.

## 4단계: 페이지 크기 조정

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

이 단계에는 페이지 크기를 설정하고 이를 가장 넓은 페이지로 조정할지 여부를 지정하는 작업이 포함됩니다.

## 5단계: 출력 렌더링

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

마지막 단계에서는 구성된 옵션을 사용하여 XPS 출력을 렌더링합니다.

## 결론

이 튜토리얼에서는 Java용 Aspose.HTML을 사용하여 XPS 페이지 크기를 조정하는 방법을 보여주었습니다. XPS 문서의 출력 크기를 제어하여 특정 요구 사항을 충족할 수 있습니다. 제공된 코드와 단계를 사용하면 Java 애플리케이션에서 이 기능을 쉽게 구현할 수 있습니다.

 질문이 있거나 추가 도움이 필요하시면 언제든지 방문해주세요.[Java 문서용 Aspose.HTML](https://reference.aspose.com/html/java/) 또는 에 도움을 요청하세요.[Aspose 포럼](https://forum.aspose.com/).

## FAQ

### Q1: Java용 Aspose.HTML은 무엇입니까?

A1: Aspose.HTML for Java는 개발자가 HTML 문서를 XPS, PDF, 이미지 등 다양한 형식으로 조작하고 변환할 수 있도록 하는 Java 라이브러리입니다.

### Q2: Java용 Aspose.HTML을 어디서 다운로드할 수 있나요?

 A2: 다음에서 Java 라이브러리용 Aspose.HTML을 다운로드할 수 있습니다.[이 링크](https://releases.aspose.com/html/java/).

### Q3: Aspose.HTML for Java에 대한 무료 평가판이 있습니까?

 A3: 예, 다음 사이트에서 Java용 Aspose.HTML 무료 평가판을 얻을 수 있습니다.[여기](https://releases.aspose.com/).

### Q4: Java용 Aspose.HTML에 대한 임시 라이선스를 어떻게 얻을 수 있나요?

 A4: Java용 Aspose.HTML에 대한 임시 라이선스를 얻으려면 다음을 방문하세요.[이 페이지](https://purchase.aspose.com/temporary-license/).

### Q5: Java용 Aspose.HTML에 대한 지원을 받을 수 있나요?

 A5: 예, Aspose 커뮤니티에서 도움과 지원을 구할 수 있습니다.[Aspose 포럼](https://forum.aspose.com/).