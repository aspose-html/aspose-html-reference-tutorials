---
date: 2026-01-02
description: Aspose.HTML를 사용하여 Java에서 EPUB를 PDF로 변환하고, 사용자 정의 PDF 페이지 크기 및 기타 PDF
  저장 옵션을 설정하는 방법을 배웁니다.
linktitle: Specifying PDF Save Options for EPUB to PDF
second_title: Java HTML Processing with Aspose.HTML
title: '맞춤 PDF 페이지 크기: EPUB을 PDF로 변환할 때 PDF 저장 옵션 지정'
url: /ko/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 맞춤 PDF 페이지 크기: EPUB을 PDF로 변환하기 위한 PDF 저장 옵션 지정

## 소개

Aspose.HTML for Java은 **EPUB을 PDF로 변환**을 쉽게 해주며, **맞춤 PDF 페이지 크기** 설정을 포함해 출력에 대한 완전한 제어를 제공합니다. 이 단계별 가이드에서는 환경 준비부터 `PdfSaveOptions`를 조정하여 생성된 PDF가 요구하는 정확한 페이지 크기에 맞도록 하는 모든 과정을 안내합니다. 출판 파이프라인을 구축하든, e‑learning 플랫폼을 만들든, 혹은 문서 변환을 자동화하든, 여기서 제공하는 기술이 유용할 것입니다.

## 빠른 답변
- **이 튜토리얼의 주요 목적은 무엇인가요?** 맞춤 PDF 페이지 크기를 적용하여 EPUB 파일을 PDF로 변환합니다.  
- **사용된 라이브러리는 무엇인가요?** Aspose.HTML for Java.  
- **라이선스가 필요합니까?** 무료 체험판을 사용할 수 있으며, 프로덕션에서는 상용 라이선스가 필요합니다.  
- **배경 색상을 변경할 수 있나요?** 예, `PdfSaveOptions`를 사용합니다.  
- **Java 8+를 지원하나요?** 물론입니다—모든 최신 Java 런타임에서 작동합니다.

## 맞춤 PDF 페이지 크기란 무엇인가요?

맞춤 PDF 페이지 크기를 사용하면 A4나 Letter와 같은 표준 크기에 의존하지 않고 출력 PDF의 각 페이지에 정확한 너비와 높이를 정의할 수 있습니다. 이는 전자책, 전단지 또는 시각적 레이아웃이 특정 디자인과 일치해야 하는 모든 상황에 특히 유용합니다.

## 왜 Aspose.HTML을 사용해 EPUB을 PDF로 변환하나요?

- **높은 충실도:** 복잡한 레이아웃, 글꼴 및 이미지를 보존합니다.  
- **세밀한 제어:** `PdfSaveOptions`를 통해 페이지 크기, 배경, 여백 등을 조정할 수 있습니다.  
- **크로스 플랫폼:** 동일한 Java 코드로 Windows, Linux, macOS에서 작동합니다.  
- **성능:** 빠른 변환을 위한 최적화된 렌더링 엔진.

## 전제 조건

- **Java 개발 환경:** JDK 8 이상이 설치되고 설정되어 있어야 합니다.  
- **Aspose.HTML for Java:** 최신 JAR 파일을 [website](https://releases.aspose.com/html/java/)에서 다운로드합니다.  
- **EPUB 파일:** 변환하려는 `.epub` 문서.

이제 모든 준비가 끝났으니 실제 변환 단계로 들어가 보겠습니다.

## 1단계: EPUB 파일 열기

먼저 `FileInputStream`을 사용해 EPUB 파일을 열어야 합니다. 이 스트림은 나중에 변환기에 전달됩니다.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

## 2단계: PDF 저장 옵션 정의

여기서 **맞춤 PDF 페이지 크기**와 선택적인 배경 색상을 설정합니다. 원하는 크기에 맞게 픽셀 값을 조정하세요.

```java
com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
anyPage.setSize(new com.aspose.html.drawing.Size(
    com.aspose.html.drawing.Length.fromPixels(3000),
    com.aspose.html.drawing.Length.fromPixels(1000))
);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
```

### 전문가 팁:
- **픽셀 vs. 포인트:** `Length.fromPixels`는 화면 픽셀을 PDF 포인트(1 포인트 = 1/72 인치)로 변환합니다. 필요한 최종 인쇄 크기를 반영하는 값을 선택하세요.

## 3단계: EPUB을 PDF로 변환

입력 스트림과 맞춤 옵션이 준비되면 변환기를 호출합니다. 출력 PDF는 지정한 위치에 저장됩니다.

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

## 전체 소스 코드

```java
Specifying PDF Save Options for EPUB to PDF
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of the PdfSaveOptions with a custom page-size and a background-color.
            com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
            com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
            com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
            anyPage.setSize(new com.aspose.html.drawing.Size(
                    com.aspose.html.drawing.Length.fromPixels(3000),
                    com.aspose.html.drawing.Length.fromPixels(1000))
            );
            pageSetup.setAnyPage(anyPage);
            options.setPageSetup(pageSetup);
            options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
            // Call the ConvertEPUB method to convert the EPUB to PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```

## 일반적인 문제 및 해결책

| Issue | Cause | Fix |
|-------|-------|-----|
| **PDF 페이지가 비어 있음** | 변환 전에 입력 스트림이 닫힘 | `convertEPUB` 이후까지 `try‑with‑resources` 블록을 열어 둡니다. |
| **페이지 크기 오류** | 원하는 인쇄 크기에 맞지 않는 픽셀 사용 | 원하는 인치를 포인트(`1 inch = 72 points`)로 변환한 뒤 `Length.fromPixels`를 사용해 픽셀로 변환합니다. |
| **폰트 누락** | EPUB에 폰트가 포함되지 않음 | 폰트가 EPUB에 포함되어 있는지 확인하거나 호스트 머신에 설치합니다. |

## 자주 묻는 질문 (FAQs)

### Aspose.HTML for Java는 무료 라이브러리인가요?
Aspose.HTML for Java는 상용 라이브러리이지만, [website](https://releases.aspose.com/)에서 무료 체험 버전을 받을 수 있습니다.

### 변환을 지원하는 EPUB 형식은 무엇인가요?
Aspose.HTML for Java는 다양한 EPUB 형식의 변환을 지원하여 대부분의 EPUB 문서와 호환됩니다.

### PDF 출력물을 더 커스터마이즈할 수 있나요?
예, `PdfSaveOptions`에서 페이지 설정, 배경 색상 및 기타 설정을 조정하여 PDF 출력을 커스터마이즈할 수 있습니다.

### Aspose.HTML for Java 체험판에 제한이 있나요?
체험판에는 일부 제한이 있을 수 있으므로 자세한 내용은 문서를 확인하시기 바랍니다.

### Aspose.HTML for Java에 대한 지원은 어디서 받을 수 있나요?
[Aspose.HTML 포럼](https://forum.aspose.com/)에서 질문에 대한 답변을 찾고 지원을 받을 수 있습니다.

---

**마지막 업데이트:** 2026-01-02  
**테스트 환경:** Aspose.HTML for Java 24.11 (작성 시 최신 버전)  
**작성자:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}