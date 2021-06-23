# PP-E2
 
### F#: Napisz funkcję, która obliczy wartość wariancji bez powtórzeń zgodnie ze wzorem n!/(n-k)!

```
let WariancjeBezPowtorzen n k = 
    let licznik = silnia n
    let mianownik = silnia (n - k)

    licznik / mianownik
```
### F#: Napisz funkcję, która określi ile razy w danym łańcuchu znaków wystąpiły dowolne cyfry. Przykładowo dla łańcucha 'Ala 123 ma k1ota' funkcja powinna zwrócić 4.

```
 open System

let rec liczZnaki slowo n ascii =
    let znak = (char(ascii))
    let rec liczZnak (slowo:string) (znak:char) i suma= 
        if i=slowo.Length then
            printfn "Wynik %A %A" znak suma
        else
            if (slowo.[i] = znak) then
                liczZnak slowo znak (i+1) (suma+1)
            else
                liczZnak slowo znak (i+1) suma
    liczZnak slowo znak 0 0

    if n < 1 then
        printfn "Koniec"
    else
        liczZnaki slowo (n-1) (ascii+1)


[<EntryPoint>]
let main argv =
    printfn "Podaj zdanie"  
    let tekst = (string(Console.ReadLine()))
    let n = 9
    let ascii = 48
    (liczZnaki tekst n ascii)
    0 // return an integer exit code 
```

### F#: Napisz program, który wczytując od użytkownika liczby z klawiatury zapamięta liczby parzyste. (Wprowadzanie zakończ, jeżeli użytkownik poda 0). Po zakończeniu wprowadzania danych program powinien wyświetlić je w odwrotnej kolejności (od ostatniej wprowadzonej do pierwszej).

```
let bezpiecznePodawanieLiczby =
    try 
        Some(int(Console.ReadLine()))
    with
        | :? System.FormatException ->  None


let podajLiczbe () = 
    let lista: int list = []

    let rec dodajLiczbe lista =   
        Console.Write "Podaj liczbe: "

        let v = bezpiecznePodawanieLiczby

        match v with
        | Some(x) -> 
            if(x <> 0 && x % 2 = 0) then
                    dodajLiczbe (lista @ [x])
                elif (x = 0) then
                    Console.WriteLine "Odwrocona lista wpisanych liczb parzystych: "
                    lista |> List.rev |> List.iter (fun v -> printfn "%d" v)
                else    
                    dodajLiczbe lista
        | None -> printfn "Podano zły format!"; 

    dodajLiczbe lista
```


### F#: Zdefiniuj nowy typ danych reprezentujący drzewo binarne. Następnie napisz program, który wyświetli elementy tego drzewa w kolejności postorder. Zademonstruj jego działanie.

```
 open System

[<EntryPoint>]
let main argv =
    let rec funPostOrder = function
    | Puste -> ()
    | Wezel(x, l, p) -> 
    
        match l with
           | Wezel(_, _, _) -> funPostOrder l
           | Puste -> ()
    
        match p with
            | Wezel(_, _, _) -> funPostOrder p
            | Puste -> ()
    
        printfn "%d" x
    0 
```
### C#: Stwórz klasy na podstawie przykładów:
```
    var ksiazki = new [] {
         new Ksiazka {Tytul = "Pan Tadeusz", RokWydania = 1998, Gatunek = 1, Cena = 30},
         new Ksiazka {Tytul = "Potop", RokWydania = 1991, Gatunek = 1, Cena = 40},
         new Ksiazka {Tytul = "W pustyni i w puszczy", RokWydania = 1990, Gatunek = 2, Cena = 30},
         new Ksiazka {Tytul = "Lalka", RokWydania = 1990, Gatunek = 1, Cena = 50},
         new Ksiazka {Tytul = "Programowanie funkcyjne w języku C#", RokWydania = 2019, Gatunek = 3, Cena = 71.20},
         new Ksiazka {Tytul = "Programowanie funkcyjne z JavaScriptem", RokWydania = 2017, Gatunek = 3, Cena = 29.40},};
         var gatunki = new [] {
         new Gatunek { id = 1, Nazwa = "Literatura piękna" },
         new Gatunek { id = 2, Nazwa = "Przygodowa" },
         new Gatunek { id = 3, Nazwa = "Programowanie" },
         new Gatunek { id = 4, Nazwa = "Projektowanie stron WWW" }
         };
```

### Napisz zapytanie Linq, które zwróci obiekt anonimowy zawierający nazwę gatunku oraz listę tytułów książek, do których jest przypisany
 
```
using System;
using System.Linq;
using System.Collections.Generic;
using System.Text;

namespace zadanie3
{
    public class Ksiazka
    {
        public string Tytul { get; set; }
        public int RokWydania { get; set; }
        public int Gatunek { get; set; }
        public double Cena { get; set; }


        public Ksiazka(string Tytul, int RokWydania, int Gatunek, double Cena)
        {
            this.Tytul = Tytul;
            this.RokWydania = RokWydania;
            this.Gatunek = Gatunek;
            this.Cena = Cena;
        }
    }

    public class Gatunek
    {
        public int id { get; set; }
        public string Nazwa { get; set; }

        public Gatunek(int id, string Nazwa)
        {
            this.id = id;
            this.Nazwa = Nazwa;
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            var ksiazki = new[] {

                new Ksiazka("Pan Tadeusz", 1998, 1, 30),
                new Ksiazka ("Potop", 1991, 1, 40),
                new Ksiazka ("W pustyni i w puszczy", 1990, 2, 30),
                new Ksiazka ("Lalka", 1990, 1, 50),
                new Ksiazka ("Programowanie funkcyjne w języku C#", 2019, 3, 71.20),
                new Ksiazka ("Programowanie funkcyjne z JavaScriptem", 2017, 3, 29.40)
            };

            var gatunki = new[] {

                new Gatunek (1, "Literatura piękna"),
                new Gatunek (2, "Przygodowa"),
                new Gatunek (3, "Programowanie" ),
                new Gatunek (4, "Projektowanie stron WWW")

            };

            for (int i = 0; i <= 4; i++)
            {
                var select = (from k in ksiazki where k.Gatunek == gatunki[i].id select k);
                Console.WriteLine(select);
            }
        }
    }
}
```

### C#: Stwórz generyczną klasę Lista implementującą listę łączoną i przechowującą wartość dowolnego typu. Stwórz ją w taki sposób, aby każdy węzeł był elementem tylko do odczytu. Następnie napisz metodę, która będzie poszukiwała elementu najmniejszego (dla dowolnego typu). Zademonstruj działanie klasy.

```
using System;

public class Wezel<T> where T : IComparable<T> {
    public Wezel<T> next;
    public T data;
}

public class Lista<T> where T : IComparable<T> {
    protected Wezel<T> head;

    public void DrukujWszystko() {
        Wezel<T> aktualny = head;
        while (aktualny != null) 
        {
            Console.WriteLine(aktualny.data);
            aktualny = aktualny.next;
        }
    }

    public void Dodaj(T data) {
        Wezel<T> nowy = new Wezel<T>();
        nowy.data = data;
        nowy.next = head;

        head = nowy;
    }

    public T ZnajdzNajmniejszy() {
        T najmniejszy = head.data;
        
        Wezel<T> aktualny = head;
        while (aktualny.next != null) 
        {
            try {
                if (aktualny.data.CompareTo(aktualny.next.data) > 0) {
                    najmniejszy = aktualny.next.data;
                }
            } catch {
                throw new ArgumentException("Obiekty nie moga byc porownywane");
            }

            aktualny = aktualny.next;
        }

        return najmniejszy;
    }
}

class Zadanie4 {
    static void Main(string[] args) {
        Lista<int> lista = new Lista<int>();
        
        lista.Dodaj(12);
        lista.Dodaj(23);
        lista.Dodaj(3);

        lista.DrukujWszystko();
        Console.WriteLine();
        Console.WriteLine(lista.ZnajdzNajmniejszy());
        Console.WriteLine();

        Lista<string> lista2 = new Lista<string>();
        
        lista2.Dodaj("abc");
        lista2.Dodaj("aaaddas");
        lista2.Dodaj("csad");

        lista2.DrukujWszystko();
        Console.WriteLine();
        Console.WriteLine(lista2.ZnajdzNajmniejszy());
    }
}
```

