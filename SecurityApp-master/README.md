Overview
This project implements JWT-based authentication for a secure RESTful API using Spring Boot, Spring Security, and JWT. It includes user registration, login, and role-based authorization. The authentication is based on JSON Web Tokens (JWT), which provides a stateless, secure way to handle user sessions. The project also supports refresh tokens for improved security and user experience.

Features : 
  User Registration & Login: Allows users to register and authenticate using their credentials.
  Role-Based Authorization: Implements role-based access control (RBAC) to restrict access to specific resources.
  JWT Authentication: Secures RESTful APIs with JWT tokens for stateless user authentication.
  Refresh Tokens: Provides refresh token functionality to extend the validity of the authentication session.
  Spring Security: Secures API endpoints and protects sensitive routes from unauthorized access.
  MySQL Database: Stores user credentials and roles in a MySQL database.
Technologies Used : 
Java (Programming Language)
Spring Boot (Framework)
Spring Security (Authentication & Authorization)
JWT (JSON Web Token) (Authentication)
JPA (Java Persistence API) (Database Operations)
MySQL (Database)
Maven (Dependency Management)
JWT Structure
The JWT used in this project consists of three parts:

Header: Specifies the token type and the signing algorithm used (e.g., HS256).
Payload: Contains the claims or user-specific data (such as username, roles, etc.).
Signature: Ensures the integrity of the token by verifying that it hasn't been altered.
API Endpoints
1. User Registration
Endpoint: POST /api/auth/register

Registers a new user by providing username, password, and roles (optional).
Hashes the password before storing it in the database.
Request Example:

json
{
  "username": "user1",
  "password": "password123",
  "roles": ["USER"]
}
Response Example:

json

{
  "message": "User registered successfully!"
}
2. User Login
Endpoint: POST /api/auth/login

Logs in a user with username and password.
Returns a JWT access token and a refresh token.
Request Example:

json

{
  "username": "user1",
  "password": "password123"
}
Response Example:

json

{
  "accessToken": "jwt_access_token_here",
  "refreshToken": "jwt_refresh_token_here"
}
3. Access Protected Resource
Endpoint: GET /api/protected-resource

Access is granted only with a valid JWT access token.
Authorization Header Example:


Authorization: Bearer <access_token>
Response Example (on success):

{
  "message": "You have access to this resource."
}
4. Refresh Token
Endpoint: POST /api/auth/refresh

Refreshes the JWT access token using a valid refresh token.
Request Example:


{
  "refreshToken": "valid_refresh_token_here"
}
Response Example:

json

{
  "accessToken": "new_jwt_access_token_here"
}
Setup and Installation
Prerequisites
Java 11 or higher
Maven (for dependency management and building the project)
MySQL Database (for user and roles storage)
1. Clone the Repository

git clone https://github.com/your-username/jwt-authentication-spring-boot.git
cd jwt-authentication-spring-boot
2. Configure MySQL Database
Create a MySQL database and user for this project.
Update the application.properties file with your database credentials:
properties
spring.datasource.url=jdbc:mysql://localhost:3306/your_database_name
spring.datasource.username=your_db_username
spring.datasource.password=your_db_password
spring.jpa.hibernate.ddl-auto=update
3. Build and Run the Application
Install the required dependencies and build the application using Maven:

mvn clean install
Run the Spring Boot application:

mvn spring-boot:run
The application should now be running on http://localhost:8080.
4. Testing the Endpoints
  You can use tools like Postman or cURL to test the API endpoints.
  For the login endpoint, pass the username and password in the request body to receive the JWT tokens.
  Use the JWT access token to make requests to protected endpoints.
  JWT Token Expiry and Refresh
  The access token expires after a set period (e.g., 15 minutes).
  The refresh token can be used to get a new access token without needing to log in again.
  When the access token expires, you can send the refresh token to the /api/auth/refresh endpoint to obtain a new access token.
Security Considerations
  Password hashing: User passwords are stored securely using BCrypt hashing.
  JWT signing: The JWT token is signed with a secret key to ensure integrity and prevent tampering.
  Token expiration: Access tokens are short-lived to minimize the impact of potential token theft.
Future Improvements
  Add support for additional user roles and permissions.
  Implement email verification for user registration.
  Enhance error handling and validation for API requests.
  Integrate with external OAuth providers (e.g., Google, Facebook).
