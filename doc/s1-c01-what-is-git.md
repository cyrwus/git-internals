### Czym jest *Git*? 

*Git* to bezmyślny tropiciel zawartości. Taki jest chyba najlepszy jego opis - nie myśl o nim w kontekście „podobny do (i tu wstaw swój ulubiony system SCM), tylko że …”, lecz jak o naprawdę interesującym systemie plików.  

*Git* śledzi zawartości - plików i katalogów. 
Jego sercem jest zbiór prostych narzędzi, które implementują hierarchiczny zapis historii oraz system zarządzania zawartością. 
Jest po prostu używany jako system SCM, choć nie do końca w takim celu został zaprojektowany. 

> Pod wieloma względami możesz postrzegać git jako system plików — jest adresowalny zawartością i ma mechanizmy wersjonowania, ale tak naprawdę zaprojektowałem go, podchodząc do zagadnienia z punktu widzenia gościa od systemu plików (hej, w końcu zajmuję się jądrem systemowym!) i nie mam absolutnie żadnego interesu w tworzeniu tradycyjnego systemu SCM.<br>  
— Linus ([*Mailing list ARChives*](http://marc.info/?l=linux-kernel&m=111314792424707))

W większości systemów SCM, zapis nowej wersji projektu oznacza zapis „delty” albo różnicy zawartości. 
Gdy *Git* tworzy zapis nowej wersji projektu, zapamiętuje nowe *drzewo*<sup>1</sup> — garść *blob'ów*<sup>2</sup> z zawartością zmienionych plików oraz kolekcję wskaźników, co da się z powrotem rozwinąć w pełen katalog zmodyfikowanych plików i podkatalogów. 
Dla określenia różnicy między dwiema wersjami, nie sumuje on wszystkich delt, po prostu patrzy na dwa drzewa i wykonuje od nowa analizę różnicową.  

To wpływa zasadniczo na łatwość rozproszenia systemu — nie ma dylematów jak zastosować złożone serie delt, lecz po prostu transferuje się katalogi i ich zawartość pomiędzy użytkownikiem który je posiada, a tym który ich zażądał. 
Chodzi o wydajność — tylko raz przechowuje się identyczne pliki i katalogi, które można kompresować i przesyłać w postaci spakowanej<sup>3</sup> — ale sama koncepcja jest tu bardzo prosta. W samym sercu systemu *Git* jest naiwnie prosty. 


<br><sup>____________________</sup>
<br><sup>1</sup> *przyp.* chodzi o strukturę hierarchiczną
<br><sup>2</sup> *przyp.* mowa o obiektach binarnych
<br><sup>3</sup> *przyp.* kompresją różnicową
