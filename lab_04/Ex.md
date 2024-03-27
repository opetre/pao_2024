### Task 0
Ne vom definii propriul utilitar pentru log-uri.
- Definiti un enum care sa reprezinte nivelele disponibile pentru logare: INFO, WARN, DEBUG, ERROR;

### Task 1
- Definiti o interfata de baza **Logger** cu 2 metode:
  - void log(LogLevel loglevel, String message);
  - void logInfo(String message) - metoda **default** care sa cheme log() implicit cu nivelul INFO;
- Creati clasa **MyLogger** care sa implementeze interfata **Logger** si metoda **log()**, aceasta trebuie sa fie capabila sa printeze in consola log-uri sub forma ```[logLevel]: logMessage```;

### Task 2
- Creati o clasa **Book** cu campuri definite de voi;
- Creati o colectie de tip lista, adaugati elemnte in ea, sortati-o, iterati prin aceasta si logati (**INFO**) fiecare element;
- Creati o colectie de tip set, adaugati elemente in ea, si logati (**WARN**) cazul in care un element nu a fost adaugat pentru ca este deja prezent.

### Task BONUS
- Modificati clasa **MyLogger** astfel incat sa implementeze design pattern-ul de **singelton**;