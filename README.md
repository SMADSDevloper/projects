#   Employee Data  Based  on  OOPS Concept

 #  description 
<i>This Employee Management System Project application stores all the employee's information in a database. It is an application developed in Java GUI technology and database used is SQLite. It contains employee information like employee id, first name etc .</i>
<br>
 #  Software Requirements
Windows XP
Apache Tomcat Web Server
Oracle

##  Technology Used
Java ,SQL, jdbc

## Hardware Requirements
Hard Disk – 2 GB
RAM – 1 GB
Processor – Dual Core or Above
Mouse
Keyboard





 # software installation 
 <li>
   <b>   java  </b><br>
    java  is  most  popular  web  base  programme  language.Java is a widely used object-oriented programming language and software platform that runs on billions of devices, including notebook computers, mobile devices, gaming consoles, medical devices and many others. The rules and syntax of Java are based on the C and C++ languages.
    jdk 17 . version  download link  https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html.

  <strong> <b> DataBase :</b></strong> <br>
     these  are  two  Sql and NO-Sql  one is  file  based   data  type another  one  is  Tabular  form   data  base . my   programme   iam  using    SQL it  help  us  programme  insert ,update and retrive   the  data base.
 mysql   version 8.0.32  it  support  the programme .It offers the basic features you expect with a database management system, including the ability to create tables, views, triggers and stored procedures.
 SQL download  link : https://dev.mysql.com/downloads/mysql/
 <br>
<strong>  jdbc  connection : </strong> <br>
it is a  application programming interface (API) for the Java programming language, which defines how a client may access a database. It is a Java-based data access technology used for Java database connectivity. It is part of the Java Standard Edition platform, from Oracle Corporation.
   download  link :https://dev.mysql.com/downloads/connector/j/
	
	
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
	
	# Demo 


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
