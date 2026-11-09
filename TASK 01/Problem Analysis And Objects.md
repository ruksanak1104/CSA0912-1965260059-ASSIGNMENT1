1) Problem Analysis

The parking management system is designed to manage vehicles entering and leaving a parking facility. It keeps track of vehicle details, available parking slots and parking tickets. The system must prevent duplicate slot allocation and ensure that every vehicle has a unique ticket number.

A. Inputs and Outputs

Inputs received by the system:
1. Vehicle registration number.
2. Vehicle type (Car, Bike, etc.).
3. Vehicle entry time.
4. Available parking slot.
5. Vehicle exit time.

Outputs produced by the system:
1. Parking ticket with a unique ticket number.
2. Allocated parking slot number.
3. Updated available slot count.
4. Parking duration and parking fee (if applicable).
5. Confirmation message when a vehicle exits.

2) Candidate Classes and Their Responsibilities

The nouns in the problem are identified as candidate classes, while verbs represent methods or operations.
1. Vehicle Class: Stores vehicle details such as registration number, vehicle type and entry time. Each vehicle is represented as a separate object.
2. Parking Slot Class: Stores the slot number and availability status. It ensures that only one vehicle occupies a slot at a time.
3. Parking Ticket Class: Generates and stores a unique ticket number, vehicle details, entry time and exit time.
4. Parking Lot Class: Manages all parking slots and parked vehicles. It handles vehicle entry, exit and slot allocation.
Each class has a separate responsibility, making the program modular, reusable and easier to maintain.

3) Business Rules

The following rules must be satisfied during every valid operation:
1. A parking slot cannot hold more than one vehicle at a time.
2. Every vehicle must have a unique registration number.
3. Every parking ticket must have a unique ticket number.
4. A ticket number must never be reused.
5. A vehicle can enter only when a suitable parking slot is available.
6. A vehicle can exit only if it is currently parked.
7. Once a vehicle exits, its parking slot must become available.
8. Vehicle details and ticket information must be maintained correctly.

4) Assumptions

1. The parking facility has a fixed number of parking slots.
2. Each slot can accommodate only one vehicle.
3. Vehicles are identified using their registration numbers.
4. The system supports different vehicle types such as cars and bikes.
5. Each vehicle receives a separate parking ticket during entry.
6. The system operates within a single parking facility.

5) Alternative Concept and Complexity Analysis

Instead of creating a separate Vehicle object, vehicle information can be stored using parallel arrays.

Example:
String regNo[] = new String[100];

String type[] = new String[100];

String entryTime[] = new String[100];


Here, the details of the same vehicle are stored at the same array index.
Comparison Between Object-Oriented Design and Parallel Arrays

1. Data Storage
- Vehicle Objects: Each vehicle is stored as an object.
- Parallel Arrays: Details are stored in separate arrays.
2. Finding a Vehicle
- Vehicle Objects: Search using the object's registration number.
- Parallel Arrays: Search through the regNo[] array.
3. Search Time
- Vehicle Objects: O(n) using linear search.
- Parallel Arrays: O(n) using linear search.
4. Adding a New Attribute
- Vehicle Objects: Add a new field to the Vehicle class.
- Parallel Arrays: Create another array and maintain matching indexes.
5. Data Management
- Vehicle Objects: Easy to manage and maintain.
- Parallel Arrays: Difficult to manage as attributes increase.
6. Code Reusability
- Vehicle Objects: Supports object-oriented programming.
- Parallel Arrays: Less flexible and harder to maintain.

Time Complexity
Searching for a vehicle:
- In both designs, linear search takes O(n) time in the worst case, where n is the number of vehicles.
- Both designs require checking registration numbers until a match is found.

Space Complexity
- Vehicle Objects: Each vehicle requires space for one object containing all its attributes.
- Parallel Arrays: Each vehicle requires one entry in every separate array. For three attributes, three array entries are required per vehicle.
Both approaches use O(n) total space for n vehicles and a fixed number of attributes. However, parallel arrays become harder to manage when new attributes are added.

6) Conclusion

The object-oriented approach is more suitable for developing a parking management system because it groups related data and operations into separate classes. It improves code organization, reusability, flexibility and maintainability compared to parallel arrays.
