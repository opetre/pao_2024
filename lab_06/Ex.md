### Task 0
Instalati PosgtreSQL server (https://www.postgresql.org/download/) si pgAdmin (https://www.pgadmin.org/download/).

### Task 1
Folosind credentialele setate de voi la pasul anterior conectativa la baza de date si creati o tabela Employees cu field-urile id, nume, experience_days.

Introduceti 3 valori (entries) in aceasta.

### Task 2
Adaugati proiectului Java dependinta driver-ului de JDBC pentru PostgreSQL (https://jdbc.postgresql.org/download/).
```org.postgresql:postgresql:42.7.3```

Tip:
- Intellij: Puteti adauga dependinte la structura proiectului folosind maven; (File -> Project Structure -> Libraries)
- Javac: Trebuie sa specificati class path-ul in care se regasesc dependintele voastre; (`-cp`)

### Task 3
Folosind sintaxa try-with-resources initializati o conexiune cu baza de date;

### Task 4
- Creati un query care sa va selecteze toate datele din tabela Employees;
- Creati un obiect model Employee si un mapper pentru acesta;
- Afisati rezultatul aplicarii mapper-ului asupra ResultSet-ului rezultat;

### Task 5
- Scrieti si executati un **UPDATE** in baza de date care sa modifice **numele** anagajatului cu id-ul **2**;
- Afisati nr de randuri afectate de acest query;
- Re-rulati logica de la task-ul 4; (nu duplicati codul)