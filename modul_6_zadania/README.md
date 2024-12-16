# Moduł 6 - Obsługa plików.

## **Zadania**

**Zadanie 1**

Wczytaj plik `zamowienia.csv` i dokonaj w nim kilku przekształceń: 
* pozbądź się znaku `z` (właściwie zł) z kolumny `Utarg`
* zamień separator wartości dziesiętnej w tej samej kolumnie na `'.'`
* pozbądź się spacji jako separatora tysięcy w kolumnie `Utarg`
* zamień format daty w pliku na RRRR-MM-DD
  
Podziel plik na dwie części i zapisz je tak, aby dane dla każdego kraju (Polska, Niemcy) znajdowały się w oddzielnych plikach o nazwach zamowienia_polska.csv i zamowienia_niemcy.csv.

```python
import csv
from datetime import datetime


# Funkcja czyszcząca kolumnę Utarg
def clean_utarg(utarg):
    # Usuń 'zł' i spacje, zamień przecinki na kropki
    utarg = utarg.replace('zł', '').replace(' ', '').replace(',', '.')
    try:
        return float(utarg)  # Zamienia na liczbę zmiennoprzecinkową
    except ValueError:
        return None  # Jeśli wartość nie jest liczbą, zwróć None


# Funkcja przekształcająca datę
def format_date(date_str):
    try:
        # Zamiana formatu daty z 'DD.MM.YYYY' na 'YYYY-MM-DD'
        return datetime.strptime(date_str, '%d.%m.%Y').strftime('%Y-%m-%d')
    except ValueError:
        return None  # Jeśli data nie pasuje do formatu, zwróć None


# Wczytaj dane z pliku CSV
with open('modul_6_zadania_zamowienia.csv', mode='r', encoding='ISO-8859-2') as infile:  # Spróbuj z innym kodowaniem
    csv_reader = csv.reader(infile, delimiter=';')

    # Wczytaj nagłówek
    header = next(csv_reader)

    # Znajdź indeksy potrzebnych kolumn
    idx_data = header.index('Data zamowienia')
    idx_utarg = header.index('Utarg')
    idx_kraj = header.index('Kraj')

    # Lista dla danych z Polski i Niemiec
    polska_data = []
    niemcy_data = []

    # Iteracja po wierszach danych
    for row in csv_reader:
        # Przekształć datę w wierszu
        row[idx_data] = format_date(row[idx_data])

        # Przekształć wartość w kolumnie Utarg
        row[idx_utarg] = clean_utarg(row[idx_utarg])

        # Podziel dane na Polskę i Niemcy
        if row[idx_kraj] == 'Polska':
            polska_data.append(row)
        elif row[idx_kraj] == 'Niemcy':
            niemcy_data.append(row)

# Zapisz dane dla Polski
with open('modul_6_zadania_zamowienia_polska.csv', mode='w', newline='', encoding='utf-8') as outfile:
    csv_writer = csv.writer(outfile, delimiter=';')
    csv_writer.writerow(header)  # Zapisz nagłówek
    csv_writer.writerows(polska_data)  # Zapisz dane dla Polski

# Zapisz dane dla Niemiec
with open('modul_6_zadania_zamowienia_niemcy.csv', mode='w', newline='', encoding='utf-8') as outfile:
    csv_writer = csv.writer(outfile, delimiter=';')
    csv_writer.writerow(header)  # Zapisz nagłówek
    csv_writer.writerows(niemcy_data)  # Zapisz dane dla Niemiec
```

**Zadanie 2**

Napisz funkcję, która przyjmuje listę plików oraz nazwę nowego pliku jako argumenty wejściowe. Funkcja scala zawartość plików w jeden plik wynikowy o podanej wcześniej nazwie.

```python
import csv

def scal_pliki(lista_plikow, plik_wynikowy):
    # Otwórz plik wynikowy do zapisu
    with open(plik_wynikowy, mode='w', newline='', encoding='utf-8') as wynikowy_plik:
        csv_writer = csv.writer(wynikowy_plik, delimiter=';')

        # Wczytaj dane z pierwszego pliku
        with open(lista_plikow[0], mode='r', encoding='utf-8') as pierwszy_plik:
            csv_reader = csv.reader(pierwszy_plik, delimiter=';')
            header = next(csv_reader)  # Wczytujemy nagłówek z pierwszego pliku
            csv_writer.writerow(header)  # Zapisujemy nagłówek do pliku wynikowego

            # Zapisz wiersze z pierwszego pliku
            for row in csv_reader:
                csv_writer.writerow(row)

        # Dla każdego kolejnego pliku dodaj jego dane do pliku wynikowego
        for plik in lista_plikow[1:]:
            with open(plik, mode='r', encoding='utf-8') as kolejny_plik:
                csv_reader = csv.reader(kolejny_plik, delimiter=';')
                next(csv_reader)  # Pomijamy nagłówek w kolejnych plikach
                for row in csv_reader:
                    csv_writer.writerow(row)  # Zapisujemy dane do pliku wynikowego

    print(f"Plik wynikowy zapisany jako {plik_wynikowy}")
```

## Zadania powtórzeniowe

**Zadanie 3**

Napisz funkcję, która będzie zwracała 3 największe wartości z listy numerycznej. Lista jest parametrem wejściowym funkcji.

```python
# Definiujemy funkcję, która przyjmuje listę jako parametr
def trzy_najwieksze(lista):
    """
    Funkcja zwraca 3 największe wartości z podanej listy numerycznej.
    Parametry: lista (list): Lista zawierająca liczby.
    Zwraca: list: Lista z 3 największymi wartościami.
    """
   
    if len(lista) < 3:  # Sprawdzamy, czy lista ma co najmniej 3 elementy
        return "Lista musi zawierać co najmniej 3 liczby!"

    # Sortujemy listę w kolejności malejącej (od największego do najmniejszego)
    # sorted() to funkcja, która zwraca posortowaną wersję listy
    # reverse=True sprawia, że sortowanie jest malejące
    posortowana = sorted(lista, reverse=True)

    # Pobieramy pierwsze 3 elementy z posortowanej listy
    # Używamy operatora "slicing" [:3], który wybiera pierwsze 3 elementy
    trzy_najwieksze = posortowana[:3]

    # Zwracamy wynik
    return trzy_najwieksze

# Testujemy funkcję
przyklad = [5, 1, 8, 3, 12, 55, 66]
wynik = trzy_najwieksze(przyklad)
print("Trzy największe liczby to:", wynik)
```

**Zadanie 4**

Mając listę `mieszana = [1, 2.3, ‘Zbyszek’, 5, ‘Marian’, 3.0]` napisz funkcję, która zapisze wartości dla każdego typu do słownika gdzie
pod kluczem równym nazwie typu zmiennej (int, float, str, itp.) wartością będzie lista elementów z listy 'mieszana' danego typu.
Przykład: `{'int': [1,5], 'str': ['Zbyszek','Marian']}` itd.

```python
def podziel_wg_typow(lista):
    """
    Funkcja dzieli elementy listy na grupy według ich typów i zapisuje je w słowniku.
    Parametry: lista (list): Lista elementów o różnych typach.
    Zwraca: dict: Słownik, gdzie klucze to nazwy typów, a wartości to listy elementów danego typu.
    """
    # Tworzymy pusty słownik, który będzie przechowywał elementy według typów
    slownik = {}

    # Przechodzimy przez każdy element listy
    for element in lista:
        # Pobieramy nazwę typu elementu
        typ = type(element).__name__    # Funkcja type() zwraca typ obiektu, np. int, float, str.
                                        # Metoda __name__ pobiera nazwę tego typu w formie tekstowej (np. int jako string "int").

        # Sprawdzamy, czy typ jest już kluczem w słowniku
        if typ not in slownik:          # Sprawdzamy, czy typ elementu jest już kluczem w słowniku. Jeśli go nie ma, tworzymy nową listę dla tego typu.
            slownik[typ] = []

        slownik[typ].append(element)     # Dodajemy element do odpowiedniej listy w słowniku

    # Zwracamy gotowy słownik
    return slownik


# Testujemy funkcję na podanej liście
mieszana = [1, 2.3, 'Zbyszek', 5, 'Marian', 3.0]
wynik = podziel_wg_typow(mieszana)
print("Słownik podzielony według typów:", wynik)
```

**Zadanie 5**

Napisz funkcję:
- parametr wejściowy to lista stringów z nazwiskami
- funkcja zapisuje do dwóch oddzielnych plików o nazwach ‘A-M_nazwiska.txt’ oraz ‘N-Ż_nazwiska.txt’ odpowiednie nazwiska z podanej listy 

```python
def zapisz_nazwiska_do_plikow(nazwiska):
    # Sprawdzamy, czy lista nazwisk nie jest pusta
    if not nazwiska:
        print("Lista nazwisk jest pusta!")
        return

    # Tworzymy dwie listy na nazwiska do zapisania
    a_m = []
    n_z = []

    for nazwisko in nazwiska:
        # Pobieramy pierwszą literę nazwiska
        pierwsza_litera = nazwisko[0].upper()  # Zamieniamy na wielką literę, by nie było problemu z małymi literami

        # Sprawdzamy, do którego zakresu należy nazwisko
        if 'A' <= pierwsza_litera <= 'M':
            a_m.append(nazwisko)
        elif 'N' <= pierwsza_litera <= 'Ż':
            n_z.append(nazwisko)

    # Zapisujemy do plików
    with open('A-M_nazwiska.txt', 'w') as file1:
        for nazwisko in a_m:
            file1.write(nazwisko + '\n')  # Zapisujemy nazwisko w nowej linii

    with open('N-Ż_nazwiska.txt', 'w') as file2:
        for nazwisko in n_z:
            file2.write(nazwisko + '\n')  # Zapisujemy nazwisko w nowej linii

nazwiska = ['Anna Jagiello', 'Kamil Bober', 'Piotr Klamerka', 'Pawel Ziolko', 'Marek Dab', 'Alicja Sosna']
zapisz_nazwiska_do_plikow(nazwiska)
```

**Zadanie 6**

Napisz funkcję, która wyświetla podany tekst odwracając kolejność liter w wyrazach. Np.
„Ala ma kota” wyświetli „alA am atok”

```python
zdanie = "Ala ma kota"
def odwroc(wyraz):
    """
    Funkcja odwraca kolejność liter w każdym wyrazie zdania.
    Parametry: zdanie (str): Tekst wejściowy.
    Zwraca:str: Tekst z odwróconymi literami w wyrazach.
    """

    # Dzielimy zdanie na listę wyrazów za pomocą metody split(). Metoda dzieli string na listę wyrazów. Domyślnie po spacjach.
    wyrazy = wyraz.split()

    # Tworzymy nową listę, w której każdy wyraz jest odwrócony
    odwrocone_wyrazy = [wyraz[::-1] for wyraz in wyrazy]

    # Łączymy odwrócone wyrazy w jedno zdanie, używając ' '.join(). Łączy elementy listy w jeden string, dodając pomiędzy " ". 
    return " ".join(odwrocone_wyrazy)

wynik = odwroc(zdanie)
print(wynik)
```

**Zadanie 7**

Napisz funkcję, która:
- jako parametr wejściowy pobiera zdanie wpisywane z klawiatury,
- ponownie z klawiatury pobiera nazwę pliku, w którym zapisany zostanie wynik działania funkcji,
- do pliku zapisywane są unikalne wyrazy ze zdania pisane małymi literami po jednym w linii,
- ze zdania zostaną usunięte ewentualne przecinki i kropki.

```python
import re  # Importujemy moduł do obsługi wyrażeń regularnych
"""
    Funkcja zapisuje unikalne słowa z podanego zdania do wskazanego pliku.
    Parametry: Brak (wszystkie dane pobierane są od użytkownika).
    Zwraca: None
"""
def zapisz_unikalne_wyrazy(zdanie, nazwa_pliku):
    # Usunięcie przecinków i kropek z tekstu, używając wyrażenia regularnego
    zdanie_bez_interpunkcji = re.sub(r'[^\w\s]', '', zdanie)

    # Dzielimy zdanie na słowa, zamieniamy na małe litery
    wyrazy = zdanie_bez_interpunkcji.lower().split()

    # Usunięcie duplikatów (uzyskanie unikalnych wyrazów)
    unikalne_wyrazy = set(wyrazy)

    # Otwiera plik w trybie zapisu. with automatycznie zamyka plik po zakończeniu pracy.
    with open(nazwa_pliku, 'w', encoding="utf-8") as plik:
        # Dodaje słowo do pliku i przechodzi do nowej linii.
        for wyraz in unikalne_wyrazy:
            plik.write(wyraz + '\n')

    print(f"Unikalne wyrazy zostały zapisane do pliku {nazwa_pliku}.")

# Przykład wywołania:
zdanie = input('Podaj zdanie:',)
nazwa_pliku = "modul_6_zadania_unikalne_wyrazy.txt"
zapisz_unikalne_wyrazy(zdanie, nazwa_pliku)
```

**Zadanie 8**

Napisz funkcję, która losuje 5 liczb całkowitych z przedziału <1, 20> dopóki w jednym losowaniu nie wystąpi 1 i 20. Wyświetl ilość
wykonanych losowań po spełnieniu warunku.

```python
import random  # Importujemy bibliotekę do losowania liczb

def losuj_liczby_z_warunkiem():
    """
    Funkcja losuje 5 liczb z przedziału 1-20 do momentu,
    aż w jednym losowaniu pojawią się zarówno liczby 1 i 20.
    Wyświetla liczbę wykonanych losowań.
    """
    liczba_losowan = 0  # Licznik losowań

    while True:  # Pętla działa aż spełniony zostanie warunek. Używamy jej, ponieważ nie znamy z góry liczby iteracji, jakie będą potrzebne do spełnienia warunku.
        liczby = random.sample(range(1, 21), 5)  # Losujemy 5 unikalnych liczb z zakresu 1-20. random.sample() pozwala na losowanie unikalnych liczb.
        liczba_losowan += 1  # Zwiększamy licznik losowań

        # Sprawdzamy, czy liczby 1 i 20 są w wyniku losowania
        if 1 in liczby and 20 in liczby:    # Wykorzystujemy operator in, by sprawdzić, czy 1 i 20 znajdują się w liście wylosowanych liczb.
            break  # Warunek spełniony, przerywamy pętlę

    # Wyświetlamy liczbę losowań
    print(f"Aby uzyskać liczby 1 i 20 w jednym losowaniu, potrzeba było {liczba_losowan} losowań.")

# Wywołanie funkcji
losuj_liczby_z_warunkiem()
```

**Zadanie 9**

Napisz funkcję, która posiada zaszytą listę 3 nagród `['samochód', '10000 PLN', 'PS 4 Pro']`. Przygotuj plik z 10 imionami i nazwiskami
zapisanymi po 1 w wierszu. Następnie funkcja wczytuje plik, losuje zwycięzcę dla każdej z trzech nagród i zapisuje wyniki w pliku o
nazwie zwycięzcy.txt wpis postaci: Imię nazwisko, nagroda.

```python
import random

def losowanie_nagrod():
    """
    Funkcja losuje zwycięzców dla 3 nagród z pliku z imionami i nazwiskami.
    Wyniki zapisuje do pliku zwycięzcy.txt.
    """
    # Nagrody do rozdania
    nagrody = ['samochód', '10000 PLN', 'PS 4 Pro']

    # Wczytanie listy imion i nazwisk z pliku
    with open('modul_6_zadania_imiona_nazwiska.txt', 'r') as plik:
        osoby = [line.strip() for line in plik.readlines()]  # Używamy strip() do usunięcia zbędnych znaków.

        zwyciezcy = random.sample(osoby, len(nagrody))  # Funkcja random.sample() wybiera losowo uczestników, ile jest nagród.

    # Przygotowanie wyników
    wyniki = []
    for i in range(3):
        wyniki.append(f"{zwyciezcy[i]}, {nagrody[i]}")

    # Zapisanie wyników do pliku
    with open('modul_6_zadania_wyniki_losowania.txt', 'w', encoding="utf-8") as plik_wyniki:
        for wynik in wyniki:
            plik_wyniki.write(wynik + '\n')

    print("Wyniki losowania zostały zapisane w pliku 'modul_6_zadania_wyniki_losowania.txt'.")

# Przykład wywołania funkcji
losowanie_nagrod()
```

**Zadanie 10**

Napisz funkcję, która:
- „rozdaje” karty z talii 52 kart (np. As pik, Dama karo, itd.) dla 4 graczy
- karty rozdawane są bez powtórzeń po 5 dla każdego gracza
- wyświetlana jest informacja jak wygląda „ręka” każdego z graczy, np. Alan [As pik, 9 karo, itd.]

```python
import random

def rozdanie_kart():
    """
    Funkcja rozdaje po 5 kart dla 4 graczy z talii 52 kart.
    Wyświetla rękę każdego gracza.
    """
    # Tworzymy talię kart
    kolory = ['pik', 'kier', 'karo', 'trefl']
    wartosci = ['2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K', 'A']
    talia = [f"{wartosc} {kolor}" for kolor in kolory for wartosc in wartosci]

    # Tasujemy talię. Funkcja random.shuffle() losowo miesza karty w talii.
    random.shuffle(talia)

    # Rozdajemy karty 4 graczom po 5 kart
    gracze = {f"Gracz {i + 1}": [] for i in range(4)}  # można zmieniać liczbę graczy
    for i in range(5):  # Każdy dostaje 5 kart, ale można zmienić
        for gracz in gracze:
            gracze[gracz].append(talia.pop())  # Pobieramy jedną kartę z talii. Pop usuwana kartę z talii i dodaje do gracza

    # Wyświetlenie rozdania
    for gracz, karty in gracze.items():
        print(f"{gracz}: {', '.join(karty)}")

# Wywołanie funkcji
rozdanie_kart()
```

**Zadanie 11**

Napisz funkcję, która wczytuje z pliku zawierającego imiona i nazwiska osób zapisane po jednym w linii, np.

Marek Markowski  
Paweł Budzikowski

Funkcja generuje dla podanej listy adresy e-mail postaci: imie.nazwisko@imgw.pl i zapisuje dane do nowego pliku dopisując przy wcześniejszym nazwisku wygenerowany adres, np.

Marek Markowski, marek.markowski@imgw.pl itd. 

W nazwach e-mail powinny być zastępowane ewentualne polskie znaki (ż,ź
na z, ą na a itd.).

```python
import unidecode  # Moduł do usuwania polskich znaków (trzeba zainstalować: pip install unidecode)

def generuj_adresy_email():
    """
    Funkcja wczytuje imiona i nazwiska z pliku, generuje adresy e-mail,
    zastępuje polskie znaki i zapisuje wynik do nowego pliku.
    """
    # Wczytanie imion i nazwisk z pliku
    with open('modul_6_zadania_imiona_nazwiska.txt', 'r') as plik:
        osoby = [line.strip() for line in plik.readlines()]  # Usuwamy białe znaki

    # Generujemy e-maile
    wyniki = []
    for osoba in osoby:
        imie, nazwisko = osoba.split()  # Rozdzielenie na imię i nazwisko
        imie_ascii = unidecode.unidecode(imie.lower())  # Usunięcie polskich znaków i zamiana na małe litery
        nazwisko_ascii = unidecode.unidecode(nazwisko.lower())
        email = f"{imie_ascii}.{nazwisko_ascii}@imgw.pl"  # Tworzymy adres e-mail
        wyniki.append(f"{osoba}, {email}")  # Dodajemy wynik w odpowiednim formacie

    # Zapisanie wyników do pliku
    with open('modul_6_zadania_wyniki_email.txt', 'w') as plik_wyniki:
        for wynik in wyniki:
            plik_wyniki.write(wynik + '\n')

    print("Adresy e-mail zostały zapisane w pliku 'modul_6_zadania_wyniki_email.txt'.")

# Wywołanie funkcji
generuj_adresy_email()
```

**Zadanie 12**

Przygotuj plik z kilkoma hasłami, które nadają się do gry 'Koło fortuny'. Wczytaj te hasła do listy i losuj jedno z nich. Na ekranie wyświetlaj hasło bez ujawniania poszczególnych liter, np.:`___ _____ ___ __ _______` dla hasła 'Bez pracy nie ma kołaczy'. Nastepnie w pętli pozwalaj uzytkownikowi na podawanie jednej litery, która będzie podstawiana w miejscach gdzie występuje lub wyświetlaj komunikat, że takiej litery nie ma w haśle. Dodaj też funkcjonalność, która pozwala na odgadnięcie (wpisanie) całego hasła.

```python
import random
import unidecode

def gra_kolo_fortuny():
    """
    Gra "Koło fortuny" - użytkownik zgaduje litery lub całe hasło.
    """
    # Wczytanie haseł z pliku
    with open('modul_6_zadania_hasla.txt', 'r') as plik:  # Otwieramy plik tekstowy z hasłami w trybie do odczytu ('r'-read). 
        hasla = [line.strip() for line in plik.readlines()]  # Odczytuje wszystkie linie z pliku i zapisuje je jako listę.                                                                  # Usuwa białe znaki
        hasla = [unidecode.unidecode(haslo) for haslo in hasla]

    # Losowanie hasła
    haslo = random.choice(hasla).lower()  # Losuje jedno hasło z listy hasla i zamieniamy na małe litery.
    ukryte_haslo = ''.join(['_' if char.isalpha() else char for char in haslo])  #Sprawdza, czy znak jest literą.
    # Jeśli znak jest literą, zastępujemy go _.
    # Jeśli nie jest literą (np. spacja, przecinek), pozostawiamy go bez zmian.

    print("Witaj w grze 'Koło Fortuny'!")
    print("Twoje hasło to:")
    print(ukryte_haslo)

    while True:  # Pobieranie litery lub całego hasła od użytkownika. Rozpoczynamy nieskończoną pętlę, która będzie działać, dopóki gracz nie zgadnie całego hasła.
        print("\nZgadnij literę lub całe hasło:")
        zgadniecie = input().strip().lower()

        if len(zgadniecie) == 1:  # Gracz zgaduje literę
            if zgadniecie in haslo:
                print(f"Litera '{zgadniecie}' jest w haśle!")
                ukryte_haslo = ''.join(
                    [zgadniecie if zgadniecie == haslo[i] else ukryte_haslo[i] for i in range(len(haslo))]
                )
                print(ukryte_haslo)
            else:
                print(f"Litera '{zgadniecie}' nie występuje w haśle.")
        elif len(zgadniecie) > 1:  # Gracz zgaduje całe hasło
            if zgadniecie == haslo:
                print(f"Brawo! Odgadłeś hasło: {haslo}")
                break
            else:
                print("To nie jest poprawne hasło. Spróbuj jeszcze raz.")

        # Sprawdzenie, czy gracz odkrył całe hasło
        if ukryte_haslo == haslo:
            print(f"Gratulacje! Odkryłeś całe hasło: {haslo}")
            break

# Uruchomienie gry
gra_kolo_fortuny()
```

**Zadanie 13**

Napisz funkcję, która będzie pobierała dwa parametry wejściowe:
* łańcuch znaków
* liczbę całkowitą

Funkcja ma skracać podany łańcuch znaków tak, żeby po dodaniu `...` na końcu jego długość nie była większa niż max (podany jako drugi parametr) i aby tekst nie był urwany w połowie wyrazu. Funkcja zwraca skrócony tekst.

```python
def skroc(tekst, max_dlugosc):
    """
    Funkcja skraca tekst tak, aby po dodaniu '...' jego długość nie przekraczała max_dlugosc
    i nie ucinała wyrazów.
    """
    # Jeśli tekst mieści się w limicie, zwracamy go bez zmian
    if len(tekst) <= max_dlugosc:
        return tekst

    # Skracanie tekstu do najbliższego pełnego wyrazu
    skrocony = tekst[:max_dlugosc].rsplit(' ', 1)[0]  # rsplit dzieli od końca, aby zachować pełne słowo
    return skrocony + '...'  # Dodaj trzy kropki


# Przykładowe użycie
print(skroc("To jest bardzo długi tekst, który trzeba skrócić.", 10))  
print(skroc("Krótki tekst.", 10))
```
