# Signal Workshop - program szkolenia dla integratora i prowadzącego

**Program szkolenia dla AV Control 1.6.8 | rewizja 19 października 2026**

Program prowadzi od otwarcia projektu do samodzielnego zaprojektowania sterowania. Obejmuje cztery główne karty, eksplorator Logiki, symbole urządzeń, przewody, debugger, panele z ośmioma motywami, ograniczony Python oraz pełny CPython z bibliotekami i własnymi plikami. Materiał podstawowy to [Podręcznik Signal Workshop](index.html), projekt `Szkolenie-Wirtualna-sala.avctrl` i grafika `Plan-sali.svg`. Konta, klawiatura, dokumentacja instalacji, monitoring i kreator e-mail stanowią część tego samego kursu. Podstawowy harmonogram obejmuje 10 sesji i 22 godziny; opcjonalny odbiór HDMI trwa dodatkowo 60 minut.

Zajęcia 1-6 wykonuje się w lokalnym symulatorze. Sesja 7 zawiera oddzielny, warunkowy odbiór na sprzęcie. Zaliczenie lokalne nie potwierdza działania transportu, GPIO, instalatora Windows, Imagera, rzeczywistego telefonu ani nowego wydania na fizycznym Raspberry Pi. Prowadzący wpisuje zakres i środowisko każdego wyniku.

## 1. Cel, uczestnicy i rezultat

Uczestnik powinien po kursie umieć otworzyć/zapisać projekt, odróżnić edycję od aktywnej rewizji, zbudować panel z poprawnym wiązaniem, przeprowadzić żądanie przez logikę i zezwolenie do komendy, odczytać TX/RX oraz jakość, znaleźć błąd w debuggerze i przygotować własny symbol Python. Nie jest wymagane programowanie na początku; część CPython wymaga pracy z krótkimi funkcjami i słownikami.

Rezultatem jest własny plik `.avctrl`, odrębny od oryginalnej Wirtualnej sali, oraz karta prób. Projekt zawiera minimum dwa urządzenia, trzy strony operatora, panel Telefon, logiczny wybór scen, interlock, timer, własny protokół, sekwencję z timeoutem, symbol urządzenia i sprawdzony symbol Python. Pełny CPython i przygotowanie bibliotek są przedmiotem sesji 6. Nie wpisuje się ich ukończenia po samej lekturze kodu. Jeżeli uczestnik realizuje krótszą ścieżkę bez CPython, karta wyników wskazuje ten pominięty zakres; nie nazywaj jej pełnym 22-godzinnym kursem.

## 2. Przygotowanie stanowiska

Prowadzący przed zajęciami:

1. Sprawdza pakiet Studio z Signal Workshop oraz dostępność symulatora, a w wariancie przeglądarkowym działający lokalny silnik.
2. Otwiera projekt szkoleniowy, potwierdza dziesięć wyłączonych urządzeń i brak komend startowych, uruchamia kopię w symulatorze.
3. Sprawdza cztery karty: Projekt, Urządzenia, Logika, Panele. W Logice otwiera formularz sygnału, debugger i warsztat Python.
4. Przygotowuje katalog prac uczestnika i kopie etapów. Nie używa aktywnej instalacji jako stanowiska przypadkowych prób.
5. Dla CPython odczytuje rzeczywisty interpreter i przygotowuje bibliotekę wymaganą przez bieżący szablon NumPy. W tej edycji wymaganie to `numpy==2.5.3`.
6. Dla wariantu offline dostarcza wheel oraz wszystkie zależności dla właściwego Python/systemu/architektury. Sprawdza nową instalację offline, a nie tylko wcześniej gotowy zestaw online.
7. Przygotowuje własne pliki UTF-8 `helpers.py` oraz celowo konfliktowy plik o tej samej nazwie dla ćwiczenia importu.
8. Ustala oddzielne stanowisko fizyczne, jeśli sesja sprzętowa ma być wykonywana. Potrzebne są dane rzeczywistego sprzętu i jego dokumentacja; profile szkoleniowe nie stanowią komend konkretnego producenta.
9. Otwiera HTML/PDF offline i sprawdza komplet ilustracji z zachowanym pochodzeniem i datą. Zapisuje wersję aplikacji oraz datę kursu. Dane systemowe i sześć obrazów hostingu są kontrolowanymi zestawami testowymi; nie zaliczają sprzętu ani dostawy poczty.
10. Przed sesją 9 przygotowuje neutralne dane metryki, kontroler testowy i raporty diagnostyczne. Przed sesją 10 przygotowuje dwie sesje izolowanego symulatora, osobne stanowisko z jednym administratorem do próby jego ochrony oraz konta TECHNIKAV o różnych zakresach instalacji.
11. Jeżeli uczestnik zamierza wykonać rzeczywisty test e-mail, wcześniej zapewnia własny aktywny adres Proton w płatnym planie z domeną, token SMTP, uprawnioną skrzynkę odbiorczą oraz zgodę na wysłanie jednej wiadomości. Bez tego kreator ćwiczy się bez wysyłki, a dostawę oznacza NIEWERYFIKOWANĄ. Nie wpisuje się hasła do skrzynki jako tokenu.

Materiały dla uczestnika: źródłowy projekt, podręcznik HTML/PDF, instrukcja Python, grafika sali, karta wyników i pusty folder etapów. Materiały sprzętowe: właściwe konwertery/transceivery, przewody, dane pinów oraz parametry urządzeń. Szczegóły napięć i transportów są w rozdziałach 17-18 podręcznika.

## 3. Harmonogram i bramki zaliczenia

| Sesja | Czas | Rozdziały | Bramka zaliczenia |
| --- | --- | --- | --- |
| 1. Organizacja pracy | 90 min | 2-7, 37 | Zapisana kopia, aktywna rewizja i poprawna nawigacja |
| 2. Panele i wygląd | 120 min | 8-10, 20, 22, 36-37 | Działający panel PC/Telefon oraz porównanie motywów |
| 3. Program sterowania | 120 min | 11-15, 33 | Tabela wyników, jeden impuls jednej komendy, czytelne przewody |
| 4. Debugger i diagnoza | 120 min | 19, 34 | Jakość, breakpoint, krok TON, ślad TX/RX i powrót do pracy |
| 5. Protokoły i transporty | 150 min | 16-18, 29-32 | Zgodne ramki, mapowanie odpowiedzi, rozpoznany timeout |
| 6. Python i biblioteki | 180 min | 21, 35 | Rzeczywisty import, pięć wyników, helper, błędy i konflikt |
| 7. Wdrożenie i odbiór | 180 min | 23-27 | Osobne dowody kontrolera, restartu i paneli albo NIEWERYFIKOWANE |
| 8. Projekt końcowy | 180 min | 28, 33-37 | Samodzielny projekt i karta prób z ograniczeniami |
| 9. Metryka i monitoring | 90 min | 38–46 | Metryka po ponownym otwarciu, wyniki i wskazówki serwisowe |
| 10. Sondy, hosting, konta i serwis | 90 min | 47–52 | Sonda, zakresy, kreator poczty, role, hasła, sesje i plan serwisu |

Łącznie: **1320 minut = 22 godziny**, bez przerw i samodzielnej powtórki. Konta i klawiatura mieszczą się w sesji 10; nie są kolejną osobną godziną kursu. Opcjonalny fizyczny moduł HDMI poniżej dodaje 60 minut, czyli cały wariant z tym modułem ma 23 godziny. Część sprzętową można odłożyć do osobnego terminu. Sesję CPython można rozdzielić na dwa spotkania po 90 minut. Jeżeli uczestnik nie zna podstaw funkcji i słowników, dodaj 60 minut wprowadzenia przed sesją 6.

## 4. Sesja 1 - od otwarcia do aktywnego projektu

**0-15 min:** prowadzący demonstruje Studio, silnik, Player i Imager. Uczestnik zapisuje własnymi słowami, która część działa po zamknięciu komputera projektanta. Następnie otwiera projekt szkoleniowy i zapisuje `Sala-01.avctrl`. Porównuje ekran powitalny z metryką w Projekcie: otwarcie karty nie aktywuje instalacji, a wpis dokumentacji nie steruje urządzeniem.

**15-35 min:** przejście przez cztery karty. W Logice uczestnik znajduje sygnał w drzewie, otwiera formularz i zamyka go. Znajduje protokół w Komendach oraz Zezwolenia w Modułach i schematach. Otwiera Kontroler i narzędzia, przechodzi do Panelu operatora i wraca. Prowadzący pyta, czym różni się strona Sala od karty Panele.

**35-55 min:** zmiana nazwy instalacji, zapis i obserwacja starego aktywnego panelu. Uruchomienie nowej rewizji i odczyt `vN`. Każdy uczestnik zapisuje numer dokumentu i aktywnej rewizji w karcie próby.

**55-75 min:** nowy sygnał bool oraz number. Poprawny typ, wartość początkowa, trwałość i jakość. Kopiowanie/duplikowanie kolekcji, zmiana nazwy kopii, próba wklejenia do niewłaściwej kolekcji i odczyt odmowy. Przy urządzeniu prowadzący pokazuje wyłączoną kopię.

**75-90 min:** globalny Ciemny/Jasny/Jak w systemie, przewijanie listy i formularza. Odświeżenie i sprawdzenie preferencji. Zapis etapu.

**Dowód:** plik etapu, nazwa i aktywna rewizja, notatka „zapis nie uruchamia projektu”, poprawnie odrzucona obca kategoria schowka. **Typowe problemy:** panel bez aktywnego projektu, próba szukania dawnych osobnych kart Sygnały/Protokoły, nowa nazwa przy starej aktywnej wersji.

## 5. Sesja 2 - panel, materiały i obsługa operatora

**0-25 min:** uczestnik tworzy własną stronę z przyciskiem chwilowym, przełącznikiem, suwakiem i odczytem. Definiuje wiązania i sprawdza zwolnienie impulsu. Importuje grafikę, wybiera dopasowanie i ukrywa etykietę obrazu.

**25-50 min:** duplikuje element i odczytuje nadal to samo wiązanie. Następnie zmienia wiązanie kopii na inne. Kopiuje wygląd z jednego źródła na dwa elementy i potwierdza zachowanie ich nazw, pozycji oraz funkcji.

**50-70 min:** grupowanie, rozgrupowanie, blokada położenia, dokładne pola pozycji, warstwy, wyrównanie dwóch oraz rozłożenie trzech niezablokowanych elementów. Prowadzący nie pozwala zaliczyć pozycji na podstawie samego otwarcia menu.

**70-100 min:** porównanie ośmiu gotowych motywów na tej samej stronie. Osobno Własny i indywidualne nadpisania. Zmiana motywu ustawia bazowy kolor, lecz zachowuje własny obraz/gradient; przed porównaniem domyślnych teł uczestnik wybiera Rodzaj tła: Jednolity kolor na kopii strony. Gradient z trzema kolorami, upload tła z listy, Wypełnij/Dopasuj oraz powielanie i kadrowanie. Wypukłość 0/0.5/1 oraz Glass/Liquid/Frost/Szron nad rzeczywistym tłem. Pełny i oszczędny wariant efektów.

**100-120 min:** Telefon, ramka 9-slice i zachowany rozmiar narożników, fokus klawiatury, poprawny i niedostępny przycisk oraz zła jakość odczytu. Uczestnik zapisuje `Sala-02.avctrl`, otwiera ponownie i sprawdza tło w panelu operatora; dołącza tabelę motywów.

**Dowód:** działanie trzech różnych wiązań, screenshot PC/Telefon, osiem wierszy porównania i wynik zezwolenia przy dwóch motywach. **Typowe problemy:** własny CSS ukrywający motyw, pomylenie globalnego wyglądu z motywem strony, nieczytelny tekst nad szkłem, etykieta ukryta wraz z oczekiwanym odczytem. Próba w emulacji telefonu pozostaje próbą emulowaną.

## 6. Sesja 3 - logika, pamięć, symbole urządzeń

**0-25 min:** AND4, pełna tabela 16 kombinacji. Uczestnik sprawdza poprawną jedynkę, poprawne zero oraz jedynkę o złej jakości. Prowadzący odróżnia wartość od jakości.

W trybie „Projekt roboczy · bez poleceń” uczestnik podłącza i usuwa przewód, zmienia stałą oraz wartość niepodłączonego wejścia. Sprawdza wynik bez publikowania, wykonuje Cofnij/Ponów i obserwuje timer odświeżany co około 200 ms. Porównuje podgląd z „Stanem opublikowanego programu” i potwierdza, że aktywna rewizja się nie zmieniła. Resetuje pamięci tylko podglądu. Pełny CPython sprawdza osobno zatwierdzonym testem w edytorze Python.

**25-50 min:** Interlock dla trzech scen i Truth table. Oczekiwane wyjścia: Prezentacja 100/101, Spotkanie 010/110, Przerwa 001/000. CLEAR zeruje, SET ALL daje 111 Interlocku. Naciśnięcie jest zwalniane między próbami.

**50-70 min:** pamięć T oraz TON. Uczestnik wskazuje stan chwilowy, trwały i retencję instancji. Prowadzący demonstruje, że zachowany wysoki stan nie jest nowym naciśnięciem.

**70-95 min:** TCP jako symbol urządzenia z ikoną, komendą i argumentem LEVEL. Uczestnik odróżnia „Połączenie TCP”, „Zajęty”, „Błąd” i „Odpowiedź aktualna” od zmapowanego odczytu. Dla UDP wskazuje gotowość lokalnego gniazda, dla RS-232 — otwarty port; żaden z tych dwóch stanów nie potwierdza obecności urządzenia. Podłącza jeden impuls i liczbowy argument **value**. Pole odpowiedzi **level** mapuje osobno na tcpFeedback; nie traktuje go jako nazwy parametru żądania. Usuwa podwójną drogę przez stary blok akcji, jeśli ją utworzył.

**95-120 min:** prowadzenie przewodów, odgałęzienie jednego źródła, mostek skrzyżowania różnych sygnałów, porządkowanie symboli. Wyniki AND przed/po rozmieszczeniu muszą być identyczne. Menu przewodu prowadzi do źródła i odbiorcy.

**Dowód:** tabela AND4, trzy sceny, symbol urządzenia, liczba żądań na impuls i schemat bez ostrzeżenia braku trasy. **Typowe problemy:** trzymana jedynka bez nowego zbocza, dwie akcje jednej komendy, niezgodne typy portów, brak miejsca na przewody, błędne uznanie skrzyżowania za połączenie.

## 7. Sesja 4 - debugger i celowo wywołane błędy

**0-20 min:** otwarcie debuggera, cztery położenia względem schematu, przeciąganie separatora i regulacja klawiaturą, pełne okno oraz niezależne okno na drugim monitorze. Zapisanie osobnych proporcji wysokości i szerokości. Odczyt aktywnej rewizji, wyszukiwanie i pinezki. Przejście do Urządzeń przy działającym osobnym oknie, powrót i dołączenie bez utraty obserwacji/filtra. Źródła i odbiorcy prowadzą do bezpośrednio powiązanych bloków.

**20-45 min:** Warunek 4: 1/good, 1/stale, 0/good, 1/good. Uczestnik wysyła bodźce i zapisuje wynik AND oraz zezwolenie. Dla bool przyciski 0/1 są operacją podania wartości, a Impuls jest osobną operacją.

**45-65 min:** breakpoint narastającego zbocza Prezentacji, odczyt przyczyny pauzy, usunięcie punktu i wznowienie. Prowadzący sprawdza, że żaden punkt nie pozostał aktywny po ćwiczeniu.

**65-90 min:** zatrzymanie programu, wejście TON, pięć kroków z odczytem czasu i dłuższe czekanie bez przyrostu zegara. Następnie kroki do progu, reset i wznowienie. Sekwencje/komunikacja/CPython używające czasu systemowego nie są ogólnie zamrażane.

**90-120 min:** jedna komenda LEVEL, filtr TX/RX, wynik akcji, zatrzymanie przewijania śladu i eksport JSON. Próba timeoutu oraz przywrócenie normalnej odpowiedzi. Sprawdzenie pamięci i anulowanie sekwencji.

**Dowód:** układ boczny i pionowy, samodzielne okno z tym samym odczytem, zachowane pinezki/filtr, wartości/jakości, przyczyna breakpointu, pięć czasów TON, stan po wznowieniu, ślad i informacja o ewentualnej utracie starszych zdarzeń. **Typowe problemy:** blokada okien przez przeglądarkę, symbole poza widokiem po zwężeniu (Zmieść schemat), mylenie przycisków Ślad/Program, impuls przy pauzie, nieaktualna rewizja, eksport uznany za nieograniczoną historię. Na RPi nie wykonuje się pauzy/kroku programu ani breakpointów.

## 8. Sesja 5 - protokół, transport i odpowiedź

**0-30 min:** profil LEVEL ASCII, parametr i CRLF. `LEVEL 40` ma 8 bajtów tekstu; CRLF dodaje 2, razem **10 bajtów**. Parametr komendy to `value`, a odebrane pole to `level`. Odpowiedź ma zmieniać odczyt, a nie wyłącznie żądaną wartość.

**30-60 min:** ramka binarna z CRC oraz mapowanie pola odpowiedzi. Celowy błąd separatora, offsetu albo typu pola; uczestnik diagnozuje go na TX/RX, potem poprawia.

**60-90 min:** USB-RS232, RS-485, UART, TCP, UDP i GPIO w symulatorze. Właściwy port/IP, kolejka magistrali, adres odbiorcy i rodzaj transportu. Parametry fizyczne pozostają zadaniem urządzenia docelowego.

**90-120 min:** trzy bramki i cztery kanały ekspanderów, oddzielny port kanału, mapowanie odczytu, adresowana RS-485, RFC2217. USR-W610 ma jeden kanał RS-232 albo RS-485 i przezroczysty TCP/UDP; standardowy RFC2217 wymaga innego zgodnego konwertera. Prowadzący wyjaśnia różnicę między siecią administracyjną a dodatkową siecią AV.

**120-150 min:** niezależne odpowiedzi dwóch kanałów, timeout i odmowa zezwolenia. Uczestnik sporządza plan rzeczywistego urządzenia z dokumentacją producenta i zakresem brakujących danych.

**Dowód:** dokładne bajty, RX i good odczytu, niezależne kanały, odczytany błąd, przywrócony stan. **Typowe problemy:** odpowiedź w niewłaściwym sygnale, wspólne mapowanie kopii urządzenia, niewłaściwy kanał konwertera, komenda szkoleniowa traktowana jako komenda producenta. Fizyczny transport pozostaje NIEWERYFIKOWANY do próby na sprzęcie.

## 9. Sesja 6 - ograniczony Python i pełny CPython

**0-30 min:** licznik impulsów i histereza z rozdziału 21. Test licznika 0/1/1/0/1 daje 0/1/1/1/2. Uczestnik rozróżnia JSON false i Python False, number/bool oraz parametry instancji.

**30-55 min:** nowy symbol NumPy, pełne środowisko, stanowość, interval i timeout. Sprawdzenie rzeczywistego interpretera. Prowadzący wyjaśnia prawa konta silnika oraz wymagane zatwierdzenie kodu. Tester nie uruchamia zadeklarowanych akcji, ale kod CPython może mieć skutki systemowe; kurs używa wyłącznie obliczeń.

**55-80 min:** instalacja online z dokładnym wymaganiem i logiem, zatwierdzenie oraz import w kroku testu. Wartości 10/20/30/40/50 przy window=4 dają 10/15/20/25/35. Reset testu przywraca pamięć początkową.

**80-105 min:** helper w pliku UTF-8. Import z dysku albo Dodaj plik, `from helpers import average`, log `print`. Zmiana helpera, ponowne zatwierdzenie, sprawdzenie nowego wyniku i powrót do właściwego kodu.

**105-135 min:** świeże przygotowanie offline ze zgodnego wheel i pełnych zależności przy wyłączonym PyPI. Uczestnik zapisuje platformę, interpreter, nazwy plików oraz log. Jeżeli środowisko było już gotowe po online, prowadzący nie zalicza tego jako odrębnego dowodu offline.

**135-155 min:** ModuleNotFoundError, bool zwrócony do number, ValueError i kontrolowany timeout. Odczyt wyjątku oraz wskazanej linii. Przywrócenie prawidłowego kodu i zatwierdzenia.

**155-180 min:** zapis symbolu z wymaganiami/helperem w bibliotece, dodanie do kopii projektu, celowy konflikt pliku/wersji, odmowa bez nadpisania i uzgodnienie. Dwie instancje z innymi parametrami i niezależną pamięcią. Włączenie wyniku do grafu oraz panelu.

**Dowód:** pięć wyników, rzeczywisty import, helper i log, osobne online/offline, odrzucony konflikt, cztery komunikaty błędów i przywrócony kod. **Typowe problemy:** pakiet zainstalowany na PC zamiast kontrolerze, wheel Windows na ARM64, brak dependency, niezatwierdzona zmiana, ndarray w JSON, próbkowanie okresowe pomylone z próbkowaniem po zmianie. Serializowana pamięć podlega jednocześnie limitowi 64 KiB i limitom struktury; pojedyncza lista ma do 1024 elementów. Instancje mają odrębne state, lecz procesy pochodzą ze współdzielonej ograniczonej puli; globalna zmienna helpera nie jest pamięcią instancji.

## 10. Sesja 7 - plan wdrożenia i odbiór na sprzęcie

Ten moduł wymaga osobnego stanowiska i świadomego wskazania kontrolera. Jeżeli sprzętu brak, uczestnik sporządza plan; wyniki sprzętowe pozostają NIEWERYFIKOWANE.

**0-30 min:** wersja pakietu, model RPi, obraz, dane startowe, dwa konta i karta SD. Zapis nośnika jest wykonywany tylko na wskazanej karcie przeznaczonej do stanowiska. Bieżąca ilustracja natywnego Imagera pokazuje UI 1.6.3; nie jest dowodem zapisu i uruchomienia karty. Uczestnik zapisuje wynik weryfikacji nośnika oraz osobny wynik pierwszego startu.

**30-60 min:** pierwszy start, WWW, czas, certyfikat, sieć i punkt przywracania. Odczyt wersji usług oraz właściwego interpretera. Sprawdzenie zachowania konfiguracji po restarcie.

**60-90 min:** środowisko CPython kontrolera, wheel dla jego architektury, zatwierdzenie kodu i pięć wyników lokalnego testera na kontrolerze. Przygotowanie symulatora nie przygotowało automatycznie RPi.

**90-120 min:** publikowanie projektu, aktywna rewizja, Player/przeglądarka, dwie niezależne sesje i rzeczywiste TX/RX urządzenia. Prowadzący odczytuje potwierdzony stan, a nie efekt naciśnięcia.

**120-150 min:** restart silnika i kontrolera, zachowanie wybranych sygnałów/pamięci, brak niezamierzonej komendy startowej, odłączenie panelu. Fizyczny telefon/tablet wymaga własnej próby dotykowej oraz oceny materiałów.

**150-180 min:** historia wersji i przywracanie projektu, plan aktualizacji, odrębne dowody instalacji, usług i urządzenia. Wyniki rozdziela się w karcie odbioru.

**Dowód:** model, wersja aplikacji/silnika/interpretera, rewizja, rzeczywisty transport i odpowiedź, osobne session IDs albo inne identyfikatory próby, zachowanie danych oraz pliki dowodowe. Nie zapisuj haseł i kluczy prywatnych. Przerwa w dostępności albo brak wymaganego środowiska pozostaje blokadą odbioru, a nie sukcesem.

## 11. Sesja 8 - samodzielny projekt końcowy

**0-30 min:** uczestnik otrzymuje wymaganie neutralnej sali: trzy sceny, poziom, dwa urządzenia, jedna sekwencja z gotowością i timeoutem, panel PC/Telefon. Sam tworzy sygnały i diagram drogi żądania/odpowiedzi.

**30-75 min:** buduje urządzenia, protokół, akcje, zezwolenia i logikę. Co najmniej jedno urządzenie występuje jako symbol; układ nie ma przewodów przez obiekty ani ostrzeżenia braku trasy.

**75-115 min:** tworzy panel, wybiera motyw, kopiuje wygląd i sprawdza trzy wiązania. Dodaje własny symbol obliczeniowy i helper. Dobiera retencję wprost do wymagania.

**115-150 min:** wykonuje próby poprawne oraz błędne w debuggerze. Eksportuje ślad i zapisuje rewizję. Udowadnia odmowę akcji przy złej jakości i poprawne przywrócenie działania.

**150-180 min:** prezentuje rezultat prowadzącemu. Prowadzący zmienia jeden parametr wejściowy i jedno wymaganie jakościowe, żeby sprawdzić zrozumienie, nie odtworzenie kolejności kliknięć. Uczestnik przekazuje projekt, karty wyników oraz listę brakujących prób sprzętowych.

**Zaliczenie:** każdy wymagany przypadek ma spodziewany i faktyczny wynik; niespełnione lub niepróbowane wymagania pozostają jawne. Sam screenshot formularza nie zalicza wykonania komendy, instalacji biblioteki ani odbioru urządzenia.

## 12. Sesja 9 - metryka instalacji i monitoring lokalny

Rozdziały 38–46 tworzą regularną sesję podstawowego kursu. Pracuj w kopii neutralnego projektu i lokalnym symulatorze. Źródło testowych danych systemowych pozwala rozpoznać pola Raspberry Pi; nie zalicza zmiany konfiguracji fizycznego kontrolera.

**0-15 min — ekran powitalny i instalacja:** uczestnik tworzy nowy projekt z ekranu powitalnego i porównuje go z kartą Projekt. Uzupełnia nazwę instalacji, kod, własną wersję programu, etap, klienta, integratora, obiekt, adres, pomieszczenia, zakres i tagi. Dodaje Numer umowy jako własne pole. Wskazuje różnicę między wersją programu autora, wersją aplikacji 1.6.8 i rewizją vN.

**15-30 min — odpowiedzialność, dokumenty i terminy:** przypisuje projektanta, programistę, weryfikującego i uruchamiającego. Dodaje dwa kontakty, jeden odnośnik dokumentu i pięć startowych czynności odbioru. Wpisuje termin przeglądu, ale nie nazywa go skonfigurowanym powiadomieniem. Wyjaśnia, dlaczego kontakt metryki nie jest kontem i odbiorcą poczty. Oznacza Wykonano tylko czynność z własnym dowodem.

**30-45 min — historia i przenoszenie:** dodaje wpis historii, sprawdza autora i datę. Cofnięcie i ponowienie wykonuje przyciskami. Eksportuje metrykę Markdown i pełny .avctrl, ponownie otwiera projekt i porównuje dane. Potwierdza, że plik Markdown nie odtwarza grafów ani zasobów. W Pracy silnika pozostawia jawne akcje startowe puste.

**45-60 min — zakres monitorowania:** w kopii symulatora włącza jedno ćwiczeniowe urządzenie i uruchamia tę rewizję. Konfiguruje Monitoruj urządzenie, stabilizację, lokalizację, wskazówki, części i narzędzia. Porównuje **Połączenie TCP**, **Gniazdo UDP gotowe**, **Port otwarty** i **Odpowiedź aktualna**. Gotowe UDP bez odbiornika nie potwierdza urządzenia; otwarty port nie wykrywa wyjęcia DB9. TCP obserwuje rzeczywisty socket i systemowy keepalive bez komend producenta.

**60-75 min — wiek i jakość odpowiedzi:** ustawia właściwą dodatnią ważność odpowiedzi, wymusza dopasowaną odpowiedź i sprawdza good. Potem wstrzymuje odpowiedź, obserwuje przekroczenie czasu oraz odczytuje przyczynę w Pomiary serwisowe. Dla urządzenia zgodnie z protokołem milczącego wybiera 0 i wyjaśnia, że Odpowiedź aktualna pozostaje nieznana. Sprawdza wyszukiwanie, filtr Błąd i szczegóły pomiaru.

**75-90 min — awaria, przywrócenie i karta serwisu:** porównuje stan błędny, nieznany i wstrzymanie alarmu. Odczytuje trzy błędne pomiary wymagane do otwarcia incydentu oraz dwa poprawne do zamknięcia. Przywraca prawidłową odpowiedź i monitoring. Sporządza kartę serwisu z ostatnim poprawnym pomiarem, hipotezą przyczyny, lokalizacją, częściami i testem na miejscu. Wyłączenie monitoringu nie zalicza naprawy.

**Dowód:** zgodna metryka po ponownym otwarciu, .avctrl i Markdown, karta odpowiedzialności, trzy stany pomiaru, dopasowana odpowiedź oraz jej przeterminowanie i przywrócenie. **Typowe problemy:** pozostawione wyłączone urządzenie, limit wieku 0 traktowany jak wieczna ważność, gotowość UDP traktowana jak połączenie z odbiornikiem, data przeglądu traktowana jak alarm. Wyjęcie USB, zamknięcie socketu i fizyczny brak odpowiedzi na stanowisku rzeczywistym mają osobne wyniki; ekran symulatora ich nie zastępuje.

## 13. Sesja 10 - sondy, hosting, poczta, konta i serwis

Rozdziały 47–52 tworzą drugą 90-minutową sesję podstawowego kursu. Prowadzący wcześniej przygotowuje projekt, uprawnienia TECHNIKAV, dwie sesje kont i ewentualne dane SMTP. Próba wysyłki jest osobną świadomą operacją uczestnika; bez przygotowanych warunków kończy się planem i statusem NIEWERYFIKOWANE.

**0-15 min — sonda i zezwolenie:** uczestnik wybiera rzeczywisty odczyt udokumentowany dla urządzenia albo neutralny profil w symulatorze. Wskazuje oczekiwaną odpowiedź, Bezpieczna do powtórzenia, akcję urządzenia oraz Potwierdzam, że zapytanie tylko odczytuje stan. Ustawia odstęp minimum 5 s. Sprawdza poprawny wynik, następnie odmowę zezwolenia i wynik odłożony. W Planowanym serwisie sonda jest wstrzymana; żaden z tych przypadków nie zamyka błędnego incydentu jako naprawionego. Nie używa POWER jako testu obecności.

**15-30 min — wspólny hosting i zakres kont:** otwiera [AV Control w TECHNIKAV](https://technikav.pl/?app=av-control), wybiera instalację, kontroler i Diagnostyka. Porównuje dwa konta o różnych zakresach. Odczytuje czas pomiaru i odbioru oraz Nieaktualny po braku kontaktu lub ponad 30 s od odbioru listy. Otwiera popup i oznacza zdarzenie przeczytane; drugie konto zachowuje własny stan. Eksportuje widoczną stronę pomiarów, nie nazywając jej całą historią. Utratę i powrót raportowania przygotowuje na kontrolowanym stanowisku.

**30-50 min — cztery kroki kreatora Proton:** właściciel otwiera Powiadomienia e-mail · konfiguracja właściciela. Wskazuje adres własnej domeny i odpowiadający mu token SMTP, nie hasło do Proton. Sprawdza `smtp.protonmail.ch:587`, STARTTLS i certyfikat. Używa **Sprawdź połączenie bez wysyłki**, wybiera uprawnionego odbiorcę i progi, a następnie zapisuje przy wyłączonych alarmach. Sprawdza warunki harmonogramu: istniejące `--update` albo pełna komenda Cron wyświetlona przez kreator. Omawia wymianę tokenu, Odłącz pocztę i jawne ponawianie niepewnych wyników. Jeżeli przygotowano własny token i zgodę, uczestnik używa **Wyślij jedną wiadomość testową** i sprawdza skrzynkę, Spam oraz Proton Wysłane. Sam sukces transportu nie dowodzi otrzymania. Bez rzeczywistego testu wpisuje NIEWERYFIKOWANE; testowe obrazy hostingu i transport zastępczy nie dowodzą dostawy.

**50-60 min — kolejka i przygotowanie wyjazdu:** porównuje ostatni dobry pomiar z hipotezą przyczyny. Uzupełnia kartę części, dokumentacji i testów na miejscu. Wyjaśnia lokalny monitoring bez internetu, trwałą kolejkę, ponowne raportowanie bez duplikatów oraz Historia ma przerwy po utracie starszych stron. Odróżnia oznaczenie alertu jako przeczytanego od zamknięcia incydentu. Przywraca projekt, sondy i ustawienia poczty do uzgodnionego stanu testowego.

**60-65 min — role i kontroler:** w izolowanym symulatorze tworzy operatora oraz drugiego administratora. Potwierdza brak edycji w panelu nawet po podaniu konta administratora. Wybiera login bez spacji na początku/końcu; aplikacja odrzuca takie spacje, a nie przycina nazwy.

**65-70 min — klawiatura:** potwierdza domyślny brak klawiatury i uchwytu w WWW na PC. Świadomie włącza ją w Ustawienia wprowadzania, wykonuje `ąĄ!`, sprawdza Alt, Shift, kursor, kasowanie i uchwyt. Pola pozostają nad wysuniętą klawiaturą; Enter w polu wielowierszowym wstawia nową linię. Zmiana preferencji PC nie zmienia domyślnej klawiatury natywnego HDMI.

**70-75 min — sesje:** sprawdza logowanie bez pamiętania, wylogowanie i odświeżenie. Następnie loguje z pamiętaniem 30 dni, sprawdza powrót ważnej sesji i jej usunięcie przez Wyloguj z panelu. Zapamiętywana jest sesja, nie hasło. Zwykły dostęp wygasa po 12 godzinach.

**75-80 min — własne hasło:** w Moje konto podaje obecne hasło, nowe oraz powtórzenie. Sprawdza komunikat niezgodności, udaną zmianę i odwołanie drugiej sesji. Stare hasło ma być odrzucone, nowe przyjęte. Zamknięcie dialogu × lub Escape bez zapisu nie zmienia hasła.

**80-85 min — administracja:** administrator resetuje hasło operatora bez znajomości starego, zmienia login i sprawdza ponowne logowanie. Puste pola nowego hasła zachowują poprzednie. Usunięcie testowego konta odwołuje jego sesje. Na przygotowanym osobnym symulatorze aplikacja ma odmówić usunięcia lub degradacji ostatniego administratora.

**85-90 min — wygląd i zamknięcie kursu:** porównuje Moje konto i logowanie w jasnym/ciemnym interfejsie oraz materiale panelu. Przy szerokości 390 px jawnie włącza klawiaturę i sprawdza czytelne trzy pola, przewijanie i zamknięcie. Przywraca opcję PC do wyłączonej, usuwa próby i zapisuje kartę wyników. Fizyczne HDMI, USB i dotyk pozostają osobnym odbiorem.

**Dowód:** sonda z potwierdzeniem oraz wynik odłożony, zakresy dwóch kont TECHNIKAV, własny stan odczytu popupu, cztery kroki kreatora i harmonogram albo plan testu, karta serwisu, role, sesje, odwołanie starego hasła i ochrona ostatniego administratora. **Typowe problemy:** kontakt w metryce pomylony z uprawnionym odbiorcą, hasło skrzynki zamiast tokenu, port 587 zablokowany na hostingu, stary raport uznany za naprawę, ukryta klawiatura PC uznana za błąd, konto SSH używane do logowania panelu. Moduły C/D/E rozdziału 51 i ćwiczenia kont rozdziału 52 są szczegółami tych samych 90 minut.

## 14. Karta próby do skopiowania

| Pole | Wpis uczestnika |
| --- | --- |
| Identyfikator ćwiczenia | Sesja / punkt / własny numer |
| Data i środowisko | Symulator Windows / lokalna przeglądarka / fizyczny RPi / telefon |
| Wersja aplikacji i silnika | Rzeczywisty odczyt |
| Projekt i aktywna rewizja | Nazwa, ID, vN |
| Dane wejściowe | Wartość, jakość, czas, parametry |
| Oczekiwany wynik | Konkretna liczba/stan/ramka/komunikat |
| Faktyczny wynik | Odczyt z panelu, debuggera lub RX |
| Dowód | Plik, zrzut, log instalacji, ślad JSON |
| Status | ZALICZONE / NIEZALICZONE / NIEWERYFIKOWANE / ZABLOKOWANE |
| Przyczyna lub ograniczenie | Bez pomijania brakujących testów |
| Stan po próbie | Wznowiono program, usunięto breakpoint, przywrócono jakość/kod |

Za ZALICZONE uznaj tylko wykonany przypadek z odpowiednim dowodem. NIEWERYFIKOWANE oznacza brak próby; ZABLOKOWANE oznacza znaną przeszkodę, np. brak zgodnego pakietu lub niedostępny kontroler. Sukces lokalny może współistnieć z niewykonanym odbiorem sprzętowym.

## 15. Ocena końcowa i dalsze utrwalanie

Ocena składa się z sześciu obszarów: model projektu, działanie panelu, logika/zezwolenia, komunikacja/potwierdzenie, diagnoza oraz Python. Każdy obszar oceniaj jako samodzielnie wykonany, wykonany z pomocą lub wymagający powtórzenia. Nie zastępuj brakującej próby średnią z pozostałych punktów.

Po kursie uczestnik powtarza projekt od pustego pliku, dodaje nową scenę, przenosi symbol z biblioteką do innego projektu oraz diagnozuje nieznaną jakość. Próby fizycznych transportów, RPi i telefonu wykonuje na osobnym stanowisku. Zmiana wydania wymaga sprawdzenia zgodności pakietu, dokumentacji i ponownego wykonania istotnych prób.

## 16. Opcjonalny moduł sprzętowy - lokalny panel HDMI (60 minut)

Ten moduł rozszerza kurs podstawowy do **23 godzin**. Potrzebne są fizyczne Raspberry Pi 3B, 4B albo 5, monitor, właściwy kabel HDMI/micro HDMI, rozpoznawana mysz/touchpad lub dotyk USB i klawiatura. Sam HDMI przesyła obraz; dotyk wymaga osobnego połączenia USB. Prowadzący używa wyłączonych lub wirtualnych urządzeń i zapewnia własne systemowe konto serwisowe. Test Cage/GTK/WebKit z wirtualnym ekranem nie zalicza sprzętu.

**0-10 min — projekt:** otwórz neutralny projekt, przygotuj dwie strony, nawigację, chwilowy przycisk i suwak. Potwierdź brak niezamierzonych akcji startowych. Sprawdź funkcje najpierw w symulatorze.

**10-20 min — aktywna rewizja:** wybierz właściwy kontroler, opublikuj po walidacji i porównaj vN. Lokalny panel pokazuje aktywny projekt, nie roboczą edycję Studio. Przygotuj login operatora AV Control na tym kontrolerze.

**20-35 min — monitor i USB:** podłącz monitor i obserwuj automatyczne wykrywanie. Sprawdź monit logowania oraz domyślnie włączoną klawiaturę HDMI. Zaloguj bez pamiętania, porównaj mysz, touchpad i dotyk, sprawdź dwie strony oraz końcową wartość suwaka. Wybór PC wyłączający klawiaturę nie może wyłączyć jej tu. Spróbuj prawego kliknięcia, gestu historii i przeciągnięcia pliku: panel nie ma otwierać innej aplikacji, przeglądarki plików ani pulpitu.

**35-45 min — ustawienia i dostęp:** jako administrator zdalnie otwórz konfigurację Raspberry Pi, sekcję Panel lokalny HDMI. Ustaw Strona początkowa, zapisz, wyłącz i włącz Automatycznie wyświetlaj panel po podłączeniu monitora. Silnik i sieciowe panele pozostają działające. Sprawdź Moje konto, wylogowanie i ponowne logowanie operatora; wylogowanie nie otwiera pulpitu.

**45-55 min — odłączenie i restart:** odłącz monitor, podłącz ponownie i potwierdź aktualny panel bez powtórzenia wcześniejszego żądania. Podczas neutralnej próby przytrzymaj chwilowy przycisk i odłącz wejście: w debuggerze potwierdź wygaśnięcie dzierżawy. Sprawdź zachowanie preferencji po restarcie oraz brak niezamierzonego odtworzenia komend.

**55-60 min — tty2 i powrót:** fizyczną klawiaturą użyj Ctrl+Alt+F2, zaloguj własnym kontem systemowym i odczytaj stan usługi. Konto AV Control nie jest loginem Linux. Zakończ sesję przez `exit` i wróć Ctrl+Alt+F1; na niektórych klawiaturach potrzebny jest Fn. Zapisz wyniki i przywróć ustawienia stanowiska.

**Odbiór:** wykrycie HDMI, poprawny obraz, logowanie i klawiatura, urządzenia USB, rzeczywisty dotyk, brak wyjścia poza panel gestami/myszą, tty2, powrót i brak powtórzenia komend. Każdy niewykonany przypadek oznacz NIEWERYFIKOWANYM. To opis zajęć w tym programie, a nie odrębny suplement szkoleniowy; techniczne szczegóły są w instrukcji PANEL-HDMI-PL.md.

## 17. Opcjonalny moduł sprzętowy - TAB5 ST7123 (90 minut)

Materiał: rozdziały 53-55 podręcznika i instrukcja TAB5. Ten moduł dodaje 90 minut do podstawowych 22 godzin; z modułem HDMI cały plan obejmuje 24,5 godziny. Prowadzący przygotowuje TAB5 ST7123 z firmware 0.3.0, kartę FAT/exFAT, sieć 2,4 GHz oraz kontroler z sygnałami wirtualnymi.

- **0-15 min:** Wi-Fi, sieć ukryta, hasło konfiguracji i blokada wejścia.
- **15-30 min:** jednorazowy kod parowania i porównanie pełnego odcisku certyfikatu.
- **30-50 min:** wysłanie dwóch różnych zestawów stron ze Studio i porównanie wyglądu.
- **50-65 min:** cztery przełączenia z SD, jasność, dźwięk i blokada sterowania offline.
- **65-80 min:** aktualizacja aplikacji przez Wi-Fi i potwierdzenie po restarcie.
- **80-90 min:** wpisanie wersji, rewizji i rzeczywistego zakresu wyników do karty odbioru.

Brak sprzętu oznacza ćwiczenie w symulatorze bez zaliczenia dotyku, SD ani OTA na TAB5. Odcinanie zasilania i wymuszenie rollbacku wymagają oddzielnie przygotowanej próby; nie są domyślnymi krokami kursu.

## 18. Przejścia między stronami (20 minut)

Ćwiczenie dodaje 20 minut do wybranego wariantu harmonogramu. Wariant podstawowy trwa wtedy
22 godziny 20 minut, a wariant z HDMI i TAB5 — 24 godziny 50 minut.

W aktualnym projekcie szkoleniowym każda z pięciu stron demonstruje inny efekt przez 520 ms:
Sala — fade, Sceny i logika — wipe w lewo, Laboratorium — wash przez kolor, Łączność — slide w górę,
Ekspandery — zoom. Nazwa i czas są widoczne na stronie. Pierwszy ekran pojawia się bez animacji;
fade sprawdza się przy powrocie do Sali.

Przejdź przez strony zakładkami i przyciskami u dołu panelu. Otwórz **Animacje stron — ćwiczenie**,
porównaj cztery kierunki wipe/slide oraz kolor wash. W **Wygląd strony / CSS** zmień czas na 0 ms
i przywróć 520 ms. Po publikacji powtórz próbę w panelu WWW, Windows Playerze, HDMI i TAB5
z aktualnym firmware oraz ponownie wysłanym panelem. Sprawdź brak powielonych komend.
W WWW włącz ograniczenie ruchu w systemie i potwierdź pominięcie animacji. Pełny opis:
[Przejścia stron panelu](../PRZEJSCIA-STRON-PL.md).
