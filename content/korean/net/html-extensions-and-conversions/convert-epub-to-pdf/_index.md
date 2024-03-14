---
title: Aspose.HTML을 사용하여 .NET에서 EPUB를 PDF로 변환
linktitle: .NET에서 EPUB를 PDF로 변환
second_title: Aspose.HTML .NET HTML 조작 API
description: .NET용 Aspose.HTML을 사용하여 EPUB를 PDF로 변환하는 방법을 알아보세요. 이 단계별 가이드에서는 원활한 문서 변환을 위한 사용자 정의 옵션, FAQ 등을 다룹니다.
type: docs
weight: 12
url: /ko/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

이 튜토리얼에서는 .NET용 Aspose.HTML을 사용하여 EPUB 파일을 PDF로 변환하는 방법을 살펴보겠습니다. Aspose.HTML은 HTML 및 EPUB 문서 작업을 위한 다양한 기능을 제공하는 강력한 .NET 라이브러리입니다. 전제 조건을 다루고, 필요한 네임스페이스를 가져오고, 여러 예를 분석하여 각 단계를 자세히 설명합니다.

## 전제 조건

시작하기 전에 다음 전제 조건이 충족되었는지 확인하세요.

1. .NET용 Aspose.HTML: .NET 프로젝트에 .NET용 Aspose.HTML이 설치되어 있는지 확인하세요. 다음에서 다운로드할 수 있습니다.[여기](https://releases.aspose.com/html/net/).

2. 데이터 디렉터리: EPUB 파일이 저장되는 데이터 디렉터리가 필요합니다.

이제 .NET용 Aspose.HTML을 사용하여 EPUB를 PDF로 변환하는 단계별 프로세스를 살펴보겠습니다.

## EPUB를 PDF로 변환

### 1단계: 프로젝트 초기화

.NET 프로젝트가 설정되어 있고 .NET용 Aspose.HTML이 설치되어 있는지 확인하세요.

### 2단계: 필수 네임스페이스 가져오기

C# 코드 파일에서 필요한 네임스페이스를 가져옵니다.

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
```

### 3단계: EPUB 파일 열기

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // 다음 단계로 계속하세요...
}
```

-  바꾸다`"Your Data Directory"` EPUB 파일이 있는 실제 디렉토리를 사용하세요.
- 이 코드는 읽을 수 있도록 EPUB 파일을 엽니다.

### 4단계: PDF 옵션 설정 및 변환 수행

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  인스턴스 만들기`PdfSaveOptions` PDF 변환 설정을 지정합니다.
-  사용`Converter.ConvertEPUB` 주어진 옵션을 사용하여 EPUB를 PDF로 변환하는 방법입니다.
- 결과 PDF를 "output.pdf"로 저장합니다.

## PDF 저장 옵션 지정

### 1단계: 프로젝트 초기화

.NET 프로젝트가 설정되어 있고 .NET용 Aspose.HTML이 설치되어 있는지 확인하세요.

### 2단계: 필수 네임스페이스 가져오기

C# 코드에서 필요한 네임스페이스를 가져옵니다.

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
```

### 3단계: EPUB 파일 열기

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // 다음 단계로 계속하세요...
}
```

-  바꾸다`"Your Data Directory"` EPUB 파일의 실제 디렉토리와 함께.
- 읽을 수 있도록 EPUB 파일을 엽니다.

### 4단계: PDF 옵션 사용자 정의

```csharp
var options = new PdfSaveOptions()
{
    PageSetup = { AnyPage = new Page() { Size = Size.FromPixels(3000, 1000) } },
    BackgroundColor = System.Drawing.Color.AliceBlue
};
```

-  인스턴스 만들기`PdfSaveOptions` 귀하의 요구 사항에 따라 사용자 정의하십시오.
- 이 예에서는 페이지 크기를 너비 3000픽셀, 높이 1000픽셀로 설정하고 배경색을 Alice Blue로 설정했습니다.

### 5단계: 변환 수행

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  사용`Converter.ConvertEPUB` 사용자 정의 옵션을 사용하여 EPUB를 PDF로 변환하는 방법입니다.
- 결과 PDF를 "output.pdf"로 저장합니다.

## 사용자 정의 스트림 공급자 사용

### 1단계: 프로젝트 초기화

.NET 프로젝트를 설정하고 .NET용 Aspose.HTML을 설치합니다.

### 2단계: 필수 네임스페이스 가져오기

C# 코드에서 필요한 네임스페이스를 가져옵니다.

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
```

### 3단계: EPUB 파일 열기

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // 다음 단계로 계속하세요...
}
```

-  바꾸다`"Your Data Directory"` EPUB 파일의 실제 디렉토리와 함께.
- 읽을 수 있도록 EPUB 파일을 엽니다.

### 4단계: 사용자 정의 스트림 공급자 사용

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    // 다음 단계로 계속하세요...
}
```

-  만들기`MemoryStreamProvider` 변환 결과를 메모리 스트림으로 관리합니다.
-  사용`Converter.ConvertEPUB` 사용자 정의 스트림 공급자를 사용하는 방법입니다.

### 5단계: 결과 저장

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.pdf"))
{
    memory.CopyTo(fs);
}
```

- 변환된 데이터가 포함된 메모리 스트림에 액세스합니다.
- 스트림 위치를 시작 부분으로 설정합니다.
- 출력 PDF 파일을 만들고 메모리 스트림의 내용을 파일에 복사합니다.

### 클래스 MemoryStreamProvider 소스 코드. 

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // 문서 렌더링 중에 생성된 MemoryStream 개체 목록
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // 이 메서드는 XPS, PDF 또는 TIFF 형식과 같이 출력 스트림이 하나만 필요할 때 호출됩니다.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // 이 메서드는 여러 출력 스트림을 생성해야 할 때 호출됩니다. 예를 들어 HTML을 렌더링하는 동안 이미지 파일(JPG, PNG 등) 목록을 표시합니다.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // 여기서 데이터로 채워진 스트림을 해제하고 예를 들어 하드 드라이브로 플러시할 수 있습니다.
            }
            public void Dispose()
            {
                // 리소스 해제
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
이제 다양한 옵션과 사용자 정의 가능성이 있는 .NET용 Aspose.HTML을 사용하여 EPUB 파일을 PDF로 변환하는 방법을 배웠습니다. Aspose.HTML은 프로세스를 단순화하여 문서 변환에 대한 유연성과 제어 기능을 제공합니다.

## 결론

.NET용 Aspose.HTML은 EPUB 파일을 PDF로 변환하기 위한 다목적 도구로, 결과 PDF 문서를 필요에 맞게 조정할 수 있는 사용자 정의 옵션을 제공합니다. 간단한 변환이 필요하든, 고급 사용자 정의가 필요하든 Aspose.HTML이 해결해 드립니다.

 아직 다운로드하지 않았다면 다음에서 .NET용 Aspose.HTML을 다운로드할 수 있습니다.[웹사이트](https://releases.aspose.com/html/net/) 지금 바로 .NET 애플리케이션에서 사용해 보세요.

---

## 자주 묻는 질문

### .NET용 Aspose.HTML은 무료로 사용할 수 있나요?
    .NET용 Aspose.HTML은 상용 제품이지만 무료 평가판을 사용할 수 있습니다.[여기](https://releases.aspose.com/).

### 변환된 PDF의 모양을 사용자 정의할 수 있습니까?
   예, 예 2에 표시된 것처럼 페이지 크기 및 배경색과 같은 옵션을 조정하여 PDF 모양을 사용자 정의할 수 있습니다.

### .NET용 Aspose.HTML에 대한 지원을 받으려면 어떻게 해야 합니까?
    다음에서 지원과 리소스를 찾을 수 있습니다.[Aspose.HTML 포럼](https://forum.aspose.com/).

### .NET용 Aspose.HTML로 변환할 수 있는 다른 형식이 있습니까?
   예, .NET용 Aspose.HTML은 HTML, EPUB 등을 포함한 다양한 문서 형식을 지원합니다.

### Aspose.HTML for ..NET은 대규모 문서 변환에 적합합니까?
   Aspose.HTML for .NET은 대규모 문서 변환을 효율적으로 처리하도록 설계되어 광범위한 애플리케이션에 적합합니다.

