# Laboratorul - 01

### Avantaje POO
- Cod modular si usor de extins
- Simplificarea complexitatii problemelor prin abstractizarea datelor
- Eliminarea codului duplicat prin refolosirea metodelor deja existente
- Cod usor de testat (automat)

### Proiectele Java
- Clasele sunt oraganizate in grupuri (foldere) numite **pachete** (packages) ce permit structurarea fiserelor intr-un mod logic si faciliteaza lizibilitatea codului
- Fiecare clasa apartine unui pachet
- Permit creerea de clase cu acelasi nume
- Acestea au o reprezentate ierarhica, e.g.
  - ```java.awt.im.<nume_clasa>```

### Tipuri de date
Desi noi modelam totul sub forma de obiecte din motive de performanta Java suporta si primitive, acestea fiind:
- **boolean** - true/false
- **char** - 'A'
- **byte** - 55 (apartine [-128,127])
- **short** - 12
- **int** - 33
- **long** - 9999999
- **float** - 0.52f (32 bit)
- **double** - 0.66 (64 bit)
De observat ca nu avem un tip de date **unsigned**.

#### Clase
- Tipuri de date definite de programatori sau deja existente in sistem
- Sunt compuse din **campuri membri** (varibile) si **metode**
- Pentru a putea declara si instantia o clasa ne folosim de keyword-ul **new**
  - ```ClassA inst = new ClassA()```
  - O exceptie o face clasa **String**
    - ```String str = "Hallo!"```
- **Camp membru**
  - Reprezinta un obiect denumit de programator ce apartine unei clase
  ```
  class Dog {
    String nume;
    int varsta;
  }
  ```
  - Campurile ce nu sunt explicit instantiate/instantiate in constructor primesc valori default: **null** pentru clase si **0**/**false** pentru primitive
  - Pentru a accesa valorile unui camp folosim sintaxa ```instantaClasa.numeCamp```
  - In mod normal acestea sunt **incapsulate** (encapsulation) pentru a ascunde starea interna si implementarea unei clase de utilizarea acesteia.
  ```
  class Dog {
    String nume;
    private int varsta;

    public int getAge() {
        return varsta;
    }
    // a se observa ca acum nu avem cum sa setam campul "varsta"
  }
  ```
- **Metode**
  - Reprezinta functionalitatile expuse de o clasa
  ```
  class Dog {
    String nume;
    int varsta;

    String vorbeste() {
        return "Woof";
    }
  }
  ```
  - Una din metodele prezente in fiecare clasa este **constructorul**. Aceasta faciliteaza crearea instantelor obiectului atunci cand o folosim impreuna cu keyword-ul **new**.
    - Constructorul defaul nu contine nici-o logica.
    ```
    class Dog {
        public Dog() {}
    }
    ```
    - Acesta poate fi **suprascris** si **supraincarcat**.

- Obiectele instantiate au fiecare un spatiu de memorie alocat
```
Dog a = new Dog();
Dog b = new Dog();

a.varsta = 5;
System.out.println(a.varsta); // afiseaza 5
System.out.println(b.varsta); // afiseaza 0
```

### Main
Punctul de start al unui program Java este metoda **main**
```
public static void main(String[] args) {}
```

Argumentele pot fi transmise in linie de comanda astfel ``` java Main arg1 arg2 arg3 ... ``` si mai tarziu folosite in cod prin intermatiul parametrului **args**.

### Specificatori de acces
Oricarui clasa, atribut, sau metoda ii este atribuit un specificator de acces cu scopul de a restrictiona accesul la entitatea respectiva din perspectiva altor clase.
Acestia fac parte din implementarea **incapsularii** codului.

| Specificator | Descriere |
| ------------ | --------- |
| private      | accesul limitat la clasa curenta |
| default      | accesul limitat la pachetul curent (package private) |
| protected    | accesul limitat la pachetul curent si clasele ce mostenesc clasa curenta |
| public       | accesul permis de oriunde |

### Code style
Va recomand sa aruncati un ochi pe [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html).

Acesta poate fi configurat si in IDE pentru auto formatare dar va recomand sa incercati mai intai sa-l intelegeti.

-------
O preferinta personala pe care vreau sa v-o expun este folosirea keyword-ului **var**.

```var intArray = new int[10];```

Acesta permite scrierea unui cod mai compact prin infera tipul de date necesar din partea dreapta a expresiilor. (exista si cazuri mai specifice cand acesta nu poate fi folosit)

### Compilarea si rularea codului Java
Se realizeaza cu ajutorul a 2 utilitare incluse in JDK
- **javac** - compileaza codul in **bytecode** ce va putea fi executat de JVM, output-ul acestuia sunt fisierele **.class**. E.g. ```$ javac Main.Java```
- **java** - permite rularea fisierelor **.class**. E.g. ```$ java Main```

### Notes
Codul Java este backwards compatible, cu alte cuvinte codul scris si rulat cu ajutorul unui JDK mai vechi va rula fara probleme atunci cand folosim o versiune mai noua.