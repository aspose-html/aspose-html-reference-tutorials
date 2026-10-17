---
date: 2026-05-14
description: Dowiedz się, jak ustawić limit czasu w Aspose.HTML for Java, skonfigurować
  Runtime Service dla konwersji html na png, zapobiegać nieskończonym pętlom i zwiększyć
  wydajność.
keywords:
- html to png conversion
- convert html to png
- java html processing
- prevent infinite loops java
- control script execution
linktitle: Konfiguracja Runtime Service w Aspose.HTML
schemas:
- author: Aspose
  dateModified: '2026-05-14'
  description: Learn how to set timeout in Aspose.HTML for Java, configure the Runtime
    Service for html to png conversion, prevent infinite loops, and boost performance.
  headline: How to Set Timeout for html to png conversion in Aspose.HTML for Java
    Runtime Service
  type: TechArticle
- description: Learn how to set timeout in Aspose.HTML for Java, configure the Runtime
    Service for html to png conversion, prevent infinite loops, and boost performance.
  name: How to Set Timeout for html to png conversion in Aspose.HTML for Java Runtime
    Service
  steps:
  - name: '**Java Development Kit (JDK)** – install it from [Oracle''s website](https://www.oracle.com/java/technologies/javase-downloads.html).'
    text: '**Java Development Kit (JDK)** – install it from [Oracle''s website](https://www.oracle.com/java/technologies/javase-downloads.html).'
  - name: '**Aspose.HTML for Java Library** – grab the newest build from the [Aspose
      releases page](https://releases.aspose.com/html/java/).'
    text: '**Aspose.HTML for Java Library** – grab the newest build from the [Aspose
      releases page](https://releases.aspose.com/html/java/).'
  - name: '**IDE** – IntelliJ IDEA, Eclipse, or NetBeans will work fine.'
    text: '**IDE** – IntelliJ IDEA, Eclipse, or NetBeans will work fine.'
  - name: '**Basic Java & HTML knowledge** – essential for following the code snippets.'
    text: '**Basic Java & HTML knowledge** – essential for following the code snippets.'
  type: HowTo
- questions:
  - answer: It lets you control script execution time, helping to **prevent infinite
      loops** and keep conversions responsive.
    question: What is the purpose of the Runtime Service in Aspose.HTML for Java?
  - answer: Get the latest version from the [releases page](https://releases.aspose.com/html/java/).
    question: How can I download Aspose.HTML for Java?
  - answer: Yes, disposing releases native resources and prevents memory leaks.
    question: Is it necessary to dispose of the `document` and `configuration` objects?
  - answer: Absolutely – change the `TimeSpan.fromSeconds()` argument to whatever
      limit fits your scenario.
    question: Can I set the JavaScript timeout to a value other than 5 seconds?
  - answer: Visit the [Aspose.HTML forum](https://forum.aspose.com/c/html/29) for
      community and staff assistance.
    question: Where can I find help if I run into issues?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: Jak ustawić limit czasu dla konwersji html na png w Aspose.HTML for Java Runtime
  Service
url: /pl/java/configuring-environment/configure-runtime-service/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak ustawić limit czasu dla konwersji html do png w Aspose.HTML dla Java Runtime Service

## Wprowadzenie
Jeśli chcesz **ustawić limit czasu** dla skryptów podczas pracy z Aspose.HTML dla Java, trafiłeś we właściwe miejsce. Kontrola wykonywania skryptów nie tylko zapobiega nieskończonym pętlom, ale także przyspiesza **konwersję html do png** i utrzymuje responsywność aplikacji. W tym samouczku przeprowadzimy Cię krok po kroku przez konfigurację Runtime Service, ograniczenie wykonywania skryptów oraz ostateczne wygenerowanie obrazu PNG z HTML bez zawieszania programu.

## Szybkie odpowiedzi
- **Co robi Runtime Service?** Umożliwia kontrolowanie czasu wykonywania skryptów i zarządzanie zasobami podczas przetwarzania HTML.  
- **Jak ustawić limit czasu dla JavaScript?** Pobierz `IRuntimeService` z konfiguracji i wywołaj `setJavaScriptTimeout(TimeSpan.fromSeconds(...))`.  
- **Czy mogę zapobiec nieskończonym pętlom?** Tak – limit czasu zatrzymuje pętle przekraczające określony limit.  
- **Czy to wpływa na konwersję html do png?** Nie, konwersja przebiega po zakończeniu skryptu lub jego przerwaniu przez limit czasu.  
- **Jakiej wersji Aspose.HTML potrzebuję?** Najnowsze wydanie ze strony pobierania Aspose.

## Jak ustawić limit czasu dla konwersji html do png w usłudze Aspose.HTML Runtime Service
Załaduj Runtime Service, zdefiniuj `TimeSpan` (np. 5 sekund) przy użyciu `TimeSpan.fromSeconds` i zastosuj go za pomocą `setJavaScriptTimeout`. To ogranicza wykonywanie JavaScript, zatrzymuje niekontrolowane pętle i zapewnia, że konwersja kończy się przewidywalnie, nie zużywając nieograniczonych zasobów CPU, jednocześnie pozwalając typowym skryptom na pełne wykonanie.

## Wymagania wstępne
Zanim przejdziemy do szczegółów, upewnij się, że masz następujące elementy:

1. **Java Development Kit (JDK)** – zainstaluj go ze [strony Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Biblioteka Aspose.HTML for Java** – pobierz najnowszą wersję ze [strony wydań Aspose](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse lub NetBeans będą odpowiednie.  
4. **Podstawowa znajomość Java i HTML** – niezbędna do śledzenia fragmentów kodu.

## Importowanie pakietów
Instrukcje importu wprowadzają wymagane klasy z Java i Aspose.HTML do zakresu, umożliwiając obsługę plików i konfigurację usług. `java.io.IOException` jest wyjątkiem rzucanym, gdy operacja I/O nie powiedzie się lub zostanie przerwana.

```java
import java.io.IOException;
```

## Krok 1: Utwórz plik HTML z kodem JavaScript
Utworzenie pliku HTML z pętlą JavaScript demonstruje potencjalny scenariusz nieskończonego skryptu, który później zatrzymamy przy użyciu limitu czasu. `java.io.FileWriter` to klasa służąca do zapisywania plików znakowych na dysku.

```java
String code = "<h1>Runtime Service</h1>\r\n" +
        "<script> while(true) {} </script>\r\n" +
        "<p>The Runtime Service optimizes your system by helping it start apps and programs faster.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("runtime-service.html")) {
    fileWriter.write(code);
}
```

- Skrypt `while(true) {}` reprezentuje potencjalną nieskończoną pętlę.  
- `FileWriter` zapisuje zawartość HTML do **runtime-service.html**.

## Krok 2: Skonfiguruj obiekt Configuration
Klasa `Configuration` przechowuje ustawienia dla wszystkich usług Aspose.HTML, w tym Runtime Service, i pełni rolę centralnego punktu dla niestandardowych opcji.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Krok 3: Skonfiguruj Runtime Service
`IRuntimeService` zapewnia kontrolę nad wykonywaniem skryptów, taką jak ustawianie limitów czasu, aby chronić środowisko hosta przed niekontrolowanym kodem.

```java
try {
    com.aspose.html.services.IRuntimeService runtimeService = configuration.getService(com.aspose.html.services.IRuntimeService.class);
    runtimeService.setJavaScriptTimeout(com.aspose.html.utils.TimeSpan.fromSeconds(5));
```

- `setJavaScriptTimeout` ogranicza wykonywanie skryptu do **5 sekund**, skutecznie **zapobiegając nieskończonym pętlom**.  
- To także **ogranicza wykonywanie skryptu** dla wszelkiego ciężkiego kodu po stronie klienta.

## Krok 4: Załaduj dokument HTML z konfiguracją
Klasa `Document` ładuje i reprezentuje stronę HTML z zastosowaną konfiguracją, zapewniając egzekwowanie reguły limitu czasu podczas parsowania.

```java
    com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("runtime-service.html", configuration);
```

- Dokument respektuje wcześniej zdefiniowany limit czasu, więc niekończąca się pętla zostanie zatrzymana po 5 sekundach.

## Krok 5: Konwertuj HTML do PNG
`ImageSaveOptions` określa format wyjściowy i opcje renderowania dla konwersji obrazu, umożliwiając czystą **konwersję html do png** po zakończeniu lub zatrzymaniu skryptu.

```java
    com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.ImageSaveOptions(),
        "runtime-service_out.png"
    );
```

- `ImageSaveOptions` instruuje Aspose.HTML, aby wyeksportował obraz PNG.  
- Powstały plik, **runtime-service_out.png**, przedstawia wyrenderowany HTML bez zawieszania.

## Krok 6: Oczyść zasoby
Wywołanie `dispose()` zwalnia natywne zasoby używane przez obiekty Aspose.HTML, zapobiegając wyciekom pamięci w długotrwale działających aplikacjach.

```java
} finally {
    if (document != null) {
        document.dispose();
    }
    if (configuration != null) {
        configuration.dispose();
    }
}
```

- Prawidłowe zwalnianie zasobów jest niezbędne w długotrwale działających aplikacjach.

## Dlaczego to ma znaczenie
Limit czasu zabezpiecza Twój pipeline konwersji, przerywając długotrwale działające skrypty, co zapobiega blokowaniu wątków i skraca całkowity czas przetwarzania, szczególnie w usługach wielokrotnych. Dzięki limitowi 5 sekund zachowujesz normalne zachowanie strony, jednocześnie odcinając nadużywające lub błędne skrypty, co prowadzi do bardziej przewidywalnej wydajności konwersji html do png.

## Częste pułapki i rozwiązywanie problemów
- **Limit czasu zbyt krótki** – Złożone strony z wieloma zasobami mogą wymagać dłuższego limitu. Zwiększ wartość `TimeSpan`, jeśli obserwujesz przedwczesne zakończenia.  
- **Brak zwolnienia zasobów** – Zapomnienie o wywołaniu `dispose()` może prowadzić do wycieków pamięci natywnej, szczególnie przy przetwarzaniu wielu dokumentów w pętli.  
- **Nieprawidłowy obiekt konfiguracji** – Zawsze pobieraj `IRuntimeService` z tej samej instancji `Configuration`, której używasz do ładowania dokumentu; w przeciwnym razie limit czasu nie zostanie zastosowany.

## Najczęściej zadawane pytania

**Q: Jaki jest cel Runtime Service w Aspose.HTML dla Java?**  
A: Umożliwia kontrolowanie czasu wykonywania skryptów, pomagając **zapobiegać nieskończonym pętlom** i utrzymywać responsywność konwersji.

**Q: Jak mogę pobrać Aspose.HTML dla Java?**  
A: Pobierz najnowszą wersję ze [strony wydań](https://releases.aspose.com/html/java/).

**Q: Czy konieczne jest zwolnienie obiektów `document` i `configuration`?**  
A: Tak, zwolnienie zasobów uwalnia natywne zasoby i zapobiega wyciekom pamięci.

**Q: Czy mogę ustawić limit czasu JavaScript na inną wartość niż 5 sekund?**  
A: Oczywiście – zmień argument w `TimeSpan.fromSeconds()` na dowolny limit pasujący do Twojego scenariusza.

**Q: Gdzie mogę znaleźć pomoc w razie problemów?**  
A: Odwiedź [forum Aspose.HTML](https://forum.aspose.com/c/html/29) w celu uzyskania pomocy od społeczności i personelu.

{{< blocks/products/products-backtop-button >}}

## Powiązane samouczki

- [Utwórz plik HTML w Javie i skonfiguruj usługę sieciową (Aspose.HTML)](/html/java/configuring-environment/setup-network-service/)
- [Jak ustawić limit czasu – Zarządzanie limitem czasu sieci w Aspose.HTML dla Java](/html/java/message-handling-networking/network-timeout/)
- [Konwertuj HTML do PNG przy użyciu Aspose.HTML dla Java](/html/java/conversion-html-to-various-image-formats/convert-html-to-png/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}