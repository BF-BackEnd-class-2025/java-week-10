# 🧱 Week 10 – Advanced Spring Boot API Projects

This week focuses on building **complete REST APIs** using Spring Boot, JPA, DTOs, validation, and exception handling.
Students will follow industry-level patterns and build practical, portfolio-ready projects.

---

## 🧩 Maven Dependencies (common to all projects)

Add these to your `pom.xml`:

```xml
<dependencies>
    <!-- Spring Boot Web -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <!-- Spring Data JPA -->
    <dependency>
        <groupId>org.springframework.boot</Id>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>

    <!-- Validation (DTOs & Inputs) -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-validation</artifactId>
    </dependency>

    <!-- PostgreSQL (or use H2 for testing) -->
    <dependency>
        <groupId>org.postgresql</groupId>
        <artifactId>postgresql</artifactId>
        <scope>runtime</scope>
    </dependency>
</dependencies>
```

---

## 📁 Project Folder Structure

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

## 1️⃣ **User Profile Manager**

Manage basic user profiles.

**Features:**

- Create user profile
- Validate: name not blank, email valid
- Unique email check
- DTO → Validation → Mapper → Entity
- Custom exception: `EmailAlreadyExistsException`

**Entity:** `User`
**DTOs:** `CreateUserDTO`, `UserResponseDTO`

---

## 2️⃣ **Product Catalog**

Manage products with proper validation.

**Features:**

- Price > 0
- Name not blank
- Throw `ProductNotFoundException`
- Return `201 CREATED` when adding new item

**Entity:** `Product`
**DTOs:** `ProductCreateDTO`, `ProductResponseDTO`

---

## 3️⃣ **Book Manager API**

CRUD operations on books.

**Rules:**

- Title required
- ISBN length must be exactly 13
- Handle invalid input with validation
- Custom error if book not found

**Entity:** `Book`
**DTOs:** `BookCreateDTO`, `BookResponseDTO`

---

## 4️⃣ **Student Record System**

Simple student management system.

**Validation:**

- Name not blank
- Email valid
- Age >= 16

**Entity:** `Student`
**DTOs:** `StudentInputDTO`, `StudentOutputDTO`

---

## 5️⃣ **Task Management API**

Manage tasks with due dates.

**Rules:**

- Title ≥ 3 characters
- Due date in the future
- Custom exception for invalid date or missing task

**Entity:** `Task`
**DTOs:** `TaskCreateDTO`, `TaskResponseDTO`

---

## 6️⃣ **Event Scheduling System**

Manage events & attendees (no authentication).

**Rules:**

- Event date must be in the future
- Capacity >= 1
- Prevent exceeding capacity via validation

**Entities:** `Event`
**DTOs:** `EventCreateDTO`, `EventResponseDTO`

---

## 7️⃣ **Contact Manager**

Store and update contacts.

**Rules:**

- Phone must match regex pattern
- Email must be valid
- Name must not be blank
- Custom exception for duplicate contacts

**Entity:** `Contact`
**DTOs:** `ContactCreateDTO`, `ContactResponseDTO`

---

## 8️⃣ **Order Processing API**

(No checkout, no payment, just local CRUD)

**Rules:**

- Quantity >= 1
- Order must contain at least one item
- Validate product IDs
- Throw custom exception when product not found

**Entities:** `Order`, `OrderItem`, `Product`
**DTOs:** `OrderRequestDTO`, `OrderResponseDTO`

---

## 9️⃣ **Car Rental**

Simple system to manage car availability.

**Rules:**

- License plate format validation
- Cannot rent a car already rented
- Custom: `CarNotAvailableException`
- Status: AVAILABLE / RENTED

**Entities:** `Car`, `Rental`
**DTOs:** `CarDTO`, `RentalRequestDTO`, `RentalResponseDTO`

---

## 🔟 **Product Reviews API**

Users leave reviews (no login).

**Rules:**

- Rating from 1 to 5
- Comment length ≤ 250
- Product ID must exist
- Return `404` when product missing

**Entity:** `Review`
**DTOs:** `ReviewRequestDTO`, `ReviewResponseDTO`

---

## 🆕 BONUS

These involve DTOs, services, mapping, and external data.

---

## 🔟➕1 **Country Importer API (External API → DB)**

Fetch countries from REST Countries API:

`https://restcountries.com/v3.1/name/{name}`

**Flow:**

- GET external data
- Map JSON → DTO → Entity
- Save to DB
- Show stored countries

**Skills:**
External API, DTO Mapping, Exception Handling

---

## 🔟➕2 **Crypto Market Snapshot API**

Fetch real crypto prices from CoinGecko API.
`https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=10&page=1`

**Rules:**

- Fetch top 10
- Save to DB
- Prevent duplicate entries
- Use DTOs to transform external JSON

**Great for:**
Mapping → DTO → Validation → Saving to DB.

---

## 🎯 What These Projects Teach Perfectly for Week 10

| Concept              | Appears In Every Project                    |
| -------------------- | ------------------------------------------- |
| DTOs                 | Request & Response DTOs                     |
| Validation           | `@NotBlank`, `@Min`, `@Email`, etc.         |
| `@Valid`             | On controller methods                       |
| Exception Handling   | `@ControllerAdvice`                         |
| Custom Exceptions    | Not-found, duplicate, capacity, date errors |
| ResponseEntity       | Return correct HTTP codes                   |
| Services             | Clean business logic                        |
| Repositories         | CRUD using JPA                              |
| Mappers              | MapStruct or manual mapping                 |
| Layered Architecture | Controller → Service → Repo                 |

---
