A. Impact Analysis 

The new requirements introduce two additional vehicle categories, a one-day pass system and an expansion from 3 to 5 floors.
Changes from the original problem:

1.	New vehicle categories: E-bikes must pay a flat parking fee, while delivery vans must pay double the car rate between 9 AM and 5 PM.

2.	One-day pass: Visitors can purchase a pass that allows parking for one day.

3.	Parking expansion: The facility now has 5 floors, and each floor has a different number of parking slots.

Affected classes, methods and data structures:

•	Vehicle: Must support the new vehicle categories through inheritance.

•	ParkingFacility: Must support 5 floors and different slot counts.

•	ParkingTicket: Must store pass details and parking information.

•	calculateFee(): Must support flat fees and time-based special rates.

•	ParkingSlot: Its allocation and release logic can remain mostly unchanged.

Why is the array design affected?

A normal two-dimensional array assumes the same number of columns for every row. Since each floor has a different number of slots, a jagged array is more suitable.

String[][] slots = new String[5][];

slots[0] = new String[5];

slots[1] = new String[8];

slots[2] = new String[6];

slots[3] = new String[10];

slots[4] = new String[7];

Each row represents a floor, and each row can have a different number of slots.
Therefore, the original design requires modifications to the vehicle hierarchy, pricing logic, ticket system and parking array.

B. Evaluation of the Original Design 

The original object-oriented design is suitable for the basic parking system, but it needs some modifications to satisfy the new requirements.

1.	Adding new vehicle types: New subclasses can be created, but adding special pricing rules to every subclass may increase code duplication. A common pricing abstraction is more flexible.

2.	Pricing rules: If pricing is implemented separately inside every vehicle class, maintaining different rates becomes difficult. Keeping pricing rules in separate classes makes the system easier to maintain.

3.	Existing tested classes: Classes such as Car, Bike and Vehicle should remain unchanged wherever possible. New functionality should be added through new subclasses and interfaces.

4.	Data structure: The original parking array must be modified into a jagged array to support different slot counts on each floor.

Evaluation: The original design is partially appropriate. It follows inheritance, encapsulation and polymorphism, but the changed requirements make a small redesign necessary.

C. Adaptation or Redesign 

Decision: Modify the original design.

The revised design uses inheritance, interfaces, method overriding and a jagged array.

Revised class structure:

•	Vehicle: Abstract parent class containing registration number and common vehicle information.

•	Car: Existing car category.

•	Bike: Existing bike category.

•	ElectricBike: New category with a flat parking fee.

•	DeliveryVan: New category with double the car rate during 9 AM to 5 PM.

•	Pass: Interface representing the one-day parking pass.

•	OneDayPass: Implements the Pass interface.

•	ParkingFacility: Manages the five floors using a jagged array.

•	ParkingTicket: Stores vehicle and ticket details.

Explanation:

•	E-bike pays a flat fee of ₹25, regardless of parking hours.

•	Delivery van pays ₹60 per hour during 9 AM to 5 PM, which is double the car rate of ₹30.

•	One-day pass costs ₹100 and remains valid for 24 hours.

•	The jagged array supports different parking capacities on all five floors.

Note: This is a focused implementation of the changed requirements. The one-day pass fee is treated as a flat fee, and the van's special rate is selected using its entry time.

D. Evidence-Based Defence 
The modified design is more suitable than completely retaining the original design.

1. Existing classes modified:

•	Vehicle is retained as the common abstract class.

•	Car and Bike remain unchanged.

•	ParkingFacility is modified to support five floors using a jagged array.

•	ParkingTicket can be extended to record pass information.

•	New classes ElectricBike, DeliveryVan and OneDayPass are added.

2. Future vehicle categories:

New vehicle types can be added by extending Vehicle and implementing their own pricing behaviour. This reduces changes to existing classes.

3. Test results:

•	E-bike for 3 hours: ₹25.

•	Delivery van for 2 hours at 11 AM: ₹120.

•	One-day pass: ₹100 for 24 hours.

•	Five floors successfully support different slot capacities.

These results confirm the new pricing calculations and floor configuration. Further integration tests are required to verify actual vehicle allocation, pass expiry and exit processing.

4. Trade-offs:

•	A jagged array supports unequal floor capacities but requires nested loops to search all slots.

•	Separate pricing methods make the system flexible but add a few classes.

•	A one-day pass simplifies visitor payments, but the system must check its expiry time.

•	Adding subclasses is easy, but too many special pricing conditions may eventually require a separate pricing-rule strategy.

Final Conclusion:

The original design is modified rather than completely redesigned. The revised system uses inheritance, abstraction, polymorphism, interfaces and jagged arrays to support the new requirements. It maintains most of the existing tested classes while allowing future vehicle categories and pricing rules to be added with fewer changes. Therefore, the modified design is more flexible, maintainable and scalable for the expanded university parking facility.



