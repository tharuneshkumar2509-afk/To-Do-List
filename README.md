# 📋 TaskFlow — To-Do Management REST API

[![Java](https://img.shields.io/badge/Java-21-orange.svg?logo=openjdk&logoColor=white)](https://openjdk.org/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-4.0.8-brightgreen.svg?logo=springboot&logoColor=white)](https://spring.io/projects/spring-boot)
[![Spring Data JPA](https://img.shields.io/badge/Spring%20Data-JPA-blue.svg?logo=spring&logoColor=white)](https://spring.io/projects/spring-data-jpa)
[![Database](https://img.shields.io/badge/Database-H2%20In--Memory-blue.svg?logo=h2&logoColor=white)](https://www.h2database.com/)
[![Build](https://img.shields.io/badge/Build-Maven-C71A36.svg?logo=apache-maven&logoColor=white)](https://maven.apache.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A robust, lightweight, and modern **RESTful Task & To-Do Management API** built with **Spring Boot 4**, **Spring Data JPA**, and **Hibernate**. TaskFlow allows users to organize, filter, prioritize, and track tasks with clean input validation and seamless in-memory database persistence.

---

## ✨ Features

- ⚡ **Full CRUD Capabilities**: Create, read, update, and delete tasks effortlessly.
- 🔄 **Quick Status Toggle**: Mark tasks as completed or pending via a dedicated endpoint.
- 🎯 **Priority Management**: Classify tasks by priority level (`LOW`, `MEDIUM`, `HIGH`).
- 🔍 **Flexible Filtering**: Query tasks based on status (`completed=true/false`) or priority level.
- 🛡️ **Validation & Error Prevention**: Built-in Jakarta Bean Validation on request payloads (`@NotBlank`, `@NotNull`).
- 💾 **Embedded Persistence**: Pre-configured H2 in-memory database with Spring Data JPA repository integration.
- 🏗️ **Clean Architecture**: Separation of concerns across Controller, Service, Repository, and Entity layers.

---

## 🛠️ Technology Stack

| Component | Technology | Version |
| :--- | :--- | :--- |
| **Language** | Java | 21 (LTS) |
| **Framework** | Spring Boot | 4.0.8 |
| **Persistence** | Spring Data JPA / Hibernate | 7.2.x |
| **Database** | H2 Database (In-Memory) | 2.4.x |
| **Validation** | Jakarta Bean Validation | 3.1.x |
| **Build Tool** | Apache Maven & Maven Wrapper | 3.9.x |

---

## 🏛️ Project Architecture

TaskFlow adopts a standard layered architecture:

```text
com.taskflow
├── TaskflowApplication.java       # Application entry point
├── controller
│   └── TaskController.java        # REST endpoints & HTTP request mapping
├── service
│   └── TaskService.java           # Business logic & transaction handling
├── repository
│   └── TaskRepository.java        # Spring Data JPA data access layer
└── entity
    └── Task.java                  # JPA Entity & validation constraints
```

---

## 🚀 Getting Started

### Prerequisites

- **Java Development Kit (JDK)**: Version 21 or higher
- **Git**: Version 2.x or higher
- *(Optional)* **Maven**: Pre-bundled with `mvnw` / `mvnw.cmd` wrapper scripts

### 1. Clone the Repository

```bash
git clone https://github.com/Jaiamar/To-Do-List.git
cd To-Do-List
```

### 2. Build the Project

Run tests and compile the code:

**Windows (PowerShell / CMD):**
```powershell
.\mvnw.cmd clean test
```

**Linux / macOS:**
```bash
./mvnw clean test
```

### 3. Run the Application

Start the embedded Tomcat server on port `8080`:

**Windows:**
```powershell
.\mvnw.cmd spring-boot:run
```

**Linux / macOS:**
```bash
./mvnw spring-boot:run
```

The application will start at: `http://localhost:8080`

---

## 📖 REST API Documentation

### Base URL
```
http://localhost:8080/api/tasks
```

### Endpoints Overview

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/api/tasks` | Create a new task |
| `GET` | `/api/tasks` | Retrieve all tasks |
| `GET` | `/api/tasks/{id}` | Retrieve a task by ID |
| `PUT` | `/api/tasks/{id}` | Update an existing task |
| `PATCH` | `/api/tasks/{id}/toggle` | Toggle task completion status |
| `GET` | `/api/tasks/priority/{priority}` | Filter tasks by priority (`LOW`, `MEDIUM`, `HIGH`) |
| `GET` | `/api/tasks/status/{completed}` | Filter tasks by completion (`true` or `false`) |
| `DELETE` | `/api/tasks/{id}` | Delete a task by ID |

---

### Request & Response Examples

#### 1. Create a Task
**Request:**
```http
POST /api/tasks HTTP/1.1
Content-Type: application/json

{
  "title": "Complete Project Documentation",
  "description": "Write and publish comprehensive README and API docs",
  "priority": "HIGH"
}
```

**Response (`200 OK`):**
```json
{
  "id": 1,
  "title": "Complete Project Documentation",
  "description": "Write and publish comprehensive README and API docs",
  "completed": false,
  "priority": "HIGH"
}
```

#### 2. Get All Tasks
**Request:**
```http
GET /api/tasks HTTP/1.1
```

**Response (`200 OK`):**
```json
[
  {
    "id": 1,
    "title": "Complete Project Documentation",
    "description": "Write and publish comprehensive README and API docs",
    "completed": false,
    "priority": "HIGH"
  }
]
```

#### 3. Toggle Task Completion
**Request:**
```http
PATCH /api/tasks/1/toggle HTTP/1.1
```

**Response (`200 OK`):**
```json
{
  "id": 1,
  "title": "Complete Project Documentation",
  "description": "Write and publish comprehensive README and API docs",
  "completed": true,
  "priority": "HIGH"
}
```

#### 4. Filter by Priority
**Request:**
```http
GET /api/tasks/priority/HIGH HTTP/1.1
```

#### 5. Filter by Status
**Request:**
```http
GET /api/tasks/status/true HTTP/1.1
```

#### 6. Delete a Task
**Request:**
```http
DELETE /api/tasks/1 HTTP/1.1
```

**Response (`200 OK`)**

---

### Quick cURL Examples

```bash
# Create task
curl -X POST http://localhost:8080/api/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"Design Homepage","description":"Create wireframes","priority":"MEDIUM"}'

# Fetch all tasks
curl http://localhost:8080/api/tasks

# Toggle task 1
curl -X PATCH http://localhost:8080/api/tasks/1/toggle

# Delete task 1
curl -X DELETE http://localhost:8080/api/tasks/1
```

---

## 🗄️ Database

TaskFlow uses an in-memory **H2 Database**:
- Data persists in memory during application runtime and resets upon restart.
- To enable the H2 Web Console for live database inspection, ensure the following is configured in `src/main/resources/application.properties`:
  ```properties
  spring.h2.console.enabled=true
  spring.h2.console.path=/h2-console
  ```
- Accessible in the browser at: `http://localhost:8080/h2-console`

---

## 📦 Packaging & Production Deployment

To generate an executable JAR file:

```bash
# On Windows
.\mvnw.cmd clean package -DskipTests

# On Linux / macOS
./mvnw clean package -DskipTests
```

Run the generated JAR directly:

```bash
java -jar target/taskflow-0.0.1-SNAPSHOT.jar
```

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## 👤 Author

- **Tharunesh Kumar A** — [GitHub Profile](https://github.com/tharuneshkumar2509-afk)
