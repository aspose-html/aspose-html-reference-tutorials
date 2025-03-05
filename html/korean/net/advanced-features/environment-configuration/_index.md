---
title: Aspose.HTML을 사용한 .NET 환경 구성
linktitle: .NET에서의 환경 구성
second_title: Aspose.HTML .NET HTML 조작 API
description: Aspose.HTML을 사용하여 .NET에서 HTML 문서를 다루는 방법을 알아보세요. 스크립트 관리, 사용자 지정 스타일, JavaScript 실행 제어 등의 작업을 위해. 이 포괄적인 튜토리얼은 여러분이 시작할 수 있도록 단계별 예제와 FAQ를 제공합니다.
type: docs
weight: 10
url: /ko/net/advanced-features/environment-configuration/
---

오늘날의 디지털 세계에서 HTML 문서를 만들고 조작하는 것은 많은 개발자에게 기본적인 작업입니다. 웹 애플리케이션을 빌드하든 HTML을 PDF나 이미지와 같은 다른 형식으로 변환해야 하든 Aspose.HTML for .NET은 툴킷에 넣어두면 강력한 도구입니다. 이 튜토리얼에서는 필수 구성 요소, 네임스페이스 가져오기, 자세한 설명이 포함된 단계별 예제를 포함하여 Aspose.HTML for .NET의 다양한 측면을 살펴보겠습니다.

## 필수 조건

.NET용 Aspose.HTML을 사용하기 전에 다음 필수 구성 요소가 있는지 확인해야 합니다.

1. Visual Studio: 개발 머신에 Visual Studio가 설치되어 있는지 확인하세요. Aspose.HTML for .NET은 Visual Studio와 원활하게 작동하도록 설계되었습니다.

2.  Aspose.HTML for .NET: 웹사이트에서 Aspose.HTML for .NET 라이브러리를 다운로드할 수 있습니다. 다음 링크를 사용하여 다운로드 페이지에 액세스하세요.[.NET용 Aspose.HTML 다운로드](https://releases.aspose.com/html/net/).

3.  설치 및 라이센스: 라이브러리를 다운로드한 후 설명서에 제공된 설치 지침을 따르세요. 일부 고급 기능을 사용하려면 유효한 라이센스가 필요할 수도 있습니다. Aspose 웹사이트에서 라이센스를 얻을 수 있습니다.[Aspose.HTML 라이센스 구매](https://purchase.aspose.com/buy).

4.  무료 평가판: 라이선스를 구매하기 전에 Aspose.HTML을 사용해 보고 싶으시다면 다음 링크에서 무료 평가판 버전을 받으실 수 있습니다:[Aspose.HTML 무료 체험판](https://releases.aspose.com/).

이제 필요한 전제 조건이 갖춰졌으므로 다음 섹션으로 넘어가서 필요한 네임스페이스를 가져오겠습니다.

## 네임스페이스 가져오기

.NET용 Aspose.HTML을 효과적으로 사용하려면 프로젝트에 적절한 네임스페이스를 가져와야 합니다. 아래에서 다룰 예제에 필요한 네임스페이스를 나열합니다.

```csharp
using Aspose.Html;
using Aspose.Html.Configuration;
using Aspose.Html.Sandbox;
using Aspose.Html.Services;
using Aspose.Html.Saving;
using System;
using System.IO;
```

이러한 네임스페이스를 가져오면 .NET용 Aspose.HTML이 제공하는 기능에 액세스할 수 있습니다.

## 스크립트 실행 비활성화

HTML 문서 내에서 스크립트 실행을 비활성화하고 PDF로 변환하는 기본 예제부터 시작해 보겠습니다. 다음 단계를 따르세요.

1. HTML 코드 조각을 만들고 "document.html"이라는 파일에 저장합니다.

```csharp
var code = "<span>Hello World!!</span> " +
           "<script>document.write('Have a nice day!');</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. Aspose.HTML 구성을 초기화하고 'scripts'를 신뢰할 수 없는 리소스로 표시합니다.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    configuration.Security |= Aspose.Html.Sandbox.Scripts;
    
    // 지정된 구성으로 HTML 문서를 초기화합니다.
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // HTML을 PDF로 변환
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

이 예에서 우리는 HTML 문서 내에서 스크립트 실행을 방지하여 PDF로 변환하는 동안 보안을 보장했습니다. 이제 다음 예로 넘어가겠습니다.

## 사용자 스타일시트 지정

때로는 HTML 문서 내의 요소에 사용자 지정 스타일을 적용하고 싶을 수 있습니다. 다음은 .NET용 Aspose.HTML을 사용하여 이를 수행하는 방법입니다.

1. HTML 코드 조각을 만들고 "document.html"이라는 파일에 저장합니다.

```csharp
var code = @"<span>Hello World!!!</span>";
System.IO.File.WriteAllText("document.html", code);
```

2.  사용자 정의 색상을 설정하세요`<span>` 사용자 스타일 시트를 사용하는 요소.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var userAgent = configuration.GetService<Aspose.Html.Services.IUserAgentService>();
    userAgent.UserStyleSheet = "span { color: green; }";
    
    // 지정된 구성으로 HTML 문서를 초기화합니다.
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // HTML을 PDF로 변환
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

 이 예에서 우리는 사용자 정의 스타일을 적용했습니다.`<span>` 요소, 텍스트 색상을 녹색으로 설정합니다. Aspose.HTML for .NET을 사용하면 스타일을 쉽게 조작할 수 있습니다.

## JavaScript 실행 시간 초과

잠재적으로 시간이 많이 걸리는 JavaScript 코드를 다룰 때는 무기한 실행을 방지하기 위해 타임아웃을 설정하는 것이 필수적입니다. 방법은 다음과 같습니다.

1. 무한 루프가 있는 HTML 코드 조각을 만들고 "document.html"이라는 이름의 파일에 저장합니다.

```csharp
var code = @"<script>while(true){}</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. JavaScript 실행 시간제한을 10초로 설정합니다.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var runtime = configuration.GetService<Aspose.Html.Services.IRuntimeService>();
    runtime.JavaScriptTimeout = TimeSpan.FromSeconds(10);
    
    // 지정된 구성으로 HTML 문서를 초기화합니다.
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // 모든 스크립트가 완료/취소될 때까지 기다렸다가 HTML을 PNG로 변환합니다.
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

이 예에서는 JavaScript 실행 시간을 10초로 제한하여 스크립트가 무한정 실행되지 않도록 했습니다. 무한정 실행되면 성능 문제가 발생할 가능성이 있습니다.

## 사용자 정의 메시지 핸들러

때로는 HTML 문서를 로드할 때 오류 메시지나 누락된 리소스를 처리해야 할 수도 있습니다. 다음은 사용자 지정 메시지 핸들러를 만드는 방법의 예입니다.

1. 누락된 이미지 파일 참조로 HTML 코드 조각을 만들고 "document.html"이라는 파일에 저장합니다.

```csharp
var code = @"<img src='missing.jpg'>";
System.IO.File.WriteAllText("document.html", code);
```

2. 네트워크 서비스에 오류 메시지 처리기를 추가하여 실패한 요청을 기록합니다.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var network = configuration.GetService<Aspose.Html.Services.INetworkService>();
    network.MessageHandlers.Add(new LogMessageHandler());
    
    // 지정된 구성으로 HTML 문서를 초기화합니다.
    // 문서를 로드하는 동안 애플리케이션은 이미지를 로드하려고 시도하며, 콘솔에서 이 작업의 결과를 볼 수 있습니다.
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // HTML을 PNG로 변환
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

이 예에서 우리는 사용자 정의 메시지 핸들러를 추가했습니다.`LogMessageHandler`) 실패한 요청에 대한 정보를 기록합니다. 이는 특히 디버깅 및 누락된 리소스를 우아하게 처리하는 데 유용할 수 있습니다.

## 결론

Aspose.HTML for .NET은 개발자가 HTML 문서를 효율적으로 작업할 수 있도록 하는 다재다능한 라이브러리입니다. 이 튜토리얼에서는 필수 개념을 다루고 스크립트 관리, 스타일시트 사용자 지정, JavaScript 실행 제어 및 사용자 지정 메시지 처리를 포함한 일반적인 작업에 대한 단계별 예를 제공했습니다.

이 튜토리얼에 설명된 단계를 따르면 Aspose.HTML for .NET의 기능을 활용하여 .NET 애플리케이션에서 자신 있게 HTML 문서를 만들고, 조작하고, 변환할 수 있습니다.

## 자주 묻는 질문

### 질문 1: 라이선스를 구매하지 않고도 .NET용 Aspose.HTML을 사용할 수 있나요?

A1: 네, 무료 평가판으로 Aspose.HTML for .NET을 사용해 보실 수 있지만, 일부 고급 기능을 사용하려면 유효한 라이선스가 필요할 수 있습니다.

### 질문 2: .NET용 Aspose.HTML 라이선스를 어떻게 얻을 수 있나요?

 A2: Aspose 웹사이트에서 라이센스를 구매할 수 있습니다.[Aspose.HTML 라이센스 구매](https://purchase.aspose.com/buy).

### 질문 3: Aspose.HTML for .NET을 사용하여 HTML 문서를 어떤 형식으로 변환할 수 있나요?

A3: .NET용 Aspose.HTML은 PDF, 이미지 등 다양한 형식으로의 변환을 지원합니다.

### 질문 4: .NET용 Aspose.HTML에 대한 커뮤니티나 지원 포럼이 있나요?

 A4: 네, Aspose 포럼에서 도움말과 지원을 찾을 수 있습니다.[Aspose.HTML 지원 포럼](https://forum.aspose.com/).

### Q5: .NET용 Aspose.HTML은 설명서와 튜토리얼을 제공하나요?

 A5: 네, 여기에서 설명서에 접근할 수 있습니다:[.NET 설명서용 Aspose.HTML](https://reference.aspose.com/html/net/).