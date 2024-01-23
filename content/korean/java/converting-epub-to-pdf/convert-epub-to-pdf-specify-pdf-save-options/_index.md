---
title: EPUB를 PDF로 저장하기 위한 PDF 저장 옵션 지정
linktitle: EPUB를 PDF로 저장하기 위한 PDF 저장 옵션 지정
second_title: Aspose.HTML을 사용한 Java HTML 처리
description: 강력한 HTML 조작 라이브러리인 Aspose.HTML을 사용하여 Java에서 EPUB를 PDF로 변환하는 방법을 알아보세요.
type: docs
weight: 12
url: /ko/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
---

## 소개

Aspose.HTML for Java는 HTML 및 EPUB 문서 작업을 위한 강력한 도구입니다. 이 단계별 가이드에서는 Java용 Aspose.HTML을 사용하여 EPUB 파일을 PDF로 변환하는 과정을 안내합니다. 숙련된 개발자이든 이제 막 시작하는 개발자이든 이 튜토리얼은 이 작업을 효율적으로 수행하는 데 필요한 지식과 기술을 제공합니다.

## 전제 조건

시작하기 전에 다음 전제 조건이 충족되었는지 확인하세요.

- Java 개발 환경: 시스템에 Java 개발 환경이 설정되어 있어야 합니다.

-  Java용 Aspose.HTML: Java용 Aspose.HTML 라이브러리를 다운로드하고 설치합니다. 라이브러리 및 관련 문서는 다음에서 찾을 수 있습니다.[웹사이트](https://releases.aspose.com/html/java/).

- EPUB 파일: PDF로 변환하려는 EPUB 파일이 필요합니다.

이제 Java용 Aspose.HTML을 사용하여 EPUB를 PDF로 변환하는 단계별 가이드를 살펴보겠습니다.

## 1단계: EPUB 파일 열기

 시작하려면 읽을 기존 EPUB 파일을 엽니다. 당신은 사용할 수 있습니다`FileInputStream` 이것을 달성하기 위해. 이 단계의 코드는 다음과 같습니다.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // 다음 단계를 위한 코드가 여기에 입력됩니다.
}
```

## 2단계: PDF 저장 옵션 정의

 인스턴스 만들기`PdfSaveOptions` 사용자 정의 페이지 크기와 배경색으로. 요구 사항에 따라 페이지 설정을 구성할 수 있습니다. 방법은 다음과 같습니다.

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

## 3단계: EPUB를 PDF로 변환

 이제`ConvertEPUB` EPUB 파일을 PDF로 변환하는 방법. 입력 스트림, PDF 저장 옵션 및 출력 위치를 지정합니다. 수행 방법은 다음과 같습니다.

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

축하해요! Java용 Aspose.HTML을 사용하여 EPUB 파일을 PDF로 성공적으로 변환했습니다. 이제 지정된 출력 위치에서 변환된 PDF 파일에 액세스할 수 있습니다.

## 완전한 소스 코드
```java
Specifying PDF Save Options for EPUB to PDF
        // 읽기 위해 기존 EPUB 파일을 엽니다.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // 사용자 정의 페이지 크기와 배경색을 사용하여 PdfSaveOptions의 인스턴스를 만듭니다.
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
            // EPUB를 PDF로 변환하려면 ConvertEPUB 메서드를 호출하세요.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```


## 결론

이 튜토리얼에서는 Java용 Aspose.HTML을 사용하여 EPUB 파일을 PDF 형식으로 변환하는 방법을 배웠습니다. 이 다용도 라이브러리는 개발자에게 문서 조작을 위한 강력한 도구를 제공합니다. 이 가이드에 설명된 단계를 따르면 EPUB에서 PDF로의 변환을 Java 애플리케이션에 원활하게 통합할 수 있습니다.

## 자주 묻는 질문(FAQ)

### Java용 Aspose.HTML은 무료 라이브러리인가요?
 Java용 Aspose.HTML은 상용 라이브러리이지만 다음 사이트에서 무료 평가판을 얻을 수 있습니다.[웹사이트](https://releases.aspose.com/).

### 변환에는 어떤 EPUB 형식이 지원됩니까?
Java용 Aspose.HTML은 다양한 EPUB 형식의 변환을 지원하여 대부분의 EPUB 문서와의 호환성을 보장합니다.

### PDF 출력을 추가로 사용자 정의할 수 있나요?
 예, 페이지 설정, 배경색 및 기타 설정을 조정하여 PDF 출력을 사용자 정의할 수 있습니다.`PdfSaveOptions`.

### Java용 Aspose.HTML 평가판에 제한 사항이 있나요?
평가판 버전에는 일부 제한 사항이 있을 수 있으므로 자세한 내용은 설명서를 확인하는 것이 좋습니다.

### Java용 Aspose.HTML에 대한 지원은 어디서 받을 수 있나요?
귀하의 질문에 대한 답변을 찾고 지원을 요청할 수 있습니다.[Aspose.HTML 포럼](https://forum.aspose.com/).
