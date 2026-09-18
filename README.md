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
                    │     Ser
```
