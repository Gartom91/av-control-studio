# Naprawa pasów na ekranie HDMI — 12.10.2026

## Objaw i ustalona przyczyna

Na rzeczywistej Raspberry Pi 4 Model B Rev 1.4 ekran logowania kiosku
wyświetlał poziome pasy zamiast tekstu i pól formularza. Zrzut z działającego
kompozytora Cage zawierał te same uszkodzenia co zdjęcie monitora. Uszkodzenie
powstawało więc już podczas rysowania widoku.

Stos graficzny: Cage 0.3.1, WebKitGTK 2.54.0, Mesa 26.2.2, V3D 4.2.14.0.
Wyjście HDMI-A-1 pracowało w 2560×1440 przy około 58,30 Hz.

## Poprawka

Jednostka `avcontrol-kiosk.service` ustawia
`WEBKIT_DISABLE_DMABUF_RENDERER=1`. Widok WebKit przekazuje klatki przez
pamięć współdzieloną. Rozdzielczość i kompozytor pozostają te same.
Opis sposobów przekazywania klatek:
[dokumentacja WebKit](https://docs.webkit.org/Ports/WebKitGTK%20and%20WPE%20WebKit/Graphics.html).

Na urządzeniu zastosowano odpowiadający temu plik
`/etc/systemd/system/avcontrol-kiosk.service.d/20-webkit-rendering.conf`
i zrestartowano usługę kiosku. Zrobiono kopię poprzedniego ustawienia;
instalacja przywracałaby je automatycznie, gdyby kiosk nie wystartował.

## Dowody

- [Przed zmianą](evidence/hdmi-rendering-2026-10-12/before.png): pasy widoczne
  już w klatce programu, 2560×1440.
- [Po zmianie](evidence/hdmi-rendering-2026-10-12/after.png): czytelny ekran
  logowania w tej samej rozdzielczości, bez pasów.
- `avcontrol.service`: identyczny PID i czas startu przed i po zmianie;
  lokalne API odpowiada `ok: true`, wersja 1.6.5.
- Skróty konfiguracji rozruchu i ustawień lokalnego panelu są identyczne.
- Istniejące testy `tests/test_local_panel.py`: 3 zakończone powodzeniem.
- Prosta plansza 1280×720 była poprawna zarówno z V3D, jak i z rendererem
  programowym. Ta plansza nie odtwarzała uszkodzenia właściwego ekranu.

Właściciel potwierdził po zmianie: „Tak, obraz jest poprawny”.
Naprawa ma zatem także potwierdzenie na rzeczywistym monitorze HDMI.
Nie wykonywano ponownego rozruchu całej maliny; ustawienie jest zapisane
na dysku i zostało sprawdzone po restarcie samej usługi kiosku.
