---
title: Aspose.HTML을 사용하여 .NET에서 EPUB를 XPS로 변환
linktitle: .NET에서 EPUB를 XPS로 변환
second_title: Aspose.HTML .NET HTML 조작 API
description: Aspose.HTML for .NET을 사용하여 .NET에서 EPUB를 XPS로 변환하는 방법을 알아보세요. 손쉬운 변환을 위한 단계별 가이드를 따르세요.
type: docs
weight: 13
url: /ko/net/html-extensions-and-conversions/convert-epub-to-xps/
---

.NET 애플리케이션에서 EPUB 파일을 XPS 형식으로 변환하는 매끄러운 방법을 찾고 계신가요? Aspose.HTML for .NET은 이를 손쉽게 달성할 수 있는 강력한 솔루션을 제공합니다. 이 단계별 가이드에서는 Aspose.HTML을 사용하여 EPUB를 XPS로 변환하는 과정을 안내해 드리겠습니다. 시작해 볼까요!

## 필수 조건

EPUB를 XPS로 변환하는 과정을 시작하기 전에 다음과 같은 필수 구성 요소가 있는지 확인해야 합니다.

### 1. .NET 라이브러리용 Aspose.HTML

 프로젝트에 Aspose.HTML for .NET 라이브러리가 설치되어 있는지 확인하세요. 아직 설치하지 않았다면 다음에서 얻을 수 있습니다.[.NET용 Aspose.HTML 다운로드 페이지](https://releases.aspose.com/html/net/).

### 2. EPUB 파일 입력

XPS로 변환하려는 EPUB 파일이 필요합니다. 변환할 수 있는 EPUB 파일이 있는지 확인하세요.

### 3. .NET 개발 환경

이 가이드에서는 사용자의 컴퓨터에 .NET 개발 환경이 설정되어 있다고 가정합니다.

## 네임스페이스 가져오기

시작하려면 Aspose.HTML에 필요한 네임스페이스를 가져와야 합니다.

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## EPUB를 XPS로 변환

EPUB 파일을 XPS 형식으로 변환하는 과정을 여러 단계로 나누어 보겠습니다.

### 1.1단계: EPUB 파일 열기

먼저 FileStream을 사용하여 기존 EPUB 파일을 열어서 읽습니다.

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // 변환 프로세스를 계속 진행하세요
}
```

### 1.2단계: XpsSaveOptions 생성

XpsSaveOptions 인스턴스를 만듭니다. 이 단계는 XPS 출력을 구성하는 데 중요합니다.

```csharp
var options = new XpsSaveOptions();
```

### 1.3단계: EPUB를 XPS로 변환

이제 ConvertEPUB 메서드를 호출하여 EPUB를 XPS로 변환해 보겠습니다.

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## 사용자 정의 XPS 옵션 지정

페이지 크기 및 배경색과 같은 사용자 정의 옵션을 지정하여 XPS 출력을 더욱 세부적으로 사용자 정의할 수 있습니다.

### 2.1단계: 사용자 정의 페이지 크기 및 배경색

사용자 지정 페이지 크기와 배경색을 사용하여 XpsSaveOptions 인스턴스를 만듭니다.

```csharp
var options = new XpsSaveOptions()
{
    PageSetup =
    {
        AnyPage = new Page()
        {
            Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
        }
    },
    BackgroundColor = System.Drawing.Color.AliceBlue,
};
```

### 2.2단계: 사용자 정의 옵션을 사용하여 EPUB를 XPS로 변환

이제 ConvertEPUB 메서드를 호출하여 사용자 지정 옵션을 사용하여 EPUB를 XPS로 변환합니다.

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## 사용자 정의 스트림 공급자 사용

이 단계에서는 사용자 지정 스트림 공급자를 사용하여 EPUB를 XPS로 변환하고 결과 데이터를 조작할 수 있습니다.

### 3.1단계: MemoryStreamProvider 생성

MemoryStreamProvider 인스턴스를 생성합니다.

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    // 변환 프로세스를 계속 진행하세요
}
```

### 3.2단계: Stream Provider를 사용하여 EPUB를 XPS로 변환

MemoryStreamProvider를 사용하여 EPUB를 XPS로 변환:

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### 3.3단계: 결과 액세스 및 저장

변환된 데이터가 포함된 메모리 스트림을 검색하여 출력 파일에 저장합니다.

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### 클래스 MemoryStreamProvider 소스 코드

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // 문서 렌더링 중에 생성된 MemoryStream 개체 목록
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // 이 메서드는 예를 들어 XPS, PDF 또는 TIFF 형식의 경우와 같이 단 하나의 출력 스트림만 필요할 때 호출됩니다.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // 이 메서드는 여러 출력 스트림을 만들어야 할 때 호출됩니다. 예를 들어 HTML을 렌더링하는 동안 이미지 파일(JPG, PNG 등)을 나열합니다.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // 여기서 데이터로 채워진 스트림을 해제하고 예를 들어 하드 드라이브에 플러시할 수 있습니다.
            }
            public void Dispose()
            {
                // 리소스 해제
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
축하합니다! Aspose.HTML for .NET을 사용하여 EPUB 파일을 XPS 형식으로 성공적으로 변환했습니다.

## 결론

이 포괄적인 튜토리얼에서는 Aspose.HTML for .NET을 활용하여 다양한 사용자 지정 옵션을 사용하여 EPUB 파일을 XPS 형식으로 변환하는 방법을 살펴보았습니다. 노련한 개발자이든 방금 시작한 개발자이든 Aspose.HTML은 프로세스를 간소화하여 EPUB에서 XPS로의 변환을 쉽게 처리할 수 있도록 합니다.

 질문이 있거나 문제가 발생했습니까? 다음을 확인하세요.[Aspose.HTML 문서](https://reference.aspose.com/html/net/) 더 많은 통찰력을 원하거나 도움을 요청하세요[Aspose.HTML 커뮤니티 포럼](https://forum.aspose.com/).

## 자주 묻는 질문

### .NET용 Aspose.HTML이란 무엇인가요?
.NET용 Aspose.HTML은 개발자가 .NET 애플리케이션에서 HTML, EPUB 및 XPS 문서로 작업할 수 있도록 해주는 강력한 라이브러리입니다.

### .NET용 Aspose.HTML은 어디서 다운로드할 수 있나요?
 .NET용 Aspose.HTML은 다음에서 다운로드할 수 있습니다.[다운로드 페이지](https://releases.aspose.com/html/net/).

### Aspose.HTML for .NET에 대한 무료 평가판이 있나요?
 네, 무료 체험판을 받으실 수 있습니다.[여기](https://releases.aspose.com/).

### .NET용 Aspose.HTML에 대한 임시 라이선스를 어떻게 얻을 수 있나요?
 임시 면허를 받으려면 다음을 방문하세요.[임시 라이센스 페이지](https://purchase.aspose.com/temporary-license/).

### Aspose.HTML for .NET에 대한 추가 튜토리얼과 문서는 어디에서 찾을 수 있나요?
 다양한 튜토리얼과 자세한 문서를 탐색해보세요.[Aspose.HTML 문서](https://reference.aspose.com/html/net/) 페이지.