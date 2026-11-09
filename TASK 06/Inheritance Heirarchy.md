1) Inheritance Hierarchy

Inheritance is an important feature of Java that allows one class to acquire the properties and methods of another class.
For the parking management system, Vehicle is the superclass, and Car, Bike and ElectricCar are subclasses.
Superclass: Vehicle
The Vehicle class contains common fields and methods shared by all vehicles.

Fields:
•	String vehicleNo
•	String vehicleType
•	double parkingRate

Methods:
•	displayDetails()
•	calculateFee()

Subclasses:
1.	Car: Inherits the common vehicle details and adds a field such as int numberOfDoors.
2.	Bike: Inherits the common vehicle details and adds a field such as int engineCC.
3.	ElectricCar: Inherits the properties of Car and adds a field such as double batteryCapacity.

This design uses:
•	Hierarchical Inheritance: Car and Bike inherit from Vehicle.
•	Multilevel Inheritance: ElectricCar inherits from Car, which inherits from Vehicle.

2) What Is Inherited and What Is Added?

Vehicle Class:
Contains common vehicle information such as registration number, type and parking rate.
Car Class:
Inherits vehicle number, vehicle type and parking rate from Vehicle. Adds the number of doors.
Bike Class:
Inherits common vehicle properties from Vehicle. Adds engine capacity.
ElectricCar Class:
Inherits vehicle properties from Vehicle through Car. Adds battery capacity and other electric vehicle details.
Inheritance avoids code duplication and improves code reusability.

3)Use of super Keyword

The super keyword is used to refer to the immediate parent class.
It is used in three ways:

A. Accessing Parent Class Constructor
super(vehicleNo, vehicleType, parkingRate);
It calls the parent class constructor to initialize inherited fields.

B. Accessing Parent Class Method
super.displayDetails();
It calls the parent class method from the subclass.

C. Accessing Parent Class Field
super.vehicleNo
It accesses the parent class field when required, especially when a subclass has a field with the same name.


4) Java Program Demonstrating Inheritance

class Vehicle {
   
    String vehicleNo;
    String vehicleType;
    double parkingRate;

    Vehicle(String vehicleNo, String vehicleType, double parkingRate) {
        this.vehicleNo = vehicleNo;
        this.vehicleType = vehicleType;
        this.parkingRate = parkingRate;

        System.out.println("Vehicle Constructor");
    }

    void displayDetails() {
        System.out.println("Vehicle No: " + vehicleNo);
        System.out.println("Vehicle Type: " + vehicleType);
    }
}

class Car extends Vehicle {
   
    int numberOfDoors;

    Car(String vehicleNo, double parkingRate, int doors) {
        super(vehicleNo, "Car", parkingRate);
        this.numberOfDoors = doors;

        System.out.println("Car Constructor");
    }
}

class ElectricCar extends Car {
   
    double batteryCapacity;

    ElectricCar(String vehicleNo, double rate,
                int doors, double battery) {

        super(vehicleNo, rate, doors);
        this.batteryCapacity = battery;

        System.out.println("ElectricCar Constructor");
    }
}

public class Main {
    
    public static void main(String[] args) {

        ElectricCar e = new ElectricCar(
            "TN01AB1111", 20, 4, 75
        );

        e.displayDetails();

        System.out.println("Doors: " + e.numberOfDoors);
        System.out.println("Battery: " + e.batteryCapacity + " kWh");
    }
}

5)Constructor Execution Order (Trace)

When an ElectricCar object is created, constructors execute from the superclass to the subclass.
Example:

ElectricCar e = new ElectricCar(“TN01AB1111”, 20, 4, 75);
Execution order:
1.	ElectricCar constructor is called.
2.	super() calls the Car constructor.
3.	Car constructor calls the Vehicle constructor using super().
4.	Vehicle constructor executes first.
5.	Car constructor executes next.
6.	ElectricCar constructor executes last.

Output:

Vehicle Constructor
Car Constructor
ElectricCar Constructor
Vehicle No: TN01AB1111
Vehicle Type: Car
Doors: 4
Battery: 75.0 kWh


6) Alternative Concept: Composition vs Inheritance

Instead of inheritance, composition can be used by creating a single Vehicle class that contains a VehicleType object.
Composition Approach:
A Vehicle object has a VehicleType object that stores the vehicle category and parking rate.

Example:

class VehicleType {
    
    String type;
    double rate;

    VehicleType(String type, double rate) {
        this.type = type;
        this.rate = rate;
    }
}

class Vehicle {
   
    String vehicleNo;
    VehicleType vehicleType;

    Vehicle(String vehicleNo, VehicleType vehicleType) {
        this.vehicleNo = vehicleNo;
        this.vehicleType = vehicleType;
    }

    double calculateFee(double hours) {
        return hours * vehicleType.rate;
    }
}

Here, different vehicle types can be created using different VehicleType objects without creating separate subclasses.
Comparison and Analysis:

1.	Adding a New Vehicle Type:

o	In inheritance, a new subclass must be created for every new vehicle type.

o	In composition, a new VehicleType object can be created with the required rate.

2.	Fee Calculation:

o	In inheritance, the appropriate subclass method calculates the parking fee.

o	In composition, the Vehicle class accesses the rate from its VehicleType object.

o	Both approaches take O(1) time when the rate is already available.

3.	Space Per Vehicle:

o	In inheritance, each vehicle object stores its common fields and subclass-specific fields.

o	In composition, each vehicle stores a reference to a VehicleType object, which also requires memory.

o	If VehicleType objects are shared, memory can be saved by avoiding repeated storage of type information and rates.

4.	Flexibility:

o	Inheritance is suitable when vehicle types have different behaviours.

o	Composition is suitable when vehicle types mainly differ in their properties, such as parking rates.

8) Conclusion
Inheritance is suitable for the parking management system because Car, Bike and ElectricCar share common vehicle properties but also have their own specific attributes. The super keyword helps initialize parent class data and reuse parent methods. Composition is an alternative that provides greater flexibility when adding new vehicle types with different parking rates.
















