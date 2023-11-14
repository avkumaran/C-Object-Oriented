
### Range-based for loop

```c++
vector<string> teamRoster;
 
// Adding player names
teamRoster.push_back("Mike");
teamRoster.push_back("Scottie");
teamRoster.push_back("Toni");

cout << "Current roster: " << endl;
 
for (string playerName : teamRoster) {
   cout << playerName << endl;
}
```

If modification of a container's elements are desired, declare the for loop's variable as a reference

```c++
for (double &gradeVal : examGrades) {
      double userGrade;
      
      cin >> userGrade;
      gradeVal = userGrade;   }
```

```c++
list<string> teamRoster;

// Adding player names
teamRoster.push_back("Mike");
teamRoster.push_back("Scottie");
teamRoster.push_back("Toni");
  
cout << "Current roster: " << endl;
   
for (string& playerName : teamRoster) {
   cout << playerName << endl;  
}
```

# Vectors

`#include <vector>`

`vector<desiredType> vectorName();`

| Member Function | Specification | What it Does |
|---|---|---|
| at() | at(size_type n) | Accesses element n. |
| size() | size_type size() const; | Return vector's size. |
| empty() | bool empty() const; | Returns true if size is 0. |
| clear() | - | Removes all elements. Vector size becomes 0. |
| push_back() | void push_back(const T& x); | Copies x to new element at vector's end, increasing size by 1.
| erase() | iterator erase (iteratorPosition); | Removes element from position. Elements from higher positions are shifted back to fill gap. Vector size decrements. ||
| insert() | iterator insert(iteratorPosition, const T& x); | Copies x to element at position. Items at that position and higher are shifted over to make room. Vector size increments. |

## Sorting a Vector of [Class](Classes) Objects

sort() function, in C++ Standard Template Library's (STL) algorithms library (sorts from lowest to highest):
1.  Add `#include <algorithm>` to enable the use of sort().
2.  Overload the < operator for the programmer-defined class.
3.  Call the sort() function as `sort(myVector.begin(), myVector.end())`

# Lists

**list**: container of ordered elements, i.e., a sequence

A C++ list is implemented as a doubly-linked list. 

A list can be declared and created as `list<T> newList;` where T represents the list's type, such as int or string. 

`#include <list>` enables use

The **push_back()** function adds an element to the end of a list. 
	Ex: `authorList.push_back("Martin");`
The **push_front()** function adds an element to the front of a list. 
	Ex: `authorList.push_front("Butler");`

| Member Function                      | Use                                                                                                                                        |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------ |
| front()                              | Returns element at the front of the list                                                                                                   |
| back()                               | Returns element at the back of the list                                                                                                    |
| push_back(newElement)                | Adds newElement to the end of the list. List's size is increased by one.                                                                   |
| push_front(newElement)               | Adds newElement to the beginning of the list. List's size is increased by one.                                                             |
| size()                               | Returns the number of elements in the list.                                                                                                |
| pop_back()                           | Removes last element in the list. List's size decrements by one                                                                            |
| pop_front()                          | Removes first element in the list. List's size decrements by one                                                                           |
| remove(existingElement)              | Removes all occurrences of elements which are equal to existingElement. List's size is decreased by number of existingElement occurrences. |
| begin()                              | Returns an iterator that points to the first element in the list.                                                                          |
| end()                                | Returns an iterator that points to after the last element of the list.                                                                     |
| insert(iteratorPosition, newElement) | Inserts newElement into the list before the iteratorPosition                                                                               |
| erase(iteratorPosition)              | Removes a single element at iteratorPosition.                                                                                              |
| erase(iteratorFirst, iteratorLast)   | Removes a range of elements from iteratorFirst (inclusive) to iteratorLast (exclusive)                                                     |


The statement `list<int>::iterator iter;` declares a list iterator for a list of integers.

Elements pointed to by the iterator are dereferenced to reveal their value. 
	Ex: `*iter` dereferences the iterator and evaluates to the element to which the iterator referred.

```c++
list<string> authorsList;
string name;
list<string>::iterator iter;

authorsList.push_back("Gamow");
authorsList.push_back("Greene");
authorsList.push_back("Penrose");

for (iter = authorsList.begin(); iter != authorsList.end(); ++iter) {
   name = *iter;   
   cout << name << endl;
}
```

# Queue

**queue**: a container of ordered elements that supports element insertion at the tail and element retrieval from the head
	A queue can be declared as `queue<T> newQueue;` where T represents the element's type, such as int or string. `#include <queue>` enables use of a queue within a program.

| Member function  | Use                                                                                                                     |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------- |
| push(newElement) | Adds new element to the tail of the queue. The queue's size increases by one.                                           |
| pop()            | Removes the element at the head of the queue.                                                                           |
| front()          | Returns, but does not remove, the element at the head of the queue. If the queue is empty, the behavior is not defined. |
| back()           | Returns, but does not remove, the element at the tail of the queue.                                                     |
| size()           | Returns the size of the queue.                                                                                          |

## Priority Queues

Each item  has a priority associated with it and elements are ordered by priority and secondarily by arrival order

```c++
// Author:  Keith Shomper
// Date:    23 Feb 2016
// Purpose: To demonstrate a MIN priority queue with duplicate primary keys

#include <iostream>
#include <iomanip>
#include <string>
#include <ctime>
#include <queue>

using namespace std;

class myC {
  public:
	myC(                          )  : key(0),  secondaryKey(0),  s("")  {  }
	myC(int ky, int sk, string str)  : key(ky), secondaryKey(sk), s(str) {  }
	int    getKey ()      const      { return key;          }
	void   setKey (int k)            { key = k;             }
	int    getSKey()      const      { return secondaryKey; }
	string getString()    const      { return s;            }
	friend bool operator<(const myC& c1, const myC& c2);
  private:
	int    key;
	int	  secondaryKey;
	string s;
};

// note the STL priority queue is not stable, therefore we need to add a
// secondary sort order (based on when inserted) to create a total order
bool operator<(const myC& c1, const myC& c2) {

	// by default the queue is a MAX queue, so we reverse the comparison
	// from '<' to '>' (see the return statements) to make it a MIN queue
	if (c1.key == c2.key) {
		return c1.secondaryKey > c2.secondaryKey;
	}

	return c1.key > c2.key;
}

typedef priority_queue<myC> myPQueue;
using   VecOfStr = vector<string>;

int main() {
	VecOfStr names = {"Tom", "Joe", "Bob", "Ben", "Jon", "Tim", "Jim", "Cam",
	                  "Jan", "Peg", "Sue", "Pat", "Pam", "Dee", "Kim", "Lee"};
	myPQueue q;
	myC      c;
	int      i;

	srand((unsigned int)time(0));

	for (i = 1; i <= (int) names.size(); i++) {
		c = myC(rand() % 10, i, names[i - 1]);
		q.push(c);
	}

	i = 1;
	while (!q.empty()) {
		c = q.top();
		cout << "Element " << setw(2)       << i       << ":  key = (" 
			<< c.getKey() << ","           << setw(2) << c.getSKey()  
			<< "), s = "  << c.getString() << "."     << endl;
		q.pop();
		i++;
	}

	return 0;
}
```

# Pair

**pair**: container that consists of two data elements. 

`#include <utility>` enables use of the pair class

A pair can be declared as `pair<F, S> newPair;` where F represents the pair's first element type and S represents the pair's second element type. 
	Ex: `pair<int, string> newPair;`

The make_pair() function creates a pair with the specified first and second values, with which a pair variable can be assigned. Each element in a pair can be accessed and modified using the pair's `first` and `second` members.

```c++
#include <iostream>
#include <string>
#include <utility>

using namespace std;

int main() {
   pair<string, int> caPair;
   
   // 2013 population data from census.gov
   caPair = make_pair("California", 38332521);
   
   cout << "Population of " << caPair.first << " in 2013 was "
        << caPair.second << "." << endl ;
   
   // 2010 population data from census.gov
   caPair.second = 37253965;
   
   cout << "Population of " << caPair.first << " in 2010 was "
        << caPair.second << "." << endl ;
   
   return 0;
}
```

# Map

**map**: container that associates (or maps) keys to values. 

`#include <map>` enables use

Generically, a map can be declared and created as `map<K, V> newMap;` where K represents the map's key type and V represents the map's value type.

The emplace() function associates a key with the specified value. If the key does not already exist, a new entry within the map is created. If the key already exists, the associated map entry is not updated. Thus, a map associates at most one value for a key.

The at() function returns the value associated with a key, such as `statePopulation.at("CA")`.

A map entry can be updated by assigning the entry with a new value. Ex: `statePopulation.at("CA") = 39776830;`

```c++
map<string, int> statePopulation;

// 2013 population data from census.gov
statePopulation.emplace("CA", 38332521);
statePopulation.emplace("AZ", 6626624);
statePopulation.emplace("MA", 6692824);
```

| Member function     | Use                                                                                            |
| ------------------- | ---------------------------------------------------------------------------------------------- |
| emplace(key, value) | Associates key with specified value. If key already exists, the map entry is not changed.      |
| at(key)             | Returns the entry associated with key. If key does not exist, throws an out_of_range exception |
| count(key)          | Returns 1 if key exists, otherwise returns 0.                                                  |
| erase(key)          | Removes the map entry for the specified key if the key exists                                  |
| clear()             | Removes all map entries.                                                                                               |

