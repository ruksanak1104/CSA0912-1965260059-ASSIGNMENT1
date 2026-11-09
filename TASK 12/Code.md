import java.time.LocalTime;

abstract class Vehicle {
    
    String regNo;

    Vehicle(String regNo) {
        
        this.regNo = regNo;
    }

    abstract double calculateFee(int hours);
}

class Car extends Vehicle {
  
    Car(String regNo) {
       
        super(regNo);
    }

    double calculateFee(int hours) {
        return hours * 30;
    }
}

class Bike extends Vehicle {
   
    Bike(String regNo) {
        
        super(regNo);
    }

    double calculateFee(int hours) {
        return hours * 10;
    }
}

class ElectricBike extends Vehicle {
   
    ElectricBike(String regNo) {
      
        super(regNo);
    }

    double calculateFee(int hours) {
       
        return 25; // Flat parking fee
    }
}

class DeliveryVan extends Vehicle {
    
    DeliveryVan(String regNo) {
    
        super(regNo);
    }

    double calculateFee(int hours) {
        
        return hours * 30;
    }

    double calculateFee(int hours, LocalTime time) {
        
        if (!time.isBefore(LocalTime.of(9, 0)) &&
        
            time.isBefore(LocalTime.of(17, 0))) {
            
            return hours * 60;
        }

        return calculateFee(hours);
    }
}

interface Pass {
   
    double getPassFee();
    
    int getValidityHours();
}

class OneDayPass implements Pass {
    
    public double getPassFee() {
    
        return 100;
    }

    public int getValidityHours() {
        
        return 24;
    }
}

class ParkingFacility {
    
    String[][] slots = new String[5][];

    ParkingFacility() {
       
        slots[0] = new String[5];
        
        slots[1] = new String[8];
        
        slots[2] = new String[6];
        
        slots[3] = new String[10];
        
        slots[4] = new String[7];
    }

    void displaySlots() {
       
        for (int i = 0; i < slots.length; i++) {
        
            int count = 0;

            
            for (int j = 0; j < slots[i].length; j++) {
            
                if (slots[i][j] == null) {
                
                    count++;
                }
            }

            System.out.println("Floor " + (i + 1) +
                " Available Slots: " + count);
        }
    }
}

public class Main {
    
    public static void main(String[] args) {

        Vehicle ebike = new ElectricBike("TN01EB1234");
        
        Vehicle van = new DeliveryVan("TN02DV5678");

        Pass pass = new OneDayPass();

        System.out.println("E-Bike Fee: Rs." +
           
            ebike.calculateFee(3));

        DeliveryVan deliveryVan = new DeliveryVan("TN02DV5678");

        System.out.println("Delivery Van Fee (11 AM): Rs." +
           
            deliveryVan.calculateFee(2, LocalTime.of(11, 0)));

        System.out.println("One-Day Pass Fee: Rs." +
           
            pass.getPassFee());

        System.out.println("Pass Validity: " +
          
            pass.getValidityHours() + " hours");

        ParkingFacility parking = new ParkingFacility();
       
        parking.displaySlots();
    }
}

