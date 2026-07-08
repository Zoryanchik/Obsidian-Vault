/*
   to make a local copy
  git clone link 

    git status to show untacked files and change it to tracked
    git add <filename>  add a new file to repo
    git commit -m "  " add a note
    git push origin main to propagate your commits back to server
    git pull explicity mergin them into your repo,k update
    .gitignore *.class
    merge conflict git add git commit
    git chekout some-feauture - switch to diff brunch
    git checkout main  merge two branches
    git merge some - feasture 

    CI is a software development practice where developers regularly integrate
their code changes into a central repository.
• Each integration is verified by an automated build and automated tests

CD is the next step in the CI/CD pipeline, where the code that passes CI
is automatically deployed to a beta production environment.

INHERITANCE
One class can inherit from, be derived from, or extend another to create new class. 
The class being extended is known as the base class, super class or the parent class.
• The new class is known as a subclass of the other.
public class Lecturer extends Person
{
 ...
}
    public class bishop extends chesspiefce
    public bishop(chess squarev s ){
    super( )} to all cthe onstrucvtor method of our super class

Polymorhism 
• Therefore, any class can be treated as a type of its super class.
Any object instance of a class that extends another can be treated as an object of that class
• but only if the underlying object is the same class or a subclass of the type you are casting to

ChessPiece c, c2;
Prawn p, p2;
p = new Prawn();
c = p;
p2 = (Prawn) c;

Abstrat c
public abstract class ChessPiece
{
public abstract boolean canMoveTo(ChessSquare s);
An Interface is a named specification of zero or more methods
A complete definition of Polymorphism in Java:
• A class can be treated as a type of its class, any of its super classes, or any of the interfaces it
implements

public interface UniversityMember
{
public void sleep();
public void drinkCoffee();
public void work();
}

// Parent class
class Person {
    String username;

    // Constructor for Person
    public Person(String username) {
        this.username = username;
    }
}

// Child class
public class Student extends Person {
    int studentID;
    String college;

    // Constructor for Student
    public Student(int studentID, String username, String college) {
        super(username); // Call to Person's constructor
        this.studentID = studentID;
        this.college = college;
    }

    // Display student details
    public void displayInfo() {
        System.out.println("Student ID: " + studentID);
        System.out.println("Username: " + username);
        System.out.println("College: " + college);
    }

    public static void main(String[] args) {
        Student s1 = new Student(101, "john_doe", "Harvard University");
        s1.displayInfo();
    }
}

*/
