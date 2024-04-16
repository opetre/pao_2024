### Task 0
- Implementati o structura de tipul linked list generica (2 clase: Node & SimpleLinkedList);
- Implementati metode pentru crearea listei, adaugarea si afisarea elementelor;
  - Metoda de afisare trebuie sa foloseaca un **Consumer**;

### Task 1
- Creati o clasa POJO la libera alegere;
- Folosind un supplier adaugati elemente in lista de tipul clasei create de voi;
- Supraincarcati metoda de printare a elementelor din lista astfel incat sa acepte un **Predicate**, iar pe baza rezultatului sa filtreze rezultatul;
  - e.g. daca lista voastra contine elemente de tipul int, puteti da un **Predicate** care sa afiseze doar elementele pare;

### Task 2
- Creati o noua metoda in SimpleLinkedList numita apply care primeste drept argument o expresie lambda **Function** si o foloseste pentru a updata fiecare valoare din lista;