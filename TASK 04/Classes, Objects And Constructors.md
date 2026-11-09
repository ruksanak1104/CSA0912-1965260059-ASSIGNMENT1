1) Classes, Fields and Methods

The parking management system is designed using four main classes. Each class represents a real-world entity and performs a specific responsibility.
1. Vehicle Class
Fields:
•	String vehicleNo – Stores the vehicle registration number.
•	String vehicleType – Stores the type of vehicle.
•	String entryTime – Stores the vehicle entry time.
Methods:
•	displayDetails() – Displays vehicle information.
•	getVehicleNo() – Returns the vehicle registration number.

2) ParkingSlot Class
Fields:
•	int slotNo – Stores the parking slot number.
•	boolean isOccupied – Indicates whether the slot is occupied.
•	Vehicle vehicle – Stores the vehicle occupying the slot.
Methods:
•	allocate() – Allocates a vehicle to the slot.
•	release() – Makes the slot available.



3) ParkingTicket Class
Fields:
•	int ticketNo – Stores the unique ticket number.
•	Vehicle vehicle – Stores vehicle details.
•	String entryTime – Stores the entry time.
•	String exitTime – Stores the exit time.
Methods:
•	generateTicket() – Generates a parking ticket.
•	displayTicket() – Displays ticket details.

4) ParkingLot Class
Fields:
•	ParkingSlot[][] slots – Stores parking slots on different floors.
•	int totalFloors – Stores the total number of floors.
Methods:
•	allocateSlot() – Finds and allocates a free slot.
•	releaseSlot() – Releases an occupied slot.
•	displayAvailableSlots() – Displays available parking slots.

2) Constructors and Their Uses
A constructor is a special method used to initialize objects when they are created.
Java supports the following types of constructors:

A. Default Constructor
A constructor without parameters.
Example:
class Vehicle {
    String vehicleNo;
    String vehicleType;

    Vehicle() {
        vehicleNo = "Not Assigned";
        vehicleType = "Unknown";
    }
}
It is used when an object needs default values.

B. Parameterized Constructor
A constructor that accepts parameters to initialize object fields.
class Vehicle {
    String vehicleNo;
    String vehicleType;

    Vehicle(String vehicleNo, String vehicleType) {
        this.vehicleNo = vehicleNo;
        this.vehicleType = vehicleType;
    }
}
It is used when vehicle details are available during object creation.

C. Overloaded Constructors
Multiple constructors in the same class with different parameter lists are called overloaded constructors.
class Vehicle {

    String vehicleNo;
    String vehicleType;

    Vehicle() {
        this("Not Assigned", "Unknown");
    }

    Vehicle(String vehicleNo) {
        this(vehicleNo, "Car");
    }

    Vehicle(String vehicleNo, String vehicleType) {
        this.vehicleNo = vehicleNo;
        this.vehicleType = vehicleType;
    }
}
Overloaded constructors allow objects to be created with different levels of information.

3) Use of this Keyword and Constructor Chaining
The keyword refers to the current object.
It is used to distinguish instance variables from constructor parameters having the same name.
Example:
Vehicle(String vehicleNo, String vehicleType) {
    this.vehicleNo = vehicleNo;
    this.vehicleType = vehicleType;
}
Constructor Chaining:
Constructor chaining means calling one constructor from another using this().
Example:
Vehicle() {
    this("Not Assigned", "Unknown");
}
It avoids repeating initialization code and improves code reusability.
The this() statement must be the first statement inside a constructor.

4) Need for a Copy Constructor
A copy constructor creates a new object using the values of an existing object.
Example:
class ParkingTicket {

    int ticketNo;
    String vehicleNo;

    ParkingTicket(int ticketNo, String vehicleNo) {
        this.ticketNo = ticketNo;
        this.vehicleNo = vehicleNo;
    }

    ParkingTicket(ParkingTicket t) {
        this.ticketNo = t.ticketNo;
        this.vehicleNo = t.vehicleNo;
    }
}
A copy constructor can be useful when creating a duplicate ticket record for reference or backup purposes.
However, a copied ticket should not be treated as a new valid parking ticket with the same ticket number. Every newly issued ticket must have a unique number.

5) Object Creation and Memory Allocation
In Java, objects are created using the new keyword.
Example:
Vehicle v1 = new Vehicle("TN01AB1111", "Car");

Memory allocation happens in two main areas:
1.	Stack Memory: Stores local variables and reference variables such as v1.
2.	Heap Memory: Stores the actual objects created using the new keyword.
The reference variable v1 stores the reference to the Vehicle object in heap memory.
When multiple reference variables point to the same object, they access the same object.

6) Alternative Concept and Complexity Analysis
Instead of using overloaded constructors, objects can be created using default constructors followed by setter methods or static factory methods.
A. Default Constructor with Setter Methods
Example:
Vehicle v = new Vehicle();

v.setVehicleNo("TN01AB1111");
v.setVehicleType("Car");

In this approach, an object is created first and its fields are initialized later using setter methods.
Advantages:
•	Easy to modify object values.
•	Flexible object initialization.
Disadvantages:
•	Objects may contain incomplete or invalid data before setters are called.
•	Requires additional validation.


B. Static Factory Methods
A static factory method creates and returns an object without directly calling its constructor from outside the class.
Example:
class ParkingTicket {

    int ticketNo;
    String vehicleNo;

    private ParkingTicket(int ticketNo, String vehicleNo) {
        this.ticketNo = ticketNo;
        this.vehicleNo = vehicleNo;
    }

    static ParkingTicket createTicket(int ticketNo, String vehicleNo) {
        return new ParkingTicket(ticketNo, vehicleNo);
    }
}

Object creation:
ParkingTicket t = ParkingTicket.createTicket(101, "TN01AB1111");
Advantages:
•	Provides better control over object creation.
•	Validation can be performed before creating an object.
•	Helps ensure valid object initialization.
Complexity Analysis

For creating n ParkingTicket objects:
1. Overloaded Constructors:
•	Time Complexity: O(n), assuming constant-time initialization per object.
•	Space Complexity: O(n), for storing n objects.
2. Default Constructor with Setters:
•	Time Complexity: O(n), assuming a fixed number of setter calls per object.
•	Space Complexity: O(n).
3. Static Factory Methods:
•	Time Complexity: O(n), assuming constant-time validation and initialization.
•	Space Complexity: O(n).
All three approaches have the same basic time and space complexity. However, they differ in object validity and flexibility.

7) Conclusion
Overloaded constructors and constructor chaining are suitable for the parking management system because they reduce repeated code and initialize objects efficiently. Static factory methods provide additional control over object creation, while setter methods offer flexibility but may allow incomplete objects. Therefore, parameterized constructors with validation are a suitable choice for creating valid Vehicle and ParkingTicket objects.







