# Week 10: Validation, DTOs & Error Handling

This week focuses on improving the **quality**, **security**, and **cleanliness** of our Spring Boot APIs by introducing:

- **Bean Validation** (using annotations like `@NotNull`, `@Size`, etc.)
- **DTOs (Data Transfer Objects)** to separate API input/output from database entities
- **Global exception handling** using `@ControllerAdvice`
- **ResponseEntity** and proper use of **HTTP status codes**

The goal is to write **professional**, **maintainable**, and **user-friendly** APIs.

---

## 📚 Learning Objectives

By the end of this week, students will be able to:

- Apply **validation** rules to incoming request data
- Explain the purpose of **DTOs** and convert between Entities ⇄ DTOs
- Implement **custom exception handling** using `@ControllerAdvice`
- Return appropriate **HTTP response codes** using `ResponseEntity`
- Provide clear and consistent **error responses** for the frontend

---

## 🧠 Key Concepts

### 1. Bean Validation

Spring Boot integrates with **Jakarta Bean Validation** to validate user input.

Examples of common annotations:

| Annotation        | Purpose                                    |
|-------------------|--------------------------------------------|
| `@NotNull`        | Field must not be null                     |
| `@NotBlank`       | String must not be empty or blank          |
| `@Size(min, max)` | String/Collection must have defined length |
| `@Min` / `@Max`   | Numeric constraints                        |
| `@Email`          | Must be a valid email format               |

Validation is usually applied in DTOs and enforced using `@Valid` in Controller methods.

---

### 2. DTOs (Data Transfer Objects)

DTOs are simple data classes used to handle **input/output** in API requests.

Why use DTOs?

* Protects database entities from being exposed directly
* Prevents users from modifying fields like `id` or timestamps
* Allows different shapes of data for **create**, **update**, and **response**

Common pattern:

```txt
Entity (database model)  ←→  DTO (API structure)
```

---

### 3. ResponseEntity & HTTP Status Codes

`ResponseEntity` lets us **control the HTTP response**:

```java
return ResponseEntity.status(HttpStatus.CREATED).body(data);
```

Examples of commonly used status codes:

| Code | Meaning               | Usage Example             |
|------|-----------------------|---------------------------|
| 200  | OK                    | Successful request        |
| 201  | Created               | New resource created      |
| 400  | Bad Request           | Validation failed         |
| 404  | Not Found             | Resource doesn’t exist    |
| 500  | Internal Server Error | Unexpected server failure |

---

### 4. Global Exception Handling with @ControllerAdvice

Instead of returning messy error messages, we create a **centralized error handler**.

Benefits:

* Clean controller logic
* Consistent error response format
* Easier debugging and front-end integration

---

## 🧰 Tools & Libraries

| Tool / Library                     | Purpose                               |
|------------------------------------|---------------------------------------|
| `jakarta.validation`               | Validation annotations and processing |
| ModelMapper / MapStruct (optional) | Automate conversion Entity ↔ DTO      |
| Postman                            | Test API errors and success cases     |

---

## 🏗️ Example Project Structure

```txt
spring-boot-advanced-api/
├── controller/           → REST controllers
├── service/              → Business logic
├── repository/           → Database layer
├── model/                → JPA entities
├── dto/                  → Data Transfer Objects
│   ├── request/          → Input DTOs
│   └── response/         → Output DTOs
├── mapper/               → MapStruct mappers
├── exception/            → Custom exceptions + Global handler
└── resources/
    └── application.properties
```
---

## ✅ Expected Outcome by End of Week

Students will be able to:

* Ensure API input is **safe**, **valid**, and **user-friendly**
* Return consistent JSON responses for errors
* Use DTOs to **decouple database design from API design**
* Write cleaner, more maintainable Spring Boot applications

---
