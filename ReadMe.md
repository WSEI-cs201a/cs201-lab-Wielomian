### Wielomian - Well formed class (15 pkt.)

Wielomian, to znane Ci pojęcie z matematyki ( [Wielomian @Wikipedia](https://pl.wikipedia.org/wiki/Wielomian) ):

\[ a_n x^n + a_{n-1} x^{n-1} + ... + a_2 x^2 + a_1 x + a_0 \]

Wielomian jest jednoznacznie reprezentowany przez ciąg jego współczynników: \( a_n, a_{n-1}, ..., a_2, a_1, a_0 \).

**Stopień wielomianu** to wartość najwyższej potęgi stojącej przy \(x\). Wielomian stopnia zerowego to tylko liczba, będąca wyrazem wolnym \(a_0\).

Twoim zadaniem jest zaimplementowanie klasy `Wielomian` spełniającej podane poniżej warunki:

1. Klasa opisuje wielomian stopnia dowolnego (to znaczy zarówno wielomian stopnia 0, stopnia 2 jak i np. stopnia 100).

2. Obiekty klasy `Wielomian` są niezmiennicze.

3. Wielomian domyślny to wielomian zerowy - tzn. stopnia zerowego, tylko wyraz wolny \(a_0 = 0\).

4. Współczynniki wielomianu są liczbami całkowitymi.

5. Klasa jest zapieczętowana (nie można z niej dziedziczyć).

___
#### Polecenia

1. Utwórz _solution_ składające się z 3 projektów: **(1 pkt.)**
   *  typu _class library_, w którym zlokalizowana będzie klasa `Wielomian`,
   *  typu _unit test_ (MSTestV2) w którym umieścisz testy jednostkowe wybranych publicznych funkcjonalności klasy `Wielomian`,
   *  typu _console application_ zawierający poniższy kod sprawdzający poprawność implementacji klasy.

W projekcie typu _console application_, w pliku `Program.cs`, wklej podany poniżej kod. Kod ten testuje poprawność wykonania poszczególnych poleceń.

```csharp
using System;
using MyMath;
using W = MyMath.Wielomian; //alias dla nazwy klasy Wielomian
using MyExtensions;
using System.Collections.Generic;

namespace z2_1_wielomian
{
    public class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("== Test implementacji klasy Wielomian! ==");

            Console.WriteLine("== Konstrukcja ==");

            Wielomian w0 = new Wielomian();
            Console.WriteLine($"wielomian domyślny W() = {w0}, stopień = {w0.Stopien}");

            Wielomian w01 = new W(-1);
            Console.WriteLine($"W(-1) = {w01}, stopień = {w01.Stopien}");

            Wielomian w02 = new W(0);
            Console.WriteLine($"W(0) = {w02}, stopień = {w02.Stopien}");

            Wielomian w03 = new W(0, 0);
            Console.WriteLine($"W(0,0) = {w03}, stopień = {w03.Stopien}");

            var w11 = new Wielomian(1, 0);
            Console.WriteLine($"W(1,0) = {w11}, stopień = {w11.Stopien}");

            var w12 = new Wielomian(1, -1);
            Console.WriteLine($"W(1,-1) = {w12}, stopień = {w12.Stopien}");

            var w3 = new W(-2, 0, 1, -3);
            Console.WriteLine($"W(-2, 0, 1, -3) = {w3}, stopień = {w3.Stopien}");

            var w31 = new W(0, 0, 0, -2, 0, 1, -3);
            Console.WriteLine($"W(0, 0, 0, -2, 0, 1, -3) = {w31}, stopień = {w31.Stopien}");

            int[] wsp = { 3, 1, 3, 0, -2, 4, 5, 1, 0, 0 };
            var wX = new Wielomian(wsp);
            Console.WriteLine($"wielomian z tablicy = {wX}, stopień = {wX.Stopien}");

            try
            {
                new Wielomian(null);
            }
            catch (NullReferenceException)
            {
                Console.WriteLine($"W( null ) --> NullReferenceException");
            }

            try
            {
                new Wielomian(new int[0]);
            }
            catch (ArgumentException e)
            {
                Console.WriteLine($"W( int[0] ) --> ArgumentException: {e.Message}");
            }

            Console.WriteLine("== Równość, nierówność ==");

            Console.WriteLine($"W(1, 2).Equals(W(1, 2)) : {(new W(1, 2)).Equals(new W(1, 2))}");
            Console.WriteLine($"wX.Equals(wX) : {wX.Equals(wX)}");
            Console.WriteLine($"wX.Equals(null) : {wX.Equals(null)}");
            Console.WriteLine($"wX.Equals(Object) : {wX.Equals(new Object())}");
            Console.WriteLine($"W(1, 2) == W(1, 2) : {new W(1, 2) == new W(1, 2)}");
            Console.WriteLine($"W(1, 2) == W(2, 1) : {new W(1, 2) == new W(2, 1)}");
            Console.WriteLine($"W(1, 2) != W(2, 1) : {new W(1, 2) != new W(2, 1)}");
            Console.WriteLine($"W(1, 2) == W(0, 1, 2) : {new W(1, 2) == new W(0, 1, 2)}");
            Console.WriteLine($"W(1, 2) != W(0, 1, 2) : {new W(1, 2) != new W(0, 1, 2)}");


            Console.WriteLine("== Operacje arytmetyczne ==");

            var w21 = new W(1, 2, 3);
            var w22 = new W(0, 1, 2);
            Console.WriteLine($"({w21}) + ({w22}) = {w21 + w22}");
            Console.WriteLine($"({w22}) + ({w21}) = {w22 + w21}");
            Console.WriteLine($"({w21}) - ({w22}) = {w21 - w22}");
            Console.WriteLine($"({w22}) - ({w21}) = {w22 - w21}");

            Console.WriteLine($"({w21}) + {10} = {w21 + 10}");
            Console.WriteLine($"{10} + ({w21}) = {10 + w21}");
            Console.WriteLine($"({w21}) - {10} = {w21 - 10}");
            Console.WriteLine($"{10} - ({w21}) = {10 - w21}");

            Console.WriteLine("== Konwersje ==");

            Wielomian w = 10;  //konwersja domyślna z int na Wielomian

            int[] t = (int[])(new W(1));
            Console.WriteLine($"int[{t.Length}]: [{String.Join(',', t)}]");

            int y = (int)(new W(1));
            Console.WriteLine($"int y: {y}");

            int[] t11 = (int[])(new W(1, 2));
            Console.WriteLine($"int[{t11.Length}]: [{String.Join(',', t11)}]");

            try
            {
                int t12 = (int)(new W(1, 2));
            }
            catch (InvalidCastException e)
            {
                Console.WriteLine($"InvalidCastException: {e.Message}");
            }

            Console.WriteLine("== indexer ==");

            Console.WriteLine("W(1,2,3): ");
            for (int i = 0; i <= w21.Stopien; i++)
                Console.WriteLine($"  w{i} = {w21[i]}");

            Console.WriteLine("== enumerator ==");

            Console.Write("W(1,2,3): ");
            foreach (var x in w21)
                Console.Write($"{x} ");
            Console.WriteLine();

            Console.WriteLine("== konstruktor dla string ==");

            Wielomian wS = Wielomian.Parse("3x^2 - 2x^1 + 1");
            Console.WriteLine("Wielomian.Parse(\"3x^2 - 2x^1 + 1\") = {0}", wS);
            Console.WriteLine($"W(3, -2, 1) == Wielomian.Parse(\"3x^2 - 2x^1 + 1\"): {new Wielomian(3, -2, 1) == wS}");

            Console.WriteLine("== Metoda rozszerzająca Eval ==");

            Console.WriteLine($"Metoda rozszerzająca: new W(1,2,1).Eval(2.0) = {new W(1, 2, 1).Eval(2.0)}");

            Console.WriteLine("== lista wielomianów, sortowanie ==");

            var lista = new List<W>
            {
                new W(),
                new W(-2,1,2),
                new W(2,1),
                new W(-2,1),
                new W(-1)
            };
            Console.WriteLine("- lista przed sortowaniem -");
            lista.ForEach( ww => Console.WriteLine(ww) );

            lista.Sort( MyMathExtensions.WielomianPoprzedzaComparison );
            Console.WriteLine("- lista po sortowaniu -");
            lista.ForEach(ww => Console.WriteLine(ww));

            System.Console.WriteLine("== koniec testu ==");
        }
    }
}
```

Podanego kodu w projekcie _console app_ **NIE WOLNO CI ZMIENIAĆ**. Oczywiście, w trakcie implementacji, możesz komentować i odkomentować wybrane fragmenty kodu, sprawdzając poprawność Twoich rozwiązań.

Analizuj podany kod i użyj w implementacji klasy `Wielomian` właściwych nazw i konstrukcji.

Wynik działania podanego kodu dla poprawnej implementacji podano poniżej:

```console
== Test implementacji klasy Wielomian! ==
== Konstrukcja ==
wielomian domyślny W() = 0, stopień = 0
W(-1) = -1, stopień = 0
W(0) = 0, stopień = 0
W(0,0) = 0, stopień = 0
W(1,0) = 1x^1 + 0, stopień = 1
W(1,-1) = 1x^1 - 1, stopień = 1
W(-2, 0, 1, -3) = -2x^3 + 0x^2 + 1x^1 - 3, stopień = 3
W(0, 0, 0, -2, 0, 1, -3) = -2x^3 + 0x^2 + 1x^1 - 3, stopień = 3
wielomian z tablicy = 3x^9 + 1x^8 + 3x^7 + 0x^6 - 2x^5 + 4x^4 + 5x^3 + 1x^2 + 0x^1 + 0, stopień = 9
W( null ) --> NullReferenceException
W( int[0] ) --> ArgumentException: wielomian nie moze być pusty
== Równość, nierówność ==
W(1, 2).Equals(W(1, 2)) : True
wX.Equals(wX) : True
wX.Equals(null) : False
wX.Equals(Object) : False
W(1, 2) == W(1, 2) : True
W(1, 2) == W(2, 1) : False
W(1, 2) != W(2, 1) : True
W(1, 2) == W(0, 1, 2) : True
W(1, 2) != W(0, 1, 2) : False
== Operacje arytmetyczne ==
(1x^2 + 2x^1 + 3) + (1x^1 + 2) = 1x^2 + 3x^1 + 5
(1x^1 + 2) + (1x^2 + 2x^1 + 3) = 1x^2 + 3x^1 + 5
(1x^2 + 2x^1 + 3) - (1x^1 + 2) = 1x^2 + 1x^1 + 1
(1x^1 + 2) - (1x^2 + 2x^1 + 3) = -1x^2 - 1x^1 - 1
(1x^2 + 2x^1 + 3) + 10 = 1x^2 + 2x^1 + 13
10 + (1x^2 + 2x^1 + 3) = 1x^2 + 2x^1 + 13
(1x^2 + 2x^1 + 3) - 10 = 1x^2 + 2x^1 - 7
10 - (1x^2 + 2x^1 + 3) = -1x^2 - 2x^1 + 7
== Konwersje ==
int[1]: [1]
int y: 1
int[2]: [2,1]
InvalidCastException: wielomian nie jest stopnia zerowego
== indexer ==
W(1,2,3):
  w0 = 3
  w1 = 2
  w2 = 1
== enumerator ==
W(1,2,3): 3 2 1
== konstruktor dla string ==
Wielomian.Parse("3x^2 - 2x^1 + 1") = 3x^2 - 2x^1 + 1
W(3, -2, 1) == Wielomian.Parse("3x^2 - 2x^1 + 1"): True
== Metoda rozszerzająca Eval ==
Metoda rozszerzająca: new W(1,2,1).Eval(2.0) = 9
== lista wielomianów, sortowanie ==
- lista przed sortowaniem -
0
-2x^2 + 1x^1 + 2
2x^1 + 1
-2x^1 + 1
-1
- lista po sortowaniu -
-1
0
-2x^1 + 1
2x^1 + 1
-2x^2 + 1x^1 + 2
== koniec testu ==
```
___


Poniższe polecenia dotyczą projektowanej klasy `Wielomian`.

Decyzję o reprezentacji wewnętrznej wielomianu (sposobu zapamiętania współczynników) podejmujesz sam.

Tworząc kod - nie duplikuj go, łącz ze sobą funkcjonalności, wywołując te, które zostały już oprogramowane.

2. Tworzenie wielomianu: **(1 pkt.)**
    * Domyślnym wielomianem jest wielomian zerowy.
    * Tworzenie wielomianu odbywa się na podstawie podania listy wartości współczynników typu `int` - od tego, stojącego przy najwyższej potędze ( \(a_n\) ) do wyrazu wolnego ( \(a_0\) ).
         > Przykładowo, wywołanie konstruktora `Wielmian(2, -3, 0, 1, -2)` spowoduje utworzenie obiektu odpowiadającemu "matematycznemu wielomianowi": \(2x^4 -3x^3 +x -2\).
    * Wielomian można również utworzyć w oparciu o przekazaną tablicę współczynników (typu `int[]`).
         > Przykładowo, dla tablicy `int[] a {2, -3, 0, 1, -2}` utworzony zostanie obiekt odpowiadający "matematycznemu wielomianowi": \(2x^4 -3x^3 +x -2\).
    * Wiodące zera na liście współczynników należy pominąć.
         > Przykładowo, dla tablicy `int[] a {0, 0, 0, 2, -3, 0, 1, -2}` utworzony zostanie obiekt odpowiadający "matematycznemu wielomianowi": \(2x^4 -3x^3 +x -2\).
    * W przypadku próby utworzenia wielomianu z argumentem `null` zgłaszany jest wyjątek `NullReferenceException`.
    * W przypadku próby utworzenia wielomianu dla tablicy o zerowej długości zwracany jest wyjątek `ArgumentException` z komentarzem "wielomian nie może być pusty".

3. Reprezentacja `ToString()` **(1 pkt.)**
    * Zapewnij reprezentację tekstową wielomianu zgodną z notacją algebraiczną (akceptowalną przez większość CAS - _Computer Algebra Systems_) - sugeruj się podanymi przykładami:
      * wielomian stopnia zero: np. dla `W(2)` zwróć `"2"`
      * wielomian stopnia > 2: np.  dla `W(3,-2,1)` zwróć `"3x^2 - 2x^1 + 1"`

4. Równość wielomianów **(1 pkt.)**
    * Dwa wielomiany są sobie równe, jeśli są tego samego stopnia i mają takie same odpowiednie współczynniki.
    * Zaimplementuj poprawnie interfejs `IEquatable<Wielomian>`.
    * Zaimplementuj przeciążone operatory `==` oraz `!=`.

5. Operacje arytmetyczne na wielomianach **(1 pkt.)**
    * Zdefiniuj przeciążone operatory dodawania wielomianów ( `+` ) oraz odejmowania wielomianów ( `-` ).
    * Zapewnij poprawne działanie dodawania/odejmowania liczby całkowitej do wielomianu.

6. Operacje konwersji **(1 pkt.)**
    * Zdefiniuj konwersję niejawną (_implicit_) z typu `int` na `Wielomian`
    * Zdefiniuj konwersję jawną (_explicit_) z typu `Wielomian`:
      * na typ `int[]`, zwracającą tablicę współczynników wielomianu, w kolejności od wyrazu zerowego (indeks `0`) do ostatniego,
      * na typ `int` zwracającą wyraz wolny wielomianu. Jeśli wielomian nie jest stopnia `0` zgłaszany jest wyjątek `InvalidCastException` z komunikatem "wielomian nie jest stopnia zerowego".

7. Przeglądanie wielomianu - indexer **(1 pkt.)**
    * Zaimplementuj mechanizm przeglądania (tylko do odczytu, bo wielomian ma być _immutable_) współczynników wielomianu poprzez odwołanie się do indeksów (`w[i]` oznacza _i_-ty współczynnik wielomianu `w`).  

8. Przeglądanie wielomianu - pętla `foreach` **(1 pkt.)**
    * Zaimplementuj mechanizm przeglądania współczynników wielomianu za pomocą pętli `foreach` w kolejności od wyrazu wolnego do współczynnika przy najwyższej potędze.

9.  Metoda parsująca ze `string` **(1 pkt.)**
    * Zaimplementuj statyczną metodę `Parse` komplementarną do tekstowej reprezentacji wielomianu (`ToString()`). Przykładowo `W(3, -2, 1) == W.Parse("3x^2 - 2x^1 + 1")`.

10. Pamiętaj o zapewnieniu pełnej niezmienniczości obiektom klasy `Wielomian` oraz o zapieczętowaniu klasy **(1 pkt.)**

___

Poniższe polecenia dotyczą projektu testów jednostkowych **(1 pkt.)**

11. Utwórz testy jednostkowe dla:
    * _properties_ `Stopien`,
    * operatora dodawania wielomianów.

___

Poniższe polecenia dotyczą projektu typu _console app_.

12. Metoda rozszerzająca - `Eval` **(2 pkt.)**
    * Utwórz metodę rozszerzającą klasę `Wielomian` o nazwie `Eval`, która dla argumentu typu `double` zwróci obliczoną wartość wielomianu dla tego argumentu.
        > Na przykład, dla wielomianu `w = new W(1,2,1)` funkcja `w.Eval(2.0)` zwróci `9.0`.

13. Sortowanie listy wielomianów **(2 pkt.)**
    * Utwórz listę kliku różnych wielomianów (różnego stopnia o różnych współczynnikach, w różnej kolejności).
    * Wypisz wielomiany umieszczone na liście (po jednym w wierszu)
    * Posortuj tę listę według następującego kryterium:
        `w1` poprzedza `w2` jeśli:
        * stopień `w1` < stopień `w2`
        * jeśli stopnie są równe, to decydują wartości współczynników wielomianów - analizując od najwyższej potęgi do wyrazu wolnego (rosnąco)
        > Przykład 1: dla wielomianów `w1(1,2,1)` oraz `w2(2,1)`, `w2` poprzedza `w1`.
        > Przykład 2: dla wielomianów `w1(1,2,1)` oraz `w2(1,2,1)`, oba są sobie równe
        > Przykład 3: dla wielomianów `w1(1,2,1)` oraz `w2(2,0,0)`, `w2` poprzedza `w1`.
    * Kryterium sortowania dostarcz jako delegat `Comparison<Wielomian>`.
    * Wypisz listę posortowaną.
___

Do oceny przesyłasz _solution_ z projektami, skompresowane w formie archiwum ZIP. Przed spakowaniem sprawdź, czy kod się kompiluje. Kod z błędami nie będzie oceniany.

Rozmiar klasy `Wielomian` - w moim przypadku - nie przekroczył 150 linii kodu, przy zachowaniu standardowego, automatycznego formatowania C#. Nie zwracałem uwagi na maksymalne uproszczenie czy kompresję zapisu.

#### Bonus

* Zmodyfikuj `ToString()` tak, aby tekstową reprezentacją wielomianu był zapis algebraiczny z pewnymi matematycznymi uproszczeniami:
  * współczynnik `0` powoduje, że jednomian w zapisie wielomianu znika (np. \(0x^2 \))
  * współczynnik `1` jednomianu nie jest zapisywany (np. zamiast \(1x^2\) zapiszemy \(x^2\))
  * potęga `1` zwyczajowo nie jest zapisywana (np. zamiast \(x^1\) zapiszemy \(x\))
  > Przykład: Wielomian `W(-2,0,1,0)` zamiast \(-2x^3 + 0x^2 + 1x^1 + 0\) zapiszemy \(-2x^3 + x\).

* Zmodyfikuj metodę `Parse` tak, aby poprawnie interpretowała również ten sposób tekstowej reprezentacji wielomianu.

* Zaimplementuj konstruktor tworzący `Wielomian` w oparciu o tak zadany napis.
