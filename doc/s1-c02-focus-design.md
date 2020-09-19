## Ukierunkowanie i forma projektu

Obmyślając i tworząc *Git'a* programiści - w tym Linus, a zwłaszcza on - skupili się na wielu obszarach.<br>
Mogło być wiele rzeczy, w których *Git* nie jest dobry, ale te rzeczy są tym, w czym *Git* jest bardzo dobry.

### Rozwój nieliniowy 
*Git* jest zoptymalizowany na tanie<sup>1</sup> i wydajne tworzenie w projekcie rozgałęzień i scaleń. 
Jest stworzony do jednoczesnej pracy wielu osób, gdzie odgałęzienia projektu rozwijane są indywidualnie i podlegają ciągłym procesom scalania i rozgałęziania. Z tego względu, rozgałęzianie jest tu niesamowicie tanie, a scalanie jest niezwykle łatwe.

### Rozwój rozproszony
*Git* został stworzony aby uprościć programowanie rozproszone. W *Git'cie* nie ma czegoś takiego jak repozytorium specjalne albo centralne - każdy klon jest w zasadzie równorzędny i właściwie mógłby w każdej chwili zastąpić inny. Może działać całkowicie offline lub z setkami zdalnych repozytoriów, do których można przesyłać / albo z których można pobierać, za pomocą kilku prostych i zestandaryzowanych protokołów.

### Wydajność
*Git* jest bardzo wydajny. W porównaniu z wieloma innymi systemami SCM<sup>2</sup>, wydaje się wręcz niewiarygodnie szybki. 
Większość operacji ma charakter lokalny, co redukuje niepotrzebne obciążenie sieci. 
Repozytoria są zazwyczaj kompresowane bardzo wydajnie, czego skutkiem jest nierzadko ich zaskakująco mały rozmiar.

> Repozytorium *Ruby on Rails*, które zawiera pełną historię tego projektu tzn. każdą wersję każdego pliku, zajmuje w *Git'cie* około 13 MB, czyli nie więcej niż dwukrotność pojedynczej wersji tego projektu (~9 MB).
Ten sam projekt w repozytorium *Subversion* zajmuje na serwerze około 115 MB.

*Git* jest również efektywny w operacjach sieciowych — ogólne protokoły transferu w *Git'cie* przesyłają jedynie spakowane wersje tylko tych obiektów, które uległy zmianie. *Git* nie będzie też próbował przesyłać dwukrotnie tej samej treści, więc jeśli nawet miałbyś taki sam plik pod dwiema różnymi nazwami, jego zawartość zostanie przesłana tylko raz.

### Wielonarzędziowa budowa
*Git* w rzeczywistości nie jest pojedynczym programem, lecz zbiorem wielu małych wyspecjalizowanych programów, co czasem denerwuje osoby próbujące nauczyć się *Git'a*, ale jest całkiem fajne, gdy chcesz zrobić z nim coś niestandardowego. 
*Git* to bardziej zestaw narzędzi, niż program — narzędzi, które można łączyć i wiązać ze sobą, aby zrobić nowe interesujące rzeczy.

> Przez długi czas *Git* był tylko surowym zestawem narzędzi, który swego czasu opakowano w przyjazny dla użytkownika SCM o nazwie *Cogito*. Jednak odkąd sam *Git* stał się łatwiejszy w użyciu, projekt ten został porzucony.

Narzędzia te można mniej więcej podzielić na dwie główne kategorie, określane często jako „ceramika” i „hydraulika”. 
Hydraulika nie jest po to, by korzystać z niej w wierszu poleceń, lecz do wykonania prostych zadań zmyślnie łączonych w większe programy i skrypty, tworzące ceramikę. Ceramika to w dużej mierze to, na czym będziemy się skupiać w tej książce — zorientowany na użytkownika interfejs, ukrywający zabawę na niskim poziomie.


<br><sup>____________________</sup>
<br><sup>1</sup> w sensie złożoności obliczeniowej
<br><sup>2</sup> SCM — ang. Software Configuration Management
