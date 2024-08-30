---
title: Aspose.HTML을 사용하여 .NET에서 문서 저장
linktitle: .NET에서 문서 저장하기
second_title: Aspose.HTML .NET HTML 조작 API
description: 단계별 가이드로 .NET용 Aspose.HTML의 힘을 활용하세요. HTML 및 SVG 문서를 만들고, 조작하고, 변환하는 방법을 알아보세요.
type: docs
weight: 16
url: /ko/net/html-document-manipulation/saving-a-document/
---

오늘날의 디지털 시대에 HTML 및 SVG 문서를 만들고 조작하는 것은 많은 소프트웨어 개발자와 기업에 필수적입니다. Aspose.HTML for .NET은 이러한 작업을 단순화하는 강력한 라이브러리로, HTML, SVG 등을 다루는 다양한 기능을 제공합니다. 이 포괄적인 가이드에서는 Aspose.HTML for .NET의 기본 사항을 살펴보고 각 예제를 따라하기 쉬운 단계로 나눕니다. 노련한 개발자이든 방금 시작했든, 이 가이드는 Aspose.HTML의 기능을 활용하는 데 매우 귀중하다는 것을 알게 될 것입니다.

## 필수 조건

이 여행을 시작하기 전에 먼저 필요한 모든 것을 갖추었는지 확인해 보겠습니다.

- 개발 환경: 컴퓨터에 Visual Studio나 다른 .NET 개발 환경이 설치되어 있는지 확인하세요.

- .NET용 Aspose.HTML: .NET용 Aspose.HTML 라이브러리를 얻어야 합니다. 여기에서 다운로드할 수 있습니다.[여기](https://releases.aspose.com/html/net/).

- C#에 대한 지식: C# 프로그래밍 언어에 대한 지식은 유익하지만 필수는 아닙니다. 이 가이드는 초보자 친화적으로 설계되었습니다.

## 네임스페이스 가져오기

.NET용 Aspose.HTML을 사용하려면 프로젝트에 필요한 네임스페이스를 가져와야 합니다. C# 코드에서 다음 네임스페이스를 포함합니다.

### 1단계: Aspose.HTML 네임스페이스 가져오기
```csharp
using Aspose.Html;
```

이 네임스페이스를 사용하면 다양한 HTML 및 SVG 조작 기능에 액세스할 수 있습니다.

## HTML을 파일로

### 1단계: 빈 HTML 문서 초기화
```csharp
// 빈 HTML 문서를 초기화합니다.
using (var document = new Aspose.Html.HTMLDocument())
{
    // 텍스트 요소를 생성하여 문서에 추가합니다.
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // HTML을 디스크에 있는 파일에 저장합니다.
    document.Save("document.html");
}
```

이 예에서 우리는 HTML 문서를 만들고 간단한 "Hello World!" 텍스트를 추가합니다. 그런 다음 HTML을 디스크의 파일에 저장합니다.

## 링크된 파일 없는 HTML

### 1단계: 간단한 HTML 파일 준비
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

여기서는 다른 파일에 대한 앵커 링크가 있는 기본 HTML 파일을 만듭니다.

### 2단계: 'document.html'을 메모리에 로드합니다.
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // 저장 옵션 인스턴스 생성
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    //최대 처리 깊이를 0으로 설정하면 연결된 HTML 파일을 잘라낼 수 있습니다.
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    // 문서를 저장하세요
    document.Save(@".\html-to-file-example\document.html", options);
}
```

이 예제에서는 HTML 문서를 메모리에 로드하고, 연결된 파일을 잘라내기 위한 최대 처리 깊이를 설정한 다음, 문서를 저장합니다. 

## HTML에서 MHTML로

### 1단계: 간단한 HTML 파일 준비
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

예제 2와 마찬가지로 다른 파일에 대한 앵커 링크가 있는 기본 HTML 파일을 만듭니다.

### 2단계: 'document.html'을 메모리에 로드하고 MHTML로 저장
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // 문서를 MHTML로 저장
    document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
}
```

여기서는 HTML 문서를 메모리에 로드하여 MHTML 형식으로 저장합니다.

## HTML에서 마크다운으로

### 1단계: HTML 코드 준비
```csharp
var html_code = "<H2>Hello World!</H2>";
```

 이 단계에서는 다음을 포함하는 HTML 코드 조각을 정의합니다.`<H2>` 요소.

### 2단계: HTML 코드에서 문서 초기화 및 마크다운으로 저장
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // 문서를 마크다운 파일로 저장합니다.
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

코드 조각에서 HTML 문서를 만들고 마크다운 파일로 저장합니다.

## SVG를 파일로

### 1단계: SVG 코드 준비
```csharp
var code = @"
    <svg xmlns='http://www.w3.org/2000/svg' 높이='80' 너비='300'>
        <g fill='none'>
            <path stroke='red' d='M5 20 l215 0' />
            <path stroke='black' d='M5 40 l215 0' />
            <path stroke='blue' d='M5 60 l215 0' />
        </g>
    </svg>";
```

여기서는 간단하고 다채로운 그래픽을 그리는 SVG 코드를 만들어 보겠습니다.

### 2단계: 코드에서 SVG 문서를 초기화하고 디스크에 저장
```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument(code, "."))
{
    // SVG 파일을 디스크에 저장
    document.Save("document.svg");
}
```

이 단계에서는 코드에서 SVG 문서를 만들고 SVG 파일로 저장합니다.

## 결론

Aspose.HTML for .NET은 .NET 애플리케이션에서 HTML 및 SVG 문서 처리를 간소화하는 다재다능한 라이브러리입니다. 이 가이드에서는 다섯 가지 필수 예를 다루었으며, 각각을 단계별 지침으로 나누었습니다. 문서를 만들거나, 조작하거나, 변환하든 Aspose.HTML이 도와드립니다. 이러한 단계를 따르면 이 강력한 도구를 마스터하는 데 큰 도움이 될 것입니다.

## 자주 묻는 질문

### 질문 1: .NET용 Aspose.HTML이란 무엇인가요?

A1: .NET용 Aspose.HTML은 HTML 및 SVG 문서 작업을 위한 광범위한 기능(작성, 조작, 변환 등)을 제공하는 .NET 라이브러리입니다.

### 질문 2: .NET용 Aspose.HTML은 어디서 다운로드할 수 있나요?

 A2: .NET용 Aspose.HTML은 다음에서 다운로드할 수 있습니다.[여기](https://releases.aspose.com/html/net/).

### Q3: .NET용 Aspose.HTML은 초보자에게 적합합니까?

A3: 네, Aspose.HTML for .NET은 초보자와 숙련된 개발자 모두 사용할 수 있습니다. 이 가이드의 예제는 초보자에게 친숙하도록 설계되었습니다.

### 질문 4: Aspose.HTML for .NET을 사용하여 HTML을 다른 형식으로 변환할 수 있나요?

A4: 네, Aspose.HTML for .NET은 예시에서 볼 수 있듯이 MHTML, Markdown 등 다양한 포맷으로의 변환을 지원합니다.

### 질문 5: .NET용 Aspose.HTML에 대한 지원은 어디에서 받을 수 있나요?

 A5: Aspose.HTML 커뮤니티 포럼에서 지원 및 질문에 대한 답변을 찾을 수 있습니다.[여기](https://forum.aspose.com/).