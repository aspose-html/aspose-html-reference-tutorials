---
title: Aspose.HTML을 사용하여 .NET에서 문서 만들기
linktitle: .NET에서 문서 만들기
second_title: Aspose.HTML .NET HTML 조작 API
description: .NET용 Aspose.HTML의 힘을 최대한 활용하세요. HTML 및 SVG 문서를 쉽게 만들고, 조작하고, 최적화하는 방법을 배우세요. 단계별 예제와 FAQ를 살펴보세요.
weight: 14
url: /ko/net/html-document-manipulation/creating-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML을 사용하여 .NET에서 문서 만들기


끊임없이 진화하는 웹 개발 세계에서는 앞서 나가는 것이 필수적입니다. .NET용 Aspose.HTML은 개발자에게 HTML 문서 작업을 위한 강력한 툴킷을 제공합니다. 처음부터 시작하든, 파일에서 로드하든, URL에서 가져오든, SVG 문서를 처리하든, 이 라이브러리는 필요한 다양성을 제공합니다.

이 단계별 가이드에서는 .NET용 Aspose.HTML 사용의 기본 사항을 살펴보고, 웹 개발 프로젝트에서 이 강력한 도구를 사용할 준비가 되었는지 확인합니다. 세부 사항을 살펴보기 전에 여정을 시작하기 위해 필수 조건과 필요한 네임스페이스를 살펴보겠습니다.

## 필수 조건

이 튜토리얼을 성공적으로 따라하고 .NET용 Aspose.HTML의 기능을 활용하려면 다음과 같은 필수 구성 요소가 필요합니다.

- .NET Framework 또는 .NET Core가 설치된 Windows 컴퓨터.
- Visual Studio와 같은 코드 편집기.
- C# 프로그래밍에 대한 기본 지식.

이제 필수 조건을 갖추었으니 시작해 보겠습니다.

## 네임스페이스 가져오기

Aspose.HTML for .NET을 사용하기 전에 필요한 네임스페이스를 가져와야 합니다. 이러한 네임스페이스에는 HTML 문서 작업에 필수적인 클래스와 메서드가 포함되어 있습니다. 아래는 가져와야 하는 네임스페이스 목록입니다.

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
    // 텍스트 요소를 생성하여 문서에 추가합니다.
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // 문서를 디스크에 저장합니다.
    document.Save("document.html");
}
```

이 예에서 우리는 빈 HTML 문서를 만들고 "Hello World!" 텍스트를 추가하는 것으로 시작합니다. 그런 다음 문서를 파일에 저장합니다.

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

여기서는 "Hello World!" 콘텐츠가 있는 파일을 준비한 다음 HTML 문서로 로드합니다. 문서의 콘텐츠를 콘솔에 인쇄합니다.

## URL에서 HTML 문서 만들기

### 1단계: 웹 페이지에서 문서 로드

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    // 문서 내용을 출력 스트림에 씁니다.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

이 예제에서는 웹 페이지에서 HTML 문서를 직접 로드하여 해당 내용을 표시합니다.

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

여기서는 문자열 변수에서 HTML 문서를 생성하여 파일에 저장합니다.

## MemoryStream에서 HTML 문서 생성

### 1단계: 메모리 스트림 객체 생성

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    // HTML 코드를 메모리 객체에 쓰세요
    sw.Write("<p>Hello World!</p>");
    // 위치를 시작으로 설정하세요
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

이 예제에서는 메모리 스트림에서 HTML 문서를 생성하고 파일에 저장합니다.

## SVG 문서 작업

### 1단계: 문자열에서 SVG 문서 초기화

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", ".))
{
    // 문서 내용을 출력 스트림에 씁니다.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

여기서는 문자열로부터 SVG 문서를 생성하고 표시합니다.

## HTML 문서를 비동기적으로 로드하기

### 1단계: HTML 문서 인스턴스 생성

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### 2단계: 'ReadyStateChange' 이벤트 구독

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    // 'ReadyState' 속성의 값을 확인합니다.
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

이 예제에서는 HTML 문서를 비동기적으로 로드하고 로드가 완료되면 'ReadyStateChange' 이벤트를 처리하여 콘텐츠를 표시합니다.

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

이 예제에서는 HTML 문서를 비동기적으로 로드하고 완료되면 'OnLoad' 이벤트를 처리하여 콘텐츠를 표시하는 방법을 보여줍니다.

## 결론적으로

역동적인 웹 개발 세계에서 적절한 도구를 사용하는 것은 매우 중요합니다. Aspose.HTML for .NET은 HTML 및 SVG 문서를 효율적으로 만들고, 조작하고, 처리할 수 있는 수단을 제공합니다. 이 포괄적인 가이드는 필수 사항을 안내하여 프로젝트에서 Aspose.HTML for .NET의 힘을 활용할 수 있도록 합니다.

## 자주 묻는 질문

### 질문 1: .NET용 Aspose.HTML이란 무엇인가요?

A1: Aspose.HTML for .NET은 개발자가 HTML 및 SVG 문서로 작업할 수 있도록 하는 강력한 .NET 라이브러리입니다. 처음부터 문서를 만드는 것부터 기존 HTML 및 SVG 파일을 구문 분석하고 조작하는 것까지 광범위한 기능을 제공합니다.

### 질문 2: .NET Core에서 Aspose.HTML for .NET을 사용할 수 있나요?

A2: 네, Aspose.HTML for .NET은 .NET Framework와 .NET Core 모두와 호환되므로 최신 .NET 애플리케이션에 적합한 다양한 선택입니다.

### 질문 3: .NET용 Aspose.HTML은 웹 스크래핑 및 파싱에 적합합니까?

A3: 물론입니다! Aspose.HTML for .NET은 URL과 문자열에서 HTML 문서를 로드하는 기능 덕분에 웹 스크래핑 및 파싱 작업에 탁월한 선택입니다. 데이터를 추출하고, 분석을 수행하는 등의 작업을 수행할 수 있습니다.

### 질문 4: .NET용 Aspose.HTML에 대한 지원은 어떻게 받을 수 있나요?

 A4: Aspose.HTML for .NET을 사용하는 동안 문제가 발생하거나 질문이 있는 경우 다음을 방문할 수 있습니다.[애스포지 포럼](https://forum.aspose.com/) 커뮤니티와 Aspose 전문가로부터 지원과 도움을 받으세요.

### A5: 자세한 문서와 다운로드 옵션은 어디에서 찾을 수 있나요?

A5: 포괄적인 문서와 다운로드 옵션에 대한 액세스는 다음 링크를 참조하세요.

- [선적 서류 비치](https://reference.aspose.com/html/net/)
- [다운로드](https://releases.aspose.com/html/net/)
- [구입하다](https://purchase.aspose.com/buy)
- [무료 체험](https://releases.aspose.com/)
- [임시 라이센스](https://purchase.aspose.com/temporary-license/)
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
