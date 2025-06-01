![[Pasted image 20250415193507.png]]
![[Pasted image 20250415192853.png]]![[Pasted image 20250415192907.png]]![[Pasted image 20250415193157.png]]![[Pasted image 20250415193244.png]]![[Pasted image 20250415193348.png]]![[Pasted image 20250415193521.png]]
Student.university will change all their uni from Lancaster to Manchester 
```
# Define a class
class Person:
    # Constructor (called when a new object is created)
    def __init__(self, name, age):
        self.name = name  # Instance variable
        self.age = age

    # Method (function that belongs to the class)
    def greet(self):
        print(f"Hi, my name is {self.name} and I am {self.age} years old.")

# Create objects (instances of the class)
person1 = Person("Alice", 30)
person2 = Person("Bob", 25)

# Call methods
person1.greet()
person2.greet()

# Inheritance: Create a class that inherits from Person
class Student(Person):
    def __init__(self, name, age, student_id):
        super().__init__(name, age)  # Call the parent constructor
        self.student_id = student_id

    def greet(self):
        # Override the parent method
        print(f"I'm {self.name}, a student with ID {self.student_id}.")

# Create a Student object
student1 = Student("Charlie", 20, "S12345")
student1.greet()

# Polymorphism: Using the same method name for different classes
def introduce(person):
    person.greet()

introduce(person1)   # Calls Person.greet
introduce(student1)  # Calls Student.greet

```