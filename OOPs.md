
# C++ OOP Cheat Sheet

---

## 1. Classes and Objects
- **Class**: Blueprint for creating objects.
- **Object**: Instance of a class.

   ```cpp
   class Car {
   public:
       string brand;
       int year;
       void drive() {
           cout << "Driving" << endl;
       }
   };
   Car myCar;
   myCar.drive();  // Object calling method
   ```

## 2. Access Modifiers
- **public**: Accessible from outside the class.
- **protected**: Accessible in the class and derived classes.
- **private**: Accessible only within the class itself.

## 3. Constructors and Destructors
- **Constructor**: Initializes objects; same name as the class.
- **Destructor**: Cleans up; same name as the class with `~`.

   ```cpp
   class Car {
   public:
       Car() { cout << "Car created" << endl; } // Constructor
       ~Car() { cout << "Car destroyed" << endl; } // Destructor
   };
   ```

## 4. Inheritance
- Reusing properties and methods from an existing class.
- **Syntax**: `class Derived : accessModifier Base { ... };`

   ```cpp
   class Vehicle {
   public:
       int speed;
   };
   class Car : public Vehicle {
   public:
       void honk() { cout << "Honk!" << endl; }
   };
   Car myCar;
   ```

## 5. Polymorphism
- **Compile-time** (Function Overloading and Operator Overloading)
- **Runtime** (Virtual functions, achieved with pointers/reference)

   ```cpp
   class Animal {
   public:
       virtual void sound() { cout << "Some sound" << endl; }
   };
   class Dog : public Animal {
   public:
       void sound() override { cout << "Woof!" << endl; }
   };
   Animal* a = new Dog();
   a->sound();  // Runtime Polymorphism
   ```

## 6. Encapsulation
- Wrapping data and functions into a single unit (class).
- Control access using private/public methods.

   ```cpp
   class Account {
   private:
       double balance;
   public:
       void deposit(double amount) { balance += amount; }
       double getBalance() { return balance; }
   };
   ```

## 7. Abstraction
- Hiding implementation details and exposing only essential features.
- Achieved using pure virtual functions in abstract classes.

   ```cpp
   class Shape {
   public:
       virtual void draw() = 0;  // Pure virtual function
   };
   class Circle : public Shape {
   public:
       void draw() override { cout << "Circle drawn" << endl; }
   };
   ```

## 8. Function Overloading and Operator Overloading
- **Function Overloading**: Same function name, different parameters.
- **Operator Overloading**: Custom implementation for operators.

   ```cpp
   class Complex {
   public:
       int real, imag;
       Complex operator + (const Complex& obj) {
           Complex temp;
           temp.real = real + obj.real;
           temp.imag = imag + obj.imag;
           return temp;
       }
   };
   ```

## 9. This Pointer
- Represents the calling object in a member function.

   ```cpp
   class Person {
   public:
       int age;
       Person(int age) { this->age = age; }
   };
   ```

## 10. Static Members
- **Static Variable**: Shared among all objects of the class.
- **Static Method**: Can be called without an object.

   ```cpp
   class Counter {
   public:
       static int count;
       Counter() { count++; }
       static int getCount() { return count; }
   };
   int Counter::count = 0;
   ```

## 11. Friend Functions
- Functions declared with the `friend` keyword can access private/protected data of a class.

   ```cpp
   class Box {
   private:
       int width;
   public:
       friend void setWidth(Box &box, int w);
   };
   void setWidth(Box &box, int w) { box.width = w; }
   ```

## 12. Pointers and Dynamic Memory in Classes
- **`new` and `delete`** are used to allocate and deallocate memory dynamically.

   ```cpp
   class Test {
   public:
       int* data;
       Test(int value) { data = new int(value); }
       ~Test() { delete data; }
   };
   ```

---

## Introduction to OOP
- **Definition**: A programming paradigm that organizes code into modules, called objects or classes, which can be
reused and combined in various ways.
- **Key Idea**: Encapsulate data within objects, separating the public interface from internal details.

---

## Components of OOP

### 1. Objects
- **Concept**: An object is an instance of a class.
- **Attributes/Properties**: Data stored within the object (e.g., color, year).
- **Methods/Behaviors**: Operations performed on objects (e.g., print, move).

**Example**: A user account in a banking system has attributes like balance and methods for depositing and
withdrawing money.

---

### 2. Encapsulation
- **Encapsulation**: Prevents direct access to internal state except through a public method.
- **Access Control**: Data is locked away from external code (e.g., password manager).
- **Hiding Details**: Data is not exposed, maintaining privacy.

**Example**: A password manager protects user passwords from being accessed directly.

---

### 3. Inheritance
- **Inheritance**: Subclassing allows one class to include the behaviors of another.
- **Overloading Methods**: Shared methods (e.g., print) are defined in subclasses or interfaces.
- **Code Redundancy**: One class handles attributes, others implement behaviors.

**Example**: A base class Animal with a print method, and subclasses Dog and Cat that override the print method
for specific actions.

---

### 4. Polymorphism
- **Polymorphism**: Objects can adapt to various forms based on context.
- **Adaptability**: An object's behavior is defined by multiple interfaces or implementations.
- **Contextual Flexibility**: Allows different behaviors in similar situations.

**Example**: Adding integers and doubles without checking their types, relying on polymorphism for flexibility.

---

## Applications and Benefits of OOP

1. **Reusability**: Repeated structures can be encapsulated within a class.
2. **Maintainability**: Clear separation of concerns through inheritance.
3. **Problem Solving**: Abstraction allows focused attention on specific tasks without considering complexity.
4. **Code Quality**: Hidden details reduce exposure and potential bugs.

**Example**: Using Object-Oriented Design to design a library system, where books are objects, classes represent
genres, authors, etc., facilitating easy maintenance and reuse of code.

---

## Summary
Object-Oriented Programming (OOP) is a fundamental approach in software development that emphasizes data
abstraction and object-oriented principles. By encapsulating data, promoting inheritance, and allowing
polymorphism, OOP enhances code organization, maintainability, and functionality. Understanding these components
provides a solid foundation for effective software design.

---