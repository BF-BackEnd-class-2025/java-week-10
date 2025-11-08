# 🔟 **Project Ideas**

## ✅ **Dependencies (same for all projects)**

Add these in `pom.xml`:

```xml
<dependencies>
    <!-- Spring Web -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <!-- Spring Data JPA -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>

    <!-- Validation (important for Week 10) -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-validation</artifactId>
    </dependency>

    <!-- PostgreSQL Driver (or use H2 for simplicity) -->
    <dependency>
        <groupId>org.postgresql</groupId>
        <artifactId>postgresql</artifactId>
        <scope>runtime</scope>
    </dependency>

    <!-- Lombok (optional but useful for DTOs) -->
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <optional>true</optional>
    </dependency>
</dependencies>
```

---

## 🏗 Project Structure (same for all)

```txt
spring-boot-validation-demo/
├── controller/
│   └── (handles requests using DTOs)
├── service/
│   └── (business logic)
├── repository/
│   └── (DB access)
├── dto/
│   ├── (request DTOs → validated inputs)
│   └── (response DTOs → formatted outputs)
├── model/
│   └── (JPA Entities)
├── exception/
│   ├── GlobalExceptionHandler.java
│   └── CustomExceptions.java
└── resources/
    └── application.properties
```

---



## 1. **User Registration API**

Users sign up with name, email, and age.

* Validate email format, name length, and age >= 18.
* Throw custom exception if email already exists.

Entity: `User`
RequestDTO: `CreateUserDTO`
ResponseDTO: `UserDTO`

---

## 2. **Product Catalog Service**

CRUD for products.

* Validate price > 0, name not blank.
* Custom error if product is not found.

Entity: `Product`
DTOs: `ProductCreateDTO`, `ProductResponseDTO`

---

## 3. **Book Library System**

Create and list books.

* Validate ISBN length = 13.
* Author name cannot be blank.

Entity: `Book`
DTOs: `BookRequestDTO`, `BookResponseDTO`

---

## 4. **Student Enrollment API**

Add & fetch students.

* Validate email format, age >= 16.
* Throw custom exception if student email already used.

Entity: `Student`
DTOs: `StudentInputDTO`, `StudentViewDTO`

---

## 5. **Task Management API**

Users create and track tasks.

* Validate title min length 3.
* Optional due date, but if present → must be in the future.

Entity: `Task`
DTOs: `CreateTaskDTO`, `TaskDTO`

---

## 6. **Event Registration Service**

Users register for events.

* Validate event date is in the future.
* Limit attendees ≤ maxSeats.

Entities: `Event`, `Attendee`
DTOs: `EventDTO`, `RegisterAttendeeDTO`

---

## 7. **Contact Manager API**

Store contact info.

* Validate phone number format using regex.
* Email unique constraint.

Entity: `Contact`
DTOs: `ContactCreateDTO`, `ContactResponseDTO`

---

## 8. **Order & Checkout API**

Users place orders for products.

* Validate quantity >= 1.
* Throw custom exceptions for invalid product IDs.

Entities: `Order`, `OrderItem`
DTOs: `CreateOrderDTO`, `OrderSummaryDTO`

---

## 9. **Car Rental Service**

Add cars and rent them.

* Validate license plate format.
* Custom exception: "CarNotAvailableException".

Entities: `Car`, `Rental`
DTOs: `CarCreateDTO`, `RentalRequestDTO`, `RentalResponseDTO`

---

## 10. **Feedback / Review Service**

Users submit reviews for items.

* Rating must be between 1 and 5.
* Comment optional but max length 250 chars.

Entity: `Review`
DTOs: `ReviewRequestDTO`, `ReviewResponseDTO`

---

## 🎓 What Students Practice in Every Project

| Concept                                    | How It's Used                                            |
|--------------------------------------------|----------------------------------------------------------|
| DTOs                                       | Clean separation between input/output and database layer |
| Validation (`@NotBlank`, `@Email`, `@Min`) | Ensures request data is correct                          |
| `@Valid` in Controllers                    | Activate validation logic                                |
| `ResponseEntity`                           | Return appropriate HTTP status codes                     |
| `@ControllerAdvice`                        | Centralized error formatting                             |
| Custom Exceptions                          | Better readability and debugging                         |

---
Happy Coding! 🚀


