# Pierwsze uruchomienie AV Control na Raspberry Pi

**[Polski](PIERWSZE-URUCHOMIENIE-PL.md) · [English](FIRST-RUN-EN.md)**

Ta procedura dotyczy nowej karty przygotowanej w **AV Control Imager** dla RPi **3B, 4B lub 5**. Aktualizacja działającego kontrolera odbywa się przez Runtime i nie wymaga wymazywania karty. Pełny kurs pozostaje w jednym podręczniku: rozdziały 23–27 opisują Imager, konfigurację, publikowanie, Player i aktualizacje.

## 1. Przygotuj kartę w Imagerze

1. Pobierz instalator Imagera z **Assets** [aktualnego wydania](https://github.com/Gartom91/av-control-studio/releases/latest). Obraz AV Control i narzędzie zapisu są dołączone. Zainstaluj także Studio, jeżeli będziesz tworzyć projekt.
2. Podłącz czytnik z kartą SD. Minimum to 8 GB; do pracy zalecamy 16 GB lub więcej. Zachowaj kopię dotychczasowych danych karty.
3. Wybierz model **3B / 4B / 5** i właściwy nośnik, sprawdzając jego numer, pojemność i woluminy.
4. Ustaw **Nazwę kontrolera**. Domyślna to `av-control`. Dla kilku kontrolerów użyj różnych nazw, np. `sala-a` i `sala-b`. Nazwa zawiera małe litery, cyfry i myślniki, maksymalnie 63 znaki.
5. Wpisz własne hasło administratora AV Control, co najmniej 12 znaków. Nie ma fabrycznego hasła administratora kontrolera.
6. Ustaw konto systemowe Linux: domyślny login to `avoperator`. Imager domyślnie proponuje to samo podane hasło dla obu kont; możesz ustawić oddzielne hasło systemowe. **To dwa niezależne konta**. SSH jest opcjonalny i domyślnie wyłączony.
7. Ethernet otrzymuje adres przez DHCP. Jeżeli potrzebujesz Wi-Fi, zaznacz konfigurację, wpisz SSID, hasło WPA2/WPA3 i kraj, np. `PL`. RPi 3B wymaga sieci 2,4 GHz.
8. Jeżeli planujesz dostęp przez stałe IP, ustaw rezerwację DHCP w routerze i wpisz to IP w **Dodatkowe adresy certyfikatu**. To pole dodaje adres do certyfikatu; samo nie ustawia adresu sieciowego.
9. **Dołączenie do TechnikAV** jest opcjonalne i domyślnie wyłączone. Nie jest potrzebne do lokalnego sterowania. Po jego wybraniu konieczna jest późniejsza akceptacja kontrolera na własnym koncie TECHNIKAV.
10. Kliknij **Przygotuj zapis karty**, sprawdź podsumowanie i wpisz wymagane `WYMAŻ numer`. Wybierz **Wymaż i zapisz kartę SD**, potwierdź właściwy nośnik oraz monit administratora Windows. Zapis usuwa wszystkie dane z tego nośnika.
11. Poczekaj na zapis, odczyt weryfikacyjny i komunikat **Karta jest gotowa**. Nie wyjmuj karty w trakcie operacji.

## 2. Uruchom kontroler i znajdź jego adres

Włóż kartę do Raspberry Pi. Podłącz Ethernet, jeśli go używasz, oraz odpowiednie zasilanie. Pierwszy start konfiguruje konto systemowe, sieć, administratora aplikacji i certyfikat HTTPS. Zaczekaj na ukończenie konfiguracji; dane parowania powstają dopiero po tym etapie.

| Ustawienie w Imagerze | Adres interfejsu |
| --- | --- |
| Domyślna nazwa `av-control` | **https://av-control.local:8443/** |
| Własna nazwa `sala-a` | **https://sala-a.local:8443/** |
| Znane IP, np. `192.168.1.50`, dodane do certyfikatu | **https://192.168.1.50:8443/** |

Port **8443** i protokół **HTTPS** są wymagane. Nowa instalacja nie ma uniwersalnego stałego IP. `192.168.1.23` jest adresem jednej konkretnej instalacji testowej, a nie domyślnym adresem obrazu.

Nazwa `.local` działa w sieci lokalnej przez mDNS. Komputer i RPi muszą mieć łączność w tej samej sieci; sieć gościnna, izolacja klientów lub oddzielne VLAN-y mogą blokować rozpoznawanie i połączenie. Jeżeli nazwa nie działa, znajdź kontroler w liście urządzeń / dzierżaw DHCP routera. Szukaj nazwy wybranej w Imagerze i odczytaj IP. Dostęp przez to IP nadal wymaga zgodności certyfikatu; nie wyłączaj jego weryfikacji.

## 3. Odczytaj parowanie i zaufaj właściwemu certyfikatowi

Po udanym pierwszym starcie na partycji boot są:

- **`AV-Control-parowanie.txt`** — rzeczywisty adres, login `admin` i odcisk SHA256 certyfikatu serwera; bez hasła.
- **`AV-Control-CA.crt`** — publiczny certyfikat CA do zaufania w przeglądarce.

Odczytaj je przez konsolę / wcześniej włączone SSH albo poprawnie wyłącz RPi i włóż kartę do czytnika PC. Nie wyjmuj karty z pracującego kontrolera. Dla skonfigurowanego SSH możesz użyć konta systemowego, np. `avoperator`, i odczytać:

```sh
cat /boot/firmware/AV-Control-parowanie.txt
```

**Studio / Player:** wpisz adres HTTPS i dokładny odcisk SHA256 z pliku parowania. Aplikacje sprawdzają odcisk, nazwę i ważność certyfikatu. Nie wymagają importu CA do Windows do własnego połączenia.

**Przeglądarka:** dodaj publiczny `AV-Control-CA.crt` z własnej karty do zaufanych urzędów certyfikacji urządzenia / przeglądarki. W Windows można otworzyć plik, wybrać instalację certyfikatu dla bieżącego użytkownika i magazyn **Zaufane główne urzędy certyfikacji**; przeglądarka z osobnym magazynem wymaga importu również tam. Zaufanie CA dotyczy certyfikatów, które ten CA wystawi — importuj wyłącznie plik z własnego kontrolera. Uruchom ponownie przeglądarkę i otwórz nazwę z pliku parowania. Prywatnych plików `.key` nie eksportuj.

Błąd HTTPS przez IP zwykle oznacza, że IP nie jest wpisane do certyfikatu. Użyj właściwej nazwy `.local` lub skonfiguruj właściwe nazwy/IP. Nie traktuj pominięcia ostrzeżenia jako zakończenia parowania. Sprawdź też datę komputera i RPi; w instalacji offline ustaw poprawny czas.

## 4. Zaloguj się i sprawdź konfigurację

Otwórz adres kontrolera i zaloguj się do AV Control jako **`admin`**, hasłem ustawionym w Imagerze. Login **`avoperator`** służy Linuxowi / SSH i nie jest domyślnym kontem WWW. Dane `admin` / `simulation` należą wyłącznie do lokalnego symulatora Studio i nie działają jako fabryczne konto Raspberry Pi.

W **Ustawienia → Konfiguracja Raspberry Pi** sprawdź model, nazwę, adresy, czas, temperaturę, miejsce na dysku i interfejsy sieciowe. UART jest domyślnie włączony w nowym obrazie, bez konsoli szeregowej. Wybór urządzenia i jego protokołu wykonujesz później w projekcie. Dodatkowy USB–Ethernet konfiguruj tu jako osobny interfejs, najlepiej według MAC.

Zmiana nazwy kontrolera odnawia certyfikat serwera. Zaktualizuj adres i odcisk w Studio / Player. Konfigurator pokazuje nowy odcisk i umożliwia pobranie publicznego CA. Zmiany sieci wymagają potwierdzenia po odzyskaniu połączenia; zastosuj instrukcję widoczną w konfiguratorze, aby uniknąć automatycznego powrotu ustawień.

## 5. Połącz Studio i opublikuj pierwszy projekt

1. W Studio wybierz połączenie z kontrolerem zamiast lokalnego symulatora. Wpisz nazwę instalacji, **Adres HTTPS kontrolera** i **Odcisk SHA256 certyfikatu z RPi**, następnie login `admin` i własne hasło.
2. Utwórz projekt lub otwórz neutralny przykład szkoleniowy. Przykład ma wyłączone transporty fizyczne. Dopasuj porty, adresy i protokoły przed ich włączeniem.
3. Dodaj strony i powiązania panelu. Sprawdź walidację i działanie w symulatorze.
4. Upewnij się, że Studio jest połączone z właściwą RPi. Opublikuj projekt: walidacja, przygotowanie wersji i jej aktywacja. Zapis lokalny projektu sam nie publikuje go na kontrolerze.
5. Otwórz **Panel operatora** w interfejsie WWW lub połącz oddzielny Player adresem i odciskiem. Panel pokazuje aktywny projekt na RPi. Po zamknięciu Studio silnik nadal pracuje.

Na nowej karcie nie ma Twojego opublikowanego projektu. Widok oczekiwania na panel jest prawidłowy, dopóki pierwszy projekt nie zostanie aktywowany.

## 6. Użytkownicy, logowanie i panel HDMI

Administrator tworzy osobne konto operatora w **Ustawieniach → użytkownicy**. Operator może zmienić własne hasło; administrator zarządza kontami i ich hasłami. [Instrukcja kont i klawiatury](KONTA-I-LOGOWANIE-PL.md).

Panel wymaga logowania. Opcja **Loguj automatycznie na tym urządzeniu (30 dni)** jest domyślnie wyłączona i dotyczy danego stanowiska. **Wyloguj z panelu** usuwa jego zapamiętaną sesję. Klawiatura ekranowa jest domyślnie ukryta na PC i w przeglądarce; można ją włączyć w ustawieniach wprowadzania tekstu na ekranie logowania, w „Moje konto” lub w Ustawieniach. Na lokalnym panelu HDMI jest domyślnie włączona. Wysuwa się od dołu po wybraniu pola; Shift i Alt udostępniają dodatkowe znaki. Fizyczna klawiatura działa normalnie.

Do panelu lokalnego podłącz monitor HDMI i mysz, touchpad lub dotyk USB. W 3B jest HDMI, w 4B / 5 micro HDMI. Dotyk zwykle wymaga osobnego USB — samo HDMI przenosi obraz. Nowy obraz domyślnie uruchamia kiosk po wykryciu monitora; wyświetla logowanie, a następnie aktywny panel, bez edytora i pulpitu. Bez projektu pokazuje oczekiwanie. Ustawienia i stronę początkową wybierasz w **Konfiguracja Raspberry Pi → Panel lokalny HDMI**. Z klawiatury **Ctrl+Alt+F2** otwiera konsolę logowania tty2, **Ctrl+Alt+F1** wraca do kiosku. [Pełna instrukcja HDMI](PANEL-HDMI-PL.md).

## 7. Aktualizacje i opcjonalny monitoring

Codzienna praca jest lokalna. Sprawdzanie aktualizacji GitHub i raporty do hostingu wymagają internetu i konfiguracji. W Ustawieniach skonfiguruj politykę aktualizacji Runtime oraz osobno aktualizacje aplikacji Windows. Aktualizacja Runtime zachowuje projekt i dane; Imager służy do nowej karty i ją wymazuje.

Jeżeli wybrano dołączenie do TECHNIKAV, zaloguj się na swoje konto **technikav.pl**, wybierz AV Control, porównaj identyfikator z lokalnym kontrolerem i zaakceptuj instalację. To konto jest odrębne od lokalnego `admin` i systemowego `avoperator`. Hosting odbiera raporty; e-mail wymaga osobnej konfiguracji odbiorców i harmonogramu hostingu. Samo wpisanie danych projektu nie włącza e-maili.

## 8. Gdy pierwszy start nie działa

| Objaw | Co sprawdzić |
| --- | --- |
| `.local` nie odpowiada | Zasilanie, przewód / SSID, lista DHCP routera, tę samą sieć i brak izolacji klientów; właściwą nazwę z Imagera |
| Brak połączenia HTTPS | Dokładny protokół HTTPS i port 8443; ukończenie pierwszej konfiguracji; usługi `avcontrol-setup.service` i `avcontrol.service` przez konsolę / SSH |
| Brak plików parowania | Czy pierwszy start ukończył konfigurację; log `journalctl -u avcontrol-setup.service -b`; nie szukaj plików na karcie przed pierwszym uruchomieniem |
| Certyfikat odrzucony | CA z właściwego kontrolera, adres objęty certyfikatem, aktualny odcisk, poprawną datę obu urządzeń |
| Hasło odrzucone | WWW: `admin` i hasło Imagera; SSH: konto systemowe; symulator ma odrębne dane |
| Monitor pokazuje oczekiwanie | Czy projekt opublikowano i aktywowano; czy zawiera strony panelu |
| Brak dotyku | Osobny przewód USB, urządzenie HID rozpoznane przez Linux, sterownik / kalibrację producenta |

Nie przesyłaj haseł, prywatnych kluczy ani zapisanych sesji w zgłoszeniu. Podaj model, wersję, wybraną nazwę, etap zatrzymania i komunikat błędu.

**Granica weryfikacji:** procedurę sprawdzono względem implementacji Imagera, pierwszej konfiguracji, parowania i kiosku. Testy pakietów / emulacja nie zastępują rozruchu nowej fizycznej karty ani prób HDMI, dotyku i portów na każdym z trzech modeli. Aktualne wykonane próby i ich ograniczenia opisuje raport konkretnego wydania.
