(Read this in other languages: [English](README.en.md) ) 

# Programiaki – nauka programowania przez zabawę dla dzieci w wieku przedszkolnym.

Zamawiający: Przedszkola

**Efekty**

_Obserwacje zostały zebrane podczas prowadzenia zajęć z wykorzystaniem  projektu lProgramiaki w łódzkich przedszkolach. Osiągnięte cele zawierają się obszarach:_

## Zalety oswojania dzieci z programowaniem

* nauka podstaw programowania poprzez zabawę z wykorzystaniem ruchu;
* uzmysłowienie dziecku, czym jest programowanie przez wskazanie jak uzyskać dane zachowanie przez określone czynności np. przygotowanie zestawu  poleceń/trasy dla robota (w szerszym kontekście będzie to przypisanie do zmiennej, kolejność wykonywania działań, sekwencyjność, grupowanie wartości, pętla, debugowanie, optymalizacja działań, podział działań na podzadania, przypisywanie czynności, poleceń do obiektów);

### Rozwój miękkich kompetencji

* kształcenie umiejętności rozmowy, komunikacji w grupie
* ukierunkowanych m.in. na rozwiązywanie problemów;
* kształcenie umiejętność wyrażania własnych uczuć, opinii i myśli;
* kształcenie umiejętności myślenia komputacyjnego, systemowego i desing thinking oraz analitycznego;

### Rozwój umiejętności niezbędnych do nauki

* kształcenie umiejętności koncentracji uwagi, zapamiętywanie informacji; 
* kształcenie umiejętności aktywnego słuchania;
* doświadczanie sukcesu w wyniku wykonania zadania;

## Kontekst i cel projektu:

Programiaki to projekt skierowany do prowadzących nauczanie w wieku przedszkolnym. Pozwala on zaznajomić dzieci z podstawami programowania poprzez wciągające gry i zabawy. W ramach projektu przygotowane zostało kompletne rozwiązanie obejmujące:

* scenariusze zajęć zgodne z materiałem jaki powinno przyswoić dziecko na danym poziomie rozwoju
* narzędzia dydaktyczne takie jak stół multimedialny, programowalny robot oraz maty i klocki
* oprogramowanie obsługujące narzędzia dydaktyczne i aplikacja umożliwiająca sprawne prowadzenie zajęć przez opiekuna grupy

Projekt Programiaki realizuje podstawowe potrzeby rozwojowe przedszkolaków związane z ruchem, doświadczaniem świata przez zmysły, rozwojem umiejętności poznawczych i nauką przez zabawę. Opiera się on na założeniu, że nauka programowania powinno być oparta na współpracy, czyli tzw. collaborative learning i dopasowana do poziomu rozwoju dziecka. Przygotowane rozwiązanie pozwala odejść od myślenia o programowaniu jako interakcji jeden-na-jeden, na rzecz nauki programowania w kontekście działania mogącego wspierać pracę zespołową. Kiedy dzieci programują wspólnie, biorą udział nie tylko w kolaboracji i pracy grupowej lecz także w nauce właściwego kształtowania relacji międzyludzkich. To wiąże się z rozwojem zdolności poruszania się w społeczeństwie i wyrobieniem sobie społecznych wzorców, które niezbędne są w negocjacji, rozwiązywaniu problemów, dzieleniu się emocjami czy pracą.

Produkt spełnia kryterium dotyczące narastania trudności i misji wraz z rozwojem umiejętności dziecka. Każda z gier ma kilka poziomów dostosowanych do umiejętności i możliwości zróżnicowanej wiekowo grupy dzieci. Dzięki specjalnie stworzonej aplikacji nauczyciel przedszkolny może zarządzać dostępem dziecka do odpowiednich poziomów. To nauczyciel decyduje, które poziomy gier włączyć, bowiem, znając swoją grupę dzieci, wie, jakimi umiejętnościami dysponują jego wychowankowie.

## Realizacja narzędzi

### Stolik multimedialny

Stolik multimedialny to interaktywne multimedialne innowacyjne stoisko prezentacyjne z funkcją nauki programowania przez interakcje z tagami RFID. W stole wbudowano czytniki RFID odczytujące dane z klocków. Gry na stole multimedialnym są tematycznie powiązane z zagadnieniami pojawiającymi się na zajęciach, stopniowo kształcą umiejętności programistyczne od najprostszych gier, w ramach których dzieci uczą się przypisywania obiektów do zmiennej, po coraz trudniejsze, np. sekwencje, pętle, pobieranie i zwracanie danych, aż do złożonej analizy problemu koniecznej do wyboru lepszej opcji w danej grze.

### Klocki

Na bazie grafik wykorzystywanych w grach wydruki 3D, we wnętrzu których znajdują się tagi RFID. Klocki swoim wyglądem reprezentują zwierzęta, kierunki, karty mnożnika etc. Ich celem jest zmniejszenie poziomu abstrakcji przy nauce programowania i, dodatkowo, ułatwienie zrealizowania przez dzieci zadań przewidzianych np. w grze ZOO, która wymaga od dzieci umiejętności identyfikowania ze słuchu dźwięków zwierząt.

### Robot

Prototyp własnej konstrukcji zbudowany na bazie LEGO Mindstorm. Robot ma za zadanie wykonywać polecenia zaprogramowane przez kod stworzony przez dzieci za pomocą klocków z tagami RFID ułożonymi na stole multimedialnym.

### Software

W ramach projektu zostało przygotowane oprogramowanie odpowiedzialne za działanie całego zestawu i umożliwiające prowadzenie zajęć.

#### Backend składa się z:

1. Aplikacji działającej na Arduino

   Aplikacja działająca na mikrokontrolerze Arduino ma za zadanie odczytać dane z podłączonych do mikrokontrolera czytników RFID. Po zaczytaniu wartości czytnika wpisuje go do tablicy z kartami - jeśli na czytniku nie jest położona żadna karta wówczas podstawia wartość 404 oznaczającą "brak karty". Aplikacja używa protokołu komunikacji i2c w trybie slave - gdy dostanie wskazane zadanie (tabela poniżej) od urządzenia pracującego w trybie "master", następne żądanie danych będzie odpowiedzią na żądane zadanie.


2. Aplikacji agregującej dane z Arduino i przesyłającej do serwera Websocket

   Aplikacja napisana w języku Python w wersji języka 3.4. Aplikacja działa na urządzeniu komunikującym się w protokole i2c w trybie master. W pętli odpytuje się podłączone do urządzenia (i skonfigurowane w aplikacji) mikrokontrolery Arduino. Jeśli na pytanie "czy jest coś nowego" dostanie odpowiedź twierdzącą wówczas uruchamia żądanie zwracające nową kartę. Otrzymaną informację przekazuje do serwera websocketowego.

3. Serwera Websocket

   Serwer websocket obsługuje połączenia przychodzące i rozpropagowuje przychodzące treści do wszystkich podłączonych klientów.

|KOD ZADANIA|OPIS ZADANIA|
|---|---|
|68|Reset Wysłanych Kart.|
|70|Ile jest podłączonych czytników RFID.|
|72|Czy pośród aktualnych kart istnieją karty jeszcze nie wysłane.|
|74|Który czytnik jeszcze nie został wysłany.|
|76|Jak długa będzie odpowiedź.|
|78|Podaj kolejną cyfrę z numeru karty. Żądanie powtarzane tyle razy ile wyniesie odpowiedź na zadanie 76.|


|KOD ZADANIA|KODY ODPOWIEDZI|OPIS|
|---|---|---|
|70|int|Liczba czytników podłączona pod miktokontroler.|
|72|20|Tak, istnieją.|
|72|22|Nie, nie istnieją.|
|74|int|Numer czytnika który nie został jeszcze przesłany.|
|76|int|Po zczytaniu karty mają one różne długości - zwraca długość numeru karty.|
|78|int|Zwraca jeden numer z ciągu znaków i ustawia index na koleną pozycję.|


#### Frontend:

1. Aplikacja nauczyciela

 Aby nadzorować proces nauki programowania dzieci w wieku przedszkolnym powstała aplikacja dla nauczycieli realizująca następujące zadania:
 * Logowanie / Wylogowanie opiekuna grupy
 * Blokada stołu w celu odciągnięcia dzieci od stołu
 * Zablokowanie panelu opiekuna (w celu aby niepowołane dziecko nie zarządzało aplikacją)
 * Uruchomienie na stole multimedialnym
 * Listowanie, dodawanie, edycja, usuwanie grup
 * Przypisywanie/Usuwanie dzieci do grup
 * Wywołanie dodawania dzieci
 * Obsługa żądania rozpoczęcia nowej gry:
   * Wybór dzieci grających w grę (w celu późniejszego przyznania punktów gamifikacji)
   * Zatwierdzenie uruchomienia poziomu w grze
 * Obsługa zatwierdzania punktów gamifikacji.

2. Aplikacja z grami (na stół multimedialny).

 Przygotowany interfejs pełni różne role, np.:
 * programowanie w zakresie kolejnych ruchów robota czy pszczółki,
 * rysowanie kształtów,
 * grupowanie kształtów czy układanie puzzli,
 * odgrywanie dźwięków.

 Dedykowany jest dzieciom z różnych grup wiekowych, 3-, 4-, 5-, 6-latków, które uznały produkt za atrakcyjny.


### Przykłady gier:

#### H4 Kolory i Kształty (Drag&Drop)

Part 1 - Kolory

1. Przeciągnij i upuść czerwony kwadrat na czerwone pole (tylko czerwone pole do upuszczania) – nauka obsługi TUI + segregowanie danych.
2. Przeciągnij i upuść zielony trójkąt na zielone pole – nauka obsługi TUI + segregowanie danych.
3. Przeciągnij i upuść niebieskie koło na niebieskie pole – nauka obsługi TUI + segregowanie danych.
4. Przeciągnij i upuść zielony kwadrat na zielone pole (dostępne 3 kolory pól do upuszczenia) – segregowanie danych, analiza problemu.
5. Przeciągnij i upuść niebieski trójkąt na niebieskie pole (dostępne 3 kolory pól do upuszczenia) – segregowanie danych, analiza problemu.
6. Przeciągnij i upuść czerwone koło na czerwone pole (dostępne 3 kolory pól do upuszczenia) – segregowanie danych, analiza problemu.
7. Posortuj niebieski kwadrat i zielone koło (dostępne 3 kolory pól do upuszczenia) – segregowanie wielu danych, analiza wielu problemów w jednym zadaniu.
8. Posortuj 2x niebieski kwadrat i czerwony trójkąt (dostępne 3 kolory pól do upuszczenia) – segregowanie wielu danych, analiza wielu problemów w jednym zadaniu.
9. Posortuj niebieski kwadrat, czerwony trójkąt i zielone koło (dostępne 3 kolory pól do upuszczenia) – segregowanie wielu danych, analiza wielu problemów w jednym zadaniu.
10. Posortuj niebieski kwadrat, czerwony trójkąt, zielone koło, zielony kwadrat, niebieski trójkąt, czerwone koło (dostępne 3 kolory pól do upuszczenia) – segregowanie wielu danych, analiza wielu problemów w jednym zadaniu.

Part 2 – Kształty

1. Przeciągnij i upuść czerwony kwadrat na kwadratowe pole (tylko kwadratowe pole do upuszczania) – segregowanie danych.
2. Przeciągnij i upuść zielony trójkąt na trójkątne pole – segregowanie danych.
3. Przeciągnij i upuść niebieskie koło na okrągłe pole – segregowanie danych.
4. Przeciągnij i upuść zielony kwadrat na kwadratowe pole (dostępne 3 typy pól do upuszczenia) – segregowanie danych, analiza problemu.
5. Przeciągnij i upuść niebieski trójkąt na trójkątne pole (dostępne 3 typy pól do upuszczenia) – segregowanie danych, analiza problemu.
6. Przeciągnij i upuść czerwone koło na okrągłe pole (dostępne 3 typy pól do upuszczenia) – segregowanie danych, analiza problemu.
7. Posortuj niebieski kwadrat i zielone koło (dostępne 3 typy pól do upuszczenia) – segregowanie wielu danych, analiza wielu problemów w jednym zadaniu.
8. Posortuj 2x niebieski kwadrat i czerwony trójkąt (dostępne 3 typy pól do upuszczenia) – segregowanie wielu danych, analiza wielu problemów w jednym zadaniu.
9. Posortuj niebieski kwadrat, czerwony trójkąt i zielone koło (dostępne 3 typy pól do upuszczenia) – segregowanie wielu danych, analiza wielu problemów w jednym zadaniu.
10. Posortuj niebieski kwadrat, czerwony trójkąt, zielone koło, zielony kwadrat, niebieski trójkąt, czerwone koło (dostępne 3 typy pól do upuszczenia) – segregowanie wielu danych, analiza wielu problemów w jednym zadaniu.

Part 3 – Kolory i Kształty

1. Przeciągnij i upuść czerwony kwadrat na kwadratowe pole (tylko czerwone kwadratowe pole do upuszczania) – segregowanie danych.
2. Przeciągnij i upuść zielony trójkąt na trójkątne pole (tylko zielone trójkątne pole do upuszczania) – segregowanie danych.
3. Przeciągnij i upuść niebieskie koło na okrągłe pole (tylko niebieskie okrągłe pole do upuszczania) – segregowanie danych.
4. Przeciągnij i upuść zielony kwadrat na kwadratowe pole (dostępne 3 typy kolorowych pól do upuszczenia) – segregowanie danych, analiza problemu.
5. Przeciągnij i upuść niebieski trójkąt na trójkątne pole (dostępne 3 typy pól do upuszczenia) – segregowanie danych, analiza problemu.
6. Przeciągnij i upuść czerwone koło na okrągłe pole (dostępne 3 typy pól do upuszczenia) – segregowanie danych, analiza problemu.
7. Posortuj niebieski kwadrat i zielone koło (dostępne 3 typy pól do upuszczenia) – segregowanie wielu danych, analiza wielu problemów w jednym zadaniu.
8. Posortuj 2x niebieski kwadrat i czerwony trójkąt (dostępne 3 typy pól do upuszczenia) – segregowanie wielu danych, analiza wielu problemów w jednym zadaniu.
9. Posortuj niebieski kwadrat, czerwony trójkąt i zielone koło (dostępne 3 typy pól do upuszczenia) – segregowanie wielu danych, analiza wielu problemów w jednym zadaniu.
10. Posortuj niebieski kwadrat, czerwony trójkąt, zielone koło, zielony kwadrat, niebieski trójkąt, czerwone koło (dostępne 3 typy pól do upuszczenia) – segregowanie wielu danych, analiza wielu problemów w jednym zadaniu.

#### Gra Pszczółka cz.1:

Dotarcie do celu poprzez użycie:

1. strzałki „w lewo” - sekwencje, pętle;
2. strzałki „w prawo” - sekwencje, pętle;
3. strzałki „w górę” - sekwencje, pętle;
4. strzałki „w dół” - sekwencje, pętle;
5. strzałki „w lewo”, poziom z pająkiem - sekwencje, pętle;
6. strzałki „w górę” i „w prawo”, poziom z pająkiem - sekwencje, pętle;
7. strzałki „w górę” i „w lewo”, poziom z pająkiem - sekwencje, pętle;
8. strzałki „w górę” i „w lewo”, poziom z pająkiem na alternatywnej drodze – sekwencje, pętle, analiza problemu;
9. strzałki „w górę” i „w lewo”, poziom z pająkiem na alternatywnej drodze – sekwencje, pętle, analiza problemu + wybór lepszej opcji;
10. strzałki „w górę”, „w lewo”, i „w prawo” poziom z pająkiem na alternatywnej drodze – sekwencje, pętle, analiza problemu + wybór lepszej opcji;
11. strzałki „w górę”, „w prawo”, i „w dół” poziom z pająkiem na alternatywnej drodze – sekwencje, pętle, analiza problemu + wybór lepszej opcji;
12. strzałki „w górę”, „w prawo”, i „w dół” poziom z pająkiem na alternatywnej drodze – sekwencje, analiza problemu + wybór lepszej opcji, pętla w pętli;
13. strzałki „w górę”, „w prawo”, i „w dół” poziom z pająkiem na alternatywnej drodze – sekwencje, pętle, analiza problemu + wybór lepszej opcji;
14. strzałki „w górę”, „w prawo”, i „w dół” poziom z pająkiem na alternatywnej drodze – sekwencje, pętle, analiza problemu (2 złe ścieżki) + wybór lepszej opcji;

Pszczółka cz. 2:

Dotarcie do celu poprzez użycie:

1. „w lewo” - sekwencje, pętle, pobieranie danych, zwracanie danych;
2. strzałki „w prawo” - sekwencje, pętle, pobieranie danych, zwracanie danych;
3. strzałki „w górę”, „w prawo” - sekwencje, pętle, pobieranie danych, zwracanie danych;
4. strzałki „w górę”, „w prawo” - sekwencje, pętle, pobieranie danych z różnych miejsc, zwracanie danych;
5. strzałki „w lewo”, „w dół”- sekwencje, pętle, pobieranie danych z różnych miejsc, zwracanie danych, pętle;
6. strzałki „w górę”, „w dół” i „w lewo” - sekwencje, pętle, pobieranie danych z różnych miejsc, zwracanie danych;
7. strzałki „w dół” i „w lewo”, - sekwencje, pobieranie danych z różnych miejsc, zwracanie danych w różne miejsca;
8. strzałki „w górę”, „w dół” i „w lewo” - sekwencje, pętle, pobieranie danych z różnych miejsc, zwracanie danych w różne miejsca;
9. strzałki we wszystkie kierunki poziom z pająkiem - sekwencje, pętle, pobieranie danych z różnych miejsc, zwracanie danych;
10. strzałki „w lewo”; poziom z pająkiem - sekwencje, pętle, pobieranie danych z, zwracanie danych;
11. strzałki we wszystkich kierunkach poziom z pająkiem na alternatywnej drodze - sekwencje, pętle, pobieranie danych z różnych miejsc, zwracanie danych w różne miejsca, analiza problemu + wybór lepszej opcji;
12. strzałki we wszystkich kierunkach poziom z pająkiem na alternatywnej drodze sekwencje, pętle, pobieranie danych z różnych miejsc, zwracanie danych w różne miejsca, analiza problemu + wybór lepszej opcji;
13. strzałki we wszystkich kierunkach poziom z pająkiem na alternatywnej drodze – sekwencje, pętle, pobieranie danych z różnych miejsc, zwracanie danych w różne miejsca, analiza problemu + wybór lepszej opcji.


### Realizacja dydaktyka

Konstrukcja zajęć jest elastyczna. Pozwala łączyć innowacyjną metodę nauczania programowania wykorzystującą multimedialny stół oraz gry i zabawy ruchowe. Oto jej główne założenia:

* w scenariuszach w ramach toku lekcji na początku pojawia się zabawa wprowadzająca,
następnie aktywności stolikowe i dywanowe, zabawy ruchowe, dalej: zabawa programistyczna, kształcąca podstawowe umiejętności, i zabawa na zakończenie;

* aktywności stolikowe (kolorowanie, karty pracy, wycinanie itp.) przeplatane są aktywnościami dywanowymi – zabawami ruchowymi;

* zabawy ruchowe mają za zadanie kształcenie sprawności w zakresie małej i dużej motoryki, a także podstawowych umiejętności programistycznych;

* w ramach gier programistycznych pojawiają się dźwięki, które wskazują na poprawny lub niepoprawny sposób wykonania zadania oraz klocki z tagami RFID identyfikującymi zwierzęta, jedzenie i kierunki czy polecenia;

* zajęcia powtórkowe dla powtórzenia i utrwalenia wiadomości, jakie dzieci uzyskały podczas poprzednich zajęć. Zaproponowane zabawy programistyczne można zmieniać w zależności od tego, które podobały się dzieciom, w jakim wieku są przedszkolaki, co sprawiało trudność – do czego trzeba wrócić. Wśród zabaw ruchowych pojawiają się nowe i znane już dzieciom. Gotowe scenariusze można modyfikować;

* czas zajęć nie jest ściśle określony, ich długość jest uzależniona od wieku i możliwości dzieci (ok. 45-60min.);

### Karty pracy

Karty zostały skonstruowane tak, by kształciły sprawność ręki czy koordynację ręka-oko i mogły je wykonywać zarówno 3-latki, jak i 6-latki. Są to: labirynty, kolorowanie elementów zgodnie z wytycznymi w zadaniu, zapisywanie kodu zgodnego ze sposobem, w jaki zostały pokolorowane elementy rysunku. Zadania umieszczone w kartach pracy są kompatybilne z zadaniami wykonywanymi na macie, a ich celem jest kształcenie podstawowych umiejętności programistycznych, np. kolejność wykonywania działań, grupowanie wartości, przypisywanie czynności do obiektów, podejmowanie decyzji w zakresie kierunku realizacji wyznaczonego celu.

Do wykorzystania w programie jest 37 kart pracy zróżnicowanych pod względem trudności zadań do wykonania. Dodatkowo w programie znajdują się karty pracy nr.38-57, są to kolorowanki z obrazami zwierząt pojawiających się w grach na stole multimedialnym.

## Podsumowanie

Podczas badań przeprowadzonych w warunkach operacyjnych (przedszkola) potwierdzono, że opracowana metodyka nauczania programowania i związana z nią pomoc dydaktyczna, jaką jest stolik multimedialny, jest efektywną realizacją kształcenia kompetencji programistycznych u dzieci w wieku przedszkolnym. Testy, w którym wzięły udział dzieci w różnym wieku, wykazały, że dzięki wykorzystaniu technologii TUI (ang. Tangible User Interface)  i klocków nasz produkt nie wymaga od użytkownika doświadczenia z podobną technologią. Programiaki są rozwiązaniem angażującym dzieci do nauki, dającym pozytywne wzmocnienie i są cenną pomocą dydaktyczną dla prowadzących zajęcia.
