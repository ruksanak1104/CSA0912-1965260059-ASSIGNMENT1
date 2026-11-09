1) Method Overriding

Method overriding is a Java feature in which a subclass provides its own implementation of a method already defined in its superclass.
In the parking management system, the calculateFee() method is overridden because different vehicle types may have different parking charges.
The following methods are overridden:
1.	Car: Calculates the parking fee based on the car parking rate.
2.	Bike: Calculates the parking fee based on the bike parking rate.
3.	ElectricCar: Calculates the parking fee based on the electric car parking rate.
This allows each vehicle type to have its own fee calculation while using the same method name.

2) Use of @Override Annotation and Rules

The @Override annotation indicates that a subclass method overrides a method from its superclass.

Example:
@Override

public double calculateFee(double hours) {
    return hours * 30;
}

Rules of method overriding:
1.	The method name and parameter list must be the same as the superclass method.
2.	The return type must be the same or a compatible covariant return type.
3.	The access modifier cannot be more restrictive than the parent method.
4.	Private and static methods cannot be overridden in the normal runtime-polymorphism sense.
5.	The @Override annotation helps the compiler detect incorrect overriding.

3) Use of final Keyword

The final keyword is used to restrict modifications in Java.

A. Final Variable

A final variable cannot be reassigned after initialization.
final String vehicleNo = "TN01AB1111";
It is useful for registration numbers because they should not change after vehicle creation.

B. Final Method

A final method cannot be overridden by subclasses.

final void displayRegistration() {
    
    System.out.println(vehicleNo);
}

It is useful when a method's behaviour must remain unchanged in all subclasses.

C. Final Class

A final class cannot be inherited by another class.

final class ParkingRules {
}
It is useful for classes that should not be extended.
The Vehicle class should not be declared final because Car, Bike and ElectricCar need to inherit from it.

4) Overriding Object Class Methods

Java provides methods such as toString(), equals() and hashCode() through the Object class.
These methods can be overridden to manage vehicle objects correctly.

A. toString()
The toString() method returns a readable string representation of an object.
@Override

public String toString() {
  
    return "Vehicle Number: " + vehicleNo;
}

It helps display vehicle information easily.

B. equals()

The equals() method compares two objects.
In the parking system, two Vehicle objects are considered equal if they have the same registration number.
@
Override

public boolean equals(Object obj) {

    if (this == obj)
        return true;

    if (!(obj instanceof Vehicle))
        return false;

    Vehicle v = (Vehicle) obj;

    return vehicleNo.equals(v.vehicleNo);
}

C. hashCode()

The hashCode() method generates a hash value for an object.
@Override

public int hashCode() {
  
    return vehicleNo.hashCode();
}
If two vehicles have the same registration number, their hash codes will also be equal.
Both equals() and hashCode() must be overridden together to maintain consistency when using collections such as HashSet and HashMap.

5) Complete Java Program Demonstrating Method Overriding

import java.util.Objects;

class Vehicle {

    final String vehicleNo;

    Vehicle(String vehicleNo) {
        this.vehicleNo = vehicleNo;
    }

    public double calculateFee(double hours) {
        return 0;
    }

    @Override
    
    public String toString() {
        return "Vehicle Number: " + vehicleNo;
    }

    @Override
   
    public boolean equals(Object obj) {

        if (this == obj)
            return true;

        if (!(obj instanceof Vehicle))
            return false;

        Vehicle v = (Vehicle) obj;

        return vehicleNo.equals(v.vehicleNo);
    }

    @Override
   
    public int hashCode() {
       
        return Objects.hash(vehicleNo);
    }
}

class Car extends Vehicle {

    Car(String vehicleNo) {
        
        super(vehicleNo);
    }

    @Override
   
    public double calculateFee(double hours) {
        
        return hours * 30;
    }
}

class Bike extends Vehicle {

    Bike(String vehicleNo) {
       
        super(vehicleNo);
    }

    @Override
   
    public double calculateFee(double hours) {
       
        return hours * 10;
    }
}

class ElectricCar extends Car {

    ElectricCar(String vehicleNo) {
        s
        uper(vehicleNo);
    }

    @Override
   
    public double calculateFee(double hours) {
      
        return hours * 20;
    }
}

public class Main {

    public static void main(String[] args) {

        Vehicle v1 = new Car("TN01AB1111");
       
        Vehicle v2 = new Bike("TN02CD2222");
        
        Vehicle v3 = new ElectricCar("TN03EF3333");

        System.out.println(v1.calculateFee(2));
        
        System.out.println(v2.calculateFee(2));
        
        System.out.println(v3.calculateFee(2));

        System.out.println(v1);

        Vehicle v4 = new Car("TN01AB1111");

        System.out.println(v1.equals(v4));
        
        System.out.println(v1.hashCode() == v4.hashCode());
    }
}

6) Expected Output

60.0

20.0

40.0

Vehicle Number: TN01AB1111

true

true

7) Alternative Concept: Switch Statement Instead of Overriding

Instead of overriding calculateFee() in each subclass, a single method with a switch statement can be used based on the vehicle type.
Example:

class Vehicle {

    String vehicleType;

    Vehicle(String vehicleType) {
       
        this.vehicleType = vehicleType;
    }

    double calculateFee(double hours) {

        switch (vehicleType) {

            case "Car":
                return hours * 30;

            case "Bike":
                return hours * 10;

            case "ElectricCar":
                return hours * 20;

            default:
                return 0;
        }
    }
}

In this approach, the fee is calculated according to the vehicle type stored in the object.

Complexity Analysis

1. Method Overriding:
•	Fee calculation takes O(1) time because the calculation involves a fixed number of arithmetic operations.
•	When a new vehicle type is added, a new subclass must be created with its own overridden method.
•	Usually, only one new subclass is required without modifying the existing classes.

2. Switch Statement:
•	Fee calculation takes O(k) time in the worst case when k vehicle types are checked sequentially.
•	When a new vehicle type is added, the switch statement must be modified.
•	The Vehicle class needs to be updated whenever a new vehicle type is introduced.

Comparison:
•	Method overriding provides better flexibility and code reusability.
•	Switch statements are simpler for a small number of vehicle types.
•	Inheritance supports runtime polymorphism, whereas the switch approach uses conditional selection.

8) Conclusion

Method overriding allows Car, Bike and ElectricCar to calculate parking fees differently using the same calculateFee() method. The @Override annotation ensures correct overriding, while the final keyword protects important data and methods. Overriding toString(), equals() and hashCode() improves object representation and comparison. Therefore, method overriding is more suitable than switch statements for an extensible parking management system.

