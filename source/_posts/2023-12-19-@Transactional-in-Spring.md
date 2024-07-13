---
title: @Transactional in Spring
date: 2023-12-19 13:28:33
toc: true  
categories:  
- Spring Boot 3

---

# @Transactional in Spring

In Java, the `@Transactional` annotation is part of the Spring framework and is used to manage transaction boundaries. A transaction is a series of operations that should either all succeed or all fail, ensuring data consistency and integrity in database operations.

### Key Features

When you use the `@Transactional` annotation on a method, Spring manages the transaction for that method. This means:

1. **Transaction Start**: A new transaction is started when the method begins execution.
2. **Transaction Commit**: If the method completes successfully, the transaction is committed, and all changes are permanently saved.
3. **Transaction Rollback**: If an exception occurs during execution, the transaction is rolled back, meaning all changes are undone.

### Usage Example

```java
@Service
public class AccountService {

    @Autowired
    private AccountDao accountDao;

    @Transactional
    public void transferMoney(int amount, String fromAccountId, String toAccountId) {
        accountDao.withdraw(amount, fromAccountId);
        accountDao.deposit(amount, toAccountId);
    }
}
```

In this example, both `withdraw` and `deposit` operations must succeed to ensure that the funds are correctly transferred from one account to another. If an exception occurs between these operations, the transaction will be rolled back, and no money will be deducted from either account.

### Advanced Features

The `@Transactional` annotation provides several parameters to further control the behavior of transactions:

- **propagation**: Defines how the transaction should propagate, such as whether it should run within an existing transaction or start a new one.
- **isolation**: Defines the isolation level for the transaction, affecting the extent to which this transaction is isolated from others in terms of visibility of data changes.
- **readOnly**: Indicates whether the transaction is read-only, optimizing performance for read-only transactions.
- **timeout**: Specifies the maximum time that the transaction can run before it is rolled back automatically.
- **rollbackFor** and **noRollbackFor**: Specify which exceptions should trigger a transaction rollback and which should not.

### Example with Advanced Features

```java
@Transactional(propagation = Propagation.REQUIRED, isolation = Isolation.DEFAULT, timeout = 30, rollbackFor = {Exception.class})
public void transferMoney(int amount, String fromAccountId, String toAccountId) {
    accountDao.withdraw(amount, fromAccountId);
    accountDao.deposit(amount, toAccountId);
}
```

In this example:

- **propagation = Propagation.REQUIRED**: The method should run within an existing transaction if available; otherwise, it should start a new one.
- **isolation = Isolation.DEFAULT**: Uses the default isolation level of the underlying datastore.
- **timeout = 30**: The transaction should be rolled back if it takes longer than 30 seconds to complete.
- **rollbackFor = {Exception.class}**: The transaction should be rolled back for any exception that is thrown.

### Isolation Levels

- **Isolation.DEFAULT**: Use the default isolation level of the underlying datastore.
- **Isolation.READ_UNCOMMITTED**: A transaction may read data that is not yet committed by other transactions.
- **Isolation.READ_COMMITTED**: A transaction cannot read data that is not yet committed by other transactions.
- **Isolation.REPEATABLE_READ**: A transaction cannot read data that is not yet committed by other transactions and ensures that if it reads the same row twice, it will get the same data both times.
- **Isolation.SERIALIZABLE**: The highest isolation level, which ensures that transactions are completely isolated from one another, preventing dirty reads, non-repeatable reads, and phantom reads.

### Propagation Types

- **Propagation.REQUIRED**: Support a current transaction; create a new one if none exists.
- **Propagation.REQUIRES_NEW**: Create a new transaction, and suspend the current transaction if one exists.
- **Propagation.MANDATORY**: Support a current transaction; throw an exception if no current transaction exists.
- **Propagation.NEVER**: Execute non-transactionally; throw an exception if a transaction exists.
- **Propagation.SUPPORTS**: Support a current transaction; execute non-transactionally if none exists.
- **Propagation.NOT_SUPPORTED**: Execute non-transactionally, suspending the current transaction if one exists.
- **Propagation.NESTED**: Execute within a nested transaction if a current transaction exists.

Using `@Transactional` effectively helps to manage the complexity of transaction management in a clean and declarative manner, improving the maintainability and reliability of your application.