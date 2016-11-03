# CppStyleGuide

[![Version](https://img.shields.io/badge/version-v1.0.1-green.svg)](https://github.com/illescasDaniel/CppStyleGuide/releases)

* [Naming](#naming)
* [Braces & Indentation](#braces--indentation)
* [Best practices](#best-practices)
* [Comments](#comments)

Naming
------

* Names should be descriptive and clear and contain only letters. 
* Abbreviations and acronyms should generally be avoided.  
* Don't worry about the name length, `int a` is not better than `int age`. 
* Variable names could contain more than one word if it looks more clear.

**Syntax styles:**

Upper case: House  
Lower case: home  
Upper camel case: HouseOfDaniel  
Lower camel case: numberOfHouses  

**Classes and Structs:**  
The first letter always in **upper** case, use **upper camel case syntax**. If is possible use only one word.

```c++ 
class Human { 
};
```

**Variables:**  
The first letter always in **lower** case, use **lower camel case** syntax.  

```c++
string name;
float moneyOnBank = 30.6;
```

**Constants:**  

* If it's a local or non global constant, use lower camel case syntax. 
* If it's a global constant you might want to use the whole name in upper case and use underscores to separate words.   

**Source Files:**

Classes should be defined in one file or two separeted files, one for headers and the other for the methods.  
Another class can be implemented on the same file only if they are very related, like nested clases or similar.

If the file contains a class named "Human" the source file should be "Human.h" for the headers and "Human.cpp" for the methods; or "Human.hpp" if you implement the entire class in one file.

* Use ".h" for header only classes or structures.
* ".cpp" for the methods implementation of classes and for the "main.cpp"
* ".hpp" for classes and it's method implementation.

Braces & Indentation
------
Use one tab character equivalent to 4 spaces for indentation.

Use K&R style with opening braces on the same line:  

```c++
int main() {
	
	bool compiles = true;
	
	if (compiles) {
		beHappy();
	}
	else {
		cry();
	}	
}

void beHappy() {
	cout << "Being happy..." << endl;
}

void beHappy() {
	cout << "Crying..." << endl;
}
```

You can also use opening braces on a different line if it's a **function**.

Best practices:
------

**Variables:**

Let's take a look at this example:

```c++ 
int johnAge = 10;
```

Why use "int" in a variable that is not suppose to be bigger than ~150?

Try to use a variable that fits better, like uint8_t, which is an unsigned number from 0 to 256.  
Why? Because it uses less memory, 8 bits instead of 32 :)

However try to avoid maths when using unsigned values:

``` c++
unsigned int age = 1;  
cout << (age > -1) << endl; // Output: false
```

Write same variables types in adjacent lines or in the same line:

```c++

// BAD
double myMoney;
int number;
double yourMoney;
int anotherNumber;

// GOOD
double myMoney, yourMoney;
int number;
int anotherNumber;

```

**Classes:**

We could use two different styles:  
a. Define the entire class in one file.  
b. Define the headers of the class in one file and the implementation in other.

a) 
Use default member values when they're always initialized with the same value, unless the value is different depending on the constructor, then initialize those values inside each constructor.  
Try to avoid empty constructors, the uninitialized members has undefined values (use default member to avoid this, if you want).

```c++
class Human {
	
	uint8_t age;
	uint8_t numberOfarms = 2;
	string name;
	bool isDisabled = false;
	
	Human(const uint8_t& age, const string& name) {
		this->age = age;
		this->name = name;
	}
	
	Human(const uint8_t& age, const string& name, const bool& isDisabled) {
		this->age = age;
		this->name = name;
		this->isDisabled = isDisabled;
	}
	
	void setAge(const uint8_t& newAge) {
		age = newAge;	
	}
	
	void setNumberOfArms(const uint8_t& newNumberOfArms) {
		if (isDisabled) {
			numberOfArms = newNumberOfArms;
		}
		// ...
	}
	
	// ...
};

```

**Main function:**

You don't need to type `return 0;` at the end.

> 4) The body of the main function does not need to contain the return statement: if control reaches the end of main without encountering a return statement, the effect is that of executing return 0; 

**For loops:**

Avoid old for loops when iterating through a range of elements:

```c++
	
	int numbers[] = {-1,2,3};
	vector<string> names = {"Daniel", "John", "Peter"};
		
	// Classic for
	
	for (uint8_t i = 0; i < 3; ++i) { // Use "size_t" for large vectors
		cout << numbers[i];
	}
	
	for (vector<string>::iterator it = names.begin(); it != names.end(); ++it) {
		cout << *it << ' ';
	}
	
	
	// For-range loop
	
	for (int number: numbers) {
		cout << number << ' ';
	}
	
	for (auto name: names) {
		cout << name << ' ';
	}

```

Comments:
-----

Make comments about something that is harder to understand (like an algorithm) or to clarify something:

```c++

/* BAD */

// Main function
int main() {
	
	// This is the number of apples
	int n;
	
	// The name of the shop
	string s;
	
	// Print text (xD)
	cout << "Daniel bought " << n << " apples in " << str << endl;
}

/* GOOD */

int main() {
	
	string name = "Daniel";
	string lastName = "ILLESCAS";
	float height = 170.0;

	// Print the name in upper case
	for (char letter: name) {
		cout << char(toupper(letter));
	}
	
	cout << toLower(lastName) << endl;
}

string toLower(string str) {
	transform(str.begin(), str.end(), str.begin(), ::tolower);
	return str;
}

```
