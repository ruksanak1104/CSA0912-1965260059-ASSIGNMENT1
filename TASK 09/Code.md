interface Chargeable {

    double chargingFee(int kWh);

    default void chargingStatus() {
        System.out.println("Charging in progress");
    }

    static void chargingInfo() {
        System.out.println("Rate: Rs.12 per kWh");
    }
}

abstract class Vehicle {

    String regNo;

    Vehicle(String regNo) {
        this.regNo = regNo;
    }

    abstract double calculateFee(double hours);

    void displayDetails() {
        System.out.println("Vehicle No: " + regNo);
    }
}

class Car extends Vehicle {

    Car(String regNo) {
        super(regNo);
    }

    @Override
   
    double calculateFee(double hours) {
        return hours * 30;
    }
}

class ElectricCar extends Car implements Chargeable {

    ElectricCar(String regNo) {
        super(regNo);
    }

    @Override
   
    public double chargingFee(int kWh) {
        return kWh * 12;
    }
}

public class Main {

    public static void main(String[] args) {

        ElectricCar e = new ElectricCar("TN01AB1111");

        e.displayDetails();

        System.out.println("Parking Fee: Rs." +
                e.calculateFee(2));

        System.out.println("Charging Fee: Rs." +
                e.chargingFee(10));

        e.chargingStatus();

        Chargeable.chargingInfo();
    }
}

