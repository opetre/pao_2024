### Task 0
Vom simula o parte din logica unei platforme de streaming.
- Creati un pachet numit **model**;
- Creati un model **Movie (Long id, String Name)**;
  - poate fi o clasa normala in care voi scrieti tot boilerplate-ul (POJO - Plain Old Java Object);
  - sau un simplu record.

### Task 1
- Creati un pachet numit **service** si o interfata **MovieService**;
- Definiti metode pentru:
  - cautarea unui film dupa nume (atat intreg, cat si pentru substring-uri e.g. "Final Destination" va fi returnat si daca trimitem doar "final"); poate returna mai multe filme, cautare case insensitive;
    - printati log-uri daca nu a fost gasit niciun film;
  - adaugarea unui film in "baza de date";
    - printati log-uri pentru a stii daca operatia sa efectuat cu succes sau nu;
  - stergerea unui film;
    - printati log-uri pentru a stii daca operatia sa efectuat cu succes sau nu;
  
### Task 2
- Creati un nou pachet sub cel de **service** numit **impl**;
- Creati clasa **MovieServiceImpl** si implementati interfata definita anterior;
- "Baza de date" va fi reprezentata printr-un camp al acestei clasa (poate fi o colectie/array);

### Task 3
- In entrypoint-ul proiectului vostru (Main) instantiati serviciul;
- Adaugati 3 filme;
- Testati cautarea
  - cu numele intreg;
  - cu un substring din nume, comun pentru cel putin 2 filme (vrem sa primim drept rezultat 2 filme);
  - cu o valoare ce nu va fi gasita;
- Stergeti un film si testati operatie prin efectuarea unei cautari dupa numele fostului film;

### Task Bonus
- Restrictionati adaugarea de noi filme pe baza numelui;
- Separati "baza de date" curenta intr-o clasa **repository** intr-un pachet nou; aceasta trebuie sa expuna public metode pentru manipularea datelor (adaugare, stergere, cautare, inlocuire);
  - folositi aceasta clasa in serviciul vostru prin agregare;