---
title: Common Data Validation Annotations in Spring MVC
date: 2023-12-18 08:55:31
toc: true  
categories:  
- Spring Boot 3

---

# Common Data Validation Annotations in Spring MVC

| Annotation                     | Description                                                  |
| ------------------------------ | ------------------------------------------------------------ |
| `@NotNull`                     | Validates that the annotated element is not null.            |
| `@NotEmpty`                    | Validates that the annotated element is not empty (not null and size > 0). |
| `@NotBlank`                    | Validates that the annotated string is not empty and contains at least one non-whitespace character. |
| `@Min(value)`                  | Validates that the annotated element's value is greater than or equal to the specified minimum value. |
| `@Max(value)`                  | Validates that the annotated element's value is less than or equal to the specified maximum value. |
| `@Size(min=, max=)`            | Validates that the annotated element's size is within the specified range (for strings, this is length; for collections, this is size). |
| `@Email`                       | Validates that the annotated element is a valid email address. |
| `@Positive`                    | Validates that the annotated element's value is a positive number (greater than 0). |
| `@PositiveOrZero`              | Validates that the annotated element's value is a non-negative number (greater than or equal to 0). |
| `@Negative`                    | Validates that the annotated element's value is a negative number (less than 0). |
| `@NegativeOrZero`              | Validates that the annotated element's value is a non-positive number (less than or equal to 0). |
| `@Pattern(regexp)`             | Validates that the annotated element's value matches the specified regular expression. |
| `@Digits(integer=, fraction=)` | Validates that the annotated element's value has the specified number of integer and fractional digits. |
| `@AssertTrue`                  | Validates that the annotated element's value is true.        |
| `@AssertFalse`                 | Validates that the annotated element's value is false.       |
| `@Past`                        | Validates that the annotated element's value is a date in the past. |
| `@PastOrPresent`               | Validates that the annotated element's value is a date in the past or present. |
| `@Future`                      | Validates that the annotated element's value is a date in the future. |
| `@FutureOrPresent`             | Validates that the annotated element's value is a date in the present or future. |

### Example Usage

Here's an example of how you can use these annotations in a model class:

```java
import javax.validation.constraints.*;

public class User {

    @NotNull(message = "Name is required")
    private String name;

    @NotEmpty(message = "Email is required")
    @Email(message = "Email should be valid")
    private String email;

    @NotNull(message = "Age is required")
    @Min(value = 18, message = "Age should be at least 18")
    @Max(value = 65, message = "Age should be at most 65")
    private Integer age;

    @Pattern(regexp = "^[a-zA-Z0-9]{5}", message = "Postal code should be 5 characters/digits")
    private String postalCode;

    @Positive(message = "Account balance must be positive")
    private Double accountBalance;

    // Getters and setters
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    public String getPostalCode() {
        return postalCode;
    }

    public void setPostalCode(String postalCode) {
        this.postalCode = postalCode;
    }

    public Double getAccountBalance() {
        return accountBalance;
    }

    public void setAccountBalance(Double accountBalance) {
        this.accountBalance = accountBalance;
    }
}
```

In a Spring MVC controller, you can use the `@Valid` annotation to trigger validation and handle the results with a `BindingResult` object:

```java
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.*;
import org.springframework.ui.Model;
import org.springframework.validation.BindingResult;

import javax.validation.Valid;

@Controller
@RequestMapping("/user")
public class UserController {

    @GetMapping("/register")
    public String showRegistrationForm(Model model) {
        model.addAttribute("user", new User());
        return "user-register";
    }

    @PostMapping("/register")
    public String registerUser(@Valid @ModelAttribute("user") User user, BindingResult bindingResult) {
        if (bindingResult.hasErrors()) {
            return "user-register";
        }
        // Save user and redirect to success page
        return "redirect:/user/success";
    }

    @GetMapping("/success")
    public String showSuccessPage() {
        return "registration-success";
    }
}
```

By using these annotations and validation mechanisms, you can ensure that your application's data meets the necessary constraints and handle invalid input gracefully.