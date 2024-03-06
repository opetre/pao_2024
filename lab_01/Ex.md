### Task 0
- Creati un proiect Java nou folosind versiunea JDK 17.
- Afisati in cosola mesajul "Hello PAO!"
- Compilati si rulati codul in linie de comanda folosind utilitarele **javac** respectiv **java**

### Task 1
- Creati un pachet nou. (numele este la libera alegere)
- Creati urmatorarele clase sub acest pachet
  - **Movie** 
    - name:String
    - rating:Float
    - genre:String
  - **Person**
    - name:String
    - favoriteGenre:String
    - minRating:Float
    - chooseMovie(Movie[]) - metoda ce primeste un array de obiecte Movie si intoarce o valoare boolean in cazul in care exista cel putin un film cu
      -  genre == favoriteGenre
      -  rating >= minRating
  - **App**
    - main - metoda principala de unde va incepe executia
    - creati un array de tip **Movie** si populatil cu min. 4 oiecte
    - creati un obiect de tip **Person** si apelati metoda **chooseMovie**, in urma careia afisati un mesaj pe baza valorii returnate
- Compilati si rulati programul
  
### Task 2
- Modificati clasele astfel incat campurile acestora sa aiba specificatorul de acces **private** si implementari metodele de getter/setter necesare pentru a putea acces campurile.

### Task 3
- Modificati crearea obiectului de tip **Person** astfel incat datele acestuia sa fie citite de la tastatura. (Hint: folositi clasa Scanner)