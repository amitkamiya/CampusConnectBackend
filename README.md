# 🎓 Campus Connect Backend

Backend REST API for **Campus Connect**, a campus community platform that connects students, faculty, and administrators through campus events, Lost & Found, activities, authentication, and campus information.

The backend is built using **Spring Boot** and provides REST APIs consumed by the Campus Connect React frontend.

---

## 🚀 Features

### 🔐 Authentication & Security

* User registration and login
* JWT-based authentication
* Spring Security integration
* Protected API endpoints
* Role-based user support
* JWT token validation
* Configurable token expiration
* Secure request authorization

### 👥 User Management

The backend manages user information and provides APIs required by the frontend for:

* User registration
* User authentication
* User information
* Campus user statistics
* Role-based access

### 📅 Event Management

The API provides functionality for managing campus events:

* Create events
* Retrieve events
* Delete events
* Store event information using PostgreSQL

### 🔎 Lost & Found

Backend APIs support campus Lost & Found functionality:

* Create Lost & Found reports
* Retrieve Lost & Found records
* Store item details
* Track item type
* Track location and description
* Associate reports with users

### 📊 Campus Statistics

The backend provides APIs used by the frontend dashboard to retrieve campus statistics, including enrolled-user information.

---

## 🛠️ Tech Stack

| Technology            | Purpose                        |
| --------------------- | ------------------------------ |
| **Java 17**           | Backend programming language   |
| **Spring Boot 3.5.5** | Application framework          |
| **Spring Web**        | REST API development           |
| **Spring Data JPA**   | Database access                |
| **PostgreSQL**        | Relational database            |
| **Spring Security**   | Authentication & authorization |
| **JWT / JJWT**        | Token-based authentication     |
| **Lombok**            | Boilerplate reduction          |
| **Bean Validation**   | Request validation             |
| **Maven**             | Dependency management & build  |
| **Docker**            | Containerization               |

The dependencies are defined in `pom.xml`, including Spring Web, Spring Security, Spring Data JPA, PostgreSQL, JJWT, Lombok, and validation.

---

## 🏗️ Backend Architecture

The backend follows a layered Spring Boot architecture:

```text
                    ┌───────────────────┐
                    │      Client       │
                    │   React Frontend  │
                    └─────────┬─────────┘
                              │
                              │ HTTP / REST
                              ▼
                    ┌───────────────────┐
                    │    Controllers    │
                    │                   │
                    │ Auth              │
                    │ Users             │
                    │ Events            │
                    │ Lost & Found      │
                    └─────────┬─────────┘
                              │
                              ▼
                    ┌───────────────────┐
                    │     Services      │
                    │                   │
                    │ Business Logic    │
                    │ Validation        │
                    │ Authentication    │
                    └─────────┬─────────┘
                              │
                              ▼
                    ┌───────────────────┐
                    │   Repositories    │
                    │   Spring Data JPA │
                    └─────────┬─────────┘
                              │
                              ▼
                    ┌───────────────────┐
                    │    PostgreSQL     │
                    │     Database      │
                    └───────────────────┘
```

---

## 🔑 Authentication Flow

Campus Connect uses JWT-based authentication.

```text
User
 │
 ▼
Login Request
 │
 ▼
Authentication Controller
 │
 ▼
Spring Security
 │
 ▼
User Validation
 │
 ▼
JWT Generation
 │
 ▼
JWT Token
 │
 ▼
Frontend
```

For protected requests, the client sends:

```http
Authorization: Bearer <JWT_TOKEN>
```

The backend validates the token before allowing access to protected resources.

The configured JWT expiration is currently 24 hours.

---

## 🔌 API Endpoints

The backend exposes REST endpoints consumed by the Campus Connect frontend.

### Authentication

```http
POST /api/auth/register
POST /api/auth/login
```

### Events

```http
GET    /api/events
POST   /api/events
DELETE /api/events/{id}
```

### Lost & Found

```http
GET  /api/lostfound
POST /api/lostfound
```

### User / Campus Statistics

```http
GET /api/user/enrolled-count
```

> The exact endpoint behavior and authorization requirements are determined by the corresponding controller implementations.

---

## 🗄️ Database

The application uses **PostgreSQL** with Spring Data JPA.

Database configuration is supplied through environment variables:

```properties
DB_URL
DB_USERNAME
DB_PASSWORD
```

The application also uses:

```properties
spring.jpa.hibernate.ddl-auto=update
```

which allows Hibernate to update the database schema based on the JPA entities.

### Database Configuration Example

```env
DB_URL=jdbc:postgresql://localhost:5432/campusconnect
DB_USERNAME=postgres
DB_PASSWORD=your_password
```

---

## ⚙️ Getting Started

### Prerequisites

Install the following:

* **Java 17**
* **PostgreSQL**
* **Git**
* Maven
  *(Maven Wrapper is included, so a separate Maven installation is optional.)*

---

## 1. Clone the Repository

```bash
git clone https://github.com/amitkamiya/CampusConnectBackend.git
```

Navigate into the project:

```bash
cd CampusConnectBackend
```

---

## 2. Configure PostgreSQL

Create a PostgreSQL database:

```sql
CREATE DATABASE campusconnect;
```

---

## 3. Configure Environment Variables

Set the following environment variables:

```env
DB_URL=jdbc:postgresql://localhost:5432/campusconnect
DB_USERNAME=postgres
DB_PASSWORD=your_password
```

The application reads these values instead of storing database credentials directly in the source configuration.

---

## 4. Configure JWT Secret

Set a secure JWT secret through an environment variable.

For example:

```env
JWT_SECRET=your_secure_jwt_secret
```

**Do not commit real JWT secrets, database passwords, API keys, or other credentials to GitHub.**

---

## 5. Run the Application

### Windows

```bash
mvnw.cmd spring-boot:run
```

### Linux / macOS

```bash
./mvnw spring-boot:run
```

The backend runs on:

```text
http://localhost:8080
```

The default port is configurable through the `PORT` environment variable and falls back to `8080`.

---

## 📦 Build the Application

### Windows

```bash
mvnw.cmd clean package
```

### Linux / macOS

```bash
./mvnw clean package
```

The generated JAR can then be executed using:

```bash
java -jar target/CampusConnect-0.0.1-SNAPSHOT.jar
```

---

## 🐳 Docker

The project includes a Dockerfile based on **Eclipse Temurin Java 17**.

The Docker image:

1. Uses Java 17
2. Copies the project into the container
3. Builds the application using Maven Wrapper
4. Exposes port `8080`
5. Runs the generated Spring Boot JAR

The repository's Dockerfile currently follows this build flow.

### Build Docker Image

```bash
docker build -t campus-connect-backend .
```

### Run Container

```bash
docker run -p 8080:8080 campus-connect-backend
```

When using Docker, make sure the required database environment variables are supplied.

---

## 📁 Project Structure

```text
CampusConnectBackend/
│
├── .mvn/
│   └── wrapper/
│
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── ...
│   │   │
│   │   └── resources/
│   │       └── application.properties
│   │
│   └── test/
│
├── .gitattributes
├── .gitignore
├── Dockerfile
├── LICENSE
├── mvnw
├── mvnw.cmd
├── pom.xml
└── README.md
```

---

## 🔗 Frontend Integration

Campus Connect consists of separate frontend and backend repositories.

### Frontend

[CampusConnectFrontend](https://github.com/amitkamiya/CampusConnectFrontend)

### Backend

[CampusConnectBackend](https://github.com/amitkamiya/CampusConnectBackend)

The React frontend communicates with this Spring Boot backend through REST APIs using Axios.

```text
┌─────────────────────────────┐
│    Campus Connect Frontend  │
│       React + Vite          │
└──────────────┬──────────────┘
               │
               │ REST API
               │ JWT
               ▼
┌─────────────────────────────┐
│    Campus Connect Backend   │
│       Spring Boot           │
└──────────────┬──────────────┘
               │
               │ JPA
               ▼
┌─────────────────────────────┐
│         PostgreSQL          │
└─────────────────────────────┘
```

---

## 🔒 Security

The application uses:

* Spring Security
* JWT authentication
* Protected API endpoints
* Environment-based database configuration
* Request validation

### Important

Never commit sensitive values such as:

```text
Database passwords
JWT secrets
API keys
Cloud credentials
```

Use environment variables or a secure secrets manager instead.

---

## 🔮 Future Enhancements

* Refresh token support
* Email verification
* Password reset
* More granular role-based permissions
* API documentation with Swagger / OpenAPI
* Global exception handling
* Unit and integration test coverage
* Database migrations using Flyway or Liquibase
* Centralized logging
* Production monitoring
* CI/CD pipeline
* API rate limiting

---

## 👨‍💻 Author

**Amit Kumar**

Computer Science & Engineering Student

[GitHub](https://github.com/amitkamiya)

---

## 📄 License

This project is licensed under the **GPL-3.0 License**.

See the [LICENSE](LICENSE) file for details.
