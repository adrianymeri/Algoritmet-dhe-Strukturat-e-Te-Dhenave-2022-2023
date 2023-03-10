### Konstruktorët

Variablat tipi i të cilave është klasë i quajmë **objekte** ose **instanca**.

Konstruktori është një funksion i veçantë i cili thirret gjatë krijimit të instancës.

Zakonisht përdoren për të inicializuar gjendjen e klasës duke i dhënë vlera fushave.

---

Konstruktori shkruhet si metodë e cila e ka emrin e klasës dhe nuk ka tip kthimi.

```cpp
class Pika {
private:
  double x;
  double y;

public:
  Pika(double x, double y) {
    this->x = x;
    this->y = y;
  }
};
```

Konstruktorët mund të mbingarkohen.

---

Kontruktori thirret gjatë krijimit të instancës.

Thirrjet e mëposhtme janë ekuivalente:

```cpp
int main() {
  Pika p1 = Pika(2.5, 3);
  Pika p2(2.5, 3);
  return 0;
}
```

---

Konstruktori më së shpeshti përdoret për të vendosur vlera në fusha.

```cpp
class Studenti {
private:
  int mosha;
  double notaMesatare;
public:
  Studenti(int mosha, double notaMesatare) {
    this->mosha = mosha;
    this->notaMesatare = notaMesatare;
  }
}
```

Vini re që mbishkrimin e identifikatorëve e tejkalojmë përmes qasjes eksplicite me `this`.

---

**Copy constructor**

Në C++ secila klasë ka një konstruktor special për kopjim të objektit.

Zakonisht kjo mund të shkaktojë sjellje të papritura, prandaj shpesh do ta ndalojmë.

```cpp
class Studenti {
public:
  // Konstruktori i kopjimit.
  Studenti(const Studenti&) { ... }
  // Operatori i shoqërimit.
  Studenti& operator=(const Studenti&) { ... }
};
```

---

**Destruktori** është bllok kodi që thirret:

- Kur tipi i alokuar në stack del nga scope.
- Kur fshihet pointeri për objektin e alokuar dinamikisht.

Zakonisht përdoret për lirim të resurseve.

---

Shkruhet në formën `~Klasa() { ... }`.

Nuk merr parametra e as nuk kthen asgjë.

```cpp
class Klasa {
private:
  int* data;

public:
  Klasa() { // Konstruktori
    this->data = new int { 0 };
  }

  ~Klasa() { // Destruktori
    delete this->data;
  }
};
```

---

**Enkapsulimi i fushave private**

Zakonisht e kontrollojmë qasjen në fusha me dy metoda publike `getX()` dhe `setX(x)`.

```cpp
class Studenti {
private:
  int mosha;

public:
  int getMosha() {
    return this->mosha;
  }

  void setMosha(int mosha) {
    this->mosha = mosha;
  }
};
```

---

**Detyrë:**
```cpp
class Personi{
    private:
        int mosha;
        string emri;
        string mbiemri;
        double nota_mesatare;
    public:
        Personi(string emri, string mbiemri, double nota_mesatare){
            mosha = 30;
            this->emri = emri;
            this->mbiemri = mbiemri;
            this->nota_mesatare = nota_mesatare;
            cout << "\nKonstruktori\n";
        }
        
        void shfaqTeDhenat(){
                cout << mosha;
                cout << endl << emri;
                cout << endl << mbiemri;
                cout << endl << nota_mesatare;
        }
        ~Personi(){
             cout << "\nDestruktori\n";
        }
};

int main() {
    Personi obj1 = Personi("Filan","Fisteku",9.8);
    Personi obj2("Filane","Fisteku",9.9);
    obj1.shfaqTeDhenat();
    cout << endl;
    obj1.shfaqTeDhenat();
    return 0;
}
```
---

**Detyrë:**
```cpp
class Studenti{
    private:
        int id;
        string emri;
        string mbiemri;
        string lendet[3];
        double nota_mesatare;
    public:
        Studenti(int id, string emri, string mbiemri, double nota_mesatare, string lendet[]){
            cout << "\nKontruktori....\n";
            this->id = id;
            this->emri=emri;
            this->mbiemri=mbiemri;
            this->nota_mesatare=nota_mesatare;
            for (int i =0; i<3; i++){
                this->lendet[i] = lendet[i];
            }
        }
        ~Studenti(){
            cout << "\nDestruktori....";
        }
    
    void display(){
        cout << id;
        cout << endl << emri;
        cout << endl << mbiemri;
        cout << endl << nota_mesatare << endl;
        for (int i = 0; i<3;i++){
            cout << lendet[i] << endl;
        }
    }
};

int main() {
    string lendet1[] = {"BP","Mat1","Fizika1"};
    string lendet2[] = {"ASDh","Mat2","QE"};
    Studenti obj1 = Studenti(123,"Filan","Fisteku",6.6, lendet1);
    obj1.display();
    cout << endl << endl;
    Studenti obj2(456,"Filane","Fistekaj",6.5,lendet2);
    obj2.display();
    return 0;
}
```

**Detyrë:** Të shkruhet klasa `Studenti` e cila ka:

- Fushat private `emri`, `mbiemri`, `mosha`, `notat[5]`
- Konstruktor që inicializon fushat.
- Metodën `nota(i)` e cila merr notën në pozitën `i`.
- Metodën `notaMesatare()`.
- Metodën `emriPlote()` e cila kthen emrin dhe mbiemrin e bashkuar.
- Metodën `shtyp()` e cila i shtyp në ekran të dhënat e studentit.

---

**Detyrë:** Të shkruhet klasa `Pika` e cila ka:

- Fushat private `x` dhe `y` (nr. real).
- Konstruktorin inicializues `Pika(x,y)` dhe metodat mbështjellëse të fushave.
- Metodën `distanca(Pika tjeter)`.
- Metodën `shtyp()` që shtyp në ekran kordinatat në formën `(x,y)`, psh. `(4,3)`.

---

**Detyrë:** Të shkruhet klasa `Rrethi` e cila ka:

- Fushat private `rrezja` (nr. real) dhe `qendra` (e tipit `Pika` nga detyra e kaluar).
- Konstruktorin `Rrethi(qendra,rrezja)`.
- Metodat `siperfaqja()` dhe `perimetri()`.
- Metodën `distanca(Rrethi tjeter)` e cila e llogarit distancën mes qendrave të rrathëve.
- Metodën `shtyp()` që shtyp në ekran qendrën dhe rrezen e rrethit.

---

**Detyrë:** Të krijohet një varg me 5 instanca të tipit `Rrethi` nga detyra e kaluar.

- Të mbushet ky varg me objekte të inicializuara sipas dëshirës.
- Të gjendet rrethi me sipërfaqen më të madhe dhe të ruhet adresa e tij në një pointer.
- Të shtypet në ekran rrethi i adresuar nga pointeri përmes metodës `shtyp()`.

---

<!-- .slide: style="font-size:0.8em;" -->

**Detyrë:** Të shkruhet klasa `NumerKompleks` me veçoritë private
`re` dhe `im` si dhe anëtarët në vijim:

- Konstruktorin `NumerKompleks(re,im)`
- Metodat `shto(k)`, `zbrit(k)`, `shumezo(k)`, ku `k` është `NumerKompleks`.
- Mbingarkimet `shto(re,im)`, `zbrit(re,im)`, `shumezo(re,im)`.
- Metodat `shtyp()`, `toString()`.

Në `main` të deklarohen disa instanca të tipit
`NumerKompleks` dhe të kryhen llogaritje të ndryshme.
