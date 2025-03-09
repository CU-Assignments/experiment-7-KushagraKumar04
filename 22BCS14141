// Easy Level

// index.html
<!DOCTYPE html>
<html>
<head>
    <title>Login Page</title>
</head>
<body>
    <form action="LoginServlet" method="post">
        Username: <input type="text" name="username"><br>
        Password: <input type="password" name="password"><br>
        <input type="submit" value="Login">
    </form>
</body>
</html>

// loginservlet.java

import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class LoginServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        String username = request.getParameter("username");
        String password = request.getParameter("password");
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();
        if (username.equals("admin") && password.equals("1234")) {
            out.println("<h1>Welcome, " + username + "!</h1>");
        } else {
            out.println("<h1>Invalid Credentials</h1>");
        }
    }
}
------------------------------------------------------------------------------------------------------
// Medium Level

// index.html

<!DOCTYPE html>
<html>
<head>
    <title>Employee Search</title>
</head>
<body>
    <form action="EmployeeServlet" method="post">
        Enter Employee ID: <input type="text" name="empId"><br>
        <input type="submit" value="Search">
    </form>
</body>
</html>


// Employeeservlet.java

import java.io.*;
import java.sql.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class EmployeeServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        String empId = request.getParameter("empId");
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
            Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/company", "root", "password");
            PreparedStatement ps = con.prepareStatement("SELECT * FROM employee WHERE id=?");
            ps.setString(1, empId);
            ResultSet rs = ps.executeQuery();
            if (rs.next()) {
                out.println("<h1>Employee Details</h1>");
                out.println("ID: " + rs.getString("id") + "<br>");
                out.println("Name: " + rs.getString("name") + "<br>");
                out.println("Department: " + rs.getString("department") + "<br>");
            } else {
                out.println("<h1>No Employee Found</h1>");
            }
        } catch (Exception e) {
            out.println(e);
        }
    }
}

// SQl table structure

CREATE TABLE employee (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    department VARCHAR(50)
);


---------------------------------------------------------------------------------------------------------------------------

// Hard Level

// index.html

<!DOCTYPE html>
<html>
<head>
    <title>Student Attendance</title>
</head>
<body>
    <form action="AttendanceServlet" method="post">
        Student Name: <input type="text" name="name"><br>
        Date: <input type="date" name="date"><br>
        Status: 
        <select name="status">
            <option value="Present">Present</option>
            <option value="Absent">Absent</option>
        </select><br>
        <input type="submit" value="Submit">
    </form>
</body>
</html>


// AttendanceServlet.java

import java.io.*;
import java.sql.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class AttendanceServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        String name = request.getParameter("name");
        String date = request.getParameter("date");
        String status = request.getParameter("status");
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
            Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/school", "root", "password");
            PreparedStatement ps = con.prepareStatement("INSERT INTO attendance(name, date, status) VALUES(?,?,?)");
            ps.setString(1, name);
            ps.setString(2, date);
            ps.setString(3, status);
            ps.executeUpdate();
            response.sendRedirect("attendance.jsp");
        } catch (Exception e) {
            response.getWriter().println(e);
        }
    }
}


// Attendance.jsp

<%@ page import="java.sql.*" %>
<html>
<body>
<h1>Attendance Records</h1>
<table border="1">
<tr><th>Name</th><th>Date</th><th>Status</th></tr>
<%
    try {
        Class.forName("com.mysql.cj.jdbc.Driver");
        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/school", "root", "password");
        Statement stmt = con.createStatement();
        ResultSet rs = stmt.executeQuery("SELECT * FROM attendance");
        while (rs.next()) {
%>
<tr>
    <td><%= rs.getString("name") %></td>
    <td><%= rs.getString("date") %></td>
    <td><%= rs.getString("status") %></td>
</tr>
<%
        }
    } catch (Exception e) {
        out.println(e);
    }
%>
</table>
</body>
</html>


// SQL Table Structure

CREATE TABLE attendance (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50),
    date DATE,
    status VARCHAR(20)
);
------------------------------------------------------------------------------------------


