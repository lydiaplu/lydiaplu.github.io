---
title: Regular Expressions
date: 2021-12-20 14:20:53
toc: true
categories:
- javascript

---

Content: Regular Expressions
<!--more-->

### Metacharacters

| Metacharacter | Description                                                  |
| ------------- | ------------------------------------------------------------ |
| .             | Matches any single character except newline and line terminator |
| \d            | Matches any digit                                            |
| \D            | Matches any non-digit                                        |
| \s            | Matches any whitespace character                             |
| \S            | Matches any non-whitespace character                         |
| \w            | Matches any word character (alphanumeric plus underscore)    |
| \W            | Matches any non-word character                               |
| \b            | Matches a word boundary                                      |
| \B            | Matches a non-word boundary                                  |



### Quantifiers

| Quantifier | Description                                                  |
| ---------- | ------------------------------------------------------------ |
| +          | Matches 1 or more occurrences                                |
| *          | Matches 0 or more occurrences                                |
| ?          | Matches 0 or 1 occurrence, can denote laziness to prevent greedy matches |
| {n}        | Matches exactly n occurrences                                |
| {n,m}      | Matches between n and m occurrences                          |
| {n,}       | Matches at least n occurrences                               |
| ^n         | Matches any string with n at the beginning                   |
| [^abc]     | When inside square brackets, denotes negation                |
| n$         | Matches any string with n at the end                         |



### Modifiers

| Modifier | Description                                                  |
| -------- | ------------------------------------------------------------ |
| i        | Case insensitive matching (/n/i matches n regardless of case) |
| g        | Global search (/n/g searches for all occurrences of n)       |
| m        | Multiline matching                                           |



### Square Brackets

| Expression         | Description                                   |
| ------------------ | --------------------------------------------- |
| [abc]              | Matches any character inside the brackets     |
| [^abc]             | Matches any character not inside the brackets |
| [0-9]              | Matches any digit from 0 to 9                 |
| [a-z]              | Matches any lowercase letter from a to z      |
| [A-Z]              | Matches any uppercase letter from A to Z      |
| [A-z]              | Matches any letter from A to z                |
| [red\|blue\|green] | Matches any of the specified alternatives     |



### Ways to Create a Regular Expression

There are two ways to create a regular expression: using a literal or using a constructor.

```javascript
var reg = new RegExp("\\d");
var reg = /\d/;
```



### Regular Expression API

**1. RegExp Methods**

| Method | Description                                                  |
| ------ | ------------------------------------------------------------ |
| test   | Searches for a specified value in a string, returns true or false |
| exec   | Searches for a specified value in a string, returns the found value and its position |

**2. String Methods**

| Method  | Description                                                  |
| ------- | ------------------------------------------------------------ |
| search  | Searches for a match against a regular expression            |
| match   | Finds one or more matches of a regular expression            |
| replace | Replaces matches with a regular expression                   |
| split   | Splits a string into an array by matching against a regular expression |

Additional Notes:

- Regular expressions are powerful tools for text processing and can greatly simplify tasks such as validation, parsing, and string manipulation.
- When using regular expressions, especially with user input, it's important to consider performance and security implications such as catastrophic backtracking and injection attacks.
- It's a good practice to comment complex regular expressions to explain their purpose and pattern, making maintenance easier for others or for future review.
- Tools like regex testers and visualizers can be immensely helpful when creating or debugging regular expressions.