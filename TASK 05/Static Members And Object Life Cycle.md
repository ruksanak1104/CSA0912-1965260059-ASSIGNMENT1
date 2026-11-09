1) Use of Static Variables

Static variables belong to the class rather than individual objects. They are shared by all objects of that class.
In the parking management system, static variables are useful for maintaining common information.

A. Ticket Counter
A static variable is used to generate unique ticket numbers.

class ParkingTicket {
    
    static int ticketCounter = 1000;
    int ticketNo;

    ParkingTicket() {
        ticketNo = ++ticketCounter;
    }
}
Here, ticketCounter is shared by all ParkingTicket objects. Every new ticket receives a different number.
An instance variable would be unsuitable because each ticket object would maintain a separate counter, which could result in duplicate ticket numbers.

B. Total Occupancy
A static variable can also maintain the total number of occupied slots in a single shared parking facility.
static int totalOccupancy = 0;
It is increased when a vehicle enters and decreased when a vehicle exits.
However, if different facilities need separate occupancy counts, an instance variable should be used instead.

2) Static Methods and Static Blocks

A. Static Methods
Static methods can be called without creating an object.
Example:
class ParkingTicket {
    static int ticketCounter = 1000;

    static int getNextTicketNumber() {
        return ++ticketCounter;
    }
}
It can be called using:
int ticket = ParkingTicket.getNextTicketNumber();
Static methods are suitable for common operations that do not depend on individual object data.

B. Static Block
A static block is executed only once when the class is initialized.
Example:
class ParkingTicket {
    static int ticketCounter;

    static {
        ticketCounter = 1000;
    }
}
It is used to initialize static variables before objects are created.

3) Object Life Cycle and Garbage Collection

When a vehicle enters the parking facility, a ParkingTicket object is created using the new keyword.
When the vehicle leaves:
1.	The parking slot is released.
2.	The ticket's exit time and other required details are updated.
3.	The ticket object may be stored in a history or record collection.
4.	If no reference points to the ticket object, it becomes eligible for garbage collection.
Garbage Collection: Java automatically removes objects from heap memory when they are no longer reachable through references. The exact time of garbage collection is decided by the JVM.

4) Passing and Returning Objects from Methods

Objects can be passed as arguments to methods and returned from methods.
Passing an Object:

void displayVehicle(Vehicle v) {
   
    System.out.println(v.vehicleNo);
}

Here, a Vehicle object is passed as an argument to the method.

Returning an Object:

ParkingTicket createTicket(Vehicle v) {
   
    return new ParkingTicket(v);
}

Here, a new ParkingTicket object is created and returned to the calling method.
Java passes object references by value, meaning the method receives a copy of the reference to the same object.

5) Alternative Concept and Complexity Analysis
The ticket counter is declared as a static variable in the ParkingTicket class. If it were an instance variable of ParkingFacility, each facility would maintain a separate counter.
Consider two parking facilities:
•	North Gate
•	South Gate

Case 1: Instance Variable
Each ParkingFacility object maintains its own ticket counter.
For example:
•	North Gate generates ticket number 1001.
•	South Gate also generates ticket number 1001.
This can cause duplicate ticket numbers across both facilities.

Case 2: Static Variable
A shared static counter can be used by all facilities.
For example:
•	North Gate generates ticket number 1001.
•	South Gate generates ticket number 1002.
This ensures unique ticket numbers across both facilities, provided they use the same shared counter.

Complexity and Space Analysis:
1.	Instance Variable: For k facility objects, each facility stores its own counter. Space required is O(k).
2.	Static Variable: Only one shared counter is maintained for all k facility objects. Space required is O(1).
3.	Ticket Objects: For n tickets, storing the ticket objects requires O(n) space in both approaches.
A static counter is suitable when ticket numbers must be unique across all facilities. If each facility needs independent ticket numbering, an instance counter is more appropriate.

6) Conclusion

Static variables and methods help manage common data and operations in the parking management system. Garbage collection automatically manages unused objects and prevents unnecessary memory usage. A static ticket counter is preferred when multiple parking facilities share one ticket numbering system because it avoids duplicate ticket numbers and saves memory.














