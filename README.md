#   Employee Data Base  Based  on  OOPS Concept

package employe;

public class EmployD {
	int id;
	int age;
	String name;
	String address;
	double salary;

	public int getId()

	{
		return id;
	}

	public void setId(int id)

	{
		this.id = id;
	}

	public int getAge()

	{
		return age;
	}

	public void setAge(int age)

	{
		this.age = age;
	}

	public String getName()

	{
		return name;
	}

	public void setName(String name)

	{
		this.name = name;
	}

	public String getAddress()

	{
		return address;
	}

	public void setAddress(String address)

	{
		this.address = address;
	}

	public double getSalary()

	{
		return salary;
	}

	public void setSalary(double salary)

	{
		this.salary = salary;
	}
}

package employe;

import java.sql.*;
import java.util.Scanner;

public class EmpData {
	static final String JDBC_DRIVER = "com.mysql.cj.jdbc.Driver";
	private static final String url = "jdbc:mysql://localhost:3308/employedata";
	private static final String user = "root";
	private static final String pwd = "root";
	EmployD ac = new EmployD();

	public static void main(String[] args) {
		Connection con = null;
		EmpData sc = new EmpData();
		Scanner sa = new Scanner(System.in);
		int choice;
		do

		{

			System.out.println("1.insert record");

			System.out.println("2view record");

			System.out.println("3.update record");

			System.out.println("4.delete record");

			System.out.println("5.search_entity");

			System.out.println("6 exit");

			System.out.println("select your choice:");
			choice = sa.nextInt();
			switch (choice)

			{

			case 1:
				sc.insertdata();
				break;
			case 2:
				sc.viewdata();
				break;
			case 3:
				sc.updatedata();
				break;
			case 4:
				sc.deletedata();
				break;
			case 5:
				sc.search_entity();
				break;
			case 6:
				System.out.println(" thank you for using ---EMS----");
			}

		} while (choice != 6); // if choice is 6 it will exit the programme

	}
	// --------------------------------------jdbc Connectivity---------------------------------------------//

	public Connection getConnect()

	{
		try

		{
			Class.forName(JDBC_DRIVER);
			//System.out.println("------driver is loaded--------");
			Connection con = DriverManager.getConnection(url, user, pwd);
			System.out.println("");
			System.out.println("--------connection established--------");
			return con;
		} catch (Exception e)

		{
			e.printStackTrace();// it display errors in method
			return null;
		}

	}
	// --------------------------------insert data--------------------------------------------------------//

	public void insertdata()

	{
		Scanner sa = new Scanner(System.in);
		System.out.println("enter id :");
		ac.setId(sa.nextInt());

		System.out.println("enter age :");
		ac.setAge(sa.nextInt());
		System.out.println("enter name :");
		ac.setName(sa.next());

		System.out.println("enter salary :");
		ac.setSalary(sa.nextDouble());
		System.out.println("enter address:");
		ac.setAddress(sa.next());
		// if we need call another class we need a create object of that class
		try

		{
			Connection con = getConnect();

			PreparedStatement stm = con
					.prepareStatement("insert into employee(id,name,age,salary,address)values(?,?,?,?,?)");
			stm.setInt(1, ac.getId());
			stm.setInt(3, ac.getAge());
			stm.setString(2, ac.getName());
			stm.setDouble(4, ac.getSalary());
			stm.setString(5, ac.getAddress());
			int x = stm.executeUpdate();
			con.close();
			stm.close();
			if (x == 1)

			{
				System.out.println("inserted entity successfully");
			} else

			{
				System.out.println("   entity is not inserted");
			}

		} catch (Exception e)

		{
			e.printStackTrace();
		} finally

		{
			System.out.println();
		}
	}
	// ----------------------------------------view data// -----------------------------------------------//

	public void viewdata()

	{

		try

		{
			Connection con = getConnect();
			PreparedStatement stm = con.prepareStatement("select* from employee");
			ResultSet rs = stm.executeQuery();
			while (rs.next()) {
				System.out.println(rs.getString(1) + " " + rs.getString(2) + " " + rs.getString(3) + " "
						+ rs.getString(4) + " " + rs.getString(5));

				// rs.getstring it automatically convert int ,double based on variable..
			}
			rs.close();
			con.close(); // closing the connection
			stm.close();
		} catch (Exception e)

		{
			e.printStackTrace();
		}

	}
	// --------------------------------------updatedata---------------------------------------------------------------------//
private void updatedata() 
	
	{
		Scanner sa = new Scanner(System.in);

		System.out.println("enter id");
		int id = sa.nextInt();
      ac.setId(id);
		System.out.println("enter age");
		int age = sa.nextInt();
 ac.setAge(age);
		System.out.println("enter name");
		String name = sa.next();
ac.setName(name);
		System.out.println("enter salary");
		double salary = sa.nextDouble();
		ac.setSalary(salary);
		System.out.println("enter address");
		String address = sa.next();
 ac.setAddress(address);
		try 
		
		{
			Connection con = getConnect();
String str="update employee set age=?,name=?,salary=?,address=?  where id=?";
			PreparedStatement stm =con.prepareStatement(str);
			stm.setInt(1, ac.getAge());
			stm.setString(2, ac.getName());
			stm.setDouble(3, ac.getSalary());
			stm.setString(4, ac.getAddress());
			stm.setInt(5, ac.getId());
			
			int x=stm.executeUpdate();
			stm.close();
			con.close();
			
			if(x==1) {
				System.out.println("update done");
			}else {
				System.out.println(" record not found");
			}
			
		} catch (Exception e) 
		
		{
			e.printStackTrace();
		}
	}

	// --------------------------------- search entity------------------------------------------------//

	private void search_entity()

	{
		try

		{
			Scanner sa = new Scanner(System.in);

			int id;
			System.out.println("enter the id :");
			id = sa.nextInt();
			Connection con = getConnect();

			PreparedStatement stm = con.prepareStatement(" select * from employee where id=?");
			stm.setInt(1, id);
			ResultSet ra = stm.executeQuery();
			while (ra.next())
				System.out.println(ra.getString(1) + " " + ra.getString(2) + " " + ra.getString(3) + " "
						+ ra.getString(4) + " " + ra.getString(5));
			stm.close();
			con.close(); // closing the connection//

		} catch (Exception e)

		{
			e.printStackTrace();
		}

	}
//------------------------------------- delete data-----------------------------------------------//

	private void deletedata()

	{
		try

		{
			Scanner sa = new Scanner(System.in);

			int id;
			System.out.println("enter the id :");
			id = sa.nextInt();
			Connection con = getConnect();

			PreparedStatement stm = con.prepareStatement(" delete from employee where id=?");
			stm.setInt(1, id);
			int x = stm.executeUpdate();
			stm.close(); // closing the connection//
			con.close();
			if (x >= 1)

			{
				System.out.println(" recorded deleted succesfully");
			} else

			{
				System.out.println(" record not found");
			}
		} catch (Exception e)

		{
			e.printStackTrace();
		}

	}
}
  /****
   output
   insert record
2view record
3.update record
4.delete record
5.search_entity
6 exit
select your choice:
2


--------connection established--------
1 sunil 12 21000.0 mumbai
2 siva 21 21000.0 hyd
3 kumar 21 32000.0 mumbai
1.insert record
2view record
3.update record
4.delete record
5.search_entity
6 exit
select your choice:
5
enter the id :
2

--------connection established--------
2 siva 21 21000.0 hyd
1.insert record
2view record
3.update record
4.delete record
5.search_entity
6 exit
select your choice:

  
  */
