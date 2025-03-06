---
title: Aspose.HTML을 사용하여 .NET에서 변환기 미세 조정
linktitle: .NET에서 변환기 미세 조정
second_title: Aspose.HTML .NET HTML 조작 API
description: Aspose.HTML for .NET을 사용하여 HTML을 PDF, XPS 및 이미지로 변환하는 방법을 알아보세요. 코드 예제와 FAQ가 포함된 단계별 튜토리얼.
weight: 16
url: /ko/net/advanced-features/fine-tuning-converters/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML을 사용하여 .NET에서 변환기 미세 조정


## 소개

Aspose.HTML for .NET은 개발자가 다양한 형식의 HTML 문서를 조작하고 변환할 수 있는 강력한 라이브러리입니다. HTML을 PDF, XPS 또는 이미지로 변환하거나 다른 HTML 관련 작업을 수행해야 하는 경우 Aspose.HTML은 작업을 완료하는 데 도움이 되는 강력한 도구 세트를 제공합니다.

이 튜토리얼에서는 Aspose.HTML for .NET의 몇 가지 필수 기능을 살펴보고 각 예제에 대한 단계별 설명을 제공합니다. 이 튜토리얼을 마치면 .NET 애플리케이션에서 Aspose.HTML for .NET을 사용하는 방법을 확실히 이해하게 될 것입니다.

## 필수 조건

예제를 살펴보기 전에 다음과 같은 전제 조건이 충족되었는지 확인하세요.

-  .NET용 Aspose.HTML: .NET용 Aspose.HTML 라이브러리가 설치되어 있어야 합니다. 다음에서 다운로드할 수 있습니다.[다운로드 링크](https://releases.aspose.com/html/net/).

-  임시 라이센스(선택 사항): 유효한 라이센스가 없는 경우 다음에서 임시 라이센스를 얻을 수 있습니다.[여기](https://purchase.aspose.com/temporary-license/).

이제 .NET용 Aspose.HTML의 몇 가지 일반적인 사용 사례를 살펴보겠습니다.

## 네임스페이스 가져오기

C# 코드에서 먼저 필요한 네임스페이스를 가져옵니다.

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Pdf;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Xps;
using Aspose.Html.Rendering.Pdf.Encryption;
using Aspose.Html.Drawing;
```

## HTML을 PDF로 변환

### 1단계: HTML 코드 준비

```csharp
var code = @"<span>Hello World!!</span>";
```

### 2단계: HTML 문서 초기화

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 3단계: PDF 장치 생성 및 출력 파일 지정

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### 4단계: HTML을 PDF로 렌더링

```csharp
document.RenderTo(device);
```

이 예에서는 HTML 스니펫을 PDF 문서로 변환합니다. 필요에 따라 HTML 코드와 출력 파일을 사용자 지정할 수 있습니다.

## 사용자 정의 페이지 크기 설정

### 1단계: HTML 코드 준비

```csharp
var code = @"<span>Hello World!!</span>";
```

### 2단계: HTML 문서 초기화

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 3단계: PDF 렌더링 옵션 생성

```csharp
var options = new PdfRenderingOptions()
{
    PageSetup =
    {
        AnyPage = new Page(
            new Size(
                Length.FromInches(5),
                Length.FromInches(2)))
    }
};
```

### 4단계: PDF 장치 생성 및 옵션 및 출력 파일 지정

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### 5단계: HTML을 PDF로 렌더링

```csharp
document.RenderTo(device);
```

이 예제에서는 생성된 PDF 문서에 사용자 지정 페이지 크기를 설정하는 방법을 보여줍니다.

## 해상도 조정

### 1단계: HTML 코드 준비 및 파일에 저장

```csharp
var code = @"
    <style>
    p
    { 
        background: blue; 
    }
    @media(min-resolution: 300dpi)
    {
        p 
        { 
            /* high-resolution screen color */
            background: green
        }
    }
    </style>
    <p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### 2단계: HTML 문서 초기화

```csharp
using (var document = new HTMLDocument("document.html"))
```

### 3단계: 저해상도에 대한 PDF 렌더링 옵션 만들기

```csharp
var options = new PdfRenderingOptions()
{
    HorizontalResolution = 50,
    VerticalResolution = 50
};
```

### 4단계: PDF 장치 생성 및 저해상도에 대한 옵션 및 출력 파일 지정

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### 5단계: 저해상도의 HTML을 PDF로 렌더링

```csharp
document.RenderTo(device);
```

### 6단계: 고해상도를 위한 PDF 렌더링 옵션 생성

```csharp
options = new PdfRenderingOptions()
{
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

### 7단계: PDF 장치 생성 및 고해상도를 위한 옵션 및 출력 파일 지정

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### 8단계: 고해상도를 위해 HTML을 PDF로 렌더링

```csharp
document.RenderTo(device);
```

이 예에서는 낮은 해상도와 높은 해상도 화면을 모두 고려하여 HTML을 PDF로 렌더링할 때 해상도를 조정하는 방법을 보여줍니다.

## 배경색 지정

### 1단계: HTML 코드 준비 및 파일에 저장

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### 2단계: HTML 문서 초기화

```csharp
using (var document = new HTMLDocument("document.html"))
```

### 3단계: 배경색으로 PDF 렌더링 옵션 초기화

```csharp
var options = new PdfRenderingOptions()
{
    BackgroundColor = System.Drawing.Color.Cyan
};
```

### 4단계: PDF 장치 생성 및 옵션 및 출력 파일 지정

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### 5단계: HTML을 PDF로 렌더링

```csharp
document.RenderTo(device);
```

이 예제는 HTML을 PDF로 변환할 때 배경색을 지정하는 방법을 보여줍니다.

## 왼쪽 및 오른쪽 페이지 크기 설정

### 1단계: HTML 코드 준비

```csharp
var code = @"<style>div { page-break-after: always; }</style>
    <div>First Page</div>
    <div>Second Page</div>
    <div>Third Page</div>
    <div>Fourth Page</div>";
```

### 2단계: HTML 문서 초기화

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 3단계: 왼쪽 및 오른쪽 페이지 크기로 PDF 렌더링 옵션 만들기

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.SetLeftRightPage(
    new Page(new Size(400, 200)),
    new Page(new Size(400, 100))
);
```

### 4단계: PDF 장치 생성 및 옵션 및 출력 파일 지정

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### 5단계: HTML을 PDF로 렌더링

```csharp
document.RenderTo(device);
```

이 예제는 HTML을 PDF로 변환할 때 왼쪽 및 오른쪽 페이지에 서로 다른 페이지 크기를 설정하는 방법을 보여줍니다.

## 콘텐츠에 맞게 페이지 크기 조정

### 1단계: HTML 코드 준비

```csharp
var code = @"<style>
    div { page-break-after: always; }
</style>
<div style='border: 1px solid red; width: 400px'>First Page</div>
<div style='border: 1px solid red; width: 600px'>Second Page</div>";
```

### 2단계: HTML 문서 초기화

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 3단계: PDF 렌더링 옵션 생성

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### 4단계: PDF 장치 생성 및 옵션 및 출력 파일 지정

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### 5단계: HTML을 PDF로 렌더링

```csharp
document.RenderTo(device);
```

이 예제는 HTML을 PDF로 변환할 때 가장 넓은 콘텐츠에 맞게 페이지 크기를 조정하는 방법을 보여줍니다.

## PDF 권한 지정

### 1단계: HTML 코드 준비

```csharp
var code = @"<div>Hello World!!</div>";
```

### 2단계: HTML 문서 초기화

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 3단계: 권한이 있는 PDF 렌더링 옵션 만들기

```csharp
var options = new PdfRenderingOptions();
options.Encryption = new PdfEncryptionInfo(
    "user_pwd",
    "owner_pwd",
    PdfPermissions.PrintDocument,
    PdfEncryptionAlgorithm.RC4_128
);
```

### 4단계: PDF 장치 생성 및 옵션 및 출력 파일 지정

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### 5단계: HTML을 PDF로 렌더링

```csharp
document.RenderTo(device);
```

이 예제에서는 HTML을 보호된 PDF로 변환할 때 권한과 암호화를 지정하는 방법을 보여줍니다.

## 이미지별 옵션 지정

### 1단계: HTML 코드 준비

```csharp
var code = @"<div>Hello World!!</div>";
```

### 2단계: HTML 문서 초기화

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 3단계: 이미지 렌더링 옵션 만들기

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### 4단계: 이미지 장치 생성 및 옵션 및 출력 파일 지정

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### 5단계: HTML을 이미지로 렌더링

```csharp
document.RenderTo(device);
```

이 예제에서는 형식, 해상도, 평활화 모드 등의 특정 렌더링 옵션을 사용하여 HTML을 이미지로 변환하는 방법을 보여줍니다.

## XPS 렌더링 옵션 지정

### 1단계: HTML 코드 준비

```csharp
var code = @"<span>Hello World!!</span>";
```

### 2단계: HTML 문서 초기화

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 3단계: 페이지 크기로 XPS 렌더링 옵션 만들기

```csharp
var options = new XpsRenderingOptions();
options.PageSetup.AnyPage = new Page(
    new Size(
        Length.FromInches(5),
        Length.FromInches(2)
    )
);
```

### 4단계: XPS 장치 생성 및 옵션 및 출력 파일 지정

```csharp
using (var device = new XpsDevice(options, "output.xps"))
```

### 5단계: HTML을 XPS로 렌더링

```csharp
document.RenderTo(device);
```

이 예제에서는 사용자 지정 페이지 크기와 렌더링 옵션을 사용하여 HTML을 XPS로 변환하는 방법을 보여줍니다.

## 여러 HTML 문서를 PDF로 결합

### 1단계: 여러 문서에 대한 HTML 코드 준비

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### 2단계: 병합할 HTML 문서 만들기

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### 3단계: HTML 렌더러 초기화

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### 4단계: 병합된 출력을 위한 PDF 장치 생성

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### 5단계: HTML 문서를 PDF로 병합

```csharp
renderer.Render(device, document1, document2, document3);
```

이 예제는 Aspose.HTML for .NET을 사용하여 여러 HTML 문서를 하나의 PDF 파일로 결합하는 방법을 보여줍니다.

## 렌더링 시간 초과 설정

### 1단계: JavaScript로 HTML 코드 준비

```csharp
var code = @"
    <script>
        var count = 0;
        setInterval(function()
        {
            var element = document.createElement('div');
            var message = (++count) + '. ' + 'Hello World!!';
            var text = document.createTextNode(message);
            element.appendChild(text);
            document.body.appendChild(element);
        }, 1000);
    </script>";
```

### 2단계: HTML 문서 초기화

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 3단계: HTML 렌더러 초기화

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### 4단계: PDF 장치 생성 및 렌더링 시간 초과 설정

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### 5단계: 시간 초과를 사용하여 HTML을 PDF로 렌더링

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

이 예제는 HTML을 PDF로 변환할 때 렌더링 시간 초과를 설정하는 방법을 보여줍니다. 이는 동적 콘텐츠나 오랫동안 실행되는 스크립트를 처리할 때 유용합니다.

## 결론

Aspose.HTML for .NET은 개발자가 HTML 문서를 효율적으로 작업할 수 있도록 하는 다재다능한 라이브러리입니다. 이 튜토리얼에서는 기본 HTML에서 PDF로의 변환부터 사용자 지정 페이지 크기, 해상도, 권한과 같은 고급 기능까지 다양한 예를 다루었습니다. 이러한 예를 따르면 .NET 애플리케이션에서 Aspose.HTML for .NET의 모든 잠재력을 활용할 수 있습니다.

 질문이 있거나 추가 지원이 필요한 경우 언제든지 방문하세요.[Aspose.HTML 포럼](https://forum.aspose.com/) 지원과 지침을 받으세요.

## 자주 묻는 질문

### Q1. .NET용 Aspose.HTML이란 무엇입니까?
   
A1: Aspose.HTML for .NET은 개발자가 HTML 문서를 프로그래밍 방식으로 조작하고 변환할 수 있는 .NET 라이브러리입니다. HTML에서 PDF, XPS, 이미지 변환을 포함하여 HTML 콘텐츠 작업을 위한 광범위한 기능과 고급 렌더링 옵션을 제공합니다.

### Q2. .NET용 Aspose.HTML은 어디서 다운로드할 수 있나요?

 A2: .NET용 Aspose.HTML은 다음에서 다운로드할 수 있습니다.[다운로드 링크](https://releases.aspose.com/html/net/).

### Q3. Aspose.HTML for .NET을 사용하려면 라이센스가 필요합니까?

A3: 라이선스 없이도 .NET용 Aspose.HTML을 사용할 수 있지만, 모든 기능을 사용하고 워터마크나 제한을 제거하려면 프로덕션 환경에서 사용하려면 라이선스를 취득하는 것이 좋습니다.

### Q4. Aspose.HTML for .NET으로 생성된 PDF 파일을 어떻게 보호할 수 있습니까?

A4: Aspose.HTML for .NET을 사용하여 HTML을 PDF로 렌더링할 때 PDF 권한 및 암호화 설정을 지정할 수 있습니다. 이를 통해 누가 결과 PDF 파일에 액세스하고 수정할 수 있는지 제어할 수 있습니다.

### Q5. HTML을 XPS나 이미지와 같은 다른 포맷으로 변환할 수 있나요?

A5: 네, Aspose.HTML for .NET은 HTML을 PDF, XPS, 이미지(예: JPEG)를 포함한 다양한 포맷으로 변환하는 것을 지원합니다. 변환 설정을 사용자 지정하여 특정 요구 사항을 충족할 수 있습니다.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
