## Algoritmet dhe Strukturat e të Dhënave – Java 6


**Detyra 1:** Te shkruhet programi qe kalkulon shumen e numrave te ruajtura ne Stack

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
**Detyra 2:**

```cpp
#include <iostream>
#include <stack>
using namespace std;

int main() {
    stack<string> languages;
    
    // add element to the Stack
    languages.push("C++");
    languages.push("Java");
    languages.push("Python");
    
    cout << languages.top();

    return 0;
}
```
---

**Detyra 3:** Fshierja e elemenenteve nga stack-u.

```cpp
#include <iostream>
#include <stack>
using namespace std;

// function prototype for display_stack utility
void display_stack(stack<string> st);

int main() {

  // create a stack of strings
  stack<string> colors;

  // push elements into the stack
  colors.push("Red");
  colors.push("Orange");
  colors.push("Blue");
  
  cout << "Initial Stack: ";
  // print elements of stack
  display_stack(colors);
  
  // removes "Blue" as it was inserted last
  colors.pop();
  
  cout << "Final Stack: ";

  // print elements of stack
  display_stack(colors);
  
  return 0;
}

// utility function to display stack elements
void display_stack(stack<string> st) {

  while(!st.empty()) {
    cout << st.top() << ", ";
    st.pop();
  }

  cout << endl;
}
```
---

**Detyra 3:**

```cpp
#include <iostream>
#include <stack>
using namespace std;

int main() {

  // create a stack of double
  stack<double> nums;
  
  cout << "Is the stack empty? ";

  // check if the stack is empty  
  if (nums.empty()) {
    cout << "Yes" << endl;
  }
  else {
    cout << "No" << endl;
  }

  cout << "Pushing elements..." << endl;

  // push element into the stack
  nums.push(2.3);
  nums.push(9.7);
 
  cout << "Is the stack empty? ";

  // check if the stack is empty  
  if (nums.empty()) {
    cout << "Yes";
  }
  else {
    cout << "No";
  }

  return 0;
}
```
