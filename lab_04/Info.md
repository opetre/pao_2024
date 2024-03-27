# Laboratorul - 04

### Enumerari (Enum)
- Un tip special de clasa care poate incapsula o serie de constante;
```
public enum PuncteCardinale {
    NORD, EST, SUD, VEST;
}
```
- Numele **constantelor** sunt scrise cu litere mari;
- Accesarea unei constante se realizeaza intr-o maniera statica
```var p = PuncteCardinale.NORD```;
- Nu trebuie instantiat folosind operatorul **new**;
- Putem definii proprietati specifice fiecarei constatante
  - Trebuie sa fie de tip **private** si **final**;
  - Trebuie definit un constructor **privat** care sa le initializeze;
  - Trebuie definite metode **public** de tip **getter**;
```
public enum PuncteCardinale {
    NORD(1, 'N'), EST(2, 'E'), SUD(3, 'S'), VEST(4, 'V');

    private final int valoare;
    private final char simbol;

    private PuncteCardinale(int valoare, char simbol) {
        this.valoare = valoare;
        this.simbol = simbol;
    }
    //getters
}
```
- Orice enum este implicit **final** deci nu poate fi extins;
- Metode mostenite din clasa parinte java.lang.Enum
  - **public final String name()**: furnizeaza numele unei constante sub forma unui șir de caractere;
  - **public final int ordinal()**: furnizeaza numarul de ordine al unei constante in cadrul enumerarii.
- Putem definii metode statice in cadrul unui enum. (e.g. convertirea unui string in enum)

### Colectii
Pachetul **java.util** contine clase si interfete utile pentru reprezentarea si manipularea colectiilor.

Colectiile ofera implementari pentru urmatoarele tipuri:
- Set (multime - elemente neduplicate)
- List (lista de elemente)
- Map (perechi cheie-valoare)

Interfata de baza este **Collection**.
De asemenea, in clasa **Collections** gasim metode statice utile lucrului cu colectii (exclusiv metode statice, e.g. ```Collections.sort(...)```).

#### Interfata List\<E\>
- O colectie care poate fi **ordonata**;
- Poate contine elemente **duplicate**;

##### Implementari concrete
- **ArrayList** = implementare sub forma de vector. Accesul la elemente se face in timp constant: O(1);
```
List<String> names = new ArrayList<>();
sau
var names = new ArrayList<String>();
```
- **LinkedList** = implementare sub forma de lista dublu inlantuita. Prin urmare, accesul la un element nu se face in timp constant, fiind necesara o parcurgere a listei: O(n);

#### Interfata Set\<E\>
- O colectie ce nu poate contine elemente duplicate;

##### Implementari concrete
- **HashSet**
  - Memoreaza elementele sale intr-o tabela de dispersie (hash table);
  - Este implementarea cea mai performanta, insa nu avem garantii asupra **ordinii** de parcurgere. Doi iteratori **diferiti** pot parcurge elementele multimii in ordine **diferita**.
- **TreeSet**
  - Memoreaza elementele sale sub forma de arbore rosu-negru;
  - Elementele sunt **ordonate** pe baza valorilor sale. Implementarea este mai **lenta** decat HashSet;
  - Complexitatea operatiilor este de **O(log(N))**;
- **LinkedHashSet**
  - Este implementat ca o tabela de dispersie, insa mentine o lista dublu-inlantuita peste toate elementele sale. Prin urmare (si spre deosebire de HashSet), elementele raman in **ordinea** in care au fost inserate.

#### Interfata Map\<K, V\>
- Un Map este un obiect care mapeaza **chei** pe **valori**;
- **Nu** pot exista chei **duplicate**.

##### Implementari concrete
- Particularitatile de implementare corespund celor de la **Set**;
- **HashMap**
```
Map<String, Integer> note = new HashMap<>();
sau
var note = new HashMap<String, Integer>();
```
- **TreeMap**
- **LinkedHashMap**

Interfata **Map.Entry** desemneaza o pereche (cheie, valoare) din map. Metodele caracteristice sunt:
- **getKey**: intoarce cheia;
- **getValue**: intoarce valoarea;
- **setValue**: permite stabilirea valorii asociata cu aceasta cheie;

#### Parcurgerea colectiilor
Se poate realiza prin 2 metode:
- **iteratori**;
  - Permit travesarea si modificarea colectiilor (e.g. stergerea unui element);
```
public interface Iterator<E> {
    boolean hasNext();
    E next();
    void remove(); // optional
}
```
```
Collection<Double> col  = new ArrayList<Double>();
Iterator<Double> it = col.iterator();
 
while (it.hasNext()) {
    Double backup = it.next();
    // apelul it.next() trebuie realizat inainte de apelul it.remove()
    if (backup < 5.0) {
        it.remove();
    }
}
```
- **for-each**;
  - Nu putem sterge un element in timpul iterarii;
```
Collection collection = new ArrayList();
for (Object o : collection) {
    System.out.println(o);
}
```

#### Compararea elementelor
Pentru tipuri complexe de date (e.g. clase definite de noi) este nevoie sa definim comportamentul de comparare.
Acest lucru se poate realiza in 2 moduri:
- Implementarea in clasa a interfetei **Comparable\<E\>** si suprascrierea metodei **compareTo**;
  - Logica de sortare se afla in clasa ale carei obiecte sunt sortate. Din acest motiv, aceasta metoda se numeste **sortare naturala**.
```
public class Student implements Comparable<Student> {
    // compuri, constructor, getter, setter
    @Override
        public int compareTo(Student o) {
            if (surname.equals(o.surname)) {
                return name.compareTo(o.name);
            } else {
                return surname.compareTo(o.surname);
            }
        }
}
```
- Definirea unei clase care implementeaza interfata **Comparator\<E\>**;
  - Logica de sortare se afla intr-o clasa separata. Astfel, putem defini mai multe metode de sortare, bazate pe diverse campuri ale obiectelor de sortat.
```
var numbers = new ArrayList<Integer>();
numbers.add(5);
numbers.add(1);
numbers.add(10);
Collections.sort(numbers, new Comparator<Integer>() {
     @Override
     public int compare(Integer o1, Integer o2) {
          return o2 - o1;
     }
});
```
- Rezultatul compararii este un integer, si se poate interpreta astfel:
  - **pozitiv** – o2 este **mai mare** decat o1
  - **zero** – o2 este **egal** cu o1
  - **negativ** – o2 este **mai mic** decat o1

#### Contractul equals - hashCode
- Daca se suprascrie equals(), trebuie suprascris si hashCode();
- Daca se foloseste o colectie ce are la baza hash-uri, trebuie suprascrise metodele equals() si hashCode();

##### Contract
- Daca apelam hashCode() de mai multe ori pe acelasi obiect, ar trebui sa se intoarca intotdeauna aceiasi valoare;
- Daca obj1 equals obj2 => hashcode obj1 == hashcode obj2;
- Daca obj1 !equals obj2 => cele doua hashcodes nu trebuie neaparat sa fie diferite, totusi e recomandat sa fie diferite d.p.d.v. complexitate;

#### Alte interfete utile:
- **Queue**
  - Interfata ce defineste o coada, cu operatiile aferente;
    - Exemplu de implementare: **PirorityQueue**;
- **Deque**
  - Interfata ce defineste o coada cu doua capete extinde interfata **Queue**;
  - Avand doua capete, poate fi folosita atat ca si coada, cat si ca si stiva
    - Exemple de implementari : **ArrayDeque**, **LinkedList**;