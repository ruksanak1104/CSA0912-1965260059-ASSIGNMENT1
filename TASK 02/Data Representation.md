1) Selection of Java Data Types

The parking management system uses suitable Java data types to store vehicle and parking information accurately.
1.	Slot Number: int is used because slot numbers are whole numbers.
2.	Vehicle Number: String is used because registration numbers contain both letters and numbers.
3.	Entry Time: LocalDateTime is used to store the exact date and time when a vehicle enters.
4.	Duration: long or int is used to store the parking duration in minutes.
5.	Parking Fee: double is used to store the parking charges because fees may contain decimal values.

2) Representation of Floors and Slots

A jagged array is used to represent the parking floors and slots.

Example:
String[][] parking = new String[3][];
parking[0] = new String[5];
parking[1] = new String[4];
parking[2] = new String[6];

Here:
•	The parking facility has 3 floors.
•	The first floor has 5 slots.
•	The second floor has 4 slots.
•	The third floor has 6 slots.
A jagged array is suitable because different floors may have different numbers of parking slots. It also avoids allocating unnecessary spaces.

3) Type Conversion and Casting

Type conversion is required when calculating parking fees based on parking duration.
For example, if the parking duration is stored in minutes, it must be converted into hours for billing.
Incorrect calculation:
int minutes = 90;
int hours = minutes / 60;
The result is 1 instead of 1.5 because integer division removes the decimal part.
Correct calculation:
int minutes = 90;
double hours = minutes / 60.0;
double fee = hours * 20;
Output:
Hours = 1.5
Fee = 30.0
Using 60.0 ensures floating-point division and avoids precision loss caused by integer division.

4) Reading Input
The Scanner class is used to read user input from the keyboard.
Example:

import java.util.Scanner;

Scanner sc = new Scanner(System.in);

System.out.print("Enter vehicle number: ");
String vehicleNo = sc.nextLine();

System.out.print("Enter slot number: ");
int slotNo = sc.nextInt();
Scanner is suitable because the parking system requires interactive input from users.

5) Alternative Concept and Complexity Analysis

Instead of using a jagged array, parking slots can be represented using a one-dimensional array or an ArrayList<String[]>.
A. One-Dimensional Array

A single array can store all parking slots using the formula:
index = floor * slotsPerFloor + slot;
This representation works well when all floors have the same number of slots. However, when floors have different numbers of slots, the formula must be modified using the total number of slots in previous floors.

B. ArrayList
An ArrayList<String[]> can store a separate array for each floor.
Example:

ArrayList<String[]> parking = new ArrayList<>();
parking.add(new String[5]);
parking.add(new String[4]);
parking.add(new String[6]);
This representation supports different numbers of slots on different floors and allows floors to be added dynamically.


Complexity Analysis:

1.	Jagged Array: Accessing a particular floor and slot takes O(1) time. Space required is O(S), where S is the total number of slots.
2.	One-Dimensional Array: Accessing a slot takes O(1) time when the correct index is calculated. It is less convenient when floors have different numbers of slots.
3.	ArrayList: Accessing a floor and slot using indexes takes O(1) time. It requires O(S) space for all slots, along with small additional storage for the list.

6) Conclusion

A jagged array is the most suitable representation for the parking management system because different floors can have different numbers of slots. Appropriate data types, Scanner input and floating-point calculations help maintain accurate vehicle records and parking fees.








