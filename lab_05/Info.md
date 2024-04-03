# Laboratorul - 05

### Exceptii
O exceptie este un eveniment care se produce in timpul executiei unui program si care perturba fluxul normal al instructiunilor acestuia.

E.g. in cadrul unui program ce prelucreaza un fisier:
- Absenta fisierului;
- Imposibilitatea de a-l citi din cauza permisiunilor insuficiente;
- Probleme cauzate de accesul concurent la fisier;

Cand o eroare se produce intr-o functie, aceasta creeaza un obiect exceptie si il paseaza catre runtime system. Un astfel de obiect contine informatii despre situatia aparuta:
- Tipul de exceptie;
- Stiva de apeluri (**stack trace**);

#### Aruncarea exceptiilor
```
var l = getArrayListObject();
if (l == null)
    throw new Exception("The list is empty");
```

##### Observatii
- Un obiect-exceptie este un obiect ca oricare altul, si se instantiaza la fel (folosind **new**);
- Aruncarea exceptiei se face folosind keyword-ul **throw**;
- Exista clasa **Exception** care desemneaza comportamentul specific pentru exceptii.
  - Clasa **Exception** este parintele majoritatii claselor exceptie din Java.
  - Exemple de exceptii comun intalnite:
    - **IndexOutOfBoundsException**: este aruncata cand un index asociat unei liste sau unui vector depaseste dimensiunea colectiei respective.
    - NullPointerException: este aruncata cand se acceseaza un obiect neinstantiat (**null**).
- in momentul in care se instantiaza un obiect-exceptie, in acesta se retine **intregul** lant de apeluri de functii prin care s-a ajuns la instructiunea curenta. Aceasta succesiune se numeste stack trace si se poate afisa prin apelul **e.printStackTrace()**, unde e este obiectul exceptie.

#### Traterea exceptiilor
Cand o exceptie a fost **aruncata**, **runtime system** incearca sa o **trateze** (**prinda**). Tratarea unei exceptii este facuta de o portiune de cod speciala.
```
public void f() throws Exception {
    List<String> l = null;
 
    if (l == null)
        throw new Exception();
}
 
public void catchFunction() {
    try {
        f();
    } catch (Exception e) {
        System.out.println("Exception found!");
    }
}
```
Se observa ca daca o functie arunca o exceptie si nu o prinde trebuie, in **general**, sa adauge clauza **throws** in **antet**.

Functia **catchFunction**:
- Pentru a prinde o exceptie, trebuie sa specificam o zona in care asteptam ca exceptia sa se produca (**guarded region**). Aceasta zona este introdusa prin blocul **try**;
- In continuare, avem blocul **catch (Exception e)**. La producerea exceptiei, blocul catch corespunzator va fi executat. Dupa aceea, programul va continua sa ruleze normal in continuare;
  - Trebuie sa tinem cont de ordinea in care blocurile sunt definite astfel incat exceptiile sa porneasca de la specific spre generic (e.g. primul catch **IOException**, urmat de alt catch cu **Exception** si nu invers);

##### Observatii
- Putem defini mai multe blocuri catch pentru a implementa o tratare preferentiala a exceptiilor, in functie de tipul acestora;
- In cazul aruncarii unei excepții intr-un bloc try, se va intra intr-un **singur bloc catch** (cel aferent excepției aruncate);
- Blocurile **try-catch** pot fi imbricate;

#### Blocul finally
- Este un bloc special ce poate fi definit **dupa** blocurile catch si **se executa mereu**, indiferent daca programul **intra sau nu** intr-un bloc catch;
- Ne este util in cazuri in care avem nevoie sa executam o sectiune de cod indiferent de rezultatul din **try**, e.g. inchiderea unui stream I/O.

#### Try-with-resources
Din Java 7, a fost adaugata construcția try-with-resources, care ne permite sa declaram resursele intr-un bloc try, cu asigurarea ca resursele vor fi inchise dupa executarea acelui bloc. Resursele declarate trebuie sa implementeze interfața **AutoCloseable**.
```
try (PrintWriter writer = new PrintWriter(file)) {
    writer.println("Hello World");
}
```

#### Tipuri de exceptii
Nu toate exceptiile trebuie prinse cu try-catch. Pentru a ințelege de ce, sa analizam clasificarea exceptiilor:
- Clasa **Throwable**
  - Superclasa tuturor erorilor și excepțiilor din Java;
  - Doar obiectele ce extind aceasta clasa pot fi aruncate de catre JVM sau prin instrucțiunea **throw**;
  - Numai aceasta clasa sau una dintre subclasele sale pot fi tipul de argument intr-o clauza catch.
- **Checked exceptions**, ce corespund clasei **Exception**
  - O aplicatie ar trebui sa le **prinda** si sa permita **continuarea** rularii programului.
  - E.g. **FileNotFoundException** cauzata din input uman.
- **Errors**, ce corespund clasei **Error**
  - Acestea definesc situatii exceptionale declansate de factori **externi** aplicatiei, pe care aceasta nu le poate anticipa si nu-si poate reveni, daca se produc.
  - E.g. **OutOfMemoryError** cauzata de alocarea unui obiect de dimensiuni prea mari.
  - Aplicatia poate incerca sa prinda aceasta eroare, pentru a **anunta** utilizatorul despre problema aparuta; dupa aceasta insa, programul **va esua** (afisand eventual stack trace).
- **Runtime Exceptions**, ce corespund clasei **RuntimeException**
  - Ca si erorile, acestea sunt conditii exceptionale, insa, spre deosebire de erori, ele sunt declansate de factori **interni** aplicatiei. Aplicatia nu poate anticipa si **nu** isi poate reveni daca acestea sunt aruncate.
  - **Runtime exceptions** sunt produse de diverse bug-uri de programare (erori de logica in aplicatie, folosire necorespunzatoare a unui API, etc).
  - E.g. **NullPointerException** cauzata de apelarea unei metode pe o referinta cu valoarea **null**.

Exceptiile **checked** sunt cele prinse de blocurile try-catch. **Toate** exceptiile sunt checked, mai puțin cele de tip **Error**, **RuntimeException** si **subclasele acestora**, adica cele de tip **unchecked**.

Putem arunca RuntimeException **fara** sa o mentionam in clauza throws din antet
```
public void f(Object o) {
    if (o == null)
        throw new NullPointerException("o is null");
}
```

#### Exceptiile in contextul mostenirii
Metodele suprascrise (**overriden**) pot arunca **numai** exceptiile specificate de metoda din **clasa de baza** sau exceptii **derivate** din acestea.

#### Definirea exceptiilor
Cand aveti o situatie in care alegerea unei exceptii (de aruncat) nu este evidenta, puteti opta pentru a scrie propria voastra exceptie, care sa extinda Exception, RuntimeException sau Error.
```
class TemperatureException extends Exception {}
 
class TooColdException extends TemperatureException {}
```

### Fluxuri I/O
Permit procesarea **input**-ului si producerea **output**-ului;
Sunt definite sub pachetul **java.io**;

Sunt reprezentate prin **stream**-uri (fluxuri de date).

#### Tipuri de stream-uri:
- **InputStream**: folosit pentru a citi date;
- **OutputStream**: folosit pentru a scrie date;

#### Byte Streams
- 8 bit (octet);
- Clase: FileInputStream/FileOutputStream;
- Utile daca vrem sa procesam date in format binar (e.g. imagini, audio, video);
```
// try-catch
var input = new FileInputStream("D:\\test.txt");    
var i = input.read(); \\ int 
System.out.print((char)i);
input.close(); // sau try-with-resources  
```

#### Character Streams
- 16 bit (character);
- Clase: FileReader/FileWriter;
- In spate, foloseste tot FileInputStream/FileOutputStream;
- Utile daca vrem sa procesam caractere Unicode;
```
var array = new char[100];
// try-catch
var input = new FileReader("input.txt");
input.read(array);
System.out.println(array);
input.close(); // sau try-with-resources
```

#### File
Permite operații specifice fișierelor și directoarelor, precum creare, ștergere, mutare etc., mai puțin operații de citire/scriere.

##### Metode
- **String getAbsolutePath()** – returneaza calea absoluta a unui fișier;
- **String getName()** – returneaza numele unui fișier;
- **boolean createNewFile()** – creeaza un nou fișier, iar daca fișierul exista deja metoda returneaza false;
- **File[] listFiles()** – listeaza fisierele dintr-un director;

#### DataInputStream & DataOutputStream
- Permit citirea și scrierea datelor la nivel de tipuri de date primitive;
- Clase: DataInputStream/DataOutputStream;
```
var dataInputStream = new DataInputStream(new FileInputStream("data/data.bin"));
var floatInput = dataInputStream.readFloat();
var longInput = dataInputStream.readLong();
dataInputStream.close(); // sau try-with-resources
```

#### Fluxuri I/O folosind buffer
- Numar mare de accesari => probleme de performanta Clase;
- Buffer-ele ne permit sa minimizam numarul de operatii I/O prin citirea si stocarea de blocuri in memorie;
- **BufferedReader**/**BufferedWriter** – fluxuri de procesare la nivel de buffer de caractere;
```
var reader = new BufferedReader(new FileReader("src/main/resources/input.txt"));
var linie = reader.readLine();
reader.close(); // sau try-with-resources
```
- **BufferedInputStream**/**BufferedOutputStream** – fluxuri de procesare la nivel de buffer de octeți;
```
var buffer = new BufferInputStream(new FileInputStream("in.txt"));
// citim primul bit
var i = buffer.read();
while (i != -1) {
  System.out.print((char) i);
  i = buffer.read();
}
buffer.close();
```
