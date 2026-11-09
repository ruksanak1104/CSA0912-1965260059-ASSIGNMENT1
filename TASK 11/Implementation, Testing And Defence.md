1) Implementation of the Parking Management System

The parking management system is implemented using Java and object-oriented programming concepts. It manages vehicle entry, slot allocation, parking fee calculation, ticket generation and vehicle exit.

The system uses:

•	Encapsulation: Private fields and public getter methods protect vehicle and ticket data.

•	Inheritance: Car, Bike and ElectricCar inherit common properties from Vehicle.

•	Polymorphism: Different vehicle types calculate parking fees using overridden methods.

•	Abstraction: An abstract Vehicle class and Chargeable interface define common behaviour and additional capabilities.

•	Arrays: A two-dimensional array stores parking slots.

•	ArrayList: Stores active parking tickets.

2) Testing and Expected Results

The system is tested using normal operations, boundary conditions and invalid inputs.

A. Normal Operations
1.	A car enters the parking facility and receives a ticket.
2.	A bike enters and receives another ticket.
3.	An electric car enters and receives another ticket.
4.	Each vehicle is allocated a separate parking slot.
5.	Vehicles exit and their parking fees are calculated.

B. Boundary Cases
1.	Last Free Slot: The vehicle is allocated to the final available slot. Any further vehicle is rejected with a Parking Full message.
2.	Zero-Minute Parking: The billable duration is zero hours, so the parking fee is ₹0.
3.	Exact Fee Boundary: A vehicle parked for exactly 60 minutes is charged for one hour.
4.	Negative Duration: The system rejects negative parking durations.

C. Invalid Cases
1.	Unknown Vehicle Type: The system should reject a vehicle type that is not supported, such as a bus, unless a Bus class is added.
2.	Duplicate Registration Number: The system checks active tickets and rejects a vehicle that is already parked.
3.	Invalid Slot Number: A slot outside the valid floor or slot range must be rejected.
4.	Vehicle Not Found: If an unregistered vehicle attempts to exit, the system displays a Vehicle Not Found message.

3) Test Results

The following results are obtained from the given Java implementation and its expected test scenarios.

Test 1: Normal Vehicle Entry and Exit

•	Input: Car, Bike and ElectricCar.

•	Expected Result: All three vehicles receive separate parking slots and tickets.

•	Actual Result: All three vehicles are successfully allocated.

Test 2: Parking Facility Full

•	Input: Four vehicles in a facility with three slots.

•	Expected Result: The fourth vehicle is rejected.

•	Actual Result: Parking Full!

Test 3: Duplicate Registration

•	Input: Enter the same registration number twice while the first ticket is active.

•	Expected Result: Duplicate registration is rejected.

•	Actual Result: Duplicate vehicle!

Test 4: Zero-Minute Parking

•	Input: Parking duration = 0 minutes.

•	Expected Result: Parking fee = ₹0.

•	Actual Result: ₹0.

Test 5: Exact One-Hour Boundary

•	Input: Parking duration = 60 minutes.

•	Expected Result: One hour is charged.

•	Actual Result: Car = ₹30, Bike = ₹10.

Test 6: Invalid Duration

•	Input: Parking duration = -10 minutes.

•	Expected Result: Invalid duration message.

•	Actual Result: Invalid duration!

Test 7: Invalid Slot Number

•	Input: Floor number = 5, slot number = 0 for a facility with only two floors.

•	Expected Result: The operation is rejected.

•	Actual Result: The slot must remain unchanged. A separate bounds-checked release method is required for this test.

Test 8: Unknown Vehicle Type

•	Input: Unsupported vehicle type.

•	Expected Result: The system rejects the vehicle type.

•	Actual Result: The supplied implementation accepts only predefined Vehicle subclasses. A user-input factory or validation method is required to display an explicit rejection message.

4) Calculation of Total Daily Collection

Consider the following scenario:

•	One Car parked for 120 minutes.

•	One Bike parked for 60 minutes.

•	One ElectricCar parked for 120 minutes with 10 kWh charging.

Manual Calculation:
1.	Car:

o	2 hours × ₹30 = ₹60.

2.	Bike:

o	1 hour × ₹10 = ₹10.

3.	ElectricCar:

o	Parking fee = 2 × ₹30 = ₹60.

o	Charging fee = 10 × ₹12 = ₹120.

o	Total = ₹180.

Total daily collection:

\[ 60+10+180=\boxed{₹250} \]

Expected program collection

₹250.00

Matches the manual calculation.

5) Evaluation of Object-Oriented Concepts

The parking management system follows the major object-oriented programming principles.

1. Encapsulation:
Private fields are used to protect vehicle and ticket information. Getter methods provide controlled access to data.

2. Inheritance:
Car, Bike and ElectricCar inherit common properties from the Vehicle class. This reduces code duplication.

3. Polymorphism:
The calculateFee() method behaves differently for different vehicle types through method overriding.

4. Abstraction:
The abstract Vehicle class defines common vehicle behaviour, while the Chargeable interface provides additional charging functionality.

Limitation:
The current implementation stores active tickets in an ArrayList and searches sequentially. This can become slower when the number of parked vehicles increases. A HashMap would provide faster ticket lookup.

6) Alternative Concept: 

ArrayList vs HashMap

Currently, active parking tickets are stored using:

ArrayList<ParkingTicket> tickets;

Another approach is to use:

HashMap<String, ParkingTicket> tickets;

Here, the vehicle registration number is used as the key, and the corresponding parking ticket is stored as the value.

A. ArrayList Approach

•	All active tickets are stored in a list.

•	During vehicle exit, the system searches each ticket using its registration number.

•	The matching ticket is removed after processing the exit.

B. HashMap Approach

•	Each ticket is stored using the vehicle registration number as its key.

•	During vehicle exit, the ticket is directly retrieved using get(regNo).

•	The ticket is removed using remove(regNo).

Example:

HashMap<String, ParkingTicket> tickets =
        
        new HashMap<>();

ParkingTicket t = tickets.get("TN01AB1111");

if (t != null) {
    tickets.remove("TN01AB1111");
}

Complexity Analysis

ArrayList:

•	Searching for a ticket takes O(n) time in the worst case.

•	Removing a ticket also takes O(n) time because remaining elements may need to be shifted.

•	Space required is O(n) for n active tickets.

HashMap:

•	Searching for a ticket takes O(1) average time.

•	Removing a ticket takes O(1) average time.

•	Space required is O(n) for n active tickets.

Therefore, HashMap is more efficient for searching and processing vehicle exits when the parking facility has many vehicles.

7) Final Recommendation

Based on the implementation and testing, the object-oriented approach is suitable for developing the parking management system.
The system successfully demonstrates vehicle entry, slot allocation, ticket generation, fee calculation and vehicle exit. The manual fee calculation of ₹250 matches the expected program collection.

The use of inheritance, encapsulation, polymorphism and abstraction improves code organization and maintainability. However, replacing ArrayList with HashMap would improve ticket-search performance for larger parking facilities.

Conclusion: The proposed parking management system provides a modular and reusable design. It can be further improved by adding database connectivity, online payment facilities and real-time parking availability.


