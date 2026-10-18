# Panel M5Stack TAB5 ST7123

TAB5 działa jako samodzielny, dotykowy panel AV Control Player. Raspberry Pi wykonuje logikę i polecenia instalacji; Studio służy do projektowania i wysyłania stron. Po wgraniu panelu Studio może być zamknięte.

## Pierwsze uruchomienie

1. Ustaw na TAB5 własne hasło konfiguracji i wpisz je ponownie. Hasło musi mieć przynajmniej 4 znaki i nie przekraczać 63 bajtów UTF-8.
2. Otwórz **Wi-Fi**. Wybierz sieć z listy i wpisz hasło albo użyj **Wpisz sieć ukrytą**. Urządzenie obsługuje sieci 2,4 GHz. Dane zostaną zapisane po udanym połączeniu.
3. W Studio połącz się z właściwym kontrolerem. W **Ustawienia → Panele M5Stack TAB5** nadaj urządzeniu nazwę i wygeneruj kod parowania.
4. Na TAB5 otwórz **Malina**, wpisz adres HTTPS kontrolera i kod. Porównaj cały odcisk certyfikatu z odciskiem wyświetlonym w Studio, a następnie zatwierdź parowanie. Kod wygasa po pięciu minutach i działa tylko raz.
5. Opublikuj projekt na kontrolerze. W **Edytorze paneli → Wgraj na TAB5** albo w ustawieniach Studio wybierz urządzenie i strony, sprawdź przygotowany panel i wyślij go. Komunikat o odebraniu oznacza, że TAB5 potwierdził także zapis panelu w swojej pamięci.

## Pełny ekran i belka

Wysłany panel zajmuje ekran **1280 × 720**. Przesuń palec od górnej krawędzi w dół, aby otworzyć belkę. Możesz w niej:

- przeciągać jasność w zakresie **20–100%**;
- regulować **Głośność sygnału** w zakresie **0–100%** lub wyłączyć dźwięki;
- wyłączyć ekran; pierwsze dotknięcie włącza go przy **20%** jasności i nie uruchamia kontrolki pod palcem;
- wejść do **Konfiguracji**, po podaniu hasła;
- otworzyć **Panele**, aby wybrać układ zapisany na karcie SD;
- przejść do poprzedniej lub następnej strony panelu.

Zamknij belkę przyciskiem albo dotknij panelu poniżej niej. Stan Wi-Fi i ikona baterii z procentami w środku znajdują się w prawym górnym rogu belki. W ekranach konfiguracji są widoczne stale. Stan baterii jest szacowany na podstawie pomiaru napięcia; jego odświeżanie nie wymaga przerysowania całego ekranu.

Alternatywny dostęp do konfiguracji: przytrzymaj pięć palców na ekranie przez sekundę. Ten gest również wymaga hasła. W **Ustawienia → Zmień hasło** wpisz nowe hasło dwukrotnie. Powrót do panelu, restart albo dziesięć minut bezczynności ponownie blokuje konfigurację. Po pięciu nieudanych próbach trzeba odczekać 30 sekund. Hasło konfiguracji jest osobne od kont Studio i Raspberry Pi; urządzenie zapisuje jego skrót z losową solą.

## Projektowanie

W projektancie wybierz wariant **TAB5** i rozmiar **1280 × 720**, aby układ odpowiadał wymiarom urządzenia. Dostępne są przyciski, przełączniki, suwaki, fadery, pokrętła, wartości liczbowe, wskaźniki, teksty, obrazy i nawigacja. Rozmiar tekstu dostosowuje się do skali strony i dostępnego miejsca. Brak warunku widoczności oznacza, że element jest widoczny. Przypisany warunek musi mieć aktualną wartość logiczną prawda.

Możesz zapisać oddzielne panele z różnych stron tego samego opublikowanego projektu. Zaznacz tylko potrzebne strony i nadaj układowi własną nazwę. Przyciski prowadzące do niewybranych stron są pomijane w kopii dla TAB5; podgląd informuje o tym przed wysłaniem. Sam projekt pozostaje zachowany. Różne nazwy nadane tym samym stronom tworzą kopie tego samego układu.

Istniejące strony o innych proporcjach są dopasowywane do całego ekranu. Grafiki zachowują sposób dopasowania **contain**, **cover** lub **stretch** ustawiony w projekcie. Dla najlepszego układu użyj osobnego wariantu TAB5.

Grafiki SVG są zamieniane w Studio na PNG wyłącznie do wysłania na urządzenie. Oryginały pozostają w projekcie. Obsługiwane są PNG i podstawowy JPEG, do 384 KiB oraz 4096 × 4096 pikseli na obraz. Panel może mieć do 16 stron, 100 elementów na stronie i 1,5 MiB danych. CSS, szkło, materiały i zaawansowane kadrowanie tła nie są odtwarzane przez natywny interfejs; podgląd przed wysłaniem pokazuje ostrzeżenia.

Ostatni panel pozostaje zapisany po restarcie. Gdy połączenie z kontrolerem jest nieaktualne, sterowanie zostaje zablokowane. Polecenia nie są odkładane do późniejszego odtworzenia. Odwołanie urządzenia w Studio unieważnia jego dostęp.

## Pamięć SD i płynność

Układ i grafiki są rysowane lokalnie. Malina przesyła tylko zmienione wartości kontrolek i odbiera polecenia. Zmiany stanu są próbkowane 30 razy na sekundę; niezmienione kontrolki nie są przerysowywane. Pod palcem suwak od razu pokazuje lokalną wartość, a polecenia są łączone, aby nie przeciążać sieci.

Przed wysłaniem wpisz **Nazwę zapisywanego panelu**. Karta SD z FAT lub exFAT przechowuje do 32 układów przypisanych do sparowanej maliny. Karta nie jest formatowana przez aplikację. Gdy biblioteka jest pełna, ostatni wysłany panel nadal zapisuje się w pamięci wewnętrznej, a istniejące pliki SD pozostają zachowane. Listę otworzysz przez **belkę → Panele**. Bez połączenia możesz przeglądać zapisane strony; sterowanie uruchomi się dopiero po sprawdzeniu wybranego panelu przez malinę. Panel z innej opublikowanej rewizji projektu wymaga ponownego wysłania ze Studio.

Nowy błąd sekwencji uruchomionej z panelu pojawia się również jako komunikat na TAB5. Dotknij komunikatu, aby go zamknąć. Pełne szczegóły pozostają w historii maliny.

## Aktualizacja firmware przez Wi-Fi

1. Połącz TAB5 z Wi-Fi i właściwą maliną. Pierwsza instalacja obsługi OTA wymaga USB; użyj przygotowanego firmware 0.2.3 lub nowszego.
2. W **Ustawienia → Panele M5Stack TAB5 → Firmware przez Wi-Fi (OTA)** wybierz plik **firmware.bin** aplikacji AV Control TAB5 ST7123. Plik może mieć do 5 MiB.
3. Wybierz wersję i naciśnij **Aktualizuj firmware** przy właściwym urządzeniu. Uprawnienia administratora Studio są wymagane do zlecenia aktualizacji.
4. TAB5 poczeka na zwolnienie przycisków i zakończenie edycji ustawień. Przy baterii poniżej 20% poczeka na ładowanie. Pokaże postęp pobierania, sprawdzi plik i uruchomi się ponownie.
5. Poczekaj na **Aktualizacja potwierdzona** w Studio. Ten komunikat oznacza sprawdzenie nowego firmware po restarcie. Wi-Fi, parowanie, hasło konfiguracji, jasność, głośność i panele zostają zachowane.

Aktualizacja zapisuje drugi obszar aplikacji. Niepełny albo błędny plik nie zastępuje działającej wersji. Jeśli nowa aplikacja nie przejdzie kontroli rozruchu w ciągu minuty, urządzenie wróci do poprzedniej wersji. Połączenie z maliną musi działać podczas pierwszego startu nowej wersji. OTA aktualizuje aplikację ESP32-P4; nie zmienia układu pamięci ani oprogramowania radia ESP32-C6.

## Firmware i pakiety

Obsługa TAB5 jest częścią oficjalnego Studio od 1.6.6. Pobierz pakiet firmware 0.2.5 oraz aplikacje z [wydania 1.6.7](https://github.com/Gartom91/av-control-studio/releases/tag/v1.6.7). Pierwsze wgrywanie przez USB opisuje instrukcja dołączona do pakietu; dalsze aktualizacje aplikacji wykonasz ze Studio przez Wi-Fi. Numer firmware jest niezależny od numeru Studio.

Zwykłe wgrywanie firmware zachowuje Wi-Fi, parowanie, hasło konfiguracji i ustawienia. Jeśli hasło zostanie zapomniane, odzyskanie dostępu wymaga fizycznego USB i jawnego wymazania pamięci ustawień; usuwa to także Wi-Fi i parowanie. Hasła nie można odczytać przez menu ani diagnostykę USB.

W firmware 0.2.5 zmiana konfiguracji chronionego panelu przez USB wymaga najpierw lokalnego odblokowania menu hasłem. Samo podłączenie kabla nie odblokowuje konfiguracji. Pierwsze przygotowanie bez ustawionego hasła pozostaje osobnym etapem. Firmware 0.2.5 obsługuje również kontrolki powiązane wyłącznie z akcją. Historyczne próby sprzętowe firmware 0.2.3 nie są odbiorem nowego pliku 0.2.5.

Sprzęt i sposób wejścia do trybu wgrywania opisuje [dokumentacja M5Stack TAB5](https://docs.m5stack.com/en/core/Tab5).

Od firmware 0.2.4 panel po starcie lub wyborze z SD potwierdza układ przez przypięte połączenie z kontrolerem przed włączeniem sterowania. Podczas braku sieci zachowuje wyłącznie lokalny podgląd. Skan biblioteki ma ograniczony zakres pracy; katalog powinien zawierać tylko pliki paneli zapisane przez TAB5.
