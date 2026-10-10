# Weryfikacja AV Control 1.6.0

Ten dokument rozdziela implementację, próby programowe, pakiety i odbiór fizycznego sprzętu. Wydanie wymaga zielonego CI dla dokładnego końcowego commitu oraz raportu wiążącego instalatory i obraz z ich sumami SHA-256.

## Nowe funkcje

- Metryka: wersjonowane dane, stabilne identyfikatory wpisów, prawidłowe daty, UTF-8, zapis/import ZIP, restart, historia wdrożeń i przywrócenie.
- UI: ekran powitalny, pola projektu, cofanie/ponawianie, eksport, jasny/ciemny motyw, tablet, filtracja i stronicowanie 101 urządzeń symulowanych.
- Monitoring: histereza incydentów, brak fikcyjnej naprawy po wyniku nieznanym/odłożonym/serwisowym, restart, potwierdzenia, kolejność, luki raportów, budżety pamięci i brak raportowania pełnych danych przed przypisaniem do hostingu.
- Podgląd roboczy: aktualizacja po zmianach i co około 200 ms, timery, Cofnij/Ponów, reset własnej pamięci, izolacja od aktywnego programu i brak wykonywania poleceń/pełnego CPythona.
- Komunikacja: sondy tylko jako zadeklarowane akcje z odpowiedzią i zgodą na odczyt, interlock, zajęta kolejka, zmiana projektu, błędy ramek i UDP oraz odzyskanie po poprawnej odpowiedzi.
- Stan transportu: gniazdo UDP, połączenie TCP i otwarty port szeregowy odróżnione od aktualnej odpowiedzi; systemowy TCP keepalive sprawdzony na prawdziwych socketach lokalnych. Próba nie potwierdza elektrycznej komunikacji z urządzeniem.
- Hosting: niezależna baza, zachowanie wspólnego dokumentu TECHNIKAV, zakresy uprawnień, części raportów, starsze uruchomienia, duplikaty, odczyt per konto, popup, telefon i konfiguracja poczty właściciela.
- Poczta: zastępczy transport testowy, brak rzeczywistych wysyłek; weryfikacja deduplikacji, błędu, jawnego ponowienia i odebrania uprawnień przed dostawą.

Dowody nowych funkcji znajdują się w `docs/evidence/service-1.6.0/`. Nie należy traktować raportów 1.5.5 jako odbioru nowych funkcji diagnostycznych.

## Pakiety i próby wykonane przed publikacją

- Pełny silnik Windows: **421 PASS, 14 SKIP** (m.in. próby wymagające POSIX), dwie ostrzegawcze informacje zależności. Kontrolę praw dostępu kiosku wykonano dodatkowo w Linux; CI wykonuje również całość dla Linux.
- Studio Windows: rzeczywista instalacja końcowego instalatora, samokontrola, natywne WebView2, podręcznik i odinstalowanie. Oddzielna próba pełnego Pythona: świeży katalog danych, NumPy 2.5.3 z wheel offline, import helpera, wyniki i unieważnienie zgody po zmianie kodu.
- Player i Imager Windows: rzeczywiste instalacje końcowych pakietów, próby natywnego interfejsu i odinstalowanie. Imager sprawdził zawarty obraz; **nie zapisywał fizycznego nośnika**.
- Linux Player: rzeczywista instalacja `.deb` w środowisku Debian 13 i natywne GTK/WebKit; logowanie, panel, zgodność certyfikatu, brak edytora i kolejki offline. Środowisko testowe, bez odbioru fizycznego pulpitu Linux.
- ARM64: rzeczywiste procesy aarch64 pod QEMU, importy skompilowanych pakietów, aktualizacja 1.5.3 → 1.6.0, zachowanie SQLite/kont/sesji/pamięci/certyfikatu i powrót po błędzie zdrowia. **Systemd i fizyczna aktualizacja wymagają odrębnego odbioru po publikacji.**
- Czysty obraz: konfiguracja UART dla 3B/4B/5, uprawnienia niewuprzywilejowanego kiosku i 186 pakietów offline. Natywny panel Wayland/GTK/WebKit sprawdzono na wirtualnym ekranie. Nie potwierdza to fizycznego HDMI/dotyku/VT.
- Benchmark Windows: **100 urządzeń symulowanych, 2000 bloków, 5 paneli**. Serie zwykła i przeciążeniowa mają oddzielne raporty z opóźnieniami, RAM i CPU; nie stanowią gwarancji tych samych wyników na RPi.

`docs/evidence/package-verification-1.6.0.json` wiąże osiem końcowych artefaktów z sumami SHA256 i sześcioma raportami prób pakietów. Publikowanie wymaga jeszcze zielonego CI **dokładnego commitu**. Nowa maszyna Windows bez WebView2, podpis Authenticode wydawcy i fizyczny zapis SD pozostają niepotwierdzone.

## Dokumentacja i ograniczenia

Główny `tutorial/AV-Control-Studio-Tutorial-PL-Signal-Workshop.pdf`: 191 stron, 52 rozdziały, 4 dodatki, 72 ilustracje (69 zrzutów i 3 schematy). HTML zachowuje pełne PNG. Konta, klawiatura, metryka, monitoring oraz tła paneli są scalone w oryginalnym dokumencie; osobny suplement usunięto. Program obejmuje 10 sesji / 22 godziny.

Tła: 13 prób walidacji i archiwum po stronie silnika; testy geometrii i zgodności wersji po stronie Studio. Test rzeczywistego UI obejmuje trzy gradienty, upload z listy, osiem trybów dopasowania obrazu, kadrowanie przed skalowaniem, cztery sposoby wypełniania 9-slice, piksele czterech narożników, wariant telefonu, zapis/import, zgodność panelu i edytora oraz odłączenie/Cofnij. Dowód: `docs/evidence/service-1.6.0/panel-backgrounds.json`.

Nowe pomiary mogą być nieznane na systemie bez odpowiedniej metryki. Historia incydentów nie zawiera pełnej serii każdej próbki. Podane wskazówki serwisowe są konfiguracją instalatora i hipotezami, a nie rozpoznaniem fizycznego uszkodzenia.

Do oddzielnego potwierdzenia: rzeczywiste odłączenie konwertera USB, UART/RS-485 na podłączonym urządzeniu, ekspander sieciowy, HDMI, fizyczny dotyk i skróty VT, odłączenie zasilania podczas aktualizacji, dostarczenie e-maila przez docelowy hosting. Sam emulator, wirtualny Wayland i test przeglądarkowy nie potwierdzają tych przypadków.
