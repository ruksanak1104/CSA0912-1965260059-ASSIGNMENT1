1) Package Structure

Packages are used in Java to organize related classes and avoid naming conflicts.
The parking management system is divided into three packages:
1.	parking.model: Contains Vehicle, Car, Bike, ParkingSlot and ParkingTicket classes. These classes represent the data and objects of the system.
2.	parking.service: Contains ParkingLot and ParkingService classes. These classes handle vehicle allocation, release and parking fee calculations.
3.	parking.app: Contains the Main class. It handles user interaction and executes the parking management system.
This structure improves code organization, reusability and maintainability.

2) Access Modifiers

Access modifiers control the visibility of classes, fields and methods.
The following access modifiers are used:
1.	Private: Used for fields such as vehicle number, parking fee and slot number to prevent direct access from outside the class.
2.	Default: Used for members that need to be accessible only within the same package.
3.	Protected: Used for methods and fields that need to be accessed by subclasses, such as inherited vehicle behaviour.
4.	Public: Used for constructors, getters and service methods that must be accessible from other packages.
Private fields provide better data security and prevent unauthorized modifications.

3) Getters and Setters with Validation

Encapsulation is achieved by declaring fields as private and accessing them through public getter and setter methods.
Example:

class ParkingSlot {

    private int slotNo;
    private boolean occupied;

    public int getSlotNo() {
        return slotNo;
    }

    public void setSlotNo(int slotNo) {

        if (slotNo <= 0) {
            throw new IllegalArgumentException(
                "Invalid slot number"
            );
        }

        this.slotNo = slotNo;
    }

    public boolean isOccupied() {
        return occupied;
    }

    public void setOccupied(boolean occupied) {
        this.occupied = occupied;
    }
}

Explanation:

•	getSlotNo() returns the slot number.

•	setSlotNo() validates the slot number before assigning it.

•	Negative and zero slot numbers are rejected.

•	Private fields prevent direct modification from outside the class.

Similarly, a parking duration setter can reject negative values.

public void setDuration(int duration) {

    if (duration < 0) {
        throw new IllegalArgumentException(
            "Duration cannot be negative"
        );
    }

    this.duration = duration;
}

4) Wrapper Classes and Autoboxing

Wrapper classes convert primitive data types into objects.

Examples:
•	Integer for int.
•	Double for double.
•	Boolean for boolean.

Autoboxing: Automatically converts a primitive value into its corresponding wrapper object.

Example:

Integer slotNo = 10;

Here, the primitive integer value is automatically converted into an Integer object.
Unboxing: Converts a wrapper object into a primitive value.

Example:

Integer a = 20;

int b = a;

Here, the Integer object is automatically converted into an int.

Risk of Using == with Wrapper Classes:

Integer a = 200;

Integer b = 200;

System.out.println(a == b);

The result may be false because == compares object references rather than numerical values.

Correct approach:

System.out.println(a.equals(b));
It compares the actual values and returns true.

5)ternative Concept and Complexity Analysis
Instead of declaring fields as private, suppose all fields are made public and validation is performed by the calling code.

Example:

class ParkingSlot {

    public int slotNo;
    public boolean occupied;
}

Object creation and validation:

ParkingSlot p = new ParkingSlot();

if (10 > 0) {
    p.slotNo = 10;
}

In this approach, the calling code is responsible for checking the values before assigning them.

Problems with Public Fields:
1.	Any class can directly modify the fields.
2.	Invalid values may enter the system.
3.	Validation code must be repeated in different places.
4.	Maintaining and debugging the program becomes difficult.
5.	Data security and consistency are reduced.

Complexity Analysis
1. Private Fields with Validating Setters:

•	Each update requires O(1) time for a simple validation check.

•	Validation is written once inside the setter.

•	All classes reuse the same validation logic.

2. Public Fields with External Validation:

•	Each update also requires O(1) time for a simple validation check.

•	The same validation must be repeated wherever the field is modified.

•	If there are m places where updates occur, validation may need to be written m times.
Both approaches have similar time costs for an individual update, but encapsulation reduces repeated code and maintenance effort.

6) Conclusion
Encapsulation protects the data of the parking management system by using private fields and public getters and setters. Packages organize related classes, while access modifiers control visibility. Validation ensures that invalid data does not enter the system. Therefore, encapsulation improves data security, consistency, reusability and maintainability.

