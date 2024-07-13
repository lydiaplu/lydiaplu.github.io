---
title: Spring MVC Data Validation
date: 2023-12-18 06:10:05
toc: true  
categories:  
- Spring Boot 3
---

# Spring MVC Data Validation

In Spring MVC, data validation is an essential feature to ensure that user input or submitted data adheres to predefined rules. Spring MVC integrates seamlessly with the Java Bean Validation (JSR 303 and JSR 349) API, providing a straightforward way to validate model data.

### 1. Add Dependencies

Add the Spring Boot Validation dependency in your `pom.xml` file if you are using Maven:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

### 2. Create the Model Class

Define fields in your model class (e.g., a form-backing object) and annotate them with appropriate Bean Validation annotations.

```java
import javax.validation.constraints.*;

public class Customer {
    private String firstName;

    @NotNull(message = "is required")
    @Size(min = 1, message = "is required")
    private String lastName = "";

    @NotNull(message = "is required")
    @Min(value = 0, message = "must be greater than or equal to zero")
    @Max(value = 10, message = "must be less than or equal to 10")
    private Integer freePasses;

    @Pattern(regexp = "^[a-zA-Z0-9]{5}", message = "only 5 chars/digits")
    private String postalCode;

    // Getters and setters
    public String getFirstName() {
        return firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

    public Integer getFreePasses() {
        return freePasses;
    }

    public void setFreePasses(Integer freePasses) {
        this.freePasses = freePasses;
    }

    public String getPostalCode() {
        return postalCode;
    }

    public void setPostalCode(String postalCode) {
        this.postalCode = postalCode;
    }
}
```

### 3. Validation in the Controller

Use the `@Valid` annotation to trigger validation logic and the `BindingResult` object to check validation results in your Spring MVC controller.

```java
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.*;
import org.springframework.ui.Model;
import org.springframework.validation.BindingResult;
import org.springframework.web.bind.WebDataBinder;
import org.springframework.beans.propertyeditors.StringTrimmerEditor;

import javax.validation.Valid;

@Controller
@RequestMapping("/customer")
public class CustomerController {

    // @InitBinder: Customizes the data binding process for web requests
    @InitBinder
    public void initBinder(WebDataBinder dataBinder) {
        // StringTrimmerEditor: Automatically trims white spaces for String fields
        StringTrimmerEditor stringTrimmerEditor = new StringTrimmerEditor(true);
        dataBinder.registerCustomEditor(String.class, stringTrimmerEditor);
    }

    @GetMapping("/showForm")
    public String showForm(Model model) {
        model.addAttribute("customer", new Customer());
        return "customer-form";
    }

    @PostMapping("/processForm")
    public String processForm(
            @Valid @ModelAttribute("customer") Customer theCustomer,
            BindingResult theBindingResult) {

        if (theBindingResult.hasErrors()) {
            // Handle errors
            return "customer-form";
        }

        // Normal business logic
        return "customer-confirmation";
    }
}
```

### 4. Frontend Form

Create a simple HTML form to submit customer information.

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Customer Form</title>
</head>
<body>
<h2>Customer Form</h2>
<form action="#" th:action="@{/customer/processForm}" th:object="${customer}" method="post">
    <label>First Name:</label>
    <input type="text" th:field="*{firstName}" />
    <br/><br/>

    <label>Last Name:</label>
    <input type="text" th:field="*{lastName}" />
    <div th:if="${#fields.hasErrors('lastName')}" th:errors="*{lastName}">Last Name Error</div>
    <br/><br/>

    <label>Free Passes:</label>
    <input type="text" th:field="*{freePasses}" />
    <div th:if="${#fields.hasErrors('freePasses')}" th:errors="*{freePasses}">Free Passes Error</div>
    <br/><br/>

    <label>Postal Code:</label>
    <input type="text" th:field="*{postalCode}" />
    <div th:if="${#fields.hasErrors('postalCode')}" th:errors="*{postalCode}">Postal Code Error</div>
    <br/><br/>

    <input type="submit" value="Submit" />
</form>
</body>
</html>
```

### Summary

1. **Add Dependencies**: Ensure the project includes the Spring Boot Validation dependency.
2. **Define Model Class**: Use Bean Validation annotations to define validation rules in the model class.
3. **Controller Validation**: Use the `@Valid` annotation and `BindingResult` object to perform and check validation in the controller.
4. **Frontend Form**: Create an HTML form to submit data and display validation error messages.

By following these steps, you can implement data validation in Spring MVC to ensure that input data meets predefined rules and constraints.