# Laboratorul - 03

#### Agregare si compozitie
-  Agregarea si compozitia reprezinta alte doua modalitati de interconectare (asociere) a doua 
clase, alaturi de mecanismul de extindere a claselor (mostenire). 
   - agregare (HAS_A) = **weak association** = obiectul incapsulat poate sa existe si dupa distrugerea containerului sau (obiectul incapsulat poate fi modificat extern)
   ```
   public A(B clasaIncapsulata) {
        this.clasaIncapsulata = clasaIncapsulata;
   }
   ```
   - compoztie (PART_OF) = **strong association** = ciclul de viata al obiectului incapsulat este dependent de ciclul de viata al obiectului container
   ```
   public A() {
        this.clasaIncapsulata = new B();
   }
   ```

#### Interfete
- Keyword: **interface**;
- Contin doar semnaturile metodelor (din java 8 putem declara si implementari **default**) si campuri constante;
- Metodele si campurile sunt publice;
- Modificatori de access disponibili: public sau default;
- Pentru a putea "folosii" o interfata aceasta trebui implementata de catre o clasa (keyword **implements**);
- O clasa poate implementa mai multe interfete;
- O clasa trebuie sa implementeze toate metodele unei interfete;
- O interfata poate avea declarate metode statice, acestea trebuie implementate;
- Interfetele pot mostenii alte interfete (**extends**).

#### Clase abstracte
- Keyword: **abstract**;
- Pot contine metode abstracte (fara implementare);
- Pot contine campuri variabile;
- Pot folosii modificatori de access (nu este default public ca la interfete);
- Pot avea constructori dar nu pot fi instantiate.

#### Clase imutabile
- O clasa este imutabila daca nu mai putem modifica
continutul unei instante a sa dupa creare;
- Clase imutabile in java: String, Clase Wrapper, BigInteger etc.;
- Avantaje:
  - thread safe;
  - usor de implementat, folosit, si testat;
  - pot fi folosite drept chei in structuri de date asociative (ex HashMap);
- Singurul dezavantaj important al claselor imutabile il constituie faptul ca sunt create mai multe obiecte intermediare, respectiv cate unul pentru fiecare operatie efectuata.

##### Regule de implementare
1. Clasa nu va permite rescrierea metodelor sale, fie declarand clasa de tip final, fie
declarand constructorii ca fiind private si folosind metode de tip factory pentru a
crea obiecte;
2. Toate campurile vor fi declarate ca fiind final (li se vor atribui valori o singura data,
printr-un constructor cu parametri) si private (nu li se pot modifica valorile direct);
3. Clasa nu va contine metode de tip set sau alte metode care pot modifica valorile
campurilor;
4. Daca exista campuri care sunt referinte spre obiecte mutabile, se va impiedica
modificarea acestora, astfel:
    4.1. Nu se vor folosi referinte spre obiecte externe, ci spre copii ale lor (se va folosi compozitia, nu agregarea);
    4.2. Nu se vor returna referinte spre campurile mutabile, ci se vor returna referinte spre copii ale lor.

#### Records
- Introduse in Java 15;
- Clasa imutabila;
- Utilizate pentru incarcarea unor date dintr-o anumita sursa, spre eventual intr-o destinatie;
- Definirea unui nou record
```
[modificatori de acces] record denumire (descriptor) {}
```
```
public record Student(String nume, int grupa, double medie) {}
```
- Orice record este in mod **implicit** o clasa de tip **final** care extinde clasa **java.lang.Record**
  - **nu poate** fi abstracta;
  - **nu poate** fi extinsa;
  - **nu poate** extinde alte clase;
  - totusi **poate** implementa una sau mai multe interfete.
- Membre statice nu mai sunt implicit de tip final si nu se mai genereaza automat metode de tip get pentru ele;
- Se pot adauga constructori supraincarcati, dar acestia trebuie sa apeleze explicit constructorul canonic;
```
public Student(String nume, int grupa) {
    this(nume, grupa, 0);
}
```
- Constructorul canonic poate fi redefinit, de obicei pentru a realiza prelucrari suplimentare sau validari ale componentelor inregistrarii.

#### String
- Reprezinta un array **imutabil** de caractere;
- Poate fi instantiat in 2 moduri
  - ```var s = "ceva"``` - valoare stocata in string pool;
  - ```var s = new String("ceva")``` - valoare stocata pe heap;
- Contine metode pentru lucrul cu String-uri precum: length(), substring(...), toLowerCase(), etc.
- Contine mai multe metode care necesita utilizarea unor expresii regulate (regex): matches(...), replaceAll(...), split(...).

#### StringBuilder
- Reprezinta un array **mutabil** de caractere;
- Sunt situatii in care se prefera utilizarea unui sir de caractere care sa poate fi modificat direct, de exemplu, cand se construieste dinamic un sir prin concatenarea mai multor siruri.
- Sunt alocate in zona de memorie heap si sunt
tratate ca niste tablouri de caractere. Dimensiunea tabloului se modifica dinamic, pe masura ce sirul este construit ( initial, sirul are o lungime de 16 caractere).

#### StringBuffer
- Reprezinta un array **mutabil** de caractere;
- Thread safe;
- Mai lent decat StringBuilder.

#### Notes
- Java este mereu **pass-by-value**.