## Model danych w *Git*

Dane *Git* tworzą strukturę, którą w fachowym języku określa się jako *acykliczny graf skierowany*.
Oznacza to, że z dowolnego *commit'a* możesz rozpocząć jednokierunkową wędrówkę przez cały łańcuch jego przodków (rodzica, rodzica-rodzica, itd.), nigdy nie przechodząc przez ten sam *commit*. 
Wszystkie *commit'y* przechowują wskaźnik do *drzewa* oraz opcjonalnie wskaźnik do poprzedniego *commit'a*, albo wskaźniki do poprzednich *commit'ów*.
Każde *drzewo* przechowuje wskaźnik do jednego lub więcej *blob'ów* i/lub poddrzew.
Ten prosty model umożliwia zapis i odtwarzanie obszernych struktur reprezentujących historie złożonych drzew zawartości, które szybko i wydajnie można dowolnie zmieniać.

Niniejsza część ma na celu zademonstrowanie, jak dokładniej wygląda opisany wyżej model.
