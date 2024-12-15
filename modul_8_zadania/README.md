# Moduł 8 - Wprowadzenie do programowania obiektowego.

**Zadania**

**Zadanie 1**  
Zadeklaruj klasę `Point` o właściwościach `x` oraz `y` (oba typ `int`). Obie właściwości powinny posiadać domyślną wartość równą zero (wywołanie konstruktora bez podania wartości inicjalizujących).

**Zadanie 2**  
Przesłoń w klasie `Point` metodę `__str__()` tak, aby zwracała tekst Point(x, y) gdzie x i y przedstawia aktualną wartość tych właściwości.

**Zadanie 3**  
Sprawdź, czy możliwe jest pomnożenie obiektu typu `Point` przez liczbę całkowitą. Zaimplementuj taką możliwość poprzez przesłonięcie metody `__mul__()`. Przetestuj działanie.

**Zadanie 4**  
Przesłoń w klasie `Point` metodę `__eq__()` odpowiedzialną za porównywanie tego obiektu (self) z innym (other) w sensie tożsamości. Wartość `True` zwracana jest tylko wtedy, gdy jest to dokładnie ten sam typ obiektu (czyli Point) oraz wartości `x` i `y` są identyczne dla obu obiektów.

**Rozwiązanie do zadania od 1 do 4**  

```python
class Point:
    def __init__(self, x=0, y=0):
        self.x = x
        self.y = y

    def __str__(self):
        return f"Point({self.x}, {self.y})"

    def __mul__(self, other):
        if isinstance(other, int):
            return Point(self.x * other, self.y * other)
        raise TypeError("Mnożenie tylko dla liczb całkowitych.")

    def __eq__(self, other):
        if isinstance(other, Point):
            return self.x == other.x and self.y == other.y
        return False

# --- Testowanie zadań ---
# Zadanie 1 i 2
p1 = Point()
print(p1)
p2 = Point(3, 4)
print(p2)

# Zadanie 3
p3 = p2 * 2
print(p3)

# Zadanie 4
print(p1 == Point())
print(p1 == Point(1, 1))
print(p1 == "nie jest obiektem typu Punkt")
```

**Zadanie 5**  
Stwórz klasę o nazwie `Polygon` i zdefiniuj właściwość `points` typu `list`, która będzie docelowo przechowywała obiekty typu `Point`. Inicjalizuj pustą listę w konstruktorze. Zdefiniuj również metodę `add_point(point: Point`), która będzie dodawała punkt do listy.

**Zadanie 6**  
W klasie `Polygon` przesłoń metodę `__str__()` tak, aby wypisanie `Polygon` wyglądało mniej więcej tak: Polygon[Point(2, 3), Point(1,1), ...].

**Zadanie 7**  
W klasie `Polygon` przesłoń metodę `__getitem__()`, tak aby możliwe było zwrócenie pojedynczego punktu (item to int) oraz wycinka (item to slice). W tej metodzie obsłuż wyjątek `TypeError` jeżeli nie jest to int lub slice.

```python
class Polygon:
    def __init__(self):
        self.points = []

    def add_point(self, point):
        if isinstance(point, Point):
            self.points.append(point)
        else:
            raise TypeError("Dodawane mogą być tylko obiekty typu Point.")

    def __str__(self):
        points_str = ", ".join(str(point) for point in self.points)
        return f"Polygon[{points_str}]"

    def __getitem__(self, item):
        if isinstance(item, (int, slice)):
            return self.points[item]
        raise TypeError("indeks musi być int lub slice.")

# --- Testowanie zadań ---
# Zadanie 5 i 6
poly = Polygon()
poly.add_point(p1)
poly.add_point(p2)
print(poly)

# Zadanie 7
print(poly[0])
print(poly[1:])
try:
    print(poly["invalid"])
except TypeError as e:
    print(e)
``
