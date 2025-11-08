# 🚨 Global Error Handling (Basic Example)

To avoid controllers returning messy or inconsistent error messages, we use:

* `@ControllerAdvice` → catches exceptions globally
* `@ExceptionHandler` → formats how errors are returned

This ensures the **frontend always receives clean, predictable JSON**.

## 1. Create a Standard Error Response Format

```java
// exception/ErrorResponse.java
package com.example.demo.exception;

import java.time.LocalDateTime;

public class ErrorResponse {
    private LocalDateTime timestamp = LocalDateTime.now();
    private int status;
    private String message;

    public ErrorResponse(int status, String message) {
        this.status = status;
        this.message = message;
    }

    // Getters only (no setters needed)
}
```

## 2. Create the Global Exception Handler

```java
// exception/GlobalExceptionHandler.java
package com.example.demo.exception;

import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.MethodArgumentNotValidException;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;

@ControllerAdvice
public class GlobalExceptionHandler 
{

    // Handle validation errors
    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<ErrorResponse> handleValidationErrors(MethodArgumentNotValidException ex) {
        String errorMessage = ex.getBindingResult().getFieldError().getDefaultMessage();
        ErrorResponse error = new ErrorResponse(400, errorMessage);
        return ResponseEntity.status(HttpStatus.BAD_REQUEST).body(error);
    }

    // Handle all other exceptions
    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleGeneralErrors(Exception ex) {
        ErrorResponse error = new ErrorResponse(500, "Something went wrong on the server");
        return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body(error);
    }
}
```

---

## ✅ Result When Validation Fails

If a user sends invalid input to:

```
POST /users
```

Response will be:

```json
{
  "timestamp": "2025-11-08T12:31:05.123",
  "status": 400,
  "message": "Email format is invalid"
}
```

Consistent, clean, and easy for frontend developers. ✅

---

## 🔥 Bonus Idea (Optional for Students)

Create a **custom exception** for “not found” cases:

```java
// exception/ResourceNotFoundException.java
package com.example.demo.exception;

public class ResourceNotFoundException extends RuntimeException {
    public ResourceNotFoundException(String message) {
        super(message);
    }
}
```

And handle it here:

```java
@ExceptionHandler(ResourceNotFoundException.class)
public ResponseEntity<ErrorResponse> handleNotFound(ResourceNotFoundException ex) {
    ErrorResponse error = new ErrorResponse(404, ex.getMessage());
    return ResponseEntity.status(HttpStatus.NOT_FOUND).body(error);
}
```

---

## 🎯 Summary for Week 10

| Feature                | Purpose                                          |
|------------------------|--------------------------------------------------|
| DTOs                   | Separate API input/output from database entities |
| `@Valid`               | Automatically enforce data validation            |
| Validation annotations | Ensure data quality and security                 |
| `@ControllerAdvice`    | Centralize and standardize error responses       |
| `ResponseEntity`       | Return correct HTTP statuses with clean JSON     |

---


