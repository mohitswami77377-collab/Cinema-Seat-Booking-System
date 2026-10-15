
import java.util.Scanner;

public class CinemaSeatBookingSystem {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        String[] movies = {
            "Devara",
            "The Paradise",
            "Salaar",
            "Guntur Kaaram",
            "Daaku Maharaj"
        };

        String[] genres = {
            "Action Drama",
            "Action Thriller",
            "Action Thriller",
            "Action Comedy",
            "Action Drama"
        };

        double[] prices = {200, 180, 220, 200, 250};

        boolean[][] seats = new boolean[5][70];
        String[][] bookingIds = new String[5][70];

        int nextBookingId = 1001;
        int choice;

        do {
            System.out.println("\n===== CINEMA TICKET BOOKING =====");
            System.out.println("1. Show Movies");
            System.out.println("2. Book Ticket");
            System.out.println("3. View Seat Availability");
            System.out.println("4. View All Booked Tickets");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");

            choice = sc.nextInt();

            switch (choice) {

                case 1:
                    System.out.println("\n===== NOW SHOWING =====");

                    for (int i = 0; i < movies.length; i++) {
                        System.out.println("\nMovie: " + movies[i]);
                        System.out.println("Genre: " + genres[i]);
                        System.out.println("Ticket Price: Rs." + prices[i]);
                        System.out.println("Total Seats: 70");
                    }
                    break;

                case 2:
                    System.out.println("\n===== SELECT MOVIE =====");

                    for (int i = 0; i < movies.length; i++) {
                        System.out.println((i + 1) + ". "
                                + movies[i] + " | "
                                + genres[i] + " | Rs." + prices[i]);
                    }

                    System.out.print("Enter movie number: ");
                    int movie = sc.nextInt();

                    if (movie < 1 || movie > movies.length) {
                        System.out.println("Invalid movie number!");
                        break;
                    }

                    int m = movie - 1;

                    System.out.println("\nMovie: " + movies[m]);
                    System.out.println("Genre: " + genres[m]);
                    System.out.println("Ticket Price: Rs." + prices[m]);

                    System.out.println("\n===== SEAT STATUS =====");
                    System.out.println("A = Available, B = Booked");

                    for (int i = 0; i < 70; i++) {
                        System.out.print("Seat " + (i + 1) + ": ");

                        if (seats[m][i]) {
                            System.out.println("BOOKED | ID: "
                                    + bookingIds[m][i]);
                        } else {
                            System.out.println("AVAILABLE");
                        }
                    }

                    System.out.print("\nEnter seat number (1-70): ");
                    int seat = sc.nextInt();

                    if (seat < 1 || seat > 70) {
                        System.out.println("Invalid seat number!");
                    } else if (seats[m][seat - 1]) {
                        System.out.println("TICKET ALREADY BOOKED!");
                        System.out.println("This seat is BLOCKED.");
                        System.out.println("Booking ID: "
                                + bookingIds[m][seat - 1]);
                        System.out.println("Please select another seat.");
                    } else {
                        seats[m][seat - 1] = true;

                        String id = "TKT" + nextBookingId++;
                        bookingIds[m][seat - 1] = id;

                        System.out.println("\n===== BOOKING SUCCESSFUL =====");
                        System.out.println("Booking ID: " + id);
                        System.out.println("Movie: " + movies[m]);
                        System.out.println("Genre: " + genres[m]);
                        System.out.println("Seat Number: " + seat);
                        System.out.println("Ticket Price: Rs." + prices[m]);
                        System.out.println("Ticket Status: BOOKED");
                        System.out.println("Seat Status: BLOCKED");
                    }
                    break;

                case 3:
                    System.out.println("\n===== ALL MOVIE SEAT STATUS =====");

                    for (int i = 0; i < movies.length; i++) {
                        System.out.println("\nMovie: " + movies[i]);
                        System.out.println("Genre: " + genres[i]);

                        int available = 0;
                        int booked = 0;

                        for (int j = 0; j < 70; j++) {
                            if (seats[i][j]) {
                                booked++;
                            } else {
                                available++;
                            }
                        }

                        System.out.println("Available Seats: " + available);
                        System.out.println("Booked Seats: " + booked);

                        for (int j = 0; j < 70; j++) {
                            if (seats[i][j]) {
                                System.out.println("Seat " + (j + 1)
                                        + " - BOOKED | ID: "
                                        + bookingIds[i][j]);
                            } else {
                                System.out.println("Seat " + (j + 1)
                                        + " - AVAILABLE");
                            }
                        }
                    }
                    break;

                case 4:
                    System.out.println("\n===== ALL BOOKED TICKETS =====");

                    boolean found = false;

                    for (int i = 0; i < movies.length; i++) {
                        for (int j = 0; j < 70; j++) {
                            if (seats[i][j]) {
                                found = true;

                                System.out.println("\nBooking ID: "
                                        + bookingIds[i][j]);
                                System.out.println("Movie: " + movies[i]);
                                System.out.println("Genre: " + genres[i]);
                                System.out.println("Seat Number: " + (j + 1));
                                System.out.println("Price: Rs." + prices[i]);
                                System.out.println("Status: BOOKED");
                            }
                        }
                    }

                    if (!found) {
                        System.out.println("No tickets booked yet.");
                    }
                    break;

                case 5:
                    System.out.println("Thank you! Visit again.");
                    break;

                default:
                    System.out.println("Invalid choice!");
            }

        } while (choice != 5);

        sc.close();
    }
}
