# Weryfikacja AV Control 1.6.8

Raport dotyczy gotowych paczek 1.6.8 i firmware TAB5 0.3.0. Identyfikator źródeł produktu: `95909b7dc6bd29c6bc8a2065ed0290c05b7cac6a8ad4c3649da16dd6c0d97955` (377 plików). Dowody testów i sumy gotowych plików są związane z tym identyfikatorem.

## Przejścia i szkolenie

Sprawdzono fade, wipe, wash, slide i zoom: osiem scenariuszy Chrome oraz po pięć efektów w gotowych Windows Player, Windows Studio, zainstalowanym skompilowanym Linux Playerze GTK/WebKit i kiosku GTK/WebKit na wirtualnym wyjściu Wayland. Próby obejmują klatki pośrednie, blokadę kontrolek na czas ruchu, sprzątanie warstw, szybką zmianę strony, ekran telefonu, ograniczenie ruchu i zmianę rozmiaru. Nawigacja nie powtórzyła poleceń sterujących.

Compositor RGB565 sprawdzono z ASAN/UBSAN: 1100 klatek, pięć efektów, cztery kierunki i pięć rozmiarów do 1280 × 720. Wynik po optymalizacji jest identyczny piksel w piksel z bazową implementacją. To dowód programu; stabilność fizycznego skanowania wyświetlacza wymaga osobnego odbioru.

Pięć istniejących stron Wirtualnej sali AV demonstruje efekty po 520 ms. Program szkolenia, ćwiczenie w Studio i [instrukcja przejść](PRZEJSCIA-STRON-PL.md) opisują ich konfigurację i podgląd. Główny PDF pozostaje w sprawdzonej edycji z 18 października: 217 stron i 83 ilustracje. Jego treść oraz Markdown porównano bajtowo w trzech aplikacjach Windows, paczce ARM i obrazie RPi.

## Gotowe pakiety

Studio i Player przeszły rzeczywistą instalację, natywne próby interfejsu i odinstalowanie. Imager przeszedł instalację w chronionym Program Files i natywne testy z przypiętym obrazem; pozostał zainstalowany. Test nie zapisywał fizycznej karty SD. Studio użyło dołączonego CPython 3.13.15 i lokalnego wheel NumPy 2.5.3 z importem własnego modułu i ponownym zatwierdzeniem zmienionego kodu.

Skompilowany Linux Player .deb zainstalowano i uruchomiono jako nieuprzywilejowany użytkownik. Pliki archiwum przenośnego porównano z instalacją. Agent 1.1.1 przeszedł 47 regresji na rzeczywistej paczce bytecode. Pakiet ARM64 uruchomiono pod QEMU z dołączonym CPython 3.13; sprawdzono aktualizację, zachowanie danych, cofnięcie ręczne i cofnięcie po nieudanym sprawdzeniu startu. To nie jest próba nowej karty na fizycznym RPi 3B/5.

## Fizyczny TAB5

Firmware 0.3.0 zawiera wspólnie uzgodnione poprawki OTA, profil ESP-IDF dla ESP32-P4 sprzed rewizji 3, rollback i PSRAM XIP. Wymagane opcje konfiguracji oraz niezmieniony układ partycji sprawdzono przed pakowaniem.

Aktualizacja 0.2.13 → 0.3.0 przez istniejący panel WWW zakończyła się potwierdzeniem 100%. USB potwierdziło 0.3.0, połączenie z kontrolerem, wykonany boot-check i brak oczekującej weryfikacji. Manifest pięciu stron i biblioteka sześciu paneli pozostały identyczne. Właściciel zgłosił brak błysków podczas tej aktualizacji. Fizyczny dotyk i odbiór animowanego HMI są odrębnymi próbami; tego raportu pakowania nie należy traktować jako ich potwierdzenia.

## Publikacja i granice

Publikator wymaga siedmiu udanych zadań CI na dokładnym końcowym commicie, lokalnych runnerów, powyższych dowodów paczek oraz podpisu ECDSA P-256. Wynik CI, commit i sumy plików zapisuje podpisany RELEASE-MANIFEST.json. Instalacja kontrolera odbywa się z GitHub przez WWW → Ustawienia → Aktualizacje Raspberry Pi. Dla TAB5 trzeba ponownie wysłać panel zawierający ustawienia przejść.

Audyt wszystkich 25 poprawek z 1.6.7 jest zachowanym historycznym punktem odniesienia. Fizyczne urządzenia mobilne, nowy rozruch SD na 3B/5 i komunikacja elektryczna GPIO/UART/RS485 nie były częścią prób tego wydania. Instalatory produktu nie mają podpisu Authenticode; podpis wydania jest weryfikowany oddzielnie.
