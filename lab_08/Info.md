# Laboratorul - 08

### Optional
Din Java 8 a fost introdus cu scopul de a permite scrierea de cod fara valori de tipul **null**.

Practic va puteti gandii la acesta drept un **Wrapper** peste orice tip de clasa.
#### Instantiere
- Optional.empty();
- Optional.of({value}); - acepta valori ce nu pot fi **null**;
- Optional.ofNullable({value}); - acepta valori ce pot fi **null**;

Pentru a putea folosii valorile invaluite de Optional trebuie sa verificam daca acestea sunt de fapt prezente.
Acest lucru se realizeaza cu functiile **isPresent()** si **isEmpty()** (Java 11+);

O alta alternativa este conditionarea actiunilor prin metoda **ifPresent()** ce asteapta un **Consumer**;
```
Optional.of("baeldung")
    .ifPresent(name -> System.out.println(name.length()));
```

Pentru a extrage valoarea din Optional avem mai multe optiuni, printre care:
- get() - trebuie sa verificam mai intai ca exista valoarea;
- orElse() - ne ofera posibilitatea de a da o valoare alternativa daca Optional este gol;
- orElseGet(Supplier) - daca Optional este gol este chemata interfata **Supplier**;
- orElseThrow() - poate fi folosita pentru a arunca o exceptie in cazul in care Optional este gol;

### Stream API
Stream-urile au fost introduse in Java 8, pentru a permite programatorului sa efectueze operatii de tipul filter, map si reduce pe colectii intr-un mod elegant si eficient.

Stream-urile pot fi obtinute prin mai multe modalitati, in special de la liste si set-uri, care expun metodele **stream()** si **parallelStream()**. Diferenta consta in faptul ca cea dintai face operatiile secvential in timp ce a doua le face in paralel pe un mediu de procesare cu mai multe core-uri.

Exemple:
```
Arrays.asList("a1", "a2", "a3").stream()
    .findFirst()
    .ifPresent(System.out::println);  // a1
```

```
Stream.of("a1", "a2", "a3")
    .findFirst()
    .ifPresent(System.out::println);  // a1
```
```
IntStream.range(1, 4)
    .forEach(System.out::println);
```
```
List.of(1, 2, 3).stream()
    .map(n -> 2 * n + 1)
    .average()
    .ifPresent(System.out::println);  // 5.0
```

#### Operatii pe stream-uri
Se impart in 2 categorii:
- **Terminale** (returneaza un **rezultat**);
  - foreach() : aplica anumite operatii supra fiecarui element din stream
  - collect() : stocheaza elementele din stream intr-o colectie
  - match() : verifica un Predicate; returenaza boolean
  - count() : returneaza numarul de elemente din stream
  - reduce() : reduce elementele unui stream, folosind o functie; returneaza Optional
  - min(), max(), average()
  - findFirst() : returneaza primul element gasit in stream
  - findAny() : returneaza un element din stream (cel mai des primul, insa in cazuri paralelizate acest lucru nu este garantat)
- **Intermediare** (returneaza un **stream**);
  - map() : converteste fiecare element din stream
  - filter() : primeste un Predicate ca si parametru si filtreaza elementele stream-ului in functie de acesta
  - sorted() : sorteaza un stream
  - distinct() : returneaza elementele distincte din stream
  - flatMap() : Stream<Collection> -> Stream

#### Map, Filter, Peek, Reduce
Provenite din Programarea functionala, functiile de map(), filter(), peek() si reduce() au fost importate in Java ca principal mijloc de lucru cu Stream-uri. Ele ajuta la reducerea considerabila a codului scris, dar pot, in acelasi timp, sa ingreuneze intelegerea acestuia, cu atat mai mult pentru programatorii aflati la inceput de cariera.
- **Map**
  - Permite conversia datelor dintr-un Stream prin schimbare a tipului sau modificare a valorii.
```
var myArray = new String[]{"bob", "alice", "paul", "ellie"};
Arrays.stream(myArray)
    .map(s -> s.toUpperCase()) // ["BOB", "ALICE","PAUL", "ELLIE"]
    .forEach(System.out::println);
```
- **Filter**
  - Asa cum spune si numele, ajuta la filtrarea elementelor unui Stream, mai precis la eliminarea elementelor nedorite din acesta. Precum functia de map(), asteapta ca argument o expresie **lambda**.
```
List.of("dog", "cat", "monkey", "elephant", "rat", "lion", "zebra").stream()
    .filter(x -> x.length() > 4)
    .toList();
```
- **Peek** (intermediar)
  - Returneaza un Stream in urma aplicarii unui **Consumer** pe elementele unui stream deja existent. Conform documentatiei Java, scopul principal al acestei metode este **debugging-ul**. Pe deasupra, un scenariu in care se poate dovedi foarte utila e reprezentat de posibilitatea de a modifica informatiile de stare interna ale unui obiect.
```
Stream.of(new Student("Alice", 21), new Student("Bob", 22), new Student("Gigel", 20)).stream()
    .peek(st -> st.setName(st.getName().toLowerCase()))
    .forEach(System.out::println);
```
- **Reduce**
  - Metodele de tip reduce sunt metode ce obtin un rezultat in urma unei operatii pentru intregul set de date. Setul de operatii functionale pe care il vom aplica asupra Stream-ului se va termina aproape intotdeauna cu o operatie de tip reduce.
  - Deja ati intalnit operatia **toList()** anterior, care este o operatie de tip reduce. Alte operatii similare ar fi **sum**, **average** si **count**.
  - Functia in sine de reduce(), spre deosebire de map si filter, accepta doua argumente: un element identitate (sau acumulator) si o expresie lambda.
```
var myArray = { "this", "is", "a", "sentence" };
var result = Arrays.stream(myArray)
                .reduce("", (a,b) -> a + b); // concatenare
```

#### flatMap si groupingBy
- **flatMap**
  - Similar cu map, aceasta functionala permite aplicarea unei metode pe elementele unui stream. Ce aduce in plus aceasta metoda este ca aplica si o operatie de flat pe stream-ul rezultat in urma aplicarii acelei operatii pe toate elementele din cadrul stream-ului. Cel mai bun exemplu ar fi daca avem de-a face cu o lista de liste, aplicam functionala flatMap(), iar rezultatul va fi o lista cu elementele combinate din acele liste;
```
List<List<Integer>> listOfLists =
        List.of(List.of(1, 2, 3, 4), List.of(10, 9, 8, 7), List.of(5, 6));
    List<Integer> singleList = listOfLists.stream().flatMap(List::stream).toList();
    System.out.println(singleList);
```
- **groupingBy**
  - Aceasta functionala se foloseste pentru a grupa elementele dintr-un stream dupa o anumita conditie (de exemplu grupatul unei liste de numere in par si impar). Aceasta intoarce o instanta de tip Map;
```
List<Integer> numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
Map<String, List<Integer>> parity =
    numbers.stream().collect(Collectors.groupingBy(i -> i % 2 != 0 ? "Odd" : "Even"));
//Even [2, 4, 6, 8, 10]
//Odd [1, 3, 5, 7, 9]
```