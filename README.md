package MySQL;



import java.sql.Connection;
import java.sql.Date;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Scanner;

public class Project {
    // Attributes
    int Id, Quantity, Price;
    String Name;
    String packing_date, Expiry_date;
    Scanner sc = new Scanner(System.in);

    // Method to create the database table
    public void create_database(Connection con) {
        try {
            // Prepare SQL statement to create the table
            PreparedStatement st = con.prepareStatement("Create table Store (p_id int primary key,p_name varchar(30),p_quantity int ,p_price int,p_packingdate date,p_Expiry date);");
            // Execute SQL query to create the table
            st.execute();
            System.out.println("\nTable Created Successfully");
        } catch (Exception e) {
            // Handle exceptions if any occur during table creation
            System.err.println(e.getMessage());
        }
    }

    // Method to insert data into the table
    public void insert(Connection con) {
        char ans;
        try {
            do {
                // Prepare SQL statement to insert values into the table
                PreparedStatement pst = con.prepareStatement("insert into Store Values (?,?,?,?,?,?)");
                // Prompt user for product details
                System.out.println("Enter id of the product :");
                Id = sc.nextInt();
                System.out.println("Enter Name of the product :");
                Name = sc.next();
                System.out.println("Enter quantity of the product :");
                Quantity = sc.nextInt();
                System.out.println("Enter price of the product :");
                Price = sc.nextInt();
                System.out.println("Enter Packing date of the product :");
                packing_date = sc.next();
                Date p_date = Date.valueOf(packing_date);
                System.out.println("Enter Expiry date of the product :");
                Expiry_date = sc.next();
                Date E_date = Date.valueOf(Expiry_date);

                // Set values to the prepared statement
                pst.setInt(1, Id);
                pst.setString(2, Name);
                pst.setInt(3, Quantity);
                pst.setInt(4, Price);
                pst.setDate(5, p_date);
                pst.setDate(6, E_date);
                // Execute SQL query to insert data into the table
                pst.executeUpdate();
                System.out.println("\nData Inserted Successfully ");
                // Prompt user for further actions
                System.out.println("\nDo you want to update something else ? ");
                ans = sc.next().charAt(0);
            } while (ans == 'y' || ans == 'Y');
        } catch (Exception e) {
            // Handle exceptions if any occur during data insertion
            System.err.println(e.getMessage());
        }
    }

    // Method to display all data from the table
    public void display_table(Connection con) {
        try {
            // Create a statement for executing SQL queries
            Statement st = con.createStatement();
            // Execute SQL query to select all data from the table
            ResultSet rs = st.executeQuery("select * from Store");
            // Print table header
            System.out.println("\nP_id\tP_Name\tP_Quantity\tP_Price\t\tP_Packingdate\tP_Expiredate");
            // Iterate through the result set and print each row
            while (rs.next()) {
                System.out.println(rs.getInt(1) + "\t" + rs.getString(2) + "\t" + rs.getInt(3) + "\t\t" + rs.getInt(4) + "\t\t" + rs.getDate(5) + "\t" + rs.getDate(6));
            }
        } catch (Exception e) {
            // Handle exceptions if any occur during data retrieval
            System.err.println(e.getMessage());
        }
    }

    // Method to perform all database operations
    public void operation() {
        try {
            //Step 1: Register the JDBC driver
            Class.forName("com.mysql.cj.jdbc.Driver");
            //Step 2: Establish connection with the database
            Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/College", "root", "root");
            // Loop to display menu and perform operations until user exits
            while (true) {
                // Display menu options
                System.out.println("\nEnter your choice from below options");
                // Get user input for operation choice
                int Choice = sc.nextInt();
                // Perform operations based on user choice
                switch (Choice) {
                    // Cases for different operations
                }
            }
        } catch (Exception e) {
            // Handle exceptions if any occur during database operations
            System.out.println(e.getMessage());
        }
    }

    // Entry point of the program
    public static void main(String[] args) throws Exception {
        // Create an instance of the Project class
        Project p = new Project();
        // Call the operation method to start database operations
        p.operation();
    }
}
