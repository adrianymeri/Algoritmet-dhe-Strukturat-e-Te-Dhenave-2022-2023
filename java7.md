## Algoritmet dhe Strukturat e të Dhënave – Java 7

**Detyra 1:**
```cpp
#include <iostream>
#include <queue>

using namespace std;

int main() {

  // create a queue of string
  queue<string> animals;

  // push elements into the queue
  animals.push("Cat");
  animals.push("Dog");
  
  cout << "Queue: ";

  // print elements of queue
  // loop until queue is empty
  while(!animals.empty()) {

    // print the element
    cout << animals.front() << ", ";

    // pop element from the queue
    animals.pop();
  }

  cout << endl;
 
  return 0;
}
```
---

**Detyra 2:**
```cpp
#include <iostream>
#include <queue>
using namespace std;

// function prototype for display_queue utility
void display_queue(queue<string> q);

int main() {

  // create a queue of string
  queue<string> animals;

  // push element into the queue
  animals.push("Cat");
  animals.push("Dog");
  animals.push("Fox");
  
  cout << "Initial Queue: ";
  display_queue(animals);
  
  // remove element from queue
  animals.pop();
  
  cout << "Final Queue: ";
  display_queue(animals);
  
  return 0;
}

// utility function to display queue
void display_queue(queue<string> q) {
  while(!q.empty()) {
    cout << q.front() << ", ";
    q.pop();
  }

  cout << endl;
}
```
---

**Detyra 3:**
```cpp
#include <iostream>
#include <queue>
using namespace std;

int main() {

  // create a queue of string
  queue<string> languages;
  
  cout << "Is the queue empty? ";

  // check if the queue is empty  
  if (languages.empty()) {
    cout << "Yes" << endl;
  }
  else {
    cout << "No" << endl;
  }

  cout << "Pushing elements..." << endl;

  // push element into the queue
  languages.push("Python");
  languages.push("C++");
 
  cout << "Is the queue empty? ";

  // check if the queue is empty  
  if (languages.empty()) {
    cout << "Yes";
  }
  else {
    cout << "No";
  }

  return 0;
}
```
---
**Te analizohen edhe sllajdet nga faqja 146 deri 158**
