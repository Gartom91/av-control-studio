# Instrukcja AV Control Studio 1.6.5

Na ekranie powitalnym znajdziesz **Otwórz projekt szkoleniowy** oraz **Podręcznik szkoleniowy**. Ilustrowany kurs Signal Workshop działa offline: 206 stron, 52 rozdziały, 4 dodatki i 77 ilustracji. Neutralny przykład Wirtualna sala AV ma 5 stron, 10 urządzeń i 3 ekspandery sieciowe. [Źródło kursu](tutorial/TUTORIAL-PL.md). Administrator kontrolera ma zakładkę **Raspberry Pi**: [konfiguracja WWW](KONFIGURACJA-RPI-PL.md).

## 1. Instalacja programu Windows

Uruchom instalator z wydania. Program instaluje się dla bieżącego użytkownika. Zawiera własne środowisko .NET i silnik Python. Jeśli WebView2 nie jest zainstalowany, instalator uruchamia dołączony pakiet Microsoft offline.

Program uruchomisz z menu Start. Pierwsze połączenie prowadzi do lokalnego symulatora: **admin / simulation**. Ten tryb jest dostępny wyłącznie na tym komputerze, pod adresem loopback. Konto fizycznego RPi ma hasło ustawione osobno podczas konfiguracji.

Instalator Studio nie jest podpisany własnym certyfikatem wydawcy. Porównaj sumę SHA256 z plikiem wydania. Deinstalacja programu pozostawia projekty i ustawienia użytkownika.

## 2. Pierwszy projekt

Na stronie **Projekt** wybierz nowy pusty projekt albo **Otwórz przykład**. Nazwę instalacji można zmieniać. Lista **Bieżący projekt** pozwala przełączać projekty zapisane lokalnie.

Zmiany są automatycznie zapisywane w magazynie Studio. **Zapisz** eksportuje przenośny plik .avctrl. W aplikacji Windows kolejne zapisy aktualizują otwarty plik; **Zapisz jako** tworzy nowy plik. W przeglądarce zapis pobiera plik. **Otwórz** wczytuje .avctrl. Dane połączeń i logowania nie trafiają do projektu.

Przyciski **Cofnij** i **Ponów** oraz Ctrl+Z / Ctrl+Shift+Z obejmują zmiany projektu. Ctrl+S zapisuje projekt.

Projekt demonstracyjny jest neutralny. Jego ramki nie stanowią protokołu żadnego konkretnego urządzenia. Przed komunikacją z urządzeniem skonfiguruj protokół zgodnie z jego dokumentacją.

### Organizacja obszaru roboczego

Podpowiedzi i bloki instrukcji mają **X** w prawym górnym rogu. Kliknij, aby ukryć cały blok. W **Ustawienia → Podpowiedzi i instrukcje** znajdziesz listę ukrytych podpowiedzi, wyszukiwanie, przywracanie pojedynczego bloku i **Przywróć wszystkie podpowiedzi**. Studio zapamiętuje wybór na tym stanowisku dla wszystkich projektów, także po restarcie. Ukrywanie obejmuje 100 rodzajów podpowiedzi: ekran powitalny, urządzenia, ekspandery, protokoły, sygnały, kreatory, logikę, Python, panele, metrykę, diagnostykę i ustawienia.

Karta **Urządzenia** oraz konfiguracja **Raspberry Pi** wykorzystują pełną szerokość strony. Panel konfiguracji otwarty z eksploratora Logiki ma przycisk **Rozwiń konfigurację na cały obszar**, który przełącza między pełnym i wąskim widokiem.

**Debugger** w Logice można umieścić pod, nad, po lewej lub po prawej stronie schematu. Przeciągnij separator, aby regulować wysokość lub szerokość. Dwuklik przywraca podział 50/50; separator obsługuje też Tab, strzałki, Shift ze strzałką, Home, End i Enter. Położenie oraz osobne proporcje obu wymiarów są zapamiętywane lokalnie. Przycisk **Pełne okno debuggera** powiększa widok, a **Debugger w osobnym oknie** pozwala przenieść go na drugi monitor. W przeglądarce zezwól na otwieranie okien dla Studio. **Przenieś debugger do Studio** lub zamknięcie osobnego okna przywraca podział. Bieżąca karta, wyszukiwanie, pinezki i zatrzymany ślad pozostają zachowane. Osobne okno wymaga działającego głównego Studio i zamyka się po wylogowaniu.

## 3. Sygnały

W **Sygnały** dodaj wartości logiczne, liczbowe, tekstowe albo bajty. Ustaw wartość początkową, możliwość zmiany przez panel oraz czas przeterminowania. Czas 0 wyłącza przeterminowanie.

Sygnał zawiera wartość i jakość: poprawna, przeterminowana, nieznana albo błąd. Zezwolenie wymaga wartości TRUE o poprawnej jakości. Dane nieznane lub stare nie zezwalają na wykonanie interlocku.

Zaznacz **Zachowaj po restarcie**, aby wybrana wartość była przechowywana w SQLite. Pamięci bloków mają własny wybór zachowania. Timery i sekwencje po restarcie rozpoczynają się zatrzymane.

Sygnały urządzeń i wyjścia logiki są aktualizowane przez silnik. Panel/API nie mogą nadpisywać fizycznych wejść ani wyjść grafu i w ten sposób omijać interlocków.

## 4. Profile protokołów

W **Protokoły** dodaj profil. Skonfiguruj sposób wydzielania ramek: delimiter HEX, stała długość, pole długości, przerwa między bajtami albo datagram.

Każda komenda składa się z uporządkowanych składników:

- tekst ASCII lub UTF-8;
- stałe bajty HEX;
- parametr tekstowy, liczbowy lub logiczny;
- pole długości;
- suma kontrolna.

Dostępne są formaty liczb całkowitych, float32/64, kolejność big/little endian, formatowanie tekstowej liczby, SUM8/16, XOR8, CRC16 Modbus/CCITT i CRC32. Pole długości może obejmować poprzedzającą część, pozostałą część lub całą ramkę; offset pozwala dopasować nagłówek/terminator do definicji producenta. Suma jest liczona w określonym zakresie bajtów. Zakończenie ramki wpisuje się w HEX, np. **0D 0A**.

Ustaw timeout i odstęp między komendami. Ponowienia są dopuszczalne tylko po zaznaczeniu **Bezpieczna do powtórzenia**.

W **Odpowiedzi** ustaw dopasowanie tekstu/HEX, pola, offsety, długość, format, bity, skalowanie i mapowanie stanów. Każde pole ma własny identyfikator niezależny od projektu. W urządzeniu przypisz te identyfikatory do sygnałów instalacji.

Potwierdzenie komendy wybiera definicję odpowiedzi. Powiązania odpowiedzi z parametrami pozwalają np. potwierdzić tylko odpowiedź o wartości zgodnej z wysłanym parametrem. Spóźniona odpowiedź o innej wartości aktualizuje odczyt, ale nie potwierdza nowszego żądania.

Odpowiedzi spontaniczne są dekodowane tak samo jak odpowiedzi na polecenia. Odpytywanie dodaje się w urządzeniu, wskazując zadeklarowaną akcję oraz interwał.

**Zapisz profil w bibliotece** pozwala użyć go ponownie. Profil nie przechowuje konkretnego adresu TCP ani portu COM.

## 5. Urządzenia

Dodawaj kolejne urządzenia w **Urządzenia**. Każde można duplikować i usuwać.

| Transport | Najważniejsze ustawienia |
| --- | --- |
| RS-232 / RS-485 / UART | USB-RS232/485 i UART Maliny; port, stabilny identyfikator USB, parametry transmisji, kierunek RS-485 i odstępy |
| TCP | Klient lub nasłuch, adres/port, ponowne połączenie, timeout |
| UDP | Adres/port docelowy, lokalny port odbioru i przypisanie źródła |
| GPIO | Wykryty chip i linia, kierunek, polaryzacja, bias, debounce, sygnał, stan początkowy i bezpieczny |
| Ekspander sieciowy RS-232 / RS-485 | Bramka Ethernet/Wi-Fi, kanał i port TCP/UDP/RFC2217, format transmisji oraz profil protokołu |

Wybierz profil i mapowanie jego pól do sygnałów. Dwa urządzenia mogą używać jednego profilu i oddzielnych odczytów.

**Nowy ekspander Ethernet/Wi-Fi:** w **Urządzenia** wybierz **Dodaj ekspander sieciowy**. Kreator przeprowadza przez adres bramki, sposób komunikacji, liczbę kanałów, porty i parametry RS-232/RS-485. Podsumowanie tworzy bramkę i osobne urządzenie dla każdego kanału. Nowe urządzenia są wyłączone do czasu świadomego włączenia i publikacji projektu. Pobierz plan ustawień, aby zastosować go w panelu producenta. RFC2217 ustawia format portu zdalnie, jeśli konwerter obsługuje ten standard; w trybach zwykłego TCP/UDP ustaw go w panelu konwertera. Adres odbiornika na wspólnej magistrali RS-485 jest parametrem komendy, a nie numerem portu TCP. [Pełna instrukcja](EKSPANDERY-SIECIOWE-PL.md).

**Nowy adapter USB–Ethernet:** podłącz kartę do maliny i otwórz **Raspberry Pi → Zmień ustawienia sieci**. Wybierz wykrytą kartę po MAC. Dla dodatkowej sieci urządzeń wybierz rolę **Sieć urządzeń — bez domyślnej bramy** i osobną podsieć, np. `192.168.50.1/24`. Profil zostanie związany z MAC, także po zmianie nazwy interfejsu. Zapis wymaga potwierdzenia działającego połączenia w ciągu 120 sekund; bez potwierdzenia wraca poprzednia konfiguracja. Nie jest tworzony serwer DHCP ani most sieciowy. Ćwiczenia: rozdziały 29–32 kursu.

**Nowy konwerter USB:** podłącz go do kontrolera RPi, połącz Studio z tym RPi, w **Urządzenia** kliknij **Odśwież porty i GPIO**, dodaj urządzenie i wybierz **RS-232 / RS-485 / UART**. Ustaw **Interfejs szeregowy**, wykryty port, parametry transmisji oraz profil, a potem opublikuj projekt. Dla USB preferuj **/dev/serial/by-id**; gdy konwerter nie ma unikalnego numeru seryjnego, użyj **/dev/serial/by-path** i tego samego gniazda. Lokalny symulator Windows używa transportów wirtualnych.

RS-485 ma tryb automatyczny, sprzętowy sterownika i programowy RTS. **W nowym obrazie AV Control 1.3 UART jest domyślnie włączony, a konsola szeregowa wyłączona.** Na 3B/4B użyj `/dev/serial0` → `/dev/ttyAMA0`; Bluetooth jest wyłączony na rzecz pełnego PL011. Na 5 użyj `/dev/ttyAMA0` na GPIO14/15, ponieważ `serial0` może oznaczać oddzielne złącze debug. UART ma poziomy **3,3 V** i wymaga transceivera do RS-232 lub RS-485. Pełna procedura: [USB-RS485-UART-PL.md](USB-RS485-UART-PL.md). Stan i ustawienia systemu są dostępne przez WWW w zakładce **Raspberry Pi**, opisanej w [KONFIGURACJA-RPI-PL.md](KONFIGURACJA-RPI-PL.md).

W trybie TCP nasłuchu jedno urządzenie oznacza jedno połączenie równocześnie. Konflikty portów i przypisanie tej samej linii GPIO są zgłaszane przed aktywacją. RPi 5 może mieć inne nazwy chipów niż RPi 3/4 — korzystaj z wykrytych możliwości kontrolera.

GPIO obsługuje linie cyfrowe. Akcje impulsowe mają określony czas; impulsy na urządzeniu są wykonywane kolejno. Anulowanie impulsu przywraca linię, a zamknięcie transportu stosuje skonfigurowany stan bezpieczny.

## 6. Akcje, sekwencje i interlocki

W **Akcje i sekwencje** wybierz ustawienie sygnału, wysłanie komendy, zapis GPIO, sekwencję lub anulowanie sekwencji. Parametry mają nazwę i typ; wartości mogą pochodzić z elementu panelu albo wejścia bloku logiki.

Sekwencja składa się z kroków: akcja, opóźnienie, oczekiwanie na warunek, rozgałęzienie, zakończenie lub błąd. Wysłanie komendy z przypisaną odpowiedzią czeka na jej potwierdzenie. Timeout powoduje błąd sekwencji. Przycisk anulowania można przypisać do osobnej akcji **Anuluj sekwencję**.

W **Zezwolenia akcji** wybierz wymagane sygnały zezwolenia i akcje objęte blokadą. Skonfiguruj akcję wykonywaną po utracie zezwolenia. Warunek jest sprawdzany także przed rzeczywistym wysłaniem oczekującej komendy. Osobny symbol **Interlock** w schemacie logiki zapamiętuje wybrane wyjście; opis poniżej.

Grupy wzajemnego wykluczania mogą działać na czas komendy albo przez zajęcie/zwolnienie grupy. Wybierz nazwę grupy i tryb w akcji. Zwolnienie jest jawną akcją projektu.

Anulowane sekwencje nie wysyłają zaległych kroków. Wykonanej wcześniej komendy nie można cofnąć; ewentualne zatrzymanie urządzenia musi być osobną, skonfigurowaną akcją.

## 7. Schematy logiki

W **Edytor logiki** dodawaj bloki z palety i łącz uchwyty wejść/wyjść. Właściwości określają sygnały, stałe, czas i wartości początkowe. **Zmieść schemat** pokazuje wszystkie bloki.

Dostępne są bramki AND/OR/NOT/NAND/NOR/XOR/XNOR, porównania, matematyka, skalowanie, wybór wartości, zbocza, pamięci, SR/RS/D latch, D/T/JK flip-flop, liczniki oraz TON/TOF/TP. Sygnał i parametry akcji mają typ bool/number/string/bytes.

Bramki mają konfigurowaną liczbę wejść, np. AND z czterema wejściami. XOR jest TRUE dla nieparzystej liczby wejść TRUE, XNOR odwraca ten wynik. Wielokanałowy NOT odwraca każde wejście oddzielnie. Zmniejszenie liczby wejść usuwa połączenia usuwanych portów; **Cofnij** przywraca je.

Symbol **Interlock** ma wejścia impulsowe i odpowiadające im wyjścia. Zbocze narastające jednego wejścia zapamiętuje jego wyjście TRUE i zeruje pozostałe. **SET ALL HIGH** ustawia wszystkie, **CLEAR** zeruje wszystkie; CLEAR ma pierwszeństwo. Przy jednoczesnych impulsach wygrywa wejście o najniższym numerze.

Symbol **Truth table** ma oddzielne liczby wejść i wyjść. Kliknij **Edytuj tablicę prawd** i w środkowym oknie zaznacz kombinację wyjść dla każdego wejścia. Impuls na wejściu wybiera jego wiersz i zapamiętuje całą kombinację aż do następnego impulsu lub CLEAR. Stan początkowy TRUE i powrót jakości odczytu nie tworzą impulsu. Dla obu symboli możesz wybrać zachowanie pamięci po restarcie.

W **Symbole Python** dodasz symbol z nazwanymi portami, parametrami i kodem Python. Formularz sprawdza kod oraz wykonuje próbę z podanymi wejściami i pamięcią. Porty łączysz w schemacie jak w blokach wbudowanych. Pełny podręcznik i przykłady: [SYMBOLE-PYTHON-PL.md](SYMBOLE-PYTHON-PL.md), dostępny także offline z edytora. Projekt **Sceny-i-logika.avctrl** pokazuje bramkę AND4, Interlock, Truth table i licznik Python.

SR daje priorytet SET, RS daje priorytet RESET. Przerzutniki reagują na zbocze narastające; reset ma pierwszeństwo. Pętla kombinacyjna jest odrzucana. Sprzężenie musi przejść przez blok pamięci.

W podglądzie online połączenia pokazują wartość i jakość, a bloki stan pamięci/timera. Sekwencje i przyczyny odmowy są widoczne w diagnostyce.

Schemat można zapisać jako moduł w bibliotece. Określ wejścia i wyjścia modułu, a potem wstaw go wielokrotnie z palety. Instancje posiadają oddzielny stan wewnętrzny.

Restart i ponowne otwarcie panelu nie odtwarzają wcześniejszych poleceń. Działania startowe uruchamiają się tylko wtedy, gdy administrator doda je do listy akcji startowych projektu.

## 8. Panele WYSIWYG

W **Edytor paneli** dodawaj strony i elementy z palety: przycisk, przełącznik, fader, slider, pokrętło, wartość, kontrolka, tekst, grafika i nawigacja.

Przeciągaj elementy, zmieniaj rozmiar uchwytem lub polami właściwości. Shift pozwala wybrać wiele elementów. Dostępne są siatka, wyrównanie, grupowanie, rozgrupowanie, kopiowanie i warstwy.

Właściwości obejmują wygląd, zakres, krok, jednostkę oraz powiązania. Tekst, kolor, widoczność i dostępność można powiązać z sygnałami. Podczas projektowania ukrywane lub blokowane elementy nadal można wybrać i edytować.

Każdy element ma **Pokaż etykietę tekstową**; wyłączenie ukrywa podpis, pozostawiając nazwę w edytorze. Suwaki, fadery, pokrętła i kontrolki mają także **Pokaż wartość / stan**. Zaznacz **Grafika** i wybierz **Wybierz grafikę z dysku**, aby od razu przypisać plik PNG/JPG/SVG. Ustaw ramkę, jej kolor i grubość oraz zaokrąglenie rogów.

Zaawansowany wygląd obejmuje **CSS elementu**, własne klasy i **CSS strony**, dostępny przez **Wygląd strony / CSS**. Podgląd aktualizuje się na żywo, a grafiki i style są zapisywane w projekcie. Przykłady i pełna instrukcja: [PANELE-I-CSS-PL.md](PANELE-I-CSS-PL.md), także offline w edytorze.

Wybierz wariant PC/tablet/telefon i dostosuj geometrię. Powiązania pozostają wspólne. Renderer podglądu i panelu operatora jest ten sam. Edytor nie wykonuje akcji urządzeń po kliknięciu edytowanego elementu.

Suwaki/fadery/pokrętła mają odstęp wysyłania w ms, z minimum 20 ms. Po zakończeniu ruchu wysyłana jest wartość końcowa. Kolejka scala wartości oczekujące dla tego elementu.

Przycisk chwilowy jest aktywny podczas przytrzymania. Panel odnawia dzierżawę co 500 ms; po utracie połączenia silnik zwalnia go najpóźniej po 2 s. Wysyłanie komend i stan urządzenia są oddzielnymi etapami; kliknięcie nie jest dowodem wykonania przez fizyczne urządzenie.

## 9. Symulator

Wybierz **Uruchom symulację**, aby zwalidować i aktywować projekt w lokalnym silniku. Wszystkie cztery transporty są wirtualne. Logika jest ta sama co na RPi.

W **Diagnostyka** wybierz urządzenie, ustaw opóźnienie, awarię, utratę UDP lub odpowiedź HEX i zastosuj. Obserwuj faktyczne bajty ramek, żądania, wysłanie, przyjęcie i potwierdzenie. Można też wymuszać wejścia symulatora.

Błąd CRC nadaje odczytowi jakość błąd. Rozłączenie zmienia jakość na nieznaną. Utrata UDP może skutkować timeoutem; system nie zakłada doręczenia datagramu.

## 10. Przygotowanie Raspberry Pi

Obraz wydania jest dla RPi 3B/4B/5, na bazie Raspberry Pi OS Lite 64-bit. Do uruchomienia potrzebujesz karty SD, zasilania i sieci lokalnej.

1. Zainstaluj osobną aplikację **AV Control Imager 1.4.0**. Obraz i program zapisujący są dołączone do instalatora; internet nie jest wymagany.
2. Wybierz RPi 3B, 4B lub 5, kartę SD (minimum 8 GB), nazwę kontrolera i hasło administratora. Ustaw konto systemowe RPi i opcjonalnie Wi-Fi/SSH.
3. Przygotuj zapis, sprawdź docelowy nośnik i zatwierdź jego wymazanie. Aplikacja zapisze i zweryfikuje kartę.
4. Włóż kartę do RPi i uruchom. Pierwszy start konfiguruje system i usługę HTTPS. Dane parowania pojawią się w **AV-Control-parowanie.txt** oraz **AV-Control-CA.crt** na partycji boot.

Pełna instrukcja konfiguratora i odtwarzacza: [APLIKACJE-PL.md](APLIKACJE-PL.md). Obraz **AV-Control-RPi-1.2.1-arm64.img.xz** jest też dostępny osobno. W oficjalnym Imagerze użyj katalogu opisującego format cloud-init; samo wybranie lokalnego obrazu nie udostępnia konfiguracji systemu. Studio nadal pozwala zapisać avctrl-setup.json na już przygotowanej partycji boot.

Aby odczytać dane parowania, użyj skonfigurowanego wcześniej SSH/konsoli albo wyłącz RPi poprawnie z konta systemowego i odczytaj kartę na PC. Z konsoli dostępne są:

```sh
sudo cat /boot/firmware/AV-Control-parowanie.txt
sudo systemctl status avcontrol.service
```

Alternatywnie całą konfigurację można przeprowadzić z konsoli poleceniem **sudo avctrl-setup**. Nie uruchamiaj ponownej konfiguracji istniejącej instalacji bez kopii jej danych, ponieważ zmienia konto administratora i certyfikat serwera.

Brak konfiguracji pozostawia usługę aplikacji nieaktywną. Kontroler nie udostępnia fabrycznego hasła sieciowego.

## 11. Parowanie i publikowanie

W Studio Windows wybierz **Ustawienia → Połączenia**. Dodaj nazwę instalacji, adres HTTPS i odcisk SHA256 z danych kontrolera. Odcisk, nazwa hosta i ważność certyfikatu są weryfikowane. Zaloguj się hasłem administratora kontrolera.

Studio przechowuje listę połączeń poza projektem, zaszyfrowaną przez Windows DPAPI dla użytkownika. Projekty można publikować na różnych kontrolerach.

W **Publikowanie** zwaliduj projekt, przygotuj wersję i aktywuj ją. Skrót publikowania wykonuje te etapy kolejno. Błąd przygotowania/aktywacji pozostawia poprzednią wersję; historię można przywracać. Projekt z poprawnym adresem, ale nieosiągalnym urządzeniem, może się aktywować z urządzeniem offline — sprawdzaj diagnostykę połączeń.

Jeden RPi wykonuje jeden aktywny projekt. Po zamknięciu Studio logika, odpytywanie i komunikacja działają dalej.

## 12. Operatorzy, odtwarzacz i przeglądarka

Osobna aplikacja **AV Control Player** odtwarza panel bez zainstalowanego Studio. Połącz kontroler przez HTTPS i odcisk certyfikatu, zaloguj operatora i używaj opublikowanych stron. Własny instalator, zapisane połączenia i pełny ekran opisano w [APLIKACJE-PL.md](APLIKACJE-PL.md).

Administrator dodaje konta w **Ustawienia**. Operator obsługuje aktywny panel, lecz nie edytuje urządzeń, projektów ani uprawnień.

Na innym PC, tablecie lub telefonie zaufaj **publicznemu CA** kontrolera w systemowym magazynie certyfikatów i otwórz jego adres HTTPS. Nigdy nie przenoś prywatnych plików .key. Adres musi odpowiadać nazwie/IP wpisanej do certyfikatu.

Logowanie do panelu jest niezależne od konta systemowego RPi. Sesja trwa maksymalnie 12 godzin. Zmiana hasła unieważnia sesje konta.

Wiele paneli widzi wspólny stan. Stara wersja panelu i powtórzone żądanie o tym samym identyfikatorze nie wykonują nowej komendy. Nie ponawiaj ręcznie operacji niebezpiecznej do powtórzenia tylko dlatego, że zniknęło połączenie.

## 13. Kopie zapasowe i diagnostyka

Projekt eksportuj do .avctrl. Biblioteka oraz robocze projekty Studio są w magazynie WebView2 bieżącego użytkownika. Dane połączeń: **%LOCALAPPDATA%\\AV Control Studio\\controllers.dpapi**. DPAPI wiąże je z kontem Windows.

Na RPi zatrzymaj usługę przed kopią całego **/var/lib/avcontrol**, aby zachować bazę, pamięci i certyfikaty razem. Po przywróceniu uruchom usługę. Zachowaj uprawnienia katalogu i nie udostępniaj kopii prywatnych kluczy.

Diagnostyka pokazuje czas skanu, opóźnienie timerów, pamięć procesu, kolejki, porty, jakość sygnałów i ramki. Przy dużym obciążeniu zegar 20 ms jest nominalny; raport testów zawiera rzeczywiste opóźnienia.

## 14. Granice potwierdzenia sprzętowego

Pakiet ARM64 sprawdzono w QEMU użytkowym i testach komputerowych. Nie wykonano pełnego rozruchu kernela obrazu na fizycznym RPi 3B/4B/5, pomiarów GPIO ani testu konwertera USB na takim RPi. Przed oddaniem konkretnej instalacji sprawdź na jej sprzęcie adresy/linie, polaryzację, bezpieczne stany, odpowiedzi i zachowanie po odłączeniu zasilania. Test telefonu w raporcie jest emulacją przeglądarki.

## 15. Aktualizacje automatyczne

Studio, Player i Imager aktualizują się z wydań GitHub. W Studio otwórz **Ustawienia → Aktualizacje Studio**, a w pozostałych aplikacjach przycisk **Aktualizacje** na górnym pasku. Włącz sprawdzanie raz dziennie oraz opcjonalnie pobieranie w tle i instalowanie po zamknięciu aplikacji. Pakiety są sprawdzane sumą SHA256 przed uruchomieniem instalatora.

Silnik RPi aktualizujesz jako administrator w **Ustawienia → Aktualizacje Raspberry Pi**. Wybierz ręczną instalację albo automatyczne okno czasowe. Nie trzeba ponownie zapisywać karty SD; zachowane są projekty, pamięci, konta i certyfikaty. Nieudane uruchomienie nowej wersji powoduje przywrócenie poprzedniej wraz z kopią danych. Domyślnie automatyka jest wyłączona, aby system działał bez internetu. Pełna instrukcja, powrót do poprzedniej wersji i migracja: [AKTUALIZACJE-PL.md](AKTUALIZACJE-PL.md).
