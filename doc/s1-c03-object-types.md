## Typy obiektów *Git'a*

W obiektach *Git'a* zawarte są rzeczywiste dane i właśnie z nich składa się repozytorium. 
Obiekty w *Git'cie* dzielimy na cztery typy główne, z których pierwsze trzy są kluczowe dla zrozumienia głównych funkcji *Git'a*.

Wszystkie typy obiektów zapisywane są w bazie obiektów, znajdującej się w **katalogu**<sup>1</sup> *Git'a*. Każdy obiekt jest skompresowany (Zlib'em) i zaadresowany wartością SHA-1, wyliczaną z jego zawartości poprzedzonej małym nagłówkiem. W przykładach będę używał dla uproszczenia pierwszych 6 znaków ciągu SHA-1, ale w rzeczywistości zawsze mają one długość 40 znaków.

> SHA oznacza *Secure Hash Algorithm*. SHA zwraca dla konkretnej wartości unikalny i jednoznaczny identyfikator o stałej długości. 
SHA-1 zastąpił SHA-0 i jest powszechnie używanym algorytmem.<br>
Więcej o tym znajdziesz w [Wikipedii](http://en.wikipedia.org/wiki/SHA1).

Aby zaprezentować parę przykładów, utworzymy małą biblioteczkę *ruby* (mającą zapewnić proste wiązania z *Git'em*) i zachowamy ten projekt w repozytorium *Git'a*. 
Oto układ naszego projektu:

![Rys. A](https://github.com/pluralsight/git-internals-pdf/blob/master/artwork/s1/layout.png)<br>
Rys. A - Prosty projekt zawierający pliki i katalogi

Zobaczmy co zrobi *Git*, gdy projekt ten zatwierdzimy do repozytorium.

---
### *Blob* (obiekt binarny)

W *Git'cie*, zawartości plików zapisywane są w *blob'ach*.

![Rys. B](https://github.com/pluralsight/git-internals-pdf/blob/master/artwork/s1/blobs.png)<br>
Rys. B - Pliki zapisywane są jako *blob'y*

Ważne jest by zrozumieć, że zachowywane są *zawartości*, a nie pliki. Nazwy i atrybuty plików nie są zapisywane w *blob'ach*, tylko ich zawartość. 

To oznacza, że jeśli gdziekolwiek w projekcie są dwa pliki, które zawierają dokładnie to samo, ale mają różne nazwy, *Git* zachowa *blob* tylko raz. To również oznacza, że podczas transferów repozytorium, np. przy *clone* lub *fetch*, *Git* prześle *blob* tylko raz, a następnie rozwinie go na wiele plików podczas wykonania *checkout'a*.

![Rys. C](https://github.com/pluralsight/git-internals-pdf/blob/master/artwork/s1/blob-expand.png)<br>
Rys. C - Zawartość *blob'a* po rozpakowaniu

---
### *Tree* (drzewo)

Katalogi mają w *Git'cie* prosty odpowiednik — *drzewa*.

![Rys. D](https://github.com/pluralsight/git-internals-pdf/blob/master/artwork/s1/trees.png)<br>
Rys. D - Drzewa to wskaźniki do *blob'ów* i innych drzew

Drzewo to zwykła lista przynależnych do niego poddrzew i *blob'ów*, wraz z ich nazwami i atrybutami. Obiekt tego typu zawiera bardzo prosty zapis tekstowy z listą atrybutów, typów, nazw oraz wartości SHA dla każdego elementu przynależnego.

![Rys. E](https://github.com/pluralsight/git-internals-pdf/blob/master/artwork/s1/tree-expand.png)<br>
Rys. E - Drzewo po rozpakowaniu

---
### *Commit* (zatwierdzenie)

No więc, skoro możemy w *Git'cie* przechowywać określone drzewa zawartości, to skąd bieże się „historia” zawartości? Jaki jest „system przechowywania historii drzew”? Odpowiedzią jest obiekt typu *commit*.

![Rys. F](https://github.com/pluralsight/git-internals-pdf/blob/master/artwork/s1/commit.png)<br>
Rys. F - *Commit*, jako wskaźnik drzewa

*Commit* to bardzo prosty i podobny do drzewa obiekt. Po prostu jest wskaźnikiem do drzewa, a dodatkowo zawiera następujące dane: *author* (autor), *commiter* (nazwa zatwierdzającego), *message* (opis *commit'u*) oraz dowolna lista rodziców – czyli *commit'ów* bezpośrednio poprzedzających ten *commit*.

![Rys. G](https://github.com/pluralsight/git-internals-pdf/blob/master/artwork/s1/commit-expand.png)<br>
Rys. G - Pierwszy *commit* po rozpakowaniu

Ponieważ był to mój pierwszy *commit*, lista rodziców jest pusta. Jeśli zrobię zatwierdzenie drugi raz, obiekt *commit* będzie wyglądał mniej więcej tak:

![Rys. H](https://github.com/pluralsight/git-internals-pdf/blob/master/artwork/s1/commit-expand2.png)<br>
Rys. H - Następny (potomny) *commit* po rozpakowaniu

Czy zauważyłeś, że w tym *commit'cie* rodzic określony jest takim samym SHA-1, jaki miał nasz poprzedni *commit*?
W większości przypadków *commit* będzie miał tylko jednego rodzica — tak jak w naszym przykładzie, ale jeśli np. połączysz dwie gałęzie, powstały *commit* wskaże dwóch rodziców.

> Obecny rekord w projekcie jądra systemu *Linux* wynosi 12 gałęzi scalonych w pojedynczy *commit*!

---
### *Tag* (znacznik)

Ostatnim typem obiektów, które znajdziesz w bazie danych *Git*, jest *znacznik*. Jest to obiekt, który pozwala nadać niezmienną skróconą nazwę konkretnemu *commit'owi*. Określa on: *object* (wskaźnik do obiektu oznaczanego), *type* (typ obiektu oznaczanego), *tag* (treść oznaczenia), *tagger* (nazwa oznaczającego) oraz wiadomość. Zazwyczaj, typem obiektu jest *commit*, wskaźnikiem obiektu jest SHA-1 *commit'a* który oznaczasz. Znacznik może mieć również sygnaturę GPG, zapewniającą integralność kryptograficzną wydania lub wersji.

![Rys. I](https://github.com/pluralsight/git-internals-pdf/blob/master/artwork/s1/tag-expand.png)<br>
Rys. I - Znacznik po rozpakowaniu

O znacznikach oraz o tym, jak różnią się one od gałęzi (które również są wskaźnikami do *commit'ów*, ale nie są przechowywane jako obiekty) powiemy trochę więcej w następnej części. Zbierzemy tam wszystko w całość, aby dostrzec, jak omówione obiekty są wzajemnie powiązane funkcjonalnie.


<br><sup>____________________</sup>
<br><sup>1</sup> standardowo, katalog *Git'a* to folder o nazwie .git
