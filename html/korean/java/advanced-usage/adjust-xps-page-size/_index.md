---
title: Java용 Aspose.HTML로 XPS 페이지 크기 조정
linktitle: XPS 페이지 크기 조정
second_title: Aspose.HTML을 사용한 Java HTML 처리
description: Aspose.HTML for Java로 XPS 페이지 크기를 조정하는 방법을 알아보세요. XPS 문서의 출력 크기를 쉽게 제어하세요.
weight: 16
url: /ko/java/advanced-usage/adjust-xps-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java용 Aspose.HTML로 XPS 페이지 크기 조정


이 튜토리얼에서는 Java용 Aspose.HTML을 사용하여 XPS 페이지 크기를 조정하는 과정을 안내합니다. 이 강력한 라이브러리를 사용하면 HTML 문서를 조작하고 XPS를 포함한 다양한 형식으로 렌더링할 수 있습니다. XPS 문서의 출력 크기를 제어해야 할 때 페이지 크기를 조정하는 것이 필수적입니다.

## 필수 조건

시작하기 전에 다음 전제 조건이 충족되었는지 확인하세요.

1. Java 개발 환경: 시스템에 Java 개발 키트(JDK)가 설치되어 있는지 확인하세요.

2.  Aspose.HTML for Java 라이브러리: Java 프로젝트에 Aspose.HTML for Java 라이브러리를 다운로드하여 포함해야 합니다. 라이브러리를 찾을 수 있습니다.[여기](https://releases.aspose.com/html/java/).

3. HTML 파일 입력: 렌더링하고 XPS 페이지 크기를 조정하려는 HTML 파일을 준비합니다. 이 튜토리얼에서는 사용자 고유의 HTML 파일을 사용할 수 있습니다.

## 패키지 가져오기

먼저, Java용 Aspose.HTML을 사용하는 데 필요한 패키지를 가져와야 합니다. Java 클래스의 시작 부분에 다음 패키지를 포함합니다.

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

 이 단계에는 다음을 만드는 것이 포함됩니다.`HTMLDocument` 그리고 스타일을 추가합니다.

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

이 단계에서는 페이지 크기를 설정하고 이를 가장 넓은 페이지로 조정할지 여부를 지정하는 것이 포함됩니다.

## 5단계: 출력 렌더링

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

마지막 단계에서는 구성된 옵션을 사용하여 XPS 출력을 렌더링합니다.

## 결론

이 튜토리얼에서는 Java용 Aspose.HTML을 사용하여 XPS 페이지 크기를 조정하는 방법을 보여드렸습니다. XPS 문서의 출력 크기를 제어하여 특정 요구 사항을 충족하는지 확인할 수 있습니다. 제공된 코드와 단계를 사용하면 Java 애플리케이션에서 이 기능을 쉽게 구현할 수 있습니다.

 질문이 있거나 추가 지원이 필요한 경우 언제든지 방문하세요.[Java 설명서를 위한 Aspose.HTML](https://reference.aspose.com/html/java/) 또는 도움을 요청하세요[애스포지 포럼](https://forum.aspose.com/).

## 자주 묻는 질문

### 질문 1: Java용 Aspose.HTML이란 무엇인가요?

A1: Java용 Aspose.HTML은 개발자가 HTML 문서를 조작하고 XPS, PDF, 이미지 등 다양한 형식으로 변환할 수 있는 Java 라이브러리입니다.

### Q2: Java용 Aspose.HTML은 어디서 다운로드할 수 있나요?

 A2: Java 라이브러리용 Aspose.HTML은 다음에서 다운로드할 수 있습니다.[이 링크](https://releases.aspose.com/html/java/).

### 질문 3: Java용 Aspose.HTML의 무료 평가판이 있나요?

 A3: 네, Java용 Aspose.HTML의 무료 평가판을 받을 수 있습니다.[여기](https://releases.aspose.com/).

### 질문 4: Java용 Aspose.HTML에 대한 임시 라이선스를 어떻게 얻을 수 있나요?

 A4: Java용 Aspose.HTML에 대한 임시 라이센스를 받으려면 다음을 방문하세요.[이 페이지](https://purchase.aspose.com/temporary-license/).

### 질문 5: Java용 Aspose.HTML에 대한 지원을 받을 수 있나요?

 A5: 예, Aspose 커뮤니티에서 도움과 지원을 받을 수 있습니다.[애스포지 포럼](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
