# Moduł 5 - Python comprehensions. Pisanie własnych funkcji.

**Zadanie 1**  

Zdefiniuj następujące zbiory, wykorzystując Python comprehension:  
A={1/x: x&isin;<1,10>}  
B={1, 2, 4, 8,…, $2^{10}$}  
C={x: x&isin; B i x jest liczbą podzielną przez 4}  

``` python
A = {1 / x for x in range(1, 11)}
B = [2 ** i for i in range(0, 11)]
C = [x for x in B if x % 4 == 0]

print(A)
print(B)
print(C)
```

**Zadanie 2**

Wygeneruj macierz (lista dwupoziomowa) losowych wartości (sprawdź pakiet **[random](https://docs.python.org/3.12/library/random.html)**)  o rozmiarach 4x4 i wykorzystując Python Comprehension zdefiniuj zmienną typu `list`, która będzie zawierała tylko elementy znajdujące się na przekątnej tej macierzy.

``` python
import random
macierz = [[random.randint(1, 10) for _ in range(4)] for _ in range(4)]
przekatna = [macierz[i][i] for i in range(4)]

for row in macierz:
    print(row)

print("\nPrzekątna macierzy:", przekatna)
```

**Zadanie 3**

Utwórz słownik z produktami spożywczymi do kupienia. Klucz to niech będzie nazwa produktu a wartość - jednostka w jakiej się je kupuje (np. sztuki, kg itd.). Wykorzystaj Python Comprehension do zdefiniowania nowej listy, gdzie będą tylko te produkty, których wartość to sztuki.

Mechanizm przedstawiony w tym podrozdziale jest bardzo przydatny, chociaż skomplikowane polecenia
mogą być wyzwaniem do zinterpretowania względem „tradycyjnego” podejścia. Więcej przykładów można
znaleźć w dokumentacji Pythona pod adresem https://docs.python.org/3.12/tutorial/datastructures.html#nested-list-comprehensions

``` python
produkty = {
       "banany": "sztuki",
        "woda": "litr",
        "bułki": "sztuki",
        "śliwki": "sztuki",
        "ser": "plastry",
    }
lista_produktów_sztuki = [key for key, value in produkty.items() if value == "sztuki"]
print("Produkty na sztuki", lista_produktów_sztuki)
```

**Zadanie 4**

Zdefiniuj funkcję, która "pyta" użytkownika o jego imię i po jego podaniu wyświetla komunikat 'Witaj {imie}!'.

``` python
def witaj():
    imie = input("Jak masz na imię? ")
    print(f"Witaj {imie}!")

witaj()
```

**Zadanie 5**  
Napisz funkcję, która przyjmuje jeden argument pozycyjny, o domyślnej wartości 4, i na podstawie tego argumentu wypisuje na wyjściu (konsola) n*n tych wartości, np.: dla liczby 3:
```python
333
333
333
```

``` python
def kwadrat(n=4):
    for i in range(n):
        print(" ".join([str(n)] * n))

kwadrat(2)
```

**Zadanie 6**

Wykorzystując poprzedni przykład zdefiniuj funkcję, która będzie liczyć iloczyn elementów ciągu.

``` python
def iloczyn(*liczby):
    # jeżeli nie ma argumentów, zwróć 1.0, ponieważ iloczyn pustego zbioru to 1
    if len(liczby) == 0:
        return 1.0
    else:
        iloczyn = 1.0  #
        # mnożymy elementy ciągu
        for i in liczby:
            iloczyn *= i
        # zwracamy wartość iloczynu
        return iloczyn

# wywołanie gdy brak argumentów
print(iloczyn())

# podajemy argumenty
print(iloczyn(1, 2, 3, 4, 5, 6, 7 ,8))
```

**Zadanie 7**

Napisz funkcję, która wykorzystuje symbol **. Funkcja przyjmuje argumenty w postaci: klucz to nazwa drużyny a wartość to ilość punktów, które drużyna zdobyła. Funkcja zlicza ile jest wszystkich punktów razem i zwraca tę wartość.

``` python
def suma_punktow(**punkty):
    suma = 0  # Inicjujemy zmienną do przechowywania sumy punktów

    for drużyna, punkty_drużyny in punkty.items():
        suma += punkty_drużyny  # Dodajemy punkty drużyny do sumy
    return suma  # Zwracamy łączną sumę punktów

print(suma_punktow(polska=3, niemcy=5, hiszpania=2))
```
