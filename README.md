# Parking_Fee_Calculator
Parking Fee Calculator for Dmart with discount based on shopping amount
/*A program for a D-Mart that calculates the parking charges based on the
duration of parking and the type of vehicle and give discount on Parking charges depending on amount spent for
shopping.*/
import java.time.Duration;
import java.time.LocalTime;
import java.util.Scanner;

public class DMartParkingCalculator{
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter vehicle type (Car/Bike/Truck): ");
        String vehicle = sc.nextLine().toLowerCase();

        System.out.print("Enter entry time in hh:mm: ");
        String entryTime = sc.next();
        LocalTime entry = LocalTime.parse(entryTime);

        System.out.print("Enter exit time in hh:mm: ");
        String exitTime = sc.next();
        LocalTime exit = LocalTime.parse(exitTime);

        Duration parkingDuration = Duration.between(entry, exit);
        double minutesParked = parkingDuration.toMinutes();
        double hoursParked = (double) minutesParked/60;

        double parkingFee = calculateParkingFee(vehicle, hoursParked);

        System.out.print("Enter your shopping amount in INR: ");
        double shoppingAmount = sc.nextDouble();
        double finalFee = Discount(parkingFee, shoppingAmount);

        System.out.printf("Your final payable amount for parking is: Rs.%.2f\n", finalFee);

    }

    public static double calculateParkingFee(String vehicle, double hoursParked) {
        double cost = 0;
        if (vehicle.equals("bike")) {
            cost = hoursParked*5; 
        }else if(vehicle.equals("car")) {
            cost = hoursParked*10; 
        }else if (vehicle.equals("truck")) {
            cost = hoursParked*15; 
        }else {
            System.out.println("Invalid vehicle type.");
        }
        return cost;
    }

    public static double Discount(double parkingFee, double shoppingAmount) {
        double discount = 0;
        if (shoppingAmount > 5000 && shoppingAmount <= 10000) {
            discount = parkingFee * 0.10;
        } else if (shoppingAmount > 10000) {
            discount = parkingFee * 0.30; 
        }
        return parkingFee - discount;
    }
}
