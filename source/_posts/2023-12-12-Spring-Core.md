---
title: Spring Core
date: 2023-12-12 11:32:30
toc: true  
categories:  
- Spring Boot 3

---

#Spring Core

#### interface

```java
public interface Coach {
    String getDailyWorkout();
}
```



#### @Component

````java
@Component
//@Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)
public class BaseballCoach implements Coach {
    @Override
    public String getDailyWorkout() {
        return "Spend 30 minutes in batting practice";
    }
}

@Component
public class CricketCoach implements Coach {
    @Override
    public String getDailyWorkout() {
        return "Practice fast bowling for 15 minutes";
    }
}

@Component
public class TennisCoach implements Coach {
    @Override
    public String getDailyWorkout() {
        return "Practice your backhand volley";
    }
}
````



#### @Autowired

````java
@RestController
public class DemoController {
    // define a private field for the dependency
    private Coach myCoach;

    // define a constructor for dependency injection
    @Autowired
    public void setCoach(@Qualifier("baseballCoach") Coach theCoach) {
        myCoach = theCoach;
    }

    @GetMapping("/dailyworkout")
    public String getDailyWorkout() {
        return myCoach.getDailyWorkout();
    }
}
````



#### @Configuration and @Bean

````java
public class SwimCoach implements Coach {
    @Override
    public String getDailyWorkout() {
        return "Swim 1000 meters as a warm up";
    }
}


@Configuration
public class SportConfig {
    @Bean
    public Coach swimCoach(){
        return new SwimCoach();
    }
}
````