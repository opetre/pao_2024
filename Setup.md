# Setup

### JDK (Java Development Kit)
In acest laborator vom folosii Java 17.

#### Windows
- Descarcati arhiva oficiala https://jdk.java.net/archive/ (v17.0.2)
- Dezarhivati arhiva sub "C:\Program Files\Java" (creati folderul Java daca este necesar)
- Copiati path-ul (e.g. "C:\Program Files\Java\jdk-17.0.2\")
- In start cautati **Edit the system enviroment variables**
- Click pe butonul **Environment Variables**
- Creati o noua variabila in **System variables** cu numele **JAVA_HOME** si valoarea path-ul copiat anterior
- Win + R -> cmd
- Rulati comanda **java --version** pentru a verifica daca instalarea s-a realizat cu succes

#### Linux (Ubuntu)
Any other distro is welcomed :) 
- Deschideti un terminal
- ```$ sudo apt update```
- ```$ sudo add-apt-repository ppa:openjdk-r/ppa```
- ```$ sudo apt install openjdk-17-jdk```
- ```$ sudo apt install openjdk-17-source```
- Setati **JAVA_HOME**
  - ```$ sudo gedit /etc/environment```
  - la finalul fisierului adaugati **JAVA_HOME="/usr/lib/jvm/java-17-openjdk-amd64"**
  - salvati fi rulati comanda ```$ source /etc/environment```
- Verificati instalarea ruland ```$ java -version```

### IDE
Aveti libertatea de a folosii orice doriti, insa va voi recomnda 2 dinte cele mai utilizate optiuni.

- IntelliJ IDEA
  - versiunea comunity este suficienta, insa daca doriti access la toate capabilitatile acestui IDE, versiunea ultimate este oferita gratis studentilor https://www.jetbrains.com/community/education/#students
- Eclipse

### Git
- https://git-scm.com/downloads

### GitHub
Va rog sa va creati un account pe https://github.com/ daca nu aveti deja.

### Maven
Nu il vom folosii pentru primele laboratoare, dar il puteti instala in avans.
https://maven.apache.org/guides/getting-started/windows-prerequisites.html