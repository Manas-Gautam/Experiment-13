# Experiment-13
## Theory: - 

### Function and Operator Overloading in C++

In C++, overloading allows you to define multiple functions or operators with the same name but different parameter types or numbers of parameters. This helps in improving code readability and flexibility by enabling the same function or operator to perform different tasks based on the context of usage.

### 1. **Function Overloading:**

Function overloading is a feature in C++ that allows you to have more than one function with the same name but with different parameter types or a different number of parameters. The function that gets called is determined by the arguments passed during the function call (the signature of the function).

#### Characteristics of Function Overloading:
- Functions must have the **same name**.
- Functions must differ in **type** or **number** of parameters (the function signature).
- The **return type alone** cannot be used to distinguish between overloaded functions.

#### Example of Function Overloading:
```cpp
#include <iostream>
using namespace std;

class MyClass {
public:
    // Function to print an integer
    void display(int x) {
        cout << "Integer: " << x << endl;
    }

    // Function to print a double
    void display(double x) {
        cout << "Double: " << x << endl;
    }

    // Function to print two integers
    void display(int x, int y) {
        cout << "Integers: " << x << ", " << y << endl;
    }
};

int main() {
    MyClass obj;

    obj.display(5);          // Calls display(int)
    obj.display(3.14);       // Calls display(double)
    obj.display(10, 20);     // Calls display(int, int)

    return 0;
}
```

#### Output:
```
Integer: 5
Double: 3.14
Integers: 10, 20
```

In the above example, the `display()` function is overloaded three times: one version accepts an integer, another accepts a double, and the third accepts two integers.

#### Rules for Function Overloading:
1. **Different parameter types:** Functions can differ by the types of parameters.
   ```cpp
   void foo(int x);
   void foo(double x);
   ```
2. **Different number of parameters:** Functions can differ by the number of parameters.
   ```cpp
   void foo(int x);
   void foo(int x, int y);
   ```
3. **Not by return type alone:** Overloading is **not** allowed based only on the return type.
   ```cpp
   int foo(int x);   // Not allowed if the parameter list is identical.
   double foo(int x);
   ```

### 2. **Operator Overloading:**

C++ allows most of its built-in operators to be overloaded so that they can be used with user-defined data types (such as classes). Operator overloading allows you to define how an operator behaves when applied to objects of a class.

#### Characteristics of Operator Overloading:
- The **syntax** of operators cannot be changed, only their functionality.
- **Predefined operators** (such as `+`, `-`, `*`, `=`, etc.) can be overloaded.
- Some operators cannot be overloaded (e.g., `::`, `.*`, `.`, and `?:`).
- Operator overloading works like function overloading; the number or types of operands determine which version of the overloaded operator is used.
- **At least one operand** in an overloaded operator must be a user-defined type (class or struct).

#### Example of Operator Overloading:

Let's overload the `+` operator to add two objects of a class.

```cpp
#include <iostream>
using namespace std;

class Complex {
private:
    int real, imag;
public:
    Complex(int r = 0, int i = 0) : real(r), imag(i) {}

    // Operator overloading for '+' to add two Complex numbers
    Complex operator + (const Complex &obj) {
        Complex temp;
        temp.real = real + obj.real;
        temp.imag = imag + obj.imag;
        return temp;
    }

    void display() {
        cout << real << " + " << imag << "i" << endl;
    }
};

int main() {
    Complex c1(3, 4), c2(1, 2);
    Complex c3 = c1 + c2;  // Using the overloaded '+' operator

    c3.display();  // Output: 4 + 6i
    return 0;
}
```

#### Output:
```
4 + 6i
```

In this example, the `+` operator is overloaded to allow the addition of two `Complex` objects. The `operator +` function returns a new `Complex` object that contains the sum of the real and imaginary parts.

#### Types of Operators that Can Be Overloaded:
1. **Arithmetic operators**: `+`, `-`, `*`, `/`, `%`, etc.
2. **Relational operators**: `==`, `!=`, `<`, `>`, `<=`, `>=`
3. **Logical operators**: `&&`, `||`, `!`
4. **Assignment operators**: `=`, `+=`, `-=`, `*=`, `/=`
5. **Unary operators**: `++`, `--`, `-` (unary minus), `+` (unary plus)
6. **Subscript operator**: `[]`
7. **Function call operator**: `()`
8. **Dereferencing operators**: `*` (pointer dereference), `->` (member access via pointer)
9. **Input/output operators**: `<<`, `>>`

#### Example of Overloading `<<` and `>>`:
```cpp
#include <iostream>
using namespace std;

class Complex {
private:
    int real, imag;
public:
    Complex(int r = 0, int i = 0) : real(r), imag(i) {}

    // Overloading '<<' operator for output
    friend ostream& operator << (ostream &out, const Complex &c) {
        out << c.real << " + " << c.imag << "i";
        return out;
    }

    // Overloading '>>' operator for input
    friend istream& operator >> (istream &in, Complex &c) {
        cout << "Enter real part: ";
        in >> c.real;
        cout << "Enter imaginary part: ";
        in >> c.imag;
        return in;
    }
};

int main() {
    Complex c1;
    cin >> c1;  // Using the overloaded '>>' operator
    cout << "The complex number is: " << c1 << endl;  // Using the overloaded '<<' operator
    return 0;
}
```

### Output:
```
Enter real part: 3
Enter imaginary part: 4
The complex number is: 3 + 4i
```

## Experiment 13{ A }: - 

## Code: - 

#include <iostream>
using namespace std;

int add(int a, int b) {
    return a + b;
}

float add(float a, float b) {
    return a + b;
}

int add(int a, int b, int c) {
    return a + b + c;
}

int main() {
    cout << "Addition of 2 integers: " << add(3, 4) << endl;
    cout << "Addition of 2 floats: " << add(3.5f, 4.5f) << endl;
    cout << "Addition of 3 integers: " << add(1, 2, 3) << endl;
    return 0;
}

## Output: - 
![image](https://github.com/user-attachments/assets/b5e50f09-dabd-436b-aea5-dd9e03784313)


## Experiment 13{ B }: - 

## Code: - 
#include <iostream>
using namespace std;

class Complex {
    private:
        float real;
        float imag;
    public:
        Complex(float r = 0, float i = 0) {
            real = r;
            imag = i;
        }
        
        Complex operator + (const Complex &obj) {
            Complex temp;
            temp.real = real + obj.real;
            temp.imag = imag + obj.imag;
            return temp;
        }
        
        void display() const {
            cout << real << " + " << imag << "i" << endl;
        }
};

int main() {
    Complex c1(3.5, 2.5);
    Complex c2(1.6, 3.7);
    Complex c3 = c1 + c2;
    
    cout << "First complex number: ";
    c1.display();
    cout << "Second complex number: ";
    c2.display();
    cout << "Sum of complex numbers: ";
    c3.display();
    return 0;
}

## Output: - 
![image](https://github.com/user-attachments/assets/7ae88537-9c08-4e29-88d5-7fc4c38d2229)

### Conclusion:
- **Function overloading** provides flexibility by allowing multiple functions with the same name but different parameters, improving code clarity.
- **Operator overloading** extends the capabilities of existing operators to work with user-defined types, making operations on objects more intuitive and natural.
Both features enhance C++'s ability to work with complex data types and improve the overall expressiveness of the language.
