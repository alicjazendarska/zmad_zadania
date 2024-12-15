# Moduł 4 - Instrukcja warunkowa. Pętle.

> Zadania

**Zadanie 1**   
Napisz skrypt, który pobiera od użytkownika zdanie i liczy w nim spacje. Wynik wyświetla na ekranie (użyj instrukcji input).

```python
from itertools import count
from os import write
zdanie = input("wpisz swoje zdanie:")
print(zdanie.count(" "))
```

**Zadanie 2**  
Napisz skrypt, który pobiera od użytkownika dwie wartości i mnoży je przez siebie. Wynik wyświetla na ekranie (ale użyj instrukcji `readline()` i `write()` z modułu `sys`).

```python
import sys
sys.stdout.write("Podaj pierwszą liczbę: ")
a = float(sys.stdin.readline().strip())
sys.stdout.write("Podaj drugą liczbę: ")
b = float(sys.stdin.readline().strip())
wynik = a * b
sys.stdout.write(f"Wynik mnożenia {a} i {b} to: {wynik}\n")
```

**Zadanie 3**  
Napisz skrypt, który pobiera od użytkownika trzy liczby a, b i c. Sprawdza następujące warunki:

* czy a zawiera się w przedziale (0,10]
* oraz czy jednocześnie a>b lub b>c.
  
W obu przypadkach (jeżeli warunki są spełnione lub nie są spełnione) należy wyświetlić odpowiedni komunikat na ekranie.

```python
a = float(input("Podaj liczbę a: "))
b = float(input("Podaj liczbę b: "))
c = float(input("Podaj liczbę c: "))
if (0 < a <= 10) and (a > b or b > c):
    print("Warunki zostały spełnione.")
else:
    print("Warunki nie zostały spełnione.")
```

**Zadanie 4**  
Napisz pętlę, która wyświetla liczby podzielne przez 5 z zakresu [0,50]

```python
for liczba in range(0, 51):
    if liczba % 5 == 0:
        print(liczba)
```

**Zadanie 5**  
Napisz pętle (while), która pobiera liczby od użytkownika i wyświetla ich kwadraty na ekranie. Liczby pobierane są w postaci oddzielonej spacjami. Pętla kończy działanie po wpisaniu słowa `quit`.

```python
while (data := input('numbers: ')) != 'quit':
    print(' '.join(str(float(n) ** 2) for n in data.split()))
```

**Zadanie 6**  
Napisz skrypt, który odczytuje liczby od użytkownika i umieszcza je na liście. Liczby dodajemy do momentu wpisania słowa 'stop' zamiast liczby. Wykorzystaj pętle while. Po wpisaniu stop wyświetl listę liczb.

```python
lista = list()
while (dane := input("Podaj liczbe (lub 'stop'): ")) != "stop":
    lista.append(int(dane))
print("Zakończono.")
print(lista)
```

**Zadanie 7**  
Napisz skrypt, który odczytuje od użytkownika liczbę wielocyfrową i sumuje jej cyfry. Wynik wyświetla na ekranie. Napisz dwa rozwiązania: jedno z uzyciem pętli `for` a drugie z użyciem pętli `while`.

```python
# Dla for
# Pobranie liczby od użytkownika
liczba = input("Podaj liczbę wielocyfrową: ")
suma_cyfr = 0
for cyfra in liczba:
    suma_cyfr += int(cyfra)
print(f"Suma cyfr liczby {liczba} wynosi: {suma_cyfr}")

# dla while
liczba = input("Podaj liczbę wielocyfrową: ")
suma_cyfr = 0
i = 0
while i < len(liczba):
    suma_cyfr += int(liczba[i])
    i += 1
print(f"Suma cyfr liczby {liczba} wynosi: {suma_cyfr}")
```

**Zadanie 8**  
Napisz skrypt, który rysuje wieżę z literek. Użytkownik podaje wysokość wieży, ale nie więcej jak 10.
```
A
AA
AAA
AAAA
AAAAA
AAAAAA
```

```python
wysokosc = int(input("Podaj wysokość: "))
if wysokosc < 1 or wysokosc > 10:
    print("Podana wysokość jest poza zakresem")
else:

    litera = 'A'
    for i in range(1, wysokosc + 1):
        print(litera * i)
```

**Zadanie 9**  
Napisz skrypt, który wyświetla i oblicza tabliczkę mnożenia od 1 do 100 w formie znanej z lekcji matematyki w szkole podstawowej.

```python
n = 10
print('  ', end='')
for i in range(1, n + 1):
    print(f'{i:>4}', end="")
print()
for row in range(1, n + 1):
    print(f"{row:>2}", end= '')
    for col in range(1, n + 1):
        print(f"{row * col:>4}", end='')
    print()

max_rzad = len(str(n ** 2)) + 1
# pierwszy wiersz
print('  ', end='')
for i in range(1, n + 1):
    print(f'{i:>{max_rzad}}', end="")
print()
# kolejne wiersze
for row in range(1, n + 1):
    print(f"{row:>2}", end='')
    for col in range(1, n + 1):
        print(f"{row * col:>{max_rzad}}", end='')
    print()
```

**Zadanie 10**  
Napisz skrypt, który rysuje diament. Użytkownik podaje wysokość nie mniej jak 3 i nie więcej jak 9, ale dopuszczamy tylko nieparzystą wysokość.

Przykład wyjścia dla `wysokosc = 3`
```
 o
ooo
 o
```
oraz `wysokosc = 5`
```
  o
 ooo
ooooo
 ooo
  o
```
itd.

```python
wys = int(input("Podaj wysokość:\n"))
znak = 'o'
if wys in [3, 5, 7, 9, 11, 13]:

    # pierwszy sposób
    for row in range(1, height + 1, 2):
        print(f"{znak * row:^{height}}")
    for row in range(height-2, 0, -2):
        print(f"{znak * row:^{height}}")

    # drugi sposób
    for row in list(range(1, wys + 1, 2)) + list(range(wys - 2, 0, -2)):
        print(f"{znak * row:^{wys}}")
else:
    print("Błędna wartość wysokość")
```
