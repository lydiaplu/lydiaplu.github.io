---
title: Custom Validation Annotations in Spring
date: 2023-12-18 10:37:08
toc: true  
categories:  
- Spring Boot 3
---

# Custom Validation Annotations in Spring

### 1. Define the Custom Validation AnnotationCustom Validation Annotations in Spring

First, you need to define a custom annotation. This annotation should be marked with `@Constraint` and specify a class that implements the `ConstraintValidator` interface as its validator.

```java
import javax.validation.Constraint;
import javax.validation.Payload;
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Constraint(validatedBy = CourseCodeConstraintValidator.class)
@Target({ElementType.METHOD, ElementType.FIELD})
@Retention(RetentionPolicy.RUNTIME)
public @interface CourseCode {
    public String value() default "LUV";
    public String message() default "must start with LUV";
    public Class<?>[] groups() default {};
    public Class<? extends Payload>[] payload() default {};
}
```

- `@Constraint(validatedBy = CourseCodeConstraintValidator.class)`: Specifies that `CourseCode` is a constraint annotation and its validation logic is implemented by `CourseCodeConstraintValidator`.
- `@Target({ElementType.METHOD, ElementType.FIELD})`: Indicates that the annotation can be applied to methods and fields.
- `@Retention(RetentionPolicy.RUNTIME)`: Ensures that the annotation is available at runtime.
- `public Class<?>[] groups() default {};`: Used to specify validation groups.
- `public Class<? extends Payload>[] payload() default {};`: Used to provide custom payload objects for the validation.

### 2. Create the Custom Validator

Next, create a class that implements the `ConstraintValidator` interface. This class contains the actual validation logic.

```java
import javax.validation.ConstraintValidator;
import javax.validation.ConstraintValidatorContext;

public class CourseCodeConstraintValidator implements ConstraintValidator<CourseCode, String> {
    private String coursePrefix;

    @Override
    public void initialize(CourseCode theCourseCode) {
        coursePrefix = theCourseCode.value();  // Read the value attribute from the annotation
    }

    @Override
    public boolean isValid(String theCode, ConstraintValidatorContext constraintValidatorContext) {
        if (theCode != null) {
            return theCode.startsWith(coursePrefix);
        } else {
            return true;  // Assume null values are valid
        }
    }
}
```

- `CourseCodeConstraintValidator` implements `ConstraintValidator<CourseCode, String>`.
- `initialize` method is used to read the `value` attribute from the annotation.
- `isValid` method contains the validation logic.

### 3. Apply the Custom Annotation

Apply the custom annotation to the fields that need to be validated.

```java
import javax.validation.constraints.NotNull;

public class Customer {

    @CourseCode(value="TOPS", message="must start with TOPS")
    private String courseCode;

    @NotNull(message = "is required")
    private String firstName;

    // Getters and setters
    public String getCourseCode() {
        return courseCode;
    }

    public void setCourseCode(String courseCode) {
        this.courseCode = courseCode;
    }

    public String getFirstName() {
        return firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }
}
```

### 4. Integrate with Spring MVC

In the Spring MVC controller, use the `@Valid` annotation to trigger the validation process.

```java
import org.springframework.stereotype.Controller;
import org.springframework.validation.BindingResult;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.PostMapping;

import javax.validation.Valid;

@Controller
public class CustomerController {

    @PostMapping("/processForm")
    public String processForm(@Valid @ModelAttribute("customer") Customer theCustomer, BindingResult theBindingResult) {
        if (theBindingResult.hasErrors()) {
            // Handle validation errors
            return "customer-form";
        }
        // Proceed with normal business logic
        return "customer-confirmation";
    }
}
```

- `@Valid`: Enables automatic validation of the `Customer` object.
- `@ModelAttribute("customer") Customer theCustomer`: Binds form data to the `Customer` object and validates it.
- `BindingResult theBindingResult`: Captures the validation errors.

By following these steps, you can create and use custom validation annotations in a Spring application to ensure that your data meets specific validation criteria.