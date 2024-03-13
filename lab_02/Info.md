# Laboratorul - 02

#### Principiile POO:
- **Abstractizarea**: simplificarea proprietatilor si functionalitatilor unui obiect; ascunderea logicii interne;
- **Incapsularea**: proprietatea claselor de a grupa datele si metodele ce actioneaza pe ele intr-o singura structură de date (clasa);
- **Mostenirea**: extinderea comportamentului unei clase realizata fara modificari pe codul deja existent;
- **Polimorfismul**: capacitatea unui obiect de a lua forme diferite.

#### Mostenirea
- prin mostenire o clasa de baza (parinte) este extinsa adaugand functionalitati mai specializate
- keyword: extends;
- nu putem mosteni mai multe clase simultan (nu intalnim "diamond problem" precum in C++);
- in Java, orice clasa extinde by default clasa Object.

#### Upcasting & Downcasting
Sunt procesele prin care o instanta a unui obiect se poate comporta drept obiectul parinte, respectiv obiectul copil.

#### **Super** keyword
Faciliteaza accesul la clasa parinte.

#### **Static** keyword
Static fields: 
- va exista intr-un singur exemplar in memorie, indiferent de numarul de instante ale clasei;
- campul este vizibil tuturor instantelor clasei si poate fi modificat de oricare dintre acestea;

Static methods:
- pot fi apelate fara a fi nevoie sa creezi o instanta a clasei.

#### **Final** keyword
- pe atribut/variabila: nu poate fi modificata (devine constanta);
- pe metoda: nu poate fi suprascrisa;
- pe clasa: nu poate fi extinsa;

#### **Abstract** keyword
- pe clasa: nu poate fi instantiata;
- pe metoda: nu are impletemtare in clasa de baza, trebuie implementata obligatoriu in clasele copil.

#### Enum
- tip special de clasa ce mapeaza o lista de constante.