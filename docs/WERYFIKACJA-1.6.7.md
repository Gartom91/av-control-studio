# Weryfikacja AV Control 1.6.7

Stan dowodów: **18 października 2026**. Wersja aplikacji: **1.6.7**; firmware M5Stack TAB5 ST7123: **0.2.5**. Raport opisuje wykonane testy oprogramowania i pakietów oraz potwierdzoną publikację wydania. Nie poświadcza odbioru nowej wersji na fizycznym Raspberry Pi ani TAB5.

## Tożsamość sprawdzonego oprogramowania

Pakiety i [kontrola ich zgodności](evidence/package-verification-1.6.7.json) wskazują ten sam zestaw **366 plików wejściowych produktu**, o skrócie `sourceSha256`:

```text
59ebee5d3de8491bcd42079b590604865afbdd1307c8219f79f01adca50ee710
```

Ten skrót identyfikuje wejścia budowania, a nie commit Git ani wszystkie pliki dokumentacji. Kontrola pakietów porównuje rzeczywiste sumy **ośmiu głównych artefaktów i sześciu raportów odbioru**; TAB5 ma dodatkowe [potwierdzenie kompilacji](evidence/tab5-build-1.6.7.json) i [raport USB/OTA](evidence/tab5-1.6.7.json). [Końcowe CI](evidence/release-ci-1.6.7.json) potwierdza siedem zadań dla commitu `5e60c8438956137d91dd42b2fab7919bcf8b9ce8`. [Lokalnie sprawdzony podpisany manifest](evidence/release-signing-1.6.7.json) wiąże te wyniki z 49 plikami wydania.

Audyt bazowy obejmował commit `09ea0c199106b094843291a476de336e88255afe`. [Tabela 25 ustaleń i poprawek](AUDYT-NAPRAWY-1.6.7.md) zachowuje identyfikatory **R1–R9, UI-01–UI-09, P-01–P-04, S-01–S-03**. [Zbiorczy dowód regresji](evidence/audit-fixes-1.6.7.json) wiąże je z konkretnymi wykonanymi przypadkami; sama obecność testu w repozytorium nie jest wynikiem jego wykonania.

## Wykonane regresje

| Zakres | Wynik | Dowód i ograniczenia |
| --- | --- | --- |
| Pełna regresja Python na Windows | **588 zaliczonych, 29 pominiętych, 0 błędów** | Końcowy JUnit `regression-windows-final-1.6.7.xml` i zapis wykonania; zestawienie w [dowodzie regresji](evidence/audit-fixes-1.6.7.json). Dwa ostrzeżenia dotyczą przestarzałych metod w zależności pySerial. Pominięte przypadki nie są zaliczeniami. |
| Bezpieczeństwo certyfikatów, konfigurator i odzyskiwanie na Linux | **110 zaliczonych, 0 pominiętych** | `security-recovery-linux-1.6.7.xml`, uwzględniony w [dowodzie regresji](evidence/audit-fixes-1.6.7.json). Izolowane testy plików, API i procesów; bez produkcyjnej usługi RPi. |
| Portable C++ TAB5 | **6 zaliczonych, 0 pominiętych** | [Raport kompilacji](evidence/tab5-build-1.6.7.json). Kod hosta wykonuje nagłówki i wybrane rzeczywiste gałęzie firmware z atrapami peryferiów. |
| Regresje interfejsu związane z audytem | **21/21 zaliczonych** | [Wyniki Chromium](evidence/audit-browser-1.6.7.json): wielodotyk, klawiatura, blokady, odrzucenie poleceń, zakresy wartości, opóźniona publikacja, pliki i sesja kiosku. |
| Transakcja natywnego otwierania pliku | **PASS** | Rzeczywista klasa C# na plikach tymczasowych; uzupełniona pełną próbą Studio opisaną poniżej. |
| Wybrane testy frontendowe Vitest | **25 zaliczonych w 4 plikach** | Końcowe wykonanie `vitest-1.6.7.log`; osobny zestaw względem 21 scenariuszy Chromium. |

Nie sumuje się tych liczb jako liczby różnych przypadków: część testów wykonano na więcej niż jednej platformie. JUnit zapisuje tożsamość i wynik przypadków, ale nie zawiera samodzielnego dowodu pochodzenia z commitu. Archiwizacja i hashe raportów oraz porównanie wejść pakietów są dodatkowymi dowodami; [ostateczne CI dla dokładnego commitu](evidence/release-ci-1.6.7.json) zakończyło się osobnym wynikiem **PASS 7/7**.

## Windows: rzeczywiste aplikacje i instalacja

[Studio — instalacja i odinstalowanie](evidence/installation-1.6.7.json): **PASS**. Zainstalowany lokalny Runtime zgłaszał 1.6.7. Sprawdzono DPAPI, zmianę i przywrócenie nazwy właściciela oraz odrzucanie nieprawidłowego pinu, hosta i wygasłego certyfikatu. Test wykonano na maszynie z WebView2; nie jest to próba świeżego Windows bez tego komponentu.

[Studio — .NET 10/WebView2](evidence/native-studio-1.6.7.json): **PASS**. Próby obejmują silnik dostarczony w pakiecie, otwarcie projektu argumentem startowym i oczekiwanie na jego walidację, logikę i Python, trwałość IndexedDB po restarcie, zachowanie zmian przy natychmiastowym zamknięciu, elementy paneli oraz podręcznik offline. Nie wykonywano w tej próbie sprawdzenia aktualnego publicznego wydania GitHub.

[Pełny Python w natywnym Studio](evidence/python-native-windows-1.6.7.json): **PASS**. W czystym katalogu danych zainstalowano offline wheel NumPy **2.5.3** dla dostarczonego SDK **3.13.15**, wykonano import pomocnika i obliczenia oraz potwierdzono unieważnienie zaufania po zmianie kodu. Brak błędów JavaScript. To zatwierdzony CPython z uprawnieniami procesu, nie sandbox systemowy.

[Player i Imager — instalacja oraz próby natywne](evidence/companions-installation-1.6.7.json): **PASS**. Player przeszedł instalację, próby sterowania, pełnego ekranu, rozłączenia i braku odtwarzania poleceń po powrocie sieci, a następnie odinstalowanie. Ten przebieg używał konta administratora ograniczonego do paneli (`operator: false`); osobną próbę operatora wykazuje Player Linux. Imager przeszedł instalację, sprawdzenie obrazu offline, wyliczania i ochrony nośników oraz odrzucenia niepotwierdzonego zapisu. Pozostawiono go zainstalowanego. **Nie wywołano zapisu fizycznego dysku ani karty SD**; wybór poprawnego nośnika w trybie read-only nie był osobno zaliczony (`readOnlyPlanTested: false`).

## Linux, ARM64 i obraz RPi

[Pakiety Linux](evidence/linux-packages-1.6.7.json) i [natywny Player GTK/WebKit](evidence/linux-player-1.6.7.json): **PASS**. Zainstalowana paczka `.deb` i archiwum przenośne mają zgodne pliki i skrót wejść budowania. Próba jako nieuprzywilejowany użytkownik obejmuje rzeczywistą kontrolę TLS, logowanie operatora, akcję panelu, pełny ekran, blokadę edytora, utratę sieci i ponowne uruchomienie. Okno działało w lokalnym środowisku Linux z wirtualnym wyjściem; nie poświadcza fizycznego pulpitu Linux.

[Runtime ARM64](evidence/arm-1.6.7.json): **PASS w QEMU user** na systemie plików przygotowanego obrazu. Sprawdzono rzeczywiste procesy aarch64, SQLite i zachowanie pamięci po restarcie procesu, wdrożenie i akcję API, Python, wygląd panelu, ekspandery i zależności ARM. `fullKernelBoot: false` oraz `physicalHardware: false` — nie uruchomiono całego jądra ani fizycznego RPi.

[Aktualizacja 1.5.3 → 1.6.7 i rollback](evidence/update-arm-1.6.7.json): **PASS** dla pakietu Runtime o SHA256 `5ef2be5120fb5fb6d0f459ce70eeed631234935e82196a343d8b2e4f1a36d0c4`. Zachowano użytkownika, sesję, certyfikat, klucz i pamięć SQLite; sprawdzono ręczny rollback i rollback po błędzie zdrowia. Test używał QEMU, zwykłych plików obrazu i kontrolowanych metadanych GitHub. Nie wykonywał systemd ani fizycznego zaniku zasilania.

[UART czystego obrazu](evidence/uart-clean-image-1.6.7.json) oraz [zawartość obrazu kiosku](evidence/hdmi-1.6.7/image.json): **PASS w zakresie konfiguracji i pakietów**. Sprawdzono ustawienia dla RPi 3B/4B/5, brak konsoli szeregowej, czysty stan użytkownika, składniki ARM, konto kiosku i brak zaszytych poświadczeń. Nie jest to pomiar elektryczny GPIO/UART ani rozruch nowej karty.

[Agent 1.1.1](evidence/agent-package-1.6.7.json): **47 testów zaliczonych**, kontrola skompilowanego archiwum i 14 sum plików. Nie rejestrowano Agenta w rzeczywistej usłudze zewnętrznej i nie uruchamiano produkcyjnej usługi.

## HDMI i TAB5

[Natywny kiosk GTK/WebKit na wirtualnym Wayland](evidence/hdmi-1.6.7/kiosk-view.json): **PASS** dla logowania, klawiatury ekranowej, ograniczeń nawigacji, stron, odzyskania połączenia oraz restartu bez odtwarzania poleceń. Wirtualne wyjście nie zastępuje fizycznego monitora, USB ani przełączenia konsoli tty.

Firmware TAB5 **0.2.5** skompilowano lokalnie w PlatformIO: **SUCCESS**. [Raport budowania](evidence/tab5-build-1.6.7.json) zapisuje źródła, artefakty i dwa ostrzeżenia zależności. [Pakiet USB i aplikacja OTA](evidence/tab5-1.6.7.json) mają sprawdzone hashe; aplikacja OTA ma SHA256 `2ac507ecd4d566f5237d80f42e51ebac57835fe09e7f7a6717e5a055d4397a78`. **Nie wgrano i nie odebrano fizycznie tego firmware.** Testy przenośne obejmują kontrolki z samą akcją i ochronę konfiguracji, ale nie fizyczny USB provision, dotyk ani wygaśnięcie odblokowania podczas OTA.

Historyczny [odbiór HDMI](WERYFIKACJA-HDMI-2026-10-12.md) dotyczy 1.6.5 z poprawką, a [odbiór TAB5](WERYFIKACJA-TAB5.md) prototypowego firmware 0.2.3. Ich wyniki pozostają oznaczonymi dowodami historycznymi; nie nadają statusu fizycznego odbioru wersji 1.6.7/0.2.5.

## Obciążenie i podręcznik

Oba nowe pomiary Windows obejmują **100 urządzeń, 2000 bloków i 5 paneli**, bez błędów poleceń i z końcową zgodnością wszystkich paneli. [Scenariusz normalny](evidence/benchmark-windows-normal-1.6.7.json) miał p95 polecenia **199,3 ms**, a p95 skanu **24,0 ms**. [Serie 100 równoległych akcji](evidence/benchmark-windows-1.6.7.json) dały p95 polecenia **2181,3 ms**, a p95 skanu **21,8 ms**. To krótkie pomiary lokalnego Windows, nie deklaracja czasu rzeczywistego ani wydajności RPi; etykieta celu 50 akcji/s nie jest dowodem utrzymania takiej przepustowości przez cały przebieg.

Podręcznik z 18 października ma **217 stron, 55 rozdziałów, 4 dodatki i 83 ilustracje**. [Raport renderowania i kontroli](tutorial/workshop-verification.json) oraz [rejestr oględzin](tutorial/page-review.json) potwierdzają **217/217 stron** i sprawdzenie 99 lokalnych odnośników. Oględziny wcześniejszych renderów zachowano wyłącznie dla identycznych obrazów stron; zmienione strony mają osobne sprawdzenie. Końcowy PDF ma SHA256 `e85efa4a0c661b5a2caccc88d42e7c87ebd4b86eec175b9935a258b8e94ff898`.

[Integracja szkolenia](evidence/training-1.6.7.json) i [zgodność podręcznika w pakietach](evidence/packaged-handbook-1.6.7.json): **PASS**. Sprawdzono wszystkie 83 ilustracje i identyczny PDF/Markdown w trzech aplikacjach Windows, aktualizacji ARM i obrazie RPi. Wszystkie **80 zrzutów ekranu są jawnie historyczne**, z 11–12 października; nowa rewizja tekstu nie zmienia ich pochodzenia.

## CI dla ostatecznego commitu

[Przebieg 39145061336](https://github.com/Gartom91/av-control-studio-source/actions/runs/39145061336) zakończył się **SUCCESS: 7/7 zadań** dla commitu `5e60c8438956137d91dd42b2fab7919bcf8b9ce8`. [Publiczny zapis wyników](evidence/release-ci-1.6.7.json) zawiera identyfikatory zadań, daty, nazwy runnerów i ich etykiety. Wszystkie zadania wykonano na lokalnych runnerach `self-hosted`/`av-control-local`; nazwy macierzy `ubuntu-latest` i `windows-latest` nie oznaczają tu maszyn hostowanych przez GitHub.

Pełna regresja CI: **Windows 588 zaliczonych / 29 pominiętych**, **Linux 611 zaliczonych / 6 pominiętych** oraz **4 zaliczone izolowane próby root bootstrap na Linux**. Siedem zaliczonych zadań to `windows-package`, `runtime (ubuntu-latest)`, `kiosk`, `runtime (windows-latest)`, `tab5`, `interface` i `linux-player`.

Pierwsza próba `windows-package` zakończyła się błędem ładowania `_cffi_backend` spowodowanym ograniczeniem długości ścieżki Windows w katalogu runnera. Ponowienie tego samego commitu w krótszym katalogu zakończyło się powodzeniem; nie zmieniono kodu produktu.

## Stan końcowych bram wydania

Lokalne testy, opisane pakiety, końcowe CI, podpis oraz publikacja kompletu 49 plików są sprawdzone. Osobne dowody potwierdzają wszystkie publiczne pobrania i próby sprawdzania aktualizacji:

| Etap | Stan w tym raporcie | Dowód i zakres |
| --- | --- | --- |
| Ostateczny commit źródeł i siedem zadań CI | **PASS 7/7** | [Dowód CI](evidence/release-ci-1.6.7.json): commit `5e60c8438956137d91dd42b2fab7919bcf8b9ce8`, siedem wyników `success`, daty oraz lokalne runnery. |
| Podpis i kontrola kompletnego zestawu | **PASS, 49 plików** | [Dowód sprawdzenia podpisu ECDSA i skróty metadanych](evidence/release-signing-1.6.7.json). Opublikowane: [manifest](https://github.com/Gartom91/av-control-studio/releases/download/v1.6.7/RELEASE-MANIFEST.json), [podpis](https://github.com/Gartom91/av-control-studio/releases/download/v1.6.7/RELEASE-SIGNATURE.json), [sumy plików](https://github.com/Gartom91/av-control-studio/releases/download/v1.6.7/SHA256SUMS.txt). |
| Publikacja v1.6.7 | **PASS** | [Dowód publikacji](evidence/publication-1.6.7.json): 49 załączników, 66 sprawdzonych odnośników README. [Pobrania publiczne](evidence/public-downloads-1.6.7.json): **49/49 anonimowych GET**, zgodne SHA256 i liczby bajtów, poprawny pobrany podpis i sumy kontrolne. |
| Sprawdzanie aktualizacji w aplikacjach Windows | **PASS 6/6** | [Próby natywnego updateCheck](evidence/publication-1.6.7.json): Studio, Player i Imager 1.6.6 wykrywają 1.6.7; wersja 1.6.7 zwraca `idle` i brak nowszej wersji. Bez wywołania pobierania i instalacji aktualizacji. |
| Fizyczny odbiór instalacji | **NIEZWERYFIKOWANE** | Osobny raport dla wskazanego urządzenia i rzeczywistych hashy wdrożonych artefaktów. |

[Wydanie v1.6.7](https://github.com/Gartom91/av-control-studio/releases/tag/v1.6.7) opublikowano **18 października 2026 o 16:49:29 UTC**. Weryfikacja anonimowych pobrań zakończyła się o **16:52:03 UTC**; objęła treść wszystkich 49 załączników, a nie tylko odpowiedzi HEAD. Podpis sprawdzono ponownie na dokładnych pobranych bajtach manifestu i podpisu. Próby `updateCheck` korzystały z rzeczywistego publicznego GitHub w natywnych oknach WebView2.

## Granice akceptacji

Brak nowej fizycznej aktualizacji RPi, rozruchu SD, potwierdzenia HDMI i dotyku USB, pomiarów UART/RS232/RS485/GPIO, próby zakupionych konwerterów, RPi 3B/5 oraz fizycznego telefonu/tabletu. Symulowane przerwania operacji plikowych nie dowodzą odporności konkretnej karty na rzeczywistą utratę zasilania. Nie wykonywano drugiego pełnego niezależnego audytu bezpieczeństwa ani nowego wdrożenia hostingu czy rzeczywistej poczty.

Instalatory AV Control nie mają własnego podpisu Authenticode. Podpis manifestu ECDSA identyfikuje wydanie i pliki, ale nie jest podpisem wydawcy instalatora. Testy funkcjonalne, ograniczony przegląd poprawek, lokalne pakiety, CI, publikacja i fizyczny odbiór są odrębnymi warstwami dowodów.
