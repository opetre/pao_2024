# Laboratorul - 09

### Unit testing
Permite verificarea izolatata si fragmentata a codului pentru a facilita prevenirea proglemelor.

Printe beneficiile unit testelor se afla:
- Cresterea calitatii codului;
- Clasele de test maresc increderea programatorului in codul sursa scris si ii permit sa urmareasca mai usor cerintele de implementare ale proiectului;
- Testele pot fi scrise inaintea implementarii, fapt ce garanteaza intelegerea functionalitatii de catre dezvoltator (**TDD**).

#### JUnit
Este un framerwork pentru scrierea si executarea testelor unitare in Java. (adaugati in classpath JUnit 5+)

Exemplu:

Consideram clasele **Student** si **Group**, o clasa de test pentru clasa **Group** poate fii
```
import org.junit.jupiter.api.*
 
public class GroupTest {
    private Group group;
 
    @BeforeEach
    public void setup() {
        group = new Group();
    }
 
    @Test
    public void testNoStudentInGroup() {
        Assertions.assertEquals(false, group.areStudentsInGroup());
    }
 
    @Test
    public void testAddStudent() {
        Student st = new Student("Elena", "11");
        group.addStudent(st);
 
        Assertions.assertTrue(group.getStudent("Elena").equals(st));
    }
 
    @AfterEach 
    public void tearDown() {
        group = null;
    }
 
}
```

#### Observatii:
- fiecare metoda de test are adnotarea: @Test
- metodele de setUp (avand adnotarea: @BeforeEach) si tearDown (avand adnotarea: @AfterEach) se apeleaza inainte, respectiv dupa fiecare test. Se intrebuinteaza pentru initializarea/eliberarea resurselor ce constituie mediul de testare, evitandu-se totodata duplicarea codului si respectandu-se principiul de independenta a testelor. Pentru exemplul dat ordinea este:
  - @BeforEach setUp
  - @Test testNoStudentInGroup
  - @AfterEach tearDown
  - @BeforeEach setUp
  - @Test testAddStudent
  - @AfterEach tearDown
- in contextul moștenirii daca ChildTest extends ParentTest ordinea de executie este urmatoarea:
  - ParentTest @BeforeEach setUp
  - ChildTest @BeforeEach setUpSub
  - ChildTest @Test testChild1
  - ChildTest @AfterEach tearDownSub
  - ParentTest @AfterEach tearDown
- Pentru compararea rezultatului asteptat cu rezultatul curent se folosesc apeluri assert:
  - assertTrue
  - assertFalse
  - assertEquals
  - assertNull / assertNotNull

Cateodata avem nevoie sa testam functionalitatea unor clase ce folosesc metode din alte clase netestate sau care nu pot fi testate. De asemenea, exista cazuri in care vrem sa testam comportamentul clasei in situatii extreme sau foarte greu de replicat (erori de disc, epuizarea spatiului pe disc, obtinerea unei anumite valorii in cazul in care folosim generatoare random).

Pentru a rezolva ușor aceste necesitati putem folosi obiecte de tip **mock**. Aceste obiecte simuleaza comporatamentul clasei mock-uite și sunt controlate din interiorul unit testelor.

Exista diverse librarii ce ne permit crearea si folosirea mock-urilor, in cazul nostru vom opta pentru **Mockito**.