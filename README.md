# TomCatServer
Here is a **step-by-step guide with commands and code** to create a basic **Attendance Management System** (Java + Servlets + JSP + MySQL + Maven) **from scratch using the terminal in Windows**.

---

## ✅ STEP 1: Create Project Directory with Maven

Open **Command Prompt (CMD)** and run:

```bash
mkdir AttendanceManagementSystem
cd AttendanceManagementSystem
mvn archetype:generate -DgroupId=com.attendance -DartifactId=attendance-management -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMode=false
```

> This creates a basic Maven web app with folder structure.

---

## ✅ STEP 2: Move into the Project Folder

```bash
cd attendance-management
```

---

## ✅ STEP 3: Open in Any Editor (VS Code or IntelliJ)

```bash
code .
```

> Or open IntelliJ > Open > Select this folder.

---

## ✅ STEP 4: Update `pom.xml` with Required Dependencies

Replace the content of `pom.xml` with:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>
    <groupId>com.attendance</groupId>
    <artifactId>attendance-management</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>war</packaging>

    <name>Attendance Management</name>

    <properties>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- Servlet API -->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>4.0.1</version>
            <scope>provided</scope>
        </dependency>

        <!-- JSP -->
        <dependency>
            <groupId>javax.servlet.jsp</groupId>
            <artifactId>javax.servlet.jsp-api</artifactId>
            <version>2.3.3</version>
            <scope>provided</scope>
        </dependency>

        <!-- JSTL -->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>jstl</artifactId>
            <version>1.2</version>
        </dependency>

        <!-- MySQL Connector -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.33</version>
        </dependency>
    </dependencies>

</project>
```

---

## ✅ STEP 5: Setup Directory for Java Classes

Create the folder manually or use:

```bash
mkdir -p src/main/java/com/attendance/controller
mkdir -p src/main/java/com/attendance/model
mkdir -p src/main/java/com/attendance/dao
```

---

## ✅ STEP 6: Add a Servlet – `LoginServlet.java`

Create a file:
`src/main/java/com/attendance/controller/LoginServlet.java`

```java
package com.attendance.controller;

import javax.servlet.*;
import javax.servlet.http.*;
import java.io.IOException;

public class LoginServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) 
        throws ServletException, IOException {
        
        String username = request.getParameter("username");
        String password = request.getParameter("password");

        if ("admin".equals(username) && "admin123".equals(password)) {
            response.sendRedirect("dashboard.jsp");
        } else {
            response.sendRedirect("login.jsp?error=true");
        }
    }
}
```

---

## ✅ STEP 7: Add `web.xml` for Servlet Configuration

Location: `src/main/webapp/WEB-INF/web.xml`

```xml
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         version="3.1">
    <servlet>
        <servlet-name>LoginServlet</servlet-name>
        <servlet-class>com.attendance.controller.LoginServlet</servlet-class>
    </servlet>

    <servlet-mapping>
        <servlet-name>LoginServlet</servlet-name>
        <url-pattern>/login</url-pattern>
    </servlet-mapping>

    <welcome-file-list>
        <welcome-file>login.jsp</welcome-file>
    </welcome-file-list>
</web-app>
```

---

## ✅ STEP 8: Create Basic `login.jsp` Page

Location: `src/main/webapp/login.jsp`

```jsp
<!DOCTYPE html>
<html>
<head>
    <title>Login</title>
</head>
<body>
<h2>Login Page</h2>
<form method="post" action="login">
    Username: <input type="text" name="username" required/><br/>
    Password: <input type="password" name="password" required/><br/>
    <input type="submit" value="Login"/>
</form>

<% if (request.getParameter("error") != null) { %>
    <p style="color:red;">Invalid credentials</p>
<% } %>
</body>
</html>
```

---

## ✅ STEP 9: Create a Dummy Dashboard Page

Location: `src/main/webapp/dashboard.jsp`

```jsp
<%@ page contentType="text/html;charset=UTF-8" %>
<html>
<head>
    <title>Dashboard</title>
</head>
<body>
    <h1>Welcome, Admin!</h1>
</body>
</html>
```

---

## ✅ STEP 10: Build and Deploy

### Compile the project:

```bash
mvn clean package
```

It generates a `target/attendance-management.war` file.

### Deploy to Tomcat:

1. Copy the WAR to Tomcat’s `webapps` folder.

2. Start Tomcat:

   ```bash
   cd path\to\tomcat\bin
   startup.bat
   ```

3. Open your browser:
   `http://localhost:8080/attendance-management`

---

## ✅ Next Steps:

If you'd like, I can help you:

* Connect to **MySQL** using JDBC
* Create real **DAO classes**
* Build a proper **admin/student/faculty dashboard**
* Generate **attendance reports**
* Add **CSS/JS frontend**

Would you like the MySQL database creation SQL and JDBC connection next?
