//# JDBC_APPLICATION
//RITRIVE THE DATA IN DATA BASE  USING JABA JDBC PROGRAME 
//SelectTest.java
package com.bce.JDBCApp1;
import java.sql.Connection;
import java.io.IOException;
import java.sql.ResultSet;
import java.sql.DriverManager;
import java.sql.Statement;
import java.util.Scanner;
public class SelectTest2 {

	public static void main(String[] args)throws Exception  {
		//initalizen variable
		Connection con=null;
		ResultSet rs=null;
		Scanner sc=null;
		Statement st=null;
		String s1=null;
		String s2=null;
		String s3=null;
		String cond=null;
	String queary=null;
		boolean flag=false;
		//create object 
		try {
			//input data end usere 
			sc=new Scanner(System.in);
			if(sc!=null)
			System.out.println("Enter the s1");
			s1=sc.next().toUpperCase();
			System.out.println("Enter the s2");
			s2=sc.next().toUpperCase();
			System.out.println("Enter the s3");
			s3=sc.next().toUpperCase();
			// from Condation 
			 cond="("+s1+","+s2+","+s3+")";
			 //Givend the ('CLEARK ','MANAGER','SELMAN');
			//load the deriver 
			Class.forName("oracl.jdbc.driver.OracleDriver");
			//establis connection 
			con=DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:xe","system","kundan");
			//create statement 
			if(con!=null)
			st=con.createStatement();
			//from select statement sql queqry 
			//SELECT empno,ename,job,sal,from emp where job  in('CLEARK','MAMNAGER','SALESMAN') ORDER BY JOB ;
			queary="select empno ,ename,job,sal from emp8 where job in"+cond+"order by job";
			System.out.println(queary);
			//send queary  in data base 
			if(st!=null)
			rs=st.executeQuery(queary);
			//processer the data Resultset 
			if(rs!=null)
			while(rs.next()) {
				flag=true;
				System.out.println(rs.getInt(1)+","+rs.getString(2)+","+rs.getString(3)+","+rs.getString(4));
			}//end while  
				if(flag==false) {
					System.out.println("No Record found ");
			
			}//end of if block 
	
		}//end of the try block
		 catch (ClassNotFoundException e) {
	            e.printStackTrace();
	        } catch (Exception e) {
	            e.printStackTrace();
	        } //END of the catch block
		finally {
			//close the object 
			try {
				if(rs!=null)
				rs.close();
			}catch(Exception e) {
				e.printStackTrace();
			}//end of the catch block 
			
			try {
				if(st!=null)
				st.close();
			}catch(Exception e) {
				e.printStackTrace();
			}//end of the catch block 
			
			try {
				if(con!=null)
				con.close();
			}catch(Exception e) {
				e.printStackTrace();
			}//end of the catch block 
		}//end of the finally block
	}//end of the main method 
}//end of the class 
