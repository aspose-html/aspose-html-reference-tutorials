---
title: Konfiguracja środowiska w .NET z Aspose.HTML
linktitle: Konfiguracja środowiska w .NET
second_title: Aspose.HTML .NET API manipulacji HTML
description: Dowiedz się, jak pracować z dokumentami HTML w .NET, używając Aspose.HTML do zadań takich jak zarządzanie skryptami, niestandardowe style, kontrola wykonywania JavaScript i wiele innych. Ten kompleksowy samouczek zawiera przykłady krok po kroku i FAQ, które pomogą Ci zacząć.
type: docs
weight: 10
url: /pl/net/advanced-features/environment-configuration/
---

W dzisiejszym cyfrowym świecie tworzenie i manipulowanie dokumentami HTML jest podstawowym zadaniem dla wielu programistów. Niezależnie od tego, czy tworzysz aplikację internetową, czy musisz przekonwertować HTML do innych formatów, takich jak PDF lub obrazy, Aspose.HTML dla .NET to potężne narzędzie, które warto mieć w swoim zestawie narzędzi. W tym samouczku przyjrzymy się różnym aspektom Aspose.HTML dla .NET, w tym wymaganiom wstępnym, importowaniu przestrzeni nazw i przykładom krok po kroku ze szczegółowymi wyjaśnieniami.

## Wymagania wstępne

Zanim przejdziemy do szczegółów dotyczących korzystania z Aspose.HTML dla platformy .NET, musisz upewnić się, że spełnione są następujące wymagania wstępne:

1. Visual Studio: Upewnij się, że masz zainstalowany program Visual Studio na swoim komputerze deweloperskim. Aspose.HTML dla .NET jest zaprojektowany tak, aby bezproblemowo współpracować z programem Visual Studio.

2.  Aspose.HTML dla .NET: Możesz pobrać bibliotekę Aspose.HTML dla .NET ze strony internetowej. Użyj poniższego łącza, aby uzyskać dostęp do strony pobierania:[Pobierz Aspose.HTML dla .NET](https://releases.aspose.com/html/net/).

3.  Instalacja i licencja: Po pobraniu biblioteki postępuj zgodnie z instrukcjami instalacji podanymi w dokumentacji. Możesz również potrzebować ważnej licencji, aby korzystać z niektórych zaawansowanych funkcji. Licencję możesz uzyskać na stronie internetowej Aspose:[Kup licencję Aspose.HTML](https://purchase.aspose.com/buy).

4.  Bezpłatna wersja próbna: Jeśli chcesz wypróbować Aspose.HTML przed zakupem licencji, możesz pobrać bezpłatną wersję próbną, klikając ten link:[Aspose.HTML Bezpłatna wersja próbna](https://releases.aspose.com/).

Teraz, gdy spełniłeś już wszystkie niezbędne wymagania, przejdźmy do następnej sekcji, w której zaimportujemy wymagane przestrzenie nazw.

## Importuj przestrzenie nazw

Aby efektywnie pracować z Aspose.HTML dla .NET, musisz zaimportować odpowiednie przestrzenie nazw do swojego projektu. Poniżej wymienimy przestrzenie nazw, których potrzebujesz do przykładów, które omówimy:

```csharp
using Aspose.Html;
using Aspose.Html.Configuration;
using Aspose.Html.Sandbox;
using Aspose.Html.Services;
using Aspose.Html.Saving;
using System;
using System.IO;
```

Po zaimportowaniu tych przestrzeni nazw można uzyskać dostęp do funkcjonalności udostępnianej przez Aspose.HTML dla .NET.

## Wyłącz wykonywanie skryptów

Zacznijmy od podstawowego przykładu wyłączenia wykonywania skryptu w dokumencie HTML i przekonwertowania go na PDF. Wykonaj następujące kroki:

1. Utwórz fragment kodu HTML i zapisz go w pliku o nazwie „document.html”.

```csharp
var code = "<span>Hello World!!</span> " +
           "<script>document.write('Have a nice day!');</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. Zainicjuj konfigurację Aspose.HTML, oznaczając „scripts” jako zasób niezaufany.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    configuration.Security |= Aspose.Html.Sandbox.Scripts;
    
    // Zainicjuj dokument HTML z określoną konfiguracją
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Konwertuj HTML do PDF
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

W tym przykładzie zapobiegliśmy wykonywaniu skryptów w dokumencie HTML, zapewniając bezpieczeństwo podczas konwersji do pliku PDF. Przejdźmy teraz do następnego przykładu.

## Określ arkusz stylów użytkownika

Czasami możesz chcieć zastosować niestandardowe style do elementów w dokumencie HTML. Oto jak możesz to zrobić za pomocą Aspose.HTML dla .NET:

1. Utwórz fragment kodu HTML i zapisz go w pliku o nazwie „document.html”.

```csharp
var code = @"<span>Hello World!!!</span>";
System.IO.File.WriteAllText("document.html", code);
```

2.  Ustaw niestandardowy kolor dla`<span>` element używający arkusza stylów użytkownika.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var userAgent = configuration.GetService<Aspose.Html.Services.IUserAgentService>();
    userAgent.UserStyleSheet = "span { color: green; }";
    
    // Zainicjuj dokument HTML z określoną konfiguracją
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Konwertuj HTML do PDF
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

 W tym przykładzie zastosowaliśmy niestandardowy styl do`<span>` element, ustawiając kolor tekstu na zielony. Aspose.HTML dla .NET pozwala na łatwą manipulację stylami.

## Limit czasu wykonania JavaScript

W przypadku potencjalnie czasochłonnego kodu JavaScript, konieczne jest ustawienie limitu czasu, aby zapobiec nieskończonemu wykonywaniu. Oto, jak możesz to zrobić:

1. Utwórz fragment kodu HTML z pętlą nieskończoną i zapisz go w pliku o nazwie „document.html”.

```csharp
var code = @"<script>while(true){}</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. Ustaw limit czasu wykonywania JavaScript na 10 sekund.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var runtime = configuration.GetService<Aspose.Html.Services.IRuntimeService>();
    runtime.JavaScriptTimeout = TimeSpan.FromSeconds(10);
    
    // Zainicjuj dokument HTML z określoną konfiguracją
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Poczekaj, aż wszystkie skrypty zostaną ukończone/anulowane i przekonwertuj HTML na PNG
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

tym przykładzie ograniczyliśmy czas wykonywania kodu JavaScript do 10 sekund, co gwarantuje, że skrypt nie będzie działał w nieskończoność, co mogłoby potencjalnie powodować problemy z wydajnością.

## Niestandardowy program obsługi wiadomości

Czasami może być konieczne obsłużenie komunikatów o błędach lub brakujących zasobów podczas ładowania dokumentu HTML. Oto przykład, jak utworzyć niestandardowy program obsługi komunikatów:

1. Utwórz fragment kodu HTML z brakującym odniesieniem do pliku obrazu i zapisz go w pliku o nazwie „document.html”.

```csharp
var code = @"<img src='missing.jpg'>";
System.IO.File.WriteAllText("document.html", code);
```

2. Dodaj obsługę komunikatów o błędach do usługi sieciowej w celu rejestrowania nieudanych żądań.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var network = configuration.GetService<Aspose.Html.Services.INetworkService>();
    network.MessageHandlers.Add(new LogMessageHandler());
    
    // Zainicjuj dokument HTML z określoną konfiguracją
    // Podczas ładowania dokumentu aplikacja spróbuje załadować obraz, a my zobaczymy wynik tej operacji w konsoli.
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Konwertuj HTML do PNG
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

W tym przykładzie dodaliśmy niestandardowy moduł obsługi wiadomości (`LogMessageHandler`) do rejestrowania informacji o nieudanych żądaniach. Może to być szczególnie przydatne do debugowania i obsługi brakujących zasobów w sposób elegancki.

## Wniosek

Aspose.HTML dla .NET to wszechstronna biblioteka, która umożliwia programistom wydajną pracę z dokumentami HTML. W tym samouczku omówiliśmy podstawowe koncepcje i podaliśmy przykłady krok po kroku dla typowych zadań, w tym zarządzania skryptami, dostosowywania arkuszy stylów, kontroli wykonywania JavaScript i obsługi niestandardowych wiadomości.

Postępując zgodnie z instrukcjami przedstawionymi w tym samouczku, możesz wykorzystać możliwości pakietu Aspose.HTML dla platformy .NET, aby tworzyć, edytować i konwertować dokumenty HTML w aplikacjach platformy .NET.

## Najczęściej zadawane pytania

### P1: Czy mogę używać Aspose.HTML dla .NET bez zakupu licencji?

A1: Tak, możesz wypróbować Aspose.HTML dla .NET, korzystając z bezpłatnej wersji próbnej, ale niektóre zaawansowane funkcje mogą wymagać ważnej licencji.

### P2: W jaki sposób mogę uzyskać licencję na Aspose.HTML dla platformy .NET?

 A2: Licencję można zakupić na stronie internetowej Aspose:[Kup licencję Aspose.HTML](https://purchase.aspose.com/buy).

### P3: Do jakich formatów mogę konwertować dokumenty HTML za pomocą Aspose.HTML dla .NET?

A3: Aspose.HTML dla .NET obsługuje konwersję do różnych formatów, w tym PDF, obrazów i innych.

### P4: Czy istnieje społeczność lub forum wsparcia dla Aspose.HTML dla .NET?

 A4: Tak, pomoc i wsparcie znajdziesz na forach Aspose:[Forum wsparcia Aspose.HTML](https://forum.aspose.com/).

### P5: Czy Aspose.HTML dla .NET udostępnia dokumentację i samouczki?

 A5: Tak, dostęp do dokumentacji jest możliwy tutaj:[Dokumentacja Aspose.HTML dla .NET](https://reference.aspose.com/html/net/).