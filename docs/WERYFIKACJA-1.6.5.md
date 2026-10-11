# Weryfikacja AV Control 1.6.5

## Zakres

Studio pozwala ukrywać przyciskiem X karty i krótsze bloki instrukcji. Katalog obejmuje 100 tematów, w tym kartę podłączenia konwertera, protokoły, sygnały, kreatory, logikę, Python, tła paneli, metrykę, diagnostykę i ustawienia. Ustawienia pokazują ukryte podpowiedzi, wyszukiwanie i przywracanie pojedyncze lub zbiorcze.

Preferencja jest lokalna i obejmuje wszystkie projekty na stanowisku. Nie zmienia modelu projektu ani danych kontrolera. Okna Studio synchronizują ustawienie. Nieprawidłowe dane magazynu są ignorowane; gdy magazyn jest niedostępny, ukrywanie i przywracanie działa w bieżącej sesji.

## Dowody

- `docs/evidence/guidance-1.6.5.json`: próby przycisku X, obsługi klawiaturą i dotykiem, nawigacji, ponownego wczytania, dwóch okien, wyszukiwania, przywracania, zachowania projektu i nieprawidłowego magazynu preferencji.
- Ogólny test interfejsu i test metryki sprawdzają edycję i eksport projektu, logikę, panele i diagnostykę.
- Lokalny przebieg sześciu zadań CI, instalatory Windows, pakiet Player Linux, obraz ARM64 i pakiet aktualizacji mają osobne raporty. Manifest wydania wiąże je z dokładnym commitem, sumami i podpisem ECDSA.
- Podręcznik jest sprawdzoną rewizją z 11 października 2026: 206 stron, 52 rozdziały, cztery dodatki i 77 ilustracji. PDF zachowuje SHA256 `2f712ee3dda6089d08e2173c05f12bc891fe82c44577c262e7b9c3b10fc37635`; `docs/tutorial/page-review.json` zawiera 206 ocen PASS. Instrukcja programu opisuje nowe ukrywanie i przywracanie podpowiedzi.

## Granice

Próba dotyku w przeglądarce sprawdza układ i cel dotknięcia o wymiarach 44 × 44 px; nie stanowi próby fizycznego ekranu. Testy obrazu ARM pod QEMU oraz kiosku na wirtualnym wyjściu Wayland nie potwierdzają rozruchu nowej fizycznej karty SD ani fizycznego HDMI, USB i komunikacji elektrycznej. Starsze pomiary i raporty są zachowane jako oznaczona wersją baza odniesienia.
