# [CppStyleGuide](https://github.com/illescasDaniel/CppStyleGuide)

Simple style guide for C++ code, could also be applied to other languages such as C or Java.

## Table of contents

-   [Naming](#naming)
-   [Braces & Indentation](#braces--indentation)
-   [Best practices](#best-practices)
-   [Comments](#comments)

## Naming

-   Names should be descriptive and clear and contain only letters. 
-   Abbreviations and acronyms should generally be avoided.  
-   Don't worry about the name length, `int a` is not better than `int age`. 
-   Variable names could contain more than one word if it looks more clear.

**Syntax styles:**

Upper case: NUMBER  
Lower case: home  
Upper camel case: HouseOfDaniel  
Lower camel case: numberOfHouses  

**Classes and Structs:**  

The first letter always in **upper** case, use **upper camel case syntax**.

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

-   If it's a local or non global constant, use **lower camel case** syntax. 
-   If it's a global constant you can type the whole name in **upper case** and use underscores to separate words.   

**Source Files:**

Classes should be defined in one or two separated files, one for the headers and the other for the methods.  
Another class can be implemented on the same file only if they are very related, like nested clases or similar.

If the file contains a class named "Human", the source file should be "Human.h" for the headers and "Human.cpp" for the methods; or "Human.hpp" if you implement the entire class in one file.

-   Use ".h" for header only classes or structures.
-   ".cpp" for the methods implementation of classes and for the "main.cpp"
-   ".hpp" for classes and it's method implementation.

## Braces & Indentation

Use a tab character equivalent to 4 spaces for indentation.

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



## Best practices:

**Variables:**

Let's take a look at this example:

```c++ 
int johnAge = 10;
```

Why use "int" in a variable that is not suppose to be bigger than ~150?

-   Try to use a variable that fits better, like **uint8_t** (unsigned char), which is an unsigned number from 0 to 256.  

Why? Because it uses less memory, 8 bits instead of 32 :)

However, try to **avoid maths when using unsigned values**:

```c++
unsigned int age = 1;  
cout << (age > -1) << endl; // Output: false
```

-   Write same variables types in adjacent lines or in the same line:

```c++
// BAD
double myMoney;
int number;
double yourMoney;
int anotherNumber;

// GOOD
double myMoney, yourMoney;
int anotherNumber;
int number;
```

-   Try to use `true` or `false` with bool variables instead of `1` or `0`.

    You can also use `boolalpha` to print true or false instead of one or cero:

    ```c++
    int main() {
    	bool isCool = true;
      	cout << boolalpha << isCool << endl; // Output: true
      
      	// OR:
      	boolalpha(cout);
      	cout << isCool << endl;
    }
    ```

**Classes:**

We could use two different styles:  

-   Define the entire class in one file.  
-   Define the headers of the class in one file and the implementation in other.

**Use default member values** when they're always initialized with the same value, unless the value is different depending on the constructor, then initialize those values individually.  

Try to **avoid empty constructors**, the uninitialized members has undefined values (use default member to avoid this, if you want).

```c++
class Human {
	
	string name;
	uint8_t age;
  
public:
	Human(const uint8_t& age, const string& name) {
		this->age = age;
		this->name = name;
	}
	
	void setAge(const uint8_t& newAge) {
      	if (newAge <= 150) {
        	age = newAge;	  
      	}
	}
  
  	bool isAdult() {
    	return (age >= 18);
  	}
	// ...
};
```

**Main function:**

You don't need to type `return 0;` at the end.

>   4) The body of the main function does not need to contain the return statement: if control reaches the end of main without encountering a return statement, the effect is that of executing `return 0;` 

***for* loops:**

Avoid old for loops when iterating through a range of elements:

```c++
	
int numbers[] = {-1,2,3};
vector<string> names = {"Daniel", "John", "Peter"};
	
// Classic for

for (uint8_t i = 0; i < 3; ++i) { // Use "size_t" for large vectors
	cout << numbers[i] << ' ';
}

for (vector<string>::iterator it = names.begin(); it != names.end(); ++it) {
	cout << *it << ' ';
}

// Range-based for loop

for (const int& number: numbers) {
	cout << number << ' ';
}

for (const auto& name: names) { // "auto" is a string in this case
	cout << name << ' ';
}
```

**Extra:**

-   Leave a blank line at the end of each file.
-   Compile your code with `-O2` or `-O3` for better performance, use `-Os` for smaller binary file size.
-   Use C++14 (or newer) compiler flag: `-std=c++14`
-   Use `-Wall` and/or `-Wextra` when debuggin to show more warnings.

## Comments:

-   Comments should be on different lines than code (except for short comments in-line) and with a space between `//` and the comment.
-   Try to use the second person:

```c++
// Sort a range of elements in a custom order using QuickSort algorithm
template <typename Type, typename Function>
void quickSort(const vector<Type>& elements, const Function& order) { /*...*/ }
```



-   Make comments about something that is a bit hard to understand (like an algorithm) or to clarify something:

```c++
/* BAD! */

// Main function
int main() {
	
	// This is the number of apples
	int a;
	
	string s;
	
	// Print text c:
	cout << "Daniel bought " << a << " apples in " << s << endl;
}

/* GOOD */

int main() {
	
	string name = "Daniel";
	string lastName = "ILLESCAS";
	float height = 170.0; // in meters

	// Print the name in upper case
	for (char letter: name) {
		cout << char(toupper(letter));
	}
	
	cout << toLower(lastName) << endl;
}

// Transform a string to lower case
string toLower(string str) {
	transform(str.begin(), str.end(), str.begin(), ::tolower);
	return str;
}
```
