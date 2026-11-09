import java.util.*;

interface Chargeable {
    
    double chargingFee(int units);
}

abstract class Vehicle {

    private final String regNo;

    Vehicle(String regNo) {
        this.regNo = regNo;
    }

    public String getRegNo() {
        return regNo;
    }

    abstract double ratePerHour();

    public double calculateFee(int minutes) {
        int hours = (minutes + 59) / 60;
        return hours * ratePerHour();
    }
}

class Car extends Vehicle {

    Car(String regNo) {
        super(regNo);
    }

    double ratePerHour() {
        return 30;
    }
}

class Bike extends Vehicle {

    Bike(String regNo) {
        super(regNo);
    }

    double ratePerHour() {
        return 10;
    }
}

class ElectricCar extends Car implements Chargeable {

    ElectricCar(String regNo) {
        super(regNo);
    }

    public double chargingFee(int units) {
        return units * 12;
    }
}

class ParkingTicket {

    private static int counter = 1000;

    private int ticketNo;
    private Vehicle vehicle;
    private int floor;
    private int slot;

    ParkingTicket(Vehicle vehicle, int floor, int slot) {
        this.ticketNo = ++counter;
        this.vehicle = vehicle;
        this.floor = floor;
        this.slot = slot;
    }

    public Vehicle getVehicle() {
        return vehicle;
    }

    public int getFloor() {
        return floor;
    }

    public int getSlot() {
        return slot;
    }

    public int getTicketNo() {
        return ticketNo;
    }
}

class ParkingFacility {

    private String[][] slots;
    private ArrayList<ParkingTicket> tickets =
            new ArrayList<>();

    private double totalCollection = 0;

    ParkingFacility(int[] slotCounts) {

        slots = new String[slotCounts.length][];

        for (int i = 0; i < slotCounts.length; i++) {
            slots[i] = new String[slotCounts[i]];
        }
    }

    public void enter(Vehicle v) {

        for (ParkingTicket t : tickets) {
            if (t.getVehicle().getRegNo().equals(v.getRegNo())) {
                System.out.println("Duplicate vehicle!");
                return;
            }
        }

        for (int f = 0; f < slots.length; f++) {

            for (int s = 0; s < slots[f].length; s++) {

                if (slots[f][s] == null) {

                    slots[f][s] = v.getRegNo();

                    ParkingTicket t =
                            new ParkingTicket(v, f, s);

                    tickets.add(t);

                    System.out.println("Vehicle entered: "
                            + v.getRegNo()
                            + " Ticket: " + t.getTicketNo()
                            + " Slot: " + f + "," + s);

                    return;
                }
            }
        }

        System.out.println("Parking Full!");
    }

    public void exit(String regNo, int minutes) {

        for (int i = 0; i < tickets.size(); i++) {

            ParkingTicket t = tickets.get(i);

            if (t.getVehicle().getRegNo().equals(regNo)) {

                if (minutes < 0) {
                    System.out.println("Invalid duration!");
                    return;
                }

                Vehicle v = t.getVehicle();

                double fee = v.calculateFee(minutes);

                if (v instanceof Chargeable c) {
                    fee += c.chargingFee(10);
                }

                int f = t.getFloor();
                int s = t.getSlot();

                slots[f][s] = null;

                totalCollection += fee;

                System.out.println("Vehicle exited: " + regNo);
                System.out.println("Parking Fee: Rs." + fee);

                tickets.remove(i);

                return;
            }
        }

        System.out.println("Vehicle not found!");
    }

    public double getTotalCollection() {
        return totalCollection;
    }
}

public class Main {

    public static void main(String[] args) {

        ParkingFacility p =
                new ParkingFacility(new int[]{2, 1});

        p.enter(new Car("TN01AB1111"));
        p.enter(new Bike("TN02CD2222"));
        p.enter(new ElectricCar("TN03EF3333"));

        p.enter(new Car("TN04GH4444"));

        p.exit("TN01AB1111", 120);
        p.exit("TN02CD2222", 60);
        p.exit("TN03EF3333", 120);

        System.out.println("Total Collection: Rs."
                + p.getTotalCollection());
    }
}

