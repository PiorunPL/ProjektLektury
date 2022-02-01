<i> Projekt zespołowy, Podstawy reprezentacji i analizy danych, Informatyka Stosowana 2021Z/2022L, Politechnika Warszawska;</i>
    
<i>Data: 01.02.2022r.</i>

# Rozpoznawanie autora utworu literackiego na podstawie treści utworu z wykorzystaniem worka słów
* Autorzy: Jakub Maciejewski, Michał Ziober, Maja Nagarnowicz, Miłosz Moroz
* <a href="https://github.com/PiorunPL/ProjektLektury" >Repozytorium projektu</a>

## Cel projektu
Celem projektu było stworzenie programu, który na podstawie wybranego fragmentu utworu literackiego rozpozna jego autora. 

Program jest w stanie oszacować pradopodobieństwo przynależności danego fragmentu tesktu do jednego z wybranych przez nas autorów:
 * Adam Mickiewicz
 * Juliusz Słowacki  
 * Krzysztof Kamil Baczyński  
 * Henryk Sienkiewicz   
 * Bolesław Prus  
 * Aleksander Fredro   
 * Maria Konopnicka
 * Jan Kochanowski   
 * Tadeusz Borowski   
 * Sofokles    
 * Stefan Żeromski
 
 ## Worek słów
 Dla każdego z powyższych autorów wybraliśmy po kilka stworzonych przez niego utworów 
(<a href="https://wolnelektury.pl/" >źródło utworów</a>, listę wybranych utworów można znaleźć w pliku `FileDownloader.ipynb` w  <a href="https://github.com/PiorunPL/ProjektLektury" >naszym repozytorium</a>), a następnie na podstawie tych tekstów utworzyliśmy worek słów odpowiadający tym autorom (informacja o słowach, które wystąpiły w danych utworach autora oraz przyporządkowana im liczba wystąpień - suma dla wszystkich tekstów).

Worki te można znaleźc w katalogu `/Bags`.

## Dopasowywanie fragmentu do autora
Procedura dopasowania przekazanego fragmentu utworu literackiego do konkretnego autora:
1. **Tworzymy worek słów dla podanego fragmentu utworu literackiego**
2. **Analizujemy procentowe występowanie słów w danym fragmencie** - dla każdego słowa przyporządkowujemy jego częstość występowania w danym fragmencie
(gdzie częstość wystąpienia to iloraz liczby wystąpień słowa w tekście i sumy wystąpień wszystkich słów w tekście)
3. **Dla każdego słowa z worka słów poszczególnego autora obliczamy częstość jego wystąpienia**
(gdzie częstość wystąpienia to iloraz liczby wystąpień słowa w wybranych utworach autora i sumy wystąpień wszystkich słów w utworach autora)
4. **Liczymy odległości pomiędzy procentową częstością wystąpień słów w przekazanym fragmencie oraz częstością wystąpień tych samych słów we wszystkich wybranych tekstach danego autora**, gdzie odległość to wartość bezwględna z różnicy tych częstości dla danego słowa
5. **Dla każdego autora sumujemy otrzymane odległości**
6. **Na podstawie tych sum szacujemy prawdopodobieństwo przynależności danego fragmentu tekstu do jednego z autorów**

## Wykorzystane modele <a id='modele'></a>
W naszym projekcie wykorzystaliśmy kilka modeli wyznaczania najbardziej prawdopodobnego autora fragmentu. Poniżej przestawiamy ich konfigurację:

* **Model pierwszy**:
   -  Worki słów tworzone są dla każdego autora (a nie dla pojedynczej lektury)
   -  Worki słów podlegają lematyzacji
   -  Z worków słów usuwane są słowa stopu
   
   
* **Model drugi**:
   -  Worki słów tworzone są dla każdego autora (a nie dla pojedynczej lektury)
   -  Worki słów podlegają lematyzacji
   -  Z worków słów nie są usuwane słowa stopu
   
   
* **Model trzeci**:
   -  Worki słów tworzone są dla każdego autora (a nie dla pojedynczej lektury)
   -  Worki słów nie podlegają lematyzacji
   -  Z worków słów są usuwane słowa stopu
   
   
* **Model czwarty**:
   -  Worki słów tworzone są dla każdego autora (a nie dla pojedynczej lektury)
   -  Worki słów nie podlegają lematyzacji
   -  Z worków słów nie są usuwane słowa stopu
   
   
* **Model piąty**:
   -  Worki słów tworzone są dla każdego autora (a nie dla pojedynczej lektury)
   -  Worki słów podlegają lematyzacji
   -  W workach słów znajdują się **tylko** słowa stopu
   
   
* **Model szósty**:
   -  Worki słów tworzone są dla każdego autora (a nie dla pojedynczej lektury)
   -  Worki słów nie podlegają lematyzacji
   -  W worach słów znajdują się **tylko** słowa stopu
   
  ## Struktura projektu
  Struktura plików w <a href="https://github.com/PiorunPL/ProjektLektury" >naszym repozytorium</a>:

* Foldery w repozytorium:

    * `/Bags` - worki słów
        * `/BagOfWords_noStopWords_Lemma` - worki słów bez uwzględnienia słów stopu, z lematyzacją
        * `/BagOfWords_noStopWords_NotLemma` - worki słów bez uwzględnienia słów stopu, bez lematyzacji
        * `/BagOfWords_onlyStopWords_Lemma` - worki słów uwzględniające tylko słowa stopu, z lematyzacją
        * `/BagOfWords_onlyStopWords_NotLemma` - worki słów uwzględniające tylko słowa stopu, bez lematyzacji
        * `/BagOfWords_withStopWords_Lemma` - worki słów z uwzględnienieniem słów stopu, z lematyzacją
        * `/BagOfWords_withStopWords_NotLemma` - worki słów z uwzględnienieniem słów stopu, bez lematyzacji
    * `/Fragments` - fragmenty z wybranych utworów literackich do testów; 108 fragmentów z 54 książek


* Pliki w repozytorium

    * `Dokumentacja.ipynb` - dokumentacja projektu
    * `FileDownloader.ipynb` - skrypt do pobierania książek ze strony + spis wykorzystanych utworów
    * `Measures.ipynb` - funkcje pomocnicze do obliczania odległości i najbardziej prawdopodobnych autorów fragmentu
    * [Modele](#modele):
        * `Model1.ipynb` - model pierwszy
        * `Model2.ipynb` - model drugi
        * `Model3.ipynb` - model trzeci
        * `Model4.ipynb` - model czwarty
        * `Model5.ipynb` - model piąty
        * `Model6.ipynb` - model szósty
    * `WordBag.ipynb` - funkcje pomocnicze do tworzenia worków słów oraz ich zapisu i odczytu z pliku + do lematyzacji
    * `stopWords.txt` - lista słów stopu

## Wykorzystane importy 
#### SpaCy - do procesu lematyzacji wykorzystany został pakiet spacy. 
* <a href="https://spacy.io/" >Link</a> do oficjalnej strony pakietu
* <a href="http://gatak.pl/2020/12/27/spacy-po-polsku-lematyzacja/" >Tutorial</a>, z którego skorzystaliśmy

####  Ipynb - dzięki temu pakietowi mogliśmy stworzyć lepszą strukturę projektu, podzielić go na różne pliki
* <a href="https://github.com/ipython/ipynb" >Link</a> do repozytorium pakietu 

#### Inne, standardowe pakiety 

## Analiza wyników i wnioski
###### Do testów skuteczności modelów przygotowaliśmy 108 fragmentów utworów literackich. Sa to fragmenty utworów, na podstawie których budowaliśmy worki słów dla wybranych przez nas autorów. Z każdego utworu (było ich 54) pobraliśmy po dwa fragmenty - jednek krótszy, drugi dłuższy. Fragmenty te można znaleźć w katalogu `/Fragments`. 
###### Skuteczność modelu to stosunek liczby poprawnych oszacowań autora fragmentu do wszystkich prób pomnożone przez 100%.
###### Suma procent poprawnych autorów  to suma prawdopodobieństw oszacowanych przez model dla autora danego fragmentu w testach przeprowadzanych na wszystkich 108 fragmentach.
###### Wnioski:
* **Najlepszym modelem okazał się być model trzeci - skuteczność ok. 80%** (worki słów nie podlegają lematyzacji, oraz są usuwane słowa stopu)

* Niewiele gorszym modelem okazał się być **model pierwszy - skuteczność ok. 79.6%** (różniący się od modelu 3 wykorzystaniem lematyzacji). 

* **Najgorszym modelem okazał się być model piąty - skuteczność ok. 62%** (worki słów podlegają lematyzacji, znajdują się w nich tylko słowa stopu), co zgadza się z naszą intuicją. Słowa stopu są najmniej charakterystycznymi słowami pozwalającymi ocenić autora tekstu, są często stosowane przez wszystkich autorów jako nierozłączna część wielu zdań w języku polskim. 

* **Model szósty** (różniący się od modelu 5 tylko brakiem lematyzacji) miał identyczną skuteczność, co model 5, miał jedynie większą sumę procentów poprawnych autorów. Możemy więc dojść do wniosku, że nasz program jest najmniej wiarygodny, gdy szacuje autora tekstu tylko i wyłączenie na podstawie słów stopu. Oba modele nie usuwają słów stopu, 

* **Modele drugi i czwarty osiągnęły taką samą skuteczność ok. 77.8%**, przy czym model 4 miał nieco większą sumę procentów poprawnych autorów (nie wykorzystywał on lematyzacji).

* Dla krótszych fragmentów szacowania programu są mniej dokładne. Czym dłuższy fragment tym zazwyczaj łatwiej dopasować autora danego fragmentu.
* Dla modeli, które nie korzystają tylko ze słów stopu, często możemy zauważyć, że program oblicza duże prawdopobieństwo dla autora, który pisał o podobnej tematyce co oryginalny autor lub żył i tworzył w zbliżonym czasie.
