
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