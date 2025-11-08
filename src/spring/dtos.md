# 🧩 DTO Example (with Validation)

## 1. **Entity Class** (Database Model)

```java
// model/User.java
package com.example.demo.model;

import jakarta.persistence.*;

@Entity
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String fullName;

    private String email;

    private int age;

    // Getters & Setters
}
```

## 2. **DTO Class** (Used for Request & Validation)

```java
// dto/UserRequestDTO.java
package com.example.demo.dto;

import jakarta.validation.constraints.*;

public class UserRequestDTO {

    @NotBlank(message = "Full name cannot be empty")
    private String fullName;

    @Email(message = "Email format is invalid")
    @NotBlank(message = "Email is required")
    private String email;

    @Min(value = 18, message = "Age must be at least 18")
    private int age;

    // Getters & Setters
}
```

## 3. **DTO for Response** (Optional — controls what we send back)

```java
// dto/UserResponseDTO.java
package com.example.demo.dto;

public class UserResponseDTO {

    private Long id;
    private String fullName;
    private String email;

    public UserResponseDTO(Long id, String fullName, String email) {
        this.id = id;
        this.fullName = fullName;
        this.email = email;
    }

    // Getters (no setters needed usually)
}
```

## 4. **Controller Using @Valid & Converting DTO → Entity**

```java
// controller/UserController.java
package com.example.demo.controller;

import com.example.demo.dto.UserRequestDTO;
import com.example.demo.dto.UserResponseDTO;
import com.example.demo.model.User;
import com.example.demo.service.UserService;

import jakarta.validation.Valid;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/users")
public class UserController {

    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    @PostMapping
    public ResponseEntity<UserResponseDTO> createUser(@Valid @RequestBody UserRequestDTO dto) {

        User savedUser = userService.createUser(dto);
        UserResponseDTO response = new UserResponseDTO(
                savedUser.getId(),
                savedUser.getFullName(),
                savedUser.getEmail()
        );

        return ResponseEntity.status(201).body(response);
    }
}
```

## 5. **Service Converting DTO to Entity**

```java
// service/UserService.java
package com.example.demo.service;

import com.example.demo.dto.UserRequestDTO;
import com.example.demo.model.User;
import com.example.demo.repository.UserRepository;

import org.springframework.stereotype.Service;

@Service
public class UserService {

    private final UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public User createUser(UserRequestDTO dto) {
        User user = new User();
        user.setFullName(dto.getFullName());
        user.setEmail(dto.getEmail());
        user.setAge(dto.getAge());
        return userRepository.save(user);
    }
}
```

---

## ✅ Key Takeaways

| Feature                | Why we use it                                       |
|------------------------|-----------------------------------------------------|
| DTOs                   | Prevent exposing internal Entity structure          |
| `@Valid`               | Automatically checks input before method logic runs |
| Validation Annotations | Guarantee clean, safe data                          |
| `ResponseEntity`       | Controls HTTP status + response format              |

---


