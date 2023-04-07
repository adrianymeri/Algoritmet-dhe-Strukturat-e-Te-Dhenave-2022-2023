## Algoritmet dhe Strukturat e të Dhënave – Java 6


## Detyra 1: Te shkruhet programi qe kalkulon shumen e numrave te ruajtura ne Stack

```cpp
#include <iostream> 
#include <iomanip> 
#include <stack> 
using namespace std; 
int main ()
{
    stack<int> stekuIm;
    int shuma (0);
    for(int i=1;i<=10;i++){
        stekuIm.push(i); //mbushe stekun me vlerat: 1,2,...,10
    }
    while (!stekuIm.empty()) //gjersa steku nuk eshte i zbrazet
    {
        cout<< "Madhesia aktuale e stekut: "
            << setw(2)<<stekuIm.size() << "; ";
        cout<< "Ne krye: "<<setw(2)<<stekuIm.top()<<"\n";
        shuma += stekuIm.top();
        stekuIm.pop();
    }
        cout<< "Shuma e anetareve te stekut, gjithsej: "<<shuma<<"\n";
return 0;
}
```
---
