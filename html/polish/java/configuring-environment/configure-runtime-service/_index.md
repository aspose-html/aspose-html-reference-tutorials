---
date: 2026-02-10
description: Dowiedz się, jak ustawić limit czasu w Aspose.HTML dla Javy, skonfigurować
  usługę Runtime Service do konwertowania HTML na PNG, zapobiegać nieskończonym pętlom
  i zwiększyć wydajność.
linktitle: Configure Runtime Service in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Jak ustawić limit czasu w usłudze Aspose.HTML dla Java Runtime
url: /pl/java/configuring-environment/configure-runtime-service/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak ustawić limit czasu w usłudze Runtime Aspose.HTML dla Java

## Wprowadzenie
Jeśli szukasz **jak ustawić limit czasu** dla skryptów podczas pracy z Aspose.HTML dla Java, trafiłeś we właściwe miejsce. Kontrola wykonywania skryptów nie tylko zapobiega nieskończonym pętlom, ale także pomaga **szybciej konwertować html na png** i utrzymać responsywność aplikacji. W tym samouczku przeprowadzimy Cię krok po kroku przez konfigurację usługi Runtime, ograniczenie wykonywania skryptu i ostateczne wygenerowanie obrazu PNG z HTML bez zawieszania programu.

## Jak ustawić limit czasu w usłudze Runtime Aspose.HTML
Zrozumienie celu usługi Runtime ułatwia dostrzeżenie, dlaczego limit czasu jest niezbędny. Usługa działa jako piaskownica dla kodu po stronie klienta, dając możliwość zatrzymania wymykającego się JavaScriptu, zanim zużyje wszystkie cykle CPU. Ustawiając limit czasu chronisz serwer przed scenariuszami odmowy usługi (DoS) i zapewniasz, że **konwersja html do png** zakończy się w przewidywalnym czasie.

## Szybkie odpowiedzi
- **Co robi usługa Runtime?** Umożliwia kontrolowanie czasu wykonywania skryptu i zarządzanie zasobami podczas przetwarzania HTML.  
- **Jak ustawić limit czasu dla JavaScript?** Użyj `runtimeService.setJavaScriptTimeout(TimeSpan.fromSeconds(...))`.  
- **Czy mogę zapobiec nieskończonym pętlom?** Tak – limit czasu zatrzymuje pętle przekraczające określony limit.  
- **Czy ma to wpływ na konwersję HTML‑do‑PNG?** Nie, konwersja przebiega po zakończeniu skryptu lub jego przerwaniu przez limit czasu.  
- **Jakiej wersji Aspose.HTML wymaga się?** Najnowszej dostępnej na stronie pobierania Aspose.  

## Wymagania wstępne
Zanim przejdziemy do szczegółów, upewnij się, że masz następujące elementy:

1. **Java Development Kit (JDK)** – zainstaluj go ze [strony Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Biblioteka Aspose.HTML dla Java** – pobierz najnowszą wersję ze [strony wydań Aspose](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse lub NetBeans będą odpowiednie.  
4. **Podstawowa znajomość Java i HTML** – niezbędna do śledzenia fragmentów kodu.

## Importowanie pakietów
Najpierw zaimportuj klasy, których będziesz potrzebować. Import `java.io.IOException` jest wymagany do obsługi plików.

```java
import java.io.IOException;
```

## Krok 1: Utworzenie pliku HTML z kodem JavaScript
Zaczniemy od wygenerowania prostego pliku HTML zawierającego pętlę JavaScript. Ta pętla działałaby w nieskończoność, gdyby nie wymuszony limit czasu, co czyni ją idealnym przykładem dla usługi Runtime.

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

## Krok 2: Utworzenie obiektu konfiguracji
Następnie utwórz instancję `Configuration`. Ten obiekt jest podstawą wszystkich usług Aspose.HTML, w tym usługi Runtime.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Krok 3: Konfiguracja usługi Runtime
Tutaj faktycznie **ustawiamy limit czasu**. Pobierając `IRuntimeService` z konfiguracji, możemy określić limit wykonywania JavaScriptu.

```java
try {
    com.aspose.html.services.IRuntimeService runtimeService = configuration.getService(com.aspose.html.services.IRuntimeService.class);
    runtimeService.setJavaScriptTimeout(com.aspose.html.utils.TimeSpan.fromSeconds(5));
```

- `setJavaScriptTimeout` ogranicza wykonywanie skryptu do **5 sekund**, skutecznie **zapobiegając nieskończonym pętlom**.  
- To także **ogranicza wykonywanie skryptu** dla wszelkiego ciężkiego kodu po stronie klienta.

## Krok 4: Załadowanie dokumentu HTML z konfiguracją
Teraz wczytaj plik HTML przy użyciu konfiguracji zawierającej naszą regułę limitu czasu.

```java
    com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("runtime-service.html", configuration);
```

- Dokument respektuje wcześniej zdefiniowany limit, więc niekończąca się pętla zostanie zatrzymana po 5 sekundach.

## Krok 5: Konwersja HTML do PNG
Po bezpiecznym załadowaniu dokumentu możemy **konwertować html na png**. Konwersja odbywa się dopiero po zakończeniu skryptu lub jego przerwaniu przez limit czasu.

```java
    com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.ImageSaveOptions(),
        "runtime-service_out.png"
    );
```

- `ImageSaveOptions` instruuje Aspose.HTML, aby wyeksportował obraz w formacie PNG.  
- Powstały plik, **runtime-service_out.png**, przedstawia wyrenderowany HTML bez zawieszania aplikacji.

## Krok 6: Czyszczenie zasobów
Na koniec zwolnij obiekty, aby uwolnić pamięć i uniknąć wycieków.

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

- Poprawne zwalnianie jest kluczowe w aplikacjach działających długo.

## Dlaczego to ważne
Ustawienie limitu czasu to nie tylko zabezpieczenie; bezpośrednio zwiększa niezawodność **konwersji html do png**. Gdy integrujesz Aspose.HTML w usłudze internetowej przetwarzającej HTML generowany przez użytkowników, złośliwy skrypt mógłby w przeciwnym razie zablokować wątek na nieokreślony czas. Skromny limit (np. 5 sekund) daje legalnym skryptom wystarczająco czasu, jednocześnie odcinając nadużycia.

## Typowe pułapki i rozwiązywanie problemów
- **Limit czasu zbyt krótki** – Złożone strony z wieloma zasobami mogą wymagać dłuższego limitu. Zwiększ wartość `TimeSpan`, jeśli obserwujesz przedwczesne przerwania.  
- **Brak zwolnienia zasobów** – Zapomnienie o wywołaniu `dispose()` może prowadzić do wycieków pamięci natywnej, szczególnie przy przetwarzaniu wielu dokumentów w pętli.  
- **Nieprawidłowy obiekt konfiguracji** – Zawsze pobieraj `IRuntimeService` z tej samej instancji `Configuration`, której używasz do ładowania dokumentu; w przeciwnym razie limit nie zostanie zastosowany.

## Najczęściej zadawane pytania

**P: Jaki jest cel usługi Runtime w Aspose.HTML dla Java?**  
O: Umożliwia kontrolowanie czasu wykonywania skryptu, pomagając **zapobiegać nieskończonym pętlom** i utrzymać responsywność konwersji.

**P: Jak mogę pobrać Aspose.HTML dla Java?**  
O: Pobierz najnowszą wersję ze [strony wydań](https://releases.aspose.com/html/java/).

**P: Czy konieczne jest zwolnienie obiektów `document` i `configuration`?**  
O: Tak, zwolnienie uwalnia zasoby natywne i zapobiega wyciekom pamięci.

**P: Czy mogę ustawić limit czasu JavaScript na inną wartość niż 5 sekund?**  
O: Oczywiście – zmień argument w `TimeSpan.fromSeconds()` na dowolny limit pasujący do Twojego scenariusza.

**P: Gdzie mogę uzyskać pomoc w razie problemów?**  
O: Odwiedź [forum Aspose.HTML](https://forum.aspose.com/c/html/29), gdzie społeczność i personel udzielają wsparcia.

---

**Ostatnia aktualizacja:** 2026-02-10  
**Testowano z:** Aspose.HTML dla Java 24.11 (najnowsza)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}