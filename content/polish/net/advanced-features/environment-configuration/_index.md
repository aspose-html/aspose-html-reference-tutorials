---
title: Konfiguracja środowiska w .NET z Aspose.HTML
linktitle: Konfiguracja środowiska w .NET
second_title: Aspose.HTML .NET API manipulacji HTML
description: Dowiedz się, jak pracować z dokumentami HTML w .NET przy użyciu Aspose.HTML do zadań takich jak zarządzanie skryptami, niestandardowe style, kontrola wykonywania JavaScript i nie tylko. Ten obszerny samouczek zawiera przykłady krok po kroku i często zadawane pytania, które pomogą Ci zacząć.
type: docs
weight: 10
url: /pl/net/advanced-features/environment-configuration/
---

dzisiejszym cyfrowym świecie tworzenie dokumentów HTML i manipulowanie nimi jest podstawowym zadaniem wielu programistów. Niezależnie od tego, czy budujesz aplikację internetową, czy chcesz przekonwertować HTML na inne formaty, takie jak PDF lub obrazy, Aspose.HTML dla .NET jest potężnym narzędziem, które warto mieć w swoim zestawie narzędzi. W tym samouczku omówimy różne aspekty Aspose.HTML dla .NET, w tym wymagania wstępne, importowanie przestrzeni nazw i przykłady krok po kroku ze szczegółowymi wyjaśnieniami.

## Warunki wstępne

Zanim zaczniemy używać Aspose.HTML dla .NET, musisz upewnić się, że spełniasz następujące wymagania wstępne:

1. Visual Studio: Upewnij się, że masz zainstalowany program Visual Studio na komputerze programistycznym. Aspose.HTML dla .NET został zaprojektowany do bezproblemowej współpracy z Visual Studio.

2.  Aspose.HTML dla .NET: Możesz pobrać bibliotekę Aspose.HTML dla .NET ze strony internetowej. Aby uzyskać dostęp do strony pobierania, użyj poniższego łącza:[Pobierz Aspose.HTML dla .NET](https://releases.aspose.com/html/net/).

3. Instalacja i licencja: Po pobraniu biblioteki postępuj zgodnie z instrukcjami instalacji zawartymi w dokumentacji. Do korzystania z niektórych zaawansowanych funkcji może być również potrzebna ważna licencja. Licencję można uzyskać ze strony internetowej Aspose:[Kup licencję Aspose.HTML](https://purchase.aspose.com/buy).

4.  Bezpłatna wersja próbna: Jeśli chcesz wypróbować Aspose.HTML przed zakupem licencji, możesz uzyskać bezpłatną wersję próbną z tego linku:[Bezpłatna wersja próbna Aspose.HTML](https://releases.aspose.com/).

Teraz, gdy masz już niezbędne wymagania wstępne, przejdźmy do następnej sekcji, w której zaimportujemy wymagane przestrzenie nazw.

## Importuj przestrzenie nazw

Aby efektywnie pracować z Aspose.HTML dla .NET, musisz zaimportować odpowiednie przestrzenie nazw do swojego projektu. Poniżej wymienimy przestrzenie nazw potrzebne w przykładach, które omówimy:

```csharp
using Aspose.Html;
using Aspose.Html.Configuration;
using Aspose.Html.Sandbox;
using Aspose.Html.Services;
using Aspose.Html.Saving;
using System;
using System.IO;
```

Po zaimportowaniu tych przestrzeni nazw możesz uzyskać dostęp do funkcjonalności zapewnianej przez Aspose.HTML dla .NET.

## Wyłącz wykonywanie skryptów

Zacznijmy od podstawowego przykładu wyłączenia wykonywania skryptu w dokumencie HTML i konwersji go do formatu PDF. Wykonaj następujące kroki:

1. Utwórz fragment kodu HTML i zapisz go w pliku o nazwie „document.html”.

```csharp
var code = "<span>Hello World!!</span> " +
           "<script>document.write('Have a nice day!');</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. Zainicjuj konfigurację Aspose.HTML, zaznaczając „skrypty” jako niezaufany zasób.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    configuration.Security |= Aspose.Html.Sandbox.Scripts;
    
    // Zainicjuj dokument HTML z określoną konfiguracją
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Konwertuj HTML na PDF
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

W tym przykładzie uniemożliwiliśmy wykonanie skryptów w dokumencie HTML, zapewniając bezpieczeństwo podczas konwersji go do formatu PDF. Przejdźmy teraz do następnego przykładu.

## Określ arkusz stylów użytkownika

Czasami możesz chcieć zastosować niestandardowe style do elementów w dokumencie HTML. Oto jak możesz to zrobić za pomocą Aspose.HTML dla .NET:

1. Utwórz fragment kodu HTML i zapisz go w pliku o nazwie „document.html”.

```csharp
var code = @"<span>Hello World!!!</span>";
System.IO.File.WriteAllText("document.html", code);
```

2.  Ustaw niestandardowy kolor dla`<span>` element przy użyciu arkusza stylów użytkownika.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var userAgent = configuration.GetService<Aspose.Html.Services.IUserAgentService>();
    userAgent.UserStyleSheet = "span { color: green; }";
    
    // Zainicjuj dokument HTML z określoną konfiguracją
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Konwertuj HTML na PDF
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

 W tym przykładzie zastosowaliśmy niestandardowy styl do pliku`<span>`elementu, ustawiając jego kolor tekstu na zielony. Aspose.HTML dla .NET pozwala z łatwością manipulować stylami.

## Limit czasu wykonania JavaScript

W przypadku potencjalnie czasochłonnego kodu JavaScript konieczne jest ustawienie limitu czasu, aby zapobiec nieokreślonemu wykonaniu. Oto jak możesz to zrobić:

1. Utwórz fragment kodu HTML z nieskończoną pętlą i zapisz go w pliku o nazwie „document.html”.

```csharp
var code = @"<script>while(true){}</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. Ustaw limit czasu wykonania JavaScript na 10 sekund.

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

W tym przykładzie ograniczyliśmy czas wykonania JavaScript do 10 sekund, zapewniając, że skrypt nie będzie działał w nieskończoność, co mogłoby potencjalnie spowodować problemy z wydajnością.

## Niestandardowa obsługa wiadomości

Czasami podczas ładowania dokumentu HTML może być konieczne obsłużenie komunikatów o błędach lub brakujących zasobów. Oto przykład tworzenia niestandardowej procedury obsługi wiadomości:

1. Utwórz fragment kodu HTML z brakującym odwołaniem do pliku obrazu i zapisz go w pliku o nazwie „document.html”.

```csharp
var code = @"<img src='missing.jpg'>";
System.IO.File.WriteAllText("document.html", code);
```

2. Dodaj moduł obsługi komunikatów o błędach do usługi sieciowej, aby rejestrować nieudane żądania.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var network = configuration.GetService<Aspose.Html.Services.INetworkService>();
    network.MessageHandlers.Add(new LogMessageHandler());
    
    // Zainicjuj dokument HTML z określoną konfiguracją
    // Podczas ładowania dokumentu aplikacja spróbuje załadować obraz, a wynik tej operacji zobaczymy w konsoli.
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Konwertuj HTML na PNG
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

W tym przykładzie dodaliśmy niestandardową procedurę obsługi wiadomości (`LogMessageHandler`) do rejestrowania informacji o nieudanych żądaniach. Może to być szczególnie przydatne do debugowania i sprawnego obsługi brakujących zasobów.

## Wniosek

Aspose.HTML dla .NET to wszechstronna biblioteka, która umożliwia programistom efektywną pracę z dokumentami HTML. W tym samouczku omówiliśmy podstawowe pojęcia i podaliśmy szczegółowe przykłady typowych zadań, w tym zarządzania skryptami, dostosowywania arkuszy stylów, kontroli wykonywania JavaScript i niestandardowej obsługi komunikatów.

Wykonując kroki opisane w tym samouczku, możesz wykorzystać moc Aspose.HTML dla .NET do bezpiecznego tworzenia, manipulowania i konwertowania dokumentów HTML w aplikacjach .NET.

## Często zadawane pytania

### P1: Czy mogę używać Aspose.HTML dla .NET bez zakupu licencji?

Odpowiedź 1: Tak, możesz wypróbować Aspose.HTML dla .NET w bezpłatnej wersji próbnej, ale niektóre zaawansowane funkcje mogą wymagać ważnej licencji.

### P2: Jak mogę uzyskać licencję na Aspose.HTML dla .NET?

 A2: Możesz kupić licencję na stronie Aspose:[Kup licencję Aspose.HTML](https://purchase.aspose.com/buy).

### P3: Na jakie formaty mogę konwertować dokumenty HTML przy użyciu Aspose.HTML dla .NET?

O3: Aspose.HTML dla .NET obsługuje konwersję do różnych formatów, w tym PDF, obrazów i innych.

### P4: Czy istnieje forum społeczności lub wsparcia dla Aspose.HTML dla .NET?

 Odpowiedź 4: Tak, możesz znaleźć pomoc i wsparcie na forach Aspose:[Forum pomocy technicznej Aspose.HTML](https://forum.aspose.com/).

### P5: Czy Aspose.HTML dla .NET udostępnia dokumentację i samouczki?

 Odpowiedź 5: Tak, możesz uzyskać dostęp do dokumentacji tutaj:[Aspose.HTML dla dokumentacji .NET](https://reference.aspose.com/html/net/).