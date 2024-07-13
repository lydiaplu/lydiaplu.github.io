---
title: Introduction to java.time
date: 2023-10-17 13:21:30
toc: true  
categories:  
- java  

---

# Introduction to `java.time`

`java.time` is a date and time API introduced in Java 8. It provides a more modern, clearer, and intuitive way to handle dates and times compared to the old `Date` and `Calendar` classes. The API is immutable, meaning once an object is created, its state cannot be changed, enhancing code readability and safety.

### Core Classes and Their Uses

1. **LocalDate**
   - **Purpose**: Represents a date without a time and without a time zone (e.g., 2023-11-19).
   - **Create Instance**: `LocalDate.now()` to get the current date; `LocalDate.of(2023, 11, 19)` to create a specific date.

2. **LocalTime**
   - **Purpose**: Represents a time without a date and without a time zone (e.g., 13:45:20).
   - **Create Instance**: `LocalTime.now()` to get the current time; `LocalTime.of(13, 45, 20)` to create a specific time.

3. **LocalDateTime**
   - **Purpose**: Represents a date and time without a time zone (e.g., 2023-11-19T13:45:20).
   - **Create Instance**: `LocalDateTime.now()` to get the current date and time; `LocalDateTime.of(2023, 11, 19, 13, 45, 20)` to create a specific date and time.

4. **ZonedDateTime**
   - **Purpose**: Represents a date and time with a time zone.
   - **Create Instance**: `ZonedDateTime.now()` to get the current date and time with time zone; `ZonedDateTime.of(localDateTime, zoneId)` to create a specific date and time with a time zone.

5. **Instant**
   - **Purpose**: Represents a timestamp, typically associated with UTC time.
   - **Create Instance**: `Instant.now()` to get the current timestamp.

6. **Duration and Period**
   - **Purpose**: Represent a span of time. `Duration` deals with time-based amounts (hours, minutes), while `Period` deals with date-based amounts (years, months, days).
   - **Create Instance**: `Duration.between(time1, time2)`; `Period.between(date1, date2)`.

### Common Operations

1. **Getting Current Date and Time**

   ```java
   LocalDate today = LocalDate.now(); // Get today's date
   LocalTime now = LocalTime.now(); // Get current time
   LocalDateTime currentDateTime = LocalDateTime.now(); // Get current date and time
   ZonedDateTime currentZonedDateTime = ZonedDateTime.now(); // Get current date and time with time zone
   ```

2. **Parsing and Formatting**

   ```java
   LocalDate date = LocalDate.parse("2023-11-19"); // Parse date string
   LocalTime time = LocalTime.parse("12:00");
   LocalDateTime dateTime = LocalDateTime.parse("2022-01-01T12:00");

   // Format date to string
   DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd");
   String formattedDate = date.format(formatter); // Output: 2023-11-19

   // Format date and time to string
   DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm");
   String formattedDateTime = dateTime.format(dateTimeFormatter); // Output: 2022-01-01 12:00
   ```

3. **Date and Time Arithmetic**

   ```java
   LocalDate today = LocalDate.now(); // Get current date
   LocalTime now = LocalTime.now(); // Get current time

   LocalDate tomorrow = today.plusDays(1); // Add one day
   LocalTime twoHoursLater = now.plusHours(2); // Add two hours

   LocalDate lastWeek = today.minusWeeks(1); // Subtract one week
   LocalTime twoHoursBefore = now.minusHours(2); // Subtract two hours
   ```

4. **Time Zone Conversion**

   ```java
   ZoneId newYorkZoneId = ZoneId.of("America/New_York");
   ZonedDateTime newYorkDateTime = currentDateTime.atZone(newYorkZoneId);
   ```

5. **Duration and Period Calculation**

   ```java
   LocalTime time1 = LocalTime.of(10, 0); // Start time
   LocalTime time2 = LocalTime.of(12, 0); // End time
   LocalDate date1 = LocalDate.of(2020, 1, 1); // Start date
   LocalDate date2 = LocalDate.of(2020, 12, 31); // End date

   // Calculate duration between two times
   Duration duration = Duration.between(time1, time2);
   // Calculate period between two dates
   Period period = Period.between(date1, date2);
   ```

6. **Special Date-Time Calculations**

   ```java
   boolean isLeapYear = LocalDate.now().isLeapYear(); // Check if current year is a leap year
   DayOfWeek dayOfWeek = LocalDate.now().getDayOfWeek(); // Get current day of the week
   int dayOfMonth = LocalDate.now().getDayOfMonth(); // Get current day of the month
   ```

### Important Notes

- Date-time objects are immutable, meaning any modification operation returns a new instance.
- All `java.time` objects are thread-safe.
- Use `DateTimeFormatter` for formatting and parsing date-time objects.
- Use `Instant` to represent specific moments, usually for timestamps.
- Use `Duration` and `Period` to calculate the difference between two date-time values.

### Summary

The `java.time` package provides a modern and comprehensive API for handling date and time in Java. Its immutable nature and thread safety make it a reliable choice for date-time manipulation in concurrent applications. By using classes like `LocalDate`, `LocalTime`, `LocalDateTime`, `ZonedDateTime`, `Instant`, `Duration`, and `Period`, developers can easily handle various date-time operations with improved code readability and safety.