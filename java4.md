### Memoria dinamike

Shpesh nuk e dimë sa hapësirë na nevojitet për shënime, psh. gjatësia e vargut.

Me operatorin `new` kërkojmë nga sistemi operativ një bllok të memories me madhësi të dëshiruar.

---

Rezultati i `new` është një **pointer** për bllokun e bajtave të alokuar në **heap**.

**Heap memoria** është memorie e procesit e cila jeton më gjatë sesa blloku i funksionit.

Zakonisht pointerët nuk na nevojiten për vlera lokale, por për vlera në heap.

---

Sintaksa: `new tipi` për një element, `new tipi[n]` për varg.
Rezultati i operacionit është pointer `tipi*`.

**Shembull:** Alokimi dinamik i një vargu:

```cpp
int n;
cout << "Sa elemente i deshironi ne varg? ";
cin >> n;
int* vargu = new int[n];
// vargu[0], vargu[1], ... vargu[n - 1]
```

---

**Shembull:** Alokimi dinamik i një strukture:

```cpp
struct Drejtkendeshi { int gjeresia; int lartesia; };

Drejtkendeshi* krijo(int a, int b) {
  Drejtkendeshi* rez = new Drejtkendeshi;
  rez->gjeresia = a;
  rez->lartesia = b;
  return rez;
}

int main() {
  Drejtkendeshi* x = krijo(2, 3);
  cout << x->lartesia;
  delete x;
  return 0;
}
```

---

**Stack** quajmë memorien statike të bllokut të funksionit.

**Heap** quajmë memorien e përbashkët të procesit.

![](/lendet/algoritmet-dhe-strukturat-e-te-dhenave/java1/img5.png)

---

Operatori `new` është i rrezikshëm, pasi që memoria e alokuar nuk fshihet vetvetiu (edhe pas përfundimit të bllokut aktual).

Fshirja e memories së alokuar dinamikisht bëhet përmes `delete` (një element) dhe `delete[]` (varg).

---

**Shembull:** Alokimi dinamik për variablën `n` dhe vargun `vargu[n]`, dhe pastaj fshierja e tyre:

```cpp
int main() {
  int* n = new int;
  cout << "Sa elemente i deshironi ne varg? ";
  cin >> *n;
  int* vargu = new int[*n];

  // ... kryejmë llogaritje

  // pastrojmë memorien
  delete n;
  delete[] vargu;
  return 0;
}
```

---

Disa shkurtesa për inicializim të vlerave gjatë alokimit dinamik:

```cpp
Drejtkendeshi* d1 = new Drejtkendeshi { 3, 4 };

Drejtkendeshi* d2 = new Drejtkendeshi;
*d2 = { 5, 6 };

int* x = new int { 21 };
```

---

**Null pointeri**

Ndonjëherë na duhet të tregojmë që pointeri nuk paraqet asnjë lokacion memorik.

Në këto raste vlera e pointerit e merr vleren 0, që zakonisht quhet `NULL`.

```cpp
int* x = NULL; // nuk ka vlerë.
```

NULL pointeri nuk mund të dereferencohet.

---

## Referencat

Nëse kemi një l-value `a`, atëherë mund ta krijojmë një alias për `a` përmes deklarimit `tipi& b = a`.

```cpp
int a = 5;
int& b = a;
b = 3;
cout << a; // shfaqet 3
```

Aliasi `b` ka lokacion memorik të njëjtë me variablën `a`, prandaj paraqesin të njëjtin shënim.

---

**Detyrë:** Të tregohet dalja në ekran për kodin në vazhdim.

```cpp
int a = 2;
int* ptr = &a;
int& b = a;
*ptr = 3;
cout << b;
```

Sikur te pointerët, simboli `&` te deklarimi i referencës ka kuptim tjetër me operatorin e adresës `&a`.

---

Referencat mund t'i përdorim në parametra të funksioneve.

```cpp
void nderro(int& a, int& b) {
  int temp = a;
  a = b;
  b = temp;
}

int main() {
  int x = 3, y = 5;
  nderro(x, y);
  cout << x << ", " << y; // Shfaqet 5, 3
  return 0;
}
```

---

**Bartja përmes vlerës dhe referencës**

- Parametrat e zakonshëm të funksioneve në C++ janë pass-by-value (përmes kopjimit).
- Nëse i deklarojmë si parametra referent, atëherë thirrja bëhet pass-by-reference (përmes adresës).

---

Kur kemi thirrje përmes referencës:

- Nuk kopjohet vlera e argumentit, por adresa e tij – parametri bëhet alias i argumentit.
- Argumenti duhet të jetë l-value – nuk mund të kemi alias në r-value.
- Nëse ndryshon vlera e argumentit, ndryshimet barten në bllokun thirrës.

---

**Detyrë:** Të shkruhet funksioni `llogarit` i cili e llogarit shumën dhe prodhimin
nga `1` deri në `n`, dhe rezultatet i vendos në parametrat referent `s` dhe `p`.

```cpp
void llogarit(int n, int &s, int &p);
```

---

**Kthimi përmes referencës**

Një funksion poashtu mund të kthejë l-value përmes referencës.

```cpp
int& elementi(int* v, int i) {
  return v[i];
}

int main() {
  int vargu[5] = { 7, 4, 5, 8, 2 };
  elementi(vargu, 3) = -1;
  cout << vargu[3]; // shfaqet -1
  return 0;
}
```

---

**Kujdes:** Vlerat lokale nuk guxojnë të kthehen, pasi që kanë jetëgjatësi vetëm në bllokun aktual.

```cpp
int& alfa() {
  int n = 5;
  return n; // gabim
}
```

---

**Referencat konstante**

Shpesh bartjen e bëjmë përmes referencës për ta evituar kopjimin që vie me bartjen përmes vlerës.

Deklarimi i variablës/parametrit si `const tipi&` mundëson krijimin e një aliasi të pandryshueshëm.

```cpp
void funksioni(const int& x) {
  const int &y = x;
}
```

---

Dërgimi dhe kthimi sipas referencës mund të bëhet edhe përmes pointerëve.

```cpp
int* elementi(int* v, int i) {
  return &v[i]; // ose v+i
}
```

Faktikisht, forma përmes `&` përkthehet nga kompajlleri në ekuivalentën e saj me pointerë.

---

**Detyrë:** Të shkruhet funksioni `llogarit` i cili e llogarit shumën dhe prodhimin
nga `1` deri në `n`, dhe rezultatet i vendos në adresat e pointerëve `*s` dhe `*p`.

```cpp
void llogarit(int n, int* s, int* p);
```

---

## Detyra shtesë

---

**Detyrë:** Të shkruhet funksioni `swap(a,b)` në variantin me pointerë dhe me referenca.

Të thirren te dy variantet nga `main` dhe të vrojtohen dallimet sintaksore.

---

**Detyrë:** Të shkruhet funksioni `kopjo(v[], n)` i cili kopjon një varg dhe kthen një pointer për kopjen e vargut.

---

**Detyrë:** Të tregohet dalja në ekran për kodin në vazhdim.

```cpp
int v1[3] = { 1, 2, 3 };
int v2[3] = { 4, 5, 6 };
int *x = v1, *y = v2;
int **z = &(*x > *y ? x : y);
cout << 2 * *(*z + 1);
```
---

<!-- .slide: style="font-size:0.8em;" -->

**Detyrë**

- Të deklarohet struktura `Drejtkendeshi`.
- Të shkruhet funksioni `lexo()`, i cili dinamikisht alokon një drejtkëndësh dhe e mbush me vlera nga tastiera.
- Në `main` të krijohet një varg prej `n` drejtkëndëshave (`n` të lexohet nga tastiera). Të mbushet vargu nga tastiera përmes funksionit `lexo`.
- Të gjendet sipërfaqja totale e të gjithë drejtkëndëshave (përmes funksionit `siperfaqja`).
- Të lirohen të gjitha resurset e alokuara.

--

```cpp
#include <iostream>
using namespace std;

struct Drejtkendeshi { int a; int b; };

Drejtkendeshi* lexo() {
  int a, b;
  cout << "Shtyp a: ";
  cin >> a;
  cout << "Shtyp b: ";
  cin >> b;
  return new Drejtkendeshi { a, b };
}

int siperfaqja(Drejtkendeshi *d) {
  return d->a * d->b;
}

int main() {
  int n;
  cout << "Jepni numrin e drejtkendeshave: ";
  cin >> n;
  Drejtkendeshi** drejtkendeshat = new Drejtkendeshi*[n];
  for (int i = 0; i < n; i++) {
    cout << "Drejtkendeshi " << (i + 1) << endl;
    drejtkendeshat[i] = lexo();
  }

  int s = 0;
  for (int i = 0; i < n; i++) {
    s += siperfaqja(drejtkendeshat[i]);
  }

  cout << "Siperfaqja totale: " << s;

  for (int i = 0; i < n; i++) {
    // Lirimi i alokimeve individuale.
    delete drejtkendeshat[i];
  }

  // Lirimi i vargut të pointerëve.
  delete[] drejtkendeshat;
  return 0;
}
```
---

**Detyrë:** Të tregohet dalja në ekran për kodin në vazhdim.

```cpp
int v[4] = { 6, 2, 7, 4 };

cout << *(v + 1) + 1;
```

---

**Detyrë:** Të tregohet dalja në ekran për kodin në vazhdim.

```cpp
int v1[3] = { 1, 2, 3 };

int v2[3] = { 4, 5, 6 };

int *p[2] = { v1, v2 };

cout << 2 * *(*(p + 1) + 1);
```

---
**Detyrë:** 

```cpp
#include <iostream>
using namespace std;
 
int main() {
   int number = 88;    // Declare an int variable and assign an initial value
   int * pNumber;      // Declare a pointer variable pointing to an int (or int pointer)
   pNumber = &number;  // assign the address of the variable number to pointer pNumber
 
   cout << pNumber << endl;  // Print content of pNumber (0x22ccf0)
   cout << &number << endl;  // Print address of number (0x22ccf0)
   cout << *pNumber << endl; // Print value pointed to by pNumber (88)
   cout << number << endl;   // Print value of number (88)
 
   *pNumber = 99;            // Re-assign value pointed to by pNumber
   cout << pNumber << endl;  // Print content of pNumber (0x22ccf0)
   cout << &number << endl;  // Print address of number (0x22ccf0)
   cout << *pNumber << endl; // Print value pointed to by pNumber (99)
   cout << number << endl;   // Print value of number (99)
                             // The value of number changes via pointer
 
   cout << &pNumber << endl; // Print the address of pointer variable pNumber (0x22ccec)
}
```
---
**Detyrë:** 

```cpp
#include <iostream>
using namespace std;
 
int main() {
   int number1 = 88, number2 = 22;
 
   // Create a pointer pointing to number1
   int * pNumber1 = &number1;  // Explicit referencing
   *pNumber1 = 99;             // Explicit dereferencing
   cout << *pNumber1 << endl;  // 99
   cout << &number1 << endl;   // 0x22ff18
   cout << pNumber1 << endl;   // 0x22ff18 (content of the pointer variable - same as above)
   cout << &pNumber1 << endl;  // 0x22ff10 (address of the pointer variable)
   pNumber1 = &number2;        // Pointer can be reassigned to store another address
 
   // Create a reference (alias) to number1
   int & refNumber1 = number1;  // Implicit referencing (NOT &number1)
   refNumber1 = 11;             // Implicit dereferencing (NOT *refNumber1)
   cout << refNumber1 << endl;  // 11
   cout << &number1 << endl;    // 0x22ff18
   cout << &refNumber1 << endl; // 0x22ff18
   //refNumber1 = &number2;     // Error! Reference cannot be re-assigned
                                // error: invalid conversion from 'int*' to 'int'
   refNumber1 = number2;        // refNumber1 is still an alias to number1.
                                // Assign value of number2 (22) to refNumber1 (and number1).
   number2++;   
   cout << refNumber1 << endl;  // 22
   cout << number1 << endl;     // 22
   cout << number2 << endl;     // 23
}
```
---
**Detyrë:** 

```cpp
// more pointers
#include <iostream>
using namespace std;

int main ()
{
    int first = 5, second = 15;
    int * p1, * p2;

    p1 = &first;   // p1 = address of first
    p2 = &second;  // p2 = address of second
    *p1 = 10;      // value pointed to by p1 = 10
    *p2 = 20;      // value pointed to by p2 = 20
    cout << "first is: " << first <<endl;
    cout << "second is: " << second <<endl;
    p2 = p1;       // p1 = p2 (value of pointer is copied)
    *p1 = 40;      // value pointed to by p1 = 20
    cout << "first is " << first <<endl;
    cout << "second is " << second <<endl;
    return 0;
}
```
---

**Detyrë:** 

```cpp
#include <iostream>
using namespace std;
 
// Function prototypes
int max(const int arr[], int size);
void replaceByMax(int arr[], int size);
void print(const int arr[], int size);
 
int main() {
   const int SIZE = 4;
   int numbers[SIZE] = {11, 22, 33, 22};
   print(numbers, SIZE);
   cout << max(numbers, SIZE) << endl;
   replaceByMax(numbers, SIZE);
   print(numbers, SIZE);
}
 
// Return the maximum value of the given array.
// The array is declared const, and cannot be modified inside the function.
int max(const int arr[], int size) {
   int max = arr[0];
   for (int i = 1; i < size; ++i) {
      if (max < arr[i]) max = arr[i];
   }
   return max;
}
 
// Replace all elements of the given array by its maximum value
// Array is passed by reference. Modify the caller's copy.
void replaceByMax(int arr[], int size) {
   int maxValue = max(arr, size);
   for (int i = 0; i < size; ++i) {
      arr[i] = maxValue;
   }
}
 
// Print the array's content
void print(const int arr[], int size) {
   cout << "{";
   for (int i = 0; i < size; ++i) {
      cout << arr[i];
      if (i < size - 1) cout << ",";
   }
   cout << "}" << endl;
}

```
