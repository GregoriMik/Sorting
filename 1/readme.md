https://pl.wikipedia.org/wiki/Sortowanie_szybkie

Algorytm

Z tablicy wybiera się element rozdzielający, po czym tablica jest dzielona na dwa fragmenty: do początkowego przenoszone są wszystkie elementy nie większe od rozdzielającego, do końcowego wszystkie większe. Potem sortuje się osobno początkową i końcową część tablicy. Rekursja kończy się, gdy kolejny fragment uzyskany z podziału zawiera pojedynczy element, jako że jednoelementowa tablica nie wymaga sortowania.

Jeśli przez l oznacza się indeks pierwszego, a przez r – ostatniego elementu sortowanego fragmentu tablicy, zaś przez i – indeks elementu, na którym tablica została podzielona, to procedurę sortowania można (w dużym uproszczeniu) przedstawić następującym pseudokodem:

  PROCEDURE Quicksort(tablica, l, r)
  BEGIN
    IF l < r THEN { jeśli fragment dłuższy niż 1 element }
      BEGIN
        i := PodzielTablice(tablica, l, r); { podziel i zapamiętaj punkt podziału }
        Quicksort(tablica, l, i-1);         { posortuj lewą część }
        Quicksort(tablica, i+1, r);         { posortuj prawą część }
      END
  END

  {wybiera element, który ma być użyty do podziału
   i przenosi wszystkie elementy mniejsze na lewo od
   tego elementu, a elementy większe lub równe, na prawo
   od wybranego elementu }
  PROCEDURE PodzielTablice(tablica, l, r)
  BEGIN
     indeksPodzialu := WybierzPunktPodzialu(l, r); {wybierz element, który posłuży do podziału tablicy}
     wartoscPodzialu := tablica[indeksPodzialu]; {zapamiętaj wartość elementu}
     Zamien(tablica, indeksPodzialu, r); {przenieś element podziału na koniec tablicy, aby sam nie brał udziału w podziale}

     aktualnaPozycja := l;
     FOR i:=l TO r-1 DO {iteruj przez wszystkie elementy, jeśli element jest mniejszy niż wartość elementu podziału dodaj go do "lewej" strony}
     BEGIN
         IF tablica[i] < wartoscPodzialu THEN
         BEGIN
             Zamien(tablica, i, aktualnaPozycja);
             aktualnaPozycja := aktualnaPozycja + 1;
         END
     END
     Zamien(tablica, aktualnaPozycja, r); {wstaw element podziału we właściwe miejsce}
     return aktualnaPozycja;
  END

  { podstawowa implementacja wyboru punktu podziału - wybiera element "środkowy" w tablicy }
  PROCEDURE WybierzPunktPodzialu(l, r)
  BEGIN
     return l + (r-l) div 2;
  END

  { zamienia miejscami elementy w komórkach i1, i2 }
  PROCEDURE Zamien(tablica, i1, i2)
  BEGIN
    IF i1<>i2 THEN
    BEGIN
     aux := tablica[i1];
     tablica[i1] := tablica[i2];
     tablica[i2] := aux;
    END
  END

Właściwe działanie algorytmu wymaga, aby procedura PodzielTablice pozostawiała element rozdzielający na końcu lewej części uzyskanej z podziału. Wówczas element ten znajduje się na swojej ostatecznej pozycji i nie podlega dalszemu przetwarzaniu – rekurencyjne wywołania Quicksort nie obejmują indeksu i. Tym samym do dalszego przetwarzania przekazuje się o jeden element mniej, co gwarantuje zakończenie rekurencji. 

=================================================================================
https://en.wikipedia.org/wiki/Quicksort

Algorithm

For proper operation of the algorithm, the SplitArray procedure must leave the pivot at the end of the left section obtained from the split. This element is then in its final position and is not processed further - recursive Quicksort calls do not include the index i. Thus, one less element is passed for further processing, which guarantees the termination of recursion. 
