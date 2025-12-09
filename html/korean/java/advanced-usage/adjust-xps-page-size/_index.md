---
date: 2025-11-29
description: Aspose.HTML for Java를 사용하여 HTML을 XPS로 변환하고 XPS 페이지 크기를 조정하는 방법을 배웁니다.
  출력 크기를 쉽게 제어하세요.
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Aspose.HTML for Java를 사용하여 HTML을 XPS로 변환하고 XPS 페이지 크기 조정
url: /ko/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML을 XPS로 변환하고 Aspose.HTML for Java로 XPS 페이지 크기 조정

이 튜토리얼에서는 **HTML을 XPS로 변환하는 방법**과 Aspose.HTML for Java를 사용해 결과 페이지 크기를 미세 조정하는 방법을 알아봅니다. 인쇄 가능한 보고서, 청구서 또는 보관용 문서를 생성하든, XPS 차원을 제어하면 출력이 기대한 대로 정확히 표시됩니다. 환경 설정부터 최종 XPS 파일 렌더링까지 모든 단계를 차근차근 진행하므로 바로 Java 애플리케이션에 이 기능을 통합할 수 있습니다.

## 빠른 답변
- **“HTML을 XPS로 변환”이란 무엇인가요?** HTML 문서를 XPS 파일로 렌더링하여 레이아웃과 스타일을 보존합니다.  
- **라이선스가 필요합니까?** 개발 단계에서는 무료 체험판으로 충분하지만, 운영 환경에서는 상용 라이선스가 필요합니다.  
- **지원되는 Java 버전은?** Java 8 이상 (JDK 11+ 권장).  
- **페이지 크기를 변경할 수 있나요?** 예 – Aspose.HTML를 사용하면 렌더링 전에 사용자 정의 치수를 지정할 수 있습니다.  
- **변환에 얼마나 걸리나요?** 일반적인 페이지는 1초 미만, 큰 문서는 더 오래 걸릴 수 있습니다.

## HTML을 XPS로 변환한다는 의미
HTML을 XPS로 변환한다는 것은 웹 기반 마크업 파일을 XPS(XML Paper Specification) 문서, 즉 PDF와 유사한 고정 레이아웃 인쇄용 포맷으로 만드는 것을 의미합니다. Java 애플리케이션에서 아카이브하거나 인쇄용으로 고품질, 장치 독립적인 문서가 필요할 때 유용합니다.

## XPS 페이지 크기를 조정해야 하는 이유
페이지 크기를 조정하면 최종 문서의 물리적 치수(A4, Letter, 사용자 정의 라벨 등)를 직접 제어할 수 있습니다. 원치 않는 스케일링을 방지하고 내용이 정확히 맞도록 하며, 불필요한 여백을 없애 파일 크기를 줄일 수도 있습니다.

## 사전 준비 사항

시작하기 전에 다음 항목을 준비하십시오:

1. **Java Development Environment** – 시스템에 Java Development Kit (JDK)가 설치되어 있어야 합니다.  
2. **Aspose.HTML for Java Library** – Aspose.HTML for Java 라이브러리를 다운로드하여 프로젝트에 포함합니다. 라이브러리는 [여기](https://releases.aspose.com/html/java/)에서 찾을 수 있습니다.  
3. **Input HTML File** – XPS 페이지 크기를 조정하고 렌더링할 HTML 파일을 준비합니다. 이 튜토리얼에서는 직접 만든 HTML 파일을 사용해도 됩니다.

## 패키지 가져오기

먼저 필요한 클래스를 가져옵니다. 이 패키지들을 통해 문서 처리, 렌더링 및 페이지 설정 기능에 접근할 수 있습니다.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## 1단계: 입력 파일 이름 설정

`FileInputStream`을 사용해 소스 HTML 파일을 읽습니다. 이 스트림은 원시 HTML을 Aspose.HTML 엔진에 전달합니다.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

## 2단계: HTMLDocument 생성 및 스타일 설정

렌더링할 내용을 나타내는 `HTMLDocument` 인스턴스를 생성합니다. 예제로 작은 CSS 블록을 삽입해 스타일링을 보여줍니다—필요에 따라 자신의 마크업으로 교체하십시오.

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
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n" +
               "\n";

// ...
```

## 3단계: XPS 렌더링 옵션 생성

HTML을 XPS로 변환할 때 적용되는 모든 설정을 담는 `XpsRenderingOptions` 객체를 인스턴스화합니다.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

## 4단계: 페이지 크기 조정

사용자 정의 페이지 크기(폭 × 높이, 포인트 단위)를 정의하고, 렌더러가 가장 넓은 페이지로 자동 확장할지 여부를 지정합니다. `adjustToWidestPage`를 `false`로 설정하면 지정한 정확한 치수가 유지됩니다.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

## 5단계: 출력 렌더링

구성된 옵션을 사용해 `XpsDevice`를 생성하고 HTML 문서를 렌더링합니다. 결과는 지정한 사용자 정의 페이지 치수를 가진 완전한 XPS 파일이 됩니다.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## 일반적인 문제와 해결 방법

| 문제 | 발생 원인 | 해결 방법 |
|------|----------|----------|
| **빈 XPS 출력** | 입력 스트림이 닫히지 않았거나 HTMLDocument가 잘못된 파일을 가리킴 | `FileInputStream`을 try‑with‑resources 블록으로 올바르게 감싸고 파일 경로가 정확한지 확인 |
| **페이지 크기가 적용되지 않음** | `adjustToWidestPage`가 `true`로 남아 있음 | Step 4에서 `pageSetup.setAdjustToWidestPage(false);` 로 설정 |
| **지원되지 않는 CSS** | Aspose.HTML가 CSS의 일부만 지원 | 기본 레이아웃, 폰트, 색상만 사용하고 고급 선택자나 CSS Grid는 피함 |
| **LicenseException** | 프로덕션 환경에서 유효한 라이선스 없이 실행 | 렌더링 전에 임시 또는 구매한 라이선스를 적용 (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`) |

## 자주 묻는 질문

**Q: Aspose.HTML for Java란 무엇인가요?**  
A: Aspose.HTML for Java는 개발자가 HTML 문서를 XPS, PDF, 이미지 등 다양한 포맷으로 조작하고 변환할 수 있게 해 주는 Java 라이브러리입니다.

**Q: Aspose.HTML for Java를 어디서 다운로드할 수 있나요?**  
A: 라이브러리는 [이 링크](https://releases.aspose.com/html/java/)에서 다운로드할 수 있습니다.

**Q: Aspose.HTML for Java의 무료 체험판이 있나요?**  
A: 예, [여기](https://releases.aspose.com/)에서 Aspose.HTML for Java 무료 체험판을 받을 수 있습니다.

**Q: Aspose.HTML for Java의 임시 라이선스는 어떻게 얻나요?**  
A: 임시 라이선스는 [이 페이지](https://purchase.aspose.com/temporary-license/)에서 신청할 수 있습니다.

**Q: Aspose.HTML for Java에 대한 지원을 받을 수 있나요?**  
A: 예, [Aspose 포럼](https://forum.aspose.com/)에서 커뮤니티 도움을 받을 수 있습니다.

**Q: 헤드리스 서버에서 HTML을 XPS로 변환할 수 있나요?**  
A: 물론 가능합니다. Aspose.HTML는 GUI가 없는 환경에서도 동작하므로 Java 런타임만 올바르게 설정하면 됩니다.

**Q: 라이브러리가 사용자 정의 페이지 여백을 지원하나요?**  
A: 예. `PageSetup.setMarginTop()`, `setMarginBottom()` 등을 사용해 `PageSetup`을 렌더링 옵션에 할당하기 전에 설정하면 됩니다.

## 결론

우리는 **HTML을 XPS로 변환하고** Aspose.HTML for Java를 사용해 페이지 크기를 조정하는 전체 과정을 살펴보았습니다. 이 단계를 따르면 정확한 레이아웃 요구사항에 맞는 인쇄 준비가 된 XPS 문서를 생성할 수 있습니다. 다양한 페이지 치수, 스타일을 실험하거나 헤더·푸터를 추가해 프로젝트에 맞게 활용해 보세요.

추가 질문이나 도움이 필요하면 [Aspose.HTML for Java 문서](https://reference.aspose.com/html/java/)를 참고하거나 [Aspose 포럼](https://forum.aspose.com/)에서 대화를 나눠 보세요.

---

**Last Updated:** 2025-11-29  
**Tested With:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}