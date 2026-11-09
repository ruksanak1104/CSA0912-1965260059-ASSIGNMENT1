1) Abstraction in Java

Abstraction is an object-oriented programming concept that hides implementation details and shows only essential features to the user.
In the parking management system, abstraction is implemented using abstract classes and interfaces.
It separates what an object should do from how it performs the operation.

2) Abstract Class – Vehicle

The Vehicle class is designed as an abstract class because all vehicles share common properties, but their parking fee calculations may differ.

Fields:
•	String regNo – Stores the vehicle registration number.

•	String vehicleType – Stores the vehicle type.

•	double parkingRate – Stores the parking rate.

Methods:

1.	getRegNo() – Returns the registration number.

2.	displayDetails() – Displays vehicle information.

3.	calculateFee() – Abstract method implemented by subclasses.

Example:

abstract class Vehicle {

    String regNo;
    
    String vehicleType;

    Vehicle(String regNo, String vehicleType) {
        this.regNo = regNo;
        this.vehicleType = vehicleType;
    }

    abstract double calculateFee(double hours);

    void displayDetails() {
        System.out.println("Vehicle No: " + regNo);
        System.out.println("Vehicle Type: " + vehicleType);
    }
}

The abstract method does not contain a method body. Subclasses provide their own implementation.

3)Interface – Chargeable

The Chargeable interface represents the charging capability of electric vehicles.
It is used because not every vehicle supports electric charging.

Example:

interface Chargeable {

    double chargingFee(int kWh);

    default void chargingStatus() {
        System.out.println("Vehicle is charging");
    }

    static void chargingInfo() {
        System.out.println("Charging rate: Rs.12 per kWh");
    }
}

Here:

•	chargingFee() calculates the charging cost.

•	chargingStatus() is a default method that provides a common implementation.

•	chargingInfo() is a static method that provides general charging information.

4) Implementation of Abstract Class and Interface

A class can extend one abstract class and implement multiple interfaces.

Example:

class Car extends Vehicle {

    Car(String regNo) {
        super(regNo, "Car");
    }

    @Override
    double calculateFee(double hours) {
        return hours * 30;
    }
}

class ElectricCar extends Car implements Chargeable {

    ElectricCar(String regNo) {
        super(regNo);
    }

    @Override
  
    public double chargingFee(int kWh) {
        return kWh * 12;
    }
}

Here:

•	Car inherits common properties from Vehicle.

•	ElectricCar inherits Car's properties and methods.

•	ElectricCar implements Chargeable to support charging operations.

This demonstrates how Java supports multiple behaviours through interfaces.

5) Why Abstract Class and Interface Are Used

Abstract Class:

•	Used when multiple classes share common fields and methods.

•	Supports constructors and instance variables.

•	Provides both abstract and concrete methods.

•	Suitable for the Vehicle hierarchy.

Interface:

•	Used to represent additional capabilities.

•	Does not require classes to share the same parent class.

•	Allows a class to implement multiple interfaces.

•	Suitable for charging and payment capabilities.
Therefore, Vehicle is an abstract class because vehicles share common data, whereas Chargeable is an interface because charging is an additional capability supported only by certain vehicles.

6) Alternative Concept and Complexity Analysis

Suppose Vehicle is changed into an interface with default methods and Chargeable is changed into an abstract class.

A. Vehicle as an Interface

interface Vehicle {

    String getRegNo();

    default void displayDetails() {
        System.out.println("Vehicle Details");
    }

    double calculateFee(double hours);
}

Here, common behaviour can be provided through default methods, and subclasses must implement the abstract methods.
However, an interface cannot have constructors or ordinary instance fields to store individual vehicle state. It cannot replace the Vehicle abstract class directly when constructor-based common initialization is required.

B. Chargeable as an Abstract Class

abstract class Chargeable {

    abstract double chargingFee(int kWh);

    void chargingStatus() {
        System.out.println("Charging in progress");
    }
}
In this approach, ElectricCar would need to extend Chargeable instead of implementing it.

Limitations of the Alternative Approach

1.	Constructors: Interfaces cannot have constructors, whereas abstract classes support constructors.

2.	Instance State: Interfaces cannot maintain ordinary per-object instance variables.

3.	Multiple Inheritance: Java allows a class to implement multiple interfaces but extend only one class. If Chargeable becomes an abstract class, a class cannot extend both Car and Chargeable.

4.	Flexibility: Using interfaces for additional capabilities makes the design more flexible.

Complexity Analysis

1. Method Execution Time:

•	Abstract class methods and interface methods both generally take O(1) time when their implementation performs a fixed number of operations.

•	There is no meaningful asymptotic time complexity difference between the two approaches.

2. Space Complexity:

•	Abstract class objects require memory for their inherited instance fields.

•	Interfaces do not add ordinary per-object instance fields.

•	Changing Chargeable into an abstract class may introduce additional instance fields and object state.
The overall space depends on the fields stored in each object and the number of objects created.

7) Conclusion

Abstraction improves the design of the parking management system by separating common vehicle properties from specific vehicle behaviours. The abstract Vehicle class provides common structure, while the Chargeable interface represents the additional charging capability of electric vehicles. This approach improves flexibility, reusability and maintainability while supporting multiple behaviours through interfaces.


