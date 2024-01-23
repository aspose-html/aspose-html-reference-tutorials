---
title: Aspose.HTML을 사용하여 .NET에서 문서 만들기
linktitle: .NET에서 문서 만들기
second_title: Aspose.HTML .NET HTML 조작 API
description: .NET용 Aspose.HTML의 강력한 기능을 활용해 보세요. HTML 및 SVG 문서를 쉽게 생성, 조작 및 최적화하는 방법을 알아보세요. 단계별 예시와 FAQ를 살펴보세요.
type: docs
weight: 14
url: /ko/net/html-document-manipulation/creating-a-document/
---

끊임없이 진화하는 웹 개발 세계에서 앞서가는 것은 필수적입니다. .NET용 Aspose.HTML은 개발자에게 HTML 문서 작업을 위한 강력한 도구 키트를 제공합니다. 처음부터 시작하든, 파일에서 로드하든, URL에서 가져오든, SVG 문서를 처리하든 이 라이브러리는 필요한 다양성을 제공합니다.

이 단계별 가이드에서는 .NET용 Aspose.HTML을 사용하는 기본 사항을 자세히 살펴보고 웹 개발 프로젝트에서 이 강력한 도구를 사용할 수 있는 준비를 갖추도록 하겠습니다. 세부 사항을 살펴보기 전에, 여정을 시작하는 데 필요한 전제 조건과 네임스페이스를 살펴보겠습니다.

## 전제 조건

이 튜토리얼을 성공적으로 따르고 .NET용 Aspose.HTML의 기능을 활용하려면 다음 전제 조건이 필요합니다.

- .NET Framework 또는 .NET Core가 설치된 Windows 머신.
- Visual Studio와 같은 코드 편집기.
- C# 프로그래밍에 대한 기본 지식.

이제 전제 조건이 준비되었으므로 시작해 보겠습니다.

## 네임스페이스 가져오기

.NET용 Aspose.HTML을 사용하기 전에 필요한 네임스페이스를 가져와야 합니다. 이러한 네임스페이스에는 HTML 문서 작업에 필수적인 클래스와 메서드가 포함되어 있습니다. 다음은 가져와야 하는 네임스페이스 목록입니다.

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

이러한 네임스페이스를 가져왔으므로 이제 단계별 예제를 살펴볼 준비가 되었습니다.

## 처음부터 HTML 문서 만들기

### 1단계: 빈 HTML 문서 초기화

```csharp
// 빈 HTML 문서를 초기화합니다.
using (var document = new Aspose.Html.HTMLDocument())
{
    // 텍스트 요소를 만들어 문서에 추가하세요.
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // 문서를 디스크에 저장합니다.
    document.Save("document.html");
}
```

이 예에서는 빈 HTML 문서를 만들고 "Hello World!"를 추가하는 것부터 시작합니다. 그것에 문자를 보내세요. 그런 다음 문서를 파일에 저장합니다.

## 파일에서 HTML 문서 만들기

### 1단계: 'document.html' 파일 준비

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### 2단계: 'document.html' 파일에서 로드

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // 문서 내용을 출력 스트림에 씁니다.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

여기서는 "Hello World!"라는 파일을 준비합니다. 콘텐츠를 HTML 문서로 로드합니다. 문서의 내용을 콘솔에 인쇄합니다.

## URL에서 HTML 문서 만들기

### 1단계: 웹 페이지에서 문서 로드

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    // 문서 내용을 출력 스트림에 씁니다.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

이 예에서는 웹 페이지에서 직접 HTML 문서를 로드하고 해당 내용을 표시합니다.

## 문자열에서 HTML 문서 만들기

### 1단계: HTML 코드 준비

```csharp
var html_code = "<p>Hello World!</p>";
```

### 2단계: 문자열 변수에서 문서 초기화

```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // 문서를 디스크에 저장합니다.
    document.Save("document.html");
}
```

여기서는 문자열 변수로 HTML 문서를 생성하고 이를 파일에 저장합니다.

## MemoryStream에서 HTML 문서 만들기

### 1단계: 메모리 스트림 객체 생성

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    // 메모리 객체에 HTML 코드 쓰기
    sw.Write("<p>Hello World!</p>");
    // 위치를 처음으로 설정
    sw.Flush();
    mem.Seek(0, System.IO.SeekOrigin.Begin);
    // 메모리 스트림에서 문서 초기화
    using (var document = new Aspose.Html.HTMLDocument(mem, "."))
    {
        // 문서를 디스크에 저장합니다.
        document.Save("document.html");
    }
}
```

이 예에서는 메모리 스트림에서 HTML 문서를 생성하고 이를 파일에 저장합니다.

## SVG 문서 작업

### 1단계: 문자열에서 SVG 문서 초기화

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "."))
{
    // 문서 내용을 출력 스트림에 씁니다.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

여기서는 문자열에서 SVG 문서를 생성하고 표시합니다.

## HTML 문서를 비동기적으로 로드하기

### 1단계: HTML 문서 인스턴스 생성

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### 2단계: 'ReadyStateChange' 이벤트 구독

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    //'ReadyState' 속성의 값을 확인하세요.
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### 3단계: 지정된 Uri에서 비동기적으로 탐색

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

이 예에서는 HTML 문서를 비동기적으로 로드하고 'ReadyStateChange' 이벤트를 처리하여 로드가 완료되면 콘텐츠를 표시합니다.

## 'OnLoad' 이벤트 처리

### 1단계: HTML 문서 인스턴스 생성

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### 2단계: 'OnLoad' 이벤트 구독

```csharp
document.OnLoad += (sender, @event) =>
{
    Console.WriteLine(document.DocumentElement.OuterHTML);
    Console.WriteLine("Loading is completed. Press any key to continue...");
};
```

### 3단계: 지정된 Uri에서 비동기적으로 탐색

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

이 예에서는 HTML 문서를 비동기적으로 로드하고 'OnLoad' 이벤트를 처리하여 완료 시 콘텐츠를 표시하는 방법을 보여줍니다.

## 결론적으로

역동적인 웹 개발 세계에서는 원하는 대로 사용할 수 있는 올바른 도구를 갖는 것이 중요합니다. .NET용 Aspose.HTML은 HTML 및 SVG 문서를 효율적으로 생성, 조작 및 처리할 수 있는 수단을 제공합니다. 이 포괄적인 가이드는 프로젝트에서 Aspose.HTML for .NET의 강력한 기능을 활용할 수 있도록 필수 사항을 안내했습니다.

## FAQ

### Q1: .NET용 Aspose.HTML이란 무엇입니까?

A1: .NET용 Aspose.HTML은 개발자가 HTML 및 SVG 문서 작업을 할 수 있게 해주는 강력한 .NET 라이브러리입니다. 처음부터 문서 작성부터 기존 HTML 및 SVG 파일 구문 분석 및 조작에 이르기까지 광범위한 기능을 제공합니다.

### Q2: .NET Core와 함께 .NET용 Aspose.HTML을 사용할 수 있나요?

A2: 예, .NET용 Aspose.HTML은 .NET Framework 및 .NET Core 모두와 호환되므로 최신 .NET 애플리케이션을 위한 다양한 선택이 가능합니다.

### Q3: .NET용 Aspose.HTML은 웹 스크래핑 및 구문 분석에 적합합니까?

A3: 물론이죠! .NET용 Aspose.HTML은 URL 및 문자열에서 HTML 문서를 로드하는 기능 덕분에 웹 스크래핑 및 구문 분석 작업에 탁월한 선택입니다. 데이터 추출, 분석 수행 등을 수행할 수 있습니다.

### Q4: .NET용 Aspose.HTML 지원에 어떻게 액세스할 수 있나요?

 A4: .NET용 Aspose.HTML을 사용하는 동안 문제가 발생하거나 질문이 있는 경우 다음을 방문하세요.[Aspose 포럼](https://forum.aspose.com/) 커뮤니티와 Aspose 전문가의 지원과 도움을 받으세요.

### A5: 자세한 문서와 다운로드 옵션은 어디에서 찾을 수 있습니까?

A5: 포괄적인 문서와 다운로드 옵션에 대한 액세스를 보려면 다음 링크를 참조하세요.

- [선적 서류 비치](https://reference.aspose.com/html/net/)
- [다운로드](https://releases.aspose.com/html/net/)
- [구입하다](https://purchase.aspose.com/buy)
- [무료 시험판](https://releases.aspose.com/)
- [임시면허](https://purchase.aspose.com/temporary-license/)