# Laboratorul - 07

### Genericitate
Folosind clasel, metode și interfețe generice în Java:
- Obtinem un cod mult mai "curat";
- Verificarea tipurilor este efectuată de **compilator**.

E.g. fara genericitate (ne bezam pe **cast**-uri)
```
List myIntList = new LinkedList(); 
myIntList.add(new Integer(0));
Integer x = (Integer) myIntList.iterator().next();
```

E.g. cu genericitate
```
List<Integer> myIntList = new LinkedList<Integer>(); 
myIntList.add(new Integer(0));
Integer x = myIntList.iterator().next();
```

#### Definirea unei structuri generice simple
```
public interface Iterator<E> {
    E next();
    boolean hasNext();
    void remove();
}
```
Sintaxa **\<E\>** (poate fi folosită orice literă) este folosită pentru a defini tipuri formale în cadrul interfețelor. Aceste tipuri pot fi folosite în mod asemănător cu tipurile uzuale, cu anumite restricții totuși. În momentul în care invocăm o structură generică ele vor fi **înlocuite cu tipurile efective utilizate în invocare**.

##### Atentie
Dacă **ChildType** este un subtip (clasă descendentă sau subinterfață) al lui **ParentType**, atunci o structură generică GenericStructure\<ChildType\> **NU** este un subtip al lui GenericStructure\<ParentType\>. Atenție la acest concept, întrucât el nu este intuitiv!

#### Wildcards (**?**)
Wildcard-urile sunt utilizate atunci când dorim să întrebuințăm o structură generică drept parametru într-o funcție și nu dorim să limităm tipul de date din colecția respectivă.
```
void printCollection(Collection<Object> c) {
    for (Object e : c)
        System.out.println(e);
}
```
O situație precum cea de mai sus ne-ar **restricționa** să folosim la apelul funcției doar o colecţie cu elemente de tip Object, care **nu** poate fi convertită la o colecție de un **alt tip**.
```
void printCollection(Collection<?> c) {
    for (Object e : c)
        System.out.println(e);
}
```
##### Bounded Wildcards
În anumite situații, faptul că un wildcard poate fi înlocuit cu orice tip se poate dovedi un **inconvenient**. Mecanismul bazat pe **Bounded Wildcards** permite introducerea unor restricţii asupra tipurilor ce pot înlocui un wildcard, obligându-le să se afle într-o relație ierarhică (de descendență) față de un tip **fix specificat**.
```
public static void listPizza(List<? extends Pizza> pizzaList) {
        for(Pizza item : pizzaList)
            System.out.println(item.getName());
    }
```
Sintaxa List<? extends Pizza> (**Upper Bounded Wildcards**) impune ca tipul elementelor listei să fie Pizza sau o subclasă a acesteia. Astfel, pList ar fi putut avea, la fel de bine, tipul List<HamPizza> sau List<CheesePizza>.
În mod similar, putem imprima constrângerea ca tipul elementelor listei să fie Pizza sau o superclasă a acesteia, utilizând sintaxa List<? super Pizza> (**Lower Bounded Wildcards**).

Utilizarea bounded wildcards se manifestă în următoarele 2 situații :
- **Lower bounded wildcards** se folosesc atunci când vrem să **modificăm** o colecție generică;
- **Upper bounded wildcards** se folosesc atunci când vrem să **parcurgem fără să modificăm** o colecție generică;

### Interfete Functionale
Interfetele ce contin **o singura metoda abstracta** (si un nr nelimitat de metode **default**) se numesc **interfete functionale**.
Pentru a permite compilatorului sa ne ajute in anumite cazuri si pentru a evidentia tipul interfetei noastre, acestea pot fi marcate cu adnotarea **@FunctionalInterface**.
```
@FunctionalInterface
public interface Foo {
    String method();
}
```

##### Note
- Intefetele functionale pot fi extinse de alte interfete functionale daca semnatura metodei abstracte este **identica**;
- Desi putem definii oricate metode default, este **recomandat** sa ne limitam la cat mai putine (ideal 0/1);

### Expresii Lambda
Lambda este un concept din **programarea funcțională** și reprezintă o **funcție anonimă**.
Majoritatea limbajelor de nivel înalt au introdus suport pentru acest concept în ultimii 15 ani, inclusiv Java, din versiunea 8.
```
int num = () -> 10;
```
##### Particularitati
- Parametrii primiți în lambda pot fi zero (() ca în exemplul de mai sus) sau mai mulți (param1, param2, …);
```
(a, b) -> a > b;
```
- Pentru un **singur** parametru putem omite parantezele;
```
a -> a / 2;
```
- Este de **preferat** sa evitam folosirea keyword-ului return in contextul lambda;
```
a -> a.toLowerCase(); // corect
a -> {return a.toLowerCase()}; // nerecomandat
```
- Este de **preferat** ca o expresie lambda sa fie scrisa pe un singur rand (one-liner), dar pot exista cazuri in care 2-3 randuri sa fie aceptabile. Un numar mai mare de randuri semnaleaza un punct pentru **refactorizarea** codului;
- Este de **preferat** sa folosim referintele metodelor in expresii lambda;
```
a -> a.toLowerCase(); // corect
a -> String::toLowerCase; // recomandat
```
- Evitati specificarea tipurilor parametriilor;
```
(a, b) -> a.toLowerCase() + b.toLowerCase(); // corect
(String a, String b) -> a.toLowerCase() + b.toLowerCase(); // nerecomandat
```

##### Interfete functionale comune
- Runnable -> run();
- Comparable -> compareTo();
- ActionListener -> actionPerformed();
- Callable -> call();

#### Tipuri de interfete functionale
- Consumer - **\<T\> arg -> void**
  - Bi-Consumer
- Predicate **\<T\> arg -> boolean**
  - Bi-Predicate
- Function **\<T\> arg -> \<R\> result**
  - Bi-Function
  - Unary Operator
  - Binary Operator 
- Supplier **void -> \<T\> result**
