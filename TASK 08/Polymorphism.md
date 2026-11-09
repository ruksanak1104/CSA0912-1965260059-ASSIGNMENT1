1) Polymorphism in Java

Polymorphism means "many forms". It allows the same method name or reference to perform different operations depending on the situation.
Java supports two types of polymorphism:
1.	Compile-time Polymorphism: Achieved through method overloading. The compiler selects the appropriate method based on the arguments.
2.	Runtime Polymorphism: Achieved through method overriding. The JVM selects the appropriate overridden method based on the actual object type at runtime.

2) Compile-Time Polymorphism (Method Overloading)
Method overloading means defining multiple methods with the same name but different parameter lists.
In the parking management system, calculateFee() can be overloaded to accept parking duration in minutes or entry and exit times.
Example:

import java.time.LocalTime;

import java.time.Duration;

class ParkingFee {

    double calculateFee(int minutes) {
        int hours = (minutes + 59) / 60;
        return hours * 30;
    }

    double calculateFee(LocalTime in, LocalTime out) {
        long minutes = Duration.between(in, out).toMinutes();
        return calculateFee((int) minutes);
    }
}

Explanation:
•	calculateFee(int minutes) calculates the fee using parking duration.
•	calculateFee(LocalTime in, LocalTime out) calculates the duration using entry and exit times.
•	The compiler selects the correct method based on the arguments passed.
This is called compile-time polymorphism.

3) Runtime Polymorphism (Method Overriding)

Runtime polymorphism is achieved through inheritance and method overriding.
A single array of Vehicle references can store different types of vehicle objects.
Example:

Vehicle[] parked = {
    
    new TwoWheeler("TN01A1"),
    
    new Car("TN02B2"),
    
    new ElectricCar("TN03C3")
};

Here:
•	Vehicle is the superclass.
•	TwoWheeler, Car and ElectricCar are subclasses.
•	All objects are stored in one Vehicle array.
This is called upcasting, where subclass objects are referred to using a superclass reference.
When calculateFee() is called, Java executes the overridden method based on the actual object type. This is called dynamic method dispatch.

4) Dynamic Method Dispatch Example

Consider the statement:

Vehicle v = new Car("TN02B2");

double fee = v.calculateFee(130);

Execution:
1.	Declared reference type: Vehicle.
2.	Actual object type: Car.
3.	The calculateFee() method is called.
4.	Java executes the Car-specific ratePerHour() method.
5.	Parking duration is 130 minutes, which is charged as 3 started hours.
6.	Fee = 3 × 30 = ₹90.
Therefore, the correct method is selected at runtime without checking the vehicle type manually.

5) Advantages of Polymorphism
1.	Reduces long if-else and switch statements.
2.	Improves code reusability.
3.	Makes the program easier to maintain.
4.	Allows different vehicle types to use the same method name with different implementations.
5.	Makes it easier to add new vehicle types without changing existing code.

6)Explanation of the Program

A. Fee Calculation

The expression:

int hours = (minutes + 59) / 60;

Calculates the number of started hours using integer arithmetic.

For 130 minutes:
•	Billable hours = (130 + 59) / 60

•	Billable hours = 189 / 60

•	Billable hours = 3

B. Parking Fee

•	TwoWheeler: 3 × 10 = ₹30.

•	Car: 3 × 30 = ₹90.

•	ElectricCar: (3 × 30) + (10 × 12) = ₹210.

C. ChargingFee Interface

The Chargeable interface defines the chargingFee() method.
ElectricCar implements this interface and calculates charging charges at ₹12 per kWh.

D. instanceof Operator

if (v instanceof Chargeable c)
    
    fee += c.chargingFee(10);

It checks whether the vehicle supports the Chargeable interface. If true, the charging fee is added.

7) Expected Output

TwoWheeler TN01A1 -> Rs 30.0

Car TN02B2 -> Rs 90.0

ElectricCar TN03C3 -> Rs 210.0

true

8) Why Does the Last Line Print true?

The last statement is:

new Car("TN02B2").equals(
    
    new ElectricCar("TN02B2")
);

It prints true because:
1.	Both objects have the same registration number, TN02B2.
2.	The equals() method compares only the registration numbers.
3.	Therefore, both objects are considered equal.
Is this correct?
Yes, if the registration number is the unique identity of a vehicle across the entire parking system. However, the system must prevent two different vehicles from being registered with the same registration number.

9)Alternative Concept: instanceof Checks Instead of Dynamic Method Dispatch
Instead of overriding methods, the program can use instanceof checks and type casting to identify each vehicle type.

Example:
double fee;

if (v instanceof ElectricCar) {
    f
    ee = 3 * 30 + 10 * 12;
}
else if (v instanceof Car) {
   
    fee = 3 * 30;
}
else if (v instanceof TwoWheeler) {
   
    fee = 3 * 10;
}
else {
    fee = 0;
}
In this approach, the program checks the vehicle type and calculates the corresponding parking fee.


Complexity Analysis

1. Dynamic Method Dispatch:
•	Time complexity: O(1) for selecting the appropriate overridden method.
•	When a new vehicle type is added, a new subclass can be created without modifying the existing fee calculation logic.
•	Code is easier to maintain and extend.

2. instanceof Approach:
•	Time complexity: O(k) in the worst case, where k is the number of vehicle types checked sequentially.
•	When a new vehicle type is added, the conditional statements must be modified.
•	Code size increases as more vehicle types are introduced.

Conclusion

Polymorphism makes the parking management system more flexible and reusable. Method overloading provides compile-time polymorphism, while method overriding provides runtime polymorphism. Dynamic method dispatch is preferred over multiple instanceof checks because it reduces conditional statements and makes adding new vehicle types easier.



