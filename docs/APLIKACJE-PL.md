# AV Control Imager i AV Control Player 1.6.6

Dwie niezależne aplikacje na Windows 10 22H2 / Windows 11 x64. Każda ma własny instalator i skrót. Studio nie musi być zainstalowane ani uruchomione. Wymagany .NET jest dołączony, a instalatory zawierają również instalator środowiska WebView2 firmy Microsoft. Po instalacji aplikacje działają w sieci lokalnej, bez chmury.

## AV Control Imager — karta SD dla RPi 3B, 4B i 5

Instalator **AV-Control-Imager-1.6.6-Windows-x64.exe** zawiera obraz Raspberry Pi OS Lite 64-bit z silnikiem AV Control i oficjalny Raspberry Pi Imager 2.0.11.1. Nie trzeba pobierać obrazu osobno ani wybierać go z katalogu systemów. Wszystkie trzy modele korzystają ze wspólnego obrazu ARM64. Model wybierasz w aplikacji.

1. Zainstaluj Imager w chronionym katalogu Program Files. Windows poprosi o uprawnienia administratora podczas instalacji i zapisu karty SD. Zapewnij około 2 GB wolnego miejsca na instalację; konfigurator zapisuje skompresowany obraz bez tworzenia pełnej kopii na PC.
2. Podłącz czytnik z kartą SD (minimum 8 GB; zalecane 16 GB lub więcej).
3. Otwórz **AV Control Imager**, wybierz **RPi 3B**, **RPi 4B** albo **RPi 5** i odśwież listę kart. Wybierz właściwy dysk według nazwy, pojemności i liter woluminów.
4. Ustaw nazwę kontrolera, hasło administratora AV Control (minimum 12 znaków) i konto systemowe RPi. Domyślnie oba konta mają podane hasło; możesz ustawić oddzielne hasło systemowe. Konta aplikacji i systemu są niezależne.
5. Ethernet działa z DHCP. Jeśli potrzebujesz Wi-Fi, zaznacz opcję, wpisz SSID, hasło WPA2/WPA3 i kod kraju, np. PL. RPi 3B korzysta z Wi-Fi 2,4 GHz; wybierz odpowiednią sieć. SSH jest opcjonalny i domyślnie wyłączony.
6. Dodatkowe nazwy/IP certyfikatu wpisz, jeżeli panel ma łączyć się przez adres inny niż nazwa kontrolera lub jego nazwa `.local`. Adres certyfikatu nie ustawia stałego adresu IP. Stały adres można zapewnić rezerwacją DHCP w routerze.
7. Kliknij **Przygotuj zapis karty**. Sprawdź model, nazwę, pojemność, numer seryjny i woluminy. Wpisz wyświetlony tekst `WYMAŻ numer` i kliknij **Wymaż i zapisz kartę SD**. Osobne okno Windows pokaże ostateczne potwierdzenie. Ta operacja usuwa wszystkie dane z wybranego nośnika.
8. Zatwierdź uprawnienia administratora Windows dla zapisu. Obraz i program zapisujący zostaną sprawdzone przez SHA256. Następnie karta zostanie zapisana, odczytana w celu weryfikacji i wysunięta. Poczekaj na komunikat **Karta jest gotowa**.
9. Włóż kartę do wybranego RPi, podłącz sieć i zasilanie. Pierwszy start konfiguruje konto systemowe, sieć, konto aplikacji i certyfikat HTTPS. Silnik uruchamia się sam i pozostaje aktywny po zamknięciu aplikacji PC.
10. Dane parowania znajdziesz na partycji boot w **AV-Control-parowanie.txt**. Możesz odczytać je z konsoli RPi lub przez SSH: `cat /boot/firmware/AV-Control-parowanie.txt`. Alternatywnie poprawnie wyłącz RPi i odczytaj kartę na PC. Plik zawiera adres, login `admin` i odcisk certyfikatu SHA256; hasła nie zawiera.

Konfigurator pomija dysk systemowy, dysk aplikacji/obrazu, dyski z plikiem wymiany oraz wewnętrzne dyski SATA/NVMe. Dopuszcza dostępne nośniki USB/SD/MMC o odpowiedniej pojemności. Numer, identyfikator, numer seryjny, pojemność i ścieżka urządzenia są sprawdzane ponownie tuż przed zapisem. Lista może zawierać także zewnętrzne dyski USB — sprawdzaj wskazaną kartę przed zatwierdzeniem.

**Anulowanie:** przycisk Anuluj zatrzymuje przygotowanie lub zapis. Anulowana albo odłączona w trakcie karta wymaga ponownego przygotowania. Nie wyjmuj karty, gdy trwa zapis lub weryfikacja. Zamknięcie aplikacji podczas pracy wymaga anulowania, a następnie zakończenia procesu zapisującego.

Hasła nie są zapisywane w projektach ani w argumentach procesu. Zadanie zapisu jest szyfrowane przez DPAPI użytkownika Windows; tymczasowe pliki konfiguracji mają ograniczone uprawnienia i są usuwane po zakończeniu zadania. Na karcie i w pamięci podręcznej cloud-init dane pierwszego uruchomienia są usuwane po udanej konfiguracji. Ustawienia Wi-Fi pozostają w pliku NetworkManager dostępnym dla administratora RPi. UAC powinien podnosić uprawnienia tego samego użytkownika Windows; przy użyciu danych innego administratora uruchom Imager od razu na jego koncie.

## AV Control Player — samodzielny panel operatora

Instalator **AV-Control-Player-1.6.6-Windows-x64.exe** zawiera tylko odtwarzacz i jego środowisko. Nie uruchamia własnego symulatora ani silnika logiki. Sterowanie wykonuje kontroler RPi lub istniejący symulator Studio.

1. W Studio przygotuj projekt i opublikuj go na kontrolerze. W ustawieniach kontrolera utwórz konto z rolą **operator**.
2. Zainstaluj i uruchom **AV Control Player** na komputerze operatora.
3. Dodaj nazwę instalacji, adres HTTPS (np. `https://sala.local:8443`) i odcisk SHA256 z danych parowania. Program sprawdza odcisk, zgodność nazwy i ważność certyfikatu. Nie musisz importować CA do Windows na potrzeby natywnego odtwarzacza.
4. Kliknij **Połącz z kontrolerem**, następnie zaloguj się kontem operatora. Można zalogować się kontem administratora, ale odtwarzacz nadal pokazuje wyłącznie panel i blokuje funkcje edycji/publikowania.
5. Obsługuj strony, przyciski, suwaki i pozostałe elementy skonfigurowane w Studio. Panel pochodzi z aktywnego projektu na kontrolerze; aktualizacja projektu jest pobierana automatycznie.
6. **Pełny ekran** lub **F11** przełącza widok. **Esc** opuszcza pełny ekran.
7. Przycisk **Kontrolery** pozwala przełączać zapisane instalacje i usuwać połączenia. Ostatni kontroler jest otwierany automatycznie przy następnym uruchomieniu. Nazwa użytkownika w górnym pasku służy do wylogowania.

Odtwarzacz korzysta z tego samego renderera co Studio i panel przeglądarkowy. Uwzględnia warianty PC/tablet/telefon i wiązania projektu. Interlocki, role, bieżąca wersja i identyfikatory żądań są nadal sprawdzane przez silnik. Po utracie połączenia elementy sterujące znikają, pojawia się komunikat, a połączenie jest ponawiane. Polecenia nie są kolejkowane do późniejszego odtworzenia. Przycisk chwilowy ma dzierżawę odnawianą w czasie przytrzymania; po zerwaniu połączenia silnik zwalnia go po maksymalnie około 2 sekundach.

Połączenia i tokeny sesji są przechowywane oddzielnie od Studio, zaszyfrowane DPAPI dla użytkownika Windows. Sesja kontrolera wygasa po 12 godzinach; wtedy zaloguj się ponownie. Wylogowanie usuwa token sesji. Usunięcie zapisanego połączenia usuwa jego lokalne dane.

Do testów z uruchomionym lokalnym symulatorem dopuszczony jest adres `http://127.0.0.1:port` (wyłącznie numeryczny adres pętli lokalnej). Hasło symulatora: `simulation`, login `admin`. Odtwarzacz nie uruchamia Studio — symulator musi już działać.

## Co potwierdzono

Szczegółowe dowody i granice testów są w **WERYFIKACJA-1.3.0.md**. Nowy czysty obraz ma włączony UART GPIO14/15 i usuniętą konsolę szeregową, z konfiguracją dla 3B/4B/5. Konfiguracja firmware oraz próby ARM64/pliku zapisu są oddzielone od rozruchu nowej fizycznej karty. Na fizycznej 4B sprawdzono silnik i WWW, ustawienia sieci z potwierdzeniem/powrotem oraz otwarcie UART i funkcje TXD0/RXD0. Nie wykonano transmisji elektrycznej ani prób fizycznej 3B/5. Własne aplikacje i instalatory nie mają podpisu Authenticode; dołączone programy producentów mają zweryfikowane podpisy.

Źródła mechanizmu zapisu i konfiguracji: [Raspberry Pi Imager CLI 2.0.11.1](https://github.com/raspberrypi/rpi-imager/blob/v2.0.11.1/src/cli.cpp), [konfiguracja obrazu i weryfikacja](https://github.com/raspberrypi/rpi-imager/blob/v2.0.11.1/src/downloadthread.cpp), [formaty konfiguracji OS](https://github.com/raspberrypi/rpi-imager/blob/v2.0.11.1/doc/os_customisation_formats.md). To samo narzędzie producenta jest używane w instalatorze projektu Guido; komendy sterowania z Guido nie zostały przeniesione.
