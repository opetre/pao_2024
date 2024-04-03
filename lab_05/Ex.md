### Task 0
Simularea unui calculator ce proceseaza date de tipul double:
- Definiti interfata **Calculator** ce contine metodele **add**, **divide**, si **average** (a se implementa folosind add si divide);
- Metodele pot arunca urmatoarele exceptii (trebuie definite sub pachetul **exception** creat de voi):
  - **NullParameterException**: este aruncata daca vreunul din parametrii primiti este null;
  - **OverflowException**: este aruncata daca suma a doua numere e egala cu **Double.POSITIVE_INFINITY**;
  - **UnderflowException**: este aruncata daca suma a doua numere e egala cu **Double.NEGATIVE_INFINITY**.

### Task 1
- Suprascrieti constructorul exceptiilor astfel incat sa accepte un mesaj;
- Implemetati interfata intr-o clasa concreta si intantiati-o in Main;
- Folosind blocuri try-catch creazi cate un scenariu in care fiecare metoda sa arunce o exceptie; 

### Task 2
- Folosind stream-uri I/O de fiecare data cand este aruncata o exceptie adaugata mesajul acesteia intr-un fisier.
