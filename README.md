# Mysql


package MySQL;

import java.sql.Connection;
import java.sql.Date;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Scanner;

public class Project 
{
	int Id,Quantity,Price;
	String Name;
	String packing_date,Expiry_date;
	Scanner sc = new Scanner(System.in);
	
	public void create_database(Connection con) 
	{	
		try
		{
			PreparedStatement st =con.prepareStatement("Create table Store (p_id int primary key,p_name varchar(30),p_quantity int ,p_price int,p_packingdate date,p_Expiry date);");
			st.execute();
			System.out.println("\nTable Created Sucessfully");
		}
		catch (Exception e) 
		{
			System.err.println(e.getMessage());
		}
	}
	
	
	public void insert(Connection con) 
	{
		char ans;
		try
		{
			do
			{
				PreparedStatement pst= con.prepareStatement("insert into Store Values (?,?,?,?,?,?)");	
				System.out.println("Enter id of the product :");
				Id=sc.nextInt();
				System.out.println("Enter Name of the product :");
				Name=sc.next();
				System.out.println("Enter quantity of the product :");
				Quantity=sc.nextInt();
				System.out.println("Enter price of the product :");
				Price=sc.nextInt();
				System.out.println("Enter Packing date of the product :");
				packing_date=sc.next();
				Date p_date=Date.valueOf(packing_date);
				System.out.println("Enter Expiry date of the product :");
				Expiry_date=sc.next();
				Date E_date=Date.valueOf(Expiry_date);
				
				pst.setInt(1,Id);
				pst.setString(2,Name);
				pst.setInt(3,Quantity);
				pst.setInt(4,Price);
				pst.setDate(5,p_date);
				pst.setDate(6,E_date);
				pst.executeUpdate();
				System.out.println("\nData Inserted Successfully ");
				System.out.println("\nDo you want to update something else ? ");
				ans=sc.next().charAt(0);
			}
			while(ans=='y' || ans =='Y');
		}
		catch (Exception e) 
		{
			System.err.println(e.getMessage());
		}
		
	}
	
	public void display_table(Connection con) 
	{
		try
		{
			Statement st = con.createStatement();
			ResultSet rs =st.executeQuery("select * from Store");
			System.out.println("\nP_id\tP_Name\tP_Quantity\tP_Price\t\tP_Packingdate\tP_Expiredate");
			while(rs.next())
			{
				System.out.println(rs.getInt(1)+"\t"+rs.getString(2)+"\t"+rs.getInt(3)+"\t\t"+rs.getInt(4)+"\t\t"+rs.getDate(5)+"\t"+rs.getDate(6));
			}
		}
		catch (Exception e) 
		{
			System.err.println(e.getMessage());
		}
		
		
	}
	
	public void update (Connection con) 
	{
		char ans;
		int count;
		try
		{
			do
			{
				System.out.println("\nWhat do you want to update ");
				System.out.println("1) Product Name ");
				System.out.println("2) Product Quantity ");
				System.out.println("3) Product Price ");
				System.out.println("4) Product Packing Date  ");
				System.out.println("5) ProductExpiry Date ");
				int Choice=sc.nextInt();
				switch (Choice) 
				{
				case 1:
					System.out.println("\nEnter Product Id ");
					Id=sc.nextInt();
					System.out.println("Enter new Product Name ");
					Name=sc.next();
					PreparedStatement pst1= con.prepareStatement("update Store set P_Name=? where P_id=?");
					pst1.setString(1, Name);
					pst1.setInt(2, Id);
					count =pst1.executeUpdate();
					if(count>0)
					{
						System.out.println("\nData Updated Successfully ");
					}
					else
					{
						System.err.println("Data Not Entered ");
					}
					break;
				case 2:
					System.out.println("\nEnter Product Id ");
					Id=sc.nextInt();
					System.out.println("Enter new Product Quanity ");
					Quantity=sc.nextInt();
					PreparedStatement pst2= con.prepareStatement("update Store set P_Quantity=? where P_id=?");
					pst2.setInt(1, Quantity);
					pst2.setInt(2, Id);
					count=pst2.executeUpdate();
					if(count>0)
					{
						System.out.println("\nData Updated Successfully ");
					}
					else
					{
						System.err.println("Data Not Entered ");
					}
					
					break;
				case 3:
					System.out.println("\nEnter Product Id ");
					Id=sc.nextInt();
					System.out.println("Enter new Product Price ");
					Price=sc.nextInt();
					PreparedStatement pst3= con.prepareStatement("update Store set P_Price=? where P_id=?");
					pst3.setInt(1, Price);
					pst3.setInt(2, Id);
					count=pst3.executeUpdate();
					if(count>0)
					{
						System.out.println("\nData Updated Successfully ");
					}
					else
					{
						System.err.println("Data Not Entered ");
					}
					break;
				case 4:
				    System.out.println("\nEnter Product Id ");
				    Id = sc.nextInt();
				    System.out.println("Enter new Product Manufacture Date ");
				    packing_date = sc.next();
				    Date P_date = Date.valueOf(packing_date);
				    PreparedStatement pst4 = con.prepareStatement("update Store set P_packingdate=? where P_id=?");
				    pst4.setDate(1, P_date);
				    pst4.setInt(2, Id); 
				    count=pst4.executeUpdate();
				    if(count>0)
					{
						System.out.println("\nData Updated Successfully ");
					}
					else
					{
						System.err.println("Data Not Entered ");
					}
				    break;
				case 5:
					System.out.println("\nEnter Product Id ");
					Id=sc.nextInt();
					System.out.println("Enter new Product Expiry Date ");
					Expiry_date=sc.next();
					Date E_date=Date.valueOf(Expiry_date);
					PreparedStatement pst5= con.prepareStatement("update Store set p_Expiry=? where P_id=?");
					pst5.setDate(1, E_date);
					pst5.setInt(2, Id);
					count=pst5.executeUpdate();
					if(count>0)
					{
						System.out.println("\nData Updated Successfully ");
					}
					else
					{
						System.err.println("Data Not Entered ");
					}
					break;
					

				default:
					System.out.println("Wrong input");
					break;
				}
				
				System.out.println("\nDo you want to update something else ? ");
				ans=sc.next().charAt(0);
			}
			while(ans=='y' || ans =='Y');
		}
		catch (Exception e) 
		{
			System.err.println(e.getMessage());
		}
		
		
	}
	
	
	public void delete (Connection con) throws SQLException
	{
		try
		{
			System.out.println("Enter product id that you want to delete ");
			Id=sc.nextInt();
			PreparedStatement pst = con.prepareStatement("delete from Store where p_id=?");
			pst.setInt(1, Id);
			int count =pst.executeUpdate();
			if(count>0)
			{
				System.out.println("Data delete succcessfully ");
			}
			else
			{
				System.err.println("Query has not been Executed");
			}
		}
		catch (Exception e) 
		{
			System.err.println(e.getMessage());
		}
	}
	
	public void View (Connection con) throws SQLException
	{
		char ans;
		do
		{
			System.out.println("\nWhich data you want to see according to ? ");
			System.out.println("1) Product Id ");
			System.out.println("2) Product Name ");
			System.out.println("3) Product Quantity ");
			System.out.println("4) Product Price ");
			System.out.println("5) Product Packing Date  ");
			System.out.println("6) Product Expiry Date ");
			int Choice=sc.nextInt();
			switch (Choice) 
			{
			case 1:
				System.out.println("\nEnter Your The product id whose data you want to see ");
				Id=sc.nextInt();
				PreparedStatement pst1 =con.prepareStatement("select * from Store where p_id=?");
				pst1.setInt(1, Id);
				ResultSet rs1=pst1.executeQuery();
				System.out.println("P_id\tP_Name\tP_Quantity\tP_Price\t\tP_Packingdate\tP_Expiredate");
				while(rs1.next())
				{
					System.out.println(rs1.getInt(1)+"\t"+rs1.getString(2)+"\t"+rs1.getInt(3)+"\t\t"+rs1.getInt(4)+"\t\t"+rs1.getDate(5)+"\t"+rs1.getDate(6));
				}
				
				break;
			case 2:
				System.out.println("\nEnter Your The product Name whose data you want to see ");
				Name=sc.next();
				PreparedStatement pst2 =con.prepareStatement("select * from Store where p_name=?");
				pst2.setString(1, Name);
				ResultSet rs2=pst2.executeQuery();
				System.out.println("P_id\tP_Name\tP_Quantity\tP_Price\t\tP_Packingdate\tP_Expiredate");
				while(rs2.next())
				{
					System.out.println(rs2.getInt(1)+"\t"+rs2.getString(2)+"\t"+rs2.getInt(3)+"\t\t"+rs2.getInt(4)+"\t\t"+rs2.getDate(5)+"\t"+rs2.getDate(6));
				}
				break;
			case 3:
				System.out.println("\nEnter Your The product Quantity whose data you want to see ");
				Quantity=sc.nextInt();
				PreparedStatement pst3 =con.prepareStatement("select * from Store where p_quantity=?");
				pst3.setInt(1, Quantity);
				ResultSet rs3=pst3.executeQuery();
				System.out.println("P_id\tP_Name\tP_Quantity\tP_Price\t\tP_Packingdate\tP_Expiredate");
				while(rs3.next())
				{
					System.out.println(rs3.getInt(1)+"\t"+rs3.getString(2)+"\t"+rs3.getInt(3)+"\t\t"+rs3.getInt(4)+"\t\t"+rs3.getDate(5)+"\t"+rs3.getDate(6));
				}
				break;
			case 4:
				System.out.println("\nEnter Your The product Price whose data you want to see ");
				Price=sc.nextInt();
				PreparedStatement pst4 =con.prepareStatement("select * from Store where p_price=?");
				pst4.setInt(1, Price);
				ResultSet rs4=pst4.executeQuery();
				System.out.println("P_id\tP_Name\tP_Quantity\tP_Price\t\tP_Packingdate\tP_Expiredate");
				while(rs4.next())
				{
					System.out.println(rs4.getInt(1)+"\t"+rs4.getString(2)+"\t"+rs4.getInt(3)+"\t\t"+rs4.getInt(4)+"\t\t"+rs4.getDate(5)+"\t"+rs4.getDate(6));
				}
				break;
			case 5:
				System.out.println("Enter Your The product Packing Date whose data you want to see ");
				packing_date=sc.next();
				PreparedStatement pst5=con.prepareStatement("select * from Store where p_packingdate=?");
				Date p_date=Date.valueOf(packing_date);
				pst5.setDate(1, p_date);
				ResultSet rs5=pst5.executeQuery();
				System.out.println("P_id\tP_Name\tP_Quantity\tP_Price\t\tP_Packingdate\tP_Expiredate");
				while(rs5.next())
				{
					System.out.println(rs5.getInt(1)+"\t"+rs5.getString(2)+"\t"+rs5.getInt(3)+"\t\t"+rs5.getInt(4)+"\t\t"+rs5.getDate(5)+"\t"+rs5.getDate(6));
				}
				break;
			case 6:
				System.out.println("Enter Your The product Expiry Date whose data you want to see ");
				Expiry_date=sc.next();
				PreparedStatement pst6=con.prepareStatement("select * from Store where p_Expiry=?");
				Date E_date=Date.valueOf(Expiry_date);
				pst6.setDate(1, E_date);
				ResultSet rs6=pst6.executeQuery();
				System.out.println("P_id\tP_Name\tP_Quantity\tP_Price\t\tP_Packingdate\tP_Expiredate");
				while(rs6.next())
				{
					System.out.println(rs6.getInt(1)+"\t"+rs6.getString(2)+"\t"+rs6.getInt(3)+"\t\t"+rs6.getInt(4)+"\t\t"+rs6.getDate(5)+"\t"+rs6.getDate(6));
				}
				break;

			default:
				System.out.println("Wrong Input ");
				break;
			}
			System.out.println("\nDo you want to Check something else ? ");
			ans=sc.next().charAt(0);
		}
		while(ans=='y' || ans =='Y');
		
	}
	
	public void order_by(Connection con ) throws SQLException
	{
		char ans;
		try
		{
			do
			{
				 Statement st = con.createStatement();
				 System.out.println("\nEnter the name by whoose order do you want to see the table");
				 String Order_name=sc.next();
				 System.out.println("\nIn ascending (asc) or Descending (desc) Order :");
				 String Order_format=sc.next();
				 ResultSet rs = st.executeQuery("select * from Store order by "+Order_name+" "+Order_format); // Modify the ORDER BY clause as per your requirement
				 System.out.println("P_id\tP_Name\tP_Quantity\tP_Price\t\tP_Packingdate\tP_Expiredate");
				 while(rs.next()) 
				 {
					 System.out.println(rs.getInt(1)+"\t"+rs.getString(2)+"\t"+rs.getInt(3)+"\t\t"+rs.getInt(4)+"\t\t"+rs.getDate(5)+"\t\t"+rs.getDate(6));
			     }
				 System.out.println("\nDo you want print table by another order");
				 ans=sc.next().charAt(0);
			}
			while(ans=='y' || ans=='Y');
		}
		catch (Exception e) 
		{
			System.err.println(e.getMessage());
		}
		 		
	}
	
	public void dropTable(Connection con)
	{
		try 
		{
			Statement st = con.createStatement();
			st.executeUpdate("drop table Store ");
			System.out.println("\nTable droped Succesfully");
		}
		catch (Exception e) 
		{
			System.err.println(e.getMessage());
		}
	}
	
	
	public void addcolumn(Connection con)
	{
		try
		{
			System.out.println("\nEnter column name that you want to add ");
			String add=sc.next();
			System.out.println("Enter data type dor that column ");
			String data=sc.next();
			PreparedStatement pst = con.prepareStatement("alter table Store add column "+add+" "+data);
			pst.executeUpdate();
			System.out.println("\ncolumn added Success fully ");
		}
		catch (Exception e) 
		{
			System.err.println(e.getMessage());
		}
	}
	
	
	public void dropcolumn(Connection con)
	{
		try
		{
			System.out.println("\nEnter column name that you want to drop ");
			String add=sc.next();
			PreparedStatement pst = con.prepareStatement("alter table Store drop column "+add);
			pst.executeUpdate();
			System.out.println("\ncolumn Dropped Success fully ");
		}
		catch (Exception e) 
		{
			System.err.println(e.getMessage());
		}
	}
	
	
	
	public void operation()
	{
		try
		{
			//Step 1) it is use to resgiter the driver . forName() method of Class is used to register the driver
			Class.forName("com.mysql.cj.jdbc.Driver");
			//Step 2) It is use to make connection with database . getConnection  method of DriverManger is used to get the connection .
			Connection con=DriverManager.getConnection("jdbc:mysql://localhost:3306/College","root","root");
			while(true)
			{
				System.out.println("\nEnter your choice from below options");
				System.out.println("1) To create a Table");
				System.out.println("2) To Insert The value Into the Table");
				System.out.println("3) To Display The entire Data of that Table");
				System.out.println("4) To Update The values in Table ");
				System.out.println("5) To Delete the values in Table");
				System.out.println("6) To Display Specific Data ");
				System.out.println("7) To Display Table Order by  ");
				System.out.println("8) Drop the table");
				System.out.println("9) Add Column to the table");
				System.out.println("10) Drop Column from the table");
				System.out.println("11) To Exit");
				int Choice=sc.nextInt();
				switch (Choice) 
				{
				case 1:
					create_database(con);
					break;
				case 2:
					insert(con);
					break;
				case 3:
					display_table(con);
					break;
				case 4:
					update(con);
					break;
				case 5:
					delete(con);
					break;
				case 6:
					View(con);
					break;
				case 7:
					order_by(con);
					break;
				case 8:
					dropTable(con);
					break;
				case 9:
					addcolumn(con);
					break;
				case 10:
					column(con);
					break;
				case 11:
					System.exit(0);
					break;

				default:
					System.out.println("Invalid Choice ");
					break;
				}
				
			}
			
		}
		catch (Exception e) 
		{
			System.out.println(e.getMessage());
		}
					
	}
	
	public static void main(String[] args) throws Exception 
	{
	    Project p = new Project();
	    p.operation();
   
	}
	
	
	 
}
