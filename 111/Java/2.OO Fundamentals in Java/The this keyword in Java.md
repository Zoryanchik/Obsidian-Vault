![[Pasted image 20250219213549.png]]![[Pasted image 20250219213737.png]]
### **ys:**

- `this` refers to the **current object** in which it is used.
- It helps **differentiate** between instance variables and parameters.
- It can be used to **call other methods** or **pass the current object** to another method


class Car {
    void printCar(Car c) {
        System.out.println("Car: " + c);
    }

    void show() {
        printCar(this); // Passes the current object
    }
}
