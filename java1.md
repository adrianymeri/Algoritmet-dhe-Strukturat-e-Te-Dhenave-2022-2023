## Algoritmet dhe Strukturat e të Dhënave – Java 1

---

## Klasat

Supozojmë një strukturë të të dhënave `Pika` e cila paraqet dyshen `(x,y)` në rrafshin kartezian:

```cpp
#include <iostream>
#include <math.h>
#include <sstream>
using namespace std;

struct Pika {
  double x;
  double y;
  
  bool baraz(Pika p) {
    return x == p.x && y == p.y;
  }

  double distanca(Pika p) {
    return sqrt(
      pow(x - p.x, 2) + pow(y - p.y, 2)
    );
  }

  double distanca_nga_qendra() {
    return sqrt(pow(x, 2) + pow(y, 2));
  }

  string toString() {
    stringstream ss;
    ss << "(" << x << ", " << y << ")";
    return ss.str();
  }

  Pika konstrukto(double x, double y) {
    Pika p = { x, y };
    return p;
  }
};

int main() {
  Pika p1, p2;
  p1 = p1.konstrukto(6.0, 3.5);
  p2 = p2.konstrukto(4.2, 7.1);

  cout << "Distanca mes pikes p1=" << p1.toString()
      << " dhe pikes p2=" << p2.toString()
      << " eshte d=" << p1.distanca(p2)
      << endl;

  if (p1.baraz(p2)) {
    cout << "Pikat jane te barabarta.";
  } else {
    cout << "Pikat jane te ndryshme.";
  }

  return 0;
}

```

---

Stili i tillë i programimit njihet si **programim procedural**.

Ekziston një stil tjetër i programimit i cili grupon të dhënat dhe funksionet mbi to në një njësi të vetme që quhet **klasë**.

Stili i programimit me klasa quhet **programimi i orientuar në objekte (POO)**.

---

## Programimi i orientuar në objekte

Klasa përshkruan strukturën e të dhënave si dhe ofron funksione të cilat veprojnë mbi ato të dhëna.

Të dhënat e klasës njihen si **fusha** ndërsa funksionet e klasës njihen si **metoda**.

---

Të dhënat e klasës deklarohen sikur te strukturat:

```cpp
class Pika {
  double x;
  double y;
};
```

Realisht, në C++ nuk ka dallim teknik ndërmjet strukturës dhe klasës.

---

**Kontrollimi i qasjes (private, public)**

Fushat **private** mund të lexohen vetëm nga funksionet brenda klasës.

Fushat **publike** mund të lexohen nga cilido bllok.

---

```cpp
class Pika {
  public:  double x;
  private: double y;
};

int main() {
  Pika p;
  p.x = 5.0; // OK
  p.y = 3.5; // Gabim, ndalohet leximi nga blloku i jashtëm
  return 0;
}
```

---

Në disa raste dëshirojmë t'i mbajmë fushat **private** me qëllim të ndalimit të qasjes nga blloqet e jashtme.

Kjo është një veçori kritike për arritjen e **enkapsulimit**.

---

Nëse nuk ceket, klasat e kanë qasjen e nënkuptuar private, ndërsa strukturat e kanë publike.

Nuk ka dallim tjetër ndëmjet strukturave dhe klasave.

---

Funksionet e klasës deklarohen bashkë me të dhënat:

```cpp
class Pika {
private:
  double x;
  double y;

public:
  double distanca_nga_qendra() {
    return sqrt(pow(x, 2) + pow(y, 2));
  }
};
```

---

Thirrja e metodës bëhet përmes operatorit të qasjes sikur te fushat:

```cpp
Pika p = ...;

cout << p.distanca_nga_qendra();
```

Në këtë rast funksioni i merr vlerat e pikës `p`.

---

```cpp
class Pika {
  private: double x, y;
  public:  bool baraz(Pika tjeter) {
    return x == tjeter.x && tjeter.y == tjeter.y;
  }
};

int main() {
  Pika p1 = ..., p2 = ...;
  if (p1.baraz(p2)) cout << "Te njejta";
  else              cout << "Te ndryshme";
  return 0;
}
```

---

Vini re se si parametri i parë i funksionit sikur `p1` në `baraz(p1,p2)` tash bëhet implicit duke marrë formën `p1.baraz(p2)`.

Argumenti implicit që paraqet referencën kontekstuale të objektit aktual në POO quhet `this`.

---

Vlera kontekstuale `this` është pointer për variablën (objektin) aktual.

```cpp
class Personi {
private:
  string emri;
  int mosha;

public:
  void shtyp_infot() {
    cout << "Emri: "  << this->emri  << endl;
    cout << "Mosha: " << this->mosha << endl;
  }
};
```

---

Nëse kemi 2 variabla `p1` dhe `p2`, me funksione të zakonshme kemi shënuar:

```cpp
shtyp_infot(p1);
shtyp_infot(p2);
```

Me metoda (stili i POO) e shënojmë:

```cpp
p1.shtyp_infot();
p2.shtyp_infot();
```

---

Edhe pse po duket që thirrja `p1.shtyp_infot()` nuk po merr parametra,
ajo realisht e mban referencën e variablës `p1` gjatë thirrjes së funksionit.

Thirrjet `p1.shtyp_infot()` dhe `p2.shtyp_infot()` japin rezultate të ndryshme
pasi që ekzekutohen në kontekste të ndryshme.

---
**Klasa Filmi:**

```cpp
#include <iostream>
using namespace std;

class Filmi{
    private:
    int id;
    string titulli;
    double imdb;
    int viti_i_realizimit;
    string zhanri;
    
    public:
    void insert (int i, string t, double imdb, int v, string z){
        id = i;
        titulli = t;
        this->imdb = imdb;
        viti_i_realizimit = v;
        zhanri = z;
    }
    void display(){
        cout << id << endl;
        cout << titulli << endl;
        cout << imdb << endl;
        cout << viti_i_realizimit << endl;
        cout << zhanri << endl;

    }
};
int main() {
    Filmi filmi1;
    filmi1.insert(123, "Interstellar",9.8,2014,"Sci-Fi");
    filmi1.display();
    cout << endl << endl;
    Filmi filmi2;
    filmi2.insert(345, "Film_tjeter",9.9,2023,"Sci-Fi");
    cout << endl << endl;
    filmi2.display();
    return 0;
}

```
---
**Klasa Studenti:**
```cpp
#include <iostream>  
using namespace std;  
class Student {  
   public:  
       int id;    
       string name;  
       void insert(int i, string n)    
        {    
            id = i;    
            name = n;    
        }    
       void display()    
        {    
            cout<<id<<"  "<<name<<endl;    
        }    
};  
int main(void) {  
    Student s1; //krijimi i nje objekti te klases Student   
    Student s2; //krijimi i nje objekti te klases Student    
    s1.insert(201, "Filan");    
    s2.insert(202, "Filane");    
    s1.display();    
    s2.display();  
    return 0;  
}  
```
---
**Klasa Punetori:**
```cpp
#include <iostream>  
using namespace std;  
class Employee {  
   public:  
       int id;    
       string name;  
       float salary;  
       void insert(int i, string n, float s)    
        {    
            id = i;    
            name = n;    
            salary = s;  
        }    
       void display()    
        {    
            cout<<id<<"  "<<name<<"  "<<salary<<endl;    
        }    
};  
int main(void) {  
    Employee e1; 
    Employee e2;  
    e1.insert(201, "Filan",990000);    
    e2.insert(202, "Filane", 29000);    
    e1.display();    
    e2.display();    
    return 0;  
}
```
---
**Shembull shtese - 1:**
```cpp
#include <iostream>
using namespace std;

// Krijo klasen
class Room {

   public:
    double length;
    double breadth;
    double height;

    double calculateArea() {
        return length * breadth;
    }

    double calculateVolume() {
        return length * breadth * height;
    }
};

int main() {

    // create objektin e klases Room
    Room room1;

    // Jep vlera anetareve te klases
    room1.length = 42.5;
    room1.breadth = 30.8;
    room1.height = 19.2;

    // Kalkulo dhe shfaq
    cout << "Area of Room =  " << room1.calculateArea() << endl;
    cout << "Volume of Room =  " << room1.calculateVolume() << endl;

    return 0;
}
```
---
**Shembull shtese - 2:**
```cpp
// Duke perdorur public dhe private

#include <iostream>
using namespace std;

class Room {

   private:
    double length;
    double breadth;
    double height;

   public:

    // funksioni qe inicializon variablat private
    void initData(double len, double brth, double hgt) {
        length = len;
        breadth = brth;
        height = hgt;
    }

    double calculateArea() {
        return length * breadth;
    }

    double calculateVolume() {
        return length * breadth * height;
    }
};

int main() {

    Room room1;

    // jep vlere variablave private si argumente
    room1.initData(42.5, 30.8, 19.2);

    cout << "Area of Room =  " << room1.calculateArea() << endl;
    cout << "Volume of Room =  " << room1.calculateVolume() << endl;

    return 0;
}
```
