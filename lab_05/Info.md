# Laboratorul - 05

### Exceptii
O excepţie este un eveniment care se produce în timpul execuţiei unui program şi care perturbă fluxul normal al instrucţiunilor acestuia.

E.g. in cadrul unui program ce prelucreaza un fisier:
- Absenţa fişierului;
- Imposibilitatea de a-l citi din cauza permisiunilor insuficiente;
- Probleme cauzate de accesul concurent la fişier;

Când o eroare se produce într-o funcţie, aceasta creează un obiect excepţie şi îl pasează către runtime system. Un astfel de obiect conţine informaţii despre situaţia apărută:
- Tipul de excepţie;
- Stiva de apeluri (**stack trace**);

#### Aruncarea excepţiilor
```
var l = getArrayListObject();
if (l == null)
    throw new Exception("The list is empty");
```

##### Observatii
- Un obiect-excepţie este un obiect ca oricare altul, şi se instanţiază la fel (folosind **new**);
- Aruncarea excepţiei se face folosind keyword-ul **throw**;
- Există clasa **Exception** care desemnează comportamentul specific pentru excepţii.
  - Clasa **Exception** este părintele majorităţii claselor excepţie din Java.
  - Exemple de exceptii comun intalnite:
    - **IndexOutOfBoundsException**: este aruncată când un index asociat unei liste sau unui vector depăşeşte dimensiunea colecţiei respective.
    - NullPointerException: este aruncată când se accesează un obiect neinstanţiat (**null**).
- În momentul în care se instanţiază un obiect-excepţie, în acesta se reţine **întregul** lanţ de apeluri de funcţii prin care s-a ajuns la instrucţiunea curentă. Această succesiune se numeşte stack trace şi se poate afişa prin apelul **e.printStackTrace()**, unde e este obiectul excepţie.

#### Traterea exceptiilor
Când o excepţie a fost **aruncată**, runtime system încearcă să o **trateze** (**prindă**). Tratarea unei excepţii este făcută de o porţiune de cod specială.
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
Se observă că dacă o funcţie aruncă o excepţie şi nu o prinde trebuie, în **general**, să adauge clauza **throws** în **antet**.

Funcţia **catchFunction**:
- Pentru a prinde o excepţie, trebuie să specificăm o zonă în care aşteptăm ca excepţia să se producă (**guarded region**). Această zonă este introdusă prin blocul **try**;
- In continuare, avem blocul **catch (Exception e)**. La producerea excepţiei, blocul catch corespunzător va fi executat. După aceea, programul va continua să ruleze normal în continuare;
  - Trebuie sa tinem cont de ordinea in care blocurile sunt definite astfel incat exceptiile sa porneasca de la specific spre generic (e.g. primul catch **IOException**, urmat de alt catch cu **Exception** si nu invers);

##### Observatii
- Putem defini mai multe blocuri catch pentru a implementa o tratare preferenţială a excepţiilor, în funcţie de tipul acestora;
- In cazul aruncării unei excepții într-un bloc try, se va intra într-un **singur bloc catch** (cel aferent excepției aruncate);
- Blocurile **try-catch** pot fi imbricate;

#### Blocul finally
- Este un bloc special ce poate fi definit **dupa** blocurile catch si **se executa mereu**, indiferent daca programul **intra sau nu** intr-un bloc catch;
- Ne este util in cazuri in care avem nevoie sa executam o sectiune de cod indiferent de rezultatul din **try**, e.g. inchiderea unui stream I/O.

#### Try-with-resources
Din Java 7, a fost adăugată construcția try-with-resources, care ne permite să declarăm resursele într-un bloc try, cu asigurarea că resursele vor fi închise după executarea acelui bloc. Resursele declarate trebuie să implementeze interfața **AutoCloseable**.
```
try (PrintWriter writer = new PrintWriter(file)) {
    writer.println("Hello World");
}
```

#### Tipuri de excepţii
Nu toate excepţiile trebuie prinse cu try-catch. Pentru a înțelege de ce, să analizăm clasificarea excepţiilor:
- Clasa **Throwable**
  - Superclasa tuturor erorilor și excepțiilor din Java;
  - Doar obiectele ce extind această clasă pot fi aruncate de către JVM sau prin instrucțiunea **throw**;
  - Numai această clasă sau una dintre subclasele sale pot fi tipul de argument într-o clauză catch.
- **Checked exceptions**, ce corespund clasei **Exception**
  - O aplicaţie ar trebui să le **prindă** şi să permită **continuarea** rulării programului.
  - E.g. **FileNotFoundException** cauzata din input uman.
- **Errors**, ce corespund clasei **Error**
  - Acestea definesc situaţii excepţionale declanşate de factori **externi** aplicaţiei, pe care aceasta nu le poate anticipa şi nu-şi poate reveni, dacă se produc.
  - E.g. **OutOfMemoryError** cauzata de alocarea unui obiect de dimensiuni prea mari.
  - Aplicaţia poate încerca să prindă această eroare, pentru a **anunţa** utilizatorul despre problema apărută; după aceasta însă, programul **va eşua** (afişând eventual stack trace).
- **Runtime Exceptions**, ce corespund clasei **RuntimeException**
  - Ca şi erorile, acestea sunt condiţii excepţionale, însă, spre deosebire de erori, ele sunt declanşate de factori **interni** aplicaţiei. Aplicaţia nu poate anticipa şi **nu** îşi poate reveni dacă acestea sunt aruncate.
  - **Runtime exceptions** sunt produse de diverse bug-uri de programare (erori de logică în aplicaţie, folosire necorespunzătoare a unui API, etc).
  - E.g. **NullPointerException** cauzata de apelarea unei metode pe o referinta cu valoarea **null**.

Excepţiile **checked** sunt cele prinse de blocurile try-catch. **Toate** excepţiile sunt checked, mai puțin cele de tip **Error**, **RuntimeException** şi **subclasele acestora**, adică cele de tip **unchecked**.

Putem arunca RuntimeException **fără** să o menţionăm în clauza throws din antet
```
public void f(Object o) {
    if (o == null)
        throw new NullPointerException("o is null");
}
```

#### Excepţiile în contextul moştenirii
Metodele suprascrise (**overriden**) pot arunca **numai** excepţiile specificate de metoda din **clasa de bază** sau excepţii **derivate** din acestea.

#### Definirea exceptiilor
Când aveţi o situaţie în care alegerea unei excepţii (de aruncat) nu este evidentă, puteţi opta pentru a scrie propria voastră excepţie, care să extindă Exception, RuntimeException sau Error.
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
- **String getAbsolutePath()** – returnează calea absolută a unui fișier;
- **String getName()** – returnează numele unui fișier;
- **boolean createNewFile()** – creează un nou fișier, iar dacă fișierul există deja metoda returnează false;
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
