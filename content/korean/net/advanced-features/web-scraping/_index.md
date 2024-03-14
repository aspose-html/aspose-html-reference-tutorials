---
title: Aspose.HTML을 사용한 .NET의 웹 스크래핑
linktitle: .NET의 웹 스크래핑
second_title: Aspose.HTML .NET HTML 조작 API
description: Aspose.HTML을 사용하여 .NET에서 HTML 문서를 조작하는 방법을 알아보세요. 향상된 웹 개발을 위해 요소를 효과적으로 탐색, 필터링, 쿼리 및 선택합니다.
type: docs
weight: 13
url: /ko/net/advanced-features/web-scraping/
---

오늘날 디지털 시대에 HTML 문서에서 정보를 조작하고 추출하는 것은 개발자의 일반적인 작업입니다. .NET용 Aspose.HTML은 .NET 애플리케이션에서 HTML 처리 및 조작을 단순화하는 강력한 도구입니다. 이 튜토리얼에서는 전제 조건, 네임스페이스 및 단계별 예제를 포함하여 Aspose.HTML for .NET의 다양한 측면을 탐색하여 잠재력을 최대한 활용하는 데 도움을 드립니다.

## 전제 조건

.NET용 Aspose.HTML의 세계로 뛰어들기 전에 몇 가지 전제 조건이 필요합니다.

1. 개발 환경: Visual Studio 또는 .NET 개발용 기타 호환 IDE가 설정된 작업 개발 환경이 있는지 확인하세요.

2.  .NET용 Aspose.HTML: 다음에서 .NET용 Aspose.HTML 라이브러리를 다운로드하여 설치하세요.[다운로드 링크](https://releases.aspose.com/html/net/). 필요에 따라 무료 평가판 버전과 라이선스 버전 중에서 선택할 수 있습니다.

3. HTML에 대한 기본 지식: Aspose.HTML for .NET을 효과적으로 사용하려면 HTML 구조와 요소에 대한 지식이 필수적입니다.

## 네임스페이스 가져오기

시작하려면 C# 프로젝트에서 필요한 네임스페이스를 가져와야 합니다. 이러한 네임스페이스는 .NET 클래스 및 기능용 Aspose.HTML에 대한 액세스를 제공합니다.

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.XPath;
using Aspose.Html.Css;
```

전제 조건을 갖추고 네임스페이스를 가져온 후 몇 가지 주요 예제를 단계별로 분석하여 .NET용 Aspose.HTML을 효과적으로 사용하는 방법을 보여드리겠습니다.

## HTML을 통해 탐색

이 예에서는 HTML 문서를 탐색하고 해당 요소에 단계별로 액세스합니다.

```csharp
public static void NavigateThroughHTML()
{
    // HTML 코드 준비
    var html_code = "<span>Hello</span> <span>World!</span>";
    
    // 준비된 코드에서 문서 초기화
    using (var document = new HTMLDocument(html_code, "."))
    {
        // BODY의 첫 번째 하위 항목(첫 번째 SPAN)에 대한 참조를 가져옵니다.
        var element = document.Body.FirstChild;
        Console.WriteLine(element.TextContent); // 출력: 안녕하세요

        // HTML 요소 사이의 공백에 대한 참조를 가져옵니다.
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // 출력: ' '

        // 두 번째 SPAN 요소에 대한 참조 가져오기
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // 출력: 월드!
    }
}
```

 이 예에서는 HTML 문서를 만들고 첫 번째 하위 항목(`SPAN` 요소), 요소 사이의 공백, 두 번째`SPAN` 요소, 기본 탐색을 보여줍니다.

## 노드 필터 사용

노드 필터를 사용하면 HTML 문서 내의 특정 요소를 선택적으로 처리할 수 있습니다.

```csharp
public static void NodeFilterUsageExample()
{
    // HTML 코드 준비
    var code = @"
        <p>Hello</p>
        <img src='image1.png'>
        <img src='image2.png'>
        <p>World!</p>";
    
    // 준비된 코드를 기반으로 문서 초기화
    using (var document = new HTMLDocument(code, "."))
    {
        // 이미지 요소에 대한 사용자 정의 필터를 사용하여 TreeWalker 만들기
        using (var iterator = document.CreateTreeWalker(document, NodeFilter.SHOW_ALL, new OnlyImageFilter()))
        {
            while (iterator.NextNode() != null)
            {
                var image = (HTMLImageElement)iterator.CurrentNode;
                Console.WriteLine(image.Src);
                // 출력: image1.png
                // 출력: image2.png
            }
        }
    }
}
```

 이 예에서는 사용자 정의 노드 필터를 사용하여 특정 요소를 추출하는 방법을 보여줍니다(이 경우`IMG` 요소)를 HTML 문서에서 가져옵니다.

## XPath 쿼리

XPath 쿼리를 사용하면 특정 기준에 따라 HTML 문서의 요소를 검색할 수 있습니다.

```csharp
public static void XPathQueryUsageExample()
{
    // HTML 코드 준비
    var code = @"
        <div class='happy'>
            <div>
                <span>Hello!</span>
            </div>
        </div>
        <p class='happy'>
            <span>World</span>
        </p>
    ";
    
    // 준비된 코드를 기반으로 문서 초기화
    using (var document = new HTMLDocument(code, "."))
    {
        // XPath 표현식을 평가하여 특정 요소 선택
        var result = document.Evaluate("//*[@class='happy']//스팬",
                                        document,
                                        null,
                                        XPathResultType.Any,
                                        null);
        
        // 결과 노드를 반복합니다.
        for (Node node; (node = result.IterateNext()) != null;)
        {
            Console.WriteLine(node.TextContent);
            // 출력: 안녕하세요
            // 출력: 월드!
        }
    }
}
```

이 예에서는 XPath 쿼리를 사용하여 해당 속성과 구조를 기반으로 HTML 문서에서 요소를 찾는 방법을 보여줍니다.

## CSS 선택자

CSS 선택기는 CSS 스타일시트가 요소를 대상으로 지정하는 방법과 유사하게 HTML 문서에서 요소를 선택하는 대체 방법을 제공합니다.

```csharp
public static void CSSSelectorUsageExample()
{
    // HTML 코드 준비
    var code = @"
        <div class='happy'>
            <div>
                <span>Hello</span>
            </div>
        </div>
        <p class='happy'>
            <span>World!</span>
        </p>
    ";
    
    // 준비된 코드를 기반으로 문서 초기화
    using (var document = new HTMLDocument(code, "."))
    {
        //CSS 선택기를 사용하여 클래스 및 계층 구조를 기반으로 요소를 추출합니다.
        var elements = document.QuerySelectorAll(".happy span");
        
        // 결과 요소 목록을 반복합니다.
        foreach (HTMLElement element in elements)
        {
            Console.WriteLine(element.InnerHTML);
            // 출력: 안녕하세요
            // 출력: 월드!
        }
    }
}
```

여기에서는 CSS 선택기를 사용하여 HTML 문서의 특정 요소를 대상으로 지정하는 방법을 보여줍니다.

이러한 예제를 통해 .NET용 Aspose.HTML을 사용하여 HTML 문서의 요소를 탐색, 필터링, 쿼리 및 선택하는 방법에 대한 기본적인 이해를 얻었습니다.

## 결론

 .NET용 Aspose.HTML은 .NET 개발자가 HTML 문서를 효율적으로 작업할 수 있도록 지원하는 다목적 라이브러리입니다. 탐색, 필터링, 쿼리 및 요소 선택을 위한 강력한 기능을 통해 다양한 HTML 처리 작업을 원활하게 처리할 수 있습니다. 이 튜토리얼을 따르고 다음 문서를 탐색하여[.NET 문서용 Aspose.HTML](https://reference.aspose.com/html/net/)을 사용하면 .NET 애플리케이션에 대해 이 도구의 잠재력을 최대한 활용할 수 있습니다.

## FAQ

### Q1. .NET용 Aspose.HTML은 무료로 사용할 수 있나요?

A1: .NET용 Aspose.HTML은 무료 평가판을 제공하지만 프로덕션 용도로 사용하려면 라이센스를 구입해야 합니다. 라이선스 세부정보 및 옵션은 다음에서 확인할 수 있습니다.[Aspose.HTML 구매](https://purchase.aspose.com/buy).

### Q2. .NET용 Aspose.HTML의 임시 라이선스를 어떻게 얻을 수 있나요?

 A2: 다음에서 테스트 목적으로 임시 라이센스를 얻을 수 있습니다.[Aspose.HTML 임시 라이센스](https://purchase.aspose.com/temporary-license/).

### Q3. .NET용 Aspose.HTML에 대한 도움말이나 지원은 어디서 찾을 수 있나요?

 A3: 문제가 발생하거나 질문이 있는 경우[Aspose.HTML 포럼](https://forum.aspose.com/) 도움과 지역 사회 지원을 위해.

### Q4. .NET용 Aspose.HTML을 학습하기 위한 추가 리소스가 있습니까?

 A4: 이 튜토리얼과 함께 다음 항목에 대한 더 많은 튜토리얼과 문서를 탐색할 수 있습니다.[.NET 문서 페이지용 Aspose.HTML](https://reference.aspose.com/html/net/).

### Q5. .NET용 Aspose.HTML은 최신 .NET 버전과 호환됩니까?

A5: .NET용 Aspose.HTML은 최신 .NET 버전 및 기술과의 호환성을 보장하기 위해 정기적으로 업데이트됩니다.